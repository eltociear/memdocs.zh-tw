---
title: 開發中 - Microsoft Intune
titleSuffix: ''
description: 正在開發的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220127"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Microsoft Intune 正在開發的項目 - 2020 年 3 月

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>iOS 公司入口網站支援橫向模式<!--6048329  -->
使用者將可以自由選擇螢幕方向來註冊其裝置、尋找應用程式，以及取得 IT 支援。 除非使用者將螢幕鎖定在直向模式，否則應用程式會自動偵測並將螢幕調整為直向或橫向模式。

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>改善了 Android 公司入口網站登入體驗<!-- 6103997  -->
我們將更新 Android 公司入口網站應用程式中數個登入畫面的版面配置，讓使用者獲得更加現代化且簡潔的體驗。

<!-- ***********************************************-->
## <a name="device-configuration"></a>裝置設定

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>適用於 macOS 裝置的有線網路裝置組態設定檔<!-- 3508686  -->
將會可以使用設定有線網路的 macOS 裝置設定檔 ([裝置設定]   > [設定檔]   > [建立設定檔]   > [macOS]  平台 > [有線網路]  設定檔類型)。 使用此功能來建立 802.1x 設定檔以管理有線網路，並將這些有線網路部署至您的 macOS 裝置。

適用於：
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>已改善在 iOS/iPadOS 和 macOS 裝置上建立設定檔時的使用者介面體驗<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
當您建立 iOS/iPadOS 或 macOS 裝置的設定檔時，將會更新端點管理員系統管理中心中的體驗。 此變更會影響下列裝置設定檔 ([裝置]   > [設定檔]   > [建立設定檔]   > [iOS]  或 [macOS]  平台)：

- 自訂：iOS/iPadOS、macOS
- 裝置功能：iOS/iPadOS、macOS
- 裝置限制：iOS/iPadOS、macOS
- 端點保護：macOS
- 擴充功能：macOS
- 喜好設定檔案：macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>已改善在 Android Enterprise 裝置上建立 OEMConfig 設定檔時的使用者介面體驗<!-- 5568645   -->
當您建立或編輯 Android Enterprise 裝置的 OEMConfig 設定檔時，端點管理系統管理中心的體驗已更新。 更新的體驗將會針對您已設定的項目提供簡短摘要。 此變更會影響 OEMConfig 裝置設定檔 ([裝置]   > [設定檔]   > [建立設定檔]   > [Android Enterprise]  平台 > [OEMConfig]  設定檔類型)。

本功能適用於：
- Android 企業 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>即將更新 Windows 平台的裝置組態設定檔設定和值<!-- 4091122 -->
當您建立 Windows 平台的裝置組態設定檔時 ([裝置]   > [組態設定檔]   > [建立設定檔]  > 任意 [Windows]  平台選項)，部分設定和其值與 CSP 不相同，而可能造成混淆。 即將更新設定名稱和其值，以便更加清楚地表示。

適用於：

- Windows 10 和更新版本裝置組態設定檔
- Windows Holographic for Business 裝置組態設定檔
- Windows 8.1 裝置組態設定檔
- Windows Phone 8.1 裝置組態設定檔

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>改善了在 Android 與 Android 企業裝置上建立裝置限制設定檔時的使用者介面體驗<!-- 5841361 -->
當您建立 Android 或 Android 企業裝置的設定檔時，將能夠體驗更新的端點管理系統管理中心。 此變更會影響下列裝置組態設定檔 ([裝置]   > [組態設定檔]   > [建立設定檔]   > 選取 [Android 裝置管理員]  或 [Android 企業]  作為平台)：

- 裝置限制：Android 裝置管理員
- 裝置限制：Android Enterprise 裝置擁有者
- 裝置限制：Android Enterprise 工作設定檔

如需您可以設定之裝置限制的詳細資訊，請參閱 [Android 裝置系統管理員](../configuration/device-restrictions-android.md) 和 [Android 企業](../configuration/device-restrictions-android-for-work.md)。

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>設定 macOS 的 Microsoft Defender ATP 應用程式  <!-- 5520115  -->
您即將可以針對以 macOS 作為 Endpoint Protection 裝置組態設定檔一部分執行的裝置，進行 Microsoft Defender ATP 應用程式的[設定](../protect/endpoint-protection-macos.md) ([裝置]   > [組態設定檔]   > [建立設定檔]  ，選取 [macOS]  作為「平台」  ，然後選取 [Endpoint Protection]  作為「設定檔類型」  )。 macOS 裝置設定將會具有八項設定。 

macOS 10.13 (High Sierra) 與更新版本支援 Defender ATP，而 [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) 應用程式必須在套用這些設定「之後」  部署到裝置。 在部署應用程式之前，您需要將這些設定傳送至裝置。 不支援 macOS 的 Beta 版。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 裝置設定原則的新 FileVault 設定<!-- 5459801   -->
我們將在 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 範本內新增設定至 [FileVault] 類別：隱藏修復金鑰。 ([裝置]   > [組態設定檔]   > [建立設定檔]  ，選取 [macOS]  作為「平台」  ，然後選取 [Endpoint Protection]  作為「設定檔類型」  )。 此設定會在 FileVault 2 加密期間隱藏來自終端使用者的個人金鑰。 裝置使用者可以隨時從 iOS 公司入口網站應用程式，或從已加密 macOS 裝置的公司入口網站，查看其個人的修復金鑰。 若要查看個人修復金鑰，使用者可以前往 [裝置詳細資料]，然後按一下「取得修復金鑰」  。

此設定不適用於先前建立的原則。 您必須重新建立 FileVault 原則，才能進行並使用此設定。 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>於下載 Win32 應用程式內容時設定傳遞最佳化代理程式<!-- 5410945  -->
您將能夠設定傳遞最佳化代理程式，以根據指派，在背景或前景模式下載 Win32 應用程式內容。 針對現有的 Win32 應用程式，內容會繼續以背景模式下載。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [應用程式]   > [所有應用程式]   >  選取 [Win32 應用程式]   > [屬性]  。 選取位於 [指派]  旁的 [編輯]  。  在 [必要]  區段中，選取 [模式]  底下的 [包含]  ，以編輯指派。  當新設定可供使用後，即會在 [應用程式設定]  區段中看到新的設定。 如需傳遞最佳化的詳細資訊，請參閱 [Win32 應用程式管理 - 傳遞最佳化](../apps/apps-win32-app-management.md#delivery-optimization)。

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>裝置管理

### <a name="change-primary-user-for-windows-devices----3794742---"></a>變更 Windows 裝置的主要使用者 <!-- 3794742 -->
您將能夠變更 Windows 混合式和 Azure AD 加入裝置的主要使用者。 若要執行此操作，請前往 [Intune]   > [裝置]   > [所有裝置]  > 選擇裝置 > [屬性]   > [主要使用者]  。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>適用於 BYOD 裝置的 PowerShell 指令碼支援<!-- 1862833  -->
PowerShell 指令碼將支援在 Intune 中已註冊 Azure AD 的裝置。 如需 PowerShell 的詳細資訊，請參閱[在 Intune 的 Windows 10 裝置上使用 PowerShell 指令碼](../apps/intune-management-extension.md)。 此功能不支援執行 Windows 10 家用版的裝置。

### <a name="new-information-in-device-details---5604099---"></a>裝置詳細資料中的新資訊<!-- 5604099 -->
下列資訊將顯示於裝置的 [概觀]  頁面上：

- 儲存體容量 (裝置上的實體儲存體總數)
- 記憶體容量 (裝置上的實體記憶體總數)

### <a name="script-support-for-macos-devices---4280361----"></a>macOS 裝置的指令碼支援<!-- 4280361  -->
您將能夠新增指令碼並將其部署至 macOS 裝置。 這項支援可讓您使用 macOS 裝置上的原生 MDM 功能，大幅延伸您能對 macOS 裝置所做的設定。

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
