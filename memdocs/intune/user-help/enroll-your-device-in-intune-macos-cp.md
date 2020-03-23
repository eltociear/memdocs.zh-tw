---
title: 使用 Intune 公司入口網站註冊 Mac | Microsoft Docs
description: 了解如何使用公司入口網站應用程式在 Intune 中註冊 Mac。
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/16/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 2ef7951217b0b6df21a86ca29a8637385aa65715
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337014"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>使用公司入口網站應用程式註冊 macOS 裝置  

使用 Intune 公司入口網站應用程式註冊您的 macOS 裝置，以安全地存取您的公司或學校電子郵件、檔案和應用程式。

組織通常會要求先註冊裝置，才能存取專屬資料。 您的裝置註冊之後，它就變成「受控」  。 您的組織可以透過 Intune 等行動裝置管理 (MDM) 提供者將原則和應用程式指派給裝置。 若要從您的裝置持續存取公司或學校資訊，您必須設定裝置以符合您組織的原則設定。  

本文描述如何使用適用於 macOS 的公司入口網站應用程式來註冊、設定及維護裝置，以符合您組織的要求。  


## <a name="what-to-expect-from-the-company-portal-app"></a>公司入口網站應用程式的預期行為

在初始設定期間，公司入口網站應用程式會要求註冊並向組織自我驗證。 公司入口網站接著會通知您必須設定以符合組織需求的任何裝置設定。 例如，組織通常會設定您必須符合的密碼字元數下限或上限需求。    

註冊裝置之後，公司入口網站一律會根據組織的需求來確保裝置受到保護。 例如，如果從未受信任的來源安裝應用程式，則公司入口網站會警告並可能限制您存取組織的資源。 這類應用程式保護原則很常見。 若要重新取得存取權，則可能需要解除安裝未受信任的應用程式。 

如果在註冊之後，您的組織強制執行新的安全性需求 (例如多重要素驗證)，公司入口網站會通知您。 您將有機會調整設定，以便繼續在裝置上工作。  

若要深入了解註冊，請參閱[當我安裝公司入口網站應用程式並註冊我的裝置時，會發生什麼情況？](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md)  

## <a name="get-your-macos-device-managed"></a>讓 macOS 裝置成為受控  
請使用下列步驟，向組織註冊 macOS 裝置。 裝置必須執行 macOS 10.12 或更新版本。   

> [!NOTE]
> 在這整個過程中，系統可能會提示您允許公司入口網站使用儲存在 Keychain 中的機密資訊。 這些提示是 Apple 安全性的一部分。 當收到提示時，請鍵入您的登入 Keychain 密碼，然後選取 [永遠允許]  。 如果按下鍵盤上的 **Enter** 或 **Return** 鍵，則此提示會改為選取 [允許]  ，而可能會產生其他提示。  

### <a name="install-company-portal-app"></a>安裝公司入口網站應用程式  
1. 移至[註冊我的 Mac](https://go.microsoft.com/fwlink/?linkid=853070)。  
2. 這會下載公司入口網站安裝程式 .pkg 檔案。 開啟安裝程式並繼續執行步驟。 
3. 同意軟體授權合約。 
4. 輸入裝置密碼或註冊的指紋，以安裝軟體。  
5. 開啟 [公司入口網站]。 

> [!IMPORTANT]
> Microsoft AutoUpdate 可能會開啟以更新 Microsoft 軟體。 安裝所有更新之後，請開啟公司入口網站應用程式。 為獲得最佳安裝體驗，請安裝最新版的 Microsoft AutoUpdate 和公司入口網站。  


### <a name="enroll-your-mac"></a>註冊 Mac  


1. 使用您的公司或學校帳戶登入公司入口網站。  
2. 當應用程式開啟時，請選取 [開始]  。  
3. 檢閱組織在已註冊裝置上可以看到與無法看到的內容。 接著，選取 [繼續]  。
4.  如果出現提示，請在 [安裝管理設定檔]  畫面上輸入裝置密碼。

    ![公司入口網站 [安裝管理設定檔] 畫面的範例螢幕擷取畫面，其中醒目提示密碼提示。](./media/install-management-profile-macos-1912.PNG)   
5. 在 [確認裝置管理]  畫面上，選取 [開啟系統偏好設定]  。  

    ![[確認裝置管理] 畫面的範例螢幕擷取畫面，其中醒目提示 [開啟系統偏好設定] 按鈕。](./media/confirm-device-management-macos-1912.PNG)  
6. 裝置的系統偏好設定隨即開啟。 從 [裝置設定檔] 清單選取 [管理設定檔]  ，然後選取 [核准]   > [核准]  。  
    ![系統偏好設定 [管理設定檔] 畫面的範例螢幕擷取畫面，其中醒目提示 [核准] 按鈕。](./media/management-profile-approve-macos-1912.PNG)   
1. 返回公司入口網站，然後選取 [繼續]  。    
2. 貴組織可能會要求您更新裝置設定。 當完成更新設定時，請選取 [檢查設定]  。  

    ![公司入口網站 [更新裝置設定] 畫面的範例螢幕擷取畫面，其中醒目提示 [檢查設定] 按鈕。](./media/update-settings-mac-1911.PNG)  
9. 當安裝程式完成時，請選取 [完成]  。  


 ## <a name="troubleshooting-and-feedback"></a>疑難排解和意見反應   

如果在註冊期間遇到問題，請移至 [說明]   > [傳送診斷報告]  ，將問題回報給 Microsoft 應用程式開發人員。 這項資訊可用來改善應用程式。 如果 IT 支援人員與開發人員聯繫以取得協助，則這些開發人員也會使用這項資訊來協助解決問題。  

將問題回報給 Microsoft 之後，即可將體驗的詳細資料傳送給 IT 支援人員。 選取 [郵寄詳細資訊]  。 在電子郵件的本文中鍵入您的體驗。 若要尋找支援人員的電子郵件地址，請移至公司入口網站應用程式 > [連絡人]  。 或是查看[公司入口網站網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
 

此外，Microsoft Intune 公司入口網站小組也歡迎您提供意見反應。 請移至 [說明]   > [傳送意見反應]  ，以分享想法和意見。  

## <a name="unverified-profiles"></a>未驗證的設定檔  
當您在 [系統喜好設定]   > [設定檔]  中檢視已安裝的行動裝置管理 (MDM) 設定檔時，有些設定檔可能會顯示未驗證狀態。 只要管理設定檔顯示已驗證狀態，您就不需要擔心。  

管理設定檔定義 MDM 通道連線。 只要管理設定檔經過驗證，透過該通道傳遞至機器的任何其他設定檔就會繼承管理設定檔的安全性特性。  

## <a name="updating-the-company-portal-app"></a>更新公司入口網站應用程式

更新公司入口網站應用程式的完成方式與任何其他 Office 應用程式一樣，都是透過適用於 macOS 的 Microsoft AutoUpdate。 深入了解[更新 macOS 版的 Microsoft 應用程式](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1)。  

## <a name="next-steps"></a>後續步驟  
是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  


