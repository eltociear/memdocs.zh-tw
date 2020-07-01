---
title: 安裝 Power BI 範例報表
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中安裝 Power BI 範例報表
ms.date: 06/25/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39bec7e8b01b35a8411400399a74eb352406c023
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383184"
---
# <a name="install-power-bi-sample-reports"></a>安裝 Power BI 範例報表
<!--5679791-->
適用於：Configuration Manager (最新分支)

從 2002 版開始，可整合 [Power BI 報表伺服器](https://docs.microsoft.com/power-bi/report-server/get-started)與 Configuration Manager 報告。 有範例報表可供您下載並安裝在 Configuration Manager 中。 此文章說明如何在 Configuration Manager 中安裝 Power BI 範例報表。

## <a name="prerequisites"></a>先決條件

- [已整合 Power BI 報表伺服器](powerbi-report-server.md)的 Configuration Manager Reporting Services 點
- [Microsoft Power BI Desktop (針對 Power BI 報表伺服器最佳化 - 2019 年 9 月)](https://www.microsoft.com/download/details.aspx?id=57271) 或更新版本

    > [!IMPORTANT]
    > - 請只使用 [Microsoft 下載中心](https://www.microsoft.com/download/)提供的 Power BI Desktop 版本，請勿使用 Microsoft Store 提供的版本。
    > - 請只使用[標示**針對 Power BI 報表伺服器最佳化**的 Power BI Desktop 版本](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop)。

## <a name="download-the-sample-reports"></a>下載範例報表

> [!IMPORTANT]
> 目前無法下載範例報表。 已暫時將其移除，以修正已回報的問題。

下載範例報表：

1. 下載 Power BI 範例報表<!-- from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452)-->。
1. 儲存 `ConfigMgrSamplePowerBIReports.exe` 檔案。 
1. 如果您從不同的裝置下載該檔案，請將其移至已安裝 Microsoft Power BI Desktop (針對 Power BI 報表伺服器最佳化) 的電腦。
1. 執行 `ConfigMgrSamplePowerBIReports.exe` 檔案以將 .pbit 檔案解壓縮。

## <a name="install-the-sample-reports"></a>安裝範例報表

安裝範例報表：

1. 在 Power BI 報表伺服器上，於 Configuration Manager 報表資料夾的根資料夾中，建立名為 `Sample Reports` 的新資料夾。
   
   :::image type="content" source="media/create-sample-reports-folder.png" alt-text="在 Configuration Manager 報告資根料夾中，建立 [Sample Report ] 資料夾" lightbox="media/create-sample-reports-folder.png":::


1. 啟動 Microsoft Power BI Desktop (針對 Power BI 報表伺服器最佳化)。
1. 依序選取 [檔案]、[開啟]，然後瀏覽至您儲存所解壓縮 .pbit 檔案的位置。
1. 選取您從 `ConfigMgrSamplePowerBIReports.exe` 檔案解壓縮的其中一個 .pbit 檔案。
1. 出現提示時，指定您的 Configuration Manager 資料庫名稱與資料庫伺服器名稱，然後選取 [載入]。
   - 如果您在載入或套用資料模型時遇到任何錯誤，請予以略過。
   
    :::image type="content" source="media/sample-report-database.png" alt-text="指定資料庫與資料庫伺服器名稱" lightbox="media/sample-report-database.png":::

1. 當報表資料已載入時，請選取 [檔案] > [另存新檔]，然後選取 [Power BI 報表伺服器]。
   
   :::image type="content" source="media/save-powerbi-report-server.png" alt-text="另存為 Power BI 報表伺服器" lightbox="media/save-powerbi-report-server.png":::

1. 將報表儲存到您在報告點上建立的 `Sample Reports` 資料夾。
     
   :::image type="content" source="media/save-sample-report.png" alt-text="儲存至 [Sample Reports] 資料夾" lightbox="media/save-sample-report.png":::

1. 針對任何其他範例報表重複該步驟。 當您完成時，請關閉 Microsoft Power BI Desktop (針對 Power BI 報表伺服器最佳化)。
1. 在 Configuration Manager 主控台中，移至 [監視] > [Power BI 報表] > [Sample Reports]。
1. 以滑鼠右鍵按一下其中一個報表，然後選取 [在瀏覽器中執行] 來啟動報表。

   :::image type="content" source="media/view-powerbi-report.png" alt-text="從 Configuration Manager 主控台執行範例報表" lightbox="media/view-powerbi-report.png":::

## <a name="next-steps"></a>後續步驟

[與 Power BI 報表伺服器整合](powerbi-report-server.md)
