---
title: 將遺失的訊息重新初始化
titleSuffix: Configuration Manager
description: 使用此圖表來開始搭配 Configuration Manager 中的 SQL 複寫重新初始化對遺失的訊息進行疑難排解
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703976"
---
# <a name="reinit-missing-message"></a>將遺失的訊息重新初始化

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

使用下列圖表來開始搭配 SQL 複寫重新初始化 (reinit) 對遺失的訊息進行疑難排解：

![用來對將遺失的訊息重新初始化進行疑難排解的圖表](media/reinit-missing-message.svg)

## <a name="queries"></a>查詢

此圖表使用下列查詢：

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>檢查站台複寫是否尚未完成重新初始化

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>從訂閱者站台取得 TrackingGuid 與狀態

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>從發行站台取得 TrackingGuid 與狀態

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>補救動作

### <a name="version-1902-and-later"></a>1902 版和更新版本

若要偵測問題並重新初始化，請執行[複寫連結分析師](../monitor-replication.md#BKMK_RLA)。

### <a name="version-1810-and-earlier"></a>1810 版和更早版本

執行下列 SQL 查詢以取得 `ReplicationGroupID`：

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

然後搭配下列值使用 `SMS_ReplicationGroup` WMI 類別上的 `InitializeData` 方法：

- ReplicationGroupID：來自上述 SQL 查詢
- SiteCode1：父站台
- SiteCode2：子站台

如需詳細資訊，請參閱 [SMS_ReplicationGroup 類別的 InitializeData 方法](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md)。

#### <a name="example"></a>範例

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>後續步驟

- [SQL 複寫重新初始化 (reinit)](sql-replication-reinit.md)
