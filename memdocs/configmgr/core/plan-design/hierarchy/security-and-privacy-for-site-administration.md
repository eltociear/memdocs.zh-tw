---
title: 站台系統管理安全性和隱私權
titleSuffix: Configuration Manager
description: 將 Configuration Manager 中站台管理的安全性和隱私權最佳化
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35c2738b363895671528196e99b324fd2fe6f5a7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704576"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Configuration Manager 中站台管理的安全性和隱私權

適用於：  Configuration Manager (最新分支)

本文包含 Configuration Manager 站台和階層的安全性與隱私權資訊。

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a> 適用於站台管理的安全性指引

使用下列指引，協助您保護 Configuration Manager 站台和階層。  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>從信任的來源執行安裝程式並保護通訊安全

為了協助防止有人竄改來源檔案，請從信任的來源執行 Configuration Manager 安裝程式。 如果在網路上儲存檔案，請保護網路位置。  

如果您從網路位置執行安裝程式，若要協助防止攻擊者竄改透過網路傳送的檔案，可在安裝檔的來源位置和站台伺服器之間使用 IPsec 或 SMB 簽署。  

若您使用安裝程式下載程式來下載安裝程式所需的檔案，請確定您會保護儲存這些檔案的位置。 此外，也會在執行安裝程式時，保護此位置的通訊通道。  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>擴充 Active Directory 結構描述並將站台發佈至網域  

不需要結構描述延伸模組即可執行 Configuration Manager，但它們會建立更安全的環境。 用戶端和站台伺服器可以從信任的來源擷取資訊。  

如果用戶端位於不受信任的網域，請在用戶端的網域部署下列站台系統角色：  

- 管理點  

- 發佈點  

> [!NOTE]  
> Configuration Manager 的受信任網域需要進行 Kerberos 驗證。 如果用戶端位於另一個樹系，且該樹系與站台伺服器的樹系間未採用雙向樹系信任，則這些用戶端會被視為位於不受信任的網域。 外部信任無法滿足此用途。  

### <a name="use-ipsec-to-secure-communications"></a>使用 IPsec 保護通訊安全

雖然 Configuration Manager 可以保護站台伺服器與執行 SQL Server 之電腦間的通訊安全，但 Configuration Manager 無法保護站台系統角色與 SQL Server 之間的通訊安全。 您只能使用 HTTPS 來設定某些站台系統，以進行站台間通訊。  

如果您未使用其他控制項來保護這些伺服器對伺服器的通道，攻擊者便可針對站台系統進行各種詐騙和攔截式攻擊。 當您無法使用 IPsec 時，請使用 SMB 簽署。  

> [!Important]  
> 保護站台伺服器與套件來源伺服器之間通訊通道的安全。 這類通訊都會使用 SMB。 如果您無法使用 IPsec 保護此通訊，請使用 SMB 簽署來確定檔案在用戶端下載並執行它們之前並未遭到竄改。  

### <a name="dont-change-the-default-security-groups"></a>不要變更預設的安全性群組

不要變更下列 Configuration Manager 針對站台系統通訊所建立及管理的安全性群組：

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;站台碼\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;站台碼\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;站台碼\>**  

Configuration Manager 會自動建立及管理這些安全性群組。 此行為包括在移除站台系統角色時移除電腦帳戶。  

為了確保服務持續性及最低權限，請勿手動編輯這些群組。  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>管理信任的根金鑰佈建流程

如果用戶端無法查詢通用目錄以取得 Configuration Manager 資訊，他們就必須仰賴信任的根金鑰來驗證有效的管理點。 信任的根金鑰會儲存於用戶端登錄中。 您可以使用群組原則或手動設定來設定它。  

如果用戶端在第一次與管理點連絡時沒有信任的根金鑰複本，則它會信任第一個與其通訊的管理點。 若要降低攻擊者將用戶端誤導至未經授權管理點的風險，您可以使用受信任的根金鑰預先佈建用戶端。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../security/plan-for-security.md#BKMK_PlanningForRTK)。  

### <a name="use-non-default-port-numbers"></a>使用非預設的連接埠號碼

使用非預設的連接埠號碼可以提供額外的安全性。 它們讓攻擊者更難探索環境以準備進行攻擊。 如果您決定使用非預設的連接埠，請在安裝 Configuration Manager 前先進行規劃。 在階層中的所有網站上一致地使用它們。 用戶端要求連接埠和網路喚醒，都是您可以使用非預設連接埠的範例。  

### <a name="use-role-separation-on-site-systems"></a>在站台系統上使用角色隔離

雖然您可以在單一電腦上安裝所有站台系統角色，但此作法很少用於生產環境網路上。 它會建立單一失敗點。  

### <a name="reduce-the-attack-profile"></a>減少攻擊面

在不同伺服器上隔離各個站台系統角色，可減少針對一個站台系統漏洞進行攻擊，並轉用於攻擊不同站台系統的機會。 許多角色需要在站台系統上安裝 Internet Information Services (IIS)，而此需求會增加攻擊面。 如果您必須合併角色以減少硬體支出，只能將 IIS 角色與其他需要 IIS 的角色合併。  

> [!IMPORTANT]  
> 後援狀態點角色是一項例外。 由於此站台系統角色會接受來自用戶端的未經驗證資料，因此，不要將後援狀態點角色指派給任何其他 Configuration Manager 站台系統角色。  

### <a name="configure-static-ip-addresses-for-site-systems"></a>為站台系統設定靜態 IP 位址

靜態 IP 位址較容易保護名稱解析攻擊。  

靜態 IP 位址也會使 IPsec 的設定較為簡單。 使用 IPsec 是在 Configuration Manager 的站台系統間進行安全通訊的安全性最佳做法。  

### <a name="dont-install-other-applications-on-site-system-servers"></a>不要在站台系統伺服器上安裝其他應用程式

當您在站台系統伺服器上安裝其他應用程式時，會增加 Configuration Manager 的攻擊面。 您也會產生不相容問題的風險。  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>需要簽署及啟用加密作為站台選項

為站台啟用簽署和加密選項。 確定所有用戶端皆可支援 SHA-256 雜湊演算法，然後啟用 [需要 SHA-256]  選項。  

### <a name="restrict-and-monitor-administrative-users"></a>限制並監視系統管理使用者

僅為您信任的使用者授與 Configuration Manager 的系統管理存取權。 接著，使用內建的安全性角色或自訂安全性角色，為他們授與最小權限。 可以建立、修改及部署軟體和設定的系統管理使用者，或許能夠控制 Configuration Manager 階層中的裝置。  

定期稽核系統管理使用者指派及其授權層級，以確認所需的變更。  

如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../../servers/deploy/configure/configure-role-based-administration.md)。  

### <a name="secure-configuration-manager-backups"></a>保護 Configuration Manager 備份

當您備份 Configuration Manager 時，此資訊會包含憑證和其他可由攻擊者用於模擬的機密資料。  

當您透過網路傳送此資料以及保護備份位置時，請使用 SMB 簽署或 IPsec。  

### <a name="secure-locations-for-exported-objects"></a>保護已匯出物件的位置

無論您從 Configuration Manager 主控台匯出或匯入物件至網路位置，都需要保護該位置和保護網路通道。

限制誰可以存取網路資料夾。  

若要防止攻擊者竄改匯出的資料，請在網路位置和站台伺服器之間使用 SMB 簽署或 IPsec。 此外，還需要保護在執行 Configuration Manager 主控台的電腦與站台伺服器之間的通訊安全。 在網路上使用 IPsec 為資料加密，以防止洩露資訊。  

### <a name="manually-remove-certificates-from-failed-servers"></a>從失敗的伺服器手動移除憑證

如果站台系統並未適當地解除安裝，或停止運作且無法還原，請從其他 Configuration Manager 伺服器中手動移除此伺服器的 Configuration Manager 憑證。

若要移除原本使用站台系統和站台系統角色所建立的對等信任，在其他站台系統伺服器上的**受信任的人**憑證存放區中，移除失敗伺服器的 Configuration Manager 憑證。 如果您重新使用伺服器而未對其進行重新格式化，則此動作非常重要。  

如需詳細資訊，請參閱[伺服器通訊的密碼編譯控制項](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication)。  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>不要將以網際網路為基礎的站台系統設定為橋接周邊網路

不要將站台系統伺服器設定為多重主目錄，如此就能讓它們連線到周邊網路和內部網路。 雖然此設定可讓以網際網路為基礎的站台系統接受來自網際網路和內部網路的用戶端連線，但它會消除周邊網路與內部網路之間的安全性界限。  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>設定站台伺服器以起始與周邊網路的連線

如果站台系統位於不受信任的網路上 (例如周邊網路)，請設定站台伺服器以起始與站台系統的連線。

根據預設，站台系統會起始與站台伺服器的連線以傳送資料。 若連線是從不受信任的網路起始到信任的網路，則此設定可能會有安全性風險。 當站台系統接受來自網際網路的連線，或位於不受信任的樹系時，請將站台系統選項設定為 [要求站台伺服器起始與此站台系統的連線]  。 安裝站台系統和所有角色之後，站台伺服器就會從信任的網路起始所有連線。  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>搭配驗證使用 SSL 橋接和終止

如果您使用 Web Proxy 伺服器進行以網際網路為基礎的用戶端管理，請搭配使用終止與驗證，來使用 SSL 橋接至 SSL。

當您在 Proxy Web 伺服器上設定 SSL 終止時，需要檢查來自網際網路的封包，然後再將其轉送到內部網路。 Proxy 網頁伺服器會驗證來自用戶端的連線，將其終止，然後開啟一個全新已驗證的連線，來連線到以網際網路為基礎的站台系統。  

當 Configuration Manager 用戶端電腦使用 Proxy Web 伺服器連線到以網際網路為基礎的站台系統時，用戶端身分識別 (GUID) 會安全地包含於封包承載內。 之後，管理點就不會將 Proxy Web 伺服器視為用戶端。

如果您的 Proxy Web 伺服器無法支援 SSL 橋接的需求，那麼，也會支援 SSL 隧道。 此選項較不安全。 來自網際網路的 SSL 封包會轉送至站台系統，而不會終止。 之後，便無法檢查它們是否含有惡意內容。  

> [!WARNING]  
> 由 Configuration Manager 註冊的行動裝置無法使用 SSL 橋接。 它們必須只使用 SSL 隧道。  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>將站台設定為喚醒電腦以安裝軟體時應使用的設定

- 如果您使用傳統的喚醒封包，請使用單點傳播而非子網路導向的廣播。  

- 如果您必須使用子網路導向的廣播，請將路由器設定為只允許來自站台伺服器的 IP 導向的廣播，且只能在非預設連接埠號碼使用。  

如需不同網路喚醒技術的詳細資訊，請參閱[規劃如何喚醒用戶端](../../clients/deploy/plan/plan-wake-up-clients.md)。

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>如果您使用電子郵件通知，請設定對 SMTP 郵件伺服器的驗證存取

盡可能使用支援驗證存取的郵件伺服器。 使用站台伺服器的電腦帳戶進行驗證。 如果必須指定使用者帳戶進行驗證，請使用具備最低權限的帳戶。  


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> 適用於站台伺服器的安全性指引

使用下列指引，協助您保護 Configuration Manager 站台伺服器。  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>將 Configuration Manager 安裝於成員伺服器，而非網域控制站上

Configuration Manager 站台伺服器和站台系統不需安裝於網域控制站上。 除了網域資料庫外，網域控制站沒有本機安全性帳戶管理 (SAM) 資料庫。 將 Configuration Manager 安裝在成員伺服器上時，您可以在本機 SAM 資料庫而非網域資料庫中維護 Configuration Manager 帳戶。  

此作法也會減少網域控制站上的攻擊面。  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>在不透過網路複製檔案的情況下安裝次要站台

執行安裝程式並建立次要站台時，不要選取將檔案從父站台複製到次要站台的選項。 此外，也不要使用網路來源位置。 透過網路複製檔案時，有經驗的攻擊者仍可劫持次要站台安裝套件，並在安裝檔案之前加以竄改。 進行此攻擊的時機很難掌握。 只要在傳輸檔案時使用 IPsec 或 SMB，就可以緩解這種攻擊。  

不要在次要站台伺服器上透過網路複製檔案，而是將來源檔案從媒體資料夾複製到本機資料夾。 接著，執行安裝程式以建立次要站台時，在 [安裝來源檔]  頁面上選取 [使用位於次要站台電腦上下列位置的來源檔案 (最安全)]  ，然後指定此資料夾。  

如需詳細資訊，請參閱[安裝次要站台](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)。

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>站台角色安裝會繼承磁碟機根目錄的權限

<!-- SCCMDocs#1380 -->
當您將第一個站台系統角色安裝到任何伺服器之前，務必先適當地設定系統磁碟機權限。 例如，`C:\SMS_CCM` 會繼承來自 `C:\` 的權限。 如果磁碟機的根目錄未受到適當保護，則低權限的使用者或許能夠存取或修改 Configuration Manager 資料夾中的內容。


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> 適用於 SQL Server 的安全性指引

Configuration Manager 使用 SQL Server 作為後端資料庫。 如果資料庫遭到入侵，攻擊者就能略過 Configuration Manager。 如果他們直接存取 SQL Server，就能透過 Configuration Manager 發動攻擊。 考量對 SQL Server 進行的攻擊會造成高風險，並適當地進行消減。  

使用以下安全性指引，協助您保護適用於 Configuration Manager 的 SQL Server。  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>不要使用 Configuration Manager 站台資料庫伺服器來執行其他 SQL Server 應用程式

當您增加對 Configuration Manager 站台資料庫伺服器的存取時，此動作會對您的 Configuration Manager 資料增加更多風險。 如果 Configuration Manager 站台資料庫遭到入侵，相同 SQL Server 電腦上的其他應用程式接著也會有危險。  

### <a name="configure-sql-server-to-use-windows-authentication"></a>設定 SQL Server 以使用 Windows 驗證

儘管 Configuration Manager 會使用 Windows 帳戶和 Windows 驗證來存取站台資料庫，但仍可設定 SQL Server 來使用 SQL Server 混合模式。 SQL Server 混合模式允許額外的 SQL 登入存取資料庫。 此設定並非必要且會增加攻擊面。  

### <a name="update-sql-server-express-at-secondary-sites"></a>在次要站台上更新 SQL Server Express

安裝主要站台時，Configuration Manager 會從 Microsoft 下載中心下載 SQL Server Express。 然後，將檔案複製到主要站台伺服器。 當您安裝次要站台並選取安裝 SQL Server Express 的選項時，Configuration Manager 會安裝先前下載的版本。 它不會檢查是否有新版本可供使用。 若要確保次要站台具有最新版本，請執行下列其中一項工作：  

- 當您安裝次要站台之後，在次要站台伺服器上執行 Windows Update。  

- 安裝次要站台之前，先在次要站台伺服器上手動安裝 SQL Server Express。 確定您會安裝最新版本和所有軟體更新。 接著，安裝次要站台，並選取使用現有 SQL Server 執行個體的選項。  

針對所有安裝的 SQL Server 版本，定期執行 Windows Update。 此作法可確保它們具有最新的軟體更新。  

### <a name="follow-general-guidance-for-sql-server"></a>遵循適用於 SQL Server 的一般指引

找出並遵循適用於您 SQL Server 版本的一般指引。 不過，請將下列 Configuration Manager 需求納入考量：  

- 站台伺服器的電腦帳戶必須是執行 SQL Server 之電腦上的系統管理群組成員。 如果您遵循 SQL Server 建議「明確佈建系統管理員主體」，則用來在站台伺服器上執行安裝程式的帳戶就必須是 SQL 使用者群組的成員。  

- 如果您使用網域使用者帳戶來安裝 SQL Server，請確定已針對發佈至 Active Directory Domain Services 的服務主體名稱 (SPN) 設定站台伺服器電腦帳戶。 若無 SPN，Kerberos 驗證會失敗，Configuration Manager 安裝程式也會失敗。  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> 適用於執行 IIS 之站台系統的安全性指引

Configuration Manager 中有多個網站系統角色需要 IIS。 保護 IIS 的程序可讓 Configuration Manager 正常運作，並降低受到安全性攻擊的風險。 在實務上，請將需要 IIS 的伺服器數量降至最低。 例如，僅執行支援用戶端基礎所需的管理點數目，針對以網際網路為基礎的用戶端管理，將高可用性和網路隔離納入考量。  

使用下列指引，協助您保護執行 IIS 的站台系統。  

### <a name="disable-iis-functions-that-you-dont-require"></a>停用您不需要的 IIS 功能

僅針對安裝的站台系統角色安裝最少的 IIS 功能。 如需詳細資訊，請參閱 [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

### <a name="configure-the-site-system-roles-to-require-https"></a>將站台系統角色設定為需要 HTTPS

當用戶端使用 HTTP (而不是使用 HTTPS) 連線到站台系統時，它們會使用 Windows 驗證。 此行為可能會切換回使用 NTLM 驗證，而非 Kerberos 驗證。 使用 NTLM 驗證時，用戶端可能會連線至 Rogue 伺服器 (惡意伺服器)。  

本指引的例外狀況可能是發佈點。 若已針對 HTTPS 設定發佈點，套件存取帳戶便無法運作。 套件存取帳戶會為內容提供授權，如此您就能限制哪些使用者可以存取內容。 如需詳細資訊，請參閱[內容管理的安全性最佳做法](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)。  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>針對站台系統角色，在 IIS 中設定憑證信任清單 (CTL)

站台系統角色  

- 您針對 HTTPS 設定的發佈點  

- 您針對 HTTPS 設定且啟用來支援行動裝置的管理點

CTL 是信任的根憑證授權單位 (CA) 的定義清單。 當您搭配群組原則與公開金鑰基礎結構 (PKI) 部署使用 CTL 時，CTL 可讓您補充網路上所設定的現有信任根 CA。 例如，隨著 Microsoft Windows 自動安裝，或透過 Windows 企業根 CA 新增的 CA。 在 IIS 中設定 CTL 時，它會定義那些信任根憑證 CA 的子集。  

此子集讓您能夠對安全性有更多的控制。 CTL 會將所接受的用戶端憑證限制為僅由 CTL 中的 CA 清單所發出的憑證。 舉例來說，Windows 隨附數個已知的協力廠商 CA 憑證，例如 VeriSign 與 Thawte。

根據預設，執行 IIS 的電腦會信任鏈結至這些已知 CA 的憑證。 在您未針對列出的站台系統角色使用 CTL 來設定 IIS 時，站台會接受擁有從這些 CA 發出之憑證的所有裝置作為有效的用戶端。 如果您使用未包含這些 CA 的 CTL 來設定 IIS，若憑證鏈結至這些 CA，站台就會拒絕用戶端連線。 若要針對列出的站台系統角色接受 Configuration Manager 用戶端，您必須使用指定 Configuration Manager 用戶端所使用之 CA 的 CTL 來設定 IIS。  

> [!NOTE]  
> 只有列出的站台系統角色才會要求您在 IIS 中設定 CTL。 Configuration Manager 用於管理點的憑證簽發者清單會在用戶端電腦連線至 HTTPS 管理點時提供該電腦相同的功能。  

如需如何在 IIS 中設定信任 CA 清單的詳細資訊，請參閱 IIS 文件。  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>不要將站台伺服器放置於具有 IIS 的電腦上

角色分離可協助降低攻擊設定檔，並提昇可復原性。 站台伺服器的電腦帳戶通常會具備所有站台系統角色的管理權限。 如果您使用用戶端推入安裝，它可能也會在 Configuration Manager 用戶端上擁有這些權限。  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>針對 Configuration Manager 使用專屬的 IIS 伺服器

儘管您可以在 Configuration Manager 也使用的 IIS 伺服器上裝載多個 Web 式應用程式，這種作法會明顯增加攻擊面。 設定不良的應用程式可能會讓攻擊者取得 Configuration Manager 站台系統的控制。 此缺口讓攻擊者能夠取得階層的控制。  

如果您必須在 Configuration Manager 站台系統上執行其他 Web 式應用程式，請為 Configuration Manager 站台系統建立自訂網站。  

### <a name="use-a-custom-website"></a>使用自訂網站

針對執行 IIS 的站台系統，設定 Configuration Manager 來使用自訂網站，而非預設網站。 如果您必須在站台系統上執行其他 Web 應用程式，必須使用自訂網站。 這種設定是一種全站台設定，而非針對特定站台系統的設定。  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>當您使用自訂網站時，移除預設虛擬目錄

當您從使用預設網站變更為使用自訂網站時，Configuration Manager 不會移除舊的虛擬目錄。 移除 Configuration Manager 原本在預設網站下建立的虛擬目錄。  

例如，針對發佈點移除下列虛擬目錄：  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>遵循 IIS 伺服器安全性指引

找出並遵循適用於您 IIS 伺服器版本的一般指引。 將 Configuration Manager 對於特定站台系統角色的所有需求都納入考量。 如需詳細資訊，請參閱 [Site and site system prerequisites](../configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> 適用於管理點的安全性指引

管理點是裝置與 Configuration Manager 間的主要介面。 考量對管理點及其執行所在之伺服器所進行的攻擊具有高風險，並適當地進行減緩。 套用所有適當的安全性指引，並監視所有異常活動。  

使用下列指引，協助保護 Configuration Manager 中的管理點。  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>將管理點上的用戶端指派給相同的站台

避免發生下列案例：將位於管理點的 Configuration Manager 用戶端指派給管理點站台以外的站台。  

若您從較早的版本遷移至 Configuration Manager 目前分支，請儘速將管理點上的用戶端遷移至新站台。  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> 適用於後援狀態點的安全性指引

如果您在 Configuration Manager 中安裝後援狀態點，請使用下列安全性指引：

如需安裝後援狀態點時的安全性考量的詳細資訊，請參閱[判定您是否需要後援狀態點](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)。  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>不要在相同的站台系統上執行任何其他角色

後援狀態點的設計是接受來自任何電腦之未經驗證的通訊。 如果您使用其他角色或網域控制站來執行此站台系統角色，則該伺服器的風險就會大幅增加。  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>安裝具有 PKI 憑證的用戶端之前，先安裝後援狀態點

如果 Configuration Manager 站台系統不接受 HTTP 用戶端通訊，您可能會因為與 PKI 相關的憑證問題，而導致您不知道用戶端是非受控的。 如果您將用戶端指派給後援狀態點，它們就會透過後援狀態點回報這些憑證問題。  

基於安全因素，您無法在安裝用戶端之後，為其指派後援狀態點。 您只能在用戶端安裝期間指派此角色。  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>避免在周邊網路中使用後援狀態點

根據設計，後援狀態點會接受來自任何用戶端的資料。 雖然周邊網路中的後援狀態點可協助您進行以網際網路為基礎之用戶端問題的疑難排解，但仍要在疑難排解的好處以及站台系統於公開存取網路內接受未經驗證資料的風險之間取得平衡。  

如果您在周邊網路或任何不受信任的網路中安裝後援狀態點，請設定站台伺服器以起始資料轉送。 不要使用允許後援狀態點來起始與站台伺服器連線的預設設定。  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> 站台管理的安全性問題

檢閱下列 Configuration Manager 安全性問題：  

- Configuration Manager 無法防禦使用 Configuration Manager 攻擊網路的授權系統管理使用者。 未經授權的系統管理使用者具有高安全性風險。 他們可能會啟動許多攻擊，其中包括下列策略：  

    - 在組織內的每部 Configuration Manager 用戶端電腦上，使用軟體部署自動安裝並執行惡意軟體。  

    - 在不使用用戶端權限的情況下，遠端控制 Configuration Manager 用戶端。  

    - 設定快速輪詢間隔和極大量的清查。 本文會針對用戶端和伺服器建立拒絕服務的攻擊。  

    - 使用階層中的一個站台以將資料寫入另一個站台的 Active Directory 資料。  

    站台階層為安全性界限。 請僅將站台視為管理界限。  

    稽核所有系統管理使用者活動並定期檢閱稽核記錄。 要求所有 Configuration Manager 系統管理使用者執行背景檢查後再進行雇用。 要求定期重新檢查作為雇用條件。  

- 如果註冊點遭到洩漏，攻擊者就能取得憑證進行驗證。 他們可以竊取註冊其行動裝置之使用者的認證。  

    註冊點會與 CA 通訊。 它可以建立、修改和刪除 Active Directory 物件。 切勿在周邊網路中安裝註冊點。 一律監視不尋常的活動。  

- 如果您讓使用者原則用於以網際網路為基礎的用戶端管理，則會增加攻擊面。  

    除了針對用戶端對伺服器連線使用 PKI 憑證，這些設定還需要 Windows 驗證。 它們可能會切換回使用 NTLM 驗證，而非 Kerberos。 NTLM 授權會輕易受到模擬和重新執行攻擊。 若要成功驗證網際網路上的使用者，您必須允許從以網際網路為基礎的站台系統連線到網域控制站。  

- 站台系統伺服器上需要 **Admin$** 共用。  

    Configuration Manager 站台伺服器會使用 Admin$ 共用，連線到站台系統並執行服務作業。 請勿停用或移除此共用。  

- Configuration Manager 會使用名稱解析服務來連線到其他電腦。 這些服務難以針對下列安全性攻擊提供保護：
    - 詐騙
    - 竄改
    - 否認性
    - 資訊洩漏
    - 拒絕服務
    - 權限提高

    找出並遵循您用以進行名稱解析之 DNS 版本的所有安全性指引。  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> 適用於探索的隱私權資訊

探索會建立網路資源的記錄，並將其儲存於 Configuration Manager 資料庫中。 探索資料記錄包含 IP 位址、OS 版本和電腦名稱等電腦資訊。 您也可以設定 Active Directory 探索方法，以傳回貴組織儲存於 Active Directory 網域服務中的所有資訊。  

Configuration Manager 預設啟用的唯一探索方法是活動訊號探索。 此方法只會探索已安裝 Configuration Manager 用戶端軟體的電腦。  

不會將探索資訊直接傳送至 Microsoft。 它會儲存於 Configuration Manager 資料庫中。 Configuration Manager 會在資料庫中保留資訊，直到刪除資料為止。 此流程每隔 90 天就會透過站台維護工作 [刪除過時探索資料]  執行一次。  
