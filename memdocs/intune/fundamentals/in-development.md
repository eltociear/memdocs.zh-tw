---
title: 開發中 - Microsoft Intune
titleSuffix: ''
description: 正在開發的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5562ef1eaa1cc98e3f5a654e90e4779e228768b6
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311198"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>iOS/iPadOS 與 macOS 公司入口網站 [裝置] 頁面的改善<!-- 6055001  -->
針對 iOS/iPadOS 與 Mac 公司入口網站應用程式的 [裝置] 頁面，我們對使用者體驗做了幾項改善。 我們已重新設計[裝置] 頁面，以提供更現代化的風格與更好的裝置資訊組織方式。 透過使用具有已定義區段標頭的單一欄，貴組織的 iOS/iPadOS 與 macOS 使用者將能夠輕鬆地檢查其裝置的狀態，以確保其安全，並維護其對組織資源的存取權。 此外，我們為裝置不符合規範的使用者加入更清楚的訊息與額外的疑難排解步驟。 如需有關公司入口網站的詳細資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>macOS 版公司入口網站註冊體驗的改善<!-- 6444452  -->
提供 macOS 版公司入口網站註冊體驗將有更簡易註冊程序，其更貼近 iOS 版公司入口網站的註冊體驗。 裝置使用者將會看到：  
- 更時尚的使用者介面。  
- 改善的註冊檢查清單。  
- 更清楚的裝置註冊指示。  
- 改善的疑難排解選項。  

如需有關公司入口網站的詳細資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>使用自發單一應用程式模式設定，將 iOS 公司入口網站設定為登入/登出應用程式<!-- 7055619  -->
您將能夠設定 iOS 公司入口網站使用自發單一應用程式模式 (ASAM)。 您可以使用 Microsoft 端點管理員主控台中的 ASAM 設定，設定 iOS 公司入口網站在登出及登入時進入或移出單一應用程式模式。 當公司入口網站處於 ASAM 中時，使用者將無法使用裝置上的任何其他應用程式或主畫面按鈕，直到他們登入公司入口網站為止。 登出之後，公司入口網站將會返回單一應用程式模式。 

若要在 Microsoft 端點管理員中將公司入口網站設定為 ASAM，請選取 [裝置] > [組態設定檔] > [建立設定檔]。 選取 [iOS/iPadOS] 作為平臺，然後選取 [裝置限制] 作為設定檔。 在 [組態設定] 索引標籤中，選取 [自發單一應用程式模式]。 將 [應用程式名稱] 設定為 `Company Portal`，並將 [應用程式套件組合識別碼] 設定為 `com.app.CompanyPortal`。 如需詳細資訊，請參閱[自發單一應用程式模式 (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) 與[單一應用程式模式](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1)。

<!-- ***********************************************-->
## <a name="device-configuration"></a>裝置設定

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>設定第三方 MDM 合作夥伴的裝置合規性狀態<!-- 6361689   -->
您很快就能在 Azure Active Directory (Azure AD) 中，允許設定由第三方行動裝置管理 (MDM) 合作夥伴所管理之 iOS 或 Android 裝置的合規性狀態。

針對合作夥伴合規性設定 Intune 時，會將由第三方 MDM 合作夥伴所管理之裝置的合規性資料傳送至 Intune 進行合規性評估。 然後會將結果傳遞至 Azure AD，其中會使用合規性資料來強制執行那些裝置的條件式存取原則。

支援即將包含下列合作夥伴：
- VMware WorkspaceONE (先前稱為 AirWatch)

若要啟用裝置合規性合作夥伴，您將在 Microsoft 端點管理員系統管理中心使用新的節點：[租用戶系統管理] > [連接器與權杖] > [合作夥伴合規性管理]，您將在其中選取 [新增合規性合作夥伴]。

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>針對不符合規範，將公司入口網站支援網站的連結新增至電子郵件<!-- 7225498    -->
我們會將新的設定新增至電子郵件通知範本，以將公司入口網站連結新增到電子郵件通知，以傳送給使用不符合規範之裝置的使用者。 ([端點安全性] > [裝置合規性] > [通知] > [建立通知])。  因為有不符合規範之裝置而收到電子郵件的使用者，可以使用此連結來開啟網站，以深入了解其裝置為什麼不符合規範。

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 裝置設定原則的新 FileVault 設定<!-- 5459801   -->
我們將在 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 範本內新增設定至 [FileVault] 類別：隱藏修復金鑰。 ([裝置] > [組態設定檔] > [建立設定檔]，選取 [macOS] 作為「平台」，然後選取 [Endpoint Protection] 作為「設定檔類型」)。 此設定會在 FileVault 2 加密期間隱藏來自終端使用者的個人金鑰。 裝置使用者可以隨時從 iOS 公司入口網站應用程式，或從已加密 macOS 裝置的公司入口網站，查看其個人的修復金鑰。 若要查看個人修復金鑰，使用者可以前往 [裝置詳細資料]，然後按一下「取得修復金鑰」。

此設定不適用於先前建立的原則。 您必須重新建立 FileVault 原則，才能進行並使用此設定。 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>在 macOS 裝置上設定內容快取<!-- 7106872 -->
在 macOS 裝置上，您可以建立組態設定檔以設定內容快取 ([裝置] > [組態設定檔] > [建立設定檔] > [macOS] \(針對平台\) > [裝置功能] \(針對設定檔\))。 使用這些設定來刪除快取、允許共用快取、設定磁碟上的快取限制等等。

如需有關內容快取的詳細資訊，請參閱[內容快取](https://developer.apple.com/documentation/devicemanagement/contentcaching) \(英文\) (會開啟 Apple 的網站)。

若要查看目前您可以設定的設定，請參閱 [Intune 中的 macOS 裝置功能設定](../configuration/macos-device-features-settings.md)。

適用於：
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 與更新版本裝置的新 VPN 設定<!-- 6602122  -->
當您建立使用 IKEv2 連線類型的 VPN 設定檔時，有一些您可以設定的新設定 ([裝置] > [組態設定檔] > [建立設定檔] > [Windows 10 及更新版本] \(針對平台\) > [VPN] \(針對設定檔\) > [基底 VPN])：

- **裝置通道**：允許裝置自動連線至 VPN，而不需要任何使用者互動 (包括使用者登入)。 此功能會要求您啟用 [Always On]，並使用 [電腦憑證] 作為驗證方法。
- 密碼編譯套件設定：設定用來保護 IKE 與子系安全性關聯的演算法，這可讓您使用戶端與伺服器設定相符。

若要查看您可以設定的設定，請移至[針對 Intune 新增 VPN 連線的 Windows 裝置設定](../configuration/vpn-settings-windows-10.md)。

適用於：
- Windows 10 和更新版本

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>封鎖共用的 iPad 裝置上的共用的 iPad 臨時工作階段<!-- 6613794 -->
在 Intune 中，有新的**封鎖共用的 iPad 臨時工作階段**設定可封鎖共用的 iPad 裝置上的臨時工作階段 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] \(針對平台\) > [裝置限制] \(針對設定檔\) > [共用的 iPad])。 啟用時，終端使用者將無法使用來賓帳戶。 他們必須使用其受控 Apple ID 與密碼登入裝置。 

如需您可以設定之設定的詳細資訊，請參閱[允許或限制功能的 iOS 和 iPadOS 裝置設定](../configuration/device-restrictions-ios.md)。

適用於：
- 執行 iOS/iPadOS 13.4 與更新版本的共用的 iPad 裝置

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>使用 Microsoft Launcher 作為完全受控 Android Enterprise 裝置的預設啟動器<!-- 4927976  -->
在 Android Enterprise 裝置擁有者裝置上，您可以將 Microsoft Launcher 設定為完全受控裝置的預設啟動器 ([裝置] > [設定設定檔] > [建立設定檔] > [Android Enterprise] \(針對平台\) > [裝置擁有者] > [裝置體驗] > [裝置限制])。 若要設定所有其他 Microsoft Launcher 設定，請使用應用程式設定原則。 

此外，還有一些其他 UI 更新，包括**專用裝置**已重新命名為**裝置體驗**。

若要查看您可以設定的所有設定，請參閱[使用 Intune 允許或限制功能的 Android Enterprise 裝置設定](../configuration/device-restrictions-android-for-work.md)。 

適用於：
- Android Enterprise 裝置擁有者完全受控裝置 (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>加入新的結構描述設定，並在 Android Enterprise 上使用 OEMConfig 搜尋現有的結構描述設定<!-- 6394386  -->
在 Intune 中，您可以在 Android Enterprise 裝置上使用 OEMConfig 來管理設定 ([裝置] > [組態設定檔] > [建立設定檔] > [Android Enterprise] \(針對平台\) > [OEMConfig] \(針對設定檔\))。 當您使用**設定設計工具**時，會顯示應用程式結構描述中的屬性。 現在，您可以在**設定設計工具**中：
- 將新的設定新增至應用程式結構描述。
- 在應用程式結構描述中搜尋新的與現有的設定。

如需 Intune 中 OEMConfig 設定檔的詳細資訊，請參閱[在 Microsoft Intune 中透過 OEMConfig 來使用和管理 Android Enterprise 裝置](../configuration/android-oem-configuration-overview.md)。

適用於：
- Android 企業

<!-- ***********************************************-->
## <a name="device-enrollment"></a>裝置註冊

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>自動裝置註冊同步錯誤<!-- 6988214 -->
系統會針對 iOS/iPadOS 與 macOS 裝置回報新的錯誤，包括
- 電話號碼中的無效字元，以及該欄位為空的情況。 
- 設定檔無效或空的設定名稱。 
- 無效/已過期的資料指標值，或找不到資料指標的情況。
- 已拒絕或過期的權杖。 
- [部門] 欄位空白或長度太長。 
- Apple 找不到設定檔，而必須建立新設定檔。 
- 已移除的 Apple Business Manager 裝置計數將會新增至概觀頁面，您可以在其中看到裝置的狀態。

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>「攜帶您自己的裝置」可使用 VPN 進行部署<!--5015344 -->
這項功能可能會延遲。

### <a name="shared-ipads-for-business--6367326---"></a>適用於商務的共用 iPad<!--6367326 -->
您能夠使用 Intune 和 Apple Business Manager 來輕鬆且安全地設定共用的 iPad，以讓多位員工可以共用裝置。 Apple 的[共用 iPad](https://developer.apple.com/education/shared-ipad/)可為多個使用者提供個人化體驗，同時保留使用者資料。 使用者可使用受控 Apple ID，在登入其組織中的任何共用 iPad 之後，存取其應用程式、資料及設定。 共用的 iPad 可與同盟身分識別搭配使用。

若要查看此功能，請移至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > [iOS] > [iOS 註冊] > [註冊方案權杖] > 選擇權杖** > [設定檔] > [建立設定檔] > [iOS]。 在 [管理設定] 頁面上，選取 [不搭配使用者親和性進行註冊]，您就會看到 [共用的 iPad] 選項。

**適用於：** iPadOS 13.4 和更新版本。 此版本新增了對共用 iPad 的暫時工作階段支援，讓使用者可在沒有受控 Apple ID 的情況下存取裝置。 登出時，裝置會清除所有使用者資料，讓裝置立即可供使用，而不需要抹除裝置。 

<!-- ***********************************************-->
## <a name="device-management"></a>裝置管理

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>變更共同管理裝置上的主要使用者<!--7319183 -->
您將能夠針對共同管理的 Windows 裝置變更裝置的主要使用者。 如需有關如何尋找並變更主要使用者的詳細資訊，請參閱[尋找 Intune 裝置的主要使用者](../remote-actions/find-primary-user.md)。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>適用於 BYOD 裝置的 PowerShell 指令碼支援<!-- 1862833  -->
PowerShell 指令碼將支援在 Intune 中已註冊 Azure AD 的裝置。 如需 PowerShell 的詳細資訊，請參閱[在 Intune 的 Windows 10 裝置上使用 PowerShell 指令碼](../apps/intune-management-extension.md)。 此功能不支援執行 Windows 10 家用版的裝置。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 將包含裝置詳細資料記錄<!--6014987  -->
若要取得 Intune 裝置詳細資料記錄，請前往 [報告] > [Log Analytics]。 您可讓裝置詳細資料相互關聯，以建置自訂查詢與 Azure 活頁簿。

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>設定 Intune 主要使用者也會設定 Azure AD 擁有者屬性<!--7319227 -->
這個即將推出的功能會在設定 Intune 主要使用者的同時，自動在新註冊的混合式 Azure AD 聯結裝置上設定擁有者屬性。 如需有關主要使用者的詳細資訊，請參閱[尋找 Intune 裝置的主要使用者](../remote-actions/find-primary-user.md)。

這是註冊程序的變更，而且只會套用至新註冊的裝置。 針對現有的混合式 Azure AD 聯結裝置，您必須手動更新 Azure AD 擁有者屬性。 若要這樣做，您可以使用[變更主要使用者功能](../remote-actions/find-primary-user.md#change-a-devices-primary-user)或[指令碼](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)。

當 Windows 10 裝置已加入混合式 Azure Directory 時，裝置的第一個使用者會成為 [端點管理員] 中的主要使用者。  目前，未在對應的 Azure AD 裝置物件上設定使用者。 這會造成比較來自 Azure AD 入口網站的擁有者屬性與 Microsoft 端點管理員系統管理中心的主要使用者屬性時發生不一致的情況。 Azure AD 擁有者屬性是用來保護對 BitLocker 修復金鑰的存取權。 在已加入混合式 Azure AD 的裝置上，不會填寫此屬性。 此限制可防止從 Azure AD 設定 BitLocker 復原的自助服務。 這個即將推出的功能可解決此限制。

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>租用戶連結：系統管理中心中的裝置時間軸<!--7220536, CM7141381 -->
當 Configuration Manager 透過租用戶連結將裝置同步至 Microsoft 端點管理員時，您現在可以看見事件的時間軸。 此時間軸會顯示裝置上過去的活動，協助您進行問題疑難排解。 如需詳細資訊，請參閱 [Configuration Manager 技術預覽版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline)。  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>租用戶連結：從系統管理中心安裝應用程式<!-- 7220536, CM6024389 -->
您現在將能從 Microsoft 端點管理系統管理中心，即時為與租用戶連結的裝置起始應用程式安裝。 如需詳細資訊，請參閱 [Configuration Manager 技術預覽版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps)。

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>租用戶連結：來自系統管理中心的 CMPivot<!--7220536, CM6024392 -->
您將可以把 [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) 的強大功能帶入 Microsoft 端點管理員系統管理中心。 允許其他角色 (例如技術服務人員) 針對個別 ConfigMgr 受控裝置，從雲端起始即時查詢，並將結果傳回給系統管理中心。 這可提供 CMPivot 的所有傳統優點，讓 IT 系統管理員和其他指定的角色能夠快速評估其環境中的裝置狀態並採取行動。 如需詳細資訊，請參閱 [Configuration Manager 技術預覽版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot)。 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>租用戶連結：從系統管理中心執行指令碼<!--7220536, CM6234688 -->
您將可以把 Configuration Manager 內部部署[執行指令碼](../../configmgr/apps/deploy-use/create-deploy-scripts.md)的強大功能帶入 Microsoft 端點管理員系統管理中心。 允許其他角色 (例如技術服務人員) 針對個別的 Configuration Manager 受控裝置，從雲端執行 PowerShell 指令碼。 對於 Configuration Manager 系統管理員已在此新環境中定義並核准的 PowerShell 指令碼，這可提供其所有傳統優點。 如需詳細資訊，請參閱 [Configuration Manager 技術預覽版 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts)。 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>適用於 Windows 10 裝置的新合併邏輯<!--179048-->
今天，如果客戶利用映像重新設定裝置，然後重新註冊裝置，則 Microsoft 端點管理員系統管理主控台中將會出現該裝置的多筆記錄。 我們正在開發新的合併邏輯，以合併 Windows 10 裝置的此類重複記錄。

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>macOS 裝置的遠端鎖定 PIN 可用性<!--7281557-->
macOS 裝置遠端鎖定 PIN 的可用性將從 7 天增加到 30 天。

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
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>請參閱

如需近期發展的詳細資料，請參閱 [Microsoft Intune 的新功能](whats-new.md)。
