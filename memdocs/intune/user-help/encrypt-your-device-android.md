---
title: 為 Intune 加密 Android 裝置 | Microsoft Docs
description: 在 Intune 要求時開啟 Android 裝置加密的步驟
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348779"
---
# <a name="encrypting-your-android-device"></a>加密 Android 裝置

裝置加密可以保護檔案及資料夾，使其在裝置遺失或遭竊時免於未經授權的存取。 在開啟裝置加密後，只有擁有正確密碼或 PIN 的人員才能登入裝置。 

組織可能會先要求您加密 Android 裝置，之後才可以存取學校或公司資源。 有些較新的 Android 裝置根據預設會立即加密。  

## <a name="turn-on-encryption"></a>開啟加密

若公司入口網站或 Microsoft Intune 應用程式提示加密裝置，請完成下列步驟。 

> [!Note]
> 某些華為、Vivo 和 OPPO 的 Android 裝置無法進行加密。 如需詳細資訊，請參閱[這裡](your-device-appears-encrypted-but-cp-says-otherwise-android.md)。  

1. 設定裝置螢幕鎖定。  
    a. 移至 [設定]   > [Lock screen and security] \(鎖定螢幕和安全性)   > [Screen lock type] \(螢幕鎖定類型\)  。  
    b. 選取 [PIN]  、[密碼]  或 [模式]  。  
    c. 請遵循畫面上的指示來設定螢幕鎖定。  

2. 返回 [鎖定螢幕和安全性]  ，然後選取 [安全啟動]  。
3. 選擇 [在裝置開啟時要求 PIN]   > [確定]  。
4. 輸入 PIN 碼來確認並加密裝置。
5. 開啟公司入口網站或 Microsoft Intune 應用程式。
    * 公司入口網站使用者：選取您的裝置並點選 [檢查裝置設定]  。 
    * Microsoft Intune 使用者：您必須等到頁面更新為止，但當其更新時，加密狀態應該就會變更為符合規範。  

執行 Android 4.4 及更早版本的裝置可能會沒有 [安全啟動]  選項。 在此情況下，請完成下列步驟來加密裝置。

1. 前往 [設定]   > [安全性]   > [加密裝置]  。 畫面上的標籤會因 Android 裝置而不同。 若沒有看到 [加密裝置]  選項，請查看下列位置：
    * [儲存體]   > [儲存體加密] 
    * 儲存體   > 螢幕鎖定和安全性   > 其他安全性設定  

2. 遵循螢幕上的指示操作。 在加密期間，您的裝置可能會重新啟動數次。
3. 開啟公司入口網站或 Microsoft Intune 應用程式。
    * 公司入口網站使用者：選取您的裝置並點選 [檢查裝置設定]  。  
    * Microsoft Intune 使用者：您必須等到頁面更新為止，但當其更新時，加密狀態應該就會變更為符合規範。

## <a name="troubleshoot"></a>疑難排解  
**問題**：您已加密裝置且

- 已停用 [加密] 按鈕。
- 您會看到仍需加密的訊息。
- 您在嘗試使用公司入口網站或 Microsoft Intune 應用程式時發生錯誤。

**可以嘗試的動作**

- 請確定您的裝置已連接電源線且正在充電。  
- 請確定您已在裝置上設定 PIN 或密碼。  

是否仍需要協助？ 請連絡公司支援人員 (可查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)以取得連絡資訊)，或是撰寫電子郵件給 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 小組</a>。  
