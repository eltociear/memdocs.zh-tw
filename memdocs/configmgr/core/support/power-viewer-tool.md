---
title: Power Viewer 工具
titleSuffix: Configuration Manager
description: 使用 Power Viewer 工具，檢視 Configuration Manager 用戶端上的電源管理功能狀態。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707566"
---
# <a name="power-viewer-tool"></a>Power Viewer 工具

適用於：  Configuration Manager (最新分支)

Power Viewer 工具是其中一種 [Configuration Manager 工具](tools.md)。 使用它來檢視 Configuration Manager 用戶端上的電源管理功能狀態。

以系統管理員身分執行 **PowerVwr.exe**。 工具啟動時，會在 [電源設定]  索引標籤上顯示本機電腦的電源功能和電源設定。 

檢視遠端電腦的電源管理資料：  

1. 移至 [檔案]  功能表，然後按一下 [連線]  。 

2. 輸入 [電腦]  名稱，以及 [使用者名稱]  和 [密碼]  (如有必要)。 

Power Viewer 有三個索引標籤：  

- **電源設定**：檢視目標電腦的電池容量和電源設定。  

- **每日活動**：檢視用戶端的每日活動圖表，其中包含下列資訊：  

    - **電腦開啟**：一天內電腦的電源狀態。 睡眠模式會視為關閉電源。  

    - **監視器開啟**：一天內監視器的開啟或關閉狀態。  

    - **作用中使用者**：一天內的使用者活動資訊。  

- **電源事件**：檢視所有每日電源事件。 用戶端會在早上 12:00 摘要這些事件。 此摘要會產生每日活動圖表的資料。  
