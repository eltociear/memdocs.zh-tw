---
title: 開發中 - Microsoft Intune
titleSuffix: ''
description: 正在開發的 Microsoft Intune 功能
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764198"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>適用於 Android 的公司入口網站引導使用者在工作設定檔註冊之後取得應用程式 <!-- 6103999  -->
我們正在改善公司入口網站中的應用程式內指引，讓使用者能更輕鬆地尋找及安裝應用程式。  使用者在註冊工作設定檔管理之後會看到一則訊息，告知其可在有徽章的 Google Play 版本中找到所建議應用程式。 使用者也會在左側公司入口網站選單中看到新的 [取得應用程式]  連結。 為了讓這些新的和已改善體驗得以完成，將會移除 [應用程式]  索引標籤。 

<!-- ***********************************************-->
## <a name="device-configuration"></a>裝置設定

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>即將更新 Windows 平台的裝置組態設定檔設定和值<!-- 4091122 -->
當您建立 Windows 平台的裝置組態設定檔時 ([裝置]   > [組態設定檔]   > [建立設定檔]  > 任意 [Windows]  平台選項)，部分設定和其值與 CSP 不相同，而可能造成混淆。 即將更新設定名稱和其值，以便更加清楚地表示。

適用於：

- Windows 10 和更新版本裝置組態設定檔
- Windows Holographic for Business 裝置組態設定檔
- Windows 8.1 裝置組態設定檔
- Windows Phone 8.1 裝置組態設定檔

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>macOS Endpoint Protection 裝置設定原則的新 FileVault 設定<!-- 5459801   -->
我們將在 [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) 範本內新增設定至 [FileVault] 類別：隱藏修復金鑰。 ([裝置]   > [組態設定檔]   > [建立設定檔]  ，選取 [macOS]  作為「平台」  ，然後選取 [Endpoint Protection]  作為「設定檔類型」  )。 此設定會在 FileVault 2 加密期間隱藏來自終端使用者的個人金鑰。 裝置使用者可以隨時從 iOS 公司入口網站應用程式，或從已加密 macOS 裝置的公司入口網站，查看其個人的修復金鑰。 若要查看個人修復金鑰，使用者可以前往 [裝置詳細資料]，然後按一下「取得修復金鑰」  。

此設定不適用於先前建立的原則。 您必須重新建立 FileVault 原則，才能進行並使用此設定。 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>裝置註冊

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>「攜帶您自己的裝置」可使用 VPN 進行部署<!--5015344 -->
這項功能可能會延遲。

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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>在端點安全性中複製原則<!-- 5892558   -->
您可在 Microsoft Endpoint Manager 系統管理中心的端點安全性節點中，選取已建立的原則，然後複製該原則以建立複本。  您能夠複製的原則包括針對下列項目所建立原則： 

- 防毒
- 磁碟加密
- 防火牆
- 端點偵測與回應
- 受攻擊面縮小
- 帳戶防護

複製會建立原始原則的複本，您接著可重新命名和編輯該複本。 複本不會包含原始原則的指派。

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>端點安全性防火牆原則的新設定檔<!-- 5653324   -->
作為預覽，我們會將 Windows 10 和更新版本的額外設定檔新增至 Intune 端點安全性中防火牆原則 ([端點安全性]   > [防火牆]   > [建立原則]  > 選取 [Windows 10 及更新版本]  )。 

這個新設定檔的每個執行個體最多可支援 150 個自訂「Microsoft Defender 防火牆規則」  。 Microsoft Defender 防火牆規則設定檔可供定義更精細的 Windows 防火牆規則，以允許或封鎖 Windows 10 中的連接埠和應用程式。

<!-- ***********************************************-->
## <a name="notices"></a>通知

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>請參閱

如需近期發展的詳細資料，請參閱 [Microsoft Intune 的新功能](whats-new.md)。



