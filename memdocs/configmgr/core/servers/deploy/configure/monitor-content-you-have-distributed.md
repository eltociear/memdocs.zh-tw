---
title: 監視內容
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 主控台了解如何監視發佈的內容。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31edf096c57b726c3723d261db7a3103fcc311f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701126"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>監視您使用 Configuration Manager 發佈的內容

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager 主控台監視發佈的內容，包括：  

- 相關聯發佈點之所有套件類型的狀態。  
- 套件中內容的內容驗證狀態。  
- 指派至特定發佈點群組的內容狀態。  
- 指派至發佈點群組的內容狀態。  
- 每個發佈點 (內容驗證、PXE 與多點傳送) 的選用功能狀態。  

> [!NOTE]  
> Configuration Manager 僅監視位於內容庫中之發佈點上的內容。 它不會監視儲存在套件或自訂共用中發佈點上的內容。  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> 內容狀態監視

[監視]  工作區中的 [內容狀態]  節點會提供有關內容套件的資訊。 在 Configuration Manager 主控台中，檢閱下列這類資訊：  

- 套件名稱、類型和識別碼
- 已傳送至套件的發佈點數量
- 相容率
- 封裝建立的時間
- 來源版本

您也可以找到任何套件的詳細狀態資訊，包括：  

- 發佈狀態
- 失敗次數
- 擱置中的發佈  
- 安裝的數量

您也可以管理對發佈點持續進行的發佈，或是未能成功將內容發佈到發佈點的發佈：  

- 當您在 [資產詳細資料]  窗格中，檢視對發佈點之發佈作業的部署狀態訊息時，可使用取消或重新發佈內容等選項。 在 [進行中]  索引標籤或**內容狀態節點**的 [錯誤]  索引標籤中，可找到此窗格。  
- 此外，當您在 [進行中]  索引標籤上，檢視作業的詳細資料時，工作詳細資料會顯示已完成之作業的百分比。作業詳細資料也會顯示作業剩餘的重試次數。 當您在 [錯誤]  索引標籤上檢視作業的詳細資料時，會顯示下一次重試之前的時間。  

當您取消尚未完成的部署時，傳送該內容的發佈作業將會停止：  

- 接著會更新部署狀態，以指出該項發佈失敗，且使用者已採取動作將其取消。  
- 此新狀態會出現在 [錯誤]  索引標籤處。  

> [!NOTE]  
> 當部署作業接近完成時，取消該發佈的動作可能不會在完成發佈點的發佈作業之前進行。 萬一發生了，就會忽略取消部署的動作，而部署狀態會顯示為成功。  
>
> 雖然您可以選擇取消針對位於站台伺服器的發佈點進行發佈的選項，但這麼做是無效的。 此行為是因為站台伺服器和站台伺服器上的發佈點，共用相同的單一執行個體內容存放區。 沒有實際的發佈作業可取消。  

當您重新發佈之前失敗的內容以傳送到發佈點時，Configuration Manager 會立即開始將該內容再次部署到發佈點。 Configuration Manager 會更新部署，以反映該重新部署進行中狀態的狀態。  

### <a name="tasks-to-monitor-content"></a>監視內容的工作

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [發佈狀態]  ，然後選取 [內容狀態]  節點。 此節點會顯示套件。  

2. 選取您想要管理的套件。  

3. 在功能區 [常用]  索引標籤上的 [內容]  群組中，選取 [檢視狀態]  。 主控台會顯示套件的詳細狀態資訊。

如需其他動作，請繼續進行下列其中一節：

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>取消仍在進行中的發佈作業  

1. 切換至 [進行中]  索引標籤。

2. 在 [資產詳細資料]  窗格中，以滑鼠右鍵按一下要取消之發佈作業的項目，然後選取 [取消]  。  

3. 選取 [是]  以確認動作，並取消對於該發佈點的發佈作業。  

#### <a name="redistribute-content-that-failed-to-distribute"></a>重新發佈無法發佈的內容  

1. 切換至 [錯誤]  索引標籤。

2. 在 [資產詳細資料]  窗格中，以滑鼠右鍵按一下要重新發佈之發佈作業的項目，然後選取 [重新發佈]  。  

3. 選取 [是]  以確認動作，並開始進行對於該發佈點的重新發佈程序。  


## <a name="distribution-point-group-status"></a>發佈點群組狀態

[監視]  工作區中的 [發佈點群組狀態]  節點會提供有關發佈點群組的資訊。 您可以檢閱如下列的資訊：  

- 發佈點群組名稱、描述和狀態
- 屬於發佈點群組的發佈點數目
- 已指派至群組的封裝數目
- 相容率

您也可以檢視下列詳細狀態資訊：  

- 發佈點群組的錯誤  
- 正在進行中的發佈數目
- 已成功發佈的數目  

### <a name="monitor-distribution-point-group-status"></a>監視發佈點群組狀態  

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [發佈狀態]  ，然後選取 [發佈點群組狀態]  節點。 它會顯示發佈點群組。  

2. 選取需要其詳細狀態資訊的發佈點群組。  

3. 在功能區的 [常用]  索引標籤上，選取 [檢視狀態]  。 它會顯示發佈點群組的詳細狀態資訊。  


## <a name="distribution-point-configuration-status"></a>發佈點組態狀態

[監視]  工作區中的 [發佈點設定狀態]  節點會提供有關發佈點的資訊。 您可以檢閱針對發佈點啟用的屬性，例如 PXE、多點傳送、內容驗證。 此外，請檢閱發佈點的發佈狀態。

> [!WARNING]  
> 發佈點設定狀態是指過去 24 小時的相對狀態。 如果發佈點發生錯誤而後復原，錯誤狀態會在發佈點復原後最多顯示 24 小時。  

### <a name="monitor-distribution-point-configuration-status"></a>監視發佈點設定狀態  

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [發佈狀態]  ，然後選取 [發佈點設定狀態]  節點。  

2. 選取發佈點。  

3. 在結果窗格中，切換至 [詳細資料]  索引標籤。它會顯示發佈點的狀態資訊。  


## <a name="client-data-sources-dashboard"></a>用戶端資料來源儀表板

使用 [用戶端資料來源]  儀表板，進一步了解用戶端在您環境中取得內容的位置。 儀表板會在用戶端下載內容，並將該資訊回報到站台之後，開始顯示資料。 此程序最多可能需要 24 小時。

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先啟用 [用戶端對等快取]  功能，才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../manage/install-in-console-updates.md#bkmk_options)。  

在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [發佈狀態]  ，然後選取 [用戶端資料來源]  節點。 選取一個要套用到儀表板的時段。 接著，選取您要檢視其資訊的界限群組。 您可以將滑鼠游標暫留在圖格上，以查看有關不同內容或原則來源的更多詳細資料。

您也可以使用報表**用戶端資料來源 - 摘要**，針對每個界限群組，檢視用戶端資料來源的摘要。

### <a name="dashboard-tiles"></a>儀表板磚

儀表板包含以下磚：  

#### <a name="client-content-sources"></a>用戶端內容來源

顯示用戶端從中取得內容的來源：

- 發佈點
- [雲端發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [對等快取](../../../plan-design/hierarchy/client-peer-cache.md)
- [傳遞最佳化](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (從 1906 版開始)<sup>[附註 1](#bkmk_note1)</sup>
- Microsoft Update：當 Configuration Manager 用戶端從 Microsoft 雲端服務下載軟體更新時，裝置會回報此來源。 這些服務包括 Microsoft Update 與 Office 365。

![儀表板的用戶端內容來源圖格](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> 從 1906 版開始<!--3555759-->若要在此儀表板上包含傳遞最佳化，請執行下列動作：
>
> - 設定用戶端設定，在軟體更新群組中**啟用用戶端快速更新安裝**
>
> - 部署 Windows 10 快速更新
>
> 如需詳細資訊，請參閱[管理適用於 Windows 10 更新的快速安裝檔案](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md)。

#### <a name="distribution-points"></a>發佈點

顯示屬於所選界限群組的發佈點數目。

#### <a name="clients-that-used-a-distribution-point"></a>使用發佈點的用戶端

此圖格會顯示選取的界限群組中有多少用戶端使用發佈點取得內容。

#### <a name="peer-cache-sources"></a>對等快取來源

此圖格會針對選取的界限群組，顯示有多少對等快取來源回報下載歷程記錄。

#### <a name="clients-that-used-a-peer"></a>使用對等的用戶端

此圖格會顯示選取的界限群組中有多少用戶端使用對等快取來源取得內容。

#### <a name="top-distributed-content"></a>熱門的發佈內容

依來源類型排列發佈最多的套件
