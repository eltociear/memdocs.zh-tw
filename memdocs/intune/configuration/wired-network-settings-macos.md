---
title: 在 Microsoft Intune 中設定 macOS 裝置的有線網路設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 建立或新增適用於 macOS 裝置的有線網路裝置組態設定檔。 查看不同的設定、新增憑證、選擇 EAP 類型，以及在 Microsoft Intune 中選取驗證方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b11a29cdfd61382e68130479a1ab465bf354c6
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107412"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中新增適用於 macOS 裝置的有線網路設定

您可以建立含有特定有線網路設定的設定檔，然後將此設定檔部署到您的 macOS 裝置。 Microsoft Intune 提供許多功能，包括驗證您的網路、新增 PKCS 或 SCEP 憑證等等。

本文將說明您可以設定的設定。

## <a name="before-you-begin"></a>開始之前

[建立有線網路裝置組態設定檔](wired-networks-configure.md)。

> [!NOTE]
> 這些設定適用於所有註冊類型。 如需註冊類型的詳細資訊，請參閱 [macOS 註冊](../enrollment/macos-enroll.md)。

## <a name="wired-network"></a>有線網路

- **網路介面**：依據服務的優先順序，選取要套用設定檔的裝置網路介面。 選項包括：
  
  - **第一個使用中的乙太網路** (預設)
  - **第二個使用中的乙太網路**
  - **第三個使用中的乙太網路**
  - **第一個乙太網路**
  - **第二個乙太網路**
  - **第三個乙太網路**
  - **任一乙太網路**

  標題中具有「使用中」的選項會使用裝置上正在運作的介面。 若沒有使用中的介面，則使用按服務優先順序設定的下一個介面。 根據預設，會選取 [第一個使用中的乙太網路]，這也是 macOS 所設定的預設設定。

- **EAP 類型**：選取用來驗證安全有線連線的可延伸驗證通訊協定 (EAP) 類型。 選項包括：

  - **EAP-FAST**：輸入 [受保護的存取認證 (PAC) 設定]。 此選項使用受保護的存取認證，用來建立用戶端與驗證伺服器之間已驗證的通道。 選項包括：
    - **請勿使用 (PAC)**
    - **使用 (PAC)** ：如果現有的 PAC 檔案已存在，請使用它。
    - **使用及佈建 PAC**：建立 PAC 檔案並新增至您的裝置。
    - **匿名使用及佈建 PAC**：建立 PAC 檔案，並在未向伺服器驗證之情況下新增至您的裝置。

  - **EAP-TLS**：另請輸入：

    - **伺服器信任** - **憑證伺服器名稱**：**新增**受信任憑證授權單位 (CA) 核發憑證中所使用的一或多個通用名稱。 輸入此資訊時，您可以略過連線到此網路時，使用者裝置上顯示的動態信任視窗。
    - **用於伺服器驗證的根憑證**：選取現有的受信任根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 以此驗證連線。
    - [用戶端驗證] - [憑證]：選取也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。
    - **身分識別隱私權 (外部身分識別)** ：輸入在回應 EAP 身分識別要求時傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **EAP-TTLS**：另請輸入：

    - **伺服器信任** - **憑證伺服器名稱**：**新增**受信任憑證授權單位 (CA) 核發憑證中所使用的一或多個通用名稱。 輸入此資訊時，您可以略過連線到此網路時，使用者裝置上顯示的動態信任視窗。
    - **用於伺服器驗證的根憑證**：選取現有的受信任根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 以此驗證連線。
    - **用戶端驗證**：選取 [驗證方法]。 選項包括：
      - **使用者名稱及密碼**：提示使用者輸入使用者名稱與密碼，以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選取您要驗證連線的方式。 請務必選擇與您網路設定相同的通訊協定。 選項包括：
          - **未加密的密碼 (PAP)**
          - **Challenge Handshake 驗證通訊協定 (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP 第 2 版 (MS-CHAP v2)**
      - **憑證**：選取也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。
      - **身分識別隱私權 (外部身分識別)** ：輸入在回應 EAP 身分識別要求時傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

  - **LEAP**

  - **PEAP**：另請輸入：

    - **伺服器信任** - **憑證伺服器名稱**：**新增**受信任憑證授權單位 (CA) 核發憑證中所使用的一或多個通用名稱。 輸入此資訊時，您可以略過連線到此網路時，使用者裝置上顯示的動態信任視窗。
    - **用於伺服器驗證的根憑證**：選取現有的受信任根憑證設定檔。 當用戶端連線到網路時，系統會向伺服器出示此憑證。 以此驗證連線。
    - **用戶端驗證**：選取 [驗證方法]。 選項包括：
      - **使用者名稱及密碼**：提示使用者輸入使用者名稱與密碼，以驗證連線。
      - **憑證**：選取也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。
      - **身分識別隱私權 (外部身分識別)** ：輸入在回應 EAP 身分識別要求時傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但不一定會執行任何動作。 請務必[指派此設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
