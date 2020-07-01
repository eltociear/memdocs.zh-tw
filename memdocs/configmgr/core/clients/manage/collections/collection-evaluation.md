---
title: 集合評估
titleSuffix: Configuration Manager
description: 了解集合評估程序、類型及觸發程序。 了解集合評估圖表及階層。
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af90154b848ddcd7cbff21917ef122ab10585098
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663858"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Configuration Manager 中的集合評估

適用於：Configuration Manager (最新分支)

Configuration Manager 會使用「集合評估」來根據您定義的集合規則更新集合成員資格。 集合評估的範圍和時機，會因站台和集合的設定及評估類型而有所不同。 

請務必了解集合評估行為，以做出適當的集合設計決策。 如需集合評估指導方針和建議，請參閱[集合的最佳做法](best-practices-for-collections.md)。

## <a name="evaluation-process"></a>評估程序

[colleval.log](https://docs.microsoft.com/mem/configmgr/core/plan-design/hierarchy/log-files#BKMK_ServerLogs) 會記錄集合評估工具建立、變更及刪除集合的時機。

概括而言，每個個別的集合評估及更新都會遵循這些步驟：

![集合更新程序概觀](media/high-level-collection-update-process.png)

1. 執行集合查詢。
1. 新增任何屬於直接成員的系統。
1. 評估所有「包含」集合。
   
   如果包含集合也有查詢規則，或有包含或排除集合，也會對其進行評估。 如果包含集合本身是限制集合，則評估其下方的任何集合。 在完整評估樹狀結構之後，將結果傳回呼叫集合。
   
1. 在傳回的結果和限制集合之間執行邏輯 `AND`。
1. 評估「排除」集合。
   
   如果排除集合也有查詢規則，或有包含或排除集合，也會對其進行評估。 如果這些集合本身是限制集合，則評估其下方的任何集合。 在完整評估樹狀結構之後，將結果傳回呼叫集合。
   
1. 將來自評估直接成員及包含集合的結果集，與評估排除集合的結果互相比較。
1. 將變更寫入資料庫並執行更新。
1. 觸發任何也要更新的相依集合。 相依集合是目前集合所限制的集合，或是使用包含或排除規則參考目前集合的集合。

## <a name="collection-evaluation-types-and-triggers"></a>集合評估類型和觸發程序

視評估類型而定，這些執行緒類型會處理集合評估：

- [主要] 用於已排程的集合更新
- [輔助] 用來手動更新具有相依集合的集合
- [單一] 用來手動更新沒有相依集合的集合
- [快速] 用於增量集合更新

下表描述集合評估觸發程序及其對應的評估類型。 

| 觸發程序 | 評估類型 | 說明 |
|---------|-----------------|-------------|
|手動|單一或輔助|「手動」是最高優先順序的集合評估。 當系統管理員要求手動集合評估時，集合評估工具會將下一個可用的評估執行緒指派給該評估。|
|已排程|主要|已排程評估的程序和手動評估相同，不過此評估是時間驅動而非事件驅動。|
|預備|單一或輔助|所有集合都會直接或間接相依於 [所有系統] 或 [所有使用者和使用者群組]。 這兩個集合每天都會在上午 4:00 進行完整的集合評估。 對這兩個集合之一進行變更，都會根據[完整集合圖表](#collection-evaluation-graph)觸發相依集合的更新。
|增量|快速|增量評估會使用集合評估圖表，來在對增量集合成員資格的更新變更時評估及更新相依集合。 Configuration Manager 會監視及更新所有集合中已針對增量更新進行設定的資源物件。<br /><br />如果集合查詢是以將在稍後更新的資訊 (例如硬體清查) 為基礎，Configuration Manager 只會在已排程的集合更新期間針對集合新增或移除該資源。|

## <a name="collection-evaluation-graph"></a>集合評估圖表

「集合評估圖表」會對應與評估目標集合相關的所有集合。 集合評估會涉及集合評估圖表中的目標集合及任何相關的集合。

當集合評估開始時，Configuration Manager 會建置包含因目標集合的變更而可能會需要評估之所有集合的圖表，並從週期中的最高層級開始。 集合評估工具接著會根據該圖表依序執行，個別評估每個集合成員資格。 在完整評估集合之後，集合評估工具會將不受此週期影響的較低層級集合從集合評估圖表中移除。

如果正在評估的集合有一或多個具有包含或排除規則，集合評估工具會將包含或排除的集合，連同該集合所限制的任何集合新增到圖表中。 如果包含或排除集合在評估期間有任何變更，圖表會繼續在該分支上執行，然後再返回主要分支。

Configuration Manager 會建置兩種類型的評估圖表，「增量」或「完整」。

### <a name="incremental-collection-evaluation"></a>增量集合評估

當資料表資料變更時，SQL 觸發程序會在 **CollectionNotifications** 資料表中插入資料列。 下次觸發集合評估排程時，其會搭配現有的集合查詢對資源識別碼進行 `AND` 處理，並在已針對「增量」集合啟用的集合上觸發更新。

增量集合評估會針對每部電腦執行單一查詢。 增量集合評估的預設站台設定為每隔五分鐘。

增量集合評估圖表只有在所參考的集合已啟用增量評估的情況下，才會加以對應。 如果增量評估已限制於未啟用增量評估的集合，圖表會根據限制集合的現有成員資格評估該集合。 

例如，下圖顯示適用於所有集合的新探索資源。 不過，集合評估只會更新 [所有伺服器] 和 [所有網域控制站] 集合。 集合評估工具不會評估其他集合，因為 [所有成員伺服器] 集合並未啟用增量評估。

![增量集合評估圖表範例](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>完整集合評估

手動或已排程的集合評估會建置包含所有相依集合的「完整」集合評估圖表。 圖表會包含參考正在更新的集合及後續集合的所有集合。 只要正在處理的集合發生更新，Configuration Manager 就會繼續沿著圖表向下評估。

下圖顯示 [所有伺服器] 集合的已排程或手動集合更新要求，如何產生包含所有適用集合的完整圖表。 由於新 DNS 伺服器和網域控制站資源位於所有集合之成員資格查詢的範圍內，因此所有集合都會更新。

![完整集合評估圖表範例 1](media/full-collection-evaluation-graph-1.png)

完整評估不一定會評估所有集合。 集合評估圖表只會在目前所參考的集合發生更新時，才會繼續評估相依集合。 如果增量更新的集合在已排程的增量評估期間更新，未啟用增量更新的參考集合便可能不會更新。 完整評估不會更新集合，而且會結束該週期的集合評估圖表和任何參考集合評估。 

在下列範例中，在現有伺服器上安裝 DNS 會使其成為 [DNS 伺服器] 集合的成員，但由於其限制的 [所有成員伺服器] 集合沒有任何更新，完整評估並不會評估 [DNS 伺服器] 集合。 下一個增量評估週期將會評估 [DNS 伺服器] 集合，因為其為增量集合。

![完整集合評估圖表範例 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>後續步驟
- [如何建立集合](create-collections.md)
- [集合的最佳作法](best-practices-for-collections.md)
- [集合評估檢視器](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer)
- TechEd Australia 的 [ConfigMgrDogs 對 ConfigMgr 2012 進行疑難排解](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) \(英文\) 研討會
