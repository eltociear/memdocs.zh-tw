---
title: 使用維護時段
titleSuffix: Configuration Manager
description: 使用集合和維護時段，在 Configuration Manager 中有效率地管理用戶端。
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428538"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>如何使用 Configuration Manager 中的維護時段

適用於：Configuration Manager (最新分支)

使用維護時段來定義 Configuration Manager 何時可以在裝置上執行會造成影響的工作。 維護時段有助於確保用戶端設定變更在不影響生產力的時間內進行。 透過 [軟體中心]，使用者可以在 [安裝狀態] 索引標籤上看到裝置的下一個維護時段。 <!--1358131-->

下列工作支援維護時段：

- 應用程式與套件部署

- 軟體更新部署

- 相容性設定部署和評估

- OS 與自訂工作順序部署

使用有效日期、開始時間與結束時間，以及週期模式來設定維護時段。 視窗的持續時間上限必須小於 24 小時。 主控台不允許超過 24 小時的單一維護時段。 例如，如果您想要允許星期六與星期日全天進行維護，則針對每一天建立兩個 24 小時的維護時段。<!-- MEMDocs#310 -->

根據預設，部署造成電腦重新啟動的行為不允許出現在維護時段之外，但是您可以覆寫預設值。 維護時段只會影響部署執行的時間。 您設定要在本機下載並執行的部署，可以在時段外下載內容。

如果用戶端電腦是維護時段的裝置集合成員，只有在其允許的執行時間上限未超過時段持續時間的情況下，部署才會執行。 如果部署無法執行，用戶端會產生警示。 然後，其會在下一個排定的維護時段內重新執行部署。

## <a name="multiple-maintenance-windows"></a>多個維護時段

如果用戶端電腦是具有維護時段之多個裝置集合的成員，則適用下列規則：  

- 如果維護時段未重疊，用戶端會將其視為兩個獨立的維護時段。

- 如果維護時段重疊，則用戶端會在兩個時段的整個時間內將其視為一個時段。 例如，您在集合上建立兩個維護時段。 第一個是從 6:00 到 7:00，第二個則是從 6:30 到 7:30 生效。 由於其重疊 30 分鐘，因此合併維護時段的有效持續時間為 90 分鐘，從 6:00 到 7:30。

當使用者從 [軟體中心] 安裝應用程式時，用戶端會立即加以啟動。 其會優先處理使用者對管理員的意圖。

在軟體中心中，如果在使用者設定的非上班時間裡有 [必要] 目的的應用程式部署達到安裝期限，用戶端就會安裝應用程式。 其會優先處理使用者的管理員意圖。

根據預設，有多個維護時段，用戶端只會在 [軟體更新] 類型時段期間安裝軟體更新。 除非是唯一的類型，否則會忽略 [所有部署] 的維護時段。 您可以使用**軟體更新**群組中的下列用戶端設定來設定此行為：**當 [軟體更新] 維護視窗可以使用時，允許安裝 [所有部署] 維護視窗中的軟體更新**。 如需詳細資訊，請參閱[關於用戶端設定](../../deploy/about-client-settings.md#bkmk_SUMMaint)。<!-- SCCMDocs#1317 -->

> [!NOTE]
> 此設定也適用於您設定以套用至**工作順序**的維護時段。<!-- SCCMDocs-pr #4596 -->
>
> 如果用戶端只有 [所有部署] 時段可用，其仍會在該時段安裝軟體更新或工作順序。

## <a name="configure-maintenance-windows"></a>設定維護時段

1. 在 Configuration Manager 主控台中，移至 [資產與合規性] 工作區。

1. 選取 [裝置集合] 節點，然後選取一個集合。

    > [!NOTE]
    > 您無法為 [所有系統] 集合建立維護時段。

1. 在功能區 [常用] 索引標籤的 [內容] 群組中，選擇 [內容]。

1. 切換至 [維護時段] 索引標籤，然後選取 [新增] 圖示。

    1. 指定 [名稱] 以唯一識別此集合的維護時段。

    1. 設定 [時間] 設定：

        - **生效日期**：維護時段的開始日期。 預設值是目前的日期。

        - **開始**與**結束**：維護時段的開始與結束時間。 其會計算時段的**持續時間**。 最短持續時間為五分鐘，最大值為 24 小時。 預設持續時間是三小時，從 01:00 到 04:00。

        - **國際標準時間 (UTC)** ：啟用此選項可讓用戶端以 UTC 時區來解譯開始與結束時間。 針對相同集合中的區域或全域散發裝置，此選項會將維護時段設定為在集合中的所有裝置上同時執行。 請停用此選項，讓用戶端使用裝置的本地時區。 預設會停用這個選項。

    1. 設定週期模式。 預設值是一週的目前日期每週一次。

    1. **將此排程套用至**：根據預設，此時段適用於**所有部署**。 您可以選取 [軟體更新] 或 [工作順序]，進一步控制在此時段中執行的部署。

        > [!TIP]
        > 如果您在相同的集合上設定多個不同類型的維護時段，請確定您了解用戶端行為。 如需詳細資訊，請參閱[多個維護時段](#multiple-maintenance-windows)。

1. 選取 [確定] 以儲存並關閉時段。

集合屬性的 [維護時段] 索引標籤會顯示所有已設定的時段。

## <a name="use-powershell"></a><a name="bkmk_powershell"></a> 使用 PowerShell

PowerShell 可用來設定維護期間。 如需詳細資訊，請參閱下列文章：

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps) \(英文\)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps) \(英文\)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps) \(英文\)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps) \(英文\)
