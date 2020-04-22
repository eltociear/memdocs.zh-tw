---
title: Configuration Manager 與 Windows 即服務
titleSuffix: Configuration Manager
description: 了解如何採用 Configuration Manager 最新分支以支援 Windows 即服務的基本資訊。
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701246"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager 與 Windows 即服務

適用於：  Configuration Manager (最新分支)

Configuration Manager 可讓您完整控制 Windows 10 的功能更新。 為了完全採用 Windows 即服務模型，您也必須採用 Configuration Manager 最新分支模型。 為了保持 Windows 10 的最新狀態，您必須確保 Configuration Manager 的最新狀態以獲得最佳體驗。 您必須具備新版本的 Configuration Manager，才能充分善用 Windows 10 的全新企業功能。 本文是採用 Configuration Manager 最新分支的必要重點文章登陸頁面。 Configuration Manager 最新分支是取得 Windows 即服務的關鍵。

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>採用 Configuration Manager 最新分支的重要文章

| 文章        | 說明          | 
| ------------- |-------------|
|[Configuration Manager 最新分支概觀](../plan-design/changes/whats-new-incremental-versions.md)|提供 Configuration Manager (目前分支) 新服務模型的簡短重點摘要|
|[支援週期](../servers/manage/current-branch-versions-supported.md)|說明新的支援與服務模型。|
|[已移除和已取代的項目](../plan-design/changes/deprecated/removed-and-deprecated.md)|提早通知可能會影響您使用 Configuration Manager 的未來變更。|
|[Configuration Manager 最新分支的更新](../servers/manage/updates.md)|說明可將功能更新套用至 Configuration Manager 的簡單主控台內方式。|
|[取得可用的更新](../servers/manage/install-in-console-updates.md#get-available-updates)|說明可用來取得全新 Configuration Manager 功能更新的兩種模式。|
|[更新檢查清單](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|提供特定版本的更新檢查清單 (如果適用的話)。| 
|[安裝新的 Configuration Manager 功能更新](../servers/manage/install-in-console-updates.md#bkmk_install)|說明功能更新的簡單安裝步驟。|
|[Windows 10 的支援](../plan-design/configs/support-for-windows-10.md)|提供 Windows 10 (與 ADK) 版本的支援矩陣。|
|[Technical Previews for Configuration Manager](../get-started/technical-preview.md)|提供 ConfigMgr Technical Preview 程式的資訊。|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>採用 Windows 即服務的重要文章

| 文章        | 說明          |
| ------------- |-------------|
|[將 Windows 作為服務管理](../../osd/deploy-use/manage-windows-as-a-service.md)|說明如何使用服務方案來部署 Windows 10 的功能更新。|
|[透過工作順序升級 Windows 10](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|利用其他建議建立工作順序以升級 Windows 10 的詳細資料。|
|[分階段部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|階段式部署可跨越多個集合，將協調且循序推出的工作順序自動化。|  
|[將 Windows 10 更新傳遞最佳化](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|使用 Configuration Manager 來管理更新內容，讓 Windows 10 隨時保持最新狀態。|
|[使用電腦分析](../../desktop-analytics/overview.md)|電腦分析可讓您評定和分析環境中裝置的整備，以升級至 Windows 10。|
|[商務用 Windows Update 整合 (選擇性)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|說明如何使用 Configuration Manager 定義及部署商務用 Windows Update (WUfB) 原則。|
|[針對 Microsoft Intune 和商務用 Windows Update 使用共同管理功能 (選擇性)](../../comanage/overview.md)|提供共同管理功能的概觀|


## <a name="related-articles"></a>相關文章

- [從 System Center 2012 Configuration Manager 就地升級至 Configuration Manager 最新分支](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [遷移至 Configuration Manager 最新分支的規劃](../migration/planning-for-migration.md)
