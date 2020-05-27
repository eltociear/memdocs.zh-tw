---
title: 您的 Android 裝置似乎已加密 | Microsoft Docs
description: 解析公司入口網站和 Microsoft Intune 應用程式中的加密狀態
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/14/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ba593c08-1a78-4013-8525-b45a948772ec
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a7ce95d5c28b1b85f27fdd0aee74e3148abfb554
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83882261"
---
# <a name="device-encrypted-but-apps-say-otherwise"></a>裝置已加密但應用程式指出並未加密

若公司入口網站或 Microsoft Intune 應用程式指出裝置並未加密，但您很確定已經加密該裝置，則請嘗試本文中的步驟。  

## <a name="add-a-startup-pin"></a>新增啟動 PIN

某些 Android 裝置會要求您建立啟動 PIN 以確保裝置的安全。 此設定的位置將會在裝置其**設定**應用程式中。 設定的名稱和位置可能會有所不同。 例如，在 Samsung Galaxy S7 上，設定稱為**安全啟動**。 若要啟用該設定及建立密碼，請前往 [設定]   > [鎖定螢幕和安全性]   > [安全啟動]  。  

## <a name="encrypt-the-entire-device"></a>加密整部裝置

本節僅適用於公司入口網站應用程式。 某些裝置可讓您選擇加密整部裝置，或僅加密已使用的空間。 請選擇加密整部裝置的選項。 若選取僅加密已使用的空間：

1. [從公司入口網站移除這部裝置](unenroll-your-device-from-intune-android.md)。
2. 解密已使用的空間。  
3. 加密整部裝置。  
4. 重新註冊裝置。  

## <a name="downgrade-your-version-of-android"></a>將您的 Android 版本降級

本節僅適用於公司入口網站應用程式。 如果您的裝置提供降級為 Android 6.0 與更新版本的選項，請執行這些動作。 若您嘗試將裝置降級，會有資料遺失的風險。 因此，建議您連絡公司支援人員以解決此問題。 在[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)上取得公司支援人員的連絡資訊。  

## <a name="specific-manufacturer-issues"></a>特定製造商問題

某些 7.0 版與更新版本 Android 裝置加密資料的方式，與特定 Android 平台標準不一致。 這些加密方法會將裝置資訊置於風險之中。 因此不支援這些裝置。

如需支援 Android 裝置的非詳盡清單，請參閱 [Intune 中支援的作業系統及瀏覽器](https://docs.microsoft.com/intune/fundamentals/supported-devices-browsers#supported-samsung-knox-standard-devices)一文。 若裝置並未列出，請聯繫裝置製造商或連絡支援人員。

> [!Note]
> Microsoft 會與製造商合作來解決我們在測試時所發現的任何問題，或是使用者回報給我們的任何問題。 只要有新的資訊，本文會隨時更新。

## <a name="update-devices"></a>更新裝置

若尚未將裝置更新到最新的 Android 版本，請前往裝置的**設定**應用程式，然後選取 [更新]  。  

## <a name="next-steps"></a>後續步驟

是否仍需要協助？ 請連絡公司支援人員 (請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)以取得連絡資訊)，或是將電子郵件傳送給 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with enrolling my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 小組</a>。  
