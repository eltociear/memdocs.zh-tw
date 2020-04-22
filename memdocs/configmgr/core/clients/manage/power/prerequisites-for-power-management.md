---
title: 電源管理的必要條件
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 中電源管理的必要條件。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696516"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Configuration Manager 中電源管理的必要條件

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的電源管理具有外部相依性和產品內的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  
 下表列出 Configuration Manager 外部使用電源管理的相依性。  

|相依性|更多資訊|  
|----------------|----------------------|  
|用戶端電腦必須可以支援必要的電源狀態|若要使用電源管理的所有功能，用戶端電腦必須可以支援睡眠、休眠、從睡眠喚醒，以及從休眠喚醒的動作。 您可以使用 [電源功能]  報告，判斷電腦是否可支援這些動作。 如需詳細資訊，請參閱[如何監視和規劃電源管理](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)主題中的[電源功能報告](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites)。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  
 下表列出 Configuration Manager 內部使用電源管理的相依性。  

|相依性|更多資訊|  
|----------------|----------------------|  
|必須先啟用電源管理，才能建立和監視電源計劃。|如需如何啟用和設定電源管理的相關資訊，請參閱[設定電源管理](../../../../core/clients/manage/power/configuring-power-management.md)。|  
|Reporting Services 點|您必須先設定 Reporting Services 點，才能檢視電源管理報告。 如需詳細資訊，請參閱[報告簡介](../../../servers/manage/introduction-to-reporting.md)。|  
