---
title: 設定硬體清查
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中設定所有用戶端或集合的硬體清查。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695446"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>如何在 Configuration Manager 中設定硬體清查

適用於：  Configuration Manager (最新分支)

此程序可設定硬體清查的預設用戶端設定，並套用到階層中的所有用戶端。 如果您只想要將這些設定套用至部分用戶端，請建立自訂裝置用戶端設定，並將它指派給包含您要設定硬體清查之裝置的集合。 請參閱[如何設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)。  

> [!NOTE]  
>  如果用戶端裝置收到來自多組用戶端設定的硬體清查設定，則當用戶端報告硬體清查時，會將每組設定的硬體清查類別合併。 此外，未核取自訂用戶端設定中具有較高優先順序的類別，並不會使用戶端停用清查該類別。 

若要在除了少數系統以外的大多數系統上停用特定硬體清查類別，必須在預設用戶端設定中取消核取該類別。 然後建立自訂用戶端設定來啟用該類別，並將它部署到目標系統。


### <a name="to-configure-hardware-inventory"></a>若要設定硬體清查  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]   > [用戶端設定]   > [預設用戶端設定]  。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

5.  在 [預設設定]  對話方塊中，選擇 [硬體清查]  。  

6.  在 [裝置設定]  清單中，設定下列項目：  

    -   **在用戶端上啟用硬體清查** - 選取 [是]  。  

    -   **硬體清查排程** - 按一下 [排程]  指定用戶端收集硬體清查的時間間隔。  

7.  設定您需要的其他[硬體清查用戶端設定](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)。  

在下次下載用戶端原則時，用戶端裝置會使用這些設定來進行設定。 若要起始單一用戶端的原則擷取，請參閱[如何管理用戶端](../../../../core/clients/manage/manage-clients.md)。  
