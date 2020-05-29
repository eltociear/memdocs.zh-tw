---
title: 雲端發佈點
titleSuffix: Configuration Manager
description: 規劃和設計透過 Microsoft Azure 與 Configuration Manager 的雲端發佈點來發佈軟體內容。
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52c2b70d2b094d5a89d80aafa61f1db67a53816f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987709"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>使用 Configuration Manager 的雲端發佈點

適用於：Configuration Manager (最新分支)

> [!Important]  
> 從 Azure 共用內容的實作已經變更。 藉由啟用 [允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容] 選項，來使用啟用內容的雲端管理閘道。 如需詳細資訊，請參閱[修改 CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)。
>
> 未來您將無法建立傳統雲端發佈點。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)。

雲端發佈點是在 Microsoft Azure 中裝載為「平台即服務」(PaaS) 的 Configuration Manager 發佈點。 此服務支援下列案例：  

- 將軟體內容提供給以網際網路為基礎的用戶端，而不需要額外的內部部署基礎結構  

- 將內容發佈系統雲端化  

- 降低傳統發佈點的需求  

本文可協助您了解雲端發佈點、規劃其使用，以及設計您的實作。 它包含下列各節：

- [功能和優點](#bkmk_features)
- [拓撲設計](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [規格](#bkmk_spec)
- [成本](#bkmk_cost)
- [效能和調整](#bkmk_perf)
- [連接埠和資料流程](#bkmk_dataflow)
- [憑證](#bkmk_certs)
- [常見問題集 (FAQ)](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a> 功能和優點

### <a name="features"></a>功能

雲端發佈點支援幾項內部部署發佈點也提供的功能：  

- 個別管理雲端發佈點，或以發佈點群組的成員身分進行管理  

- 使用雲端發佈點作為後援內容位置  

- 支援以內部網路和網際網路為基礎的用戶端  

### <a name="benefits"></a>優點

雲端發佈點提供以下額外優勢：  

- 站台會加密內容，再於 Azure 中將它傳送至雲端發佈點。  

- 為了滿足用戶端對內容要求的不斷變化需求，請以手動方式在 Azure 中調整雲端服務。 此動作不需要您在 Configuration Manager 中安裝和佈建額外的發佈點。  

- 支援從針對其他內容技術所設定的用戶端下載的內容，例如 Windows BranchCache 和替代內容提供者。  

- 從 1806 版開始，使用雲端發佈點作為提取發佈點的來源位置。  


## <a name="topology-design"></a><a name="bkmk_topology"></a> 拓撲設計

雲端發佈點的部署和作業包括下列元件：  

- Azure 中的**雲端服務**。 站台會將內容發佈到此服務，而此服務則將它儲存在 Azure 雲端儲存體中。 管理點會視需要將可用來源清單中的此內容位置提供給用戶端。  

- **管理點**站台系統角色可以回應一般用戶端要求。  

    - 內部部署用戶端通常會使用內部部署管理點。  

    - 以網際網路為基礎的用戶端使用[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)或[以網際網路為基礎的管理點](../../clients/manage/plan-internet-based-client-management.md)。  

- 雲端發佈點會使用**以憑證為基礎的 HTTPS** Web 服務，以協助保護與用戶端之間的網路通訊。 用戶端必須信任此憑證。  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
從 1806 版開始，使用 **Azure Resource Manager 部署**來建立雲端發佈點。 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) 是可將所有解決方案資源當作單一實體 (稱為[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)) 來管理的新式平台。 使用 Azure Resource Manager 部署雲端發佈點時，站台會使用 Azure Active Directory (Azure AD) 來驗證並建立必要的雲端資源。 這個現代化的部署不需要傳統的 Azure 管理憑證。  

> [!Note]  
> 此功能不會啟用對 Azure 雲端服務提供者 (CSP) 的支援。 使用 Azure Resource Manager 的雲端發佈點部署會繼續使用 CSP 不支援的傳統雲端服務。 如需詳細資訊，請參閱 [Azure CSP 中可用的 Azure 服務](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  

從 Configuration Manager 1902 版開始，對於雲端發佈點的新執行個體，Azure Resource Manager 是唯一的部署機制。 現有的部署可繼續運作。<!-- 3605704 -->

在 Configuration Manager 1810 版和更早版本中，雲端發佈點精靈仍會使用 Azure 管理憑證來提供**傳統服務部署**的選項。 若要簡化資源的部署與管理，請針對所有新的雲端發佈點執行個體使用 Azure Resource Manager 部署模型。 如果可能，請透過 Resource Manager 重新部署現有的雲端發佈點執行個體。

> [!Important]  
> 從 1810 版開始，Azure 已淘汰傳統服務部署，不再供 Configuration Manager 使用。 這是支援建立這些 Azure 部署的最後版本。 此功能將會在未來的 Configuration Manager 版本中移除。<!--SCCMDocs-pr issue #2993-->  

Configuration Manager 不會將現有的傳統雲端發佈點移轉至 Azure Resource Manager 部署模型。 使用 Azure Resource Manager 部署來建立新的雲端發佈點，然後移除傳統雲端發佈點。

### <a name="hierarchy-design"></a>階層設計

您建立雲端發佈點的位置取決於哪些用戶端需要存取內容。 從 1806 版開始，有三種類型的雲端發佈點：  

- Azure Resource Manager 部署：在主要站台或管理中心網站建立此類型。  

- 傳統服務部署：只能在主要站台建立此類型。  

- 雲端管理閘道也可以提供內容給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。 如需詳細資訊，請參閱[規劃雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)。<!--1358651-->  

為了判斷是否要在界限群組中包含雲端發佈點，請考慮下列行為：  

- 以網際網路為基礎的用戶端不依賴界限群組。 它們只會使用網際網路對應發佈點或雲端發佈點。 如果您只使用雲端發佈點來服務這些類型的用戶端，則不需要將它們包含在界限群組中。  

- 如果您想要內部網路上的用戶端使用雲端發佈點，則它必須位於與用戶端相同的界限群組中。 用戶端將雲端發佈點的優先順序設定為其內容來源的最後一項，因為從 Azure 下載內容會產生相關聯的成本。 因此，雲端發佈點通常會作為以內部網路為基礎之用戶端的後援來源。 如果您想要雲端優先設計，則請設計您的界限群組，以符合此商務需求。 如需詳細資訊，請參閱[設定界限群組](../../servers/deploy/configure/boundary-groups.md)。  

即使您將雲端發佈點安裝在 Azure 的特定區域中，用戶端也不會察覺到 Azure 區域。 他們會隨機選取雲端發佈點。 如果您將雲端發佈點安裝在多個區域，而用戶端在內容位置清單中收到多個雲端發佈點，則用戶端可能不會使用同一個 Azure 區域中的雲端發佈點。  

### <a name="backup-and-recovery"></a>備份與復原  

在階層中使用雲端發佈點時，請使用下列資訊來協助您規劃備份或復原功能：  

- 當您使用**備份站台伺服器**維護工作，Configuration Manager 會自動包含雲端發佈點的設定。  

- 備份伺服器驗證憑證並儲存其複本。 如果您在 Azure 中使用傳統服務部署，也請備份 Azure 管理憑證並儲存其複本。 將 Configuration Manager 主要站台還原到不同的伺服器時，您必須重新匯入憑證。  


## <a name="requirements"></a><a name="bkmk_requirements"></a> 需求

- 您需要有 **Azure 訂用帳戶**才能裝置服務。  

    - 需要 **Azure 系統管理員**參與部分元件的初始建立 (視您的設計而定)。 此角色不需要 Configuration Manager 中的權限。  

- 站台伺服器需要**網際網路存取**來部署和管理雲端服務。  

- 使用 **Azure Resource Manager** 部署方法時，請將 Configuration Manager 與 [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) 整合於**雲端管理**。 不需要 Azure AD 「使用者探索」。  

- **伺服器驗證憑證**。 如需詳細資訊，請參閱下面的[憑證](#bkmk_certs)一節。  

    - 為了降低複雜性，請針對伺服器驗證憑證使用公開憑證提供者。 當您這麼做時，也需要用戶端的 **DNS CNAME 別名**來解析雲端服務的名稱。  

- 在 Configuration Manager 1810 版或更早版本中，如果使用 Azure 傳統部署方法，您需要 **Azure 管理憑證**。 如需詳細資訊，請參閱下面的[憑證](#bkmk_certs)一節。  

    > [!TIP]  
    > 從 Configuration Manager 1806 版開始，使用 **Azure Resource Manager** 部署模型。 它並不需要此管理憑證。  
    >
    > 自 1810 版開始淘汰傳統部署方法。  

- 將 [雲端服務] 群組中的用戶端設定 [允許存取雲端發佈點] 設為 [是]。 根據預設，此值是設為 [否] 。  

- 用戶端裝置需要**網際網路連線能力**，而且必須使用 **IPv4**。  


## <a name="specifications"></a><a name="bkmk_spec"></a> 規格

- 雲端發佈點支援[用戶端和裝置支援的作業系統](../configs/supported-operating-systems-for-clients-and-devices.md)中列出的所有 Windows 版本。  

- 系統管理員會發佈下列類型的支援軟體內容：  
  - 應用程式
  - 套件
  - OS 升級套件
  - 協力廠商軟體更新  

    > [!Important]  
    > - 雖然 Configuration Manager 主控台不會封鎖將 Microsoft 軟體更新發佈到雲端發佈點的作業，但您需要支付 Azure 成本來儲存用戶端未使用的內容。 以網際網路為基礎的用戶端一律會從 Microsoft Update 雲端服務取得 Microsoft 軟體更新內容。 請勿將 Microsoft 軟體更新發佈到雲端發佈點。
    > - 使用 CMG 來儲存內容時，如果已啟用 [Download delta content when available] \(在提供差異內容時下載\) 的[用戶端設定](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)，協力廠商更新的內容就不會下載至用戶端。 <!--6598587--> 

- 從 1806 版開始，設定提取發佈點以使用雲端發佈點作為來源。 如需詳細資訊，請參閱[關於來源發佈點](use-a-pull-distribution-point.md#about-source-distribution-points)。<!--1321554-->  

### <a name="deployment-settings"></a>部署設定

- **視執行工作順序所需，將內容下載到本機**。 從 1910 版開始，工作順序引擎就可以從已啟用內容的 CMG 或雲端發佈點下載套件。 此變更為您的 Windows 10 就地升級部署提供額外的彈性，現在支援範圍擴大到以網際網路為基礎的裝置。

- **啟動工作順序之前下載所有內容到本機**。 在 Configuration Manager 1906 版和更早版本中，其他選項 (例如**視執行工作順序所需，將內容下載到本機**) 在此案例中無法運作。 工作順序引擎無法從雲端來源下載內容。 Configuration Manager 用戶端必須先從雲端來源下載內容，才能啟動工作順序。 如有需要，您仍然可以在 1910 版中使用此選項，以符合您的需求。

- 雲端發佈點不支援使用 [從發佈點執行程式] 選項的套件部署。 請使用 [從發佈點下載內容並在本機執行] 部署選項。  

### <a name="limitations"></a>限制  

- 您無法將雲端發佈點用於 PXE 或啟用多點傳送的部署。  

- 雲端發佈點不支援 App-V 串流應用程式。  

- 您無法在雲端發佈點上[預先設置內容](manage-network-bandwidth.md#BKMK_PrestagingContent)。 管理雲端發佈點的主要站台發佈管理員會轉送所有內容。  

- 您無法將雲端發佈點設定為提取發佈點。  


## <a name="cost"></a><a name="bkmk_cost"></a> 成本

<!--501018-->
> [!IMPORTANT]  
> 下面的成本資訊僅供評估之用。 您的環境可能有其他變數會影響使用雲端發佈點的總成本。  

Configuration Manager 包含下列可協助控制成本及監視資料存取的選項：  

- 控制及監視儲存於雲端服務中的內容量。 如需詳細資訊，請參閱[監視雲端發佈點](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)。  

- 設定 Configuration Manager 在用戶端下載的閾值達到或超過每月限制時，向您發出警示。 如需詳細資訊，請參閱[資料轉送閾值警示](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts)。

- 為了協助減少用戶端從雲端發佈點轉送的資料量，請使用下列其中一項對等快取技術：  
  - Configuration Manager 對等快取
  - Windows BranchCache
  - Windows 10 傳遞最佳化  

    如需詳細資訊，請參閱[內容管理的基本概念](fundamental-concepts-for-content-management.md)。  

### <a name="components"></a>元件

雲端發佈點會使用下列 Azure 元件，並會針對 Azure 訂用帳戶產生費用：  

> [!Tip]  
> 從 1806 版開始，雲端管理閘道也可以提供內容給用戶端。 這項功能會透過合併 Azure VM 來降低成本。 如需詳細資訊，請參閱[雲端管理閘道的成本](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost)。  

#### <a name="virtual-machine"></a>虛擬機器

- 雲端發佈點使用 Azure 雲端服務作為平台即服務 (PaaS)。 此服務使用會產生計算成本的虛擬機器 (VM)。  

- 每個雲端發佈點服務會使用兩個標準 A0 VM。  

- 請參閱 [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/)以利判斷潛在成本。

    > [!NOTE]  
    > 虛擬機器的成本隨地區而異。

#### <a name="outbound-data-transfer"></a>輸出資料傳輸

- 流入 Azure 的所有資料流程皆為免費 (輸入或上傳)。 從站台發佈至雲端發佈點的內容將上傳至 Azure。  

- 費用是根據自 Azure 流出 (輸出或下載) 的資料而定。 從 Azure 流出的雲端發佈點資料流程包含用戶端下載的軟體內容。  

- 如需詳細資訊，請參閱[監視雲端發佈點](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)。  

- 請參閱 [Azure 頻寬定價詳細資料](https://azure.microsoft.com/pricing/details/bandwidth/)以利判斷潛在成本。 資料傳輸的訂價為階層式。 使用的量越多，每 GB 的價格便越低。  

#### <a name="content-storage"></a>內容儲存體

- 以網際網路為基礎的用戶端能從 Microsoft Update 雲端服務免費取得 Microsoft 軟體更新內容。 請勿將含有 Microsoft 軟體更新的軟體更新部署套件發佈到雲端發佈點。 否則，針對用戶端永遠不會使用的內容，將會產生資料儲存體成本。  

- 根據部署模型而定，雲端發佈點會使用下列標準 Blob 儲存體：  

    - Azure Resource Manager 部署會使用 Azure 本地備援儲存體 (LRS)。 這項變更可降低儲存體帳戶的成本。 傳統部署沒有使用額外的 GRS 功能。 如需詳細資訊，請參閱[本地備援儲存體](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs) \(部分機器翻譯\)。  

    - 具有 Configuration Manager 1810 版或更早版本的傳統部署會使用 Azure 異地備援儲存體 (GRS)。 如需詳細資訊，請參閱[異地備援儲存體](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs)。  

#### <a name="other-costs"></a>其他成本

- 每個雲端服務都具有動態 IP 位址。 每個不同的雲端發佈點會使用新的動態 IP 位址。 針對每個雲端服務新增額外的 VM 將不會增加這些位址。  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a> 連接埠和資料流程

雲端發佈點有兩個主要的資料流程：  

- 站台伺服器連線到 Azure 以設定雲端發佈點服務  

- 用戶端連線到雲端發佈點以下載內容  

### <a name="site-server-to-azure"></a>站台伺服器至 Azure

您不需要針對內部部署網路開啟任何輸入連接埠。 站台伺服器會起始與 Azure 和雲端發佈點的所有通訊，來部署、更新和管理雲端服務。 站台伺服器需要建立對 Microsoft 雲端的輸出連線。 這個動作等同於將發佈點網站系統角色安裝至特定網站。  

### <a name="client-to-cloud-distribution-point"></a>用戶端至雲端發佈點

您不需要針對內部部署網路開啟任何輸入連接埠。 以網際網路為基礎的用戶端直接與 Azure 服務進行通訊。 內部網路上使用雲端發佈點的用戶端需要連線至 Microsoft 雲端。

如需內容位置優先順序和以內部網路為基礎的用戶端何時使用雲端發佈點的詳細資訊，請參閱[內容來源優先順序](fundamental-concepts-for-content-management.md#content-source-priority)。

用戶端使用雲端發佈點作為內容位置時：  

1. 管理點為用戶端提供存取權杖，以及內容來源清單。 此權杖的有效時間為 24 小時，可讓用戶端存取雲端發佈點。  

2. 管理點使用雲端發佈點的**服務 FQDN** 來回應用戶端的位置要求。 這個內容與伺服器驗證憑證的一般名稱相同。  

    如果您使用網域名稱 (例如 WallaceFalls.contoso.com)，則用戶端會先嘗試解析此 FQDN。 您需要有網域之網際網路對應 DNS 的 CNAME 別名，以供用戶端解析 Azure 服務名稱，例如：WallaceFalls.cloudapp.net。  

3. 用戶端接著會將 Azure 服務名稱 (例如 WallaceFalls.cloudapp.net) 解析為有效的 IP 位址。 這個回應應該由 Azure 的 DNS 處理。  

4. 用戶端連線到雲端發佈點。 Azure 針對其中一個 VM 執行個體的連線進行負載平衡。 用戶端使用存取權杖驗證其本身。  

5. 雲端發佈點驗證用戶端的存取權杖，，然後為用戶端提供 Azure 儲存體中的確切內容位置。  

6. 如果用戶端信任雲端發佈點的伺服器驗證憑證，它會連線到 Azure 儲存體以下載內容。


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a> 效能和調整

<!--494872-->

如同任何發佈點設計，請考慮下列因素：  

- 同時用戶端連線的數目上限
- 用戶端下載的內容大小
- 符合業務需求的所允許時間長度

根據您的[拓樸設計](#bkmk_topology)而定，如果用戶端可以為任何指定的內容選擇多個雲端發佈點，它們自然會在這些雲端服務中隨機設定。 如果您只將內容的某些部分發佈到單一雲端發佈點，而且大量的用戶端嘗試同時下載此內容，這個活動會對該單一雲端發佈點施加更高的負載。 新增額外的雲端發佈點也包含個別的 Azure 儲存體服務。 如需用戶端如何與雲端發佈點元件通訊和下載內容的詳細資訊，請參閱[連接埠和資料流程](#bkmk_dataflow)。  

雲端發佈點使用兩個 Azure VM 作為 Azure 儲存體的前端。 這個預設部署可滿足大部分客戶的需求。 在某些極端的情況下，由於含有大量的同時用戶端連線 (例如，150,000 個用戶端)，Azure VM 的處理產能無法跟上用戶端要求。 您無法調整用於雲端發佈點的 Azure VM 大小。 雖然您無法為 Configuration Manager 中的雲端發佈點設定 VM 執行個體的數目，但如有必要，請在 Azure 入口網站中重新設定雲端服務。 請手動新增更多的 VM 執行個體，或將服務設定為自動調整。

> [!Important]  
> 當您更新 Configuration Manager 時，站台會重新部署雲端服務。 如果您以手動方式在 Azure 入口網站中重新設定雲端服務，執行個體的數目就會重設為預設值 2。  

Azure 儲存體服務支援單一檔案每秒 500 個要求。 單一雲端發佈點的效能測試支援在 24 小時內將 100-MB 的單一檔案發佈到 50,000 個用戶端。<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a> 憑證  

根據雲端發佈點的設計而定，您需要一或多個數位憑證。  

### <a name="general-information"></a>一般資訊

<!--SCCMDocs issue #779-->
雲端發佈點的憑證支援下列設定：  

- 4096 位元金鑰長度

- 第 3 版憑證。 如需詳細資訊，請參閱 [CNG 憑證概觀](../network/cng-certificates-overview.md)。  

- 從 1802 版開始，當您使用下列原則設定 Windows 時：**系統密碼編譯：使用 FIPS 相容演算法進行加密、雜湊及簽署**  

- 從 1802 版開始，支援 TLS 1.2。 如需詳細資訊，請參閱[密碼編譯控制項技術參考](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities)。  

### <a name="server-authentication-certificate"></a>伺服器驗證憑證

所有雲端發佈點部署都需要此憑證。

如需詳細資訊，請參閱 [CMG 伺服器驗證憑證](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)，並視需要參閱下列子章節：  

- 用戶端的 CMG 受信任的根憑證
- 公用提供者所發出的伺服器驗證憑證
- 企業 PKI 所發出的伺服器驗證憑證

雲端發佈點使用此類型憑證的方式與雲端管理閘道相同。 用戶端也必須信任此憑證。 為了降低複雜性，Microsoft 建議使用公用提供者所發出的憑證。

除非您使用萬用字元憑證，否則請勿重複使用相同的憑證。 雲端發佈點和雲端管理閘道的每個執行個體都需要唯一的伺服器驗證憑證。

如需如何從 PKI 建立此憑證的詳細資訊，請參閱[部署雲端發佈點的服務憑證](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)。  

### <a name="azure-management-certificate"></a>Azure 管理憑證

*傳統服務部署需要此憑證。Azure Resource Manager 部署則不需要。*

> [!Important]  
> 從 Configuration Manager 1806 版開始，使用 **Azure Resource Manager** 部署模型。 它並不需要此管理憑證。  
>
> 自 1810 版開始淘汰傳統部署方法。  
>
> 從 Configuration Manager 1902 版開始，對於雲端發佈點的新執行個體，Azure Resource Manager 是唯一的部署機制。 Configuration Manager 1902 版或更新版本中不需要此憑證。<!-- 3605704 -->

如果搭配 Configuration Manager 1810 版或更早版本使用 Azure 傳統部署方法，您需要 **Azure 管理憑證**。 如需詳細資訊，請參閱雲端管理閘道憑證文章的 [Azure 管理憑證](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt)一節。 Configuration Manager 站台伺服器會使用此憑證向 Azure 進行驗證，以建立和管理傳統部署。  

為了降低複雜性，請在所有 Azure 訂用帳戶和所有 Configuration Manager 站台中，針對雲端發佈點和雲端管理閘道的所有傳統部署，使用相同的 Azure 管理憑證。


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> 常見問題集 (FAQ)

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>用戶端是否需要憑證才能從雲端發佈點下載內容？

不需要用戶端驗證憑證。 但用戶端確實必須信任雲端發佈點所使用的伺服器驗證憑證。 如果此憑證由公開憑證提供者發行，則大部分的 Windows 裝置已包含這些提供者的受信任根憑證。 如果您已從貴組織的 PKI 發行伺服器驗證憑證，您的用戶端必須信任整個鏈結中的發行憑證。 此鏈結包含根憑證授權單位和任何中繼憑證授權單位。 根據您的 PKI 設計而定，此憑證會為雲端發佈點的部署帶來額外的複雜性。 為了避免這種複雜性，Microsoft 建議使用用戶端已信任的公開憑證提供者。  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>我的內部部署用戶端可以使用雲端發佈點嗎？

是。 如果您想要內部網路上的用戶端使用雲端發佈點，則它必須位於與用戶端相同的界限群組中。 用戶端將雲端發佈點的優先順序設定為其內容來源的最後一項，因為從 Azure 下載內容會產生相關聯的成本。 因此，雲端發佈點通常會作為以內部網路為基礎之用戶端的後援來源。 如果您想要雲端優先設計，則請據此設計您的界限群組。 如需詳細資訊，請參閱[設定界限群組](../../servers/deploy/configure/boundary-groups.md)。  

### <a name="do-i-need-azure-expressroute"></a>我需要 Azure ExpressRoute 嗎？

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 可讓您將內部部署網路擴充到 Microsoft 的雲端。 Configuration Manager 雲端發佈點並不需要 ExpressRoute 或其他這類虛擬網路連線。  

如果您的組織使用 ExpressRoute，請隔離雲端發佈點的 Azure 訂用帳戶與使用 ExpressRoute 的訂用帳戶。 此設定可確保雲端發佈點不會以這種方式意外連線。  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>我需要維護 Azure 虛擬機器嗎？

不需要任何維護。 雲端發佈點的設計使用 Azure 平台即服務 (PaaS)。 使用您提供的訂用帳戶，Configuration Manager 會建立必要的 VM、儲存體和網路功能。 Azure 會保護並更新虛擬機器。 這些 VM 不屬於您的內部部署環境，在此情況下是基礎結構即服務 (IaaS)。 雲端發佈點是將您的 Configuration Manager 環境延伸到雲端的 PaaS。 如需詳細資訊，請參閱 [PaaS 雲端服務模型的安全性優點](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model)。  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>雲端發佈點是否使用 Azure CDN？

Azure 內容傳遞網路 (CDN) 是一種全球解決方案，透過在世界各地策略性放置的實體節點上快取內容，可迅速地傳遞高頻寬內容。 如需詳細資訊，請參閱[什麼是 Azure CDN？](https://docs.microsoft.com/azure/cdn/cdn-overview)。

Configuration Manager 雲端發佈點目前不支援 Azure CDN。


## <a name="next-steps"></a>後續步驟

[安裝雲端發佈點](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
