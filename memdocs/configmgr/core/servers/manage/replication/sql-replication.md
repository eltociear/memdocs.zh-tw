---
title: SQL 複寫
titleSuffix: Configuration Manager
description: 使用此圖表來開始對 Configuration Manager 站台之間的 SQL 複寫進行疑難排解
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699856"
---
# <a name="sql-replication"></a>SQL 複寫

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

使用下列圖表來在連結失敗時開始對 SQL 複寫進行疑難排解：

![用來對 SQL 複寫進行疑難排解的圖表](media/sql-replication.svg)

## <a name="queries"></a>查詢

此圖表使用下列查詢：

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>檢查複寫群組連結是否處於已降級或失敗狀態

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>檢查複寫群組連結最近是否已計算

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>檢查 SQL 維護模式

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>後續步驟

- [SQL 複寫重新初始化 (reinit)](sql-replication-reinit.md)
- [SQL 效能](sql-performance.md)
- [SQL 設定](sql-configuration.md)
