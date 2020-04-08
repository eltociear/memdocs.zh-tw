---
title: 開發中 - Microsoft Intune
titleSuffix: ''
description: 正在開發的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f53096f25b4bb05b80d11246ac2fa01486f6e42
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808182"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>Microsoft Intune 正在開發的項目 - 2020 年 4 月

為了協助您整備及規劃，此頁面會列出正在開發，但尚未發行的 Intune UI 更新及功能。 除了此頁面上的資訊之外： 

- 若我們預期您將需要在變更前先行採取動作，我們會在 Office 訊息中心發佈輔助性貼文。
- 當功能進入生產環境時，無論是作為預覽功能還是正式推出，功能描述都會從此頁面移除，並移到[新功能](whats-new.md)頁面。
- 此頁面和[新增功能](whats-new.md)頁面會定期更新。 請回來查看其他更新。
- 請參閱 [Microsoft 365 藍圖](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)以取得策略性交付與時間表。

> [!NOTE]
> 此頁面反映我們目前對未來版本中 Intune 功能的預期。 日期和個別功能可能會變更。 此頁面不會描述開發中的所有功能。

**RSS 摘要**：將下列 URL 複製並貼上至您的摘要讀取器中，以了解此頁面何時更新：`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>應用程式管理

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Android 應用程式設定原則更新<!-- 6113334  -->
即將更新 Android 應用程式設定原則，讓系統管理員能夠在建立應用程式組態設定檔之前，先選取裝置註冊類型。 該功能已新增至註冊類型式 ([工作設定檔] 或 [裝置擁有者]) 的憑證設定檔帳戶中。  此功能發行時，會發生下列情況：

- 在此功能發行前所建立現有原則若沒有任何與該原則建立關聯的憑證設定檔，則會預設為裝置註冊類型的 [工作設定檔] 和 [裝置擁有者設定檔]。
- 在此功能發行前建立的現有原則若具有與其建立關聯的憑證設定檔，則僅會預設為 [工作設定檔]。
- 如果建立新的設定檔，並為裝置註冊類型選取了 [工作設定檔] 和 [裝置擁有者設定檔]，則將無法為憑證設定檔與應用程式設定原則建立關聯。
- 如果已建立新的設定檔，且僅選取 [工作設定檔]，則可以使用在 [裝置設定] 下建立的 [工作設定檔] 憑證原則。
- 如果已建立新的設定檔，且僅選取 [裝置擁有者]，則可以使用在 [裝置設定] 下建立的 [裝置擁有者] 憑證原則。

現有原則將不會修復或發行新的憑證。

此外，我們將會新增 Gmail 與 Nine 電子郵件組態設定檔，這些組態設定檔適用於 [工作設定檔] 和 [裝置擁有者] 註冊類型，包括在這兩個電子郵件設定類型上使用憑證設定檔。  您在 [裝置設定] 的 [工作設定檔] 下所建立所有 Gmail 或 Nine 原則都會繼續套用至裝置，且不需要將其移至應用程式設定原則。

在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可選取 [應用程式]   > [應用程式設定原則]  來尋找應用程式設定原則。 若需要應用程式設定原則的詳細資訊，請參閱 [Microsoft Intune 的應用程式設定原則](../apps/app-configuration-policies-overview.md)。

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft 小組現在已包含在 macOS 版的 Office 365 套件中<!-- 5903936  -->
在 Microsoft 端點管理員中獲指派 macOS 版 Microsoft Office 的使用者，除了現有 Microsoft Office 應用程式 (Word、Excel、PowerPoint、Outlook 以及 OneNote) 之外，也會獲得 Microsoft 小組。 Intune 會辨識已安裝其他 macOS 版 Office 應用程式的現有 Mac 裝置，並會在下次裝置簽入 Intune 時嘗試安裝 Microsoft 小組。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可藉由選取 [應用程式]   > [macOS]   > [新增]  來找到 macOS 版的 **Office 365 套件**。 如需詳細資訊，請參閱[使用 Microsoft Intune 將 Office 365 指派給 macOS 裝置](../apps/apps-add-office365-macos.md)。

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>[自訂] 窗格的群組目標支援 <!-- 4722837  -->
您將能夠在 [自訂] 窗格中，將設定目標設為使用者群組。 從 Intune 入口網站內，選取 [用戶端應用程式]   > [自訂]  。 如需詳細資訊，請參閱 [如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](company-portal-app.md]。

<!-- ***********************************************-->
## <a name="device-configuration"></a>裝置設定

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>適用於 macOS 裝置的有線網路裝置組態設定檔<!-- 3508686  -->
將會可以使用設定有線網路的 macOS 裝置設定檔 ([裝置設定]   > [設定檔]   > [建立設定檔]   > [macOS]  平台 > [有線網路]  設定檔類型)。 使用此功能來建立 802.1x 設定檔以管理有線網路，並將這些有線網路部署至您的 macOS 裝置。

適用於：
- macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>即將更新 Windows 平台的裝置組態設定檔設定和值<!-- 4091122 -->
當您建立 Windows 平台的裝置組態設定檔時 ([裝置]   > [組態設定檔]   > [建立設定檔]  > 任意 [Windows]  平台選項)，部分設定和其值與 CSP 不相同，而可能造成混淆。 即將更新設定名稱和其值，以便更加清楚地表示。

適用於：

- Windows 10 和更新版本裝置組態設定檔
- Windows Holographic for Business 裝置組態設定檔
- Windows 8.1 裝置組態設定檔
- Windows Phone 8.1 裝置組態設定檔

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>設定 macOS 的 Microsoft Defender ATP 應用程式  <!-- 5520115  -->
您即將可以針對以 macOS 作為 Endpoint Protection 裝置組態設定檔一部分執行的裝置，進行 Microsoft Defender ATP 應用程式的[設定](../protect/endpoint-protection-macos.md) ([裝置]   > [組態設定檔]   > [建立設定檔]  ，選取 [macOS]  作為「平台」  ，然後選取 [Endpoint Protection]  作為「設定檔類型」  )。 macOS 裝置設定將會具有八項設定。 

macOS 10.13 (High Sierra) 與更新版本支援 Defender ATP，而 [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) 應用程式必須在套用這些設定「之後」  部署到裝置。 在部署應用程式之前，您需要將這些設定傳送至裝置。 不支援 macOS 的 Beta 版。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 裝置設定原則的新 FileVault 設定<!-- 5459801   -->
我們將在 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 範本內新增設定至 [FileVault] 類別：隱藏修復金鑰。 ([裝置]   > [組態設定檔]   > [建立設定檔]  ，選取 [macOS]  作為「平台」  ，然後選取 [Endpoint Protection]  作為「設定檔類型」  )。 此設定會在 FileVault 2 加密期間隱藏來自終端使用者的個人金鑰。 裝置使用者可以隨時從 iOS 公司入口網站應用程式，或從已加密 macOS 裝置的公司入口網站，查看其個人的修復金鑰。 若要查看個人修復金鑰，使用者可以前往 [裝置詳細資料]，然後按一下「取得修復金鑰」  。

此設定不適用於先前建立的原則。 您必須重新建立 FileVault 原則，才能進行並使用此設定。 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>傳送不合規動作的推播通知 <!-- 1733150   -->
針對 iOS 和 Android 平台，我們將為不合規性新增動作，該動作會透過公司入口網站應用程式傳送應用程式推播通知。 使用者可以按一下 [通知] 以啟動公司入口網站應用程式，然後顯示不符合規範的原因。 系統管理員將能夠在 Microsoft 端點管理員系統管理中心設定這項新動作，前往 [裝置]   > [相容性原則]   > [建立原則]  ，然後選取 [動作]  以傳送應用程式推播通知。

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>受控 Google Play 應用程式發行前測試<!-- 2681933  -->
組織使用[應用程式發行前測試的 Google Play 封閉測試追蹤](https://support.google.com/googleplay/android-developer/answer/3131213)，將能夠使用 Intune 來管理這些追蹤。 您將能夠選擇性地將發佈至 Google Play 生產階段前追蹤的商務營運應用程式指派給試驗群組，以便執行測試。 在 Intune 中，您也可以看到應用程式是否具有已發佈的生產前組建測試追蹤，以及是否能夠將該追蹤指派給 AAD 使用者或裝置群組。 這項功能適用於所有目前支援的 Android Enterprise 案例 (工作設定檔、完全受控以及專用)。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可藉由選取 [應用程式]   > [Android]   > [新增]  來新增受控 Google Play 應用程式。 如需詳細資訊，請參閱[使用 Intune 將受控 Google Play 應用程式新增至 Android Enterprise 裝置](../apps/apps-add-android-for-work.md)。

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>在 Android 上管理 Outlook 的 S/MIME 設定<!-- 6517085   -->
您將能夠使用應用程式設定原則，在執行 Android Enterprise 的裝置上管理 Outlook 的 S/MIME 設定。 您也可以選擇是否允許裝置使用者啟用或停用 Outlook 設定中的 S/MIME。 若要使用 Android 的應用程式設定原則，請在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，前往 [應用程式]   > [應用程式設定原則]   > [新增]   > [受控裝置]  。

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>iOS/iPadOS 裝置上 SSO 和 SSO 應用程式延伸模組設定檔中的其他選項<!-- 6504155  -->
在 iOS/iPadOS 裝置上，您可：

- 在 SSO 設定檔中 ([裝置]   > [組態設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [裝置功能]  作為設定檔 > [單一登入]  )，將 Kerberos 主體名稱設定為 SSO 設定檔中的安全性帳戶管理員 (SAM) 帳戶名稱。 
- 在 SSO 應用程式延伸模組設定檔中 ([裝置]   > [組態設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [裝置功能]  作為設定檔類型 > [單一登入應用程式延伸模組]  )，按幾下滑鼠便能使用新的 SSO 應用程式延伸模組類型設定 iOS/iPadOS Microsoft Azure AD 延伸模組。 您可啟用共用裝置的 Azure AD 延伸模組，並將延伸模組特定的資料傳送至延伸模組。

適用於：
- iOS/iPadOS 13.0+

如需在 iOS/iPadOS 裝置上使用單一登入的詳細資訊，請參閱[單一登入應用程式延伸模組概觀](../configuration/device-features-configure.md#single-sign-on-app-extension)和[單一登入設定清單](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)。

<!-- ***********************************************-->
## <a name="device-enrollment"></a>裝置註冊

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>「攜帶您自己的裝置」可使用 VPN 進行部署<!--5015344 -->
新 Autopilot 設定檔的 [跳過網域連線能力檢查]  切換可供使用自己的第三方 Win32 VPN 用戶端，部署混合式 Azure AD Join 裝置，而不需存取公司網路。 若要查看新的切換，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]    > [Windows]   > [Windows 註冊]   > [部署設定檔]   > [建立設定檔]   > [全新體驗 (OOBE)]  。

<!-- ***********************************************-->
## <a name="device-management"></a>裝置管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>適用於 BYOD 裝置的 PowerShell 指令碼支援<!-- 1862833  -->
PowerShell 指令碼將支援在 Intune 中已註冊 Azure AD 的裝置。 如需 PowerShell 的詳細資訊，請參閱[在 Intune 的 Windows 10 裝置上使用 PowerShell 指令碼](../apps/intune-management-extension.md)。 此功能不支援執行 Windows 10 家用版的裝置。

### <a name="script-support-for-macos-devices---4280361----"></a>macOS 裝置的指令碼支援<!-- 4280361  -->
您將能夠新增指令碼並將其部署至 macOS 裝置。 這項支援可讓您使用 macOS 裝置上的原生 MDM 功能，大幅延伸您能對 macOS 裝置所做的設定。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 將包含裝置詳細資料記錄<!--6014987  -->
若要取得 Intune 裝置詳細資料記錄，請前往 [報告]   > [Log Analytics]  。 您可讓裝置詳細資料相互關聯，以建置自訂查詢與 Azure 活頁簿。

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>裝置擁有權類型變更時的推播通知<!-- 5575875  -->
您可在基於隱私權考量，將裝置擁有權類型從個人變更為公司時，設定傳送推播通知給 Android 與 iOS 公司入口網站使用者。 您可在 Microsoft 端點管理員中找到這項設定，方法為選取 [租用戶管理]   > [自訂]  。 若要深入了解裝置擁有權如何影響終端使用者，請參閱[變更裝置擁有權](../enrollment/corporate-identifiers-add.md#change-device-ownership)。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>安全性

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Android 完全受控裝置上的衍生認證支援<!--4839592-->
您將能夠在 Android Enterprise 完全受控裝置上使用衍生認證。 將會包含針對擷取 Entrust Datacard、Intercede 和 DISA Purebred 衍生認證的支援。 若應用程式支援，您可以將衍生認證用於應用程式驗證、Wi-Fi、VPN 或 S/MIME 簽署和/或加密。

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>macOS 裝置的隱私權喜好設定<!-- 2934232 --> 
隨著 macOS Catalina 10.15 的發行，Apple 新增了安全性與隱私權的增強功能。 根據預設，應用程式與處理序無法在沒有使用者同意的情況下存取特定資料。 如果未經過使用者同意，則應用程式與處理序可能無法運作。 Intune 將新增設定的支援，可讓 IT 系統管理員在執行 macOS 10.14 和更新版本的裝置上，代表終端使用者允許 (或不允許) 資料存取。 這些設定可確保應用程式與處理序繼續正常運作，並減少終端使用者接收到提示的次數。

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>更新了 Windows 10 Endpoint Protection 設定檔設定的 UI 文字與標籤<!-- 5983747 -->
我們將更新 Windows 10 裝置組態設定檔中各種設定的文字，讓您更容易理解這些設定的用途與結果。

我們即將更新的設定會包括 Windows 10 裝置組態設定檔的下列項目：

- [裝置限制](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender 防毒軟體  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender 防毒軟體

Intune 所支援的設定不會變更。 此僅為 Microsoft 端點管理系統管理中心內的 UI 文字更新。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>請參閱

如需近期發展的詳細資料，請參閱 [Microsoft Intune 的新功能](whats-new.md)。



