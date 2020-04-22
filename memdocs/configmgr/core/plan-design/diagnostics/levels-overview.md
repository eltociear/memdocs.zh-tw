---
title: 診斷使用方式資料的層級
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 所收集的診斷及使用方式資料層級
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703796"
---
# <a name="levels-of-diagnostic-usage-data"></a>診斷使用方式資料的層級

適用於：  Configuration Manager (最新分支)

Configuration Manager 會收集三個層級的診斷及使用方式資料：[基本]  、[增強]  和 [完整]  。 這項功能預設會設定為增強層級。

> [!IMPORTANT]
> Configuration Manager 不會在「基本」層級或「增強」層級上收集站台碼、站台名稱、IP 位址、使用者名稱、電腦名稱、實體位址或電子郵件地址。 在「完整」層級上對此資訊所做的任何收集都不具目的性。 在記錄檔或記憶體快照等進階診斷資訊中即潛在地包含此資訊。 Microsoft 不會使用這項資訊來辨識或連絡您，也不會用作廣告用途。

## <a name="levels"></a>層級

### <a name="basic"></a>基本

「基本」層級包含您階層的相關資料。 這是協助改善您安裝或升級體驗的必要項目。 這項資料也可協助判斷適用於您階層的 Configuration Manager 更新。

### <a name="enhanced"></a>增強

「增強」層級是安裝完成後的預設值。 這個層級包含「基本」層級中所收集資料和功能的特定資料。 它會顯示不同功能的使用頻率和持續時間。 它也包含 Configuration Manager 用戶端設定資料：元件名稱、狀態、輪詢間隔等特定設定。 軟體更新相關資訊只會包含功能使用方式的基礎資訊，不包含此層級更新合規性的資料。

Microsoft 建議您使用這個層級，因為其會提供 Microsoft 必要的基本資料，以在產品和服務版本中做出改善。

此層級不會收集的資料，如下列一些範例所示：

- 站台、使用者、電腦或其他物件的名稱

- 安全性相關物件的詳細資料

- 弱點 (例如需要軟體更新的系統數量)

### <a name="full"></a>完整

「完整」層級包含「基本」和「增強」層級中的所有資料。 它也包含 Endpoint Protection、更新相容性百分比和軟體更新資訊的其他資訊。 此層級也可包含系統檔案和記憶體快照等進階診斷資訊。 這項進階資料可能包含擷取時存在於記憶體或記錄檔中的個人資訊。

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> 如何變更層級

若要變更資料收集層級，您需要**站台**物件類別上的**修改**權限。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。
1. 在功能區中選取 [階層設定]  。
1. 切換至 [診斷及使用方式資料]  索引標籤，然後選擇資料層級。

## <a name="version-specific-details"></a><a name="bkmk_versions"></a> 版本特定詳細資料

下列文章詳細說明 Configuration Manager 以每個支援版本在每個層級上收集的特定資料：

- [2002 的診斷及使用方式資料](levels-of-diagnostic-usage-data-collection-2002.md)
- [1910 的診斷及使用方式資料](levels-of-diagnostic-usage-data-collection-1910.md)
- [1906 的診斷及使用方式資料](levels-of-diagnostic-usage-data-collection-1906.md)
- [1902 的診斷及使用方式資料](levels-of-diagnostic-usage-data-collection-1902.md)
- [1810 的診斷及使用方式資料](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [常見問題集](frequently-asked-questions.md)
