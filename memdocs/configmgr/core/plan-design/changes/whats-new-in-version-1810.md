---
title: 1810 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 最新分支 1810 版所引進之變更和新功能的詳細資料。
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a9770dca209669659abf6e4fc9c23d5e6972981
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073546"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Configuration Manager 最新分支 1810 版的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 最新分支 1810 更新可以透過主控台內更新的方式取得。 在執行 1710、1802 或 1806 版的站台上套用此更新。 <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> 本文摘要說明 Configuration Manager 1810 版的變更和新功能。  

請一律檢閱適用於安裝此更新的最新檢查清單。 如需詳細資訊，請參閱[安裝更新 1810 的檢查清單](../../servers/manage/checklist-for-installing-update-1810.md)。 更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist)。

若要利用 Configuration Manager 的新功能，請先將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> 已淘汰的功能和作業系統

在[已移除與已淘汰的項目](deprecated/removed-and-deprecated.md)中實作支援變更之前，請先了解這些變更。

自 2018 年 8 月 14 日起，淘汰混合式行動裝置的管理功能。 如需詳細資訊，請參閱[混合式 MDM 有哪些改變？](../../../mdm/understand/what-happened-to-hybrid.md)。<!--Intune feature 2683117-->  

對 Mac 與 Linux (所有版本) System Center Endpoint Protection (SCEP) 的支援，於 2018 年 12 月 31 日終止。 支援終止後，將不再繼續提供 Mac 版 SCEP 與 Linux 版 SCEP 的新病毒定義。 如需詳細資訊，請參閱[支援終止部落格文章](https://go.microsoft.com/fwlink/?linkid=870182)。

Configuration Manager 現已淘汰 Azure 的傳統服務部署。 開始在雲端管理閘道和雲端發佈點使用 Azure Resource Manager 部署。 如需詳細資訊，請參閱[規劃 CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)。



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> 站台基礎結構

### <a name="support-for-windows-server-2019"></a>Windows Server 2019 的支援

<!--1359195-->
Configuration Manager 現在支援 Windows Server 2019 和 Windows Server 1809 版作為站台系統。

如需詳細資訊，請參閱[站台系統伺服器支援的作業系統](../configs/supported-operating-systems-for-site-system-servers.md)。


### <a name="hierarchy-support-for-site-server-high-availability"></a>站台伺服器高可用性的階層支援

<!--3607755, fka 1358224-->
管理中心網站和子主要站台現在可擁有其他的被動模式站台伺服器。

如需詳細資訊，請參閱[站台伺服器高可用性](../../servers/deploy/configure/site-server-high-availability.md)。


### <a name="improvements-to-setup-prerequisites"></a>安裝程式必要條件的改善

當您安裝或更新至 1810 版時，Configuration Manager 安裝程式現在包含或改善下列必要條件檢查：

- **系統重新啟動擱置中**：此必要條件檢查現在更有彈性。 它會檢查 Windows 功能的其他登錄機碼。 如需詳細資訊，請參閱[暫止的系統重新啟動](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart)。 <!--SCCMDocs-pr issue 3010-->  

- **SQL 變更追蹤清除**：站台資料庫是否有 SQL 變更追蹤資料待辦項目的新檢查。 如需詳細資訊，包括確認及清除此待辦項目的程序，請參閱 [SQL 變更追蹤清除](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking)。 <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client 版本**：這項必要條件檢查會針對支援 TLS 1.2 的 SQL Native Client 版本進行更新。 最低版本為 [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402)。 如需詳細資訊，請參閱 [SQL Native Client 版本](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。 <!--SCCMDocs-pr issue 3094-->  

- **Windows 叢集節點上的站台系統**：設定管理員安裝程式程序不會再封鎖在具有容錯移轉叢集 Windows 角色的電腦上安裝站台伺服器角色。 SQL Always On 需要此角色，因此先前您無法將站台資料庫共置在站台伺服器上。 透過這項變更，您可以使用較少的伺服器建立高可用性的站台，方法是被動模式中使用 SQL AlwaysOn 和站台伺服器。 如需詳細資訊，請參閱 [Windows 容錯移轉叢集](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster)。 <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>用戶端通知動作的新權限

<!--SCCMDocs-pr issue #2972-->
用戶端通知動作現在需要 SMS_Collection 類別的**通知資源**權限。 下列內建角色預設具有此權限：

- 系統高權限管理員  
- 基礎結構系統管理員  

將此權限新增至需要使用用戶端通知動作的任何自訂角色。

如需詳細資訊，請參閱[用戶端通知](../../clients/manage/client-notification.md)。



## <a name="content-management"></a><a name="bkmk_content"></a> 內容管理

### <a name="new-boundary-group-options"></a>新的界限群組選項

<!--1358749-->
界限群組現在包含下列其他設定，讓您加強掌控環境中的內容發佈：

- **優先使用發佈點而非相同子網路中的對等**：根據預設，管理點會將對等快取來源的優先順序排在內容位置清單之前。 此設定會反轉與對等快取來源位於相同子網路的用戶端優先順序。  

- **優先使用雲端發佈點而非一般發佈點**：如果您的分公司辦公室網際網路連結較快，您現在可以優先使用雲端內容。  

如需詳細資訊，請參閱[適用於對等下載的界限群組選項](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)。


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>對等快取來源用戶端版本的管理見解規則

<!-- 1358008 -->
[管理見解]  節點的新規則，可識別作為對等快取來源，但尚未從 1806 之前的用戶端版本升級的用戶端。 新的規則為 [將對等快取來源升級為 Configuration Manager 用戶端的最新版本]  ，而且屬於新的 [主動式維護]  規則群組。 1806 之前的用戶端無法作為執行 1806 或更新版本之用戶端的對等快取來源。 請選取 [採取動作]  以開啟顯示用戶端清單的裝置檢視。

如需詳細資訊，請參閱[管理見解](../../servers/manage/management-insights.md)。



## <a name="client-management"></a><a name="bkmk_client"></a> 用戶端管理

### <a name="new-client-notification-action-to-wake-up-device"></a>新增用戶端通知動作以喚醒裝置

<!--1317364-->
您現在可以從 Configuration Manager 主控台喚醒用戶端，即使用戶端與站台伺服器位在不同的子網路也一樣。 如果您需要執行維護作業或查詢裝置，不會受到睡眠的遠端用戶端所限。 站台伺服器使用用戶端通知通道來識別在同一遠端子網路上喚醒的另一個用戶端。 然後，喚醒的用戶端會傳送網路喚醒要求 (Magic 封包)。

如需詳細資訊，請參閱[設定網路喚醒](../../clients/deploy/configure-wake-on-lan.md)和[如何喚醒用戶端](../../clients/deploy/plan/plan-wake-up-clients.md)。

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>從裝置節點執行用戶端通知的新選項

<!--1317364-->
到 1810 為止，[用戶端通知]  選項僅從 [裝置集合] 節點，或是檢視 [裝置集合] 的成員資格時提供。 現在可從 [裝置]  節點直接執行 [用戶端通知]  。 不需要再從集合成員資格檢視中執行。

如需詳細資訊，請參閱[用戶端通知](../../clients/manage/client-notification.md)。


### <a name="improvements-to-collection-evaluation"></a>集合評估的改善

<!--3607726, fka 1358981-->
集合評估行為的下列變更可改善網站效能：  

- 之前當您在以查詢為基礎的集合上設定排程時，網站會繼續評估查詢是否啟用了 [排程此集合的完整更新]  集合設定。 若要完全停用排程，必須將排程變更為 [無]  。 現在網站會在您停用此設定時清除排程。 若要指定集合評估排程，請啟用 [排程此集合的完整更新]  選項。  

- 您無法停用內建集合 (例如 [所有系統]  ) 評估，但現在可以設定排程。 此行為可讓您在符合業務需求時自訂此動作。

如需詳細資訊，請參閱[如何建立集合](../../clients/manage/collections/create-collections.md#bkmk_create)。


### <a name="improvement-to-client-installation"></a>用戶端安裝的改善

<!--1358840-->
安裝 Configuration Manager 用戶端時，ccmsetup 處理序就會連絡管理點以找出必要內容。 先前，在此程序中，管理點只會傳回用戶端目前界限群組中的發佈點。 如果沒有內容可用，則安裝程序會回復為從管理點下載內容。 沒有任何選項可以後援到其他界限群組中可能有必要內容的發佈點。 現在，管理點會傳回根據界限群組設定的發佈點。

如需詳細資訊，請參閱[設定界限群組](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)。



## <a name="co-management"></a><a name="bkmk_comgmt"></a> 共同管理

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>共同受控裝置的必要應用程式合規性政策

<!--1358196-->
在 Configuration Manager 中定義必要應用程式的合規性政策規則。 此應用程式評量是傳送至 Microsoft Intune 以共同管理裝置之整體合規性狀態的一部分。

如需詳細資訊，請參閱[共同管理工作負載](../../../comanage/workloads.md)。


### <a name="improvement-to-co-management-dashboard"></a>共同管理儀表板的改善

<!--1358980-->
同管理儀表板已使用下列更多詳細資訊予以增強：  

- [共同管理註冊狀態]  磚包含其他狀態

- 有漏斗圖的新 [共同管理狀態]  磚，會顯示註冊程序的狀態

- 具有 [註冊錯誤]  計數的新磚

![共同管理儀表板螢幕擷取畫面顯示前四個磚](media/1358980-comgmt-dashboard.png)

如需詳細資訊，請參閱[共同管理儀表板](../../../comanage/how-to-monitor.md#co-management-dashboard)。


### <a name="improvements-to-internet-based-client-setup"></a>以網際網路為基礎的用戶端設定改善

<!--3607731, fka 1359181-->
此版本進一步簡化網際網路用戶端的 Configuration Manager 用戶端設定程序。 站台會將額外的 Azure Active Directory (Azure AD) 資訊發佈至雲端管理閘道 (CMG)。 已加入 Azure AD 的用戶端會在 ccmsetup 過程中從 CMG 取得此資訊 (使用它所加入的同一租用戶)。 在具有多個 Azure AD 租用戶的環境中，此行為可進一步簡化共同管理的裝置註冊作業。 現在只有兩個必要的 ccmsetup 屬性，分別是 **CCMHOSTNAME** 和 **SMSSiteCode**。

如需詳細資訊，請參閱[如何準備網路型裝置進行共同管理](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)。



## <a name="application-management"></a><a name="bkmk_app"></a> 應用程式管理

### <a name="convert-applications-to-msix"></a>將應用程式轉換為 MSIX

<!--3607729, fka 1359029-->
從 1806 版開始，Configuration Manager 支援新的 Windows 10 應用程式套件 (.msix) 格式部署。 現在，您可以將現有的 Windows Installer (.msi) 應用程式轉換為 MSIX 格式。

如需詳細資訊，請參閱[建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md#bkmk_msix)。  


### <a name="repair-applications"></a>修復應用程式

<!--1357866-->
指定 Windows Installer 和指令碼安裝程式部署類型的修復命令列。 然後，如果啟用部署上的選項，軟體中心就會出現 [修復]  應用程式的新按鈕。 當您為應用程式設定修復程式時，使用者便可從「軟體中心」啟動命令。

如需詳細資訊，請參閱[建立應用程式](../../../apps/deploy-use/create-applications.md#bkmk_dt-content)和[部署應用程式](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)。


### <a name="approve-application-requests-via-email"></a>透過電子郵件核准應用程式要求

<!--1321550-->
設定應用程式核准要求的電子郵件通知。 當使用者要求應用程式時，您會收到一封電子郵件。 按一下電子郵件中的連結來核准或拒絕要求，而不需使用 Configuration Manager 主控台。

如需詳細資訊，請參閱[核准應用程式](../../../apps/deploy-use/app-approval.md)。


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>偵測方法不會載入 Windows PowerShell 設定檔

<!--3607762, fka 1359239-->
您可以使用 Windows PowerShell 指令碼處理應用程式偵測方法和設定項目中的設定。 現在，在用戶端上執行這些指令碼時，Configuration Manager 用戶端會使用 `-NoProfile` 參數呼叫 PowerShell。 此選項會啟動 PowerShell，但不含設定檔。

PowerShell 設定檔是在 PowerShell 啟動時執行的指令碼。 您可以建立 PowerShell 設定檔來自訂您的環境，並將工作階段特定項目新增至您啟動的每一個 PowerShell 工作階段。

> [!Note]  
> 此行為變更不適用於[指令碼](../../../apps/deploy-use/create-deploy-scripts.md)或 [CMPivot](../../servers/manage/cmpivot.md)。 這兩種功能皆已使用此 PowerShell 參數。  

如需詳細資訊，請參閱[建立應用程式](../../../apps/deploy-use/create-applications.md)和[建立自訂設定項目](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)。



## <a name="os-deployment"></a><a name="bkmk_osd"></a> 作業系統部署

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>現有裝置的 Windows Autopilot 工作順序支援

<!--3607717, fka 1358333-->
[現有裝置適用的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) 現在提供 Windows 10 1809 版或更新版本。 這項新功能可讓您使用單一的原生 Configuration Manager 工作順序，重新安裝映像及佈建 Windows 7 裝置使用 [Windows Autopilot user-driven mode](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) (Windows Autopilot 使用者導向模式)。

如需詳細資訊，請參閱[適用於現有裝置的 Windows Autopilot](../../../osd/deploy-use/windows-autopilot-for-existing-devices.md)。


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>指定提供離線作業系統映像的磁碟機

<!--1358924-->
現在指定將軟體更新新增至作業系統映像及作業系統升級套件時，Configuration Manager 使用的磁碟機。 此程序會使用暫存檔來耗用大量磁碟空間，因此，此選項可讓您彈性地選取要使用的磁碟機。

如需詳細資訊，請參閱[管理作業系統映像](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive)或[管理作業系統升級套件](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive)。


### <a name="task-sequence-support-for-boundary-groups"></a>界限群組的工作順序支援

<!--1359025-->
裝置執行工作順序並且需要取得內容時，現在會使用與 Configuration Manager 用戶端類似的界限群組行為。

如需詳細資訊，請參閱[界限群組](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd)。


### <a name="improvements-to-driver-maintenance"></a>驅動程式維護的改善

<!--3607716, fka 1358270-->
驅動程式套件現有針對 [製造商]  和 [型號]  的額外中繼資料欄位。 您可以使用這些欄位來設定驅動程式套件的資訊標記，以協助一般例行性作業，或識別可刪除的舊版和重複驅動程式。

如需詳細資訊，請參閱[管理驅動程式](../../../osd/get-started/manage-drivers.md)。

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Windows 10 服務方案篩選條件的增強功能

<!--3098809, 3113836, 3204570 -->
其他篩選器已新增至 Windows 10 服務計畫。 您現在可以依**架構**、**產品類別**進行篩選，以及升級是否為**已取代**。

如需詳細資訊，請參閱 [Windows 10 服務方案](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan)。

### <a name="new-task-sequence-variable-for-last-action-name"></a>最後一個動作名稱的新工作順序變數

<!--SCCMDocs-pr issue #2964-->
除了工作順序變數 _SMSTSLastActionRetCode，工作順序還會設定新的變數 **_SMSTSLastActionName**。 它也會將這個值記錄在 smsts.log 檔案中。 這個新變數對工作順序的疑難排解很有幫助。 當步驟失敗時，自訂指令碼會包含步驟名稱及傳回碼。

如需詳細資訊，請參閱[工作順序變數](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName)。



## <a name="software-updates"></a><a name="bkmk_sum"></a> 軟體更新

### <a name="phased-deployment-of-software-updates"></a>軟體更新的階段式部署

<!--1358146-->
您可以建立軟體更新的階段式部署。 階段式部署可讓您根據可自訂的準則與群組，以組織協調且循序的軟體推出。

如需詳細資訊，請參閱[建立階段式部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)。


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>軟體更新的維護時段改善

<!--vso2839307-->
下列用戶端設定位於**軟體更新**群組，在維護時段中控制軟體更新的安裝行為：**當 [軟體更新] 維護視窗可以使用時，允許安裝 [所有部署] 維護視窗中的更新**

此選項預設為 [否]  ，以與現有的行為保持一致。 將它變更為 [是]  可讓用戶端使用其他可用的維護視窗來安裝軟體更新。

如需詳細資訊，請參閱[軟體更新用戶端設定](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint)。


### <a name="improvement-to-software-updates-maintenance"></a>對軟體更新維護的改進

<!--2839349-->
WSUS 清理工作現在會在次要站台上執行。 次要站台的 WSUS 會針對過期更新執行 WSUS 清理，並拒絕已取代的更新。

如需詳細資訊，請參閱[從 1810 版開始的 WSUS 清理行為](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)

### <a name="improvement-to-software-update-supersedence-rules"></a>軟體更新取代規則的改進

<!--3098809, 2977644-->
您現在可以單獨為非功能更新指定功能更新的取代規則。 這表示在完成提供 Windows 10 用戶端的服務之前，不會從 Configuration Manager 中移除您的升級。

如需詳細資訊，請參閱 [取代規則](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules)。

## <a name="reporting"></a><a name="bkmk_report"></a> 報告

### <a name="improvement-to-lifecycle-dashboard"></a>生命週期儀表板改善

<!--1358702-->
產品生命週期儀表板現在包含 **System Center 2012 Configuration Manager 和更新版本**的資訊。

另外還有新的報表：**生命週期 05A - 產品生命週期儀表板**。 它包含類似主控台中儀表板的資訊。

如需此儀表版的詳細資訊，請參閱[使用產品生命週期儀表板](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)。


### <a name="improvement-to-data-warehouse"></a>資料倉儲改善

<!--1358870-->
您現在可以將多個資料表從站台資料庫同步至資料倉儲。 這項變更可讓您根據業務需求建立更多報表。

如需詳細資訊，請參閱[資料倉儲](../../servers/manage/data-warehouse.md)。



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 主控台

### <a name="configuration-manager-administrator-authentication"></a>Configuration Manager 系統管理員驗證

<!--1357013-->
您現在可以指定系統管理員存取 Configuration Manager 站台的最低驗證層級。 這項功能會強制系統管理員以必要層級登入 Windows。 若要設定此設定，請找出 [階層設定]  中的 [驗證]  索引標籤。

如需詳細資訊，請參閱[規劃 SMS 提供者](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)。


### <a name="support-center"></a>支援中心

<!--1357489-->
使用支援中心來進行用戶端疑難排解、即時檢視記錄檔，或擷取 Configuration Manager 用戶端電腦的狀態，以於稍後進行分析。 支援中心是結合眾多系統管理員疑難排解工具的單一工具。 支援中心的安裝程式位於站台伺服器的 **cd.latest\SMSSETUP\Tools\SupportCenter** 資料夾中。

如需詳細資訊，請參閱[支援中心](../../support/support-center.md)。


### <a name="management-insights-dashboard"></a>管理見解儀表板

<!--1357979-->
[管理見解]  節點現在包含圖形化儀表板。 此儀表板會顯示規則狀態的概觀，讓您更輕鬆地顯示進度。 儀表板包含以下磚：

- **管理見解索引**：追蹤管理見解規則的整體進度。 索引是加權平均值。 重大規則最為值得。 此索引提供選擇性規則的最小加權。  

- **管理見解群組**：在每個群組中顯示規則的百分比。  

- **管理見解優先順序**：依優先順序顯示規則的百分比。  

- **所有見解**：包含優先順序和狀態的見解表。  

![管理見解儀表板的螢幕擷取畫面](media/1357979-management-insights-dashboard.png)

如需詳細資訊，請參閱[管理見解](../../servers/manage/management-insights.md)。


### <a name="improvements-to-cmpivot"></a>CMPivot 的改善

<!--1359068-->
CMPivot 包含下列改善：

- 儲存 [我的最愛]  查詢  

- 在 [查詢摘要] 索引標籤上，選取失敗或離線裝置計數，然後選取 [建立集合]  選項。

如需 CMPivot 的其他效能和疑難排解改善詳細資訊，請參閱[指令碼的改善](#bkmk_scripts)。

如需 CMPivot 的相關詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md)。


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> 指令碼的改善

<!--1358239-->
您現在可以檢視原始或結構化 JSON 格式的詳細指令碼輸出。 此格式可讓輸出變得更容易讀取與分析。

下列效能和疑難排解改善適用於 CMPivot 和指令碼：

- 已更新的用戶端會透過快速通訊通道將小於 80 KB 的輸出傳回給站台。 這項變更可提高檢視指令碼或查詢輸出的效能。  

- 用於疑難排解的其他記錄檔  

如需詳細資訊，請參閱下列文章：  

- [從 Configuration Manager 主控台建立和執行 PowerShell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)  

- [針對 CMPivot 進行疑難排解](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>SMS 提供者 API

<!--3607711, fka 1321523-->
SMS 提供者現在會透過 HTTPS 提供 WMI 的唯讀 API 交互操作性存取，稱為「系統管理服務」  。 此 REST API 可用於取代自訂 Web 服務，以存取來自網站的資訊。

**SMS 提供者**顯示為具有允許透過雲端管理閘道進行通訊之選項的角色：。 此設定目前的使用方式，是從遠端裝置透過電子郵件核准應用程式。

如需詳細資訊，請參閱[規劃 SMS 提供者](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)。



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> 內部部署 MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>新內部部署 MDM 部署已不再需要 Intune 連線

<!--1359124-->
內部部署 MDM 的新部署先決條件已不必設定 Microsoft Intune 訂閱。 但您的組織仍需要 Intune 授權才能使用這項功能。 您目前無法從現有的內部部署 MDM 部署移除 Intune 連線。 如需詳細資訊，請參閱 [Intune 支援部落格文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。



## <a name="other-updates"></a>其他更新

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 1810 版中變更的摘要](https://support.microsoft.com/help/4482169)。

如需適用於 Configuration Manager 之 Windows PowerShell Cmdlet 變更的詳細資訊，請參閱 [PowerShell 1810 版版本資訊](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps)。

自 2019 年 3 月 25 日起，就可在主控台中使用以下更新彙總套件 (4488598)：[適用於 Configuration Manager 目前分支 1810 版的更新彙總套件 2](https://support.microsoft.com/help/4488598) \(英文\)。 這會取代先前的更新彙總 KB 4486457。


### <a name="hotfixes"></a>Hotfix

以下其它 Hotfix 可用於處理特定問題：

| 識別碼 | 標題 | 日期 | 主控台內 |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune 連接器憑證不會在 Configuration Manager 中更新 | 2019 年 1 月 18 日 | 是 |
| [4490434](https://support.microsoft.com/help/4490434) \(機器翻譯\) | 在 Configuration Manager 中會建立重複的使用者探索欄 | 2019 年 2 月 22 日 | 是 |
| [4490575](https://support.microsoft.com/help/4490575) \(機器翻譯\) | 在 Configuration Manager 1810 版中，更新安裝停止回應或永不顯示完成 | 2019 年 2 月 22 日 | 是 |


## <a name="next-steps"></a>後續步驟

當您準備安裝此版本時，請參閱[安裝 Configuration Manager 的更新](../../servers/manage/updates.md)和[安裝更新 1810 的檢查清單](../../servers/manage/checklist-for-installing-update-1810.md)。

> [!TIP]  
> 若要安裝新的站台，請使用 Configuration Manager 的基準版本。  
>
> 深入了解：
>
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)  

如需已知的重大問題，請參閱[版本資訊](../../servers/deploy/install/release-notes.md)。

更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist)。
