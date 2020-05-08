---
title: 診斷和使用方式資料
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 所收集關於本身的診斷及使用方式資料。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904407"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Configuration Manager 的診斷及使用方式資料

適用於：  Configuration Manager (最新分支)

Configuration Manager 會收集與其本身相關的診斷和使用方式資料，Microsoft 會使用這些資料來改進未來版本的安裝體驗、品質及安全性。  

每個 Configuration Manager 階層都會啟用診斷和使用方式資料。 其是由每週在每個主要站台和管理中心網站 (CAS) 上執行的 SQL Server 查詢所組成。 當階層使用 CAS 時，子主要站台會將其資料複寫至該 CAS。 在您階層的頂層站台，[服務連接點](../../servers/deploy/configure/about-the-service-connection-point.md)會在檢查更新時提交此資訊。 如果服務連接點處於離線模式，則可使用[服務連線工具](../../servers/manage/use-the-service-connection-tool.md)來傳送此資訊。

> [!NOTE]  
> Configuration Manager 只會從站台的 SQL Server 資料庫收集資料，而不會直接從用戶端或站台伺服器收集資料。  

如需詳細資訊，請參閱 [Microsoft 隱私權聲明](https://privacy.microsoft.com/privacystatement)。  

> [!div class="nextstepaction"]
> [Microsoft 如何使用診斷及使用方式資料](how-diagnostics-and-usage-data-is-used.md)
