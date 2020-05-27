---
title: 什麼是裝置註冊 | Microsoft Docs
description: 了解向公司入口網站和 Microsoft Intune 應用程式註冊裝置的意義為何。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/13/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 523caa6b-d792-4bb6-bddb-24b2479932d8
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 3f80fffc21ac4dcd256120b03dc1e0bebe20ab52
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880706"
---
# <a name="what-is-device-enrollment"></a>什麼是裝置註冊？
若要從裝置存取公司或學校資源，則將需要向 Intune 公司入口網站應用程式或 Microsoft Intune 應用程式註冊裝置。 

裝置註冊期間：

* 裝置會向組織登錄。 此步驟可確保您有權存取組織的電子郵件、應用程式和 Wi-Fi。 
* 組織的裝置管理原則會套用到裝置。 原則可能包含裝置密碼和加密等需求。 這些需求的目的是保護裝置和組織資料的安全，避免其受到未經授權的存取。

在更新裝置設定以符合組織的需求後，註冊便已完成。 您可以幾乎任何地方安全地登入公司或學校帳戶。  

本文描述註冊的其他層面，例如如何取得應用程式、支援裝置，以及移除或重設裝置。  

## <a name="company-portal-and-microsoft-intune-app"></a>公司入口網站和 Microsoft Intune 應用程式

公司入口網站和 Microsoft Intune 應用程式會針對原則或設定變更提出警示，讓您可以採取動作，而無須失去對公司或學校的存取權。 

公司入口網站應用程式會將個人和公司資訊分開，讓您可以維持生產力及保持集中。 這也可以提供您公司和學校應用程式，讓您可以尋找及安裝與工作相關的應用程式。  

### <a name="get-company-portal"></a>取得公司入口網站

在某些情況下，組織將會為您在裝置上安裝公司入口網站應用程式。 您也可以從 Microsoft Store、App Store 和 Google Play 商店等應用程式市集安裝應用程式。 若要從網頁瀏覽器存取應用程式，請使用公司或學校帳戶登入[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  

### <a name="get-microsoft-intune-app"></a>取得 Microsoft Intune 應用程式

若需要使用 Microsoft Intune 應用程式，則組織將會為您在裝置上安裝該應用程式。  

## <a name="whats-the-difference-between-the-apps-and-the-website"></a>應用程式與網站之間的差異為何？
公司入口網站應用程式適用於 Windows 10、iOS、macOS 和 Android 裝置。 其可以和裝置的個別平台完美整合。 網站版本可從任何裝置存取，不論您使用哪種裝置，都能提供您相同且通用的體驗。 

Microsoft Intune 應用程式適用於公司擁有的 Android 裝置，且沒有網站。  

## <a name="what-kind-of-devices-can-you-enroll-with-company-portal"></a>您可以使用公司入口網站註冊哪些類型的裝置？
您可以使用公司入口網站註冊下列裝置：  

- Windows 裝置
  - Windows 10 Mobile
  - Windows 10 Desktop
  - Windows Phone 8。1
  - Windows 8。1
- Apple 裝置
    - iOS
    - macOS
- Android 裝置


## <a name="what-kind-of-devices-can-you-enroll-with-the-microsoft-intune-app"></a>您可以使用 Microsoft Intune 應用程式註冊哪些類型的裝置？  
您可以註冊由公司擁有並已經過組織設定，用來搭配應用程式使用的 Android 裝置。 應用程式支援 Android 6.0 及更新版本。 

## <a name="can-you-remove-a-device-from-the-company-portal"></a>您是否可以從公司入口網站移除裝置？
您可以從公司入口網站移除或重設裝置。 [移除]  與 [重設]  不同。

在裝置移除期間，公司入口網站會取消註冊及取消登錄裝置。 裝置會失去對公司入口網站的存取權。 公司或學校資料也可能會遭到移除。 

在裝置重設期間，公司入口網站會嘗試將電腦或裝置重設為製造商的預設設定。 所有公司或學校資料及所有個人資料都會從裝置移除。 例如，若遺失了裝置，則重設便相當有用。 您可以從公司入口網站遠端進行重設。  

## <a name="can-you-remove-a-device-from-the-microsoft-intune-app"></a>您是否可以從 Microsoft Intune 應用程式移除裝置？
否，您無法從 Microsoft Intune 應用程式移除公司擁有的裝置。  

## <a name="what-if-i-cant-see-my-device-in-the-company-portal-or-microsoft-intune-app"></a>如果在公司入口網站或 Microsoft Intune 應用程式中看不到裝置怎麼辦？
若要在公司入口網站中查看裝置，則必須先註冊裝置。 在註冊之後，若仍然無法看到您所有的裝置，請嘗試透過公司入口網站進行同步或檢查存取。 您將不會看到您公司所擁有及管理的裝置。

在 Microsoft Intune 應用程式中，您只會看見目前正在使用的裝置。 您無法在應用程式中看見其他註冊的裝置。  

## <a name="where-else-can-i-go-for-help"></a>我還能去哪裡尋求協助？  
若要針對常見問題進行疑難排解，請查看下列這些平台特定文件：  

- [修正 Android 裝置常見的問題](check-compliance-on-your-device-android.md)  
- [修正 iOS 裝置常見的問題](troubleshoot-your-device-ios.md)
- [修正 macOS 裝置常見的問題](troubleshoot-your-device-macos.md)
- [修正 Windows 裝置常見的問題](troubleshoot-your-device-windows.md)

您也可以連絡 IT 支援人員。 公司入口網站和 Microsoft Intune 應用程式提供協助和支援頁面，其中列出了連絡資訊及報告問題的方式。 您也可以在組織的[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)上取得連絡資訊。  

## <a name="next-steps"></a>後續步驟  

若您已準備好存取公司或學校帳戶，請遵循組織的指示來註冊裝置。 您也可以在下列文章中找到逐步註冊指導。

* [註冊 Windows 10 裝置](enroll-windows-10-device.md)
* [註冊您的 Android 裝置](enroll-device-android-company-portal.md)
* [使用 Android 工作設定檔註冊](enroll-device-android-work-profile.md)
* [使用 Microsoft Intune 應用程式註冊](enroll-device-android-microsoft-intune-app.md)
* [註冊 iOS 裝置](enroll-your-device-in-intune-ios.md)
* [註冊您組織提供的 iOS 裝置](enroll-your-device-dep-ios.md)
* [註冊 macOS 裝置](enroll-your-device-in-intune-macos-cp.md)
* [註冊您組織提供的 macOS 裝置](enroll-company-device-macos.md)
