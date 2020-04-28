---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1806 版中可用的新功能。
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 647eba601cbfa5304bf02f8bcf059fe6e851cbf0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074056"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Configuration Manager Technical Preview 1806 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1806 版中可用的功能。 您可以安裝此版本，以將新功能更新並新增至您的技術預覽版網站。 

請先檢閱[技術預覽版](technical-preview.md)文章，再安裝此更新。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 的已知問題

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> 站台無法以遠端內容庫進行升級
<!--514642-->
站台無法升級，並在 **cmupdate.log** 中出現下列錯誤：  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

當內容庫位於遠端位置時，此版本會發生這個問題。

#### <a name="workaround"></a>因應措施
請將內容庫移到站台伺服器的本機磁碟機。 如需詳細資訊，請參閱[針對站台伺服器設定遠端內容庫](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)。 



</br>

**以下是您可以使用此版本試用的新功能。**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> 協力廠商軟體更新
<!--1352101-->
針對您提出的 [UserVoice 意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)，此版本會進一步反覆支援協力廠商軟軟體更新。 針對一些常見案例，您不再需要使用 System Center Updates Publisher (SCUP)。 Configuration Manager 主控台中的新 [協力廠商軟體更新類別目錄]  節點可讓您訂閱協力廠商的類別目錄，將其更新發佈到您的軟體更新點，然後將其部署至用戶端。 

此版本提供下列協力廠商軟體更新類別目錄：

 | 發行者 | 類別目錄名稱 |
 |--------|---------------------|
 | HP | HP 用戶端更新類別目錄 |

SCUP 會繼續支援其他類別目錄和案例。 Configuration Manager 主控台的 [協力廠商軟體更新類別目錄] 節點中的類別目錄清單是動態的，將在其他類別目錄可供使用且受支援時進行更新。


### <a name="prerequisites"></a>先決條件
- 以啟用 HTTPS 的軟體更新點設定軟體更新管理。 如需詳細資訊，請參閱 [Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md) (準備軟體更新管理)。  
  - 針對此版本中的這項功能，軟體更新點必須位在站台伺服器上。 <!--515810--> 

    > [!Tip]  
    > 軟體更新點需要 HTTPS，因為它是用來處理簽署憑證的 WSUS API 需求。 用戶端不需要同時啟用 HTTPS。 如需在 WSUS 上啟用 HTTPS 的詳細資訊，請參閱下列文章以取得協助：  
    > - [使用安全通訊端層通訊協定確保 WSUS 的安全](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [WSUS 支援部落格文章](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- 軟體更新點 (WSUSContent 資料夾) 上有足夠的磁碟空間來儲存協力廠商軟體更新的來源二進位檔案內容。 必要的儲存體數量因廠商、更新類型以及您為部署所發佈的特定更新而異。 如果您需要將 WSUSContent 資料夾移至具有更多可用空間的另一個磁碟機，請參閱 WSUS 支援小組的部落格文章 [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) (如何變更 WSUS 在本機儲存更新的位置)。  

- 啟用並部署用戶端設定 [軟體更新]  群組中的 [[啟用協力廠商軟體更新]](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) 用戶端設定。  

- 站台伺服器需要透過 HTTPS 連接埠 443 對 download.microsoft.com 進行網際網路存取。 協力廠商軟體更新同步處理服務目前會在站台伺服器上執行。 這項服務會更新可用的協力廠商類別目錄清單、在您訂閱時下載類別目錄，並在發佈時下載更新。 必要的話，請在站台伺服器電腦之站台系統角色內容的 [Proxy]  索引標籤上，設定網際網路 Proxy 設定。  


### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。


#### <a name="phase-1-enable-and-set-up-the-feature"></a>階段 1：啟用和設定功能
針對「每個階層」執行下列步驟一次  ，以啟用和設定要使用的功能：  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取階層中的頂層站台。 在功能區中，按一下 [設定站台元件]  ，然後選取 [軟體更新點]  。  

3. 切換至 [協力廠商更新]  索引標籤。選取 [啟用協力廠商軟體更新]  的選項。 如需憑證選項的詳細資訊，請參閱[各種能啟用協力廠商軟體更新支援的改善](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)。  

   > [!Note]  
   > 如果您使用 Configuration Manager 的預設選項來管理此憑證，就會在 [管理]  工作區之 [安全性]  底下的 [憑證]  節點中建立類型為 [協力廠商 WSUS 簽署]  的新憑證。  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>階段 2：訂閱協力廠商類別目錄和同步處理更新
針對您要訂閱的「每個協力廠商類別目錄」  執行下列步驟：  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。  

2. 選取要訂閱的類別目錄，然後按一下功能區中的 [訂閱類別目錄]  。   

3. 檢閱並核准類別目錄的憑證。  

   > [!Note]  
   > 當您訂閱協力廠商軟體更新類別目錄時，您在此精靈中檢閱並核准的憑證就會新增至站台。 此憑證的類型是 [協力廠商軟體更新類別目錄]  。 您可以從 [管理]  工作區之 [安全性]  底下的 [憑證]  節點中管理憑證。  

4. 完成精靈。  

   > [!Tip]  
   > 初次訂閱之後，應該會立即開始下載類別目錄。 然後，它會在此版本中每隔 24 小時重新同步一次。 如果您不想等候類別目錄自動下載，請按一下功能區中的 [立刻同步]  。  
   > 
   > 下載類別目錄之後，產品中繼資料必須同步處理至軟體更新點。 如需這個程序以及手動起始方式的詳細資訊，請參閱[同步處理軟體更新](../../sum/get-started/synchronize-software-updates.md)。 此時，您可以在 [所有更新]  節點中看到協力廠商更新。 

5. 接下來，針對您要訂閱的協力廠商類別目錄設定軟體更新點 [產品]  。 如需詳細資訊，請參閱[設定要同步處理的分類和產品](../../sum/get-started/configure-classifications-and-products.md)。 產品準則變更之後，必須再次進行軟體更新同步處理。

在您可以看到來自用戶端的合規性結果之前，它們必須掃描並評估更新。 您可以從用戶端的 Configuration Manager 控制台中執行 [軟體更新掃描週期]  動作，以手動方式觸發此週期。 如需此程序的詳細資訊，請參閱[軟體更新簡介](../../sum/understand/software-updates-introduction.md)。


#### <a name="phase-3-deploy-third-party-software-updates"></a>階段 3：部署協力廠商軟體更新
針對您要部署至用戶端的「任何協力廠商軟體更新」  ，執行下列步驟：  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [所有軟體更新]  節點。  

   > [!Tip]  
   > 按一下 [新增準則]  來篩選更新清單。 例如，若要檢視所有來自 Adobe 的更新，請針對 [Adobe Systems, Inc.]  新增 [廠商]  。  

2. 選取用戶端所需的更新。 按一下 [發佈協力廠商軟體更新內容]  ，並檢閱 SMS_ISVUPDATES_SYNCAGENT.log 中的進度。 此動作會從廠商下載更新二進位檔案，並將它們儲存在軟體更新點上的 WSUSContent 資料夾。 它還會將更新的狀態從僅有中繼資料變更為具有內容且可部署。  

   > [!Note]  
   > 當您發佈協力廠商軟體更新內容時，用來簽署內容的任何憑證都會新增至站台。 這些憑證的類型是 [協力廠商軟體更新內容]  。 您可以從 [管理]  工作區之 [安全性]  底下的 [憑證]  節點中管理這些憑證。  

3. 使用現有的軟體更新管理程序來部署更新。 如需詳細資訊，請參閱 [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (部署軟體更新)。 在 [部署軟體更新精靈] 的 [下載位置]  頁面中，選取 [從網際網路下載軟體更新]  的預設選項。 在此案例中，內容已經發佈到軟體更新點，該軟體更新點可用來下載部署套件的內容。


### <a name="monitoring-progress-of-third-party-software-updates"></a>監視協力廠商軟體更新的進度
協力廠商軟體更新的同步處理是由站台伺服器上的 SMS_ISVUPDATES_SYNCAGENT 元件處理。 您可以檢視來自此元件的狀態訊息，或參閱 SMS_ISVUPDATES_SYNCAGENT.log 中更詳細的狀態。 此記錄檔位於站台伺服器之站台安裝目錄的 **Logs** 子資料夾中。 根據預設，此路徑是 `C:\Program Files\Microsoft Configuration Manager\Logs`。 如需監視一般軟體更新管理程序的詳細資訊，請參閱[監視軟體更新](../../sum/deploy-use/monitor-software-updates.md)。


### <a name="known-issues"></a>已知問題
- 協力廠商軟體更新同步處理服務不支援設定為使用 [WSUS 伺服器連線帳戶]  的軟體更新點。 如果在 [軟體更新點內容] 頁面的 [Proxy 和帳戶設定]  索引標籤上設定了此帳戶，您會看到 SMS_ISVUPDATES_SYNCAGENT.log 中出現下列錯誤：  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
如需此帳戶的詳細資訊，請參閱[軟體更新點連線帳戶](../plan-design/hierarchy/accounts.md#software-update-point-connection-account)。<!--515492-->  

- 請勿將其他工具 (例如 SCUP) 與這個新的整合式協力廠商軟體更新功能混合使用。 協力廠商軟體更新同步處理服務無法將內容發佈至僅有中繼資料的更新，此更新是透過另一個應用程式、工具或指令碼 (例如 SCUP) 新增至 WSUS。 對這些更新執行的 [發佈協力廠商軟體更新內容]  動作會失敗。 如果您需要部署此功能尚未支援的協力廠商更新，請完整使用現有的程序來部署這些更新。<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>設定 Microsoft Edge 的 Windows Defender SmartScreen 設定
<!--1353701-->
此版本在 [Microsoft Edge 瀏覽性合規性設定原則](../../compliance/deploy-use/browser-profiles.md)中新增三項 [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) 設定。 此原則目前在 [SmartScreen 設定]  頁面中包含下列額外設定：
- **允許 SmartScreen**：指定是否允許 Windows Defender SmartScreen。 如需詳細資訊，請參閱 [AllowSmartScreen 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)。
- **使用者可以覆寫站台的 SmartScreen 提示**：指定使用者是否可覆寫 Windows Defender SmartScreen 篩選工具有關潛在惡意網站的警告。 如需詳細資訊，請參閱 [PreventSmartScreenPromptOverride 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)。
- **使用者可以覆寫檔案的 SmartScreen 提示**：指定使用者是否可覆寫 Windows Defender SmartScreen 篩選工具有關下載未驗證檔案的警告。 如需詳細資訊，請參閱 [PreventSmartScreenPromptOverrideForFiles 瀏覽器原則](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)。



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>從 Microsoft Intune 為共同受控裝置同步處理 MDM 原則
<!--1357377-->
從此版本開始，當您[切換共同管理工作負載](../../comanage/how-to-switch-workloads.md)時，共同受控裝置就會從 Microsoft Intune 自動同步處理 MDM 原則。 當您在 Configuration Manager 主控台中從 [用戶端通知] 起始 [下載電腦原則]  動作時，也會進行這項同步處理作業。 如需詳細資訊，請參閱[使用用戶端通知起始用戶端原則擷取](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>使用共同管理將 Office 365 工作負載轉換至 Intune
<!--1357841-->
您現在可以在啟用共同管理之後，將 Office 365 工作負載從 Configuration Manager 轉換至 Microsoft Intune。 若要轉換此工作負載，請前往共同管理內容頁面，然後將滑動軸從 [Configuration Manager] 移至 [試驗] 或 [全部]。 如需詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../comanage/overview.md)。

另外還有新的全域條件：**在裝置上是否由 Intune 管理 Office 365 應用程式**。 預設會新增這項條件，作為新的 Office 365 應用程式的需求。 當您轉換這個工作負載時，共同受控用戶端不符合應用程式的需求，因此不會安裝透過 Configuration Manager 部署的 Office 365。

### <a name="known-issue"></a>已知問題
- 這項工作負載轉換目前僅適用於 Office 365 部署。 Configuration Manager 會繼續管理 Office 365 更新。<!--510876--> 如需包括可能因應措施的詳細資訊，請參閱 Configuration Manager 1802 版之版本資訊中的[變更 Office 365 用戶端設定不適用](../servers/deploy/install/release-notes.md)。



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager 現在是一種整合工具，可讓您將舊版 Configuration Manager 2007 套件轉換至 Configuration Manager 最新分支應用程式。 接著，您便可以使用應用程式的功能，例如相依性、需求規則和使用者裝置親和性。

> [!Tip]  
> Package Conversion Manager 現有功能的舊版文件，可於 [TechNet](https://technet.microsoft.com/library/hh531519.aspx) 取得。 相關資訊目前正在逐步移轉至 docs.microsoft.com 文件庫。

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

> [!Important]  
> 如果您先前已安裝舊版的 Package Conversion Manager，請先解除安裝後再升級您的網站。 新的整合版本不需要進行安裝，但可能會與現有的版本發生衝突。  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [應用程式管理]  ，並選取 [套件]  。  
2. 選取套件。 功能區的 [套件轉換]  群組提供下列三個選項：  
     - **分析套件**：藉由分析套件開始轉換程序。
     - **轉換套件**：某些套件可以輕鬆地轉換成具有此動作的應用程式。
     - **修正並轉換**：有些套件需要在轉換成應用程式之前修正問題。  

   如需這些動作的詳細資訊，請參閱[如何分析和轉換套件](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29)。  

3. 移至 [監視]  工作區，然後選取 [套件轉換狀態]  。 這個新的儀表板會顯示站台中套件的整體分析與轉換狀態。 新的背景工作會自動彙總分析資料。  

   > [!Tip]  
   > Package Conversion Manager 不會要求您排程套件分析。 整合式摘要工作現在會處理此動作。  

![[套件轉換狀態] 儀表板的螢幕擷取畫面](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>部署軟體更新但沒有內容
<!--1357933-->
您現在可以將軟體更新部署到裝置，而不需要先下載軟體更新內容並將其發佈到發佈點。 在處理極大量的更新內容時，或者您始終希望用戶端從 Microsoft Update 的雲端服務取得內容時，這項功能很有用。 此案例中的用戶端也可以從已具有必要內容的對等節點下載內容。 Configuration Manager 用戶端會繼續管理內容的下載，因此可以利用 Configuration Manager 的對等快取功能或其他技術，例如傳遞最佳化。 這項功能支援 Configuration Manager 軟體更新管理所支援的任何更新類型，包括 Windows 和 Office 更新。 

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 按一般方式開始軟體更新部署。 如需詳細資訊，請參閱 [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (部署軟體更新)。
2. 在 [部署軟體更新精靈] 的 [部署套件]  頁面上，選取 [無部署套件]  的新選項。

### <a name="known-issues"></a>已知問題
- 以此設定部署的更新所使用的圖示不正確地顯示一個紅色 X，如同更新無效一樣。 如需詳細資訊，請參閱[軟體更新所使用的圖示](../../sum/understand/software-updates-icons.md)。 <!--515556-->  
- 這項設定只會與 [部署軟體更新精靈] 整合。 它目前不適用於自動部署規則。 <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office 自訂工具與 Office 365 安裝程式整合
<!--1358149-->
Office 自訂工具現在已於 Configuration Manager 主控台中與 Office 365 安裝程式整合。 為 Office 365 建立部署時，您現在可以動態設定最新的 Office 管理能力設定。 Office 自訂工具會在發行 Office 365 新組建的同一時間更新。 一旦推出新的管理能力設定，您就可以立即在 Office 365 中利用這些設定。 

### <a name="prerequisites"></a>先決條件
- 執行 Configuration Manager 主控台的電腦必須透過 HTTPS 連接埠 443 存取網際網路。 [Office 365 用戶端安裝精靈] 會使用 Windows 標準的網頁瀏覽器 API 來開啟 [https://config.office.com](https://config.office.com )。 如果使用網際網路 Proxy，使用者必須能夠存取此 URL。

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，然後選取 [Office 365 用戶端管理]  節點。
2. 按一下儀表板的 [Office 365 安裝程式]  磚，以啟動 [Office 365 用戶端安裝精靈]。 如需詳細資訊，請參閱[部署 Office 365 應用程式](../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps)。
3. 在 [Office 設定]  頁面上，按一下 [移至 Office 網頁]  。 使用線上 Office 自訂工具來指定此部署的設定。 
4. 完成時，按一下右上角的 [提交]  。 完成 [Office 365 用戶端安裝精靈]。



## <a name="improvements-to-cloud-management-gateway"></a>雲端管理閘道的改進
此版本包含對雲端管理閘道 (CMG) 的以下改善：

### <a name="simplified-client-bootstrap-command-line"></a>簡化的用戶端啟動程序命令列
<!--1358215-->
透過 CMG 在網際網路上安裝 Configuration Manager 用戶端時，現在需要較少的命令列屬性。 如需此案例其中一個範例的詳細資訊，請在準備共同管理時，參閱[安裝 Configuration Manager 用戶端的命令列](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)。 

所有案例都需要有下列命令列屬性：
- CCMHOSTNAME  
- SMSSITECODE  

使用 Azure AD 進行用戶端驗證，而不是以 PKI 為基礎的用戶端驗證憑證時，需要下列屬性：
- AADCLIENTAPPID  
- AADRESOURCEURI  

如果用戶端將漫遊回到內部網路，則需要下列屬性：
- SMSMP  

下列範例包含所有上述屬性：   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

如需詳細資訊，請參閱[用戶端安裝屬性](../clients/deploy/about-client-installation-properties.md)。

### <a name="download-content-from-a-cmg"></a>從 CMG 下載內容
<!--1358651-->
之前，您必須將雲端發佈點和 CMG 部署為不同的角色。 目前在此版本中，CMG 也可以提供內容給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。 若要啟用這項功能，請在 CMG 內容的 [設定]  索引標籤上啟用 [允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容]  的新選項。 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>使用 Azure AD 時不需要受信任的根憑證
<!--503899-->
當您建立 CMG 時，不再需要於 [設定] 頁面上提供[受信任的根憑證](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot)。 使用 Azure Active Directory (Azure AD) 進行用戶端驗證時，不需要此憑證，但以前在精靈中需要此憑證。

> [!Important]  
> 如果您要使用 PKI 用戶端驗證憑證，則仍然必須將受信任的根憑證新增至 CMG。



## <a name="improvements-to-secure-client-communications"></a>安全用戶端通訊的改善
<!--1358278,1358279-->
此版本會繼續透過移除網路存取帳戶的其他相依性，反覆[改善安全用戶端通訊](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)。 當您啟用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  的新站台選項時，下列案例不需要網路存取帳戶即可從發佈點下載內容：  

- 從開機媒體或 PXE 執行的工作順序
- 從軟體中心執行的工作順序  

這些工作順序可以是 OS 部署或自訂。 它也支援工作群組電腦。



## <a name="software-center-infrastructure-improvements"></a>軟體中心基礎結構改善
<!--1358309-->
不再需要應用程式類別目錄角色，就能在軟體中心顯示使用者可用的應用程式。 這項變更可協助您減少將應用程式傳遞給使用者所需的伺服器基礎結構。 軟體中心現在依賴管理點來取得這項資訊，這可透過將更大型的環境指派給[界限群組](../servers/deploy/configure/boundary-groups.md#management-points)，協助這些環境更適當地調整大小。

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 從站台移除所有的應用程式類別目錄角色。 這些角色包含應用程式類別目錄 Web 服務點和應用程式類別目錄網站點。
2. 將可用的應用程式部署至使用者集合。
3. 使用軟體中心作為目標使用者來瀏覽、要求和安裝應用程式。

### <a name="known-issue"></a>已知問題
- 如果您使用加入 Azure Active Directory 的用戶端搭配這項功能，請勿將站台設定為 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  。 它目前與此功能相衝突。<!--515846--> 如需這項設定的詳細資訊，請參閱[改善的安全用戶端通訊](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)。



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>為裝置上的所有使用者佈建 Windows 應用程式套件
<!--1358310-->
您現在可以為裝置上的所有使用者，使用 Windows 應用程式套件佈建應用程式。 此案例的其中一個常見範例是從商務用和教育用 Microsoft Store，向學校學生所使用的所有裝置佈建應用程式，例如 Minecraft：教育版。 之前，Configuration Manager 只支援針對每位使用者安裝這些應用程式。 在登入新裝置之後，學生就必須等候存取應用程式。 現在，應用程式會針對所有使用者佈建到裝置，讓他們能夠更快速地提高生產力。

> [!Important]  
> 在裝置上安裝、佈建和更新相同 Windows 應用程式套件的不同版本時，請謹慎處理，因為這可能會造成非預期的結果。 使用 Configuration Manager 佈建應用程式，但接著允許使用者從 Microsoft Store 更新應用程式時，可能會發生這種行為。 如需詳細資訊，請參閱[管理從商務用 Microsoft Store 購買的應用程式](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)時的下一個步驟指引。  

佈建離線授權應用程式時，Configuration Manager 不會讓 Windows 從 Microsoft Store 自動進行更新。  

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 建立新的應用程式。 此應用程式必須來自 Windows 應用程式套件或離線授權應用程式，而後者已從商務用和教育用 Microsoft Store 進行同步處理。  

2. 在 [建立應用程式精靈] 的 [一般資訊]  頁面上，啟用 [在裝置上為所有使用者佈建此應用程式]  的選項。  

   > [!Tip]  
   > 如果您要修改現有的應用程式，此設定位於應用程式內容的 [使用者體驗]  索引標籤上。  

3. 將應用程式部署至裝置集合。  

4. 使用不同的使用者帳戶登入目標裝置，並啟動應用程式。  

> [!Note]  
> 如果您需要從使用者已登入的裝置解除安裝佈建的應用程式，則需要建立兩個解除安裝部署。 將第一個解除安裝部署的目標設為包含裝置的裝置集合。 將第二個解除安裝部署的目標設為包含使用者的使用者集合，且這些使用者已登入具有佈建應用程式的裝置。 在裝置上解除安裝佈建的應用程式時，Windows 目前也不會為使用者解除安裝該應用程式。 



## <a name="improvements-to-the-surface-dashboard"></a>Surface 儀表板的改善
<!--1358654-->
此版本包含對 [Surface 儀表板](../clients/manage/surface-device-dashboard.md)的以下改善：
- 選取圖表區段時，Surface 儀表板現在會顯示相關裝置的清單。
   - 按一下 [Surface 裝置的百分比]  磚會開啟 Surface 裝置的清單。
   - 按一下 [前五個韌體版本]  磚中的長條會開啟含有該特定韌體版本之 Surface 裝置的清單。
- 從 Surface 儀表板檢視這些裝置清單時，您可以用滑鼠右鍵按一下裝置並執行一般動作。



## <a name="hardware-inventory-default-unit-revision"></a>修訂硬體清查預設單位
<!--514442-->
在 [Configuration Manager 1710 版](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure)中，許多報表檢視中使用的預設單位已從百萬位元組 (MB) 變更為十億位元組 (GB)。 因為已進行[大整數值的硬體清查改善](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)，並根據客戶的意見反應修訂，這個預設單位現在又是 MB。



## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
