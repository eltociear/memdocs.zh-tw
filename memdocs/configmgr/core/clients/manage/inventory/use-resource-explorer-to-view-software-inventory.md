---
title: 使用資源總管檢視軟體清查
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用資源總管檢視軟體清查。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690066"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>如何在 Configuration Manager 中使用資源總管檢視軟體清查

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中使用資源總管，檢視從階層中電腦所收集的軟體清查相關資訊。  

> [!NOTE]  
>  資源總管會等待軟體清查週期在用戶端上執行之後，才會顯示所有的清查資料。  

 資源總管提供下列軟體清查資訊：  

-   **軟體**：  

    -   **收集到的檔案** - 在軟體清查期間收集到的檔案。  

    -   **檔案詳細資料** - 在軟體清查期間清查到與特定產品或製造商無關聯的檔案。  

    -   **上次軟體掃描** - 用戶端電腦上次執行軟體清查和檔案收集的日期和時間。  

    -   **產品詳細資料** - 軟體清查所清查且依製造商分組的軟體產品。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台執行資源總管  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] 

2.  在 [資產與合規性]  工作區中，選擇 [裝置]  或開啟顯示裝置的任何集合。  

3.  選擇您想要檢視、包含清查的電腦，然後在 [首頁]  索引標籤 > [裝置]  群組中，選擇 [開始]   >   資源總管。

4.  您可以在資源總管視窗的右窗格中，以滑鼠右鍵按一下任何項目，然後選擇 [內容]  以更容易閱讀的格式檢視收集到的清查資訊。  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> 檢視及管理收集到的診斷檔案

從 Configuration Manager 版本 2002 開始，當使用用戶端通知來[收集用戶端記錄](../client-notification.md#client-diagnostics)時，請使用 [資源總管] 來檢視及管理所收集的檔案。 

1. 從 [裝置]  節點中，以滑鼠右鍵按一下要檢視其記錄的裝置。
1. 選取 [開始]  ，然後選取 [資源總管]  。
1. 從 [資源總管]  中，按一下 [診斷檔案]  。
1. 在 [診斷檔案]  清單中，您可以看到檔案的收集日期。 用戶端記錄的名稱格式為 `Support_<guid>.zip`。
1. 以滑鼠右鍵按一下 ZIP 檔案，然後選取下列其中一個選項：
    - [開啟支援中心]  ：啟動[支援中心](../../../support/support-center.md)。
    - **複製**：從 [資源總管] 複製資料列資訊。
    - [檢視檔案]  ：使用檔案總管開啟 ZIP 檔案所在的資料夾。
    - [儲存]  ：針對選取的檔案開啟 [儲存檔案] 對話方塊。
    - [匯出]  ：儲存 [診斷檔案]  中顯示的 [資源總管] 資料行。
    - **重新整理**：重新整理檔案清單。
    - [內容]  ：傳回所選檔案的內容。 

[![檢閱並儲存 [資源總管] 的用戶端記錄](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>後續步驟

[使用支援中心](../../../support/support-center.md)以檢視收集到的診斷檔案。
