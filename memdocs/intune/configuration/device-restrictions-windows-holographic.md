---
title: Windows Holographic Business 裝置設定 - Microsoft Intune - Azure | Microsoft Docs
description: 閱讀及設定 Microsoft Intune 中適用於 Windows Holographic for Business 的裝置限制設定。 控制取消註冊、地理位置、密碼、從應用程式市集安裝應用程式、Microsoft Edge 中的 Cookie 和快顯、Microsoft Defender、搜尋、雲端與儲存體、藍牙連線能力、系統時間，以及使用情況資料。
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 301cdd9403b0bb3e2d64c8707782ecbc639dc044
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556042"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>使用 Intune 允許或限制功能的 Windows Holographic for Business 裝置設定

這篇文章列出並說明您可以在 Windows Holographic for Business 裝置 (例如 Microsoft Hololens) 上控制的不同設定。 作為行動裝置管理 (MDM) 解決方案的一部分，請使用這些設定來允許或停用功能、控制安全性等。

身為 Intune 系統管理員，您可以建立這些設定並將其指派給您的裝置。

## <a name="before-you-begin"></a>開始之前

[建立 Windows 10 裝置限制組態設定檔](device-restrictions-configure.md#create-the-profile)。

當您建立 Windows 10 裝置限制組態設定檔時，設定會比本文所列的更多。 Windows Holographic for Business 裝置支援本文中的設定。

## <a name="app-store"></a>App Store

- **自動更新來自市集的應用程式**：[封鎖] 會防止自動從 Microsoft Store 安裝更新。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許自動更新從 Microsoft Store 安裝的應用程式。

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate) \(部分機器翻譯\)

- **安裝信任的應用程式**：選擇是否可以安裝非 Microsoft Store 應用程式，也稱為側載。 側載是安裝、然後執行或測試未經 Microsoft Store 認證的應用程式。 例如，僅公司內部使用的應用程式。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **封鎖**：防止側載。 無法安裝非 Microsoft Store 應用程式。
  - **允許**：允許側載。 可以安裝非 Microsoft Store 應用程式。

  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps) \(部分機器翻譯\)

- **開發人員解除鎖定**：允許 Windows 開發人員設定，例如允許使用者修改側載的應用程式。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **封鎖**：防止開發人員模式和側載應用程式。
  - **允許**：允許開發人員模式和側載應用程式。

  [ApplicationManagement/AllowDeveloperUnlock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>行動數據與連線

- **藍牙**：[封鎖] 防止使用者啟用藍牙。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會在裝置上允許藍牙。

  [Connectivity/AllowBluetooth CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **藍牙探索**：[封鎖] 防止其他藍牙啟用的裝置探索此裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許其他具備藍牙功能的裝置 (例如耳機) 探索此裝置。

  [Bluetooth/AllowDiscoverableMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **藍牙通知**：[封鎖] 防止裝置傳送出藍牙通知。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許裝置送出藍牙公告。

  [Bluetooth/AllowAdvertising CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>雲端與儲存體

- **Microsoft 帳戶**：[封鎖] 會防止使用者建立 Microsoft 帳戶與裝置的關聯。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許新增及使用 Microsoft 帳戶。

  [Accounts/AllowMicrosoftAccountConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>控制台和設定

- **修改系統時間**：[封鎖] 會禁止使用者變更裝置的日期和時間設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許使用者變更這些設定。

  [Settings/AllowDateTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>一般

- **手動取消註冊**：[封鎖] 會禁止使用者使用裝置上的工作場所控制台刪除工作場所帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Experience/AllowManualMDMUnenrollment CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **地理位置**：[封鎖] 會禁止使用者開啟裝置的定位服務。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Experience/AllowFindMyDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**：[封鎖] 會停用裝置的 Cortana 語音助理。 Cortana 關閉時，使用者仍可搜尋，在裝置上尋找項目。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許 Cortana。

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge 瀏覽器

- **啟動體驗** > **允許快顯**：[是] (預設) 允許網頁瀏覽器的快顯視窗。 [否] 防止瀏覽器顯示快顯視窗。

  [Browser/AllowPopups CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **我的最愛和搜尋** > **顯示搜尋建議**：[是] (預設) 會允許搜尋引擎在您於網址列鍵入搜尋字詞時建議網站。 [否] 會防止此功能。

  [Browser/AllowSearchSuggestionsinAddressBar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **隱私權與安全性** > **允許密碼管理員**：[是] (預設) 允許 Microsoft Edge 自動使用密碼管理員，讓使用者儲存及管理裝置上的密碼。 [否] 防止 Microsoft Edge 使用密碼管理員。

  [Browser/AllowPasswordManager CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **隱私權與安全性** > **Cookie**：選擇在網頁瀏覽器中處理 Cookie 的方式。 選項包括：
  - **允許**：Cookie 會儲存在裝置上。
  - **封鎖所有 Cookie**：Cookie 不會儲存在裝置上。
  - **只封鎖第三方 Cookie**：協力廠商或合作對象 Cookie 不會儲存在裝置上。

  [Browser/AllowCookies CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **隱私權與安全性** > **傳送「不要追蹤」標頭**：[是] 會向要求追蹤資訊的網站傳送不追蹤標頭 (建議選項)。 [否] (預設) 不會傳送讓網站追蹤使用者的標頭。 使用者可以進行此設定。

  [Browser/AllowDoNotTrack CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **適用於 Microsoft Edge 的 SmartScreen**：[需要] 會開啟 Microsoft Defender SmartScreen，並防止使用者將其關閉。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會開啟 SmartScreen，並允許使用者將其開啟或關閉。

  [Browser/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>密碼

- **密碼**：[需要] 會強制使用者必須輸入密碼，才能存取裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許不用密碼即可存取裝置。 僅適用於本機帳戶。 網域帳戶密碼仍然由 Active Directory (AD) 和 Azure AD 設定。

  [DeviceLock/DevicePasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **裝置從閒置狀態恢復時必須輸入密碼**：[需要] 會強制使用者輸入密碼，才能在裝置閒置後予以解除鎖定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 在閒置後不需要 PIN 或密碼。

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>報告和遙測

- **共用使用方式資料**：選擇提交診斷資料的層級。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者可以選擇要提交的層級。 根據預設，OS 不會共用任何資料。
  - **安全性**：協助提升 Windows 安全性的必要資訊，包括已連線使用者體驗與遙測元件設定、惡意軟體移除工具及 Microsoft Defender 的相關資料
  - **基本**：基本裝置資訊，包括品質相關資料、應用程式相容性、應用程式使用量資料和 [安全性] 層級的資料
  - **增強**：額外的見解，包括 Windows、Windows Server、System Center 和應用程式的使用方式、執行方式、進階的可靠性資料，以及 [基本] 和 [安全性] 層級的資料
  - **完整**：找出及協助修正問題的所有必要資料，加上 [安全性]、[基本] 和 [增強] 層級的資料。

  [System/AllowTelemetry CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>搜尋

- **搜尋位置**：[封鎖] 會禁止 Windows Search 使用位置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許此功能。

  [Search/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
