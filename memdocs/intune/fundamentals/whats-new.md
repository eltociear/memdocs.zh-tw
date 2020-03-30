---
title: Microsoft Intune 的新功能 - Azure | Microsoft Docs
titleSuffix: ''
description: 了解 Intune Azure 入口網站中的新功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d8ff51b8b20c5f6505cb341f666ce043b086b3b
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220178"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune 的新功能

了解每週的 Microsoft Intune 新功能。 您也可以尋找[重要通知](#notices)、[過去的版本](whats-new-archive.md)，以及[如何發佈 Intune 服務更新](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) \(英文\) 的相關資訊。 

> [!Note]
> 每個[每月更新](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) \(英文\) 最多可能需要三天的推出時間，而且將依照下列順序推出：
>
> - 第 1 天：亞太地區 (APAC)
> - 第 2 天：歐洲、中東、非洲 (EMEA)
> - 第 3 天：北美洲
> - 第 4 天+：Intune 政府版
>
> 某些功能可能會在數週內推出，且不會在第一週就提供給所有客戶。
>
> 請檢查[開發中頁面](in-development.md)，以了解某個版本中即將推出的功能清單。

**RSS 摘要**：將下列 URL 複製並貼上至您的摘要讀取器中，以在本頁更新時收到通知：`https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
-->  

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>2020 年 3 月 16 日當週 (2003 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>macOS 與 iOS 公司入口網站更新<!-- 5779439, 5780234  -->
macOS 與 iOS 公司入口網站的 [設定檔] 窗格已更新為包含 [登出] 按鈕。 此外，也已在 macOS 公司入口網站中進行對 [設定檔] 窗格的 UI 改善。 如需公司入口網站的詳細資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>在 iOS 裝置上將 Web 剪輯的目標重新設定為 Microsoft Edge<!-- 5455276   -->
iOS 裝置上新部署的 Web 剪輯 (釘選的 Web 應用程式) 需要在受保護的瀏覽器中開啟，因而將會在 Microsoft Edge (而非 Intune Managed Browser) 中開啟。 您必須為預先存在的 Web 剪輯重定目標，以確保其會在 Microsoft Edge (而非 Intune Managed Browser) 中開啟。 如需詳細資訊，請參閱[透過搭配 Microsoft Intune 使用 Microsoft Edge 來管理 Web 存取](../apps/manage-microsoft-edge.md)和[將 Web 應用程式新增至 Microsoft Intune](../apps/web-app.md)。

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>搭配適用於 Android 的 Microsoft Edge 使用 Intune 診斷工具<!-- 4735244  -->
適用於 Android 的 Microsoft Edge 現在已與 Intune 診斷工具整合。 與適用於 iOS 的 Microsoft Edge 上的體驗類似，在裝置上的 Microsoft Edge URL 列 (網址方塊) 中輸入 "about:intunehelp"，將會啟動 Intune 診斷工具。 此工具將提供詳細的記錄。 系統可以引導使用者收集這些記錄並傳送給 IT 部門，或檢視特定應用程式的 MAM 記錄。

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>更新 Intune 商標和自訂<!-- 5236032  -->
我們已更新名為「商標和自訂」的 Intune 窗格，改善的功能包括：

- 將該窗格重新命名為 [自訂]  。
- 改善設定的配置與設計。
- 改善設定的文字與工具提示。

若要在 Intune 中尋找這些設定，請巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [租用戶系統管理]   > [自訂]  。 如需現有自訂的資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>使用者的個人加密修復金鑰<!-- 6273943  -->
目前提供新的 Intune 功能，可讓使用者透過 Android 公司入口網站應用程式或透過 Android Intune 應用程式，擷取其 Mac 裝置的個人加密 **FileVault** 修復金鑰。 公司入口網站應用程式與 Intune 應用程式中都會提供一個連結，該連結將開啟 Chrome 瀏覽器並連線至 Web 公司入口網站，使用者可在該網站中看到存取其 Mac 裝置所需的 **FileVault** 修復金鑰。 如需加密的詳細資訊，請參閱[搭配 Intune 使用裝置加密](../protect/encrypt-devices.md)。

#### <a name="optimized-dedicated-device-enrollment----6114580-wnready---"></a>已將專用裝置註冊最佳化 <!-- 6114580 wnready -->
我們正在將 Android Enterprise 專用裝置的註冊最佳化，以便能夠更輕鬆地將與 Wi-Fi 相關聯的 SCEP 憑證套用到 2019 年 11 月 22 日前註冊的專用裝置。 針對新註冊，Intune 應用程式將繼續安裝，但終端使用者將不再需要於註冊期間執行**啟用 Intune 代理程式**步驟。 安裝將會在背景中自動進行，而與 Wi-Fi 相關聯的 SCEP 憑證可以在不需與終端使用者互動的情況下進行部署和設定。  

隨著 Intune 服務後端部署，這些變更將在三月的整個月內分階段推出。 所有租用戶都將在三月結束時具備這個新行為。 如需相關資訊，請參閱 [Android Enterprise 專用裝置中的 SCEP 憑證支援](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147) \(英文\)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>在 Windows 裝置上建立系統管理範本時的新使用者體驗<!--5096036 -->
根據客戶的意見反應，以及我們移至新 Azure 全螢幕體驗的進展，我們使用了資料夾檢視來重建系統管理範本設定檔體驗。 我們尚未對任何設定或現有設定檔進行變更。 因此，您現有的設定檔將保持不變，並且將可在新檢視中使用。 您仍然可以選取 [所有設定]  ，然後使用搜尋來瀏覽所有設定選項。 樹狀檢視會依電腦及使用者設定來分割。 您將在相關聯的資料夾中找到 Windows、Office 和 Edge 設定。  

適用於：
- Windows 10 和更新版本

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>使用 IKEv2 VPN 連線的 VPN 設定檔可以搭配 iOS/iPadOS 裝置使用 Always On<!-- 1947932   -->
在 iOS/iPadOS 裝置上，您可以建立使用 IKEv2 連線的 VPN 設定檔 ([裝置]   > [組態設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [VPN]  作為設定檔類型)。 現在，您可以搭配 IKEv2 設定 Always-On。 設定之後，IKEv2 VPN 設定檔會自動連線，並保持連線 (或快速重新連線) 至 VPN。 即使在網路之間移動或將裝置重新開機，仍會保持連線。

在 iOS/iPadOS 上，Always-On VPN 僅限用於 IKEv2 設定檔。

若要查看您可設定的 IKEv2 設定，請前往[在 Microsoft Intune 中於 iOS 裝置上新增 VPN 設定](../configuration/vpn-settings-ios.md#ikev2-settings)。

適用於：
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>在 Android 企業裝置的 OEMConfig 裝置組態設定檔中刪除套件組合與組合陣列<!-- 5550355   -->
在 Android Enterprise 裝置上，您會建立並更新 OEMConfig 設定檔 ([裝置]   > [組態設定檔]   > [建立設定檔]   > [Android Enterprise]  作為平台 > [OEMConfig]  作為設定檔類型)。 使用者現在能夠使用 Intune 中的 [設定設計工具]  來刪除套件組合與套件組合陣列。

如需 OEMConfig 設定檔的詳細資訊，請參閱[在 Microsoft Intune 中透過 OEMConfig 來使用和管理 Android Enterprise 裝置](../configuration/android-oem-configuration-overview.md)。

適用於：
- Android 企業

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>設定 iOS/iPadOS Microsoft Azure AD SSO 應用程式延伸模組<!-- 5672534   -->
Microsoft Azure AD 小組已建立重新導向的單一登入 (SSO) 應用程式延伸模組，讓 iOS/iPadOS 13.0+ 的使用者能夠使用單一登入來存取 Microsoft 應用程式和網站。 先前使用 Microsoft Authenticator 應用程式進行代理驗證的所有應用程式，都將繼續透過新的 SSO 延伸模組來取得 SSO。 透過 Azure AD SSO 應用程式延伸模組版本，您可以使用重新導向的 SSO 應用程式延伸模組類型來設定 SSO 延伸模組 ([裝置]   > [組態設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [裝置功能]  作為設定檔類型 > [單一登入應用程式延伸模組]  )。

適用於：
- iOS 13.0 與更新版本
- iPadOS 13.0 和更新版本

如需 iOS SSO 應用程式延伸模組的詳細資訊，請參閱[單一登入應用程式延伸模組](../configuration/device-features-configure.md#single-sign-on-app-extension)。

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>已從 iOS/iPadOS 裝置限制設定檔中移除 [修改企業應用程式信任設定] 設定<!-- 6225131   -->
在 iOS/iPadOS 裝置上，您可以建立裝置限制設定檔 ([裝置]   > [組態設定檔]   > [建立設定檔]   > 選取 [iOS/iPadOS]  作為平台 > 選取 [裝置限制]  作為設定檔類型)。 Apple 已移除 [修改企業應用程式信任設定]  設定，同時也會從 Intune 中移除此設定。 如果您目前在設定檔中使用此設定，則不會有任何影響，而且會從現有設定檔中加以移除。 此設定也會從 Intune 的所有報告中移除。

適用於：
- iOS/iPadOS

若要查看您可以限制的設定，請前往[允許或限制功能的 iOS 和 iPadOS 裝置設定](../configuration/device-restrictions-ios.md)。

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>疑難排解：暫止的 MAM 原則通知已變更為資訊圖示<!--6348954 -->
[疑難排解] 刀鋒視窗上暫止 MAM 原則的通知圖示已變更為資訊圖示。

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>設定合規性政策時的 UI 更新<!-- 3961639    -->
我們已在 Microsoft 端點管理員中更新[建立合規性政策](../protect/create-compliance-policy.md#create-the-policy)的 UI ([裝置]   > [合規性政策]   > [原則]   > [建立原則]  )。 我們提供一個新的使用者體驗，其中包含您先前使用的相同設定和詳細資料。 新體驗會遵循類似精靈的流程來建立合規性政策，並包含可讓您在其中為原則新增「指派」  的新頁面和 [檢閱 + 建立]  頁面，而您可以在建立原則之前，於此頁面檢閱設定。

#### <a name="retire-noncompliant-devices---1827291---------"></a>淘汰不符合規範的裝置<!-- 1827291       -->
我們已為不符合規範的裝置新增一個動作，讓您可新增至任何原則，以[淘汰不符合規範的裝置](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)。  新動作 (**淘汰不符合規範的裝置**) 不僅會從裝置中移除所有公司資料，還會導致 Intune 無法管理該裝置。  此動作會在觸達設定的值 (以天為單位)，且裝置在該時間點變成符合淘汰資格時執行。 最小值為 30 天。  明確的 IT 系統管理員核准必須使用「淘汰不符合規範的裝置」  區段來淘汰裝置，系統管理員可以在該區段中淘汰所有符合條件的裝置。

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>iOS 企業 Wi-Fi 設定檔中的 WPA 與 WPA2 支援<!--6215273   -->
[適用於 iOS 的企業級 Wi-Fi 設定檔](../configuration/wi-fi-settings-ios.md#enterprise-profiles)現在支援 [安全性類型]  欄位。 針對 [安全性類型]  ，您可以選取 [WPA Enterprise]  或 [WPA/WPA2 Enterprise]  ，然後指定 [EAP 類型]  的選取項目。  ([裝置]   > [組態設定檔]   > [建立設定檔]  、選取 [iOS/iPadOS]  作為「平台」  ，然後選取 [Wi-Fi]  作為「設定檔」  )。 

新的企業級選項與可供適用於 iOS 之基本 Wi-Fi 設定檔使用的選項類似。

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>適用於憑證、電子郵件、VPN 及 Wi-Fi、VPN 設定檔的新使用者體驗<!-- 5615208   -->
我們已在端點管理系統管理中心，更新用來建立及修改下列設定檔類型的[使用者體驗](../configuration/device-profile-create.md) ([裝置]   > [組態設定檔]   > [建立設定檔]  )。 新體驗與先前設定相同，但會使用類似精靈的體驗，且不太需要水平捲動。 您不需要修改現有設定也能使用新的體驗。

- 衍生認證
- 電子郵件
- PKCS 憑證
- PKCS 匯入憑證
- SCEP 憑證
- 信任的憑證
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>設定是否可在 Android 與 iOS 公司入口網站中註冊<!-- 4260128  -->
您可以設定在具有提示 (或沒有提示) 的情況下，讓使用者能夠在 Android 與 iOS 裝置的公司入口網站中註冊裝置，或讓使用者無法註冊裝置。 若要在 Intune 中尋找這些設定，請巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [租用戶系統管理]   > [自訂]   > [編輯]   > [裝置註冊]  。  

對裝置註冊設定的支援需要終端使用者具有下列公司入口網站版本：
-    iOS 上的公司入口網站：4.4 版或更新版本
-    Android 上的公司入口網站：5.0.4715.0 或更新版本

如需現有公司入口網站自訂的詳細資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>[Android 裝置概觀] 頁面上的新 Android 報告<!-- 5435435   -->
我們已在 [Android 裝置概觀] 頁面中，將報告新增至 Microsoft 端點管理員系統管理主控台，以顯示每個裝置管理解決方案中已註冊的 Android 裝置數量。 此圖表 (如同 Azure 主控台中已有的相同圖表) 會顯示工作設定檔、完全受控、專用，以及已註冊裝置系統管理員的裝置數量。 若要查看報告，請選擇 [裝置]   > [Android]   > [概觀]  。

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-idready-wnready-wnstaged--"></a>引導使用者從 Android 裝置系統管理員管理至工作設定檔管理<!--5857738 idready wnready wnstaged-->
我們將發行 Android 裝置系統管理員平台的新合規性設定。 此設定可供在裝置由裝置系統管理員管理時，將其設為不符合規範。

在這些不符合規範的裝置上，於 [更新裝置設定]  頁面中，使用者會看到 [移至新的裝置管理安裝程式]  訊息。 如果使用者點選 [解決]  按鈕，系統將引導完成下列動作：

1. 從裝置系統管理員管理取消註冊
2. 在工作設定檔管理中註冊
3. 解決合規性問題 
 
為了透過 Android 企業轉移到更加現代化、豐富且安全的裝置管理，Google 正在減少新 Android 版本中裝置系統管理員的支援。  Intune 只能為執行 Android 10 和更新版本的裝置系統管理員所管理 Android 裝置提供完整支援，且支援僅提供至 2020 年度第 2 季。 在此期間過後，執行 Android 10 或更新版本的裝置系統管理員所管理裝置 (Samsung 除外) 將無法再完全受控。 尤其受影響的裝置不會再收到新密碼要求。 如需詳細資訊，請參閱此[注意事項](#decreasing-support-for-android-device-administrator)。

如需此設定的詳細資訊，請參閱[將 Android 裝置從裝置系統管理員移至工作設定檔管理](../enrollment/android-move-device-admin-work-profile.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>資料倉儲現在提供 MAC 位址<!-- 6123680  -->
Intune 資料倉儲會在 `device` 實體中提供 MAC 位址作為新屬性 (`EthernetMacAddress`)，以允許系統管理員在使用者與主機 MAC 位址之間相互關聯。 此屬性有助於觸達特定使用者，並針對網路上發生的事件進行疑難排解。 系統管理員也可以在 [Power BI 報告](../developer/reports-proc-get-a-link-powerbi.md)中使用此屬性來建置更豐富的報告。 如需詳細資訊，請參閱 Intune 資料倉儲[裝置](../developer/intune-data-warehouse-collections.md#devices)實體。

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>其他資料倉儲裝置庫存屬性<!-- 6125732  -->
其他裝置庫存屬性均可使用 Intune 資料倉儲來取得。 下列屬性現在會透過[裝置](../developer/intune-data-warehouse-collections.md#devices)集合來公開：
- 'Model'：裝置型號。
- 'Office365Version'：安裝於裝置上的 Office 365 版本。
- 'PhysicalMemoryInBytes'：實體記憶體 (以位元組為單位)。
- `TotalStorageSpaceInBytes`：儲存體容量總計 (以位元組為單位)。

如需詳細資訊，請參閱 [Microsoft Intune 資料倉儲 API](../developer/reports-nav-intune-data-warehouse.md) 和 Intune 資料倉儲[裝置](../developer/intune-data-warehouse-collections.md#devices)實體。

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>更新說明及支援工作流程以支援其他服務<!-- 5654170   -->
我們已更新 Microsoft 端點管理員系統管理中心的 [說明及支援] 頁面，現在可在其中[選擇您所使用的管理類型](../fundamentals/get-support.md#options-to-access-help-and-support)。 透過這項變更，您將可以從下列管理類型中選取：

- Configuration Manager (包含電腦分析)
- Intune
- 共同管理

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全性

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>使用安全性系統管理員的焦點原則預覽作為端點安全性的一部分<!--6131401  -->
在公開預覽中，我們已在 Microsoft 端點管理系統管理中心的 [端點安全性] 節點下方新增數個新的原則群組。 身為安全性系統管理員，您可以使用這些新原則，來將焦點放在裝置安全性的特定層面，以管理不同的相關設定群組，而不會產生較大裝置設定原則主體的額外負荷。

除了新的「適用於 Microsoft Defender 防毒軟體的防毒軟體原則」  (請參閱下文) 之外，這其中每個新預覽原則和設定檔的設定，都是您目前可能已經透過[裝置組態設定檔](../configuration/device-profile-create.md)設定的相同設定。

以下是所有處於預覽狀態的新原則類型及其可用的設定檔類型：

- **防毒軟體 (預覽)** ：
  - macOS：
    - **防毒軟體**：管理適用於 macOS 的 [防毒軟體原則設定](../protect/antivirus-microsoft-defender-settings-macos.md)，以管理 [Mac 版 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) \(部分機器翻譯\)。

  - Windows 10 及更新版本：
    - **Microsoft Defender 防毒軟體**：管理雲端保護、防毒軟體的排除項目、補救、掃描選項等[防毒軟體原則設定](../protect/antivirus-microsoft-defender-settings-windows.md)。

      「Microsoft Defender 防毒軟體」  的防毒軟體設定檔是一種例外狀況，其引進了可在裝置限制設定檔中找到的新設定執行個體。 這些新的防毒軟體設定：

        - 與在裝置限制中找到的設定相同，但可針對在設定為裝置限制時無法使用的設定支援第三個選項。
        - 在將適用於 Endpoint Protection 的[共同管理工作負載滑動軸](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)設定為 Intune 時，會套用至與 Configuration Manager 共同管理的裝置。

     規劃使用新的 [防毒軟體]   > [Microsoft Defender 防毒軟體]  設定檔，來替代透過裝置限制設定檔進行設定。

  - **Windows 安全性體驗**：管理終端使用者能在 Microsoft Defender 安全性中心檢視的 Windows 安全性設定及其所收到的通知。 這些設定與可用來作為裝置設定 Endpoint Protection 設定檔的設定一樣。

- **磁碟加密 (預覽)** ：
  - macOS：
    - **FileVault**
  - Windows 10 及更新版本：
    - **BitLocker**
- **防火牆 (預覽)** ：
  - macOS：
    - **macOS 防火牆**
  - Windows 10 及更新版本：
    - **Microsoft Defender 防火牆**
- **端點偵測及回應 (預覽)** ：
  - Windows 10 及更新版本：-**Windows 10 Intune**
- **受攻擊面縮小 (預覽)** ：
  - Windows 10 及更新版本：
    - **應用程式與瀏覽器隔離**
    - **Web 防護**
    - **應用程式控制**
    - **受攻擊面縮小規則**
    - **裝置控制**
    - **惡意探索保護**
- **帳戶保護 (預覽)** ：
  - Windows 10 及更新版本：
    - **帳戶保護**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>2020 年 3 月 9 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>於下載 Win32 應用程式內容時設定傳遞最佳化代理程式<!-- 5410945 -->

您可以設定傳遞最佳化代理程式，以根據指派在背景或前景模式下載 Win32 應用程式內容。 針對現有的 Win32 應用程式，內容會繼續以背景模式下載。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [應用程式]   > [所有應用程式]   >  選取 [Win32 應用程式]   > [屬性]  。 選取位於 [指派]  旁的 [編輯]  。  在 [必要]  區段中，選取 [模式]  底下的 [包含]  ，以編輯指派。  您會在 [應用程式設定]  區段中看到新的設定。 如需傳遞最佳化的詳細資訊，請參閱 [Win32 應用程式管理 - 傳遞最佳化](../apps/apps-win32-app-management.md#delivery-optimization)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>變更 Windows 裝置的主要使用者<!-- 3794742   -->
您可變更 Windows 混合式和 Azure AD 加入裝置的主要使用者。 若要執行此操作，請前往 [Intune]   > [裝置]   > [所有裝置]  > 選擇裝置 > [屬性]   > [主要使用者]  。 如需詳細資訊，請參閱[變更裝置的主要使用者](../remote-actions/find-primary-user.md#change-a-devices-primary-user)。

也已為此工作建立新的 RBAC 授權 (受控裝置/集合主要使用者)。 已將授權新增至內建角色，包括技術服務人員、學校系統管理員和端點安全性管理員。

這項功能會在預覽期間向客戶全面推出。 您應該會在接下來的幾週內看到這項功能。


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>2020 年 3 月 2 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Microsoft 端點管理員租用戶連結：裝置同步及裝置動作<!-- 6317104, CM3555758-->
Microsoft 端點管理員會將設定管理員和 Intune 整合至單一主控台。 從設定管理員技術預覽版 2002.2 版開始，您可以將設定管理員裝置上傳至雲端服務，並在系統管理中心對其採取動作。 如需詳細資訊，請參閱[Configuration Manager Technical Preview 2002.2 版中的功能](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach)。

請先檢閱[Configuration Manager Technical Preview 文章](https://docs.microsoft.com/configmgr/core/get-started/technical-preview)，再安裝此更新。 本文會讓您熟悉使用技術預覽版的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。

#### <a name="bulk-remote-actions--4576882--"></a>大量遠端動作<!--4576882-->
您現在可以針對下列遠端動作發出大量命令：重新啟動、重新命名、AutoPilot 重設、抹除及刪除。 若要查看新的大量動作，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]   > [所有裝置]   > [大量動作]  。

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>改善了所有裝置清單的搜尋、排序以及篩選<!--6179023-->
已改善 [所有裝置] 清單，以獲得更佳的效能、搜尋、排序以及篩選。 如需詳細資訊，請參閱[此支援提示](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946) (英文)。

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>2020 年 2 月 24 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>macOS 公司入口網站使用者體驗改善<!-- 5568987 -->
我們已改善 macOS 裝置註冊體驗與 Mac 的公司入口網站應用程式。 您將看到下列改善：
- 在註冊期間獲得更佳的 Microsoft **自動更新**體驗，可確保使用者擁有最新版公司入口網站。
- 註冊期間增強的合規性檢查步驟。
- 支援複製的事件識別碼，可讓使用者更快速從裝置將錯誤傳送給您的公司支援小組。

如需註冊與 Mac 的公司入口網站應用程式詳細資訊，請參閱[使用公司入口網站應用程式註冊您的 macOS 裝置](../user-help/enroll-your-device-in-intune-macos-cp.md)。

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>適用於 Better Mobile 的應用程式保護原則現在支援 iOS 與 iPadOS<!-- 6224512  -->

在 2019 年 10 月，Intune 應用程式保護原則新增了功能，以使用來自 Microsoft Threat Defense 合作夥伴的資料。 透過這項更新，您現在可以根據在 iOS 與 iPadOS 上使用 Better Mobile 的裝置健全狀況，並藉由應用程式保護原則來封鎖或選擇性地抹除使用者的公司資料。  如需詳細資訊，請參閱[使用 Intune 建立 Mobile Threat Defense 應用程式防護原則](../protect/mtd-app-protection-policy.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>從 [所有裝置] 清單匯出改為壓縮的 CSV 格式<!--6343117-->
現在從 [裝置]   > [所有裝置]  清單匯出已改為壓縮的 CSV 格式。


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>2020 年 2 月 17 日當週 (2002 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>macOS 版 Microsoft Defender 進階威脅防護 (ATP) 應用程式<!-- 5424618 -->
Intune 提供一種簡單的方式，以將適用於 macOS 的 Microsoft Defender 進階威脅防護 (ATP) 應用程式部署至受控 Mac 裝置。 如需詳細資訊，請參閱[使用 Microsoft Intune 將 Microsoft Defender ATP 新增至 macOS 裝置](../apps/apps-advanced-threat-protection-macos.md)，以及[適用於 Mac 的 Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (機器翻譯)。  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>在 iOS 裝置上透過 Cisco AnyConnect VPN 啟用網路存取控制 (NAC)<!-- 4860111  -->
在 iOS 裝置上，您可以建立 VPN 設定檔，並使用不同的連線類型，包含 Cisco AnyConnect ([裝置設定]   > [設定檔]   > [建立設定檔]   > [iOS]  平台 > [VPN]  設定檔類型 > [Cisco AnyConnect]  連線類型)。

您可以透過 Cisco AnyConnect 啟用網路存取控制 (NAC)。 若要使用此功能：

1. 在 [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) (Cisco 身分識別服務引擎系統管理員指南) 中，使用**將 Microsoft Intune 設定為 MDM 伺服器**中的步驟，在 Azure 中設定 Cisco 身分識別服務引擎 (ISE)。
2. 在 Intune 裝置設定檔中，選取 [啟用網路存取控制 (NAC)]  設定。

若要查看所有可用的 VPN 設定，請前往[在 iOS 裝置上進行 VPN 設定](../configuration/vpn-settings-ios.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>[Apple MDM Push Certificate] 頁面上的序號<!--5947765  -->
[Apple MDM Push Certificate] 頁面現在會顯示序號。 如果您無法存取建立憑證的 Apple ID，則需要序號來重新取得 Apple MDM Push Certificate 的存取權。 若要查看序號，請前往 [裝置]   > [iOS]   > [iOS 註冊]   > [Apple MDM Push Certificate]  。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>將 OS 更新推送至已註冊 iOS/iPadOS 裝置的新更新排程選項<!--5879689  -->
為 iOS/iPadOS 裝置的作業系統更新規劃排程時，您將可以選擇下列選項。 這些選項適用於使用 Apple Business Manager 或 Apple School Manager 註冊類型的裝置。
- 在下次簽入時更新
- 在排程時間的期間內更新
- 在排程時間的期間外更新

針對後面兩個選項，您可以建立多個時間範圍。

若要查看新選項，請前往 MEM > [裝置]   > [iOS]   > [iOS/iPadOS 的更新原則]   > [建立設定檔]  。

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>選擇要推送至已註冊裝置的 iOS/iPadOS 更新<!--5879689  -->
您可以選擇特定的 iOS/iPadOS 更新 (除了最新更新之外)，以推送至使用 Apple Business Manager 或 Apple School Manager 註冊的裝置。 這些裝置必須將裝置設定原則設為將軟體更新可見度延遲數天。 若要查看這項功能，請前往 MEM > [裝置]   > [iOS]   > [iOS/iPadOS 的更新原則]   > [建立設定檔]  。



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>裝置安全性

#### <a name="improved-intune-reporting-experience---3791418-----"></a>已改善的 Intune 報告體驗<!-- 3791418   -->
Intune 現在提供已改善的報告體驗，包括新報表類型、更好的報表組織、更聚焦的檢視、已改善的報表功能，以及更一致且即時的資料。 報告體驗將從公開預覽改為 GA (正式版本)。 此外，GA 版本將會提供當地語系化支援、Bug 修正、設計改善、且在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的圖格上彙總裝置合規性資料。

新的報告類型著重於下列資訊：

- **營運** - 提供最新記錄，包含負面健康情況焦點。 
- **組織** - 提供整體狀態的更廣泛摘要。
- **歷程記錄** - 提供一段時間的模式和趨勢。
- **專家** - 可讓您使用未經處理資料來建立您自己的自訂報表。

第一組新報表專注於裝置合規性。 如需詳細資訊，請參閱[部落格 - Microsoft Intune 報告架構](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) \(英文\) 和 [Intune 報表](reports.md)。

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>合併了 UI 中安全性基準的位置<!-- 6177074   -->
我們藉由從數個 UI 位置中移除了「安全性基準」  ，以此合併在 Microsoft 端點管理員系統管理中心尋找[安全性基準](../protect/security-baselines.md)的路徑。 若要尋找安全性基準，您現在可以使用下列路徑：[端點安全性]   > [安全性基準]  。

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>針對匯入的 PKCS 憑證擴大支援<!-- 6044197  -->
我們針對使用[匯入的 PKCS 憑證](../protect/certificates-imported-pfx-configure.md#supported-platforms)擴大了支援，藉以支援「Android Enterprise 完全受控裝置」  。 一般而言，匯入 PFX 憑證會用於 S/MIME 加密案例，其中使用者的所有裝置上都需要其加密憑證，以便進行電子郵件解密。

下列平台支援匯入 PFX 憑證：

- Android - 裝置管理員
- Android Enterprise - 完全受控
- Android Enterprise - 工作設定檔
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>查看裝置的端點安全性設定<!-- 6206460  -->
我們更新了 Microsoft 端點管理員系統管理中心內的選項名稱，以便檢視[適用於特定裝置的端點安全性設定](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)。 此選項已重新命名為 [端點安全性設定]  ，因為其會顯示適用的安全性基準，以及在安全性基準以外建立的其他原則。 在先前，此選項的名稱為「安全性基準」  。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>角色型存取控制

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Intune 角色使用者介面變更即將推出<!--5801612   -->
[Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的使用者介面 > [租用戶系統管理]   >  [角色]  已經變更為更容易使用且直覺的設計。 此體驗提供您現在所使用的相同設定和詳細資料，但新體驗是採用精靈型程序。

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>2020 年 2 月 17 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="microsofts-new-office-app---5859926---"></a>Microsoft 的新增 Office 應用程式<!-- 5859926 -->
Microsoft 的新增 Office 應用程式現已正式推出，可供下載及使用。 Office 應用程式提供合併式的體驗，讓您的使用者可在單一應用程式中任意使用 Word、Excel 和 PowerPoint。 您可以將應用程式保護原則套用至應用程式，以確保所要存取的資料受到保護。

如需詳細資訊，請參閱[如何使用 Office 行動裝置預覽應用程式啟用 Intune 應用程式保護原則](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493) (英文)。

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>2020 年 2 月 10 日當週

### <a name="windows-7-ends-extended-support--3042987---"></a>Windows 7 的延伸支援結束<!--3042987 -->
Windows 7 的延伸支援於 2020 年 1 月 14 日結束。 Intune 也同時淘汰對執行 Windows 7 的裝置支援。 無法再取得協助保護您 PC 的技術協助與自動更新。 您應該升級至 Windows 10。 如需詳細資訊，請參閱[計畫變更部落格文章](https://aka.ms/Windows7_Intune) \(英文\)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Windows 10 裝置上的 Microsoft Edge 77 版與更新版本<!-- 5843584 -->
Intune 現在支援解除安裝 Windows 10 裝置上的 Microsoft Edge 77 版與更新版本。 如需詳細資訊，請參閱[將適用於 Windows 10 的 Microsoft Edge 新增至 Microsoft Intune](../apps/apps-windows-edge.md)。

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>已從公司入口網站 Android 工作設定檔註冊移除畫面<!--6103987 -->
我們已從公司入口網站中的 Android 工作設定檔註冊流程移除 [下一步是什麼?]  畫面，以簡化使用者體驗。 移至[使用 Android 工作設定檔註冊](../user-help/enroll-device-android-work-profile.md)，以查看已更新的 Android 工作設定檔註冊流程。  

#### <a name="company-portal-app-improved-performance---6178652---"></a>公司入口網站應用程式已改進效能<!-- 6178652 -->
公司入口網站應用程式已更新，以支援使用 ARM64 處理器之裝置 (例如 Surface Pro X) 的效能改進。先前，公司入口網站在模擬的 ARM32 模式中運作。 現在，在 10.4.7080.0 和更新版本中，公司入口網站應用程式是針對 ARM64 原生地編譯的。 如需公司入口網站應用程式的詳細資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>2020 年 1 月 27 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>適用於 macOS 其他 Microsoft Edge 77 版部署通道的 Intune 支援<!-- 5983950  -->
Microsoft Intune 現在支援適用於 macOS 的 Microsoft Edge 應用程式的其他 [穩定]  部署通道。 [穩定]  通道是在企業環境中廣泛部署 Microsoft Edge 的建議通道。 其會每六週更新一次，每個版本都會納入來自 [Beta]  通道的改良功能。 除了 [穩定]  與 [Beta]  通道，Intune 也支援 [Dev]  通道。 公開預覽提供適用於 macOS 的 Microsoft Edge 77 版與更新版本的 [穩定] 與 [Dev] 通道。 瀏覽器的自動更新預設為 [開啟]。 如需詳細資訊，請參閱[使用 Microsoft Intune 將 Microsoft Edge 新增至 macOS 裝置](../apps/apps-edge-macos.md)。

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>淘汰 Microsoft Intune Managed Browser<!--5728447 -->
即將淘汰 Intune Managed Browser。 將 Microsoft Edge 用於受保護的 Intune 瀏覽器體驗。 如需詳細資訊，請參閱項目「[採取行動：將 Microsoft Edge 用於受保護的 Intune 瀏覽器體驗](whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience)」(下方的 [通知](whats-new.md#notices) 一節中)。

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>2020 年 1 月 20 日當週 (2001 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>將應用程式新增至 Intune 時的使用者體驗變更<!-- 4705829   -->
當您透過 Intune 新增應用程式時，將會看到新的使用者體驗。 此體驗提供您先前所使用的相同設定與詳細資料，但在將應用程式新增至 Intune 之前，新體驗是採用精靈型程序。 此新體驗也會在新增應用程式之前提供檢閱頁面。 從 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，選取 [應用程式]   > [所有應用程式]   > [新增]  。 如需詳細資訊，請參閱[將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

#### <a name="require-win32-apps-to-restart----5622282-----"></a>要求 Win32 應用程式重新啟動 <!-- 5622282   -->
您可以要求 Win32 應用程式必須在成功安裝後重新啟動。 此外，您也可以選擇必須重新啟動之前的時間量 (寬限期)。

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>在 Intune 中設定應用程式時的使用者體驗變更<!-- 4207990   -->
在 Intune 中建立應用程式設定原則時，您會看到新的使用者體驗。 此體驗提供您先前所使用的相同設定和詳細資料，但在將原則新增至 Intune 之前，新體驗是採用精靈型程序。 從 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，選取 [應用程式]   > [應用程式設定原則]   > [新增]  。 如需詳細資訊，請參閱 [Microsoft Intune 的應用程式設定原則](../apps/app-configuration-policies-overview.md)。 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>適用於 Windows 10 的其他 Microsoft Edge 部署通道的 Intune 支援<!-- 5861774 -->
Microsoft Intune 現在支援適用於 Windows 10 應用程式的 Microsoft Edge (77 版和更新版本) 的其他 [穩定]  部署通道。 [穩定]  通道是在企業環境中廣泛部署適用於 Windows 10 的 Microsoft Edge 的建議通道。 此通道會每六週更新一次，每個版本都會納入 [Beta]  通道的改良功能。 除了 [穩定]  與 [Beta]  通道，Intune 也支援 [Dev]  通道。 如需詳細資訊，請參閱[適用於 Windows 10 的 Microsoft Edge - 設定應用程式設定](../apps/apps-windows-edge.md#configure-app-settings)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>已改進在設定 Exchange ActiveSync 內部部署連接器 UI 時的使用者介面體驗<!-- 5695492   -->
我們已更新[設定 Exchange ActiveSync 內部部署連接器](../protect/exchange-connector-install.md)的體驗。 更新的體驗會使用單一窗格來設定、編輯及摘要說明內部部署連接器的詳細資料。

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>將自動 Proxy 設定新增至 Android Enterprise 工作設定檔的 Wi-Fi 設定檔<!-- 4490822   -->
在 Android Enterprise 工作設定檔裝置上，您可以建立 Wi-Fi 設定檔。 當您選擇 Wi-Fi 企業類型時，您也可以輸入在 Wi-Fi 網路上使用的可延伸的驗證通訊協定 (EAP) 類型。

現在，當您選擇企業類型時，您也可以輸入自動 Proxy 設定，包括 Proxy 伺服器 URL，例如 `proxy.contoso.com`。

若要查看您可以設定的目前 Wi-Fi 設定，[在 Microsoft Intune 中新增適用於執行 Android Enterprise 與 Android kiosk 之裝置的 Wi-Fi 設定](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only)。

適用於：
- Android Enterprise 工作設定檔

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>依裝置製造商封鎖 Android 註冊<!--5197392  -->
您可以根據裝置的製造商來封鎖裝置的註冊。 此功能適用於 Android 裝置系統管理員與 Android Enterprise 工作設定檔裝置。 若要查看註冊限制，請移至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]   > [註冊限制]  。

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>iOS/iPadOS 建立註冊類型設定檔 UI 的改進<!-- 6055005 -->
針對 iOS/iPadOS 使用者註冊，[建立註冊類型設定檔]  [設定]  頁面已簡化，以改進 [註冊類型]  選擇程序，同時維持相同的功能。 若要查看新的 UI，請移至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]   > [iOS]   > [iOS 註冊]   > [註冊類型]   > [建立設定檔]   > [設定]  頁面。 如需詳細資訊，請參閱[在 Intune 中建立使用者註冊設定檔](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="new-information-in-device-details---4471759-5604099----"></a>裝置詳細資料中的新資訊<!-- 4471759 5604099  -->
下列資訊現在位於裝置的 [概觀]  頁面上：
- 記憶體容量 (裝置上的實體記憶體數量)
- 儲存體容量 (裝置上的實體儲存體數量) 
- CPU 架構

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>iOS 略過啟用鎖定遠端動作已重新命名為停用啟用鎖定 <!--5904591  -->
[略過啟用鎖定]  遠端動作已重新命名為 [停用啟用鎖定]  。 如需詳細資訊，請參閱[使用 Intune 停用 iOS 啟用鎖定](../remote-actions/device-activation-lock-disable.md)。

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>適用於 Autopilot 裝置的 Windows 10 功能更新部署支援<!-- 5948137   -->
Intune 現在支援使用 [Windows 10 功能更新部署](../protect/windows-update-for-business-configure.md#windows-10-feature-updates)將 Autopilot 已註冊裝置設為目標。

Windows 10 功能更新原則無法在 Autopilot 全新體驗 (OOBE) 期間套用，而且只會在裝置完成佈建 (通常為一天) 之後、於第一次 Windows Update 掃描時套用。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Windows Autopilot 部署報告 (預覽) <!-- 3856172   -->
新報告會詳細說明透過 Windows Autopilot 部署的每個裝置。 如需詳細資訊，請參閱 [Autopilot 部署報告](../enrollment/enrollment-autopilot.md#autopilot-deployments-report)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>角色型存取控制

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>新的 Intune 內建角色端點安全性管理員<!--4253397   -->
有新的 Intune 內建角色可用：端點安全性管理員。 這個新角色可讓系統管理員擁有 Intune 中端點管理員節點的完整存取權，以及其他區域的唯讀存取權。 角色是 Azure AD「安全性系統管理員」角色的擴充。 如果您目前只有全域管理員作為角色，則不需要做任何變更。 如果您使用角色，並想要端點安全性管理員所提供的細微性，請在該角色可用時指派該角色。 如需有關內建角色的詳細資訊，請參閱[角色型存取控制](role-based-access-control.md)。

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>2020 年 1 月 6 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>iOS 版 Microsoft Outlook 的 S/MIME 支援<!-- 2669398 -->
Intune 支援在 iOS 裝置上傳遞可搭配 iOS 版 Microsoft Outlook 使用的 S/MIME 簽署和加密憑證。 如需詳細資訊，請參閱[適用於 iOS 和 Android 的 Outlook 中敏感度標籤和保護](https://aka.ms/omsmime)。

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>使用 Microsoft 連線快取伺服器來快取 Win32 應用程式內容<!-- 6030314 -->
您可以在 Configuration Manager 發佈點上安裝 Microsoft 連線快取伺服器，來快取 Intune Win32 應用程式內容。 如需詳細資訊，請參閱 [Configuration Manager 中的 Microsoft 連線快取 - Intune Win32 應用程式的支援](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>角色型存取控制

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Windows 10 系統管理範本 (ADMX) 設定檔現已支援範圍標籤 <!--5137390 -->
您現在可以將範圍標籤指派至系統管理範本設定檔 (ADMX)。 若要這麼做，請移至 [Intune]   > [裝置]   > [組態設定檔]  > 在清單中選擇系統管理範本設定檔 > [屬性]   > [範圍標籤]  。 如需範圍標籤的詳細資訊，請參閱[將範圍標籤指派至其他物件](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects)。

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>2019 年 12 月 30 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>從 MEM 加密的 macOS 裝置取出個人修復金鑰<!-- 4851745 -->
終端使用者可以使用 iOS 公司入口網站應用程式來取出其個人修復金鑰 (FileVault 金鑰)。 具有個人修復金鑰的裝置必須向 Intune 註冊，並透過 Intune 以 FileVault 加密。 使用 iOS 公司入口網站應用程式，終端使用者可以按一下 [取得修復金鑰]  ，在其加密的 macOS 裝置上取出其個人修復金鑰。 您也可以透過選取 [裝置]   > *已加密且已註冊的 macOS 裝置* > [取得修復金鑰]  從 Intune 擷取修復金鑰。 如需有關 FileVault 的詳細資訊，請參閱 [macOS 的 FileVault 加密](../protect/encrypt-devices.md#filevault-encryption-for-macos)。

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>iOS 和 iPadOS 使用者授權的 VPP 應用程式<!-- 5619268 -->
針對使用者已註冊的 iOS 和 iPadOS 裝置，將不再向使用者顯示已部署為可用的新建裝置授權 VPP 應用程式。 不過，終端使用者將會繼續查看公司入口網站內所有使用者授權的 VPP 應用程式。 如需與 VPP 應用程式相關的詳細資訊，請參閱[如何使用 Microsoft Intune 管理透過 Apple 大量採購方案購買的 iOS 和 macOS 應用程式](../apps/vpp-apps-ios.md)。

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>2019 年 12 月 23 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>通知 - Windows 10 1703 (RS2) 將退出支援 <!-- 5026679 -->
從 2018 年 10 月 9 日開始，Windows 10 1703 (RS2) 退出了家用版、專業版和工作站專業版的 Microsoft 平台支援。 針對 Windows 10 企業版和教育版，Windows 10 1703 (RS2) 已在 2019 年 10 月 8 日退出平台支援。 從 2019 年 12 月 26 日開始，我們會將 Windows 公司入口網站應用程式的最低版本更新為 Windows 10 1709 (RS3)。 執行 1709 之前版本的電腦將不再從 Microsoft Store 接收應用程式的更新版本。 我們先前已將這項變更傳達給透過訊息中心管理舊版 Windows 10 的客戶。 如需詳細資訊，請參閱 [Windows 生命週期資料表](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>2019 年 12 月 16 日當週

### <a name="device-configuration"></a>裝置設定

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Windows 10 裝置的系統管理範本更新 <!-- 5941568 -->

您可以使用 Microsoft Intune 中的 ADMX 範本來控制和管理 Microsoft Edge、Office 和 Windows 的設定。 Intune 中的系統管理範本會進行下列原則設定更新：

- 已新增 Microsoft Edge 版本 78 和 79 的支援。
- 包含[系統管理範本檔案 (ADMX / ADML) 和 Office 365 ProPlus、Office 2019 和 Office 2016](https://www.microsoft.com/download/details.aspx?id=49030) 中 2019 年 11 月 11 日的 ADMX 檔案。

如需 Intune 中 ADMX 範本的詳細資訊，請參閱[在 Microsoft Intune 中使用 Windows 10 範本設定群組原則設定](../configuration/administrative-templates-windows.md)。

適用於：

- Windows 10 及更新版本

## <a name="week-of-december-9-2019-1912-service-release"></a>2019 年 12 月 9 日當週 (1912 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>移轉到 Microsoft Edge 以進行受控瀏覽案例<!-- 5173762 -->
隨著 Intune Managed Browser 即將淘汰，我們對應用程式防護原則進行了變更，以簡化將使用者移至 Edge 所需的步驟。 我們已將應用程式防護原則設定 [限制使用其他應用程式的 Web 內容傳輸]  中的選項更新為下列其中一項：

- 任何應用程式
- Intune Managed Browser
- Microsoft Edge
- 非受控瀏覽器 

當您選取 [Microsoft Edge]  時，終端使用者會看到條件式存取訊息，通知他們需要 Microsoft Edge才能進行受控瀏覽案例。 如果終端使用者尚未使用自己的 AAD 帳戶下載和登入 Microsoft Edge，也將收到執行此作業的提示。  這相當於以啟用 MAM 的應用程式為目標，並將應用程式組態設定 `com.microsoft.intune.useEdge` 設定為 [True]  。 使用 [受原則管理的瀏覽器]  設定的現有應用程式防護原則現在會選取 **Intune Managed Browser**，且您不會看到任何行為變更。 這表示如果您已將應用程式組態設定 [useEdge]  設定為 [True]  ，則使用者會看到使用 Microsoft Edge 的訊息。 建議利用受控瀏覽案例的所有客戶，都將其應用程式防護原則更新為 [限制使用其他應用程式的 Web 內容傳輸]  ，以確保使用者無論在哪一個應用程式啟動連結，都能看到轉換至 Microsoft Edge 的適當指引。 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>設定組織帳戶的應用程式通知內容<!-- 2576686  -->
Android 和 iOS 裝置上的 Intune 應用程式保護原則 (APP) 可讓您控制組織帳戶的應用程式通知內容。 您可以選取一個選項 ([允許]、[封鎖組織資料] 或 [已封鎖])，來指定要針對所選應用程式顯示組織帳戶通知的方式。 此功能需要應用程式的支援，而且可能不適用所有已啟用 APP 的應用程式。 適用於 iOS 的 Outlook 版本 4.15.0 (或更新版本) 和適用於 Android 的 Outlook 4.83.0 (或更新版本) 將支援此設定。 此設定可在主控台中使用，但該功能將在 2019 年 12 月 16 日之後開始生效。 如需 APP 的詳細資訊，請參閱[什麼是應用程式防護原則？](../apps/app-protection-policy.md)

#### <a name="microsoft-app-icons-update--4677605----"></a>Microsoft 應用程式圖示更新<!--4677605  -->
應用程式保護原則和應用程式設定原則的 [應用程式目標] 窗格中，針對 Microsoft 應用程式使用的圖示已更新。

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>需要在 Android 上使用核准的鍵盤<!--4761794  -->
作為應用程式保護原則的一部分，您可以指定 [**核准的鍵盤**](../apps/app-protection-policy-settings-android.md#data-protection) 設定來管理哪些 Android 鍵盤可以與受控 Android 應用程序一起使用。 當使用者開啟受控應用程式，而且尚未針對該應用程式使用核准的鍵盤時，系統會提示他們切換至裝置上已安裝的其中一個核准的鍵盤。 如有需要，系統會提供連結以從 Google Play 商店下載核准的鍵盤，以供他們安裝和設定。 當使用者的使用中鍵盤不是其中一個核准的鍵盤時，使用者只能編輯受控應用程式中的文字欄位。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>已更新 iOS、iPadOS 和 macOS 裝置上的應用程式和網站的單一登入體驗<!-- 4999578  -->
Intune 已新增更多 iOS、iPadOS 和 macOS 裝置的單一登入 (SSO) 設定。 您現在可以設定由您的組織或您的身分識別提供者所撰寫的重新導向 SSO 應用程式延伸模組。 使用這些設定可以為使用新式驗證方法 (例如 OAuth 和 SAML2) 的應用程式和網站設定順暢的單一登入體驗。 

這些新的設定會展開 SSO 應用程式延伸模組和 Apple 內建 Kerberos 延伸模組先前的設定 ([裝置]   > [裝置設定]   > [設定檔]   > [建立設定檔]   > [iOS/iPadOS]  或 [macOS]  作為平台類型 > [裝置功能]  作為設定檔類型)。 

若要查看您可以設定的 SSO 應用程式延伸模組設定的完整範圍，請移至 [iOS 上的 SSO](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) 和 [macOS 上的 SSO](../configuration/macos-device-features-settings.md#single-sign-on-app-extension)。

適用於：

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>我們已更新適用於 iOS 和 iPadOS 裝置的兩個裝置限制設定，以更正其行為<!-- 5701352    -->
針對 iOS 裝置，您可以建立裝置限制設定檔，以**允許無線 PKI 更新**和**封鎖 USB 受限模式** ([裝置]   > [裝置設定]   > [設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [裝置限制]  作為設定檔類型)。 在此版本之前，下列設定的 UI 設定和描述不正確，而且目前已更正。 從這個版本開始，設定行為如下所示：

**封鎖無線 PKI 更新**：[封鎖]  會防止您的使用者接收軟體更新，除非裝置已連線到電腦。 [未設定]  (預設)：允許裝置在不連線到電腦的情況下接收軟體更新。
- 先前，此設定可讓您將其設定為：[允許]  可讓您的使用者在不將其裝置連線到電腦的情況下接收軟體更新。
**允許裝置鎖定時使用 USB 配件**：[允許]  可讓 USB 配件與鎖定時間超過一小時的裝置交換資料。 [未設定]  (預設) 不會更新裝置上的 USB 受限模式，而且如果超過一小時就會封鎖 USB 配件，使其無法從裝置傳送資料。
- 先前，此設定可讓您將其設定為：[封鎖]  可停用受監督裝置上的 USB 受限模式。

如需您可以設定之設定的詳細資訊，請參閱[使用 Intune 來允許或限制功能的 iOS 和 iPadOS 裝置設定](../configuration/device-restrictions-ios.md)。

本功能適用於：

- iOS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>適用於 macOS 裝置的有線網路裝置組態設定檔<!-- 3508686  -->
   > [!NOTE]
   > 此功能已延後，但即將發行。

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>禁止使用者在 Android Enterprise 裝置擁有者裝置上的受控金鑰儲存區中設定憑證認證<!-- 3311998 -->
在 Android Enterprise 裝置擁有者裝置上，您可以設定新的設定，以封鎖使用者在受控金鑰儲存區中設定其憑證認證 ([裝置設定]   > [設定檔]   > [建立設定檔]   > [Android Enterprise]  作為平台 > [僅限裝置擁有者] > [裝置限制]  作為設定檔類型 > [使用者 + 帳戶]  )。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="protected-wipe-action-now-available--51150000---"></a>受保護的抹除動作現已推出<!--51150000 -->
您現在可以選擇使用 [抹除裝置] 動作來執行裝置的受保護抹除。 受保護的抹除與標準抹除相同，不同之處在於關閉裝置電源時無法規避。 受保護的抹除會繼續嘗試重設裝置，直到成功為止。 在某些設定中，此動作可能會使裝置無法重新啟動。 如需詳細資訊，請參閱[淘汰或抹除裝置](../remote-actions/devices-wipe.md)。

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>裝置乙太網路 MAC 位址已新增至裝置的 [概觀] 頁面<!--5562275 -->
您現在可以在 [裝置詳細資料] 頁面 ([裝置]   > [所有裝置]  > 選擇裝置 > [概觀]  ) 上看到裝置的乙太網路 MAC 位址。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>裝置安全性

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>已改善在啟用裝置型條件式存取原則時共用裝置的體驗<!-- 1734096  -->
藉由在強制執行原則時檢查使用者的最新合規性評估，我們改善了與多個以裝置型條件式存取原則為目標的使用者共用裝置的體驗。 如需詳細資訊，請參閱下列概觀文章：
- [條件式存取的 Azure 概觀](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Intune 裝置合規性概觀](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>使用 PKCS 憑證設定檔，搭配憑證來佈建裝置<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
當與 Wi-Fi 和 VPN 的設定檔建立關聯時，您現在即可使用 PKCS 憑證設定檔，將憑證發行至執行 Android for Work、iOS/iPadOS 和 Windows 的「裝置」  。 先前這三個平台僅支援以使用者型憑證，且裝置型支援僅限於 macOS。

> [!NOTE]
> 不支援搭配 Wi-Fi 設定檔使用 PKCS 憑證設定檔。 當您使用 [EAP 類型](../configuration/wi-fi-settings-windows.md#enterprise-profile)時，請改為使用 SCEP 憑證設定檔。

若要使用裝置型憑證，同時[為支援的平台建立 PKCS 憑證設定檔](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile)，請選取 [設定]  。 您現在會看到 [憑證類型]  的設定，該設定支援 [裝置] 或 [使用者] 的選項。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="centralized-audit-logs--5603185-5697164---"></a>集中式稽核記錄<!--5603185, 5697164 -->
新的集中式稽核記錄體驗現在會將所有類別的稽核記錄收集到單一頁面中。 您可以篩選記錄，以取得您要尋找的資料。 若要查看稽核記錄，請移至 [租用戶管理]   > [稽核記錄]  。 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>稽核記錄活動詳細資料中包含的範圍標籤資訊<!--5763534 -->
稽核記錄活動詳細資料現在包含範圍標籤資訊 (適用於支援範圍標籤的 Intune 物件)。 如需有關稽核記錄的詳細資訊，請參閱[使用稽核記錄追蹤及監視事件](monitor-audit-logs.md)。

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>2019 年 12 月 2 日當週

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>新的 Microsoft Endpoint Configuration Manager 共同管理授權<!--5027281-->
具有軟體保證的 Configuration Manager 客戶可取得適用於 Windows 10 電腦的 Intune 共同管理功能，不需要購買額外的 Intune 授權，即可進行共同管理。 客戶不再需要將個別的 Intune/EMS 授權指派給其終端使用者，即可共同管理 Windows 10。
- Configuration Manager 所管理並已註冊共同管理之裝置的權限，幾乎與 Intune 獨立版 MDM 受控電腦的權限相同。 不過，重設之後，則無法使用 Autopilot 來重新佈建些裝置。
- 使用其他方式在 Intune 中註冊的 Windows 10 裝置需要完整的 Intune 授權。
- 其他平台上的裝至仍然需要完整的 Intune 授權。

如需詳細資訊，請參閱[授權條款](https://www.microsoft.com/en-us/Licensing/product-licensing/products)。

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>2019 年 11 月 18 日當週 (1911 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>選擇性地抹除應用程式資料時的 UI 更新<!-- 4102028 -->
在 Intune 中選擇性地抹除應用程式資料的 UI 已更新。 UI 變更包括：
- 使用壓縮成單一窗格的精靈樣式格式簡化體驗。
- 針對建立流程的更新，以包含指派。
- 檢視屬性 (建立新的原則之前) 或編輯屬性時所設定之所有內容的摘要頁面。 此外，當編輯屬性時，摘要只會顯示正在編輯的屬性類別中的項目清單。

如需詳細資訊，請參閱[如何只抹除 Intune 管理之應用程式中的公司資料](../apps/apps-selective-wipe.md)。

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>iOS 和 iPadOS 協力廠商鍵盤支援<!-- 4922950 -->
在 2019 年 3 月，我們宣布移除「協力廠商鍵盤」iOS 應用程式保護原則。 該功能將回到 Intune，且包含 iOS 和 iPadOS 支援。 若要啟用此設定，請瀏覽新的或現有 iOS/iPadOS 應用程式保護原則的 [資料保護]  索引標籤，並在 [資料傳輸]  底下尋找 [協力廠商鍵盤]  設定。

此原則設定的行為與先前的實作稍有不同。 在使用 SDK 12.0.16 版和更新版本的多重身分識別應用程式中，若該應用程式為應用程式保護原則的目標，且此設定為 [封鎖]  時，終端使用者將無法在其組織和個人帳戶中選擇協力廠商鍵盤。 使用 SDK 12.0.12 版和更早版本的應用程式會繼續表現我們部落格文章標題中記載的行為，[已知問題：在 iOS 中未針對個人帳戶封鎖協力廠商鍵盤](https://aka.ms/3rdparty_iOS_Intune) \(英文\)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>將目標 macOS 使用者群組設定為需要 Jamf 管理<!-- 4061739  --> 
您可以將特定使用者群組作為目標，其 [macOS 裝置會由 Jamf 管理](../protect/conditional-access-integrate-jamf.md)。 這個目標可讓您將 Jamf 合規性整合套用至 macOS 裝置的子集，而其他裝置則會由 Intune 管理。 如果您已經使用 Jamf 整合，則預設會將所有使用者作為整合目標。

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>在 iOS 裝置上建立電子郵件裝置組態設定檔時的新 Exchange ActiveSync 設定<!-- 4892824   --> 
在 iOS/iPadOS 裝置上，您可以在裝置組態設定檔中設定電子郵件連線能力 ([裝置設定]   > [設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [電子郵件]  作為設定檔類型)。 

有新的 Exchange ActiveSync 設定可供使用，包括：
- **要同步的 Exchange 資料**：選擇要同步處理 (或封鎖同步處理) 行事曆、連絡人、提醒事項、便箋和電子郵件的 Exchange 服務。
- **允許使用者變更同步設定**：允許 (或封鎖) 使用者在其裝置上變更這些服務的同步處理設定。  

如需這些設定的詳細資訊，請移至 [Intune 中 iOS 裝置的電子郵件設定檔設定](../configuration/email-settings-ios.md)。 

適用於：

- iOS 13.0 與更新版本
- iPadOS 13.0 和更新版本

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>防止使用者將個人 Google 帳戶新增至 Android Enterprise 完全受控和專用裝置<!-- 5353228   -->
在 Android Enterprise 完全受控和專用的裝置上，有新的設定可防止使用者建立個人 Google 帳戶 ([裝置設定]   > [設定檔]   > [建立設定檔]   >  [Android Enterprise]  作為平台 > [僅限裝置擁有者] > [裝置限制]  作為設定檔類型 > [使用者及帳戶] 設定   > [個人 Google 帳戶]  )。

若要查看您可以設定的設定，請參閱[使用 Intune 來允許或限制功能的 Android Enterprise 裝置設定](../configuration/device-restrictions-android-for-work.md)。

適用於：

- 完全受控的 Android Enterprise 裝置
- Android Enterprise 專用裝置

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>Siri 命令的伺服器端記錄設定已從 iOS/iPadOS 裝置限制設定檔中移除 <!-- 5468501   -->
在 iOS 和 iPadOS 裝置上，[Siri 命令的伺服器端記錄]  設定已從 Microsoft 端點管理員系統管理員主控台中移除 ([裝置設定]   > [設定檔]   > [建立設定檔]   > [iOS/iPadOS]  作為平台 > [裝置限制]  作為設定檔類型 > [內建應用程式]  )。 

此設定不會影響裝置。 若要從現有設定檔中移除設定，請開啟設定檔、進行任何變更，然後儲存設定檔。 設定檔隨即更新，並從裝置刪除設定。

若要查看您可以設定的所有設定，請參閱[使用 Intune 來允許或限制功能的 iOS 和 iPadOS 裝置設定](../configuration/device-restrictions-ios.md)。

適用於：

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Windows 10 功能更新 (公開預覽)<!-- 2384877 -->
您現在可以將 [Windows 10 功能更新](../protect/windows-update-for-business-configure.md#windows-10-feature-updates)部署至 Windows 10 裝置。 Windows 10 功能更新是新的軟體更新原則，可設定您想要裝置安裝並保持的 Windows 10 版本。 您可以使用此新原則類型以及現有的 Windows 10 更新通道。

收到 Windows 10 功能更新原則的裝置會安裝所指定 Windows 版本，並在編輯或移除原則之前保持為該版本。 執行較新 Windows 版本的裝置仍會保持為其目前版本。 保持為特定 Windows 版本之裝置仍然可以從 Windows 10 更新通道安裝該版本的品質和安全性更新。

自本週開始，會向租用戶推出此新的原則類型。 這項原則將於近日推出供租用戶使用。

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>在 macOS 應用程式的 plist 檔案中新增和變更重要資訊<!-- 4736278 -->
在 macOS 裝置上，您現在可以建立裝置組態設定檔，以上傳與應用程式或裝置相關聯的屬性清單檔案 (.plist) ([裝置設定]   > [設定檔]   > [建立設定檔]   > [macOS]  作為平台 > [喜好設定檔案]  作為設定檔類型)。

只有部分應用程式支援受控喜好設定，而這些應用程式可能不允許您管理所有設定。 請務必上傳設定裝置通道設定的屬性清單檔案，而不是使用者通道設定。

如需此功能的詳細資訊，請參閱[使用 Microsoft Intune 將屬性清單檔案新增至 macOS 裝置](../configuration/preference-file-settings-macos.md)。

適用於：

- 執行 10.7 和更新版本的 macOS 裝置

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>編輯 Autopilot 裝置的裝置名稱值<!-- 2640074 -->
您可以針對已加入 Azure AD 的 Autopilot 裝置，編輯其裝置名稱值。  如需詳細資訊，請參閱[編輯 Autopilot 裝置屬性](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes)。

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>編輯 Autopilot 裝置的群組標籤值<!-- 4816775   -->
您可以編輯 Autopilot 裝置的群組標籤值。 如需詳細資訊，請參閱[編輯 Autopilot 裝置屬性](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="updated-support-experience---5012398---"></a>已更新支援體驗<!-- 5012398 -->

自即日起，會向租用戶推出針對[取得 Intune 說明及支援](get-support.md)之更新及簡化的主控台內體驗。 這項新體驗將於近日推出供您使用。

我們已改善主控台內常見問題的搜尋和意見反應，以及您用於連絡支援人員的工作流程。 當您建立支援問題時，您會看到回撥或電子郵件回覆的即時預估，且進階與統一支援客戶可以輕鬆地指定其問題的嚴重性，以協助更快取得支援。

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>已改善的 Intune 報告體驗 (公開預覽) <!-- 3791418 -->
Intune 現在提供已改善的報告體驗，包括新報表類型、更好的報表組織、更聚焦的檢視、已改善的報表功能，以及更一致且即時的資料。 新報表類型著重於下列項目：

- **營運** - 提供最新記錄，包含負面健康情況焦點。 
- **組織** - 提供整體狀態的更廣泛摘要。
- **歷程記錄** - 提供一段時間的模式和趨勢。
- **專家** - 可讓您使用未經處理資料來建立您自己的自訂報表。

第一組新報表專注於裝置合規性。 如需詳細資訊，請參閱[部落格 - Microsoft Intune 報告架構](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) \(英文\) 和 [Intune 報表](reports.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>角色型存取控制

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>重複的自訂或內建角色 <!-- 1081938   -->
您現在可以複製內建和自訂角色。 如需詳細資訊，請參閱[複製角色](../fundamentals/create-custom-role.md#copy-a-role)。

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>學校系統管理員角色的新權限 <!-- 5621805  -->  
已經新增兩個新權限 ([指派設定檔]  和 [同步裝置]  ) 至學校系統管理員角色 > [權限]   > [註冊計劃]  。 同步設定檔權限可讓群組管理員同步處理 Windows Autopilot 裝置。 指派設定檔權限可讓他們刪除使用者起始的 Apple 註冊設定檔。 它也讓他們有權管理 Autopilot 裝置指派和 Autopilot 部署設定檔指派。 如需學校系統管理員/群組管理員所有權限的清單，請參閱[指派群組管理員](https://docs.microsoft.com/intune-education/group-admin-delegate) \(部分機器翻譯\)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全性

#### <a name="bitlocker-key-rotation---2564951----"></a>BitLocker 金鑰輪替<!-- 2564951  -->
您可以使用 Intune 裝置動作，針對執行 Windows 1909 版或更新版本的受控裝置，從遠端[輪替 BitLocker 修復金鑰](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)。 若要有資格輪替修復金鑰，裝置必須設定為支援修復金鑰輪替。  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>更新專用裝置註冊以支援 SCEP 裝置憑證部署 <!-- 5198878  -->
Intune 現在支援對 Android Enterprise 專用裝置進行憑證型 Wi-Fi 存取設定檔的 SCEP 裝置憑證部署。 Microsoft Intune 應用程式必須存在於裝置上才能部署。 因此，我們已經更新 Android Enterprise 專用裝置的註冊體驗。 新註冊仍然以相同方式開始 (使用 QR、NFC、零觸控或裝置識別碼)，但現在有要求使用者安裝 Intune 應用程式的步驟。 現有裝置將會輪流自動安裝該應用程式。

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>企業對企業的 Intune 稽核記錄<!--5670211 -->
企業對企業 (B2B) 共同作業可讓您安全地與來自任何其他組織的來賓使用者共用公司的應用程式和服務，同時保有您公司資料的控制權。 Intune 現在支援 B2B 來賓使用者的稽核記錄。 例如，當來賓使用者進行變更時，Intune 將能夠透過稽核記錄來捕捉此資料。 如需詳細資訊，請參閱[什麼是 Azure Active Directory B2B 中的來賓使用者存取權？](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>2019 年 11 月 11 日當週  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>已改善公司入口網站的 macOS 註冊體驗 <!-- 5074349  -->  
提供 macOS 註冊體驗的公司入口網站有更簡易註冊程序，其更貼近 iOS 版公司入口網站的註冊體驗。 裝置使用者現在會看到：  

- 更時尚的使用者介面。  
- 改善的註冊檢查清單。  
- 更清楚的裝置註冊指示。  
- 改善的疑難排解選項。  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>從 Windows 公司入口網站應用程式啟動的 Web 應用程式<!-- 5030972 -->
終端使用者現在可以直接從 Windows 公司入口網站應用程式啟動 Web 應用程式。 終端使用者可以選取 Web 應用程式，然後選擇 [在瀏覽器中開啟]  選項。 已發佈的 Web URL 會直接在網頁瀏覽器中開啟。 此功能將於下周推出。 如需 Web 應用程式的詳細資訊，請參閱[將 Web 應用程式新增至 Microsoft Intune](../apps/web-app.md)。  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Windows 10 公司入口網站中新的指派類型資料行 <!-- 5459950  -->
公司入口網站 > [已安裝的應用程式]   > [指派類型]  資料行已重新命名為 [由您的組織要求]  。  使用者在該資料行下會看到 [是]  或 [否]  值，其表示應用程式為必要或是由其組織設為選擇性。 因為裝置使用者對可用應用程式的概念深感困惑，所以才有這些變更。 如需從公司入口網站安裝應用程式的詳細資訊，請參閱[在裝置上安裝和共用應用程式](../user-help/install-apps-cpapp-windows.md)。 使用者如需設定公司入口網站應用程式的詳細資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>2019 年 11 月 4 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>裝置安全性

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Microsoft Azure Government 上支援安全性基準<!-- 4062552 -->

*Microsoft Azure Government* 上裝載的 Intune 的執行個體現在可以使用[安全性基準](../protect/security-baselines.md)來協助您保護您的使用者與裝置。

## <a name="whats-new-archive"></a>新功能封存
針對過去幾個月，請參閱[新功能封存](whats-new-archive.md)。

## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


