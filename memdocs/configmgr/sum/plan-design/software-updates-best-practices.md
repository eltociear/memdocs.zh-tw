---
title: 軟體更新的最佳作法
titleSuffix: Configuration Manager
description: 使用這些最佳做法在 Configuration Manager 中進行軟體更新。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: eb9a675970abb581a793208c73506e1e94cc6f63
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906694"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>在 Configuration Manager 中進行軟體更新的最佳做法

適用於：  Configuration Manager (最新分支)

本文包含在 Configuration Manager 中進行軟體更新的最佳做法。 該資訊會根據針對初始安裝和進行中操作的最佳做法進行排序。  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a> 安裝最佳做法  

當您在 Configuration Manager 中安裝軟體更新時，請使用下列最佳做法。  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a> 針對軟體更新點使用共用的 WSUS 資料庫  

當您在主要站台安裝一個以上的軟體更新點時，請在相同的 Active Directory 樹系中針對各軟體更新點使用相同的 WSUS 資料庫。 如果您共用相同資料庫，則當用戶端切換至新的軟體更新點時，可能會大幅度減輕，但不完全排除可能遭遇到的用戶端和網路效能影響。 當用戶端切換到與舊的軟體更新點共用資料庫的新軟體更新點時，仍會進行差異掃描，但此掃描遠低於 WSUS 伺服器自己擁有資料庫的情況。 如需切換軟體更新點的詳細資訊，請參閱[切換軟體更新點](plan-for-software-updates.md#BKMK_SUPSwitching)。  

> [!IMPORTANT]  
>  當您針對軟體更新點使用共用的 WSUS 資料庫時，請一併共用本機 WSUS 內容資料夾。  

如需共用 WSUS 資料庫的詳細資訊，請參閱下列部落格文章：  

- [How to implement a shared SUSDB for Configuration Manager software update points](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103) (如何為 Configuration Manager 軟體更新點實作共用的 SUSDB)  

- [使用 Configuration Manager 時，共用內容資料庫之多個 WSUS 執行個體的考量](https://docs.microsoft.com/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb) \(英文\)。


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a> 當 Configuration Manager 和 WSUS 使用相同的 SQL Server 時，請將其中一個設定為使用具名執行個體，並將另一個應用程式設定為使用預設的執行個體  

如果 Configuration Manager 和 WSUS 資料庫共用相同的 SQL Server 執行個體，您會很難在兩個應用程式間判斷資源使用情況。 為 Configuration Manager 和 WSUS 使用不同的 SQL Server 執行個體。 這項設定可讓您更輕鬆地疑難排解和診斷各個應用程式間可能發生的資源使用問題。  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a> 指定 [在本機存放更新] 設定  

當您安裝 WSUS 時，請選取 [在本機存放更新]  的設定。 此設定會使 WSUS 下載與軟體更新建立關聯的授權條款。 它會在同步處理期間下載條款，並將這些條款儲存在 WSUS 伺服器的本機硬碟上。 如果您未選取此設定，用戶端電腦可能無法通過具有授權條款之軟體更新的相容性掃描。 軟體更新點的 **WSUS 同步處理管理員**元件預設每隔 60 分鐘就會確認一次此設定。  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a> 操作的最佳做法  

當您使用軟體更新時，請使用下列最佳作法：  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a> 在單一軟體更新部署時，將軟體更新數目限制為 1000  

在各個軟體更新部署時，將軟體更新數目限制為 1000。 當您建立自動部署規則時，請確認指定的準則不會導致多於 1000 個軟體更新。 如果您手動部署軟體更新時，請勿選取多於 1000 個更新。  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a> 每一次針對「週二修補程式日」和一般部署執行 ADR 時，建立新的軟體更新群組  

部署中有 1000 個軟體更新的限制。 當您建立自動部署規則 (ADR) 時，可以指定每一次執行規則時，是要使用現有的更新群組，還是建立新的更新群組。 如果您在產生多個軟體更新的 ADR 中指定準則，並以週期性排程執行規則時，請在每次執行規則時建立新的軟體更新群組。 此行為可防止部署超過 1000 個軟體更新的每一部署限制。  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a> 使用 ADR 的現有軟體更新群組進行 Endpoint Protection 定義更新  

當您經常使用 ADR 部署 Endpoint Protection 定義更新時，請務必使用現有的軟體更新群組。 否則，在一段時間後，ADR 可能會建立數百個軟體更新群組。 定義更新發行者通常會將定義更新設定為在該更新由四個較新的更新所取代時到期。 因此，ADR 所建立的軟體更新群組，絕不會包含四個以上發行者的定義更新：一個使用中，三個已取代。  



## <a name="see-also"></a>另請參閱  
 [規劃軟體更新](plan-for-software-updates.md)
