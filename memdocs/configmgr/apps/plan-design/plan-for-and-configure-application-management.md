---
title: 規劃應用程式管理
titleSuffix: Configuration Manager
description: 實作和設定必要的相依性，以便在 Configuration Manager 中部署應用程式。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689046"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>在 Configuration Manager 中規劃和設定應用程式管理

適用於：  Configuration Manager (最新分支)

使用本文中的資訊，協助您實作必要的相依性，以便在 Configuration Manager 中部署應用程式。  



## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

執行下列站台系統角色的伺服器上都需要 IIS：

- 管理點  
- 發佈點  

如需詳細資訊，請參閱 [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

> [!Note]  
> 應用程式類別目錄也需要 IIS。 但是，最新分支版本 1806 不支援 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>適用於行動裝置之程式碼簽署應用程式的憑證

進行應用程式程式碼簽署以將其部署至行動裝置時，請勿使用以第 3 版範本 (**Windows Server 2008 Enterprise Edition**) 所產生的憑證。 此憑證範本所建立的憑證與行動裝置適用的 Configuration Manager 應用程式不相容。

如果您的行動裝置應用程式使用 Active Directory 憑證服務進行應用程式程式碼簽署，請勿使用第 3 版的憑證範本。


### <a name="audit-sign-in-events-for-user-device-affinity"></a>針對使用者裝置親和性稽核登入事件  

如果您想要自動建立使用者裝置親和性，請設定用戶端來稽核登入事件。

為了判斷自動使用者裝置親和性，Configuration Manager 用戶端會從 Windows 安全性事件記錄讀取**成功**類型的登入事件。 使用下列兩個稽核原則來啟用這些事件：

- **稽核帳戶登入事件**
- **稽核登入事件**

要自動建立使用者和裝置之間的關聯性，請務必在用戶端電腦上啟用這兩種設定。 您可以使用 Windows 群組原則設定這些設定。

如需使用者裝置親和性的詳細資訊，請參閱[連結使用者和裝置與使用者裝置親和性](../deploy-use/link-users-and-devices-with-user-device-affinity.md)。  



## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性


### <a name="management-point"></a>管理點

用戶端會連絡管理點來下載用戶端原則，以便尋找內容。

從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。

在 1902 版和更早版本中，用戶端會使用管理點來連線到應用程式類別目錄。 如果用戶端無法存取管理點，就無法使用應用程式類別目錄。

> [!Note]  
> 從 1806 版開始，不再需要應用程式類別目錄角色，就能在軟體中心顯示使用者可用的應用程式。 如需詳細資訊，請參閱[設定軟體中心](plan-for-software-center.md#bkmk_userex)。<!--1358309-->  
>
> 從 1906 版開始，即無法安裝新的應用程式類別目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
  

### <a name="distribution-point"></a>發佈點

您的階層中至少需要一個發佈點，才能將應用程式部署到用戶端。 站台伺服器預設會在標準安裝期間啟用一個發佈點站台。 發佈點的數量和位置會根據您環境的特定需求而有所差異。

如需安裝發佈點及管理內容之方式的詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  


### <a name="reporting-services-point"></a>Reporting Services 點

若要使用 Configuration Manager 中的報告來管理應用程式，請先安裝並設定 Reporting Services 點。

如需詳細資訊，請參閱[報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  


### <a name="client-settings"></a>用戶端設計

許多用戶端設定都會控制用戶端如何在裝置上安裝應用程式及使用者體驗。 這些用戶端設定包括下列群組：

- 電腦代理程式  
- 電腦重新啟動  
- 軟體中心  
- 軟體部署  
- 使用者和裝置親和性  

如需詳細資訊，請參閱下列文章：

- [關於用戶端設定](../../core/clients/deploy/about-client-settings.md)  
- [如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>應用程式管理的安全性權限

- **應用程式作者**安全性角色包括建立、變更及淘汰應用程式所需的權限。  

- **應用程式部署管理員**安全性角色包括部署應用程式所需的權限。  

- [應用程式系統管理員]  安全性角色具備 [應用程式作者]  和 [應用程式部署管理員]  等安全性角色的所有權限。  

如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>使用 App-V 4.6 SP1 或更新版的用戶端執行虛擬應用程式

若要在 Configuration Manager 中建立虛擬應用程式，請在裝置上安裝 App-V 4.6 SP1 或更新版本。

此外，需先使用 [Microsoft 支援服務文章 2645225](https://support.microsoft.com/help/2645225) \(英文\) 中所述的 Hotfix 來更新 App-V 用戶端，然後才能部署虛擬應用程式。  


### <a name="application-catalog"></a>應用程式類別目錄

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](#bkmk_remove-appcat)。  

#### <a name="application-catalog-web-service-point"></a>應用程式類別目錄 Web 服務點

應用程式類別目錄 Web 服務點是一個站台系統角色，它會將可從您軟體程式庫取得的軟體相關資訊提供給使用者所存取的應用程式類別目錄網站。

如需如何設定此站台系統角色的詳細資訊，請參閱[安裝並設定應用程式類別目錄](#bkmk_appcat)。  

#### <a name="application-catalog-website-point"></a>應用程式類別目錄網站點

應用程式類別目錄網站點是一個站台系統角色，可提供可用軟體清單給使用者。

如需如何設定此站台系統角色的詳細資訊，請參閱[安裝並設定應用程式類別目錄](#bkmk_appcat)。

#### <a name="discovered-user-accounts-for-application-catalog"></a>適用於應用程式類別目錄的已探索使用者帳戶

Configuration Manager 必須先探索到使用者帳戶，使用者才能檢視及要求應用程式類別目錄中的應用程式。 如需詳細資訊，請參閱[執行探索](../../core/servers/deploy/configure/run-discovery.md)。  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a> 設定軟體中心  

如需對軟體中心進行設定並設定其商標的詳細資訊，請參閱[針對軟體中心進行規劃](plan-for-software-center.md)。


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a> 移除應用程式類別目錄

<!-- SCCMDocs-pr issue 3051 -->

1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。 下列清單摘要說明變更：

- 從 1806 版開始，不再支援應用程式類別目錄網站點的 **Silverlight 使用者體驗**。<!--1358309--> 已不再「需要」  但仍「支援」  應用程式類別目錄 Web 服務點角色。

- 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。

- 1910 版會終止對應用程式類別目錄角色的支援。  

這些反覆的「軟體中心」與管理點改良可簡化您的基礎結構並去除需要應用程式類別目錄才能供使用者部署的情況。 「軟體中心」可以在沒有應用程式類別目錄的情況下提供所有應用程式部署。 此外，若您啟用 TLS 1.2 並搭配應用程式類別目錄使用 HTTP，使用者無法看到以使用者為目標的可用部署。 將 Configuration Manager 更新至 1906 版或更新版本，以受益於這些功能改善。

1. 將所有用戶端更新到 1806 版或更新版本。 建議使用 1906 版。  

1. 設定「軟體中心」商標，而不是在應用程式類別目錄網站角色的屬性中設定。 如需詳細資訊，請參閱[軟體中心用戶端設定](../../core/clients/deploy/about-client-settings.md#software-center)。  

1. 檢閱預設與任何自訂用戶端設定。 在 [電腦代理程式]  群組中，確定 [預設應用程式類別目錄網站點]  是 `(none)`。  

    在 1902 版和更舊的版本中，當階層中沒有任何應用程式類別目錄角色時，用戶端只會切換為使用管理點。 否則，用戶端會繼續使用階層中的其中一個應用程式類別目錄執行個體。 此行為適用於個別主要站台。  

1. 從所有主要站台移除**應用程式類別目錄網站**與**應用程式類別目錄 Web 服務**站台系統角色。

移除應用程式類別目錄角色之後，「軟體中心」會開始使用管理點來進行以使用者為目標的可用部署。 在 1902 版和更早版本中，此變更最多需要 65 分鐘才會發生。 若要在特定用戶端上確認此行為，請檢閱 `SCClient_<username>.log`，並查看類似下一行的項目：

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a> 安裝並設定應用程式類別目錄  

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](#bkmk_remove-appcat)。  

### <a name="step-1-web-server-certificate-for-https"></a>步驟 1：適用於 HTTPS 的 Web 伺服器憑證

如果您使用 HTTPS 連線，請將 Web 伺服器憑證部署到適用於應用程式類別目錄網站點和應用程式類別目錄 Web 服務點的站台系統伺服器。

如果您希望用戶端從網際網路使用應用程式類別目錄，則將 Web 伺服器憑證部署到至少一個管理點。 設定它，讓用戶端可從網際網路連線。

如需憑證需求的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  


### <a name="step-2-client-authentication-certificate-for-https"></a>步驟 2：適用於 HTTPS 的用戶端驗證憑證

如果您使用用戶端 PKI 憑證來與管理點連線，請將用戶端驗證憑證部署到用戶端電腦。 雖然用戶端不會使用用戶端 PKI 憑證來連線到應用程式類別目錄，但它們必須先連線到管理點，才能使用應用程式類別目錄。

在下列案例中，將用戶端驗證憑證部署到用戶端電腦：

- 內部網路上的所有管理點只接受 HTTPS 用戶端連線。
- 用戶端會從網際網路連線到應用程式類別目錄。

如需憑證需求的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>步驟 3：安裝並設定應用程式類別目錄角色

將應用程式類別目錄 Web 服務點和應用程式類別目錄網站角色安裝於相同的站台上。 您不一定要將它們安裝到相同的伺服器上或相同的 Active Directory 樹系中。 不過，應用程式類別目錄 Web 服務點必須與站台資料庫位於相同的樹系中。

如需伺服器放置的詳細資訊，請參閱[規劃站台系統伺服器和站台系統角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)。

> [!NOTE]  
> 在主要站台上安裝應用程式類別目錄。 您無法將它安裝於次要站台或管理中心網站。  

在新的站台系統伺服器或站台中現有的伺服器上，安裝應用程式類別目錄。 如需一般程序的詳細資訊，請參閱[安裝站台系統角色](../../core/servers/deploy/configure/install-site-system-roles.md)。 在新增站台系統角色或建立站台系統伺服器的精靈中，從清單中選取下列角色：  

- **應用程式類別目錄 Web 服務點**  
- **應用程式類別目錄網站點**  

> [!TIP]  
> 如果您想要讓用戶端電腦透過網際網路使用應用程式類別目錄，請指定網際網路完整網域名稱 (FQDN)。  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>確認這些站台系統角色的安裝  

- 狀態訊息：使用元件 **SMS_PORTALWEB_CONTROL_MANAGER** 和 **SMS_AWEBSVC_CONTROL_MANAGER**。  

    例如 **SMS_PORTALWEB_CONTROL_MANAGER** 的狀態識別碼 **1015** 可確認「站台元件管理員」已成功安裝在應用程式類別目錄網站點上。  

- 記錄檔：搜尋 **SMSAWEBSVCSetup.log** 和 **SMSPORTALWEBSetup.log**。  

    如需詳細資訊，請搜尋 **awebsvcMSI.log** 和 **portlwebMSI.log** 記錄檔。  


### <a name="step-4-configure-client-settings"></a>步驟 4：設定用戶端設定

如果您希望所有使用者均擁有相同的設定，請設定預設用戶端設定。 否則，請針對特定集合設定自訂用戶端設定。

如需詳細資訊，請參閱下列文章：

- [關於用戶端設定](../../core/clients/deploy/about-client-settings.md)  
    - 電腦代理程式  
    - 電腦重新啟動  
    - 軟體中心  
    - 軟體部署  
    - 使用者和裝置親和性  
- [如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)  

當 Configuration Manager 用戶端接著下載用戶端原則時，它會使用這些設定來設定裝置。 若要觸發單一用戶端的原則擷取，請參閱[如何管理用戶端](../../core/clients/manage/manage-clients.md)。


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>步驟 5：確認應用程式類別目錄可運作

利用下列程序確認應用程式類別目錄可運作。

> [!NOTE]  
> 應用程式類別目錄使用者體驗需要 Microsoft Silverlight。 如果您直接從瀏覽器使用應用程式類別目錄，請先確認電腦上已安裝 Microsoft Silverlight。  

> [!TIP]  
> 缺少必要條件是應用程式類別目錄在安裝後未能正常運作的最常見原因。 請確認應用程式類別目錄站台系統角色的角色先決條件。 如需詳細資訊，請參閱 [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

在瀏覽器中，輸入應用程式類別目錄網站的位址。 確認網頁會顯示三個索引標籤：[應用程式類別目錄]  、[我的應用程式要求]  和 [我的裝置]  。  

從下列清單中使用應用程式類別目錄的適當位址，其中 `<server>` 是電腦名稱、內部網路 FQDN 或網際網路 FQDN：  

- HTTPS 用戶端連線和預設站台系統角色設定：`https://<server>/CMApplicationCatalog`  

- HTTP 用戶端連線和預設站台系統角色設定：`http://<server>/CMApplicationCatalog`  

- HTTPS 用戶端連線和自訂站台系統角色設定：`https://<server>:<port>/<web application name>`  

- HTTPS 用戶端連線和自訂站台系統角色設定：`http://<server>:<port>/<web application name>`  

> [!NOTE]  
> 如果您已使用網域系統管理員帳戶登入裝置，Configuration Manager 用戶端就不會顯示通知訊息。 例如，指出有新軟體可供使用的訊息。  
