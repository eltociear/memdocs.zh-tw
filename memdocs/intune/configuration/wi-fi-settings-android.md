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
ms.openlocfilehash: 2ca465bf8356a16f9716d45456f9675384ffb518
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086410"
---
# <a name="add-wi-fi-settings-for-devices-running-android-in-microsoft-intune"></a>在 Microsoft Intune 中為執行 Android 的裝置設定新增 Wi-Fi 設定

您可以建立含有特定 WiFi 設定的設定檔，然後將此設定檔部署到您的 Android 裝置。 Microsoft Intune 提供許多功能，包括驗證您的網路、新增 PKS 或 SCEP 憑證等等。

這些 Wi-Fi 設定分為兩種類別：基本設定和企業層級設定。

本文說明了這些設定。

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](wi-fi-settings-configure.md)。

## <a name="basic"></a>基本

- **Wi-Fi 類型**：選擇 [基本]  。
- **SSID**：輸入 **service set identifier**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。

## <a name="enterprise"></a>企業

- **Wi-Fi 類型**：選擇 [企業]  。
- **SSID**：輸入 **service set identifier**，其為裝置要連線之無線網路的實際名稱。 但當使用者選擇此連線時，只會看到您設定的 [網路名稱]  。
- **隱藏的網路**：選擇 [啟用]  可在裝置的可用網路清單中隱藏此網路。 不會廣播 SSID。 選擇 [停用]  可在裝置的可用網路清單中顯示此網路。
- **EAP 類型**：選擇用來驗證安全無線連線的可延伸驗證通訊協定 (EAP) 類型。 選項包括：

  - **EAP-TLS**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 其會驗證連線。

    - **用戶端驗證** - **用戶端驗證的用戶端憑證 (身分識別憑證)** ：選擇 也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

    - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **EAP-TTLS**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 其會驗證連線。

    - **用戶端驗證**：選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **未加密的密碼 (PAP)**
          - **Challenge Handshake 驗證通訊協定 (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **PEAP**：另請輸入：

    - **伺服器信任** - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 其會驗證連線。

    - **用戶端驗證**：選擇 [驗證方法]  。 選項包括：

      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 驗證方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。 選項包括：

          - **無**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**

      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。

      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接下來，請[指派此設定檔](device-profile-assign.md)。

## <a name="more-resources"></a>其他資源

- [Wi-Fi 設定概觀](wi-fi-settings-configure.md)，包括其他平台。

- 使用 Android 企業或 Android Kiosk 裝置嗎？ 如果是，請參閱[適用於執行 Android 企業的裝置和專用裝置的 Wi-Fi 設定](wi-fi-settings-android-enterprise.md)。
