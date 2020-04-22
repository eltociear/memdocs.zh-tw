---
title: 規劃移轉
titleSuffix: Configuration Manager
description: 先了解站台和階層，再將資料移轉至 Configuration Manager 最新分支目的地階層。
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702826"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>遷移至 Configuration Manager 最新分支的規劃

適用於：  Configuration Manager (最新分支)

將資料遷移至 Configuration Manager 最新分支目的地階層之前，請確定您熟悉 Configuration Manager 中的站台和階層。 如需站台和階層的詳細資訊，請參閱 [Configuration Manager 的基礎](../../core/understand/fundamentals.md)。  

將 Configuration Manager 最新分支階層安裝為目的地階層，才能從支援的來源階層移轉資料。  

在您安裝目的地階層後，可先設定想要在目的地階層中使用的管理特性和功能，然後再開始移轉資料。  

此外，您可能必須規劃來源階層和目的地階層之間的重疊。 例如，您可以將來源階層設定為使用相同網路位置或界限作為目的地階層，然後在目的地階層安裝新用戶端，並使用自動站台指派。 在此案例中，由於全新安裝的 Configuration Manager 用戶端可以從任一階層選取站台加入，因此可能會不正確地將用戶端指派到您的來源階層。 因此，請規劃將目的地階層中的每個新用戶端指派給該階層的特定站台，而不使用自動站台指派。  

如需站台指派的詳細資訊，請參閱 [Configuration Manager 不同版本之間的互通性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)中的[用戶端站台指派考量](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment)。  

使用下列文章有助於規劃如何將支援的來源階層遷移至 Configuration Manager 目的地階層：

-   [移轉必要條件](../../core/migration/prerequisites-for-migration.md)  

-   [系統管理員移轉規劃檢查清單](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [判斷是否要將資料遷移至 Configuration Manager 最新分支](../../core/migration/determine-whether-to-migrate-data.md)  

-   [規劃來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [系統管理員移轉規劃檢查清單](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [規劃用戶端移轉策略](../../core/migration/planning-a-client-migration-strategy.md)  

-   [規劃內容部署移轉策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [規劃將 Configuration Manager 物件移轉至 Configuration Manager 最新分支](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [規劃監視移轉活動](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [規劃完成移轉](../../core/migration/planning-to-complete-migration.md)  
