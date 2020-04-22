---
title: 新增 1710 版 | Microsoft Docs
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 1710 版中變更和所引進新功能的詳細資料。
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c541c257d885ee5cba9e174a86a6859b078c8594
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702406"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Configuration Manager 1710 版中的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 更新 1710 版的最新分支以主控台內的更新形式提供，適用於先前安裝且執行 1610、1702 或 1706 版本的站台。

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 1710 版中變更的摘要](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran) \(機器翻譯\)。

下列針對此版本的其他變更也已可供使用：
- [適用於 Configuration Manager 最新分支 1710 版的更新彙總套件](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v) \(機器翻譯\)
- [適用於 Configuration Manager 最新分支 1710 版的更新彙總套件 2](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch) \(機器翻譯\)

> [!TIP]  
> 若要安裝新的站台，您必須使用 Configuration Manager 的基準版本。  
>
> 深入了解：    
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)  
> - [在站台安裝更新](../../servers/manage/updates.md)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

下列各節提供 Configuration Manager 1710 版中推出的變更和新功能詳細資料。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站台基礎結構

### <a name="updates-for-peer-cache-----sms500850---"></a>對等快取的更新  <!-- sms500850 -->
從這個版本開始，對等快取不再是發行前版本功能。  這個版本中並未推出其他對等快取的變更。 如需詳細資訊，請參閱 [Configuration Manager 用戶端的對等快取](../hierarchy/client-peer-cache.md)。

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Azure Government 雲端的雲端發佈點支援   <!-- sms491428 -->
您現在可以在 Azure Government 雲端中使用[雲端式發佈點](../hierarchy/use-a-cloud-based-distribution-point.md)。   

### <a name="inventory-default-unit-revision----sms503697---"></a>修訂清查預設單位 <!-- sms503697 -->
因為裝置現在包含大小以 GB、TB 和更高級別計算的硬碟，所以這個版本將許多檢視使用的預設單位 (SMS_Units) 從 MB 變更成 GB。 例如，v_gs_LogicalDisk.FreeSpace 值現在回報 GB 單位。


<!-- ## Migration  -->


## <a name="client-management"></a>用戶端管理

### <a name="co-management-for-windows-10-devices"></a>Windows 10 裝置的共同管理    
<!-- 1350871 -->
在先前的 Windows 10 更新中，您已可以將 Windows 10 裝置同時聯結到內部部署的 Active Directory (AD) 及雲端式 Azure AD (混合式 Azure AD)。 自 Configuration Manager 1710 版開始，共同管理能夠利用這項改善，讓您使用 Configuration Manager 和 Intune 來同時管理多部 1709 版 (又稱 Fall Creators Update) 的 Windows 10 裝置。 這個解決方案能讓您從傳統管理過渡到現代化管理，並提供您使用分段式方法來完成轉換。 如需詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../../comanage/overview.md)。

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>從 Configuration Manager 主控台重新啟動電腦  <!-- 1356283 -->
從此版本開始，您可以使用 Configuration Manager 主控台來識別需要重新啟動的用戶端裝置，然後使用用戶端通知動作來重新啟動這些裝置。

請參閱[如何管理用戶端](../../clients/manage/manage-clients.md#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>應用程式管理
### <a name="improvements-for-run-scripts------1236459---"></a>執行指令碼的加強   <!-- 1236459 -->
這個版本對**執行指令碼**功能帶來了多項改進，讓您可以部署 PowerShell 指令碼，以在受管理裝置上執行。 這項功能最初於 1706 版推出。

增強功能包括：
- 使用安全性範圍協助控制可以使用執行指令碼的人員
- 即時監視您執行的指令碼
- 指令碼參數會顯示在 [建立指令碼精靈] 中，支援認證，並會識別為強制或選擇性參數。

如需關於執行指令碼的詳細資訊，請參閱[建立與執行指令碼](../../../apps/deploy-use/create-deploy-scripts.md)。

### <a name="new-mobile-application-management-policy-settings"></a>新的行動應用程式管理原則設定
<!-- 1324760 -->
行動應用程式管理原則設定已新增了下列設定：
- **停用連絡人同步**：防止應用程式將資料儲存至裝置上的原生「連絡人」應用程式。
- **停用列印**：防止應用程式列印公司或學校資料。

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>軟體中心已不會再使大於 250x250 的圖示出現失真  
<!-- 1356194 -->

在此版本中，軟體中心已不會再使大於 250x250 的圖示出現失真。 軟體中心先前會使這些圖示變得模糊不清。 您現在可以設定像素尺寸最多為 512x512 的圖示，該圖示於顯示時將不會出現失真。

若要在軟體中心中為應用程式新增圖示，請參閱[建立應用程式](../../../apps/deploy-use/create-applications.md)。

## <a name="operating-system-deployment"></a>作業系統部署
 > [!TIP]   
 > <!-- 1354281 -->
 > 自 Windows 10 1709 版 (也稱為 Fall Creators Update) 開始，Windows Media 即包含多個版本。 設定工作順序以使用作業系統升級套件或作業系統映像時，請務必選取[支援由 Configuration Manager 使用的版本](../configs/support-for-windows-10.md#windows-10-as-a-client)。

### <a name="add-child-task-sequences-to-a-task-sequence"></a>將子工作順序新增至工作順序
<!-- 1261338 -->

您可以新增一個會執行另一個工作順序的新工作順序步驟，這會在工作順序之間建立父子式關係。 這可讓您建立更多可以重複使用的模組化工作順序。  

若要深入了解子工作順序，請參閱[子工作順序](../../../osd/understand/task-sequence-steps.md#child-task-sequence)。

## <a name="software-center-customization"></a>軟體中心自訂
<!-- 1351224 -->
您可以在 [軟體中心] 上加入企業品牌元素，以及指定索引標籤的可見性。 您可以加入 [軟體中心] 特定的公司名稱、設定 [軟體中心] 組態色彩佈景主題、設定公司標誌，以及設定用戶端裝置的可見索引標籤。

如需詳細資訊，請參閱[規劃和設定應用程式管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。

## <a name="software-updates"></a>軟體更新

### <a name="surface-driver-updates-----1098490---"></a>Surface 驅動程式更新  <!-- 1098490 -->
從這個版本開始，管理 Surface 驅動程式更新不再是發行前版本功能。  


## <a name="reporting"></a>報告

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>限制 Windows 10 增強資料只傳送與 Windows Analytics 裝置健全狀況相關的資料
<!-- 1356148 -->

現在您可以將 Windows 10 診斷資料收集層級設定為 [增強 (受限)]  。 在 Windows 10 1709 版或更新版本中，此設定讓您能夠獲取可對環境中之裝置採取動作的深入解析，而不需讓裝置回報 [增強式]  層級中的所有資料。

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>行動裝置管理

### <a name="actions-for-non-compliance"></a>處理不符合規範狀況的動作 
<!--1321366 -->    
您現在已可為套用到不合規範之裝置的動作，設定按時間排序的順序。 例如，您可透過電子郵件來通知使用者不合規的裝置，或將那些裝置標記為不合規。

### <a name="windows-10-arm64-device-support"></a>Windows 10 ARM64 裝置支援
<!-- 1355000 -->

當執行 Windows 10 的 ARM 64 裝置可用時，即支援混合式行動裝置管理 (MDM) 案例。

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Configuration Manager 主控台中改進的 VPN 設定檔體驗 
<!-- 1318232 -->

我們在此版本中更新了 VPN 設定檔精靈和屬性頁，以顯示所選平台的合適設定：


- 每個平台都有自己的工作流程，這表示新的 VPN 設定檔只包含平台支援的設定。
- [支援的平台]  頁面現在會出現在 [一般]  頁面之後。  您現在要先選擇平台再設定屬性值。
- 當平台設定為 [Android]  、[Android for Work]  或 [Windows Phone 8.1]  時，就不需要也不會顯示 [支援的平台]  頁面。
- Configuration Manager 用戶端型工作流程已結合混合式行動裝置 (MDM) 用戶端型 Windows 10 工作流程，它們支援相同的設定。
- 每個平台工作流程只包含適用於該工作流程的設定。  例如，Android 的工作流程包含適用於 Android 的設定，適用於 iOS 或 Windows 10 行動裝置版的設定不會再出現在 Android 的工作流程中。
- [自動 VPN] 頁面已淘汰並予移除。

這些變更適用於新的 VPN 設定檔。  

為將相容性風險降至最低，不變更現有的 VPN 設定檔。  當您編輯現有的設定檔時，顯示的設定一如當初建立設定檔時一樣。  

如需詳細資訊，請參閱[行動裝置上的 VPN 設定檔](../../../protect/deploy-use/vpn-profiles.md)。

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>對密碼編譯的支援有限：新一代 (CNG) 憑證 <!-- 1356191 -->

Configuration Manager 對密碼編譯的支援有限：新一代 (CNG) 憑證。 設定管理員用戶端可以搭配 CNG 金鑰儲存提供者 (KSP) 中的私密金鑰來使用 PKI 用戶端驗證憑證。 有 KSP 的支援，設定管理員用戶端可以支援硬體式私密金鑰，例如 PKI 用戶端驗證憑證的 TPM KSP。

如需詳細資訊，請參閱 [CNG 憑證概觀](../network/cng-certificates-overview.md)。

## <a name="protect-devices"></a>保護裝置

### <a name="create-and-deploy-exploit-guard-policies"></a>建立與部署惡意探索防護原則
<!-- 1355468 -->

您可以[建立與部署原則](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md)，用以管理 Windows Defender 惡意探索防護的全部四個元件，包含攻擊面縮減、資料夾存取控制、惡意探索防護以及網路保護。

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>建立及部署 Windows Defender 應用程式防護原則
<!-- 1351960 -->

您可以使用 Configuration Manager Endpoint Protection，[建立及部署 Windows Defender 應用程式防護原則](../../../protect/deploy-use/create-deploy-application-guard-policy.md)。

### <a name="device-guard-policy-changes"></a>Device Guard 原則變更
<!-- 1355092 -->
Device Guard 原則有下列三項相關變更：

- Device Guard 原則已重新命名為 Windows Defender 應用程式控制原則。 因此，像 [建立 Device Guard 原則]  精靈這樣的名稱，現在已名為 [建立 Windows Defender 應用程式控制原則]  精靈。
- 使用 Windows 1709 版 Fall Creators Update 的裝置不需要重新啟動，就能套用 Windows Defender 應用程式控制原則。 重新啟動仍是預設，不過您也可以[關閉重新啟動](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)。
- 您可以[設定裝置來自動執行 Intelligent Security Graph 信任的軟體](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)。





## <a name="next-steps"></a>後續步驟
當您已準備好要安裝此版本時，請參閱 [Configuration Manager 的更新](../../servers/manage/updates.md)。
