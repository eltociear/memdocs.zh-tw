---
title: 如何部署至生產環境
titleSuffix: Configuration Manager
description: 部署至電腦分析生產環境群組的操作指南。
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0a7ffe8eea1048e696ce7dd254d58364226efc58
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268774"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>如何使用電腦分析部署至生產環境

在[部署至試驗](deploy-pilot.md)且檢閱過資產狀態後，即可隨時更新其餘的生產環境。

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

生產環境裝置更新部署有三大部分需要完成：

1. [檢閱需要升級決策的資產](#bkmk_review)：為使裝置就緒以供部署生產環境，其資產的升級決策必須設為 [就緒]  或 [Ready, remediations required] \(就緒 (需要補救)\)  。  

2. [部署至已就緒的裝置](#bkmk_deploy)：使用 Configuration Manager 更新已準備就緒的裝置。 電腦分析提供部署生產環境的就緒裝置清單，以及監視部署成功的報告。  

3. [監視已更新裝置的健全狀況](#bkmk_monitor)：隨著更新部署的進展，監視重要資產的健全狀況。 如有需要注意的資產，請針對其疑難排解並修正這些問題。 您若無法修正這些問題，請將受影響裝置的升級決策設為 [無法]  來停止部署這些裝置。  

> [!NOTE]  
> 當您對試驗部署的成功有十足把握時，可隨時開始生產環境部署。 不要求所有試驗裝置都必須先達到 [已完成] 狀態。  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a> 檢閱需要升級決策的資產

電腦分析會引導您完成檢閱生產環境部署資產的程序。 在 Azure 入口網站中，移至 [部署計劃]  並選取一項部署計劃，然後選取左側功能表中的 [準備生產]  。

![在電腦分析中準備生產環境檢視的螢幕擷取畫面](media/prepare-production.png)

檢閱應用程式的狀態。 使用此資訊為這些資產逐一設定升級決策。

使用每一個索引標籤來檢閱應用程式的狀態。 在每個索引標籤檢視中，您可以篩選結果以顯示要升級的裝置、需要注意的裝置、有混合結果的裝置，以及未定狀態的裝置。

選取 [Meeting Goals] \(達成目標\)  ，根據下列準則篩選可能已就緒可供部署生產環境的資產檢視：

- 風險：升級前已知風險評定 (針對已安裝此資產的裝置更新)  

- 健全狀態：裝置在其他部署中的升級後評定，以及安裝更新後是否發生問題。 如需健全狀況的詳細資訊，請參閱[監視已更新裝置的健全狀況](#bkmk_monitor)。  

若要核准升級某項資產，請在清單中選取其名稱，然後從 [升級決策]  清單中選取下列選項之一：

- 正在檢閱
- 準備
- 就緒 (有補救)
- 無法
- 未檢閱

若要一次為多個應用程式設定此值，針對 [選取此項目] 請使用第一欄  ，然後選擇 [設定升級決策]  。

![針對多個應用程式的 [設定升級決策] 選項](media/prep-prod-set-upgrade-decision.png)

選取 [無資料]  檢視無法分類的資產。 這些資產通常是電腦分析範圍不足的資產，因而無法分析風險或健全狀況的狀態。 若要改善涵蓋範圍，請將擁有這些資產的其他裝置新增至試驗，或要求試驗使用者嘗試使用這些資產。

有些資產狀態可能為 [需要注意]  或 [混合結果]  。 您可能需要另行檢閱這些資產，才能決定是否升級它們。

檢閱所有應用程式。 一旦所指定裝置的所有資產皆具有正向升級決策，其狀態就會變更為 [可用於生產環境]。 選取第三個部署步驟：**部署**，以查看目前部署計劃主頁上的計數。


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a> 部署至已就緒的裝置

Configuration Manager 會使用電腦分析的資料來建立生產環境部署集合。 請不要使用傳統部署來部署工作順序。 使用下列程序建立電腦分析整合式部署：

如已遵循建議程序來[部署至試驗裝置](deploy-pilot.md#deploy-to-pilot-devices)，則 Configuration Manager 階段式部署即準備就緒。 當您將資產標示為 [就緒]  時，電腦分析會自動同步處理這些裝置與 Configuration Manager。 然後，這些裝置就會新增至生產環境集合。 當階段式部署移至第二個階段時，這些生產環境裝置即會獲得升級部署。

如已將階段式部署設定為 [手動開始第二個階段部署]  ，即需要手動將它移至下一個階段。 如需詳細資訊，請參閱[管理和監視階段式部署](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move)。

如已在試驗集合建立電腦分析整合式單一部署，則需要重複該程序以部署至生產環境集合。


### <a name="address-deployment-alerts"></a>處理部署警示

和試驗部署一樣，電腦分析會建議您在生產環境部署期間需要注意的任何問題。 在電腦分析中，移至 [部署計劃]，然後選取左側功能表中的 [部署狀態]  。 [部署狀態] 檢視會列出下列類別的裝置：  

- 未開始
- 進行中
- Completed
- 需要注意 - 裝置 (依裝置名稱排序)
- 需要注意 - 問題 (依問題類型排序)

![電腦分析生產環境部署狀態的螢幕擷取畫面](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a> 監視已更新裝置的健全狀況

[準備生產]  頁面著重於協助您制定資產升級決策。 根據預設，該頁面僅顯示還不是 [就緒]  狀態的資產。 [監視器健全狀況]  頁面會顯示任何值得注意資產的健全狀況問題，即使這些資產標示為 [就緒]  。 如果發現問題，您可以針對問題進行疑難排解並加以修正，或將升級決策變更為 [無法]  。 當您變更升級決策時，此動作可防止日後在擁有該資產的裝置上升級。

依資產的下列健全狀態篩選此頁面：

| 健全狀態篩選 | 說明 |
|----------------------|-------------|
| **需要注意** | (預設篩選條件) 電腦分析偵測到該資產某些健全狀況計量在統計資料方面有顯著迴歸
| **達成目標** | 電腦分析未偵測到行為的迴歸 |
| **資料不足** | 電腦分析有關此資產的資料不足，無法提出任何建議 |
| **無資料** | 此資產尚無任何使用量資料 |

若要顯示所有資產未經篩選的檢視，請選取目前的篩選條件。 此動作會移除該篩選條件。

> [!NOTE]  
> 為減少資料不足的資產數目，電腦分析會監視已升級為部署計劃所指定目標 Windows 版本的所有裝置上資產。 這些裝置包括特定部署計劃未包含的裝置。  

預設的排序次序是依擁有該特定資產事件的裝置數目排列，以便您可以快速查看造成最多問題的裝置。 例如，檢視 [應用程式]  時，它會依**過去兩周內發生應用程式損毀的裝置**來排序。

如果想要查看所有資產的健全狀況，甚至是資料不足以供電腦分析進行統計推斷的資產，請使用下列程序：

1. 選取 [Devices with incidents in last two weeks] \(過去兩週內發生事件的裝置\)  一欄的下拉式箭頭。 僅將篩選條件新增至曾在少數裝置上發生過有趣事件的資產。 例如，顯示值**大於** 100 的項目。  

2. 選取 [% Devices with incidents in the last two weeks] \(過去兩週內發生事件的裝置百分比\)  一欄的下拉式箭頭，並選取依 [遞減]  排序。  

    所產生檢視會顯示事件數最少但事件發生率最高的資產。  

3. 選取某項資產以取得詳細資料，或變更其升級決策。  

如需詳細資訊，請參閱[健全狀態監視](health-status-monitoring.md)。
