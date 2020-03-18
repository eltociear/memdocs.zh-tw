---
title: 在 Microsoft Intune 中設定 Android 裝置的 Wi-Fi 設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 建立或新增適用於 Android 的 WiFi 裝置組態設定檔。 請查看不同的設定，包括在 Microsoft Intune 中新增憑證、選擇 EAP 類型，以及選取驗證方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46188be8ed347e488a89dc5f6f4e10390aa821bc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79363846"
---
# <a name="add-wi-fi-settings-for-devices-running-android-in-microsoft-intune"></a>在 Microsoft Intune 中為執行 Android 的裝置設定新增 Wi-Fi 設定

您可以建立含有特定 WiFi 設定的設定檔，然後將此設定檔部署到您的 Android 裝置。 Microsoft Intune 提供許多功能，包括驗證您的網路、新增 PKS 或 SCEP 憑證等等。

這些 Wi-Fi 設定分為兩種類別：基本設定和企業層級設定。

本文說明了這些設定。

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](device-profile-create.md)。

## <a name="basic"></a>基本

- **Wi-Fi 類型**：選擇 [基本]  。
- **SSID**：輸入**服務組識別元**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。

## <a name="enterprise"></a>企業

- **Wi-Fi 類型**：選擇 [企業]  。
- **SSID**：輸入**服務組識別元**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。
- **EAP 類型**：選擇用來驗證安全無線連線的可延伸的驗證通訊協定 (EAP) 類型。 選項包括：

  - **EAP-TLS**：另請輸入：

    - **伺服器信任** - **用於伺服器驗證的根憑證**：選擇現有之受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 其會驗證連線。

    - **用戶端驗證** - **進行用戶端驗證的用戶端憑證 (身分識別憑證)** ：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

    - **身分識別隱私權 (外部身分識別)** ：輸入在回應 EAP 身分識別要求時傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **EAP-TTLS**：另請輸入：

    - **伺服器信任** - **用於伺服器驗證的根憑證**：選擇現有之受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 其會驗證連線。

    - **用戶端驗證**：選擇一個 [驗證方法]  。 選項包括：

      - **使用者名稱及密碼**：提示使用者輸入使用者名稱及密碼，以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選擇您要驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **未加密的密碼 (PAP)**
          - **Challenge Handshake 驗證通訊協定 (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **身分識別隱私權 (外部身分識別)** ：輸入在回應 EAP 身分識別要求時傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **PEAP**：另請輸入：

    - **伺服器信任** - **用於伺服器驗證的根憑證**：選擇現有之受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 其會驗證連線。

    - **用戶端驗證**：選擇一個 [驗證方法]  。 選項包括：

      - **使用者名稱及密碼**：提示使用者輸入使用者名稱及密碼，以驗證連線。 另請輸入：
        - **進行驗證的非 EAP 方法 (內部識別)** ：選擇您要驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **無**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **身分識別隱私權 (外部身分識別)** ：輸入在回應 EAP 身分識別要求時傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接下來，請[指派此設定檔](device-profile-assign.md)。

## <a name="more-resources"></a>其他資源

- [Wi-Fi 設定概觀](wi-fi-settings-configure.md)，包括其他平台。

- 使用 Android 企業或 Android Kiosk 裝置嗎？ 如果是，請參閱[適用於執行 Android 企業的裝置和專用裝置的 Wi-Fi 設定](wi-fi-settings-android-enterprise.md)。
