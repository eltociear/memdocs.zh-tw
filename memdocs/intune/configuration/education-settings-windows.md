---
title: Microsoft Intune 中的 Windows 10 教育設定 - Azure | Microsoft Docs
description: 查看適用於 Windows 10 裝置的所有教育設定清單。 在 Intune 中搭配「進行測驗」應用程式在裝置組態設定檔中使用這些設定、選擇使用者或學生的登入方式、在測驗期間監視螢幕等等。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 551f0a442f81712cff29a9ff6f55c62aeaba547a
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078187"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>使用 Intune 在 Windows 10 裝置上設定「進行測驗」應用程式

「進行測驗」應用程式可供在教室中的 Windows 10 裝置上安全地管理線上測驗。 若要設定「進行測驗」應用程式，則必須在 Intune 中建立裝置組態設定檔，並設定安全性評定設定。 本文描述您會在「進行測驗」應用程式中看見的設定。 

設定好設定檔之後，請將其指派並部署給學生。 

[Intune 中的「進行測驗」應用程式](education-settings-configure.md)提供此功能的詳細資訊。

## <a name="before-you-begin"></a>開始之前

[建立裝置組態設定檔](education-settings-configure.md#create-a-device-profile)。

## <a name="take-a-test-settings"></a>「進行測驗」設定
建立裝置組態設定檔之後，請前往 [設定檔類型]  ，然後選取 [安全性評定 (教育)]  。 您會看見下列「進行測驗」應用程式的設定。 


- **帳戶類型**：選擇使用者登入測驗的方式。 選項包括：
  - Azure AD 帳戶
  - 網域帳戶
  - 本機帳戶
  - 本機來賓帳戶：僅適用於執行 Windows 10 1903 版和更新版本的裝置。    
- **帳戶使用者名稱**：輸入要搭配「進行測驗」應用程式使用的帳戶使用者名稱。 您可以使用下列格式來輸入帳戶：
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **帳戶名稱**：若要設定本機來賓帳戶類型，請輸入用於「進行測驗」應用程式的帳戶使用者名稱。 帳戶名稱會顯示為登入畫面上的磚。 學生可以按一下該磚來啟動測試。  
- **評定 URL**：輸入您要讓使用者進行之測驗的 URL。 如需取得此 URL 的詳細資訊，請參閱[「進行測驗」文件](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) \(部分機器翻譯\)。
- **印表機連線**：選擇 [必要]  ，僅允許連線至印表機的裝置來存取「進行測驗」應用程式。 此設定也會讓受測者可使用應用程式的 [列印] 按鈕。 [未設定]  ，允許學生使用未連線至印表機的裝置來存取應用程式。  
- **螢幕監視**：選擇 [允許]  以在使用者接受測驗時監視螢幕活動。 [未設定]  會讓您無法在測驗期間監視螢幕。
- **文字建議**：選擇 [允許]  來讓受測者看見文字建議。 [未設定]  會在使用者接受測驗時封鎖文字建議。

## <a name="next-steps"></a>後續步驟

請務必[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
