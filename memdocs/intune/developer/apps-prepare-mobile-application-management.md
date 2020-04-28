---
title: 使用 Microsoft Intune 針對行動應用程式管理準備應用程式
description: 本主題中的資訊可協助您決定使用 App Wrapping Tool 和 App SDK 時機，以讓您的自訂企業營運應用程式得以使用行動應用程式管理原則。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 863e6e540fcb79ff18accc40142a8e50c1406943
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078068"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>準備應用程式防護原則的企業營運應用程式

您可以使用 Intune App Wrapping Tool 或 Intune App SDK，讓應用程式使用應用程式保護原則。 使用這項資訊可了解這兩種方法和其使用時機。

## <a name="intune-app-wrapping-tool"></a>Intune App Wrapping Tool

App Wrapping Tool 主要用於**內部**企業營運 (LOB) 應用程式。 此工具是可建立應用程式包裝函式的命令列應用程式，因而可讓 Intune 應用程式保護原則管理應用程式。 保護由獨立軟體廠商 (ISV) 所提供的應用程式時，不需要釐清該 ISV 是否仍會支援封裝的應用程式。

您不需要原始程式碼即可使用工具，但需要簽署認證。 如需簽署認證的詳細資訊，請參閱 [Intune 部落格](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/)。 如需 App Wrapping Tool 文件，請參閱 [Android App Wrapping Tool](app-wrapper-prepare-android.md) 和 [iOS App Wrapping Tool](app-wrapper-prepare-ios.md)。

應用程式包裝工具**不**支援 Apple App Store 或 Google Play 商店中的應用程式。 它也不支援某些需要開發人員整合的功能 (請參閱下列的功能比較表)。

如需 Intune 中未註冊裝置上應用程式保護原則之 App Wrapping Tool 的詳細資訊，請參閱[保護未在 Microsoft Intune 註冊之裝置上的企業營運應用程式和資料](../apps/apps-add.md)。

### <a name="reasons-to-use-the-app-wrapping-tool"></a>使用 App Wrapping Tool 的原因

* 您的應用程式沒有內建資料保護功能
* 您的應用程式部署於內部
* 您沒有 App 原始程式碼的存取權限
* 您未開發應用程式
* 您的應用程式具有最低的使用者驗證體驗

### <a name="supported-app-development-platforms"></a>支援的應用程式開發平台

|**App Wrapping Tool** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |是|是|
|**Android**|否 - 使用 [Intune App SDK Xamarin 繫結](app-sdk-xamarin.md)。|是|

## <a name="intune-app-sdk"></a>Intune App SDK

App SDK 的設計主要是針對 Apple App Store 或 Google Play Store 中具有應用程式並想要可以使用 Intune 管理應用程式的客戶。 不過，任何應用程式都可以利用 SDK 的整合，即使它是企業營運應用程式也是一樣。

若要深入了解 SDK，請參閱[概觀](app-sdk.md)。 若要開始使用 SDK，請參閱[開始使用 Microsoft Intune App SDK](app-sdk-get-started.md)。

### <a name="reasons-to-use-the-sdk"></a>使用 SDK 的理由

* 您的應用程式沒有內建資料保護功能
* 您的應用程式部署在公開應用程式商店 (例如 Google Play 或 Apple 的 App Store)
* 您是應用程式開發人員並且擁有使用 SDK 的技術背景
* 您的應用程式有其他的 SDK 整合
* 您的應用程式經常更新

### <a name="supported-app-development-platforms"></a>支援的應用程式開發平台

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|是 - 使用 [Intune App SDK Xamarin 繫結](app-sdk-xamarin.md)。|否|
|**Android**| 是 - 使用 [Intune App SDK Xamarin 繫結](app-sdk-xamarin.md)。|否|

## <a name="not-using-an-app-development-platform-listed-above"></a>不是使用上列應用程式開發平台嗎？

Intune SDK 開發小組會針對使用原生 Android、iOS (Obj-C、Swift)、Xamarin 與 Xamarin.Forms 平台所建置的應用程式，主動地進行測試並維護支援。 雖然有部分客戶成功搭配其他平台 (例如 React Native 和 NativeScript) 整合 Intune SDK，我們並沒有針對使用我們所不支援之平台的應用程式開發人員提供明確的指引或外掛程式。 

## <a name="feature-comparison"></a>功能比較

如果應用程式是使用 App SDK 或 App Wrapping Tool，則其設定如此表格所列。 有些功能需要應用程式開發人員在 Intune SDK 的基本整合之外套用一些邏輯，因此，如果應用程式使用 App Wrapping Tool，就不會啟用那些功能。 

|功能|App SDK|App Wrapping Tool|
|-----------|---------------------|-----------|
|限制要在公司管理的瀏覽器中顯示網頁內容|X|X|
|禁止 Android、iTunes 或 iCloud 備份|X|X|
|允許應用程式將資料傳送到其他應用程式|X|X|
|允許應用程式接收來自其他應用程式的資料|X|X|
|限制利用其他應用程式剪下、複製及貼上|X|X|
|指定可從受控應用程式剪下或複製的字元數|X|X|
|需要簡單的 PIN 碼才能存取|X|X|
|指定 PIN 重設之前的嘗試次數|X|X|
|允許指紋而非 PIN|X|X|
|允許臉部辨識而非 PIN (僅限 iOS)|X|X|
|需要公司認證才能存取|X|X|
|設定 PIN 到期日|X|X|
|封鎖受管理的應用程式在已進行 JB 或 Root 破解的裝置上執行|X|X|
|加密應用程式資料|X|X|
|在指定的分鐘數之後重新檢查存取需求|X|X|
|指定離線寬限期|X|X|
|封鎖螢幕擷取 (僅限 Android)|X|X|
|不註冊裝置的 MAM 支援|X|X|
|完整抹除應用程式資料|X|X|
|在多重身分識別案例中選擇性抹除公司和學校資料 <br><br>**注意︰** 若是 iOS/iPadOS，應用程式會隨管理設定檔一併移除。|X||
|禁止「另存新檔」|X||
|目標應用程式組態 (或透過「MAM 通道」設定應用程式)|X|X|
|支援多重身分識別|X||
|可自訂樣式 |X|||
|使用 Citrix mVPN 的隨選應用程式 VPN 連線|X|X| 
|停用連絡人同步|X|X|
|停用列印|X|X|
|需要最低的應用程式版本|X|X|
|需要最低的作業系統|X|X|
|需要最低的 Android 安全性修補程式版本 (僅 Android)|X|X|
|需要最低的 Intune SDK for iOS (僅限 iOS)|X|X|
|SafetyNet 裝置證明 (僅限 Android)|X|X|
|對應用程式進行威脅掃描 (僅限 Android)|X|X|
|需要 Mobile Threat Defense 廠商裝置的最高風險等級|X||
|設定組織帳戶的應用程式通知內容|X|X|
|需要使用核准的鍵盤 (僅限 Android)|X|X|
|需要應用程式保護原則 (條件式存取)|X||
|需要經過核准的用戶端應用程式 (條件式存取)|X||

## <a name="next-steps"></a>後續步驟

若要深入了解應用程式保護原則和 Intune，請參閱下列主題：

- [Android App Wrapping Tool](app-wrapper-prepare-android.md)<br>
- [iOS App Wrapping Tool](app-wrapper-prepare-ios.md)<br>
- [使用 SDK 讓應用程式進行行動應用程式管理](app-sdk.md)
