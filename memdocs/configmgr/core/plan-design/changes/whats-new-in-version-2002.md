---
title: 2002 版有什麼新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 最新分支 2002 版所引進的變更與新功能詳細資料。
ms.date: 05/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: afdcc608133d306042c9c6dc817396bb2fc3f387
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126476"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Configuration Manager 最新分支 2002 版的新功能

適用於：Configuration Manager (最新分支)

Configuration Manager 最新分支的更新 2002 可透過主控台內更新的方式取得。 在執行 1810 版或更新版本的站台上套用此更新。 <!-- baseline only statement:-->在安裝新站台時，也可以基準版本的形式取得。 本文摘要說明 Configuration Manager 2002 版的變更和新功能。

請一律檢閱適用於安裝此更新的最新檢查清單。 如需詳細資訊，請參閱[安裝更新 2002 的檢查清單](../../servers/manage/checklist-for-installing-update-2002.md)。 更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)。

若要充分利用 Configuration Manager 的新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

> [!TIP]
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Microsoft 端點管理員租用戶連結

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a> 裝置同步及裝置動作
<!--3555758-->
Microsoft Endpoint Manager 是一個整合的解決方案，可用於管理您的所有裝置。 Microsoft 將 Configuration Manager 和 Intune 整合到稱為 **Microsoft 端點管理員系統管理中心**的單一主控台。 從這個版本開始，您可以將 Configuration Manager 裝置上傳至雲端服務，並從系統管理中心的 [裝置] 刀鋒視窗中採取動作。

如需詳細資訊，請參閱 [Microsoft 端點管理員租用戶附加](../../../tenant-attach/device-sync-actions.md)。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> 站台基礎結構

### <a name="remove-a-central-administration-site"></a>移除管理中心網站
<!-- 3607277 -->

如果階層包含管理中心網站 (CAS) 和單一子主要站台，則現在可以移除 CAS。 此動作會將 Configuration Manager 基礎結構簡化為單一獨立主要站台。 此動作會將站對站複寫的複雜性簡化，並將管理工作重點放在單一主要站台上。

如需詳細資訊，請參閱[移除 CAS](../../servers/deploy/install/remove-central-administration-site.md)。

### <a name="new-management-insight-rules"></a>新的管理見解規則

此版本包含下列管理見解規則：

- **Configuration Manager 評定**群組中的九個規則由 Microsoft Premier Field Engineering 提供。 這些規則是 Microsoft Premier 在服務中樞提供的許多其他檢查範例。<!-- 3607758 -->

  - Active Directory 安全性群組探索設定的執行頻率過高
  - Active Directory 系統探索設定的執行頻率過高
  - Active Directory 使用者探索設定的執行頻率過高
  - 集合僅限於所有系統或所有使用者
  - 已停用活動訊號探索
  - 為累加式更新啟用長時間執行的集合查詢
  - 減少發佈點上的應用程式和套件數目
  - 次要站台安裝問題
  - 將所有站台更新為相同版本

- **雲端服務**群組中的兩個額外規則有助設定站台來新增安全的 HTTPS 通訊：<!-- 6268489 -->

  - 沒有正確 HTTPS 設定的站台
  - 未上傳至 Azure AD 的裝置

如需詳細資訊，請參閱[管理見解](../../servers/manage/management-insights.md)。

### <a name="improvements-to-administration-service"></a>系統管理服務的改善

<!-- 5728365 -->

系統管理服務是 SMS 提供者的 REST API。 以前必須實作下列相依性之一：

- 為整個站台啟用增強的 HTTP
- 手動將 PKI 型憑證繫結至裝載 SMS 提供者角色的伺服器上 IIS

從這個版本開始，系統管理服務會自動使用站台的自我簽署憑證。 這項變更有助於減少摩擦以更易於使用系統管理服務。 站台一律會產生此憑證。 [Use Configuration Manager-generated certificates for HTTP site systems] \(針對 HTTP 站台系統使用 Configuration Manager 產生的憑證\) 的增強 HTTP 站台設定，其僅控制站台系統是否使用此憑證。 現在系統管理服務會忽略此站台設定，因為此服務一律使用站台的憑證，即使目前沒有其他站台系統使用增強的 HTTP 也一樣。 您仍然可以使用 PKI 型的伺服器驗證憑證。

如需詳細資訊，請參閱下列新文章：

- [什麼是系統管理服務？](../../../develop/adminservice/overview.md)
- [如何設定管理服務](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>適用於 Azure Active Directory 探索和群組同步的 Proxy 支援

<!-- 5913817 -->

下列項目現在已可使用站台系統的 Proxy 設定 (包括驗證)：

- Azure Active Directory (Azure AD) 使用者探索
- Azure AD 使用者群組探索
- 將集合成員資格結果同步至 Azure Active Directory 群組

如需詳細資訊，請參閱 [Proxy 伺服器支援](../network/proxy-server-support.md#bkmk_other)。

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> 雲端連結管理

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>重大狀態訊息顯示必要端點的伺服器連線錯誤

<!-- 5566763 -->

如果 Configuration Manager 站台伺服器無法連線至雲端服務的必要端點，則會引發重大狀態訊息識別碼 11488。 當站台伺服器無法連線至服務時，SMS_SERVICE_CONNECTOR 元件狀態會變更為重大。 在 Configuration Manager 主控台的 [元件狀態] 節點中檢視詳細狀態。

### <a name="token-based-authentication-for-cloud-management-gateway"></a>雲端管理閘道的權杖型驗證

<!-- 5686290 -->

雲端管理閘道 (CMG) 支援許多類型的用戶端，但即便使用增強 HTTP，這些用戶端還是需要用戶端驗證憑證。 對於以網際網路為基礎的用戶端而言，若不常連線至內部網路、則無法加入 Azure Active Directory (Azure AD)，且沒有方法可安裝 PKI 發行憑證，則可能難以佈建此憑證需求。

從這個版本開始， Configuration Manager 使用下列方法來擴充其裝置支援：

- 在內部網路註冊以取得唯一權杖
- 為以網際網路為基礎的裝置建立大量註冊權杖

如需詳細資訊，請參閱 [CMG 的權杖型驗證](../../clients/deploy/deploy-clients-cmg-token.md)。

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Microsoft Endpoint Configuration Manager 雲端功能

<!--5834830-->

當有新雲端式功能可用於 Microsoft 端點管理員系統管理中心或內部部署 Configuration Manager 安裝的其他附加雲端服務時，現在即可在 Configuration Manager 主控台中加入這些新功能。 如需在 Configuration Manager 主控台中啟用功能的詳細資訊，請參閱[從更新啟用選擇性功能](../../servers/manage/install-in-console-updates.md#bkmk_options)。

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> 電腦分析

如需電腦分析雲端服務每月變更的詳細資訊，請參閱[電腦分析的新功能](../../../desktop-analytics/whats-new.md)。

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>連線健全狀況儀表板顯示用戶端連線問題

使用 Configuration Manager 中的電腦分析連線健全狀況儀表板，以監視用戶端的連線能力健全狀況。 這項功能現在有助更輕鬆地識別兩個領域中用戶端 Proxy 設定的問題：

- **端點連線能力檢查**：如果用戶端無法連線到必要的端點，即會在儀表板中看到設定警示。 向下切入以查看用戶端因 Proxy 設定問題而無法連線的端點。<!-- 4963230 -->

- **連線能力狀態**：如果您的用戶端使用 Proxy 伺服器來存取電腦分析雲端服務，則 Configuration Manager 現在會顯示來自用戶端的 Proxy 驗證問題。 向下切入以查看因 Proxy 驗證而無法註冊的用戶端。<!-- 4963383 -->

如需詳細資訊，請參閱[監視連線健全狀況](../../../desktop-analytics/monitor-connection-health.md)。

## <a name="real-time-management"></a><a name="bkmk_real"></a> 即時管理

### <a name="improvements-to-cmpivot"></a>CMPivot 的改善

<!-- 5870934 -->

我們讓巡覽 CMPivot 實體變得更容易。 您現在可以搜尋 CMPivot 實體。 並已新增圖示，可供輕鬆區分實體與實體物件類型。

如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002)。

## <a name="content-management"></a><a name="bkmk_content"></a> 內容管理

### <a name="exclude-certain-subnets-for-peer-content-download"></a>排除特定子網路以進行對等內容下載

<!-- 3555777 -->

界限群組包含下列適用對於對等下載的選項：**對等下載期間，僅使用相同子網路中的對等**。 如果啟用此選項，則管理點的內容位置清單，只會包含位於與用戶端相同子網路與界限群組中的對等來源。 根據網路設定，您現在可以排除特定子網路以進行比對。 例如，您想要包含界限，但排除特定的 VPN 子網路。

如需詳細資訊，請參閱[界限群組選項](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)。

### <a name="proxy-support-for-microsoft-connected-cache"></a>Microsoft 連線快取的 Proxy 支援

<!-- 5856396 -->

如果環境使用未驗證的 Proxy 伺服器來存取網際網路，則現在當啟用 Microsoft 連線快取的 Configuration Manager 發佈點時，該發佈點可以透過 Proxy 進行通訊。 如需詳細資訊，請參閱 [Microsoft 連線快取](../hierarchy/microsoft-connected-cache.md)。

## <a name="client-management"></a><a name="bkmk_client"></a> 用戶端管理

### <a name="client-log-collection"></a>用戶端記錄收集

<!-- 4226618 -->

您現在可以觸發用戶端裝置，將其用戶端記錄上傳到站台伺服器，方法是從 Configuration Manager 主控台傳送用戶端通知動作。

如需詳細資訊，請參閱[用戶端通知](../../clients/manage/client-notification.md#client-diagnostics)。

### <a name="wake-up-a-device-from-the-central-administration-site"></a>從管理中心網站喚醒裝置

<!-- 6030715 -->

您現在可從管理中心網站 (CAS) 的 [裝置] 或 [裝置集合] 節點中，使用用戶端通知動作來喚醒裝置。 過去僅主要站台提供此動作。

如需詳細資訊，請參閱[如何設定網路喚醒](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810)。

### <a name="improvements-to-support-for-arm64-devices"></a>對 ARM64 裝置支援的改善

<!--5954175-->

在具有需求規則或適用性清單的物件上所支援 OS 版本清單中，已提供**所有 Windows 10 (ARM64)** 平台。

> [!NOTE]
> 如果您先前已選取最上層的 **Windows 10** 平台，則此動作會自動選取 [所有 Windows 10 (64 位元)] 和 [所有 Windows 10 (32位元)]。 系統不會自動選取這個新平台。 如果想要新增 [所有 Windows 10 (ARM64)]，請在清單中手動選取該選項。

如需 Configuration Manager 支援 ARM64 裝置的詳細資訊，請參閱 [ARM64 上的 Windows 10](../configs/support-for-windows-10.md#bkmk_arm64)。

### <a name="track-configuration-item-remediations"></a>追蹤設定項目補救
<!--4261411-->
現在可根據設定項目合規性規則使用 [Track remediation history when supported] \(在支援時追蹤補救歷程記錄\)。 啟用此選項時，任何針對設定項目在用戶端上發生的補救都會產生狀態訊息。 該歷程記錄會儲存於 Configuration Manager 資料庫中。

[如何為 Configuration Manager 用戶端所管理的 Windows 桌上型電腦和伺服器電腦建立自訂設定項目](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track)。

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a> 應用程式管理

### <a name="microsoft-edge-management-dashboard"></a>Microsoft Edge 管理儀表板

<!-- 3871913 -->

Microsoft Edge 管理儀表板可供深入了解 Microsoft Edge 和其他瀏覽器的使用方式。 在此儀表板中，您可以：

- 查看有多少裝置已安裝 Microsoft Edge
- 查看有多少用戶端已安裝不同版本的 Microsoft Edge
- 在不同裝置上查看已安裝的瀏覽器
- 檢視裝置慣用的瀏覽器

從 [軟體程式庫] 工作區中，按一下 [Microsoft Edge 管理] 以查看儀表板。 按一下 [瀏覽] 並選擇另一個集合，以變更圖形資料的集合。 根據預設，下拉式清單會列出五個最大的集合。 當您選取不在清單中的集合時，新選取的集合即會佔據下拉式清單中最後一位。

如需詳細資訊，請參閱 [Microsoft Edge 管理](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash)。

### <a name="improvements-to-microsoft-edge-management"></a>針對 Microsoft Edge 管理的改善

<!-- 4561024 -->

您現在可以建立 Microsoft Edge 應用程式，並將其設定為接收自動更新，而非停用自動更新。 此變更可讓您選擇搭配 Configuration Manager 管理 Microsoft Edge 的更新，或允許 Microsoft Edge 自動更新。 建立應用程式時，請在 [Microsoft Edge 設定] 頁面上選取 [Allow Microsoft Edge to automatically update the version of the client] \(允許 Microsoft Edge 自動更新終端使用者裝置上的用戶端版本\)。

如需詳細資訊，請參閱 [Microsoft Edge 管理](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate)。

### <a name="task-sequence-as-an-app-model-deployment-type"></a>工作順序即應用程式模型部署類型

<!-- 3555953 -->

您現在可以透過應用程式模型，使用工作順序安裝複雜的應用程式。 將部署類型新增到本身為工作順序的應用程式 (安裝或解除安裝應用程式)。 此功能提供下列行為：

- 在軟體中心內使用圖示顯示應用程式工作順序。 圖示可讓使用者更輕易地尋找和識別應用程式工作順序。

- 定義應用程式工作順序的額外中繼資料，包括當地語系化資訊

如需詳細資訊，請參閱[建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)。

## <a name="os-deployment"></a><a name="bkmk_osd"></a> 作業系統部署

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>在用戶端註冊後立即啟動工作順序

<!-- 5526972 -->

當安裝並註冊新的 Configuration Manager 用戶端，同時在其中部署工作順序時，很難判斷用戶端在註冊後多久才會執行工作順序。 此版本引進新的用戶端設定屬性，讓您能夠使用該屬性在用戶端成功向站台註冊後，於其上啟動工作順序。

如需詳細資訊，請參閱[關於用戶端安裝屬性 - PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts)。

### <a name="improvements-to-check-readiness-task-sequence-step"></a>檢查整備程度工作順序步驟的改善

<!-- 6005561 -->

現在可於**檢查整備程度**工作順序步驟中驗證更多裝置屬性。 您可以在工作順序中使用此步驟來驗證目標電腦是否符合先決條件。

- 目前 OS 的架構
- 最低 OS 版本
- 最高 OS 版本
- 用戶端最低版本
- 目前 OS 的語言
- AC 電源已插入
- 網路介面卡已連線，且不是無線網路

如需詳細資訊，請參閱[工作順序步驟 - 檢查整備程度](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness)。

### <a name="improvements-to-task-sequence-progress"></a>工作順序進度的改善

<!-- 5932692 -->

工作順序進度視窗現在包含下列改善：

- 您可啟用工作順序進度視窗來顯示目前的步驟編號、步驟總數和完成百分比
- 增加視窗的寬度來提供更多的空間，以在單一行中顯示完整的組織名稱

如需詳細資訊，請參閱 [OS 部署的使用者體驗](../../../osd/understand/user-experience.md#task-sequence-progress)。

### <a name="improvements-to-os-deployment"></a>改善 OS 部署

此版本包含下列針對 OS 部署的改善：

- 工作順序環境包含新的唯讀變數 `_TSSecureBoot`。<!--5842295--> 請使用此變數來判斷安全開機在已啟用 UEFI 裝置上的狀態。 如需詳細資訊，請參閱 [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot)。

- 設定工作順序變數，以設定**執行命令列**和**執行 PowerShell 指令碼**步驟的使用者內容。<!-- 5573175 --> 如需詳細資訊，請參閱 [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) 和 [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser)。

- 您現在可以在**執行 PowerShell 指令碼**步驟中將**參數**屬性設定為變數。<!-- 5690481 --> 如需詳細資訊，請參閱[執行 PowerShell 指令碼](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)。

- Configuration Manager PXE 回應程式現在會將狀態訊息傳送至站台伺服器。 這項變更可供更輕鬆地對使用此服務的 OS 部署進行疑難排解。<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> 軟體更新

### <a name="orchestration-groups"></a>協調流程群組

<!-- 3098816 -->

建立協調流程群組以使用更好的方式控制裝置的軟體更新部署。 許多伺服器系統管理員都需要更謹慎地管理特定工作負載的更新，並自動化它們之間的行為。

協調流程可讓您依百分比、特定數字或明確順序來彈性地更新裝置。 您也可以在裝置執行更新部署之前或之後執行 PowerShell 指令碼。

協調流程群組的成員可以是任意 Configuration Manager 用戶端，而不只是伺服器。 協調流程群組規則會將所有軟體更新部署的裝置套用到包含協調流程群組成員的任何集合。 其他部署行為仍然適用。 例如，維護時段與部署排程。

如需詳細資訊，請參閱[協調流程群組](../../../sum/deploy-use/orchestration-groups.md)。

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>在服務堆疊更新之後評估軟體更新

<!-- 4639943 -->

Configuration Manager 現在會偵測服務堆疊更新 (SSU) 是否為多個更新之安裝的一部分。 偵測到 SSU 時，系統會先加以安裝。 在安裝 SSU 之後，會執行軟體更新評估週期以安裝剩餘的更新。 此變更允許在服務堆疊更新之後安裝相依的累積更新。 裝置不需要在安裝之間重新啟動，且不需要建立額外的維護時段。 系統只會針對非使用者起始的安裝優先安裝 SSU。 例如，如果使用者起始來自軟體中心的多個更新安裝，系統可能不會先安裝 SSU。

如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu)。

### <a name="office-365-updates-for-disconnected-software-update-points"></a>適用於已中斷連線軟體更新點的 Office 365 更新

<!-- 4065163 -->

您可使用新的工具，將 Office 365 更新從已連線到網際網路的 WSUS 伺服器，匯入至已中斷連線的 Configuration Manager 環境中。 先前當您在已中斷連線的環境中匯出及匯入軟體更新的中繼資料時，您並無法部署 Office 365 更新。 Office 365 更新需要從 Office API 與 Office CDN 下載其他中繼資料，這在已中斷連線的環境中是做不到的。

如需詳細資訊，請參閱[從已中斷連線的 Office 365 更新點同步處理軟體更新](../../../sum/get-started/synchronize-office-updates-disconnected.md)。

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a>保護

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>擴展 Microsoft Defender 進階威脅防護 (ATP) 上線

<!-- 5229962 -->
Configuration Manager 已擴展將裝置上線至 Microsoft Defender ATP 的支援。 如需詳細資訊，請參閱 [Microsoft Defender 進階威脅防護](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md#onboard-devices)。

## <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a> 透過 Microsoft 端點管理員系統管理中心將 Configuration Manager 用戶端上線至 Microsoft Defender ATP
<!--5691658-->
現在可以將 Microsoft Defender ATP 端點偵測及回應 (EDR) 上線原則部署到 Configuration Manager 受控用戶端。 這些用戶端不需要 Azure AD 或 MDM 註冊，且原則會將目標放在 ConfigMgr 集合而不是 Azure AD 群組。

此功能可讓客戶從單一管理體驗的 Microsoft Endpoint Manager 系統管理中心，管理 Intune MDM 和 Configuration Manager 用戶端 EDR/ATP 上線。 如需詳細資訊，請參閱 [Intune 中端點安全性的端點偵測與回應原則](../../../../intune/protect/endpoint-security-edr-policy.md)。

> [!Important]
> 針對此功能，您將需要安裝在您的環境中的 Hotfix 彙總套件 [KB4563473](https://support.microsoft.com/help/4563473)。

### <a name="improvements-to-bitlocker-management"></a>BitLocker 管理的改善

- BitLocker 管理原則現在包含其他額外設定，包括適用於固定式及抽取式磁碟機的原則。<!-- 5925683 --> 如需詳細資訊，請參閱 [BitLocker 設定參考](../../../protect/tech-ref/bitlocker/settings.md)。

- 在 Configuration Manager 最新分支 1910 版中，若要整合 BitLocker 復原服務，則必須針對管理點啟用 HTTPS。 需要有 HTTPS 連線，才能從 Configuration Manager 用戶端，將網路上的修復金鑰加密至管理點。 對許多客戶而言，設定管理點和所有 HTTPS 用戶端可能會很困難。

    從這個版本開始，HTTPS 需求適用於裝載復原服務的 IIS 網站，而不是整個管理點角色。 這項變更放寬了憑證需求，但仍然會加密傳輸中的修復金鑰。<!-- 5925660 --> 如需詳細資訊，請參閱[加密復原資料](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md)。

## <a name="reporting"></a><a name="bkmk_report"></a> 報告

### <a name="integrate-with-power-bi-report-server"></a>與 Power BI 報表伺服器整合

<!-- 3721603 -->

現在可將 Power BI 報表伺服器與 Configuration Manager 報告整合。 這項整合為您提供現代化視覺效果和更好的效能。 其新增的 Power BI 報表主控台支援類似 SQL Server Reporting Services 已有的功能。

如需詳細資訊，請參閱[與 Power BI 報表伺服器整合](../../servers/manage/powerbi-report-server.md)。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 主控台

### <a name="show-boundary-groups-for-devices"></a>顯示裝置的界限群組

<!--6521835-->

為了協助對具有界限群組的裝置行為進行更完善疑難排解，您現在可以檢視特定裝置的界限群組。 在 [裝置] 節點中，或當顯示 [裝置集合] 的成員時，將新的 [界限群組] 資料行新增至清單檢視。

如需詳細資訊，請參閱[界限群組](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary)。

### <a name="send-a-smile-improvements"></a>傳送笑臉的改善

<!-- 5891852 -->

當傳送笑臉或傳送苦臉時，會在提交意見反應時建立狀態訊息。 這項改善會提供下列記錄：

- 提交意見反應的時間
- 提交意見反應的人員
- 意見反應識別碼
- 是否成功提交意見反應

識別碼為 53900 的狀態訊息代表提交成功，而 53901 則為提交失敗。

如需詳細資訊，請參閱[產品意見反應](../../understand/find-help.md#BKMK_1806Feedback)。

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>在所有子資料夾中搜尋設定項目和設定基準

<!--5891241-->

類似於舊版的改善功能，您現在可以從 [設定項目] 和 [設定基準] 節點使用 [所有子資料夾] 搜尋選項。

## <a name="tools"></a><a name="bkmk_tools"></a> 工具

### <a name="onetrace-log-groups"></a>OneTrace 記錄群組

<!-- 5559993 -->

OneTrace 現在支援可自訂的記錄群組，與支援中心的功能類似。 記錄檔群組可讓您開啟單一案例的所有記錄檔。 OneTrace 目前包含下列案例的群組：

- 應用程式管理
- 相容性設定 (也稱為 Desired Configuration Management)
- 軟體更新

如需詳細資訊，請參閱[支援中心 OneTrace](../../support/support-center-onetrace.md)。

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a> 將內部部署站台延伸及移轉到 Microsoft Azure 的改善
<!--5665775, 6307931-->
用於將內部部署站台延伸及移轉到 Microsoft Azure 的工具，現在支援在單一 Azure 虛擬機器上佈建多個站台系統角色。 您可以在初始 Azure 虛擬機器部署完成之後，新增站台系統角色。

如需詳細資訊，請參閱[將內部部署站台延伸及移轉到 Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role)。

## <a name="other-updates"></a>其他更新

從此版本開始，下列功能已不再是[發行前版本](../../servers/manage/pre-release-features.md)：

- [Azure Active Directory 使用者群組探索](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [將集合成員資格結果同步至 Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [CMPivot 獨立](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [共同受控裝置的用戶端應用程式](../../../comanage/workloads.md#client-apps) (先前稱為*適用於共同受控裝置的行動應用程式*)<!-- 1357892/3600959 -->

如需適用於 Configuration Manager 的 Windows PowerShell Cmdlet 變更詳細資訊，請參閱 [PowerShell 2002 版版本資訊](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps)。

如需管理服務 REST API 變更的詳細資訊，請參閱[管理服務版本資訊](../../../develop/adminservice/release-notes.md#bkmk_2002)。

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 2002 版中變更的摘要](https://support.microsoft.com/help/4556203) \(機器翻譯\)。

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>後續步驟

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

從 2020 年 5 月 11 日起，2002 版可供所有客戶安裝。

當準備安裝此版本時，請參閱[安裝 Configuration Manager 的更新](../../servers/manage/updates.md)，以及[安裝更新 2002 的檢查清單](../../servers/manage/checklist-for-installing-update-2002.md)。

> [!TIP]
> 若要安裝新的站台，請使用 Configuration Manager 的基準版本。
>
> 深入了解：
>
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

如需已知的重大問題，請參閱[版本資訊](../../servers/deploy/install/release-notes.md)。

更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist)。
