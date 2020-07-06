---
title: 電腦分析中的更新
titleSuffix: Configuration Manager
description: 了解電腦分析中的安全性和功能更新。
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590961"
---
# <a name="updates-in-desktop-analytics"></a>電腦分析中的更新

在電腦分析入口網站中，檢視安全性和功能更新的狀態。 在電腦分析主功能表的 [監視] 群組中，選取這些節點。 這些節點可讓您深入了解環境中這些更新的狀態。

<!--7362999-->

> [!IMPORTANT]
> 電腦分析會顯示裝置的安全性和功能更新狀態，以及與電腦分析工作區建立關聯的商業識別碼。 無論是否使用 Configuration Manager 註冊裝置，都會發生此行為。 這些磚上的裝置總數可能與[**已連線服務**](monitor-connection-health.md#commercial-id-configuration)中註冊裝置數目不符。

## <a name="security-updates"></a>安全性更新

若要檢閱安全性更新的目前狀態，請在電腦分析的 [監視] 區段中，選取 [安全性更新]：

![電腦分析的 [安全性更新] 節點](media/security-updates.png)

此檢視摘要說明執行 Windows 10 的裝置「安全性」更新。 橫條圖中的裝置依下列標籤分類：

#### <a name="latest"></a>最新

裝置正在執行該版本和通道的最新安全性更新。

#### <a name="latest-1"></a>最新-1

裝置所正在執行安全性更新版本比該通道上最新的可用更新舊一個版本。

#### <a name="older"></a>較舊

裝置正在執行的安全性更新版本比「最新-1」的版本舊。

#### <a name="not-measured"></a>未經測量

電腦分析未評定過此裝置。 此狀態包括執行 Windows 7、Windows 8.1 的裝置，或針對 Windows 測試人員計畫登錄的 Windows 10 裝置。  

若要查看安全性更新的採用趨勢，請選取特定 Windows 版本的 [檢視其他]。 堆疊區域圖會根據其在一段時間內安裝的安全性更新來分類裝置。

若要檢閱安全性更新的部署狀態，請選取 [查看全部]。 此檢視會列出下列類別的裝置：

- 未開始
- 進行中
- Completed
- 需要注意 - 裝置 (依裝置名稱排序)
- 需要注意 - 問題 (依問題類型排序)

若要顯示服務仍在處理新資訊的裝置，請選取 [檢視最近的資料]。 在下一次完整資料重新整理後，電腦分析會顯示此資訊。

  > [!IMPORTANT]
  > **檢視最近的資料**的 [電腦分析] 選項已被取代。 此動作將在未來的 [電腦分析] 服務版本中移除。 如需詳細資訊，請參閱[已淘汰的功能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。<!--7080949-->  

## <a name="feature-updates"></a>功能更新

若要檢閱功能更新的目前狀態，請在電腦分析的 [監視] 區段中，選取 [功能更新]：

![電腦分析的 [功能更新] 節點](media/feature-updates.png)

此檢視摘要說明正在執行 Windows 10 的裝置「功能」更新。

如需服務期間的詳細資訊，請參閱 [Windows 生命週期資料表](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。  

橫條圖中的裝置依下列標籤分類：

#### <a name="in-service"></a>服務中

裝置正在執行該版本和通道的最新功能更新。  

#### <a name="near-end-of-service"></a>服務即將到期

裝置正在執行的功能更新服務即將於 90 天內到期。

#### <a name="end-of-service"></a>服務到期

裝置正在執行的功能更新已超過服務結束日期。 這些日期特定於企業版和教育版 Windows。 其不適用於家用版、專業版、專業教育版或工作站專業版。 如需詳細資訊，請參閱 [Windows 生命週期資料表](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

#### <a name="not-measured"></a>未經測量

電腦分析未評定過此裝置。 此狀態包括執行 Windows 7、Windows 8.1 的裝置，或針對 Windows 測試人員計畫登錄的 Windows 10 裝置。

選取磚來查看功能更新的採用趨勢。 堆疊區域圖會根據其在一段時間內安裝的功能更新來分類裝置。

## <a name="next-steps"></a>後續步驟

- [了解電腦分析資產](about-assets.md)：裝置、驅動程式和應用程式  

- [了解部署計劃](about-deployment-plans.md)  
