---
title: DP 作業佇列管理員
titleSuffix: Configuration Manager
description: 使用 DP 作業佇列管理員，針對 Configuration Manager 發佈點的內容發佈作業進行疑難排解和管理。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694336"
---
# <a name="dp-job-queue-manager"></a>DP 作業佇列管理員

適用於：  Configuration Manager (最新分支)

發佈點 (DP) 作業佇列管理員是其中一個 [Configuration Manager 工具](tools.md)。 使用它，針對 Configuration Manager 發佈點的進行中內容發佈作業進行疑難排解和管理。 

此工具會顯示套件傳輸管理員元件在其佇列中所具有的作業清單。 它也會顯示作業的狀態：準備好執行、執行中或重試中。 它可讓您操縱佇列中的工作、將作業移至清單中較高的位置、取消作業，或手動開始執行作業。

它也會從發佈點執行作業所在的站台伺服器取得資訊。 此工具會透過提供者連線至站台伺服器。 它不會連線至每個遠端發佈點來收集此資訊。 因為它會觸發動作，並透過提供者取得資訊，所以反映來自遠端發佈點的變更會有一些延遲。



## <a name="usage"></a>使用方式

執行 **DPJobMgr.exe**。 此工具的主功能表包含下列索引標籤： 

- [連線](#bkmk_connect)：建立與主要站台伺服器的初始連線  

- [概觀](#bkmk_overview)：以單一檢視摘要在所有發佈點上執行的所有作業  

- [發佈點資訊](#bkmk_dp-info)：複選發佈點來追蹤發佈點，並管理相關的單一作業  

- [管理作業](#bkmk_manage-jobs)：以一個一般檢視顯示所有作業和其狀態的清單。 操縱作業、將它們往上移動、取消或手動開始。  


### <a name="connect-tab"></a><a name="bkmk_connect"></a> 連線索引標籤

使用此索引標籤，建立與主要站台伺服器的初始連線。 它會使用目前登入的使用者認證。 您無法連線至管理中心網站或次要站台。 連線需要**系統高權限管理員**安全性角色。

此工具在成功建立連線之後，其底部的通知會確認已連線至站台伺服器。 


### <a name="overview-tab"></a><a name="bkmk_overview"></a> 概觀索引標籤

顯示所有發佈點上所有作業的摘要。 請參閱下列資料行：  

- **發佈點**：列出發佈點的名稱  

- **執行中的作業**：顯示正在特定發佈點上執行的並行作業數目。  

    > [!Tip]  
    > 並行軟體發佈數目是站台設定。 已在 [軟體發佈元件內容] 中修改此設定。  

- **作業總數**：顯示以特定發佈點為目標的所有作業數目。 此數目包含執行中、重試中或等候執行的作業。  

- **重試總數**：顯示已在特定發佈點上重試作業的次數。 較高的數目可能代表該特定發佈點的一般問題。  


> [!Tip]  
> - 若要排序此索引標籤中的每個資料行，請按一下資料行名稱  
> 
> - 按一下 [重新整理]  ，以手動重新整理此索引標籤中的資訊  
> 
> - 按一下 [Start Auto Refresh] \(開始自動重新整理\)  ，並設定自動重新整理間隔，以自動重新整理此索引標籤中的資訊。 預設重新整理間隔為兩分鐘。  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a> [Distribution Point Info] \(發佈點資訊\) 索引標籤

顯示已連線站台下的所有發佈點清單。 左側窗格會列出所有發佈點。 視需要按一下 [全選]  或 [全部取消選取]  ，或複選此清單中的特定發佈點。 右側窗格會顯示所選取發佈點的作業。

有八個資料行：  

- **狀態圖示**：有三種可能的狀態圖示：  

    - **就緒**：指出特定作業已完成所有驗證步驟。 它已準備好新增至執行中並行作業。 處於此狀態的作業通常處於等候階段。 它們會等待目前執行中處理序完成，才開啟其空間。  

    - **執行中**：指出特定作業目前正在發佈點上執行。 針對長期執行作業 (大型套件)，通常會有時間取得完成的進度 (%)。 它會將此百分比顯示在此檢視的 [進度]  資料行中。 針對小型的套件，[進度]  資料行可能會保持空白。 從遠端發佈點接收狀態之前可能已完成作業。  

    - **重試**：指出特定作業已失敗，且目前處於重試狀態。 在重試間隔之後會重試此作業。 此間隔是可設定的，並且預設為 30 分鐘。  

- **軟體**：以特定發佈點為目標的套件名稱  

- **套件識別碼**：以特定發佈點為目標之套件的套件識別碼  

- **大小**：套件的大小 (KB)  

- **進度**：作業完成百分比。 如需詳細資訊，請參閱**執行中**狀態圖示描述。  

- **開始/重新啟動時間**：針對執行中作業，此值是開始時間 (綠色)。 針對重試作業，此值是重試該作業的時間。  

- **重試次數**：它已重試此套件的次數。  

- **發佈點名稱**：發佈點的完整網域名稱 (FQDN)  

> [!Tip]  
> - 若要排序此索引標籤中的每個資料行，請按一下資料行名稱  
> 
> - 按一下 [重新整理]  ，以手動重新整理此索引標籤中的資訊  
> 
> - 按一下 [Start Auto Refresh] \(開始自動重新整理\)  ，並設定自動重新整理間隔，以自動重新整理此索引標籤中的資訊。 預設重新整理間隔為兩分鐘。  
> 
> - 如果您需要修改特定作業，請以滑鼠右鍵按一下此檢視中的該作業，然後選取 [管理作業]  。 此動作會開啟[管理作業索引標籤](#bkmk_manage-jobs)。  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a> 管理作業索引標籤

以一個一般檢視顯示所有作業和其狀態的清單。 它包含的八個資料行與 [Distribution Point Info (發佈點資訊) 索引標籤](#bkmk_dp-info)相同。在此檢視中，以滑鼠右鍵按一下作業來執行下列動作：  

- **執行**：啟動處於任何狀態的作業 (但執行中除外)  

- **移至頂端**：將一或多個作業移至佇列頂端。 此動作可能會導致立即執行作業。 較低優先順序的作業可能會因此動作而暫停。  

- **上移**：將特定作業往上移動一列。 較低優先順序的作業可能會因此動作而暫停執行。  

- **下移**：將特定作業往下移動一列。  

- **移至底部**：將一或多個作業移至佇列底部。  

    > [!Tip]  
    > 拖放清單中的作業，以移動作業。  

- **取消**：嘗試取消一或多個作業。  

    > [!Note]  
    > 您無法取消接近其最終完成時間的作業。 如果站台伺服器也是發佈點，則您無法取消站台伺服器上的作業。  



## <a name="see-also"></a>請參閱

- [內容管理的基本概念](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [套件傳輸管理員](../plan-design/hierarchy/package-transfer-manager.md)
