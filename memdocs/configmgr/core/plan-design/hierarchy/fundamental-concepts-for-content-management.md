---
title: 內容管理基本概念
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的工具和選項來管理您部署的內容。
ms.date: 12/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1355b6d670e94d985717dfb32386f579cba42a0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078663"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Configuration Manager 中的內容管理基本概念

適用於：  Configuration Manager (最新分支)

Configuration Manager 支援健全的工具和選項系統來管理軟體內容。 應用程式、套件、軟體更新和 OS 部署等軟體部署都需要內容。 Configuration Manager 會將內容同時儲存在站台伺服器和發佈點上。 在位置之間傳輸此內容時會需要大量的網路頻寬。 若要有效規劃及使用內容管理基礎結構，請先了解可用的選項與設定。 然後考量如何使用它們，才能最滿足您的網路環境和內容部署需求。  

> [!TIP]  
> 如需有關內容發佈程序的詳細資訊，以及尋求診斷和解決一般內容發佈問題的協助，請參閱[了解 Microsoft Configuration Manager 中的內容發佈及進行疑難排解](https://support.microsoft.com/help/4000401/content-distribution-in-mcm)(機器翻譯\)。

下列各節是內容管理的重要概念。 當概念需要其他資訊或複雜資訊時，便會提供連結將您導向那些詳細資料。


## <a name="accounts-used-for-content-management"></a>用於內容管理的帳戶

下列帳戶可用於內容管理：  

### <a name="network-access-account"></a>網路存取帳戶

用戶端用以連線到發佈點和存取內容。 根據預設，會先嘗試電腦帳戶。  

提取發佈點也會使用此帳戶從遠端樹系中的來源發佈點下載內容。  

從 1806 版開始，某些情況下已不再需要網路存取帳戶。 您可以允許站台使用具有 Azure Active Directory 驗證的增強 HTTP。<!--1358228-->

如需詳細資訊，請參閱[網路存取帳戶](accounts.md#network-access-account)。

### <a name="package-access-account"></a>套件存取帳戶

根據預設，Configuration Manager 會將發佈點上的內容存取權授與一般存取帳戶使用者和系統管理員。 不過，您可以設定其他權限以限制存取。

如需詳細資訊，請參閱 [Package access account](accounts.md#package-access-account) (套件存取帳戶)。


## <a name="bandwidth-throttling-and-scheduling"></a>頻寬節流設定和排程

節流和排程選項皆可協助您控制將內容從站台伺服器發佈到發佈點的時機。 這些功能類似於站台對站台檔案式複寫的頻寬控制，但並不直接相關。  

如需詳細資訊，請參閱[在 System Center Configuration Manager 中管理網路頻寬以進行內容管理](manage-network-bandwidth.md)。


## <a name="binary-differential-replication"></a>二進位差異複寫

Configuration Manager 會使用二進位差異複寫 (BDR) 來更新您先前發佈至其他站台或遠端發佈點的內容。 若要支援 BDR 降低頻寬使用量，請在發佈點上安裝 [遠端差異壓縮]  功能。 如需詳細資訊，請參閱[發佈點必要條件](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq)。

BDR 可將用來傳送所發佈內容更新的網路頻寬降到最低。 每當您變更內容來源檔案時，它只會重新傳送新的或已變更的內容，而不會傳送整組檔案。  

使用 BDR 時，Configuration Manager 會針對您之前發佈的每一組內容，識別來源檔案的變更。  

- 當來源內容中的檔案發生變更時，站台會建立該內容的新累加版本。 然後只將已變更的檔案複寫到目的地站台和發佈點。 如果您將檔案重新命名、移動或變更檔案的內容，系統就會將該檔案視為已變更。 舉例來說，如果您替換之前發佈至數個站台之驅動程式套件中的一個驅動程式檔案，系統只會複寫那個已變更的驅動程式檔案。  

- Configuration Manager 最多可支援五個累加版本的內容集。 在第五次更新之後，下次對內容集進行變更時，站台就會建立一個新版本的內容集。 Configuration Manager 便會發佈新的內容集以取代舊的內容集以及任何累加版本。 在發佈新的內容集之後，稍後對來源檔案進行的累加變更會再次由 BDR 複寫。  

系統支援階層中每個父子站台之間的 BDR。 在站台內的站台伺服器與其標準發佈點之間可支援 BDR。 不過，提取發佈點和雲端發佈點則不支援使用 BDR 來傳輸內容。 提取發佈點支援檔案層級的差異、傳送新的檔案，但不支援檔案內的區塊。

應用程式會一律使用二進位差異複寫。 BDR 對套件而言是選用的，預設不會啟用。 若要針對套件使用 BDR，請為每個套件啟用此功能。 當您建立或編輯套件時，請選取 [啟用二進位差異複寫]  選項。


### <a name="bdr-or-delta-replication"></a>BDR 或差異複寫

<!-- SCCMDocs#1209 -->
下列清單摘要說明「二進位差異複寫」  (BDR) 與「差異複寫」  之間的不同。

#### <a name="summary-of-binary-differential-replication"></a>二進位差異複寫摘要

- Configuration Manager 對 Windows「遠端差異壓縮」  的稱呼
- 「區塊」  層級的差異
- 針對應用程式一律啟用
- 在舊版套件上為選用
- 如果檔案已經存在於發佈點上而有變更，站台就會使用 BDR 來複寫區塊層級的變更，而不會複寫整個檔案。

#### <a name="summary-of-delta-replication"></a>差異複寫摘要

- 「檔案」  層級的差異
- 預設為開啟，無法設定
- 當套件發生變更時，站台會檢查對個別檔案的變更，而不會檢查對整個套件的變更。
    - 如果檔案發生變更，請使用 BDR 來進行工作
    - 如果有新檔案，請複製新檔案


## <a name="peer-caching-technologies"></a>對等快取技術

<!-- SCCMDocs#1044 -->

Configuration Manager 支援數個選項來管理相同網路上對等裝置之間的內容：

- [BranchCache](#branchcache)
- [傳遞最佳化](#delivery-optimization)
- [Configuration Manager 對等快取](#peer-cache)

使用下表來比較這些技術的主要功能：

| 功能  | 對等快取  | 傳遞最佳化  | BranchCache  |
|---------|---------|---------|---------|
| 跨子網路 | 是 | 是 | 否 |
| 頻寬節流處理 | 是 (BITS) | 是 (原生) | 是 (BITS) |
| 部分內容 | 是 | 是 | 是 |
| 控制磁碟上的快取大小 | 是 | 是 | 是 |
| 對等來源探索 | 手動 (用戶端設定) | 自動 | 自動 |
| 同儕節點探索 | 透過管理點 (使用界限群組) | DO 雲端服務 | 廣播 |
| 報告 | 用戶端資料來源儀表板 | 用戶端資料來源儀表板 | 用戶端資料來源儀表板 |
| WAN 使用控制 | 界限群組 | DO GroupID | 僅限子網路 |
| 支援的內容 | 所有 ConfigMgr 內容 | Windows 更新、驅動程式、市集應用程式 | 所有 ConfigMgr 內容 |
| 原則控制 | 用戶端代理程式設定 | 用戶端代理程式設定 (部分) | 用戶端代理程式設定 |

### <a name="recommendations"></a>建議

- 現代化管理：如果您已經在使用現代化工具 (例如 Intune)，請實作「傳遞最佳化」

- Configuration Manager 和共同管理：使用對等快取與「傳遞最佳化」的組合。 使用對等快取搭配內部部署發佈點，並針對雲端案例使用「傳遞最佳化」。

- 已實作的現有 BranchCache：同時使用這全部三種技術。 針對 BranchCache 所不支援的案例，使用對等快取和「傳遞最佳化」。


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) 是一項 Windows 技術。 用戶端如果支援 BranchCache 並已下載您為 BranchCache 設定的部署，便可作為其他支援 BranchCache 之用戶端的內容來源。  

例如，您有一個執行 Windows Server 2012 或更新版本的發佈點，並且設定為 BranchCache 伺服器。 當第一個支援 BranchCache 的用戶端從此伺服器要求內容時，用戶端會下載並快取該內容。  

- 接著，該用戶端會將內容提供給相同子網路上支援 BranchCache 的額外用戶端，這些用戶端也會快取該內容。  
- 相同子網路上的其他用戶端就不需從發佈點下載內容。  
- 該內容會分散在多個用戶端上以供未來傳輸。  

如需詳細資訊，請參閱[對 Windows BranchCache 的支援](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache)。

## <a name="delivery-optimization"></a>傳遞最佳化

<!-- 1324696 -->
您可以使用 Configuration Manager 界限群組，來定義和規範在您的公司網路上以及到遠端辦公室的內容發佈。 [Windows 傳遞最佳化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是一種雲端式點對點技術，可在 Windows 10 裝置之間共用內容。 請設定讓「傳遞最佳化」在於同儕節點之間共用內容時，使用您的界限群組。 用戶端設定會套用界限群組識別碼作為用戶端上的「傳遞最佳化」群組識別碼。 當用戶端與「傳遞最佳化」雲端服務進行通訊時，它會使用此識別碼來尋找含有內容的同儕節點。 如需詳細資訊，請參閱[傳遞最佳化](../../clients/deploy/about-client-settings.md#delivery-optimization)用戶端設定。

傳遞最佳化是針對適用於 Windows 10 品質更新的快速安裝檔案，將 Windows 10 更新傳遞最佳化的建議技術。 從 Configuration Manager 1910 版開始，若要使用「傳遞最佳化」的點對點功能，必須要能透過網際網路存取「傳遞最佳化」雲端服務。 如需所必要網際網路端點的資訊，請參閱[傳遞最佳化的常見問題集](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。 最佳化可用於所有 Windows 更新。 如需詳細資訊，請參閱[將 Windows 10 更新傳遞最佳化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)。


## <a name="microsoft-connected-cache"></a>Microsoft 連線快取

<!--3555764-->
從 1906 版開始，您可以在發佈點上安裝 Microsoft 連線快取伺服器。 藉由快取此內部部署內容，您的用戶端就可以受益於傳遞最佳化功能，但您可以協助保護 WAN 連結。

> [!NOTE]
> 從 1910 版開始，這項功能現在稱為 **Microsoft 連線快取**。 先前稱為傳遞最佳化網路內快取 (DOINC)。

此快取伺服器可視需要以透明方式快取傳遞最佳化所下載的內容。 使用用戶端設定可確保只將此伺服器提供給本機 Configuration Manager 界限群組的成員。

此快取不同於 Configuration Manager 的發佈點內容。 如果您選擇與發佈點角色相同的磁碟機，則會另外儲存內容。

如需詳細資訊，請參閱 [Configuration Manager 中的 Microsoft 連線快取](microsoft-connected-cache.md)。


## <a name="peer-cache"></a>對等快取

用戶端對等快取可協助您管理對遠端位置中用戶端進行的內容部署。 對等快取是一個內建的 Configuration Manager 解決方案，可讓用戶端直接從其本機快取與其他用戶端共用內容。

先將啟用對等快取的用戶端設定部署至集合。 該集合的成員即可作為相同界限群組中其他用戶端的對等內容來源。

從 1806 版開始，用戶端對等快取來源可以將內容分割成組件。 這些組件會將網路傳輸減到最少以降低 WAN 使用量。 管理點可提供內容組件的更詳細追蹤。 它會嘗試排除對每一界限群組的相同內容進行多重下載的情況。<!--1357346-->

如需詳細資訊，請參閱 [Configuration Manager 用戶端的對等快取](client-peer-cache.md)。


## <a name="windows-pe-peer-cache"></a>Windows PE 對等快取

使用 Configuration Manager 來部署新 OS 時，執行工作順序的電腦可以使用 Windows PE 對等快取。 它們會從對等快取來源下載內容，而不會從發佈點下載內容。 此行為有助於在分公司沒有本機發佈點的案例中，將 WAN 流量降到最低。

如需詳細資訊，請參閱 [Windows PE 對等快取](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)。


## <a name="windows-ledbat"></a>Windows LEDBAT

<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) 是 Windows Server 的一個網路壅塞控制功能，可協助管理背景網路傳輸。 針對所支援 Windows Server 版本上執行的發佈點，啟用一個選項來協助調整網路流量。 然後用戶端只會使用網路頻寬 (可用時)。

如需 Windows LEDBAT 的一般詳細資訊，請參閱 [New transport advancements](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) (新的傳輸功能改善) 部落格文章。

當您[設定一般的發佈點設定](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general)時，如需如何搭配 Configuration Manager 發佈點使用 Windows LEDBAT 的詳細資訊，請參閱 [調整下載速度來使用未使用的網路頻寬 (Windows LEDBAT)]  設定。


## <a name="client-locations"></a>用戶端位置

用戶端可從下列位置存取內容：  

- **內部網路** (內部部署)：  

    - 發佈點可以使用 HTTP 或 HTTPS。  

    - 請只在內部部署發佈點無法使用時，才將雲端發佈點用於後援。  

- **內部網路**：  

    - 需要網際網路對向發佈點接受 HTTPS。  

    - 可以使用雲端發佈點或雲端管理閘道 (CMG)。  

        從 1806 版開始，CMG 也可以提供內容給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。 如需詳細資訊，請參閱[修改 CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md)。

- **工作群組**：  

    - 需要發佈點接受 HTTPS。  

    - 可使用雲端發佈點或 CMG。  


## <a name="content-source-priority"></a>內容來源優先順序

當用戶端需要內容時，會對管理點提出內容位置要求。 管理點會傳回對所要求內容有效的來源位置清單。 這份清單會根據特定案例、使用的技術、站台設計、界限群組和部署設定而有所不同。 下列清單包含用戶端可使用之所有可能的內容來源位置，並依優先順序列出：  

1. 作為用戶端之相同電腦上的發佈點
2. 相同網路子網路中的對等來源
3. 相同網路子網路中的發佈點
4. 相同界限群組中的對等來源
5. 目前界限群組中的發佈點
6. 設定後援之鄰近界限群組中的發佈點
7. 預設站台界限群組中的發佈點
8. Windows Update 雲端服務
9. 網際網路對向發佈點
10. Azure 中的雲端發佈點

> [!Note]  
> <!-- SCCMDocs#1607 -->「傳遞最佳化」不適用於此來源優先順序。 此清單是 Configuration Manager 用戶端尋找內容的方式。 「Windows Update 代理程式」會下載適用於「傳遞最佳化」的內容。 如果「Windows Update 代理程式」找不到該內容，則 Configuration Manager 用戶端會使用此清單來搜尋它。

## <a name="content-library"></a>內容庫

內容庫是 Configuration Manager 中內容的單一執行個體存放區。 此內容庫可縮減您所發佈內容的整體大小。  

- 進一步了解[內容庫](the-content-library.md)。
- 使用[內容庫清理工具](content-library-cleanup-tool.md)，將不再與應用程式關聯的內容移除。  


## <a name="distribution-points"></a>發佈點

Configuration Manager 使用發佈點來儲存在用戶端電腦上執行軟體所需要的檔案。 用戶端必須能存取至少一個發佈點，且必須可從該發佈點下載檔案以用於您所部署的內容。  

基本 (非特製化) 發佈點通常是指標準發佈點。 標準發佈點有以下兩個值得特別注意的變化：  

- **提取發佈點**：發佈點的變化，發佈點可在此取得其他發佈點 (來源發佈點) 中的內容。 此程序類似於用戶端從發佈點下載內容的方式。 當站台伺服器將內容直接發佈到每個發佈點時，提取發佈點可協助您避免這段期間所發生的網路頻寬瓶頸，提升內容發佈的效率。 [使用提取發佈點](use-a-pull-distribution-point.md)。

- **雲端發佈點**：為安裝於 Microsoft Azure 上的一種發佈點變化。 [了解如何使用雲端發佈點](use-a-cloud-based-distribution-point.md)。  

標準發佈點可支援一系列設定和功能：  

- 使用**排程**或**頻寬節流設定**之類的控制項，來協助控制此傳輸。  

- 使用其他選項 (包括**預先設置的內容**和**提取發佈點**) 將網路使用量降到最低和進行控制。  

- **BranchCache**、**對等快取**及**傳遞最佳化**是您部署內容時，可用來降低網路頻寬的對等技術。  

- 針對 OS 部署，有各種不同的設定，例如 **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** 和 **[多點傳送](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  

- 適用於**行動裝置**的選項  
  
雲端發佈點和提取發佈點支援上述許多相同設定，但每種發佈點變化亦有其特定限制。  


## <a name="distribution-point-groups"></a>發佈點群組

發佈點群組是可簡化內容發佈的發佈點邏輯群組。  

如需詳細資訊，請參閱[管理發佈點群組](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)。


## <a name="distribution-point-priority"></a>發佈點優先順序

發佈點優先順序值的依據是將先前部署傳送到該發佈點所花費的時間。  

- 此值會自我調整。 您可以在每個發佈點上設定此值，以協助 Configuration Manager 更快將內容傳輸至更多發佈點。  

- 將內容同時發佈至多個發佈點，或發佈至某個發佈點群組時，站台會先將內容傳送至優先順序最高的伺服器。 然後才將該相同內容傳送至優先順序較低的發佈點。  

- 發佈點優先順序不會取代套件的發佈優先順序。 套件優先順序仍然是站台何時傳送不同內容的決定因素。  

例如，您有一個套件優先順序高的套件。 您將它發佈至發佈點優先順序低的伺服器。 這個高優先順序套件的傳輸順序一律會在優先順序低的套件之前。 即使站台將優先順序較低的套件發佈至發佈點優先順序較高的伺服器，仍然會套用套件優先順序。

套件的高優先順序可確保 Configuration Manager 先將該內容發佈至發佈點，然後才傳送任何優先順序較低的套件。  

> [!NOTE]  
> 提取發佈點也會使用優先順序的概念來排序其來源發佈點的順序。  
>
> - 對伺服器進行之內容傳輸的發佈點優先順序，與提取發佈點所使用的優先順序截然不同。 提取發佈點在從來源發佈點搜尋內容時，會使用自己的優先順序。  
> - 如需詳細資訊，請參閱[使用提取發佈點](use-a-pull-distribution-point.md)。  


## <a name="fallback"></a>後援

Configuration Manager 最新分支在關於用戶端如何尋找具有內容的發佈點方面有數項變更，包括後援。

用戶端如果無法從與其目前界限群組關聯的發佈點中找到內容，可切換回使用與鄰近界限群組關聯的內容來源位置。 鄰近界限群組必須與用戶端的目前界限群組具有已定義的關聯性，才能用於後援。 此關聯性包括一段設定的時間，而用戶端必須在此時間內在本機找不到內容，才能將來自鄰近界限群組的內容來源納入其搜尋範圍。

不再使用慣用發佈點概念，也不再提供或強制執行 [允許內容的後援來源位置]  設定。

如需詳細資訊，請參閱[界限群組](../../servers/deploy/configure/boundary-groups.md)。


## <a name="network-bandwidth"></a>網路頻寬

若要協助管理發佈內容時所用的網路頻寬量，您可以使用下列選項：  

- **預先設置的內容**：將內容傳輸至某個發佈點，而不將內容發佈至整個網路。  

- **使用排程及節流**：此設定可協助您控制將內容發佈到發佈點的時機和方式。  

如需詳細資訊，請參閱[在 System Center Configuration Manager 中管理網路頻寬以進行內容管理](manage-network-bandwidth.md)。


## <a name="network-connection-speed-to-content-source"></a>內容來源的網路連線速度

Configuration Manager 最新分支在關於用戶端如何尋找具有內容的發佈點方面有數項變更。 這些變更包括對內容來源的網路速度。

不再使用將發佈點定義為**快**或**慢**的網路連線速度。 相反地，與界限群組相關聯的每個站台系統都會視為相同。

如需詳細資訊，請參閱[界限群組](../../servers/deploy/configure/boundary-groups.md)。


## <a name="on-demand-content-distribution"></a>依需求發佈內容

依需求發佈內容是一個適用於個別應用程式和套件部署的選項。 此選項可讓您依需求將內容發佈至慣用的伺服器。  

- 若要為部署啟用這項設定，請啟用：[將此套件的內容發佈至慣用發佈點]  。  

- 如果您啟用此選項進行部署，而用戶端要求該內容，但用戶端的任何慣用發佈點上皆未提供內容，則 Configuration Manager 會自動將該內容發佈到用戶端的慣用發佈點。  

- 雖然這會觸發 Configuration Manager 自動將內容發佈到該用戶端的慣用發佈點，但是用戶端可能會在用戶端的慣用發佈點收到部署之前，先從其他發佈點取得該內容。 發生此行為時，內容就會出現在該發佈點上，以供下一個搜尋該部署的用戶端使用。  

如需詳細資訊，請參閱[界限群組](../../servers/deploy/configure/boundary-groups.md)。


## <a name="package-transfer-manager"></a>套件傳輸管理員

套件傳輸管理員是站台伺服器元件，可將內容傳輸至其他電腦上的發佈點。  

如需詳細資訊，請參閱[套件傳輸管理員](package-transfer-manager.md)。  


## <a name="prestage-content"></a>預先設置內容

預先設置內容是一個將內容傳輸至某個發佈點，而不將內容發佈至整個網路的程序。  

如需詳細資訊，請參閱[在 System Center Configuration Manager 中管理網路頻寬以進行內容管理](manage-network-bandwidth.md)。
