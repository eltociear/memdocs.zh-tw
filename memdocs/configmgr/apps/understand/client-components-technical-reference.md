---
title: 應用程式部署用戶端元件技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 中應用程式部署進行疑難排解所使用的用戶端元件。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688846"
---
# <a name="understanding-application-deployment-client-components"></a>了解應用程式部署用戶端元件

適用於：  Configuration Manager (最新分支)

應用程式部署評估和強制執行作業是由用戶端上的 DCM 代理程式和 CI 代理程式元件處理。 本文說明一般 DCM 和 CI 代理程式作業的運作方式。

## <a name="dcm-agent"></a>DCM 代理程式

DCM 代理程式是負責評估設定項目 (包含應用程式) 的高階用戶端元件。 當部署已啟用或強制執行時，會建立 DCM 代理程式作業，讀取指派原則及決定需要執行的動作。 您可以使用 DCM 代理程式作業識別碼，在用戶端上的 **DCMAgent.log** 中追蹤此活動，其可透過尋找應用程式唯一識別碼來識別。

### <a name="device-deployments"></a>裝置部署

- 針對**必要**部署，DCMAgent.log 會顯示適用的動作。 根據部署期限是否已經過，這些動作可能會有所不同。

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- 針對**可用**部署，DCMAgent.log 會顯示部署 `is not mandatory`。 針對這些部署，應用程式評估已完成，但是除非使用者起始安裝，否則會略過強制執行。

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>使用者部署

- 針對**必要**部署，DCMAgent.log 會顯示適用的動作。 根據部署期限是否已經過，這些動作可能會有所不同。

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- 針對**可用**部署，當使用者起始應用程式安裝時，會建立 DCM 代理程式作業以進行評估和強制執行。

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI 代理程式

CI 代理程式是負責設定項目評估和補救的用戶端元件。 DCM 代理程式會讀取指派原則，並為 CI 代理程式元件建立作業，以執行要求的動作。 **DCMAgent.log** 會記錄 CI 代理程式作業識別碼，這對於在用戶端上的 **CIAgent.log** 中追蹤 CI 代理程式活動相當有用。

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

一般的 CI 代理程式作業會經過多個階段，可以藉由篩選 **CIAgent.log** 中的 CI 代理程式作業識別碼然後尋找 `TransitionState` 來識別。 應用程式部署 CI 代理程式作業的一些主要階段如下：

- **DownloadingCIs**
  - 在此階段中，會下載評估應用程式所需的應用程式中繼資料。 中繼資料包括偵測方法、需求規則、全域條件等。您可以在 **CIDownloader.log** 和 **DataTransferService.log** 中追蹤此活動。 針對**可用**部署，此程序會在第一次評估應用程式期間發生。 但是針對**必要**部署，此程序會在下載原則之後立即發生。

- **InvokingSdmMethod**
  - 在此階段中，會使用應用程式偵測方法來檢查是否已安裝應用程式，並決定預期狀態。 您可以在 **AppDiscovery.log** 和 **AppIntentEval.log** 中追蹤此活動。 如需此階段的詳細資訊，請參閱[應用程式評估](deployment-evaluation-technical-reference.md)。

- **StateDownloadingContents**
  - 在此階段中，會視需要下載應用程式內容。 您可以在 **CAS.log**、**ContentTransferManager.log**、**LocationServices.log** 和 **DataTransferService.log** 中追蹤此活動。 如需此階段的詳細資訊，請參閱[應用程式下載](deployment-download-technical-reference.md)。

- **StateEnforcingCIs**
  - 在此階段中，會起始應用程式安裝。 您可以在 **AppEnforce.log** 中追蹤此活動。 如需此階段的詳細資訊，請參閱[應用程式安裝](deployment-install-technical-reference.md)。

- **StateEnforcementReporting**
  - 在此階段中，會記錄應用程式安裝狀態，以向管理點報告。 您可以在 **StateMessage.log** 中追蹤此活動。

雖然 CI 代理程式作業會經過所有階段，但是如果不是必要階段則會略過。 例如，針對**可用**部署，會略過 StateDownloadingContents 和 StateEnforcingCIs 階段，直到使用者嘗試從軟體中心安裝應用程式。 不過，針對**必要**部署，當啟用指派時，StateDownloadingContents 階段會下載應用程式內容 (如有必要)，但是如果期限是在未來，則會略過 StateEnforcingCIs 階段。 藉由篩選 CI 代理程式作業識別碼並且尋找 `Skipping policy`，即可在 CIAgent.log 中觀察此行為。

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>後續步驟

- [應用程式評估](deployment-evaluation-technical-reference.md)
- [應用程式下載](deployment-download-technical-reference.md)
- [應用程式安裝](deployment-install-technical-reference.md)
