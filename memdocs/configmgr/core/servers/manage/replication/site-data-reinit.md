---
title: 網站資料重新初始化
titleSuffix: Configuration Manager
description: 使用此圖表開始針對 Configuration Manager 階層中的站台資料進行 SQL 複寫重新初始化疑難排解
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078580"
---
# <a name="troubleshoot-site-data-reinit"></a>針對站台資料重新初始化進行疑難排解

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

使用下列圖表開始針對 Configuration Manager 階層中的站台資料進行 SQL 複寫重新初始化疑難排解：

![針對站台資料重新初始化進行疑難排解的圖表](media/site-data-reinit.svg)

## <a name="queries"></a>查詢

此圖表會使用下列查詢：

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>檢查站台複寫是否尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>從 CA 取得 TrackingGuid 與狀態

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>從主要站台取得 TrackingGuid 與狀態

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>檢查主要站台是否未處於維護模式

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>檢查追蹤識別碼的要求狀態

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>後續步驟

- [將遺失的訊息重新初始化](reinit-missing-message.md)
- [全域資料重新初始化](global-data-reinit.md)
