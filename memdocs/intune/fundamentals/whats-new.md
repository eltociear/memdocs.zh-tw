---
title: Microsoft Intune 的新功能 - Azure | Microsoft Docs
titleSuffix: ''
description: 了解 Intune Azure 入口網站中的新功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/23/2020
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
ms.openlocfilehash: 87cf4d9fc21b951386c496e49fe482810febcda3
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85263949"
---
# <a name="whats-new-in-microsoft-intune"></a>Microsoft Intune 的新功能

在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，了解每週的 Microsoft Intune 新功能。 您也可以尋找[重要通知](#notices)、[過去的版本](whats-new-archive.md)，以及[如何發佈 Intune 服務更新](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) \(英文\) 的相關資訊。 

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
### Scripts


<!-- ########################## -->

## <a name="week-of-june-22-2020"></a>2020 年 6 月 22 日當週

### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>使用指令碼套件主動補救終端使用者的裝置問題<!-- 5933328 -->
您可以在終端使用者裝置上建立並執行指令碼套件，以主動找出並修正貴組織中首要的支援問題。 部署指令碼套件有助於減少聯絡支援人員的次數。 請選擇建立自己的指令碼套件，或部署我們已撰寫並在環境中使用的其中一個指令碼套件，以減少支援票證。 Intune 可讓您查看已部署指令碼套件的狀態，並且監視偵測和修復的結果。 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選取 [報表] > [端點分析] > [主動式補救]。 如需詳細資訊，請參閱[主動式補救](https://aka.ms/uea_prs) (英文)。

### <a name="device-security"></a>裝置安全性

### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>在 Android 的相容性原則中使用 Microsoft Defender ATP<!-- 4425686  -->

您現在可以使用 Intune [將 Android 裝置上線到 Microsoft Defender 進階威脅防護](../protect/advanced-threat-protection.md#onboard-android-devices) (MicrosoftDefender ATP) 上。 將註冊裝置上線之後，您的 Android 合規性政策就可以使用來自 Microsoft Defender ATP 的「威脅等級」訊號。 這些是您先前可用於 Windows 10 裝置的相同訊號。

### <a name="configure-defender-atp-web-protection-for-android-devices---6185563-wnready---"></a>設定 Android 裝置適用的 Defender ATP Web 防護<!-- 6185563 WNReady -->

當您使用 Android 裝置適用的 Microsoft Defender 進階威脅防護 (Microsoft Defender ATP) 時，您可以[設定 Microsoft Defender ATP Web 防護](../protect/advanced-threat-protection.md#configure-web-protection-on-devices-that-run-android) (英文) 來停用網路釣魚掃描功能，或防止該掃描使用 VPN。

視 Android 裝置向 Intune 註冊的方式而定，以下選項可供使用：

- Android 裝置系統管理員：使用自訂 OMA-URI 設定來停用 Web 防護功能，或只在掃描期間停用 VPN。
- Android Enterprise 工作設定檔：使用應用程式組態設定檔和設定設計工具來停用所有 Web 防護功能。

## <a name="week-of-june-15-2020--2006-service-release"></a>2020 年 6 月 15 日當週 (2006 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>受控應用程式的電信資料傳輸保護<!-- 6884491  -->
在受保護的應用程式中偵測到超連結電話號碼時，Intune 會檢查其是否已套用保護原則，讓該號碼能夠轉移到撥號應用程式。 當受原則管理的應用程式開始處理這類內容時，您可以選擇內容的傳送方式。 在 Microsoft Endpoint Manager 中建立應用程式保護原則時，請從 [將組織資料傳送至其他應用程式]選取 [受控應用程式] 選項，然後選取 [將電信資料傳送至] 的選項。 如需有關此資料保護設定的詳細資訊，請參閱 [Microsoft Intune 的 Android 應用程式保護原則設定](../apps/app-protection-policy-settings-android.md)與 [iOS 應用程式保護原則設定](../apps/app-protection-policy-settings-ios.md)。 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Azure AD 企業和 Office Online 應用程式在公司入口網站中的整合傳遞<!-- 7414033  -->
在 Intune 的 [自訂] 窗格中，您可以在公司入口網站中選取 [隱藏] 或 [顯示] **Azure AD 企業應用程式**和 **Office Online 應用程式**。 每個終端使用者都會從所選 Microsoft 服務看到其整個應用程式的類別目錄。 根據預設，每個額外的應用程式來源都會設定為 [隱藏]。 這項功能會先在公司入口網站網站中生效，接著預計在 Windows 公司入口網站中提供支援。 請在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)選取 [租用戶系統管理] > [自訂] 來尋找此組態設定。 如需相關資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>macOS 版公司入口網站註冊體驗的改善<!-- 6444452  -->
提供 macOS 註冊體驗的公司入口網站有更簡易註冊程序，其更貼近 iOS 版公司入口網站的註冊體驗。 裝置使用者將會看到：  
- 更時尚的使用者介面。  
- 改善的註冊檢查清單。  
- 更清楚的裝置註冊指示。  
- 改善的疑難排解選項。  

如需有關公司入口網站的詳細資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>iOS/iPadOS 與 macOS 公司入口網站 [裝置] 頁面的改善<!-- 6055001 -->
我們已變更公司入口網站 [裝置] 頁面，以改善 iOS/iPadOS 和 Mac 使用者的應用程式體驗。 除了打造更為現代化的外觀與風格之外，在已經定義區段標題的單一資料行之下，裝置詳細資料也經過重新安排，使用者更方便查看裝置狀態。 我們也為裝置不符合規範的使用者，加入更清楚的訊息與疑難排解步驟。 如需有關公司入口網站的詳細資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。 若要手動同步處理裝置，請參閱[手動同步處理您的 iOS 裝置](../user-help/sync-your-device-manually-ios.md)。  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>iOS/iPadOS 公司入口網站的雲端設定<!-- 7071303  -->
iOS/iPadOS 公司入口網站的新**雲端**設定，可讓使用者將其驗證重新導向至適用於貴組織的適當雲端。 預設設定中會設為**自動**，這會將驗證導向至使用者裝置自動偵測到的雲端。 如果貴組織的驗證必須重新導向至非自動偵測到的雲端 (例如公用雲端或政府雲端)，您的使用者可以選取 [設定] 應用程式 > [公司入口網站] > [雲端]，以手動方式選取適當的雲端。 如果您的使用者是從另一部裝置登入，且其裝置不會自動偵測適當的雲端，才能從 [自動] 變更 [雲端] 設定。 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>重複的 Apple VPP 權杖<!-- 7101606  -->
具有相同**權杖位置** 的 Apple VPP 權杖現在會標示為「重複」，並可在移除重複權杖時再次同步。 您仍能為標記為「重複」的權杖指派和撤銷授權。 不過，一旦權杖標記為「重複」時，可能不會反映新應用程式的授權和已購買書籍。 若要從您的租用戶中尋找 Apple VPP 權杖，請從 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) 中選取 [租用戶系統管理] > [連接器與權杖] > [Apple VPP 權杖]。 如需與 VPP 權杖相關的詳細資訊，請參閱[如何使用 Microsoft Intune 管理透過 Apple 大量採購方案購買的 iOS 和 macOS 應用程式](../apps/vpp-apps-ios.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>在 macOS 裝置上的 Wi-Fi 設定檔中新增多個根憑證來進行 EAP-TLS 驗證<!-- 2077871  -->

在 macOS 裝置上，您可以建立 Wi-Fi 設定檔，並選取可延伸的驗證通訊協定 (EAP) 驗證類型 ([裝置] >  [設定檔] > [建立設定檔] > [macOS] 平台 > [Wi-Fi] 設定檔 > [Wi-Fi 類型] 設定為 [企業])。

當您將 **EAP 類型**設定為 **EAP-TLS**、**EAP-TTLS** 或 **PEAP** 驗證時，即可新增多個根憑證。 在此之前只能新增一個根憑證。

如需與您可以設定的設定相關詳細資訊，請參閱[在 Microsoft Intune 中新增適用於 macOS 裝置的 Wi-Fi 設定](../configuration/wi-fi-settings-macos.md)。

適用於：
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>在 Windows 10 和更新版本的裝置上搭配使用 PKCS 憑證與 Wi-Fi 設定檔<!-- 3246388   -->
您可以使用 SCEP 憑證來驗證 Windows Wi-Fi 設定檔 ([裝置設定]  > [設定檔] > [建立設定檔] > [Windows 10 和更新版本] 平台 > [WiFi] 設定檔類型 > [企業] > [EAP 類型] > )。 現在，您可以將 PKCS 憑證與 Windows Wi-Fi 設定檔搭配使用。 這項功能可讓使用者以您租用戶中新的或現有 PKCS 憑證設定檔來驗證 Wi-Fi 設定檔。 

如需與您可設定的 Wi-Fi 設定相關的詳細資訊，請參閱[在 Intune 中為 Windows 10 和更新版本裝置新增 Wi-Fi 設定](../configuration/wi-fi-settings-windows.md)。

適用於：
- Windows 10 和更新版本

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>適用於 macOS 裝置的有線網路裝置組態設定檔<!-- 3508686  -->
將會可以使用設定有線網路的 macOS 裝置設定檔 ([裝置] > **[設定檔] > [建立設定檔] > [macOS] 平台 > [有線網路] 設定檔類型)。 使用此功能來建立 802.1x 設定檔以管理有線網路，並將這些有線網路部署至您的 macOS 裝置。

如需這項功能的詳細資訊，請參閱 [macOS 裝置上的有線網路](../configuration/wired-networks-configure.md) (英文)。

適用於：
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>使用 Microsoft Launcher 作為完全受控 Android Enterprise 裝置的預設啟動器<!-- 4927976   -->
在 Android Enterprise 裝置擁有者裝置上，您可以將 Microsoft Launcher 設定為完全受控裝置的預設啟動器 ([裝置] > [設定設定檔] > [建立設定檔] > [Android Enterprise] \(針對平台\) > [裝置擁有者] > [裝置體驗] > [裝置限制])。 若要設定所有其他 Microsoft Launcher 設定，請使用[應用程式設定原則](../apps/configure-microsoft-launcher.md)。 

此外，還有一些其他 UI 更新，包括**專用裝置**已重新命名為**裝置體驗**。

若要查看您可以設定的所有設定，請參閱[使用 Intune 允許或限制功能的 Android Enterprise 裝置設定](../configuration/device-restrictions-android-for-work.md)。 

適用於：
- Android Enterprise 裝置擁有者完全受控裝置 (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>使用自發性單一應用程式模式設定，將 iOS 公司入口網站設定為登入/登出應用程式<!-- 7055619   -->
在 iOS/iPadOS 裝置上，您可以將應用程式設定為在自發性單一應用程式模式 (ASAM) 中執行。 公司入口網站應用程式現在支援 ASAM，而且可以設定為「登入/登出」應用程式。 在此模式中，使用者必須登入公司入口網站應用程式，才能使用其他應用程式和裝置上的主畫面按鈕。 當使用者登出公司入口網站應用程式時，裝置會回到單一應用程式模式，並鎖定公司入口網站應用程式。

若要將公司入口網站設定為在 ASAM 中，請前往 [裝置] > [設定檔] > [建立設定檔] > [iOS/iPadOS] 平台 > [裝置限制] 設定檔 > [自發性單一應用程式模式]。

如需詳細資訊，請參閱[自發性單一應用程式模式 (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) 與[「單一 App 模式」承載資料設定](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (開啟 Apple 的網站)。

適用於：
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>在 macOS 裝置上設定內容快取<!-- 7106872   -->
在 macOS 裝置上，您可以建立組態設定檔以設定內容快取 ([裝置] > [組態設定檔] > [建立設定檔] > [macOS] \(針對平台\) > [裝置功能] \(針對設定檔\))。 使用這些設定來刪除快取、允許共用快取、設定磁碟上的快取限制等等。

如需有關內容快取的詳細資訊，請參閱[內容快取](https://developer.apple.com/documentation/devicemanagement/contentcaching) \(英文\) (會開啟 Apple 的網站)。

若要查看您可以設定的設定，請參閱 [Intune 中的 macOS 裝置功能設定](../configuration/macos-device-features-settings.md)。

適用於：
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>加入新的結構描述設定，並在 Android Enterprise 上使用 OEMConfig 搜尋現有的結構描述設定<!-- 6394386   -->
在 Intune 中，您可以在 Android Enterprise 裝置上使用 OEMConfig 來管理設定 ([裝置] > [組態設定檔] > [建立設定檔] > [Android Enterprise] \(針對平台\) > [OEMConfig] \(針對設定檔\))。 當您使用**設定設計工具**時，會顯示應用程式結構描述中的屬性。 現在，您可以在**設定設計工具**中：

- 將新的設定新增至應用程式結構描述。
- 在應用程式結構描述中搜尋新的與現有的設定。

如需 Intune 中 OEMConfig 設定檔的詳細資訊，請參閱[在 Microsoft Intune 中透過 OEMConfig 來使用和管理 Android Enterprise 裝置](../configuration/android-oem-configuration-overview.md)。

適用於：
- Android 企業

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>封鎖共用的 iPad 裝置上的共用的 iPad 臨時工作階段<!-- 6613794  -->
在 Intune 中，有新的**封鎖共用的 iPad 臨時工作階段**設定可封鎖共用的 iPad 裝置上的臨時工作階段 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] \(針對平台\) > [裝置限制] \(針對設定檔\) > [共用的 iPad])。 啟用時，終端使用者將無法使用來賓帳戶。 他們必須使用其受控 Apple ID 與密碼登入裝置。 

如需詳細資訊，請參閱[使用 Intune 來允許或限制功能的 iOS 和 iPadOS 裝置設定](../configuration/device-restrictions-ios.md)。

適用於：
- 執行 iOS/iPadOS 13.4 與更新版本的共用的 iPad 裝置

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>「攜帶您自己的裝置」可使用 VPN 進行部署<!--5015344  -->
新的 Autopilot 設定檔 [跳過網域連線能力檢查] 切換按鈕可讓您使用自己的協力廠商 Win32 VPN 用戶端來部署混合式 Azure AD Join 裝置，而不需存取公司網路。 若要查看新的切換，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置]  > [Windows] > [Windows 註冊] > [部署設定檔] > [建立設定檔] > [全新體驗 (OOBE)]。

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>註冊狀態頁面設定檔可以設定為裝置群組<!--3952138 -->
註冊狀態頁面 (ESP) 設定檔先前只能以使用者群組為目標。 現在您也可以將其設定為目標裝置群組。 如需詳細資訊，請參閱[設定註冊狀態頁面](../enrollment/windows-enrollment-status.md)。

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>自動裝置註冊同步錯誤<!-- 6988214 -->
系統會針對 iOS/iPadOS 與 macOS 裝置回報新的錯誤，包括
- 電話號碼中的無效字元，以及該欄位為空的情況。 
- 設定檔無效或空的設定名稱。 
- 無效/已過期的資料指標值，或找不到資料指標的情況。
- 已拒絕或過期的權杖。 
- [部門] 欄位空白或長度太長。 
- Apple 找不到設定檔，而必須建立新設定檔。 
- 已移除的 Apple Business Manager 裝置計數將會新增至概觀頁面，您可以在其中看到裝置的狀態。

#### <a name="shared-ipads-for-business--6367326-----"></a>適用於商務的共用 iPad<!--6367326   -->
您可以使用 Intune 和 Apple Business Manager 來輕鬆且安全地設定共用的 iPad，以讓多位員工可以共用裝置。 Apple 的[共用 iPad](https://developer.apple.com/education/shared-ipad/)可為多個使用者提供個人化體驗，同時保留使用者資料。 使用者可使用受控 Apple ID，在登入其組織中的任何共用 iPad 之後，存取其應用程式、資料及設定。 共用的 iPad 可與同盟身分識別搭配使用。

若要查看這項功能，請移至 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > [iOS] > [iOS 註冊] > [註冊方案權杖] > 選擇權杖** > [設定檔] > [建立設定檔] > [iOS]。 在 [管理設定] 頁面上，選取 [不搭配使用者親和性進行註冊]，您就會看到 [共用的 iPad] 選項。

需要：iPadOS 13.4 與更新版本。 此版本新增了對共用 iPad 的暫時工作階段支援，讓使用者可在沒有受控 Apple ID 的情況下存取裝置。 登出時，裝置會清除所有使用者資料，讓裝置立即可供使用，而不需要抹除裝置。 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>Apple 自動裝置註冊的已更新使用者介面<!--7430322 -->
使用者介面已更新為將 Apple 的「裝置註冊計劃」取代為「自動裝置註冊」，以配合 Apple 術語。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>macOS 的裝置遠端鎖定 PIN 可用性<!--7281557   -->
macOS 裝置遠端鎖定 PIN 的可用性已從 7 天增加到 30 天。

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>變更共同管理裝置上的主要使用者<!--7319183  -->
您能夠變更共同受控 Windows 裝置的裝置主要使用者。 如需有關如何尋找並變更主要使用者的詳細資訊，請參閱[尋找 Intune 裝置的主要使用者](../remote-actions/find-primary-user.md)。 這項功能將會在接下來的幾週逐步推出。

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>設定 Intune 主要使用者也會設定 Azure AD 擁有者屬性<!--7319227 -->
這個新功能會在設定 Intune 主要使用者的同時，自動在新註冊的混合式 Azure AD 聯結裝置上設定擁有者屬性。 如需有關主要使用者的詳細資訊，請參閱[尋找 Intune 裝置的主要使用者](../remote-actions/find-primary-user.md)。

這是註冊程序的變更，而且只會套用至新註冊的裝置。 針對現有的混合式 Azure AD 聯結裝置，您必須手動更新 Azure AD 擁有者屬性。 若要這樣做，您可以使用[變更主要使用者功能](../remote-actions/find-primary-user.md#change-a-devices-primary-user)或[指令碼](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices)。

當 Windows 10 裝置已加入混合式 Azure Directory 時，裝置的第一個使用者會成為 [端點管理員] 中的主要使用者。  目前，未在對應的 Azure AD 裝置物件上設定使用者。 這會造成比較來自 Azure AD 入口網站的擁有者屬性與 Microsoft 端點管理員系統管理中心的主要使用者屬性時發生不一致的情況。 Azure AD 擁有者屬性是用來保護對 BitLocker 修復金鑰的存取權。 在已加入混合式 Azure AD 的裝置上，不會填寫此屬性。 此限制可防止從 Azure AD 設定 BitLocker 復原的自助服務。 這個即將推出的功能可解決此限制。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>裝置安全性

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>在 macOS 裝置的 FileVault 2 加密期間，對使用者隱藏修復金鑰<!-- 5459801  -->
我們已在 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) 範本內新增設定至 [FileVault] 類別：**隱藏修復金鑰**。 此設定會在 FileVault 2 加密期間隱藏來自終端使用者的個人金鑰。 

若要檢視已加密 macOS 裝置的個人修復金鑰，裝置使用者可以前往下列任何位置，然後按一下 [取得 macOS 裝置的修復金鑰]： 

- iOS/iPadOS 公司入口網站應用程式
- Intune 應用程式
- 公司入口網站
- Android 公司入口網站應用程式

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Android 完全受控上的 Outlook 支援 S/MIME 簽署和加密憑證<!--5896415   -->
您現在可以在執行 Android Enterprise 完全受控裝置上的 Outlook 使用憑證，以進行 S/MIME 簽署和加密。

這會在其他 Android 版本 (Android 上的 Outlook 支援 S/MIME 簽署和加密憑證) 上，延伸上個月新增的支援。 您可以使用 SCEP 和 PKCS 匯入的憑證設定檔來佈建這些憑證。

如需這項支援的詳細資訊，請參閱 Exchange 文件中的 [iOS 和 Android 的 Outlook 中敏感度標籤和保護](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) (機器翻譯)。

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>針對不符合規範，將公司入口網站支援網站的連結新增至電子郵件<!-- 7225498    -->
當您[設定通知訊息範本](../protect/actions-for-noncompliance.md#create-a-notification-message-template)，以傳送不符合規範的電子郵件通知時，請使用**公司入口網站網站連結**的新設定，自動納入公司入口網站的網站連結。 由將此選項設為 [啟用]，使用的裝置不符合規範裝置，而依據此範本而收到電子郵件的使用者，就能使用此連結開啟網站，深入了解自己的裝置為什麼不符合規範。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>授權

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>管理員不再需要 Intune 授權，即可存取 Microsoft Endpoint Manager 管理主控台<!--1335430 -->
您現在可以設定整個租用戶的切換，移除管理員存取 MEM 和 查詢圖形 ApI 的 Intune 授權需求。 一旦您移除授權需求就無法再恢復。 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>指令碼 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>在 macOS 裝置上的 Shell 指令碼可用性<!-- 7134839  -->
適用於 macOS 裝置的 Shell 指令碼現在可供政府雲端和中國客戶使用。 如需詳細資訊，請參閱[在 Intune 中於 macOS 裝置使用 Shell 指令碼](../apps/macos-shell-scripts.md)。



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>2020 年 6 月 8 日當週   

### <a name="app-management"></a>應用程式管理  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>iOS/iPadOS 公司入口網站中的資訊畫面更新 <!--7032452 -->
已更新 iOS/iPadOS 公司入口網站中的資訊畫面，以便更清楚地說明管理員可在裝置上查看和執行的動作。 這類釐清內容僅適用於公司擁有的裝置。 僅更新文字，管理員可以在使用者裝置上查看或執行的動作不會實際修改。 若要查看已更新的畫面，請移至 [Intune 終端使用者應用程式的 UI 更新](./whats-new-app-ui.md)。

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>已更新 Android 應用程式條件式啟動終端使用者的體驗<!-- 5736084 -->
2006 版的 Android 公司入口網站具有以 2005 版更新為依據的變更。 在 2005 版本中，我們推出了一項更新，其中由應用程式保護原則發出警告、封鎖或抹除的 Android 裝置使用者會看到完整的頁面訊息，說明警告、封鎖或抹除的原因，以及補救問題的步驟。 在 2006 版本中，指派應用程式保護原則的 Android 應用程式首次使用者將會透過引導式流程進行，以補救導致應用程式存取遭到封鎖的問題。 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>2020 年 5 月 25 日當週

### <a name="app-management"></a>應用程式管理

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>ARM64 裝置上的 Windows 32 位元 (x86) 應用程式<!-- 5477661 -->
部署為可供 ARM64 裝置使用的 Windows 32 位元 (x86) 應用程式，現在將會顯示在公司入口網站中。 如需有關 Windows 32 位元應用程式的詳細資訊，請參閱 [Win32 應用程式管理](../apps/apps-win32-app-management.md)。

#### <a name="windows-company-portal-app-icon---7114635---"></a>Windows 公司入口網站應用程式圖示<!-- 7114635 -->
Windows 公司入口網站應用程式的圖示已更新。 如需有關公司入口網站的詳細資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>2020 年 5 月 18 日當週

### <a name="app-management"></a>應用程式管理  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>更新適用於 iOS/iPadOS 與 macOS 之公司入口網站應用程式的圖示<!--6057697 -->
我們已更新公司入口網站中的圖示，這些圖示支援雙螢幕裝置且具有更現代化的外觀和感覺，並與「Microsoft Fluent Design 系統」一致。 若要查看已更新的圖示，請移至 [Intune 終端使用者應用程式的 UI 更新](./whats-new-app-ui.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>裝置安全性

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>使用端點偵測與回應原則將裝置加入 Defender ATP<!-- 7130165  -->

使用[端點偵測和回應 (EDR) 的端點安全性原則](../protect/endpoint-security-edr-policy.md)，為您的 Microsoft Defender 進階威脅防護 (Defender ATP) 部署進行裝置上線和設定。 EDR 支援由 Intune (MDM) 管理的 Windows 裝置原則，以及由 Configuration Manager 管理的 Windows 裝置個別原則。 

若要將原則用於 Configuration Manager 裝置，您必須[設定 Configuration Manager 以支援 EDR 原則](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy)。 設定包括：

- 設定您的 Configuration Manager 以進行「租用戶附加」。
- 安裝 Configuration Manager 的主控台內更新，以支援 EDR 原則。 此更新僅適用於已啟用「租用戶附加」的階層。
- 將您的裝置集合從階層同步至 Microsoft 端點管理員系統管理中心。


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>2020 年 5 月 11 日當週 (2005 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>在公司入口網站中自訂自助裝置動作<!--4393379 -->
您可以自訂在公司入口網站應用程式和網站中，向使用者顯示的可用自助裝置動作。 若要協助禁止非預期的裝置動作，您可以選取 [租用戶系統管理] > [自訂]，為公司入口網站應用程式進行這些設定。 以下是可用的動作：
- 在公司 Windows 裝置上隱藏 [移除] 按鈕。
- 在公司 Windows 裝置上隱藏 [重設] 按鈕。
- 在公司 iOS 裝置上隱藏 [重設] 按鈕。
- 在公司 iOS 裝置上隱藏 [移除] 按鈕。
如需詳細資訊，請參閱[來自公司入口網站的使用者自助裝置動作](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal)。

#### <a name="auto-update-vpp-available-apps---3640511----"></a>自動更新 VPP 可用的應用程式<!-- 3640511  -->
當**自動應用程式更新**已啟用 VPP 權杖時，將會自動更新發佈為大量採購方案 (VPP) 可用應用程式的應用程式。 先前，VPP 可用的應用程式不會自動更新。 有較新版本可用時，終端使用者必須前往公司入口網站並重新安裝應用程式。 必要的應用程式會繼續支援自動更新。




#### <a name="android-company-portal-user-experience---5736084----"></a>Android 公司入口網站使用者體驗<!-- 5736084  -->
在 2005 版的 Android 公司入口網站中，透過應用程式防護原則發出警告、封鎖或抹除的 Android 裝置終端使用者，將會獲得新的使用者體驗。 終端使用者不會看到目前的對話方塊體驗，而是看到完整的頁面訊息，其中說明警告、封鎖或抹除的原因，以及補救問題的步驟。 如需詳細資訊，請參閱 [Android 裝置的應用程式防護體驗](../apps/app-protection-policy.md#app-protection-experience-for-android-devices)和 [Microsoft Intune 的 Android 應用程式防護原則設定](../apps/app-protection-policy-settings-android.md)。

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>macOS 版公司入口網站中的多個帳戶支援<!-- 5779449  -->
macOS 裝置上的公司入口網站現在會快取使用者帳戶，讓登入變得更容易。 使用者在每次啟動應用程式時，不再需要登入公司入口網站。 此外，如果快取了多個使用者帳戶，則公司入口網站會顯示帳戶選擇器，因此使用者不需要輸入其使用者名稱。 

#### <a name="newly-available-protected-apps---7060934-----"></a>新推出的受保護應用程式<!-- 7060934   -->
下列受保護的應用程式現已推出：
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero - email for attorneys

如需受保護應用程式的詳細資訊，請參閱[受 Microsoft Intune 保護的應用程式](../apps/apps-supported-intune-apps.md)。

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>從公司入口網站搜尋 Intune 文件<!-- 1736480   -->
您現在可直接從 macOS 應用程式的公司入口網站搜尋 Intune 文件。 在功能表列中，選取 [說明] > [搜尋] 並輸入搜尋的關鍵字，以快速找到問題的解答。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Zebra Technologies 裝置的 OEMConfig 支援改善<!-- 4184154 -->
Intune 完整支援 Zebra OEMConfig 提供的所有功能。 使用 Android Enterprise 和 OEMConfig 來管理 Zebra Technologies 裝置的客戶，可以將多個 OEMConfig 設定檔部署至一部裝置。 客戶也可以檢視有關其 Zebra OEMConfig 設定檔狀態的詳細報告。

如需詳細資訊，請參閱[在 Microsoft Intune 中對 Zebra 裝置部署多個 OEMConfig 設定檔](../configuration/oemconfig-zebra-android-devices.md)。

其他 OEM 的 OEMConfig 行為沒有任何變更。

適用於：
- Android 企業
- 支援 OEMConfig 的 Zebra Technologies 裝置。 如需支援的具體詳細資料，請連絡 Zebra。

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>在 macOS 裝置上設定系統延伸模組<!-- 6255624 -->
在 macOS 裝置上，您可建立核心延伸模組設定檔，以在核心層級進行設定 ([裝置] > [組態設定檔] > [macOS] (針對平台) > [核心延伸模組] (針對設定檔))。 Apple 最終會淘汰核心延伸模組，並在未來的版本中以系統延伸模組取代。

系統延伸模組會在使用者空間中執行，而不具有核心的存取權限。 目標是要提高安全性並提供更多的終端使用者控制，同時限制核心層級的攻擊。 核心延伸模組和系統延伸模組都可供使用者安裝應用程式延伸模組，以擴充作業系統的原生功能。

在 Intune 中，您可同時設定核心延伸模組和系統延伸模組 ([裝置] > [組態設定檔] > [macOS] (針對平台) > [系統延伸模組] (針對設定檔))。 核心延伸模組適用於 10.13.2 和更新版本。 系統延伸模組則適用於 10.15 和更新版本。 從 macOS 10.15 到 macOS 10.15.4，核心延伸模組和系統延伸模組可並存執行。 

若要了解 macOS 裝置上的這些延伸模組，請參閱[新增 macOS 延伸模組](../configuration/kernel-extensions-overview-macos.md)。

適用於：
- macOS 10.15 與更新版本

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>在 macOS 裝置上設定應用程式和處理序的隱私權喜好設定<!-- 2934232   --> 
隨著 macOS Catalina 10.15 的發行，Apple 新增了安全性與隱私權的增強功能。 根據預設，應用程式與處理序無法在沒有使用者同意的情況下存取特定資料。 如果未經過使用者同意，則應用程式與處理序可能無法運作。 Intune 將新增設定的支援，可讓 IT 系統管理員在執行 macOS 10.14 和更新版本的裝置上，代表終端使用者允許 (或不允許) 資料存取。 這些設定可確保應用程式與處理序繼續正常運作，並減少提示的次數。 

如需您可以管理的設定詳細資訊，請參閱 [macOS 隱私權喜好設定](../configuration/device-restrictions-macos.md#privacy-preferences)。

適用於：
- macOS 10.14 和更新版本

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>註冊限制支援範圍標籤<!--4209550  -->
您現在可以將範圍標籤指派給註冊限制。 若要這麼做，請移至 [Microsoft Endpoint Manager系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > [註冊限制] > [建立限制]。 建立任一類型的限制，且您將看到 [範圍標籤] 頁面。 如需詳細資訊，請參閱[設定註冊限制](../enrollment/enrollment-restrictions-set.md)。

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Hololens 2 裝置的 Autopilot 支援<!--6305220  -->
Windows Autopilot 現在支援 Hololens 2 裝置。 如需詳細資訊以了解如何使用適用於 HoloLens 的 Autopilot，請參閱[適用於 HoloLens 2 的 Windows Autopilot](https://docs.microsoft.com/hololens/hololens2-autopilot)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>針對 iOS 大量使用同步遠端動作<!--6440956  idmiss-->
您現在可以一次在最多 100 部 iOS 裝置上使用同步遠端動作。 若要查看此功能，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > [所有裝置] > [大量裝置動作]。 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>自動裝置同步間隔縮短為 12 小時<!--3077535  -->
針對 Apple 的自動裝置註冊，Intune 與 Apple Business Manager 之間的自動裝置同步間隔已從 24 小時縮短為 12 小時。 如需同步的詳細資訊，請參閱[同步受控裝置](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>裝置安全性

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Android 裝置上 DISA Purebred 的衍生認證支援<!-- 6939073     -->
您現在可以在完全受控的 Android Enterprise 裝置上，使用 *DISA Purebred* 作為[衍生認證](../protect/derived-credentials.md)提供者。 支援包括為 DISA Purebred 擷取衍生認證。 若應用程式支援衍生認證，即可將其用於應用程式驗證、Wi-Fi、VPN 或 S/MIME 簽署及 (或) 加密。 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>在遇到不合規的情形時傳送推播通知 <!-- 1733150   -->
您現在可以設定[因應不合規情形的動作](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)，在使用者的裝置未達合規性政策條件時傳送推播通知給使用者。 新的動作是**傳送推播通知給終端使用者**，Android 和 iOS 裝置上均支援此動作。

當使用者在其裝置上選取推播通知時，公司入口網站或 Intune 應用程式隨即開啟，以顯示不合規原因的詳細資料。

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>端點安全性內容和新功能<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Intune [端點安全性](../protect/endpoint-security.md)的文件現已可供使用。 在 Microsoft Endpoint Manager 系統管理中心的端點安全性節點中，您可以：

- 建立焦點安全性原則並將其部署至您的受控裝置
- 設定與 Microsoft Defender 進階威脅防護的整合，及管理安全性工作，以協助為 ATP 小組找出的具風險裝置降低風險
- 設定安全性基準
- 管理裝置合規性及條件式存取原則
- 若已為用戶端附加設定了 Configuration Manager，就可以從 Intune 和 Configuration Manager 檢視所有裝置的合規性狀態。

除了可用的內容之外，本月的端點安全性還包括下列新內容：

- [**端點安全性原則**](../protect/endpoint-security-policy.md)已結束「預覽」階段，現已「正式推出」並可用於實際執行環境，但有兩個例外：

  - 在新的「公開預覽」中，您可將 [**Microsoft Defender 防火牆規則**設定檔](../protect/endpoint-security-firewall-policy.md#firewall-profiles)用於 Windows 10 防火牆原則。 此設定檔的每個執行格體都可以設定最多 150 個防火牆規則，以補足您的 Microsoft Defender 防火牆設定檔。 
  - 帳戶防護安全性原則仍為預覽階段。 

- 您現在可以[**建立端點安全性原則的重複項**](../protect/endpoint-security-policy.md#duplicate-a-policy)。 重複項會保留原始原則的設定，但會有新名稱。 新的原則執行個體不會包含對群組的任何指派，直到您編輯新的原則執行個體以新增指派為止。 您可以複製下列原則：
  - 防毒
  - 磁碟加密
  - 防火牆
  - 端點偵測與回應
  - 受攻擊面縮小
  - 帳戶防護

- 您現在可以[**建立安全性基準的重複項**](../protect/security-baselines.md#duplicate-a-security-baseline)。 重複項會保留原始基準的設定值，但會有新名稱。 新的基準執行個體不會包含對群組的任何指派，直到您編輯新的基準執行個體以新增指派為止。

- 端點安全性防毒原則的新報告現已推出：[**Windows 10 狀況不良的端點**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints)。 這份報告是您在檢視端點安全性防毒原則時，可以選取的新頁面。 此報告會顯示 MDM 管理的 Windows 10 裝置防毒軟體狀態。  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Android 上的 Outlook 支援 S/MIME 簽署和加密憑證<!-- 7207474  -->
您現在可以在 Android 上的 Outlook 使用憑證進行 S/MIME 簽署和加密。 藉由這項支援，您可以使用 SCEP、PKCS 和 PKCS 匯入的憑證設定檔來佈建這些憑證。 下列是支援的 Android 平台：

- Android Enterprise 工作設定檔
- Android 裝置管理員

即將推出完全受控的 Android Enterprise 裝置支援。

如需這項支援的詳細資訊，請參閱 Exchange 文件中的 [iOS 和 Android 的 Outlook 中敏感度標籤和保護](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) (機器翻譯)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="device-reports-ui-update---6269408---"></a>裝置報表 UI 更新<!-- 6269408 -->
報表概觀窗格現在提供 [摘要] 和 [報表] 索引標籤。在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)依序選取 [報表] 和 [報表] 索引標籤，即可查看可用的報表類型。 如需相關資訊，請參閱 [Intune 報表](../fundamentals/reports.md)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>指令碼

#### <a name="macos-script-support---6376978----"></a>macOS 指令碼支援<!-- 6376978  -->
macOS 的指令碼支援現已正式推出。 此外，我們也已針對使用者指派的指令碼，以及已向 Apple 自動裝置註冊 (先前為裝置註冊計劃) 進行註冊的 macOS 裝置新增支援。 如需詳細資訊，請參閱[在 macOS 裝置上的 Intune 中使用 Shell 指令碼](../apps/macos-shell-scripts.md)。


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>2020 年 5 月 4 日當週  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>適用於 Android 的公司入口網站會引導使用者在工作設定檔註冊之後取得應用程式 <!-- 6103999 -->
我們已改善公司入口網站中的應用程式內指導方針，讓使用者能更輕鬆地尋找並安裝應用程式。 使用者在註冊工作設定檔管理之後會收到一則訊息，說明如何在有徽章的 Google Play 版本中找到建議的應用程式。 我們已更新[使用 Android 工作設定檔註冊裝置](../user-help/enroll-device-android-work-profile.md)中的最後一個步驟以顯示新的訊息。 使用者也會在左側公司入口網站選單中看到新的 [取得應用程式] 連結。 為了為這些新的與已改善的體驗騰出空間，已移除 [應用程式] 索引標籤。 若要查看已更新的畫面，請移至 [Intune 終端使用者應用程式的 UI 更新](./whats-new-app-ui.md)。 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>2020 年 4 月 20 日當週

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Microsoft 端點管理員租用戶連結：裝置同步及裝置動作<!-- 6317104, CM3555758  -->
Microsoft 端點管理員會將設定管理員和 Intune 整合至單一主控台。 從 Configuration Manager 2002 版開始，您可將 Configuration Manager 裝置上傳至雲端服務，並在系統管理中心對其採取動作。 如需詳細資訊，請參閱 [Microsoft 端點管理員租用戶連結：裝置同步及裝置動作](../../configmgr/tenant-attach/device-sync-actions.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Microsoft Office 365 專業增強版重新命名<!-- 6368143 -->
Microsoft Office 365 專業增強版正在重新命名為 **Microsoft 365 Apps 企業版**。 若要深入了解，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) (機器翻譯)。 我們通常會在文件中將其稱為 Microsoft 365 Apps。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可藉由選取 [應用程式] > [Windows] > [新增] 來找到應用程式套件。 如需新增應用程式的資訊，請參閱[將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>2020 年 4 月 13 日當週 (2004 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>在 Android Enterprise 裝上上管理 Outlook 的 S/MIME 設定<!-- 6517085   -->
您可以使用應用程式設定原則，在執行 Android Enterprise 的裝置上管理 Outlook 的 S/MIME 設定。 您也可以選擇是否允許裝置使用者啟用或停用 Outlook 設定中的 S/MIME。 若要使用 Android 的應用程式設定原則，請在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，前往 [應用程式] > [應用程式設定原則] > [新增] > [受控裝置]。 如需有關設定 Outlook 設定的詳細資訊，請參閱 [Microsoft Outlook 組態設定](../apps/app-configuration-policies-outlook.md)。

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>受控 Google Play 應用程式發行前測試<!-- 2681933  -->
使用 [Google Play 封閉式測試追蹤進行應用程式發行前測試](https://support.google.com/googleplay/android-developer/answer/3131213)的組織可以使用 Intune 來管理這些追蹤。 您可以選擇性地將發佈至 Google Play 生產前追蹤的應用程式指派給試驗群組，以便執行測試。 在 Intune 中，您可以看到應用程式是否具有已發佈的生產前組建測試追蹤，以及是否能夠將該追蹤指派給 AAD 使用者或裝置群組。 這項功能適用於所有目前支援的 Android Enterprise 案例 (工作設定檔、完全受控以及專用)。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可藉由選取 [應用程式] > [Android] > [新增] 來新增受控 Google Play 應用程式。 如需詳細資訊，請參閱[使用受控 Google Play 封閉式測試追蹤](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks)。

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft 小組現在已包含在 macOS 版的 Office 365 套件中<!-- 5903936  -->
在 Microsoft 端點管理員中獲指派 macOS 版 Microsoft Office 的使用者，除了現有 Microsoft Office 應用程式 (Word、Excel、PowerPoint、Outlook 以及 OneNote) 之外，也會獲得 Microsoft 小組。 Intune 會辨識已安裝其他 macOS 版 Office 應用程式的現有 Mac 裝置，並會在下次裝置簽入 Intune 時嘗試安裝 Microsoft 小組。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可藉由選取 [應用程式] > [macOS] > [新增] 來找到 macOS 版的 **Office 365 套件**。 如需詳細資訊，請參閱[使用 Microsoft Intune 將 Office 365 指派給 macOS 裝置](../apps/apps-add-office365-macos.md)。

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Android 應用程式設定原則更新<!-- 6113334  -->
已更新 Android 應用程式設定原則，讓系統管理員能夠在建立應用程式組態設定檔之前，先選取裝置註冊類型。 該功能已新增至註冊類型式 ([工作設定檔] 或 [裝置擁有者]) 的憑證設定檔帳戶中。  此更新提供下列各項：

1. 如果建立新的設定檔，並為裝置註冊類型選取了 [工作設定檔] 和 [裝置擁有者設定檔]，將無法為憑證設定檔與應用程式設定原則建立關聯。
2. 如果已建立新的設定檔，且僅選取 [工作設定檔]，則可以使用在 [裝置設定] 下建立的 [工作設定檔] 憑證原則。
3. 如果已建立新的設定檔，且僅選取 [裝置擁有者]，則可以使用在 [裝置設定] 下建立的 [裝置擁有者] 憑證原則。 

> [!IMPORTANT]
> 在此功能發行前 (2020 年 4 月發行 - 2004) 所建立現有原則若沒有任何與該原則建立關聯的憑證設定檔，則會預設為裝置註冊類型的 [工作設定檔] 和 [裝置擁有者設定檔]。 此外，在此功能發行前建立的現有原則若具有與其建立關聯的憑證設定檔，則僅會預設為 [工作設定檔]。

此外，我們將會新增 Gmail 與 Nine 電子郵件組態設定檔，這些組態設定檔適用於 [工作設定檔] 和 [裝置擁有者] 註冊類型，包括在這兩個電子郵件設定類型上使用憑證設定檔。  您在 [裝置設定] 的 [工作設定檔] 下所建立所有 Gmail 或 Nine 原則都會繼續套用至裝置，且不需要將其移至應用程式設定原則。

在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，可選取 [應用程式] > [應用程式設定原則] 來尋找應用程式設定原則。 若需要應用程式設定原則的詳細資訊，請參閱 [Microsoft Intune 的應用程式設定原則](../apps/app-configuration-policies-overview.md)。

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>裝置擁有權類型變更時的推播通知<!-- 5575875 -->
您可在基於隱私權考量，將裝置擁有權類型從 [個人] 變更為 [公司] 時，設定傳送推播通知給 Android 與 iOS 公司入口網站使用者。 根據預設，此推播通知設定為關閉。 您可在 Microsoft 端點管理員中找到這項設定，方法為選取 [租用戶管理] > [自訂]。 若要深入了解裝置擁有權如何影響終端使用者，請參閱[變更裝置擁有權](../enrollment/corporate-identifiers-add.md#change-device-ownership)。

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>[自訂] 窗格的群組目標支援<!-- 4722837  -->
您可以在 [自訂] 窗格中，將設定的目標設為使用者群組。 若要在 Intune 中尋找這些設定，請巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [租用戶系統管理] > [自訂]。 如需自訂的詳細資訊，請參閱[如何自訂 Intune 公司入口網站應用程式、公司入口網站及 Intune 應用程式](../apps/company-portal-app.md)。


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>iOS、iPadOS 和 macOS 上支援的多個「評估每個連線嘗試」隨選 VPN 規則<!-- 6424615  -->
Intune 使用者體驗允許相同 VPN 設定檔中有多個隨選 VPN 規則具有 [評估每個連線嘗試] 動作 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] 或 [macOS] 適用於平台 > [VPN] 適用於設定檔 > [自動 VPN] > [隨選])。

其只接受清單中的第一個規則。 此行為是固定的，而且 Intune 會評估清單中的所有規則。 每個規則都會以其出現在隨選規則清單中的順序進行評估。

> [!NOTE]
> 如果有現有的 VPN 設定檔使用這些隨選 VPN 規則，則下次變更 VPN 設定檔時，就會套用修正。 舉例來說，進行次要變更 (例如變更連線名稱)，然後儲存設定檔。
>
> 如果您使用 SCEP 憑證進行驗證，此變更會使此 VPN 設定檔的憑證重新發出。

適用於：
- iOS/iPadOS
- macOS

如需 VPN 設定檔的詳細資訊，請參閱[建立 VPN 設定檔](../configuration/vpn-settings-configure.md)。

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>iOS/iPadOS 裝置上 SSO 和 SSO 應用程式延伸模組設定檔中的其他選項<!-- 6504155   -->

在 iOS/iPadOS 裝置上，您可：
- 在 SSO 設定檔中 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] 作為平台 > [裝置功能] 作為設定檔 > [單一登入])，將 Kerberos 主體名稱設定為 SSO 設定檔中的安全性帳戶管理員 (SAM) 帳戶名稱。 
- 在 SSO 應用程式延伸模組設定檔中 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] 作為平台 > [裝置功能] 作為設定檔類型 > [單一登入應用程式延伸模組])，按幾下滑鼠便能使用新的 SSO 應用程式延伸模組類型設定 iOS/iPadOS Microsoft Azure AD 延伸模組。 您可在共用裝置模式中啟用裝置的 Azure AD 擴充功能，並將擴充功能特有的資料傳送至擴充功能。

適用於：
- iOS/iPadOS 13.0+

如需在 iOS/iPadOS 裝置上使用單一登入的詳細資訊，請參閱[單一登入應用程式延伸模組概觀](../configuration/device-features-configure.md#single-sign-on-app-extension)和[單一登入設定清單](../configuration/ios-device-features-settings.md#single-sign-on-app-extension)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>若有預設設定檔，請刪除 Apple Automated Device Enrollment 權杖<!--6393220 -->
之前，您無法刪除預設設定檔，這表示您無法刪除與其相關聯的 Automated Device Enrollment 權杖。 現在，您可以在下列情況下刪除權杖：
- 未將任何裝置指派給權杖
- 預設設定檔已存在。若要這麼做，請刪除預設設定檔，然後刪除相關聯的權杖。
如需詳細資訊，請參閱[從 Intune 刪除 ADE 權杖](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune)。

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>已擴大 Apple Automated Device Enrollment 和 Apple Configurator 2 裝置、設定檔和權杖的支援<!--3542402 -->
為了協助散發的 IT 部門和組織，Intune 現在支援每個權杖最多 1000 個註冊設定檔、每個 Intune 帳戶最多 2000 個 Automated Device Enrollment (先前稱為 DEP) 權杖，以及每個權杖最多 75000 個裝置。 每個註冊設定檔的裝置都沒有特定限制，但低於每個權杖的裝置數目上限。

Intune 現在最多支援 1000 個 Apple Configurator 2 設定檔。

如需詳細資訊，請參閱[支援的磁碟區](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume)。

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>所有裝置頁面的資料行項目變更<!--6967616 -->
在 [所有裝置] 頁面上，[管理者] 資料行已變更：
- 現在會顯示 Intune，而不是 MDM
- 現在會顯示「共同管理」，而不是「MDM/ConfigMgr 代理程式」

匯出值不會改變。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>信任的平台管理員 (TPM) 版本資訊現在位於 [裝置硬體] 頁面上<!--6224914 idmiss -->
您現在可以在裝置的硬體頁面上看到 TPM 版本號碼 ([Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > 選擇裝置 > [硬體] > 查看 [系統機殼] 底下)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>收集記錄，以針對指派給 macOS 裝置的指令碼進行更妥善的疑難排解<!-- 6359853  -->
您現在可以收集記錄，以改善針對指派給 macOS 裝置的指令碼進行的疑難排解。 您最多可以收集 60 MB (已壓縮) 或 25 個檔案 (以先發生者為準)。 如需詳細資訊，請參閱[使用記錄收集對 macOS 殼層指令碼原則進行疑難排解](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection)。
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全性

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>衍生認證用以佈建具有憑證的 Android Enterprise 完全受控裝置<!--4839592    -->
Intune 現在支援使用[衍生認證](../protect/derived-credentials.md)作為 Android 裝置的驗證方法。 衍生認證是國家標準暨技術研究院 (NIST) 800-157 標準的實作，用於將憑證部署至裝置。 我們對 Android 的支援擴展了我們對執行 iOS/iPadOS 之裝置的支援。

衍生認證仰賴個人識別驗證 (PIV) 或一般存取卡 (CAC)，如智慧卡。 若要取得其行動裝置的衍生認證，使用者必須從 Microsoft Intune 應用程式中啟動，並遵循您所使用之提供者獨有的註冊工作流程。 對於所有提供者來說，共同的要求是在電腦上使用智慧卡向衍生認證提供者進行驗證。 該提供者接著會將憑證發行至衍生自使用者智慧卡的裝置。

您可以使用衍生認證作為 VPN 和 Wi-Fi 的裝置組態設定檔的驗證方法。 您也可使用其進行應用程式驗證，以及針對支援 S/MIME 的應用程式進行 S/MIME 簽署和加密。

Intune 現在支援下列 Android 衍生認證提供者：
- Entrust Datacard
- Intercede

第三個提供者 DISA Purebred 將在未來的版本中提供給 Android 使用。

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Microsoft Edge 安全性基準現已正式運作<!--6586139 -->

新版本的 [Microsoft Edge 安全性基準](../protect/security-baselines.md#available-security-baselines)現已可用，並以公開上市 (GA) 的形式發行。 先前的 Edge 基準處於預覽狀態。  2020 年 4 月的新基準版本 (Edge 80 版及更新版本)。 

隨著此新基準的發行，您將無法再根據先前的基準版本建立設定檔，但您可繼續使用您以這些版本建立的設定檔。 您也可選擇[更新現有的設定檔，以使用最新的基準版本](../protect/security-baselines.md#change-the-baseline-version-for-a-profile)。 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>2020 年 4 月 6 日當週

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>macOS 裝置的新殼層指令碼設定<!-- 6884363 -->
設定 macOS 裝置的殼層指令碼時，您現在可以進行下列新設定： 
- 在裝置上隱藏指令碼通知
- 指令碼頻率
- 指令碼失敗時可重試的次數上限

如需詳細資訊，請參閱[在 macOS 裝置上的 Intune 中使用 Shell 指令碼](../apps/macos-shell-scripts.md)。

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>2020 年 3 月 30 日當週

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Microsoft 端點管理員系統管理中心的新網址<!-- 3704810 -->
為了與去年 Ignite 的 Microsoft 端點管理員公告保持一致，我們已將 Microsoft 端點管理員系統管理中心 (先前稱為 Microsoft 365 裝置管理) 的網址變更為 [https://endpoint.microsoft.com](https://endpoint.microsoft.com)。 舊的系統管理中心網址 ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) 將會繼續運作，但建議開始使用新的網址來存取 Microsoft 端點管理員系統管理中心。

如需詳細資訊，請參閱[使用 Microsoft 端點管理員系統管理中心簡化 IT 工作](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center)。  


### <a name="app-management"></a>應用程式管理  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>iOS 公司入口網站支援橫向模式<!--6048329  -->   
使用者現在可以自由選擇螢幕方向來註冊其裝置、尋找應用程式，以及取得 IT 支援。 除非使用者將螢幕鎖定在直向模式，否則應用程式會自動偵測並將螢幕調整為直向或橫向模式。  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>macOS 裝置的指令碼支援 (公開預覽)<!-- 4280361  -->
您可新增指令碼並將其部署至 macOS 裝置。 這項支援可讓您使用 macOS 裝置上的原生 MDM 功能，大幅延伸您能對 macOS 裝置所做的設定。 如需詳細資訊，請參閱[在 macOS 裝置上的 Intune 中使用 Shell 指令碼](../apps/macos-shell-scripts.md)。

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>2020 年 3 月 24 日當週

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>改善了在 Android 與 Android 企業裝置上建立裝置限制設定檔時的使用者介面體驗<!-- 5841361 -->
當建立 Android 或 Android 企業裝置的設定檔時，端點管理系統管理中心的體驗已有所更新。 此變更會影響下列裝置組態設定檔 ([裝置] > [組態設定檔] > [建立設定檔] > 選取 [Android 裝置管理員] 或 [Android 企業] 作為平台)：

- 裝置限制：Android 裝置管理員
- 裝置限制：Android Enterprise 裝置擁有者
- 裝置限制：Android Enterprise 工作設定檔

如需您可以設定之裝置限制的詳細資訊，請參閱 [Android 裝置系統管理員](../configuration/device-restrictions-android.md) 和 [Android 企業](../configuration/device-restrictions-android-for-work.md)。

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>已改善在 iOS/iPadOS 和 macOS 裝置上建立設定檔時的使用者介面體驗<!-- 5569002 5568997 -->
當建立 iOS 或 macOS 裝置的設定檔時，端點管理系統管理中心的體驗已有所更新。 此變更會影響下列裝置組態設定檔 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] 或 [macOS] 作為平台)：

- 自訂：iOS/iPadOS、macOS
- 裝置功能：iOS/iPadOS、macOS
- 裝置限制：iOS/iPadOS、macOS
- 端點保護：macOS
- 擴充功能：macOS
- 喜好設定檔案：macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>macOS 裝置上 [裝置功能] 中的 [從使用者設定隱藏] 設定<!-- 6524869 -->

當在 macOS 裝置上建立裝置功能組態設定檔時，有一項新的 [從使用者設定隱藏] 設定 ([裝置] > [組態設定檔] > [建立設定檔] > [macOS] 作為平台 > [裝置功能] 設定檔 > [登入項目])。

這項功能會設定 macOS 裝置上 [使用者和群組] 登入項目應用程式清單中的應用程式隱藏核取記號。 現有設定檔顯示清單中的這項設定為未設定。 若要進行這項設定，系統管理員可以更新現有的設定檔。

當設定為 [隱藏] 時，會核取應用程式的隱藏核取方塊，且使用者無法加以變更。 這也會在使用者登入其裝置之後，對使用者隱藏應用程式。

> [!div class="mx-imgBorder"]
> ![在使用者於 Microsoft Intune 和端點管理員中登入裝置之後，隱藏 macOS 裝置上的應用程式](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

如需您可進行的設定詳細資訊，請參閱 [macOS 裝置功能設定](../configuration/macos-device-features-settings.md)。

本功能適用於：

- macOS

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

- 將該窗格重新命名為 [自訂]。
- 改善設定的配置與設計。
- 改善設定的文字與工具提示。

若要在 Intune 中尋找這些設定，請巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [租用戶系統管理] > [自訂]。 如需現有自訂的資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>使用者的個人加密修復金鑰<!-- 6273943  -->
目前提供新的 Intune 功能，可讓使用者透過 Android 公司入口網站應用程式或透過 Android Intune 應用程式，擷取其 Mac 裝置的個人加密 **FileVault** 修復金鑰。 公司入口網站應用程式與 Intune 應用程式中都會提供一個連結，該連結將開啟 Chrome 瀏覽器並連線至 Web 公司入口網站，使用者可在該網站中看到存取其 Mac 裝置所需的 **FileVault** 修復金鑰。 如需加密的詳細資訊，請參閱[搭配 Intune 使用裝置加密](../protect/encrypt-devices.md)。

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>已將專用裝置註冊最佳化 <!-- 6114580  -->
我們正在將 Android Enterprise 專用裝置的註冊最佳化，以便能夠更輕鬆地將與 Wi-Fi 相關聯的 SCEP 憑證套用到 2019 年 11 月 22 日前註冊的專用裝置。 針對新註冊，Intune 應用程式將繼續安裝，但終端使用者將不再需要於註冊期間執行**啟用 Intune 代理程式**步驟。 安裝將會在背景中自動進行，而與 Wi-Fi 相關聯的 SCEP 憑證可以在不需與終端使用者互動的情況下進行部署和設定。  

隨著 Intune 服務後端部署，這些變更將在三月的整個月內分階段推出。 所有租用戶都將在三月結束時具備這個新行為。 如需相關資訊，請參閱 [Android Enterprise 專用裝置中的 SCEP 憑證支援](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147) \(英文\)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>在 Windows 裝置上建立系統管理範本時的新使用者體驗<!--5096036 -->
根據客戶的意見反應，以及我們移至新 Azure 全螢幕體驗的進展，我們使用了資料夾檢視來重建系統管理範本設定檔體驗。 我們尚未對任何設定或現有設定檔進行變更。 因此，您現有的設定檔將保持不變，且將可在新檢視中使用。 您仍然可以選取 [所有設定]，然後使用搜尋來瀏覽所有設定選項。 樹狀檢視會依電腦及使用者設定來分割。 您將在相關聯的資料夾中找到 Windows、Office 和 Edge 設定。  

適用於：
- Windows 10 和更新版本

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>使用 IKEv2 VPN 連線的 VPN 設定檔可以搭配 iOS/iPadOS 裝置使用 Always On<!-- 1947932   -->
在 iOS/iPadOS 裝置上，您可以建立使用 IKEv2 連線的 VPN 設定檔 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] 作為平台 > [VPN] 作為設定檔類型)。 現在，您可以搭配 IKEv2 設定 Always-On。 設定之後，IKEv2 VPN 設定檔會自動連線，並保持連線 (或快速重新連線) 至 VPN。 即使在網路之間移動或將裝置重新開機，仍會保持連線。

在 iOS/iPadOS 上，Always-On VPN 僅限用於 IKEv2 設定檔。

若要查看您可設定的 IKEv2 設定，請前往[在 Microsoft Intune 中於 iOS 裝置上新增 VPN 設定](../configuration/vpn-settings-ios.md#ikev2-settings)。

適用於：
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>在 Android 企業裝置的 OEMConfig 裝置組態設定檔中刪除套件組合與組合陣列<!-- 5550355   -->
在 Android Enterprise 裝置上，您會建立並更新 OEMConfig 設定檔 ([裝置] > [組態設定檔] > [建立設定檔] > [Android Enterprise] 作為平台 > [OEMConfig] 作為設定檔類型)。 使用者現在能夠使用 Intune 中的 [設定設計工具] 來刪除套件組合與套件組合陣列。

如需 OEMConfig 設定檔的詳細資訊，請參閱[在 Microsoft Intune 中透過 OEMConfig 來使用和管理 Android Enterprise 裝置](../configuration/android-oem-configuration-overview.md)。

適用於：
- Android 企業

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>設定 iOS/iPadOS Microsoft Azure AD SSO 應用程式延伸模組<!-- 5672534   -->
Microsoft Azure AD 小組已建立重新導向的單一登入 (SSO) 應用程式延伸模組，讓 iOS/iPadOS 13.0+ 的使用者能夠使用單一登入來存取 Microsoft 應用程式和網站。 先前使用 Microsoft Authenticator 應用程式進行代理驗證的所有應用程式，都將繼續透過新的 SSO 延伸模組來取得 SSO。 透過 Azure AD SSO 應用程式延伸模組版本，您可以使用重新導向的 SSO 應用程式延伸模組類型來設定 SSO 延伸模組 ([裝置] > [組態設定檔] > [建立設定檔] > [iOS/iPadOS] 作為平台 > [裝置功能] 作為設定檔類型 > [單一登入應用程式延伸模組])。

適用於：
- iOS 13.0 與更新版本
- iPadOS 13.0 和更新版本

如需 iOS SSO 應用程式延伸模組的詳細資訊，請參閱[單一登入應用程式延伸模組](../configuration/device-features-configure.md#single-sign-on-app-extension)。

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>已從 iOS/iPadOS 裝置限制設定檔中移除 [修改企業應用程式信任設定] 設定<!-- 6225131   -->
在 iOS/iPadOS 裝置上，您可以建立裝置限制設定檔 ([裝置] > [組態設定檔] > [建立設定檔] > 選取 [iOS/iPadOS] 作為平台 > 選取 [裝置限制] 作為設定檔類型)。 Apple 已移除 [修改企業應用程式信任設定] 設定，同時也會從 Intune 中移除此設定。 如果您目前在設定檔中使用此設定，則不會有任何影響，而且會從現有設定檔中加以移除。 此設定也會從 Intune 的所有報告中移除。

適用於：
- iOS/iPadOS

若要查看您可以限制的設定，請前往[允許或限制功能的 iOS 和 iPadOS 裝置設定](../configuration/device-restrictions-ios.md)。

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>疑難排解：暫止的 MAM 原則通知已變更為資訊圖示<!--6348954 -->
[疑難排解] 刀鋒視窗上暫止 MAM 原則的通知圖示已變更為資訊圖示。

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>設定合規性政策時的 UI 更新<!-- 3961639    -->

我們已在 Microsoft 端點管理員中更新[建立合規性政策](../protect/create-compliance-policy.md#create-the-policy)的 UI ([裝置] > [合規性政策] > [原則] > [建立原則])。 我們提供一個新的使用者體驗，其中包含您先前使用的相同設定和詳細資料。 新體驗會遵循類似精靈的流程來建立合規性政策，並包含可讓您在其中為原則新增「指派」的新頁面和 [檢閱 + 建立] 頁面，而您可以在建立原則之前，於此頁面檢閱設定。

#### <a name="retire-noncompliant-devices---1827291---------"></a>淘汰不符合規範的裝置<!-- 1827291       -->
我們已為不符合規範的裝置新增一個動作，讓您可新增至任何原則，以[淘汰不符合規範的裝置](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance)。  新動作 (**淘汰不符合規範的裝置**) 不僅會從裝置中移除所有公司資料，還會導致 Intune 無法管理該裝置。  此動作會在觸達設定的值 (以天為單位)，且裝置在該時間點變成符合淘汰資格時執行。 最小值為 30 天。  明確的 IT 系統管理員核准必須使用「淘汰不符合規範的裝置」區段來淘汰裝置，系統管理員可以在該區段中淘汰所有符合條件的裝置。

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>iOS 企業 Wi-Fi 設定檔中的 WPA 與 WPA2 支援<!--6215273   -->
[適用於 iOS 的企業級 Wi-Fi 設定檔](../configuration/wi-fi-settings-ios.md#enterprise-profiles)現在支援 [安全性類型] 欄位。 針對 [安全性類型]，您可以選取 [WPA Enterprise] 或 [WPA/WPA2 Enterprise]，然後指定 [EAP 類型] 的選取項目。  ([裝置] > [組態設定檔] > [建立設定檔]、選取 [iOS/iPadOS] 作為「平台」，然後選取 [Wi-Fi] 作為「設定檔」)。 

新的企業級選項與可供適用於 iOS 之基本 Wi-Fi 設定檔使用的選項類似。

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>適用於憑證、電子郵件、VPN 及 Wi-Fi、VPN 設定檔的新使用者體驗<!-- 5615208   -->
我們已在端點管理系統管理中心，更新用來建立及修改下列設定檔類型的[使用者體驗](../configuration/device-profile-create.md) ([裝置] > [組態設定檔] > [建立設定檔])。 新體驗與先前設定相同，但會使用類似精靈的體驗，且不太需要水平捲動。 您不需要修改現有設定也能使用新的體驗。

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
您可以設定在具有提示 (或沒有提示) 的情況下，讓使用者能夠在 Android 與 iOS 裝置的公司入口網站中註冊裝置，或讓使用者無法註冊裝置。 若要在 Intune 中尋找這些設定，請巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [租用戶系統管理] > [自訂] > [編輯] > [裝置註冊]。  

對裝置註冊設定的支援需要終端使用者具有下列公司入口網站版本：
-    iOS 上的公司入口網站：4.4 版或更新版本
-    Android 上的公司入口網站：5.0.4715.0 或更新版本

如需現有公司入口網站自訂的詳細資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>[Android 裝置概觀] 頁面上的新 Android 報告<!-- 5435435   -->
我們已在 [Android 裝置概觀] 頁面中，將報告新增至 Microsoft 端點管理員系統管理主控台，以顯示每個裝置管理解決方案中已註冊的 Android 裝置數量。 此圖表 (如同 Azure 主控台中已有的相同圖表) 會顯示工作設定檔、完全受控、專用，以及已註冊裝置系統管理員的裝置數量。 若要查看報告，請選擇 [裝置] > [Android] > [概觀]。

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>引導使用者從 Android 裝置系統管理員管理至工作設定檔管理<!--5857738   -->
我們將發行 Android 裝置系統管理員平台的新合規性設定。 此設定可供在裝置由裝置系統管理員管理時，將其設為不符合規範。

在這些不符合規範的裝置上，於 [更新裝置設定] 頁面中，使用者會看到 [移至新的裝置管理安裝程式] 訊息。 如果使用者點選 [解決] 按鈕，系統將引導完成下列動作：

1. 從裝置系統管理員管理取消註冊
2. 在工作設定檔管理中註冊
3. 解決合規性問題 
 
為了透過 Android 企業轉移到更加現代化、豐富且安全的裝置管理，Google 正在減少新 Android 版本中裝置系統管理員的支援。  Intune 只能為執行 Android 10 和更新版本的裝置系統管理員所管理 Android 裝置提供完整支援，且支援僅提供至 2020 年度第 2 季。 在此期間過後，執行 Android 10 或更新版本的裝置系統管理員所管理裝置 (Samsung 除外) 將無法再完全受控。 尤其受影響的裝置不會再收到新密碼要求。

如需此設定的詳細資訊，請參閱[將 Android 裝置從裝置系統管理員移至工作設定檔管理](../enrollment/android-move-device-admin-work-profile.md)。 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>監視及疑難排解

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>資料倉儲現在提供 MAC 位址<!-- 6123680  -->
Intune 資料倉儲會在 `device` 實體中提供 MAC 位址作為新屬性 (`EthernetMacAddress`)，以允許系統管理員在使用者與主機 MAC 位址之間相互關聯。 此屬性有助於觸達特定使用者，並針對網路上發生的事件進行疑難排解。 系統管理員也可以在 [Power BI 報告](../developer/reports-proc-get-a-link-powerbi.md)中使用此屬性來建置更豐富的報告。 如需詳細資訊，請參閱 Intune 資料倉儲[裝置](../developer/intune-data-warehouse-collections.md#devices)實體。

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>其他資料倉儲裝置庫存屬性<!-- 6125732  -->
其他裝置庫存屬性均可使用 Intune 資料倉儲來取得。 下列屬性現在會透過 [devices](../developer/reports-ref-devices.md#devices) 搶鮮版 (Beta) 集合來公開：
- `ethernetMacAddress` - 此裝置的唯一網路識別碼。
- `model` - 裝置型號。
- `office365Version` - 安裝於裝置上的 Office 365 版本。
- `windowsOsEdition` - 作業系統版本。

下列屬性現在會透過 [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) 搶鮮版 (Beta) 集合來公開：
- `physicalMemoryInBytes` - 實體記憶體 (以位元組為單位)。
- `totalStorageSpaceInBytes`：儲存體容量總計 (以位元組為單位)。

如需詳細資訊，請參閱 [Microsoft Intune 資料倉儲 API](../developer/reports-nav-intune-data-warehouse.md)。

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>更新說明及支援工作流程以支援其他服務<!-- 5654170   -->
我們已更新 Microsoft 端點管理員系統管理中心的 [說明及支援] 頁面，現在可在其中[選擇您所使用的管理類型](../fundamentals/get-support.md#options-to-access-help-and-support)。 透過這項變更，您將可以從下列管理類型中選取：

- Configuration Manager (包含電腦分析)
- Intune
- 共同管理

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>安全性

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>使用安全性系統管理員的焦點原則預覽作為端點安全性的一部分<!--6131401  -->
在公開預覽中，我們已在 Microsoft 端點管理系統管理中心的 [端點安全性] 節點下方新增數個新的原則群組。 身為安全性系統管理員，您可以使用這些新原則，來將焦點放在裝置安全性的特定層面，以管理不同的相關設定群組，而不會產生較大裝置設定原則主體的額外負荷。

除了新的「適用於 Microsoft Defender 防毒軟體的防毒軟體原則」(請參閱下文) 之外，這其中每個新預覽原則和設定檔的設定，都是您目前可能已經透過[裝置組態設定檔](../configuration/device-profile-create.md)設定的相同設定。

以下是所有處於預覽狀態的新原則類型及其可用的設定檔類型：

- **防毒軟體 (預覽)** ：
  - macOS：
    - **防毒軟體**：管理適用於 macOS 的 [防毒軟體原則設定](../protect/antivirus-microsoft-defender-settings-macos.md)，以管理 [Mac 版 Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) \(部分機器翻譯\)。

  - Windows 10 及更新版本：
    - **Microsoft Defender 防毒軟體**：管理雲端保護、防毒軟體的排除項目、補救、掃描選項等[防毒軟體原則設定](../protect/antivirus-microsoft-defender-settings-windows.md)。

      「Microsoft Defender 防毒軟體」的防毒軟體設定檔是一種例外狀況，其引進了可在裝置限制設定檔中找到的新設定執行個體。 這些新的防毒軟體設定：

        - 與在裝置限制中找到的設定相同，但可針對在設定為裝置限制時無法使用的設定支援第三個選項。
        - 在將適用於 Endpoint Protection 的[共同管理工作負載滑動軸](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)設定為 Intune 時，會套用至與 Configuration Manager 共同管理的裝置。

     規劃使用新的 [防毒軟體] > [Microsoft Defender 防毒軟體] 設定檔，來替代透過裝置限制設定檔進行設定。

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

您可以設定傳遞最佳化代理程式，以根據指派在背景或前景模式下載 Win32 應用程式內容。 針對現有的 Win32 應用程式，內容會繼續以背景模式下載。 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [應用程式] > [所有應用程式] >  選取 [Win32 應用程式] > [屬性]。 選取位於 [指派] 旁的 [編輯]。  在 [必要] 區段中，選取 [模式] 底下的 [包含]，以編輯指派。  您會在 [應用程式設定] 區段中看到新的設定。 如需傳遞最佳化的詳細資訊，請參閱 [Win32 應用程式管理 - 傳遞最佳化](../apps/apps-win32-app-management.md#delivery-optimization)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>變更 Windows 裝置的主要使用者<!-- 3794742   -->
您可變更 Windows 混合式和 Azure AD 加入裝置的主要使用者。 若要執行此操作，請前往 [Intune] > [裝置] > [所有裝置] > 選擇裝置 > [屬性] > [主要使用者]。 如需詳細資訊，請參閱[變更裝置的主要使用者](../remote-actions/find-primary-user.md#change-a-devices-primary-user)。

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
您現在可以針對下列遠端動作發出大量命令：重新啟動、重新命名、AutoPilot 重設、抹除及刪除。 若要查看新的大量動作，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > [所有裝置] > [大量動作]。

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>改善了所有裝置清單的搜尋、排序以及篩選<!--6179023-->
已改善 [所有裝置] 清單，以獲得更佳的效能、搜尋、排序以及篩選。 如需詳細資訊，請參閱[此支援提示](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946) (英文)。  

### <a name="app-management"></a>應用程式管理  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>改善了 Android 公司入口網站登入體驗    
我們已更新 Android 公司入口網站應用程式中數個登入畫面的版面配置，讓使用者獲得更加現代化且簡潔的體驗。 若要查看改善，請參閱[應用程式 UI 中的新功能](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui)。

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
現在從 [裝置] > [所有裝置] 清單匯出已改為壓縮的 CSV 格式。


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>2020 年 2 月 17 日當週 (2002 服務版本)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>應用程式管理

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>macOS 版 Microsoft Defender 進階威脅防護 (ATP) 應用程式<!-- 5424618 -->
Intune 提供一種簡單的方式，以將適用於 macOS 的 Microsoft Defender 進階威脅防護 (ATP) 應用程式部署至受控 Mac 裝置。 如需詳細資訊，請參閱[使用 Microsoft Intune 將 Microsoft Defender ATP 新增至 macOS 裝置](../apps/apps-advanced-threat-protection-macos.md)，以及[適用於 Mac 的 Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (機器翻譯)。  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>裝置設定

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>在 iOS 裝置上透過 Cisco AnyConnect VPN 啟用網路存取控制 (NAC)<!-- 4860111  -->
在 iOS 裝置上，您可以建立 VPN 設定檔，並使用不同的連線類型，包含 Cisco AnyConnect ([裝置設定] > [設定檔] > [建立設定檔] > [iOS] 平台 > [VPN] 設定檔類型 > [Cisco AnyConnect] 連線類型)。

您可以透過 Cisco AnyConnect 啟用網路存取控制 (NAC)。 若要使用此功能：

1. 在 [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) (Cisco 身分識別服務引擎系統管理員指南) 中，使用**將 Microsoft Intune 設定為 MDM 伺服器**中的步驟，在 Azure 中設定 Cisco 身分識別服務引擎 (ISE)。
2. 在 Intune 裝置設定檔中，選取 [啟用網路存取控制 (NAC)] 設定。

若要查看所有可用的 VPN 設定，請前往[在 iOS 裝置上進行 VPN 設定](../configuration/vpn-settings-ios.md)。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>裝置註冊

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>[Apple MDM Push Certificate] 頁面上的序號<!--5947765  -->
[Apple MDM Push Certificate] 頁面現在會顯示序號。 如果您無法存取建立憑證的 Apple ID，則需要序號來重新取得 Apple MDM Push Certificate 的存取權。 若要查看序號，請前往 [裝置] > [iOS] > [iOS 註冊] > [Apple MDM Push Certificate]。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>裝置管理

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>將 OS 更新推送至已註冊 iOS/iPadOS 裝置的新更新排程選項<!--5879689  -->
為 iOS/iPadOS 裝置的作業系統更新規劃排程時，您將可以選擇下列選項。 這些選項適用於使用 Apple Business Manager 或 Apple School Manager 註冊類型的裝置。
- 在下次簽入時更新
- 在排程時間的期間內更新
- 在排程時間的期間外更新

針對後面兩個選項，您可以建立多個時間範圍。

若要查看新選項，請前往 MEM > [裝置] > [iOS] > [iOS/iPadOS 的更新原則] > [建立設定檔]。

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>選擇要推送至已註冊裝置的 iOS/iPadOS 更新<!--5879689  -->
您可以選擇特定的 iOS/iPadOS 更新 (除了最新更新之外)，以推送至使用 Apple Business Manager 或 Apple School Manager 註冊的裝置。 這些裝置必須將裝置設定原則設為將軟體更新可見度延遲數天。 若要查看這項功能，請前往 MEM > [裝置] > [iOS] > [iOS/iPadOS 的更新原則] > [建立設定檔]。



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
我們藉由從數個 UI 位置中移除了「安全性基準」，以此合併在 Microsoft 端點管理員系統管理中心尋找[安全性基準](../protect/security-baselines.md)的路徑。 若要尋找安全性基準，您現在可以使用下列路徑：[端點安全性] > [安全性基準]。

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>針對匯入的 PKCS 憑證擴大支援<!-- 6044197  -->
我們針對使用[匯入的 PKCS 憑證](../protect/certificates-imported-pfx-configure.md#supported-platforms)擴大了支援，藉以支援「Android Enterprise 完全受控裝置」。 一般而言，匯入 PFX 憑證會用於 S/MIME 加密案例，其中使用者的所有裝置上都需要其加密憑證，以便進行電子郵件解密。

下列平台支援匯入 PFX 憑證：

- Android - 裝置管理員
- Android Enterprise - 完全受控
- Android Enterprise - 工作設定檔
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>查看裝置的端點安全性設定<!-- 6206460  -->
我們更新了 Microsoft 端點管理員系統管理中心內的選項名稱，以便檢視[適用於特定裝置的端點安全性設定](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device)。 此選項已重新命名為 [端點安全性設定]，因為其會顯示適用的安全性基準，以及在安全性基準以外建立的其他原則。 在先前，此選項的名稱為「安全性基準」。

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>角色型存取控制

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Intune 角色使用者介面變更即將推出<!--5801612   -->
[Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [租用戶系統管理] > [角色] 使用者介面已改善為更容易使用且直覺的設計。 此體驗提供您現在所使用的相同設定和詳細資料，但新體驗是採用精靈型程序。

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
我們已從公司入口網站中的 Android 工作設定檔註冊流程移除 [下一步是什麼?] 畫面，以簡化使用者體驗。 移至[使用 Android 工作設定檔註冊](../user-help/enroll-device-android-work-profile.md)，以查看已更新的 Android 工作設定檔註冊流程。  

#### <a name="company-portal-app-improved-performance---6178652---"></a>公司入口網站應用程式已改進效能<!-- 6178652 -->
公司入口網站應用程式已更新，以支援使用 ARM64 處理器之裝置 (例如 Surface Pro X) 的效能改進。先前，公司入口網站在模擬的 ARM32 模式中運作。 現在，在 10.4.7080.0 和更新版本中，公司入口網站應用程式是針對 ARM64 原生地編譯的。 如需公司入口網站應用程式的詳細資訊，請參閱[如何設定 Microsoft Intune 公司入口網站應用程式](../apps/company-portal-app.md)。

## <a name="whats-new-archive"></a>新功能封存
針對過去幾個月，請參閱[新功能封存](whats-new-archive.md)。

## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


