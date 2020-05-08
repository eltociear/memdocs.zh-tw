---
title: 支援的 SQL Server 版本
titleSuffix: Configuration Manager
description: 取得裝載 Configuration Manager 站台資料庫的 SQL Server 版本與設定需求。
ms.date: 04/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3c52008089a6d23d5c4efe44f0970bb186eb334a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904640"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Configuration Manager 的 SQL Server 版本支援

適用於：  Configuration Manager (最新分支)

每個 Configuration Manager 站台都必須有支援的 SQL Server 版本和設定，才能裝載站台資料庫。  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server 執行個體和位置

### <a name="central-administration-site-and-primary-sites"></a>管理中心網站和主要站台

站台資料庫必須使用完整的 SQL Server 安裝。  

SQL Server 可以位於：  

- 站台伺服器電腦。  
- 站台伺服器的遠端電腦。  

以下是支援的執行個體：  

- SQL Server 預設或具名執行個體。  
- 多個執行個體設定。  
- SQL Server 叢集。 請參閱[使用 SQL Server 叢集裝載站台資料庫](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)。
- SQL Server AlwaysOn 可用性群組。 如需詳細資訊，請參閱[適用於高可用性站台資料庫的 SQL Server AlwaysOn](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="secondary-sites"></a>次要站台

站台資料庫可以使用預設的完整 SQL Server 安裝執行個體，或是使用 SQL Server Express。  

SQL Server 必須位於站台伺服器電腦上。  

### <a name="limitations-to-support"></a>支援上的限制

不支援下列設定：

- 網路負載平衡 (NLB) 叢集設定中的 SQL Server 叢集
- 叢集共用磁碟區 (CSV) 上的 SQL Server 叢集
- SQL Server 資料庫鏡像技術以及點對點複寫

僅支援將 SQL Server 異動複寫用於將物件複寫至設定為使用[資料庫複本](../../servers/deploy/configure/database-replicas-for-management-points.md)的管理點。  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> 支援的 SQL Server 版本

在具有多個站台的階層中，不同站台可以使用不同版本的 SQL Server 來裝載站台資料庫。 前提是需符合下列項目：

- Configuration Manager 支援您使用的 SQL Server 版本。
- 您所使用的 SQL Server 版本仍受 Microsoft 支援。
- SQL Server 支援這兩種 SQL Server 版本之間的複寫。 如需詳細資訊，請參閱 [SQL Server 複寫回溯相容性](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility)。

針對 SQL Server 2016 與之前的版本，對每個 SQL 版本與 Service Pack 的支援遵循 [Microsoft 生命週期](https://aka.ms/sqllifecycle)原則。 支援包括累積更新在內的特定 SQL Server Service Pack，除非它們中斷對 Service Pack 基準版本的回溯相容性。 從 SQL Server 2017 開始，將不會發行 Service Pack，因為它遵循[現代化的維護模型](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server) \(英文\)。 SQL Server 小組會建議持續的[主動式累積更新安裝](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) (當它們成為可用時)。

除非另有指定，否則以下是 Configuration Manager 所有現用版本支援的 SQL Server 版本。 如果新增新 SQL Server 版本的支援，就會註明新增該支援的 Configuration Manager 版本。 同樣地，如果支援已被取代，請查看受影響之 Configuration Manager 版本的詳細資料。

> [!IMPORTANT]  
> 當您在管理中心網站針對資料庫使用 SQL Server Standard 時，您會限制一個階層所能支援的用戶端總數。 請參閱 [Size and scale numbers](size-and-scale-numbers.md)(大小與縮放比例)。

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019：Standard、Enterprise

從 Configuration Manager 1910 版開始，您可以使用此版本來搭配任何累積更新，只要 SQL 生命週期支援您的累積更新版本即可。

此版本的 SQL 可用於下列網站:

- 管理中心網站
- 主要站台
- 次要站台

#### <a name="known-issue-with-sql-server-2019"></a>SQL Server 2019 的已知問題

SQL 2019 中<!--6436234--> 新的[純量 UDF 內嵌](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining)功能有已知的問題。 若要解決此問題並停用 UDF 內嵌，請在 SQL 2019 伺服器上執行下列指令碼：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

雖然不一定是必要的，但在執行此指令碼之後，您可能需要重新啟動 SQL 伺服器。 如需詳細資訊，請參閱[停用純量 UDF 內嵌而不變更相容性層級](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level)。

您可以安全地停用站台資料庫伺服器的這個 SQL 功能，因為 Configuration Manager 不會使用該功能。

如果您未在 SQL 2019 中停用純量 UDF 內嵌，站台伺服器將會隨機失敗，以查詢站台資料庫。 例如，您會在 **hman.log** 中看到下列錯誤：

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

您可能會在其他記錄中看到類似的錯誤，例如 **SmsAdminUI.log**。

SQL Server 2019 版會記錄下列錯誤：

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

您也會在其記錄目錄中看到來自 SQL 的損毀傾印 (`.mdump` 檔案)，其預設為 `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`。

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017：Standard、Enterprise

您可以使用此版本來搭配[累積更新版本 2](https://support.microsoft.com/help/4052574)或更高版本，只要 SQL 生命週期支援您的累積更新版本即可。 此版本的 SQL 可用於下列網站:

- 管理中心網站  
- 主要站台  
- 次要站台  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016：Standard、Enterprise  
<!--514985-->
您可以搭配 SQL 生命週期所支援的最低 Service Pack 與累積更新使用此版本。 此版本的 SQL 可用於下列網站:

- 管理中心網站  
- 主要站台  
- 次要站台  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014：Standard、Enterprise

您可以搭配 SQL 生命週期所支援的最低 Service Pack 與累積更新使用此版本。 此版本的 SQL 可用於下列網站:

- 管理中心網站  
- 主要站台  
- 次要站台

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012：Standard、Enterprise

您可以搭配 SQL 生命週期所支援的最低 Service Pack 與累積更新使用此版本。 此版本的 SQL 可用於下列網站:

- 管理中心網站  
- 主要站台  
- 次要站台  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

您可以使用此版本來搭配[累積更新版本 2](https://support.microsoft.com/help/4052574)或更高版本，只要 SQL 生命週期支援您的累積更新版本即可。 此版本的 SQL 可用於下列網站:

- 次要站台
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

您可以搭配 SQL 生命週期所支援的最低 Service Pack 與累積更新使用此版本。 此版本的 SQL 可用於下列網站:

- 次要站台

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

您可以搭配 SQL 生命週期所支援的最低 Service Pack 與累積更新使用此版本。 此版本的 SQL 可用於下列網站:

- 次要站台  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

您可以搭配 SQL 生命週期所支援的最低 Service Pack 與累積更新使用此版本。 此版本的 SQL 可用於下列網站:

- 次要站台  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> 必要的 SQL Server 組態

以下是您針對站台資料庫使用之所有 SQL Server 安裝 (包括 SQL Server Express) 的必要設定。 當 Configuration Manager 安裝 SQL Server Express 作為次要站台安裝的一部分時，就會自動建立這些設定。  

### <a name="sql-server-architecture-version"></a>SQL Server 架構版本

Configuration Manager 需要 64 位元版本的 SQL Server 才能裝載站台資料庫。  

### <a name="database-collation"></a>資料庫定序

在每個站台上，針對站台和站台資料庫使用的 SQL Server 執行個體都必須使用下列定序：**SQL_Latin1_General_CP1_CI_AS**。  

針對中國 GB18030 標準，Configuration Manager 支援此定序的兩個例外狀況。 如需詳細資訊，請參閱[國際支援](../hierarchy/international-support.md)。  

### <a name="database-compatibility-level"></a>資料庫相容性層級

Configuration Manager 要求站台資料庫的相容性層級，必須不小於 Configuration Manager 版本的最低支援 SQL Server 版本。 例如，從 1702 版開始，[資料庫相容性層級](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database)須大於或等於 110。 <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server 功能

只有 **Database Engine Services** 功能為每個站台伺服器所需。  

Configuration Manager 資料庫複寫不需要 **SQL Server 複寫**功能。 不過，當您使用 [管理點的資料庫複本](../../servers/deploy/configure/database-replicas-for-management-points.md)時，需要此 SQL Server 設定。  

### <a name="windows-authentication"></a>Windows 驗證

Configuration Manager 需要 **Windows 驗證**來驗證資料庫連線。  

### <a name="sql-server-instance"></a>SQL Server 執行個體

為每個站台使用專用的 SQL Server 執行個體。 執行個體可以是**具名執行個體**或**預設執行個體**。  

### <a name="sql-server-memory"></a>SQL Server 記憶體

使用 SQL Server Management Studio 來為 SQL Server 保留記憶體。 在 [伺服器記憶體選項]  底下，設定 [最小伺服器記憶體]  設定。 如需有關如何設定此設定的詳細資訊，請參閱 [SQL Server 記憶體伺服器設定選項](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options)。  

- **針對與站台伺服器安裝在同一部電腦上的資料庫伺服器**：請將 SQL Server 記憶體的限制設為可用可定址系統記憶體的 50% 到 80%。  

- **針對站台伺服器遠端的專用資料庫伺服器**：請將 SQL Server 記憶體的限制設為可用可定址系統記憶體的 80% 到 90%。  

- **針對為每個使用中 SQL Server 執行個體的緩衝集區所保留的記憶體**：  

  - 針對管理中心網站：設定最小值 8 GB。  
  - 針對主要站台：設定最小值 8 GB。  
  - 針對次要站台：設定最小值 4 GB。  

### <a name="sql-nested-triggers"></a>SQL 巢狀觸發程序

必須啟用 SQL 巢狀觸發程序。 如需詳細資訊，請參閱[設定巢狀觸發程序伺服器設定選項](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### <a name="sql-server-clr-integration"></a>SQL Server CLR 整合

站台資料庫會要求啟用 SQL Server 通用語言執行平台 (CLR)。 當 Configuration Manager 安裝時，會自動啟用此選項。 如需 CLR 的詳細資訊，請參閱 [SQL Server CLR 整合簡介](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)。  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

站台間複寫以及單一主要站台都需要 SQL Server Service Broker。

### <a name="trustworthy-setting"></a>TRUSTWORTHY 設定

Configuration Manager 會自動啟用 SQL [TRUSTWORTHY 資料庫屬性](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property)。 Configuration Manager 要求此屬性為 **ON**。

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> 選擇性的 SQL Server 組態

下列組態可選擇性用於使用完整 SQL Server 安裝的各個資料庫。  

### <a name="sql-server-service"></a>SQL Server 服務

您可以將 SQL Server 服務設為執行時使用：  

- *低權限網域使用者*帳戶：  

  - 此設定是最佳做法，可能需要您手動註冊該帳戶的服務主體名稱 (SPN)。  

- 執行 SQL Server 的電腦**本機系統**帳戶：  

  - 使用本機系統帳戶簡化組態程序。  
  - 當您使用本機系統帳戶時，Configuration Manager 會自動註冊 SQL Server 服務的 SPN。  
  - 針對 SQL Server 服務使用本機系統帳戶不是 SQL Server 最佳做法。  

當執行 SQL Server 的電腦不使用其本機系統帳戶執行 SQL Server 服務時，請在 Active Directory Domain Services 中，設定執行 SQL Server 服務之帳戶的 SPN。 (若是使用系統帳戶，將會自動為您登錄 SPN)。

如需有關站台資料庫之 SPN 的詳細資訊，請參閱[管理站台資料庫伺服器的 SPN](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN)。  

如需如何變更 SQL Server 服務使用之帳戶的詳細資訊，請參閱 [SCM 服務 - 變更服務啟動帳戶](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account)。  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

需要有 SQL Server Reporting Services 才能安裝可讓您執行報告的 Reporting Services 點。 Configuration Manager 支援與站台資料庫相同的 SQL Server 版本來進行報告。

如需詳細資訊，請參閱 [規劃 Configuration Manager 中的報告](../../servers/manage/prerequisites-for-reporting.md)。

> [!IMPORTANT]  
> 從舊版升級 SQL Server 之後，您可能會看到下列錯誤︰*報表產生器不存在*。  
> 若要解決這個錯誤，您必須重新安裝 Reporting Services 點站台系統角色。  

### <a name="data-warehouse-service-point"></a>資料倉儲服務點

資料倉儲會使用個別的資料庫。 您可以將其裝載在站台資料庫伺服器上，或個別的 SQL Server 上。 如需詳細資訊，請參閱 [Configuration Manager 的資料倉儲服務點](../../servers/manage/data-warehouse.md)。

### <a name="sql-server-ports"></a>SQL Server 連接埠

如為 SQL Server 資料庫引擎和站台間複寫通訊，可以使用預設 SQL Server 連接埠設定或指定自訂連接埠：  

- **站台間通訊**使用 SQL Server Service Broker，其預設使用連接埠 TCP 4022。  
- SQL Server 資料庫引擎與不同 Configuration Manager 站台系統角色之間的**站台內通訊**，預設會使用連接埠 TCP 1433。 下列網站系統角色會直接與 SQL Server 資料庫通訊：  

  - 管理點  
  - SMS 提供者的電腦  
  - Reporting Services 點  
  - 網站伺服器  

當執行 SQL Server 的電腦裝載來自多個站台的資料庫時，每個資料庫都必須使用不同的 SQL Server 執行個體。 此外，每個執行個體都必須設定為使用一組唯一的連接埠。  

> [!WARNING]  
> Configuration Manager 不支援動態連接埠。 由於 SQL Server 具名執行個體預設使用動態連接埠連線至資料庫引擎，因此，當您使用具名執行個體時，必須手動設定要用於網站間通訊的靜態連接埠。  

如果在執行 SQL Server 的電腦上啟用防火牆，請確定將它設定為允許您的部署正在使用之連接埠，以及與 SQL Server 通訊的電腦之間的任何網路位置所使用的連接埠。  

如需如何設定 SQL Server 以使用特定連接埠的詳細資訊，請參閱[將伺服器設定為在特定 TCP 連接埠上接聽](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。  

## <a name="upgrade-options-for-sql-server"></a>SQL Server 的升級選項

如果需要升級您的 SQL Server 版本，請使用下列其中一個方法 (依複雜度由低到高排列)：  

- [就地升級 SQL Server](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) \(建議選項\)  

- 在新的電腦上安裝新的 SQL Server 版本，然後[使用 Configuration Manager 安裝程式的資料庫移動](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)選項，將您的站台伺服器指向新的 SQL Server  

- 使用[備份及復原](../../servers/manage/backup-and-recovery.md)。 支援針對 SQL 升級案例使用備份及復原。 檢閱[復原站台前的考量](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site)時，您可以忽略 SQL 版本需求。
