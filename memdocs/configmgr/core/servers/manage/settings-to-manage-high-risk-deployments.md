---
title: 管理高風險部署
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中設定部署驗證站台設定，於系統管理員建立高風險部署時對其發出警告。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703296"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>管理 Configuration Manager 高風險部署的設定

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager，您可以設定「部署驗證」  站台設定。 這些設定會在系統管理員建立高風險工作順序部署時發出警告。 高風險部署的定義：  

- 自動安裝的部署  

- 有可能會導致非預期的結果  

例如，具有**必要**用途且會部署作業系統的工作順序，會被視為高風險。  

> [!WARNING]
> 如果您使用 PXE 部署，並以網路介面卡作為第一個開機裝置來設定裝置硬體，則這些裝置就可以自動啟動 OS 部署工作順序，而不需要使用者互動。 部署驗證不會管理此設定。 雖然此設定可以簡化處理程序並減少使用者互動，但會將裝置置於意外重新安裝映像的更高風險中。

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a> 部署驗證設定

若要降低不需要的高風險部署所帶來的風險，您可以設定這些部署驗證設定中的大小限制：  

- **收集大小限制**：當您建立部署時，隱藏所含用戶端數目超過限制的集合。  

  - **預設大小**：當您建立部署時，此設定預設會隱藏所含用戶端數目超過此限制的集合。 您仍然可以在建立部署時看到這些集合，但預設會予以隱藏。 預設值為 **100**。 輸入的值為 **0** 時可忽略此設定。  

  - **大小上限**：當您建立部署時，此設定一律會隱藏所含用戶端數目超過此限制的集合。 預設值是 **0**，其會忽略此設定。 [大小上限]  的值必須大於 [預設大小]  的值。  

    例如，將 [預設大小]  設為 100，而 [大小上限]  設為 1000。 當您建立高風險部署時，[選取集合]  視窗只會顯示所含用戶端低於 100 個的集合。 如果您清除 [隱藏成員計數大於站台大小上限設定的集合]  設定，則此視窗會顯示所含用戶端低於 1000 個的集合。  

- **包含站台系統伺服器的集合**：當目標集合包含具有站台系統角色的電腦時封鎖部署，或在建立部署之前要求驗證。 當部署遭到封鎖時，請選取另一個符合部署驗證準則的集合，以繼續建立部署。  

> [!NOTE]
> 高風險的部署一律限制於自訂集合、您建立的集合，以及內建的 [未知的電腦]  集合。 當您建立高風險的部署時，您無法選取 [所有系統]  這類的內建集合。  

## <a name="configure-deployment-verification"></a>設定部署驗證

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區、展開 [站台設定]  、選取 [站台]  ，然後選取要設定的主要站台。

2. 在功能區中，選取 [屬性]  ，然後切換到 [部署驗證]  索引標籤。

3. 設定您想要使用的[設定](#bkmk_settings)，然後選取 [確定]  以儲存設定並關閉屬性。

## <a name="next-steps"></a>後續步驟

[管理工作順序 - 具有強烈影響的設定](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[設定站台和階層](../deploy/configure/configure-sites-and-hierarchies.md)
