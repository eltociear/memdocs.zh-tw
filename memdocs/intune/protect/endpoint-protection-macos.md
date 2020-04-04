---
title: 在 Microsoft Intune 中於 macOS 上新增 Endpoint Protection - Azure | Microsoft Docs
description: 在 macOS 裝置上，使用閘道管理員來判斷可安裝應用程式的位置，包括 Mac App Store。 此外，也使用 Microsoft Intune 來啟用或設定防火牆以允許特定應用程式、封鎖特定應用程式、使用隱形模式，甚至是封鎖特定類型的連入連線。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359459"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune 中的 macOS Endpoint Protection 設定  

此文章說明您可以為執行 macOS 的裝置設定的 Endpoint Protection 設定。 您可以使用 macOS 裝置設定檔來設定這些設定，以在 Intune 中進行[端點保護](endpoint-protection-configure.md)。  

## <a name="before-you-begin"></a>開始之前

[建立 macOS Endpoint Protection 設定檔](endpoint-protection-configure.md)。

## <a name="gatekeeper"></a>閘道管理員  

- **允許從這些位置下載的應用程式**  
  根據下載應用程式的位置，限制裝置可以啟動的應用程式。 用意是要保護裝置免於惡意程式碼危害，而只允許來自您所信任來源的應用程式。  

  - **未設定**  
  - **Mac App Store**  
  - **Mac App Store 和已識別的開發人員**  
  - **任何位置**  

  **預設**：尚未設定  

- **使用者可覆寫閘道管理員**  
  防止使用者覆寫閘道管理員設定，並防止使用者透過按住 Control 鍵再按一下來安裝應用程式。 啟用時，使用者可以按住 Control 鍵再按一下任何應用程式來安裝該應用程式。  
 
  - **未設定** - 使用者可以按住 Control 同時按一下來安裝應用程式。  
  - **封鎖** - 防止使用者按住 Control 同時按一下來安裝應用程式。  

  **預設**：尚未設定  

## <a name="firewall"></a>防火牆  

使用防火牆來控制個別應用程式 (而非個別連接埠) 的連線。 使用個別應用程式設定可讓您更容易獲得防火牆保護的好處。 這還有助於防止不想要的應用程式控制為合法應用程式開啟的網路連接埠。  

**一般**
- **防火牆**  
  啟用防火牆以設定您環境中處理連入連線的方式。  
  - **未設定**  
  - **啟用**  

  **預設**：尚未設定  

- **連入連線**  
  除了基本網際網路服務所需的連線 (例如 DHCP、Bonjour 及 IPSec) 之外，封鎖所有連入連線。 此功能也會封鎖所有共用服務，例如「檔案共用」和「螢幕共用」。 如果您目前使用共用服務，請將此設定保持為 [未設定]  。  
  - **未設定**  
  - **封鎖**  

  **預設**：尚未設定  

**允許或封鎖特定應用程式的連入連線。**  

  - **允許的應用程式**  
    選取明確允許接收連入連線的應用程式。  

  - **封鎖的應用程式**  
    選取應封鎖連入連線的應用程式。  

  - **隱形模式**  
    若要防止電腦回應探查要求，請啟用隱形模式。 電腦會繼續回應已授權應用程式的連入要求。 ICMP (ping) 等未預期的要求都會予以忽略。  
    - **未設定**  
    - **啟用**  

    **預設**：尚未設定  

## <a name="filevault"></a>FileVault  
如需 Apple FileVault 設定的詳細資訊，請參閱 Apple 開發人員內容中的 [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault)。 

> [!IMPORTANT]  
> 自 macOS 10.15 起，FileVault 設定需要使用者核准的 MDM 註冊。 

- **FileVault**  
  您可以在執行 macOS 10.13 和更新版本的裝置上，使用 XTS-AES 128 搭配 FileVault 來「啟用」  完整磁碟加密。  
  - **未設定**  
  - **啟用**  

  **預設**：尚未設定  

  - **修復金鑰類型**  
    將會為裝置建立「個人金鑰」  修復金鑰。 請設定個人金鑰的下列設定。  

    - **個人修復金鑰的位置** - 指定簡短的訊息給使用者，其說明如何以及在何處可以擷取其個人修復金鑰。 系統在使用者忘記密碼而提示其輸入個人修復金鑰時，會將此文字插入至使用者在其登入畫面上看到的訊息中。  

    - **個人修復金鑰輪替** - 指定此裝置上個人修復金鑰的輪替頻率。 您可以選取預設的 [未設定]  ，或 **1** 到 **12** 個月的值。  

  - **停用登出時的提示**  
    當使用者登出時，避免提示使用者要求其啟用 FileVault。當設定為 [停用] 時，會停用登出時的提示，並改為在使用者登入時向其提示。  
    - **未設定**  
    - **停用** - 在登出時停用提示。

    **預設**：尚未設定  

  - **允許略過的次數**  
  設定使用者可以忽略幾次啟用 FileVault 的提示，使用者即會需要 FileVault 才能登入。 

    - **未設定** - 在允許下一次登入之前，需要在裝置上進行加密。  
    - **1** 到 **10** - 需要在裝置上進行加密之前，允許使用者忽略提示 1 到 10 次。  
    - **無限制，一律提示** - 系統會提示使用者啟用 FileVault，但永遠不需要加密。  
 
    **預設**：變動  - 當 [停用登出時的提示]  設定為 [未設定]  時，此設定預設為 [未設定]  。 當 [停用登出時的提示]  設定為 [停用]  時，此設定預設為 **1**，且 [未設定]  值不是選項。

如需使用 FileVault 搭配 Intune 的詳細資訊，請參閱 [FileVault 修復金鑰](encryption-monitor.md#filevault-recovery-keys)。

## <a name="next-steps"></a>後續步驟

[指派設定檔](../configuration/device-profile-assign.md)並[監視其狀態](../configuration/device-profile-monitor.md)。

您也可以在 [Windows 10 和更新版本的裝置](endpoint-protection-windows-10.md)上設定 Endpoint Protection。
