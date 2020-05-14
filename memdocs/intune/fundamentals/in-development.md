---
title: 開發中 - Microsoft Intune
titleSuffix: ''
description: 正在開發的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906964"
---
# <a name="in-development-for-microsoft-intune"></a>Microsoft Intune 正在開發的項目

為了協助您整備及規劃，此頁面會列出正在開發，但尚未發行的 Intune UI 更新及功能。 除了此頁面上的資訊之外： 

- 若我們預期您將需要在變更前先行採取動作，我們會在 Office 訊息中心發佈輔助性貼文。
- 當功能進入生產環境時，無論是作為預覽功能還是正式推出，功能描述都會從此頁面移除，並移到[新功能](whats-new.md)頁面。
- 此頁面和[新增功能](whats-new.md)頁面會定期更新。 請回來查看其他更新。
- 請參閱 [Microsoft 365 藍圖](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS)以取得策略性交付與時間表。

> [!NOTE]
> 此頁面反映目前對即將推出版本中 Intune 功能的預期。 日期和個別功能可能會變更。 此頁面不會描述開發中的所有功能。

**RSS 摘要**：將下列 URL 複製並貼上至您的摘要讀取器中，以了解此頁面何時更新：`https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**此文章上次更新日期為上方標題底下所列的日期。**

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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>支援 Mac 版公司入口網站中的多個帳戶<!-- 5779449  -->
macOS 裝置上的公司入口網站現在會快取使用者帳戶，讓登入變得更容易。 使用者在每次啟動應用程式時，不再需要登入公司入口網站。 此外，如果快取了多個使用者帳戶，則公司入口網站會顯示帳戶選擇器，因此使用者不需要輸入其使用者名稱。 

### <a name="auto-update-vpp-available-apps---3640511----"></a>自動更新 VPP 可用的應用程式<!-- 3640511  -->
當**自動應用程式更新**已啟用 VPP 權杖時，將會自動更新發佈為大量採購方案 (VPP) 可用應用程式的應用程式。 目前，VPP 可用的應用程式不會自動更新。 相反地，終端使用者必須前往公司入口網站並在有較新版本可用時重新安裝應用程式。 不過，必要的應用程式目前確實支援自動更新。

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>在公司入口網站中自訂自助裝置動作<!--4393379  -->
您能夠自訂在公司入口網站應用程式和網站中，向使用者顯示的可用自助裝置動作。 若要協助防止非預期的裝置動作，則將可選取 [租用戶系統管理]   > [自訂]   > [建立]   > [隱藏功能]  來設定公司入口網站應用程式的這些設定。 以下是可用的動作：
- 在公司 Windows 裝置上隱藏 [移除]  按鈕。
- 在公司 Windows 裝置上隱藏 [重設]  按鈕。
- 在公司 iOS 裝置上隱藏 [重設]  按鈕。
- 在公司 iOS 裝置上隱藏 [移除]  按鈕。

如需詳細資訊，請參閱[來自公司入口網站的使用者自助裝置動作](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)。

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Azure AD 企業應用程式或 Office Online 應用程式在公司入口網站中的整合傳遞<!--4404429 -->
您將能夠在公司入口網站中切換 ([隱藏]  或 [顯示]  ) Azure AD 企業應用程式或 Office Online 應用程式的顯示。 每個使用者都會從所選 Microsoft 服務看到其整個應用程式的類別目錄。 根據預設，每個額外的應用程式來源都會設定為 [隱藏]  。 這項功能會先在 2005 版的公司入口網站網站中生效，並預期在 Windows、iOS/iPadOS 和 macOS 公司入口網站中提供支援。 請在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內選取 [租用戶系統管理]   > [自訂]  來尋找這個未來的設定。 如需相關資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>從公司入口網站搜尋 Intune 文件<!-- 1736480 -->
您現在可直接從 macOS 應用程式的公司入口網站搜尋 Intune 文件。 在功能表列中，選取 [說明]   > [搜尋]  並輸入搜尋的關鍵字，以快速找到問題的解答。

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>適用於 Android 的公司入口網站引導使用者在工作設定檔註冊之後取得應用程式 <!-- 6103999  -->
我們正在改善公司入口網站中的應用程式內指引，讓使用者能更輕鬆地尋找及安裝應用程式。  使用者在註冊工作設定檔管理之後會看到一則訊息，告知其可在有徽章的 Google Play 版本中找到所建議應用程式。 使用者也會在左側公司入口網站選單中看到新的 [取得應用程式]  連結。 為了讓這些新的和已改善體驗得以完成，將會移除 [應用程式]  索引標籤。 

### <a name="android-company-portal-user-experience---5736084---"></a>Android 公司入口網站使用者體驗<!-- 5736084 -->
在 2005 版的 Android 公司入口網站中，透過應用程式防護原則發出警告、封鎖或抹除的 Android 裝置終端使用者，將會獲得新的使用者體驗。 終端使用者不會看到目前的對話方塊體驗，而是看到完整的頁面訊息，其中說明警告、封鎖或抹除的原因，以及補救問題的步驟。 如需詳細資訊，請參閱 [Android 裝置的應用程式防護體驗](../apps/app-protection-policy.md#app-protection-experience-for-android-devices)和 [Microsoft Intune 的 Android 應用程式防護原則設定](../apps/app-protection-policy-settings-android.md)。


<!-- ***********************************************-->
## <a name="device-configuration"></a>裝置設定

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>在 macOS 裝置上設定系統延伸模組<!-- 6255624  -->
在 macOS 裝置上，您可建立核心延伸模組設定檔，以在核心層級進行設定 ([裝置]   > [組態設定檔]   > [macOS]  (針對平台) > [核心延伸模組]  (針對設定檔))。 Apple 最終會淘汰核心延伸模組，並在未來的版本中以系統延伸模組取代。 系統延伸模組會在使用者空間中執行，而不會授與核心的存取權限。 目標是要提高安全性並提供更多的終端使用者控制，同時限制核心層級的攻擊。 核心延伸模組和系統延伸模組都可供使用者安裝應用程式延伸模組，以擴充作業系統的原生功能。

在 Intune 中，您可同時設定核心延伸模組和系統延伸模組 ([裝置]   > [組態設定檔]   > [macOS]  (針對平台) > [系統延伸模組]  (針對設定檔))。 核心延伸模組適用於 10.13.2 和更新版本。 系統延伸模組則適用於 10.15 和更新版本。 從 macOS 10.15 到 macOS 10.15.4，核心延伸模組和系統延伸模組可並存執行。 

若要了解 macOS 裝置上的核心延伸模組，請參閱[新增 macOS 核心延伸模組](../configuration/kernel-extensions-overview-macos.md)。

適用於：
- macOS 10.15 與更新版本

<!-- ***********************************************-->
## <a name="device-enrollment"></a>裝置註冊

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>「攜帶您自己的裝置」可使用 VPN 進行部署<!--5015344 -->
這項功能可能會延遲。

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>自動裝置同步間隔縮短為 12 小時<!--3077535 -->
針對 Apple 的自動裝置註冊，Intune 與 Apple Business Manager 之間的自動裝置同步間隔將會從 24 小時縮短為 12 小時。 如需同步的詳細資訊，請參閱[同步受控裝置](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices)。

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Hololens 2 裝置的 Autopilot 支援<!--6305220-->
Windows Autopilot 將支援 Hololens 2 裝置。 如需在 Intune 中使用 Autopilot 的詳細資訊，請參閱[使用 Windows Autopilot 在 Intune 中註冊 Windows 裝置](../enrollment/enrollment-autopilot.md)。

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>註冊限制將支援範圍標籤<!--4209550 -->
您能夠將範圍標籤指派給註冊限制。 若要這麼做，請移至 [Microsoft Endpoint Manager系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]   > [註冊限制]   > [建立限制]  。 建立任一類型的限制，且您將看到 [範圍標籤]  頁面。

### <a name="shared-ipads-for-business--6367326---"></a>適用於商務的共用 iPad<!--6367326 -->
您能夠使用 Intune 和 Apple Business Manager 來輕鬆且安全地設定共用的 iPad，以讓多位員工可以共用裝置。 Apple 的[共用 iPad](https://developer.apple.com/education/shared-ipad/)可為多個使用者提供個人化體驗，同時保留使用者資料。 使用者可使用受控 Apple ID，在登入其組織中的任何共用 iPad 之後，存取其應用程式、資料及設定。 共用的 iPad 可與同盟身分識別搭配使用。

若要查看這項功能，請移至 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]   > [iOS]   > [iOS 註冊]   > [註冊方案權杖]  > 選擇權杖** > [設定檔]   > [建立設定檔]   > [iOS]  。 在 [管理設定]  頁面上，選取 [不搭配使用者親和性進行註冊]  ，您就會看到 [共用的 iPad]  選項。

**適用於：** iPadOS 13.4 和更新版本。 此版本新增了對共用 iPad 的暫時工作階段支援，讓使用者可在沒有受控 Apple ID 的情況下存取裝置。 登出時，裝置會清除所有使用者資料，讓裝置立即可供使用，而不需要抹除裝置。 

<!-- ***********************************************-->
## <a name="device-management"></a>裝置管理

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>適用於 BYOD 裝置的 PowerShell 指令碼支援<!-- 1862833  -->
PowerShell 指令碼將支援在 Intune 中已註冊 Azure AD 的裝置。 如需 PowerShell 的詳細資訊，請參閱[在 Intune 的 Windows 10 裝置上使用 PowerShell 指令碼](../apps/intune-management-extension.md)。 此功能不支援執行 Windows 10 家用版的裝置。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 將包含裝置詳細資料記錄<!--6014987  -->
若要取得 Intune 裝置詳細資料記錄，請前往 [報告]   > [Log Analytics]  。 您可讓裝置詳細資料相互關聯，以建置自訂查詢與 Azure 活頁簿。


### <a name="macos-script-support---6376978----"></a>macOS 指令碼支援<!-- 6376978  -->
macOS 的指令碼支援現已正式推出。 此外，我們還將針對使用者指派的指令碼，以及已向 Apple 自動裝置註冊 (先前為裝置註冊計劃) 進行註冊的 macOS 裝置新增支援。 如需詳細資訊，請參閱[在 macOS 裝置上的 Intune 中使用 Shell 指令碼](../apps/macos-shell-scripts.md)。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視及疑難排解

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI 相容性報表範本 V2.0<!-- 636958  -->
系統管理員可將 Power BI 相容性報表範本的版本從 V1.0 更新為 V2.0。 V2.0 將包含改善的設計，以及要呈現為範本一部分的計算和資料變更。 如需相關資訊，請參閱[使用 Power BI 連線至資料倉儲](../developer/reports-proc-get-a-link-powerbi.md)。

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>安全性

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Android 裝置上 DISA Purebred 的衍生認證支援<!--4839592 -->
您將能夠在 Android Enterprise 完全受控裝置上使用 *DISA Purebred* 作為[衍生認證](../protect/derived-credentials.md)提供者 (**租用戶管理** > **連接器和權杖** > **衍生認證**)。 將會包含針對 DISA Purebred 擷取衍生認證的支援。 若應用程式支援，您可以將衍生認證用於應用程式驗證、Wi-Fi、VPN 或 S/MIME 簽署和/或加密。 

Intune 在四月新增了 *Entrust Datacard* 和 *Intercede* 作為衍生認證的提供者。 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>macOS 裝置的隱私權喜好設定<!-- 2934232 --> 
隨著 macOS Catalina 10.15 的發行，Apple 新增了安全性與隱私權的增強功能。 根據預設，應用程式與處理序無法在沒有使用者同意的情況下存取特定資料。 如果未經過使用者同意，則應用程式與處理序可能無法運作。 Intune 將新增設定的支援，可讓 IT 系統管理員在執行 macOS 10.14 和更新版本的裝置上，代表終端使用者允許 (或不允許) 資料存取。 這些設定可確保應用程式與處理序繼續正常運作，並減少終端使用者接收到提示的次數。


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>在端點安全性中複製原則<!-- 5892558   -->
您可在 Microsoft Endpoint Manager 系統管理中心的端點安全性節點中，選取已建立的原則，然後複製該原則以建立複本。  您能夠複製的原則包括針對下列項目所建立原則： 

- 防毒
- 磁碟加密
- 防火牆
- 端點偵測與回應
- 受攻擊面縮小
- 帳戶防護

複製會建立原始原則的複本，您接著可重新命名和編輯該複本。 複本不會包含原始原則的指派。

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>傳送不合規動作的推播通知 <!-- 1733150   -->
針對 iOS 和 Android 平台，我們將為不相容狀況新增動作，該動作會透過公司入口網站應用程式傳送應用程式推播通知。 使用者可按一下通知以啟動公司入口網站應用程式，然後顯示不相容的原因。 系統管理員將能夠在 Microsoft 端點管理員系統管理中心設定這項新動作，前往 [裝置]   > [相容性原則]   > [建立原則]  ，然後選取 [動作]  以傳送應用程式推播通知。 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>端點安全性防火牆原則的新設定檔<!-- 5653324   -->
作為預覽，我們會將 Windows 10 和更新版本的額外設定檔新增至 Intune 端點安全性中防火牆原則 ([端點安全性]   > [防火牆]   > [建立原則]  > 選取 [Windows 10 及更新版本]  )。 

這個新設定檔的每個執行個體最多可支援 150 個自訂「Microsoft Defender 防火牆規則」  。 Microsoft Defender 防火牆規則設定檔可供定義更精細的 Windows 防火牆規則，以允許或封鎖 Windows 10 中的連接埠和應用程式。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>請參閱

如需近期發展的詳細資料，請參閱 [Microsoft Intune 的新功能](whats-new.md)。



