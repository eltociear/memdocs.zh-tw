---
title: 應用程式的安全性和隱私權
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中管理應用程式時之安全性和隱私權的指引與建議。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689066"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>在 Configuration Manager 中進行應用程式管理的安全性和隱私權

適用於：  Configuration Manager (最新分支)

## <a name="security-guidance-for-application-management"></a>應用程式管理的安全性指引  

### <a name="use-the-software-center-without-the-application-catalog"></a>在沒有應用程式目錄的情況下使用軟體中心

<!--1358309-->

從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 此設定可協助您減少將應用程式傳遞給使用者所需的伺服器基礎結構。

從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。 減少伺服器基礎結構，也會減少受攻擊面。

若要針對以網際網路為基礎的用戶端提供一致且安全的應用程式體驗，請使用 Azure Active Directory 與雲端管理閘道。

如需詳細資訊，請參閱[設定軟體中心](plan-for-software-center.md#bkmk_userex)。

### <a name="use-https-with-the-application-catalog"></a>使用 HTTPS 搭配應用程式類別目錄

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

將「應用程式類別目錄」網站點和「應用程式類別目錄」Web 服務點設定成接受 HTTPS 連線。 使用此設定時，會向使用者驗證伺服器。 傳輸的資料會受到保護，以免遭到竄改和檢視。

藉由教導使用者只連線到受信任的網站，來協助防止社交工程攻擊。 教育使用者惡意網站的危險性。

如果您不使用 HTTPS，請勿使用商標設定選項。 這些設定會在應用程式類別目錄中顯示貴組織的名稱以作為身分識別證明。  


### <a name="use-role-separation"></a>使用角色隔離

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

將應用程式類別目錄網站點和應用程式類別目錄 Web 服務點安裝於不同的伺服器上。 如果網站遭到入侵，便會與 Web 服務點分離。 此設計有助於保護 Configuration Manager 用戶端和基礎結構。 如果網站點會接受來自網際網路的用戶端連線，此設定特別重要。 它讓伺服器更容易遭受攻擊。  

### <a name="close-browser-windows"></a>關閉瀏覽器視窗

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

教育使用者在完成使用應用程式類別目錄之後將瀏覽器視窗關閉。 若使用者以用於應用程式類別目錄的同一個瀏覽器視窗瀏覽外部網站，瀏覽器會繼續使用內部網路中信任站台所適用的安全性設定。  

### <a name="centrally-specify-user-device-affinity"></a>集中指定使用者裝置親和性

手動指定使用者裝置親和性，而不是讓使用者識別自己的主要裝置。 請勿啟用以使用方式為基礎的設定。

請勿將自使用者或裝置收集到的資訊視為已授權。 如果您使用受信任系統管理員未指定的使用者裝置親和性來部署軟體，可能會將該軟體安裝到未獲授權來接收該軟體的電腦和使用者。  

### <a name="dont-run-deployments-from-distribution-points"></a>請勿從發佈點執行部署

一律將部署設定為從發佈點下載內容，而不是直接於發佈點上執行。 當您將部署設定為從發佈點下載內容並於本機執行時，Configuration Manager 用戶端會在下載內容後驗證套件雜湊。 如果該雜湊與原則中的雜湊不相符，用戶端就會捨棄該套件。

如果您將部署設定為直接從發佈點執行，Configuration Manager 用戶端就不會驗證套件雜湊。 此行為意謂著 Configuration Manager 用戶端可以安裝已遭竄改的軟體。

如果您必須直接從發佈點安裝部署，請對發佈點上的套件使用 NTFS 最低權限。 此外，也請使用網際網路通訊協定安全性 (IPsec) 來確保用戶端與發佈點之間的通道安全，以及確保發佈點與站台伺服器之間的通道安全。

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a> 請勿讓使用者與提高權限的處理序互動
  
如果您啟用 [以系統管理權限執行]  或 [針對系統安裝]  選項，請勿讓使用者與那些應用程式互動。 當您設定應用程式時，可以設定 [允許使用者檢視程式安裝並與其互動]  。 此設定可允許使用者回應使用者介面中任何必要的提示。 如果您也將應用程式設定成 [以系統管理權限執行]  (或從 1802 版開始為 [針對系統安裝]  )，執行該程式之電腦上的攻擊者便可透過使用者介面在用戶端電腦上提升權限。

透過使用Windows Installer 的程式進行安裝，並針對需要系統管理認證的軟體部署，使用依使用者提升的權限。 安裝程式必須在不具系統管理認證的使用者內容中執行。 Windows Installer 依使用者提升的權限，提供您部署包含此需求的應用程式時一個最安全的方式。

### <a name="restrict-whether-users-can-install-software-interactively"></a>限制使用者是否可以互動方式安裝軟體

在 [電腦代理程式]  群組中設定 [安裝權限]  用戶端設定。 這項設定會限制可在軟體中心安裝軟體的使用者類型。

例如，您可建立自訂用戶端設定，將 [安裝權限]  設為 [僅限系統管理員]  。 將此用戶端設定套用到伺服器集合。 此設定可防止不具系統管理權限的使用者在那些伺服器上安裝軟體。  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>針對行動裝置，則只能部署已簽署的應用程式

部署行動裝置應用程式時，僅針對由行動裝置信任的憑證授權單位 (CA) 完成程式碼簽署的應用程式進行部署。

例如：

- 由知名 CA (例如 VeriSign) 簽署的廠商應用程式。  

- 您未透過 Configuration Manager 而獨立使用內部 CA 簽署的內部應用程式。  

- 建立應用程式類型與使用簽署憑證時，您使用 Configuration Manager 簽署的內部應用程式。

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>保護行動裝置應用程式簽署憑證的位置

如果您使用 Configuration Manager 中的 [建立應用程式精靈]  簽署行動裝置應用程式，請確保簽署憑證檔案的位置和通訊通道的安全。 為了協助防止提升權限和攔截式攻擊，請將簽署憑證檔案儲存在受保護的資料夾中。

請在下列電腦之間使用 IPsec：

- 執行 Configuration Manager 主控台的電腦
- 儲存憑證簽署檔案的電腦
- 儲存應用程式來源檔案的電腦

或者，在執行 [建立應用程式精靈]  之前，不透過 Configuration Manager 而獨立簽署應用程式。

### <a name="implement-access-controls"></a>實作存取控制

為了保護參照電腦，請實作存取控制。 當您透過瀏覽參照電腦的方式在部署類型中設定偵測方法時，請確定該電腦並未遭到入侵。

### <a name="restrict-and-monitor-administrative-users"></a>限制並監視系統管理使用者

限制並監視您授與下列應用程式管理角色型安全性角色的系統管理使用者︰

- **應用程式系統管理員**
- **應用程式作者**
- **應用程式部署管理員**

即使您已設定以角色為基礎的系統管理，可建立和部署應用程式的系統管理使用者所具有的權限可能比您想像的多。 例如，建立或變更應用程式的系統管理使用者，可以選取其安全性範圍以外的相依應用程式。

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>在具有相同信任層級的虛擬環境中設定 App-V 應用程式

當您設定 Microsoft Application Virtualization (App-V) 虛擬環境時，請選取在虛擬環境中擁有相同信任層級的應用程式。 由於 App-V 虛擬環境中旳應用程式可共用資源 (例如剪貼簿)，請設定虛擬環境，使其選取的應用程式都擁有相同信任層級。

如需詳細資訊，請參閱[建立 App-V 虛擬環境](../deploy-use/create-app-v-virtual-environments.md)。

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>確定 macOS 應用程式來自可信任的來源

如果您部署適用於 macOS 裝置的應用程式，請確定來源檔案均來自可信任的來源。 CMAppUtil 工具不會驗證來源套件的簽章。 請確定該套件來自您信任的來源。 CMAppUtil 工具無法偵測檔案是否已遭竄改。

### <a name="secure-the-cmmac-file-for-macos-apps"></a>保護適用於 macOS 應用程式的 cmmac 檔案

如果您部署適用於 macOS 電腦的應用程式，請保護 **.cmmac** 檔案的位置。 CMAppUtil 工具會產生此檔案，您接著要將它匯入到 Configuration Manager。 此檔案並未經過簽署或驗證。

當您將此檔案匯入到 Configuration Manager 時，請保護通訊通道。 為了協助防止此檔案遭到竄改，將它儲存於受保護的資料夾中。 請在下列電腦之間使用 IPsec：

- 執行 Configuration Manager 主控台的電腦  
- 儲存 **.cmmac** 檔案的電腦  

### <a name="use-https-for-web-applications"></a>針對 Web 應用程式使用 HTTPS

如果您設定 Web 應用程式部署類型，請使用 HTTPS 來保護連線的安全。 如果您使用 HTTP 連結而不是 HTTPS 連結來部署 Web 應用程式，則裝置可能被重新導向到 Rogue 伺服器。 在裝置與伺服器之間傳輸的資料可能會遭到竄改。


## <a name="security-issues-for-application-management"></a>應用程式管理的安全性問題  

- 低權限使用者可在用戶端電腦上從用戶端快取複製檔案。  

     使用者可以讀取用戶端快取，但無法寫入。 但只要有讀取權限，使用者可在不同電腦之間複製應用程式安裝檔案。  

- 低權限的使用者可在用戶端電腦上變更記錄軟體部署歷程記錄的檔案。  

     由於應用程式歷程記錄資訊未受到保護，因此使用者可以針對回報是否已安裝應用程式的檔案進行變更。  

- 未簽署 App-V 套件。  

     Configuration Manager 中的 App-V 套件不支援簽署。 數位簽章可確認內容來自受信任的來源，且在傳輸過程中未遭到更改。 此安全性問題沒有任何風險降低方式。 請依照安全性最佳做法，從受信任的來源和安全的位置下載內容。  

- 已發佈的 App-V 應用程式可供電腦上的所有使用者安裝。  

     若已在電腦上發佈 App-V 應用程式，所有登入該電腦的使用者都可安裝此應用程式。 在發佈應用程式之後，您便無法限制可安裝應用程式的使用者。  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> 應用程式類別目錄需要 Microsoft Silverlight 5 憑證和更高的信任模式  

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

Configuration Manager 用戶端 1710 版和較早版本需要 Microsoft Silverlight 5，其必須在提高權限的信任模式中執行，讓使用者可從應用程式類別目錄安裝軟體。 根據預設，Silverlight 會以部分信任模式執行，以防止應用程式存取使用者資料。 如果尚未安裝，Configuration Manager 就會在用戶端上自動安裝 Microsoft Silverlight 5。 根據預設，Configuration Manager 會將電腦代理程式的 [允許 Silverlight 應用程式在更高的信任模式下執行]  用戶端設定設為 [是]  。 此設定讓已簽署和信任的 Silverlight 應用程式能夠要求更高的信任模式。  

當您安裝應用程式類別目錄網站點站台系統角色時，用戶端會同時將 Microsoft 簽署憑證安裝在每部 Configuration Manager 用戶端電腦上的 [信任的發行者] 電腦憑證存放區中。 此憑證所簽署的 Silverlight 應用程式會在更高的信任模式下執行，這是電腦從「應用程式類別目錄」安裝軟體所需的模式。 Configuration Manager 會自動管理此簽署憑證。 若要提高服務連續性，請勿手動刪除或移動此 Microsoft 簽署憑證。  

> [!WARNING]  
> 啟用 [允許 Silverlight 應用程式在更高的信任模式下執行]  用戶端設定時，會讓已由電腦存放區或使用者存放區上 [受信任的發行者] 憑證存放區中憑證所簽署的所有 Silverlight 應用程式，能夠在更高的信任模式下執行。 此用戶端設定無法特別針對「Configuration Manager 應用程式類別目錄」或針對電腦存放區中的 [受信任的發行者] 憑證存放區，啟用更高的信任模式。 如果惡意程式碼在 [受信任的發行者] 存放區中新增 Rogue 憑證，使用自己 Silverlight 應用程式的惡意程式碼現在便也可以在更高的信任模式下執行。  

如果您將 [允許 Silverlight 應用程式在更高的信任模式下執行]  設定設為 [否]  ，用戶端就無法移除 Microsoft 簽署憑證。  

如需 Silverlight 中信任的應用程式詳細資訊，請參閱[信任的應用程式](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\))。  


## <a name="privacy-information-for-application-management"></a>應用程式管理的隱私權資訊  

應用程式管理可讓您在階層中的任何用戶端上，執行任何應用程式、程式或指令碼。 Configuration Manager 無法控制您所執行的應用程式、程式或指令碼的類型，或是它們所傳輸的資訊類型。 在應用程式部署程序期間，Configuration Manager 可能會於用戶端和伺服器之間，傳輸可識別裝置與登入帳戶的資訊。  

Configuration Manager 會保存軟體部署程序的狀態資訊。 除非用戶端使用 HTTPS 來進行通訊，否則軟體部署狀態資訊在傳輸期間不會進行加密。 此狀態資訊在資料庫中不會以加密形式儲存。  

使用 Configuration Manager 應用程式安裝以遠端、互動或無訊息方式在用戶端上安裝軟體，可能會受到該軟體的軟體授權合約所約束。 這個用法有別於 Configuration Manager 的軟體授權條款。 在您使用 Configuration Manager 部署軟體之前，請一律檢閱並同意軟體授權條款。  

Configuration Manager 會收集關於應用程式的診斷和使用方式資料，Microsoft 會使用這些資料來改進未來版本。 如需詳細資訊，請參閱[診斷和使用方式資料](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。

應用程式部署預設並不會進行，而是需要數個設定步驟才能進行。  

下列功能有助於提升軟體部署的效率：

- **使用者裝置親和性**會將使用者對應到裝置。 Configuration Manager 系統管理員可將軟體部署至使用者。 用戶端會自動將軟體安裝在使用者最常使用的一或多部電腦上。  

- 當您安裝 Configuration Manager 用戶端時，**軟體中心**會自動安裝於裝置上。 使用者會從軟體中心變更設定、瀏覽並安裝軟體。  

- **應用程式類別目錄**是一個讓使用者要求軟體安裝的網站。  

    > [!Important]  
    > 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a> 使用者裝置親和性隱私權資訊

- Configuration Manager 可能會在用戶端與管理點站台系統之間傳輸資訊。 資訊可能會識別電腦與登入帳戶，以及登入帳戶的使用方式摘要。  

- 除非已將管理點設定成要求用戶端使用 HTTPS 進行通訊，否則不會加密在用戶端與伺服器之間傳輸的資訊。  

- 電腦與登入帳戶使用方式資訊 (用來將使用者與裝置對應) 會儲存在用戶端電腦上、傳送到管理點，然後儲存在 Configuration Manager 資料庫中。 根據預設，超過 90 天的舊資訊會從資料庫刪除。 藉由設定 [刪除過時使用者裝置親和性資料]  站台維護工作，就可以設定刪除行為。  

- Configuration Manager 會保存使用者裝置親和性的狀態資訊。 除非已將用戶端設定成使用 HTTPS 來與管理點進行通訊，否則狀態資訊不會在傳輸過程中加密。 狀態資訊不會以加密形式儲存於資料庫。  

- 用於建立使用者與裝置親和性的電腦和登入使用方式資訊會隨時保持啟用狀態。 使用者與系統管理使用者都可提供使用者親和性資訊。  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a> 軟體中心隱私權資訊

- 軟體中心可讓 Configuration Manager 系統管理員發佈任何應用程式、程式或指令碼，以供使用者執行。 Configuration Manager 無法控制類別目錄中所發佈的程式或指令碼的類型，或是它們所傳輸的資訊類型。  

- Configuration Manager 可能會在用戶端與管理點之間傳輸資訊。 此資訊可能會識別電腦與登入帳戶。 除非您設定管理點以要求用戶端使用 HTTPS 進行連線，否則不會加密在用戶端與伺服器之間傳輸的資訊。  

- 應用程式核准要求的相關資訊會儲存在 Configuration Manager 資料庫中。 被取消或拒絕的要求與對應的要求歷程記錄項目，預設會在 30 天後刪除。 藉由設定 [刪除過時應用程式要求資料]  站台維護工作，就可以設定刪除行為。 處於核准與擱置狀態的應用程式核准要求永遠不會遭到刪除。  

- 當您在裝置上安裝 Configuration Manager 用戶端時，即會自動安裝軟體中心。  

### <a name="application-catalog-privacy-information"></a>應用程式類別目錄隱私權資訊

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](plan-for-and-configure-application-management.md#bkmk_remove-appcat)。  

- 根據預設，不會安裝應用程式類別目錄。 此安裝需要數個設定步驟。  

- 應用程式類別目錄可讓 Configuration Manager 系統管理員發佈任何應用程式、程式或指令碼，以供使用者執行。 Configuration Manager 無法控制類別目錄中所發佈的程式或指令碼的類型，或是它們所傳輸的資訊類型。  

- Configuration Manager 可能會在用戶端與應用程式類別目錄站台系統角色之間。 此資訊可能會識別電腦與登入帳戶。 除非已將這些站台系統角色設定成要求用戶端使用 HTTPS 進行連線，否則不會加密在用戶端與伺服器之間傳輸的資訊。  
