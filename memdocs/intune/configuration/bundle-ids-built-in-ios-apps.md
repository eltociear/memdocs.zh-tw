---
title: Microsoft Intune 中內建應用程式的 iOS/iPadOS 套件組合識別碼 - Azure | Microsoft Docs
titleSuffix: ''
description: 查看內建 iOS 與 iPadOS 應用程式的套件組合識別碼清單。 使用這些套件組合識別碼，可明確允許使用 Microsoft Intune 裝置組態設定檔和原則中的應用程式。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7de0b978c24f28988c62854a249505a0598db95
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084070"
---
# <a name="bundle-ids-for-built-in-ios-and-ipados-apps-you-can-use-in-intune"></a>您可以在 Intune 中使用之內建 iOS 與 iPadOS 應用程式的套件組合識別碼

當您在 iOS/iPadOS 裝置上設定功能時，您也可以在 iOS/iPadOS 裝置上新增內建的應用程式。 此文章列出一些常見內建 iOS/iPadOS 應用程式的套件組合識別碼。 若要尋找其他應用程式的套件組合識別碼，請連絡軟體廠商。 查看 Apple 的 [iOS/iPadOS 套件識別碼](https://support.apple.com/guide/mdm/ios-bundle-ids-mdm90f60c1ce/web)清單 (將會開啟 Apple 的網站)。

## <a name="bundle-ids"></a>套件組合識別碼

| 套件組合識別碼                   | 應用程式名稱     | 發行者 |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | App Store    | Apple     |
| com.apple.store.Jolly       | Apple Store  | Apple     |
| com.apple.calculator        | 計算機   | Apple     |
| com.apple.mobilecal         | 行事曆     | Apple     |
| com.apple.camera            | 相機       | Apple     |
| com.apple.mobiletimer       | 時鐘        | Apple     |
| com.apple.clips             | 剪輯        | Apple     |
| com.apple.compass           | 指南針      | Apple     |
| com.apple.MobileAddressBook | 連絡人     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com.apple.DocumentsApp      | 檔案        | Apple     |
| com.apple.mobileme.fmf1     | 尋找朋友 | Apple     |
| com.apple.mobileme.fmip1    | 尋找 iPhone  | Apple     |
| com.apple.gamecenter        | Game Center  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | 健康       | Apple     |
| com.apple.Home              | 家庭         | Apple     |
| com.apple.iBooks            | 書籍       | Apple     |
| com.apple.iMovie            | iMovie       | Apple     |
| com.apple.itunesconnect.mobile | iTunes Connect | Apple |
| com.apple.MobileStore       | iTunes Store | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | 郵件         | Apple     |
| com.apple.Maps              | 地圖         | Apple     |
| com.apple.measure           | 度量      | Apple     |
| com.apple.MobileSMS         | 訊息     | Apple     |
| com.apple.Music             | 音樂        | Apple     |
| com.apple.news              | 新聞         | Apple     |
| com.apple.mobilenotes       | 備忘錄        | Apple     |
| com.apple.Numbers           | Numbers      | Apple     |
| com.apple.Pages             | Pages        | Apple     |
| com.apple.mobilephone       | 電話        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | 照片       | Apple     |
| com.apple.podcasts          | Podcast     | Apple     |
| com.apple.reminders         | 提醒事項    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | 設定     | Apple     |
| com.apple.shortcuts         | 捷徑    | Apple     |
| com.apple.SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | 股市       | Apple     |
| com.apple.tips              | 提示         | Apple     |
| com.apple.tv                | 電視           | Apple     |
| com.apple.videos            | 影片       | Apple     |
| com.apple.VoiceMemos        | 語音備忘錄   | Apple     |
| com.apple.Passbook          | 錢包       | Apple     |
| com.apple.Bridge            | Watch        | Apple     |
| com.apple.weather           | 天氣      | Apple     |

## <a name="next-steps"></a>後續步驟

使用這些套件組合識別碼可設定[裝置功能](ios-device-features-settings.md)，以及在 iOS/iPadOS 裝置上[允許或限制某些設定](device-restrictions-ios.md)。
