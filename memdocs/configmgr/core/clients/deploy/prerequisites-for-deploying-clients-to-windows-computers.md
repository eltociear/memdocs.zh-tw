---
title: Windows 用戶端部署必要條件
titleSuffix: Configuration Manager
description: 了解將設定管理員用戶端部署至 Windows 電腦的必要條件。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694786"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>在 Configuration Manager 中將用戶端部署至 Windows 電腦的必要條件

適用於：  Configuration Manager (最新分支)

在環境中部署 Configuration Manager 用戶端會擁有下列外部相依性和產品內的相依性。 此外，每一種用戶端部署方法都有自己的相依性，必須符合這些相依性用戶端安裝才能成功。  

如需 Configuration Manager 用戶端之最低硬體和 OS 需求的詳細資訊，請參閱[支援的設定](../../plan-design/configs/supported-configurations.md)。  

> [!NOTE]  
> 本文章只列出最低需求的軟體版本號碼。  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a> Windows 用戶端的必要條件  

使用下列資訊來判斷在 Windows 裝置上安裝 Configuration Manager 用戶端時的必要條件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  

|元件|說明|  
|---|---|  
|Windows Installer 3.1.4000.2435 版|支援針對套件和軟體更新使用 Windows Installer 更新 (.msp) 檔案所需。|  
|Microsoft 背景智慧型傳送服務 (BITS) 2.5 版|需要在用戶端電腦和 Configuration Manager 站台系統之間進行節流資料傳送。 BITS 不會在用戶端安裝期間自動下載。 在電腦上安裝 BITS 時，通常需要重新啟動才能完成安裝。<br /><br /> 大部分作業系統都包含 BITS。 如果沒有的話，請先安裝 BITS，再安裝 Configuration Manager 用戶端。|  
|Microsoft 工作排程器|在用戶端上啟用此服務，以完成用戶端安裝。|  
|SHA-2 程式碼簽署支援|從 1906 版開始，用戶端需要支援 SHA-2 程式碼簽署演算法。 如需詳細資訊，請參閱 [SHA-2 程式碼簽署支援](#bkmk_sha2)。|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a> SHA-2 程式碼簽署支援

<!--SCCMDocs-pr#3404-->
由於 SHA-1 演算法的缺點以及為了符合業界標準，Microsoft 現在只會使用更安全的 SHA-2 演算法來簽署 Configuration Manager 二進位檔。 舊的 Windows OS 版本需要 SHA-2 程式碼簽署支援的更新。 如需詳細資訊，請參閱 [2019 年 Windows 和 WSUS 的 SHA-2 程式碼簽署支援需求](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus)。

如果您未更新這些 OS 版本，則無法安裝 Configuration Manager 用戶端 1906 版。 此行為適用於新的用戶端安裝或從舊版更新。

如果您需要在未更新或比上面列出版本還舊的 Windows 版本上管理用戶端，請使用 Configuration Manager 延伸互通性用戶端 (EIC) 1902 版。 如需詳細資訊，請參閱[延伸互通性用戶端](../../understand/interoperability-client.md)。

> [!Tip]  
> 如果您未使用[自動用戶端更新](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)，並以另一個機制更新用戶端，請務必更新 ccmsetup 的版本。 較舊版的 ccmsetup 可能無法正確驗證 1906 版用戶端二進位檔上的新 SHA-2 程式碼簽署憑證。 例如，如果您將 ccmsetup.exe 複製到檔案共用，或將 ccmsetup.msi 與群組原則搭配使用。<!-- 4963362 -->
>
> 下列用戶端更新機制不應受到影響：
>
> - 用戶端推入安裝：它會使用來自網站的用戶端套件
> - 以軟體更新為基礎的安裝：網站更新會重新發佈至 WSUS
> - Intune MDM 管理的 Windows 裝置：這項機制的支援版本已經支援 SHA-2 程式碼簽署，但使用最新的 ccmsetup.msi 仍然很重要

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a> Configuration Manager 外部的相依性和安裝期間自動下載的相依性  

Configuration Manager 用戶端具有外部相依性。 這些相依性取決於用戶端電腦上的 OS 版本和安裝的軟體。  

如果用戶端需要這些相依性才能完成安裝，就會自動進行安裝。  

|元件|說明|  
|---|---|  
|Windows Update 代理程式 7.0.6000.363 版|Windows 支援更新偵測和部署所需。|  
|Microsoft Core XML Services (MSXML) 6.20.5002 版和更新版本|支援在 Windows 中處理 XML 文件所需。|  
|Microsoft 遠端差異壓縮 (RDC)|最佳化透過網路的資料傳輸所需。|  
|Microsoft Visual C++ 2013 可轉散發套件 12.0.21005.1 版|支援用戶端操作所需。 當您在用戶端電腦上安裝此更新時，可能需要重新啟動以完成安裝。|  
|Microsoft Visual C++ 2005 可轉散發套件 8.0.50727.42 版|針對 1606 版和更早版本，支援 Microsoft SQL Server Compact 作業所需。|  
|Windows Imaging API 6.0.6001.18000|允許 Configuration Manager 管理 Windows 映像 (.wim) 檔案所需。|  
|Microsoft Policy Platform 1.2.3514.0|允許用戶端評估合規性設定所需。|  
|Microsoft .NET Framework 4.5.2 版|支援用戶端操作所需。 如果未安裝 Microsoft .NET Framework 4.5 版或更新版本，就會自動安裝在用戶端電腦上。 如需詳細資訊，請參閱 [關於 Microsoft.NET Framework 4.5.2 版的其他詳細資料](#dotNet)。|  
|Microsoft SQL Server Compact 4.0 SP1 元件|儲存用戶端操作相關資訊所需。|  

> [!Important]
> 最新分支版本 1806 不支援應用程式目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> 如果您仍然使用應用程式目錄網站使用者體驗，則用戶端需要 Microsoft Silverlight 5.1.41212.0。 用戶端不會自動安裝 Silverlight。 應用程式目錄的主要功能現在已包含在軟體中心內。<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a> 關於 Microsoft.NET Framework 4.5.2 版的其他詳細資料  

> [!NOTE]  
> 不再支援 .NET 4.0、4.5 和 4.5.1。 如需詳細資訊，請參閱 [Microsoft .NET Framework 支援週期原則常見問題集](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)。  

Microsoft .NET Framework 4.5.2 版可能需要重新啟動才能完成安裝。 使用者會在系統匣中看到**需要重新啟動** 的通知。 下列常見案例需要用戶端電腦重新啟動：  

- 電腦執行多個 .NET 應用程式或服務。  

- 缺少 .NET 安裝需要的一或多個軟體更新。  

- 電腦還在等待重新啟動前一個安裝的 .NET Framework 軟體更新。  

安裝 .NET Framework 4.5.2 之後，可能需要其他更新。 這些後續更新可能需要另外重新啟動電腦。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

如需詳細資訊，請參閱[判斷用戶端的站台系統角色](plan/determine-the-site-system-roles-for-clients.md)。  

|元件|說明|  
|---|---|  
|管理點|若要部署 Configuration Manager 用戶端，您不需要管理點。 用戶端需要管理點才能透過站台傳輸資訊。 若沒有管理點，就無法管理用戶端電腦。|  
|發佈點|發佈點在用戶端部署和管理中是選擇性但建議使用的站台系統角色。 所有發佈點都會裝載用戶端來源檔案。 在用戶端部署或更新期間，用戶端會尋找最接近的發佈點來下載來源檔案。 如果站台沒有發佈點，電腦就會從其管理點下載用戶端來源檔案。|  
|後援狀態點|後援狀態點在用戶端部署中是選用，但是建議使用網站系統角色。 後援狀態點會追蹤用戶端部署，並且在無法與管理點通訊時，讓 Configuration Manager 站台中的電腦傳送狀態訊息。|  
|Reporting Services 點|Reporting Services 點是選擇性但建議使用的站台系統角色。 它會顯示與用戶端部署和管理相關的報告。 如需詳細資訊，請參閱[報告簡介](../../servers/manage/introduction-to-reporting.md)。|  

### <a name="installation-method-dependencies"></a>安裝方法相依性  

以下是各種用戶端安裝方法特定的必要條件。  

#### <a name="client-push-installation"></a>用戶端推入安裝  

- 站台使用用戶端推入安裝帳戶來連線到電腦，以安裝用戶端。 您可以在 [用戶端推入安裝內容] 的 [帳戶]  索引標籤上，指定這些帳戶。 此帳戶必須是目的地電腦上本機系統管理員群組的成員。  

    如果您未指定用戶端推入安裝帳戶，站台伺服器會使用其電腦帳戶。  

- 站台需要探索您要安裝用戶端的電腦。 至少需要一個 Configuration Manager 探索方法。  

- 電腦擁有 ADMIN$ 共用。  

- 若要將 Configuration Manager 用戶端自動推入探索到的資源，請在 [用戶端推入安裝內容] 中，選取 [Enable client push installation to assigned resources] \(對指派的資源啟用用戶端推入安裝\)  選項。  

- 用戶端電腦需要與發佈點或管理點通訊，才能下載來源檔案。  

- 當您需要 Kerberos 相互驗證時，用戶端必須位於信任的 Active Directory 樹系中。 Windows 中的 Kerberos 依賴 Active Directory 進行相互驗證。<!--1358204-->  

若要使用用戶端推入，您需要下列安全性權限：  

- 若要設定用戶端推入安裝帳戶：[站台]  物件的 [修改]  和 [讀取]  權限。  

- 使用用戶端推送將用戶端安裝至集合、裝置和查詢：[集合]  物件的 [修改資源]  和 [讀取]  權限。  

[基礎結構系統管理員]  預設安全性角色包括管理用戶端推入安裝的必要權限。  

#### <a name="software-update-point-based-installation"></a>以軟體更新點為基礎的安裝  

- 如果您尚未擴充 Active Directory 架構，或是您要安裝另一個樹系中的用戶端，請使用群組原則來佈建 CCMSetup.exe 的安裝參數。 如需詳細資訊，請參閱[如何佈建用戶端安裝內容](deploy-clients-to-windows-computers.md#BKMK_Provision)。  

- 將 Configuration Manager 用戶端發佈到軟體更新點。  

- 若要下載來源檔案，用戶端電腦需要與發佈點或管理點通訊。  

如需管理 Configuration Manager 軟體更新所需的安全性權限，請參閱[軟體更新的必要條件](../../../sum/plan-design/prerequisites-for-software-updates.md)。  

#### <a name="group-policy-based-installation"></a>以群組原則為基礎的安裝  

- 如果您尚未擴充 Active Directory 架構，或是您要安裝另一個樹系中的用戶端，請使用群組原則來佈建 CCMSetup.exe 的安裝參數。 如需詳細資訊，請參閱[如何佈建用戶端安裝內容](deploy-clients-to-windows-computers.md#BKMK_Provision)。  

- 若要下載來源檔案，用戶端電腦需要與發佈點或管理點通訊。  

#### <a name="logon-script-based-installation"></a>登入指令碼為基礎的安裝  

若要下載來源檔案，用戶端電腦需要與發佈點或管理點通訊。 除非您使用下列命令列參數指定 CCMSetup.exe：`ccmsetup /source`  

#### <a name="manual-installation"></a>手動安裝  

若要下載來源檔案，用戶端電腦需要與發佈點或管理點通訊。 除非您使用下列命令列參數指定 CCMSetup.exe：`ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM 安裝

- 需要 Microsoft Intune 訂閱和適當的授權。  

- 需要裝置具有網際網路存取功能，即使它不是以網際網路為基礎。  

- 依使用案例而定，您可能也需要下列一或兩項技術：  

    - Azure Active Directory  

    - 雲端管理閘道  

#### <a name="workgroup-computer-installation"></a>工作群組電腦安裝  

若要存取 Configuration Manager 站台伺服器網域的資源，請針對該站台設定網路存取帳戶。  

如需如何設定網路存取帳戶的詳細資訊，請參閱 [內容管理的基本概念](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>軟體發佈為基礎的安裝 (僅適用於升級)  

- 如果您尚未擴充 Active Directory 架構，或是您要安裝另一個樹系中的用戶端，請使用群組原則來佈建 CCMSetup.exe 的安裝參數。 如需詳細資訊，請參閱[如何佈建用戶端安裝內容](deploy-clients-to-windows-computers.md#BKMK_Provision)。

- 若要下載來源檔案，用戶端電腦需要與發佈點或管理點通訊。  

如需使用應用程式管理來升級 Configuration Manager 用戶端所需的安全性權限，請參閱[應用程式管理的安全性與隱私權](../../../apps/plan-design/security-and-privacy-for-application-management.md)。  

#### <a name="automatic-client-upgrades"></a>自動用戶端升級  

您必須是 [系統高權限管理員]  安全性角色的成員，才能設定自動用戶端升級。  

### <a name="firewall-requirements"></a>防火牆需求  

如果站台系統伺服器與您要安裝 Configuration Manager 用戶端的電腦之間有防火牆，請參閱[用戶端適用的 Windows 防火牆和連接埠設定](windows-firewall-and-port-settings-for-clients.md)。  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a> 行動裝置用戶端的必要條件  

當您在行動裝置上安裝設定管理員用戶端並註冊行動裝置時，請使用此資訊來判斷必要條件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性

- Microsoft 企業憑證授權單位 (CA)，其擁有用於部署及管理行動裝置所需憑證的憑證範本。  

    發行 CA 必須在註冊程序期間自動核准來自行動裝置使用者的憑證要求。  

    如需憑證需求的詳細資訊，請參閱[憑證設定檔的安全性和隱私權](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)。  

- 安全性群組，其中包含可註冊其行動裝置的使用者。  

    此安全性群組用來設定行動裝置註冊期間所使用的憑證範本。  

- 選擇性但建議使用：名為 **ConfigMgrEnroll** 的 DNS 別名 (CNAME 記錄)。 為註冊 Proxy 點的伺服器名稱設定此別名。  

    此 DNS 別名為支援自動探索註冊服務所需。 如果您未設定此 DNS 記錄，使用者就必須在註冊過程中手動指定註冊 Proxy 點的名稱。  

- 執行註冊點和註冊 Proxy 點站台系統角色之電腦的站台系統角色相依性。  

    如需詳細資訊，請參閱[站台系統伺服器支援的作業系統](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性

如需詳細資訊，請參閱[判斷用戶端的站台系統角色](plan/determine-the-site-system-roles-for-clients.md)。  

- 針對 HTTPS 用戶端連線設定且針對行動裝置啟用的管理點  

    在行動裝置上安裝 Configuration Manager 用戶端時一律需要管理點。 除了 HTTPS 設定需求以及為行動裝置啟用之外，必須使用網際網路 FQDN 設定管理點並接受來自網際網路的用戶端連線。  

- 註冊點和註冊 Proxy 點  

    註冊 Proxy 點會管理來自行動裝置的註冊要求，註冊點則可完成註冊程序。 註冊點必須位於與網站伺服器相同的 Active Directory 樹系集中，但註冊 Proxy 點可以位於另一個樹系中。  

- 行動裝置註冊的用戶端設定  

    設定用戶端設定以允許使用者註冊行動裝置並設定至少一個註冊設定檔。  

- Reporting Services 點  

    Reporting Services 點是選用服務，但建議使用可顯示行動裝置註冊與用戶端管理相關報告的網站系統角色。  

    如需詳細資訊，請參閱[報告簡介](../../servers/manage/introduction-to-reporting.md)。  

- 若要設定行動裝置的註冊，您必須擁有下列安全性權限：  

    - 新增、修改以及刪除註冊站台系統角色：[站台]  物件的 [修改]  權限。  

    - 進行註冊的用戶端設定：預設用戶端設定需要 [站台]  物件的 [修改]  權限，自訂用戶端設定則需要 [用戶端代理程式]  權限。  

    [系統高權限管理員]  預設安全性角色包括設定註冊站台系統角色的必要權限。  

- 若要管理已註冊的行動裝置，您必須擁有下列安全性權限：  

    - 抹除或淘汰行動裝置：[集合]  物件的 [刪除資源]  。  

    - 取消抹除或淘汰命令：[集合]  物件的 [刪除資源]  。  

    - 允許及封鎖行動裝置：[集合]  物件的 [修改資源]  。  

    - 從遠端鎖定或重設行動裝置密碼：[集合]  物件的 [修改資源]  。  

    [操作系統管理員]  預設安全性角色包括管理行動裝置的必要權限。  

    如需如何設定安全性權限的詳細資訊，請參閱[以角色為基礎的系統管理基本概念](../../understand/fundamentals-of-role-based-administration.md)和[設定以角色為基礎的系統管理](../../servers/deploy/configure/configure-role-based-administration.md)。  

### <a name="firewall-requirements"></a>防火牆需求

例如路由器與防火牆以及 Windows Firewall (如適用) 等網路干擾裝置都必須允許與行動裝置註冊相關的流量：  

- 行動裝置與註冊 Proxy 點之間：HTTPS (預設為 TCP 443)  

- 註冊 Proxy 點與註冊點之間：HTTPS (預設為 TCP 443)  

如果您使用 Proxy 網頁伺服器，必須設定伺服器允許 SSL 通道作業。 行動裝置不支援 SSL 橋接作業。  
