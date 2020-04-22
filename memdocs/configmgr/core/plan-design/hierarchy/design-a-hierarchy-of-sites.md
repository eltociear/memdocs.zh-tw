---
title: 設計站台階層
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 可用的拓撲和管理選項，以規劃您的站台階層。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3c642e97589ff345e4eb3a17b63b3fdfbc2891f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703586"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>為 Configuration Manager 設計站台階層

適用於：  Configuration Manager (最新分支)

在安裝新 Configuration Manager 階層的第一個站台之前，最好了解：  

- Configuration Manager 可用的拓撲  

- 可用的站台類型及其彼此的關聯性  

- 每種站台類型提供的管理範圍  

- 可減少需要安裝之站台數目的內容管理選項  

然後規劃有效率地滿足您目前業務需求，並可於稍後擴充以管理未來成長的拓撲。  

規劃時，請留意將額外站台新增至階層或獨立站台的限制：  

- 在管理中心網站之下安裝新的主要站台，最多可達階層所[支援的主要站台數目](../configs/size-and-scale-numbers.md)。  

- [擴充獨立主要站台以安裝新的管理中心網站](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)，然後安裝額外的主要站台。  

- 在主要站台之下安裝新的次要站台，最多可達[主要站台的支援限制](../configs/size-and-scale-numbers.md)與整體階層的支援限制。  

- 您無法將先前安裝的站台新增至現有的階層來合併兩個獨立站台。 Configuration Manager 只支援將新的站台安裝到現有的站台階層。  


> [!NOTE]  
> 在規劃新的 Configuration Manager 安裝時，請注意[版本資訊](../../servers/deploy/install/release-notes.md)，其中詳細說明使用中版本的目前問題。 此版本資訊適用於 Configuration Manager 的所有分支。 當您使用 [Technical Preview 分支](../../get-started/technical-preview.md)時，您可以在每一版的 Technical Preview 文件中找到與該分支相關的問題。  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a> 階層拓樸  

階層拓撲範圍從：  

- 最簡單：單一獨立主要站台  

- 最複雜：一組已連線的主要和次要站台，其中管理中心網站是階層的最頂層站台  

您用於階層中之類型和站台計數的主要驅策因素，通常是您必須支援的裝置數目和類型。   

### <a name="standalone-primary-site"></a>獨立主要站台

當獨立主要站台可支援管理所有的裝置和使用者時，請使用此站台。 如需詳細資訊，請參閱[大小和縮放比例](../configs/size-and-scale-numbers.md)。 當貴公司的地理位置可由單一主要站台服務時，此拓撲也會成功。 若要協助管理網路流量，請使用界限群組中的多個管理點及仔細規劃過的內容基礎結構。 如需詳細資訊，請參閱[設定界限群組](../../servers/deploy/configure/boundary-groups.md)和[內容管理的基本概念](fundamental-concepts-for-content-management.md)。  

此拓撲提供下列優點：  

- 簡化管理負荷  

- 簡化用戶端站台指派及探索可用資源及服務  

- 消除站台間資料庫複寫所引起的可能延遲  

- 透過管理中心網站將獨立主要站台展開為較大階層的選項。 此選項可讓您稍後安裝新的主要站台，以擴展您的部署規模。  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>有一或多個子主要站台的管理中心網站 

當您需要多個主要站台以支援管理所有的裝置和使用者時，請使用此拓撲。 當您需要使用多個單一主要站台時所需。 

此拓撲提供下列優點：  

- 支援最多 25 個主要站台，讓您擴展階層的規模。    

- 除非您重新安裝站台，否則一律會使用管理中心網站。 這是永久性選項。 您無法中斷連結子主要站台以作為獨立主要站台。  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> 判斷何時要使用管理中心網站。  

使用管理中心網站設定全階層設定，並監視階層中的所有網站及物件。 此站台類型不會直接管理用戶端。 它會協調站台對站台的資料複寫，包括整個階層的站台和用戶端設定。  

使用下列資訊，協助您決定何時要安裝管理中心網站：  

- 管理中心網站是階層中的頂層站台。  

- 當您設定具有一個以上主要站台的階層時，請安裝管理中心網站。  

     - 如果您立即需要兩個或兩個以上的主要站台，請先安裝管理中心網站。  

     - 當您已經擁有主要站台，並想要接著安裝管理中心網站時，請[擴充獨立主要站台](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)以安裝管理中心網站。  

- 管理中心網站只支援使用主要站台作為子站台。  

- 管理中心網站自身則不能被指派任何用戶端。  

- 管理中心網站不支援直接支援用戶端的站台系統角色，例如管理點及發佈點。  

- 您可以從連線到管理中心網站的 Configuration Manager 主控台管理階層中的所有用戶端，並執行所有站台管理工作。 這些工作包括安裝管理點或在子主要或次要站台的其他站台系統角色。  

- 當您使用管理中心網站時，它是您唯一可以在階層中查看所有站台資料的位置。 此資料包括清查資料及狀態訊息等資訊。  

- 從管理中心網站設定整個階層的探索作業。 從管理中心網站，指派要在個別站台執行的探索方法。  

- 若要管理整個階層的安全性，請指派不同的安全性角色、安全性範圍與集合給不同的系統管理使用者。 這些設定可套用到階層中的各個站台。  

- 設定複寫以控制階層中各站台間的通訊。 排程站台資料的資料庫複寫，以及管理站台間檔案資料傳輸的頻寬。  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> 判斷何時使用主要站台。  

使用主要站台管理用戶端。 安裝主要站台，作為管理中心網站底下的子站台，或是作為新階層的第一個站台。 作為階層中第一個站台的主要站台會建立獨立主要站台。 子主要站台和獨立主要站台都支援次要站台。  

基於下列原因，請考慮新增額外的主要站台：  

- 若要增加裝置數目，請使用單一階層進行管理。  

- 符合組織的管理需求。 例如，您可能會在遠端位置安裝主要站台，以管理透過低頻寬網路傳送的部署內容。  

     - 將資料傳輸到發佈點時，請考慮改用網路頻寬節流的選項。 該項內容管理功能可以取代安裝其他站台的需求。  


下列資訊可協助您決定何時要安裝主要站台：  

- 主要站台可以是獨立主要站台或是較大階層中的子主要站台。 當主要站台是含管理中心網站之階層的成員時，站台會使用資料庫複寫在站台之間複寫資料。 除非您需要支援的用戶端和裝置數目超過單一主要站台支援的數目，否則請考慮安裝獨立主要站台。 安裝獨立主要站台之後，如果未來需要，請將它展開，以回報至新的管理中心網站來擴大部署的規模。  

- 主要站台僅支援使用管理中心網站作為父站台。  

- 主要站台僅支援使用次要站台作為子站台，而且支援多個次要站台。  

- 主要站台負責處理所指派用戶端的所有用戶端資料。  

- 主要站台使用資料庫複寫，直接與其管理中心網站進行通訊。 安裝新站台時會自動設定此行為。  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> 判斷何時使用次要站台。  

使用次要站台管理在低頻寬網路上部署內容與用戶端資料的傳輸。  

您可經由管理中心網站或次要站台的直接父主要站台來管理次要站台。 次要站台已連接到主要站台。 您無法在還未解除安裝的狀況下，將其移至不同的父站台，然後重新安裝為新主要站台下的子站台。

不過，您可以在兩個對等次要站台間路由內容，協助管理以檔案為基礎的部署內容複寫。 為將用戶端資料移轉到主要站台上，次要站台會使用以檔案為基礎的複寫。 次要站台也會使用資料庫複寫，以與其父主要站台進行通訊。  

若套用以下任何一種狀況，請考量安裝次要站台：  

- 您不需要有針對系統管理使用者的本機連線點。  

- 您必須管理將部署內容傳輸到階層中較低站台的作業。  

- 您必須管理傳送到階層中較高站台的用戶端資訊。  

如果您不想安裝次要站台，又有用戶端位於遠端位置，請考慮下列選項：  

- 使用 Windows BranchCache 等點對點技術  

- 啟用發佈點進行頻寬控制與排程   

搭配或不搭配次要站台，使用這些內容管理選項。 這有助於減少您的 Configuration Manager 基礎結構大小。 如需 Configuration Manager 中內容管理選項的詳細資訊，請參閱[判斷何時要使用內容管理選項](#BKMK_ChooseSecondaryorDP)。  


使用下列資訊，協助您決定何時要安裝次要站台：  

- 若沒有本機 SQL Server 執行個體可用，次要站台會在站台安裝期間自動安裝 SQL Server Express。  

- 安裝次要站台是從 Configuration Manager 主控台中起始，而不是直接在電腦上執行安裝程式。  

- 次要站台使用站台資料庫中資訊的子集。 此行為可減少父主要站台與次要站台間 SQL 所複寫的資料量。  

- 次要站台支援將以檔案為基礎的內容路由至有一般父主要站台的其他次要站台。  

- 安裝次要站台時會自動在次要站台伺服器上安裝管理點和發佈點站台系統角色。  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> 判斷何時要使用內容管理選項。  

如果您有用戶端位於遠端位置，請考慮使用一個或多個內容管理選項，不要使用主要或次要站台。 下列選項通常不需要安裝站台：  

- Windows 10 傳遞最佳化  

- Configuration Manager 對等快取  

- Windows BranchCache  

- 設定發佈點進行頻寬控制  

- 將內容手動複製到發佈點 (預先設置的內容)  


若適用以下任一狀況，請考慮部署發佈點，而不要安裝另一個站台：  

- 您的網路頻寬足以讓遠端位置的用戶端電腦與主要站台的管理點進行通訊。 用戶端會與管理點進行通訊，以下載用戶端原則、傳送清查、傳送報告狀態及傳送探索資訊。  

- 背景智慧型傳送服務 (BITS) 並不會為您的網路需求提供足夠的頻寬控制。  

如需 Configuration Manager 中內容管理選項的詳細資訊，請參閱[內容管理的基本概念](fundamental-concepts-for-content-management.md)。  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> 階層拓撲之外  

除了您的初始階層拓撲之外，也請考慮下列問題：  

- 階層中的不同站台有哪些站台系統角色提供服務或功能？  

- 如何管理您基礎結構中的階層範圍設定和功能？  


下列常見考量事項涵蓋在不同的文章中。 此資訊會影響階層設計或受到階層設計所影響，因此十分重要：  

- 當準備[管理電腦和裝置](../../clients/manage/manage-clients.md)時，請考量裝置是位於內部部署、雲端中還是包含使用者擁有的裝置 (BYOD)。 亦請考量您要如何管理受多種管理選項支援的裝置。 例如，使用 Configuration Manager 或透過與 Microsoft Intune 整合來管理 Windows 10 裝置。 如需詳細資訊，請參閱[選擇裝置管理解決方案](../choose-a-device-management-solution.md)。  

- 了解可用的網路基礎結構可能會如何影響遠端位置之間的資料流程。 如需詳細資訊，請參閱[準備您的網路環境](../network/configure-firewalls-ports-domains.md)。 也要考量您的使用者和裝置的地理位置，以及他們是透過您的內部部署網路或內部網路存取您的基礎結構。  

- 規劃內容基礎結構，以有效率地發佈您部署至所管理裝置的內容。 此內容可能是應用程式、軟體更新或作業系統。 如需詳細資訊，請參閱[管理內容與內容基礎結構](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

- 決定打算使用哪些 [Configuration Manager 的特性和功能](../changes/features-and-capabilities.md)。 不同功能需要不同的站台系統角色或 Windows 基礎結構。 在多個站台階層中，決定其部署位置以最有效率地使用網路和伺服器資源。  

- 考量資料和裝置的安全性，包括公開金鑰基礎結構 (PKI) 的使用。 如需詳細資訊，請參閱 [PKI 憑證需求](../network/pki-certificate-requirements.md)。  


檢閱下列站台特定設定的文章：  

- [規劃 SMS 提供者](plan-for-the-sms-provider.md)  

- [規劃站台資料庫](plan-for-the-site-database.md)  

- [規劃站台系統伺服器和站台系統角色](plan-for-site-system-servers-and-site-system-roles.md)  

- [規劃安全性](../security/plan-for-security.md)  

- 部署站台內的內容時[Managing network bandwidth](manage-network-bandwidth.md) 。  


請考量下列跨越站台和階層的設定  

- 站台和階層的[高可用性選項](../../servers/deploy/configure/high-availability-options.md)

- [擴充 Active Directory 架構](../network/extend-the-active-directory-schema.md)並設定站台以[發佈站台資料](../../servers/deploy/configure/publish-site-data.md)  

- [站台間的資料傳輸](data-transfers-between-sites.md)  

- [以角色為基礎的系統管理基本概念](../../understand/fundamentals-of-role-based-administration.md)  

- [管理網際網路上的用戶端](../../clients/manage/manage-clients-internet.md)  

