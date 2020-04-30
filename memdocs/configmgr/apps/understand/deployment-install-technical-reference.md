---
title: 應用程式安裝技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 應用程式安裝進行疑難排解的技術參考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688816"
---
# <a name="application-installation"></a>應用程式安裝

適用於：  Configuration Manager (最新分支)

在繼續之前，請先參閱[應用程式部署用戶端元件](client-components-technical-reference.md)以了解 DCM 和 CI 代理程式作業處理。

應用程式安裝是在強制執行部署時，由 DCM 代理程式和 CI 代理程式元件執行。 可用和必要部署的強制執行時間會有所不同。 若要了解何時強制執行指派，請參閱[應用程式部署至裝置集合](device-deployment-technical-reference.md)或[應用程式部署至使用者集合](user-deployment-technical-reference.md)文章。

## <a name="enforcement-initiation"></a>強制執行起始

應用程式安裝是由用戶端上的 CI 代理程式元件在 **StateEnforcingCIs** 階段期間起始。 無論應用程式是部署至裝置集合或使用者集合，此程序都相同。

- 針對**可用**部署，當使用者從軟體中心起始應用程式安裝時，就會安裝應用程式。
- 針對**必要**部署，應用程式會在部署期限安裝。 但是，使用者可以在期限之前，從軟體中心起始安裝。

當 CI 代理程式起始應用程式安裝時，會建立由 CI 工作管理員元件處理的工作。 CI 工作管理員接著會起始安裝。 您可以使用部署類型唯一識別碼，在 **CITaskMgr.log** 中追蹤此活動。

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>應用程式強制執行

在應用程式強制執行起始之後，用戶端會再次執行應用程式偵測，以確保應用程式尚未安裝。 一旦判斷應用程式未安裝，就會起始應用程式安裝。 您可以使用部署類型唯一識別碼，在用戶端上的 **AppEnforce.log** 中追蹤此活動。

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>安裝驗證

安裝應用程式之後，會再次使用應用程式偵測方法，以確保應用程式偵測為已安裝。

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

最後，在強制執行完成之後，CI 代理程式會收到工作完成通知，而且 CI 代理程式作業會移至下一個階段。

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>後續步驟

[針對應用程式部署進行疑難排解](../deploy-use/troubleshoot-application-deployment.md)
