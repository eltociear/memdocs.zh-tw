---
title: 開始使用 Microsoft Intune App SDK
description: 使用 Microsoft Intune 快速為行動應用程式啟用行動應用程式管理 (MAM)。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 38ebd3f5-cfcc-4204-8a75-6e2f162cd7c1
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6427c2bf77255399813edd62519fd365c3cb2a68
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84166088"
---
# <a name="get-started-with-the-microsoft-intune-app-sdk"></a>開始使用 Microsoft Intune App SDK

本指南可協助您使用 Microsoft Intune 快速啟用行動應用程式，以支援應用程式保護原則。 若能先了解 [Intune App SDK 概觀](app-sdk.md)中說明的 Intune App SDK 優點，可能會對您很有幫助。

Intune App SDK 支援跨 iOS 和 Android 的類似案例，而且能為 IT 系統管理員建立跨平台的一致體驗。 但是，由於平台差異和限制，因此針對特定功能的支援有些微差異。

## <a name="register-your-store-app-with-microsoft"></a>向 Microsoft 註冊您的市集應用程式

### <a name="if-your-app-is-internal-to-your-organization-and-will-not-be-publicly-available"></a>如果應用程式是無法公開的組織內部應用程式：

您**不需要**  註冊應用程式。 針對由您公司或為了您公司撰寫的內部[企業營運 (LOB) 應用程式](../apps/apps-add.md#app-types-in-microsoft-intune)，IT 管理員將會在內部部署應用程式。 Intune 可偵測是否已使用 SDK 建置應用程式，並允許 IT 系統管理員對其套用應用程式保護原則。 您可以跳到[啟用 iOS 或 Android 應用程式的應用程式保護原則](#enable-your-ios-or-android-app-for-app-protection-policy)這一節。

### <a name="if-your-app-will-be-released-to-a-public-app-store-like-the-apple-app-store-or-google-play"></a>如果您的應用程式將會發行到公開應用程式商店 (例如 Apple App Store 或 Google Play)：

您 _**必須**_ 先向 Microsoft Intune 註冊應用程式，並同意註冊條款。 然後 IT 系統管理員就可以將應用程式保護原則套用至受控應用程式，該應用程式將會列為 [Intune 受保護的合作夥伴應用程式](../apps/apps-supported-intune-apps.md#partner-apps)。

等到註冊已完成且 Microsoft Intune 小組確認之後，Intune 系統管理員就不會有將應用程式保護原則套用至應用程式深層連結的選項。 Microsoft 也會將您的應用程式加到其 [Microsoft Intune Partner 頁面](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)。 應用程式的圖示將會在那裡顯示，以表示該應用程式支援 Intune 應用程式保護原則。

### <a name="the-registration-process"></a>註冊程序
若要開始註冊程序，且如果您尚未使用 Microsoft 連絡人，請填寫 [Microsoft Intune App Partner Questionnaire](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR80SNPjnVA1KsGiZ89UxSdVUMEpZNUFEUzdENENOVEdRMjM5UEpWWjJFVi4u) (Microsoft Intune 應用程式合作夥伴問卷)。

我們將會使用問卷回應中列出的電子郵件地址與您連絡，並繼續註冊程序。 此外，如果有任何疑慮，我們也會使用您註冊的電子郵件地址與您連絡。

> [!NOTE]
> 問卷中及透過與 Microsoft Intune 小組的電子郵件通訊收集的所有資訊，皆會遵循 [Microsoft 隱私權聲明](https://www.microsoft.com/privacystatement/default.aspx)中的規定來處理。

**註冊程序的相關作業**：

1. 提交問卷之後，我們將會透過您註冊的電子郵件地址與您連絡，以確認我們成功收到郵件或要求其他資訊以完成註冊。

2. 在收齊您的所有必要資訊之後，我們即會傳送 Microsoft Intune 應用程式夥伴協議給您簽署。 本協議會說明相關條款，您的公司必須先接受這些條款，才能成為 Microsoft Intune 應用程式合作夥伴。

3. 當您的應用程式成功註冊 Microsoft Intune 服務，以及當 [Microsoft Intune 合作夥伴](https://www.microsoft.com/cloud-platform/microsoft-intune-apps)網站上將您的應用程式顯示為精選應用程式時，皆可獲得通知。

4. 最後，您應用程式的深層連結就會包含在下一次的每月 Intune 服務更新中。 例如，如果在 7 月完成註冊資訊，將於 8 月中支援深層連結。

深層連結是應用程式列於公用 App Store 中的連結。 如果未來您應用程式的深層連結有所變更，您將必須重新註冊應用程式。

> [!NOTE]
> 如果您使用了新版 Intune App SDK 更新您的應用程式，必須通知我們。

## <a name="download-the-sdk-files"></a>下載 SDK 檔案

適用於原生 iOS 和 Android 的 Intune App SDK 會裝載在 Microsoft GitHub 帳戶上。 這些公用存放庫具備分別適用於原生 iOS 和 Android 的 SDK 檔案︰

* [iOS 版 Intune App SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios)
* [Android 版 Intune App SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-android)

如果您的應用程式是 Xamarin 應用程式，請使用這項 SDK 變體：

* [Intune App SDK Xamarin 繫結](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)

建議您註冊一個 GitHub 帳戶，以用來從我們的存放庫執行分支作業及提取作業。 GitHub 可讓開發人員與我們的產品小組進行溝通、開啟問題並接收快速回應、檢視版本資訊，以及將意見提供給 Microsoft。 如有 Intune App SDK GitHub 問題，請連絡 msintuneappsdk@microsoft.com。

## <a name="enable-your-ios-or-android-app-for-app-protection-policy"></a>啟用 iOS 或 Android 應用程式的應用程式保護原則

您需要下列其中一個開發人員指南，協助您將 Intune App SDK 整合到應用程式：

* **[Intune App SDK for iOS 開發人員指南](app-sdk-ios.md)** ：此文件將逐步引導您使用 Intune App SDK 來啟用原生 iOS 應用程式。

* **[Intune App SDK for Android 開發人員指南](app-sdk-android.md)** ：此文件將逐步引導您使用 Intune App SDK 來啟用原生 Android 應用程式。

* **[Intune App SDK Xamarin 繫結指南](app-sdk-xamarin.md)** ：此文件將協助您使用 Xamarin for Intune 應用程式保護原則來建置 iOS 與 Android 應用程式。



## <a name="enable-your-ios-or-android-app-for-app-based-conditional-access"></a>為 iOS 或 Android 應用程式啟用以應用程式為基礎的條件式存取

除了為您的應用程式啟用應用程式保護原則之外，您的應用程式也需要符合下列條件才能適當地搭配 Azure ActiveDirectory (AAD) 應用程式型條件式存取運作：

* 應用程式是使用 [Azure Active Directory 驗證程式庫](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-libraries)所建置並針對 AAD 訊息代理程式驗證啟用。

* 您應用程式的 [AAD 用戶端識別碼](https://docs.microsoft.com/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#configure-a-native-client-application)在 iOS 與 Android 平台上都必須是唯一的。

## <a name="configure-telemetry-for-your-app"></a>設定應用程式的遙測

Microsoft Intune 會收集應用程式使用量統計資料的資料。

* **iOS 版 Intune App SDK**：此 SDK 預設會記錄使用事件的相關 SDK 遙測資料。 這些資料會傳送到 Microsoft Intune。

  * 如果您選擇不要將 SDK 遙測資料從應用程式傳送至 Microsoft Intune，則必須停用遙測傳輸，方法是在 IntuneMAMSettings 字典中將 `MAMTelemetryDisabled` 屬性設定為 "YES"。

* **Android 版 Intune App SDK**：Intune App SDK for Android 不會控制來自您應用程式的資料收集。 公司入口網站應用程式預設會記錄遙測資料。 這些資料會傳送到 Microsoft Intune。 根據 Microsoft 原則，我們不會收集任何個人識別資訊 (PII)。 

  * 如果終端使用者選擇不要傳送此資料，則必須在公司入口網站應用程式的 [設定] 下關閉遙測。 若要深入了解，請參閱[關閉 Microsoft 使用狀況資料收集](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android)。 

## <a name="line-of-business-app-version-numbers"></a>企業營運應用程式版本號碼

Intune 的企業營運應用程式現在會顯示 iOS 和 Android 應用程式的版本號碼。 此號碼會顯示在 Azure 入口網站的應用程式清單及 [應用程式概觀] 刀鋒視窗中。 使用者可以在公司入口網站應用程式及入口網站中看到應用程式號碼。

### <a name="full-version-number"></a>完整的版本號碼

完整的版本號碼可識別特定的應用程式版本。 此號碼會顯示為_版本_(_組建_)。 例如 2.2(2.2.17560800)。 

完整的版本號碼有兩個部分：

- **版本**  
  版本號碼是人類可讀的應用程式版本號碼。 可供使用者識別不同的應用程式版本。

- **組建編號**  
  組建編號是內部編號，用於偵測應用程式與以程式設計方式管理應用程式。 組建編號是指參考程式碼變更的應用程式反覆項目。

### <a name="version-and-build-number-in-android-and-ios"></a>Android 和 iOS 中的版本與組建編號

Android 和 iOS 會在應用程式參考中同時使用版本和組建編號。 不過，這兩個作業系統都有作業系統特定的意義。 下表說明這些詞彙的關係。

在開發用於 Intune 的企業營運應用程式時，請記得同時使用版本和組建編號。 Intune 應用程式管理功能仰賴於有意義的 **CFBundleVersion** (適用於 iOS) 和 **PackageVersionCode** (適用於 Android)。 這些數字會包含在應用程式資訊清單中。 

Intune|iOS|Android|說明|
|---|---|---|---|
版本號碼|CFBundleShortVersionString|PackageVersionName |這個數字表示使用者的特定應用程式版本。|
組建編號|CFBundleVersion|PackageVersionCode |這個數字用來表示應用程式程式碼中的反覆項目。|

#### <a name="ios"></a>iOS

- **CFBundleShortVersionString**  
  指定配套的版本號碼。 此數字可識別應用程式的發行版本。 此數字可供使用者用來參考應用程式。
- **CFBundleVersion**  
  配套的組建版本，可識別配套的反覆項目。 此數字可識別發行或未發行的配套。 此數字用於偵測應用程式。

#### <a name="android"></a>Android

- **PackageVersionName**  
  向使用者顯示的版本號碼。 這個屬性可以設定為原始字串或字串資源的參考。 此字串除了顯示給使用者之外，沒有任何其他的用途。
- **PackageVersionCode**  
  內部版本號碼。 此數字只能用來判斷某個版本是否比另一個版本更新，較高的數字表示較新的版本。 這不是版本 

## <a name="next-steps-after-integration"></a>整合後的後續步驟

### <a name="test-your-app"></a>測試應用程式
在您完成整合 iOS 或 Android 應用程式與 Intune App SDK 的必要步驟之後，需要確定使用者和 IT 系統管理員的所有應用程式保護原則皆已啟用且正常運作。若要測試整合式應用程式，您需要下列項目：

* **Microsoft Intune 測試帳戶**：若要對 Intune 受控應用程式測試 Intune 應用程式保護功能，您將需要一個 Microsoft Intune 帳戶。

  * 如果您是為 iOS 或 Android 市集應用程式啟用 Intune 應用程式保護原則的 ISV，完成註冊步驟中所述的 Microsoft Intune 註冊後，即會收到促銷代碼。 促銷代碼將可讓您註冊 Microsoft Intune 試用版，以獲得 1 年的延長使用時間。

  * 如果您開發的是不會傳送至商店的企業營運應用程式，您應該透過組織來存取 Microsoft Intune。 您也可以在 [Microsoft Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0) 中註冊以獲得 1 個月免費試用版。

  * 如果您要使用終端使用者帳戶來測試行動裝置上的應用程式，請務必在使用系統管理員帳戶登入之後，於 Microsoft 365 系統管理中心網站為該帳戶提供 Intune 授權 (請參閱[指派 Microsoft Intune 授權](../fundamentals/licenses-assign.md))。

* **Intune 應用程式保護原則**：若要對應用程式測試所有 Intune 應用程式保護原則，您應該要知道每個原則設定的預期行為。 請參閱 [iOS 應用程式保護原則](../apps/app-protection-policy-settings-ios.md)和 [Android 應用程式保護原則](../apps/app-protection-policy-settings-android.md)的描述。 如果應用程式已整合 Intune SDK，但未列於可設為目標的應用程式清單中，則可在選取 [自訂應用程式] 時，於文字方塊中指定應用程式的套件組合識別碼 (iOS) 或套件名稱 (Android)。 

* **疑難排解**：如果您在手動測試應用程式的安裝使用者體驗時遇到任何問題，請參閱[針對應用程式安裝問題進行疑難排解](../apps/troubleshoot-app-install.md)。 

### <a name="give-your-app-access-to-the-intune-app-protection-service-optional"></a>將您應用程式存取權授與 Intune 應用程式保護服務 (選擇性)

若您的應用程式使用自己的自訂 Azure Active Directory (AAD) 設定來進行驗證，則您應該針對兩個公用市集應用程式與內部 LOB 應用程式執行下列步驟。 **若您的應用程式使用 Intune SDK 預設用戶端識別碼**，則不要執行步驟。 

一旦在 Azure 租用戶內註冊您的應用程式，且它出現在 [所有應用程式]  下，您就必須將您的應用程式存取權授與 Intune 應用程式保護服務 (先前稱為 MAM 服務). 在 Azure 入口網站中：

1. 移至 [Azure Active Directory]  刀鋒視窗。
2. 在 [應用程式註冊]  下，移至應用程式的清單設定。
3. 按一下 [+ 新增權限]  。
4. 按一下 [組織使用的 API]  。 
5. 在搜尋方塊中輸入 **Microsoft 行動應用程式管理**。
6. 在 [委派的權限]  底下，選取 [DeviceManagementManagedApps.ReadWrite:**讀取及寫入使用者的應用程式管理資料]** * 核取方塊。
7. 按一下 [新增權限]  。

> [!NOTE]
> 如果應用程式因為存取此資源時發生錯誤而限制登入 (https\://intunemam.microsoftonline.com)，則必須使用應用程式的用戶端識別碼來傳送附註給 msintuneappsdk@microsoft.com。 這是現今的手動核准程序。

### <a name="badge-your-app-optional"></a>為應用程式加上徽章 (選擇性)

驗證 Intune 應用程式保護原則在應用程式中運作之後，您可以使用 Intune 應用程式保護標誌為應用程式圖示加上徽章。

這個徽章對 IT 系統管理員、終端使用者和潛在 Intune 客戶表示您的應用程式使用 Intune 應用程式保護原則。 它鼓勵 Intune 客戶使用和採用您的應用程式。

徽章是一個公事包圖示，可以在下面的範例中看到︰

![Intune 應用程式保護原 - 徽章範例 1](./media/app-sdk-get-started/badge-example-1.png) ![Intune 應用程式保護原 - 徽章範例 2](./media/app-sdk-get-started/badge-example-2.png)

**為應用程式加上徽章的必要步驟**：

* 可讀取 **.eps** 檔案的映像操作應用程式，或可讀取 **.ai** 檔案的 Adobe 應用程式。

* 您可以在 Microsoft Intune GitHub 找到 [Intune app badge assets and guidelines](https://github.com/msintuneappsdk/intune-app-partner-badge) (Intune 應用程式徽章資產和指導方針)。
