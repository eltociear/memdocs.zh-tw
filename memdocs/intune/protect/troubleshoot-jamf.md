---
title: 針對 Jamf Pro 與 Microsoft Intune 的整合進行疑難排解
titleSuffix: Microsoft Intune
description: 針對將 Jamf Pro for Mac 裝置與 Microsoft Intune 整合時一些最常見問題進行疑難排解的建議。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f685f1f3d009d7ba7a1dc061ec3025b2f8c96b5f
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084641"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>針對 Jamf Pro 與 Microsoft Intune 的整合進行疑難排解

本文可協助 Intune 管理員了解和針對 Jamf Pro for macOS 與 Intune 整合的問題進行疑難排解。

> [!TIP]  
> 本文中大部分的資訊原本都出現在 support.microsoft.com 上的[針對在將 Jamf 與 Microsoft Intune 整合時發生的問題進行疑難排解](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) (英文) 一文中。

## <a name="prerequisites"></a>先決條件

開始疑難排解前，請先收集基本資訊來釐清問題，並減少尋找解決方案的時間。 例如，當遇到與 Jamf-Intune 整合相關的問題時，請一律驗證已滿足所有的先決條件。 請在開始疑難排解前，檢閱下列考量：

- 檢閱[將 Jamf Pro 與 Intune 整合](conditional-access-integrate-jamf.md#prerequisites)中的先決條件。
- 所有使用者都必須擁有 Microsoft Intune 和 Microsoft AAD 進階 P1 授權 
- 您必須具備在 Jamf Pro 主控台中擁有 Microsoft Intune 整合權限的使用者帳戶。
- 您必須具備在 Azure 中擁有全域管理員權限的使用者帳戶。


請在調查 Jamf Pro 與 Intune 的整合時考慮下列資訊： 
- 確切錯誤訊息為何？
- 錯誤訊息在哪裡？
- 問題何時開始發生？  Jamf Pro 與 Intune 的整合是否曾正常運作過？
- 有多少使用者受到影響？ 所有使用者都受到影響，還是只有部分使用者受到影響？
- 有多少裝置受到影響？ 所有裝置都受到影響，還是只有部分裝置受到影響？
 

## <a name="common-problems"></a>常見問題 

下列資訊有助識別和解決在設定 Intune 和 Jamf Pro 整合後常見的裝置問題。  

| 問題   | 更多資訊                  |
|-----------------|--------------------------|
| **裝置在 Jamf Pro 中標記為沒有回應**  | [裝置無法使用 Jamf Pro 或 Azure AD 存回](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Mac 裝置在開啟裝置無法登錄的應用程式時出現提示，要求進行 keychain 登入**  | [使用者收到提示，要求提供密碼來允許應用程式向 Azure AD 進行登錄](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)。 |
| **裝置無法登錄**  | 原因可能如下： <br> **-** [原因 1 - Azure 中的 Jamf Pro 應用程式所擁有的權限不正確](#cause-1) <br> **-** [原因 2 - Azure AD 中的 *Jamf Native macOS Connector* 發生問題](#cause-2) <br> **-** [原因 3 - 使用者沒有有效的 Intune 或 Jamf 授權](#cause-3) <br> **-** [原因 4 - 使用者並未使用 Jamf Self Service 來啟動公司入口網站應用程式](#cause-4) <br> **-** [原因 5 - Intune 整合已關閉](#cause-5) <br> **-** [原因 6 - 裝置先前已在 Intune 中註冊，或使用者嘗試登錄裝置多次](#cause-6) <br> **-** [原因 7 - JamfAAD 從使用者的 keychain 中要求存取「Microsoft Workplace Join 金鑰」](#cause-7) |
|  **Mac 裝置在 Intune 中顯示符合規範，但在 Azure 中卻顯示不符合規範** | [裝置登錄問題](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Intune 主控台中出現使用 Jamf 註冊 Mac 裝置的重複項目** | [相同的裝置有多個登錄](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **合規性政策無法評估裝置** | [原則目標裝置群組](#compliance-policy-fails-to-evaluate-the-device) |
| **無法擷取 Microsoft Graph API 的存取權杖** | 原因可能如下： <br> -[Azure 中 Jamf Pro 應用程式的權限](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Jamf 或 Intune 授權已過期](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [連接埠並未開啟](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>裝置在 Jamf Pro 中標記為沒有回應  

**原因**：下列為裝置由 Jamf Pro 標記為「沒有回應」  的常見原因：

- 裝置無法使用 Jamf Pro 存回。  
  Jamf Pro 預期裝置每 15 分鐘進行存回。 若裝置在 24 小時的期間內無法存回，Jamf 即會將裝置標記為沒有回應。  

- 裝置無法使用 Azure AD 存回。  
  成功登錄至 Azure AD 後，macOS 裝置會收到 Azure 權杖：
  - 這個權杖每 12 小時會重新整理一次。   
  - 當權杖重新整理失敗超過 24 小時，Jamf Pro 即會將裝置標記為沒有回應。  
  - 若 Azure 權杖過期，使用者即會收到提示，要求登入 Azure 以取得新的權杖。 用於 Azure 存取的重新整理權杖每七天會產生一次。

**解決方法**  
在裝置由 Jamf Pro 標記為「沒有回應」  後，裝置的已註冊使用者必須登入，才能修正沒有回應的狀態。 其必須是已加入公司帳戶的使用者，因為這些使用者在其登入 keychain 中擁有 Intune 的身分識別。



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Mac 裝置在開啟應用程式時出現提示，要求進行 keychain 登入  

在設定 Intune 和 Jamf Pro 整合並部署條件式存取原則後，使用 Jamf Pro 所管理裝置的使用者會在開啟 Teams、Outlook 等 Microsoft Office 365 應用程式，以及其他需要 Azure AD 驗證的應用程式時收到提示，要求提供密碼。 

例如，開啟 Microsoft Teams 時，會出現包含與下列範例相似文字的提示：

``` 
  Microsoft Teams wants to sign using key "Microsoft Workplace Join Key" in your keychain.  
  To allow this, enter the "login" keychain password 
```

**原因**：Jamf Pro 會為每個需要 Azure AD 登錄的適用應用程式產生這些提示。 

**解決方法**   
出現提示時，使用者必須提供其裝置密碼來登入 Azure AD。 這些選項包括：
- **拒絕** - 不要登入且不要使用應用程式。
- **允許** - 單次登入。 下一次當應用程式開啟時，會再次出現登入提示。
- **一律允許** - 為應用程式快取登入認證。 下一次當應用程式開啟時，不會再次出現登入提示。  

為應用程式選取 [一律允許]  只會核准該應用程式未來的登入。 其他應用程式仍會出現提示要求驗證，直到這些應用程式也設為 [一律允許]  為止。 單一應用程式的快取認證無法由其他應用程式使用。  

### <a name="devices-fail-to-register"></a>裝置無法登錄  

Mac 裝置無法登錄有數個常見的原因。  

#### <a name="cause-1"></a>原因 1  

**Azure 中的 Jamf Pro 企業應用程式具有錯誤權限，或擁有一個以上的權限**  

  當在 Azure 中建立應用程式時，您必須移除所有預設 API 權限，然後將單一的 *update_device_attributes* 權限指派給 Intune。 

  **解決方法**  
  檢閱並視需要修正在 Azure AD 中所建立 Jamf 應用程式的權限。 請參閱[在 Azure AD 中建立 Jamf 應用程式](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory)的程序。 

#### <a name="cause-2"></a>原因 2  

****Jamf Native macOS Connector** 應用程式並未在您的 Azure AD 租用戶中建立，或該連接器的同意是由不具備全域管理員權限的帳戶所簽署**  

  **解決方法**  
  請參閱 docs.jamf.com 上 [Integrating with Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) (與 Microsoft Intune 整合) 中的 *Configuring macOS Intune Integration* (設定 macOS Intune 整合) 一節。 

#### <a name="cause-3"></a>原因 3

**使用者沒有有效的 Intune 或 Jamf 授權**  

  缺少有效授權可能導致下列錯誤，該錯誤指出 Jamf 授權已過期：  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **解決方法**
  - Jamf 授權：請連絡 Jamf 尋求協助，以取得新的 Jamf 授權。  
  - Intune 授權：將有效的授權指派給使用者，或連絡 Microsoft 或合作夥伴，以取得如何取得目前授權的資訊。

#### <a name="cause-4"></a>原因 4  

**使用者並未使用 *Jamf Self Service* 來啟動公司入口網站應用程式**

若要透過 Jamf 讓裝置成功註冊且向 Intune 登錄，則使用者必須使用 Jamf Self Service 來開啟 Intune 公司入口網站。 若使用者手動開啟公司入口網站，則裝置即會在沒有連線到 Jamf 的情況下註冊及登錄。  

若要判斷裝置用來註冊及登錄的服務，請在裝置上查看公司入口網站應用程式。 透過 Jamf 登錄時，您應該會收到通知來要求開啟 Self-Service 應用程式以進行變更。

在公司入口網站應用程式中，使用者可能會看到 **`Not registered`** ，且在公司入口網站記錄中，可能會出現與下列範例相似的項目：  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**解決方法**  
將登錄來源從 Intune 變更為 Jamf：
1. [從 Intune 取消註冊 macOS 裝置](https://docs.microsoft.com/mem/intune/user-help/unenroll-your-device-from-intune-macos)。 為了避免使並未完全從 Intune 中移除的裝置變得更為複雜，請參閱原因清單中的[原因 6  ](#cause-6)。  

2. 在裝置上，使用 Jamf Self Service 開啟公司入口網站應用程式，然後使用 Intune 註冊裝置。 這項工作需要[已使用 Jamf 部署 macOS 的公司入口網站應用程式](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro)，且[已在 Jamf Pro 中建立原則，向 Azure AD 登錄使用者裝置](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory)。  

3. 入口網站開啟時，所看到的第一個畫面即會提示您進行登入。 使用公司或學校帳戶  

4. 公司入口網站會確認您的帳戶資訊，並顯示您的裝置註冊和裝置合規性狀態。 黃色三角形醒目提示您需要採取以保護學校或公司用 macOS 裝置的動作。 按一下 [開始] 開始註冊。  

5. 如果出現提示，請鍵入您電腦的登入資訊。  
     
註冊裝置管理可能需要幾分鐘的時間。 在此期間，您可以在裝置上執行其他事項。 完成公司存取設定之後，您會收到一則訊息，讓您知道已完成。

#### <a name="cause-5"></a>原因 5  

**Intune 整合已關閉**

若 Intune 整合已關閉，使用者即會在嘗試登錄裝置時，於公司入口網站中收到包含下列訊息的彈出式視窗：  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

Jamf Pro 伺服器會在整合關閉時傳送脈衝到 Intune 伺服器，告知其 Intune 整合已停用。 

**解決方法**  
在 Jamf Pro 內重新啟用 Intune 整合。 請參閱[在 Jamf Pro 中設定 Microsoft Intune 整合](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro)。


#### <a name="cause-6"></a><a name="cause-6"></a>原因 6  

**裝置先前已在 Intune 中註冊，或使用者多次嘗試登錄裝置**

若裝置已從 Jamf 取消註冊，但並未正確地從 Intune 中移除，或使用者多次嘗試進行登錄，您即會在入口網站中看到相同裝置的多個執行個體。 這會導致 Jamf 註冊失敗。

**解決方法**  
1. 在 Mac 上，啟動**終端機**。
2. 執行 **sudo JAMF removemdmprofile**。
3. 執行 **sudo JAMF removeFramework**。
4. 在 JAMF Pro 伺服器上，刪除電腦的清查記錄。
5. 從 AzureAD 刪除裝置。
6. 刪除裝置上的下列檔案 (若存在的話)：
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Microsoft 工作階段傳輸金鑰 (公開與私密金鑰)
   - Microsoft Workplace Join 金鑰 (公開與私密金鑰)
7. 從裝置上的 keychain 移除任何參考 *Microsoft*、*Intune*，或「公司入口網站」  的項目，包括 DeviceLogin.microsoft.com 憑證。 移除除 JAMF 公開和私密金鑰以外的 *JAMF* 參考。 
   > [!IMPORTANT]  
   > 移除公開和私密金鑰會中斷裝置註冊。

8. 刪除任何所找到的下列項目：  
   - 種類：應用程式密碼；帳戶：com.microsoft.workplacejoin.thumbprint
   - 種類：應用程式密碼；帳戶：com.microsoft.workplacejoin.registeredUserPrincipalName
   - 種類：憑證；發行者：MS-Organization-Access
   - 種類：身分識別喜好設定；名稱 (ADFS STS URL (若有的話))： https://adfs\<DNSName>.com/adfs/ls
   - 種類：身分識別喜好設定；名稱： https://enterpriseregistration.windows.net
   - 種類：身分識別喜好設定；名稱： https://enterpriseregistration.windows.net/  
9. 重新啟動 Mac 裝置。
10. 從裝置解除安裝公司入口網站。
11. 請前往 portal.manage.microsoft.com 並刪除所有 Mac 裝置的執行個體。 等待至少 30 分鐘，再前往下一個步驟。
12. 在 JAMF Pro 中重新註冊裝置。
13. 重新開啟 Self Service 並啟動登錄原則。


#### <a name="cause-7"></a>原因 7  

**JamfAAD 從使用者的 keychain 中要求存取「Microsoft Workplace Join 金鑰」**

在登錄期間，macOS 裝置的使用者會收到下列提示，要求允許 JamfAAD 存取其 keychain 中的金鑰： 

```
   JamfAAD wants to access key "Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the "login" keychain password
```

**解決方法**  
為了成功向 Azure AD 登錄裝置，Jamf 會要求使用者提供其帳戶密碼，並選取 [允許]  。

這項要求與本文稍早[在開啟應用程式時 Mac 裝置出現提示，要求進行 keychain 登入](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app)的請求相似。  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Mac 裝置在 Intune 中顯示符合規範，但在 Azure 中卻顯示不符合規範  

**原因**：下列情況可能會導致裝置在 Intune 中顯示為符合規範，但在 Azure 中卻顯示不符合規範：  
- 裝置並未正確登錄。  
- 裝置在沒有進行必要清除的情況下多次登錄。

**解決方法**  
若要解決此問題，請遵循本文稍早＜裝置無法登錄＞  的[原因 6  ](#cause-6) 解決方案。 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Intune 主控台中出現使用 Jamf 註冊 Mac 裝置的重複項目  
 
**原因**：裝置向 Intune 登錄多次，通常是從 Intune 移除後重新登錄所致。  

從 Intune 和 Jamf Pro 整合中移除裝置時，可能會留下一些資料，其會導致後續的登錄建立重複項目。  

**解決方法**  
若要解決此問題，請遵循本文稍早＜裝置無法登錄＞  的[原因 6  ](#cause-6) 解決方案。 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>合規性政策無法評估裝置  

**原因**：Jamf 與 Intune 的整合不支援以裝置群組為目標的合規性政策。 

**解決方法**  
為要指派給使用者群組的 macOS 裝置修改合規性政策。 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>無法擷取 Microsoft Graph API 的存取權杖

您會收到下列錯誤：

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

此錯誤的來源可能是下列其中一個原因： 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Azure 中的 Jamf Pro 應用程式發生權限問題

在 Azure 中登錄 Jamf Pro 應用程式時，發生了下列其中一個狀況：  
- 應用程式收到超過一個權限。
- 未選取 [ ***\<your 公司 >*** ] 選項的 [授與系統管理員同意]。  

**解決方法**  
請參閱本文稍早[裝置無法登錄](#devices-fail-to-register)原因 1 的解決方案。

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Jamf-Intune 整合所需要的授權已過期

**解決方案**：請參閱本文稍早[裝置無法登錄](#devices-fail-to-register)原因 3 的解決方案。 

#### <a name="the-required-ports-arent-open-on-your-network"></a>必要的連接埠並未在網路上開啟

**解決方案**：檢閱將 Jamf Pro 與 Intune 整合[先決條件](conditional-access-integrate-jamf.md#prerequisites)中的網路連接埠資訊。


## <a name="next-steps"></a>後續步驟
深入了解[將 Jamf Pro 與 Intune 整合](conditional-access-integrate-jamf.md)