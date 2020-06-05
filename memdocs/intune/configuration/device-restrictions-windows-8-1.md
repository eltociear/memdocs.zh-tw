---
title: Microsoft Intune 中的 Windows 8.1 裝置限制設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 了解執行 Windows 8.1 的裝置上可用以控制裝置設定與功能的 Intune 設定。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36a74e503f15fe982eeaf1addfed40d0c599cb2c
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556229"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Microsoft Intune Windows 8.1 裝置限制設定

此文章將說明可以針對執行 Windows 8.1 的裝置進行設定的 Microsoft Intune 裝置限制設定。

## <a name="before-you-begin"></a>開始之前

[建立 Windows 8.1 裝置限制組態設定檔](device-restrictions-configure.md#create-the-profile)。

## <a name="general"></a>一般

- **共用使用方式資料**：[封鎖] 可防止裝置將診斷與使用方式遙測資訊提交給 Microsoft。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **防火牆**：[必要] 會開啟 Windows 防火牆。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **使用者帳戶控制**：設定使用者帳戶控制 (UAC)。 選擇在裝置上發生變更時如何通知使用者。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - [一律通知]
  - [在應用程式變更時通知]
  - [在應用程式變更時通知 (但不讓桌面變暗)]
  - [永不通知]

## <a name="password"></a>密碼

- **必要的密碼類型**：選擇此選項以限制使用者必須輸入密碼，才能存取裝置。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **英數字元**：密碼必須混合數字和字母。
  - **數字**：密碼只能是數字。
- **密碼長度下限**：輸入所需的字元數下限，從 6 到 16 個字元。 例如，輸入 `6` 表示密碼長度至少需要六個數字或字元。
- **登入失敗幾次後即抹除裝置**：輸入抹除裝置前允許的密碼錯誤次數，從 1 到 14 個字元。
- **鎖定螢幕前的最大閒置時間 (分鐘)** ：輸入鎖定裝置螢幕前的最大閒置時間，從 1 到 60 分鐘。 例如，輸入 `5 Minutes` 會在閒置 5 分鐘後鎖定裝置。 當設定為 [未設定] 時，Intune 則不會變更或更新此設定。
- **密碼到期 (天數)** ：輸入裝置密碼的有效期限，從 1 到 255 天。 例如，輸入 `90`，密碼會在 90 天後到期。 當此值為空白時，Intune 則不會變更或更新此設定。
- **避免重複使用以前用過的密碼**：輸入不得重複使用的舊密碼，從 1 到 24。 列如，輸入 `5` 讓使用者無法將新密碼設定為其目前密碼或之前使用過的四個密碼之一。 當此值為空白時，Intune 則不會變更或更新此設定。
- **圖片密碼與 PIN**：圖片密碼可讓使用者利用圖片上的手勢登入。 PIN 可讓使用者快速利用 4 位數代碼登入。

  [封鎖] 可防止使用圖片或 PIN 作為密碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

- **加密**：[必要] 會要求裝置必須加密，包括檔案。 並非所有裝置都支援加密。 當設定為 [未設定] 時，Intune 則不會變更或更新此設定。

  若要設定此設定並正確回報合規性，也請設定：

  - **必要的密碼類型**：至少設定為 [數值]。
  - **密碼長度下限**：至少設定為 `6`。

  若要在執行 Windows 8.1 的裝置上強制加密，您必須在每個裝置上安裝 [2014 年 12 月適用於 Windows 的 MDM 用戶端更新](https://support.microsoft.com/kb/3013816) 。

  如果您針對 Windows 8.1 裝置啟用此設定，則裝置的所有使用者必須都具有 Microsoft 帳戶。

  為了讓加密能夠運作，裝置必須符合 [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) 硬體認證需求。

  當您在裝置上強制加密時，就只能從使用者 Microsoft 帳戶存取修復金鑰，該帳戶是從其 OneDrive 帳戶進行存取的。 您無法為使用者修復此金鑰。

## <a name="browser"></a>瀏覽器

- **自動填寫**：[封鎖] 可防止使用者變更瀏覽器中的自動完成設定，以及自動填入表單欄位。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許自動填寫。
- **詐騙警告**：[必要] 會在瀏覽器中顯示潛在詐騙網站的詐騙警告。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **適用於 Microsoft Edge 的 SmartScreen**：[封鎖] 會關閉 Microsoft Defender SmartScreen。 當存取網站和下載檔案時，SmartScreen 會尋找潛在的網路詐騙與惡意軟體。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會開啟 SmartScreen。
- **允許 JavaScript**：[封鎖] 會防止在瀏覽器中執行 JavaScript 等指令碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，作業系統會允許 JavaScript。
- **快顯視窗**：[封鎖] 會開啟快顯封鎖程式，防止網頁瀏覽器中的快顯視窗。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **不要追蹤標頭**：[封鎖] 會防止裝置將「不要追蹤」標頭傳送給要求追蹤資訊的網站。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **外掛程式**：[封鎖] 會防止使用者在 Internet Explorer 中新增外掛程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **內部網路網站中的單一文字輸入**：單一文字輸入可讓使用者僅輸入一個單字，例如 `hr` 或 `benefits`，即可進入內部網路網站。 [封鎖] 會防止此功能。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **自動偵測內部網路網站**：[封鎖] 可防止瀏覽器自動偵測內部網路網站。 內部網路對應規則已封鎖。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **網際網路安全性層級**：設定網際網路網站的安全性層級。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **高**
  - [中高]
  - **中**
- **內部網路安全性層級**：設定內部網路網站的安全性層級。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **低**
  - [中低]
  - **中**
  - [中高]
  - **高**
- **信任網站安全性層級**：設定信任的網站區域的安全性等級。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **低**
  - [中低]
  - **中**
  - [中高]
  - **高**
- **受限網站的高安全性**：設定受限制的網站區域的安全性等級。 [已設定] 會強制對受限網站執行高安全性。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **企業模式功能表存取**：[封鎖] 會防止使用者從 Internet Explorer 存取企業模式功能表選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  當設定為 [未設定] 時，也請輸入：

  - **記錄報告位置 URL**：輸入 URL 位置，以取得顯示已開啟企業模式存取權網站的報告。

- **企業模式網站清單位置 (僅限桌面版)** ：輸入可以企業模式開啟的網站清單位置。

## <a name="cellular"></a>行動電話通訊

- **數據漫遊**：[封鎖] 會防止裝置使用行動電話通訊網路時進行數據漫遊。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="cloud-and-storage"></a>雲端與儲存體

- **工作資料夾 URL**：輸入工作資料夾的 URL，允許跨裝置同步處理文件。 當設定為 [未設定] (預設) 或保留空白時，Intune 則不會變更或更新此設定。
- **在沒有 Microsoft 帳戶的情況下存取 Windows 郵件應用程式**：[封鎖] 則無法在沒有 Microsoft 帳戶的情況下存取 Windows 郵件應用程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="next-steps"></a>後續步驟

在 [Windows 10 和更新版本](device-restrictions-windows-10.md)上建立裝置限制設定檔。
