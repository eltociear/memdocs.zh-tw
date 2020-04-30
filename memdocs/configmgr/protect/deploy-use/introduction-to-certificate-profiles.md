---
title: 憑證設定檔簡介
titleSuffix: Configuration Manager
description: 了解如何搭配使用 Configuration Manager 中的憑證設定檔與 Active Directory 憑證服務。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 35269e7c727031a9cd66072985f3d9ec362978cf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706316"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>介紹 Configuration Manager 中的憑證設定檔

適用於：  Configuration Manager (最新分支)

憑證設定檔適用於 Active Directory 憑證服務和網路裝置註冊服務 (NDES) 角色。 建立和部署受控裝置的驗證憑證，讓使用者可以輕鬆地存取組織資源。 例如，您可以建立和部署憑證設定檔，以提供必要的憑證讓使用者進行 VPN 連線和無線連線。

憑證設定檔可以自動設定使用者裝置以存取組織的資源 (例如 Wi-Fi 網路和 VPN 伺服器)。 使用者可以存取這些資源，而不需要手動安裝憑證或使用頻外程序。 憑證設定檔有助於保護資源，因為您可以使用公開金鑰基礎結構 (PKI) 支援的更多安全設定。 例如，因為您已經在受控裝置上部署必要憑證，所以可以要求所有 Wi-Fi 及 VPN 連線進行伺服器驗證。

憑證設定檔提供下列管理功能：  

- 針對執行不同 OS 類型和版本的裝置，從憑證授權單位 (CA) 註冊和更新憑證。 然後，這些憑證就可以用於 Wi-Fi 和 VPN 連線。  

- 部署受信任的根 CA 憑證或中繼 CA 憑證。 上述憑證會在需要伺服器驗證時，在裝置上針對 VPN 和 Wi-Fi 連線設定信任鏈結。  

- 監視和報告已安裝的憑證。  

**範例 1**：所有員工都必須連線到位於多個辦公室位置的 Wi-Fi 熱點。 若要啟用輕鬆的使用者連線，請先部署連線至 Wi-Fi 所需的憑證。 然後部署參考憑證的 Wi-Fi 設定檔。  

**範例 2**：您已備妥 PKI。 您想要改用更具彈性且安全的憑證部署方法。 使用者必須從其個人裝置存取組織資源而不會危及安全性。 使用特定裝置平台所支援的設定及通訊協定來設定憑證設定檔。 裝置之後可以自動向網際網路對向註冊伺服器要求這些憑證。 接著，將 VPN 設定檔設定為使用這些憑證，以讓裝置可以存取組織資源。  

## <a name="types"></a>類型

有三種類型的憑證設定檔：  

- **受信任的 CA 憑證**：部署可信任的根 CA 或中繼 CA 憑證。 當裝置必須對伺服器進行驗證時，這些憑證便會形成信任鏈結。  

- **簡單憑證註冊通訊協定 (SCEP)** ：透過使用 SCEP 通訊協定要求裝置或使用者的憑證。 此類型需要執行 Windows Server 2012 R2 或更新版本的伺服器擁有網路裝置註冊服務 (NDES) 角色。

    若要建立**簡單憑證註冊通訊協定 (SCEP)** 憑證設定檔，您必須先建立**信任的 CA 憑證**設定檔。

- **個人資訊交換 (.pfx)** ：要求裝置或使用者的 .pfx (也稱為 PKCS #12) 憑證。<!--1321368--> 有兩種方法可建立 PFX 憑證設定檔：

  - 從現有憑證[匯入認證](../../mdm/deploy-use/import-pfx-certificate-profiles.md)
  - [定義憑證](../../mdm/deploy-use/create-pfx-certificate-profiles.md)授權單位以處理要求

  > [!Note]  
  > 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

  您可以使用 Microsoft 或 Entrust 作為**個人資訊交換 (.pfx)** 憑證的憑證授權單位。

## <a name="requirements"></a>需求

若要部署使用 SCEP 的憑證設定檔，請在站台系統伺服器上安裝憑證登錄點。 也可以在執行 Windows Server 2012 R2 或更新版本的伺服器上為 NDES 安裝原則模組 (Configuration Manager 原則模組)。 這部伺服器需要 Active Directory 憑證服務角色。 其也需要可供需要憑證的裝置存取的正常運作 NDES。 如果您的裝置需要從網際網路註冊憑證，則您的 NDES 伺服器必須可供從網際網路存取。 例如，若要安全地啟用從網際網路到 NDES 伺服器的流量，您可以使用 [Azure 應用程式 Proxy](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)。

PFX 憑證也需要憑證登錄點。 也請針對憑證指定憑證授權單位 (CA) 與相關的存取認證。 您可以將 Microsoft 或 Entrust 指定為憑證授權單位。  

如需 NDES 如何支援原則模組以供 Configuration Manager 部署憑證的詳細資訊，請參閱[使用原則模組和網路裝置註冊服務](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\))。

Configuration Manager 可根據需求將憑證部署至不同裝置類型與作業系統上的其他憑證存放區。 支援下列裝置和作業系統：  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> 請使用 Configuration Manager 內部部署 MDM 來管理 Windows Phone 8.1 和 Windows 10 行動裝置版。 如需詳細資訊，請參閱[內部部署 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。

Configuration Manager 的典型案例是安裝受信任的根 CA 憑證以驗證 Wi-Fi 和 VPN 伺服器。 典型的連線會使用下列通訊協定：

- 驗證通訊協定：EAP-TLS、EAP-TTLS 和 PEAP
- VPN 通道通訊協定：IKEv2、L2TP/IPsec 和 Cisco IPsec

企業根 CA 憑證必須安裝在裝置上，此裝置才能使用 SCEP 憑證設定檔要求憑證。  

您可以在 SCEP 憑證設定檔中指定設定，以針對不同的環境或連線需求要求自訂的憑證。 [建立憑證設定檔精靈]  具有兩個頁面的註冊參數。 第一個頁面 [SCEP 註冊]  包括註冊要求以及憑證安裝位置的設定。 第二個頁面 [憑證內容]  則說明要求的憑證本身。  

## <a name="deploy"></a>部署

當您部署 SCEP 憑證設定檔時，Configuration Manager 用戶端會處理原則。 然後，其會從管理點要求 SCEP 挑戰密碼。 裝置會建立公開/私密金鑰組，並產生憑證簽署要求 (CSR)。 其會將此要求傳送至 NDES 伺服器。 NDES 伺服器會透過 NDES 原則模組，將要求轉送到憑證登錄點站台系統。 憑證登錄點會驗證要求、檢查 SCEP 挑戰密碼，並確認要求未遭篡改。 接著，其會核准或拒絕要求。 若核准，NDES 伺服器就會將簽署要求傳送至已連線的憑證授權單位 (CA) 以進行簽署。 CA 會簽署要求，然後將憑證傳回給提出要求的裝置。

將憑證設定檔部署至使用者或裝置集合。 您可以指定每個憑證的目的地存放區。 適用性規則會決定裝置是否可以安裝憑證。

當您將憑證設定檔部署至使用者集合時，[使用者裝置親和性](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)會決定使用者的哪個裝置要安裝憑證。 當您將具有使用者憑證的憑證設定檔部署至裝置集合時，根據預設，每個使用者的主要裝置都會安裝憑證。 若要將憑證安裝至使用者的任何裝置上，請在 [建立憑證設定檔精靈]  的 [SCEP 註冊]  頁面上變更此行為。 如果裝置位於工作組中，Configuration Manager 就不會部署使用者憑證。  

## <a name="monitor"></a>監視

您可以檢視合規性結果或報告來監視憑證設定檔部署。 如需詳細資訊，請參閱[如何監視憑證設定檔](monitor-certificate-profiles.md)。

## <a name="automatic-revocation"></a>自動撤銷

在下列情況下，Configuration Manager 會自動撤銷使用憑證設定檔建立的使用者和電腦憑證：  

- Configuration Manager 管理功能已將裝置淘汰。  

- Configuration Manager 階層已封鎖裝置。  

網站伺服器會傳送撤銷命令到發行憑證授權單位，以撤銷憑證。 撤銷的原因是 [操作停止]  。

> [!NOTE]
> 若要正確撤銷憑證，階層中頂層站台的電腦帳戶需要有可在 CA 上**核發和管理憑證**的權限。
>
> 為了提升安全性，您也可以限制 CA 上的 CA 管理員。 然後只對此帳戶授與您用於站台上 SCEP 設定檔的特定憑證範本權限。

## <a name="next-steps"></a>後續步驟

- [建立憑證設定檔](create-certificate-profiles.md)

- [設定憑證基礎結構](certificate-infrastructure.md)
