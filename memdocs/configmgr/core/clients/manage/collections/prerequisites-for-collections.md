---
title: 集合必要條件
titleSuffix: Configuration Manager
description: 取得在 Configuration Manager 中使用集合的必要條件。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695536"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Configuration Manager 中集合的必要條件

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的集合只包含產品內的相依性。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

|相依性|更多資訊|  
|----------------|----------------------|  
|Reporting Services 點|必須先安裝 Reporting Services 點站台系統角色，才能執行集合的報告。 如需詳細資訊，請參閱[報告簡介](../../../servers/manage/introduction-to-reporting.md)。|  
|若要管理集合，必須授與特定的安全性權限。|您必須具備下列安全性權限來管理合規性設定：<br /><br /> - 建立和管理集合：[集合]  物件的 [建立]  、[刪除]  、[修改]  、[修改資料夾]  、[移動物件]  、[讀取]  和 [讀取資源]  。<br /><br /> - 管理集合設定：[集合]  物件的 [修改集合設定]  。<br /><br /> 需要所有集合資料夾 (包括根資料夾) 的 [修改資料夾]  權限。|  
