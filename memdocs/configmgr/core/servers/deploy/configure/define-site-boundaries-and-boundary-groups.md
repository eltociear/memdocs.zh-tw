---
title: 使用界限和界限群組
titleSuffix: Configuration Manager
description: 使用界限和界限群組來為您管理的裝置，定義網路位置與可存取的站台系統。
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b1a6bb6ff9fdffad65db884fe8c3b68d3fc3263
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690896"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>定義站台界限與界限群組

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的「界限」  會定義您內部網路上的網路位置。 這些位置包括您想要管理的裝置。 「界限群組」  是您所設定之界限的邏輯群組。

一個階層可以包含任意數目的界限群組。 每個界限群組均可包含下列界限類型的任意組合：  

- IP 子網路  
- Active Directory 站台名稱  
- IPv6 首碼  
- IP 位址範圍  

內部網路上的用戶端會評估其目前網路位置，然後使用該資訊來識別所屬界限群組。  

用戶端將界限群組用於：  

- **尋找指派的站台：** 界限群組讓用戶端能夠在主要站台尋找用戶端指派。 此行為亦稱為「自動站台指派」  。  

- **尋找可用的特定站台系統角色：** 將界限群組關聯至特定的站台系統角色。 接著，站台會為用戶端提供界限群組中的站台系統清單。 用戶端會使用這些站台系統來進行尋找內容或附近管理點之類的動作。  

位於內部網路的用戶端或設為僅限內部網路的用戶端不會使用界限資訊。 這些用戶端不會使用自動站台指派。 它們可以從其指派站台中以網際網路為基礎的發佈點或雲端式發佈點下載內容。  

從 1902 版開始，您可以將雲端管理閘道 (CMG) 關聯至界限群組。 如需詳細資訊，請參閱 [CMG 階層設計](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design)。<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a> 建議

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>使用符合您需求的最少界限混合

使用您選擇之適合您環境類型的一或多個界限類型。 若要簡化管理工作，請使用可讓您使用最少界限數目的界限類型。

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>避免重疊自動站台指派的界限

雖然每個界限群組都同時支援站台指派和站台系統參考，還是要分別建立一組僅適用於站台指派的界限群組。 請確保界限群組中的每個界限均非另一個具有不同站台指派之界限群組的成員。

- 單一界限可包含於多個界限群組中  

- 每個界限群組都可以和不同主要站台建立關係以進行站台指派  

- 若界限為兩個具有不同站台指派之界限群組的成員，則用戶端會隨機選取要加入的站台。 此行為可能不適用您想要讓用戶端加入的站台。 此設定稱為「重疊界限」  。  

    對於內容位置而言，重疊界限不會產生問題。 它可以是一個很實用的設定，可為用戶端提供其可使用的額外資源或內容位置。  


## <a name="next-steps"></a>後續步驟

- [將網路位置定義為界限](boundaries.md)

- [設定界限群組](boundary-groups.md)
