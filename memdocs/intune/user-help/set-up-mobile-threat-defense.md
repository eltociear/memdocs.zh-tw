---
title: 在您的行動裝置上安裝 Mobile Threat Defense
description: 了解如何在您的行動裝置上安裝 Mobile Threat Defense。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/25/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b5df63a14f27b657c585eb43e09b02368d969939
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084403"
---
# <a name="install-mobile-threat-defense"></a>安裝 Mobile Threat Defense   

根據組織的安全性需求，您可能必須安裝 Mobile Threat Defense (MTD) 廠商應用程式。 此類應用程式會偵測裝置上的威脅 (例如可疑的應用程式、網路和 OS 弱點) 並警告您。  

如果沒有所需的 MTD 應用程式，則會禁止您使用公司或學校帳戶來登入受保護的應用程式。 在本文中，您將了解[如何安裝 MTD 應用程式](set-up-mobile-threat-defense.md#install-app)以防止遭到封鎖。  

有多種 MTD 廠商應用程式可供安裝；組織會讓您知道要使用哪一種。 


## <a name="information-your-organization-can-see"></a>組織可以看到的資訊   

組織無法看到您個人應用程式中的任何資料，例如文字、電子郵件和圖片。 不過，MTD 應用程式會將您應用程式的相關資訊 (例如名稱和版本) 回報給組織。 所回報實際資訊取決於公司使用的 MTD 廠商。 組織可能會看到：   

* 應用程式名稱  
* 應用程式識別碼：在 Google Play 中識別應用程式的唯一名稱。  
* 應用程式版本和簡短版本號碼：應用程式的特定版本號碼。  
* 應用程式套件組合和動態大小：應用程式在您的裝置上使用的空間量。 


## <a name="install-app"></a>安裝應用程式    
當登入受保護的應用程式時，系統會自動提示您安裝 MTD 應用程式。 請遵循畫面上的步驟來完成安裝。 您可以利用本節中的步驟來取得其他協助。  
 
系統也可能會提示您註冊裝置。 必須註冊才能確認您的身分識別，並將學校或公司帳戶連線到裝置。 如果尚未註冊，則會在安裝 MTD 應用程式之前，自動引導您完成該設定。 當到達 [取得存取權]  畫面時，您可以開始執行安裝步驟。  

如需裝置註冊的詳細資訊，請參閱[在組織的網路上註冊個人裝置](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network) (機器翻譯)。  

### <a name="ios-setup"></a>iOS 設定  

1. 在 [取得存取權]  畫面上，遵循指示來安裝組織所需的 MTD 應用程式。   
2. 返回 [取得存取權]  畫面，然後選取 [開啟]  。  
3. MTD 應用程式會要求開啟 Microsoft Authenticator 的權限。 選取 [開啟]  。 
4. 選取公司帳戶以進行登入。 
5. 等候 MTD 應用程式掃描裝置是否有安全性威脅。 
6. 返回您原本嘗試存取的學校或公司應用程式。 此時，組織可能會提示您設定其他應用程式安全性需求，例如建立 PIN。   
7. 您現在應該可以存取應用程式。 如果您仍被封鎖：  
    * 在 [取得存取權]  畫面上，請選取 [重新檢查]  。  
    * 移至 MTD 應用程式，並檢查是否有任何威脅。 完成建議的步驟，以解決威脅並重新取得存取權。    

### <a name="android-setup"></a>Android 設定 

1. 在 [取得存取權]  畫面上，遵循指示來安裝組織所需的 MTD 應用程式。  
2. 返回 [取得存取權]  畫面，然後選取 [開啟]  。  
3. 如有需要，MTD 應用程式會要求存取您裝置特定區域的權限。 為了讓此應用程式正常運作，您必須**允許**存取連絡人。 要求的權限會因 MTD 廠商而異。  
4. 選取公司帳戶以進行登入。  
5. 等候 MTD 應用程式掃描裝置是否有安全性威脅。  
6. 返回您原本嘗試存取的學校或公司應用程式。 此時，組織可能會提示您設定其他應用程式安全性需求，例如建立 PIN。  
7. 您現在應該可以存取應用程式。 如果您仍被封鎖：  
    * 在 [取得存取權]  畫面上，請選取 [重新檢查]  。  
    * 移至 MTD 應用程式，並檢查是否有任何威脅。 完成建議的步驟，以解決威脅並重新取得存取權。  

### <a name="installation-failed"></a>安裝失敗  

如果安裝失敗，請連絡 IT 支援人員。 前往[公司入口網站網站](https://go.microsoft.com/fwlink/?linkid=2010980)來尋找您組織的連絡資訊。  

您也可以將應用程式記錄檔傳送給 IT 支援人員，以提供安裝的其他相關內容。  
* Android 使用者：從公司入口網站[上傳及以電子郵件傳送記錄檔](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)。   

* iOS 裝置使用者：從 iOS 版 Microsoft Edge [擷取及傳送記錄檔](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs)。  

## <a name="resolve-a-threat"></a>解決威脅  
如果威脅超過您組織定義的威脅等級，則組織將會：  
   
* 封鎖存取：禁止您在登入公司或學校帳戶之後，使用組織的受保護應用程式。  
* 抹除資料：從您組織的一或多個受保護應用程式，刪除公司或學校資料。  

若要解決威脅並重新取得存取權，請在裝置上開啟 MTD 應用程式。 請完整閱讀提供的資訊，以了解威脅如何影響裝置及其解決方法。 在遵循步驟以解決威脅之後，請回到 MTD 應用程式並起始新的掃描。 組織可能需要幾分鐘的時間才能重新取得存取權。  

## <a name="next-steps"></a>後續步驟  

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。

