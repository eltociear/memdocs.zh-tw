---
title: 端點之間的通訊
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站台系統與元件如何透過網路通訊。
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587245"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Configuration Manager 中端點之間的通訊

適用於：  Configuration Manager (最新分支)

本文描述 Configuration Manager 站台系統與用戶端如何透過網路通訊。 它包含下列各節：  

- [站台內站台系統之間的通訊](#Planning_Intra-site_Com)  
  - [站台伺服器到發佈點](#bkmk_site2dp)  

- [從用戶端到站台系統和服務的通訊](#Planning_Client_to_Site_System)  
  - [用戶端到管理點的通訊](#bkmk_client2mp)  
  - [用戶端到發佈點的通訊](#bkmk_client2dp)  
  - [從網際網路或未受信任之樹系的用戶端通訊考量](#BKMK_clientspan)  

- [跨 Active Directory 樹系的通訊](#Plan_Com_X-Forest)  
  - [支援樹系中站台伺服器樹系不信任的網域電腦](#bkmk_noforesttrust)  
  - [支援工作群組中的電腦](#bkmk_workgroup)  
  - [可支援跨多個網域和樹系之站台或階層的案例](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> 站台內站台系統之間的通訊  

當 Configuration Manager 站台系統或元件透過網路與其他站台系統或站台中的元件通訊時，會根據站台設定方式來使用下列其中一項通訊協定：  

- 伺服器訊息區 (SMB)  

- HTTP  

- HTTPS  

除了從站台伺服器到發佈點的通訊以外，站台中伺服器對伺服器的通訊可能會在任何時間發生。 這些通訊不會使用任何機制來控制網路頻寬。 由於您無法控制站台系統之間的通訊，因此請務必將站台系統伺服器安裝在快速且網路連線良好的位置。  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a> 站台伺服器到發佈點

為了協助您管理從站台伺服器到發佈點的內容傳送，請使用下列策略：  

- 設定網路頻寬控制與排程的發佈點。 這些控制與站台間位址所使用的設定相似。 當傳送內容至遠端網路位置是您主要的頻寬考量時，即可使用此設定，而不需安裝另一個 Configuration Manager 站台。  

- 您可以將發佈點安裝為預先設置的發佈點。 預先設置的發佈點可讓您使用以手動方式放置於發佈點伺服器的內容，並可免除透過網路傳送內容檔案的需求。  

如需詳細資訊，請參閱[管理內容管理的網路頻寬](manage-network-bandwidth.md)。

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> 從用戶端到站台系統和服務的通訊

用戶端會起始與站台系統角色、Active Directory 網域服務及線上服務的通訊。 若要啟用這些通訊，防火牆必須允許用戶端和其通訊端點之間的網路流量。 如需用戶端與這些端點進行通訊時所用連接埠和通訊協定的詳細資訊，請參閱 [Configuration Manager 中使用的連接埠](ports.md)。  

用戶端必須先使用服務位置找到支援用戶端通訊協定 (HTTP 或 HTTPS) 的角色，才能與站台系統角色通訊。 根據預設，用戶端會使用最安全的可用方法。 如需詳細資訊，請參閱[了解用戶端如何找到站台資源和服務](understand-how-clients-find-site-resources-and-services.md)。  

若要使用 HTTPS，請設定下列其中一個選項：  

- 使用公開金鑰基礎結構 (PKI)，並在用戶端與伺服器上安裝 PKI 憑證。 如需如何使用憑證的資訊，請參閱 [PKI 憑證需求](../network/pki-certificate-requirements.md)。  

- 從 1806 版開始，您可以將站台設定為 [對 HTTP 站台系統使用 Configuration Manager 產生的憑證]  。 如需詳細資訊，請參閱[Enhanced HTTP](enhanced-http.md) (增強 HTTP)。  

在部署使用網際網路資訊服務 (IIS) 並支援從用戶端進行通訊的網站系統角色時，您必須指定用戶端要使用 HTTP 或 HTTPS 連線至網站系統。 如果您使用 HTTP，您也必須考慮簽署和加密選擇。 如需詳細資訊，請參閱[規劃簽署與加密](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption)。  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a> 用戶端到管理點的通訊

當用戶端與管理點通訊時，有兩個策略：驗證 (傳輸) 和授權 (訊息)。 此程序會視下列因素而有所不同：

- 站台設定：僅限 HTTPS、允許 HTTP 或 HTTPS，或允許已啟用增強 HTTP 的 HTTP 或 HTTPS
- 管理點設定：HTTPS 或 HTTP
- 以裝置為中心案例的裝置身分識別
- 以使用者為中心案例的使用者身分識別

請使用下表來了解此程序的運作方式：  

| MP 類型  | 用戶端驗證  | 用戶端授權<br>裝置身分識別  | 用戶端授權<br>使用者身分識別  |
|----------|---------|---------|---------|
| HTTP     | 匿名<br>使用增強 HTTP，站台會驗證 Azure AD 的「使用者」  或「裝置」  權杖。 | 位置要求：匿名<br>用戶端套件：匿名<br>登錄，使用下列其中一個方法來證明裝置身分識別：<br> - 匿名 (手動核准)<br> - Windows 整合式驗證<br> - Azure AD 的「裝置」  權杖 (增強 HTTP)<br>登錄後，用戶端會使用訊息簽署來證明裝置身分識別 | 在以使用者為中心的案例中，使用下列其中一個方法來證明使用者身分識別：<br> - Windows 整合式驗證<br> - Azure AD 的「使用者」  權杖 (增強 HTTP) |
| HTTPS    | 使用下列其中一個方法：<br> - PKI 憑證<br> - Windows 整合式驗證<br> - Azure AD 的「使用者」  或「裝置」  權杖 | 位置要求：匿名<br>用戶端套件：匿名<br>登錄，使用下列其中一個方法來證明裝置身分識別：<br> - 匿名 (手動核准)<br> - Windows 整合式驗證<br> - PKI 憑證<br> - Azure AD 的「使用者」  或「裝置」  權杖<br>登錄後，用戶端會使用訊息簽署來證明裝置身分識別 | 在以使用者為中心的案例中，使用下列其中一個方法來證明使用者身分識別：<br> - Windows 整合式驗證<br> - Azure AD 的「使用者」  權杖 |

> [!Tip]  
> 如需為不同裝置身分識別類型設定管理點及搭配雲端管理閘道使用的詳細資訊，請參閱[啟用 HTTPS 的管理點](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a> 用戶端到發佈點的通訊

當用戶端與發佈點通訊時，它只需要在下載內容之前進行驗證。 請使用下表來了解此程序的運作方式：

| DP 類型  | 用戶端驗證  |
|----------|---------|
| HTTP     | - 匿名 (若允許)<br>- 使用電腦帳戶或網路存取帳戶進行 Windows 整合式驗證<br> - 內容存取權杖 (增強 HTTP) |
| HTTPS    | - PKI 憑證<br> - 使用電腦帳戶或網路存取帳戶進行 Windows 整合式驗證<br> - 內容存取權杖 |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a>從網際網路或未受信任之樹系的用戶端通訊考量

如需詳細資訊，請參閱下列文章：

- [規劃雲端管理閘道](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [以網際網路為基礎的用戶端管理規劃](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> 跨 Active Directory 樹系的通訊  

Configuration Manager 支援跨 Active Directory 樹系的站台與階層。 它也支援不在相同 Active Directory 樹系作為站台伺服器的網域電腦，以及工作群組中的電腦。  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a> 支援樹系中站台伺服器樹系不信任的網域電腦

- 在該不受信任的樹系中安裝站台系統角色，並可選擇是否將站台資訊發佈至 Active Directory 樹系  

- 管理這些電腦，如同它們是工作群組電腦一樣  

在不受信任的 Active Directory 樹系中安裝站台系統伺服器時，會將樹系中來自用戶端的用戶端到伺服器通訊保留在該樹系內，而且 Configuration Manager 可以使用 Kerberos 驗證電腦。 將站台資訊發佈至用戶端樹系時，用戶端可以從其 Active Directory 樹系擷取網站資訊 (如可用管理點清單)，而不用從其指派的管理點下載此資訊。  

> [!NOTE]  
> 若想管理網際網路上的裝置，您可以在站台系統伺服器位於 Active Directory 樹系時，在您的周邊網路中安裝以網際網路為基礎的站台系統角色。 此案例並不需要在周邊網路與站台伺服器的樹系間建立雙向信任。  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a> 支援工作群組中的電腦  

- 在工作群組電腦使用 HTTP 用戶端連線到站台系統角色時，手動核准工作群組電腦。 Configuration Manager 無法使用 Kerberos 來驗證這些電腦。  

- 請設定工作群組用戶端使用網路存取帳戶，這些電腦才能從發佈點擷取內容。  

- 提供工作群組用戶端尋找管理點的替代機制。 使用 DNS 發佈、WINS，或直接指派管理點。 這些用戶端無法從 Active Directory 網域服務擷取站台資訊。  

如需詳細資訊，請參閱下列文章：  

- [管理衝突的記錄](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [網路存取帳戶](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [如何在工作群組電腦上安裝 Configuration Manager 用戶端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> 可支援跨多個網域和樹系之站台或階層的案例  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>案例 1：跨樹系階層中網站間的通訊

此案例需要支援 Kerberos 驗證的雙向樹系信任。  如果您沒有支援 Kerberos 驗證的雙向樹系信任，Configuration Manager 就不支援遠端樹系中的子站台。  

Configuration Manager 支援在遠端樹系中 (需要父站台樹系內的雙向信任) 安裝子站台。 例如，只要存在所需的信任，您可以在與主要父站台不同的樹系中放置次要站台。  

> [!NOTE]  
> 子站台可以是主要站台 (其中管理中心網站是父站台) 或次要站台。  

Configuration Manager 中的站台間通訊使用資料庫複寫和以檔案為基礎的傳輸。 安裝站台時，必須指定帳戶，以便在指定伺服器上安裝站台。 此帳戶也會建立與維護網站間的通訊。 站台成功安裝並起始以檔案為基礎的傳輸與資料庫複寫後，就不需要為了與站台通訊設定其他項目。  

存在雙向樹系信任時，Configuration Manager 就不需要任何其他設定步驟。  

根據預設，當您安裝新的子站台時，Configuration Manager 會設定下列元件：  

- 每個站台以檔案為基礎的站台間複寫路由 (其使用站台伺服器電腦帳戶)。 Configuration Manager 會將每部電腦的電腦帳戶加入目的地電腦的 **SMS_SiteToSiteConnection_&lt;站台碼\>** 群組中。  

- 每個站台上 SQL Server 之間的資料庫複寫。  

另請進行下列設定：  

- 中介防火牆和網路裝置必須允許 Configuration Manager 要求的網路封包。  

- 樹系間的名稱解析必須能夠運作。  

- 若要安裝網站或網站系統角色，您必須指定一個在指定電腦上具備本機系統管理權限的帳戶。  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>案例 2：跨樹系站台中的通訊

此案例不需要雙向樹系信任。  

主要站台支援將站台系統角色安裝到遠端樹系的電腦上。  

- 應用程式類別目錄 Web 服務點是唯一的例外。  只有與站台伺服器相同的樹系中才予以支援。  

- 站台系統角色接受來自網際網路的連線時，作為安全性最佳做法，請將這些站台系統角色安裝在樹系界限會為站台伺服器提供保護的位置 (例如周邊網路中)。  

在不受信任之樹系中的電腦上安裝站台系統角色：  

- 指定站台用來安裝站台系統角色的**站台系統安裝帳戶**。 (帳戶必須具有本機系統管理認證才能連接。)然後在指定電腦上安裝站台系統角色。  

- 選取 [要求站台伺服器起始與此站台系統的連線]  站台系統選項。 此設定要求站台伺服器必須建立與站台系統伺服器間的連線，以傳輸資料。 這項設定可防止位於不受信任位置的電腦起始與受信任網路內站台伺服器的聯繫。 這些連線會使用 **網站系統安裝帳戶**。  

若要使用安裝在不受信任樹系中的站台系統角色，防火牆必須允許網路流量，即使站台伺服器會起始資料傳輸亦同。  

此外，下列網站系統角色需要直接存取網站資料庫。 因此，防火牆必須允許來自不受信任的樹系到站台 SQL Server 的適用流量：  

- Asset Intelligence 同步處理點  

- Endpoint Protection 點  

- 註冊點  

- 管理點  

- Reporting Service 點  

- 狀態移轉點  

如需詳細資訊，請參閱 [Configuration Manager 中使用的連接埠](ports.md)。  

您可能需要設定站台資料庫的管理點和註冊點存取權。

- 根據預設，當您安裝這些角色時，Configuration Manager 會設定新站台系統伺服器的電腦帳戶作為站台系統角色的連線帳戶。 然後會將帳戶新增至適當的 SQL Server 資料庫角色。  

- 在不受信任的網域中安裝這些站台系統角色時，請設定站台系統角色連線帳戶啟用站台系統角色，以便從資料庫取得資訊。  

如果您將網域使用者帳戶設定為這些站台系統角色的連線帳戶，請確定網域使用者帳戶能正確存取該站台上的 SQL Server 資料庫：  

- 管理點：**管理點資料庫連線帳戶**  

- 註冊點：**註冊點連線帳戶**  

在您規劃其他樹系中的網站系統角色時，請考量以下其他資訊：  

- 如果您執行 Windows 防火牆，請設定適用的防火牆設定檔，以便在站台資料庫伺服器和安裝有遠端站台系統角色的電腦間傳遞通訊。

- 以網際網路為基礎的管理點信任包含使用者帳戶的樹系時，即支援使用者原則。 不存在信任時，就僅支援電腦原則。  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>案例 3：用戶端並未與站台伺服器處於相同 Active Directory 樹系時，用戶端與站台系統角色間的通訊

當用戶端與其站台的站台伺服器不在相同的樹系中時，Configuration Manager 支援以下情況：  

- 在用戶端樹系與站台伺服器樹系間存在雙向樹系信任。  

- 站台系統角色伺服器位於與用戶端相同的樹系中。  

- 用戶端位於網域電腦上，該電腦和站台伺服器間不存在雙向樹系信任，而在用戶端樹系中未安裝站台系統角色。  

- 用戶端位於工作群組電腦上。  

加入網域之電腦上用戶端的站台發佈到其 Active Directory 樹系時，這些用戶端就可以使用服務位置的 Active Directory 網域服務。  

若要將站台資訊發佈至另一個 Active Directory 樹系：  

- 指定樹系，然後在 [系統管理]  工作區的 [Active Directory 樹系]  節點中啟用發佈至該樹系。  

- 設定每個站台將其資料發佈至 Active Directory 網域服務。 此設定可啟用該樹系中的用戶端，以擷取網站資訊和找出管理點。 針對無法在服務位置使用 Active Directory 網域服務的用戶端，您可以使用 DNS、WINS，或用戶端指派的管理點。  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a> 案例 4：將 Exchange Server 連接器放在遠端樹系中  

若要支援此案例，請確定樹系間的名稱解析運作正常。 例如，設定 DNS 轉寄。 當您設定 Exchange Server 連接器時，請指定 Exchange Server 的內部網路 FQDN。 如需詳細資訊，請參閱[使用 Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

## <a name="see-also"></a>請參閱

- [規劃安全性](../security/plan-for-security.md)  

- [Configuration Manager 用戶端的安全性和隱私權](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
