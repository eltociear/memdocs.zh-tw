---
title: 如何建立 VPN 設定檔
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中建立 VPN 設定檔。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 17811d0bb0b72ebee6879d5dab90e165b439081b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694246"
---
# <a name="how-to-create-vpn-profiles-in-configuration-manager"></a>如何在 Configuration Manager 中建立 VPN 設定檔

適用於：  Configuration Manager (最新分支)

Configuration Manager 支援多種 VPN 連線類型。 如需可供不同裝置平台使用的連線類型詳細資訊，請參閱 [VPN 設定檔](vpn-profiles.md)。

若為協力廠商 VPN 連線，請先發佈 VPN 應用程式再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們執行此動作。 如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。

## <a name="create-a-vpn-profile"></a>建立 VPN 設定檔

1. 移至 Configuration Manager 主控台的 [資產與相容性]  工作區，依序展開 [相容性設定]  和 [公司資源存取]  ，然後選取 [VPN 設定檔]  節點。

1. 在功能區的 [首頁]  索引標籤上，選擇 [建立]  群組中的 [建立 VPN 設定檔]  。

1. 在 [建立 VPN 設定檔精靈] 的 [一般]  頁面上，指定下列資訊：

    - **名稱**：輸入可以在主控台中，專門用於識別 VPN 設定檔的唯一名稱。

        > [!NOTE]
        > 請勿在 VPN 設定檔名稱中使用下列字元：`\/:*?<>|; `。 Windows VPN 設定檔不支援這些特殊字元。

    - **描述**：視需要輸入描述，以提供 VPN 設定檔的更多資訊。

    - **VPN 設定檔類型**：選取適當的平台。

        如果選取 **Windows 8.1** 平台，您也可以 [從檔案匯入]  。 此動作會從 XML 檔案匯入 VPN 設定檔資訊。 若選取此選項，精靈的步驟將只剩下下列頁面：[支援的平台]  與 [匯入 VPN 設定檔]  。

1. 在 [支援的平台]  頁面上，選取此 VPN 設定檔支援的作業系統版本。

1. 在 [連線]  頁面上，指定下列資訊：

    - **連線類型**：選擇 VPN 連線類型。 如需支援類型的詳細資訊，請參閱 [VPN 設定檔](vpn-profiles.md)。

    - **伺服器清單**：新增要用於 VPN 連線的新伺服器。 視連線類型而定，您可以新增一或多部 VPN 伺服器，並指定預設的伺服器。

    - **連線到公司 Wi-Fi 網路時不要使用 VPN**：設定當用戶端位於內部網路時，不要使用 VPN。 如有必要，請指定連線特定的 DNS 名稱。

1. 在精靈的 [驗證方法]  頁面中，選擇連線類型支援的方法。 此頁面上設定和可用選項會因選取的連線類型而異。 如需詳細資訊，請參閱[驗證方法參考](#bkmk_auth)。

1. 在 [Proxy 設定]  頁面上，如果 VPN 使用 Proxy 伺服器，賄請為您環境選取適當的其中一個選項。 然後提供 Proxy 的設定資訊。

1. [應用程式]  頁面僅適用於 Windows 10 設定檔。 新增可自動連線到此 VPN 的桌面和通用應用程式。 應用程式類型決定應用程式識別碼：

    - 為「桌面應用程式」  提供應用程式的檔案路徑。

    - 為「通用應用程式」  提供套件系列名稱 (PFN)。 若要了解如何尋找應用程式的 PFN，請參閱[尋找個別應用程式 VPN 的套件系列名稱](find-a-pfn-for-per-app-vpn.md)。

    您也可以設定選項，讓 [只有列出的 APP 可以使用此 VPN]  。

    > [!IMPORTANT]
    > 為您設定個別應用程式 VPN 所編譯的所有相關聯應用程式清單提供保護。 如果未經授權的使用者變更您的清單，而您將該清單匯入個別應用程式 VPN 應用程式清單中，就可能會授與 VPN 權限，讓 VPN 存取本不該存取的應用程式。

1. [界限]  頁面只適用於設定 VPN 界限的 Windows 10 設定檔。 您可以新增下列選項︰

    - **網路流量規則**：設定要針對 VPN 連線啟用的通訊協定、本機連接埠、遠端連接埠和位址範圍。  

        > [!Note]
        > 如果您未建立網路流量規則，則會啟用所有通訊協定、連接埠和位址範圍。 當您建立規則之後，VPN 連線便只會使用您在該項規則或其他規則中所指定的通訊協定、連接埠和位址範圍。

    - **DNS 名稱與伺服器**：裝置建立連線後，VPN 連線所使用的 DNS 伺服器。

    - **路由**：使用 VPN 連線的網路路由。 如果建立超過 60 個路由，可能會導致原則失敗。

1. 完成精靈。

新的 VPN 設定檔會顯示在 [資產與合規性]  工作區的 [VPN 設定檔]  節點中。

## <a name="authentication-method-reference"></a><a name="bkmk_auth"></a>驗證方法參考

視連線類型而定的可用 VPN 驗證方法：

### <a name="certificates"></a>憑證

如果用戶端憑證會驗證 RADIUS 伺服器 (例如，網路原則伺服器)，則憑證中的主體別名必須設為使用者主體名稱。

支援的連線類型：

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- 檢查點行動 VPN

### <a name="username-and-password"></a>使用者名稱和密碼

支援的連線類型：

- Pulse Secure
- F5 Edge Client
- Dell SonicWALL Mobile Connect
- 檢查點行動 VPN

### <a name="microsoft-eap-ttls"></a>Microsoft EAP-TTLS

支援的連線類型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- PPTP
- IKEv2
- L2TP

### <a name="microsoft-protected-eap-peap"></a>Microsoft Protected EAP (PEAP)

支援的連線類型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="microsoft-secured-password-eap-mschap-v2"></a>Microsoft secured password (EAP-MSCHAP v2)

支援的連線類型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="smart-card-or-other-certificate"></a>智慧卡或其他憑證

支援的連線類型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="mschap-v2"></a>MSCHAP v2

支援的連線類型：

- Microsoft SSL (SSTP)
- Microsoft Automatic
- IKEv2
- PPTP
- L2TP

### <a name="use-machine-certificates"></a>使用電腦憑證

支援的連線類型：

- IKEv2

### <a name="additional-authentication-options"></a>其他驗證選項

如果 Windows 用戶端版本支援此功能，即會提供 [設定]  驗證方法的選項。 此選項會開啟 Windows 屬性視窗，讓您設定驗證方法。

視選取的選項而定，系統可能會要求指定更多資訊，例如：

- **在每次登入時記住使用者認證**：因為系統記住了使用者認證，所以使用者不必每次連線都要輸入認證。  

- **選取用戶端驗證的用戶端憑證**：選取先前建立的用戶端 SCEP 憑證設定檔，以驗證 VPN 連線。 如需詳細資訊，請參閱[建立 PFX 憑證設定檔](create-certificate-profiles.md)。

## <a name="next-steps"></a>後續步驟

- 若為協力廠商 VPN 連線，請先發佈 VPN 應用程式再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們執行此動作。 如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。

- 部署 VPN 設定檔。 如需詳細資訊，請參閱[如何部署設定檔](deploy-wifi-vpn-email-cert-profiles.md)。
