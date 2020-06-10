---
title: 使用 Microsoft Intune 建立 iOS/iPadOS 或 macOS 裝置設定檔 - Azure | Micrososft Docs
description: 新增或建立 iOS、iPadOS 或 macOS 裝置設定檔。 在 Microsoft Intune 中針對 AirPrint、主畫面配置、應用程式通知、共用裝置、單一登入及網路內容篩選器設定進行設定。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 349fdc7b0f13f0999b8c9993bcaba1d458ebac59
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989198"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>在 Intune 中新增 iOS、iPadOS 或 macOS 裝置功能設定

Intune 包含許多可協助系統管理員控制 iOS、iPadOS 和 macOS 裝置的功能和設定。 例如，系統管理員可以：

- 允許使用者存取您網路中的 AirPrint 印表機
- 將應用程式與資料夾新增至主畫面，包括新增頁面
- 選擇是否要顯示應用程式通知及如何顯示
- 設定鎖定畫面以顯示一則訊息或資產標記，特別適用於共用裝置
- 為使用者提供在應用程式之間共用認證的安全單一登入體驗
- 篩選使用成人內容語言的網站，並允許或封鎖特定網站

Intune 會使用「組態設定檔」來依據貴組織的需求建立和自訂這些設定。 在設定檔中新增這些功能之後，接著將該設定檔推送或部署至組織中的 iOS/iPadOS 和 macOS 裝置。

本文描述您可以設定的各種功能，並示範如何建立裝置組態設定檔。 您也可以查看適用於 [iOS/iPadOS](ios-device-features-settings.md) 和 [macOS](macos-device-features-settings.md) 裝置的所有可用設定。

## <a name="airprint"></a>AirPrint

AirPrint 是可讓裝置透過無線網路列印到檔案的 Apple 功能。 在 Intune 中，您可以將 AirPrint 資訊新增至裝置。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的 AirPrint](ios-device-features-settings.md#airprint) 和 [macOS 上的 AirPrint](macos-device-features-settings.md#airprint)。

如需 AirPrint 的詳細資訊，請參閱 Apple 網站上的[關於 AirPrint](https://support.apple.com/HT201311)。

適用於：

- iOS 7.0 和更新版本
- iPadOS 13.0 和更新版本
- macOS 10.10 和更新版本

## <a name="app-notifications"></a>應用程式通知

選擇 iOS 和 iPadOS 裝置上應用程式接收通知的方式。 例如傳送應用程式通知，以使其顯示於通知中心、顯示於鎖定畫面上或播放音效。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的應用程式通知](ios-device-features-settings.md#app-notifications)。

如需此功能的詳細資訊，請參閱 Apple 網站上的[通知](https://developer.apple.com/notifications/) \(英文\)。

適用於：

- iOS 9.3 與更新版本
- iPadOS 13.0 和更新版本

## <a name="associated-domains"></a>相關網域

相關網域可讓您在網域 (例如 `contoso.com`) 和您的應用程式之間建立關聯性。 此功能可讓您：

- 在組織中的應用程式與網站之間共用資料和登入認證。
- 使用以您的網站為基礎的應用程式功能，例如，單一登入應用程式擴充功能、通用連結，以及自動填滿密碼。

  例如，建立相關網域以允許自動填滿密碼為與您應用程式相關聯的網站建議認證 (例如密碼)。

如需可在 Intune 中設定的設定清單，請參閱 [macOS 上的相關網域](macos-device-features-settings.md#associated-domains)。

如需此功能的詳細資訊，請參閱 Apple 網站上的[設定應用程式的相關網域](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) \(英文\)。

適用於：

- macOS 10.15 與更新版本

## <a name="home-screen-layout"></a>主畫面配置

這些設定會在 iOS 和 iPadOS 裝置的 Dock 和主畫面上設定應用程式配置和資料夾。 您可以：

- 使用 **Dock** 設定來將應用程式或資料夾新增至畫面。 例如，在裝置 Dock 上顯示 [Safari] 和 [郵件] 應用程式。
- 新增您想要顯示於主畫面上的**頁面**，以及要顯示於每個頁面上的應用程式。 例如，新增 [Contoso] 頁面，然後在此頁面上新增 [設定] 應用程式。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的主畫面配置](ios-device-features-settings.md#home-screen-layout)。

適用於：

- iOS 9.3 與更新版本
- iPadOS 13.0 和更新版本

## <a name="lock-screen-message"></a>鎖定畫面訊息

使用這些設定以在登入視窗和鎖定畫面上顯示自訂訊息或文字。 例如，您可以輸入「若遺失，請送回...」訊息，並顯示資產標籤資訊。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的鎖定畫面訊息設定](ios-device-features-settings.md#lock-screen-message)。

如需鎖定畫面訊息的詳細資訊，請參閱 Apple 網站上的 [LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage) \(英文\)。

適用於：

- iOS 9.3 與更新版本
- iPadOS 13.0 和更新版本

## <a name="login-items"></a>登入項目

使用此功能，來選擇使用者登入裝置時所開啟的應用程式、自訂應用程式、檔案和資料夾。

如需可在 Intune 中設定的設定清單，請參閱 [macOS 上的登入項目](macos-device-features-settings.md#login-items)。

適用於：

- macOS 10.13 與更新版本

## <a name="login-window"></a>登入視窗

控制登入畫面的外觀，以及使用者在登入之前可使用的功能。 例如，新增具有自訂訊息的橫幅，選擇是否要顯示 [睡眠] 按鈕，以及其他功能。

如需可在 Intune 中設定的設定清單，請參閱 [macOS 上的登入視窗](macos-device-features-settings.md#login-window)。

適用於：

- macOS 10.7 和更新版本

## <a name="single-sign-on"></a>單一登入

大部分的企業營運 (LOB) 應用程式需要某種程度的使用者驗證才會支援安全性。 在許多情況下，驗證都會要求使用者重複輸入相同認證。 為了改善使用者體驗，開發人員可以建立使用單一登入 (SSO) 的應用程式。 使用單一登入可減少使用者必須輸入認證的次數。

單一登入設定檔是以 Kerberos 為基礎。 Kerberos 是一種網路驗證通訊協定，其使用秘密金鑰加密來驗證用戶端與伺服器應用程式。 Intune 設定會在存取伺服器或指定的應用程式時定義 Kerberos 帳戶資訊，並處理網頁和原生應用程式的 Kerberos 挑戰。 Apple 建議您使用 [Kerberos SSO 應用程式擴充功能](#single-sign-on-app-extension) (在本文中) 設定，而不是 SSO 設定。  

若要使用單一登入，請確定您已具備：

- 已將程式碼撰寫成會在裝置上的單一登入中尋找使用者認證存放區的應用程式。
- 設定進行 iOS/iPadOS 裝置單一登入的 Intune。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的單一登入](ios-device-features-settings.md#single-sign-on)。

適用於：

- iOS 7.0 和更新版本
- iPadOS 13.0 和更新版本

## <a name="single-sign-on-app-extension"></a>單一登入應用程式擴充功能

這些設定會設定應用程式擴充功能，以便為您的 iOS、iPadOS 和 macOS 裝置啟用單一登入 (SSO)。 大部分的企業營運 (LOB) 應用程式和組織網站都需要某種程度的安全使用者驗證。 在許多情況下，驗證都會要求使用者重複輸入相同認證。 SSO 讓使用者在輸入其認證一次之後，就能存取應用程式和網站。 SSO 也會為使用者提供更好的驗證體驗，並減少重複提示認證的次數。

在 Intune 中，使用這些設定來設定貴組織、您的識別提供者、Microsoft 或 Apple 所建立的 SSO 應用程式延伸模組。 SSO 應用程式擴充功能會為您的使用者處理驗證。 這些設定會設定重新導向類型和認證類型的 SSO 應用程式延伸模組。

- 重新導向類型是專為 OpenID Connect、OAuth 與 SAML2 等新式驗證通訊協定設計的。 您可以在 macOS 裝置上使用一般重新導向擴充功能。 對於 iOS/iPadOS 裝置，您可選擇 Microsoft 的 Azure AD SSO 擴充功能 ([Microsoft 企業單一登入外掛程式](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)) 和一般重新導向擴充功能。
- 認證類型是專為挑戰和回應驗證流程所設計。 您可以在 Apple 所提供的 Kerberos 特定認證擴充功能和一般認證擴充功能之間進行選擇。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS SSO 應用程式延伸模組](ios-device-features-settings.md#single-sign-on-app-extension)和 [macOS SSO 應用程式延伸模組](macos-device-features-settings.md#single-sign-on-app-extension)。

如需開發 SSO 應用程式延伸模組的詳細資訊，請觀賞 Apple 網站上的[可擴充的企業 SSO](https://developer.apple.com/videos/play/tech-talks/301) \(英文\)。 若要閱讀 Apple 的功能描述，請瀏覽[「單一登入延伸功能」承載資料設定](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web)。 

> [!NOTE]
> **單一登入應用程式擴充功能**與**單一登入**功能不同：
>
> - **單一登入應用程式延伸模組**設定適用於 iPadOS 13.0 (和更新版本)、iOS 13.0 (和更新版本) 及 macOS 10.15 (和更新版本)。 **單一登入**設定適用於 iPadOS 13.0 (和更新版本) 及 iOS 7.0 和更新版本。
>
> - **單一登入應用程式延伸模組**設定會定義識別提供者或組織用於提供順暢企業登入體驗的延伸模組。 **單一登入**設定會定義當使用者存取伺服器或應用程式時的 Kerberos 帳戶資訊。
>
> - **單一登入應用程式擴充功能**會使用 Apple 作業系統進行驗證。 因此，可能會提供比**單一登入**更好的終端使用者體驗。
>
> - 從開發觀點來看，透過**單一登入應用程式延伸模組**，您可以使用任何類型的重新導向 SSO 或認證 SSO 驗證。 使用**單一登入**，您只能使用 Kerberos SSO 驗證。
>
> - Kerberos **單一登入應用程式延伸模組**是由 Apple 所開發，並內建於 iOS/iPadOS 13.0+ 和 macOS 10.15+ 平台。 內建的 Kerberos 延伸模組可用來將使用者登入支援 Kerberos 驗證的原生應用程式和網站。 **單一登入**不是 Apple 的 Kerberos 實作。
>
> - 內建的 Kerberos **單一登入應用程式延伸模組**可處理網頁和應用程式的 Kerberos 挑戰，就像是**單一登入**一樣。 不過，內建的 Kerberos 延伸模組支援密碼變更，且在企業網路中的表現更佳。 當您決定要使用**單一登入應用程式延伸模組**或**單一登入**時，建議使用延伸模組，因為其效能和功能均已獲得改善。

適用於：

- iOS 13.0 與更新版本
- iPadOS 13.0 和更新版本
- macOS 10.15 與更新版本

## <a name="wallpaper"></a>桌布

將自訂的 .png、.jpg 或 .jpeg 影像新增至受監督 iOS/iPadOS 裝置。 例如，使用 Intune 來將公司標誌新增至裝置上的鎖定畫面。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的底色圖案](ios-device-features-settings.md#wallpaper)。

適用於：

- iOS
- iPadOS 13.0 和更新版本

## <a name="web-content-filter"></a>Web 內容篩選

這些設定會使用 Apple 的內建自動篩選演算法來評估網頁，並封鎖成人內容和成人語言。 您也可以建立已允許的網頁連結及受限制之網頁連結的清單。 例如，您可以允許僅開啟 `contoso` 網站。

如需可在 Intune 中設定的設定清單，請參閱 [iOS/iPadOS 上的內容篩選](ios-device-features-settings.md#web-content-filter)。

適用於：

- iOS 7.0 和更新版本
- iPadOS 13.0 和更新版本

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選擇您的裝置平台。 選項包括：  

        - **iOS/iPadOS**
        - **macOS**

    - **設定檔**：選取 [裝置功能]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱是 **macOS：設定登入畫面**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。

7. 在 [組態設定] 中，您可進行的設定會根據您選擇的平台而不同。 選擇您平台來進行詳細設定：

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. 選取 [下一步]。
9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="next-steps"></a>後續步驟

雖然設定檔已建立，但它可能還不會執行任何動作。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

檢視適用於 [iOS/iPadOS](ios-device-features-settings.md) 和 [macOS](macos-device-features-settings.md) 裝置的所有裝置功能設定。
