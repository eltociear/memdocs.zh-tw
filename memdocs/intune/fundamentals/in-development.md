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
ms.openlocfilehash: 107ac1e2aef18bcb72a6fe1f94eade23c3f85319
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216513"
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
<!--## App management-->


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


<!-- ***********************************************-->
<!--## Device enrollment-->



<!-- ***********************************************-->
## <a name="device-management"></a>裝置管理

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
