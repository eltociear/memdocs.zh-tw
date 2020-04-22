---
title: SQL 設定
titleSuffix: Configuration Manager
description: 使用此圖表來開始對 Configuration Manager 的 SQL 設定進行疑難排解
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707616"
---
# <a name="sql-configuration"></a>SQL 設定

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

使用下列圖表來開始對與 SQL Service Broker 相關的 SQL 設定進行疑難排解：

![用來對 SQL 設定進行疑難排解的圖表](media/sql-configuration.svg)

## <a name="queries"></a>查詢

此圖表具有下列查詢和動作：

### <a name="check-if-sql-can-deliver-ssb-messages"></a>檢查 SQL 是否能傳遞 SSB 訊息

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>補救動作

### <a name="remediate-the-issues-reported-from-transmission_status"></a>補救從 transmission_status 回報的問題

常見問題：

- 防火牆設定
- 網路組態
- SSB 憑證設定錯誤

### <a name="run-sql-profiler-to-trace-ssb-events"></a>執行 SQL Profiler 來追蹤 SSB 事件

在 CAS 和主要站台資料庫上執行 SQL Profiler 來追蹤與 SQL Service Broker 相關的事件：

- **Audit Broker Login**
- **Audit Broker Conversation**
- **Broker** 類別中的事件
