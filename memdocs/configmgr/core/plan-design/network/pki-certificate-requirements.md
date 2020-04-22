---
title: PKI 憑證需求
titleSuffix: Configuration Manager
description: 尋找 Configuration Manager 可能會需要之 PKI 憑證的需求。
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6a73e68-57d8-4786-842b-36669541d8ff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3729bdc28cce961bd081ddb461d3d1da45d6c017
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701486"
---
# <a name="pki-certificate-requirements-for-configuration-manager"></a>Configuration Manager 的 PKI 憑證需求

適用於：  Configuration Manager (最新分支)

下表列出 Configuration Manager 可能需要的公開金鑰基礎結構 (PKI) 憑證。 這項資訊假設已具備 PKI 憑證的基本知識。 如需詳細資訊，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](example-deployment-of-pki-certificates.md)。

如需 Active Directory 憑證服務的詳細資訊，請參閱下列文件：  

- Windows Server 2012：[Active Directory 憑證服務概觀](https://go.microsoft.com/fwlink/p/?LinkId=286744)  

- Windows Server 2008：[Windows Server 2008 中的 Active Directory 憑證服務](https://go.microsoft.com/fwlink/p/?LinkId=115018)

如需使用新一代密碼編譯新一代 (CNG) API 憑證與 Configuration Manager 的資訊，請參閱 [CNG 憑證概觀](cng-certificates-overview.md)。


> [!IMPORTANT]  
> Configuration Manager 支援安全雜湊演算法 2 (SHA-2) 憑證。 SHA-2 憑證會帶來重要的安全性優勢。 因此，我們建議：
> - 發行以 SHA-2 (包含 SHA-256 和 SHA-512 等) 簽署的新伺服器及用戶端驗證憑證。
> - 所有網際網路面向服務都應該使用 SHA-2 憑證。 例如，如果購買雲端管理閘道所用的公開憑證，請確定也購買 SHA-2 憑證。  
>
>自 2017 年 2 月 14 日起生效，Windows 將不再信任以 SHA-1 簽署的特定憑證。 我們通常會建議您發行以 SHA-2 (包含 SHA-256 及 SHA-512 及更多) 簽署的新伺服器及用戶端驗證憑證。 此外，我們也建議所有網際網路服務都使用 SHA-2 憑證。 例如，如果您購買要搭配雲端管理閘道使用的公開憑證，請確定您購買的是 SHA-2 憑證。
>
> 在大部分的情況下，變更 SHA-2 憑證對作業沒有任何影響。 如需詳細資訊，請參閱 [Windows Enforcement of SHA1 certificates](https://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-sha1-certificates.aspx) (Windows 強制 SHA1 憑證)。

您可以使用任何 PKI 來建立、部署及管理這些憑證，除了下列例外狀況之外：

- Configuration Manager 註冊於行動裝置和 Mac 電腦上的用戶端憑證
- Microsoft Intune 自動建立以管理行動裝置的憑證

當您使用 Active Directory 憑證服務及憑證範本時，此 Microsoft PKI 解決方案可簡化憑證管理工作。 使用下表中的 [要使用的 Microsoft 憑證範本]  欄，可找出最符合憑證需求的憑證範本。 只有在 Enterprise Edition 或 Datacenter Edition 伺服器作業系統 (例如 Windows Server 2008 Enterprise 和 Windows Server 2008 Datacenter) 上執行的企業憑證授權單位，才能使用範本型憑證。  

 利用下面各節檢視憑證需求。  

##  <a name="pki-certificates-for-servers"></a><a name="BKMK_PKIcertificates_for_servers"></a> 伺服器的 PKI 憑證  

|Configuration Manager 元件|憑證用途|[要使用的 Microsoft 憑證範本]|憑證中的特定資訊|Configuration Manager 中使用憑證的方式|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|執行 Internet Information Services (IIS) 且設定為使用 HTTPS 用戶端連線的站台系統：<br /><br /> <ul><li>管理點</li><li>發佈點</li><li>軟體更新點</li><li>狀態移轉點</li><li>註冊點</li><li>註冊 Proxy 點</li><li>應用程式類別目錄 Web 服務點</li><li>應用程式類別目錄網站點</li><li>憑證登錄點</li></ul>|伺服器驗證|**Web 伺服器**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]** 。<br /><br /> 如果網站系統接受來自網際網路的連線，則 [主體名稱] 或 [主體別名] 必須包含網際網路完整網域名稱 (FQDN)。<br /><br /> 如果站台系統接受來自內部網路的連線，則根據站台系統的設定，[主體名稱] 或 [主體別名] 必須包含內部網路 FQDN (建議使用) 或電腦名稱。<br /><br /> 如果網站系統同時接受來自網際網路及內部網路的連線，則必須同時指定網際網路 FQDN 和內部網路 FQDN (或電腦名稱)，並使用 & 符號分隔兩個名稱。<br /><br /> **注意︰** 若軟體更新點只接受來自網際網路的用戶端連線，則憑證必須同時包含網際網路 FQDN 和內部網路 FQDN。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> Configuration Manager 不會指定此憑證支援的金鑰長度上限。 請查閱您的 PKI 和 IIS 文件，了解此憑證的任何金鑰大小相關問題。|此憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中。<br /><br /> 此網頁伺服器憑證可用來對用戶端驗證這些伺服器，以及使用安全通訊端層 (SSL) 加密用戶端與這些伺服器之間傳送的所有資料。|  
|雲端發佈點|伺服器驗證|**Web 伺服器**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]** 。<br /><br /> [主體名稱] 必須包含 FQDN 格式的客戶定義服務名稱及網域，做為特定雲端架構發佈點執行個體的 [一般名稱]。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援金鑰長度：4,096 位元。|此服務憑證用來對 Configuration Manager 用戶端驗證雲端架構的發佈點服務，以及使用安全通訊端層 (SSL) 加密兩者之間傳送的所有資料。 此憑證必須以公開金鑰憑證標準 (PKCS #12) 格式匯出，而且必須得知密碼，才能在建立雲端架構發佈點時匯入。<br /><br /> **注意：** 此憑證會搭配 Windows Azure 管理憑證使用。 |  
|執行 Microsoft SQL Server 的網站系統伺服器|伺服器驗證|**Web server**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]** 。<br /><br /> [主題名稱] 必須包含內部網路完整網域名稱 (FQDN)。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|此憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中。 Configuration Manager 會自動將此憑證複製到 Configuration Manager 階層中可能需要與伺服器建立信任之伺服器的受信任人存放區。<br /><br /> 這些憑證用於伺服器對伺服器驗證。|  
|SQL Server 叢集：執行 Microsoft SQL Server 的網站系統伺服器|伺服器驗證|**Web server**|**[增強金鑰使用方法]** 值必須包含 **[伺服器驗證 (1。3。6。1。5。5。7。3。1)]** 。<br /><br /> [主題名稱] 必須包含叢集的內部網路完整網域名稱 (FQDN)。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 當您設定 Configuration Manager 以使用 SQL Server 叢集時，憑證必須至少有兩年的有效期間。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|您在叢集中的某個節點上要求並安裝此憑證後，請匯出憑證，再將它匯入 SQL Server 叢集中每個額外的節點。<br /><br /> 此憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中。 Configuration Manager 會自動將此憑證複製到 Configuration Manager 階層中可能需要與伺服器建立信任之伺服器的受信任人存放區。<br /><br /> 這些憑證用於伺服器對伺服器驗證。|  
|下列網站系統角色的網站系統監視：<br /><br /><ul><li>管理點</li><li>狀態移轉點</li></ul>|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 電腦的 [主體名稱] 欄位或 [主體別名] 欄位中必須擁有唯一的值。<br /><br /> **注意︰** 如果您使用多個值作為 [主體別名]，則只會使用第一個值。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|即使未安裝 Configuration Manager 用戶端，列出的站台系統伺服器上仍必須有此憑證。 這項設定可監視這些站台系統角色的健全狀況並回報給網站。<br /><br /> 這些網站系統的憑證必須位於 [電腦] 憑證存放區的 [個人] 存放區中。|  
|執行 Configuration Manager 原則模組與網路裝置註冊服務角色服務的伺服器|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 對於憑證主體或主體別名 (SAN) 並無特定需求。 您可以針對多個執行網路裝置註冊服務之伺服器使用同一個憑證。<br /><br /> 支援 SHA-2 及 SHA-3 雜湊演算法。<br /><br /> 支援金鑰長度：1,024 位元和 2,048 位元。||  
|已安裝發佈點的網站系統|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 對於憑證主體或主體別名 (SAN) 並無特定需求。 您可以針對多個發佈點使用同一個憑證。 不過，建議每個發佈點使用不同的憑證。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|此憑證有兩種用途：<br /><br /><ul><li>在發佈點傳送狀態訊息之前，對啟用 HTTPS 的管理點驗證發佈點。</li><li>若已選取 [為用戶端啟用 PXE 支援]  發佈點選項，憑證會傳送至電腦。 如果作業系統部署程序中的工作順序，包含擷取用戶端原則或傳送清查資訊等用戶端動作，用戶端電腦就能在部署作業系統期間連線到啟用 HTTPS 的管理點。</li></ul> 此憑證僅於作業系統部署程序期間使用，不會安裝到用戶端上。 由於是暫時使用的緣故，如果不想使用多個用戶端憑證，您可以在每次部署作業系統時使用同一個憑證。<br /><br /> 此憑證必須以公開金鑰憑證標準 (PKCS #12) 格式匯出， 而且必須得知密碼，才能匯入至發佈點內容。<br /><br /> **注意︰** 此憑證的需求與部署作業系統之開機映像用戶端憑證相同。 由於需求相同，因此您可以使用相同的憑證檔案。|  
|執行 Microsoft Intune 連接器的網站系統伺服器|用戶端驗證|不適用：Intune 會自動建立此憑證。|[增強金鑰使用方法]  值包含**用戶端驗證 (1.3.6.1.5.5.7.3.2)** 。<br /><br /> 有三個自訂延伸可唯一識別客戶的 Windows Intune 訂閱。<br /><br /> 金鑰大小是 2,048 位元，並且使用 SHA-1 雜湊演算法。<br /><br /> **注意︰** 您無法變更這些設定。 此資訊僅供參考。|此憑證會在您訂閱 Microsoft Intune 時，自動要求並安裝到 Configuration Manager 資料庫。 當您安裝 Microsoft Intune 連接器時，此憑證就會安裝到執行 Microsoft Intune 連接器的網站系統伺服器上。 憑證會安裝在 [電腦] 憑證存放區中。<br /><br /> 此憑證用於使用 Microsoft Intune 連接器對 Microsoft Intune 驗證 Configuration Manager 階層。 兩者之間一律使用安全通訊端層 (SSL) 傳送資料。|  

###  <a name="proxy-web-servers-for-internet-based-client-management"></a><a name="BKMK_PKIcertificates_for_proxyservers"></a> 網際網路型用戶端管理的 Proxy Web 伺服器  
 如果網站支援網際網路型用戶端管理，且您透過使用 SSL 終止 (橋接) 功能進行傳入網際網路連線的方式使用 Proxy Web 伺服器，則該 Proxy Web 伺服器具備下表所列的憑證需求。  

> [!NOTE]  
>  如果您使用 Proxy Web 伺服器但不使用 SSL 終止 (通道) 功能，Proxy Web 伺服器便不需 要其他憑證。  

|網路基礎結構元件|憑證用途|[要使用的 Microsoft 憑證範本]|憑證中的特定資訊|Configuration Manager 中使用憑證的方式|  
|--------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|透過網際網路接受用戶端連線的 Proxy Web 伺服器|伺服器驗證與用戶端驗證|1. <br />                        **Web 伺服器**<br /><br /> 2. <br />                        **工作站驗證**|[主體名稱] 欄位或 [主體別名] 欄位中的網際網路 FQDN。 如果您使用 Microsoft 憑證範本，則 [主體別名] 僅適用於工作站範本。<br /><br /> 支援 SHA-2 雜湊演算法。|此憑證用於對網際網路用戶端驗證下列伺服器，以及加密用戶端及此伺服器之間使用 SSL 傳送的所有資料：<br /><br /><ul><li>以網際網路為基礎的管理點</li><li>以網際網路為基礎的發佈點</li><li>以網際網路為基礎的軟體更新點</li></ul> 用戶端驗證是用於橋接 Configuration Manager 用戶端與網際網路型網站系統之間的用戶端連線。|  

##  <a name="pki-certificates-for-clients"></a><a name="BKMK_PKIcertificates_for_clients"></a> 用戶端的 PKI 憑證  

|Configuration Manager 元件|憑證用途|[要使用的 Microsoft 憑證範本]|憑證中的特定資訊|Configuration Manager 中使用憑證的方式|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Windows 用戶端電腦|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 用戶端電腦的 [主體名稱] 欄位或 [主體別名] 欄位中必須包含唯一值。<br /><br /> **注意︰** 如果您使用多個值作為 [主體別名]，則只會使用第一個值。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|根據預設，Configuration Manager 會在電腦憑證存放區的個人存放區中尋找電腦憑證。<br /><br /> 除了軟體更新點和應用程式類別目錄網站點外，此憑證會在執行 IIS 及設定使用 HTTPS 的站台系統伺服器驗證用戶端。|  
|行動裝置用戶端|用戶端驗證|**驗證的工作階段**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> SHA-1<br /><br /> 支援的金鑰長度上限是 2,048 位元。<br /><br /> **注意：**<br /><br /><ul><li>這些憑證的格式必須是識別名編碼規則 (DER) 編碼二進位 X.509。</li><li>不支援 Base64 編碼的 X.509 格式。</li></ul>|此憑證會在與行動裝置用戶端通訊的站台系統伺服器 (例如管理點和發佈點) 驗證該用戶端。|  
|部署作業系統的開機映像|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 憑證的 [主體名稱] 欄位或 [主體別名 (SAN)] 皆無特定需求，所有開機映像皆可使用同一個憑證。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|如果作業系統部署程序中的工作順序包含擷取用戶端原則或傳送清查資訊之類的用戶端動作，便會使用憑證。<br /><br /> 此憑證僅於作業系統部署程序期間使用，不會安裝到用戶端上。 由於是暫時使用的緣故，如果不想使用多個用戶端憑證，您可以在每次部署作業系統時使用同一個憑證。<br /><br /> 您必須以公開金鑰憑證標準 (PKCS #12) 格式匯出此憑證，而且必須知道密碼，才能將憑證匯入 Configuration Manager 開機映像。<br /><br /> 此憑證是暫時提供給工作順序使用，並非用於安裝用戶端。 如果您的環境只有 HTTPS ，則用戶端必須具備可與站台通訊並且讓部署可以繼續進行的有效憑證。 用戶端可在加入 Active Directory 時自動產生憑證，或您可以使用其他方法安裝用戶端憑證。<br /><br /> **注意︰** 此憑證的需求與裝有發佈點之站台系統的伺服器憑證需求相同。 由於需求相同，因此您可以使用相同的憑證檔案。|  
|Mac 用戶端電腦|用戶端驗證|Configuration Manager 註冊：**驗證的工作階段**<br /><br /> 獨立於 Configuration Manager 的憑證安裝：**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 針對建立使用者憑證的 Configuration Manager，會在憑證的 [主體] 值中自動填入註冊 Mac 電腦之人員的使用者名稱。<br /><br /> 若憑證安裝作業不使用 Configuration Manager 註冊，而是從 Configuration Manager 獨立部署電腦憑證，該憑證的 [主體] 值必須是唯一的。 例如，請指定該電腦的 FQDN。<br /><br /> 不支援 [主體別名] 欄位。<br /><br /> 支援 SHA-2 雜湊演算法。<br /><br /> 支援的金鑰長度上限是 2,048 位元。|此憑證會在與 Mac 用戶端電腦通訊的站台系統伺服器 (例如管理點和發佈點) 驗證該電腦。|  
|Linux 及 UNIX 用戶端電腦|用戶端驗證|**工作站驗證**|**[增強金鑰使用方法]** 值必須包含 **[用戶端驗證 (1。3。6。1。5。5。7。3。2)]** 。<br /><br /> 不支援 [主體別名] 欄位。<br /><br /> 私密金鑰必須可匯出。<br /><br /> 如果用戶端的作業系統支援 SHA-2，則支援 SHA-2 雜湊演算法。 如需詳細資訊，請參閱[規劃在 Configuration Manager 中將用戶端部署至 Linux 和 UNIX 電腦](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)中的[關於不支援 SHA-256 的 Linux 和 UNIX 作業系統](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)一節。<br /><br /> 支援金鑰長度：2,048 位元。<br /><br /> **注意︰** 這些憑證的格式必須是識別名編碼規則 (DER) 編碼二進位 X.509。 不支援 Base64 編碼的 X.509 格式。|此憑證會在與 Linux 或 UNIX 用戶端電腦通訊的站台系統伺服器 (例如管理點和發佈點) 驗證該電腦。 必須以公開金鑰憑證標準 (PKCS#12) 格式匯出此憑證，而且必須知道密碼，才能在指定 PKI 憑證時將此憑證指定至用戶端。<br /><br /> 如需其他資訊，請參閱[規劃在 Configuration Manager 中將用戶端部署至 Linux 和 UNIX 電腦](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)中的[規劃 Linux 和 UNIX 伺服器的安全性與憑證](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_SecurityforLnU)一節。|  
|下列情況適用的根憑證授權單位 (CA) 憑證：<br /><br /><ul><li>作業系統部署</li><li>行動裝置註冊</li><li> 用戶端憑證驗證</li></ul>|信任來源的憑證鏈結|不適用。|標準的根 CA 憑證。|當用戶端需要將通訊伺服器的憑證鏈結到信任的來源時，必須提供根 CA 憑證。 下列情況皆適用：<br /><br /><ul><li>部署作業系統時，以及將用戶端電腦連線至設定使用 HTTPS 之管理點的工作順序執行時。</li><li>當您註冊受 Configuration Manager 管理的行動裝置時。</li></ul> 此外，如果用戶端憑證的 CA 與核發管理點憑證的 CA 屬於不同階層，必須提供用戶端的根 CA 憑證。|  
|由 Microsoft Intune 註冊的行動裝置|用戶端驗證|不適用：Intune 會自動建立此憑證。|[增強金鑰使用方法]  值包含**用戶端驗證 (1.3.6.1.5.5.7.3.2)** 。<br /><br /> 有三個自訂延伸可唯一識別客戶的 Windows Intune 訂閱。<br /><br /> 使用者可以在註冊期間提供憑證主體的值。 不過，Intune 不會使用此值識別裝置。<br /><br /> 金鑰大小是 2,048 位元，並且使用 SHA-1 雜湊演算法。<br /><br /> **注意︰** 您無法變更這些設定。 此資訊僅供參考。|驗證使用者使用 Microsoft Intune 註冊行動裝置時，會自動要求並安裝此憑證。 裝置上產生的憑證位於電腦存放區中，並且會對 Intune 驗證註冊的行動裝置，以便管理該裝置。<br /><br /> 由於憑證中有自訂延伸模組，因此只能驗證針對組織建立的 Intune 訂閱。|
