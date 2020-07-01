---
title: 集合最佳做法
titleSuffix: Configuration Manager
description: 取得在 Configuration Manager 中設定集合及集合評估的建議。
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ee640a70eea9f2e8470e852409911d28e542bc2
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663363"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager 集合的最佳做法

適用於：Configuration Manager (最新分支)

某些集合管理指導方針可能會互相衝突。 例如，基於效能因素，您應該限制頻繁更新的集合數目。 但頻繁更新集合可帶來方便性，因為大部分的 Configuration Manager 功能都取決於集合。 在您設計及設定集合和集合評估時，請仔細考量效能影響和商務需求。

針對 Configuration Manager 集合，請使用下列最佳做法。  

## <a name="configure-maintenance-window-for-updates"></a>設定更新的維護時段

您可以設定用於裝置集合的維護期間，以限制 Configuration Manager 可以在這些裝置上安裝軟體的次數。 如果您將維護時段設定得太小，則用戶端可能無法安裝重要的軟體更新，導致用戶端容易遭受更新可緩解之問題的影響。

規劃維護時段時要謹記的重要考慮事項：

- 預設軟體更新執行階段上限為 60 分鐘。
- 當 Configuration Manager 計算是否可以安裝更新時，它會將執行階段上限多加 5 分鐘，作為重新開機時間。
- 維護時段的剩餘持續時間必須超過軟體更新執行階段上限加五分鐘的時間。

## <a name="avoid-frequent-collection-evaluation"></a>避免頻繁的集合評估

完整集合評估不僅會評估目標集合，也會評估該集合在發生更新時所限制的任何集合。 此外，如果沒有排程的集合會限制集合更新，系統仍然會加以評估。 因此，某些集合的評估次數可能會高於您所預期的頻率。

在繁忙的 Configuration Manager 環境中，您可以透過縮減排程以避免重複的集合評估來改善集合評估效能。 在深度樹狀結構中，您可以減少在樹狀結構中位於較深入位置之集合的評估頻率，因為較高層級的集合評估也會觸發較低層級的集合評估。

## <a name="understand-the-collection-evaluation-graph"></a>了解集合評估圖表

請留意集合評估圖表的運作方式，以設計出適當的集合結構。 不要仰賴使用完整集合評估來更新所有集合，因為其不一定會這麼做。 如果增量更新的集合是依排程進行更新，未啟用增量更新的參考集合便可能不會更新。 因為更新很可能會在增量評估期間發生，完整評估可能不會更新集合，而且會結束該週期的集合評估圖表。 在該情況下，將不會發生任何參考集合評估。 如需詳細資訊，請參閱[集合評估圖表](collection-evaluation.md#collection-evaluation-graph)。

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a> 限制增量更新

對許多集合啟用增量更新可能會導致評估延遲。 最好將增量更新的集合數目限制為 200 個。 確切的數目會取決於：

- 集合總數
- 階層中新增資源和變更資源的頻率
- 階層中的用戶端數目
- 階層中集合成員資格規則的複雜性

如果增量評估週期所花費的時間比所設定的更新頻率還要長，便代表 Configuration Manager 必須持續處理集合評估，這可能會影響系統效能。 請減少增量更新集合的數目，或是增加增量評估週期之間的時間。

基於增量集合的潛在影響，請務必針對建立集合及指派更新排程制定原則或程序。 原則考量的範例如下：

- 僅針對用於安全性範圍、用戶端設定及維護時段的集合使用增量更新。 這些集合更新會影響用戶端行為及資源存取。
- 針對沒有授權核准的應用程式，請對現有集合公告這些應用程式，並使用全域條件來限制可用性。
- 針對具有已排程完整集合更新的其他集合概述適當的期間。

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>避免從 CAS 評估大型樹狀結構

在 Configuration Manager 環境中，管理中心網站 (CAS) 不會評估集合成員資格。 主要站台是唯一會評估集合的站台。 次要站台會作為 Proxy，並僅使用複寫自主要站台的資料。

若要要求集合更新，CAS 會向每個主要站台傳送要求。 主要站台會評估集合，並將結果傳回 CAS。 只有在所有集合評估指示皆已複寫到所有站台，所有站台都評估所有集合，且所有資料都傳回 CAS 並合併之後，集合評估結果才會出現。

下圖示範當 CAS 要求手動集合更新時的流程：

![來自 CAS 的手動集合更新](media/manual-collection-update-from-cas.png)

來自具有多個主要站台之 CAS 的集合更新可能會相當耗時。 如果集合無法及時評估，使用者可能會很想要重複要求。

當集合評估執行緒開始並載入評估圖表之後，評估將會繼續，直到集合評估圖表變成空的為止。 執行緒接著會終止，並可供下一個評估使用。 不過，如果在執行緒評估集合的期間，有另一個集合評估週期排入佇列，執行緒便會立即重新啟動以嘗試評估這個「錯過的」週期。

每個評估方法都會在其自己的執行緒中執行。 Configuration Manager 可能會在執行緒內嘗試多次為相同的集合繪製圖表。 Configuration Manager 接著會卸載第二個和後續的要求。

為了防止這些情況，請避免對大型樹狀結構使用手動集合評估，特別是在處理具有多個站台的 CAS 時。

## <a name="consider-collection-depth-and-cross-referencing"></a>考慮集合深度及交互參照

為了在商務需求和效能之間取得平衡，請務必了解您建立的集合結構，以及其對其他集合的相依性。 如果您建立的集合具有參考一或多個集合的規則，且這些所參考的集合也會參考其他集合，系統會評估所有那些集合以建立集合的成員資格。

Configuration Manager 中的包含和排除集合規則，可讓參考集合的工作比撰寫自訂 WQL 查詢來得輕鬆許多。 不過，如果使用包含和排除集合會導致較高的效能成本，您可以改為使用 WQL 查詢方法：

包含：

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

排除：

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>使用 CEViewer 來監視集合評估

您可以使用[集合評估檢視器 (CEViewer)](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) 來監視正在評估的集合數目，以及每個集合在更新上所花費的時間長度。 CEViewer 位於站台伺服器上的 [CD.Latest] 資料夾中。

若要使用 SQL 手動執行類似的檢查，您可以使用下列查詢：

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


