---
title: 執行計量摘要工具
titleSuffix: Configuration Manager
description: 使用執行計量摘要工具，在 Configuration Manager 中觸發軟體計量摘要工作。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707536"
---
# <a name="run-meter-summarization-tool"></a>執行計量摘要工具

適用於：  Configuration Manager (最新分支)

執行計量摘要工具是其中一種 [Configuration Manager 工具](tools.md)。 使用它，立即觸發主要站台上軟體計量摘要的維護工作。 根據預設，這些工作會依 [站台維護]  工作中的排程執行，而這類工作在每天的上午 12:00 之後啟動。 

這些工作摘要 **MeterData** SQL 資料表中的資料，並將摘要結果寫入至 **FileUsageSummary** 和 **MonthlyUsageSummary** 資料表。 然後，您會在軟體計量報表中看到彙總結果。 任何可連線至主要站台資料庫的 Configuration Manager 系統管理使用者都可以使用此工具來執行摘要。 

此工具會執行 [檔案使用摘要]  和 [每月使用摘要]  軟體計量資料摘要工作。 它會摘要所有現有計量資料，而不需要一般 12 時制等待期間。 在裝載站台資料庫的 SQL Server 上執行它。 如果摘要成功，則結束代碼設定為 `0`。 如果發生錯誤，則結束代碼為 `1`。



## <a name="usage"></a>使用方式

### <a name="command-line"></a>命令列

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>選項

#### <a name="database-name"></a>資料庫名稱
SQL Server 上的站台資料庫名稱。

#### <a name="delay-in-hours-for-summarization"></a>摘要延遲 (小時)
此工具會摘要延遲之前所產生的軟體計量使用量。 根據預設，此延遲為零。


### <a name="example"></a>範例

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>摘要 12 小時前所產生的軟體計量使用量

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>請參閱

- [維護工作](../servers/manage/maintenance-tasks.md)
- [使用軟體計量監視應用程式使用量](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
