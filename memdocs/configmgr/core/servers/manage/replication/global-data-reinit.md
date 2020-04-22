---
title: 全域資料重新初始化
titleSuffix: Configuration Manager
description: 使用此圖表開始針對 Configuration Manager 階層中的全域資料進行 SQL 複寫重新初始化疑難排解
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694296"
---
# <a name="troubleshoot-global-data-reinit"></a>針對全域資料重新初始化進行疑難排解

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

使用下列圖表開始針對 Configuration Manager 階層中的全域資料進行 SQL 複寫重新初始化疑難排解：

![針對全域資料重新初始化進行疑難排解的圖表](media/global-data-reinit.svg)

## <a name="queries"></a>查詢

此圖表使用下列查詢：

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>檢查站台複寫是否尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>從主要站台取得 TrackingGuid 與狀態

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>從 CA 取得 TrackingGuid 與狀態

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>檢查追蹤識別碼的要求狀態

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>後續步驟

- [將遺失的訊息重新初始化](reinit-missing-message.md)
