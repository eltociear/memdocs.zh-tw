---
title: 技術預覽版 1803
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 技術預覽版 1803 版中可用的新功能。
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701946"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Configuration Manager Technical Preview 1803 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager 技術預覽版 1803 版中可用的功能。 您可以安裝此版本，以將新功能更新並新增至您的技術預覽版網站。 

請先檢閱[技術預覽版](technical-preview.md)文章，再安裝此更新。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**以下是您可以使用此版本試用的新功能。**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>提取發佈點支援以雲端發佈點作為來源  
<!--1321554-->
許多客戶在遠端或分公司使用[提取發佈點](../plan-design/hierarchy/use-a-pull-distribution-point.md)，這會經由 WAN 從來源發佈點下載內容。 如果您的遠端辦公室有較佳的網際網路連線，或是若要降低 WAN 連結上的負載，現在可以使用 Microsoft Azure 中的[雲端發布點](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)作為來源。 當您在發佈點屬性的 [提取發佈點]  索引標籤上新增來源時，站台中所有雲端發佈點現在都會列為可用的發佈點。 除此之外，兩個站台系統角色的行為都保持不變。 

### <a name="prerequisites"></a>先決條件
- 提取發佈點必須能夠存取網際網路，才能與 Microsoft Azure 通訊。
- 內容必須發佈至來源雲端發佈點。

> [!Note]  
> 此功能會導致您的 Azure 訂用帳戶需要支付資料儲存和網路輸出的費用。 如需詳細資訊，請參閱[使用雲端式發佈的成本](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost)。



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>用戶端對等快取支援部分下載以降低 WAN 使用量
<!--1357346-->
用戶端對等快取來源現在可以將內容分割成組件。 這些組件會將網路傳輸減到最少以降低 WAN 使用量。 管理點可提供內容組件的更詳細追蹤。 它會嘗試排除對每一界限群組的相同內容進行多重下載的情況。 

### <a name="example-scenario"></a>範例案例
Contoso 具有一個單一主要站台，其中含有兩個界限群組：總部 (HQ) 和分公司。 界限群組之間有 30 分鐘的後援關聯性。 站台的管理點和發佈點只在 HQ 界限中。 分公司位置沒有任何本機發佈點。 分公司的四個用戶端中有兩個已設定為對等快取來源。 

![針對範例案例所述的網路設定圖](media/1357346-peer-cache-source-parts.png)

1. 您將內容相關部署的目標設定為分公司的全部四個用戶端。 您已只將內容發佈至發佈點。
2. Client3 和 Client4 沒有適用於部署的本機來源。 管理點會指示用戶端先等候 30 分鐘，再切換回遠端界限群組。
3. Client1 (PCS1) 是第一個向管理點重新整理原則的對等快取來源。 由於已啟用此用戶端作為對等快取來源，因此管理點會指示它立即從發佈點開始下載組件 A。  
4. 當 Client2 (PCS2) 連絡管理點時，由於組件 A 已經在進行中但尚未完成，因此管理點會指示它立即從發佈點開始下載組件 B。
5. PCS1 完成組件 A 的下載，並立即通知管理點。 由於組件 B 已經在進行中但尚未完成，因此管理點會指示它從發佈點開始下載組件 C。
6. PCS2 完成組件 B 的下載，並立即通知管理點。 管理點會指示它從發佈點開始下載組件 D。 
7. PCS1 完成組件 C 的下載，並立即通知管理點。 管理點會通知它遠端發佈點已無任何其他組件可供下載。 管理點會指示它從其本機對等 PCS2 下載組件 B。
8. 此程序會繼續執行，直到兩個用戶端對等快取來源都擁有對方的所有組件為止。 管理點會先排列遠端發佈點中組件的優先順序，再指示對等快取來源從本機對等下載組件。 
9. 在 30 分鐘後援期間到期後，第一個重新整理原則的是 Client3。 它現在會回頭向管理點確認，而管理點則會通知該用戶端有新的本機來源。 它會從其中一個用戶端對等快取來源下載全部內容，而不會經由 WAN 從發佈點下載全部內容。 用戶端會排列本機對等快取來源的優先順序。 

> [!Note]  
> 如果用戶端對等快取來源數目超出內容組件數目，管理點就會指示額外的對等快取來源像一般用戶端一樣等候後援。 


### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 像往常一樣設定[界限群組](../servers/deploy/configure/boundary-groups.md)和[對等快取來源](../plan-design/hierarchy/client-peer-cache.md)。
2. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  。 按一下功能區的 [階層設定]  。 
3. 在 [一般]  索引標籤上，啟用 [將用戶端對等快取來源設定為將內容分割成組件]  選項。 
4. 建立必要的內容相關部署。  

   > [!Note]  
   > 此功能只有當用戶端在背景下載內容時才有作用，例如進行必要部署時。 依需求進行的下載 (例如當使用者安裝「軟體中心」內的可用部署時) 則如常運作。  

1. 若要看看它們如何處理將內容分成多組件來下載的情況，請查看用戶端對等快取來源上的 **ContentTransferManager.log**，以及管理點上的 **MP_Location.log**。  
 



## <a name="maintenance-windows-in-software-center"></a>軟體中心內的維護時間範圍
<!--1358131-->
「軟體中心」現在會顯示下一個排定的維護時間範圍。 在 [安裝狀態] 索引標籤上，將檢視從 [全部] 切換成 [預定進行]。 它會顯示時間範圍和已排定的部署清單。 如果沒有任何未來的維護時間範圍，此清單就會空白。 

![在 [安裝狀態] 索引標籤上顯示預定進行部署清單的「軟體中心」](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>軟體中心內網頁的自訂索引標籤
<!--1358132-->
您現在可以建立自訂索引標籤以在「軟體中心」內開啟網頁。 此功能可讓您以一致且可靠的方式向使用者顯示內容。 以下清單包括幾個範例：
- 連絡 IT：有關如何連絡組織 IT 部門的資訊
- IT 支援中心：IT 自助動作，例如搜尋知識庫或開立支援票證。
- 使用者文件：適用於組織內使用者的各種 IT 主題 (例如使用應用程式或升級至 Windows 10) 相關文章。


### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 在 Configuration Manager 主控台 [系統管理]  工作區的 [用戶端設定]  節點中，開啟 [預設用戶端設定]  原則。
2. 選取 [軟體中心]  群組。
3. 針對 [軟體中心設定]  ，按一下 [自訂]  。
4. 切換至 [索引標籤]  索引標籤。
5. 啟用 [為軟體中心指定自訂索引標籤]  選項。
    1. 在 [索引標籤]  文字欄位中輸入名稱。 此名稱是在「軟體中心」內向使用者顯示的名稱。
    2. 在 [內容 URL]  文字欄位中輸入有效的 URL。 此 URL 是使用者按一下此索引標籤時「軟體中心」所顯示的內容。

> [!Tip]  
> 「軟體中心」會使用 Internet Explorer 元件來轉譯網頁。

## <a name="enable-third-party-software-update-support-on-clients"></a>啟用用戶端上的協力廠商軟體更新支援

您現在可以允許設定 Configuration Manager 來進行協力廠商軟體更新。 當您為 SUP 元件屬性**啟用協力廠商軟體更新**時，SUP 會下載 WSUS 用於協力廠商更新的簽署憑證。 <!--1357605-->

在用戶端設定中選取 [啟用協力廠商軟體更新]  會執行下列動作： 
- 在用戶端上，它會設定「允許內部網路 Microsoft 更新服務位置的已簽署更新」原則 
- 將簽署憑證安裝至用戶端上的 [受信任的發行者] 存放區。 

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 在 Configuration Manager 階層中的頂層站台上，移至 [系統管理]  節點，展開 [站台設定]  ，然後展開 [站台]  。
2. 在頂層站台伺服器上按一下滑鼠右鍵並選取 [設定站台元件]  ，然後選取 [軟體更新點]  。
3. 按一下 [協力廠商更新]  索引標籤，然後勾選 [啟用協力廠商軟體更新]  。
4. 開啟 [用戶端設定]  ，然後移至 [軟體更新]  的設定。
5. 確定將 [啟用協力廠商軟體更新]  設定為 [是]  。

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>允許從監視檢視進行複製/貼上資產詳細資料
由於使用者的 [User Voice 意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det)，您現在可以在部署和發佈狀態監視檢視的資產詳細資料窗格中，啟用複製/貼上功能。  <!--1357552-->

## <a name="scap-extensions"></a>SCAP 延伸模組
您可以從 [Cd.latest] 資料夾底下的 SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi 取得「SCAP 延伸模組」的發行前版本。 這個發行前版本的 SCAP 延伸模組可以安裝在任何目前支援的 Configuration Manager 最新分支版本和 LTSB 1606。



## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
