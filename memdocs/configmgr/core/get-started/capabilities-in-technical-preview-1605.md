---
title: Technical Preview 1605 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1605 版中可用的功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: c38230b44f7f18e3f60cb4c88b31a03e10a37d30
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705596"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Configuration Manager Technical Preview 1605 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1605 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

 **此 Technical Preview 的已知問題：**  

- 在 Technical Preview 1605 中，如果您在安裝後更新管理點的內容，您可能會看到強制主控台關閉的主控台錯誤。  如果發生這種情況，您可以解除安裝管理點，然後使用所需的設定來重新安裝管理點。 或者，您可以修改管理點，再安裝 Technical Preview 1605。  

- 如果您透過 Technical Preview 1604 使用商務用 Windows 市集功能，然後升級至 Technical Preview 1605，您將無法再檢視登入資料。 所有其他功能會繼續運作。 如果您使用 Technical Preview 1604 登入，安裝 Technical Preview 1605 後會保持登入，而不需要採取進一步的動作。  

  **以下是您可以使用此版本試用的新功能。**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> 適用於 Windows 10 裝置的個別應用程式 VPN  
 針對使用 Configuration Manager 與 Intune 管理的 Windows 10 裝置，您可以加入會自動開啟 VPN 連線的應用程式清單，這個 VPN 連線是透過 Configuration Manager 管理主控台所設定。 您可以選擇僅限這些應用程式的 VPN 流量，或繼續允許透過 VPN 連線的所有流量。  

 **需求**：  

-   具備 Intune 的 Configuration Manager  

-   至少一部裝置已部署 Windows 10 VPN 設定檔  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> 安裝軟體更新工作順序的改進  
 已對「安裝軟體更新」工作順序做了下列改進：  

-   您可以使用新的工作順序變數 SMSTSSoftwareUpdateScanTimeout，在「安裝軟體更新」工作順序步驟期間，控制軟體更新掃描的逾時。 預設值為 30 分鐘。  

-   已改進記錄功能。 smsts.log 記錄檔將包含參考其他記錄檔的新記錄檔項目，以協助您在軟體更新安裝程序期間疑難排解問題。  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> 準備 ConfigMgr 用戶端以進行擷取之工作順序步驟的改進  
 「準備 ConfigMgr 用戶端」步驟現在會完全移除 Configuration Manager 用戶端，而不是只移除金鑰資訊。 當工作順序部署擷取的作業系統映像時，每次都會安裝新的 Configuration Manager 用戶端。  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> 必要應用程式部署的寬限期  
 在某些情況下，您可能想要提供更多時間給使用者，以在超過您設定的任何期限之後，還能安裝必要應用程式部署。 例如，如果使用者剛結束休假，他們可能必須等候很長的時間，讓逾期的應用程式部署完成安裝。 不過如果需要，他們仍可隨時立即安裝應用程式。  

 為了協助解決這個問題，您現在可以藉由將 Configuration Manager 用戶端設定部署至集合，來定義**寬限期**。  

 若要設定寬限期，請採取下列動作：  

1. 在用戶端設定的 [電腦代理程式]  頁面上，將新內容 [延後到部署期限後施行的寬限期 (小時)]  設定為 **1** 到 **120** 小時之間的值。  

2. 在新的應用程式部署中，或在現有部署的內容中，選取 [排程]  頁面上的 [根據使用者喜好設定，延遲強制施行此部署，最多可延後用戶端設定中所定義的寬限期]  核取方塊。  

    已選取此核取方塊並以您同時部署用戶端設定之裝置為目標的所有部署，都會使用此寬限期。  

   在此版本中，用戶端裝置不會使用您所設定的寬限期。 如果您設定寬限期並選取此核取方塊，就會在過了期限後使用者所設定的第一個非營業時間內安裝此應用程式。  

   [軟體更新部署精靈]、[自動部署規則精靈] 和 [內容] 頁面都已新增類似的選項。 不過，此 Technical Preview 目前尚未實作這些選項。  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> 遠端裝置動作的全新體驗  
 從 Configuration Manager 主控台執行遠端裝置動作的體驗已改善。  
現在從 [資產與相容性]  工作區存取 [遠端裝置動作]  功能表即可找到 [淘汰/抹除]  、[重設密碼]  、[遠端鎖定]  和 [略過啟用鎖定]  等常見動作。  

 ![新的 [遠端裝置動作] 螢幕擷取畫面](media/New-Remote-Device-Actions.png)  

 您可以在下列位置找到每個作業的狀態：  

- 當您從 [裝置]  節點選取裝置時，在詳細資料窗格中。  

- 在裝置的 [內容]  頁面。  

- 在 [裝置]  節點的主頁面 (預設可能不會看到所有欄)。  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> 商務用 Windows 市集應用程式  
 [商務用 Windows 市集](https://www.microsoft.com/business-store)是您可以在其中為您的組織尋找並個別或大量採購應用程式的地方。 藉由將市集連線到 Configuration Manager，您便可以從 Configuration Manager 主控台管理大量採購應用程式，例如：  

- 您可以將已購買的應用程式清單與 Configuration Manager 進行同步處理  

- 已同步處理的應用程式會出現在 Configuration Manager 主控台中，您可以部署這些應用程式，就像部署任何其他應用程式一樣  

- Configuration Manager 每隔 24 小時會從市集下載應用程式授權資訊，您可以在 Configuration Manager 主控台中檢閱此資訊  

  在 Technical Preview 1604 版中，您可以在 Configuration Manager 主控台中同步處理並檢視商務用 Windows 市集應用程式。 在此版本中，我們新增了從已同步處理的市集應用程式建立和部署 Configuration Manager 應用程式的功能。  

### <a name="set-up-windows-store-for-business-synchronization"></a>設定商務用 Windows 市集同步處理  

1.  在 Azure Active Directory 中，將 Configuration Manager 註冊為 [Web 應用程式和/或 Web API] 管理工具。 這會提供您一個稍後將會需要的用戶端識別碼。  

    1.  在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 [Active Directory] 節點中，選取您的 Azure Active Directory，然後按一下 [應用程式]   >  **[新增]** 。  

    2.  按一下 [加入我的組織正在開發的應用程式]  。  

    3.  輸入應用程式的名稱，選取 [Web 應用程式]  和/或 [Web API]  ，然後按一下 [下一步]  箭號。  

    4.  為 [登入 URL]  和 [應用程式識別碼 URI]  輸入相同的 URL。 URL 可以是任何內容，不需要解析為實際的位址。 例如，您可以輸入 **https://&lt;您的網域>/sccm**。  

    5.  完成精靈。  

2.  在 Azure Active Directory 中，為已註冊的管理工具建立用戶端金鑰。  

    1.  反白選取您剛才建立的應用程式，然後按一下 [設定]  。  

    2.  從 [金鑰]  底下的清單中選取持續時間，然後按一下 [儲存]  。 這會建立一個新的用戶端金鑰。 在您成功將商務用 Windows 市集連線到 Configuration Manager 之前，請勿離開此頁面。  

3.  在商務用 Windows 市集中，將 Configuration Manager 設定為市集管理工具。  

    1.  開啟 [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools)，然後在提示時登入。  

    2.  視需要接受使用條款  

    3.  在 [管理工具]  底下，按一下 [Add a management tool]\ (新增管理工具)  。  

    4.  在 [Search for the tool by name]\(依名稱搜尋工具)  中，輸入您先前在 AAD 中所建立應用程式的名稱，然後按一下 [新增]  。  

    5.  按一下您剛才匯入之應用程式旁邊的 [啟用]  。  

    6.  如果您想要允許購買離線授權的應用程式，請在 [Show Offline-Licensed Apps Wizard]\(顯示離線授權的應用程式精靈)  中，按一下 [是]  。  

4.  從「商務用 Windows 市集」至少購買一個應用程式。  

5.  在 Configuration Manager 主控台的 [管理]  工作區中，展開 [雲端服務]  ，然後按一下 [商務用 Windows 市集]  。  

6.  在 [常用]  索引標籤的 [建立]  群組中，按一下 [新增商務用 Windows 市集帳戶]  。  

7.  從 Azure Active Directory 中，加入您的租用戶識別碼、用戶端識別碼及用戶端金鑰，然後完成精靈。  

8.  完成之後，您就會在 Configuration Manager 主控台的 [商務用 Windows 市集帳戶]  清單中看到您設定的帳戶。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後利用 Microsoft Connect 網站上的 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)頁面，讓我們知道其運作狀況：  

 從商務用 Windows 市集離線授權的應用程式建立和部署 Configuration Manager 應用程式。  

1. 在 Configuration Manager 主控台的 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後按一下 [市集應用程式的授權資訊]  。  

2. 選擇要部署的應用程式，然後在 [常用]  索引標籤的 [建立]  群組中，按一下 [建立應用程式]  。  

   建立 Configuration Manager 應用程式以包含商務用 Windows 市集應用程式。 然後可以如處理任何其他 Configuration Manager 應用程式一樣，部署及監視此應用程式。  

> [!IMPORTANT]  
>  當您使用單一部署類型從離線授權的應用程式建立 Configuration Manager 應用程式時，此應用程式可以部署至受 MDM 管理的裝置，也可以使用 Configuration Manager 用戶端進行管理。 如果您嘗試使用多種部署類型來部署應用程式，安裝將會失敗。  
>   
>  您目前無法使用 Configuration Manager 部署線上授權的應用程式。  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> 大量採購應用程式的一般改進  

-   在此版本中，商務用 Windows 市集和 iOS 應用程式市集的大量採購應用程式已合併到 [市集應用程式的授權資訊]  檢視。  

-   針對 IOS 大量採購應用程式，已從 [建立應用程式精靈] 的 [iOS 瀏覽器的應用程式套件]  對話方塊中移除 [Apple 大量採購方案] 索引標籤。 若要建立 iOS 大量採購應用程式，請使用下列步驟：  

    1.  1.  在 Configuration Manager 主控台的 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後按一下 [市集應用程式的授權資訊]  。  

    2.  2.  選擇要部署的應用程式，然後在 [常用]  索引標籤的 [建立]  群組中，按一下 [建立應用程式]  。  

-   您在 Configuration Manager 主控台中用來取得和上傳大量採購應用程式之 Apple VPP 權杖的位置已變更。 您現在可以在 [雲端服務]   > [Apple 大量採購方案權杖]  節點底下的 [管理]  工作區中執行這項作業。  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> 企業資料保護 (EDP)  
 您可以建立讓您部署企業資料保護 (EDP) 原則的設定項目，包括讓您選擇受保護的應用程式、EDP 保護層級，以及如何在網路上尋找企業資料。 如需 EDP 的詳細資訊，請參閱下列主題：  

- [使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [使用 Configuration Manager 建立和部署 Windows 資訊保護 (WIP) 原則](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> 使用者可從公司入口網站安裝應用程式  
 Configuration Manager 1511 版中引進了內部部署 MDM。 在舊版中，您可以將應用程式部署至受 MDM 管理的 Windows 10 裝置，其部署目的為受內部部署 MDM 管理之裝置的**必要**安裝。  

 在此版本中，您現在可以部署應用程式，其部署目的為可供受內部部署 MDM 管理的 Windows 10 電腦使用者**使用**，而且使用者現在可以自行從公司入口網站安裝這些應用程式。
在此 Technical Preview 中，如果公司入口網站開啟超過 15 分鐘，使用者會看到一則錯誤訊息。 若要解決此問題，請重新啟動公司入口網站。  

### <a name="before-you-start"></a>在您開始使用 Intune 之前  

#### <a name="server-prerequisites"></a>伺服器先決條件  

-   .NET 4.5 或更高版本 (需要重新啟動)  

-   適用於設定指令碼的 PowerShell 3.0 (需要重新啟動)  

#### <a name="client-prerequisites"></a>用戶端先決條件  

-   Windows 10 Desktop 1511 (作業系統組建 10586.218) 或更新版本  

#### <a name="general-prerequisites"></a>一般先決條件  

-   請確定您已完成[內部部署行動裝置管理的準備步驟](https://technet.microsoft.com/library/mt613153.aspx)並[註冊您的裝置](https://technet.microsoft.com/library/mt627870.aspx)。  

-   為了確保在使用公司入口網站時有最佳的應用程式安裝體驗，請確定 Configuration Manager 已連線到 Microsoft Intune。  

-   如果您選擇大量註冊選項，請為已註冊的裝置設定使用者裝置親和性，再嘗試此案例。  

### <a name="configuration-steps"></a>設定步驟  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>安裝應用程式類別目錄角色並啟用行動裝置管理支援  

1.  新增應用程式類別目錄 Web 服務和網站角色  

    1.  選取 [HTTPS 模式]  和 [允許行動裝置使用此應用程式類別目錄 Web 服務點]  選項。  

    2.  此 Technical Preview 的限制：  

        -   您必須解除安裝任何現有的應用程式類別目錄角色，再選取允許行動裝置進行連線的選項。  

        -   請確定只有一組應用程式類別目錄角色，而且這些角色會與註冊點以及註冊 Proxy 點角色共置於同一個站台系統。  

2.  確認下列元件在 Configuration Manager 主控台的 [元件狀態] 節點中運作正常：  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>設定界限  
 設定僅限內部網路發佈點所需的界限。  

> [!NOTE]  
>  行動裝置管理目前只支援 IPv4 範圍界限。  

### <a name="deploy-the-company-portal-application-and-configuration"></a>部署公司入口網站應用程式和設定  

1. 使用此 Technical Preview 隨附的設定指令碼，準備進行公司入口網站部署和設定：  

   1. 開啟提升權限的 PowerShell 命令視窗。  

   2. 執行 **set-executionPolicy RemoteSigned**  

   3. 從 **&lt;SCCM 安裝目錄\>\cd.latest\SMSSETUP\TOOLS\MDM** 資料夾執行 **.\ConfigurationScript.ps1**  

      設定指令碼會執行下列動作：  

   4. 使用相同資料夾中的 **CompanyPortalOnPremisesMDM.appx**，以 Windows 應用程式套件部署類型建立 Configuration Manager 應用程式。  

   5. 建立設定公司入口網站的設定項目和設定基準。  

   6. 部署設定基準和應用程式，並將應用程式新增至所有發佈點。  

   > [!NOTE]
   >  如果應用程式類別目錄角色未與主要站台共置，請採取下列動作：  
   > 
   > - 在 [資產與相容性] 工作區中，找到 [OnPremMDM Portal Configuration CI - server urls]\(OnPremMDM 入口網站設定 CI - 伺服器 URL) 設定項目    
   >   -   將 [相容性規則]  值變更為應用程式類別目錄角色所在之站台系統的完整網域名稱。  

2. 部署公司入口網站應用程式及其設定之後，請使用 Configuration Manager 主控台的 [部署]  區段，確認應用程式和設定基準與指定裝置相容。 公司入口網站會在裝置的 [開始] 功能表中顯示為 [公司入口網站 (Technical Preview)]  。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後利用 Microsoft Connect 網站上的 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)頁面，讓我們知道其運作狀況：  

1.  使用支援的部署類型將數個應用程式部署至使用者集合，其部署目的為 [可用]  。 在此 Technical Preview 中，需要系統管理員核准的應用程式不受支援，而且不會顯示在公司入口網站中。  

2.  使用者接著可以從公司入口網站瀏覽並安裝應用程式。  

     開啟公司入口網站之後，您會看到 **Configuration Manager** 的 [驗證] 對話方塊。請指定使用者的 Active Directory 認證 (格式為 user@domain 或「網域\使用者」) 以進行登入。  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> 提供全新的軟體中心更新和作業系統索引標籤  
 在此版本中，已進行下列變更來改進軟體中心應用程式的配置：  

-   [應用程式]索引標籤已分割成三個不同的索引標籤：[更新]、[作業系統]\(前兩者之前位於 [篩選] 清單中)，以及 [應用程式]。       

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> 提供伺服器群組  
 Configuration Manager Technical Preview 1511 版提供建立集合的功能，此集合中的所有裝置會組成伺服器群組。 之後，您可以設定將軟體更新部署至伺服器群組時所要使用的伺服器群組設定、控制在任何指定時間更新的電腦百分比，以及設定預先部署和部署後 PowerShell 指令碼來執行自訂動作。  

 Configuration Manager Technical Preview 1605 版新增功能來依您定義的指定順序更新伺服器群組中的電腦、新增用以檢視伺服器群組中電腦狀態的增強監視，並提供清除部署鎖定的功能，這在用戶端無法安裝軟體更新時會很有用，而且可防止其他用戶端安裝其軟體更新。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後利用 Microsoft Connect 網站上的 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)頁面，讓我們知道其運作狀況：  

-   我可以建立代表伺服器群組的集合。 針對這項測試，您可以將收集成員資格規則設定為這個集合中有兩部電腦。   

-   我可以指定伺服器群組中的電腦根據集合的伺服器群組設定，依特定順序安裝軟體更新。 使用程序中的範例指令碼來指定預先部署和部署後指令碼。  

-   我可以將軟體更新部署至此集合。 檢閱 C:\temp 中的 start.txt 和 end.txt 檔案 (從範例指令碼建立)，並確認伺服器群組中電腦上的部署開始和結束時間。 如需詳細資訊，請檢閱 UpdatesDeployment.log 檔案。  

#### <a name="to-create-a-collection-for-a-server-group"></a>建立伺服器群組的集合  

1.  [建立裝置集合](https://technet.microsoft.com/library/gg712295.aspx)將伺服器群組的電腦包含在內。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置集合]  ，再以滑鼠右鍵按一下包含伺服器群組電腦的集合，然後按一下 [內容]  。  

3.  在 [一般]  索引標籤上，選取 [所有裝置都屬於相同的伺服器群組]  ，然後按一下 [設定]  。  

4.  在 [伺服器群組設定]  頁面上，指定下列其中一項設定：  

    -   **允許同時更新一部分的電腦**：指定任一時間只能更新某個百分比的用戶端。 例如，集合有 10 個用戶端，且設定在同一時間更新 30% 的用戶端，則在任何指定時間內，只有 3 個用戶端會安裝軟體更新。  

    -   **允許同時更新多部電腦**：指定任一時間只能更新某個數量的用戶端。  

    -   **指定維護順序**：指定集合中的用戶端要按照您設定的順序，一次更新一個。 用戶端只會在清單排位在它前面的用戶端完成軟體更新安裝之後，才安裝軟體更新。  

5.  指定是否要使用預先部署 (節點清空) 指令碼或部署後 (節點繼續) 指令碼。  

    > [!TIP]  
    >  以下是可將目前時間寫入文字檔案之預先部署和部署後指令碼的測試範例：  
    >   
    >  **預先部署**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **部署後**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>將軟體更新部署至伺服器群組並監視狀態  

1.  在伺服器群組集合中[部署軟體更新](https://technet.microsoft.com/library/gg712304.aspx)。  

2.  [監視軟體更新部署](https://technet.microsoft.com/library/gg712304.aspx)。 當用戶端等候安裝軟體更新時，除了軟體更新部署的標準監視檢視之外，也會顯示新狀態描述。 此新狀態會顯示 [正在等候鎖定]  。  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>清除伺服器群組中的電腦部署鎖定  

1.  在 [資產與相容性]  工作區中，按一下 [裝置集合]  ，然後按一下要清除部署鎖定的集合。  

2.  在 [常用]  索引標籤的 [部署]  群組中，按一下 [清除伺服器群組部署鎖定]  。 當用戶端無法安裝軟體更新，並阻止其他用戶端安裝軟體更新時，您可以手動清除部署鎖定。  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Microsoft Defender 進階威脅防護服務支援  
 Microsoft Defender 進階威脅防護 (ATP) 是可協助企業偵測、調查和回應其網路之進階攻擊的服務。 Microsoft Defender ATP 在過去稱為 Windows Defender ATP。 深入了解 [Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection)。 Configuration Manager 可協助您連線到受管理的 Windows 10 Anniversary Edition 用戶端裝置並進行監視。  

### <a name="try-it-now"></a>立即試試看！  
 請嘗試完成下列工作，然後利用 Microsoft Connect 網站上的 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)頁面，讓我們知道其運作狀況：  

- 將裝置連線到 Microsoft Defender 進階威脅防護 (ATP) 線上服務  

- 監視受控裝置的 Microsoft Defender ATP 部署  

  **先決條件**  

- 訂閱 Microsoft Defender 進階威脅防護線上服務  

- 執行 Windows 10 Anniversary Edition (組建 14328 和更新版本) 的用戶端  

- 建立用戶端登入設定檔  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>如何建立登入設定檔  

  1.  登入 Microsoft Defender ATP 線上服務  

  2.  按一下 [Client On-boarding]\(用戶端登入)功能表項目   

  3.  選取 [Configuration Manager]  ，然後按一下 [下載套件]  。  

  4.  下載壓縮的封存檔案 (.zip)，並將內容解壓縮。  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>將適用於 Microsoft Defender ATP 的裝置上架  

1. 在 Configuration Manager 主控台中，瀏覽至 [資產與相容性]   > [概觀]   > [Endpoint Protection]   > [Windows Defender ATP 原則]  ，然後按一下 [建立 Windows Defender ATP 原則]  。 [Microsoft Defender ATP 原則精靈] 隨即開啟。  

2. 輸入Microsoft Defender ATP 原則的 [名稱]  和 [描述]  ，然後選取 [上線]  。 按一下 [下一步]。  

3. **瀏覽**至組織的 Microsoft Defender ATP 雲端服務租用戶所提供設定檔。 按一下 [下一步]  。  

4. 指定為了分析而從受管理裝置收集和分享的範例檔案。  

   - **無** - 不收集任何範例檔案進行分析  

   - **可攜式執行檔** - 收集網路攻擊中可能遭到惡意探索的檔案進行分析，例如程式檔 (.exe)、動態程式庫連結 (.dll) 檔案、字型檔案和類似檔案  

     按一下 [下一步]  。  

5. 檢閱摘要並完成精靈。  

6. 您現已可按一下 [部署]  ，將 Microsoft Defender ATP 原則部署至受管理的用戶端電腦。  

##### <a name="monitor-microsoft-defender-atp"></a>監視 Microsoft Defender ATP  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視]   > [概觀]   > [安全性]  ，然後按一下 [Windows Defender ATP]  。  

2.  檢閱 [Microsoft Defender 進階威脅防護] 儀表板。  

    -   **Windows Defender 代理程式部署狀態** – 已上架使用中 Microsoft Defender ATP 原則，且符合受管理用戶端電腦的數目與百分比  

    -   **Windows Defender ATP 代理程式健全狀況** - 回報其 Microsoft Defender ATP 代理程式狀態的電腦用戶端百分比  

        -   **狀況良好** - 運作正常  

        -   **非使用中** - 在這段期間不會將任何資料傳送至服務  

        -   **代理程式狀態** - Windows 中未執行此代理程式的系統服務  

        -   **未上線** - 已套用原則，但代理程式尚未回報原則上線  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> 內部部署裝置健康情況證明  
 Windows 10 裝置的健康情況證明現在可以設定為使用內部部署基礎結構來進行通訊。 系統管理員可以指定是要透過雲端還是內部部署資源來執行報告。 如果選取內部部署來執行健康情況證明報告，便可接著指定服務的 URL。 這可讓無法存取網際網路的用戶端電腦使用健康情況證明來啟用和管理裝置。  

### <a name="enable-health-attestation-for-on-premises-devices"></a>為內部部署裝置啟用健康情況證明  
 在 1605 版中，我們已修正 Technical Preview 1604 版中發現的一些錯誤。  若要試試看，請使用用戶端代理程式設定來設定內部部署「健康情況證明服務」。  

1.  在 Configuration Manager 主控台中，巡覽至 [管理]   > [概觀]   > [用戶端設定]  ，然後將 [使用內部部署健康情況證明服務]  設定為 [是]  。  

2.  指定 **[內部部署健康情況證明服務 URL]** ，然後按一下 **[確定]** 。  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> 提供在安裝軟體更新後重新啟動 Windows 10 用戶端的新選項  
 如果需要重新啟動的軟體更新使用 Configuration Manager 來進行部署並安裝於電腦上，則會排定擱置重新啟動，並顯示重新啟動對話方塊。 目前針對 Windows 8 和更舊版本，如果您使用 Windows 電源選項 (而不是透過重新啟動對話方塊) 關閉或重新啟動電腦，則在重新啟動電腦之後會保留重新啟動對話方塊，而且在設定的期限時需要重新啟動電腦。 在此 Technical Preview 中，只要 Configuration Manager 軟體更新擱置重新啟動，處於 Windows 電源選項的 Windows 10 電腦上就會有 [更新並重新啟動]  和 [更新並關機]  選項。 使用其中一個選項之後，在重新開機之後不會顯示重新啟動對話方塊。  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> 使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置  
 您現在可以透過匯入國際行動設備識別碼 (IMEI)，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。  您也可以匯入 iOS 裝置的序號。  匯入的資訊將會設定註冊為「公司」之裝置的擁有權。  每一位存取服務的使用者還是需要 Intune 授權。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後利用 Microsoft Connect 網站上的 [Configuration Manager 意見反應計劃](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)頁面，讓我們知道其運作狀況：  

-   匯入 .csv 檔案中的一組 IMEI 編號。 每個資料列可包含此 IMEI 編號，後面接著詳細資料欄位。  

-   從 Configuration Manager 主控台手動匯入 IMEI 編號。  

-   匯入 .csv 檔案中的一組 iOS 序號。 同樣地，每個資料列會包含一個數字，後面接著該裝置的任何詳細資料。  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>使用 IMEI 或 iOS 序號預先宣告公司擁有的裝置  

1. 在 Configuration Manager 主控台中，移至 [資產與相容性]   > [概觀]   > [公司擁有的所有裝置]   > [預先宣告的裝置]  ，然後按一下 [建立預先宣告的裝置]  。 [預先宣告的裝置精靈] 隨即開啟。  

2. 指定您要如何新增裝置資訊：  

   -   **上傳包含 IMEI 編號和詳細資料的 .csv 檔案** - 若要上傳編號清單，請參閱步驟 3。  

   -   **手動新增 IMEI 編號與詳細資料** - 若要手動輸入資訊，請輸入 IMEI 編號或 iOS 序號及裝置的詳細資料，然後繼續進行步驟 4。  

3. 針對上傳的檔案，瀏覽至內含資訊的 .csv 檔案，以預先宣告公司擁有的裝置。 檔案必須具有下列格式，不包括第一列 (僅提供作為指引)：  

   |**IMEI 編號**|**iOS 序列**|**作業系統**|**詳細資料**|
   |---|---|---|---|
   |123456789012345||WINDOWS|公司擁有的 Windows 裝置|
   |123456789012|A0BCD0EFGH0J|IOS|公司擁有的 iOS 裝置|
   |123456789012346||ANDROID|公司擁有的 Android 裝置|

    **欄：**  

   - 欄 1：IMEI 編號 - 每一列都需要 IMEI 編號或 iOS 序號  

   - 欄 2：iOS 序號 - 只能預先宣告 iOS 序號。 針對其他裝置平台則使用 IMEI 編號  

   - 欄 3：裝置的作業系統 (必須全部為大寫)：  

     -   IOS - 所有 iOS 裝置  

     -   WINDOWS - 包含 Windows 手機、Window 10 行動裝置和 Windows 電腦  

     -   ANDROID - 所有 Android 裝置  

   - 欄 4：詳細資料 - Configuration Manager 主控台中所顯示的其他裝置資訊  

     按一下 [下一步]  。  

4. 檢閱檔案匯入的結果。 先前已匯入的 IMEI 或序號會以新的詳細資料更新其詳細資料。  按一下 [下一步]  繼續，或按一下 [上一步]  保留已更新的詳細資料，然後完成精靈。  
