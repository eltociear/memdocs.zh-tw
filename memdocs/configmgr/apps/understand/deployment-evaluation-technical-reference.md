---
title: 應用程式評估技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 應用程式評估進行疑難排解的技術參考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688836"
---
# <a name="application-deployment-evaluation"></a>應用程式部署評估

適用於：  Configuration Manager (最新分支)

在繼續之前，請先參閱[應用程式部署用戶端元件](client-components-technical-reference.md)以了解 DCM 和 CI 代理程式作業處理。

應用程式評估是在啟用部署時，由 DCM 代理程式和 CI 代理程式元件執行。 若要了解何時啟用指派，請參閱[應用程式部署至裝置集合](device-deployment-technical-reference.md)或[應用程式部署至使用者集合](user-deployment-technical-reference.md)文章。

## <a name="application-detection-and-evaluation"></a>應用程式偵測和評估

應用程式評估是在 CI 代理程式作業的 **InvokingSdmMethod** 階段期間執行。 用戶端會在這個階段評估針對應用程式定義的偵測方法，以判斷應用程式是否已在裝置上安裝。 您可以使用部署類型唯一識別碼或部署類型名稱，在 **AppDiscovery.log** 中追蹤此活動。

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> 上述範例顯示 MSI 應用程式的偵測，其中偵測是藉由檢查 MSI 產品代碼是否已安裝在裝置上來完成。 針對使用替代偵測方法的應用程式，會使用適當的偵測方法來檢查是否已安裝應用程式。

接著，用戶端會根據部署目的，評估應用程式的預期狀態。 此步驟也牽涉到偵測應用程式是否有針對應用程式應該接受的任何相依性或取代規則。 您可以使用應用程式和部署類型唯一識別碼，在 **AppIntentEval.log** 中追蹤此活動。

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

在上述記錄項目中，**目前狀態**指出應用程式目前是否安裝在裝置上。 **適用性**指出應用程式根據定義的需求規則是否適用。 **ResolvedState**指出應用程式根據部署目的的預期狀態。

> [!TIP]
> 使用[部署監視工具](../../core/support/deployment-monitoring-tool.md)以檢視應用程式狀態、適用性狀態及需求違規。

## <a name="next-steps"></a>後續步驟

- [應用程式下載](deployment-download-technical-reference.md)
