---
title: 監視階層
titleSuffix: Configuration Manager
description: 了解如何使用主控台中的 [監視] 工作區來在 Configuration Manager 中監視基礎結構。
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66fc6744ef7d1aaf90a5e7339cc9a5174c0d33f6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694396"
---
# <a name="monitor-the-hierarchy"></a>監視階層

適用於：  Configuration Manager (最新分支)

若要在 Configuration Manager 中監視基礎結構，請使用 Configuration Manager 主控台中的 [監視]  工作區。  

> [!NOTE]  
> 例外狀況是在移轉站台期間，在該情況下不會使用此位置。 若要監視此程序，請移至 [系統管理]  工作區的 [移轉]  節點。 如需詳細資訊，請參閱[用於移轉到 Configuration Manager 最新分支的作業](../../migration/operations-for-migration.md)。  

除了使用 Configuration Manager 主控台來監視之外，請使用下列功能：

- [報告簡介](introduction-to-reporting.md)
- [記錄檔](../../plan-design/hierarchy/log-files.md)。  

當您在監視站台時，可尋找指出有問題需要您處理的記號。 例如：  

- 站台伺服器和站台系統上的積存檔案。  

- 指出錯誤或問題的狀態訊息。  

- 無法進行站台內通訊。  

- 伺服器上系統事件記錄中的錯誤和警告訊息。  

- Microsoft SQL Server 錯誤記錄中的錯誤和警告訊息。  

- 長時間未回報狀態的站台或用戶端。  

- SQL Server 資料庫的回應緩慢。  

- 硬體故障的跡象。  

如果監視工作顯示任何問題跡象，請調查問題的來源。 然後迅速修復它以將站台失敗的風險降到最低。  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> 監視常見管理工作

Configuration Manager 從 Configuration Manager 主控台內提供內建的監視。

### <a name="alerts"></a>警示

如需詳細資訊，請參閱[監視警示](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts)。  

### <a name="compliance-settings"></a>相容性設定

如需詳細資訊，請參閱[如何監視相容性設定](../../../compliance/deploy-use/monitor-compliance-settings.md)。

### <a name="content"></a>Content

如需監視內容的一般資訊，請參閱[管理內容與內容基礎結構](../deploy/configure/manage-content-and-content-infrastructure.md)。  

如需監視特定類型內容的詳細資訊：

- [監視應用程式](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [監視套件和程式](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [針對軟體更新監視內容](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [針對 OS 部署監視內容](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

如需詳細資訊，請參閱[如何監視 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)。  

### <a name="os-deployment"></a>OS 部署

如需詳細資訊，請參閱[監視 OS 部署](../../../osd/deploy-use/monitor-operating-system-deployments.md)。

### <a name="monitor-power-management"></a>監視電源管理

如需詳細資訊，請參閱 [How to monitor and plan for power management](../../clients/manage/power/monitor-and-plan-for-power-management.md) (如何監視及規劃 Configuration Manager 的電源管理)。  

### <a name="monitor-software-metering"></a>監視軟體計量

如需詳細資訊，請參閱[使用軟體計量監視應用程式使用量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

### <a name="monitor-software-updates"></a>監視軟體更新

如需詳細資訊，請參閱 [Monitor software updates](../../../sum/deploy-use/monitor-software-updates.md) (監視軟體更新)。  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> 監視站台階層

[監視]  工作區的 [站台階層]  節點提供您 Configuration Manager 階層和站台間連結的概觀。 您可以使用兩種檢視：  

- **階層圖**：以簡化的拓撲圖顯示您的階層，其只會顯示重要資訊。 如需詳細資訊，請參閱[階層圖](#hierarchy-diagram)。  

- **地理檢視**：以地圖顯示您的站台，並顯示您所設定的站台位置。 如需詳細資訊，請參閱[地理檢視](#geographical-view)。  

使用 [站台階層]  節點來監視每個站台的健康情況。 同時監視站台間的複寫連結，以及其與外在因素 (例如地理位置) 的關聯性。  

站台狀態和站台間連結狀態都會複寫為站台資料，而非全域資料。 當您將 Configuration Manager 主控台連線到子主要站台時，您將無法檢視其他主要站台或其子次要站台的站台或連結狀態。 例如，在具有多個主要站台的階層中，當您將主控台連線到某個主要站台時，您可以檢視子次要站台、該主要站台及管理中心網站的狀態。 在此檢視中，您並無法看見管理中心網站底下其他站台的狀態。  

若要控制 [站台階層]  節點中的顯示方式，請使用 [設定設定值]  動作。 階層會複寫您在此節點中設定的設定。  

### <a name="hierarchy-diagram"></a>階層圖

階層圖會以拓撲圖顯示您的站台。 選取某個站台，然後檢視來自該站台的狀態訊息摘要。 鑽研以檢視狀態訊息，然後存取該站台的 [屬性]  。  

若要檢視某個站台或站台間複寫連結的高階狀態，請將滑鼠指標暫留在該物件上。 複寫連結狀態不會全域複寫。 若要檢視階層中所有主要站台之間的複寫連結詳細資料，請將主控台連線到管理中心網站。  

下列選項可修改階層圖：  

#### <a name="groups"></a>中

設定能在階層圖中觸發變更的主要站台和次要站台數目。 此顯示變更會將站台合併成單一物件。 然後您將能看見站台的總數，以及狀態訊息和站台狀態的高階彙總。 群組設定不會影響地理檢視。  

#### <a name="favorite-sites"></a>我的最愛站台

將個別站台指定為最愛站台。 階層圖會以星號圖示識別我的最愛站台。 當您使用群組時，我的最愛站台不會與其他站台合併。 它們一律會個別顯示。  

### <a name="geographical-view"></a>地理檢視

地理檢視會以地圖顯示各站台的位置。 它只會顯示您搭配位置設定的站台。 當您在此檢視中選取站台時，它會顯示針對父站台或子站台的複寫連結。 和階層圖檢視不同的是，您不能在此檢視中顯示站台狀態訊息或複寫連結詳細資料。  

> [!NOTE]  
> 若要使用地理檢視，您的 Configuration Manager 主控台所連線的電腦必須已安裝 Internet Explorer，並且能夠使用 HTTP 通訊協定存取 Bing 地圖服務。  

下列選項可修改地理檢視：  

#### <a name="site-location"></a>站台位置

使用下列其中一個類型來指定每個站台的地理位置：

- 街道地址
- 地標名稱，例如城市名稱
- 緯度和經度座標

例如，若要使用 Redmond, Washington 的緯度和經度，請指定 **N 47 40 26.3572 W 122 7 17.4432** 作為站台的位置。 您不需要指定經度或緯度的度、分或秒的符號。 Configuration Manager 會使用 Bing 地圖服務，在地理檢視上顯示位置。 接著您便可以搭配地理位置來檢視您的階層。 此檢視能針對可能會影響特定站台或站台間複寫的地區問題提供見解。  

當您指定某個位置時，可使用 [位置]  方塊來搜尋階層中的特定站台。 選取站台之後，請在 [位置]  資料行輸入位置的縣 (市) 名稱或街道地址。 Configuration Manager 使用 Bing 地圖服務以解析此位置。  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>後續步驟

[監視資料庫複寫](monitor-replication.md)
