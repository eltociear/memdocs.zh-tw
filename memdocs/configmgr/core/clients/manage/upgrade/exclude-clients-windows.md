---
title: 針對 Windows 排除用戶端升級
titleSuffix: Configuration Manager
description: 了解如何在 System Center Configuration Manager 中排除 Windows 用戶端不進行升級。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696846"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>如何在 Configuration Manager 中排除用戶端不進行升級

適用於：  Configuration Manager (最新分支)

您可以排除用戶端集合自動安裝更新的用戶端版本。 此排除功能可用於在升級用戶端時，需要更小心對待的電腦集合。 在排除集合中的用戶端會略過安裝更新版用戶端軟體的要求。

此排除功能適用於下列方法：

- 自動升級
- 以軟體更新為基礎的升級
- 登入指令碼
- 群組原則

> [!NOTE]
> 雖然使用者介面指出用戶端不會透過任何方法升級，但您可以使用兩種方法來覆寫這些設定。 請使用用戶端推入安裝和手動用戶端安裝來覆寫此設定。 如需詳細資訊，請參閱[如何升級已排除的用戶端](#bkmk_override)。

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a> 設定排除

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，選取 [站台]  節點，然後在功能區中選取 [階層設定]  。

2. 切換至 [用戶端升級]  索引標籤。

3. 選取 [排除指定的用戶端不進行升級]  選項。 然後選取您要排除的**排除集合**。 您只能選取單一集合進行排除。

4. 選取 [確定]  以關閉並儲存設定。

![自動升級的排除範圍設定](media/automatic_upgrade_exclusion.png)

排除集合中的用戶端更新原則之後，它們不會自動安裝用戶端更新。 如需詳細資訊，請參閱[如何升級 Windows 電腦的用戶端](upgrade-clients-for-windows-computers.md)。

> [!NOTE]
> 排除的用戶端仍會下載並執行 Ccmsetup，但不會升級。

當您將用戶端從排除集合移除時，直到下一個自動升級週期為止，它都不會自動升級。

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a> 如何升級已排除的用戶端

如果裝置是您從升級排除之集合的成員，您仍然可以使用下列其中一種方法來升級用戶端：

- **用戶端推入安裝**：Ccmsetup 允許用戶端推入安裝，因為它是您的直接意圖。 此方法可讓您升級用戶端，而不需將它從集合中移除，或將整個集合從排除中移除。

- **手動用戶端安裝**：使用下列 Ccmsetup 命令列參數手動升級已排除的用戶端： **/IgnoreSkipUpgrade**

    如果您嘗試手動升級屬於排除集合成員的用戶端，但未使用此參數，則該用戶端不會升級。 如需詳細資訊，請參閱[如何手動安裝 Configuration Manager 用戶端](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)。

## <a name="see-also"></a>請參閱

- [升級用戶端](upgrade-clients.md)

- [如何將用戶端部署至 Windows 電腦](../../deploy/deploy-clients-to-windows-computers.md)

- [延伸互通性用戶端](../../../understand/interoperability-client.md)
