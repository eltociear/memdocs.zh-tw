---
title: 延伸互通性用戶端
titleSuffix: Configuration Manager
description: 了解如何使用延伸互通性用戶端，透過最新分支站台來取得靜態 Configuration Manager 用戶端的長期支援。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78e89307e66107b259d818a84fa4dbca878a843c
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590893"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>使用適用於延伸互通性的 Configuration Manager 用戶端軟體來搭配未來的「最新分支」站台版本使用

適用於：Configuration Manager (最新分支)  

商務需求可能不允許您定期更新某些裝置上的 Configuration Manager 用戶端。 例如，您需要遵循變更管理原則，或裝置為關鍵任務所需。 為配合這些需求，您可以安裝長期使用的新用戶端，稱為延伸互通性用戶端 (EIC)。 請將 EIC 只用於無法頻繁更新的特定裝置，例如資訊站或收銀機裝置。 至於您大部分的用戶端，則繼續使用[自動用戶端升級](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)。

## <a name="how-it-works"></a>運作方式

一般來說，當您為 Configuration Manager 安裝新的[主控台內更新](../servers/manage/install-in-console-updates.md)時，用戶端即會自動更新其用戶端軟體，以便使用這些新功能。 在這類案例中，您仍會更新為最新分支，並接收新功能和更新。 大多數裝置會使用您安裝的每個更新版本來更新 Configuration Manager 用戶端軟體。 不過，您可以在不想接收用戶端軟體更新的關鍵系統子集上，安裝延伸互通性用戶端。 除非您明確地對這些用戶端部署新版用戶端軟體，否則它們不會安裝新的用戶端軟體。

## <a name="supported-versions"></a>支援的版本

下表列出此案例所支援的 Configuration Manager 用戶端版本：

| 版本 | 可用時間 | 支援結束日期 |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 2019 年 3 月 27 日 | 不得早於 2021 年 3 月 27 日 |
| 1802<br/>5.00.8634 | 2018 年 5 月 1 日 | 不得早於 2020 年 5 月 1 日 |
| 1606<br/>5.00.8412 | 2016 年 11 月 18 日 | 2019 年 5 月 1 日 |

> [!TIP]  
> EIC 至少在發行日期兩年內都會受到支援。 如需發行日期的詳細資訊，請參閱 [Configuration Manager 最新分支版本支援](../servers/manage/current-branch-versions-supported.md)。  

在用戶端的支援到期之前，請針對您使用最新分支管理的裝置，規劃其上的延伸互通性用戶端更新。 若要執行此作業，請從 Microsoft 下載新版本的用戶端，然後將該更新的用戶端軟體部署到使用目前延伸互通性用戶端的裝置。

## <a name="how-to-use-the-eic"></a>如何使用 EIC

1. 將這些裝置新增至集合，然後從自動用戶端升級排除該集合。 如需詳細資訊，請參閱[如何排除用戶端不進行升級](../clients/manage/upgrade/exclude-clients-windows.md)。  

1. 從 Configuration Manager 更新安裝媒體的 `\SMSSETUP\Client` 資料夾取得支援的 EIC 版本。 確定您已複製整個資料夾的內容。  

<!--
    > [!TIP]
    > To find Configuration Manager media in the [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), go to the **Downloads and Keys** tab, and search for **Microsoft Endpoint Configmgr (current branch)**.
-->

1. 在那些裝置上手動安裝 EIC。 如需詳細資訊，請參閱[手動安裝用戶端](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)。  

    > [!Important]  
    > 將 1606 版用戶端升級為 1802 版時，請使用 CCMSETUP 選項 **/AlwaysExcludeUpgrade:True**。 否則，用戶端可能會從管理點收到原則，在排除原則之前自動升級。  

## <a name="limitations"></a>限制

- 您無法藉由使用主控台內更新，取得延伸互通性用戶端軟體的更新。 如需如何更新 EIC 的詳細資訊，請參閱[如何升級已排除的用戶端](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override)。  

- EIC 只支援下列功能：  

  - 軟體更新  
  - 硬體與軟體清查
  - 封裝和程式

## <a name="next-steps"></a>後續步驟

[如何排除用戶端不進行升級](../clients/manage/upgrade/exclude-clients-windows.md)

若要確保用戶端已正確安裝在您要的裝置上，請參閱[如何監視用戶端](../clients/manage/monitor-clients.md)。
