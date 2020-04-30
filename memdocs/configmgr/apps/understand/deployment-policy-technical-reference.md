---
title: 應用程式部署原則技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 中應用程式部署原則進行疑難排解的技術參考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688826"
---
# <a name="application-deployment-policy"></a>應用程式部署原則

適用於：  Configuration Manager (最新分支)

## <a name="policy-creation"></a>原則建立

當您部署應用程式時，會建立 [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) 類別的執行個體，代表將應用程式指派給集合。 您可以在 **SMSProv.log** 追蹤此活動。

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

在 Configuration Manager 資料庫中，此資訊是儲存在 `CI_CIAssignments` 資料表中，其中 `AssignmentType` 2 表示應用程式部署。 當建立指派時，SMS 資料庫監視元件會偵測資料表中的變更，然後通知 Object Replication Manager 處理 CI Assignment (CIA) 原則。 然後，Object Replication Manager 元件會針對資料庫中的應用程式指派建立原則，儲存在資料庫的 `Policy` 資料表中，原則識別碼是根據應用程式唯一識別碼。 您可以藉由參考指派唯一識別碼，在 **objreplmgr.log** 中追蹤此活動，該識別碼可以從[開始之前](app-deployment-technical-reference.md#before-you-begin)區段中參考的 SQL 查詢取得。

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

您可以使用類似下面的 SQL 查詢，在資料庫中看到應用程式指派的原則。

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>原則目標

產生原則之後，原則提供者元件會將此原則指派給集合 (應用程式部署的目標) 中的資源。 原則目標資訊會儲存在資料庫的 `ResPolicyMap` 資料表中。 您可以使用上述查詢所傳回的 PADBID，在 **policypv.log** 中追蹤此活動。 不過，如果同時處理多個原則，記錄中記錄的 PADBID 不一定會符合上述查詢所傳回的 PADBID。

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap` 資料表不包含將應用程式部署為**可用**於使用者集合的任何目標資訊。 軟體中心會從管理點查詢這些應用程式的清單，當使用者從軟體中心要求應用程式時，會動態產生這些應用程式的原則目標資訊。

## <a name="next-steps"></a>後續步驟

- [裝置集合的應用程式部署](device-deployment-technical-reference.md)
- [使用者集合的應用程式部署](user-deployment-technical-reference.md)
