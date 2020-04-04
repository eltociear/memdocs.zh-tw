---
title: 針對 Microsoft Intune 中的 Windows 裝置註冊問題進行疑難排解
titleSuffix: Microsoft Intune
description: 針對在 Intune 中註冊 Windows 裝置時的一些最常見問題進行疑難排解的建議。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 04bc86ff697ed7083cacd552cbf9ebe5096a228c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326875"
---
# <a name="troubleshoot-windows-device-enrollment-problems-in-microsoft-intune"></a>針對 Microsoft Intune 中的 Windows 裝置註冊問題進行疑難排解

此文章可協助 Intune 管理員了解在 Intune 中註冊 Windows 裝置時的問題，並進行疑難排解。

## <a name="prerequisites"></a>先決條件
開始疑難排解之前，請務必先收集一些基本資訊。 此資訊可協助您進一步了解問題，並縮短尋找解決方案的時間。

收集與問題相關的下列資訊：
- 是否已將有效的 Intune 授權指派給使用者？ 使用者必須先獲指派所需的授權，才可以註冊其裝置。
- Windows 裝置上是否已安裝最新的更新？ Intune 中的某些功能僅適用於最新版本的 Windows。 Windows Update 提供了許多已知問題的修正。 套用所有最新的更新通常可修正 Windows 裝置註冊問題。 
- 確切錯誤訊息為何？
- 您會在哪裡看到錯誤訊息？
- 問題何時開始發生？ 註冊成功了嗎？ 
- 哪個平台 (Android、iOS/iPadOS、Windows) 有問題？
- 有多少使用者受到影響？ 所有使用者都受到影響，還是只有部分使用者受到影響？
- 有多少裝置受到影響？ 所有裝置都受到影響，還是只有部分裝置受到影響？
- 什麼是 MDM 授權單位？
- 如何執行註冊？ 是「攜帶您自己的裝置」(BYOD)，還是使用註冊設定檔的 Apple 自動裝置註冊 (ADE)？

## <a name="error-messages"></a>錯誤訊息

### <a name="this-user-is-not-authorized-to-enroll"></a>此使用者無權註冊。

錯誤 0x801c003：「此使用者無權註冊。 您可以再試一次，或連絡您的系統管理員，並告知錯誤碼 (0x801c0003)。」
錯誤 80180003：「發生問題。 此使用者無權註冊。 您可以再試一次，或連絡您的系統管理員，並告知錯誤碼 80180003。」

**原因：** 下列任何一情況： 

- 使用者已註冊 Intune 中允許的裝置數目上限。    
- 裝置已由裝置類型限制封鎖。    
- 電腦正在執行 Windows 10 家用版。 不過，只有在 Windows 10 專業版與更新版本上，才支援註冊 Intune 或加入 Azure AD。

#### <a name="resolution"></a>解決方案
此問題有幾種可能的解決方式：

##### <a name="remove-devices-that-were-enrolled"></a>移除已註冊的裝置
1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。    
2. 前往 [使用者]   > [所有使用者]  。    
3. 選取受影響的使用者帳戶，然後按一下 [裝置]  。    
4. 選取任何未使用或不想要的裝置，然後按一下 [刪除]  。 

##### <a name="increase-the-device-enrollment-limit"></a>提高裝置註冊限制

> [!NOTE]
> 這個方法會提高所有使用者的裝置註冊限制，而不只是受影響的使用者。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 移至 [裝置]   > [註冊限制]   > [預設值]  \(在 [裝置限制]  下\) > [屬性]   > [編輯]  \([裝置限制]  旁\) > 提高 [裝置限制]  \(最高 15\) > [檢閱並儲存]  。    
 

##### <a name="check-device-type-restrictions"></a>檢查裝置類型限制
1. 使用全域管理員帳戶登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 移至 [裝置]   > [註冊限制]  ，然後在 [裝置類型限制]  下選取 [預設]  限制。    
3. 選取 [平台]  ，然後針對 [Windows (MDM)]  選取 [允許]  。

    > [!IMPORTANT]
    > 如果目前的設定已經是 [允許]  ，請將其變更為 [封鎖]  並儲存設定，然後再將其變更回 [允許]  並儲存設定。 這會重設註冊設定。

4. 等候約 15 分鐘，然後再次註冊受影響的裝置。    

##### <a name="upgrade-windows-10-home"></a>升級 Windows 10 家用版
[將 Windows 10 家用版升級至 Windows 10 專業版](https://support.microsoft.com/help/12384/windows-10-upgrading-home-to-pro)或更新版本。 



### <a name="this-user-is-not-allowed-to-enroll"></a>不允許此使用者註冊。

錯誤 0x801c0003：「不允許此使用者註冊。 您可以再試一次，或連絡您的系統管理員，並告知錯誤碼 801c0003。」

**原因：** [使用者可以將裝置加入 Azure AD]  設定設為 [無]  。 這可防止新使用者將其裝置加入 Azure AD。 因此，Intune 註冊會失敗。

#### <a name="resolution"></a>解決方案
1. 以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com/)。    
2. 移至 [Azure Active Directory]   > [裝置]   > [裝置設定]  。    
3. 將 [使用者可以將裝置加入 Azure AD]  設定為 [全部]  。    
4. 重新註冊裝置。   

### <a name="the-device-is-already-enrolled"></a>已註冊該裝置。

錯誤 8018000a：「發生問題。 已註冊該裝置。  您可以連絡系統管理員，並告知錯誤碼 8018000a。」

**原因：** 下列其中一個條件成立：
- 不同的使用者已在 Intune 中註冊裝置，或已將裝置加入至 Azure AD。 若要判斷是否為這種情況，請移至 [設定]   > [帳戶]   > [公司存取]  。 尋找與下列類似的訊息：「系統上有其他使用者已經連線到公司或學校。 請移除該公司或學校連線，然後再試一次。」    

#### <a name="resolution"></a>解決方案

使用下列方法來解決此問題：

##### <a name="remove-the-other-work-or-school-account"></a>移除其他公司或學校帳戶
1. 登出 Windows，然後使用已註冊或已加入裝置的其他帳戶登入。    
2. 移至 [設定]   > [帳戶]   > [公司存取]  ，然後移除工作或學校帳戶。
3. 登出 Windows，然後使用您的帳戶登入。    
4. 在 Intune 中註冊裝置，或將裝置加入至 Azure AD。 



### <a name="this-account-is-not-allowed-on-this-phone"></a>此電話不允許此帳戶。

錯誤：「此電話不允許此帳戶。 請確定您提供的資訊正確，然後再試一次，或向您的公司要求支援。」

**原因：** 嘗試註冊裝置的使用者沒有有效 Intune 授權。

#### <a name="resolution"></a>解決方案
將有效的 Intune 授權指派給使用者，然後註冊裝置。


### <a name="looks-like-the-mdm-terms-of-use-endpoint-is-not-correctly-configured"></a>似乎未正確設定 MDM 使用規定端點。

**原因：** 下列其中一個條件成立： 
 - 您在租用戶上同時使用適用於 Office 365 與 Intune 的行動裝置管理 (MDM)，而嘗試註冊裝置的使用者沒有有效的 Intune 授權或 Office 365 授權。     
- Azure AD 中的 MDM 條款及條件為空白或未包含正確的 URL。    

#### <a name="resolution"></a>解決方案

若要修正此問題，請使用下列任一種方法： 
 
##### <a name="assign-a-valid-license-to-the-user"></a>指派有效的授權給使用者
移至 [Microsoft 365 系統管理中心](https://admin.microsoft.com)，然後將 Intune 或 Office 365 授權指派給使用者。

##### <a name="correct-the-mdm-terms-of-use-url"></a>更正 MDM 使用規定 URL
  1. 登入 [Azure 入口網站](https://portal.azure.com/)，然後選取 [Azure Active Directory]  。    
  2. 選取 [行動性 (MDM 與 MAM)]  ，然後按一下 [Microsoft Intune]  。    
  3. 選取 [還原預設的 MDM URL]  ，確認 [MDM 使用規定 URL]  已設定為 **https://portal.manage.microsoft.com/TermsofUse.aspx** 。    
  4. 選擇 [儲存]  。    


### <a name="something-went-wrong"></a>發生問題。

錯誤 80180026：「發生問題。 確認您使用了正確的登入資訊，且您的組織確有使用此功能。 您可以再試一次，或連絡您的系統管理員，並告知錯誤碼 80180026。」

**原因：** 當嘗試將 Windows 10 電腦加入至 Azure AD，且下列兩個條件都成立時，就會發生此錯誤： 
- Azure 中已啟用 MDM 自動註冊。    
- Windows 10 電腦上已安裝 Intune 電腦用戶端 (Intune 電腦代理程式)。

#### <a name="resolution"></a>解決方案
使用下列其中一個方法來解決此問題：

##### <a name="disable-mdm-automatic-enrollment-in-azure"></a>停用 Azure 中的 MDM 自動註冊。
1. 登入 [Azure 入口網站](https://portal.azure.com/)。    
2. 移至 [Azure Active Directory]   > [行動性 (MDM 與 MAM)]   > [Microsoft Intune]  。    
3. 將 [MDM 使用者範圍]  設定為 [無]  ，然後按一下 [儲存]  。    
     
##### <a name="uninstall"></a>解除安裝
從電腦解除安裝 Intune 電腦用戶端代理程式。    

### <a name="the-software-cannot-be-installed"></a>無法安裝軟體。

錯誤：「無法安裝軟體，0x80cf4017。」

**原因：** 用戶端軟體已過期。

#### <a name="resolution"></a>解決方案
1. 登入 [https://admin.manage.microsoft.com](https://admin.manage.microsoft.com)。    
2. 移至 [管理員]   > [用戶端軟體下載]  ，然後按一下 [下載用戶端軟體]  。    
3. 儲存安裝套件，然後再安裝用戶端軟體。 


### <a name="the-account-certificate-is-not-valid-and-may-be-expired"></a>帳戶憑證無效，而且可能已經過期。

錯誤：「此帳戶憑證無效，而且可能已經過期，0x80cf4017。」

**原因：** 用戶端軟體已過期。

#### <a name="resolution"></a>解決方案
1. 登入 [https://admin.manage.microsoft.com](https://admin.manage.microsoft.com)。    
2. 移至 [管理員]   > [用戶端軟體下載]  ，然後按一下 [下載用戶端軟體]  。    
3. 儲存安裝套件，然後再安裝用戶端軟體。    

### <a name="your-organization-does-not-support-this-version-of-windows"></a>您的組織不支援此版本的 Windows。 

錯誤：「發生問題。 您的組織不支援此版本的 Windows。  (0x80180014)」

**原因：** Intune 租用戶中的 Windows MDM 註冊已停用。

#### <a name="resolution"></a>解決方案
若要在獨立的 Intune 環境中修正此問題，請遵循下列步驟： 
 
1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]   > [註冊限制]  > 選擇裝置類型限制。    
2. 針對 [Windows (MDM)]  ，選擇 [屬性]   > [編輯]  \(在 [平台設定]  旁\) > [允許]  。    
3. 按一下 [檢閱並儲存]  。    

### <a name="a-setup-failure-has-occurred-during-bulk-enrollment"></a>大量註冊期間發生安裝程式失敗。

**原因：** 不允許個別佈建套件的帳戶套件 (Package_GUID) 中 Azure AD 使用者帳戶將裝置加入至 Azure AD。 當您使用 Windows 設定設計工具 (WCD) 或「設定學校電腦」應用程式來設定佈建套件時，系統會自動建立這些 Azure AD 帳戶，而這些帳戶會接著用來將裝置加入 Azure AD。

#### <a name="resolution"></a>解決方案
1. 以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com/)。    
2. 移至 [Azure Active Directory] > [裝置] > [裝置設定]  。    
3. 將 [使用者可以將裝置加入 Azure AD]  設定為 [全部]  或 [已選取]  。

   如果您選擇 [已選取]  ，請按一下 [已選取]  ，然後按一下 [新增成員]  ，以將可加入其裝置的所有使用者新增至 Azure AD。 確定已新增佈建套件的所有 Azure AD 帳戶。
 
如需如何為 Windows 設定設計工具建立佈建套件的詳細資訊，請參閱[建立適用於 Windows 10 的佈建套件](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-create-package) \(部分機器翻譯\)。

如需「設定學校電腦」應用程式的詳細資訊，請參閱[使用「設定學校電腦」應用程式](https://docs.microsoft.com/education/windows/use-set-up-school-pcs-app) \(部分機器翻譯\)。


### <a name="auto-mdm-enroll-failed"></a>自動 MDM 註冊：Failed 

當您嘗試使用「群組原則」自動註冊 Windows 10 裝置時，您遇到下列問題： 
- 在工作排程器的 [Microsoft]   > [Windows]   > [EnterpriseMgmt]  下，[由註冊用戶端建立的排程，用於從 AAD 自動註冊 MDM]  工作的最後執行結果如下：**事件 76 自動 MDM 註冊：失敗 (未知的 Win32 錯誤碼：0x8018002b)**       
- 在事件檢視器中，下列事件會記錄在**應用程式及服務記錄檔/Microsoft/Windows/DeviceManagement-Enterprise-Diagnostics-Provider/Admin** 底下：   
    ```asciidoc
    Log Name: Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider/Admin
    Source: DeviceManagement-Enterprise-Diagnostics-Provider
    Event ID: 76
    Level: Error
    Description: Auto MDM Enroll: Failed (Unknown Win32 Error code: 0x80180002b)
    ```
**原因：** 下列其中一個條件成立： 
- UPN 包含未驗證或無法路由傳送的網域，例如 .local (如 joe@contoso.local)。    
- [MDM 使用者範圍]  設定為 [無]  。 

#### <a name="resolution"></a>解決方案
如果 UPN 包含未驗證或無法路由傳送的網域，請遵循下列步驟： 

1. 在執行 Active Directory Domain Services (AD DS) 的伺服器上，在 [執行]  對話方塊中輸入 **dsa.msc**，然後按一下 [確定]  ，以開啟 [Active Directory 使用者及電腦]  。    
2. 按一下您網域底下的 [使用者]  ，然後執行下列動作：  
    - 如果只有一個受影響的使用者，請在使用者上按一下滑鼠右鍵，然後按一下 [內容]  。 在 [帳戶]  索引標籤上 [使用者登入名稱]  底下的 UPN 尾碼下拉式清單中，選取有效的 UPN 尾碼，例如 contoso.com，然後按一下 [確定]  。    
    - 如果有多個受影響的使用者，請選取使用者，然後在 [動作]  功能表中按一下 [內容]  。 在 [帳戶]  索引標籤上，選取 [UPN 尾碼]  核取方塊，在下拉式清單中選取有效的 UPN 尾碼 (例如 contoso.com)，然後按一下 [確定]  。
3. 等候下次同步處理，或在已提高權限的 PowerShell 提示字元中執行下列命令，從同步處理伺服器強制執行差異同步處理：
    ```powershell
    Import-Module ADSync
    Start-ADSyncSyncCycle -PolicyType Delta
    ```

如果 [MDM 使用者範圍]  設定為 [無]  ，請遵循下列步驟： 
 
1. 登入 [Azure 入口網站](https://portal.azure.com/)，然後選取 [Azure Active Directory]  。
2. 選取 [行動性 (MDM 與 MAM)]  ，然後選取 [Microsoft Intune]  。    
3. 將 [MDM 使用者範圍]  設定為 [全部]  。 或者，將 [MDM 使用者範圍]  設定為 [部分]  ，然後選取可以自動註冊其 Windows 10 裝置的群組。    
4. 將 [MAM 使用者範圍]  設定為 [無]  。


### <a name="an-error-occurred-while-creating-autopilot-profile"></a>建立 Autopilot 設定檔時發生錯誤。

**原因：** 裝置名稱範本的指定命名格式不符合需求。 例如，您針對序列巨集使用小寫，例如 %serial% 而不是 %SERIAL%。

#### <a name="resolution"></a>解決方案

確定命名格式符合下列需求：

- 為您的裝置建立唯一名稱。 名稱必須是 15 個字元或更少，而且可以包含字母 (a-z、A-Z)、數字 (0-9) 與連字號 (‐)。
- 名稱不可以全部為數字。
- 名稱不能包含空格。
- 使用 %SERIAL% 巨集新增硬體特定序號。 或者，使用 %RAND:<位數>% 巨集來新增隨機的數字字串，該字串包含 <位數> 位數。 例如，MYPC-%RAND:6% 會產生 MYPC-123456 之類的名稱。

### <a name="something-went-wrong-oobeidps"></a>發生問題。 OOBEIDPS。

**原因：** 如果有 Proxy、防火牆或其他網路裝置封鎖對識別提供者 (IdP) 的存取，就會發生此問題。

#### <a name="resolution"></a>解決方案
確定不會封鎖 Autopilot 其網際網路服務的必要存取權。 如需詳細資訊，請參閱 [Windows Autopilot 網路需求](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements-network) \(部分機器翻譯\)。


### <a name="registering-your-device-for-mobile-management-failed3-0x801c03ea"></a>正在註冊您的裝置以進行行動管理 (失敗: 3，0x801C03EA)。

**原因：** 裝置具有支援 2.0 版但尚未升級至 2.0 版的 TPM 晶片。

#### <a name="resolution"></a>解決方案
將 TPM 晶片升級至 2.0 版。

如果問題持續發生，請檢查相同的裝置是否在兩個指派的群組中，而且各群組都獲指派不同的 Autopilot 設定檔。 如果它是在兩個群組中，請決定應套用至裝置的 Autopilot 設定檔，然後移除另一個設定檔的指派。

如需有關如何使用 Autopilot 在 kiosk 模式中部署 Windows 裝置的詳細資訊，請參閱[使用 Windows Autopilot 部署 kiosk](https://blogs.technet.microsoft.com/mniehaus/2018/06/07/deploying-a-kiosk-using-windows-autopilot/) \(英文\)。


### <a name="securing-your-hardware-failed-0x800705b4"></a>保護硬體 (失敗：0x800705b4)。

錯誤 800705b4： 
```
Securing your hardware (Failed: 0x800705b4)
Joining your organization's network (Previous step failed)
Registering your device for mobile management (Previous step failed)
```

**原因：** 目標 Windows 裝置不符合下列任一需求：

- 裝置必須具有實體 TPM 2.0 晶片。 具有虛擬 TPM (例如 Hyper-V VM) 或 TPM 1.2 晶片的裝置無法在自我部署模式下使用。
- 裝置必須執行下列其中一個 Windows 版本：
    - Windows 10 組建 1703 或更新版本。
    - 如果使用混合式 Azure AD Join，則為 Windows 10 組建 1809 或更新版本。


#### <a name="resolution"></a>解決方案
確定目標裝置符合「原因」  一節中所述的兩個需求。

如需有關如何使用 Autopilot 在 kiosk 模式中部署 Windows 裝置的詳細資訊，請參閱[使用 Windows Autopilot 部署 kiosk](https://blogs.technet.microsoft.com/mniehaus/2018/06/07/deploying-a-kiosk-using-windows-autopilot/) \(英文\)。


### <a name="something-went-wrong-error-code-80070774"></a>發生問題。 錯誤碼koError Code 80070774。

錯誤 0x80070774：發生問題。 確認您使用了正確的登入資訊，且您的組織確有使用此功能。 您可以再試一次，或連絡您的系統管理員，並告知錯誤碼 80070774。

當裝置在初始登入畫面期間逾時時，通常會在混合式 Azure AD Autopilot 情節中重新啟動裝置之前發生此問題。 這表示因為連線問題，所以找不到或無法成功連線到網域控制站。 或者，裝置已進入無法加入網域的狀態。

**原因：** 最常見的原因是正在使用混合式 Azure AD Join，且已在 Autopilot 設定檔中設定 [指派使用者] 功能。 使用 [指派使用者] 功能會在初始登入畫面期間，於裝置上執行 Azure AD 加入，讓裝置處於無法加入內部部署網域的狀態。 因此，[指派使用者] 功能只應用於標準 Azure AD Join Autopilot 情節。  混合式 Azure AD Join 情節中不應使用此功能。

此錯誤的另一個可能原因是已刪除 Autopilot 物件的相關聯 AzureAD 裝置。 若要解決此問題，請刪除 Autopilot 物件，然後重新匯入雜湊來產生新物件。

#### <a name="resolution"></a>解決方案

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 > [裝置]   > [Windows]   > [Windows 裝置]  。
2. 選取發生問題的裝置 > 按一下最右側的省略符號。
3. 選取 [取消指派使用者]  ，並等候程序完成。
4. 請先確認已指派混合式 Azure AD Autopilot 設定檔，再重新嘗試 OOBE。

#### <a name="second-resolution"></a>第二個解決方案
如果問題持續發生，請在裝載離線網域加入 Intune 連接器的伺服器上，檢查 ODJ 連接器服務記錄內是否已記錄事件識別碼 30312。 事件 30312 看起來像下面這樣：

```
Log Name:      ODJ Connector Service
Source:        ODJ Connector Service Source
Event ID:      30132
Level:         Error
Description:
{
          "Metric":{
                   "Dimensions":{
                             "RequestId":"<RequestId>",
                             "DeviceId":"<DeviceId>",
                             "DomainName":"contoso.com",
                             "ErrorCode":"5",
                             "RetryCount":"1",
                              "ErrorDescription":"Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation",
                              "InstanceId":"<InstanceId>",
                              "DiagnosticCode":"0x00000800",
                              "DiagnosticText":"Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation [Exception Message: \"DiagnosticException: 0x00000800. Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation\"] [Exception Message: \"Failed to call NetProvisionComputerAccount machineName=<ComputerName>\"]"
                   },
                   "Name":"RequestOfflineDomainJoinBlob_Failure",
                   "Value":0
          }
}
```

此問題的原因通常是因為不正確地將權限委派給建立 Windows Autopilot 裝置的組織單位。 如需詳細資訊，請參閱[提高組織單位中的電腦帳戶限制](windows-autopilot-hybrid.md#increase-the-computer-account-limit-in-the-organizational-unit)。

1. 開啟 [Active Directory 使用者和電腦 (DSA.msc)]  。
2. 以滑鼠右鍵按一下您將用來建立混合式 Azure AD 聯結電腦的組織單位 > [委派控制]  。
3. 在 [委派控制精靈]  中，選取 [下一步]   > [新增]   > [物件類型]  。
4. 在 [物件類型]  窗格中，選取 [電腦]  核取方塊 > [確定]  。
5. 在 [選取使用者、電腦或群組]    窗格的 [輸入要選取的物件名稱]  方塊中，輸入要安裝連接器的電腦名稱。
6. 選擇 [檢查名稱]  以驗證您的項目 > [確定]   > [下一步]  。
7. 選取 [建立自訂工作來委派]   > [下一步]  。
8. 選取 [只有在這個資料夾內的下列物件]  核取方塊，然後依序選取 [電腦物件]  、[將選取的物件建立到這個資料夾中]  和 [刪除在這個資料夾中選取的物件]  核取方塊。
9. 選取 [下一步]  。
10. 在 [權限]  下，選取 [完全控制]  核取方塊。 此動作會選取所有其他選項。
11. 選取 [下一步]   > [完成]  。

### <a name="the-enrollment-status-page-times-out-before-the-sign-in-screen"></a>[註冊狀態] 頁面在登入畫面之前逾時

**原因：** 如果下列所有情況都成立，就會發生此問題：
- 您正在使用註冊狀態頁面來追蹤商務用 Microsoft Store 應用程式。
- 您有一個需要將裝置標記為符合規範之控制項的 Azure AD 條件式存取原則。
- 此原則適用於所有雲端應用程式與 Windows。

#### <a name="resolution"></a>解決方案：
嘗試執行下列任一作業：
- 將 Intune 合規性政策的目標設定為裝置。 確定您可以在使用者登入之前判斷合規性。
- 針對市集應用程式使用離線授權。 如此一來，Windows 用戶端就不需要在判斷裝置合規性之前先聯繫 Microsoft Store。

## <a name="next-steps"></a>後續步驟

- [疑難排解 Intune 的裝置註冊問題](troubleshoot-device-enrollment-in-intune.md)
- [在 Intune 論壇中發問](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [查看 Microsoft Intune 支援小組部落格](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess) \(英文\)
- [查看 Microsoft Enterprise Mobility 與安全性小組部落格](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210) \(英文\)
- [取得 Microsoft Intune 支援](../fundamentals/get-support.md)
- [尋找共同管理註冊錯誤](https://docs.microsoft.com/configmgr/comanage/how-to-monitor#enrollment-errors)
