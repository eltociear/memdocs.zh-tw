---
title: 站台大小與效能指常見問題集
titleSuffix: Configuration Manager
description: 關於站台大小和效能的 Configuration Manager 常見問題解答。
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073257"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Configuration Manager 站台大小和效能常見問題集

適用於：  Configuration Manager (最新分支)

本文件描述關於 Configuration Manager 站台大小調整指引和常見效能問題的常見問題集。

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>機器和磁碟設定常見問題集與範例

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>我應該如何格式化我的站台伺服器和 SQL Server 上的磁碟？

在至少兩個不同的磁碟區上分隔 Configuration Manager 收件匣和 SQL 檔案。 此分隔可讓您針對其執行的不同類型 I/O，將叢集配置大小最佳化。 

針對裝載您站台伺服器收件匣的磁碟區，請使用具有 4K 或 8K 配置單位的 NTFS。 ReFS 會寫入 64k，即使是小型檔案。 Configuration Manager 具有許多小型檔案，因此 ReFS 可能會產生不必要的磁碟額外負荷。

針對包含 SQL 資料庫檔案的磁碟，請使用 NTFS 或 ReFS 格式與 64K 配置單位。

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>我應該如何且在何處配置我的 SQL 資料庫檔案？

現代化固態硬碟 (SSD) 的陣列與 Azure 進階儲存體，可在單一磁碟區 (極少數磁碟) 上提供高 IOPS。 一般來說，您通常會將更多磁碟機新增至陣列以取得額外儲存空間，而不是額外的輸送量。 如果您使用實體主軸型的磁碟，您可能需要比在單一磁碟區上所能產生之 IOPS 還更多的 IOPS。 您應該為 *.mdf* 檔案配置 60% 的建議 IOPS 和磁碟空間總量，為 *.ldf* 檔案配置 20%，並為記錄和資料暫存檔案配置 20%。 *.ldf* 和暫存檔案可以放置在單一磁碟區上，佔用您配置 IOPS 的 40% (20% + 20%)。

早於 SQL Server 2016 的 SQL Server 預設只會建立一個暫存資料檔案。 您應該建立更多暫存資料檔案，以避免 SQL 鎖定並等候存取單一檔案。 社群對於暫存資料檔案的最佳數目有不同意見，從四到八個不等。 測試顯示四到八個幾乎沒有差異，因此您可以建立四個「同樣大小」  的暫存資料檔案。 您 tempdb 資料檔案最高應為整個資料庫大小的 20-25%。

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>是否有任何其他建議的磁碟設定？

在可以設定時，將 RAID 控制器記憶體設定為 70% 寫入作業配置、30% 讀取作業配置。 一般情況下，請為站台資料庫使用 RAID 10 陣列設定。 針對 I/O 需求較低的小規模站台或您使用快速 SSD， RAID 1 也是可以接受的。 對於較大的磁碟陣列，請將備援磁碟設定為自動取代失敗的磁碟。

**範例：具備實體磁碟的實體機器** 

針對共置站台伺服器和具有 **100,000** 個用戶端的 SQL Server [大小指導方針](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)，站台伺服器收件匣為 1200 IOPS，SQL Server 檔案為 5000 IOPS。

合適的磁碟設定看起來會如下所示：

| 磁碟機<sup>1</sup> | RAID | 格式 | 磁碟區內容 | 所需的 IOPS 下限| 提供的 IOPS 概略值<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | ConfigMgr 收件匣    |     1700            | 1751             |
| 12x15k         | 10        | 64k ReFS    | SQL .mdf             | 60%*5000 = 3000     | 3476             |
| 8x15k          | 10        | 64k ReFS    | SQL .ldf、暫存檔案 | 40%*5000 = 2000     | 2322             |

1. 不包含建議的備援磁碟。 
2. 此值來自[範例磁碟設定](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>我在 Windows Server 上使用 Hyper-V。 我應該如何為 Configuration Manager VM 設定磁碟以獲得最佳效能？

如果硬體資源 (CPU 核心和傳遞儲存體) 100% 專用於虛擬機器 (VM)，則 Hyper-V 可提供類似於實體伺服器的效能。 使用固定大小的 *.vhd* 或 *.vhdx* 磁碟檔案，會造成至少 1-5% 的 I/O 效能影響。 使用動態擴充的 *.vhd* 或 *.vhdx* 磁碟檔案，會對 Configuration Manager 工作負載造成最高 25% 的 I/O 效能影響。 如果您需要動態擴充磁碟，請將額外的 25% IOPS 效能新增到陣列作為補償。

當您在 VM 內執行您的 Configuration Manager 站台伺服器或 SQL 時，請將 Hyper-V 主機 OS 磁碟機從 VM OS 和資料磁碟機中區隔開來。

如需 VM 最佳化的詳細資訊，請參閱 [Hyper-V 伺服器效能微調](/windows-server/administration/performance-tuning/role/hyper-v-server/)。

**範例：Hyper-V VM 型站台伺服器** 

針對共置站台伺服器和具有 **150,000** 個用戶端的 SQL Server [大小指導方針](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)，站台伺服器收件匣為 1800 IOPS，SQL Server 檔案為 7400 IOPS。

合適的磁碟設定看起來會如下所示：

| 磁碟機<sup>1</sup> | RAID | 格式<sup>2</sup> | 磁碟區內容 | 所需的 IOPS 下限| 提供的 IOPS 概略值<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Hyper-V 主機 OS           | -                    | -                |
| 2x10k          | 1         | -              | (VM) 站台伺服器 OS       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | (VM) ConfigMgr 收件匣    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64k ReFS       | (VM) 主機 SQL (所有檔案) | 7400                 | 14346            |

1. 不包含建議的備援磁碟。 
2. VM 磁碟機 (基礎磁碟區專用) 之大小固定的傳遞 *.vhdx*。 
3. 此值來自[範例磁碟設定](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>針對 Microsoft Azure 中的 Configuration Manager 環境，是否有任何建議？

您可以從閱讀 [Azure 的 Configuration Manager 常見問題集](configuration-manager-on-azure.md)開始。

利用進階儲存體型磁碟的 Azure 基礎結構即服務 (IaaS) VM 可具有高 IOPS。 在這些 VM 上設定額外磁碟空間以符合預期的磁碟空間需求，而不是為了額外的 IOPS。

Azure 儲存體本質上是冗餘的，且不需要多個磁碟來提供可用性。 您可以在磁碟管理員或儲存空間中將磁碟進行等量，以提供額外的空間和效能。

如需如何將進階儲存體效能最大化，以及在 Azure IaaS VM 中執行 SQL server 的詳細資訊與建議，請參閱：

- [將應用程式效能最佳化](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [磁碟指引](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**範例：Azure 型站台伺服器** 

針對共置站台伺服器和具有 **50,000** 個用戶端的 SQL Server [大小指導方針](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)，站台伺服器收件匣為 8 核心、32 GB 及 1200 IOPS，SQL Server 檔案為 2800 IOPS。

合適的 Azure 機器可能是 DS13v2 (8 核心、56 GB)，並具備下列磁碟設定：

| 磁碟機 | 格式 | 包含 | 所需的 IOPS 下限| 提供的 IOPS 概略值<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;標準&gt; | -             | 站台伺服器 OS     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | ConfigMgr 收件匣  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64k ReFS      | SQL (所有檔案<sup>2</sup>) | 2800                 | 3112             |

1. 此值來自[範例磁碟設定](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。
2. [Azure 指引](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)允許將 TempDB 放在 SSD 型的本機 *D:* 磁碟機中，因為其不會超出可用空間，並允許額外的磁碟 I/O 分配。

**範例：Azure 型站台伺服器 (即時效能提升)** 

Azure 磁碟輸送量受限於 VM 的大小。 上述 Azure 範例中的設定，可能會限制未來的擴充或額外效能。 如果您在 Azure VM 的初始部署期間新增其他磁碟，您可以轉換您的 Azure VM，以便在未來以最低的預付投資來提升處理能力。 比起日後因需要而進行更複雜的移轉，隨需求變更來預先規劃提升站台效能會輕鬆得多。

變更上述 Azure 範例中的磁碟，以了解 IOPS 如何變更。

**DS13v2** 

| 磁碟機<sup>1</sup> | 格式 | 包含 | 所需的 IOPS 下限| 提供的 IOPS 概略值<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;標準&gt; | -             | 站台伺服器 OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr 收件匣  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (所有檔案<sup>3</sup>) | 2800                 | 3984             |

1. 磁碟會使用儲存空間進行等量。
2. 此值來自[範例磁碟設定](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 VM 大小會限制效能。
3. [Azure 指引](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)允許將 TempDB 放在 SSD 型的本機 *D:* 磁碟機中，因為其不會超出可用空間，並允許額外的磁碟 I/O 分配。

如果您未來需要更高的效能，您可以將您的 VM 轉換為 DS14v2，這會將 CPU 和記憶體提升為兩倍。 該 VM 大小允許的額外磁碟頻寬，也會立即提升您先前所設定磁碟上的可用磁碟 IOPS。

**DS14v2**

| 磁碟機<sup>1</sup> | RAID | 格式 | 包含 | 所需的 IOPS 下限| 提供的 IOPS 概略值<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;標準&gt; | -             | 站台伺服器 OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | ConfigMgr 收件匣  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (所有檔案<sup>3</sup>) | 2800                 | 6182             |

1. 磁碟會使用儲存空間進行等量。
2. 此值來自[範例磁碟設定](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)。 VM 大小會限制效能。
3. [Azure 指引](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)允許將 TempDB 放在 SSD 型的本機 *D:* 磁碟機中，因為其不會超出可用空間，並允許額外的磁碟 I/O 分配。

## <a name="other-common-sql-server-related-performance-questions"></a>其他常見的 SQL Server 相關效能問題 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>使用與站台伺服器共置的 SQL 執行，或在遠端伺服器上執行，哪個較好？

假設單一伺服器的大小合適，或兩部伺服器之間的網路連線能力充足，兩者都可以充分執行。

遠端 SQL 需要額外伺服器的預付和作業成本，但對於大部分的大型客戶來說這是常見的。 此設定的優點包括：

- 增加站台可用性選項，例如 SQL Always On
- 能夠執行繁重報告，並減少偷聽站台處理的情況
- 在某些情況下可讓災害復原變得更簡單
- 更簡單的安全性管理
- SQL 管理的角色區隔，例如不同的 DBA 小組

共置的 SQL 需要單一伺服器，適用於大多數小型客戶。 此設定的優點包括：

- 機器、授權和維護成本較低
- 站台中的失敗點較少
- 對於規劃停機時間有更完善的掌控

### <a name="how-much-ram-should-i-allocate-for-sql"></a>我應該為 SQL 配置多少 RAM？

根據預設，SQL 會使用您伺服器的所有可用記憶體，可能會導致機器上的 OS 和其他處理序不夠用。 若要避免潛在的效能問題，請務必明確地將記憶體配置給 SQL。 在與 SQL 伺服器共置的站台伺服器上，請確定 OS 具有足夠的 RAM 可供檔案快取並進行其他作業。 請確定剩餘的 RAM 足夠供 SMSExec 和其他 Configuration Manager 處理序使用。 在遠端伺服器上執行 SQL 時，您可以將「大部分」  的記憶體配置給 SQL，但非所有記憶體。 請檢閱[大小指導方針](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines)以獲得初步指引。 

SQL Server 記憶體配置應無條件進位至整數 GB。 此外，當 RAM 增加至高量時，您可以讓 SQL 具有較高比例。 例如，如果有 256 GB 或更多的 RAM 可用，您可以將 SQL 設為最高 95%，這樣仍會保留足夠的記憶體給 OS。 監視分頁檔是不錯的方法，可確保有足夠記憶體給作業系統和 Configuration Manager 中的任何處理序。

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>核心近來十分便宜。 我是否應該將大量核心新增至我的 SQL Server？

如果您有超過 16 個實體核心且 SQL Server 沒有足夠的 RAM，您可能會遇到記憶體爭用問題。 當每個核心至少有 3-4 GB 的 RAM 可供 SQL 使用時，Configuration Manager 工作負載的效能會更好。 為您的 SQL Server 新增核心時，請務必按比例增加 RAM。

### <a name="will-sql-always-on-impact-my-performance"></a>SQL Always On 是否會影響我的效能？

一般情況下，當 SQL 複本伺服器之間有充足的網路功能時，SQL Always On 對系統效能的影響微不足道。 您可以在繁忙的 SQL Always On 環境中，讓資料庫記錄檔 *.ldf* 檔案快速增加。 不過，成功備份資料庫之後，就會自動釋放記錄檔空間。 新增 SQL 作業讓 Configuration Manager 資料庫執行備份，例如每 24 小時備份一次，以及每六小時執行一次 *.ldf* 備份。 如需 SQL Always On 和 Configuration Manager (包括其他 SQL 備份策略) 的詳細資訊，請參閱[高度可用站台資料庫的 SQL Server Always On](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="should-i-enable-sql-compression-on-my-database"></a>我是否應該在我的資料庫上啟用 SQL 壓縮？

不建議您對 Configuration Manager 資料庫使用 SQL 壓縮。 雖然在 Configuration Manager 資料庫上啟用壓縮不會造成功能性問題，但與可能會對系統產生的相當大效能影響相比，測試結果在節省大小方面並未顯示出有顯著的效果。

### <a name="should-i-enable-sql-encryption-on-my-database"></a>我是否應該在我的資料庫上啟用 SQL 加密？

Configuration Manager 資料庫中的任何祕密都已安全儲存，但新增 SQL 加密可以增加另一層安全性。 在您的資料庫上啟用加密不會造成任何功能性問題，但根據您選擇加密的資料表，以及您使用的 SQL 版本，效能最多可能會降低 25%。 因此請謹慎使用加密，特別是在大規模環境中。 也請務必更新您的備份和復原計劃，以確保您可以成功復原加密的資料。

### <a name="what-version-of-sql-should-i-run"></a>我應該執行哪個版本的 SQL？

針對支援的 SQL 版本，請參閱 [SQL Server 版本支援](../plan-design/configs/support-for-sql-server-versions.md)。 從效能觀點來看，所有支援的 SQL 版本都符合所需的效能準則。 不過，SQL 2012 和 SQL 2016 或更新版本在 Configuration Manager 工作負載某些方面的表現，通常會優於 SQL 2014。 此外，在 SQL 2012 相容性層級 (110) 執行 SQL 2014 可改善整體效能。 在安裝期間，在 SQL 2012 和 SQL 2014 上執行的 Configuration Manager 資料庫會設定為相容性層級 110。 SQL 2016 或更新版本會設為該 SQL 版本的預設相容性層級，例如為 SQL 2016 設為 130。 在安裝下一個主要 Configuration Manager 最新分支版本之前，就地升級 SQL 不會更新相容性層級。 

如果您在 SQL 2016 或更新版本上看到特定 SQL 查詢的不尋常等候逾時或速度緩慢 (例如在管理主控台中使用 RBAC 時)，請嘗試將 Configuration Manager 資料庫的 SQL 相容性層級變更為 110。 在 SQL 2014 與更新版本的 SQL 上執行 SQL 相容性層級 110 受到完整支援。 如需詳細資訊，請參閱 [SQL 查詢逾時或主控台在特定 Configuration Manager 資料庫查詢的速度緩慢](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d)。

由於各種已知的效能相關問題或其他潛在問題，自 2018 年 1 月起您應該「避免」  使用下列 SQL 版本：

- SQL 2012 SP3 CU1 至 CU5
- SQL 2014 SP1 CU6 至 SP2 CU2
- SQL 2016 RTM 至 CU3、SP1 CU3 至 CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>我是否應該實作任何其他的 SQL 編製索引工作？

是，請每週更新一次索引，每天更新一次統計資料，以提升 SQL 效能。 Configuration Manager 和 SQL 社群提供的第三方指令碼和其他資訊，可協助將這些工作最佳化。

在大型站台中，視您的使用模式而定，某些 SQL 資料表 (例如 CI\_CurrentComplianceStatusDetails、HinvChangeLog) 可能會非常大。 您可能需要減少或改變依次維護的方法。

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>我何時應該在次要站台上使用完整的 SQL Server，而不是 SQL Express？

SQL Express 不會對次要站台造成任何顯著的效能影響，足以供大部分的客戶使用。 其也易於部署和管理，且幾乎是所有客戶 (不論大小) 的建議設定。

只有一種情況可能會需要完整的 SQL Server 安裝。 如果您的環境中有大量發佈點、套件或來源，則可能會超過 SQL Express 的 10 GB 大小限制。 如果套件數目乘以發佈點數目超過 4,000,000 (例如 2,000 個 DP 與 2,000 件內容)，請考慮在次要站台上使用完整的 SQL Server。 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>我是否應該在我的資料庫變更 MaxDOP 設定？

將您的設定保留為 0 (使用所有可用的處理器)，在大部分情況下對於整體處理效能是最理想的。

許多 Configuration Manager 系統管理員遵循下列文章提供的指導方針：[Recommendations and guidelines for the "max degree of parallelism" configuration option in SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi) (SQL Server 中「平行處理原則的最大程度」設定選項的建議和指導方針)。 在大多數現代化的大型硬體上，此指引建議最高設為 8。 但是，如果您執行許多小型查詢，數量高於處理器數目，則將其設定為較高的數目可能會有幫助。 在較大的站台上具有較多可用核心時，限制於 8 並不一定是最佳設定。 

在具備超過 8 個核心的 SQL Server 上，先從設為 0 開始，且僅在您遇到效能問題或過多鎖定時才進行變更。 設為 0 時，如果因為遇到效能問題而需要變更 MaxDOP，則改為設定新值，該值須至少大於或等於該站台 SQL 伺服器大小的最低建議核心數目。 低於此值則幾乎一律會產生負面的效能影響。 例如，100,000 個用戶端站台的遠端 SQL Server，必須至少具有 12 個核心。 如果您的 SQL server 有 16 個核心，請以值 12 開始測試您的 MaxDOP 設定。

## <a name="other-common-performance-related-questions"></a>其他常見的效能相關問題

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>我應該為防毒軟體排除站台伺服器 (或其他角色) 上的哪些資料夾？

在任何系統上停用防毒保護時請特別留意。 在高容量且安全的環境中，建議您停用「主動監視」  以獲得最佳效能。

如需建議的防毒軟體排除詳細資訊，請參閱 [Configuration Manager 2012 和最新分支站台伺服器、站台系統和用戶端的建議防毒軟體排除](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu)。

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>將 WSUS 與 Configuration Manager 搭配使用時，我可以如何讓其表現更好？

變更幾項關鍵 IIS 設定 (例如 WsusPool 佇列長度和 WsusPool 專用記憶體限制) 可以改善 WSUS 效能，即使在較小型的安裝上也是。 如需詳細資訊，請參閱[建議的硬體](../plan-design/configs/recommended-hardware.md)。

也請確定您已為執行 WSUS 的作業系統安裝最新更新：

- Windows Server 2012：任何發行於 2017 年 10 月或之後的非「僅限安全性」累積更新。 ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2：任何發行於 2017 年 8 月或之後的非「僅限安全性」累積更新。 ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016：任何發行於 2017 年 8 月或之後的非「僅限安全性」累積更新。 ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>我應該在我的 WSUS 伺服器上執行哪種維護？

請參閱 [Microsoft WSUS 與 Configuration Manager SUP 維護完整指南](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)。

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>我想要為我的站台設定基本效能監視。 我應該注意什麼？

傳統的伺服器效能監視可有效運作於一般 Configuration Manager。 您也可以利用適用於 Configuration Manager、SQL Server 和 Windows Server 之各種 System Center Operations Manager 管理組件來監視伺服器的基本健全狀況。 您也可以直接使用 Configuration Manager 提供的 Windows 效能監視器 (PerfMon) 計數器。 監視各個收件匣中的待辦項目，以取得潛在站台效能問題或待辦項目的早期警告徵兆。

## <a name="see-also"></a>請參閱

- [站台大小與效能指導方針](../plan-design/configs/site-size-performance-guidelines.md)
- [Azure 的 Configuration Manager 常見問題集](configuration-manager-on-azure.md)
