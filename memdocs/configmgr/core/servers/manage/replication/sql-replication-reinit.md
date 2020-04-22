---
title: SQL 複寫重新初始化
titleSuffix: Configuration Manager
description: 使用此圖表來開始對 Configuration Manager 站台之間的 SQL 複寫重新初始化進行疑難排解
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0e48f2c04e218a7f0eba1b7f06dec768edc8af4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699876"
---
# <a name="sql-replication-reinit"></a>SQL 複寫重新初始化

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

使用下列圖表來開始對 SQL 複寫重新初始化 (reinit) 進行疑難排解：

![用來對 SQL 複寫重新初始化進行疑難排解的圖表](media/sql-replication-reinit.svg)

## <a name="queries"></a>查詢

此圖表使用下列查詢：

### <a name="check-if-site-is-in-maintenance-mode"></a>檢查站台是否處於維護模式

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>檢查哪個複寫群組尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>檢查全域資料

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>檢查站台資料

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>後續步驟

- [全域資料重新初始化](global-data-reinit.md)
- [站台資料重新初始化](site-data-reinit.md)
- [SQL 設定](sql-configuration.md)
