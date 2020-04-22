---
title: 適用於 Android 企業和 Kiosk 裝置的 Wi-Fi 設定 - Microsoft Intune | Microsoft Docs
description: 建立或新增適用於 Android 企業和 Android Kiosk 的 WiFi 裝置組態設定檔。 請查看不同的設定，包括在 Microsoft Intune 中新增憑證、選擇 EAP 類型，以及選取驗證方法。 針對 Kiosk 裝置，也請輸入您網路的預先共用金鑰。
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
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38c3c4adb7029303eaad34b1d5a9fdef774c0f00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086438"
---
# <a name="add-wi-fi-settings-for-android-enterprise-dedicated-and-fully-managed-devices-in-microsoft-intune"></a>在 Microsoft Intune 中針對 Android Enterprise 專用與完全受控裝置新增 Wi-Fi 設定

您可以建立含有特定 WiFi 設定的設定檔，然後將此設定檔部署到您的 Android 企業完全受控與專用裝置。 Microsoft Intune 提供許多功能，包括驗證您的網路、使用預先共用金鑰等等。

本文說明了這些設定。 [在您的裝置上使用 Wi-Fi](wi-fi-settings-configure.md) 包含 Microsoft Intune 中 Wi-Fi 功能的詳細資訊。

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](wi-fi-settings-configure.md)。

## <a name="device-owner-only"></a>僅限裝置擁有者

若要部署到 Android Enterprise 專用或完全受控裝置，請選取此選項。  Android Enterprise 專用與完全受控裝置目前支援 SCEP 憑證部署，但不支援 PKCS。

### <a name="basic"></a>基本

- **Wi-Fi 類型**：選擇 [基本]  。
- **網路名稱**：輸入此 Wi-Fi 連線的名稱。 終端使用者查看其裝置的可用 Wi-FI 連線時，會看到此名稱。 例如，輸入 **Contoso WiFi**。
- **SSID**：輸入 **service set identifier**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。
- **Wi-Fi 類型**：選取向 Wi-Fi 網路驗證時要使用的安全性通訊協定。 選項包括：

  - **開放 (無驗證)** ：只有在網路不安全時才使用此選項。
  - **WEP 預先共用金鑰**：在 [預先共用金鑰]  中輸入密碼。 當您的組織建置或設定網路時，也會設定密碼或網路金鑰。 請輸入此密碼或網路金鑰作為 PSK 值。
  - **WEP 預先共用金鑰**：在 [預先共用金鑰]  中輸入密碼。 當您的組織建置或設定網路時，也會設定密碼或網路金鑰。 請輸入此密碼或網路金鑰作為 PSK 值。

### <a name="enterprise"></a>企業

- **Wi-Fi 類型**：選擇 [企業]  。
- **SSID**：輸入 **service set identifier**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。
- **EAP 類型**：選擇用來驗證安全無線連線的可延伸驗證通訊協定 (EAP) 類型。 選項包括：

  - **EAP-TLS**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證，並用來驗證連線。

    - **用戶端驗證** - **用戶端驗證的用戶端憑證 (身分識別憑證)** ：選擇也會部署到裝置的 SCEP 或用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

    - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **EAP-TTLS**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證，並用來驗證連線。

    - **用戶端驗證**：選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **未加密的密碼 (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **PEAP**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證，並用來驗證連線。

    - **用戶端驗證**：選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 驗證方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **無**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

## <a name="work-profile-only"></a>僅限工作設定檔

### <a name="basic"></a>基本

- **Wi-Fi 類型**：選擇 [基本]  。
- **SSID**：輸入 **service set identifier**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。

### <a name="enterprise"></a>企業

- **Wi-Fi 類型**：選擇 [企業]  。
- **SSID**：輸入 **service set identifier**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。
- **EAP 類型**：選擇用來驗證安全無線連線的可延伸驗證通訊協定 (EAP) 類型。 選項包括：

  - **EAP-TLS**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證，並用來驗證連線。

    - **用戶端驗證** - **用戶端驗證的用戶端憑證 (身分識別憑證)** ：選擇 也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

    - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **EAP-TTLS**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證，並用來驗證連線。

    - **用戶端驗證**：選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **未加密的密碼 (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **PEAP**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證，並用來驗證連線。

    - **用戶端驗證**：選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 驗證方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **無**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

- **Proxy 設定**：指定組織所使用的 Proxy 設定。 選項包括：

  - **無** - 您不使用 Proxy 伺服器。
  - **自動** - 選取此選項來使 [Proxy 伺服器 URL]  設定可用；您會使用此設定來指定 Proxy 伺服器，或是包含您 Proxy 伺服器清單的 Proxy 自動設定 (PAC) 檔案。

- **Proxy 伺服器 URL**：此設定會在您將 [Proxy 設定]  設定為 [自動]  時可供使用。 指定下列其中一個選項來將裝置導向到您的 Proxy 伺服器：

  - IP 位址。 例如， `10.0.0.11`
  - URL。 例如 `http://proxyserver.contoso.com`。
  - Proxy 自動設定 (PAC) 檔案的 URL。 例如：`http://proxy.contoso.com/proxy.pac`。

  如需 PAC 檔案的詳細資訊，請參閱 [Proxy 自動設定 (PAC) 檔案](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) \(英文\) (會開啟非 Microsoft 網站)。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接者，請[指派此設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以為 [Android](wi-fi-settings-android.md)、[iOS/iPadOS](wi-fi-settings-ios.md)、[macOS](wi-fi-settings-macos.md)、[Windows 10](wi-fi-settings-windows.md) 與 [Windows 8.1](wi-fi-settings-import-windows-8-1.md) 裝置建立 Wi-Fi 設定檔。
