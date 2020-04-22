---
title: 診斷資料集合
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 如何收集本身的診斷及使用資料。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688466"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Configuration Manager 如何收集診斷及使用方式資料

適用於：  Configuration Manager (最新分支)

為了收集 Configuration Manager 的診斷和使用資料，每個主要站台每週都會執行 SQL Server 查詢。 在多站台階層中，會將資料複寫至管理中心網站。  

在階層的頂層站台，服務連接點會在檢查更新時提交此資訊。 服務連接點的模式決定資料傳輸方式︰

- **連線**：服務連接點會每週一次自動將診斷及使用方式資料傳送至雲端服務。

- **離線**：使用[服務連線工具](../../servers/manage/use-the-service-connection-tool.md)來手動傳輸診斷及使用方式資料。

如需詳細資訊，請參閱 [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) (關於服務連接點)。

> [!div class="nextstepaction"]
> [如何檢視診斷和使用情況資料](view-diagnostics-and-usage-data.md)
