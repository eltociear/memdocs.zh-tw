---
title: 在 Microsoft Intune 中設定 macOS 裝置的 Wi-Fi 設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 建立或新增適用於 macOS 裝置的 WiFi 裝置組態設定檔。 請查看不同的設定，包括在 Microsoft Intune 中新增憑證、選擇 EAP 類型，以及選取驗證方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e878294a9af6b80358aa495aa4d10ac6ed93404
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086353"
---
# <a name="add-wi-fi-settings-for-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中新增適用於 macOS 裝置的 Wi-Fi 設定

您可以建立含有特定 WiFi 設定的設定檔，然後將此設定檔部署到您的 macOS 裝置。 Microsoft Intune 提供許多功能，包括驗證您的網路、新增 PKS 或 SCEP 憑證等等。

這些 Wi-Fi 設定分為兩種類別：基本設定和企業層級設定。

本文說明了這些設定。

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](wi-fi-settings-configure.md)。

> [!NOTE]
> 這些設定適用於所有註冊類型。 如需註冊類型的詳細資訊，請參閱 [macOS 註冊](../enrollment/macos-enroll.md)。

## <a name="basic-profiles"></a>基本設定檔

- **Wi-Fi 類型**：選擇 [基本]  。
- **網路名稱**：輸入此 Wi-Fi 連線的名稱。 此值是使用者瀏覽裝置上的可用連線清單時所見到的名稱。
- **SSID**：[服務組識別元]  (service set identifier) 的縮寫。 此內容是裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的網路名稱。
- **自動連線**：選擇 [啟用]  可讓裝置在位於網路連線範圍內時自動連線到此網路。 選擇 [停用]  可防止裝置自動連線。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。
- **安全性類型**：選取向 Wi-Fi 網路驗證時要使用的安全性通訊協定。 選項包括：

  - **開放 (無驗證)** ：只有在網路不安全時才使用此選項。
  - **WPA/WPA2 - Personal**：在 [預先共用金鑰]  中輸入密碼。 當您的組織建置或設定網路時，也會設定密碼或網路金鑰。 請輸入此密碼或網路金鑰作為 PSK 值。
  - **WEP**

- **Proxy 設定**：選項包括：
  - **無**：不設定任何 Proxy 設定。
  - **手動**：輸入 **Proxy 伺服器位址**作為 IP 位址，以及其**連接埠號碼**。
  - **自動**：使用檔案設定 Proxy 伺服器。 輸入包含設定檔的 [Proxy 伺服器 URL]  (例如 `http://proxy.contoso.com`)。

## <a name="enterprise-profiles"></a>企業設定檔

- **Wi-Fi 類型**：選擇 [企業]  。
- **SSID**：[服務組識別元]  (service set identifier) 的縮寫。 此內容是裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的網路名稱。
- **自動連線**：選擇 [啟用]  可讓裝置在位於網路連線範圍內時自動連線到此網路。 選擇 [停用]  可防止裝置自動連線。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。

- **EAP 類型**：選擇用來驗證安全無線連線的可延伸驗證通訊協定 (EAP) 類型。 選項包括：

  - **EAP-FAST**：輸入**受保護的存取認證 (PAC) 設定**。 此選項使用受保護的存取認證，用來建立用戶端與驗證伺服器之間已驗證的通道。 選項包括：
    - **請勿使用 (PAC)**
    - **使用 (PAC)** ：如果現有的 PAC 檔案已存在，請使用它。
    - **使用及佈建 PAC**：建立 PAC 檔案並新增到您的裝置。
    - **使用及匿名佈建 PAC**：建立 PAC 檔案，並在未向伺服器驗證的情況下新增到您的裝置。

  - **EAP-SIM**

  - **EAP-TLS**：另請輸入：

    - **伺服器信任** - **憑證伺服器名稱**：[ 新增]  您信任之憑證授權單位 (CA) 核發的憑證中所使用的一或多個通用名稱。 輸入此資訊時，可以略過連線到此 Wi-Fi 網路時，使用者裝置上顯示的動態信任視窗。
    - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，會向伺服器提供此憑證，並用來驗證連線。

    - **用戶端驗證** - **用戶端驗證的用戶端憑證 (身分識別憑證)** ：選擇 也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

  - **EAP-TTLS**：另請輸入：

    - **伺服器信任** - **憑證伺服器名稱**：[ 新增]  您信任之憑證授權單位 (CA) 核發的憑證中所使用的一或多個通用名稱。 輸入此資訊時，可以略過連線到此 Wi-Fi 網路時，使用者裝置上顯示的動態信任視窗。
    - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，會向伺服器提供此憑證，並用來驗證連線。

    - **用戶端驗證** - 選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。

          選項包括：[未加密的密碼 (PAP)]  、[Challenge Handshake 驗證通訊協定 (CHAP)]  、[Microsoft CHAP (MS-CHAP)]  ，或 [Microsoft CHAP 第 2 版 (MS-CHAP v2)] 

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **LEAP**

  - **PEAP**：另請輸入：

    - **伺服器信任** - **憑證伺服器名稱**：[ 新增]  您信任之憑證授權單位 (CA) 核發的憑證中所使用的一或多個通用名稱。 輸入此資訊時，可以略過連線到此 Wi-Fi 網路時，使用者裝置上顯示的動態信任視窗。
    - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，會向伺服器提供此憑證，並用來驗證連線。

    - **用戶端驗證** - 選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

- **Proxy 設定**：選項包括：
  - **無**：不設定任何 Proxy 設定。
  - **手動**：輸入 **Proxy 伺服器位址**作為 IP 位址，以及其**連接埠號碼**。
  - **自動**：使用檔案設定 Proxy 伺服器。 輸入包含設定檔的 [Proxy 伺服器 URL]  (例如 `http://proxy.contoso.com`)。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接者，請[指派此設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

在 [Android](wi-fi-settings-android.md)、[Android Enterprise](wi-fi-settings-android-enterprise.md)、[iOS/iPadOS](wi-fi-settings-ios.md) 與 [Windows 10](wi-fi-settings-windows.md) 裝置上，設定 Wi-Fi 設定。
