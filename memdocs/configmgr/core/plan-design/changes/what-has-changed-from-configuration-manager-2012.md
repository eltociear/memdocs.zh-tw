---
title: 2012 版的變更
titleSuffix: Configuration Manager
description: 識別 Configuration Manager 與 System Center 2012 Configuration Manager 中的變更與新功能。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704436"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>System Center 2012 Configuration Manager 的變更內容

適用於：  Configuration Manager (最新分支)

Configuration Manager 的最新分支推出 System Center 2012 Configuration Manager 的重要變更。 本文識別 Configuration Manager 最新分支原始基準版本 1511 內的重大變更和新功能。 若要了解 Configuration Manager 最新更新中推出的變更，請參閱 [Configuration Manager 累加版本的新功能](whats-new-incremental-versions.md)。

> [!NOTE]
> 從 1910 版開始，Configuration Manager 現在是 Microsoft 端點管理員的一部分。 如需詳細資訊，請參閱 [Microsoft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem)。

2015 年 12 月發行的 Configuration Manager (版本 1511) 是 Microsoft 目前 Configuration Manager 產品的初始版本。 其通常稱為 Configuration Manager 最新分支。 「最新分支」  指出此版本支援產品的累加式更新。 它也提供一個方法來區別此版本與舊版 Configuration Manager。  

Configuration Manager 最新分支：  

- 不同於 Configuration Manager 2007 或 System Center 2012 Configuration Manager 等舊版，產品名稱中不使用年份或產品識別碼。  

- 支援累加式產品中更新 (也稱為更新版本)。 初始版本為版本 1511。 較新版本透過主控台內更新的方式於一年中發行數次，例如 1910 版。  

- 使用基準版本進行安裝。 雖然 1511 是原始的基準版本，但也會不定時發行新的基準版本，例如 2002。 基準版本可用來安裝新的 Configuration Manager 站台和階層，或從支援的 System Center 2012 Configuration Manager 版本進行升級。  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a> 主控台內更新

Configuration Manager 使用稱為**更新和服務**的主控台內服務方式，可輕鬆尋找並安裝建議的更新。  

某些版本只以 Configuration Manager 主控台內現有站台的更新形式提供。 您無法使用這些更新來安裝新的 Configuration Manager 站台。 例如，1910 更新只能從 Configuration Manager 主控台內取得。 這會用來更新已執行支援 Configuration Manager 版本的站台。

另外，也會定期發行更新版本作為新的「基準」  版本。 例如，更新版本 2002 同時也是基準。 您可以使用基準版本來安裝新的站台或階層。 不要從較舊的基準版本 (例如 1802) 開始，並升級至最新版本。 請一律使用最新的基準。

如需詳細資訊，請參閱下列文章：

- [Configuration Manager 的更新](../../servers/manage/updates.md)
- [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a> 服務連接點  

Configuration Manager 最新分支包含新的站台系統角色：**服務連接點**：  

- 許多已啟用雲端之功能的連絡點

- 下載站台的更新

- 將站台的相關診斷及使用方式資料上傳到 Microsoft 雲端

此站台系統角色支援線上和離線操作模式。 如需詳細資訊，請參閱 [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) (關於服務連接點)。  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a> 診斷及使用方式資料

Configuration Manager 會收集站台和基礎結構的相關診斷及使用方式資料。 這項資訊是透過服務連接點編譯並提交給 Microsoft 雲端服務。 Configuration Manager 需要這項資料，才能下載適用於您環境的更新。 當設定服務連接點時，可以指定所收集的資料層級，以及自動 (線上) 或手動 (離線) 提交資料。

如需詳細資訊，請參閱[診斷和使用方式資料](../diagnostics/diagnostics-and-usage-data.md)。  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a> 已過時功能  

某些功能 (例如 [Intel 主動管理技術 (AMT) 型電腦的原生支援](#bkmk_AMT)) 已從 Configuration Manager 主控台移除。 其他功能 (例如網路存取保護) 則已完整移除。 此外，不再支援一些較舊的 Microsoft 產品 (如 Windows Vista、Windows Server 2008 和 SQL Server 2008)。  

如需已取代功能的清單，請參閱[已移除和已取代項目](deprecated/removed-and-deprecated.md)。  

如需所支援產品、作業系統和設定的詳細資料，請參閱[支援的設定](../configs/supported-configurations.md)。  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Intel 主動管理技術 (AMT) 支援  

Configuration Manager 最新分支已從 Configuration Manager 主控台內移除 AMT 型電腦的原生支援。 當使用 [Microsoft Configuration Manager 的 Intel SCS 附加元件](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)時，仍會完全管理 AMT 電腦。 附加元件可讓您存取管理 AMT 的最新功能，同時移除 Configuration Manager 併入那些變更之前所引入的限制。  

移除的 Configuration Manager 整合 AMT 包括頻外管理。 頻外管理點站台系統角色已不再使用。  

> [!Note]
> 這項變更不會影響 System Center 2012 Configuration Manager 中的頻外管理。

## <a name="changes-in-functionality"></a>功能變更

下列各節摘要說明 System Center 2012 R2 Configuration Manager 與 Configuration Manager 最新分支版本 (版本 1511) 之間功能區域的一些重大變更。 如需較新功能變更的詳細資訊，請參閱[累加版本的新功能](whats-new-incremental-versions.md)。

### <a name="client-deployment"></a>用戶端部署  

Configuration Manager 引入新的功能，可用於先測試 Configuration Manager 用戶端的新版本，再使用新的軟體升級站台的其餘部分。 您可以設定用來試驗新用戶端的進入生產階段前集合。 在您滿意進入生產階段前的新用戶端軟體之後，即可升級用戶端，以使用新的版本來自動升級站台的其餘部分。  

如需如何測試用戶端的詳細資訊，請參閱[如何測試進入生產階段前集合用戶端升級](../../clients/manage/upgrade/test-client-upgrades.md)。  

### <a name="os-deployment"></a>OS 部署  

請注意 OS 部署的下列變更：

- 在 [建立工作順序] 精靈中，提供新的工作順序類型：**從升級套件升級作業系統**。 這會建立將電腦從 Windows 7 或 Windows 8.1 升級至 Windows 10 的步驟。 如需詳細資訊，請參閱[將 Windows 升級至最新版本](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

- 部署作業系統時，現在可以使用 Windows PE 對等快取。 執行工作順序來部署 OS 的電腦可使用 Windows PE 對等快取，從對等快取來源取得內容，而不是從發佈點下載內容。 此行為有助於在分公司沒有本機發佈點的案例中，將 WAN 流量降到最低。 如需詳細資訊，請參閱[準備 Windows PE 對等快取以減少 WAN 流量](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)。  

- 您現在可以檢視 Windows 的狀態 (如同環境中的服務一般)。 您也可以建立服務方案，以確立部署更新步調，並確保在新組建發行時，Windows 10 最新分支電腦保持為最新狀態。 此外，您可以在 Windows 10 用戶端的組建支援即將結束時檢視警示。 如需詳細資訊，請參閱[管理 Windows 即服務](../../../osd/deploy-use/manage-windows-as-a-service.md)。  

### <a name="application-management"></a>應用程式管理  

請注意下列應用程式管理變更：

- Configuration Manager 可讓您部署執行 Windows 10 和更新版本之裝置的通用 Windows 平台 (UWP) 應用程式。 如需詳細資訊，請參閱[建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md)。  

- 軟體中心有全新的時尚外貌。 使用者可用的應用程式先前只出現在應用程式類別目錄，而現在會出現於軟體中心的 [應用程式] 索引標籤下。此行為讓使用者更容易找到這些部署，而不需要參考個別應用程式類別目錄。 此外，也不再需要已啟用 Silverlight 的瀏覽器。 如需詳細資訊，請參閱[規劃和設定應用程式管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

- 透過 MDM 應用程式的新 Windows Installer 類型可讓您建立以 Windows Installer 為基礎的應用程式，並部署到執行 Windows 10 的已註冊電腦上。 如需詳細資訊，請參閱[建立 Windows 應用程式](../../../apps/get-started/creating-windows-applications.md)。  

- 在 Configuration Manager 2012 中，若要指定 Windows 市集中應用程式的連結，您可以直接指定連結，或瀏覽至已安裝應用程式的遠端電腦。 在 Configuration Manager 最新分支中，您仍然可以直接輸入連結，但現在，您可以直接從 Configuration Manager 主控台瀏覽市集中的應用程式，而不是瀏覽至參照電腦。  

### <a name="software-updates"></a>軟體更新  

請注意下列軟體更新變更：

- Configuration Manager 現在可以偵測出電腦軟體更新管理方法之間的差異。 具體來說，它可以區別連線至商務用 Windows Update (WUfB) 的 Windows 10 電腦，和連線至 WSUS 的電腦。 **UseWUServer** 是新屬性，並指定是否使用 WUfB 管理電腦。 您可以在集合中使用此設定，以移除這些電腦不進行軟體更新管理。 如需詳細資訊，請參閱 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)。  

- 您現在可從 Configuration Manager 主控台排程及執行 WSUS 清理工作。 在 [軟體更新點元件]  內容中，當您選取執行 WSUS 清理工作時，它會在下一次軟體更新同步處理時執行。 到期的軟體更新在 WSUS 伺服器上會設為拒絕狀態，而電腦上的 Windows Update 代理程式不會再掃描這些軟體更新。 如需詳細資訊，請參閱 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)。  

### <a name="compliance-settings"></a>相容性設定  

請注意下列合規性設定變更：

- Configuration Manager 改進了建立設定項目的工作流程。 現在，當您建立設定項目並選取支援的平台時，只能使用與該平台相關的設定。 請參閱[開始使用合規性設定](../../../compliance/get-started/get-started-with-compliance-settings.md)。  

- [建立設定項目精靈]  現在可讓您更輕鬆地選擇您想要建立的設定項目類型。 此外，新增和更新的設定項目適用於：  

    - 使用 Configuration Manager 用戶端管理的 Windows 10 裝置  

    - 使用 Configuration Manager 用戶端管理的 Mac OS X 裝置  

    - 使用 Configuration Manager 用戶端管理的 Windows 桌上型電腦和伺服器電腦  

    - 不使用 Configuration Manager 用戶端管理的 Windows 8.1 和 Windows 10 裝置  

    如需詳細資訊，請參閱[如何建立設定項目](../../../compliance/deploy-use/create-configuration-items.md)。  

- 支援管理未使用 Configuration Manager 用戶端所管理的 Mac OS X 電腦設定。

### <a name="on-premises-mobile-device-management"></a>內部部署行動裝置管理  

您現在可以使用內部部署 Configuration Manager 基礎結構管理行動裝置。 所有裝置和管理資料都是在內部部署進行處理，且不屬於 Microsoft Intune 或其他雲端服務。 這種類型的裝置管理不需要用戶端軟體。 Configuration Manager 會使用裝置 OS 的內建功能來管理裝置。  

如需詳細資訊，請參閱[使用內部部署基礎結構來管理行動裝置](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。

## <a name="next-steps"></a>後續步驟

[累加版本的新功能](whats-new-incremental-versions.md)
