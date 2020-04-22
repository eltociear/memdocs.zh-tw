---
title: 監視移轉
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 主控台來監視移轉工作的進度和成功與否。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693396"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>規劃在 Configuration Manager 中監視移轉活動

適用於：  Configuration Manager (最新分支)

藉由 Configuration Manager，您就可以在連線至目的地階層的 Configuration Manager 主控台中監視移轉。 在 Configuration Manager 主控台的 [管理]  工作區中，您可以使用 [移轉]  節點監視移轉工作的進度和成功與否。 您可以檢視每個移轉作業 (可識別已移轉的物件) 的摘要資訊、哪些物件尚未移轉，以及排除在移轉作業之外的物件數目。 您還可以查看與移轉問題相關的詳細資料。  

## <a name="view-migration-progress"></a>檢視移轉進度  
 若要檢視移轉作業的進度，請使用下列任何一項動作：  

-   在 Configuration Manager 主控台的 [管理]  工作區中，展開 [移轉作業]  節點，並選取移轉作業，然後選取 [作業中的物件]  索引標籤。  

-   使用 Configuration Manager 記錄檔檢閱移轉進度，或識別任何問題。 移轉管理員是一種 Configuration Manager 程序，可追蹤移轉動作，並將這些動作記錄在站台伺服器上 **\&lt;安裝路徑\>\\LOGS** 資料夾的 migmctrl.log 檔案中。  

    > [!NOTE]  
    >  如果移轉作業失敗，請盡快檢閱 migmctrl.log 檔案中的詳細資料。 移轉記錄檔項目會持續新增至檔案，並覆寫舊的詳細資料。 如果項目遭到覆寫，您可能無法識別移轉物件所遇到的問題，是否與移轉問題有關。 移轉活動會記錄在階層的頂層站台，不論您在設定移轉時 Configuration Manager 主控台連線到哪個站台。  

-   使用 Configuration Manager 報告。 Configuration Manager 提供多種內建移轉報告，或者您也可以編輯這些報告以符合您的需求。 如需 Configuration Manager 報表的詳細資訊，請參閱[報告簡介](../servers/manage/introduction-to-reporting.md)。  
