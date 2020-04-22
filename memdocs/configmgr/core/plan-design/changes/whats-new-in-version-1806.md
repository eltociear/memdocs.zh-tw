---
title: 1806 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 最新分支 1806 版中變更和所引進新功能的詳細資料。
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 295940337f191b791d8c7a86de4003466213df6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702336"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Configuration Manager 最新分支 1806 版的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 最新分支的 1806 更新可以透過主控台內更新的方式取得。 在執行 1706、1710 或 1802 版的站台上套用此更新。 <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

請一律檢閱適用於安裝此更新的最新檢查清單。 如需詳細資訊，請參閱[安裝更新 1806 的檢查清單](../../servers/manage/checklist-for-installing-update-1806.md)。 更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist)。

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

下列各節提供 Configuration Manager 最新分支 1806 版中變更和新功能的詳細資料。  



## <a name="deprecated-features-and-operating-systems"></a>已淘汰的功能和作業系統

在[已移除和已取代的項目](deprecated/removed-and-deprecated.md)中實作支援變更之前，請先了解這些變更。

自 2018 年 8 月 14 日起，混合式行動裝置管理功能已淘汱。 如需詳細資訊，請參閱[混合式 MDM 有哪些改變？](../../../mdm/understand/what-happened-to-hybrid.md)。<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>站台基礎結構

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager 一律提供大型中央裝置資料存放區，供客戶處理報表時使用。 站台通常會每週收集此資料。 CMPivot 是新的主控台內公用程式，現在可存取環境中裝置的即時狀態。 它能立即在目標集合中，所有目前已連線的裝置上執行查詢，然後傳回結果。 然後，您可以使用這個工具來篩選此資料並進行分組。 提供線上用戶端的即時資料，讓您更快速地回答事務問題、解決問題，並回應安全性事件。 

如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md)。  


### <a name="site-server-high-availability"></a>站台伺服器的高可用性
<!--1128774-->
獨立主要站台伺服器角色的高可用性是一個以 Configuration Manager 為基礎的解決方案，能夠安裝被動模式的額外站台伺服器。 被動模式的站台伺服器，是您在主動模式之現有站台伺服器以外的站台伺服器。 被動模式的站台伺服器可在有需要時立即使用。 

如需詳細資訊，請參閱下列文章： 
- [站台伺服器的高可用性](../../servers/deploy/configure/site-server-high-availability.md) 
- [流程圖 - 設定被動模式的站台伺服器](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [流程圖 - 將站台伺服器升階 (已規劃)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [流程圖 - 將站台伺服器升階 (未規劃)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>管理見解的改善
此版本包含下列管理見解改善：  

- 某些管理見解現在可以選擇採取動作。 此動作正在主控台中巡覽至相關聯節點，或顯示篩選過的查詢型檢視。<!--1357930-->  

- 主動式維護這個新群組具有六個新的規則，協助突顯潛在設定問題來避免定期維護費。<!--1352184-->  

如需詳細資訊，請參閱[管理見解](../../servers/manage/management-insights.md)。


### <a name="configuration-manager-tools"></a>Configuration Manager 工具
<!--1357145-->
Configuration Manager 伺服器和用戶端工具現在已包含在伺服器上。 在站台伺服器的 `CD.Latest\SMSSETUP\Tools` 資料夾中找到它們。 不需要採取進一步的安裝。 

如需詳細資訊，請參閱 [Configuration Manager 工具](../../support/tools.md)。


### <a name="exclude-active-directory-containers-from-discovery"></a>從探索排除 Active Directory 容器
<!--1358143-->
若要減少探索到的物件數目，請從 Active Directory 系統探索排除特定容器。 

如需詳細資訊，請參閱[設定 Active Directory 系統探索](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd)。



## <a name="content-management"></a>內容管理

### <a name="configure-a-remote-content-library-for-the-site-server"></a>針對站台伺服器設定遠端內容庫
<!--1357525-->
若要設定站台伺服器高可用性，或釋出您管理中心或主要站台伺服器上的硬碟空間，請將內容庫重新定位到另一個儲存位置。 將內容庫移至站台伺服器上的另一個磁碟機、個別的伺服器，或是存放區域網路 (SAN) 上的容錯磁碟。 

如需詳細資訊，請參閱下列文章： 
- [內容庫](../hierarchy/the-content-library.md)
- [流程圖 - 管理內容庫](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Azure Resource Manager 的支援雲端發佈點支援
<!--1322209-->
建立雲端發佈點時，精靈現在會提供建立 [Azure Resource Manager deployment]  \(Azure Resource Manager 部署\)的選項。 Azure Resource Manager 是可將所有解決方案資源當作單一實體 (稱為資源群組) 來管理的新式平台。 使用 Azure Resource Manager 部署雲端發佈點時，站台會使用 Azure Active Directory 來驗證並建立必要的雲端資源。 這個現代化的部署不需要傳統的 Azure 管理憑證。 

也會修改並增強雲端發佈點的功能文件。 如需詳細資訊，請參閱下列文章：
- [使用雲端發佈點](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [安裝雲端發佈點](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>提取發佈點支援以雲端發佈點作為來源  
<!--1321554-->
許多客戶在遠端或分公司使用提取發佈點，其會經由 WAN 從來源發佈點下載內容。 如果您的遠端辦公室有較佳的網際網路連線，或是若要降低 WAN 連結上的負載，現在可以使用 Microsoft Azure 中的雲端發佈點作為來源。 當您在發佈點屬性的 [提取發佈點]  索引標籤上新增來源時，站台中所有雲端發佈點現在都會列為可用的發佈點。 除此之外，兩個站台系統角色的行為都保持不變。 

如需詳細資訊，請參閱[使用提取發佈點](../hierarchy/use-a-pull-distribution-point.md)。


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>啟用要使用網路壅塞控制的發佈點
<!--1358112-->
Windows 低額外延遲背景傳輸 (LEDBAT) 是 Windows Server 的一個功能，能協助管理背景網路傳輸。 針對所支援 Windows Server 版本上執行的發佈點，啟用一個選項來協助調整網路流量。 有的話，用戶端只會使用網路頻寬。 

如需詳細資訊，請參閱 [Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat)。


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>用戶端對等快取支援部分下載以降低 WAN 使用量
<!--1357346-->
用戶端對等快取來源現在可以將內容分割成組件。 這些組件會將網路傳輸減到最少以降低 WAN 使用量。 管理點可提供內容組件的更詳細追蹤。 它會嘗試排除對每一界限群組的相同內容進行多重下載的情況。 

如需詳細資訊，請參閱[部分下載支援](../hierarchy/client-peer-cache.md#bkmk_parts)。 


### <a name="boundary-group-options-for-peer-downloads"></a>適用於對等下載的界限群組選項
<!--1356193-->
界限群組現在包含其他設定，使您更能掌握環境中的內容發佈。 此版本新增下列選項：  

- **允許此界限群組中的對等下載**：管理點會為用戶端提供內容位置清單，其中包含對等來源。 此設定也會影響套用傳遞最佳化的群組識別碼。  

- **對等下載期間，僅使用相同子網路中的對等**：管理點只會包含於內容位置清單對等來源中，而這些來源位於與用戶端相同的子網路。  

如需詳細資訊，請參閱[適用於對等下載的界限群組選項](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)。


### <a name="improvement-to-peer-cache-source-location-status"></a>對等快取來源位置狀態改善
<!--SCCMDocs issue 850-->
Configuration Manager 在判斷對等快取來源是否已漫遊到另一個位置的效率更高。 此行為可確保管理點將它當作內容來源提供給新位置 (而非舊位置) 的用戶端。 如果您使用對等快取功能並搭配漫遊對等快取來源，將站台更新至 1806 版之後，也請將所有對等快取來源更新至最新的用戶端版本。 在更新至最新版 1806 之前，管理點不會在內容位置清單中包含這些對等快取來源。

如需詳細資訊，請參閱[對等快取的需求](../hierarchy/client-peer-cache.md#requirements)。



<!-- ## Migration  -->



## <a name="client-management"></a>用戶端管理

### <a name="improvement-to-client-push-security"></a>用戶端推送安全性改善
<!--1358204-->
使用用戶端推送方法安裝 Configuration Manager 用戶端時，站台現在可以要求 Kerberos 相互驗證。 此增強功能有助於保護伺服器和用戶端之間的通訊。 

如需詳細資訊，請參閱[如何使用用戶端推入來安裝用戶端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a> 增強的 HTTP 站台系統
<!--1356889,1358228-->
建立所有 Configuration Manager 通訊路徑都使用 HTTPS 通訊，不過管理 PKI 憑證需付出額外的人力物力，對於某些客戶而言實難以辦到。

此版本在用戶端與網站系統通訊方面，增強很多的功能。 在站台屬性 [用戶端電腦通訊]  索引標籤上，選取 [HTTPS] 或 [HTTP]  選項，然後啟用新選項 [Use Configuration Manager-generated certificates for HTTP site systems] \(讓 HTTP 站台系統使用 Configuration Manager 產生的憑證\)  。 此功能是[發行前版本功能](../../servers/manage/pre-release-features.md)。

如需詳細資訊，請參閱[Enhanced HTTP](../hierarchy/enhanced-http.md) (增強 HTTP)。


### <a name="azure-ad-device-identity"></a>Azure AD 裝置身分識別 
<!--1358460-->
[加入 Azure AD](/azure/active-directory/devices/concept-azure-ad-join) 或沒有任何 Azure AD 使用者登入的[混合式 Azure AD 裝置](/azure/active-directory/devices/concept-azure-ad-join-hybrid)，可以安全地與其指派站台通訊。 現在只要有雲端裝置識別，便能到 CMG 和管理點進行驗證。  

如需詳細資訊，請參閱[Enhanced HTTP](../hierarchy/enhanced-http.md) (增強 HTTP)。


### <a name="cmtrace-installed-with-client"></a>與用戶端一起安裝的 CMTrace
<!--1357971-->
CMTrace 檢視工具現在會與 Configuration Manager 用戶端一起自動安裝。 它會被新增至用戶端安裝目錄，根據預設，就是 `%WinDir%\ccm\cmtrace.exe`。 

如需詳細資訊，請參閱 [CMTrace](../../support/cmtrace.md)。


### <a name="cloud-management-dashboard"></a>雲端管理儀表板
<!--1358461-->
新的雲端管理儀表板提供雲端管理閘道 (CMG) 使用量的集中式檢視。 當站台配合 Azure AD 時，它也會顯示雲端使用者和裝置相關資料。   

這項功能也包括 **CMG 連線分析器**，它能即時驗證，以協助解決問題。 主控台內的公用程式會檢查目前狀態的服務，以及檢查 CMG 連接點與任何允許 CMG 流量的管理點，二者之間通訊頻道。 

如需詳細資訊，請參閱[監視 CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md) 的下列章節：  
- [雲端管理儀表板](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [連接分析器](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>雲端管理閘道的改進

1806 版包含下列雲端管理閘道 (CMG) 改善：

#### <a name="simplified-client-bootstrap-command-line"></a>簡化的用戶端啟動程序命令列
<!--1358215-->
透過 CMG 在網際網路上安裝 Configuration Manager 用戶端時，命令列現在需要較少的屬性。 這項改善可減少準備共同管理時，在 Microsoft Intune 中所使用的命令列大小。 

如需詳細資訊，請參閱[如何準備網路型裝置進行共同管理](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)。

#### <a name="download-content-from-a-cmg"></a>從 CMG 下載內容
<!--1358651-->
之前，您必須將雲端發佈點和 CMG 部署為不同的角色。 CMG 現在也可以將內容提供給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。 

如需詳細資訊，請參閱[修改 CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)。

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>使用 Azure AD 時不需要受信任的根憑證
<!--503899-->
當您建立 CMG 時，不再需要於 [設定] 頁面上提供[受信任的根憑證](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot)。 使用 Azure Active Directory (Azure AD) 進行用戶端驗證時，不需要此憑證，但以前在精靈中需要此憑證。 如果您要使用 PKI 用戶端驗證憑證，則仍然必須將受信任的根憑證新增至 CMG。



## <a name="co-management"></a>共同管理

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>從 Microsoft Intune 為共同受控裝置同步處理 MDM 原則
<!--1357377-->
當您切換共同管理工作負載時，共同受控裝置就會從 Microsoft Intune 自動同步處理 MDM 原則。 當您在 Configuration Manager 主控台中從 [用戶端通知] 起始 [下載電腦原則]  動作時，也會進行這項同步處理作業。 

如需詳細資訊，請參閱[如何將 Configuration Manager 工作負載切換至 Intune](../../../comanage/how-to-switch-workloads.md)。


### <a name="transition-new-workloads-to-intune-using-co-management"></a>使用共同管理將新的工作負載轉換至 Intune
在啟用共同管理之後，下列工作負載現在可以從 Configuration Manager 轉換至 Intune：  

- **裝置設定**<!--1357903-->:此工作負載可讓您使用 Intune 部署 MDM 原則，同時繼續使用 Configuration Manager 部署應用程式。  

- **Office 365**<!--1357841-->:裝置不會從 Configuration Manager 安裝 Office 365 部署。  

- **行動應用程式**<!--1357892-->:從 Intune 部署的所有可用應用程式都可以在公司入口網站中使用。 您從 Configuration Manager 部署的應用程式可在軟體中心使用。 此功能是[發行前版本功能](../../servers/manage/pre-release-features.md)。  

若要轉換這些工作負載，請前往共同管理屬性頁面，然後將工作負載滑動軸從 [Configuration Manager] 移至 [試驗]  或 [全部]  。 

如需詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../../comanage/overview.md)。


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>一個 Intune 租用戶有多個階層的支援
<!--1357944-->
有些客戶會有數個 Configuration Manager 階層，而且未來想要合併至 Azure Active Directory 和 Microsoft Intune 的單一租用戶。 共同管理現在支援將多個 Configuration Manager 環境連線至相同的 Intune 租用戶。

如需詳細資訊，請參閱[共同管理必要條件](../../../comanage/overview.md#prerequisites)。
 


## <a name="compliance-settings"></a>相容性設定

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>設定 Microsoft Edge 的 Windows Defender SmartScreen 設定
<!--1353701-->
Microsoft Edge 瀏覽器合規性設定原則新增下列三個 Windows Defender SmartScreen 設定： 
- 允許 SmartScreen
- 使用者可以覆寫站台的 SmartScreen 提示
- 使用者可以覆寫檔案的 SmartScreen 提示

如需詳細資訊，請參閱[設定 Microsoft Edge 設定](../../../compliance/deploy-use/browser-profiles.md)。


### <a name="scap-extensions"></a>SCAP 延伸模組
<!--1357552-->
將安全性內容自動化通訊協定 (SCAP) 內容轉換成合規性設定基準，並使用主控台延伸模組產生 SCAP 報表。 此功能也包含新的儀表板，以視覺化方式顯示用戶端合規性和 XCCDF 規則合規性。 





## <a name="application-management"></a>應用程式管理

### <a name="phased-deployment-of-applications"></a>應用程式的階段式部署
<!--1358147-->
建立應用程式的階段式部署。 階段式部署可讓您根據可自訂的準則與群組，以組織協調且循序的軟體推出。 例如，將應用程式部署至試驗集合，然後根據成功準則自動繼續推出。 

如需詳細資訊，請參閱下列文章：  

- [建立階段式部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [管理及監視階段式部署](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>為裝置上的所有使用者佈建 Windows 應用程式套件
<!--1358310-->
針對裝置上的所有使用者，使用 Windows 應用程式套件佈建應用程式。 此案例的其中一個常見範例是從商務用和教育用 Microsoft Store，向學校學生所使用的所有裝置佈建應用程式，例如 Minecraft：教育版。 之前，Configuration Manager 只支援針對每位使用者安裝這些應用程式。 在登入新裝置之後，學生就必須等候存取應用程式。 現在，應用程式會針對所有使用者佈建到裝置，讓他們能夠更快速地提高生產力。 

如需詳細資訊，請參閱[建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md#bkmk_provision)。


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office 自訂工具與 Office 365 安裝程式整合
<!--1358149-->
Office 自訂工具現在已於 Configuration Manager 主控台中與 Office 365 安裝程式整合。 為 Office 365 建立部署時，請動態設定最新的 Office 管理能力設定。 Microsoft 在發行新的 Office 365 組建時會更新 Office 自訂工具。 一旦推出新的管理能力設定，這項整合就可讓您立即在 Office 365 中利用這些設定。 

如需詳細資訊，請參閱[部署 Office 365 應用程式](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps)。


### <a name="support-for-new-windows-app-package-formats"></a>支援新的 Windows 應用程式套件格式
<!--1357427-->
Configuration Manager 現在支援部署新的 Windows 10 應用程式套件 (.msix) 與應用程式套件組合 (.msixbundle) 格式。 

如需詳細資訊，請參閱[建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md#bkmk_msix)。


### <a name="uninstall-application-on-approval-revocation"></a>在核准撤銷時解除安裝應用程式
<!--1357891-->
您撤銷應用程式核准時的行為已經變更。 現在，當您拒絕應用程式的要求時，用戶端會從使用者的裝置解除安裝該應用程式。 此行為需要您啟用 [依據裝置為使用者核准應用程式要求]  [選用功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。 

如需詳細資訊，請參閱[部署應用程式](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)。


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
套件轉換管理員現在是一個整合工具，可讓您將舊版套件轉換為 Configuration Manager 最新分支應用程式。 接著，您便可以使用應用程式的功能，例如相依性、需求規則和使用者裝置親和性。

如需詳細資訊，請參閱[套件轉換管理員](../../../apps/pcm/package-conversion-manager.md)。



## <a name="os-deployment"></a>OS 部署

### <a name="improvements-to-phased-deployments"></a>階段式部署的改善

此版本包含下列階段式部署改善：  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>建立具有手動設定階段的階段式部署
<!--1358148-->
針對工作順序，現在會在您建立階段式部署時手動設定階段。 從 [建立階段式部署精靈] 的 [階段]  索引標籤，新增多達 10 個額外階段。 您仍然可以自動建立預設的兩階段部署。 

如需詳細資訊，請參閱[建立具有手動設定階段的階段式部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual)。

#### <a name="phased-deployment-status"></a>階段式部署狀態
<!--1358577-->
階段式部署現在具有原生的監視體驗。 從 [監視]  工作區中的 [部署]  節點，選取階段式部署，然後按一下功能區中的 [階段式部署狀態]  。 

如需詳細資訊，請參閱[管理和監視階段式部署](../../../osd/deploy-use/manage-monitor-phased-deployments.md)。  

#### <a name="gradual-rollout-during-phased-deployments"></a>在階段式部署期間逐步推出
<!--1358578-->
在階段式部署期間，現在可在每個階段中逐步推出。 此行為有助於減緩部署問題的風險，並降低因將內容發佈到用戶端而導致的網路負載。 依據每個階段的設定而定，站台可以逐步開放軟體以供使用。 階段中的每個用戶端都有一個相對於軟體可供使用時間的期限。 可用時間與期限之間的時間範圍，對於階段中的所有用戶端而言都一樣。 

如需詳細資訊，請參閱[階段設定](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings)。  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 就地升級工作順序的改善
<!--1358500-->
Windows 10 就地升級的預設工作順序範本，現在包含其他群組並附帶新增的建議動作，以防萬一升級程序失敗。 有了這些動作，解決問題就簡單多了。 Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) 就是這種工具之一。 它是獨立診斷工具，可用來取得 Windows 10 升級為何失敗的詳細資料。 

如需詳細資訊，請參閱[建立工作順序以升級作業系統](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure)。


### <a name="improvements-to-pxe-enabled-distribution-points"></a>支援 PXE 的發佈點改善
<!--1357580-->
在發佈點內容的 [PXE]  索引標籤上，核取 [在不使用 Windows 部署服務的情況下啟用 PXE 回應程式]  。 這個新選項會啟用發佈點上的 PXE 回應程式，而不需要 Windows 部署服務 (WDS)。 因為 WDS 並非必要，所以啟用 PXE 的發佈點可以是用戶端或伺服器作業系統 (包含 Windows Server Core)。 這個新的 PXE 回應程式服務支援 IPv6，而且也會強化遠端辦公室中支援 PXE 之發佈點的彈性。 

如需詳細資訊，請參閱[在發佈點上啟用 PXE](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。


### <a name="network-access-account-not-required-for-some-scenarios"></a>在某些情況下不需要網路存取帳戶
<!--1358278,1358279-->
[增強 HTTP 站台系統](#bkmk_ehttp)功能也會移除與網路存取帳戶的一些相依性。 當您啟用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  的新站台選項時，下列案例不需要網路存取帳戶即可從發佈點下載內容：  

- 從開機媒體或 PXE 執行的工作順序
- 從軟體中心執行的工作順序  

這些工作順序可以是 OS 部署或自訂。 它也支援工作群組電腦。

如需詳細資訊，請參閱[工作順序和網路存取帳戶](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount)。


### <a name="other-improvements-to-os-deployment"></a>其他 OS 部署改善

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>遮罩儲存在工作順序變數中的敏感性資料
 <!--1358330-->
 在**設定工作順序變數**步驟中，選取 [不要顯示此值]  的新選項。 

 如需詳細資訊，請參閱[設定工作順序變數](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)。 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>在工作順序的「執行命令」步驟期間遮罩程式名稱
 <!--1358493-->
 若要防止顯示或記錄潛在的敏感性資料，請設定工作順序變數 **OSDDoNotLogCommand**。  

 如需詳細資訊，請參閱[工作順序變數](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand)。 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>安裝驅動程式時 DISM 參數的工作順序變數
 <!--516679/2840016-->
 若要指定 DISM 的其他命令列參數，請使用新的工作順序變數 **OSDInstallDriversAdditionalOptions**。 

 如需詳細資訊，請參閱[工作順序變數](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions)。 

#### <a name="option-to-use-full-disk-encryption"></a>使用完整磁碟加密的選項
 <!--SCCMDocs-pr issue 2671-->
 **啟用 BitLocker** 和**預先佈建 BitLocker** 步驟現在包含 [Use full disk encryption]  \(使用完整磁碟加密\) 的選項。 根據預設，這些步驟會加密磁碟機上的已使用空間。 建議使用此預設行為，因為它的速度更快且更具效率。 

 如需詳細資訊，請參閱[啟用 BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) 和[預先佈建 BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker)。 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>用戶端佈建模式無法使用 Windows 10 升級相容性掃描來啟用
 <!--SCCMDocs-pr issue 2812-->
 現在當您啟用 [執行 Windows 安裝程式相容性掃描但不啟動升級]  選項時，**升級作業系統**工作順序步驟不會使 Configuration Manager 用戶端進入佈建模式。

 如需詳細資訊，請參閱[升級作業系統](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)。

#### <a name="revised-documentation-for-task-sequence-variables"></a>工作順序變數的修訂文件
目前提供兩篇新文章來了解工作順序變數：  

- [如何使用工作順序變數](../../../osd/understand/using-task-sequence-variables.md)是一篇新文章，其中說明不同類型的變數、設定變數的方法，以及如何存取它們的方式。  

- [工作順序變數](../../../osd/understand/task-sequence-variables.md)為適用於所有可用工作順序變數的參考。 這篇文章結合了先前會將內建變數與動作變數分隔開來的文章。 



## <a name="software-center"></a>軟體中心

> [!Important]  
> 若要利用 Configuration Manager 的新功能，請先將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。


### <a name="software-center-infrastructure-improvements"></a>軟體中心基礎結構改善
<!--1358309-->
不再需要應用程式類別目錄角色，就能在軟體中心顯示使用者可用的應用程式。 這項變更可協助您減少將應用程式傳遞給使用者所需的伺服器基礎結構。 軟體中心現在依賴管理點來取得這項資訊，這可透過將更大型的環境指派給[界限群組](../../servers/deploy/configure/boundary-groups.md#management-points)，協助這些環境更適當地調整大小。

如需詳細資訊，請參閱[設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

> [!Note]  
> 1806 中不再「需要」  應用程式類別目錄網站點和 Web 服務點角色，但它們仍為「支援的」  角色。 
> 
> 不再支援應用程式類別目錄網站點的 **Silverlight 使用者體驗**。 如需詳細資訊，請參閱[已移除和已淘汰的功能](deprecated/removed-and-deprecated-cmfeatures.md)。  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>在軟體中心中指定應用程式類別目錄網站連結的可見性
<!--1358214-->
使用用戶端設定，控制是否要將 [開啟應用程式類別目錄網站]  連結顯示在軟體中心的 [安裝狀態]  節點中。  

如需詳細資訊，請參閱[軟體中心用戶端設定](../../clients/deploy/about-client-settings.md#software-center)。

> [!Note]  
> 不再支援應用程式類別目錄網站點的 **Silverlight 使用者體驗**。 如需詳細資訊，請參閱[已移除和已淘汰的功能](deprecated/removed-and-deprecated-cmfeatures.md)。  


### <a name="custom-tab-for-webpage-in-software-center"></a>軟體中心內網頁的自訂索引標籤
<!--1358132-->
使用用戶端設定，建立自訂索引標籤以在軟體中心開啟網頁。 此功能可讓您以一致且可靠的方式向使用者顯示內容。 以下清單包括幾個範例：  

- 連絡 IT：有關如何連絡組織 IT 部門的資訊  

- IT 支援中心：IT 自助動作，例如搜尋知識庫或開立支援票證。  

- 使用者文件：適用於組織內使用者的各種 IT 主題 (例如使用應用程式或升級至 Windows 10) 相關文章。  

如需詳細資訊，請參閱[軟體中心用戶端設定](../../clients/deploy/about-client-settings.md#software-center)和[軟體中心使用者指南](../../understand/software-center.md)。


### <a name="maintenance-windows-in-software-center"></a>軟體中心內的維護時間範圍
<!--1358131-->
「軟體中心」現在會顯示下一個排定的維護時間範圍。 在 [安裝狀態] 索引標籤上，將檢視從 [全部] 切換成 [預定進行]。 它會顯示時間範圍和已排定的部署清單。 如果沒有任何未來的維護時間範圍，此清單就會空白。 

如需詳細資訊，請參閱[如何使用維護時間範圍](../../clients/manage/collections/use-maintenance-windows.md)和[軟體中心使用者指南](../../understand/software-center.md)。



## <a name="software-updates"></a>軟體更新

### <a name="third-party-software-updates"></a>協力廠商軟體更新
<!--1357605, 1352101, 1358714-->
協力廠商軟體更新可讓您在 Configuration Manager 主控台中訂閱合作夥伴類別目錄，以及將更新發佈至 WSUS。 您接著可以使用現有軟體更新管理程序來部署這些更新。 

如需詳細資訊，請參閱[啟用協力廠商更新](../../../sum/deploy-use/third-party-software-updates.md)。


### <a name="deploy-software-updates-without-content"></a>部署軟體更新但沒有內容
<!--1357933-->
將軟體更新部署至裝置，而不需要先下載內容並將其散發至發佈點。 在處理極大量的更新內容時，或者您始終希望用戶端從 Microsoft Update 的雲端服務取得內容時，這項功能很有用。 此案例中的用戶端也可以從已具有必要內容的對等節點下載內容。 Configuration Manager 用戶端會繼續管理內容的下載，因此可以利用 Configuration Manager 的對等快取功能或其他技術，例如傳遞最佳化。 這項功能支援 Configuration Manager 軟體更新管理所支援的任何更新類型，包括 Windows 和 Office 更新。 

如需詳細資訊，請在[手動部署軟體更新](../../../sum/deploy-use/manually-deploy-software-updates.md)或[自動部署軟體更新](../../../sum/deploy-use/automatically-deploy-software-updates.md)時查看 [No deployment package] \(無部署套件\)  選項。


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>依軟體更新架構篩選自動部署規則
 <!--1322266-->
您現在可以篩選自動部署規則 (ADR) 來排除架構 (例如 Itanium 和 ARM64)。 在 [建立自動部署規則精靈] 的 [軟體更新]  頁面上，現在提供 [架構]  屬性篩選。 

如需詳細資訊，請參閱[自動部署軟體更新](../../../sum/deploy-use/automatically-deploy-software-updates.md)。


### <a name="improved-wsus-maintenance"></a>改善的 WSUS 維護 
<!--1357898-->
[WSUS 清除精靈] 現在會根據軟體更新點元件屬性上所定義的取代規則來拒絕過期更新。 

如需詳細資訊，請參閱[軟體更新維護](../../../sum/deploy-use/software-updates-maintenance.md)。



## <a name="reporting"></a>報告

### <a name="new-software-updates-compliance-report"></a>新的軟體更新合規性報表
<!--1357775-->
檢視軟體更新合規性的報告通常包含來自最近尚未連絡站台之用戶端的資料。 新報表 (**合規性 9 - 整體健全狀況與合規性**) 可讓您依「狀況良好」的用戶端，針對特定的軟體更新群組來篩選合規性結果。 此報告會針對您環境內的有效用戶端顯示更真實的合規性狀態。 

如需詳細資訊，請參閱[軟體更新報表](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports)。



## <a name="inventory"></a>清查

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a> 大整數值的硬體清查改善
<!--1357880-->
硬體清查之前會限制大於 4,294,967,296 (2^32) 的整數。 硬碟大小 (位元組) 這類屬性可能會達到此限制。 管理點無法處理超過此限的整數值，因此沒有值會儲存在資料庫中。 在此版本中，現在的限制已增加至 18,446,744,073,709,551,616 (2^64)。 

如需詳細資訊，請參閱[使用大整數值](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint)。


### <a name="hardware-inventory-default-unit-revision"></a>修訂硬體清查預設單位
<!--514442-->
在 [Configuration Manager 1710 版](whats-new-in-version-1710.md#site-infrastructure)中，許多報表檢視中使用的預設單位已從百萬位元組 (MB) 變更為十億位元組 (GB)。 因為已進行[大整數值的硬體清查改善](#bkmk_bigint)，並根據客戶的意見反應修訂，這個預設單位現在又是 MB。



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager 主控台

### <a name="product-lifecycle-dashboard"></a>產品生命週期儀表板
<!--1319632-->
產品生命週期儀表板會針對安裝於利用 Configuration Manager 管理之裝置上的 Microsoft 產品，顯示 Microsoft 生命週期原則的狀態。 它也會提供環境中 Microsoft 產品、支援狀態和支援終止日期的相關資訊。 使用儀表板來了解每項產品的支援可用性。 這項資訊可以在您所使用的 Microsoft 產品達到其目前的終止支援之前，協助您規劃更新該產品的時機。   

如需詳細資訊，請參閱[產品生命週期儀表板](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)。


### <a name="copy-asset-details-from-monitoring-views"></a>從監視檢視複製資產詳細資料
<!--1357856-->
[監視]  工作區的下列區域現在支援複製文字：  

- 在 [部署]  節點中，選取部署，然後按一下 [檢視狀態]  。 在 [部署狀態] 檢視的 [資產詳細資料]  窗格中，選取一或多個裝置。  

- 展開 [發佈狀態]  節點，然後選取 [內容狀態]  。 選取軟體的某個部分，然後按一下 [檢視狀態]  。 在 [內容狀態] 檢視的 [資產詳細資料]  窗格中，選取一或多個發佈點。 

以滑鼠右鍵按一下 [資產]，然後選取 [複製]  。 此動作會將所選取的資產複製為逗號分隔的清單，其中包含完整詳細資料。 鍵盤快速鍵 **CTRL** + **C** 也適用於這些檢視。 

如需詳細資訊，請參閱 [1806 版的主控台改善](../../servers/manage/admin-console.md#copy-details-in-monitoring-views)。


### <a name="improvements-to-the-surface-dashboard"></a>Surface 儀表板的改善
<!--1358654-->
此版本包含下列 Surface 儀表板改善：  

- 當您選取特定圖表區段時，Surface 儀表板現在會顯示相關裝置的清單：  

   - 按一下 [Surface 裝置的百分比]  磚會開啟 Surface 裝置的清單。  

   - 按一下 [前五個韌體版本]  磚中的長條會開啟含有該特定韌體版本之 Surface 裝置的清單。  

- 從 Surface 儀表板檢視這些裝置清單時，請以滑鼠右鍵按一下裝置來執行一般動作。  

如需詳細資訊，請參閱 [Surface 儀表板](../../clients/manage/surface-device-dashboard.md)。


### <a name="view-the-currently-signed-on-user-for-a-device"></a>檢視裝置的目前登入使用者
<!--1358202-->
根據預設，[Assets and Compliance]  \(資產與合規性\) 工作區的 [裝置]  節點現在會顯示 [Currently logged on user]  \(目前登入的使用者\) 的資料行。 它也會針對任何集合特定裝置清單顯示。 這個值是[用戶端狀態](../../clients/manage/monitor-clients.md#bkmk_indStatus)目前的值。 使用者登出時，用戶端會清除此值。 如果沒有任何使用者登入，則此值會空白。 

如需詳細資訊，請參閱 [1806 版的主控台改善](../../servers/manage/admin-console.md#view-users-for-a-device)。


### <a name="submit-feedback-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台提交意見反應  
<!--1357542-->

傳送笑臉！ 您現在可以把自己的相關經驗直接告訴 Configuration Manager 小組。 從 Configuration Manager 主控台傳送意見反應很容易。 如果您有任何的讚美、問題或建議，請不吝告知。 在 Configuration Manager 主控台中，按一下功能區上方右上角的笑臉按鈕。 這個意見反應會直接傳送給 Microsoft 的 Configuration Manager 產品小組。 雖然我們仍支援使用 Windows 10 意見反應中樞，不過建議您使用主控台內建的意見反應機制。  

如需詳細資訊，請參閱 [1806 版的主控台改善](../../servers/manage/admin-console.md#send-feedback)和[產品意見反應](../../understand/find-help.md#BKMK_1806Feedback)。



## <a name="other-updates"></a>其他更新

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Summary of changes in Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4459701) (Configuration Manager 最新分支 1806 版中的變更摘要)。

如需設定管理員中 Windows PowerShell Cmdlet 變更的詳細資訊，請參閱 [PowerShell 1806 版本資訊](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps)。

自 2018 年 10 月 24 日起，就可在主控台中使用以下更新彙總套件 (4462978)：[適用於 Configuration Manager 目前分支 1806 版的更新彙總套件](https://support.microsoft.com/help/4462978) (機器翻譯)。


### <a name="hotfixes"></a>Hotfix

以下其它 Hotfix 可用於處理特定問題：

| 識別碼 | 標題 | 日期 | 主控台內 |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Configuration Manager 1806 版的第一波更新 | 2018 年 8 月 31 日 | 是 |
| [4465865](https://support.microsoft.com/help/4465865) | 若 WSUS 中斷連線，就不會在 Configuration Manager 環境中下載軟體更新<br><br>此更新也包含在更新彙總套件中 (4462978) | 2018 年 10 月 1 日 | 是 |
| [4471892](https://support.microsoft.com/help/4471892) | 在 Configuration Manager 1806 中，PXE 回應程式不會在子網路之間運作 | 2018 年 11 月 23 日 | 否 |
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune 連接器憑證不會在 Configuration Manager 中更新 | 2019 年 1 月 18 日 | 是 |


## <a name="next-steps"></a>後續步驟

當您準備好安裝此版本時，請參閱[安裝 Configuration Manager 的更新](../../servers/manage/updates.md)和[安裝更新 1806 的檢查清單](../../servers/manage/checklist-for-installing-update-1806.md)。

> [!TIP]  
> 若要安裝新的站台，請使用 Configuration Manager 的基準版本。  
>
> 深入了解：    
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

如需已知的重大問題，請參閱[版本資訊](../../servers/deploy/install/release-notes.md)。

更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist)。
