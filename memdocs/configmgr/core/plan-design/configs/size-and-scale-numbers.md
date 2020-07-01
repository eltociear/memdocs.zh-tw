---
title: 大小和縮放比例
titleSuffix: Configuration Manager
description: 判斷您的環境中支援裝置所需的站台系統角色和站台數目。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5109ababd00011784618f9c989e1d2b756a322d9
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715623"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Configuration Manager 的大小和縮放數字

適用於：Configuration Manager (最新分支)

每個 Configuration Manager 部署都有可支援的站台、站台系統角色和裝置數目上限。 這些數目會根據您的階層結構、使用的站台類型和數目，以及部署的站台系統角色而不同。 本文中的資訊可協助您判斷支援您預期管理之裝置所需的站台系統角色和站台數目。

如需詳細資訊，請參閱下列文章：

- [建議的硬體](recommended-hardware.md)
- [支援的站台系統伺服器作業系統](supported-operating-systems-for-site-system-servers.md)  
- [用戶端和裝置的支援作業系統](supported-operating-systems-for-clients-and-devices.md)
- [站台和站台系統必要條件](site-and-site-system-prerequisites.md)

這些支援數目是以適用於 Configuration Manager 的建議硬體為基礎。 它們也會以所有可用的 Configuration Manager 功能預設設定為依據。 若您未使用建議的硬體，或使用更積極的自訂設定，可能會降低站台系統的效能。 站台系統可能不會符合指定的支援層級 (以下為其中一個更積極的用戶端設定範例：執行硬體或軟體清查的頻率高於每隔七天一次的預設值)。

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a> 站台類型  

### <a name="central-administration-site"></a>管理中心網站  

- 管理中心網站可支援最多 25 個子主要站台。  

### <a name="primary-site"></a>主要網站  

- 每一個主要站台可支援最多 250 個次要站台。  

- 每個主要站台的次要站台數目是根據持續連線且可靠的廣域網路 (WAN) 連線。 若為具有少於 500 個用戶端的位置，請考慮發佈點，而不是次要站台。  

  如需主要站台可支援之用戶端和裝置數目的相關資訊，請參閱[站台和階層的用戶端數目](#bkmk_clientnumbers)。  

### <a name="secondary-site"></a>次要網站  

- 次要站台不支援子站台。  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Site system roles

### <a name="application-catalog-web-service-point"></a>應用程式類別目錄 Web 服務點  

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- 您可以在主要站台安裝應用程式類別目錄 Web 服務點的多個執行個體。  

### <a name="application-catalog-website-point"></a>應用程式類別目錄網站點  

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- 您可以在主要站台安裝應用程式類別目錄網站點的多個執行個體。  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a> 雲端管理閘道

- 您可以在主要站台或管理中心網站安裝雲端管理閘道 (CMG) 的多個執行個體。  

    > [!Tip]  
    > 在階層中，於管理中心網站上建立 CMG。  

  - 在 Azure 雲端服務中，一個 CMG 支援一到 16 個虛擬機器 (VM) 執行個體。  

  - 每個 CMG VM 執行個體均可支援 6,000 個同時用戶端連線。 當 CMG 因用戶端數目超過支援上限而處於高負載狀態下時，它仍然會處理要求，但可能會出現延遲的情形。  

如需詳細資訊，請參閱 CMG [效能和擴充](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)。

### <a name="cloud-management-gateway-connection-point"></a>雲端管理閘道連接點

- 您可以在主要站台安裝 CMG 連接點的多個執行個體。  

- 一個 CMG 連接點可支援一個最多含四個 VM 執行個體的 CMG。 如果 CMG 有四個以上的 VM 執行個體，請新增第二個 CMG 連接點以進行負載平衡。 含 16 個 VM 執行個體的 CMG，就應該連結四個 CMG 連接點。

如需詳細資訊，請參閱 CMG [效能和擴充](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)。

> [!NOTE]
> 在考量 CMG 連接點的硬體需求時，請參閱[遠端站台系統伺服器的建議硬體](recommended-hardware.md#bkmk_RemoteSiteSystem)。<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>發佈點  

- 每個站台的發佈點：  

  - 每個主要和次要站台支援最多 250 個發佈點。  

  - 每個主要和次要站台支援最多 2000 個其他設定為提取發佈點的發佈點。 **例如**，當 2000 個發佈點設定為提取發佈點時，單一主要站台可支援 2250 個發佈點。  

  - 每個發佈點支援最多 4,000 個用戶端連線。  

  - 提取發佈點在存取來自來源發佈點的內容時，行為類似用戶端。  

- 每個主要站台支援最多合併總計 5,000 個發佈點。 這個總數包含在主要站台的所有發佈點，以及主要站台所屬子次要站台的所有發佈點。  

- 每個發佈點支援最多合併總計 10,000 個封裝和應用程式。  

> [!WARNING]  
> 一個發佈點可支援的用戶端實際數目，取決於網路速度和伺服器的硬體設定。  
>
> 一個來源發佈點可支援的提取發佈點數目，同樣取決於網路速度和來源發佈點的硬體設定。 但此數目也受到您已部署的內容量影響。 產生這種影響的原因在於，不同於用戶端通常會在部署期間的不同時間存取內容，所有的提取發佈點都會在同一時間要求內容。 提取發佈點可以要求所有可用內容，而不只它們適用的內容。 當您在來源發佈點放置高處理負載時，將內容發佈到目標發佈點時可能會產生無法預期的延遲。  

### <a name="fallback-status-point"></a>後援狀態點  

- 每個後援狀態點最多可以支援 100,000 個用戶端。  

### <a name="management-point"></a>管理點  

- 每個主要站台可支援最多 15 個管理點。  

    > [!TIP]  
    > 請不要在從主要站台伺服器或站台資料庫伺服器之緩慢連結的伺服器上安裝管理點。  

- 每個次要站台支援單一管理點，它必須安裝在次要站台伺服器上。  

如需管理點可支援之用戶端與裝置數目的相關資訊，請參閱[管理點](#bkmk_mp)一節。  

> [!NOTE]
> 如果您啟用管理點以支援[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)，其將按常規來為網際網路型用戶端要求提供服務。 無論服務的是內部部署或網際網路型用戶端，管理點的大小調整指導方針都不會改變。

### <a name="software-update-point"></a>軟體更新點  

使用下列建議作為基準。 此基準可協助您判定適用於組織的軟體更新容量規劃資訊。 實際的容量需求可能會依下列準則而與本文中列出的建議有所不同：

- 您的特定網路環境
- 您用來裝載軟體更新點站台系統的硬體
- 受控的用戶端數目
- 安裝在伺服器上的其他站台系統角色  

> [!NOTE]
> 如果您啟用軟體更新點以支援[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)，其將按常規來為網際網路型用戶端要求提供服務。 無論服務的是內部部署或網際網路型用戶端，軟體更新點的大小調整指導方針都不會改變。

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> 軟體更新點的容量規劃  

支援的用戶端數目，取決於軟體更新點上執行的 Windows Server Update Services (WSUS) 版本。 同時也取決於是否存在與其他站台系統角色共存的軟體更新點站台系統角色：  

- 當軟體更新點伺服器上執行的是 WSUS，而且軟體更新點與其他站台系統角色共存時，軟體更新點最多可支援 25,000 個用戶端。  

- 當遠端伺服器符合 WSUS 需求、將 WSUS 與 Configuration Manager 搭配使用，而且您設定了下列設定時，軟體更新點就能支援多達 150,000 個用戶端：

  IIS 應用程式集區：

  - 將 WsusPool 佇列長度增加至 2000
  - 將 WsusPool 專用記憶體限制增加為 4 倍，或設為 0 (無限制)。 例如，如果預設限制為 1,843,200 KB，則會增加為 7,372,800。 如需詳細資訊，請參閱這篇 [Configuration Manager 支援小組部落格文章](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/)。  

    如需軟體更新點的硬體需求詳細資訊，請參閱[站台系統的建議硬體](recommended-hardware.md#bkmk_ScaleSieSystems)。  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a> 軟體更新物件的容量規劃  

使用下列容量資訊規劃軟體更新物件：  

- **將部署中的軟體更新數目限制為 1000 個** - 將各軟體更新部署的軟體更新數目限制為 1000 個。 當您建立自動部署規則 (ADR) 時，可指定限制軟體更新數目的準則。 ADR 會在指定的準則傳回超過 1000 個軟體更新時失敗。 從 Configuration Manager 主控台的 [自動部署規則] 節點檢查 ADR 的狀態。 當您手動部署軟體更新時，請勿選取部署多於 1000 個更新。  

  此外，請在設定基準中將軟體更新數目限制為 1000。 如需詳細資訊，請參閱[建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)。

- **自動部署規則的 580 個安全性範圍限制** -<!--ado 4962928-->
將自動部署規則 (ADR) 上的安全性範圍數目限制為小於 580 個。 當您建立 ADR 時，會自動新增可存取它的安全性範圍。 若設定 580 個以上的安全性範圍，ADR 將無法執行，而且會在 ruleengine.log 中記錄錯誤。

### <a name="sms-provider"></a>SMS 提供者

<!-- SCCMDocs#1958 -->

SMS 提供者的每個執行個體都支援來自多個請求的同時連線。 這些連線的唯一限制是 Windows 可用的伺服器連線數目，以及伺服器上可用來服務連線要求的資源。

如需詳細資訊，請參閱[規劃 SMS 提供者](../hierarchy/plan-for-the-sms-provider.md)。

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> 站台和階層的用戶端數目

使用下列資訊，判斷您可以於站台上或階層中支援的用戶端數目和用戶端類型。  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> 使用管理中心網站的階層

管理中心網站支援的裝置總數，包含針對下列三個群組所列出之最多裝置數目：  

- 700,000 部 Windows 桌上型電腦。 另請參閱對[內嵌裝置](#embedded)的支援。

- 25,000 部執行 Mac 和 Windows CE 7.0 的裝置  

- 使用內部部署行動裝置管理 (MDM) 管理的 100,000 部裝置

例如，在階層中，您可以支援 700,000 部桌上型電腦、最多 25,000 部 Mac 與 Windows CE 7.0 裝置，以及最多 100,000 部由內部部署 MDM 管理的裝置。 這個階層總共支援 825,000 部裝置。

> [!IMPORTANT]  
> 在管理中心網站使用 SQL Server 標準版的階層中，階層支援最多 50,000 部桌上型電腦與裝置。 若要支援超過 50,000 部桌上型電腦與裝置，您必須使用 SQL Server Enterprise Edition。 這項需求只適用於管理中心網站。 它不適用於獨立主要站台或子主要站台。 您針對主要站台使用的 SQL Server 版本並不會限制其容量來支援指定的用戶端數目。

在獨立主要站台使用中的 SQL Server 版本不會限制該站台容量，以支援最多指定數目的用戶端。  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a> 子主要站台

使用管理中心網站之階層中的每個子主要站台支援下列用戶端數目：  

- 總計 150,000 部用戶端與裝置，不限於特定群組或類型，只要支援不超過階層所支援的數目即可。 另請參閱[內嵌裝置](#embedded)的支援。

例如，主要站台支援 25,000 部 Mac 和 Windows CE 7.0 裝置。 該數目為階層的限制。 此主要站台接著可支援額外的 125,000 部桌上型電腦。 子主要站台所支援裝置的總數為支援的最大限制：150,000。

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a> 獨立主要站台

獨立主要站台支援下列的裝置數目：  

- 總計 175,000 部用戶端與裝置，不得超過：  

  - 150,000 部電腦 (執行 Windows、Linux 和 UNIX 的電腦)。 另請參閱[內嵌裝置](#embedded)的支援。

  - 25,000 部執行 Mac 和 Windows CE 7.0 的裝置

  - 使用內部部署 MDM 管理的 50,000 部裝置  

例如，支援 150,000 部桌上型電腦和 10,000 部 Mac 的獨立主要站台只支援由內部部署 MDM 管理的額外 15,000 部行動裝置。

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a> 主要站台和 Windows Embedded 裝置

主要站台支援已啟用檔案型寫入篩選器 (FBWF) 的 Windows Embedded 裝置。 當內嵌的裝置未啟用寫入篩選器時，主要站台支援的內嵌裝置數目上限即為該站台允許的裝置數目。 如果內嵌的裝置已啟用 FBWF 或整合寫入篩選器 (UWF)，主要站台就可以支援最多 10,000 個 Windows 內嵌裝置。 您必須針對可在[規劃將用戶端部署至 Windows Embedded 裝置](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)內找到之重要注意事項中所列的例外狀況設定這些裝置。 主要站台只支援 3,000 部已啟用 EWF 且未針對例外狀況而設定的 Windows Embedded 裝置。

### <a name="secondary-sites"></a><a name="bkmk_sec"></a> 次要站台

次要站台支援下列裝置數目：  

- 15,000 部桌上型電腦 (執行 Windows、Linux 和 UNIX 的電腦)  

### <a name="management-points"></a><a name="bkmk_mp"></a> 管理點

每個管理點都可以支援下列數目的裝置：  

- 總計 25,000 部用戶端和裝置，不得超過：  

  - 25,000 部桌上型電腦 (執行 Windows、Linux 和 UNIX 的電腦)  

  - 下列其中之一 (非兩者皆是)：  

    - 使用內部部署 MDM 管理的 10,000 部裝置  

    - 10,000 部執行 Mac 和 Windows CE 7.0 用戶端的裝置
