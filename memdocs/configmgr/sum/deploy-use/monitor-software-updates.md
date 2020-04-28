---
title: 監視軟體更新
titleSuffix: Configuration Manager
description: Configuration Manager 主控台提供警示與狀態，以監視更新及合規性。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110367"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>在 Configuration Manager 中監視軟體更新

適用於：  Configuration Manager (最新分支)

Configuration Manager 提供多種方式協助您監視軟體更新物件、程序和合規性資訊。 您可以使用下列各區段來監視軟體更新。

## <a name="software-updates-dashboard"></a>軟體更新儀表板

(於 1610 版引進) 

從 Configuration Manager 1610 版開始，您可以使用軟體更新儀表板檢視貴組織裝置目前的合規性狀態，並快速分析資料查看哪些裝置有風險。 若要檢視儀表板，請瀏覽至 [監視]   > [概觀]   > [安全性]   > 「Software Updates Dashboard」 (軟體更新儀表板)  。

## <a name="drill-through-required-updates"></a>鑽研需要的更新
<!--4224414-->
*(於 1906 版推出)*

您可以鑽研合規性統計資料，以了解哪些裝置需要特定的 Microsoft 365 Apps 軟體更新。 若要檢視裝置清單，您需要檢視更新及裝置所屬集合的權限。 向下切入至裝置清單：

1. 前往 [軟體程式庫]   > [軟體更新]   > [所有軟體更新]  。
1. 選取至少一部裝置所需的任何更新。
1. 查看 [摘要]  索引標籤，然後尋找 [統計資料]  下方的圓形圖。
1. 選取圓形圖旁的 [需要檢視]  超連結，以向下切入至裝置清單。
1. 此動作會帶您前往 [裝置]  下方的臨時節點，以查看需要更新的裝置。 您也可以對節點採取動作，例如從清單建立新的集合。


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> 軟體更新的警示  
 您可以設定軟體更新的警示，在軟體更新部署的合規性層級低於設定的百分比時通知系統管理使用者。 您可以在下列位置設定軟體更新部署的警示：  

-   ADR 設定：您可以在 [自動部署規則精靈] 和 ADR 內容中設定警示設定。  

-   部署設定：您可以在 [部署軟體更新精靈] 和部署內容中設定警示設定。  

進行警示設定後，如果指定的條件發生，Configuration Manager 就會產生警示。 您可以在下列位置檢閱軟體更新警示：  

1.  在 [軟體程式庫]  工作區的 [軟體更新]  節點中檢閱最近的警示。  

2.  在 [監視]  工作區的 [警示]  節點中管理設定的警示。  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a> 軟體更新同步處理狀態  
 啟動同步處理程序後，您可以從 Configuration Manager 主控台監視階層中所有軟體更新點的同步處理程序。 利用下列程序監視軟體更新同步處理程序。  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>若要監視軟體更新同步處理程序  

- 在 Configuration Manager 主控台中，瀏覽至 [監視]   > [概觀]   > [軟體更新點同步處理狀態]  。  

    Configuration Manager 階層中的軟體更新點會顯示在結果窗格中。 從此檢視中，您可以監視所有軟體更新點的同步處理狀態。 若要查看同步處理程序的詳細資訊，您可以檢閱 wsyncmgr.log 檔案，該檔案位於各站台伺服器的 <Configuration Manager 安裝路徑  >\Logs 中。  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> 軟體更新部署狀態  
 您在軟體更新群組中部署軟體更新或部署個別軟體更新後，可以監視部署狀態。 利用下列程序監視軟體更新群組或軟體更新的部署狀態。  

#### <a name="to-monitor-deployment-status"></a>若要監視部署狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視]   > [概觀]   > [部署]  。  

2.  按一下您要監視其部署狀態的軟體更新群組或軟體更新。  

3.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態]  。  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> 軟體更新報告  
 軟體更新的狀態訊息會提供有關軟體更新合規性，以及有關軟體更新部署的評估和強制執行狀態的資訊。 您可以執行軟體更新報告顯示這些狀態訊息。 有超過 30 種預先定義的軟體更新報告可供您使用。 這些報告分成數種類別，可以用來報告有關軟體更新和部署的特定資訊。 除了使用預先設定的報告之外，您也可以根據企業需要建立自訂軟體更新報告。 如需詳細資訊，請參閱[報告作業和維護](../../core/servers/manage/operations-and-maintenance-for-reporting.md)。  

### <a name="recommended-software-updates-reports"></a>建議的軟體更新報告
以下是有助於識別可能問題的一些報告： 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>合規性 9 - 整體健全狀況與合規性 (從 1806 版開始)
此報告包含下列部分：

- **狀況良好的用戶端與用戶端總計**：這個橫條圖會比較已在指定期間與站台通訊的「狀況良好」用戶端，以及指定集合中的用戶端總數。
- **合規性概觀**：這個圓形圖顯示在指定的集合內，有效用戶端上特定軟體更新群組的整體合規性狀態。
- **依發行項識別碼顯示前 5 個不符合規範的項目**：這個橫條圖會針對指定集合內有效用戶端上不符合規範者，顯示指定群組中的前五名軟體更新。
- 報告底部有一個含進一步詳細資料的表格，其中列出指定群組中的軟體更新。

#### <a name="management-2---updates-required-but-not-deployed"></a>管理 2 - 必要但尚未部署的更新

此報告顯示特定更新分類中的廠商特定軟體更新，這些更新已被偵測為用戶端必需的，但尚未部署到特定集合。 

#### <a name="troubleshooting-2---deployment-errors"></a>疑難排解 2 - 部署錯誤

此報告會傳回站台上的部署錯誤，以及發生每個錯誤的電腦計數。 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> 監視內容  
 您可以在 Configuration Manager 主控台中監視內容，檢閱與關聯發佈點相關之所有套件類型的狀態。 包括套件中內容的內容驗證狀態、指派至特定發佈點群組的內容狀態、指派至發佈點的內容狀態，以及每個發佈點的選用功能狀態 (內容驗證、PXE 和多點傳送)。  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> 內容狀態監視  
 [監視]  工作區中的 [內容狀態]  節點會提供有關內容套件的資訊。 您可以檢閱有關套件的一般資訊、套件的發佈狀態，以及有關套件的詳細狀態資訊。 利用下列程序可檢視內容狀態。  

#### <a name="to-monitor-content-status"></a>若要監視內容狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視]   > [概觀]   > [發佈狀態]   > [內容狀態]  。 套件便會顯示。  

2.  選取要檢視其詳細狀態資訊的套件。  

3.  在 [首頁]  索引標籤上，按一下 [檢視狀態]  。 套件的詳細狀態資訊隨即顯示。  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> 發佈點群組狀態  
 [監視]  工作區中的 [發佈點群組狀態]  節點會提供有關發佈點群組的資訊。 您可以檢閱有關發佈點群組的一般資訊，例如發佈點群組狀態和相容性比率，以及發佈點群組的詳細狀態資訊。 利用下列程序可檢視發佈點群組狀態。  

#### <a name="to-monitor-distribution-point-group-status"></a>若要監視發佈點群組狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視]   > [概觀]   > [發佈狀態]   > [發佈點群組狀態]  。 發佈點群組隨即顯示。  

2.  選取要檢視其詳細狀態資訊的發佈點群組。  

3.  在 [首頁]  索引標籤上，按一下 [檢視狀態]  。 發佈點群組的詳細狀態資訊隨即顯示。  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> 發佈點組態狀態  
 [監視]  工作區中的 [發佈點設定狀態]  節點會提供有關發佈點的資訊。 您可以檢閱已啟用的發佈點屬性，例如 PXE、多點傳送及內容驗證。 您也可以檢視發佈點的詳細狀態資訊。 利用下列程序可檢視發佈點設定狀態。  

#### <a name="to-monitor-distribution-point-configuration-status"></a>若要監視發佈點設定狀態  

1.  在 Configuration Manager 主控台中，瀏覽至 [監視]   > [概觀]   > [發佈狀態]   > [發佈點設定狀態]  。 發佈點隨即顯示。  

2.  選取要檢視其發佈點狀態資訊的發佈點。  

3.  在結果窗格中，按一下 [詳細資料]  索引標籤。發佈點的狀態資訊隨即顯示。  

## <a name="next-steps"></a>後續步驟

- [軟體更新的記錄檔](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [軟體更新管理白皮書](https://www.microsoft.com/download/confirmation.aspx?id=44578) \(英文\)
