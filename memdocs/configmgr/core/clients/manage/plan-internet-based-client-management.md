---
title: 以網際網路為基礎的用戶端管理
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中建立方案來管理以網際網路為基礎的用戶端。
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587228"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Configuration Manager 中以網際網路為基礎的用戶端管理規劃

適用於：  Configuration Manager (最新分支)

使用以網際網路為基礎的用戶端管理 (IBCM) 來在 Configuration Manager 用戶端連線到內部網路時進行管理。 使用 IBCM 的優點：

- 可完整控制提供服務的伺服器和角色
- 無任何雲端服務相依性
- 可以不需要虛擬私人網路 (VPN)
- 所有成本都與內部部署的服務建立關聯

因為在公用網路上管理用戶端電腦的安全性需求較高，所以 IBCM 要求使用 PKI 憑證。 這個設定可確保連線會由獨立的授權單位進行驗證。 當 IBCM 用戶端和站台伺服器傳送資料時會經過加密且處於安全狀態。  

## <a name="client-communications"></a>用戶端通訊

下列主要站台上站台系統角色支援來自不受信任位置的用戶端連線：

> [!NOTE]
> 雖然 IBCM 著重於以網際網路為基礎的案例，但相同行為也適用於位於不受信任 Active Directory 樹系中的用戶端。 次要站台不支援來自不受信任位置的用戶端連線。

- Configuration Manager 原則模組 (NDES) 的憑證登錄點

- 發佈點

- 雲端發佈點

- 註冊 Proxy 點

- 後援狀態點

- 管理點

- 軟體更新點

> [!NOTE]
> 1910 版已終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[移除應用程式類別目錄](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)。 針對仍支援的 Configuration Manager 1906 版及更早版本，應用程式類別目錄網站點可接受來自以網際網路為基礎用戶端的連線。

### <a name="about-internet-facing-site-systems"></a>關於網際網路對向的站台系統

用戶端樹系與站台系統伺服器之間不需要有信任。 不過，當包含網際網路對向站台系統的樹系信任包含使用者帳戶的樹系時，此設定仍支援針對網際網路上的裝置使用以使用者為基礎的原則 (在啟用 [用戶端原則]  用戶端設定 [從網際網路用戶端啟用使用者原則要求]  的情況下)。

例如，下列設定會說明 IBCM 何時會針對網際網路上的裝置支援使用者原則：

- 以網際網路為基礎的管理點位於周邊網路中。 該網路也具備唯讀網域控制站來驗證使用者。 周邊與內部網路之間的防火牆允許 Active Directory 封包。

- 使用者帳戶位於以內部網路為基礎的樹系中。 以網際網路為基礎管理點位於以周邊為基礎的樹系中。 周邊樹系信任內部樹系。 周邊與內部網路之間的防火牆允許驗證封包。

- 使用者帳戶和以網際網路為基礎管理點都位於以內部網路為基礎的樹系中。 您使用 Web Proxy 伺服器將管理點發佈到網際網路。

### <a name="use-a-web-proxy-server"></a>使用 Web Proxy 伺服器

您可在使用 Web Proxy 伺服器，將以網際網路為基礎的站台系統發佈到網際網路時，將站台系統放在內部網路中。 請針對來自網際網路的用戶端連線，或來自網際網路和內部網路的用戶端連線設定這些站台系統。 當使用 Web Proxy 伺服器時，您可設定伺服器，讓安全通訊端層 (SSL) 橋接至 SSL 或 SSL 隧道。

#### <a name="ssl-bridging-to-ssl"></a>SSL 橋接至 SSL

SSL 橋接至 SSL 是建議且更安全的設定，因為這項設定會搭配驗證使用 SSL 終止。 其會搭配電腦驗證來驗證用戶端電腦。 您向 Configuration Manager 註冊的行動裝置不支援 SSL 橋接。

搭配位於 Proxy 的 SSL 終止，其會在將封包轉寄至內部網路前先檢查封包。 Proxy 會驗證來自用戶端的連線，將其終止，然後開啟一個全新已驗證的連線來連線到以網際網路為基礎站台系統。 當 Configuration Manager 用戶端使用 Proxy 時，用戶端會安全地在封包承載中包含其身分識別 (GUID)。 管理點不會將 Proxy 視為用戶端。 Configuration Manager 不支援將 HTTP 橋接至 HTTPS，或從 HTTPS 到 HTTP。

> [!NOTE]
> Configuration Manager 不支援設定協力廠商 SSL 橋接設定。 例如 Citrix Netscaler 或 F5 BIG-IP。 請與您的裝置廠商合作，以設定它來與 Configuration Manager 搭配使用。

#### <a name="tunneling"></a>隧道

若 Proxy 網頁伺服器不支援 SSL 橋接的需求，Configuration Manager 也支援 SSL 隧道。 您也可使用 SSL 隧道來支援向 Configuration Manager 註冊的行動裝置。 這是較不安全的選項，因為 Proxy 會在沒有 SSL 終止的情況下，將 SSL 封包從網際網路轉寄到站台系統。 Proxy 不會檢查封包是否包含惡意內容。 使用 SSL 通道時，Proxy 網頁伺服器不需要憑證。

## <a name="plan-for-internet-based-clients"></a>規劃以網際網路為基礎的用戶端

決定是要設定以網際網路為基礎的用戶端以在內部網路和網際網路上進行管理，還是僅限在網際網路進行用戶端管理。 您只能在用戶端安裝期間設定此管理選項。 若要在稍後進行變更，請重新安裝用戶端。

> [!NOTE]
> 如果設定管理點以支援以網際網路為基礎的用戶端，則連線到此管理點的用戶端將會在下一次重新整理可用管理點其清單時成為具有網際網路連線功能。
>
> 您不需要將僅限網際網路用戶端管理的設定限制在網際網路上。 您也可在內部網路上使用該項目。

設定為僅在網際網路上接受管理的用戶端，則只會和設定從網際網路進行用戶端連線的站台系統進行通訊。 請在下列案例中使用此設定：

- 您知道永遠不會連線到內部網路的電腦。 例如：遠端位置的銷售點電腦。
- 將用戶端通訊限制在僅限 HTTPS。 例如：支援防火牆和受限制的安全性原則。
- 當在周邊網路中安裝以網際網路為基礎的站台系統，且希望將這些伺服器作為 Configuration Manager 用戶端管理時。

> [!NOTE]
> 若希望管理網際網路上的工作群組用戶端，則請將這些用戶端安裝為僅限網際網路。
>
> 當設定行動裝置使用以網際網路為基礎的管理點時，會自動設為僅限網際網路。

您可設定其他用戶端接受網際網路和內部網路用戶端管理。 當用戶端偵測到網路變更時，便會自動在 IBCM 和內部網路用戶端管理之間切換。 如果這些用戶端找到並連線到支援內部網路用戶端連線的管理點，便會將這些用戶端作為內部網路用戶端管理。 內部網路用戶端擁有完整的 Configuration Manager 功能。 如果用戶端找不到或無法連線到支援內部網路用戶端連線的管理點，便會嘗試連線到以網際網路為基礎的管理點。 如果此動作成功，這些用戶端接著便會由以網際網路為基礎的站台系統，在其指派的站台中進行管理。

自動切換的優點是用戶端可在連線到內部網路時使用所有功能，並在連線到網際網路時取得基本的管理。 在網際網路上開始的內容下載可以在內部網路上順利繼續，反之亦然。

## <a name="prerequisites"></a>先決條件

Configuration Manager 中的 IBCM 具有下列相依性：

- 用戶端需要網際網路連線。 Configuration Manager 使用裝置現有的網際網路連線。 行動裝置必須擁有直接網際網路連線。 完整的用戶端電腦可具備直接網際網路連線，或使用 Proxy 網頁伺服器來連線。

- 支援 IBCM 的站台系統需要網際網路連線，且必須位於 Active Directory 網域中。 以網際網路為基礎的站台系統不需要與站台伺服器 Active Directory 樹系建立信任關係。 但是，當以網際網路為基礎的管理點可使用 Windows 驗證來驗證使用者時，便支援使用者原則。 若 Windows 驗證失敗，則只支援裝置原則。

    > [!NOTE]
    > 若要支援使用者原則，則另請在**用戶端原則**群組中啟用下列用戶端設定：
    >
    > - **啟用用戶端的使用者原則輪詢**
    > - **從網際網路用戶端啟用使用者原則要求**  

- 用來部署和管理以網際網路為基礎用戶端和站台系統伺服器必要憑證的公開金鑰基礎結構 (PKI)。 如需詳細資訊，請參閱 [PKI 憑證需求](../../plan-design/network/pki-certificate-requirements.md)。

- 針對支援 IBCM 站台系統的網際網路完整網域名稱 (FQDN) 註冊公用 DNS 主機項目。

### <a name="client-communication-requirements"></a>用戶端通訊需求

中介防火牆或 Proxy 伺服器必須允許以網際網路為基礎站台系統的用戶端通訊：

- 支援 HTTP 1.1  

- 允許多部分 MIME 附件的 HTTP 內容類型 (多部分/混合和應用程式/octet-stream)。  

#### <a name="verbs"></a>動詞

針對以網際網路為基礎站台系統的伺服器角色，允許下列動詞：

| [角色] | 動詞 |
|------|-------|
| 管理點 | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| 發佈點 | - HEAD<br>- GET<br>- PROPFIND |
| 後援狀態點 | POST |
| 應用程式類別目錄網站點 | -POST<br>-GET |

#### <a name="http-headers"></a>HTTP 標頭

針對以網際網路為基礎站台系統的伺服器角色，允許下列 HTTP 標頭：

| [角色] | HTTP 標頭 |
|------|--------------|
| 管理點 | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| 發佈點 | Range: |

若要了解使用軟體更新點從網際網路進行用戶端連線時的類似通訊需求，請參閱 Windows Server Update Services (WSUS) 的說明文件。

## <a name="unsupported-features"></a>不支援的功能

並非所有用戶端管理功能都適合網際網路。 Configuration Manager 不支援網際網路上用戶端的一些功能。 這些未受支援的功能通常依賴 Active Directory Doman Services 或不適合公用網路。

當使用 IBCM 於網際網路上管理用戶端時，不支援下列功能：

- 透過網際網路的用戶端部署，例如用戶端推入和以軟體更新為基礎的用戶端部署。 使用手動用戶端安裝。

- 自動站台指派

- 網路喚醒

- OS 部署。 但是，您可部署不會在 OS 上部署的工作順序。

- 遠端控制

- 使用者軟體部署。 此功能依賴應用程式類別目錄，但此項目已淘汰。

- 用戶端漫遊。 漫遊會讓用戶端總是找出最接近的發佈點來下載內容。 無論頻寬或實體位置為何，用戶端都會以不確定方式選取其中一個以網際網路為基礎的站台系統。

當設定軟體更新點接受來自網際網路的連線時，以網際網路為基礎的用戶端一律會掃描此軟體更新點，以判斷需要的軟體更新。 當這些用戶端位於網際網路上時，用戶端會先嘗試從 Microsoft Update 下載軟體更新，而非從以網際網路為基礎的發佈點下載。 若此行為失敗，用戶端接著會嘗試從以網際網路為基礎的發佈點下載所需軟體更新。

> [!TIP]
> Configuration Manager 用戶端會自動判斷它是位於內部網路還是網際網路。 如果用戶端可連絡網域控制站或內部部署管理點，則會將其連線類型設定為「目前為內部網路」  。 否則，其會切換至「目前為網際網路」  ，並和指派給站台的站台系統通訊。
