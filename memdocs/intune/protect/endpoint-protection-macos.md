---
title: 使用 Microsoft Intune 在 macOS 裝置上設定 Endpoint Protection | Microsoft Docs
description: 使用 Intune 設定 macOS 裝置使用內建防火牆來允許或封鎖特定應用程式，或使用隱形模式、使用 Gatekeeper 來判斷應用程式的安裝位置，以及使用 FileVault 磁碟加密。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107520"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune 中的 macOS Endpoint Protection 設定

此文章說明您可以為執行 macOS 的裝置設定的 Endpoint Protection 設定。 您可以使用 macOS 裝置設定檔來設定這些設定，以在 Intune 中進行[端點保護](endpoint-protection-configure.md)。

## <a name="before-you-begin"></a>開始之前

[建立 macOS Endpoint Protection 設定檔](endpoint-protection-configure.md)。

## <a name="firewall"></a>防火牆

使用防火牆來控制個別應用程式 (而非個別連接埠) 的連線。 使用個別應用程式設定可讓您更容易獲得防火牆保護的好處。 這還有助於防止不想要的應用程式控制為合法應用程式開啟的網路連接埠。

- [啟用防火牆]

  在 macOS 上啟用防火牆，然後設定環境中處理連入連線的方式。

  - [未設定] (預設)
  - **是**

- [封鎖所有連入連線]

  除了基本網際網路服務所需的連線 (例如 DHCP、Bonjour 及 IPSec) 之外，封鎖所有連入連線。 此功能也會封鎖所有共用服務，例如「檔案共用」和「螢幕共用」。 如果您目前使用共用服務，請將此設定保持為 [未設定]。

  - [未設定] (預設)
  - **是**

  當將 [封鎖所有連入連線] 設定為 [未設定] 時，您可接著設定哪些應用程式可以或不可以接收連入連線。

  **允許的應用程式**：設定允許接收連入連線的應用程式清單。

  - **依套件組合識別碼新增應用程式**：輸入應用程式的[套件組合識別碼](../configuration/bundle-ids-built-in-ios-apps.md)。 Apple 的網站會提供[內建 Apple 應用程式](https://support.apple.com/HT208094)清單。
  - **新增市集應用程式**：選取先前新增至 Intune 的市集應用程式。 如需詳細資訊，請參閱[將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

  **封鎖的應用程式**：設定封鎖連入連線的應用程式清單。

  - **依套件組合識別碼新增應用程式**：輸入應用程式的[套件組合識別碼](../configuration/bundle-ids-built-in-ios-apps.md)。 Apple 的網站會提供[內建 Apple 應用程式](https://support.apple.com/HT208094)清單。
  - **新增市集應用程式**：選取先前新增至 Intune 的市集應用程式。 如需詳細資訊，請參閱[將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

- **啟用隱形模式**

  若要防止電腦回應探查要求，請啟用隱形模式。 電腦會繼續回應已授權應用程式的連入要求。 ICMP (ping) 等未預期的要求都會予以忽略。

  - [未設定] (預設)
  - **是**

## <a name="gatekeeper"></a>閘道管理員

- **允許從這些位置下載的應用程式**

  根據下載應用程式的位置，限制裝置可以啟動的應用程式。 用意是要保護裝置免於惡意程式碼危害，而只允許來自您所信任來源的應用程式。

  - [未設定] (預設)
  - **Mac App Store**
  - **Mac App Store 和已識別的開發人員**
  - **任何位置**

- **不允許使用者覆寫閘道管理員**

  防止使用者覆寫閘道管理員設定，並防止使用者透過按住 Control 鍵再按一下來安裝應用程式。 啟用時，使用者可以按住 Control 鍵再按一下任何應用程式來安裝該應用程式。

  - **未設定** (預設) - 使用者可按住 Ctrl 同時按一下來安裝應用程式。
  - **是** - 防止使用者按住 Control 同時按一下來安裝應用程式。

## <a name="filevault"></a>FileVault

如需 Apple FileVault 設定的詳細資訊，請參閱 Apple 開發人員內容中的 [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault)。

> [!IMPORTANT]
> 自 macOS 10.15 起，FileVault 設定需要使用者核准的 MDM 註冊。

- **啟用 FileVault**  

  您可以在執行 macOS 10.13 和更新版本的裝置上，使用 XTS-AES 128 搭配 FileVault 來「啟用」完整磁碟加密。

  - [未設定] (預設)
  - **是**

  當 [啟用 FileVault] 設定為 [是] 時，即可進行下列設定：

  - **修復金鑰類型**

    將會為裝置建立「個人金鑰」修復金鑰。 請設定個人金鑰的下列設定。

  - **個人修復金鑰的委付位置描述**

    指定簡短的訊息給使用者，其說明如何以及在何處可擷取其個人修復金鑰。 系統在使用者忘記密碼而提示其輸入個人修復金鑰時，會將此文字插入至使用者在其登入畫面上看到的訊息中。

  - **個人修復金鑰輪替**

    指定裝置的個人修復金鑰輪替頻率。 您可以選取預設的 [未設定]，或 **1** 到 **12** 個月的值。

  - **隱藏修復金鑰**

    選擇在 FileVault 2 加密期間對裝置使用者隱藏個人金鑰。

    - **未設定** (預設) - 在加密期間向裝置使用者顯示個人金鑰。
    - **是** - 在加密期間對裝置使用者隱藏個人金鑰。

    加密後，裝置使用者可從下列位置檢視已加密 macOS 裝置的個人修復金鑰：
    - iOS/iPadOS 公司入口網站應用程式
    - Intune 應用程式
    - 公司入口網站
    - Android 公司入口網站應用程式

    若要檢視金鑰，請從應用程式或網站移至已加密 macOS 裝置的 [裝置詳細資料]，然後選取 [取得修復金鑰]。

  - **停用登出時的提示**

    當使用者登出時，避免提示使用者要求其啟用 FileVault。當設定為 [停用] 時，會停用登出時的提示，並改為在使用者登入時向其提示。

    - [未設定] (預設)
    - **是** - 在登出時停用提示。

  - **允許略過的次數**

    設定使用者可以忽略幾次啟用 FileVault 的提示，使用者即會需要 FileVault 才能登入。

    - **未設定** - 在允許下一次登入之前，需要在裝置上進行加密。
    - **0** - 要求裝置在下一次使用者登入裝置時加密。
    - **1** 到 **10** - 需要在裝置上進行加密之前，允許使用者忽略提示 1 到 10 次。
    - **無限制，一律提示** - 系統會提示使用者啟用 FileVault，但永遠不需要加密。

    此設定其預設值取決於 [停用登出時的提示] 設定。當 [停用登出時的提示] 設定為 [未設定] 時，此設定預設為 [未設定]。 當 [停用登出時的提示] 設定為 [是] 時，此設定預設為 **1**，且 [未設定] 值不是選項。

## <a name="next-steps"></a>後續步驟

[指派設定檔](../configuration/device-profile-assign.md)並[監視其狀態](../configuration/device-profile-monitor.md)。

您也可以在 [Windows 10 和更新版本的裝置](endpoint-protection-windows-10.md)上設定 Endpoint Protection。
