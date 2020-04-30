---
title: 應用程式部署至裝置集合技術參考
titleSuffix: Configuration Manager
description: 適用於 Configuration Manager 的應用程式部署至裝置集合技術參考疑難排解。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688786"
---
# <a name="application-deployment-for-device-collections"></a>裝置集合的應用程式部署

適用於：  Configuration Manager (最新分支)

將應用程式部署至裝置集合時，原則會以集合中的所有裝置為目標，不論部署目的為何。 本文說明用戶端上的原則下載和部署處理。

> [!TIP]
> 可以藉由執行[開始之前](app-deployment-technical-reference.md#before-you-begin)區段中參考的 SQL 查詢，取得檢閱用戶端記錄所需的所有資訊。

## <a name="policy-download"></a>原則下載

應用程式部署的原則以用戶端為目標之後，用戶端會在下一個原則輪詢週期下載原則。 當用戶端下載原則時，除了部署原則之外，還會下載相關的原則。 這些相關原則包括應用程式的原則、部署類型、全域條件等。您可以使用應用程式或指派唯一識別碼，在用戶端上的 **PolicyAgent** 中追蹤原則下載活動。

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

在用戶端上下載原則之後，排程器元件會建立部署啟用和強制執行的排程。

## <a name="deployment-activation"></a>部署啟用

啟用部署時，就會起始應用程式評估。 排程器元件會建立排程，以在部署中設定的「可用時間」啟動指派。 此活動可以使用應用程式指派唯一識別碼，在用戶端上的 **Scheduler.log** 中追蹤。

- 針對**必要**部署，系統會建立啟用排程，但是最多有兩小時的延遲，以避免網站伺服器和發佈點的資源爭用。 延遲可協助避免爭用，因為如果應用程式是根據定義的需求規則而適用，則應用程式內容可能會在評估期間下載。

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- 針對**可用**部署，系統會建立啟用排程，以在「部署」中設定的「可用時間」引發。

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

到達排程時間時，排程器元件會將啟用訊息傳送至 DCM 代理程式，以執行應用程式評估。

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM 代理程式會接收啟用訊息，並建立作業來評估應用程式。

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>部署強制執行

啟用強制執行時，就會起始應用程式安裝。

- 針對**必要**部署，排程器會在下載原則之後建立期限排程，以在部署期限強制執行應用程式。 根據預設，期限排程不是隨機的。 啟用的隨機行為可以由[停用期限隨機設定](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization)用戶端設定來控制。

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    在期限時，排程器元件會將期限訊息傳送至 DCM 代理程式。 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM 代理程式會接收期限訊息，並建立作業來強制執行應用程式。
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > 針對具有過去期限的部署，應用程式會立即由相同的 DCM 代理程式 (執行評估、下載和安裝動作) 啟用及強制執行。

- 針對**可用**部署，由於使用者從軟體中心起始應用程式安裝時會發生強制執行，所以沒有任何期限排程。 當使用者啟動安裝時，會建立 DCM 代理程式作業來執行應用程式評估、下載和安裝。 此活動可以在用戶端上的 **DCMAgent.log** 中追蹤。

## <a name="next-steps"></a>後續步驟

- [了解應用程式部署用戶端元件](client-components-technical-reference.md)
