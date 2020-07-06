---
title: 開發中 - Microsoft Intune
titleSuffix: ''
description: 正在開發的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14b571c069fd2484e7e3fd5f2841f6e5884ecc80
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502675"
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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>公司入口網站與 Android 上 Intune 應用程式中的裝置圖示更新<!-- 6057023  -->
我們正在更新公司入口網站與 Android 裝置上 Intune 應用程式中的裝置圖示，以建立更現代化的外觀與風格，並與 Microsoft Fluent Design System 一致。 如需相關資訊，請參閱 [iOS/iPadOS 與 macOS 之公司入口網站應用程式中的圖示更新](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-)。 

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>未註冊受控 iOS 與 Android Enterprise 裝置上 Outlook 的 S/MIME<!-- 6517155  -->
您將能夠在 iOS 與 Android Enterprise 裝置上使用適用於未註冊受控裝置的應用程式設定原則，來啟用 Outlook 的 S/MIME。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選取 [應用程式] > [應用程式設定原則] > [新增] > [受管理的應用程式]。 此外，您可以選擇是否允許使用者在 Outlook 中變更此設定。 如需 Outlook 組態設定的詳細資訊，請參閱 [Microsoft Outlook 組態設定](../apps/app-configuration-policies-outlook.md)。

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS 公司入口網站將會支援 Apple 的自動裝置註冊，而不需要使用者親和性<!-- 7282707  --> 
使用 Apple 的自動裝置註冊註冊的裝置將會支援 iOS 公司入口網站，而不需要已指派的使用者。 終端使用者可以登入 iOS 公司入口網站，在未使用裝置親和性註冊的 iOS/iPadOS 裝置上，將自己建立為主要使用者。 如需自動裝置註冊的詳細資訊，請參閱[使用 Apple 的自動裝置註冊來自動註冊 iOS/iPadOS 裝置](../enrollment/device-enrollment-program-enroll-ios.md)。

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Win32 應用程式安裝通知與公司入口網站<!-- 7485945  -->
終端使用者將能夠決定 [Microsoft Intune Web 公司入口網站](https://portal.manage.microsoft.com/)中所顯示的應用程式應該由公司入口網站應用程式或 Web 公司入口網站開啟。 只有在終端使用者已安裝公司入口網站應用程式，並在瀏覽器之外啟動 Web 公司入口網站應用程式時，才能使用此選項。

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>公司入口網站新增 Configuration Manager 應用程式支援<!-- 4297660 -->
公司入口網站現在支援 Configuration Manager 應用程式。 此功能可讓終端使用者在公司入口網站中查看共同管理之客戶的 Configuration Manager 與 Intune 部署應用程式。 此支援將會協助系統管理員合併不同的終端使用者入口網站體驗。 如需詳細資訊，請參閱[在共同管理的裝置上使用公司入口網站應用程式](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal)。

<!-- ***********************************************-->
## <a name="device-configuration"></a>裝置設定

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>設定第三方 MDM 合作夥伴的裝置合規性狀態<!-- 6361689   -->
擁有協力廠商 MDM 解決方案的 Microsoft 365 客戶將能夠透過整合 Microsoft Intune 裝置合規性服務，以對 iOS 和 Android 上的 Microsoft 365 應用程式強制執行條件式存取原則。 協力廠商 MDM 廠商會利用 Intune 裝置合規性服務，將裝置合規性資料傳送至 Intune。 接著，Intune 會進行評估以判斷裝置是否受信任，並在 Azure AD 中設定條件式存取屬性。  客戶必須在 Microsoft 端點管理員系統管理中心或 Azure AD 入口網站中設定 Azure AD 條件式存取原則。  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Windows 10 與更新版本裝置的新 VPN 設定<!-- 6602122  -->
當您建立使用 IKEv2 連線類型的 VPN 設定檔時，有一些您可以設定的新設定 ([裝置] > [組態設定檔] > [建立設定檔] > [Windows 10 及更新版本] \(針對平台\) > [VPN] \(針對設定檔\) > [基底 VPN])：

- **裝置通道**：允許裝置自動連線至 VPN，而不需要任何使用者互動 (包括使用者登入)。 此功能會要求您啟用 [Always On]，並使用 [電腦憑證] 作為驗證方法。
- 密碼編譯套件設定：設定用來保護 IKE 與子系安全性關聯的演算法，這可讓您使用戶端與伺服器設定相符。

若要查看您可以設定的設定，請移至[針對 Intune 新增 VPN 連線的 Windows 裝置設定](../configuration/vpn-settings-windows-10.md)。

適用於：
- Windows 10 和更新版本

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Android Enterprise 裝置擁有者專用裝置 (COSU) 上受控主畫面的新功能<!-- 7414175 7133328 7133720 7134873 7135184  -->
在 Android Enterprise 裝置上，系統管理員將可以使用裝置組態設定檔，在使用多應用程式 Kiosk 模式的專用裝置上自訂受控主畫面 ([裝置] > [組態設定檔] > [建立設定檔] > 為平台選取 [Android Enterprise] > [僅限裝置擁有者] > 為設定檔選取 [裝置限制] > [裝置體驗])。

具體而言，您可以：

- 自訂圖示、變更螢幕方向，以及在徽章圖示上顯示應用程式通知 <!--7414175-->
- 隱藏受控設定進入點 <!--7133328-->
- 更容易存取偵錯功能表 <!--7133720-->
- 建立已允許的 Wi-Fi 網路清單 <!-- 7134873-->
- 更容易存取裝置資訊 <!-- 7135184-->

如需詳細資訊，請參閱[允許或限制功能的 Android Enterprise 裝置設定](../configuration/device-restrictions-android-for-work.md)。

適用於：

- Android Enterprise 裝置擁有者專用裝置 (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>裝置註冊

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>公司擁有、個人啟用的裝置 (預覽)<!--4442275 -->
Intune 將支援 Android Enterprise 公司擁有且工作設定檔為 OS 版本 Android 8 與更新版本的裝置。 使用工作設定檔的公司擁有裝置是 Android Enterprise 解決方案集中的其中一個企業管理案例。 此案例適用於公司與個人用途的單一使用者裝置。 這個公司擁有、個人啟用 (COPE) 的案例提供：

- 工作與個人設定檔容器化
- 系統管理員的裝置層級控制
- 終端使用者的個人資料與應用程式將維持私用的保證

第一個公開預覽版本將包含在正式推出版本中的功能子集。 會以輪流方式新增額外功能。 第一次預覽中將會提供的功能包括：

- 註冊：系統管理員可以使用不會過期的唯一權杖來建立多個註冊設定檔。 裝置註冊可以透過 NFC、權杖項目、QR 代碼、零接觸或 Knox 行動裝置註冊來完成。
- 裝置設定：現有完全受控和專用裝置設定的子集。
- 裝置合規性：目前適用於完全受控裝置的合規性政策。
- 裝置動作：刪除裝置 (重設成出廠預設值)、將裝置重新開機及鎖定裝置。  
- 應用程式管理：應用程式指派、應用程式設定與相關聯的報告功能 
- 條件式存取



<!-- ***********************************************-->
## <a name="device-management"></a>裝置管理

### <a name="device-compliance-logs-now-in-english--6014904---"></a>裝置合規性記錄現已推出英文版<!--6014904 -->
IntuneDeviceComplianceOrg 記錄只有 ComplianceState、OwnerType 與 DeviceHealthThreatLevel 的列舉。 在未來的更新中，這些記錄在資料行中將會有英文資訊。

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>適用於 BYOD 裝置的 PowerShell 指令碼支援<!-- 1862833  -->
PowerShell 指令碼將支援在 Intune 中已註冊 Azure AD 的裝置。 如需 PowerShell 的詳細資訊，請參閱[在 Intune 的 Windows 10 裝置上使用 PowerShell 指令碼](../apps/intune-management-extension.md)。 此功能不支援執行 Windows 10 家用版的裝置。

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics 將包含裝置詳細資料記錄<!--6014987  -->
若要取得 Intune 裝置詳細資料記錄，請前往 [報告] > [Log Analytics]。 您可讓裝置詳細資料相互關聯，以建置自訂查詢與 Azure 活頁簿。

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

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>macOS 裝置的遠端鎖定動作更新<!--7032805 -->
macOS 裝置的遠端鎖定動作更新將會包含：
- 復原 PIN 會在刪除前顯示 30 天 (而不是七天)。
- 如果系統管理員已開啟第二個瀏覽器，並嘗試從不同的索引標籤或瀏覽器再次觸發命令，Intune 將會允許命令通過。 但是報告狀態會設定為 [失敗]，而不是產生新的 PIN。
- 如果先前的命令仍在擱置中，或裝置未簽入，則系統管理員將無法發出另一個遠端鎖定命令。
這些變更的設計目的是要防止在多個遠端鎖定命令之後覆寫正確的 PIN。

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>將軟體更新部署到 macOS 裝置 <!-- 3194876 -->
您將能夠將軟體更新部署到 macOS 裝置群組。 此功能包括重大、韌體、設定檔與其他更新。 您將能夠在下一次裝置簽入時傳送更新，或選取每週排程，以在您設定的時段內或外部署更新。 當您想要在標準工作時間以外更新裝置時，或當您的技術支援中心人員都在忙碌時，這會很有用。 您也會取得所有已部署更新之 macOS 裝置的詳細報表。 您可以依每個裝置鑽研報表，以查看特定更新的狀態。

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>監視及疑難排解

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>其他資料倉儲 v1.0 屬性<!-- 6125732   -->
其他屬性均可使用 Intune 資料倉儲 v1.0 來取得。 下列屬性現在會透過 [devices](../developer/reports-ref-devices.md#devices) 實體來公開：
- `ethernetMacAddress` - 此裝置的唯一網路識別碼。
- `office365Version` - 安裝於裝置上的 Office 365 版本。

下列屬性現在會透過 [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) 實體來公開：
- `physicalMemoryInBytes` - 實體記憶體 (以位元組為單位)。
- `totalStorageSpaceInBytes`：儲存體容量總計 (以位元組為單位)。

如需詳細資訊，請參閱 [Microsoft Intune 資料倉儲 API](../developer/reports-nav-intune-data-warehouse.md)。

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Power BI 相容性報表範本 V2.0<!-- 636958  -->
系統管理員可將 Power BI 相容性報表範本的版本從 V1.0 更新為 V2.0。 V2.0 將會包含改善的設計，以及要呈現為範本一部分的計算與資料變更。 如需相關資訊，請參閱[使用 Power BI 連線至資料倉儲](../developer/reports-proc-get-a-link-powerbi.md)。

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>角色型存取控制

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>自訂原則的範圍標籤支援<!--6182440 -->
您將能夠將範圍標籤指派給自訂原則。 若要這樣做，請移至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [租用戶管理]> [自訂]，您會在其中看到 [範圍標籤] 設定選項。

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>指派設定檔及更新設定檔權限變更<!--7177586 -->
指派設定檔與更新設定檔的角色型存取控制權限將會變更：
- 指派設定檔：具有此權限的系統管理員也能夠將設定檔指派給權杖，以及將預設設定檔指派給權杖。
- 更新設定檔：有此權限的系統管理員將僅能夠更新現有設定檔。

<!-- ***********************************************-->
## <a name="security"></a>安全性

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Symantec Endpoint Security 與 Check Point Sandblast 的應用程式保護原則支援<!--  4452423, 4731168 -->

在 2019 年 10 月，Intune 應用程式保護原則新增了功能，以使用來自一些 Microsoft Threat Defense 合作夥伴 (MTD 合作夥伴) 的資料。 我們會新增下列合作夥伴的支援，以根據裝置的健康情況，使用應用程式保護原則來封鎖或選擇性地抹除使用者的公司資料：

- Android、iOS 與 iPadOS 上的 **Check Point Sandblast**
- Android、iOS 與 iPadOS 上的 **Symantec Endpoint Security**

如需搭配 MTD 合作夥伴使用應用程式保護原則的相關資訊，請參閱[使用 Intune 建立 Mobile Threat Defense 應用程式防護原則](../protect/mtd-app-protection-policy.md)。

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>在向 Intune 註冊之前，儲存已使用 FileVault 加密 macOS 裝置的修復金鑰<!--5239424   -->
很快地，macOS 裝置如果未由 Intune 的 FileVault 原則加密，或在向 Intune 註冊之前已加密，其終端使用者不需要將裝置解密，Intune 就可以將其重新加密。 相反地，目前的加密可以保持不變，而使用者可以前往公司入口網站網站，他們可以在其中選擇「儲存修復金鑰」以提交其已加密 macOS 裝置的個人修復金鑰。 提交有效金鑰後，Intune 會輪替個人金鑰以產生新金鑰，而使用者仍然可透過公司入口網站網站、iOS/公司入口網站、Android 公司入口網站或 Intune 應用程式來取得新金鑰。 如果使用者的 macOS 裝置遭鎖定，其即可從任何裝置存取那些位置來檢視金鑰。

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>在 macOS FileVault 磁碟加密期間，對裝置使用者隱藏個人修復金鑰<!--  5475632  -->
我們會將名為 [隱藏復原金鑰] 的新設定新增至 FileVault 的端點安全性磁碟加密原則 ([端點安全性] > [磁碟加密] > [建立設定檔] > [macOS] > [FileVault])。 當您啟用新設定時，Intune 會在加密期間，對 macOS 裝置的使用者隱藏個人修復金鑰。 透過在此時隱藏金鑰，您可以協助保護其安全，因為使用者將無法在等候裝置加密時將其寫下。 相反地，如果需要復原，使用者一律可以使用任何裝置透過 Intune 公司入口網站網站來檢視其個人修復金鑰。

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>已改善裝置安全性基準詳細資料的檢視<!-- 5536846   -->
我們正致力於改善安全性基準設定的詳細資料顯示，當您鑽研裝置的詳細資料 ([端點安全性] > [裝置]) 時將可看到。  針對每個已指派的安全性基準，您將能檢視包含每個設定 (包括設定類別、設定名稱，以及該裝置上每個設定的狀態) 的簡單清單。

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>管理使用 Windows 10 裝置端點安全性防毒原則的定義更新來源位置<!-- 6347801  -->  
我們即將在 Windows 10 裝置的端點安全性防毒原則的「更新」類別中新增兩個新設定，其可協助您管理裝置如何取得更新定義 ([端點安全性] > [防毒] > [建立原則] > [Windows 10 及更新版本] > [Microsoft Defender 防毒軟體])。

有了新的設定，您就可以將 UNC 檔案共用新增為定義更新的下載來源位置，並定義連絡不同來源位置的順序。 新設定將會管理下列 Defender CSP：

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources) \(部分機器翻譯\)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder) \(部分機器翻譯\)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>將租用戶連結裝置上線至 MDATP 的端點偵測及回應原則即將移出預覽狀態<!-- 7303816   -->
作為 Intune 中端點安全性的一部分，端點偵測及回應 (EDR) 原則搭配由 Configuration Manager 管理裝置使用的原則，很快就會移出預覽狀態並公開推出 ([端點安全性] > [端點偵測及回應] > [建立原則] > [Windows 10 和 Windows Server])。 當您設定 [Configuration Manager 的租用戶連結](../../configmgr/tenant-attach/device-sync-actions.md)之後，您可以接著使用 EDR 原則，將由 Configuration Manager 管理的裝置上架到 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP)。 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>安全性基準節點的改善<!-- 7433136   -->
為了改善 Microsoft 端點管理員系統管理中心的安全性基準節點的可用性，我們將移除每個基準的 [概觀] 索引標籤，而且將會改為開啟基準 [設定檔] 索引標籤 ([端點安全性] > [安全性基準] > [基準])。

每個基準的 [概觀] 頁面都會顯示圖表與圖格，其會彙總來自您所部署最後一個基準版本的結果。 如果您鑽研版本以取得更多詳細資料，該資訊會與您所看到的內容重複。 移除 [概觀] 頁面之後，當您直接鑽研版本時，那些圖表與彙總詳細資料將維持可用。  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>防火牆規則移轉工具預覽<!-- 6423187  -->
我們正在建置以 PowerShell 為基礎且可用來移轉 Windows Defender 防火牆規則的工具，該工具目前處於公開預覽狀態。 當您安裝並執行該工具時，其會以 Windows 10 用戶端的目前設定為基礎，自動建立 Intune 的端點安全性防火牆規則原則。

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>端點安全性受攻擊面縮小原則中裝置控制設定檔的新設定<!--7032084 -->
我們會將 Windows 10 裝置的數個設定新增至端點安全性 [受攻擊面縮小] 原則的 [裝置控制] 設定檔 ([端點安全性] > [受攻擊面縮小] > [建立原則] > [Windows 10 及更新版本] > [裝置控制])。 

新的設定將會與目前在 [裝置設定] 的[裝置限制設定檔](../configuration/device-restrictions-windows-10.md)中可用的那些設定相同。 要新增至 [裝置控制] 設定檔的設定應該包含各種藍牙設定。  


<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>請參閱

如需近期發展的詳細資料，請參閱 [Microsoft Intune 的新功能](whats-new.md)。
