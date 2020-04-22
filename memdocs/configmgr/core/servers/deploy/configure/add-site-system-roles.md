---
title: 新增站台系統角色
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站台系統角色，以及如何新增角色以擴充站台的功能和容量。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8a4ef1c4377e7b5ffba4ab0f04394ff1253c40df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704896"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>為 Configuration Manager 新增站台系統角色

適用於：  Configuration Manager (最新分支)

每個 Configuration Manager 站台都支援多個站台系統角色。 每個角色都會擴充站台的功能與容量，以提供服務給站台以及管理裝置與使用者。 站台系統伺服器上的每個站台系統角色，都必須來自相同的站台。

Configuration Manager 不支援單一站台系統伺服器上多個站台的站台系統角色。

> [!TIP]
> 如果您不熟悉站台系統角色的基本概念，或不熟悉站台伺服器、站台系統伺服器與站台系統角色之間的差異，請參閱 [Configuration Manager 的基礎](../../../understand/fundamentals.md)。

下列文章會詳述安裝站台系統角色的程序與相關詳細資料：

- [安裝站台系統角色](install-site-system-roles.md)：有關如何使用兩個主控台內部精靈安裝新站台系統角色的基本指導。

- [安裝雲端發佈點](install-cloud-based-distribution-points-in-microsoft-azure.md)：使用 Microsoft Azure 託管部署至用戶端的內容。

- [安裝供內部部署行動裝置管理 (MDM) 使用的站台系統角色](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)：使用 Configuration Manager 內部部署 MDM，將站台系統角色設定為支援管理現代裝置。

- [站台系統角色的設定選項](configuration-options-for-site-system-roles.md)：有些站台系統角色支援需要更多詳細資料的設定，但使用者介面不足以說明。

- [移除站台系統角色](../install/uninstall-sites-and-hierarchies.md#bkmk_role)：從站台系統伺服器移除角色的指導和程序。
