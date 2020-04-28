---
title: CMG 憑證
titleSuffix: Configuration Manager
description: 了解搭配雲端管理閘道使用的不同數位憑證。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 33e4ecbac965206ec4043f5adf91d2dbfb9602d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694936"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>雲端管理閘道的憑證

適用於：  Configuration Manager (最新分支)

根據您透過雲端管理閘道 (CMG) 管理網際網路上用戶端所使用的案例，您可能需要下列一或多個數位憑證：  

- [CMG 伺服器驗證憑證](#bkmk_serverauth)  
  - [用戶端的 CMG 受信任根憑證](#bkmk_cmgroot)  
  - [公用提供者所發行的伺服器驗證憑證](#bkmk_serverauthpublic)  
  - [企業 PKI 所發行的伺服器驗證憑證](#bkmk_serverauthpki)  

- [用戶端驗證憑證](#bkmk_clientauth)  
  - [CMG 的用戶端受信任根憑證](#bkmk_clientroot)  

- [啟用 HTTPS 的管理點](#bkmk_mphttps)  

- [Azure 管理憑證](#bkmk_azuremgmt)  

如需不同案例的詳細資訊，請參閱[針對雲端管理閘道進行規劃](plan-cloud-management-gateway.md)。

## <a name="general-information"></a>一般資訊

<!--SCCMDocs issue #779-->
雲端管理閘道的憑證支援下列設定：  

- 2048 位元或 4096 位元金鑰長度

- 適用於憑證私密金鑰的金鑰儲存提供者。 如需詳細資訊，請參閱 [CNG 憑證概觀](../../../plan-design/network/cng-certificates-overview.md)。  

- 當您使用下列原則設定 Windows 時：**系統密碼編譯:使用 FIPS 相容演算法於加密，雜湊，以及簽章**  

- **TLS 1.2**。 如需詳細資訊，請參閱[如何啟用 TLS 1.2](../../../plan-design/security/enable-tls-1-2.md)。  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a> CMG 伺服器驗證憑證

*所有案例都需要此憑證。*

在 Configuration Manager 主控台中建立 CMG 時，您需要提供此憑證。

CMG 會建立以網際網路為基礎的用戶端連線至的 HTTPS 服務。 伺服器需要伺服器驗證憑證來建立安全通道。 從公用提供者取得此用途的憑證，或者從您的公開金鑰基礎結構 (PKI) 發行它。 如需詳細資訊，請參閱[用戶端的 CMG 受信任的根憑證](#bkmk_cmgroot)。

> [!NOTE]
> CMG 伺服器驗證憑證支援萬用字元。 某些憑證授權單位會發出使用使用萬用字元作為主機名稱的憑證。 例如 `*.contoso.com`。 某些組織會使用萬用字元憑證來簡化其 PKI，並降低維護成本。<!--491233-->  
>
> 如需如何搭配 CMG 使用萬用字元憑證的詳細資訊，請參閱[設定 CMG](setup-cloud-management-gateway.md#set-up-a-cmg)。<!--SCCMDocs issue #565-->  

此憑證需要全球唯一名稱來識別 Azure 中的服務。 要求憑證之前，請確認您想要的 Azure 網域名稱是唯一的。 例如，*GraniteFalls.CloudApp.Net*。

1. 登入 [Azure 入口網站](https://portal.azure.com)。
1. 選取 [所有資源]  ，然後選取 [新增]  。
1. 搜尋**雲端服務**。 選取 [建立]  。
1. 在 [DNS 名稱]  欄位中輸入您想要的前置詞，例如 *GraniteFalls*。 介面將會反映網域名稱可用或已由另一個服務使用。

    > [!Important]  
    > 請勿在入口網站中建立服務，只要使用此程序檢查名稱可用性。

如果您也將針對內容啟用 CMG，請確認 CMG 服務名稱也是唯一的 Azure 儲存體帳戶名稱。 如果 CMG 雲端服務名稱是唯一的，但儲存體帳戶名稱不是，Configuration Manager 就無法在 Azure 中佈建該服務。 在 Azure 入口網站中，使用下列變更重複執行上述程序：

- 搜尋**儲存體帳戶**
- 在 [儲存體帳戶名稱]  欄位中測試您的名稱

DNS 名稱前置詞 (例如 *GraniteFalls*) 的長度必須是 3 到 24 個字元，而且只能使用英數位元。 請勿使用特殊字元，例如破折號 (`-`)。<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a> 用戶端的 CMG 受信任根憑證

用戶端必須信任 CMG 伺服器驗證憑證。 有兩種方式可完成此信任：

- 使用來自公用且全球受信任的憑證提供者的憑證。 例如 (但不限於)，DigiCert、Thawte 或 VeriSign。 Windows 用戶端包含來自這些提供者的受信任的根憑證授權單位 (CA)。 使用這些提供者之一發出的伺服器驗證憑證，您的用戶端會自動信任它。  

- 使用來自您的公開金鑰基礎結構 (PKI) 的企業 CA 所發出的憑證。 大部分企業 PKI 實作會將信任的根 CA 新增到 Windows 用戶端。 例如，使用搭配群組原則的 Active Directory 憑證服務。 如果您從用戶端未自動信任的 CA 發出 CMG 伺服器驗證憑證，請將 CA 受信任的根憑證新增至以網際網路為基礎的用戶端。  

  - 您也可以使用 Configuration Manager 憑證設定檔，在用戶端上佈建憑證。 如需詳細資訊，請參閱[憑證設定檔簡介](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)。

  - 如果您打算[從 Intune 安裝 Configuration Manager 用戶端](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)，也可以使用 Intune 憑證設定檔在用戶端上佈建憑證。 如需詳細資訊，請參閱[設定憑證設定檔](https://docs.microsoft.com/intune/certificates-configure)。

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a> 公用提供者所發行的伺服器驗證憑證

第三方憑證提供者無法建立 CloudApp.net 的憑證，因為該網域為 Microsoft 所擁有。 您只能取得針對您所擁有網域發出的憑證。 從第三方提供者取得憑證的主要原因是您的用戶端已信任該提供者的根憑證。

使用下列程序建立 DNS 別名：

1. 在貴組織的公用 DNS 中建立正式名稱記錄 (CNAME)。 此記錄會為 CMG 建立一個易記名稱的別名 (您在公開憑證中使用)。

    例如，Contoso 會將其 CMG 命名為 **GraniteFalls**。 在 Azure 中，此名稱會成為 **GraniteFalls.CloudApp.Net**。 在 Contoso 的公用 DNS contoso.com 命名空間中，DNS 系統管理員會針對真實的主機名稱 **GraniteFalls.CloudApp.net**，為 **GraniteFalls.Contoso.com** 建立新的 CNAME 記錄。  

2. 使用 CNAME 別名的一般名稱 (CN) 向公用提供者要求伺服器驗證憑證。
例如，Contoso 使用 **GraniteFalls.Contoso.com** 做為憑證 CN。  

3. 使用此憑證在 Configuration Manager 主控台中建立 CMG。 在 [建立雲端管理閘道精靈] 的 [設定]  頁面上：  

    - 當您為此雲端服務新增伺服器憑證時 (從**憑證檔案**)，精靈會從憑證 CN 擷取主機名稱來作為服務名稱。  

    - 然後，它會將該主機名稱附加至 **cloudapp.net**，或者適用於 Azure 美國政府雲端的 **usgovcloudapp.net**，以作為服務 FQDN 在 Azure 中建立服務。  

    - 例如，當 Contoso 建立 CMG 時，Configuration Manager 會從憑證 CN 擷取主機名稱 **GraniteFalls**。 Azure 會將實際服務建立為 **GraniteFalls.CloudApp.net**。  

當您在 Configuration Manager 中建立 CMG 執行個體時，雖然憑證包含 GraniteFalls.Contoso.com，但 Configuration Manager 只會擷取主機名稱，例如：GraniteFalls。 建立雲端服務時，Azure 會要求將此主機名稱附加至 CloudApp.net。 您網域 (Contoso.com) 中 DNS 命名空間的 CNAME 別名會同時對應至這兩個 FQDN。 Configuration Manager 提供用戶端存取此 CMG 的原則，並透過 DNS 對應結合在一起，以安全地存取 Azure 中的服務。<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a> 企業 PKI 所發行的伺服器驗證憑證

與雲端發佈點相同，針對 CMG 建立自訂 SSL 憑證。 遵循[為雲端架構的發佈點部署服務憑證](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)中的指示，但針對下列作業採用不同的做法：

- 當要求自訂 Web 伺服器憑證時，請針對憑證的一般名稱提供 FQDN。 此名稱可以是一個您擁有的公用網域名稱，或是您也可以使用 cloudapp.net 網域。 如果使用您自己的公用網域，請參考上述程序，在您組織的公用 DNS 中建立一個 DNS 別名。  

- 將 cloudapp.net 公用網域用於 CMG 網頁伺服器憑證時：  

  - 在 Azure 公用雲端上，使用以 **cloudapp.net** 結尾的名稱  

  - 針對 Azure 美國政府雲端，使用以 **usgovcloudapp.net** 結尾的名稱  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a> 用戶端驗證憑證

*執行 Windows 8.1 的網際網路型用戶端與未加入 Azure Active Directory (Azure AD) 的 Windows 10 裝置需要此憑證。CMG 連接點上也需要此憑證。已加入 Azure AD 的 Windows 10 用戶端則不需要。*

用戶端會使用此憑證來向 CMG 進行驗證。 混合式部署或已加入雲端網域的 Windows 10 裝置不需要此憑證，因為它們使用 Azure AD 進行驗證。

在 Configuration Manager 環境之外佈建此憑證。 例如，使用 Active Directory 憑證服務和群組原則來發出用戶端驗證憑證。 如需詳細資訊，請參閱[部署 Windows 電腦的用戶端憑證](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)。

若要安全地轉送用戶端要求，CMG 連接點需要用戶端驗證憑證，其會對應至 HTTPS 管理點上的伺服器驗證憑證。 如果用戶端使用 Azure AD 驗證，或您設定增強式 HTTP 的管理點，則不需要此憑證。 如需詳細資訊，請參閱[啟用 HTTPS 的管理點](#bkmk_mphttps)。

> [!NOTE]
> Microsoft 建議將裝置加入至 Azure AD。 以網際網路為基礎的裝置可以使用 Azure AD 向 Configuration Manager 進行驗證。 無論該裝置是在網際網路上，或與內部網路連線，Azure AD 都會同時啟用裝置與使用者案例。 如需詳細資訊，請參閱[使用 Azure AD 身分識別安裝和註冊用戶端](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。
>
> 從 2002 版開始，<!--5686290--> Configuration Manager 已可支援不常連線至內部網路、無法加入 Azure Active Directory (Azure AD)，且沒有方法可安裝 PKI 發行憑證等的裝置。 如需詳細資訊，請參閱 [CMG 的權杖型驗證](../../deploy/deploy-clients-cmg-token.md)。

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a> CMG 的用戶端受信任根憑證

*使用用戶端驗證憑證時，需要此憑證。當所有用戶端都使用 Azure AD 進行驗證時，不需要此憑證。*

在 Configuration Manager 主控台中建立 CMG 時，您需要提供此憑證。

CMG 必須信任用戶端驗證憑證。 若要完成這個信任，請提供受信任的根憑證鏈結。 請務必在信任鏈結中新增所有憑證。 例如，如果用戶端驗證憑證是由中繼 CA 所發行的，請同時新增中繼憑證和根 CA 憑證。

> [!Note]  
> 當建立 CMG 時，已不再需要於 [設定] 頁面上提供受信任的根憑證。 使用 Azure Active Directory (Azure AD) 進行用戶端驗證時，不需要此憑證，但以前在精靈中需要此憑證。 如果您要使用 PKI 用戶端驗證憑證，則仍然必須將受信任的根憑證新增至 CMG。<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> 在 1902 版和更早版本中，您只能指定兩個信任的根 CA，以及四個中繼 (從屬) CA。

#### <a name="export-the-client-certificates-trusted-root"></a>匯出用戶端憑證的受信任的根目錄

將用戶端驗證憑證發出到電腦後，請在該電腦上使用此程序匯出受信任的根目錄。

1. 開啟 [開始] 功能表。 輸入「執行」以開啟 [執行] 視窗。 開啟 `mmc`。  

2. 從 [檔案] 功能表中，選擇 [新增/移除嵌入式管理單元...]  。  

3. 在 [新增或移除嵌入式管理單元] 對話方塊中，選取 [憑證]  ，然後選取 [新增]  。  

    1. 在 [憑證嵌入式管理單元] 對話方塊中，選取 [電腦帳戶]  ，然後選取 [下一步]  。  

    1. 在 [選取電腦] 對話方塊中，選取 [本機電腦]  ，然後選取 [完成]  。  

    1. 在 [新增或移除嵌入式管理單元] 對話方塊中，選取 [確定]  。  

4. 依序展開 [憑證]  和 [個人]  ，然後選取 [憑證]  。  

5. 選取使用目的為**用戶端驗證**的憑證。  

    1. 從 [動作] 功能表中，選取 [開啟]  。  

    1. 移至 [憑證路徑]  索引標籤。  

    1. 選取鏈結中下一個憑證，然後選取 [檢視憑證]  。  

6. 在這個新的 [憑證] 對話方塊上，移至 [詳細資料]  索引標籤。選取 [複製到檔案...]  。  

7. 使用預設憑證格式 **DER 編碼二進位 X.509 (.CER)** 完成 [憑證匯出精靈]。 記下您所匯出之憑證的名稱和位置。  

8. 匯出原始用戶端驗證憑證之憑證路徑中的所有憑證。 請記下哪些匯出的憑證為中繼 CA，以及哪些是受信任的根 CA。  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a> 啟用 HTTPS 的管理點

在 Configuration Manager 環境之外佈建此憑證。 例如，使用 Active Directory 憑證服務和群組原則來發出 Web 伺服器憑證。 如需詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)和[為執行 IIS 的站台系統部署 Web 伺服器憑證](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。

在使用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  站台選項時，HTTP 可作為管理點。 如需詳細資訊，請參閱[Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md) (增強 HTTP)。

> [!Tip]  
> 如果您未使用增強式 HTTP，而且您的環境具有多個管理點，您不需要針對 CMG 全部啟用 HTTPS。 將啟用 CMG 的管理點設定為**僅限網際網路**。 之後，您的內部部署用戶端就不會嘗試使用它們。<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>管理點的增強型 HTTP 憑證

當您啟用增強型 HTTP 時，站台伺服器會產生名為 **SMS 角色 SSL 憑證**的自我簽署憑證，發行自根 SMS 發行憑證。 管理點會將此憑證新增到繫結至連接埠 443 的 IIS 預設網站。

### <a name="management-point-client-connection-mode-summary"></a>管理點用戶端連線模式摘要

這些表格摘要說明根據用戶端和站台版本的類型，管理點是否需要 HTTP 或 HTTPS。

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>以網際網路為基礎的用戶端與雲端管理閘道通訊

使用下列用戶端連線模式設定內部部署管理點，以允許來自 CMG 的連線：

| 用戶端類型   | 管理點 |
|------------------|------------------|
| 工作群組        | E HTTP<sup>[附註 1](#bkmk_note1)</sup>、HTTPS |
| 加入 AD 網域 | E HTTP<sup>[附註 1](#bkmk_note1)</sup>、HTTPS |
| 加入 Azure AD  | E-HTTP、HTTPS |
| 混合式加入    | E-HTTP、HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **附註 1**：此設定要求用戶端必須有[用戶端驗證憑證](#bkmk_clientauth)，而且僅支援以裝置為主的案例。  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>內部部署用戶端與內部部署管理點通訊

使用下列用戶端連線模式設定內部部署管理點：

| 用戶端類型   | 管理點 |
|------------------|------------------|
| 工作群組        | HTTP、HTTPS |
| 加入 AD 網域 | HTTP、HTTPS |
| 加入 Azure AD  | HTTPS       |
| 混合式加入    | HTTP、HTTPS |

> [!NOTE]  
> 加入 AD 網域的用戶端同時支援使用 HTTP 或 HTTPS 管理點來通訊的以裝置及使用者為中心案例。  
>
> 加入 Azure AD 和混合式加入的用戶端可針對以裝置為主的案例透過 HTTP 來通訊，但需要使用 E-HTTP 或 HTTPS 才能進行以使用者為主的案例。 否則他們的行為會與工作群組用戶端相同。  

#### <a name="legend-of-terms"></a>字詞說明

- *工作群組*：裝置未加入網域或 Azure AD，但有[用戶端驗證憑證](#bkmk_clientauth)  
- *加入 AD 網域*：您將裝置加入了內部部署 Active Directory 網域  
- *加入 Azure AD*：也稱為「加入雲端網域」，您將裝置加入了 Azure Active Directory 租用戶  
- *混合式加入*：您將裝置同時加入了 Active Directory 網域與 Azure AD 租用戶  
- *HTTP*：在管理點屬性上，您將用戶端連線設定為 **HTTP**  
- *HTTPS*：在管理點屬性上，您將用戶端連線設定為 **HTTPS**  
- *E-HTTP*：在站台屬性的 [用戶端電腦通訊]  索引標籤上，您要將站台系統設定設為 [HTTPS 或 HTTP]  ，並啟用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  選項。 您會設定 HTTP 的管理點，HTTP 管理點已就緒，可供 HTTP 與 HTTPS 通訊使用 (權杖驗證案例)。  
    > [!Note]
    > 從 1906 版開始，此索引標籤稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a> Azure 管理憑證

*傳統服務部署需要此憑證。Azure Resource Manager 部署則不需要。*

> [!Important]  
> 從 1810 版開始，Configuration Manager 已淘汰 Azure 的傳統服務部署。 針對雲端管理閘道，會開始使用 Azure Resource Manager 部署。 如需詳細資訊，請參閱[規劃 CMG](plan-cloud-management-gateway.md#azure-resource-manager)。
>
> 從 Configuration Manager 1902 版開始，對於雲端管理閘道的新執行個體，Azure Resource Manager 是唯一的部署機制。 Configuration Manager 1902 版或更新版本中不需要此憑證。<!-- 3605704 -->

您會在 Azure 入口網站中提供此憑證，以及在於 Configuration Manager 主控台中建立 CMG 時提供。

若要在 Azure 中建立 CMG，Configuration Manager 服務連接點必須先向您的 Azure 訂用帳戶驗證。 當使用傳統服務部署時，它會使用 Azure 管理憑證進行此驗證。 Azure 系統管理員會將此憑證上傳至您的訂用帳戶。 當您在 Configuration Manager 主控台中建立 CMG 時，請提供此憑證。

如需如何上傳管理憑證的詳細資訊和指示，請參閱 Azure 文件中的下列文章：

- [雲端服務和管理憑證](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [上傳 Azure 服務管理憑證](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> 請務必複製與管理憑證相關聯的訂用帳戶 ID。 您將使用此憑證在 Configuration Manager 主控台中建立 CMG。

## <a name="next-steps"></a>後續步驟

- [設定雲端管理閘道](setup-cloud-management-gateway.md)  

- [雲端管理閘道的相關常見問題集](cloud-management-gateway-faq.md)  

- [雲端管理閘道器的安全性和隱私權](security-and-privacy-for-cloud-management-gateway.md)  
