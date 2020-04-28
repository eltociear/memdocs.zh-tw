---
title: 用戶端對等快取
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 部署內容時，針對來源位置使用用戶端對等快取。
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c302e839c2a41ba27d160db24928f7e202de78dc
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110180"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Configuration Manager 用戶端的對等快取

適用於：  Configuration Manager (最新分支)

<!--1101436-->
使用對等快取，協助您管理對遠端位置中用戶端進行的內容部署。 對等快取是一個內建的 Configuration Manager 解決方案，可讓用戶端直接從其本機快取與其他用戶端共用內容。   

> [!Note]  
> 在 1906 版中，Configuration Manager 預設會啟用此功能。 在 1902 版或更早版本中，Configuration Manager 預設不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  



## <a name="overview"></a>概觀

定義：  

- **對等快取用戶端**：從對等下載內容的任何 Configuration Manager 用戶端  

- **對等快取來源**：您為對等快取啟用並具有要與其他用戶端共用之內容的 Configuration Manager 用戶端  

使用用戶端設定，讓用戶端能夠使用對等快取來源。 您不需要啟用對等快取用戶端。 當您啟用用戶端作為對等快取來源時，管理點會將其包含在內容位置來源清單中。<!--510397--> 如需此程序的詳細資訊，請參閱[作業](#operations)。  

對等快取來源必須是對等快取用戶端之目前界限群組的成員。 管理點在提供給用戶端的內容來源清單中，不會包含來自鄰近界限群組的對等快取來源。 它只會包含來自鄰近界限群組的發佈點。 如需目前和鄰近界限群組的詳細資訊，請參閱[界限群組](../../servers/deploy/configure/boundary-groups.md)。<!--SCCMDocs issue 685-->  

Configuration Manager 用戶端使用對等快取，將快取中的各種內容類型提供給其他用戶端。 此內容包括 Microsoft 365 Apps 企業版與快速安裝檔案。<!--SMS.500850-->  

對等快取不會取代 Windows BranchCache 或傳遞最佳化等其他解決方案的使用。 對等快取會搭配其他解決方案使用。 這些技術提供您更多的選項，以擴充傳統內容部署解決方案，例如發佈點。 對等快取是一個不依賴 BranchCache 的自訂解決方案。 如果您未啟用或使用 BranchCache，則對等快取仍能運作。  

> [!Note]  
> 從 1802 版開始，在部署上一律會啟用 Windows BranchCache。 已移除 [允許用戶端與同一個子網路上的其他用戶端共用內容]  設定。<!--SCCMDocs issue 539--> 如果發佈點支援此設定，且在用戶端中已啟用，用戶端就會使用 BranchCache。 如需詳細資訊，請參閱[設定 BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache)。<!--SCCMDocs issue 735-->   



## <a name="operations"></a>作業

若要啟用對等快取，請將[用戶端設定](#bkmk_settings)部署至集合。 該集合的成員即可作為相同界限群組中其他用戶端的對等快取來源。  

- 以對等內容來源運作的用戶端，會使用狀況訊息向其管理點提交可用的快取內容清單。

   > [!NOTE]
   > 請參閱 [Configuration Manager 中的狀況訊息](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map)以取得適用的對等內容來源狀況訊息清單，特別是包含狀況訊息識別碼 7200、7201、7202 和 7203 的清單。

- 相同界限群組中的另一個用戶端會對管理點提出內容位置要求。 伺服器會傳回潛在內容來源清單。 此清單包含具有內容且在線上的每個對等快取來源。 它也包含該界限群組中的發佈點和其他內容來源位置。 如需詳細資訊，請參閱[內容來源優先順序](fundamental-concepts-for-content-management.md#content-source-priority)。  

- 像往常一樣，搜尋內容的用戶端會從提供的清單中選取一個來源。 然後嘗試取得內容。  

從 1806 版開始，界限群組會包含其他設定，以使您更能掌控環境中的內容發佈。 如需詳細資訊，請參閱[適用於對等下載的界限群組選項](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)。<!--1356193-->

> [!NOTE]  
> 如果用戶端退回至鄰近界限群組來要求內容，管理點就不會將來自鄰近界限群組的對等快取來源新增至潛在內容來源位置清單。  

只選擇最適合作為對等快取來源的用戶端。 請依據底座類型、磁碟空間和網路連線等屬性，評估用戶端適用性。 如需可協助您選取最適合用於對等快取之用戶端的詳細資訊，請參閱[這個由 Microsoft 顧問所維護的部落格](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801)。


### <a name="limited-access-to-a-peer-cache-source"></a>限制存取對等快取來源  

當對等要求內容時，若符合下列任一條件，則對等快取來源會拒絕內容要求：  

- 電力偏低模式  

- 處理器負載超過 80%  

- 磁碟 I/O 的 *AvgDiskQueueLength* 超過 10  

- 無法再連線至電腦  

> [!Tip]  
> 在 Configuration Manager SDK 中，您可以使用對等來源功能的用戶端設定伺服器 WMI 類別 (*SMS_WinPEPeerCacheConfig*) 來進行這些設定。  

當對等快取來源拒絕內容要求時，對等快取用戶端會繼續在其內容來源位置清單中搜尋內容。   



## <a name="requirements"></a>需求

- 對等快取支援[用戶端和裝置支援的作業系統](../configs/supported-operating-systems-for-clients-and-devices.md)中列為支援的所有 Windows 版本。 不支援以非 Windows 作業系統作為對等快取來源或對等快取用戶端。  

- 對等快取來源必須是已加入網域的 Configuration Manager 用戶端。 不過，未加入網域的用戶端仍可以從已加入網域的對等快取來源取得內容。  

- 用戶端只能從其目前界限群組中的對等快取來源下載內容。  

- 除了下列例外狀況，不需要[網路存取帳戶](accounts.md#network-access-account)：  

  - 當啟用對等快取的用戶端從軟體中心執行工作順序，且它會重新開機至開機映像時，請設定站台中的網路存取帳戶。 當裝置位於 Windows PE 中時，它會使用網路存取帳戶，從對等快取來源取得內容。  

  - 必要時，對等快取來源會使用網路存取帳戶來驗證來自對等的下載要求。 此帳戶只需網域使用者權限即可滿足上述用途。  

- 在 1802 (含) 之前的版本中，目前的對等快取來源界限取決於用戶端上次的活動訊號探索提交而定。 因此，基於對等快取的目的，若用戶端漫遊至不同的界限群組，仍然可能被視為是其先前界限群組的成員。 這項行為會導致提供給用戶端的對等快取來源不在其中繼網路位置上。 請勿啟用漫遊用戶端作為對等快取來源。<!--SCCMDocs issue 641-->  

  > [!Important]  
  > 從 1806 版開始，設定管理員在判斷對等快取來源是否已漫遊到另一個位置的效率更高。 此行為可確保管理點將它當作內容來源提供給新位置 (而非舊位置) 的用戶端。 如果您使用對等快取功能並搭配漫遊對等快取來源，將站台更新至 1806 版之後，也請將所有對等快取來源更新至最新的用戶端版本。 在更新至最新版 1806 之前，管理點不會在內容位置清單中包含這些對等快取來源。<!--SCCMDocs issue 850-->  

- 管理點會先驗證對等快取來源已上線，再嘗試下載內容。<!--sms.498675--> 透過使用 TCP 連接埠 10123 的「快速通道」通知用戶端時，就會發生此驗證。<!--511673-->  

> [!Note]  
> 若要利用 Configuration Manager 的新功能，請先將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a> 對等快取用戶端設定

如需對等快取用戶端設定的詳細資訊，請參閱[用戶端快取設定](../../clients/deploy/about-client-settings.md#client-cache-settings)。 

如需如何設定這些設定的詳細資訊，請參閱[如何設定用戶端設定](../../clients/deploy/configure-client-settings.md)。

如果啟用對等快取的用戶端是使用 Windows 防火牆，Configuration Manager 會設定您在用戶端設定中指定的防火牆連接埠。



## <a name="partial-download-support"></a><a name="bkmk_parts"></a> 部分下載支援
<!--1357346-->
從 1806 版開始，用戶端對等快取來源現在可以將內容分割成組件。 這些組件會將網路傳輸減到最少以降低 WAN 使用量。 管理點可提供內容組件的更詳細追蹤。 它會嘗試排除對每一界限群組的相同內容進行多重下載的情況。 


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


### <a name="configure-partial-download"></a>設定部分下載

1. 像往常一樣設定[界限群組](../../servers/deploy/configure/boundary-groups.md)和對等快取來源。  

2. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  。 按一下功能區的 [階層設定]  。  

3. 在 [一般]  索引標籤上，啟用 [將用戶端對等快取來源設定為將內容分割成組件]  選項。  

4. 建立必要的內容相關部署。  

   > [!Note]  
   > 此功能只有當用戶端在背景下載內容時才有作用，例如進行必要部署時。 依需求進行的下載 (例如當使用者安裝「軟體中心」內的可用部署時) 則如常運作。  

若要看看它們如何處理將內容分成多組件來下載的情況，請查看用戶端對等快取來源上的 **ContentTransferManager.log**，以及管理點上的 **MP_Location.log**。  



## <a name="guidance-for-cache-management"></a>快取管理的指引
<!--510645-->
對等快取依賴 Configuration Manager 用戶端快取來共用內容。 在您的環境中管理用戶端快取時，請考慮下列幾點：  

- Configuration Manager 用戶端快取不同於發佈點上的內容庫。 當您管理發佈至發佈點的內容時，Configuration Manager 用戶端會自動管理其快取中的內容。 您可以透過一些設定和方法，來協助控制哪些內容會在對等快取來源的快取中。 如需詳細資訊，請參閱[設定 Configuration Manager 用戶端的用戶端快取](../../clients/manage/manage-clients.md#BKMK_ClientCache)。  

- 對等快取來源會套用正常快取大小和維護。 如需詳細資訊，請參閱[設定用戶端快取大小](../../clients/deploy/about-client-settings.md#configure-client-cache-size)。 請考慮如 OS 升級套件或 Windows 10 快速更新檔案等較大內容的大小。 根據對等快取來源上的可用磁碟空間，比較您對此內容的需求。  

- 對等快取來源用戶端會在對等下載內容時，更新快取中此內容的上次參考時間。 當用戶端自動維護其快取時會使用此時間戳記，先移除較舊的內容。 因此，它應該會等待移除對等快取用戶端較常下載的內容 (如果有的話)。  

- 如有必要，請在 OS 部署工作順序期間，使用 **SMSTSPreserveContent** 變數將內容保留在用戶端快取中。 如需詳細資訊，請參閱[工作順序變數](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent)。  

- 如有必要，請在建立下列軟體時，使用 [將內容保存在用戶端快取中]  選項：  
  - 應用程式
  - 套件
  - OS 映像
  - OS 升級套件
  - 開機映像



## <a name="monitoring"></a>監視   

為協助您了解對等快取的使用情況，請檢視 [用戶端資料來源]  儀表板。 如需詳細資訊，請參閱[用戶端資料來源儀表板](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)。

您也可以使用報表來檢視對等快取使用情況。 在主控台中，移至 [監視]  工作區，展開 [報告]  ，然後選取 [報表]  節點。 下列報表的類型全部都是 [軟體發佈內容]  ：  

1.  **對等快取來源內容拒絕**：界限群組中對等快取來源拒絕內容要求的頻率。  

    > [!Note]  
    > **已知問題**<!--486652-->:向下切入 *MaxCPULoad* 或 *MaxDiskIO* 之類的結果時，您可能會收到錯誤，暗示找不到報告或詳細資料。 若要解決此問題，請使用其他兩種報表，直接顯示結果。  

2. **對等快取來源內容拒絕條件**：顯示指定界限群組或拒絕類型的拒絕詳細資料。 

    > [!Note]  
    > **已知問題**<!--486652-->:您無法從可用的參數中選取，而必須改為手動輸入。 如 [對等快取來源內容拒絕]  報表中所示，輸入 [界限群組名稱]  和 [拒絕類型]  的值。 例如，您可能會在 [拒絕類型]  輸入 *MaxCPULoad* 或 *MaxDiskIO*。  

3. **對等快取來源內容拒絕詳細資料**：顯示用戶端已要求但遭到拒絕的內容。  

    > [!Note]  
    > **已知問題**<!--486652-->:您無法從可用的參數中選取，而必須改為手動輸入。 依據「對等快取來源內容拒絕」  報告所示，輸入「拒絕類型」  的值。 然後，輸入您想進一步了解的內容來源的「資源識別碼」  。 
    > 
    > 尋找內容來源的資源識別碼︰  
    > 
    > 1. 尋找「依條件的對等快取來源內容拒絕」  報告結果中顯示為「對等快取來源」  的電腦名稱。  
    > 
    > 2. 移至 [資產與合規性]  工作區，選取 [裝置]  節點，然後搜尋該電腦的名稱。 使用 [資源識別碼] 欄中的值。  

