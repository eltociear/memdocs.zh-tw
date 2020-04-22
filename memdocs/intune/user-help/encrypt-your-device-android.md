---
title: 為 Intune 加密 Android 裝置 | Microsoft Docs
description: 在 Intune 要求時開啟 Android 裝置加密的步驟
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/31/2020
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: d9e074def368927504c3f3c1761ec21b3ab62d22
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696268"
---
# <a name="encrypting-your-android-device"></a>加密 Android 裝置

裝置加密可以保護檔案及資料夾，使其在裝置遺失或遭竊時免於未經授權的存取。 其會使沒有密碼的人無法存取裝置上的資料，也無法讀取資料。 

您的組織可能會要求您執行下列動作，才能存取學校或公司資源：

* [加密您的裝置](#encrypt-device)
* [啟用安全啟動](#enable-secure-startup)
* [設定啟動密碼、PIN 或其他驗證方法](#set-startup-passcode)  

> [!Note]
> 某些華為、Vivo 和 OPPO 的 Android 裝置無法進行加密。 如需詳細資訊，請參閱[裝置已加密，但應用程式表示裝置未加密 ](your-device-appears-encrypted-but-cp-says-otherwise-android.md)。  

## <a name="encrypt-device"></a>加密裝置

請遵循下列步驟來加密您的裝置。 您的裝置可能會重新啟動數次。 

加密選項的名稱與位置，會根據您的裝置製造商與 Android 版本而有所不同。 

1. 開啟 [設定]  應用程式。
2. 在應用程式的搜尋列中輸入**安全性**或**加密**，以尋找相關的設定。
3. 點選選項來加密您的裝置。 遵循螢幕上的指示操作。  
4. 出現提示時，請設定鎖定畫面密碼、PIN 或其他驗證方法 (如果您的組織允許)。 
5. 若要重新檢查設定，請開啟公司入口網站或 Microsoft Intune 應用程式。
    * 公司入口網站使用者：選取您的裝置並點選 [檢查裝置設定]  。 
    * Microsoft Intune 使用者：您必須等到頁面更新為止，但當其更新時，加密狀態應該就會變更為符合規範。 

## <a name="enable-secure-startup"></a>啟用安全啟動

您的組織可能會要求您啟用安全啟動，作為其加密原則的一部分。 此功能可在手機啟動之前，要求輸入密碼或 PIN，以進一步保護您的裝置。 您有許多其他驗證選項，但會根據您的組織允許的內容而有所不同。 

安全啟動選項的名稱與位置，會根據您的裝置製造商與 Android 版本而有所不同。 在某些裝置上，此設定可能稱為**增強式保護**。 

1. 開啟 [設定]  應用程式。
2. 在應用程式的搜尋列中，輸入**安全啟動**。
3. 點選 [安全啟動]   > [在裝置開啟時要求 PIN]  。
4. 出現提示時，請輸入您的裝置 PIN。   
5. 若要重新檢查設定，請開啟公司入口網站或 Microsoft Intune 應用程式。
    * 公司入口網站使用者：選取您的裝置並點選 [檢查裝置設定]  。 
    * Microsoft Intune 使用者：您必須等到頁面更新為止，但當其更新時，加密狀態應該就會變更為符合規範。  


## <a name="set-startup-passcode"></a>設定啟動密碼   
當您[加密您的裝置](#encrypt-device)並[啟用安全啟動](#enable-secure-startup)時，系統會提示您設定裝置 PIN、密碼或其他驗證方法 (如果您的組織允許)。 不需要進一步的步驟。 

選擇或變更鎖定畫面類型：

1. 開啟 [設定]  應用程式。
2. 在應用程式的搜尋列中，輸入**畫面鎖定**。
3. 點選 [畫面鎖定類型]  。
4. 點選您要使用的畫面鎖定類型，並遵循螢幕上的指示來確認。  

## <a name="troubleshoot"></a>疑難排解    
**問題**：已停用 [加密] 按鈕。   

**可以嘗試的方法**： 
* 確定您的裝置已完全充電並連接電源線。 加密可能需要一些時間，而且需要滿電電池。   

**問題**：您看到裝置仍需加密的訊息。  

**可以嘗試的方法**：
   *  [在您的裝置上設定鎖定畫面](#set-startup-passcode)。 
   * [啟用安全啟動](#enable-secure-startup)。

是否仍需要協助？ 請連絡公司支援人員 (可查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)以取得連絡資訊)，或是撰寫電子郵件給 <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">Microsoft Android 小組</a>。  
