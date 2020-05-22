---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1802 版中可用的功能。
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 94208da3eda33cba69f04bbbf42edd08b585c1c4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428198"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Configuration Manager Technical Preview 1802 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

此文章介紹 Configuration Manager 技術預覽 1802 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 

安裝本版的 Technical Preview 之前，請先參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 的已知問題
- **當您有以被動模式執行的站台伺服器時，更新到新的預覽版本會失敗**。 如果您有[被動模式下的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)，則您必須先解除安裝被動模式站台伺服器，再更新成這個新的預覽版本。 當您的站台完成更新之後，就可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在 Configuration Manager 主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。
  <!--sms 489412-->


</br>

**以下是您可以使用此版本試用的新功能。**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>使用共同管理將 Endpoint Protection 工作負載轉換至 Intune    
<!-- 1357365 -->
在此版本中，您現在可以在啟用共同管理之後，將 Endpoint Protection 工作負載從 Configuration Manager 轉換至 Intune。 若要轉換 Endpoint Protection 工作負載，移至共同管理內容頁面，然後將滑動軸從 Configuration Manager 移至 [試驗]  或 [全部]  。 如需詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../comanage/overview.md)。


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>設定 Windows 傳遞最佳化以使用 Configuration Manager 界限群組
<!-- 1324696 -->
您可以使用 Configuration Manager 界限群組，來定義和規範在您的公司網路上以及到遠端辦公室的內容發佈。 [Windows 傳遞最佳化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是一種雲端式點對點技術，可在 Windows 10 裝置之間共用內容。 從這個版本開始，設定傳遞最佳化，以便在同儕節點之間共用內容時使用界限群組。 新的用戶端設定會套用界限群組識別碼，以作為用戶端上的傳遞最佳化群組識別碼。 當用戶端與傳遞最佳化雲端服務進行通訊時，它會使用此識別碼來尋找含有所需內容的同儕節點。 

### <a name="prerequisites"></a>先決條件
- 傳遞最佳化僅適用於 Windows 10 用戶端

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 在 Configuration Manager 主控台之 [系統管理]  工作區的 [用戶端設定]  節點中，建立自訂的用戶端裝置設定原則。
2. 選取新的**傳遞最佳化**群組。
3. 啟用 [請在傳遞最佳化群組識別碼使用 Configuration Manager 界限群組]  設定。

如需詳細資訊，請參閱[傳遞最佳化選項](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization)中的**群組**傳遞模式選項。



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>透過雲端管理閘道的 Windows 10 就地升級工作順序
<!-- 1357149 -->

Windows 10 [就地升級工作順序](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)現在支援部署到以網際網路為基礎且透過[雲端管理閘道](../clients/manage/cmg/plan-cloud-management-gateway.md)管理的用戶端。 此功能讓遠端使用者可以更輕鬆地升級到 Windows 10，而不需連線到公司網路。 

確定會將就地升級工作順序所參考的所有內容發佈到[雲端發佈點](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)。 否則，裝置無法執行工作順序。

當您部署升級工作順序時，請使用下列設定：
- **允許工作順序針對網際網路上的用戶端執行** (位於部署的 [使用者體驗] 索引標籤上)。
- **啟動工作順序之前下載所有內容到本機** (位於部署的 [發佈點] 索引標籤上)。 其他像是**視執行工作順序所需，將內容下載到本機**的選項無法在此案例中運作。 工作順序引擎目前無法從雲端發佈點取得內容。 Configuration Manager 用戶端必須先從雲端發佈點下載內容，然後才能啟動工作順序。
- (選擇性  ) **預先下載此工作順序的內容** (位於部署的 [一般] 索引標籤上)。 如需詳細資訊，請參閱[設定預先快取內容](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content)。



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 就地升級工作順序的改善
<!-- 1357425 -->
Windows 10 就地升級的預設工作順序範本現在包含其他群組，其中具有要在升級程序前後新增的建議動作。 這些動作在許多已順利升級到 Windows 10 裝置的客戶之間是通用的。 

### <a name="new-groups-under-prepare-for-upgrade"></a>**準備升級**下的新群組
- **電池檢查**：在此群組中新增步驟，以確認電腦是使用電池還是電線。 此動作需要自訂指令碼或公用程式來執行這項檢查。
- **網路/有線連線檢查**：在此群組中新增步驟，以確認電腦是否連線到網路，且未使用無線連線。 此動作需要自訂指令碼或公用程式來執行這項檢查。
- **移除不相容的應用程式**：在此群組中新增步驟，以移除與此版本 Windows 10 不相容的任何應用程式。 將應用程式解除安裝的方法各不相同。 如果應用程式使用 Windows Installer，請從應用程式之 Windows Installer 部署類型內容的 [程式]  索引標籤中複製**解除安裝程式**命令列。 然後使用解除安裝程式命令列，在此群組中新增**執行命令列**步驟。 例如： </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **移除不相容的驅動程式**：在此群組中新增步驟，以移除與此版本 Windows 10 不相容的任何驅動程式。
- **移除/暫止協力廠商安全性**：在此群組中新增步驟，以移除或暫止協力廠商安全性程式，例如防毒軟體。
   - 如果您使用協力廠商的磁碟加密程式，請使用 **/ReflectDrivers** [命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)，將其加密驅動程式提供給 Windows 安裝程式。 在此群組的工作順序中，新增[設定工作順序變數](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步驟。 將工作順序變數設為 **OSDSetupAdditionalUpgradeOptions**。 搭配驅動程式的路徑來將值設為 **/ReflectDriver**。 這個[工作順序動作變數](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)會附加工作順序所使用的 Windows 安裝程式命令列。 如需這個程序的任何其他指引，請連絡您的軟體廠商。

### <a name="new-groups-under-post-processing"></a>**後續處理**下的新群組
- **套用以安裝程式為基礎的驅動程式**：在此群組中新增步驟以從套件安裝以安裝程式為基礎的驅動程式 (.exe)。
- **安裝/啟用協力廠商安全性**：在此群組中新增步驟，以安裝或啟用協力廠商安全性程式，例如防毒軟體。 
- **設定 Windows 預設應用程式與關聯**：在此群組中新增步驟以設定 Windows 預設應用程式與檔案關聯。 首先，使用您所需的應用程式關聯來準備參照電腦。 接著，執行下列命令列來匯出： </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>將 XML 檔案新增至套件。 然後，在此群組中新增[執行命令列](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟。 指定包含 XML 檔案的套件，然後指定下列命令列： </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> 如需詳細資訊，請參閱[匯出或匯入預設應用程式關聯](https://docs.microsoft.com/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)。
- **套用自訂項目與個人化項目**：在此群組中新增步驟以套用 [開始] 功能表自訂項目，例如組織程式群組。 如需詳細資訊，請參閱[自訂開始畫面](https://docs.microsoft.com/windows-hardware/manufacture/desktop/customize-the-start-screen)。

### <a name="additional-recommendations"></a>其他建議
- 檢閱 Windows 文件以[解決 Windows 10 升級錯誤](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)。 這篇文章也包含有關升級程序的詳細資訊。
- 在預設的**檢查整備程度**步驟中，啟用 [確認最小可用磁碟空間 (MB)]  。 針對 32 位元作業系統升級套件，將值設為至少 **16384** (16 GB)，或針對 64 位元設為 **20480** (20 GB)。 
- 使用 **SMSTSDownloadRetryCount** [內建工作順序變數](../../osd/understand/task-sequence-variables.md)來重試下載原則。 目前依預設，用戶端會重試兩次；已將此變數設為二 (2)。 如果您的用戶端不在有線的公司網路連線上，額外的重試次數可協助用戶端取得原則。 使用此變數，如果它無法下載原則，除了延遲失敗以外，不會造成任何負面的副作用。<!-- 501016 --> 此外，從預設的 15 秒增加 **SMSTSDownloadRetryDelay** 變數。
- 執行內嵌相容性評估。 
   - 提早在**準備升級**群組中新增第二個**升級作業系統**步驟。 將其命名為「升級評估」  。 指定相同的升級套件，然後啟用**執行 Windows 安裝程式相容性掃描但不啟動升級**的選項。 啟用 [選項] 索引標籤上的 [發生錯誤時繼續]  。 
   - 緊接這個*升級評估*步驟，新增**執行命令列**步驟。 指定下列命令列：</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>在 [選項]  索引標籤上，新增下列條件： </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>此傳回碼是 MOSETUP_E_COMPAT_SCANONLY (0xC1900210) 的十進位對等項，表示此為成功的相容性掃描，沒有任何問題。 如果*升級評估*步驟成功並傳回此代碼，即可略過此步驟。 否則，如果評估步驟傳回任何其他傳回碼，此步驟就會使用Windows 安裝程式相容性掃描的傳回碼來使工作順序失敗。
   - 如需詳細資訊，請參閱[升級作業系統](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)。
- 如果您想要在此工作順序期間將裝置從 BIOS 變更為 UEFI，請參閱[在就地升級期間從 BIOS 轉換至 UEFI](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)。

如果您有進一步的建議，請從功能區的 [首頁]  索引標籤傳送**意見反應**。



## <a name="improvements-to-pxe-enabled-distribution-points"></a>支援 PXE 的發佈點改善
<!-- 1357580 -->
為了釐清在 Technical Preview 1706 版中首度引進的[新 PXE 功能](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)的行為，我們已將 [支援 IPv6]  選項重新命名。 在發佈點內容的 [PXE]  索引標籤上，核取 [在不使用 Windows 部署服務的情況下啟用 PXE 回應程式]  。 

此選項會啟用發佈點上的 PXE 回應程式，而不需要 Windows 部署服務 (WDS)。 如果您在已經支援 PXE 的發佈點上啟用這個新選項，Configuration Manager 就會暫止 WDS 服務。 如果您停用這個新選項，但仍**為用戶端啟用 PXE 支援**，則發佈點會再次啟用 WDS。

由於 WDS 並非必要，因此，支援 PXE 的發佈點可以是用戶端或伺服器作業系統，包括 Windows Server Core。 這個新的 PXE 回應程式服務會繼續支援 IPv6，而且也會強化遠端辦公室中支援 PXE 之發佈點的彈性。

> [!NOTE]
> 此服務使用與 Technical Preview 1712 版中[用戶端的 PXE 回應程式服務](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service)相同的基本技術。 該功能不需要發佈點角色的額外負荷。

### <a name="multicast"></a>多點傳送
若要在發佈點的 [多點傳送]  索引標籤上啟用和設定多點傳送，發佈點必須使用 WDS。 
- 如果您**為用戶端啟用 PXE 支援**並**啟用多點傳送來同時傳送資料到多個用戶端**，則您無法**啟用 PXE 回應程式而不需 Windows 部署服務**。
- 如果您**為用戶端啟用 PXE 支援**並**啟用 PXE 回應程式而不需 Windows 部署服務**，則您無法**啟用多點傳送來同時傳送資料到多個用戶端**。



## <a name="deployment-templates-for-task-sequences"></a>工作順序的部署範本
<!-- 1357391 -->
工作順序的部署精靈現在可以建立一個部署範本。 該部署範本可以儲存並套用到現有或新的工作順序來建立部署。 

### <a name="try-it-out"></a>試試看！  
請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。 

 **建立新工作順序部署的部署範本** <br/> 
1. 在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  。
2. 以滑鼠右鍵按一下工作順序，然後選取 [部署]  。 
3. 在 [一般]  索引標籤上，請注意現在有一個 [選取部署範本]  的選項。 
4. 繼續透過 [部署軟體精靈]  選取工作順序的部署設定。 
5. 當您到達 [部署軟體精靈]  的 [摘要]  索引標籤時，按一下 [儲存成範本]  。
6. 指定範本的名稱，然後選取要儲存在範本中的設定。 
7. 按一下 **[儲存]** 。 現在已可從 [選取部署範本]  選項中取得該範本。



## <a name="product-lifecycle-dashboard"></a>產品生命週期儀表板
<!--1319632-->
新的[產品生命週期儀表板](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)會針對安裝於利用 Configuration Manager 管理的裝置上的 Microsoft 產品，顯示 Microsoft 產品生命週期原則的狀態。 該儀表板會提供有關環境中的 Microsoft 產品、支援狀態，以及支援結束日期的資訊。 您可以使用儀表板來了解每項產品的支援可用性。 

若要存取 Configuration Manager 主控台中的生命儀表板，請移至 [資產與合規性]   >[Asset Intelligence]   >[產品生命週期]  。



## <a name="improvements-to-reporting"></a>報表的改善
<!--1357653-->
我們已根據[您的意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) \(英文\) 新增了一份**特定集合的 Windows 10 維護詳細資料**的新報表。 此報表會顯示資源識別碼、NetBIOS 名稱、OS 名稱、OS 版本名稱、組建、OS 分支，以及 Windows 10 裝置的服務狀態。 若要存取此報表，請移至 [監視]   >[報表]   >[報表]   >[作業系統]   >[特定集合的 Windows 10 維護詳細資料]  。



## <a name="improvements-to-software-center"></a>軟體中心的增強功能
<!--1357592-->
根據[您的意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) \(英文\)，現在可在軟體中心隱藏已安裝的應用程式。 啟用此選項時，[應用程式] 索引標籤中將不再顯示已安裝的應用程式。 

### <a name="try-it-out"></a>試試看！
在軟體中心用戶端設定中啟用 [在軟體中心內隱藏安裝的應用程式]  設定。 當使用者安裝應用程式時，請觀察軟體中心內的行為。



## <a name="improvements-to-run-scripts"></a>執行指令碼的改善
<!--1236459-->
[執行指令碼](../../apps/deploy-use/create-deploy-scripts.md)功能現在會使用 JSON 格式傳回指令碼輸出。 此格式一律傳回可讀取的指令碼輸出。 無法執行的指令碼可能不會收到傳回的輸出。 



## <a name="boundary-group-fallback-for-management-points"></a>管理點的界限群組後援
<!-- 1324594 -->
從這個版本開始，您可以在[界限群組](../servers/deploy/configure/boundary-groups.md)之間設定管理點的後援關聯性。 此行為可為用戶端使用的管理點提供更好的控制。 在界限群組內容的 [關聯性]  索引標籤上，有個適用於管理點的新資料行。 當您新增新的後援界限群組時，管理點的後援時間目前一律為零 (0)。 此行為與站台預設界限群組上的**預設行為**一樣。

先前當您在安全網路中有受保護的管理點時，會發生一個常見的問題。 主要公司網路上的用戶端會收到包含這個受保護管理點的原則，即使它們無法跨越防火牆來與它通訊也一樣。 若要解決此問題，使用 [永不後援]  選項，以確保用戶端只會為它們可以通訊的管理點提供後援。

將站台升級至此版本時，Configuration Manager 會將所有非網際網路對向管理點新增至站台預設界限群組。 此升級行為確保舊版用戶端能夠繼續與管理點通訊。 為了充分利用此功能，請將您的管理點移至所需的界限群組。

管理點界限群組後援不會在用戶端安裝 (ccmsetup) 期間變更行為。 如果命令列未使用 /MP 參數來指定初始管理點，新的用戶端就會收到可用管理點的完整清單。 針對它的初始啟動程序流程，用戶端會使用它可存取的第一個管理點。 一旦用戶端向站台註冊之後，它就會收到依這個新行為正確排序的管理點清單。 

### <a name="prerequisites"></a>先決條件
- 啟用[慣用的管理點](../servers/deploy/configure/boundary-groups.md#bkmk_preferred)。 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  。 按一下功能區的 [階層設定]  。 在 [一般]  索引標籤上，啟用 [用戶端偏好使用界限群組中指定的管理點]  。 

### <a name="known-issues"></a>已知問題
- 作業系統部署程序並不知道界限群組。

### <a name="troubleshooting"></a>疑難排解
新的項目會出現在 **LocationServices.log** 中。 **位置**屬性會識別下列其中一種狀態：
- 0：Unknown
- 1：指定的管理點只位於適用於後援的站台預設界限群組
- 2：指定的管理點位於遠端或鄰近的界限群組。 當管理點同時位於鄰近和站台預設界限群組時，位置為 2。
- 3：指定的管理點位於本機或目前的界限群組。 當管理點位於目前的界限群組以及鄰近或站台預設界限群組時，位置為 3。 如果您未在階層設定中啟用慣用的管理點設定，位置一律為 3，而不論管理點位於哪一個界限群組。

用戶端會先使用本機管理點 (位置 3)、其次是遠端 (位置 2)，然後是後援 (位置 1)。 

當用戶端在 10 分鐘內收到五個錯誤，且無法與其目前界限群組中的管理點通訊時，它會嘗試聯繫鄰近或站台預設界限群組中的管理點。 如果目前界限群組中的管理點稍後重新上線，用戶端將在下一個重新整理週期返回本機管理點。 重新整理週期為 24 小時，或是當 Configuration Manager 代理程式服務重新啟動時。



## <a name="improved-support-for-cng-certificates"></a>已改善對 CNG 憑證的支援
<!-- 1357314 -->
Configuration Manager (最新分支) 1710 版支援[密碼編譯：新一代 (CNG) 憑證](../plan-design/network/cng-certificates-overview.md)。 1710 版會在數種案例中限制對用戶端憑證的支援。 

從這個 Technical Preview 版本開始，請針對下列支援 HTTPS 的伺服器角色使用 CNG 憑證：
- 管理點
- 發佈點
- 軟體更新點

[不支援的案例](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios)清單則維持不變。



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Azure Resource Manager 的雲端管理閘道支援
<!-- 1324735 -->
建立[雲端管理閘道](../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) 的執行個體時，精靈現在會提供選項來建立 **Azure Resource Manager 部署**。 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) 是可將所有解決方案資源當作單一實體 (稱為[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)) 來管理的新式平台。 使用 Azure Resource Manager 部署 CMG 時，站台會使用 Azure Active Directory (Azure AD) 來驗證並建立必要的雲端資源。 這個現代化的部署不需要傳統的 Azure 管理憑證。  

CMG 精靈仍會使用 Azure 管理憑證來提供**傳統服務部署**的選項。 若要簡化資源的部署與管理，我們建議針對所有新的 CMG 執行個體使用 Azure Resource Manager 部署模型。 如果可能，請透過 Resource Manager 重新部署現有的 CMG 執行個體。

Configuration Manager 不會將現有的傳統 CMG 執行個體移轉至 Azure Resource Manager 部署模型。 使用 Azure Resource Manager 部署來建立新的 CMG 執行個體，然後移除傳統的 CMG 執行個體。 

> [!IMPORTANT]
> 此功能不會啟用對 Azure 雲端服務提供者 (CSP) 的支援。 使用 Azure Resource Manager 的 CMG 部署會繼續使用 CSP 不支援的傳統雲端服務。 如需詳細資訊，請參閱 [Azure CSP 中可用的 Azure 服務](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services)。  

### <a name="prerequisites"></a>先決條件
- 與 [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) 整合。 不需要 Azure AD 使用者探索。
- 相同的[雲端管理閘道需求](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements)，但 Azure 管理憑證除外。

### <a name="try-it-out"></a>試試看！  
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 在 Configuration Manager 主控台的 [系統管理]  工作區中，展開 [雲端服務]  ，然後選取 [雲端管理閘道]  。 按一下功能區的 [建立雲端管理閘道]  。 
2. 在 [一般]  頁面上，選取 [Azure Resource Manager 部署]  。 按一下 [登入]  ，使用 Azure 訂用帳戶系統管理員帳戶進行驗證。 精靈會使用整合先決條件期間所儲存的 Azure AD 訂用帳戶資訊，自動填入其餘欄位。 如果您擁有多個訂用帳戶，請選取需要使用的訂用帳戶。 按一下 [下一步]  。  
3. 在 [設定]  頁面上，如往常般提供伺服器 PKI 憑證檔案。 此憑證會定義 Azure 中的 CMG 服務名稱。 選取 [區域]  ，然後針對資源群組選項選取 [新建]  或 [使用現有的]  。 輸入新的資源群組名稱，或從下拉式清單中選取現有的資源群組。 
4. 完成精靈。

> [!NOTE] 
> 針對選取的 Azure AD 伺服器應用程式，Azure 會指派訂用帳戶**參與者**權限。 

在服務連接點上，使用 **cloudmgr.log** 監視服務部署進度。



## <a name="approve-application-requests-for-users-per-device"></a>針對每個裝置的使用者核准應用程式要求
<!-- 1357015 -->
從這個版本開始，當使用者要求需要核准的應用程式時，特定的裝置名稱現在為要求的一部分。 如果系統管理員核准要求，使用者就只能在該裝置上安裝應用程式。 使用者必須提交其他要求，才能在其他裝置上安裝應用程式。 

> [!NOTE]
> 此功能是選擇性的。 更新至此版本時，請在更新精靈中啟用此功能。 或者，稍後在主控台中啟用此功能。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../servers/manage/install-in-console-updates.md#bkmk_options)。

### <a name="prerequisites"></a>先決條件
- 將 Configuration Manager 用戶端升級至最新版本
- 在[電腦代理程式](../clients/deploy/about-client-settings.md#computer-agent)群組中啟用**使用新的軟體中心**用戶端設定

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 將可用的應用程式部署至使用者集合。
2. 在 [部署設定]  頁面上，啟用下列選項：**系統管理員必須在裝置上核准此應用程式要求**。
3. 身為目標使用者，請使用軟體中心來提交應用程式的要求。 
4. 在 Configuration Manager 主控台的 [軟體程式庫]  工作區中，檢視 [應用程式管理]  下的 [核准要求]  。 目前在適用於每個要求的清單中都會有一個**裝置**資料行。 當您針對要求採取動作時，[應用程式要求] 對話方塊也會包含使用者從中提交要求的裝置名稱。



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>在已加入 Azure AD的裝置上使用軟體中心瀏覽和安裝使用者可用的應用程式
<!-- 1322613 -->
如果您將可用的應用程式部署至使用者，他們現在就能在 Azure Active Directory (Azure AD) 裝置上，透過軟體中心瀏覽和安裝這些應用程式。  

### <a name="prerequisites"></a>先決條件
- 在管理點上啟用 HTTPS
- 將站台與 [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) 整合
- 將可用的應用程式部署至使用者集合
- 將任何應用程式內容發佈至[雲端發佈點](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- 在[電腦代理程式](../clients/deploy/about-client-settings.md#computer-agent)群組中啟用**使用新的軟體中心**用戶端設定
- 用戶端必須是： 
   - Windows 10
   - 已加入 Azure AD，也稱為已加入雲端網域
- 支援以網際網路為基礎的用戶端：
    - [雲端管理閘道](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - 啟用用戶端設定：[用戶端原則](../clients/deploy/about-client-settings.md#client-policy)群組中的 [從網際網路用戶端啟用使用者原則要求] 
- 支援公司網路上的用戶端：
    - 將雲端發佈點新增至用戶端所使用的界限群組
    - 用戶端必須能夠解析支援 HTTPS 之管理點的完整網域名稱 (FQDN)



## <a name="report-on-windows-autopilot-device-information"></a>報告 Windows AutoPilot 裝置資訊
<!-- 1351442 -->
Windows AutoPilot 是使用新式方法來將新的 Windows 10 裝置上架並加以設定的解決方案。 如需詳細資訊，請參閱 [Windows AutoPilot 概觀](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)。 向 Windows AutoPilot 註冊現有裝置的方法之一是，將裝置資訊上傳至商務用和教育用的 Microsoft 網上商店。 此資訊包括裝置序號、Windows 產品識別碼及硬體識別碼。 使用 Configuration Manager 來收集和報告此裝置資訊。 

### <a name="prerequisites"></a>先決條件
- 此裝置資訊僅適用於 Windows 10 1703 版及更新版本上的用戶端

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 在 Configuration Manager 主控台的 [監視]  工作區中，依序展開 [報表]  節點和 [報表]  ，然後選取 [硬體 - 一般]  節點。
2. 執行新的報表 **Windows AutoPilot 裝置資訊**，然後檢視結果。 
3. 在報表檢視器中按一下**匯出**圖示，然後選取 [CSV (逗號分隔)]  選項。
4. 儲存檔案之後，將資料上傳至商務用和教育用的 Microsoft 網上商店。 如需詳細資訊，請參閱[在商務用和教育用的 Microsoft 網上商店新增裝置](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)。 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>適用於 Windows Defender 惡意探索防護之 Configuration Manager 原則的改善
<!-- 1356220 -->
針對 [Windows Defender 惡意探索防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)，已在 Configuration Manager 中新增適用於攻擊面縮減和受控資料夾存取權元件的額外原則設定。

**適用於受控資料夾存取權的新設定**<br/>
當您設定受控資料夾存取權時有兩個其他選項：[僅封鎖磁碟磁區]  和 [僅稽核資料磁區]  。 這兩個設定只允許針對開機磁區啟用受控資料夾存取權，而且不會啟用特定資料夾或預設受保護資料夾的保護。 

**適用於攻擊面縮減的新設定**
- 使用進階防護來防範勒索軟體。
- 封鎖從 Windows 本機安全性授權子系統竊取認證。 
- 封鎖可執行檔執行，除非它們符合普遍性、存留期或信任的清單準則。 
- 封鎖從 USB 執行的不受信任和未簽署的程序。



## <a name="microsoft-edge-browser-policies"></a>Microsoft Edge 瀏覽器原則
<!-- 1357310 -->
針對在 Windows 10 用戶端上使用 [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) 網頁瀏覽器的客戶，您現在可以建立 Configuration Manager 合規性設定原則來設定數個 Microsoft Edge 設定。 此原則目前包含下列設定：
- **將 Microsoft Edge 瀏覽器設為預設值**：將適用於網頁瀏覽器的 Windows 10 預設應用程式設定設為 Microsoft Edge
- **允許網址列下拉式清單**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [AllowAddressBarDropdown 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)。
- **允許同步 Microsoft 瀏覽器之間的我的最愛**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [SyncFavoritesBetweenIEAndMicrosoftEdge 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)。
- **允許在結束時清除瀏覽資料**：需要 Windows 10 (1703 版或更新版本)。 如需詳細資訊，請參閱 [ClearBrowsingDataOnExit 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)。
- **允許「不要追蹤」標頭**：如需詳細資訊，請參閱 [AllowDoNotTrack 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)。
- **允許自動填入**：如需詳細資訊，請參閱 [AllowAutofill 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)。
- **允許 Cookie**：如需詳細資訊，請參閱 [AllowCookies 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)。
- **允許快顯封鎖程式**：如需詳細資訊，請參閱 [AllowPopups 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)。
- **允許網址列的搜尋建議**：如需詳細資訊，請參閱 [AllowSearchSuggestionsinAddressBar 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)。
- **允許將內部網路流量傳送到 Internet Explorer**：如需詳細資訊，請參閱 [SendIntranetTraffictoInternetExplorer 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)。
- **允許密碼管理員**：如需詳細資訊，請參閱 [AllowPasswordManager 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)。
- **允許開發人員工具**：如需詳細資訊，請參閱 [AllowDeveloperTools 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)。
- **允許延伸模組**：如需詳細資訊，請參閱 [AllowExtensions 瀏覽器原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)。

### <a name="prerequisites"></a>先決條件
- 已加入 Azure Active Directory 的 Windows 10 用戶端。 

### <a name="known-issues"></a>已知問題
- 已加入內部部署網域的裝置無法在此版本中套用此原則。 此問題也會與已加入混合式網域的裝置有關。

### <a name="try-it-out"></a>試試看！  
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

**建立原則**
1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 展開 [合規性設定]  ，然後選取新的 **Microsoft Edge 瀏覽器設定檔**節點。 按一下功能區選項以**建立 Microsoft Edge 瀏覽器原則**。
2. 指定原則的**名稱**、選擇性地輸入**描述**，然後按一下 [下一步]  。
3. 在 [設定]  頁面上，針對要包含在此原則中的設定來將值變更為 [已設定]  ，然後按一下 [下一步]  。
4. 在 [支援的平台]  頁面上，選取要套用此原則的作業系統版本和架構，然後按一下 [下一步]  。 
5. 完成精靈。

**部署原則**
1. 選取您的原則，然後按一下功能區選項以**部署**。
2. 按一下 [瀏覽]  ，以選取要部署原則的使用者或裝置集合。 
3. 視需要選取其他選項。 當原則不符合規範時產生警示。 設定用戶端使用此原則來評估裝置合規性的排程。
4. 按一下 [確定]  以建立部署。

就像任何合規性設定原則，用戶端會按照您指定的排程來修復設定。 在 Configuration Manager 主控台中[監視和報告裝置合規性](../../compliance/deploy-use/monitor-compliance-settings.md)。



## <a name="report-for-default-browser-counts"></a>報告預設瀏覽器計數
<!-- 1357830 -->
現在有一份新報表，可顯示使用特定網頁瀏覽器作為 Windows 預設值之用戶端的計數。 

### <a name="known-issues"></a>已知問題
- 當您第一次開啟此報表時，它只會顯示計數，而不會顯示 BrowserProgID。 若要解決此問題，請以下列語法編輯報表的查詢：  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>試試看！  
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。
1. 在 **Configuration Manager** 主控台的 [監視]  工作區中，依序展開 [報表]  和 [報表]  ，然後選取 [軟體 - 公司與產品]  。
2. 執行 [預設瀏覽器計數]  報表。

針對一般 BrowserProgID 使用下列參考：
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**：Microsoft Edge
- **IE.HTTP**：Microsoft Internet Explorer
- **ChromeHTML**：Google Chrome
- **OperaStable**：Opera Software
- **FirefoxURL-308046B0AF4A39CB**：Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>支援 Windows 10 ARM64 裝置
<!-- 1353704 -->
從這個版本開始，Windows 10 ARM64 裝置上便支援 Configuration Manager 用戶端。 現有的用戶端管理功能應該可以使用這些新的裝置來運作。 例如，硬體和軟體清查、軟體更新以及應用程式管理。 目前不支援作業系統部署。 

## <a name="changes-to-phased-deployments"></a>對分階段部署所做的變更
<!-- 1357405 -->
分階段部署可在多個集合中，將協調且循序的軟體推出作業自動化。 在這個 Technical Preview 版本中，您可以在管理主控台中針對工作順序完成分階段部署精靈，並建立部署。 不過，第二個階段不會在滿足第一個階段的成功準則之後自動開始。 您可以使用 SQL 陳述式，手動開始第二個階段。   

### <a name="try-it-out"></a>試試看！  
  請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。
 
**建立工作順序的分階段部署** </br>
1. 在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  。
2. 以滑鼠右鍵按一下現有的工作順序，然後選取 [Create Phased Deployment] \(建立分階段部署)  。 
3. 在 [一般]  索引標籤上，指定分階段部署的名稱、描述 (選擇性)，然後選取 [自動建立預設的兩階段部署]  。 
4. 填入 [第一個集合]  和 [第二個集合]  欄位。 選取 [下一步]  。
5. 在 [設定]  索引標籤上，針對每個排程設定選擇一個選項，然後在完成時選取 [下一步]  。 
6. 在 [階段]  索引標籤上，視需要編輯任一階段，然後按一下 [下一步]  。
7. 在 [摘要]  索引標籤上確認您的選擇，然後按一下 [下一步]  繼續進行。
8. 已達到第一個階段的成功準則時，請按照指示，使用 SQL 陳述式來開始第二個階段。
 
**使用 SQL 陳述式來開始第二個階段**
1. 識別您使用下列 SQL 查詢所建立之部署的 PhasedDeploymentID：<br/> `Select * from PhasedDeployment`
2. 執行下列陳述式以開始生產階段：<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
