---
title: 集合最佳做法
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 集合的最佳做法。
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695236"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager 集合的最佳做法

適用於：  Configuration Manager (最新分支)

針對 Configuration Manager 集合，請使用下列最佳做法。  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a> 請勿將累加式更新用於許多集合

如果您啟用 [針對此集合使用累加式更新]  選項，這項組態可能會在針對許多集合啟用時，導致評估延遲。 臨界值約為階層中的 200 個集合。 確切數目則取決於下列因素：  

- 集合總數  

- 階層中新增資源和變更資源的頻率  

- 階層中的用戶端數目  

- 階層中集合成員資格規則的複雜性  

## <a name="maintenance-window-size-for-software-updates"></a>軟體更新的維護時段大小

您可以設定用於裝置集合的維護期間，以限制 Configuration Manager 可以在這些裝置上安裝軟體的次數。 如果您將維護時段設定得太小，則用戶端可能無法安裝重要的軟體更新，導致用戶端容易遭受攻擊，安裝軟體更新可降低遭受攻擊的風險。

> [!Tip]
> 規劃維護時段時要謹記的重要考慮事項：
>
> - 預設軟體更新執行階段上限為 60 分鐘。
> - 當 Configuration Manager 計算是否可以安裝更新時，它會將執行階段上限多加 5 分鐘，作為重新開機時間。
> - 維護時段的剩餘持續時間必須超過軟體更新執行階段上限加五分鐘的時間。
