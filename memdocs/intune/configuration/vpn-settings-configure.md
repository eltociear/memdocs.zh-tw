---
title: 在 Microsoft Intune 中將 VPN 設定新增至裝置 - Azure | Microsoft Docs
description: 針對 Android 裝置系統管理員、Android 企業、iOS、iPadOS、macOS 與 Windows 裝置，請使用內建設定，在 Microsoft Intune 中建立虛擬私人網路 (VPN) 連線。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64356bf9be0c2c439c1f4fc296a9728a7937b001
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086567"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>在 Intune 中建立 VPN 設定檔以連線到 VPN 伺服器

虛擬私人網路 (VPN) 為使用者提供安全的組織網路遠端存取。 裝置會使用 VPN 連線設定檔來啟動與 VPN 伺服器的連線。 Microsoft Intune 中的 **VPN 設定檔**會將 VPN 設定指派給組織中的使用者與裝置，讓他們可以輕鬆且安全地連線到組織網路。

例如，您想要使用連線到組織網路上檔案共用所需的設定來設定所有 iOS/iPadOS 裝置。 您會建立包含這些設定的 VPN 設定檔。 接著，您需將此設定檔指派給所有擁有 iOS/iPadOS 裝置的使用者。 這些使用者會在可用的網路清單中看到此 VPN 連線，而且很輕鬆就能建立連線。

> [!NOTE]
> 您可以使用 [Intune 自訂設定原則](custom-settings-configure.md)來建立下列平台的 VPN 設定檔：
>
> * Android 4 及更新版本
> * 執行 Windows 8.1 和更新版本的已註冊裝置
> * Windows Phone 8.1 和更新版本
> * 執行 Windows 10 Desktop 的已註冊裝置
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>VPN 連線類型

您可使用下列連線類型，建立 VPN 設定檔︰

- 自動
  - Windows 10

- Check Point Capsule VPN
  - Android 裝置管理員
  - Android 企業工作設定檔
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Android 裝置管理員
  - Android 企業工作設定檔
  - Android Enterprise 裝置擁有者 (完全受控)
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Android 裝置管理員
  - Android 企業工作設定檔：使用[應用程式設定原則](../apps/app-configuration-policies-use-android.md)
  - Android 企業裝置擁有者 (完全受控)：使用[應用程式設定原則](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- 自訂 VPN
  - iOS/iPadOS
  - macOS

  在[使用自訂設定來建立設定檔](custom-settings-configure.md)中，使用 URI 設定來建立自訂 VPN 設定檔。

- F5 Access
  - Android 裝置管理員
  - Android 企業工作設定檔
  - Android Enterprise 裝置擁有者 (完全受控)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android 企業工作設定檔：使用[應用程式設定原則](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Android 裝置管理員
  - Android 企業工作設定檔
  - Android Enterprise 裝置擁有者 (完全受控)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Android 裝置管理員
  - Android 企業工作設定檔
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Zscaler
  - Android 企業工作設定檔：使用[應用程式設定原則](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS

> [!IMPORTANT]
> 您必須先針對設定檔安裝適用的 VPN 應用程式，才能使用指派至裝置的 VPN 設定檔。 為協助您使用 Intune 指派應用程式，請參閱[什麼是 Microsoft Intune 應用程式管理？](../apps/app-management.md)。  

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。
3. 輸入下列內容：

    - **平台**：選擇您的裝置平台。 選項包括：
      - **Android 裝置系統管理員**
      - **Android Enterprise** > **僅限裝置擁有者**
      - **Android Enterprise** > **僅限工作設定檔**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 及以上版本**
      - **Windows 8.1 及更新版本**
      - **Windows Phone 8.1**
    - **設定檔**：選取 [VPN]  。

4. 選取 [建立]  。
5. 在 [基本資訊]  中，輸入下列內容：

    - **名稱**：為設定檔輸入描述性名稱。 命名您的設定檔，以方便之後能輕鬆識別。 例如，良好的設定檔名稱為**適用於整家公司的 VPN 設定檔**。
    - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]  。
7. 在 [組態設定]  中，您可進行的設定會根據您選擇的平台而不同。 選取您的平台來進行詳細設定：

    - [Android 裝置系統管理員](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (包括 Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. 選取 [下一步]  。
9. 在 [範圍標籤]  (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]  。

10. 在 [指派]  中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]  。

11. 在 [檢閱 + 建立]  中，檢閱您的設定。 當您選取 [建立]  時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="secure-your-vpn-profiles"></a>保護您的 VPN 設定檔

VPN 設定檔可以使用來自不同製造商的多種連線類型及通訊協定。 這些連線通常會透過以下方法來保護。

### <a name="certificates"></a>憑證

當您建立 VPN 設定檔時，請選擇先前在 Intune 中建立的 SCEP 或 PKCS 憑證設定檔。 這個設定檔稱為識別憑證。 此憑證可用來針對您為允許使用者裝置進行連線而建立的受信任憑證設定檔 (或*根憑證*) 進行驗證。 受信任的憑證會指派到可驗證 VPN 連線的電腦 (一般是 VPN 伺服器)。

如需如何在 Intune 中建立及使用憑證設定檔的詳細資訊，請參閱[如何利用 Microsoft Intune 設定憑證](../protect/certificates-configure.md)。

### <a name="user-name-and-password"></a>使用者名稱和密碼

使用者藉由提供使用者名稱和密碼向 VPN 伺服器進行驗證。

## <a name="next-steps"></a>後續步驟

一旦設定檔建立完成，它還不會執行任何動作。 接下來，[將設定檔指派給一些裝置](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以在 [Android 裝置系統管理員/Android 企業](android-pulse-secure-per-app-vpn.md)與 [iOS/iPadOS](vpn-setting-configure-per-app.md) 裝置上，建立及使用個別應用程式 VPN。
