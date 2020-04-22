---
title: 建立子設定項目
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中建立子設定項目。
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d194d9e80c037a13dde3d694793b695dfa5902e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693206"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>如何在 Configuration Manager 中建立子設定項目

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的子設定項目是設定項目的複本，其保留原始設定項目的關聯性，因此會繼承父設定項目的原始設定。  

當您在 Configuration Manager 主控台中檢視子設定項目的內容時，無法編輯含有其驗證準則的繼承物件和設定。 不過，您可以將額外驗證準則新增至子組態項目並加以編輯，您也可以將新的物件和設定新增至子組態項目。
建立和編輯子設定項目的範例，是重新調整原始設定項目以符合商務需求。  

> [!NOTE]  
>  您只能透過 [Windows 桌上型電腦和伺服器 (自訂)]  類型的組態項目來建立子組態項目。  

## <a name="to-create-a-child-configuration-item"></a>若要建立子組態項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性]   > [相容性設定]   > [設定項目]  。  

3.  在 [設定項目]  清單中，選取您要為其建立子設定項目的設定項目，然後在 [首頁]  索引標籤的 [設定項目]  群組中，按一下 [建立子設定項目]  。  

4.  在 [建立子設定項目精靈]  的 [一般]  頁面中，您可以選擇父設定項目的特定修訂版以用來建立子項。 此精靈的其他步驟與建立標準組態項目的步驟一致。 如需詳細資訊，請參閱[如何為 Windows 桌上型電腦和伺服器電腦建立自訂設定項目](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)。  

5.  完成精靈。 新的子設定項目即會顯示在 [設定項目]  清單中。  
