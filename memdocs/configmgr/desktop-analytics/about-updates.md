---
title: 電腦分析中的更新
titleSuffix: Configuration Manager
description: 了解電腦分析中的安全性和功能更新。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec510414f11aa312e6c1a7d1d5bfa8126f473fe3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706576"
---
# <a name="updates-in-desktop-analytics"></a>電腦分析中的更新

在電腦分析入口網站中，檢視安全性和功能更新的狀態。 在電腦分析主功能表的 [監視] 群組中，選取這些節點。 這些節點可讓您深入了解環境中這些更新的狀態。


## <a name="security-updates"></a>安全性更新

若要檢閱安全性更新的目前狀態，請在電腦分析的 [監視]  區段中，選取 [安全性更新]  ：

![電腦分析的 [安全性更新] 節點](media/security-updates.png)

此檢視摘要說明執行 Windows 10 的裝置「安全性」  更新。 橫條圖中的裝置依下列標籤分類：

#### <a name="latest"></a>最新

裝置正在執行該版本和通道的最新安全性更新。

#### <a name="latest-1"></a>最新-1

裝置所正在執行安全性更新版本比該通道上最新的可用更新舊一個版本。

#### <a name="older"></a>較舊

裝置正在執行的安全性更新版本比「最新-1」的版本舊。

#### <a name="not-measured"></a>未經測量

電腦分析未評定過此裝置。 此狀態包括執行 Windows 7、Windows 8.1 的裝置，或針對 Windows 測試人員計畫登錄的 Windows 10 裝置。  

Windows 不會報告「不使用 Microsoft 帳戶驗證」  的 Windows 10 裝置資料。 這項驗證通常會在 Windows 安裝程式全新體驗 (OOBE) 中完成。<!-- 5148153 -->


## <a name="feature-updates"></a>功能更新

若要檢閱功能更新的目前狀態，請在電腦分析的 [監視]  區段中，選取 [功能更新]  ：

![電腦分析的 [功能更新] 節點](media/feature-updates.png)

此檢視摘要說明正在執行 Windows 10 的裝置「功能」  更新。

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

Windows 不會報告「不使用 Microsoft 帳戶驗證」  的 Windows 10 裝置資料。 這項驗證通常會在 Windows 安裝程式全新體驗 (OOBE) 中完成。<!-- 5148153 -->


## <a name="next-steps"></a>後續步驟

- [了解電腦分析資產](about-assets.md)：裝置、驅動程式和應用程式  

- [了解部署計劃](about-deployment-plans.md)  
