---
title: 設定電源管理
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中設定電源管理。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696596"
---
# <a name="configure-power-management-in-configuration-manager"></a>在 Configuration Manager 中設定電源管理

適用於：  Configuration Manager (最新分支)

本文會說明如何在 Configuration Manager 中設定電源管理。

## <a name="enable-and-configure-client-settings"></a>啟用及設定用戶端設定

此程序會設定電源管理的「預設用戶端設定」  。 套用至您階層中的所有電腦。

如果您只想要將這些設定套用至部分電腦，請建立「自訂裝置用戶端設定」  。 然後將它指派給包含電源管理電腦的集合。 如需詳細資訊，請參閱[如何設定用戶端設定](../../deploy/configure-client-settings.md)。  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後依序選取 [用戶端設定]  節點和 [預設用戶端設定]  。

1. 在功能區 [常用]  索引標籤的 [內容]  群組中，選取 [內容]  。  

1. 選取 [電源管理]  群組。  

1. 啟用用戶端設定以 [允許管理裝置電源]  。

1. 設定您需要的其他用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定 - 電源管理](../../deploy/about-client-settings.md#power-management)。  

用戶端會在下次下載用戶端原則時設定這些設定。 若要起始單一用戶端的原則擷取，請參閱[如何管理用戶端](../manage-clients.md#BKMK_PolicyRetrieval)。  

## <a name="exclude-computers"></a>排除電腦

您可以阻止電腦集合接收電源管理設定。 如果電腦為排除在電源管理設定外之「任何」  集合的成員，該電腦即不適用電源管理設定。 即使它是另一個套用電源管理設定集合的成員，也適用此行為。  

您可能因為下列原因而想要將電腦排除在電源管理之外：  

- 因為業務需要，電腦必須隨時保持開啟狀態。  

- 您有一個不想套用電源管理設定的電腦控制項集合。  

- 某些電腦無法套用電源管理設定。  

- 您想要電源管理排除執行 Windows Server 的電腦。  

> [!NOTE]  
> 如果用戶端設定設定為 [允許使用者從電源管理排除其裝置]  ，使用者就可以使用軟體中心將自己的電腦排除在電源管理之外。  

若要找出排除在電源管理外的電腦，請執行 [排除的電腦]  報告。 如需此報告的詳細資訊，請參閱[如何監視和規劃電源管理](monitor-and-plan-for-power-management.md#BKMK_Excluded)。  

> [!IMPORTANT]  
> 將電腦排除在電源管理外，會造成所有電源設定還原成其原始值。 您無法將個別的電源設定還原為其原始值。  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>如何從電源管理排除電腦集合  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選擇 [裝置集合]  節點。  

1. 選取您要排除在電源管理外的集合。 在功能區 [常用]  索引標籤的 [內容]  群組中，選取 [內容]  。  

1. 切換至 [電源管理]  索引標籤，然後選取 [絕不套用電源管理設定到此集合中的電腦]  。  

## <a name="next-steps"></a>後續步驟

[如何建立和套用電源計劃](create-and-apply-power-plans.md)

[如何監視和規劃電源管理](monitor-and-plan-for-power-management.md)
