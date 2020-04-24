---
title: 站台大小與效能指導方針
titleSuffix: Configuration Manager
description: 站台大小相關的效能測試結果、方法和指導方針。
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 7380621fdc7a7f4d26b4844df3ee9026f0997024
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688646"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Configuration Manager 站台大小和效能指導方針

適用於：  Configuration Manager (最新分支)

Configuration Manager 在延展性和效能方面引領業界。 其他文件涵蓋[支援延展性限制的上限](size-and-scale-numbers.md)和以環境規模上限執行站台的[硬體指導方針](recommended-hardware.md)。 這篇文章針對各種規模的環境提供補充性效能指導方針。 本指導方針可協助您更準確地估計部署 Configuration Manager 所需的硬體。

本文著重於 Configuration Manager 效能瓶頸的最大因素：磁碟輸入/輸出子系統或 IOPS。 文章：

- 顯示詳細資料並著重於 IOPS 的測試結果
- 記錄如何用您自己的環境和硬體重新產生測試
- 針對各種規模的環境建議磁碟 IOPS 需求 

## <a name="performance-test-methodology"></a>效能測試方法

您可以用許多獨特的方式部署 Configuration Manager，但請務必在任何調整大小的討論中了解幾個變數。 其中一個變數是「功能間隔」  ，例如清查週期。 另一個變數是使用者、軟體部署或系統參考或部署的其他「物件」  等等數目。 效能測試會在「載入」  期間套用這些變數。 載入產生物件的速率是在不同規模環境中使用生產環境部署之企業客戶的一般速率。

> [!NOTE] 
> 客戶遙測資料允許使用對大多數客戶而言最常見的案例、組態和設定來測試最新分支組建。 這篇文章中的建議是根據這些平均值。 您的經驗可能會因環境規模和設定而變。 一般情況下，Configuration Manager 需要物件和間隔方面的常識。 即使您可以收集系統上每個檔案，或將週期間隔設為一分鐘，並不表示您應該這麼做。

下列各節強調在針對大型企業測試和模型化處理需求時，使用的一些重要設定和組態。 這些指導方針可協助設定對於建議硬體大小的基本系統效能期望。

### <a name="feature-intervals-settings"></a>功能間隔設定 
大部分測試在系統的重要週期中使用預設間隔。 例如，硬體清查測試每週發生一次，且會有比預設 *.mof* 檔案大的檔案。 某些週期性的功能間隔，尤其是硬體和軟體清查週期，可能對於環境的效能特性有重大影響。 環境中若啟用資料收集的積極預設間隔，便需要加大的硬體，且與活動的增加直接成正比。 例如，假設您有 25,000 個桌面用戶端，且想要比預設間隔快兩倍的速度收集硬體清查。 您應該從調整站台的硬體開始著手，就彷彿您有 50,000 個用戶端。

### <a name="objects"></a>物件 
測試應該使用大型企業通常會與系統搭配使用的物件「上平均值」  。 典型值為數千個集合和應用程式，部署到數十萬名使用者或系統。 應該同時對系統中「所有」  物件以這些限制執行測試。 許多客戶運用數種功能，但通常不會以這些上限使用產品的所有功能。 測試所有產品功能有助於確保最佳的可能全系統效能，且對於某些客戶可能會使用高於平均用量的功能有緩衝。 

### <a name="loads"></a>負載 
測試應該也以大於標準「平均一天」  負載執行，方法是執行模擬，在系統上產生尖峰使用量需求。 其中一個範例是模擬週二修補程式日的推出，以確定系統可以在這些天的尖峰活動期間快速地傳回更新合規性資料。 另一個範例是模擬在廣泛惡意程式碼爆發期間的站台活動，以確保能夠及時通知和回應。 雖然建議大小的部署機器在任何一天可能未充分使用，但有更多極端情況需要一些處理緩衝。

### <a name="configurations"></a>設定
在某個範圍的實體、Hyper-V 和 Azure 硬體上執行測試，且混用支援的作業系統和 SQL Server 版本。 務必驗證支援設定的最差情況。 一般情況下，Hyper-V 和 Azure 在設定類似時，會傳回與同等實體硬體類似的效能結果。 較新伺服器作業系統效能通常會同於或優於較舊的支援伺服器作業系統。 雖然所有支援平台都符合最低需求，但支援產品 (Windows 和 SQL 等) 的最新版本通常會產生更佳效能。 

最大變化來自於使用中的 SQL Server 版本。 如需 SQL Server 版本的詳細資訊，請參閱[應該執行哪個版本的 SQL？](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run)。 

## <a name="key-performance-determinants"></a>關鍵效能決定因素

您可以使用各種不同設定、不同方式，以及不同站台大小來測試並測量 Configuration Manager 效能。 下列設定和物件可能會大幅影響效能。 在您的環境中測試和模型化效能時，請務必考慮它們。

> [!CAUTION]
> 雖然有幾個層面的 Configuration Manager 有正式的最大值或使用者介面限制以避免過多使用量，但超越指導方針可能對於站台效能有顯著的負面影響。 超過建議的層級或忽略大小調整指導方針，通常需要較大的硬體，且也可能使環境無法維護，直到您縮減頻率或各種物件的計數為止。

### <a name="hardware-inventory"></a>硬體清查
若要測試基準效能，請將硬體清查收集設定為每週一次，並使用預設 *.mof* 檔案大小加上大約 20% 的額外屬性。 不要啟用所有屬性，且只收集您真正需要的屬性。 針對「一律」  隨著「每個」  清查週期變化的屬性進行收集時要特別注意，例如可用的虛擬記憶體。 收集這些屬性可能導致每個清查週期從每個用戶端有過多的變換。

### <a name="software-inventory"></a>軟體清查
若要測試基準效能，請將軟體清查收集設定為一週一次，且「僅限產品」  詳細資料。 收集許多檔案可能對清查子系統造成顯著的壓力。 避免指定最後可能會跨許多用戶端收集數千個檔案的篩選條件，例如 *\*.exe* 或 *\*.dll*。

### <a name="collections"></a>集合
基準效能測試可以包含數千個集合，且具有各種不同的範圍、大小、複雜度和更新設定。 站台效能不是完全只受站台上的集合數目影響。 效能也是集合查詢複雜度、完整和增量的更新和變更頻率、集合之間相依性以及集合中用戶端數目等的交叉產物。

可能的話，請讓有昂貴或複雜動態規則查詢的集合減到最少。 對於需要這些規則類型的集合，請設定適當的更新間隔和更新時間，讓系統上的集合重新評估影響降到最低。 例如，在午夜更新，而不是上午 8:00。

啟用集合的累加式更新，可確保快速且及時地更新集合成員資格。 但即使累加式更新有效率，它們仍對系統造成負載。 請為您所預期變更頻率與對成員資格接近即時的更新需要，取得兩者之間的平衡。 例如，假設您預期集合成員有大量變換，但您不需要接近即時的成員資格更新。 依特定時間間隔按照已排定完整更新來更新集合，會比啟用累加式更新更有效率，且對系統產生較少負載。 

當您啟用累加式更新時，請減少對相同集合的任何已排定完整更新。 它們只是一種評估的備份方法，因為累加式更新應該以接近即時方式維持您的集合成員資格更新。 [集合的最佳做法](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental)針對累加式更新建議總集合的數目上限，但如文章所指出，您的體驗可能視許多因素而有所不同。

只具有直接成員資格規則與限制集合 (不執行累加式更新) 的集合，不需要已排定的完整更新。 針對這些類型的集合停用更新排程，以避免對系統造成不必要負載。 如果限制集合使用累加式更新，只具有直接成員資格規則的集合可能最長 24 小時不會反映成員資格更新，或是在已排定的重新整理發生之前不會反映。

雖然並非最佳做法，但某些組織會建立數百甚至數千個集合，作為許多商務程序的一部分。 如果您使用自動化來建立集合，務必要正確地啟用任何所需的累加式更新。 最小化並散佈任何完整更新排程，以避免在單一時段內的集合評估作用點。 建立一般清理程序來刪除未使用的集合，特別是如果您自動建立集合，而在一段時間後不再需要那些集合。

請記住，當您將部署之類的工作設定目標為您集合中所有物件時，Configuration Manager 會為它們建立原則。 成員資格變更，不論是透過已排定的重新整理還是累加式更新，都可能為整個系統產生許多其他工作。 最新分支組建具有「所有系統」和「所有使用者」集合的特殊原則最佳化。 當目標為整個企業時，請使用內建集合而不是這些內建集合的複製品。

若要更深入地調查效能，您可以使用 [Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) 中的集合評估檢視器 (CEViewer)。

### <a name="discovery-methods"></a>探索方法
針對基準效能測試，請每週執行一次以伺服器為基礎的探索方法，並視需要啟用差異探索來保持資料在當週為最新。 測試應探索之物件數量應該與模擬的企業規模成正比。 活動訊號探索的效能基準測試也應該一週執行一次。

探索資料是全域資料。 常見的效能相關問題，是在階層中誤設定以伺服器為基礎的探索方法，導致重複探索來自多個主要站台的相同資源。 請仔細設定探索方法來最佳化與目標服務 (例如 Active Directory 網域控制站) 的通訊，同時避免在多個主要站台上重複相同的探索範圍。

## <a name="general-sizing-guidelines"></a>一般的大小調整指導方針 

根據上述[效能測試方法](#performance-test-methodology)，下表提供特定數目受管理用戶端的一般「最低」  硬體需求指導方針。 這些值應該允許具有指定數目用戶端的客戶，以夠快的速度處理物件來管理所指定站台。 運算能力的價格每年都在持續降低，以下需求有些對於現代化伺服器硬體組態而言很小。 超過下列指導方針的硬體，對於需要額外處理能力，或有特殊產品使用模式的站台而言，會按比例提高站台的效能。 

| 桌面用戶端  | 站台類型/角色  | 核心<sup>1</sup>   | 記憶體 (GB)   | SQL 記憶體配置  | IOPS：收件匣<sup>2</sup>  | IOPS：SQL<sup>2</sup>   | 所需儲存空間 (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | 主要站台或 CAS，並在相同伺服器上具有資料庫站台角色   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25k  | 主要站台或 CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | 遠端 SQL                                                  | 4   | 16  | 70% |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50k  | 主要站台或 CAS，並在相同伺服器上具有資料庫站台角色   | 8   | 32  | 70% | 1200 | 2800 | 600  |
| 50k  | 主要站台或 CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | 遠端 SQL                                                  | 8   | 24  | 70% |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100k | 主要站台或 CAS，並在相同伺服器上具有資料庫站台角色   | 12  | 64  | 70% | 1200 | 5000 | 1100 |
| 100k | 主要站台或 CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | 遠端 SQL                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | 主要站台或 CAS，並在相同伺服器上具有資料庫站台角色   | 16  | 96  | 70% | 1800 | 7400 | 1600 |
| 150k | 主要站台或 CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | 遠端 SQL                                       | 16  | 72   | 90% |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | CAS，並在相同伺服器上具有資料庫站台角色   | 20+ | 128+ | 80% | 1800+ | 9000+   | 5000+ |
| 700k | CAS                                              | 8+  | 16+  |     | 1800+ |         | 500+  |
|      | 遠端 SQL                                       | 16+ | 96+  | 90% |       | 9000+   | 4500+ |
|      |                                                             |     |     |     |      |      |      |
| 5k   | 次要站台                                   | 4   | 8    |     | 500   | -       | 200   |
| 15k  | 次要站台                                   | 8   | 16   |     | 500   | -       | 300   |

**附註**

1. **核心**：Configuration Manager 會執行許多同步處理序，因此針對各種不同的站台規模，需要特定的最少 CPU 核心數。 雖然核心每年都變得更快，請務必確定特定的最少核心數會以平行方式工作。 一般情況下，在 2015 年以後生產之任何伺服器層級 CPU 都符合表格中所指定核心的基本效能需求。 Configuration Manager 會利用超過建議的額外核心，但一般而言，一旦您有建議的最少核心數，便應該優先進行 CPU 資源投資，以加快現有核心的速度，而不是新增更多較慢的核心。 例如，Configuration Manager 使用 16 個快速的核心來進行重要處理工作會比使用 24 個較慢的核心效能更好，假設其他系統資源 (例如磁碟 IOPS) 都足夠的話。
   
   核心和記憶體之間的關聯性也很重要。 一般情況下，每個核心具有少於 3 到 4 GB 的 RAM，可能會降低您 SQL 伺服器上的總處理功能。 SQL 與站台伺服器元件共置時，每個核心會需要更多的 RAM。
   
   > [!NOTE]
   > 所有測試會設定機器電源計劃，以允許最大 CPU 功率耗用量與效能。
   
2. **IOPS：收件匣和 IOPS：SQL** 會參照 Configuration Manager 和 SQL 邏輯磁碟機的 IOPS 需求。 **IOPS：收件匣**資料行會顯示 Configuration Manager 收件匣目錄所在邏輯磁碟機的 IOPS 需求。 **IOPS：SQL** 資料行會顯示各個 SQL 檔案使用的邏輯磁碟機總 IOPS 需求。 這些資料行不同的原因在於，兩個磁碟機應該有不同格式。 如需建議 SQL 磁碟設定和檔案最佳做法的詳細資訊和範例，包括跨多個磁碟分割來分散檔案的詳細資訊，請參閱[站台規模和效能的常見問題集](../../understand/site-size-performance-faq.md)。
   
   這兩個 IOPS 資料行都使用來自業界標準工具 *Diskspd* 的資料。 如需複製這些測量的指示，請參閱[如何測量磁碟效能](#how-to-measure-disk-performance)。 一般情況下，一旦您符合基本 CPU 和記憶體需求，儲存子系統對站台效能具有最大的影響，且這裡的改善功能會提供投資最大回報。
   
3.  **所需儲存空間：** 這些實際值可能不同於其他記錄下來的建議。 我們提供這些數字只作為一般指導方針；個別的需求可能變化相當大。 請在安裝站台之前仔細規劃磁碟空間需求。 假設此儲存體的一些數量在大多數時間會保持為可用磁碟空間。 您可以將這個緩衝區空間用於復原案例，或需要有可用磁碟空間以進行安裝套件展開的升級案例。 您的站台可能要求額外儲存體來進行大量資料收集、較長的資料保留期，以及大量的軟體發佈內容。 您也可以在較低輸送量的個別磁碟區上儲存這些項目。

## <a name="how-to-measure-disk-performance"></a>如何測量磁碟效能 

您可以使用業界標準工具 *Diskspd*，視大小不同的 Configuration Manager 環境需要，提供標準化的 IOPS 建議。 雖然並不詳盡，下列測試步驟和命令列會提供簡單且可重現方式來評估您的伺服器磁碟子系統輸送量。 您可以比較您的結果，與[一般大小調整指導方針](#general-sizing-guidelines)資料表中的最低建議 IOPS。 

請參閱[範例磁碟設定](#example-disk-configurations)，以取得實驗室環境中各式各樣硬體組態的測試結果。 您可以使用資料作為初步起點，從頭設計新環境的儲存子系統。

### <a name="to-test-disk-iops"></a>測試磁碟 IOPS  
1. 下載 *Diskspd* 公用程式，網址如下：[https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62)。
   
1. 確定您有至少 100 GB 的可用磁碟空間。 停用可能會妨礙或造成磁碟額外負載的任何應用程式，例如目錄的使用中防毒掃描、SQL 或 SMSExec。
   
1. 透過提高權限的命令提示字元，執行 *Diskpd*。 
   
   針對您想要測試的磁碟區，依序執行兩回合的工具。 第一項測試會執行一分鐘的 64k 大小、隨機寫入作業。 這項測試可確保控制器快取載入和磁碟空間配置，以防動態擴充磁碟區。 捨棄第一項測試的結果。 第二項測試應該「立即」  接在第一項測試之後，並執行五分鐘相同的負載。
   
   例如，使用下列特定命令列測試 G:\\ 磁碟區。
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. 檢閱第二個測試的輸出，在**每秒的 I/O** 資料行找到 IOPS 總計。 在下列範例中，IOPS 總計是 **3929.18**。

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>範例磁碟設定

下表顯示使用各種測試實驗室設定，執行[如何測量磁碟效能](#how-to-measure-disk-performance)中測試步驟的結果。 使用此資料作為「初步」  起點，從頭設計新環境的儲存子系統。 

### <a name="physical-machines-and-hyper-v"></a>實體機器和 Hyper-V 
硬體持續改善。 預期較新世代的硬體和不同硬體組合 (例如 SSD 和 SAN) 會超過下述效能。 這些結果是在設計伺服器或與硬體廠商討論時，需要考量的基本起點。

下表顯示在各種測試實驗室設定中，不同磁碟子系統的測試結果，包括主軸和以 SSD 為基礎的硬碟機。 所有設定會將磁碟格式化為 64k 叢集，並將它們連接到企業類別磁碟控制器。 除了 RAID 陣列磁碟計數，它們還各自具有至少一個備用磁碟。

| 磁碟類型   | 不包括 + 1 個備用磁碟的磁碟計數 | RAID     | 測量的 IOPS  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15k SAS          | 2                                                  |           1   | 620           |
| 15k SAS          | 4                                                  |           10  | 1206          |
| 15k SAS          | 6                                                  |           10  | 1751          |
| 15k SAS          | 8                                                  |           10  | 2322          |
| 15k SAS          | 10                                                 |           10  | 2882          |
| 15k SAS          | 12                                                 |           10  | 3476          |
| 15k SAS          | 16                                                 |           10  | 4236          |
| 15k SAS          | 20                                                 |           10  | 5148          |
| 15k SAS          | 30                                                 |           10  | 7398          |
| 15k SAS          | 40                                                 |           10  | 9913          |
| SSD SATA         | 2                                                  |           1   | 3300          |
| SSD SATA         | 4                                                  |           10  | 5542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15607         |

這些是此範例使用的裝置。 這項資訊並不建議任何特定硬體型號或製造商。 

| 磁碟類型    | 型號      | RAID 控制器 | 快取記憶體和設定 |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15k RPM SAS HD    | HP EH0300JDYTH  | 智慧型陣列 P822     | 2GB，20% 讀取 / 80% 寫入           |
| SSD SATA          | ATA MK0200GCTYV | 智慧型陣列 P420i    | 1GB，20% 讀取/80% 寫入           |
| SSD SAS           | HP MO0800 JEFPB | 智慧型陣列 P420i    | 1GB，20% 讀取/80% 寫入           |

### <a name="azure-machine-and-disk-performance"></a>Azure 機器和磁碟效能 
Azure 磁碟效能取決於數個因素，例如 Azure VM 的大小，以及它使用的磁碟數目和類型。 Azure 也持續新增與下列圖表不同的新機型和磁碟速度。 如需 Configuration Manager 在 Azure 上執行的詳細資訊，以及了解 Azure 上磁碟 I/O 上的其他資訊，請參閱 [Azure 上的 Configuration Manager 常見問題集](../../understand/configuration-manager-on-azure.md)。

所有磁碟都格式化為 NTFS 64k 叢集大小，且具有多個磁碟的列會透過 Windows 磁碟管理公用程式設定為等量磁碟區。

| Azure VM| Azure 磁碟| 硬碟計數 | 可用空間 | 測量的 IOPS   | 限制因素   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Azure VM 大小   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Azure VM 大小   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Azure VM 大小   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Azure VM 大小   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1994  | Azure VM 大小   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1024 MB                   | 1992  | Azure VM 大小   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1024 MB                   | 1993  | Azure VM 大小   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2048 MB                   | 1992  | Azure VM 大小   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2334  | P20 磁碟        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1024 MB                   | 3984  | Azure VM 大小   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1536 MB                   | 3984  | Azure VM 大小   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1024 MB                   | 3112  | P30 磁碟        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2048 MB                   | 3984  | Azure VM 大小   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3072 MB                   | 3996  | Azure VM 大小   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2335  | P20 磁碟        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1024 MB                   | 4639  | P20 磁碟        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1536 MB                   | 6913  | P20 磁碟        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2048 MB                   | 7966  | Azure VM 大小   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1024 MB                   | 3112  | P30 磁碟        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2048 MB                   | 6182  | P30 磁碟        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3072 MB                   | 7963  | Azure VM 大小   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4096 MB                   | 7968  | Azure VM 大小   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | P30 磁碟        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | P30 磁碟        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | P30 磁碟        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Azure VM 大小   |

## <a name="see-also"></a>請參閱

- [站台大小和效能常見問題集](../../understand/site-size-performance-faq.md)
- [Azure 的 Configuration Manager - 常見問題集](../../understand/configuration-manager-on-azure.md)
- [大小和縮放比例](size-and-scale-numbers.md)
- [建議的硬體](recommended-hardware.md)
