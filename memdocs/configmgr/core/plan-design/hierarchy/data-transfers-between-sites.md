---
title: 站台間的資料傳輸
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 如何在站台之間移動資料，以及如何管理資料在您網路上的傳輸。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703616"
---
# <a name="data-transfers-between-sites"></a>站台間的資料傳輸

適用於：  Configuration Manager (最新分支)

Configuration Manager 會使用*檔案複寫*與*資料庫複寫*在站台之間傳送不同類型的資訊。 了解 Configuration Manager 如何在站台之間移動資料，以及如何管理資料在您網路上的傳輸。  

## <a name="types-of-replication"></a>複寫類型

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /> 檔案型複寫

Configuration Manager 會使用檔案複寫在階層中網站間傳送檔案資料。 此資料包括您想要部署到子站台中發佈點的應用程式和封裝。 它也會處理未處理的探索資料記錄，站台會將這些資料記錄傳送至其父站台，然後加以處理。  

如需詳細資訊，請參閱[檔案型複寫](file-based-replication.md)。

### <a name="database-replication"></a><a name="bkmk_dbrep" /> 資料庫複寫

Configuration Manager 資料庫複寫會使用 SQL Server 來傳輸資料。 它會使用這個方法，將其站台資料庫中的變更與階層中其他站台資料庫的資訊合併。

如需詳細資訊，請參閱[資料庫複寫](database-replication.md)。

如需針對 SQL 複寫進行疑難排解的協助，請參閱[針對 SQL 複寫進行疑難排解](../../servers/manage/replication/overview.md)。

## <a name="see-also"></a>請參閱

[監視複寫](../../servers/manage/monitor-replication.md)
