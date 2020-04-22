---
title: 規劃軟體更新
titleSuffix: Configuration Manager
description: 在 Configuration Manager 生產環境中使用軟體更新之前，請務必先規劃軟體更新點基礎結構。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: dca6f3e4bf67ac4c947f785016d781e538ee0a4e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708746"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>在 Configuration Manager 中規劃軟體更新

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 生產環境中使用軟體更新之前，請務必先進行規劃程序。 成功的軟體更新實作一定要有良好的軟體更新點基礎結構計劃。 如需軟體更新容量規劃的資訊，請參閱[大小和縮放比例](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point)。


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> 判斷軟體更新點基礎結構  

本節包含下列子主題：    
- [軟體更新點清單](#BKMK_SUPList)
- [軟體更新點切換](#BKMK_SUPSwitching)
- [手動將用戶端切換到新軟體更新點](#BKMK_ManuallySwitchSUPs)
- [不受信任樹系中的軟體更新點](#BKMK_SUP_CrossForest)
- [在頂層站台上使用現有 WSUS 伺服器作為同步處理來源](#BKMK_WSUSSyncSource)
- [次要站台上的軟體更新點](#BKMK_SUPSecSite)  
- [規劃以網際網路為基礎的用戶端](#bkmk_internet-clients)  
- [規劃軟體更新內容](#bkmk_content)  
- [規劃協力廠商更新](#bkmk_thirdparty)  


管理中心網站和所有子主要站台必須擁有軟體更新點。 當您在規劃軟體更新點基礎結構時，請判斷下列相依性：
- 安裝站台軟體更新點的位置  
- 哪些站台需要可接受來自以網際網路為基礎之用戶端通訊的軟體更新點
- 次要站台是否需要軟體更新點  

> [!IMPORTANT]  
>  如需軟體更新所需之內部和外部相依性的詳細資訊，請參閱[軟體更新的必要條件](prerequisites-for-software-updates.md)。  

在 Configuration Manager 主要站台上新增多個軟體更新點來提供容錯功能。 軟體更新點的容錯移轉設計與設計管理點所使用單純的隨機模型不同。 和管理點的設計不同，當用戶端切換至新的軟體更新點時，軟體更新點設計中會有用戶端和網路效能成本。 當用戶端切換至新的 WSUS 伺服器以掃描軟體更新時，會導致類別目錄大小增加，並且會提高相關聯用戶端及網路效能的需求。 因此，用戶端會與其順利掃描的上一個軟體更新點保留親和性。  

您在主要站台上安裝的第一個軟體更新點，即是您在主要站台上新增之所有其他軟體更新點的同步處理來源。 在您新增軟體更新點並啟動同步處理之後，從 [監視]  工作區的 [軟體更新點同步處理狀態]  節點檢視軟體更新點的狀態和同步處理來源。  

當設定為站台同步處理來源的軟體更新點失敗時，手動移除失敗的角色。 然後選取新的軟體更新點以作為同步處理來源。 如需詳細資訊，請參閱[移除站台系統角色](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role)。  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> 軟體更新點清單  

Configuration Manager 在下列案例會為用戶端提供軟體更新點清單：  

- 新的用戶端收到啟用軟體更新的原則  

- 用戶端無法連絡其指派的軟體更新點，並需要切換至其他軟體更新點  

用戶端會從清單中隨機選取軟體更新點。 它會優先選取位於相同樹系中的軟體更新點。 Configuration Manager 為用戶端提供的清單會依用戶端的類型而有所不同：  

-   **以內部網路為基礎的用戶端**：您可以設定為只允許內部網路連線接收軟體更新點清單，或允許網際網路和內部網路用戶端連線接收軟體更新點清單。  

-   **以網際網路為基礎的用戶端**：您可以設定為只允許網際網路連線接收軟體更新點清單，或允許網際網路和內部網路用戶端連線接收軟體更新點清單。  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> 軟體更新點切換  

> [!NOTE]  
> 用戶端會使用界限群組來尋找新的軟體更新點。 如果其目前的軟體更新點不再可供存取，它們也會使用界限群組進行後援並尋找新的軟體更新點。 請將個別的軟體更新點新增至不同的界限群組，來控制用戶端可以尋找的伺服器。 如需詳細資訊，請參閱[軟體更新點](../../core/servers/deploy/configure/boundary-groups.md#software-update-points)。  

如果站台擁有多個軟體更新點，而其中有一個軟體更新點失敗或無法使用，用戶端將會連線至不同的軟體更新點。 透過此新的伺服器，用戶端會繼續掃描最新的軟體更新。 當用戶端第一次獲指派軟體更新點時，除非無法掃描，否則會保持指派給該軟體更新點。  

軟體更新的掃描可能會失敗好幾次，並傳回非重試錯誤碼。 當掃描失敗且傳回重試錯誤碼時，用戶端會開始進行重試程序，以掃描軟體更新點上的軟體更新。 導致傳回重試錯誤碼的高層級狀態，通常是因為無法與 WSUS 伺服器連線，或是發生暫時性的超載情形。 當用戶端無法掃描軟體更新時，它會使用下列程序：  

1.  用戶端會在下列情況下掃描軟體更新：  
    - 依其排程時間
    - 手動從用戶端的 [控制台] 執行時
    - 手動從 Configuration Manager 主控台透過用戶端通知動作執行時
    - 透過 Configuration Manager SDK 方法執行時  

2.  如果掃描失敗，用戶端會等待 30 分鐘重試掃描。 它會使用相同的軟體更新點。  

3.  用戶端每 30 分鐘至少重試四次。 當第四次重試失敗，並再等待兩分鐘後，用戶端會移至其清單中的下一個軟體更新點。  

4.  用戶端會對新的軟體更新點重複此程序。 掃描成功後，用戶端會繼續連線到新的軟體更新點。  

下列清單提供可在考量軟體更新點重試及切換案例時使用的其他資訊：  

-   如果用戶端與內部網路中斷連線，並且無法掃描軟體更新，該用戶端不會切換至另一個軟體更新點。 這是預期發生的失敗情形，因為用戶端無法與內部網路或允許內部網路連線的軟體更新點連線。 Configuration Manager 用戶端會判斷內部網路軟體更新點的可用性。  

-   如果您想要管理網際網路上的用戶端，並已設定多個軟體更新點接收網際網路用戶端通訊，則會遵循先前所述的標準重試程序進行切換程序。  

-   如果啟動掃描程序，但用戶端在掃描完成前關閉，此情況不會視為掃描失敗，也不會將此狀況計為四次重試的計數中。  

當 Configuration Manager 收到下列任一 Windows Update 代理程式錯誤碼時，用戶端會重試連線：  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

若要查閱錯誤碼的意義，請將十進位的錯誤碼轉換成十六進位，然後在 [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx) (Windows Update 代理程式 - 錯誤碼 Wiki) 此類網站上，搜尋十六進位值。例如，十進位的錯誤碼 2149842970 為十六進位 8024001A，這表示未設定 WU_E_POLICY_NOT_SET A 原則值。  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a> 手動將用戶端切換到新軟體更新點

當主動式軟體更新點發生問題時，將 Configuration Manager 用戶端切換到新軟體更新點。 只有在用戶端從管理點收到多個軟體更新點時，才會發生這項變更。

> [!IMPORTANT]    
> 當您切換裝置以使用新伺服器時，裝置就會使用後援設定來尋找新伺服器。 用戶端會在其下一個軟體更新掃描週期期間，切換到新的軟體更新點。<!-- SCCMDocs#1537 -->
>
> 在開始這項變更之前，請先檢閱您的界限群組設定，確定軟體更新點均位於正確的界限群組中。 如需詳細資訊，請參閱[軟體更新點](../../core/servers/deploy/configure/boundary-groups.md#software-update-points)。  
>
> 切換到新的軟體更新點會產生額外的網路流量。 流量取決於您的 WSUS 組態設定 (例如已同步的分類和產品)，或是否共用 WSUS 資料庫。 如果您打算切換多部裝置，請考慮在維護期間進行。 此時間可在用戶端使用新軟體更新點掃描時，降低對您網路的影響。  

#### <a name="process-to-switch-software-update-points"></a>切換軟體更新點的程序  
在裝置集合上開始這項變更。 觸發之後，用戶端會在下次掃描時尋找另一個軟體更新點。  

1.  在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選擇 [裝置集合]  節點。  

2.  選取目標集合。 在功能區之 [首頁]  索引標籤的 [集合]  群組中，按一下 [用戶端通知]  ，然後按一下 [切換至下一個軟體更新點]  。  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> 不受信任樹系中的軟體更新點  

在站台上建立一或多個軟體更新點，以支援不受信任樹系中的用戶端。 若要在其他樹系中新增軟體更新點，請先在該樹系中安裝及設定 WSUS 伺服器。 接著，再啟動精靈以新增具有軟體更新點站台系統角色的 Configuration Manager 站台伺服器。 在精靈中設定下列設定，即可與不受信任樹系中的 WSUS 順利連線：  

-   指定可存取不受信任樹系中 WSUS 伺服器的**站台系統安裝帳戶**。  

-   指定要連線到 WSUS 伺服器的 **WSUS 伺服器連線帳戶**。  

例如，您的樹系 A 中有一個主要站台，以及兩個軟體更新點 (SUP01 和 SUP02)。 針對相同的主要站台，您在樹系 B 中也有兩個軟體更新點 (SUP03 和 SUP04)。切換至下一個軟體更新點時，用戶端會優先選取相同樹系中的伺服器。  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a> 在頂層站台上使用現有 WSUS 伺服器作為同步處理來源  

通常會在階層的頂層站台設定與 Microsoft Update 同步處理軟體更新中繼資料。 當您的組織安全性原則不允許頂層站台存取網際網路時，請設定頂層站台的同步處理來源使用現有的 WSUS 伺服器。 此 WSUS 伺服器不在您的 Configuration Manager 階層中。 例如，您在連線到網際網路的網路 (DMZ) 中有 WSUS 伺服器，但頂層站台所在的內部網路無法存取網際網路。 請將 DMZ 中的 WSUS 伺服器設定為軟體更新中繼資料的同步處理來源。 並設定 DMZ 中的 WSUS 伺服器，使用 Configuration Manager 中所需的相同準則來同步軟體更新。 否則，頂層站台可能不會與預期的軟體更新同步處理。 當您安裝軟體更新點時，請設定 WSUS 伺服器連線帳戶。 此帳戶必須能夠存取 DMZ 中的 WSUS 伺服器。 另請確認防火牆允許適當連接埠的流量。 如需詳細資訊，請參閱[軟體更新點用來同步處理來源的連接埠](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS)。  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> 次要站台上的軟體更新點  

軟體更新點在次要站台上是選用項目。 只在次要站台上安裝一個軟體更新點。 當次要站台未安裝軟體更新點時，次要站台界限內的裝置會使用其指派主要站台的軟體更新點。 當次要站台之裝置和父主要站台的軟體更新點之間的網路頻寬有所受限時，您通常會在次要站台上安裝軟體更新點。 當主要站台的軟體更新點接近容量限制時，您也可以使用此設定。 順利安裝軟體更新點並在次要站台上進行設定後，會針對用戶端更新全站台原則，同時會開始使用新的軟體更新點。  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a> 規劃以網際網路為基礎的用戶端

當您需要管理從您的網路漫遊至網際網路的裝置時，請規劃如何管理這些裝置上的軟體更新。 Configuration Manager 針對此案例提供數項技術支援。 請視需要使用其中一項或一組技術，以符合您組織的需求。

#### <a name="cloud-management-gateway"></a>雲端管理閘道
在 Microsoft Azure 中建立雲端管理閘道，並啟用至少一個內部部署軟體更新點，以允許來自以網際網路為基礎之用戶端的流量。 當用戶端漫遊至網際網路時，它們會繼續對您的軟體更新點進行掃描。 所有以網際網路為基礎的用戶端一律會從 Microsoft Update 雲端服務取得內容。 

如需詳細資訊，請參閱[規劃雲端管理閘道](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)。  

#### <a name="internet-based-client-management"></a>以網際網路為基礎的用戶端管理
將軟體更新點放在網際網路對向網路中，並將它啟用以允許來自以網際網路為基礎之用戶端的流量。 當用戶端漫遊至網際網路時，它們會切換至此軟體更新點進行掃描。 所有以網際網路為基礎的用戶端一律會從 Microsoft Update 雲端服務取得內容。

如需以網際網路為基礎之用戶端管理優缺點的詳細資訊，請參閱[管理網際網路上的用戶端](../../core/clients/manage/manage-clients-internet.md)。

#### <a name="windows-update-for-business"></a>Windows Update for Business
商務用 Windows Update 可讓您確保 Windows 10 裝置一律為具有最新品質和功能更新的最新狀態。 這些裝置會直接連線到 Windows Update 雲端服務。 Configuration Manager 能夠區分使用 WUfB 與 WSUS 來取得軟體更新的 Windows 10 電腦。

如需詳細資訊，請參閱[與商務用 Windows Update 整合](../deploy-use/integrate-windows-update-for-business-windows-10.md)。


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a> 規劃軟體更新內容

用戶端必須下載軟體更新的內容檔案，才能進行安裝。 Configuration Manager 提供數項技術以支援此內容的管理和傳遞。 或者，設定軟體更新部署以允許或要求用戶端直接從 Microsoft Update 雲端服務取得內容。

#### <a name="download-and-distribute-content"></a>下載並散發內容 
根據預設，Configuration Manager 中的軟體更新管理程序會使用內建內容管理功能。 這些功能包括集中式儲存單一版本內容庫，以及發佈點站台系統角色的分散式設計。 您可以在下載並發佈軟體更新部署套件時使用這些功能。 

如需詳細資訊，請參閱[下載軟體更新](../deploy-use/download-software-updates.md)。

#### <a name="manage-express-installation-files-for-windows-10"></a>管理適用於 Windows 10 的快速安裝檔案
Configuration Manager 支援使用適用於 Windows 10 更新的快速安裝檔案。 快速更新檔案和支援的技術 (例如傳遞最佳化) 可協助降低將大型內容檔案下載至用戶端的網路影響。 

如需詳細資訊，請參閱[將 Windows 10 更新傳遞最佳化](../deploy-use/optimize-windows-10-update-delivery.md)。

#### <a name="clients-download-content-from-the-internet"></a>用戶端從網際網路下載內容
當您將軟體更新部署至用戶端時，請設定部署讓用戶端從 Microsoft Update 雲端服務下載內容。 當用戶端無法從其他內容來源下載內容時，仍可從網際網路下載內容。 

從 1806 版開始，您不需要在部署軟體更新時建立部署套件。 當您選取 [沒有任何部署套件]  選項時，用戶端仍可從本機來源下載內容 (如果適用)，但通常會從 Microsoft Update 服務下載。<!--1357933-->

以網際網路為基礎的用戶端一律會從 Microsoft Update 雲端服務下載內容。 請勿將軟體更新部署套件發佈到雲端發佈點。 您會支付雲端發佈點儲存的費用，但用戶端不會下載這些套件。 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a> 規劃協力廠商更新
Configuration Manager 會與 WSUS 整合，以原生支援 Microsoft 所發佈的軟體更新。 大多數客戶會使用其他協力廠商應用程式，這些應用程式也需要更新。 若要確保協力廠商應用程式處於最新狀態，需要考量幾個選項。

#### <a name="supersede-applications-to-update"></a>取代應用程式以進行更新
使用 Configuration Manager 之應用程式管理功能的取代關聯性，來升級或取代現有的應用程式。 當您取代應用程式時，請指定新的部署類型來取代已取代應用程式的部署類型。 另請決定是否要先升級或解除安裝已取代的應用程式，再安裝取代的應用程式。

如需詳細資訊，請參閱[修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)。

#### <a name="third-party-software-updates"></a>協力廠商軟體更新
從 1806 版開始，請使用 Configuration Manager 主控台中的 [協力廠商軟體更新類別目錄]  節點來訂閱協力廠商類別目錄、將其更新發佈到您的軟體更新點，然後將其部署至用戶端。<!--1352101-->

如需詳細資訊，請參閱[協力廠商軟體更新](../deploy-use/third-party-software-updates.md)。

#### <a name="system-center-updates-publisher"></a>System Center 更新發行者
System Center Updates Publisher (SCUP) 是一個獨立的工具，可讓獨立軟體廠商或企業營運應用程式開發人員管理自訂更新。 這些更新包含具有相依性的更新，例如驅動程式和更新配套。

如需詳細資訊，請參閱 [System Center Updates Publisher](../tools/updates-publisher.md)。



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a> 規劃軟體更新點安裝  

本節包含下列子主題：  
- [軟體更新點的需求](#BKMK_SUPSystemRequirements)
- [規劃 WSUS 安裝](#BKMK_PlanningForWSUS)
- [設定防火牆](#BKMK_ConfigureFirewalls)  


本節提供有關採取某些步驟才能順利規劃及準備軟體更新點安裝的資訊。 在您為 Configuration Manager 中的軟體更新點建立站台系統角色之前，需要考量幾項需求。 具體需求取決於您的 Configuration Manager 基礎結構。 當您將軟體更新點設定為使用 HTTPS 進行通訊時，請務必檢閱本節的內容。 具備 HTTPS 功能的伺服器需要額外步驟才能正常運作。  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> 軟體更新點的需求  

在符合 WSUS 的最低需求及支援 Configuration Manager 站台系統設定的站台系統上，安裝軟體更新點角色。  

-   如需 Windows Server 中 WSUS 伺服器角色的最低需求詳細資訊，請參閱 [Review considerations and system requirements](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements) (檢閱考量及系統需求)。  

-   如需 Configuration Manager 站台系統所支援設定的詳細資訊，請參閱[站台及站台系統必要條件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> 規劃 WSUS 安裝  

在您針對軟體更新點角色所設定的所有站台系統伺服器上安裝支援版本的 WSUS。 當您未在站台伺服器上安裝軟體更新點時，請在站台伺服器上安裝 WSUS 管理主控台。 此元件可讓站台伺服器與軟體更新點上執行的 WSUS 進行通訊。  

當您在 Windows Server 2012 或更新版本上使用 WSUS 時，請設定額外的權限，以允許 Configuration Manager 中的 **WSUS Configuration Manager** 元件連線至 WSUS。 此元件會定期執行健全狀況檢查。 選擇下列其中一個選項以設定必要權限：  

-   新增 [SYSTEM]  帳戶至 [WSUS Administrators]  群組  

-   新增 **NT AUTHORITY\SYSTEM** 帳戶作為 WSUS 資料庫 (SUSDB) 的使用者。 設定最小的 webService 資料庫角色成員資格。  
  
如需如何在 Windows Server 上安裝 WSUS 的詳細資訊，請參閱 [Install the WSUS Server Role](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role) (安裝 WSUS 伺服器角色)。  

當您在主要站台安裝一個以上的軟體更新點時，請在相同的 Active Directory 樹系中針對各軟體更新點使用相同的 WSUS 資料庫。 共用相同的資料庫可提升用戶端切換至新軟體更新點時的效能。 如需詳細資訊，請參閱[針對軟體更新點使用共用的 WSUS 資料庫](software-updates-best-practices.md#bkmk_shared-susdb)。  

#### <a name="configuring-the-wsus-content-directory-path"></a>設定 WSUS 內容目錄路徑

安裝 WSUS 時，您必須提供內容目錄路徑。 WSUS 內容目錄主要用於儲存用戶端在掃描期間所需的 Microsoft 軟體授權條款檔案。 Configuration Manager  WSUS 內容目錄不應與 Configuration Manager 軟體部署套件的內容來源目錄重疊。 若將 WSUS 內容目錄與 Configuration Manager 套件來源重疊，會導致從 WSUS 內容目錄移除不正確的檔案。

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a> 設定 WSUS 使用自訂網站  
當您安裝 WSUS 時，可以選擇使用現有 IIS 預設網站，或建立自訂 WSUS 網站。 為 WSUS 建立自訂網站可讓 IIS 在專用的虛擬網站上裝載 WSUS 服務。 否則，它會共用其他 Configuration Manager 站台系統或應用程式使用的相同網站。 當您在站台伺服器上安裝軟體更新點角色時，特別需要此設定。 當您在 Windows Server 2012 或更新版本中執行 WSUS 時，預設會將 WSUS 設定為 HTTP 使用連接埠 8530，HTTPS 使用連接埠 8531。 當您建立站台的軟體更新點時，請指定這些連接埠。  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> 使用現有 WSUS 基礎結構  
在將 Configuration Manager 安裝為軟體更新點之前，請選取在您環境中作用的 WSUS 伺服器。 設定軟體更新點時，請指定同步處理設定。 Configuration Manager 會連線至在軟體更新點伺服器上執行的 WSUS 伺服器，並且以相同的設定值設定 WSUS。 

將伺服器設定為軟體更新點之前，請將其產品和分類設定與您的 Configuration Manager 設定進行比較。 如果在將現有的 WSUS 伺服器設定為軟體更新點之前就已同步此伺服器，而且產品和分類清單不同，則無論設定為何，都會同步所有的軟體更新中繼資料。 此行為會導致站台資料庫中的軟體更新中繼資料與預期不符。 

當您將產品或分類直接新增至 WSUS 管理主控台，然後立即啟動同步處理時，會經歷相同的行為。 根據預設，Configuration Manager 會連線到 WSUS，並且重設任何在 Configuration Manager 以外修改的設定。 與您在同步處理設定中所指定的產品和分類不符的軟體更新會設定為到期。 然後從站台資料庫中予以移除。  

當 WSUS 伺服器設定為軟體更新點時，就無法將它當作獨立的 WSUS 伺服器使用。 如果您需要未受 Configuration Manager 管理的個別獨立 WSUS 伺服器，請在不同的伺服器上設定它。  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> 將 WSUS 設定為複本伺服器  
當您在主要站台伺服器上新增軟體更新點角色時，您無法使用設定為複本的 WSUS 伺服器。 當 WSUS 伺服器設定為複本時，Configuration Manager 無法設定 WSUS 伺服器，而且 WSUS 同步處理會失敗。 您在主要站台安裝的第一個軟體更新點就是預設的軟體更新點。 站台的其他軟體更新點會設定為預設軟體更新點的複本。  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> 決定是否要將 WSUS 設定為使用 SSL  
使用 SSL 通訊協定來協助確保軟體更新點的安全。 WSUS 會使用 SSL 驗證對 WSUS 伺服器通訊的用戶端電腦與下游 WSUS 伺服器。 WSUS 還會使用 SSL 將軟體更新中繼資料加密。 當您選擇以 SSL 確保 WSUS 的安全時，請在安裝軟體更新點之前準備好 WSUS 伺服器。 如需詳細資訊，請參閱 WSUS 文件中的 [Configure SSL on the WSUS server](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) (設定 WSUS 伺服器上的 SSL) 一文。 

當您安裝並設定軟體更新點時，請選取 [為 WSUS 伺服器啟用 SSL 通訊]  選項。 否則，Configuration Manager 就不會設定 WSUS 使用 SSL。 當您在軟體更新點上啟用 SSL 時，也請將子站台上的任何軟體更新點設定為使用 SSL。  


###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a> 設定防火牆  

Configuration Manager 管理中心網站上的軟體更新點會與軟體更新點上的 WSUS 通訊。 WSUS 會與同步處理來源通訊以同步軟體更新中繼資料。 子站台上的軟體更新點會與父站台上的軟體更新點通訊。 當主要站台有一個以上的軟體更新點時，其他軟體更新點會與預設軟體更新點通訊。 預設角色是在站台安裝的第一個軟體更新點。  

您可能需要設定防火牆，以允許 WSUS 在下列情況下使用 HTTP 或 HTTPS 流量： 
- 在軟體更新點與網際網路之間
- 在軟體更新點與其上游同步處理來源之間
- 在其他軟體更新點之間  

與 Microsoft Update 的連線一律設定為 HTTP 使用連接埠 80 以及 HTTPS 使用連接埠 443。 使用自訂連線埠，從子站台軟體更新點上的 WSUS 連線到父站台軟體更新點上的 WSUS。 當您的安全性原則不允許連線時，請使用匯出和匯入同步處理方法。 如需詳細資訊，請參閱本文中的[同步處理來源](#BKMK_SyncSource)一節。 如需 WSUS 所使用連接埠的詳細資訊，請參閱[如何判斷 WSUS 在 Configuration Manager 中使用的連接埠設定](../get-started/install-a-software-update-point.md#wsus-settings)。  


#### <a name="restrict-access-to-specific-domains"></a>限制對特定網域的存取權  

如果貴組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，則您需要允許主動式軟體更新點存取網際網路端點。 然後 WSUS 和自動更新即可與 Microsoft Update 雲端服務進行通訊。

如需詳細資訊，請參閱[網際網路存取需求](../../core/plan-design/network/internet-endpoints.md#bkmk_sum)。


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> 規劃同步處理設定  

本節包含下列子主題：  
- [同步處理來源](#BKMK_SyncSource)
- [同步處理排程](#BKMK_SyncSchedule)
- [更新分類](#BKMK_UpdateClassifications)
- [產品](#BKMK_UpdateProducts)
- [取代規則](#BKMK_SupersedenceRules)
- [語言](#BKMK_UpdateLanguages)  
- [執行時間上限](#bkmk_maxruntime)


Configuration Manager 中的軟體更新同步處理會根據您設定的準則下載軟體更新中繼資料。 您階層中的頂層站台會從 Microsoft Update 同步軟體更新。 您可以選擇將頂層站台上的軟體更新點設定為與現有 WSUS 伺服器同步處理，而不是在 Configuration Manager 階層中。 子主要站台會同步處理管理中心網站上軟體更新點的軟體更新中繼資料。 在您安裝並設定軟體更新點之前，請使用本節規劃同步處理設定。  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> 同步處理來源  

軟體更新點的同步處理來源設定會指定軟體更新點擷取軟體更新中繼資料的位置。 它也會指定同步處理程序是否建立 WSUS 報告事件。  

-   **同步來源**：根據預設，頂層站台的軟體更新點會設定 Microsoft Update 的同步來源。 您可以選擇以現有的 WSUS 伺服器同步處理頂層站台。 子主要站台上的軟體更新點會將同步處理來源設定為管理中心網站的軟體更新點。  

    -  您在主要站台安裝的第一個軟體更新點 (即預設的軟體更新點) 會與管理中心網站同步處理。 主要站台上的其他軟體更新點則會與主要站台上的預設軟體更新點同步處理。  

    - 當軟體更新點與 Microsoft Update 或上游更新伺服器中斷連線時，請將同步處理來源設定為不與設定的同步處理來源同步。 相反地，將它設定為使用 **WSUSUtil** 工具的匯出與匯入功能來同步軟體更新。 如需詳細資訊，請參閱[從已中斷連線的軟體更新點同步處理軟體更新](../get-started/synchronize-software-updates-disconnected.md)。  

-   **WSUS 報告事件：** 用戶端電腦上的 Windows Update 代理程式可以建立 WSUS 報告的事件訊息。 Configuration Manager 不會使用這些事件。 因此，預設會選取 [不要建立 WSUS 報告事件]  選項。 沒有建立這些事件時，軟體更新評估與合規性掃描期間是用戶端唯一應該連線至 WSUS 伺服器的時間。 如果需要這些事件用於報告 Configuration Manager 以外的範圍，請修改此設定以建立 WSUS 報告事件。  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> 同步處理排程  

在 Configuration Manager 階層中頂層站台上的軟體更新點設定同步處理排程。 當您設定同步處理排程時，軟體更新點會在您指定的日期和時間進行與同步處理來源的同步處理。 自訂排程可讓您同步軟體更新，以針對您的環境進行最佳化。 請考慮 WSUS 伺服器、站台伺服器和網路的效能需求。 例如，每週上午 2:00 進行一次。 或者，使用 Configuration Manager 主控台中 [所有軟體更新]  或 [軟體更新群組]  節點的 [同步處理軟體更新]  動作，手動啟動頂層站台上的同步處理。  

> [!TIP]  
>  請使用適合您環境的時間來排程執行軟體更新同步處理的時間。 常見的情形是將同步處理排程設定為在 Microsoft 每個月的第二個星期二的定期軟體更新發行後馬上執行。 這一天通常稱為「週二修補日」  。 如果您使用 Configuration Manager 傳遞 Endpoint Protection 和 Windows Defender 定義以及引擎更新，請考慮將同步處理排程設定為每天執行。  

在軟體更新點成功同步之後，它會將同步處理要求傳送至子站台。 如果您在主要站台有其他軟體更新點，它會將同步處理要求傳送至各個軟體更新點。 此程序會在階層中的每個站台上重複。  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> 更新分類  

每個軟體更新都利用有助於組織不同類型更新的更新分類來加以定義。 在同步處理程序期間，站台會同步指定分類的中繼資料。 

Configuration Manager 支援下列更新分類的同步處理：  

-   **重大更新**：針對特定問題指定廣為發行的更新，以解決與安全性無關的重大 Bug。  

-   **定義更新**：病毒或其他定義檔案的更新。  

-   **Feature Pack**：於產品發行之外散發的新產品功能，通常會包含在下一次的完整產品發行中。  

-   **安全性更新**：與安全相關問題且廣為發行的產品特定更新。  

-   **Service Pack**：套用至 OS 或應用程式的累計 Hotfix 集。 這些 Hotfix 包含安全性更新、重大更新和軟體更新。  

-   **工具**：有助於完成一或多項工作的公用程式或功能。  

-   **更新彙總套件**：封裝在一起以便於部署的累計 Hotfix 集。 這些 Hotfix 包含安全性更新、重大更新和軟體更新。 更新彙總套件一般處理特定領域，例如安全性或產品元件。  

-   **更新**：針對目前已安裝應用程式或檔案的更新。  

-   **升級**：新版 Windows 10 的功能更新。  

請只在頂層站台上設定更新分類設定。 更新分類設定不會在子站台的軟體更新點上設定，因為軟體更新中繼資料是從頂層站台複寫而來。 當您選取更新分類時，請留意選取的分類越多，同步處理軟體更新中繼資料的時間就會越長。  

> [!WARNING]  
>  最佳做法是在您第一次同步之前清除所有分類。 在初始同步處理後，選取所需的分類，然後重新執行同步處理。  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a> 產品  

各個軟體更新的中繼資料會針對適用的更新定義一或多項產品。 產品即為特定版本的 OS 或應用程式。 產品的範例有 Microsoft Windows 10。 而產品系列則是指衍生出個別產品的基礎 OS 或應用程式。 產品系列的範例有 Microsoft Windows，Windows 10 和 Windows Server 2016 就是其中的成員。 請選取產品系列或產品系列中的個別產品。  

當軟體更新適用於多項產品，而且至少已選取其中一項產品要進行同步處理時，即使您並未選取全部產品，Configuration Manager 主控台也會顯示所有產品。 例如，您只選取 Windows Server 2012 產品。 如果軟體更新適用於 Windows Server 2012 和 Windows Server 2012 Datacenter Edition，則會在站台資料庫中提供兩種產品的軟體更新。  

請只在頂層站台上設定產品設定。 產品設定不會在子站台的軟體更新點上設定，因為軟體更新中繼資料是從頂層站台複寫而來。 所選的產品越多，花在同步軟體更新中繼資料的時間就越久。  

> [!IMPORTANT]  
>  Configuration Manager 會儲存一份產品和產品系列清單，您可以在第一次安裝軟體更新點時從中選擇。 在您完成同步處理之前，可能無法選取在 Configuration Manager 發行後發行的產品和產品系列。 同步處理程序會更新可供您選擇的可用產品和產品系列清單。 請在您第一次同步軟體更新之前清除所有產品。 在初始同步處理後，選取所需的產品，然後重新執行同步處理。  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a> 取代規則  

通常，取代其他軟體更新的軟體更新，會執行下列一個或多個動作：  

-   增強、改進或更新由一個或多個先前發行之更新所提供的修正程式。  

-   提升已取代更新檔案套件的效率，如果已核准安裝更新，則會將其安裝在用戶端上。 例如，已取代的更新可能包含與修正不再相關的檔案，或與新的更新支援的作業系統不再相關的檔案。 更新的取代檔案套件中不會包含這些檔案。  

-   更新較新版本的產品。 換句話說，它會更新不再適用於舊版本或產品設定的版本。 如果更新修改為擴充語言支援，更新也可以取代其他更新。 例如，Microsoft Office 的新版修訂版產品更新可能會移除對舊版 OS 的支援，但可能在初始更新版本中新增對新語言的其他支援。  

在軟體更新點內容中，指定已取代的軟體更新立即到期。 此設定可防止在新的部署中包含這些更新。 它也會標記現有的部署，指出其包含一或多個已到期的軟體更新。 或者，指定已取代的軟體更新經過多久以後到期。 此動作可讓您繼續進行部署。 

在您需要部署已取代的軟體更新時，考慮下列案例：  

-   取代的軟體更新只支援較新版本的 OS。 您的某些用戶端電腦執行的是舊版 OS。  

-   取代的軟體更新比其所取代的軟體更新的適用性更加受限。 此行為將不適用於某些用戶端。  

-   如果取代的軟體更新未獲核准部署在您的生產環境。  

    > [!NOTE]  
    > - 在 Configuration Manager 1806 版之前，當 Configuration Manager 將已取代的軟體更新設定為 [已到期]  時，它並不會在 WSUS 中將該更新設定為 [已拒絕]  。 用戶端會繼續掃描已到期的更新，直到更新以手動方式或透過自訂指令碼被拒絕。  在 Configuration Manager 1806 版之後，Configuration Manager 也會拒絕 WSUS 中已被取代的更新。 如需 WSUS 清除工作的詳細資訊，請參閱[軟體更新維護](../deploy-use/software-updates-maintenance.md)。
    > - 從 Configuration Manager 1810 版開始，您可分別指定**功能更新**與**與非功能更新**的取代規則行為。

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a> 語言  

軟體更新點的語言設定可讓您設定： 
- 哪些摘要詳細資料的語言 (軟體更新中繼資料) 要與軟體更新同步  
- 為軟體更新下載的軟體更新檔案語言  

#### <a name="software-update-file"></a>軟體更新檔案  
針對軟體更新點內容中的 [軟體更新檔案]  設定，設定語言。 此設定會在您於站台下載軟體更新時提供可用的預設語言。 您可以在每次下載或部署軟體更新時，修改預設選取的語言。 下載程序進行期間，如果有提供所選語言的軟體更新檔案，則會將已設定語言的軟體更新檔案下載到部署套件來源位置。 接著，將它們複製到站台伺服器的內容庫。 然後將它們發佈到針對套件所設定的發佈點。  

使用您環境中最常使用的語言來設定軟體更新檔案語言設定。 例如，您站台中的用戶端大部分會使用英文和日文版的 Windows 或應用程式。 該站台上很少使用其他語言。 當您下載或部署軟體更新時，請在 [軟體更新檔案]  欄位中只選取 [英文] 和 [日文]。 此動作可讓您在部署及下載精靈的 [語言選擇]  頁面中使用預設設定。 此動作也可避免下載不需要的更新檔案。 請在 Configuration Manager 階層中的各個軟體更新點設定此設定。  



#### <a name="summary-details"></a>摘要詳細資料  
進行同步處理程序期間，會使用您所指定的語言更新軟體更新的摘要詳細資訊 (軟體更新中繼資料)。 此中繼資料提供軟體更新的相關資訊，例如：
- Name
- 說明
- 更新支援的產品
- 更新分類
- 文章識別碼
- 下載 URL
- 適用性規則

請只在頂層站台上設定摘要詳細資料設定。 子站台上的軟體更新點並未設定摘要詳細資料，因為軟體更新中繼資料是使用以檔案為基礎的複寫從管理中心網站複寫而來。 當您選取摘要詳細資料語言時，請只選取您環境中所需的語言。 所選的語言越多，花在同步處理軟體更新中繼資料的時間就越久。 Configuration Manager 會以執行 Configuration Manager 主控台的 OS 地區設定，顯示軟體更新中繼資料。 如果 OS 的地區設定未提供軟體更新的當地語系化內容，則會顯示英文版的軟體更新資訊。  

> [!IMPORTANT]  
>  選取您需要的所有摘要詳細資料語言。 當頂層站台的軟體更新點與同步處理來源進行同步時，所選的摘要詳細資料語言會判斷所擷取的軟體更新中繼資料。 如果您在至少執行一次同步處理後修改摘要詳細資料語言，則只有在新的或更新的軟體更新時，才會擷取已修改之摘要詳細資料語言的軟體更新中繼資料。 除非在同步處理來源上變更軟體更新，否則已同步的軟體更新，不會使用已修改語言之新中繼資料進行更新。


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a>執行時間上限
<!--3734426-->
*(於 1906 版推出)*

從 1906 版開始，您可以指定時間上限，要求軟體更新安裝必須在這段時間內完成。 您可以為下列內容指定執行時間上限：

- **Windows 功能更新的執行時間上限 (分鐘)**
  - **功能更新** - 屬於以下三種分類中其中一種的更新：
    - 升級
    - 更新彙總套件
    - Service Pack

- **Office 365 更新與 Windows 非功能更新的執行時間上限 (分鐘數)**
  - **非功能更新** - 並非功能升級的更新，以及其產品已列為下列其中一項的更新：
    - Windows 10 (所有版本)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- 這些設定只會變更從 Microsoft Update 同步新更新的執行時間上限。 它不會變更現有功能或非功能更新的執行時間。
- 所有其他產品和分類都無法使用此設定進行設定。 若您需要變更這些更新中其中一項的執行時間上限，請[設定軟體更新設定](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings)

> [!NOTE]
> 在 1906 版中，當安裝頂層軟體更新點時，會無法使用執行階段上限。 安裝之後，請在最上層軟體更新點上編輯執行階段上限。

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a> 規劃軟體更新維護期間  

新增專用於軟體更新安裝的維護期間。 此動作可讓您設定一般的維護期間和用於軟體更新的不同維護期間。 當您同時設定一般的維護期間和軟體更新維護期間時，用戶端只會在軟體更新維護期間安裝軟體更新。 

從 Configuration Manager 1810 版開始，您可以變更此行為並允許軟體更新在一般維護期間安裝。 如需有關此用戶端設定的詳細資訊，請參閱[軟體更新用戶端設定](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)。

如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> 提供在安裝軟體更新後重新啟動 Windows 10 用戶端的選項

使用 Configuration Manager 部署及安裝需要重新啟動的軟體更新時，用戶端會排程擱置重新啟動，並顯示重新啟動對話方塊。

只要 Configuration Manager 軟體更新擱置重新啟動，處於 Windows 電源選項的 Windows 10 電腦上就會有 [更新並重新啟動]  和 [更新並關機]  選項。 使用其中一個選項之後，在電腦重新啟動之後不會顯示重新啟動對話方塊。 在某些情況下，作業系統可能會移除擱置的重新開機選項。 如果 Windows 10 中的快速啟動功能已啟用，就可能發生這種情況。 如需詳細資訊，請參閱[無法在 Windows 10 中使用快速啟動安裝更新](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup)。

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a> 在服務堆疊更新之後評估軟體更新
<!--4639943-->
從 2002 版開始，Configuration Manager 會偵測服務堆疊更新 (SSU) 是否為多個更新安裝的一部分。 偵測到 SSU 時，系統會先加以安裝。 在安裝 SSU 之後，會執行軟體更新評估週期以安裝剩餘的更新。 此變更允許在服務堆疊更新之後安裝相依的累積更新。 裝置不需要在安裝之間重新啟動，且不需要建立額外的維護時段。 系統只會針對非使用者起始的安裝優先安裝 SSU。 例如，如果使用者起始來自軟體中心的多個更新安裝，系統可能不會先安裝 SSU。


## <a name="next-steps"></a>後續步驟
一旦規劃軟體更新，請參閱 [Prepare for software updates management](../get-started/prepare-for-software-updates-management.md) (準備軟體更新管理)。  

如需管理 Windows 即服務的詳細資訊，請參閱 [Configuration Manager 即服務與 Windows 即服務的基本概念](../../core/understand/configuration-manager-and-windows-as-service.md)。
