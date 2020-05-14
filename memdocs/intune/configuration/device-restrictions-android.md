---
title: Microsoft Intune 中 Android 的裝置限制設定 | Microsoft Docs
description: 查看可在 Microsoft Intune 中控制及限制的所有 Android 裝置系統管理員設定清單。 使用這些設定來控制密碼、存取 Google Play、允許或禁止應用程式、控制瀏覽器設定、封鎖應用程式、備份至 Google 雲端，以及控制訊息、語音、數據漫遊、Wi-Fi 及藍牙連線選項。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5fc11d7302c30dd53314eb2312d37842b081a6b3
ms.sourcegitcommit: 5f9d5d22114ae5aeb0270c7fb59c5dced5f48826
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82862355"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Intune 中的 Android 與 Samsung Knox Standard 裝置限制設定

本文將告訴您所有的 Microsoft Intune 裝置限制設定，讓您可以為執行 Android 的裝置進行設定。

>[!TIP]
>如果沒有您想要的設定，您可以使用[自訂設定檔](custom-settings-android.md)來設定裝置。

## <a name="before-you-begin"></a>開始之前

[建立裝置組態設定檔](device-restrictions-configure.md)。

## <a name="general"></a>一般

- **相機**：[封鎖]  會防止存取裝置相機。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許存取裝置相機。

  Intune 只管理裝置相機的存取權。 無權存取圖片或影片。

- **複製並貼上 (僅限 Samsung Knox)** ：[封鎖]  可防止複製並貼上。 [未設定]  允許使用裝置的複製和貼上功能。
- **應用程式之間的剪貼簿共用 (僅限 Samsung Knox)** ：[封鎖]  可防止使用剪貼簿在應用程式間複製並貼上。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許裝置的複製和貼上功能。
- **診斷資料提交 (僅限 Samsung Knox)** ：[封鎖]  會阻止使用者從裝置提交 Bug 報表。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用者提交資料。
- **抹除 (僅限 Samsung Knox)** ：允許使用者在裝置上執行[抹除](../remote-actions/devices-wipe.md)動作。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。
- **地理位置 (僅限 Samsung Knox)** ：[封鎖]  會停用裝置，使其無法使用位置資訊。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許裝置使用位置資訊。
- **關閉電源 (僅限 Samsung Knox)** ：[封鎖]  可防止使用者關閉裝置電源。 也會防止設定 [登入失敗幾次後即抹除裝置]  設定，使其無法運作。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用者關閉裝置電源。
- **螢幕擷取 (僅限 Samsung Knox)** ：[封鎖]  可防止擷取螢幕畫面。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會讓使用者擷取螢幕內容為影像。
- **語音助理 (僅限 Samsung Knox)** ：[封鎖]  會停用 S 語音服務。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許在裝置上使用 S 語音服務和應用程式。 此設定不適用於 Bixby 或用於大聲讀取螢幕內容的語音助理。
- **YouTube (僅限 Samsung Knox)** ：[封鎖]  可防止使用者使用 YouTube 應用程式。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許在裝置上使用 YouTube 應用程式。
- **允許共用裝置 (僅限 Samsung Knox)** ：將受控 Samsung Knox Standard 裝置設定為共用。 [允許]  可讓使用者使用 Azure AD 認證登入和登出裝置。 無論裝置是否在使用中，都受到管理。

  搭配 SCEP 憑證設定檔使用時，此功能可讓使用者和所有擁有相同應用程式的使用者共用裝置。 但是，每個使用者都有自己的 SCEP 使用者憑證。 當使用者登出時，會清除所有應用程式資料。 此功能僅限於 LOB 應用程式。

  當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可避免多位使用者使用 Azure AD 認證在裝置上登入公司入口網站應用程式。
- **封鎖日期和時間的變更 (Samsung Knox)** ：[封鎖]  可防止使用者變更裝置的日期和時間設定。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用者變更日期和時間設定。

## <a name="password"></a>密碼

- **密碼**：[需要]  會要求使用者必須輸入密碼，才能存取裝置。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用者不用輸入密碼即可存取裝置。

    > [!NOTE]
    > Samsung Knox 裝置在 MDM 註冊期間會自動要求 4 位數的 PIN。 原生 Android 裝置可能會自動要求 PIN，以符合條件式存取。

- **密碼長度下限**：輸入 4-16 個所需的最少數字或字元。 例如，輸入 `6` 表示密碼長度至少需要六個數字或字元。
- **停止活動最多幾分鐘後鎖定螢幕**：輸入裝置必須閒置多久，螢幕才會自動鎖定。 例如，輸入 `5` 會在閒置 5 分鐘後鎖定裝置。 當值為空白或設定為 [未設定]  時，Intune 不會變更或更新此設定。

  在裝置上，使用者無法在設定檔中設定大於已設定時間的時間值。 使用者可以設定較低的時間值。 例如，如果設定檔設定為 `15` 分鐘，則使用者可以將值設定為 5 分鐘。 使用者無法將值設定為 30 分鐘。

- **登入失敗幾次後即抹除裝置**：輸入抹除裝置的密碼錯誤次數：4-11。 `0` (零) 可停用裝置抹除功能。 當此值為空白時，Intune 不會變更或更新此設定。
- **密碼到期 (天數)** ：輸入裝置密碼必須在多少天後變更，介於 1-365 之間。 例如，輸入 `90`，密碼會在 90 天後到期。 密碼到期時，系統會提示使用者建立新的密碼。 當此值為空白時，Intune 不會變更或更新此設定。
- **必要的密碼類型**：輸入所需的密碼複雜性等級，以及是否可以使用生物識別裝置。 選項包括：
  - **裝置預設**
  - **低安全性生物識別**：[比較強式與弱式生物特徵辨識](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) \(英文\) (開啟 Android 的網站)
  - **至少包含數字**：包含數值字元，例如 `123456789`。
  - **複雜數字**：不允許重複或連續的數字，例如 "1111" 或 "1234"。 在將此設定指派給裝置之前，請務必將這些裝置上的公司入口網站應用程式更新至最新版本。

    當設定為 [複數]  ，並將此設定指派給執行 Android 5.0 版以前的裝置時，就會套用下列行為：

    - 如果公司入口網站應用程式執行的版本早於 1704，就不會將任何 PIN 原則套用至裝置，且會在 Microsoft 端點管理員系統管理中心中顯示錯誤。
    - 如果公司入口網站應用程式執行 1704 版或更新版本，則只能套用簡單的 PIN。 Android 5.0 版之前的版本不支援此設定。 Microsoft 端點管理員系統管理中心未顯示任何錯誤。

  - **至少包含字母**：包含字母表中的字母。 數字和符號不是必要項目。
  - **至少包含英數字元**：包含大寫字母、小寫字母及數字字元。
  - **至少包含英數字元和符號**：包含大寫字母、小寫字母、數字字元、標點符號及符號。

- **避免重複使用以前用過的密碼**：使用此設定限制使用者建立以前用過的密碼。 輸入不得重複使用的舊密碼，從 1 到 24。 列如，輸入 `5` 讓使用者無法將新密碼設定為其目前密碼或之前使用過的四個密碼之一。 當此值為空白時，Intune 不會變更或更新此設定。
- **指紋解除鎖定 (僅限 Samsung Knox)** ：[封鎖]  可防止使用指紋解鎖裝置。 當設定為 [未設定]  (預設值) 時，Intune 不會變更或更新此設定。根據預設，OS 會允許使用者使用指紋解鎖裝置。
- **Smart Lock 與其他信任代理程式**：[封鎖]  可防止 Smart Lock 或其他信任代理程式調整鎖定畫面設定。 此功能 (也稱為信任代理程式) 可供在裝置位於受信任的位置時，停用或略過裝置鎖定畫面密碼。 例如，當裝置連線到特定的藍牙裝置或靠近 NFC 標記時，就能使用此功能。 您可以使用此設定來防止使用者設定 Smart Lock。

  當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。

  這項設定適用於：

  - Samsung KNOX Standard 5.0+

- **加密**：選擇 [需要]  以加密裝置上的檔案。 並非所有裝置都支援加密。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 若要設定此設定並正確報告合規性，也請設定：
  1. **密碼**：設定為 [需要]  。
  2. **必要的密碼類型**：設定為 [至少包含數字]  。
  3. **密碼長度下限**：至少設定為 `4`。

  > [!NOTE]
  > 如果實施加密原則，Samsung Knox 裝置會要求使用者設定一個六個字元的複雜密碼來作為裝置密碼。

## <a name="google-play-store"></a>Google Play 商店

- **Google Play 商店 (僅限 Samsung Knox)** ：[封鎖]  可防止使用者使用 Google Play 商店。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用者存取裝置上的 Google Play 商店。

## <a name="restricted-apps"></a>受限應用程式

使用這些設定來允許或防止在裝置上使用特定的應用程式。 Android 和 Samsung Knox Standard 裝置支援此功能。

- **未設定** (預設值)：Intune 不會變更或更新此設定。
- **禁止的應用程式**：列出不允許使用者安裝與執行的應用程式 (不受 Intune 管理)。 如果使用者安裝此清單中的應用程式，則 Intune 會通知您。
- **核准的應用程式**：列出允許使用者安裝的應用程式。 若要持續符合規範，使用者絕不能安裝其他應用程式。  自動允許受 Intune 管理的應用程式，包括公司入口網站應用程式。
- **應用程式清單**：**新增**您的應用程式：
  - **應用程式套件組合識別碼**：輸入應用程式的配套識別碼。
  - **App Store URL**：輸入所要應用程式的 Google Play 商店 URL。 例如，如果您想要新增適用於 Android 的 Microsoft 遠端桌面應用程式，請輸入 `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`。

    若要尋找應用程式的 URL，請開啟 [Google Play 商店](https://play.google.com/store/apps)，然後搜尋該應用程式。 例如，搜尋 `Microsoft Remote Desktop Play Store` 或 `Microsoft Planner`。 選取應用程式，並複製 URL。
  
  - **應用程式名稱**：輸入所要的名稱。 這是向使用者顯示的名稱。
  - **發行者** (選擇性)：輸入應用程式的發行者，例如 `Microsoft`。

您也可以 [匯入]  具有應用程式詳細資料 (包括 URL) 的 CSV 檔案。 使用 <*app url*>、<*app name*>、<*app publisher*> 格式。 或者，以相同格式**匯出**包含受限應用程式清單的現有清單。

> [!IMPORTANT]
> 使用受限應用程式設定的裝置設定檔，必須指派給使用者群組，而非裝置群組。

## <a name="browser"></a>瀏覽器

- **網頁瀏覽器 (僅限 Samsung Knox)** ：[封鎖]  可防止在裝置上使用預設網頁瀏覽器。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用裝置的預設網頁瀏覽器。
- **自動填入 (僅限 Samsung Knox)** ：[封鎖]  可防止瀏覽器自動填入文字。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許自動填寫。
- **Cookie (僅限 Samsung Knox)** ：選擇如何處理裝置上的網站 Cookie。 選項包括：
  - 允許
  - 封鎖所有 Cookie
  - 允許來自瀏覽網站的 Cookie
  - 允許來自目前網站的 Cookie
- **JavaScript (僅限 Samsung Knox)** ：[封鎖]  可防止在瀏覽器中執行 JavaScript。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許這些指令碼。
- **快顯 (僅限 Samsung Knox)** ：[封鎖]  會開啟快顯封鎖程式，防止網頁瀏覽器中的快顯視窗。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許快顯。

## <a name="allow-or-block-apps"></a>允許或封鎖應用程式

使用這些設定在 Samsung Knox Standard 裝置上允許、封鎖或隱藏特定應用程式。 使用者無法開啟或執行隱藏的應用程式。

選項包括：

- **允許安裝的應用程式 (僅限 Samsung Knox Standard)** ：新增使用者可以安裝的應用程式。 使用者無法安裝不在清單上的應用程式。
- **禁止啟動的應用程式 (僅限 Samsung Knox Standard)** ：輸入使用者不得在裝置上執行的應用程式。
- **對使用者隱藏的應用程式 (僅限 Samsung Knox Standard)** ：輸入裝置上隱藏的應用程式。 使用者無法探索或執行這些應用程式。

請為每項設定新增應用程式：

- **依套件名稱新增應用程式**：輸入應用程式名稱，以及應用程式套件的名稱。 主要用於企業營運應用程式。 
- **依 URL 新增應用程式**：輸入應用程式名稱，以及其在 Google Play 商店中的 URL。
- **新增市集應用程式**：從您在 Intune 中管理的應用程式清單中選取一個應用程式。

## <a name="cloud-and-storage"></a>雲端與儲存體

- **Google 備份 (僅限 Samsung Knox)** ：[封鎖]  可防止裝置同步至 Google 備份。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用 Google 備份。
- **Google 帳戶自動同步 (僅限 Samsung Knox)** ：[封鎖]  可防止裝置上的 Google 帳戶自動同步功能。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 允許自動同步 Google 帳戶設定。
- **抽取式存放裝置 (僅限 Samsung Knox)** ：[封鎖]  可防止裝置使用卸除式存放裝置。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許裝置使用卸除式存放裝置，例如 SD 記憶卡。
- **加密儲存卡上的內容 (僅限 Samsung Knox)** ：[需要]  能強制執行儲存卡上的加密。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用未加密的儲存卡。 並非所有裝置都支援儲存卡加密。 若要確認，請與裝置製造商聯繫。

## <a name="cellular-and-connectivity"></a>行動數據與連線

- **數據漫遊 (僅限 Samsung Knox)** ：[封鎖]  會防止在行動電話通訊網路上進行數據漫遊。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許資料漫遊。
- **SMS/MMS 傳訊 (僅限 Samsung Knox)** ：[封鎖]  可防止裝置上的簡訊。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用簡訊和多媒體簡訊。
- **語音撥號 (僅限 Samsung Knox)** ：[封鎖]  可防止使用者在裝置上使用語音撥號功能。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許語音撥號。
- **語音漫遊 (僅限 Samsung Knox)** ：[封鎖]  會防止透過行動電話通訊網路進行語音漫遊。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許語音漫遊。
- **藍牙 (僅限 Samsung Knox)** ：[封鎖]  可防止在裝置上使用藍牙。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用藍牙。
- **NFC (僅限 Samsung Knox)** ：[封鎖]  會在支援近距離無線通訊 (NFC) 的裝置上停用使用此作業。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許 NFC 作業。
- **Wi-Fi (僅限 Samsung Knox)** ：[封鎖]  可防止在裝置上使用 Wi-Fi。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用 Wi-Fi。
- **Wi-Fi 共享 (僅限 Samsung Knox)** ：[封鎖]  可防止在裝置上使用 Wi-Fi 網際網路共用功能。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用 Wi-Fi 網際網路共用功能。

## <a name="kiosk"></a>Kiosk

Kiosk 設定僅套用至 Samsung Knox Standard 裝置，且只套用至您使用 Intune 管理的應用程式。

- 新增您想要在裝置處於 kiosk 模式時執行的應用程式。 在 kiosk 模式中，只會執行您新增的應用程式；未新增的應用程式無法執行。 當裝置處於 kiosk 模式時，預先安裝的瀏覽器不會作為應用程式執行。 如果瀏覽器為必要項目，請考慮使用[受控瀏覽器](../apps/app-configuration-managed-browser.md)。

  您的應用程式選項：

  - **依套件名稱新增應用程式**：主要用於企業營運應用程式。 輸入應用程式名稱，以及應用程式套件的名稱。
  - **依 URL 新增應用程式**：輸入應用程式名稱，以及其在 Google Play 商店中的 URL。
  - **新增市集應用程式**：從您在 Intune 中管理的應用程式清單中選取一個應用程式。

- **螢幕睡眠按鈕**：[封鎖]  可防止或隱藏螢幕睡眠按鈕。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許裝置上的螢幕睡眠及喚醒按鈕。
- **音量按鈕**：[封鎖]  可防止使用者藉由停用音量按鈕調整音量。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許在裝置上使用音量按鈕。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以為 [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) 和 [Windows 10](kiosk-settings.md) 裝置建立 kiosk 設定檔。
