---
title: 使用維護時段
titleSuffix: Configuration Manager
description: 使用集合和維護時段，在 Configuration Manager 中有效率地管理用戶端。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695456"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>如何使用 Configuration Manager 中的維護時段

適用於：  Configuration Manager (最新分支)

維護時段可讓您定義何時可在裝置集合上執行 Configuration Manager 操作。 您可以藉助維護時段，確保用戶端設定變更發生的期間不會影響生產力。 從 Configuration Manager 1806 版開始，您的使用者可以從 [軟體中心]  的 [安裝狀態]  索引標籤查看下一個維護時段的時間。 <!--1358131-->

 下列操作支援維護時段：  

- 軟體部署  

- 軟體更新部署  

- 相容性設定部署和評估  

- 作業系統部署  

- 工作順序部署  

  請設定維護時段的開始日期、開始和完成時間，以及定期模式。 視窗的持續時間上限必須小於 24 小時。 根據預設，部署造成電腦重新啟動的行為不允許出現在維護時段之外，但是您可以覆寫預設值。 維護時段只會影響部署程式執行的時間，而設定在本機上下載及執行的應用程式可以在時段之外下載內容。  

  如果用戶端電腦是維護時段的裝置集合成員，則部署程式只會在允許的執行時間上限未超過針對時段設定的持續時間時執行。 如果程式執行失敗，將會產生警示，且部署將會在下一次排程的維護視窗有可用時間時重新執行。  

## <a name="using-multiple-maintenance-windows"></a>使用多個維護視窗  
 如果用戶端電腦是具有維護時段之多個裝置集合的成員，則適用下列規則：  

- 如果維護時段未重疊，則會視為兩個獨立的維護時段。  

- 如果維護時段重疊，則會視為包含兩個維護時段所涵蓋時段的單一維護時段。 例如，如果兩個視窗的持續時間各為一小時，其中有 30 分鐘重疊，則維護時段的有效持續時間會是 90 分鐘。  

  當使用者從軟體中心起始應用程式安裝時，應用程式將會立即安裝，而不理會任何維護時段。  

  如果在軟體中心使用者設定的非營業時間裡，有 **必要** 目的的應用程式部署面臨安裝期限，就會安裝應用程式。 

### <a name="how-to-configure-maintenance-windows"></a>如何設定維護視窗  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性]  >  [裝置集合]  。  

3.  在 [裝置集合]  清單中，選取一個集合。 您無法為 [所有系統]  集合建立維護時段。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

5.  在 [&lt;集合名稱\> 內容]  對話方塊的 [維護時段]  索引標籤中，選擇新增  圖示。  

6.  完成 [&lt;新增\> 排程]  對話方塊。  

7.  從 [將此排程套用至]  下拉式清單中進行選取。  

8.  選擇 [確定]  ，然後關閉 [&lt;集合名稱\> 內容]  對話方塊。  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> 使用 PowerShell

PowerShell 可用來設定維護期間。  如需詳細資訊，請參閱：

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow) \(英文\)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow) \(英文\)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow) \(英文\)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow) \(英文\)
