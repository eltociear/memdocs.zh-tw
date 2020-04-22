---
title: 監視資料庫複寫
titleSuffix: Configuration Manager
description: 了解如何監視 Configuration Manager 階層中的 SQL Server 複寫。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 96cce5d4aaa352177b1c24ff78cf15e90ea6e823
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694406"
---
# <a name="monitor-database-replication"></a>監視資料庫複寫

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager 主控台 [監視]  工作區中的 [資料庫複寫]  節點來監視資料庫複寫的詳細資料。 您可以監視站台間複寫連結的狀態。 它也會顯示所連線站台之複寫群組的初始化和複寫。  

> [!TIP]  
> 雖然 [資料庫複寫]  節點也會顯示在 [系統管理]  工作區中的 [階層設定]  節點底下，您並無法從該位置檢視資料庫複寫連結的複寫狀態。  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> 複寫連結狀態  

站台間的資料庫複寫會涉及多組資訊的複寫，稱為「複寫群組」  。 每個複寫群組都會傳送及接收不同優先順序的資料。 根據預設，您無法修改複寫群組中所包含的資料及複寫的頻率。  

當複寫連結為作用中，且其狀態非失敗或已降級時，所有群組都會快速複寫。 若有一個或多個群組無法在預期的時間內完成複寫，該連結會顯示為「已降級」  。 已降級的連結仍然可以運作，但您應該監視它們以確保它們會返回作用中狀態。 請調查它們以確保不會發生額外的降級或複寫失敗。  

針對每個複寫連結，請指定不成功的已複寫群組可以重試的次數。 在重試此次數之後，站台便會將該連結的狀態設定為已降級或失敗。 即使只有一個群組沒有成功複寫，站台仍然會將該連結的狀態設定為已降級或失敗。 設定此狀態的原因是因為有單一複寫群組無法在指定的嘗試次數內完成複寫。 如需詳細資訊，請參閱[資料庫複寫閾值](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)。  

使用下列資訊來了解可能需要進一步調查的複寫連結狀態：  

### <a name="link-is-active"></a>連結使用中

未偵測到問題，連結通訊正進行中。

當父站台正在升級到新的版本，且您從子站台檢視連結狀態時，連結狀態會顯示為作用中。 完成更新之後，在子站台具有和父站台相同的版本之前，從父站台所檢視的連結狀態將一律為作用中。 從子站台檢視時，它會顯示為正在設定。  

### <a name="link-is-degraded"></a>連結已降級

複寫正常運作，但至少有一個複寫物件或群組發生延遲。 監視處於此狀態的連結。 檢閱連結上兩個站台的資訊，以取得連結可能失敗的徵兆。

當站台接收到的複寫資料無法快速將資料認可到資料庫時，連結可能也會顯示降級的狀態。 進行大量資料複寫時，可能會發生此行為。 例如，將軟體更新部署至大量的電腦上。 連結上的父站台可能會需要一些時間來處理如此數量的複寫資料。 父站台上的處理延隔會導致它將連結狀態設為已降級，直到它可以順利處理待處理的資料為止。

### <a name="link-has-failed"></a>連結已失敗

複寫無法運作。 複寫連結可能可以在不採取進一步動作的情況下復原。 若要調查及協助補救此連結上的複寫，請使用複寫連結分析師 (RLA)。

此狀態也可能表示複寫連結上父站台和子站台之間發生實體網路的問題。


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a> 監視複寫狀態

使用 [監視]  工作區中的 [資料庫複寫]  節點來檢視複寫連結的狀態。 檢視複寫連結上每個站台之資料庫的詳細資料。 您也可以檢視與複寫群組相關的詳細資料。 若要檢視這些詳細資料，請選取複寫連結，然後針對您要檢視的複寫狀態選取適當的索引標籤。

下列小節會提供複寫狀態之不同索引標籤的詳細資料：

### <a name="summary"></a>[摘要]

檢視連結上兩個站台間的站台資料及全域資料之複寫的高階資訊。  

選取 [檢視歷史流量資料的報告]  以檢視顯示該連結上的複寫所使用之網路頻寬詳細資料的報告。  

### <a name="parent-site"></a>父站台

針對複寫連結上的父站台，檢視與資料庫相關的詳細資料，包括：  

- SQL Server 的防火牆連接埠  

- 可用磁碟空間  

- 資料庫檔案位置  

- 憑證  

### <a name="child-site"></a>子站台

針對複寫連結上的子站台，檢視與資料庫相關的詳細資料，包括：  

- SQL Server 的防火牆連接埠  

- 可用磁碟空間  

- 資料庫檔案位置  

- 憑證  

### <a name="initialization-detail"></a>初始化詳細資料

檢視透過連結進行複寫之群組的初始化狀態。 此資訊可協助您識別初始化複寫資料正在進行中或已失敗。  

使用此資訊來識別站台可能處於「互通性模式」  的時機。 互通性模式會在子站台與父站台使用不同版本的 Configuration Manager 時發生。  

### <a name="replication-detail"></a>複寫詳細資料

檢視透過連結進行複寫之每個群組的複寫狀態。 使用此資訊來協助識別在複寫特定資料時發生的問題或延遲。 它可以協助判斷適用於此連結的適當資料庫複寫閾值。 如需詳細資訊，請參閱[資料庫複寫閾值](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)。  

> [!TIP]  
> 站台資料的複寫群組只會從子站台傳送至父站台。 全域資料的複寫群組則會雙向複寫。  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a> 複寫連結分析師

Configuration Manager 包含**複寫連結分析師** (RLA)，可用來分析及修復複寫問題。 在複寫失敗時使用 RLA 來補救連結失敗。 它也很適合用於複寫已停止運作，但站台尚未將它回報為失敗的情況。

使用 RLA 來補救階層中下列電腦之間的複寫問題：  

- 站台伺服器和站台資料庫伺服器之間  

- 某個站台的資料庫伺服器和另一個站台的資料庫伺服器之間 (也稱為站台間複寫)  

> [!Note]  
> 複寫失敗的方向並不重要。

在 Configuration Manager 主控台或命令提示字元中執行 RLA：  

- 在 Configuration Manager 主控台中執行：移至 [監視]  工作區，然後選取 [資料庫複寫]  節點。 選取想要分析的複寫連結，然後選取功能區中的 [複寫連結分析師]  。  

- 若要在命令提示字元中執行，請輸入下列命令：`%ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

當您執行 RLA 時，它會使用一系列診斷規則和檢查來偵測問題。 您可以檢視該工具所識別的問題。 當有可用來解決某個問題的指示時，它便會顯示它們。 如果 RLA 能自動補救某個問題，它會向您顯示該選項。

當 RLA 完成時，它會將結果儲存到下列以 XML 為基礎的報告中，以及執行該工具之使用者桌面上的記錄檔中：  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA 在補救部分問題時會停止下列服務。 當補救完成時，它會重新啟動這些服務：  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

如果 RLA 無法完成補救，請視需要在站台伺服器上重新啟動這些服務。  

RLA 會記錄所有調查和補救動作，以提供其不會在精靈中顯示的額外詳細資料。  

### <a name="rla-prerequisites"></a>RLA 必要元件

您用來執行 RLA 的帳戶必須具備下列權限：

- 涉及複寫連結之每部電腦上的本機系統管理員權限。

- 涉及複寫連結之每個 SQL Server 資料庫上的 sysadmin 權限。  

> [!Note]  
> 帳戶不需要特定 Configuration Manager 以角色為基礎的系統管理安全性角色。 具備 [資料庫複寫]  節點存取權的系統管理使用者可以在 Configuration Manager 主控台中執行該工具。 具備每部電腦之足夠權限的系統管理員可以在命令提示字元執行該工具。  

### <a name="rla-known-issue"></a>RLA 已知問題

RLA 會針對從 System Center 2012 Configuration Manager 升級的主要站台產生 SQL Server Service Broker (SSB) 憑證錯誤。 此問題是因為在 Configuration Manager 最新分支中對憑證名稱所作的變更所導致。 您可以放心地忽略這些錯誤。  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a> 監視資料庫複寫  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>監視高階站台對站台資料庫複寫狀態

1. 在 Configuration Manager 主控台中，按一下 [監視]  工作區。  

2. 選取 [站台階層]  節點以開啟 [階層圖]  檢視。  

3. 將滑鼠指標暫留在兩個站台之間的線條上。 檢視這些站台的全域及站台資料複寫的狀態。  

### <a name="monitor-the-status-of-a-replication-link"></a>監視複寫連結的狀態

1. 在 Configuration Manager 主控台中，按一下 [監視]  工作區。  

2. 選取 [資料庫複寫]  節點，然後選取您要監視的複寫連結。 然後選取適當的索引標籤以檢視該連結之複寫狀態的各種不同詳細資料。  
