---
title: 對 SQL 複寫進行疑難排解
titleSuffix: Configuration Manager
description: 使用這些圖表來協助了解 Configuration Manager 站台之間的 SQL 複寫，並對其進行疑難排解
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703986"
---
# <a name="troubleshoot-sql-replication"></a>對 SQL 複寫進行疑難排解

在多站台階層中，Configuration Manager 會使用 SQL 複寫在站台之間傳送資料。 如需詳細資訊，請參閱[資料庫複寫](../../../plan-design/hierarchy/database-replication.md)。

若要深入了解 SQL 複寫並協助對其問題進行疑難排解，請使用這些圖表。

- [SQL 複寫](sql-replication.md)
- [SQL 設定](sql-configuration.md)
- [SQL 效能](sql-performance.md)
- [SQL 複寫重新初始化 (reinit)](sql-replication-reinit.md)
- [全域資料重新初始化](global-data-reinit.md)
- [站台資料重新初始化](site-data-reinit.md)
- [將遺失的訊息重新初始化](reinit-missing-message.md)

這些疑難排解圖表是相互連接的。 使用下列圖表來了解其關聯性：

![SQL 複寫疑難排解程序的概觀圖表](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

如需詳細資訊，請參閱下列來自 Microsoft 支援服務的部落格系列文章：

- [ConfigMgr DRS 同步處理內部資訊](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317) \(英文\)
- [已推出 ConfigMgr 2012 資料複寫服務 (DRS)](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916) \(英文\)
- [ConfigMgr 2012 DRS – 疑難排解常見問題集](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934) \(英文\)
- [ConfigMgr 2012 DRS 初始化內部資訊](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948) \(英文\)
- [ConfigMgr 2012：DRS 和 SQL Service Broker 憑證問題](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910) \(英文\)
