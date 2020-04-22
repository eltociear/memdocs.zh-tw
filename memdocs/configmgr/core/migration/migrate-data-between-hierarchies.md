---
title: 移轉資料
titleSuffix: Configuration Manager
description: 了解如何將資料從來源階層傳送至 Configuration Manager 目的地階層。
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701746"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>在 Configuration Manager 階層間移轉資料

適用於：  Configuration Manager (最新分支)

使用移轉，將資料從所支援來源階層傳送至您的 Configuration Manager (最新分支) 目的地階層。 當您從來源階層移轉資料時︰  

- 您會從來源基礎結構中的站台資料庫存取資料，然後將該資料傳送到目前的環境。  

- 移轉不會變更來源階層中的資料。 相反地，它會探索資料並將複本儲存在目的地階層的資料庫中。  

在規劃移轉策略時，請考慮下列幾點：  

- 您可以將現有 Configuration Manager 2007 SP2 基礎結構移轉至 Configuration Manager (最新分支)。  

- 您可以從來源站台移轉部分或所有支援的資料。  

- 您可以從單一來源站台將資料移轉至目的地階層中數個不同的站台。  

- 您可以將資料從多個來源站台移至目的地階層中的單一站台。  


下列影片討論並示範兩個常見的[移轉案例](#BKMK_MigrationScenarios)。 它也包含在移轉計劃中納入 Microsoft Azure 的選項。
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a> 概念  

 Configuration Manager 在移轉期間會使用下列概念和字詞。  

#### <a name="source-hierarchy"></a>來源階層
此階層會執行 Configuration Manager 的受支援版本，並包含您想要移轉的資料。 當您設定移轉時，會在指定來源階層的頂層站台時識別來源階層。 指定來源階層後，目的地階層的底層站台會從指定來源站台的資料庫收集資料，以識別您可以移轉的資料。 

如需詳細資訊，請參閱[來源階層](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies)。

#### <a name="source-sites"></a>來源站台
來源階層中的站台，可以讓您用來將資料移轉到目的地階層。 

如需詳細資訊，請參閱[來源站台](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites)。

#### <a name="destination-hierarchy"></a>目的地階層
Configuration Manager (最新分支) 階層，是為了從來源階層匯入資料而執行移轉的位置。

#### <a name="data-gathering"></a>資料收集
正在進行對來源階層的識別程序，此來源階層可以移轉到目的地階層。 Configuration Manager 會依排程檢查來源階層。 此程序會識別來源階層中您之前已移轉的資訊有無任何變化，同時也會識別在目的地階層中您可能想要更新的資訊。

如需詳細資訊，請參閱[資料收集](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)。

#### <a name="migration-jobs"></a>移轉作業
設定移轉特定物件，然後管理將這些物件移轉至目的地階層的程序。

如需詳細資訊，請參閱[規劃移轉作業策略](planning-a-migration-job-strategy.md)。

#### <a name="client-migration"></a>用戶端移轉
從來源站台的資料庫將用戶端使用的資訊傳送到目的地階層資料庫的程序。 此資料移轉後隨即會將裝置上用戶端軟體升級為目的地階層的用戶端軟體版本。

如需詳細資訊，請參閱[規劃用戶端移轉策略](planning-a-client-migration-strategy.md)。

#### <a name="shared-distribution-points"></a>共用發佈點
在移轉期間，來源階層中 Configuration Manager 與目的地階層共用的發佈點。

在移轉期間，指派至目的地階層之站台的用戶端可以透過共用發佈點取得資訊。

如需詳細資訊，請參閱[在來源和目的地階層之間共用發佈點](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)。

#### <a name="monitoring-migration"></a>監視移轉
監視移轉活動的程序。 您可以在 [系統管理]  工作區的 [移轉]  節點監視移轉進度和成功與否。

如需詳細資訊，請參閱[規劃監視移轉活動](planning-to-monitor-migration-activity.md)。

#### <a name="stop-gathering-data"></a>停止收集資料
停止從來源站台收集資料的程序。 當您不再需要從來源階層移轉資料，或者想要暫停進行移轉相關活動時，可以將目的地階層設定為停止從來源階層收集資料。

如需詳細資訊，請參閱[資料收集](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)。

#### <a name="clean-up-migration-data"></a>清除移轉資料
移除從目的地階層資料庫移轉的相關資訊，以完成從來源階層進行移轉的程序。

如需詳細資訊，請參閱[規劃完成移轉](planning-to-complete-migration.md)。



## <a name="typical-workflow"></a>一般工作流程  

設定移轉的工作流程：

1.  指定受支援的來源階層。  

2.  設定資料收集。 資料收集可讓 Configuration Manager 收集可從來源階層移轉之資料的相關資訊。  

     在您停止資料收集程序之前，Configuration Manager 會自動按照簡單的排程重複資料收集程序。 根據預設，資料收集程序每四小時重複一次，以便 Configuration Manager 能夠在來源階層中識別資料有何變化。 共用發佈點也需要進行資料收集。  

3.  建立移轉作業，在來源和目的地階層之間移轉資料。  

4.  您隨時可以使用 [停止收集資料]  動作來停止資料收集程序。 停止收集資料時，Configuration Manager 不會再識別來源階層中的資料有何變化，也不能再共用發佈點。 通常，當您不想再移轉資料或共用來源階層的發佈點時，就可以使用此動作。  

5.  來源階層中所有站台的資料收集皆停止後，您可以選擇使用 [清除移轉資料]  動作來清除移轉資料。 這個動作會從目的地階層的資料庫中刪除從來源階層進行移轉的相關歷程資料。  

移轉資料之後，不再需要來源階層來管理環境中的裝置，您可以解除委任該來源階層和基礎結構。  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a> 案例  

 Configuration Manager 支援下列移轉案例：
- [從 Configuration Manager 2007 階層移轉](#bkmk_2007)  
- [從 Configuration Manager 2012 或其他 Configuration Manager 階層移轉](#bkmk_2012)

> [!NOTE]  
>  將包含獨立站台的階層擴充為包含管理中心網站的階層並不屬於移轉。 如需階層擴充的資訊，請參閱[擴充獨立主要站台](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)。  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a> 從 Configuration Manager 2007 階層移轉  

 當您使用移轉功能從 Configuration Manager 2007 移轉資料時，可以將投資保留在現有的站台基礎結構中，並且獲得下列優勢：  

#### <a name="site-database-improvements"></a>站台資料庫的改善
Configuration Manager (最新分支) 資料庫支援完整 Unicode。

#### <a name="database-replication-between-sites"></a>站台間的資料庫複寫
Configuration Manager (最新分支) 中的複寫是以 Microsoft SQL Server 為基礎。 此行為能改善站對站資料傳送的效能。

#### <a name="user-centric-management"></a>使用者為中心的管理
使用者聚焦於 Configuration Manager (最新分支) 中的管理工作。 例如，即使不知道使用者的裝置名稱，您仍然可以將軟體發佈給該使用者。 此外，Configuration Manager 讓使用者能夠進一步控制要將哪些軟體安裝在其裝置上，以及安裝軟體的時間。

#### <a name="hierarchy-simplification"></a>階層簡化
Configuration Manager (最新分支) 可讓您建置簡單的站台階層。 這項改善是由於引進了管理中心網站類型及主要和次要站台的行為變更所致。 相較於舊版本，Configuration Manager (最新分支) 會使用較少的網路頻寬，而且需要較少的伺服器。

#### <a name="role-based-administration"></a>以角色為基礎的系統管理
Configuration Manager (最新分支) 採用的這種中央安全性模式可用於根據您的系統管理及商務需求提供全階層的防護及管理。

> [!NOTE]  
>  因為 System Center 2012 Configuration Manager 中第一次引進的設計變更，所以您無法將 Configuration Manager 2007 升級至 Configuration Manager (最新分支)。 支援從 System Center 2012 Configuration Manager 就地升級至 Configuration Manager (最新分支)。  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a> 從 Configuration Manager 2012 或其他 Configuration Manager 階層移轉  
 從 System Center 2012 Configuration Manager 或 Configuration Manager 階層移轉資料的程序相同。 此程序包括將資料從多個來源階層移轉至單一目的地階層。 當公司取得已經由 Configuration Manager 管理的其他資源時，您可以使用此程序。 此外，您可以將資料從測試環境移轉至 Configuration Manager 生產環境。 此程序可讓您將投資保存在 Configuration Manager 測試環境中。  



## <a name="see-also"></a>請參閱  

-   [規劃移轉至 Configuration Manager](planning-for-migration.md)  

-   [設定移轉的來源階層和來源站台](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [移轉的作業](operations-for-migration.md)  

-   [移轉的安全性和隱私權](security-and-privacy-for-migration.md)  

-   [開始使用 Configuration Manager](../servers/deploy/start-using.md)
