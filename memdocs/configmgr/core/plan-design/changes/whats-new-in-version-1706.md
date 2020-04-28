---
title: 1706 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 1706 版中變更和所引進新功能的詳細資料。
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a4fa056c9c0708d2cecc0ca5f244e134e22ad10b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073704"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Configuration Manager 1706 版中的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 更新 1706 版的最新分支以主控台內的更新形式提供，適用於先前安裝且執行 1606、1610 或 1702 版本的站台。

> [!TIP]  
> 若要安裝新的站台，您必須使用 Configuration Manager 的基準版本。  
>
> 深入了解：    
> - [安裝新的站台](https://technet.microsoft.com/library/mt590197.aspx)  
> - [在站台安裝更新](https://technet.microsoft.com/library/mt607046.aspx)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)  

下列各節提供 Configuration Manager 1706 版中所推出之變更和新功能的詳細資料。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站台基礎結構

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Windows 10 和 Office 365 快速安裝檔案的用戶端對等快取支援  
<!-- 1352486 -->
從這個版本開始，對等快取支援適用於 Windows 10 的內容發佈快速安裝檔案和適用於 Office 365 的更新檔案。 支援此變更不需要任何其他設定。

### <a name="updates-for-the-data-warehouse"></a>針對資料倉儲的更新
<!-- 1277922 -->
資料倉儲已不再是發行前版本功能。 我們也已更新必要條件，以包含針對 SQL Server Always On 可用性群組上的資料庫，以及容錯移轉叢集的支援。 如需詳細資訊，請參閱[資料倉儲服務點](../../servers/manage/data-warehouse.md)。

### <a name="accessibility-improvements"></a>協助工具改進
<!-- 1253000 -->
我們也針對 Configuration Manager 主控台的協助工具新增其他改進。 如需詳細資料，請參閱[協助工具功能](../../understand/accessibility-features.md)。

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>針對 SQL Server Always On 可用性群組的改進
<!-- 1352094 -->
在此版本中，您現在可以在與 Configuration Manager 搭配使用的 SQL Server Always On 可用性群組中使用非同步認可複本。 這意謂著您可以將額外的複本新增到可用性群組來作為離站 (遠端) 備份，然後在災害復原案例中使用這些備份。  
- Configuration Manager 支援使用非同步認可複本來復原您的同步複本。 如需有關如何完成此操作的資訊，請參閱＜備份與復原＞主題中的[站台資料庫復原選項](../../servers/manage/recover-sites.md#site-database-recovery-options)。
- 此版本不支援容錯移轉成使用非同步認可複本作為您的站台資料庫。
如需詳細資訊，請參閱[準備使用 Always On 可用性群組](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="update-reset-tool"></a>更新重設工具
<!-- 1324589 -->
從 1706 版開始，Configuration Manager 主要站台和管理中心網站包含 Configuration Manager 更新重設工具 **CMUpdateReset.exe**。 當主控台內更新無法下載或複寫時，請使用此工具搭配所有仍受支援的最新分支版本來修正問題。 如需詳細資訊，請參閱[更新重設工具](../../servers/manage/update-reset-tool.md)。

### <a name="high-dpi-console-support"></a>高 DPI 主控台支援  
<!-- 1353476 -->
在此版本中，應該已修正有關在高 DPI 裝置 (例如 Surface Book) 上檢視 UI 時，Configuration Manager 主控台如何縮放及顯示不同 UI 部分的問題。

### <a name="improved-boundary-groups-for-software-update-points"></a>改進的軟體更新點界限群組
<!-- 1324591 -->
此版本包含對軟體更新點與界限群組搭配運作方式的改進。 以下摘要說明新的後援行為：
- 軟體更新點的後援現在會針對後援至鄰近界限群組使用可設定的時間。
- 不論後援設定為何，用戶端會在 120 分鐘內持續嘗試連線到最後所使用的軟體更新點。 在持續 120 分鐘都無法連線到該伺服器之後，用戶端就會檢查其集區中可用的軟體更新點，以便找出新的更新點。
- 在持續兩小時都無法連線到其原始伺服器之後，用戶端就會切換到較短的新軟體更新點連線週期。 這意謂著如果用戶端無法與新伺服器連線，它會迅速從可用伺服器集區中選取下一部伺服器，然後嘗試與該伺服器連線。

如需詳細資訊，請參閱「最新分支」之＜界限群組＞主題中的[軟體更新點](../../servers/deploy/configure/boundary-groups.md#software-update-points)。

### <a name="azure-ad-integration-with-configuration-manager"></a>Azure AD 與 Configuration Manager 的整合
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
在此版本中，我們已經改進 Configuration Manager 與 Azure Active Directory (Azure AD) 的整合。  這些改進能簡化要搭配 Configuration Manager 使用之 Azure 服務的設定方式，並協助您管理透過 Azure AD 驗證的用戶端和使用者。

改進的整合能達成下列項目：  
- Azure 服務精靈：此精靈提供能取代個別工作流程的通用設定體驗，以設定下列您會搭配 Configuration Manager 使用的 Azure 服務。
  - **雲端管理**：讓用戶端使用 Azure Active Directory (Azure AD) 進行驗證。 您也可以設定 Azure AD 使用者探索。
  - **Log Analytics 連接器** 連線到 Azure Log Analytics，並同步處理集合資料。
  - **更新整備小幫手**：連線至更新整備小幫手，並檢視用戶端升級相容性資料。
  - **商務用 Windows 市集**：連線至商務用 Windows 市集的線上市集，並為您的組織取得可以搭配 Configuration Manager 進行部署的應用程式。


  這是透過使用 [Azure 伺服器 Web 應用程式](/azure/app-service/app-service-authentication-overview)來提供訂用帳戶和設定詳細資料來完成，您不再需要於每次向 Azure 設定新的 Configuration Manager 元件或服務時，都需輸入相同的訂用帳戶和設定行系資料。 如需詳細資訊，請參閱 [Azure 服務精靈](../../servers/deploy/configure/azure-services-wizard.md)。

- 使用 Azure AD 在網際網路上驗證用戶端，來存取您的 Configuration Manager 站台。 Azure AD 能取代設定及使用用戶端驗證憑證的需求。 這需要雲端管理閘道站台系統角色。 如需詳細資訊，請參閱[從網際網路安裝及指派 Configuration Manager 用戶端並使用 Azure AD 進行驗證](../../clients/deploy/deploy-clients-cmg-azure.md)。

- 在位於網際網路上的電腦上安裝及管理 Configuration Manager 用戶端。 這需要使用雲端管理閘道站台系統角色。 如需詳細資訊，請參閱[從網際網路安裝及指派 Configuration Manager 用戶端並使用 Azure AD 進行驗證](../../clients/deploy/deploy-clients-cmg-azure.md)。

- 設定 Azure AD 使用者探索。  您可以使用 Azure 服務精靈來設定這個新的探索方法。 這個新方法會查詢您的 Azure AD，以取得您可以接著搭配傳統探索資料使用的使用者資料。  同時支援完整和差異同步處理。  如需詳細資訊，請參閱 [Azure AD 使用者探索](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)。

### <a name="peer-cache-improvements"></a>對等快取改進
<!-- 1252345 -->
對等快取已不再使用網路存取帳戶來驗證來自對等的下載要求。 當用戶端仍然需要帳戶時，有一個注意事項。 針對開機進入 WinPE，並從對等快取來源存取內容的用戶端，這仍是必須的。 如需詳細資訊，請參閱[對等快取的需求與考量](../hierarchy/client-peer-cache.md#requirements)。


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>相容性設定

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>未受 Configuration Manager 用戶端管理之 Windows 10 裝置的新組態設定
<!-- 1354715 -->
在此版本中，我們已針對向 Intune 註冊，或由 Configuration Manager 於內部部署管理的 Windows 10 裝置，加入新的組態項目設定。 這些設定包括：

- **密碼**
  - 裝置加密
- **裝置**
  - 修改區域設定 (僅限桌面)
  - 修改電源及睡眠設定
  - 修改語言設定
  - 修改系統時間
  - 修改裝置名稱
- **市集**
  - 自動更新來自市集的應用程式
  - 僅使用私人市集
  - 啟動來自市集的應用程式
- **Microsoft Edge**
  - 禁止存取 about:flags
  - 覆寫 SmartScreen 提示
  - 針對檔案覆寫 SmartScreen 提示
  - WebRTC localhost IP 位址
  - 預設搜尋引擎
  - OpenSearch XML URL
  - 首頁 (僅限桌面)

如需所有 Windows 10 設定的詳細資料，請參閱[如何為不是使用 Configuration Manager 用戶端所管理的 Windows 8.1 和 Windows 10 裝置建立組態項目](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。

### <a name="new-device-compliance-policy-rules"></a>新的裝置合規性政策規則

* **必要的密碼類型**。 指定使用者必須建立英數密碼還是數值密碼。 如果是英數密碼，您還需指定密碼必須包含的字元集數目下限。 四個字元集為：小寫字母、大寫字母、符號和數字。

  **支援於：**
  * Windows Phone 8 或更新版本
  * Windows 8.1+
  * iOS 6 或更新版本
  <br></br>
* **封鎖裝置上的 USB 偵錯**。 您不需要進行此設定，因為 Android for Work 裝置上已停用 USB 偵錯。

  **支援於：**
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本
  <br></br>
* **封鎖來自不明來源的應用程式**。 要求裝置必須防止來自不明來源的應用程式安裝。 您不需要進行此設定，因為 Android for Work 裝置一律會限制來自不明來源的安裝。

  **支援於：**
  * Android 4.0+
  * Samsung KNOX Standard 4.0 或更新版本
  <br></br>
* **需要對應用程式進行威脅掃描**。 此設定會指定在裝置上啟用 [驗證應用程式] 功能。

  **支援於：**
  * Android 4.2 到 4.4
  * Samsung KNOX Standard 4.0 或更新版本


## <a name="application-management"></a>應用程式管理

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台執行 PowerShell 指令碼
<!-- 1236459 -->

在 Configuration Manager 中，您可以使用套件和程式將指令碼部署至用戶端裝置。 在此版本中，我們已加入可讓您採取下列動作的新功能：

- 將 PowerShell 指令碼匯入到 Configuration Manager
- 從 Configuration Manager 主控台編輯指令碼 (僅適用於未簽署的指令碼)
- 將指令碼標示為 [已核准] 或 [已拒絕] 以提升安全性
- 在 Windows 用戶端電腦及內部部署受管理 Windows 電腦的集合上執行指令碼。 您不須部署指令碼，它們會以近乎即時的方式在用戶端裝置上執行。
- 在 Configuration Manager 主控台中檢查指令碼所傳回的結果。

如需詳細資訊，請參閱[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)。

### <a name="new-mobile-application-management-policy-settings"></a>新的行動應用程式管理原則設定    
<!--1324760-->
從此版本開始，您可以使用三個新的行動應用程式管理 (MAM) 原則設定：

- **封鎖螢幕擷取 (僅限 Android 裝置)：** 指定在使用此應用程式時，裝置的螢幕擷取功能會遭到封鎖。


## <a name="operating-system-deployment"></a>作業系統部署

### <a name="hardware-inventory-collects-secure-boot-information"></a>硬體清查會收集安全開機資訊
硬體清查現在會收集安全開機是否在用戶端上啟用的相關資訊。 此資訊預設會儲存在 **SMS_Firmware** 類別 (於 1702 版中推出) 中，並於硬體清查中啟用。 如需硬體清查的詳細資訊，請參閱[如何設定硬體清查](../../clients/manage/inventory/configure-hardware-inventory.md)。

### <a name="collapsible-task-sequence-groups"></a>可摺疊的工作順序群組
此版本引入展開和摺疊工作順序群組的功能。 您可以個別或一次展開或摺疊所有群組。

### <a name="reload-boot-images-with-current-windows-pe-version"></a>以目前的 Windows PE 版本重新載入開機映像
當您在選取的開機映像上執行 [更新發佈點]  時，您現在可以選擇在開機映像中重新載入 (來自 Windows ADK 安裝目錄的) 最新版本的 Windows PE。 如需詳細資訊，請參閱[使用開機映像更新發佈點](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)。

## <a name="software-updates"></a>軟體更新

### <a name="improvements-to-express-update-download-time"></a>針對快速更新下載時間的改進
在此版本中，我們已大幅改進快速更新的下載時間。 如需詳細資訊，請參閱[管理適用於 Windows 10 更新的快速安裝檔案](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md)。

### <a name="manage-microsoft-surface-driver-updates"></a>管理 Microsoft Surface 驅動程式更新
<!-- 1098490 -->
您現在可以使用 Configuration Manager 來管理 Microsoft Surface 驅動程式更新。    


#### <a name="prerequisites"></a>先決條件
- 所有軟體更新點都必須執行 Windows Server 2016。    
- 您必須開啟此發行前版本功能才能使用它。 如需詳細資訊，請參閱[使用發行前版本功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

#### <a name="to-manage-surface-driver-updates"></a>管理 Surface 驅動程式更新

1. 啟用 Microsoft Surface 驅動程式的同步處理。 使用[設定分類和產品](../../../sum/get-started/configure-classifications-and-products.md)中的程序，並在 [分類]  索引標籤上選取 [包含 Microsoft Surface 驅動程式與韌體更新]  核取方塊，來啟用 Surface 驅動程式。
2. [同步處理 Microsoft Surface 驅動程式](../../../sum/get-started/synchronize-software-updates.md)。
3. [部署已同步處理的 Microsoft Surface 驅動程式](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>設定 Windows Update for Business 延遲原則
<!-- 1290890 -->
您現在可以為 Windows Update for Business 直接管理的 Windows 10 裝置，設定 Windows 10「功能更新」或「品質更新」的延遲原則。 您可以在 [軟體程式庫]   > [Windows 10 服務]  底下的新 [Windows Update for Business 原則]  節點中管理延遲原則。

如需詳細資料，請參閱[與 Windows 10 中的 Windows Update for Business 整合](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies)。

### <a name="improved-user-notifications-for-office-365-updates"></a>適用於 Office 365 更新的改良式使用者通知
我們已進行一些改進，可在用戶端安裝 Office 365 更新時，運用 Office 的「隨選即用」使用者體驗。 這包括快顯和應用程式內通知，以及倒數計時體驗。 如需詳細資訊，請參閱 [Office 365 更新的重新啟動行為與用戶端通知](../../../sum/deploy-use/manage-office-365-proplus-updates.md#restart-behavior-and-client-notifications-for-office-365-updates)

## <a name="reporting"></a>報告

### <a name="use-windows-analytics-with-configuration-manager"></a>搭配使用 Windows Analytics 與 Configuration Manager
<!-- 1318608 -->
Windows Analytics 是一組解決方案，可讓您獲取環境目前狀態的深入解析。 您環境中的裝置會回報 Windows 遙測資料。 資料可以透過 Azure 入口網站來存取。 在「更新整備小幫手」的案例中，資料可直接從 Configuration Manager 主控台的監視節點中取得。


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>行動裝置管理

### <a name="updates-to-android-for-work-sharing-configuration"></a>針對 Android for Work 共用設定的更新
<!-- 1338403 -->
在此版本中，[工作設定檔]  設定群組中的 [允許工作和個人設定檔之間的資料共用]  設定的值已經更新。 我們也新增了可封鎖在工作與個人設定檔之間進行複製貼上動作的自訂設定。


### <a name="android-and-ios-enrollment-restrictions"></a>Android 和 iOS 的註冊限制
<!-- 1290826 -->
隨著此版本的發行，您現在可以指定使用者無法註冊個人 Android 或 iOS 裝置。 新裝置限制設定可讓您限制 Android 裝置註冊只能在預先宣告的裝置上執行。 對於 iOS 裝置，您可以封鎖除了以 Apple 的裝置註冊計劃、Apple Configurator 或 Intune 裝置註冊管理員帳戶註冊之裝置以外的所有裝置。

## <a name="protect-devices"></a>保護裝置

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>在 Device Guard 原則中包含對特定檔案和資料夾的信任
<!--1324676-->
在此版本中，我們已在 Device Guard 原則管理中新增進一步的功能。

您現在可以視需要在 Device Guard 原則中新增對特定檔案或資料夾的信任。 這可讓您：

- 克服與受管理安裝程式相關的問題
- 信任無法以 Configuration Manager 部署的商務營運應用程式
- 信任作業系統部署映像中所包含的應用程式

如需詳細資料，請參閱[使用 Configuration Manager 的 Device Guard 管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)。
