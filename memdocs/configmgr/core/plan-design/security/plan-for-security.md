---
title: 規劃安全性
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 的安全性最佳做法與相關資訊。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4c10922bbe855bfbd89228d1887db06399c261ca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695776"
---
# <a name="plan-for-security-in-configuration-manager"></a>規劃 Configuration Manager 中的安全性

適用於：  Configuration Manager (最新分支)

本文描述規劃 Configuration Manager 實作安全性時可考量的概念。 它包含下列各節：  

- [規劃憑證 (自我簽署與 PKI)](#BKMK_PlanningForCertificates)  
  - [密碼編譯：新一代 (CNG) 憑證](#bkmk_plan-cng)  
  - [增強 HTTP](#bkmk_plan-ehttp)  
  - [CMG 和 CDP 的憑證](#bkmk_plan-cmgcdp)  
  - [站台伺服器簽署憑證 (自我簽署)](#bkmk_plansitesign)  
  - [PKI 憑證撤銷](#BKMK_PlanningForCRLs)  
  - [PKI 受信任的根憑證和憑證簽發者](#BKMK_PlanningForRootCAs)  
  - [PKI 用戶端憑證選擇](#BKMK_PlanningForClientCertificateSelection)  
  - [用於 PKI 憑證和以網際網路為基礎的用戶端管理轉換策略](#BKMK_PlanningForPKITransition)  

- [規劃受信任的根金鑰](#BKMK_PlanningForRTK)  

- [規劃簽署與加密](#BKMK_PlanningForSigningEncryption)  

- [規劃以角色為基礎的系統管理](#BKMK_PlanningForRBA)  

- [規劃 Azure Active Directory](#bkmk_planazuread)  

- [規劃 SMS 提供者驗證](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> 規劃憑證 (自我簽署與 PKI)  

Configuration Manager 使用自我簽署憑證及公開金鑰基礎結構 (PKI) 憑證的組合。  

請盡可能使用 PKI 憑證。 如需詳細資訊，請參閱 [PKI 憑證需求](../network/pki-certificate-requirements.md)。 當 Configuration Manager 在註冊行動裝置期間要求 PKI 憑證時，您必須使用 Active Directory 網域服務和企業憑證授權單位。 針對其他所有 PKI 憑證，請從 Configuration Manager 獨立部署和管理這些憑證。 

當用戶端電腦連線到以網際網路為基礎的站台系統時，需要 PKI 憑證。 使用雲端管理閘道和雲端發佈點的一些案例也需要 PKI 憑證。 如需詳細資訊，請參閱[管理網際網路上的用戶端](../../clients/manage/manage-clients-internet.md)。

使用 PKI 時，您也可利用 IPsec 協助保護站台內站台系統之間和站台之間的伺服器對伺服器通訊，以及電腦之間其他的資料傳輸。 IPsec 實作不受 Configuration Manager 影響。  

沒有 PKI 憑證可用時，Configuration Manager 會自動產生自我簽署憑證。 Configuration Manager 中的某些憑證一律會自我簽署。 在大部分情況下，Configuration Manager 會自動管理自我簽署憑證，您不需要採取額外動作。 站台伺服器簽署憑證即為一例。 此憑證一律會自我簽署。 這會確保用戶端從管理點下載的原則已從站台伺服器送出，且未遭竄改。  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a> 密碼編譯：新一代 (CNG) 憑證  

Configuration Manager 支援密碼編譯：新一代 (CNG) 憑證。 設定管理員用戶端可以搭配 CNG 金鑰儲存提供者 (KSP) 中的私密金鑰來使用 PKI 用戶端驗證憑證。 有 KSP 的支援，設定管理員用戶端可以支援硬體式私密金鑰，例如 PKI 用戶端驗證憑證的 TPM KSP。 如需詳細資訊，請參閱 [CNG 憑證概觀](../network/cng-certificates-overview.md)。


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a> 增強 HTTP  

建議所有 Configuration Manager 通訊路徑都使用 HTTPS 通訊，但因管理 PKI 憑證造成的額外負荷，對於某些客戶而言是項挑戰。 Azure Active Directory (Azure AD) 整合功能的引進，可減少一些憑證需求，但無法根除。 從 1806 版開始，您可以啟用站台使用 [增強 HTTP]  。 這項設定使用自我簽署憑證和 Azure AD 的組合來支援站台系統上的 HTTPS。 它不需要 PKI。 如需詳細資訊，請參閱[增強 HTTP](../hierarchy/enhanced-http.md)。  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a> CMG 和 CDP 的憑證

透過雲端管理閘道 (CMG) 和雲端發佈點 (CDP) 管理網際網路上的用戶端需要使用憑證。 憑證的數目和類型會視您的特定案例而有所不同。 如需詳細資訊，請參閱下列文章：
- [雲端管理閘道的憑證](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [雲端發佈點的憑證](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a> 規劃站台伺服器簽署憑證 (自我簽署)  

用戶端可從 Active Directory 網域服務及用戶端推入安裝，安全地取得一份網站伺服器簽署憑證複本。 如果用戶端無法利用這些機制的其中一種來取得一份憑證複本，請在安裝用戶端時予以安裝。 如果用戶端第一次與站台通訊是透過以網際網路為基礎的管理點，此程序尤其重要。 由於此站台連線到不受信任的網路，因此更容易遭受攻擊。 如果不採用這個額外步驟，用戶端便會自動從管理點下載一份站台伺服器簽署憑證複本。  

在下列情況中，用戶端無法安全地取得一份站台伺服器憑證複本：  

- 您未使用用戶端推入安裝用戶端，而且：  

  - 您尚未延伸 Configuration Manager 的 Active Directory 架構。  

  - 您尚未將用戶端的站台發佈至 Active Directory 網域服務。  

  - 用戶端來自不受信任的樹系或工作群組。  

- 您正在使用以網際網路為基礎的用戶端管理，而且當用戶端在網際網路時，您會安裝用戶端。  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>安裝用戶端和一份網站伺服器簽署憑證複本  

1.  找出主要站台伺服器上的站台伺服器簽署憑證。 此憑證是儲存在 Windows 的 **SMS** 憑證存放區中。 其主體名稱為**站台伺服器**，易記名稱為**站台伺服器簽署憑證**。  

2.  匯出不含私密金鑰的憑證，將檔案儲存在安全的地方，只從安全通道存取該檔案。  

3.  使用下列 client.msi 內容安裝用戶端：`SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> 規劃 PKI 憑證撤銷  

當您搭配 Configuration Manager 使用 PKI 憑證時，請規劃使用憑證撤銷清單 (CRL)。 裝置使用 CRL 來確認連線電腦上的憑證。 CRL 是憑證授權單位 (CA) 所建立並簽署的檔案。 它有一份由 CA 簽發但撤銷的憑證清單。 當憑證管理員撤銷憑證時，該憑證的指紋會新增至 CRL。 例如，如果已簽發的憑證已知或有遭到洩露的可能。

> [!IMPORTANT]  
> 由於 CA 簽發憑證時會將 CRL 的位置新增至憑證，因此請務必在部署 Configuration Manager 所使用的任何 PKI 憑證之前，先規劃 CRL。  

IIS 一律會檢查用戶端憑證的 CRL，您無法在 Configuration Manager 中變更這項設定。 Configuration Manager 用戶端預設一律會檢查 CRL 有無站台系統。 指定站台內容和 CCMSetup 內容來停用此設定。  

如果電腦使用憑證撤銷檢查，卻無法找出 CRL，電腦的反應就像憑證鏈中所有的憑證都已被撤銷一樣。 會有這樣的行為，是因為它們無法驗證憑證是否有在憑證撤銷清單內。 在這樣的情況下，需要憑證且包含 CRL 檢查的連線都會失敗。 當您在驗證是否能透過瀏覽 CRL 的 http 位置來存取 CRL 時，請務必注意 Configuration Manager 會以 LOCAL SYSTEM 的身分執行。 因此，在使用者內容下以網頁瀏覽器測試 CRL 的可存取性或許會成功，但因為受到內部 Web 篩選解決方案的影響，所以對同樣的 CRL URL 嘗試進行 http 連線時，電腦帳戶可能會遭到封鎖。 在這種情況下，可能有必要在所有 Web 篩選解決方案上將 CRL URL 加入允許清單。

在每一次使用憑證時檢查 CRL，如此可提供比使用已撤銷之憑證更多的安全性。 但同時也會造成用戶端連線延遲及額外的處理工作。 如果用戶端在網際網路或不受信任的網路上，您的組織可能需要這項額外的安全性檢查。  

在判定 Configuration Manager 用戶端是否須檢查 CRL 之前，請先向您的 PKI 系統管理員查詢。 之後，當下列兩項條件成立時，再考慮保留 Configuration Manager 中啟用的這個選項：  

- 您的 PKI 基礎結構支援 CRL，且會發佈在所有 Configuration Manager 用戶端都可找到它的地方。 這些用戶端可能包含網際網路上的裝置，以及不受信任樹系中的裝置。  

- 檢查每一個站台系統 (其設定為使用 PKI 憑證) 連線的 CRL 需求，遠大於下列需求：  
  - 更快速連線  
  - 用戶端的有效處理  
  - 找不到 CRL 時，用戶端無法連線到伺服器的風險  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> 規劃 PKI 受信任根憑證及憑證簽發者清單  

如果您的 IIS 站台系統使用 PKI 用戶端憑證，以透過 HTTP 供用戶端驗證之用，或是透過 HTTPS 供用戶端驗證及加密之用時，您可能必須匯入根 CA 憑證，並將它當成站台內容來使用。 以下是兩個案例︰  

- 您使用 Configuration Manager 部署作業系統，且管理點只接受 HTTPS 用戶端連線。  

- 您使用未鏈結至管理點所信任根憑證的 PKI 用戶端憑證。  

  > [!NOTE]  
  > 當您從簽發用於管理點之伺服器憑證的相同 CA 階層來簽發用戶端 PKI 憑證時，您不需要指定這個根 CA 憑證。 不過，如果您使用多重 CA 階層，但不確定其是否彼此信任，即可匯入用戶端 CA 階層所適用的根 CA。  

如果必須匯入 Configuration Manager 的根 CA 憑證，請將該憑證從簽發 CA 或從用戶端電腦匯出。 如果從簽發 CA 匯出也是根 CA 的憑證，請確保未匯出私密金鑰。 將匯出的憑證檔案儲存在安全位置，以防遭到竄改。 當您設定站台時，需要檔案的存取權。 如果是透過網路來存取檔案，請務必利用 IPsece 來防止通訊內容遭到竄改。  

如果匯入的根 CA 憑證已更新，您就必須匯入更新的憑證。  

這些匯入的根 CA 憑證及每一個管理點的根 CA 憑證，會建立一份 Configuration Manager 電腦以下列方式使用的憑證簽發者清單：  

- 當用戶端連線到管理點時，管理點會確認用戶端憑證鏈結至站台憑證簽發者清單中的受信任根憑證。 如果沒這麼做，就會拒絕憑證，PKI 連線就會失敗。  

- 當用戶端選取 PKI 憑證並擁有憑證簽發者清單時，即可選取鏈結至憑證簽發者清單中之受信任根憑證的憑證。 如果沒有符合者，用戶端就不會選取 PKI 憑證。 如需詳細資訊，請參閱[規劃 PKI 用戶端憑證選擇](#BKMK_PlanningForClientCertificateSelection)。  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> 規劃 PKI 用戶端憑證選擇  

如果您的 IIS 站台系統使用 PKI 用戶端憑證，以透過 HTTP 供用戶端驗證之用，或是透過 HTTPS 供用戶端驗證及加密之用時，請規劃 Windows 用戶端如何選取可供 Configuration Manager 使用的憑證。  

> [!NOTE]  
> 有些裝置不支援憑證選擇方法。 它們反倒會自動選取第一個滿足憑證需求的憑證。 例如，Mac 電腦上的用戶端及行動裝置不支援憑證選擇方法。  

在許多情況下，預設的設定和行為即已足夠。 Windows 電腦上的 Configuration Manager 用戶端，會依此順序使用下列準則篩選多種憑證：  

1.  憑證簽發者清單：憑證鏈結至管理點所信任的根 CA。  

2.  憑證在 [個人]  預設憑證存放區中。  

3.  憑證是有效的，未撤銷，也未過期。 有效性檢查會確認私密金鑰的可存取性。  

4.  憑證具有用戶端驗證功能，或是簽發給電腦名稱。  

5.  憑證具有最長的有效期。  

利用下列機制，將用戶端設定為使用憑證簽發者清單：  

- 將它與 Configuration Manager 站台資訊一起發佈至 Active Directory 網域服務。  

- 使用用戶端推入來安裝用戶端。  

- 用戶端在順利被指派到其站台後，會從管理點下載該清單。  

- 在用戶端安裝期間將它指定為 CCMCERTISSUERS 的 CCMSetup client.msi 內容。  

第一次安裝且尚未指派到站台的用戶端，不具備憑證簽發者清單，所以會略過此檢查。 如果用戶端的確擁有憑證簽發者清單，但沒有鏈結至憑證簽發者清單中受信任根憑證的 PKI 憑證時，憑證選擇會失敗。 用戶端不會繼續其他憑證選擇準則。  

在多數情況下，Configuration Manager 用戶端會正確地識別出唯一且適當的 PKI 憑證。 不過，若不符合此行為，就不需根據用戶端驗證功能來選取憑證，您可以設定其他兩種選擇方法：  

- 用戶端憑證主體名稱的部分相符字串。 此方法在比對時不區分大小寫。 如果主旨欄位正在使用電腦完整網域名稱 (FQDN)，而且是根據網域尾碼選擇憑證 (例如 **contoso.com**)，則適用此方法。 不過，您可使用此選擇方法來識別憑證主體名稱 (用以區分與用戶端憑證存放區其他憑證的不同) 中循序字元的任何字串。  

  > [!NOTE]
  > 您不可將主體別名 (SAN) 的部分相符字串當成站台設定來使用。 雖然您可使用 CCMSetup 為 SAN 指定部分相符字串，但在下列案例中，該相符字串將會被站台內容覆寫：  
  > 
  > - 用戶端會擷取發佈至 Active Directory 網域服務的站台資訊。  
  >   - 用戶端是使用用戶端推入安裝的。  
  > 
  >   只有在您手動安裝用戶端，且用戶端不從 Active Directory 網域服務擷取站台資訊時，才使用 SAN 中的部分相符字串。 例如，這些狀況僅適用於網際網路用戶端。  

- 用戶端憑證的主體名稱屬性值或主體別名 (SAN) 屬性值相符。 此方法在比對時區分大小寫。 如果您使用 X500 辨別名稱或符合 RFC 3280 的對等物件識別 (OID)，且您希望根據屬性值進行憑證選擇，則適用此方法。 您可以僅指定屬性與您要求的值來唯一識別或驗證憑證，和區別憑證存放區中的其他憑證。  

下表顯示針對用戶端憑證選擇準則 Configuration Manager 支援的屬性值。  

|OID 屬性|辨別名稱屬性|屬性定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|網域元件|  
|1.2.840.113549.1.9.1|E 或 E-mail|電子郵件地址|  
|2.5.4.3|CN|一般名稱|  
|2.5.4.4|SN|主體名稱|  
|2.5.4.5|SERIALNUMBER|序號|  
|2.5.4.6|C|國碼 (地區碼)|  
|2.5.4.7|L|位置|  
|2.5.4.8|S 或 ST|省份名稱|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|組織名稱|  
|2.5.4.11|OU|組織單位|  
|2.5.4.12|T 或 Title|標題|  
|2.5.4.42|G 或 GN 或 GivenName|指定的名稱|  
|2.5.4.43|I 或 Initials|縮寫|  
|2.5.29.17|(沒有值)|主體替代名稱|  

若套用選取準則後有一個以上的合適憑證，您可以覆寫預設設定以選取有效期間最長的憑證，或者改為指定不選取任何憑證。 在此案例中，用戶端無法和有 PKI 憑證的 IIS 站台系統進行通訊。 用戶端會將錯誤訊息傳送至指派的後援狀態點，向您警示憑證選取失敗，如此您就可以變更或縮小憑證選擇準則。 接著，用戶端行為就會根據失敗的連線是經由 HTTPS 或 HTTP 來進行。  

- 如果失敗的連線是經由 HTTPS：用戶端會嘗試透過 HTTP 進行連線，並使用用戶端自我簽署憑證。  

- 如果失敗的連線是經由 HTTP：用戶端會嘗試使用自我簽署用戶端憑證，透過 HTTP 進行另一個連線。  

若要協助識別唯一 PKI 用戶端憑證，除了在 [電腦]  存放區中的 [個人]  預設值外，您也可以指定自訂存放區。 不過，您必須從 Configuration Manager 單獨建立此存放區。 您必須能夠將憑證部署至此自訂存放區，並在有效期間到期前更新憑證。  

如需詳細資訊，請參閱[設定用戶端 PKI 憑證設定](configure-security.md#BKMK_ConfigureClientPKI)。  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> 規劃用於 PKI 憑證和以網際網路為基礎的用戶端管理轉換策略  

Configuration Manager 中的彈性設定選項可讓您逐漸轉換用戶端和網站，以使用 PKI 憑證來協助確保用戶端端點的安全。 PKI 憑證提供更好的安全性讓您管理網際網路用戶端。  

由於 Configuration Manager 中設定選項和選擇的數目，會使得轉換站台的方法不只一種，如此一來，所有用戶端就都會使用 HTTPS 連線。 不過，您可以遵循這些步驟作為指引：  

1. 安裝並設定 Configuration Manager 網站，如此網站系統就會接受透過 HTTPS 和 HTTP 的用戶端連線。  

2. 設定網站內容中的 用戶端電腦通訊  索引標籤，如此 站台系統設定  就會是 **HTTP 或 HTTPS**，然後選取 使用可用的 PKI 用戶端憑證 (用戶端驗證功能  。  如需詳細資訊，請參閱[設定用戶端 PKI 憑證設定](configure-security.md#BKMK_ConfigureClientPKI)。  

    > [!Note]
    > 從 1906 版開始，此索引標籤稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

3. 針對用戶端憑證試驗 PKI 首度發行。 如需部署範例，請參閱[部署 Windows 電腦的用戶端憑證](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)。  

4. 使用用戶端推入安裝方法安裝用戶端。 如需詳細資訊，請參閱[如何使用用戶端推入來安裝 Configuration Manager 用戶端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。  

5. 使用 Configuration Manager 主控台中的報告和資訊來監控用戶端部署和狀態。  

6. 檢視 [資產與相容性]  工作區 [裝置]  節點中的 [用戶端憑證]  欄位，來追蹤有多少用戶端使用用戶端 PKI 憑證  

    您也可以在電腦上部署 Configuration Manager HTTPS 整備評估工具(**cmHttpsReadiness.exe**)。 然後使用報告檢視有多少電腦可以搭配 Configuration Manager 使用用戶端 PKI 憑證。  

   > [!NOTE]
   >  當您安裝 Configuration Manager 用戶端時，它會安裝 `%windir%\CCM` 資料夾中的 **CMHttpsReadiness.exe** 工具。 當您執行此工具時，可以使用下列命令列選項：  
   > 
   > - `/Store:<name>`：此選項相當於 **CCMCERTSTORE** client.msi 內容  
   > - `/Issuers:<list>`：此選項相當於 **CCMCERTISSUERS** client.msi 內容    
   > - `/Criteria:<criteria>`：此選項相當於 **CCMCERTSEL** client.msi 內容    
   > - `/SelectFirstCert`：此選項相當於 **CCMFIRSTCERT** client.msi 內容    
   > 
   >   如需詳細資訊，請參閱[關於用戶端安裝內容](../../clients/deploy/about-client-installation-properties.md)。  

7. 您自信有足夠的用戶端能成功使用其用戶端 PKI 憑證透過 HTTP 進行驗證時，請遵循下列步驟作業：  

   1.  將 PKI Web 伺服器憑證部署至將執行網站上其他管理點的成員伺服器，並在 IIS 中設定該憑證。 如需詳細資訊，請參閱[為執行 IIS 的站台系統部署 Web 伺服器憑證](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  

   2.  將管理點角色安裝在此伺服器上，並在 [HTTPS]  的管理點內容中設定 [用戶端連線]  選項。  

8. 監控並確認具備 PKI 憑證的用戶端藉由使用 HTTPS 來使用新的管理點。 您可以使用 IIS 記錄或效能計數器進行確認。  

9. 重新設定其他網站系統角色以使用 HTTPS 用戶端連線。 如果您想管理網際網路上的用戶端，請確認站台系統具備網際網路 FQDN。 請設定個別管理點和發佈點，以接受來自網際網路的用戶端連線。  

    > [!IMPORTANT]  
    > 設定站台系統角色以接受來自網際網路的連線前，請檢閱以網際網路為基礎的用戶端管理規劃資訊和必要條件。 如需詳細資訊，請參閱[端點間的通訊](../hierarchy/communications-between-endpoints.md)。  

10. 延伸用戶端與執行 IIS 之站台系統的 PKI 憑證首度發行。 按需求設定 HTTPS 用戶端連線與網際網路連線的站台系統角色。  

11. 針對最高安全性：當您確認所有用戶端都使用用戶端 PKI 憑證進行驗證和加密時，請將網站內容變更至僅使用 HTTPS。  

    此規劃會先導入 PKI 憑證僅透過 HTTP 進行驗證，然後透過 HTTPS 驗證並加密。 遵循此規劃來漸漸導入這些憑證時，您可以降低用戶端變成非受控的風險。 您也會因 Configuration Manager 支援的最高安全性而受益。  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> 規劃受信任的根金鑰  

Configuration Manager 受信任的根金鑰提供 Configuration Manager 用戶端機制來確認站台系統隸屬其階層。 每個網站伺服器會產生網站交換金鑰，以與其他網站通訊。 來自階層頂層網站的網站交換金鑰稱為受信任的根金鑰。  

Configuration Manager 中受信任根金鑰的功能類似公開金鑰基礎結構的根憑證。 由受信任根金鑰的私密金鑰所簽署的任何物件，都會沿著階層受到信任。 用戶端會將站台的受信任根金鑰複本儲存在 **root\ccm\locationservices** WMI 命名空間中。 

例如，站台會對管理點發出憑證，並使用受信任根金鑰的私密金鑰進行簽署。 站台會與用戶端分享其受信任根金鑰的公開金鑰。 然後，用戶端可以區別出階層中的管理點與不在階層中的管理點。   

用戶端會使用兩種機制來自動擷取受信任根金鑰的公開複本。  

- 您可以延伸 Configuration Manager 的 Active Directory 架構，並將站台發佈至 Active Directory 網域服務。 然後，用戶端會從通用類別目錄伺服器擷取此站台資訊。 如需詳細資訊，請參閱[準備 Active Directory 以發佈站台](../network/extend-the-active-directory-schema.md)。  

- 您可以使用用戶端推入安裝方法來安裝用戶端。 如需詳細資訊，請參閱[用戶端推入安裝](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)。  

如果用戶端無法使用其中一種機制來擷取受信任的根金鑰，就會信任由第一個與其通訊之管理點所提供的受信任根金鑰。 在此案例中，可能會將用戶端錯誤導向到攻擊者的管理點 (該管理點會接收來自 Rogue 管理點的原則)。 此動作必須由狡猾的攻擊者發動。 只有用戶端從有效管理點擷取受信任根金鑰前的短時間內，才會發動這項攻擊。 若要降低攻擊者錯誤導向用戶端至 Rogue 管理點的這種風險，請使用受信任的根金鑰來預先佈建用戶端。  

使用以下程序預先佈建並確認 Configuration Manager 用戶端的受信任根金鑰：  

- [使用檔案以受信任的根金鑰預先佈建用戶端](#bkmk_trk-provision-file)  

- [在不使用檔案的狀況下，以受信任的根金鑰預先佈建用戶端](#bkmk_trk-provision-nofile)  

- [確認用戶端上的受信任根金鑰](#bkmk_trk-verify)  

- [移除或取代受信任的根金鑰](#bkmk_trk-reset)  

  > [!NOTE]  
  > 如果用戶端可以從 Active Directory 網域服務或用戶端推入取得受信任的根金鑰，則您不需要預先佈建。 
  > 
  > 當用戶端使用 HTTPS 與管理點通訊時，您不需要預先佈建受信任的根金鑰。 它們會透過 PKI 憑證建立信任關係。  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a> 使用檔案以受信任的根金鑰預先佈建用戶端  

1.  在站台伺服器上，以文字編輯器開啟下列檔案：`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  找出項目 **SMSPublicRootKey=** 。 從該行複製金鑰，然後在不進行任何變更的狀況下關閉檔案。  

3.  建立新的文字檔，並貼上您從 mobileclient.tcf 檔案中複製的金鑰資訊。  

4.  將檔案儲存至所有電腦都可以存取的位置，以確保檔案的安全，避免遭到竄改。  

5.  使用接受 client.msi 內容的任何安裝方法來安裝用戶端。 指定下列內容：`SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > 當您在用戶端安裝期間指定受信任的根金鑰時，請同時指定站台碼。 請使用下列 client.msi 內容：`SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a> 在不使用檔案的狀況下，以受信任的根金鑰預先佈建用戶端  

1.  在站台伺服器上，以文字編輯器開啟下列檔案：`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  找出項目 **SMSPublicRootKey=** 。 從該行複製金鑰，然後在不進行任何變更的狀況下關閉檔案。  

3.  使用接受 client.msi 內容的任何安裝方法來安裝用戶端。 指定下列 client.msi 內容：`SMSPublicRootKey=<key>`。其中 `<key>` 是您從 mobileclient.tcf 複製來的字串。  

    > [!IMPORTANT]  
    >  當您在用戶端安裝期間指定受信任的根金鑰時，請同時指定站台碼。 請使用下列 client.msi 內容：`SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a> 確認用戶端上的受信任根金鑰  

1. 以系統管理員的身分開啟 Windows PowerShell 主控台。  

2. 執行下列命令：  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

傳回的字串是受信任的根金鑰。 請確認它與站台伺服器上 mobileclient.tcf 檔案中的 **SMSPublicRootKey** 值相符。  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a> 移除或取代受信任的根金鑰  

您可以使用 client.msi 內容 **RESETKEYINFORMATION = TRUE**，從用戶端移除受信任的根金鑰。 

若要取代受信任的根金鑰，請重新安裝用戶端與新的受信任根金鑰。 例如，使用用戶端推入，或指定 client.msi 內容 **SMSPublicRootKey**。  

如需這些安裝內容的詳細資訊，請參閱[關於用戶端安裝參數和內容](../../clients/deploy/about-client-installation-properties.md)。



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> 規劃簽署與加密  
 
針對所有用戶端通訊使用 PKI 憑證時，您不需要為協助保護用戶端資料通訊而規劃簽署與加密。 如果您設定執行 IIS 的任何站台系統以允許 HTTP 用戶端連線，請決定如何協助站台保護用戶端通訊。  

若要協助保護用戶端傳送至管理點的資料，您可以要求用戶端簽署資料。 您也可以要求 SHA-256 演算法進行簽署。 這項設定比較安全，但除非所有用戶端都支援 SHA-256，否則無法要求此演算法。 許多作業系統原本就支援此演算法，但較舊的作業系統則需要更新或是 Hotfix。 

簽署有助保護資料不受竄改，而加密則可確保資料不會洩漏。 您可以為用戶端傳送至網站內管理點的清查資料與狀況訊息啟用 3DES 加密。 您不需要在用戶端上安裝任何更新以支援此選項。 用戶端和管理點需要使用額外的 CPU 來進行加密和解密。  

如需如何進行簽署和加密設定的詳細資訊，請參閱[設定簽署及加密](configure-security.md#BKMK_ConfigureSigningEncryption)。  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> 規劃以角色為基礎的系統管理  

如需詳細資訊，請參閱[以角色為基礎的系統管理基本概念](../../understand/fundamentals-of-role-based-administration.md)。  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a> 規劃 Azure Active Directory

Configuration Manager 與 Azure Active Directory (Azure AD) 整合，以允許站台和用戶端使用新式驗證。 將您的站台連線到 Azure AD 可支援下列 Configuration Manager 案例：

**用戶端**  

- [透過雲端管理閘道管理網際網路上的用戶端](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [管理已加入雲端網域的裝置](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [共同管理](../../../comanage/overview.md)  

- [部署使用者可用的應用程式](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [商務用 Microsoft Store Online 應用程式](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- 降低基礎結構需求。 例如，[使用管理點的軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)，而不是應用程式類別目錄  

- [管理 Office 365 應用程式](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**伺服器**  

- [電腦分析](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [社群中樞](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [雲端發佈點](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [使用者探索](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


如需將您的站台連線到 Azure AD 的詳細資訊，請參閱[設定 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)。


如需 Azure AD 的詳細資訊，請參閱 [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a> 規劃 SMS 提供者驗證
<!--1357013--> 

從 1810 版開始，您可以指定系統管理員存取 Configuration Manager 站台的最低驗證層級。 這項功能會強制系統管理員以必要層級登入 Windows。 它會套用至存取 SMS 提供者的所有元件。 例如，Configuration Manager 主控台、SDK 方法和 Windows PowerShell Cmdlet。 

此設定是全階層設定。 在您變更此設定之前，請確定所有 Configuration Manager 系統管理員都能以必要的驗證層級登入 Windows。 

可用的層級如下：

- **Windows 驗證**：需要使用 Active Directory 網域認證驗證。   

- **憑證驗證**：需要使用由信任的 PKI 憑證授權單位發出的有效憑證進行驗證。  

- **Windows Hello 企業版驗證**：需要以繫結至裝置強式雙因素驗證進行驗證並使用生物識別技術或 PIN。  

如需詳細資訊，請參閱[規劃 SMS 提供者](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)。 



## <a name="see-also"></a>請參閱
- [Configuration Manager 用戶端的安全性和隱私權](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [設定安全性](configure-security.md)  

- [端點間的通訊](../hierarchy/communications-between-endpoints.md)  

- [密碼編譯控制技術參考](cryptographic-controls-technical-reference.md)  

- [PKI 憑證需求](../network/pki-certificate-requirements.md)  

