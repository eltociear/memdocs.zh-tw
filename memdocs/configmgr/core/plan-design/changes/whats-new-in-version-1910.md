---
title: 1910 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 最新分支 1910 版所引進之變更和新功能的詳細資料。
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a52b70b0a753036c506e5d515cbac048d6771295
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879061"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Configuration Manager 最新分支 1910 版的新功能

適用於：Configuration Manager (最新分支)

Configuration Manager 最新分支的更新 1910 可以透過主控台內更新的方式取得。 在執行 1806 版或更新版本的站台上套用此更新。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> 本文摘要說明 Configuration Manager 1910 版的變更和新功能。

請一律檢閱適用於安裝此更新的最新檢查清單。 如需詳細資訊，請參閱[安裝更新 1910 的檢查清單](../../servers/manage/checklist-for-installing-update-1910.md)。 更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)。

若要充分利用 Configuration Manager 的新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

> [!TIP]
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager 現在是 Microsoft Endpoint Manager 的一部分。

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager 是一個整合的解決方案，可用於管理您的所有裝置。 Microsoft 將 Configuration Manager 和 Intune 整合成簡化的授權。 繼續運用現有的 Configuration Manager 投資，同時以自有步調來利用 Microsoft 雲端的強大功能。

下列 Microsoft 管理解決方案全都是 Microsoft Endpoint Manager 品牌的一部分：

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [電腦分析](../../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [裝置管理系統管理員主控台](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)中的其他功能

如需詳細資訊，請參閱 Brad Anderson (Microsoft 公司副總裁) 所張貼有關 Microsoft 365 的下列文章：

- [公告部落格文章](https://aka.ms/cmannounce)
- [願景文章](https://aka.ms/MEMVisionPaper)
- [公告摘要影片](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Microsoft 端點管理員隨附的 Configuration Manager 有何變更？

在 1910 版中，除了名稱變更之外，Configuration Manager 的運作方式仍然相同。 某些名稱的變更，可能會影響對下列元件的使用：

- **Configuration Manager 主控台**：尋找主控台的捷徑，以及 [Microsoft 端點管理員] 資料夾中 Windows [開始] 功能表下方的 [遠端控制檢視器]。

- **軟體中心**：尋找 [Microsoft 端點管理員] 資料夾中 Windows [開始] 功能表下方的 [軟體中心] 捷徑。

![Microsoft 端點管理員 [開始] 功能表圖示](media/microsoft-endpoint-manager-start-menu.png)

請務必更新您維護的所有內部文件，以納入這些新的位置。

> [!TIP]
> 在 Windows 10 中開啟 [開始] 功能表時，鍵入名稱即可找到該圖示。 例如，輸入 `Configuration Manager` 或 `Software Center`。

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> 站台基礎結構

### <a name="reclaim-sedo-lock"></a>回收 SEDO 鎖定

<!--4786915-->

從[最新分支 1906 版](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)開始，您可以清除工作順序上的鎖定。 您現在可以在 Configuration Manager 主控台中清除任何物件上的鎖定。

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md#bkmk_sedo)。

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>將內部部署站台延伸及移轉到 Microsoft Azure
<!--3556022-->

這個新工具可協助您以程式設計方式為 Configuration Manager 建立 Azure 虛擬機器 (VM)。 您可以使用預設設定站台角色 (如被動站台伺服器、管理點與發佈點) 安裝它。 在驗證過新角色後，您就可以使用他們作為額外站台系統以獲得高可用性。 您也可以移除內部部署站台系統角色，並指保留 Azure VM 角色。

如需詳細資訊，請參閱[將內部部署站台延伸及移轉到 Microsoft Azure](../../support/azure-migration-tool.md)。

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a> 電腦分析

如需電腦分析雲端服務每月變更的詳細資訊，請參閱[電腦分析的新功能](../../../desktop-analytics/whats-new.md)。

## <a name="real-time-management"></a><a name="bkmk_real"></a> 即時管理

### <a name="optimizations-to-the-cmpivot-engine"></a>對 CMPivot 引擎的最佳化
<!--3197353-->
我們已在 CMPivot 引擎中新增一些重要的最佳化功能。 現在您可以將更多處理功能推送至 ConfigMgr 用戶端。 最佳化會大幅減少執行 CMPivot 查詢所需的網路和伺服器 CPU 負載。 藉由這些最佳化，您現在可以即時對數 GB 的用戶端資料進行 sift 檢查。 

如需詳細資訊，請參閱 [CMPivot 引擎的最佳化](../../servers/manage/cmpivot.md#bkmk_optimization)。

### <a name="additional-cmpivot-entities-and-enhancements"></a>其他 CMPivot 實體及增強功能
<!--5410930-->
我們已新增一些新 CMPivot 實體與實體增強功能以協助進行疑難排解及搜捕。 我們包含了下列實體以進行查詢：

- Windows 事件記錄檔 ([WinEvent](../../servers/manage/cmpivot.md#bkmk_WinEvent))
- 檔案內容 ([FileContent](../../servers/manage/cmpivot.md#bkmk_File))
- 由處理序載入的 DLL ([ProcessModule](../../servers/manage/cmpivot.md#bkmk_ProcessModule))
- Azure Active Directory 資訊 ([AADStatus](../../servers/manage/cmpivot.md#bkmk_AadStatus))
- Endpoint Protection 狀態 ([EPStatus](../../servers/manage/cmpivot.md#bkmk_EPStatus))

此版本也包括數個 CMPivot 的[其他改良功能](../../servers/manage/cmpivot.md#bkmk_Other)。 如需詳細資訊，請參閱[從 1910 版開始的 CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot1910)。

## <a name="content-management"></a><a name="bkmk_content"></a> 內容管理

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Intune Win32 應用程式的 Microsoft 已連線快取支援

<!--5032900-->

當在 Configuration Manager 發佈點上啟用 Microsoft 已連線快取時，這些發佈點現在可以將 Microsoft Intune Win32 應用程式提供給共同管理的用戶端。

如需詳細資訊，請參閱 [Configuration Manager 中的 Microsoft 連線快取](../hierarchy/microsoft-connected-cache.md#bkmk_intune)。

> [!NOTE]
> Configuration Manager 最新分支 1906 版包含[傳遞最佳化的網路內快取](../hierarchy/microsoft-connected-cache.md)，其為安裝在 Windows Server 的開發中應用程式。 從最新分支 1910 版開始，這項功能現在稱為 Microsoft 已連線快取。
>
> 當在 Configuration Manager 發佈點上安裝已連線快取時，其會將傳遞最佳化服務流量卸載至本機來源。 已連線快取會以位元組範圍層級，有效率地快取內容來執行此行為。

## <a name="client-management"></a><a name="bkmk_client"></a> 用戶端管理

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>在合規性政策評定中納入自訂設定基準
<!--3608345-->

您現在可以將自訂設定基準的評估新增為合規性政策評定規則。 在建立或編輯設定基準時，您現在可以使用 [在合規性政策評定期間評估此基準] 選項。 在新增或編輯合規性政策規則時，您會有一個稱為 [在合規性政策評定中納入已設定的基準] 的條件。

針對共同管理的裝置，以及當設定 Intune 以將 Configuration Manager 合規性評估結果作為整體合規性狀態的一部分時，此資訊將會傳送至 Azure Active Directory。 您接著即可將其用於 Office 365 資源的條件式存取。

如需詳細資訊，請參閱[在合規性政策評定中納入自訂設定基準](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)。

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>啟用 Windows 10 企業版多工作階段的使用者原則

<!--4737447-->

Configuration Manager 最新分支 1906 版引進了為 [Windows 虛擬桌面](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)的支援。 此 Microsoft Azure 環境支援數個 OS 版本，其中某些版本可允許多個並行作用中的使用者工作階段。 例如，Windows 10 企業版多工作階段便是這些作業系統版本的其中之一。

如果您需要這些多工作階段裝置的使用者原則，也能接受任何潛在的效能影響，您現在即可設定用戶端設定以啟用使用者原則。 在 [用戶端原則] 群組中，設定 [啟用多個使用者工作階段的使用者原則] 設定。

如需詳細資訊，請參閱[如何設定用戶端設定](../../clients/deploy/configure-client-settings.md)。


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a> 應用程式管理

### <a name="deploy-microsoft-edge-version-77-and-later"></a>部署 Microsoft Edge 77 版與更新版本
<!--4561024-->
全新 Microsoft Edge 已準備好供企業使用。 您現在可以部署 Microsoft Edge 77 版與更新版本給您的使用者。 系統管理員可以選擇搶鮮版 (Beta)、Dev 或穩定通道 ，以及要部署的 Microsoft Edge 用戶端版本。

如需詳細資訊，請參閱[部署 Microsoft Edge 77 版與更新版本](../../../apps/deploy-use/deploy-edge.md)。

### <a name="improvements-to-application-groups"></a>應用程式群組的改善

<!--4760058-->

從最新分支版本 1906 開始，您可以建立作為單一部署傳送給裝置集合的應用程式群組。 此版本改善了此功能：

- 使用者可以在軟體中心內針對應用程式群組選取 [解除安裝]。
- 您可以將映程式群組部署到**使用者集合**。

如需更多一般資訊，請參閱[建立應用程式群組](../../../apps/deploy-use/create-app-groups.md)。


## <a name="os-deployment"></a><a name="bkmk_osd"></a> 作業系統部署

### <a name="improvements-to-the-task-sequence-editor"></a>工作順序編輯器的改善

 工作順序編輯器包含下列改善：

- **搜尋工作順序編輯器：**<!--4621085--> 如果您有包含許多群組和步驟的大型工作順序，可能很難找到特定步驟。 您現在可以在工作順序編輯器中進行搜尋。 這項動作可讓您更快地在工作順序中找到步驟。
- **複製並貼上工作順序條件：**<!--4621098--> 如果想要在工作順序步驟之間重複使用條件，您現在可以在工作順序編輯器中複製及貼上條件。

如需詳細資訊，請參閱說明如何[使用工作順序編輯器](../../../osd/understand/task-sequence-editor.md)的新文章。

### <a name="task-sequence-performance-improvements-power-plans"></a>工作順序效能改善：電源計劃

<!--3555926-->

您現在可以使用高效能電源計劃來執行工作順序。 此選項可改善工作順序的整體速度。 此選項會將 Windows 設定為使用內建的高效能電源計劃，以更高的耗電量來提供最大效能。

如需詳細資訊，請參閱[電源計劃的工作順序效能改善](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf)。

### <a name="task-sequence-download-on-demand-over-the-internet"></a>工作順序會從網際網路隨選下載

<!--3601238-->

您可以使用工作順序來透過雲端管理閘道 (CMG) 部署 Windows 10 就地升級。 不過，它要求部署必須先下載所有內容到本機，才能開始執行工作順序。

從此版本開始，工作順序引擎就可以從已啟用內容的 CMG 或雲端發佈點下載套件。 此變更為您的 Windows 10 就地升級部署提供額外的彈性，現在支援範圍擴大到以網際網路為基礎的裝置。

如需詳細資訊，請參閱[透過 CMG 部署 Windows 10 就地升級](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)。

### <a name="improvements-to-os-deployment"></a>改善 OS 部署

此版本包含下列針對 OS 部署的改善。

#### <a name="boot-image-keyboard-layout"></a>開機映像鍵盤配置

<!--4910348-->

設定開機映像的預設鍵盤配置。 在開機映像的 [自訂] 索引標籤上，使用新的 [設定 WinPE 中的預設鍵盤配置] 選項。 如果您選取 en-us 以外的語言，則 Configuration Manager 仍會在可用的輸入地區設定中包含 en-us。 在裝置上，初始鍵盤配置是選取的地區設定，但使用者可以視需要將裝置切換為 en-us。

如需詳細資訊，請參閱[管理開機映像](../../../osd/get-started/manage-boot-images.md#customization)。

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>匯入 OS 升級套件的單一索引

<!--4931110-->

匯入 OS 升級套件時，您可以使用 [從選取的升級套件的 install.wim 檔案中擷取特定的映像索引] 選項。 此行為類似於 [OS 映像](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)，但會覆寫作業系統升級套件中的現有 install.wim。 此選項會將映像索引擷取至暫存位置，然後再將其移至原始來源目錄。

如需詳細資訊，請參閱[管理 OS 升級套件](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs)。

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>在工作順序中將執行命令列步驟的結果輸出到變數

<!--user story 4977616/bug 4798352-->

[執行命令列] 步驟現在包含 [輸出為工作順序變數] 選項。 當您啟用此選項時，工作順序會將命令的輸出儲存到您指定的自訂工作順序變數。

如需詳細資訊，請參閱[執行命令列](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)。

#### <a name="improvements-to-task-sequence-debugger"></a>工作順序偵錯工具的改善

此版本包含工作順序偵錯工具的改善：

- 使用新的工作順序變數 **TSDebugOnError** 在工作順序傳回錯誤時自動啟動偵錯工具。<!-- 5012536 -->
- 若您在偵錯工具中建立中斷點，然後工作順序重新啟動電腦，偵錯工具會在重新啟動之後維持中斷點。<!-- 5012509 -->

如需詳細資訊，請參閱[工作順序偵錯工具](../../../osd/deploy-use/debug-task-sequence.md)和[工作順序變數 - TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError)。

#### <a name="improved-language-support-in-task-sequence"></a>工作順序中改善的語言支援

<!--5411057, 5138936-->

此版本對 OS 部署期間的語言設定新增了控制。 若您已套用這些語言設定，此變更可協助您簡化您的 OS 部署工作順序。 您只需要為內建**套用 Windows 設定**步驟的每個語言使用一個執行個體 (使用該語言的條件)，而不需要為每個語言使用多個步驟或使用獨立的指令碼。

使用**套用 Windows 設定**工作順序步驟來設定下列新設定：

- 輸入法地區設定 (預設鍵盤配置)
- 系統地區設定
- UI 語言
- UI 語言後援
- 使用者地區設定

如需詳細資訊，請參閱[套用 Windows 設定](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)。

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Windows 10 就地升級的新變數

<!--4680263-->

您現在可以設定新的工作順序變數 **SetupCompletePause**，以在高效能裝置完成 Windows 安裝程式時，解決 Window 10 就地升級工作順序的時間問題。 當您以秒為單位為此變數指派值時，Windows 安裝程式程序會在啟動工作順序之前延遲該時間量。 此逾時可讓 Configuration Manager 用戶端有額外的時間可初始化。

如需詳細資訊，請參閱[工作順序變數 - SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause)。

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a> 軟體更新

### <a name="additional-options-for-third-party-update-catalogs"></a>協力廠商更新類別目錄的其他選項
<!--4469002-->
針對協力廠商更新目錄的同步處理，您現在擁有更精細的控制能力。 從 Configuration Manager 1910 版開始，您可以個別設定每個目錄的同步處理排程。 在使用包含分類更新的目錄時，您可以將同步處理設為僅包含特定的更新類別，以避免同步處理整個目錄。 使用分類目錄時，如果您確定將會部署類別，則可以將其設定為自動下載並發佈至 Windows Server Update Services (WSUS)。

如需詳細資訊，請參閱[啟用協力廠商更新](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910)。

### <a name="use-delivery-optimization-for-all-windows-updates"></a>針對所有 Windows 更新使用傳遞最佳化
<!--4699118-->
過去，您只能將傳遞最佳化用於快速更新。 透過 Configuration Manager 1910 版，您現在可以使用傳遞最佳化來散發執行 Windows 10 1709 版或更新版本之用戶端的所有 Windows Update 內容。

如需詳細資訊，請參閱：
- [將 Windows 10 更新傳遞最佳化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [軟體更新的用戶端設定](../../clients/deploy/about-client-settings.md#software-updates)
- [傳遞最佳化的用戶端設定](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>適用於 ADR 的其他軟體更新篩選器
<!--4852033-->
現在您可以使用 [已部署] 作為自動部署規則 (ADR) 的更新篩選器。 此篩選器可協助識別可能需要部署至試驗或測試集合的新更新。

如需詳細資訊，請參閱[自動部署軟體更新](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)。

## <a name="office-management"></a><a name="bkmk_o365"></a> Office 管理


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Office 365 專業增強版試驗與健康情況儀表板
<!--4488272, 4488301-->

Office 365 專業增強版試驗和健康情況儀表板可協助您規劃、試驗及部署 Office 365 專業增強版。 儀表板會對含有 Office 365 專業增強版的裝置提供健康情況見解，為您找出可能會影響部署計劃的問題。 Office 365 專業增強版試驗與健康情況儀表板會根據增益集清查提供試驗裝置的建議。

如需詳細資訊，請參閱 [Office 365 專業增強版試驗與健康情況儀表板](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot)。

## <a name="protection"></a><a name="bkmk_protect"></a>保護

### <a name="bitlocker-management"></a>BitLocker 管理

<!--3601034-->

Configuration Manager 現在提供下列適用於 BitLocker 磁碟機加密的管理功能：

- 將 BitLocker 用戶端部署到受控 Windows 裝置。
- 管理裝置加密原則。
- 產生合規性報告。
- 使用管理和監視網站來復原金鑰。
- 存取使用者自助入口網站。

如需詳細資訊，請參閱[規劃 BitLocker 管理](../../../protect/plan-design/bitlocker-management.md)。

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 主控台

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>透過主控台連線來檢視使用中的主控台及傳送訊息給系統管理員
<!--4923997-->
我們已對 [主控台連線] 做出下列改善：

- 能夠透過 Microsoft Teams 向其他 Configuration Manager 系統管理員傳送訊息的能力。
- [上次主控台活動訊號] 欄已取代 [上次連線時間] 欄。
  - 前景中的開放主控台會每 10 分鐘傳送一次訊號，以判斷哪些主控台連線目前為作用中。

如需詳細資訊，請參閱[檢視最近連線的主控台](../../servers/manage/admin-console.md#bkmk_viewconnected)和[訊息管理員](../../servers/manage/admin-console.md#bkmk_message)。

### <a name="client-diagnostics-actions"></a>用戶端診斷動作

<!--4433455-->

Configuration Manager 主控台中有 [用戶端診斷] 的新裝置動作：

- **啟用詳細資訊記錄：** 將 CCM 元件的全域記錄層級變更為 [詳細資訊]，並啟用 [偵錯記錄]。
- **停用詳細資訊記錄：** 將全域記錄層級變更為*預設值*，並停用偵錯記錄。

如需詳細資訊，請參閱[用戶端診斷](../../clients/manage/client-notification.md#client-diagnostics)。

### <a name="improvements-to-console-search"></a>主控台搜尋的改善
<!--4640570-->

此版本包含下列 Configuration Manager 主控台中搜尋的改善：

- 您現在可以 [驅動程式套件] 與 [查詢] 節點使用 [所有子資料夾] 搜尋選項。<!--2841181,5424892-->
- 當搜尋傳回超過 1,000 個結果時，請選取通知列上的 [確定] 以檢視更多結果。<!--4640570-->

## <a name="other-updates"></a>其他更新

如需適用於 Configuration Manager 之 Windows PowerShell Cmdlet 變更的詳細資訊，請參閱 [PowerShell 1910 版版本資訊](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps)。

如需管理服務 REST API 變更的詳細資訊，請參閱[管理服務版本資訊](../../../develop/adminservice/release-notes.md#bkmk_1910)。

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 1910 版中變更的摘要](https://support.microsoft.com/help/4535776) \(機器翻譯\)。

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
自 2020 年 2 月 18 日起，就可在主控台中使用下列更新彙總套件 (4537079)：[Microsoft Endpoint Configuration Manager 最新分支 1910 版的更新彙總套件](https://support.microsoft.com/help/4537079) \(機器翻譯\)。



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>後續步驟

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
從 2019 年 12 月 20 日起，1910 版可供所有客戶安裝。

當您準備安裝此版本時，請參閱[安裝 Configuration Manager 的更新](../../servers/manage/updates.md)和[安裝更新 1910 的檢查清單](../../servers/manage/checklist-for-installing-update-1910.md)。

> [!TIP]
> 若要安裝新的站台，請使用 Configuration Manager 的基準版本。
>
> 深入了解：
>
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md) 
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines) 

如需已知的重大問題，請參閱[版本資訊](../../servers/deploy/install/release-notes.md)。

更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist)。
