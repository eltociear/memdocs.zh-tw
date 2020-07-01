---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: 規劃以將 SQL Server AlwaysOn 可用性群組與 Configuration Manager 搭配使用
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 576f909be15a35f4c29e803236c220cdde33c0ac
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383150"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>準備將 SQL Server AlwaysOn 可用性群組與 Configuration Manager 搭配使用

適用於：Configuration Manager (最新分支)

您可以使用本文來準備 Configuration Manager 以使用 SQL Server AlwaysOn 可用性群組。 此功能可為站台資料庫提供高可用性和災害復原解決方案。  

Configuration Manager 支援在下列位置使用可用性群組：

- 在主要站台和管理中心網站。
- 內部部署環境或 Microsoft Azure 中。

當您在 Microsoft Azure 中使用可用性群組時，可以使用「Azure 可用性設定組」來進一步提升站台資料庫的可用性。 如需 Azure 可用性集合的詳細資訊，請參閱 [管理虛擬機器的可用性](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)。

> [!Important]
> 在您繼續操作之前，必須先熟悉 SQL Server 和 SQL Server 可用性群組的設定。 接下來的資訊會參考 SQL Server 文件庫和程序。


## <a name="supported-scenarios"></a>支援的案例

以下是將可用性群組與 Configuration Manager 搭配使用的支援案例。 如需每個案例的詳細資訊和程序，請參閱[針對 Configuration Manager 來設定可用性群組](configure-aoag.md)。

- [建立要與 Configuration Manager 搭配使用的可用性群組](configure-aoag.md#bkmk_create)  
- [設定站台使用可用性群組](configure-aoag.md#bkmk_configure)  
- [在裝載站台資料庫的可用性群組中新增或移除同步的複本成員](configure-aoag.md#bkmk_sync)  
- [從非同步認可複本設定或復原站台](configure-aoag.md#bkmk_async)  
- [將站台資料庫從可用性群組移到獨立 SQL Server 的預設或具名執行個體](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>先決條件

下列先決條件適用於所有案例。 如果有其他先決條件適用於特定案例，該案例將會隨附那些先決條件的詳細說明。

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager 帳戶和權限

#### <a name="installation-account"></a>安裝帳戶

您用來執行 Configuration Manager 安裝程式的帳戶必須是：

- 每部可用性群組成員電腦上的本機 **Administrators** 群組成員。
- 每個裝載站台資料庫之 SQL Server 執行個體上的 **sysadmin**。

#### <a name="site-server-to-replica-member-access"></a>站台伺服器到複本成員的存取

站台伺服器的電腦帳戶必須是具備可用性群組成員身分之每部電腦上的本機 **Administrators** 群組成員。

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>版本

可用性群組中的每個複本都必須執行您 Configuration Manager 版本所支援的 SQL Server 版本。 只要 SQL Server 支援，可用性群組的不同節點便可執行不同版本的 SQL Server。 如需詳細資訊，請參閱 [Configuration Manager 的 SQL Server 版本支援](../../../plan-design/configs/support-for-sql-server-versions.md)。<!--SCCMDocs issue 656-->

#### <a name="edition"></a>版本

請使用 SQL Server *Enterprise* Edition。

#### <a name="account"></a>帳戶

每個 SQL Server 執行個體都可在網域使用者帳戶 (**服務帳戶**) 或非網域帳戶下執行。 群組中的每個複本可以有不同的設定。

- 使用具有最低可能權限的帳戶。 如需詳細資訊，請參閱 [SQL Server 安裝的安全性考量](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)。  

- 如需有關為 SQL Server 設定服務帳戶和權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)。  

- 若要使用非網域帳戶，您必須使用憑證。 如需詳細資訊，請參閱[使用資料庫鏡像端點憑證 (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql)。  

- 如需詳細資訊，請參閱[為 Always On 可用性群組建立資料庫鏡像端點](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell)。  


### <a name="database"></a>資料庫

#### <a name="configure-the-database-on-a-new-replica"></a>設定新複本上的資料庫

請為每個複本的資料庫進行下列設定：  

- 啟用 [CLR 整合]：

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    如需詳細資訊，請參閱 [CLR 整合](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling)。  

- 將 [最大文字複寫大小] 設定為 `2147483647`：  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- 將資料庫擁有者設定為 [SA 帳戶]。 您不需要啟用此帳戶。

- 將 **TRUSTWORTY** 設定設為 **ON**：

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    如需詳細資訊，請參閱 [TRUSTWORTHY 資料庫屬性](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property)。

- 啟用 [Service Broker]：  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > 您無法在已屬於可用性群組的資料庫上啟用 [Service Broker] 選項。 您必須先啟用該選項，才能將其新增至可用性群組。<!-- SCCMDocs#1432 -->

- 設定 Service Broker 優先權：

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

請只在主要複本上進行這些設定。 若要設定次要複本，請先將主要複本容錯移轉成次要複本。 此動作可讓次要複本變成新的主要複本。

#### <a name="database-verification-script"></a>資料庫驗證指令碼

請執行下列 SQL 指令碼來驗證主要複本及次要複本的資料庫設定。 您必須先將次要複本變更為主要複本，才能修正次要複本上的問題。

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>可用性群組設定

#### <a name="replica-members"></a>複本成員

- 可用性群組必須有一個主要複本。  

- 在您 SQL Server 版本所支援的可用性群組中，使用相同數目和類型的複本。

- 您可以使用非同步認可複本來復原您的同步複本。 如需詳細資訊，請參閱[站台資料庫復原選項](../../manage/recover-sites.md#site-database-recovery-options)。  

    > [!Warning]  
    > Configuration Manager 不支援「容錯移轉」成使用非同步認可複本作為您的站台資料庫。 如需詳細資訊，請參閱[容錯移轉及容錯移轉模式 (AlwaysOn 可用性群組)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups)。  

Configuration Manager 不會驗證非同步認可複本的狀態來確認它是最新複本。 使用非同步認可複本作為站台資料庫會讓您站台和資料的完整性有風險。 就設計而言，此複本可能不會同步。 如需詳細資訊，請參閱 [SQL Server AlwaysOn 可用性群組概觀](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)。

每個複本成員必須具有下列設定：

- 使用「預設執行個體」或「具名執行個體」  

- [主要角色的連線] 設定為 [允許所有連線]  

- [可讀取次要] 設定為 [是]  

- 已針對 [手動容錯移轉]進行啟用

    > [!Note]
    > 在 1902 版和更舊版本中，您需要在 SQL Server 上設定所有可用性群組，以進行手動容錯移轉。 即使不裝載站台資料庫，也需要進行此設定。
    >
    > 從 1906 版開始，設定為 [自動容錯移轉] 時，Configuration Manager 支援使用可用性群組同步複本。 在下列情況下，請設定 [手動容錯移轉]：
    >
    > - 您執行 Configuration Manager 安裝程式來指定使用可用性群組中的站台資料庫。  
    > - 您為 Configuration Manager 安裝任何更新。 (不僅僅是適用於站台資料庫的更新)。  

- 所有成員都需要相同的[植入模式](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)。<!-- SCCMDocs-pr#3899 --> Configuration Manager 安裝程式包含必要條件檢查，以便在透過 [安裝] 或 [復原] 建立資料庫時驗證這項設定。

    > [!Note]  
    > 當安裝程式建立資料庫，而且您設定**自動**植入時，可用性群組必須擁有建立資料庫的權限。 這項需求同時適用於新的資料庫或復原。 如需詳細資訊，請參閱[自動植入次要複本](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security)。<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>複本成員位置

請將所有複本裝載在內部部署的可用性群組中，或全部裝載在 Microsoft Azure 上。 不支援含有內部部署成員和 Azure 中成員的群組。

Configuration Manager 安裝程式必須連線至每個複本。 當您在 Azure 中設定可用性群組，而該群組位於內部或外部負載平衡器之後時，請開啟下列預設連接埠：

- RPC 端點對應程式：**TCP 135**

- SQL Server Service Broker：**TCP 4022**  

- 透過 TCP 的 SQL：**TCP 1433**

安裝完成之後，這些連接埠必須保持開啟，以供 Configuration Manager 和複寫連結分析師使用。<!-- MEMDocs#375 -->

您可以使用自訂連接埠來進行這些設定。 請在端點及可用性群組中的所有複本上，使用相同的自訂連接埠。

若要讓 SQL 在站台間複寫資料，請在 Azure 負載平衡器中建立每個連接埠的負載平衡規則。 如需詳細資訊，請參閱[設定內部負載平衡器的高可用性連接埠](https://docs.microsoft.com/azure/load-balancer/load-balancer-configure-ha-ports) \(部分機器翻譯\)。<!-- MEMDocs#252 -->

#### <a name="listener"></a>接聽程式

可用性群組至少必須有一個 *可用性群組接聽程式*。 當您將 Configuration Manager 設定為使用可用性群組中的站台資料庫時，它會使用此接聽程式的虛擬名稱。 雖然一個可用性群組可以包含多個接聽程式，但是 Configuration Manager 只能使用一個接聽程式。 如需詳細資訊，請參閱[建立或設定 SQL Server 可用性群組接聽程式](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)。

#### <a name="file-paths"></a>檔案路徑

當您執行 Configuration Manager 安裝程式來設定讓站台使用可用性群組中的資料庫時，每部次要複本伺服器都必須具有 SQL Server 檔案路徑，且此路徑與目前主要複本上站台資料庫檔案的檔案路徑相同。 如果相同的路徑不存在，安裝程式就無法新增可用性群組的執行個體作為站台資料庫的新位置。  

本機 SQL Server 服務帳戶必須具備此資料夾的 [完全控制] 權限。

只有當您使用 Configuration Manager 安裝程式來指定可用性群組中的資料庫執行個體時，次要複本伺服器才需要此檔案路徑。 在它完成可用性群組中站台資料庫的設定之後，您便可以從次要複本伺服器刪除不使用的路徑。

例如，請考慮下列案例：

- 您建立一個使用三部 SQL Server 的可用性群組。  

- 您的主要複本伺服器是 SQL Server 2014 的全新安裝。 它預設會將資料庫 .MDF 和 .LDF 檔案儲存在 `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` 中。  

- 您已將兩部次要複本伺服器都從舊版升級至 SQL Server 2014。 藉由此升級，這些伺服器會保留原始檔案路徑來儲存資料庫檔案：`C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`。  

- 將站台資料庫移到此可用性群組之前，請在每個次要複本伺服器上建立下列檔案路徑：`C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`。 此路徑是主要複本上所使用路徑的複本，即使次要複本並不會使用此檔案位置。  

- 接著，您需將該伺服器上新建立之檔案位置的完全控制存取權，授與每個次要複本上的 SQL Server 服務帳戶。  

- 現在，您可以成功執行 Configuration Manager 安裝程式，來設定讓站台使用可用性群組中的站台資料庫。  

#### <a name="multi-subnet-failover"></a>多重子網路容錯移轉

<!-- SCCMDocs-pr#3734 -->
從 1906 版開始，您可以在 SQL Server 中啟用 [MultiSubnetFailover 連接字串關鍵字](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover)。 您也需要手動將下列值新增至站台伺服器上的 Windows 登錄：

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> 使用具有多重子網路容錯轉移的[站台伺服器高可用性](site-server-high-availability.md)和 SQL Server Always On，並不會針對災害復原案例提供自動容錯移轉的完整功能。

如果您需要在遠端位置建立具有成員的可用性群組，請根據最低的網路延遲排定優先順序。 網路延遲高可能會導致複寫失敗。<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>限制與已知問題

下列限制適用於所有案例。

### <a name="unsupported-sql-server-options-and-configurations"></a>不支援的 SQL Server 選項和設定

- **基本可用性群組**：在 SQL Server 2016 Standard Edition 中引進，基本可用性群組不支援對次要複本的讀取權限。 設定需要此存取權。 如需詳細資訊，請參閱[基本 SQL Server 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017)。  

- **容錯移轉叢集執行個體**：搭配 Configuration Manager 使用的複本不支援容錯移轉叢集執行個體。 如需詳細資訊，請參閱 [SQL Server Always On 容錯移轉叢集執行個體](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server)。  

- **MultiSubnetFailover**：在 1902 版和更舊版本中，不支援在多重子網路設定中，搭配 Configuration Manager 使用可用性群組。 您也無法使用 [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) 關鍵字連接字串。

    若要支援此設定，請將 Configuration Manager 更新至 1906 版或更新版本。 如需詳細資訊，請參閱[多重子網路容錯移轉](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)先決條件。

### <a name="sql-servers-that-host-additional-availability-groups"></a>裝載額外可用性群組的 SQL Server

<!--SCCMDocs issue 649-->
如果 SQL Server 除了您用於 Configuration Manager 的群組之外，還裝載一或多個可用性群組，則在您執行 Configuration Manager 安裝程式時，它會需要特定的設定。 這些設定也是為 Configuration Manager 安裝更新所需的設定。 每個可用性群組中的每個複本都必須具有下列設定：

- 手動容錯移轉  
- 允許任何唯讀連線  

> [!Note]
> 在 1902 版和更舊版本中，您需要在 SQL Server 上設定所有可用性群組，以進行手動容錯移轉。 即使不裝載站台資料庫，也需要進行此設定。
>
> 從 1906 版開始，設定為 [自動容錯移轉] 時，Configuration Manager 支援使用可用性群組同步複本。 在下列情況下，請設定 [手動容錯移轉]：
>
> - 您執行 Configuration Manager 安裝程式來指定使用可用性群組中的站台資料庫。  
> - 您為 Configuration Manager 安裝任何更新。 (不僅僅是適用於站台資料庫的更新)。  

### <a name="unsupported-database-use"></a>不支援的資料庫使用

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager 僅支援可用性群組中的站台資料庫

SQL Server Always On 可用性群組中的 Configuration Manager 不支援下列資料庫：  

- 報表資料庫  
- WSUS 資料庫  

#### <a name="pre-existing-database"></a>既存的資料庫

您無法使用在複本上建立的新資料庫。 當您設定可用性群組時，請將現有 Configuration Manager 資料庫的複本還原至主要複本。  

#### <a name="distributed-views"></a>分散式檢視

<!-- SCCMDocs-pr#3792 -->
在 1902 版和更舊版本中，如果您將站台資料庫裝載在 SQL Server Always On 可用性群組上，則無法啟用資料庫複寫的[分散式檢視](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep)。 若要支援此設定，請更新至 1906 版或更新版本。


### <a name="setup-errors-in-configmgrsetuplog"></a>ConfigMgrSetup.log 中的安裝程式錯誤

當您執行 Configuration Manager 安裝程式，以便將站台資料庫移至可用性群組時，它會嘗試處理可用性群組次要複本上的資料庫角色。 **ConfigMgrSetup.log** 檔案會顯示下列錯誤：  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

您可以放心地忽略這些錯誤。

### <a name="site-expansion"></a>站台擴充

<!--SCCMDocs issue 568-->
如果您將獨立主要站台的站台資料庫設定為使用 SQL Always On，您就無法擴充該站台來包括管理中心網站。 如果您嘗試進行此程序，它會失敗。 若要擴充站台，請暫時從可用性群組中移除主要站台資料庫。

新增次要站台時，您不需要對設定進行任何變更。


## <a name="changes-for-site-backup"></a>站台備份的變更

### <a name="backup-database-files"></a>備份資料庫檔案
  
當站台資料庫使用可用性群組時，請執行內建的「備份站台伺服器」維護工作，以備份常用的 Configuration Manager 設定和檔案。 請勿使用該備份所建立的 .MDF 或 .LDF 檔案。 應改為使用 SQL Server 來直接備份這些資料庫檔案。

### <a name="transaction-log"></a>交易記錄  

請將站台資料庫的復原模式設定為 [完整]。 就可用性群組中的 Configuration Manager 使用而言，這是必要設定。 規劃以監視及維護站台資料庫交易記錄的大小。 在完整復原模型中，必須等到建立資料庫或交易記錄的完整備份之後，才會強行寫入交易。 如需詳細資訊，請參閱 [SQL Server 資料庫的備份與還原](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)。


## <a name="changes-for-site-recovery"></a>站台復原的變更

如果至少有一個可用性群組節點仍可運作，請使用 [略過資料庫復原 (如果資料庫未受到影響，則使用此選項)] 站台復原選項。

從 1906 版開始，站台復原可以在 SQL Always On 群組上重新建立資料庫。 此程序適用於手動和自動植入。<!-- SCCMDocs-pr#3846 -->

在 1902 版或更舊版本中，當您遺失可用性群組的所有節點時，則必須先重新建立可用性群組，才能復原站台。 Configuration Manager 無法重建或還原可用性節點。 請重新建立群組、還原備份，然後重新設定 SQL。 接著，使用 [略過資料庫復原 (如果資料庫未受到影響，則使用此選項)] 站台復原選項。

如需詳細資訊，請參閱[備份和復原](../../manage/backup-and-recovery.md)。


## <a name="changes-for-reporting"></a>報告的變更

### <a name="install-the-reporting-service-point"></a>安裝 Reporting Service 點

Reporting Services 點不支援使用可用性群組的接聽程式虛擬名稱。 它也不支援將其資料庫裝載在 SQL Server Always On 可用性群組中。  

- 根據預設，Reporting Services 點安裝會將 [站台資料庫伺服器名稱] 設定為指定成接聽程式的虛擬名稱。 請將此設定變更為指定可用性群組中複本的電腦名稱和執行個體。  

- 若要在某個複本節點離線時，卸載報告功能並提升可用性，請考慮在每個複本節點上安裝額外的 Reporting Services 點。 然後將每個 Reporting Services 點設定為使用自己的電腦名稱。 當您在可用性群組的每個複本上安裝 Reporting Services 點時，報告功能將一律可以連線到作用中的報告點伺服器。  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>切換主控台所使用的 Reporting Services 點

1. 在 Configuration Manager 主控台中，移至 [監視] 工作區、展開 [報告]，然後選取 [報告] 節點。

1. 在功能區中，選取 [報告選項]。  

1. 在 [報告選項] 對話方塊中，選取您想要使用的 Reporting Services 點。  


## <a name="next-steps"></a>後續步驟

本文描述當您使用可用性群組時，Configuration Manager 所需常見工作的先決條件、限制及變更。 如需了解安裝及設定讓您站台使用可用性群組的程序，請參閱[設定可用性群組](configure-aoag.md)。
