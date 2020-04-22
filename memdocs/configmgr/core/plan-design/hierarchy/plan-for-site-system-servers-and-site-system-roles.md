---
title: 規劃站台系統角色
titleSuffix: Configuration Manager
description: 規劃 Configuration Manager 階層時，請考量站台系統伺服器和站台系統角色。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706496"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>在 Configuration Manager 中規劃站台系統伺服器和站台系統角色

適用於：  Configuration Manager (最新分支)

您安裝的每個 Configuration Manager 站台都包含站台伺服器，即**站台系統伺服器**。 站台亦可包含從站台伺服器遠端到電腦上的其他站台系統伺服器。 站台系統伺服器 (站台伺服器或遠端站台系統伺服器) 支援 **站台系統角色**。  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a> 站台系統伺服器  

當您在電腦上安裝站台系統角色時，該電腦會變成站台系統伺服器。 您可以在每個站台安裝一或多個額外的站台系統伺服器。 您不需要安裝額外的站台系統伺服器，而且可以選擇直接在站台伺服器電腦上執行所有站台系統角色。 每部站台系統伺服器都會支援一或多個站台系統角色。 藉由共用伺服器上站台系統角色的處理負載，額外的伺服器能協助擴充站台的功能和容量。  

在考慮加入站台系統伺服器時，請確認伺服器符合預期用途的先決條件。 也會將它新增至頻寬足以與預期端點通訊的網路位置。 這些端點包含站台伺服器、網域資源、雲端式位置、站台系統伺服器和用戶端。  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  

在伺服器上安裝站台系統角色，以提供站台額外的功能。 範例包括：  

- 額外的管理點，讓站台可以支援更多裝置，直至站台支援的容量。  

- 額外的發佈點，以擴充內容基礎結構，並改善裝置的內容發佈效能。  

- 一或多個站台系統角色專屬功能。 例如，軟體更新點可讓您管理受控裝置的軟體更新。 Reporting Services 點可讓您執行報表來監視、了解和共用您環境的資訊。  

不同的 Configuration Manager 站台可以支援不同的站台系統角色集合。 這組支援的站台系統角色取決於站台類型。 (站台類型包含管理中心網站、主要站台或次要站台)。階層的拓撲可限制特定站台類型上放置某些角色。 例如，只有階層的頂層站台才支援服務連線點。 頂層站台可以是管理中心網站，也可以是獨立主要站台。 子主要站台或次要站台不支援此角色。  

安裝站台之後，您可以將部分站台系統角色的位置從站台伺服器上的預設位置移動到到另一部伺服器。 例如，管理點或發佈點角色預設會安裝在主要或次要站台伺服器上。 也會安裝某些站台系統角色的額外執行個體，以擴充站台功能並滿足業務需求。 有些角色是必要的，有些則是選擇性的。  

### <a name="configuration-manager-site-server"></a>Configuration Manager 站台伺服器

此角色識別 Configuration Manager 安裝程式執行所在的伺服器以安裝站台，或是您安裝次要站台的伺服器。 除非解除安裝站台，否則您無法移動或解除安裝此角色。  

### <a name="configuration-manager-site-system"></a>Configuration Manager 網站系統

這個角色會指派給您安裝站台或安裝站台系統角色的任何電腦。 除非您從電腦移除最後一個站台系統角色，否則無法移動或解除安裝此角色。  

### <a name="configuration-manager-component-site-system-role"></a>Configuration Manager 元件站台系統角色

此角色識別可執行 **SMS Executive** 服務執行個體的站台系統。 您需要支援其他角色，例如管理點。 除非您從電腦移除最後一個適用的站台系統角色，否則無法移動或解除安裝此角色。  

### <a name="configuration-manager-site-database-server"></a>Configuration Manager 站台資料庫伺服器

站台會將此角色指派給包含站台資料庫執行個體的站台系統伺服器。 執行安裝程式來修改站台，使其使用不同的 SQL Server 執行個體來裝載站台資料庫，才能將此角色移至新的伺服器。  

### <a name="sms-provider"></a>SMS 提供者

站台會將此角色指派給裝載 SMS 提供者執行個體的每部電腦。 此提供者是 Configuration Manager 主控台與站台資料庫之間的介面。 根據預設，此角色會自動安裝在管理中心網站和主要站台的站台伺服器上。 在每個站台上安裝額外的執行個體，以將存取權提供給額外的系統管理使用者或用於備援。  

若要安裝額外的提供者，請執行 Configuration Manager 安裝程式以[管理 SMS 提供者](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。 接著，在其他電腦上安裝額外的提供者。 只在電腦上安裝一個 SMS 提供者執行個體。 該電腦必須位於與站台伺服器相同的網域中。  

### <a name="application-catalog-web-service-point"></a>應用程式類別目錄 Web 服務點

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

一種站台系統角色，可將軟體程式庫中的軟體資訊提供給應用程式類別目錄網站。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

### <a name="application-catalog-website-point"></a>應用程式類別目錄網站點

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

一種網站系統角色，可提供使用者一份應用程式類別目錄中的可用軟體清單。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

### <a name="asset-intelligence-synchronization-point"></a>Asset Intelligence 同步處理點

連接 Microsoft 以下載 Asset Intelligence 類別目錄資訊的站台系統角色。 此角色也會上傳未分類的標題，讓 Microsoft 可以考慮未來將它們加入類別目錄中。 階層只支援此角色在階層的頂層站台有單一執行個體。 如果您將獨立主要站台擴充至較大的階層，則請從主要站台解除安裝此角色。 然後在管理中心網站安裝它。

如需詳細資訊，請參閱 [Configuration Manager 中的 Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

### <a name="certificate-registration-point"></a>憑證登錄點

與執行網路裝置註冊服務 (NDES) 之伺服器通訊的站台系統角色。 此角色會管理使用簡單憑證註冊通訊協定 (SCEP) 的裝置憑證要求。 只有主要站台和管理中心網站支援這個角色。

即使單一憑證登錄點即可提供功能給整個階層，不過您也可以在站台以及相同階層中的多個站台安裝此角色的多個執行個體。 此設計可協助負載平衡。 當多個執行個體存在於階層中時，用戶端會隨機指派到其中一個憑證登錄點。  

每個憑證登錄點都需存取個別的 NDES 執行個體。 您不能將兩個以上的憑證登錄點設定為使用相同 NDES 執行個體。 此外，請不要在執行 NDES 的相同伺服器上安裝憑證登錄點。  

### <a name="cloud-management-gateway-connection-point"></a>雲端管理閘道連接點

與[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)通訊的站台系統角色。  

### <a name="data-warehouse-service-point"></a>資料倉儲服務點

使用資料倉儲服務點來儲存並報告您 Configuration Manager 環境的長期歷程記錄資料。 如需詳細資訊，請參閱[資料倉儲](../../servers/manage/data-warehouse.md)。  

### <a name="distribution-point"></a>發佈點

包含可供用戶端下載之來源檔案的站台系統角色，例如：

- 應用程式內容
- 軟體套件
- 軟體更新
- OS 映像
- 開機映像  

根據預設，當您安裝新的主要或次要站台時，會在站台伺服器上安裝此角色。 管理中心網站不支援此角色。 在支援的站台以及相同階層中的多個站台，安裝此角色的多個執行個體。 如需詳細資訊，請參閱[內容管理的基本概念](fundamental-concepts-for-content-management.md)和[管理內容與內容基礎結構](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="endpoint-protection-point"></a>Endpoint Protection 點

一種網站系統角色，Configuration Manager 用於接受 Endpoint Protection 授權條款，以及設定雲端保護服務的預設成員資格。 階層只支援此角色的單一執行個體，而且它必須位在頂層站台。 如果您將獨立主要站台擴充至較大的階層，則請從主要站台解除安裝此角色，然後在管理中心網站安裝此角色。 如需詳細資訊，請參閱 [Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

### <a name="enrollment-point"></a>註冊點

一種站台系統角色，可使用 Configuration Manager PKI 憑證註冊行動裝置和 macOS 電腦。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

如果使用者使用 Configuration Manager 註冊行動裝置，且其 Active Directory 帳戶位於站台伺服器樹系不信任的樹系中，則請在使用者樹系中安裝註冊點。 Configuration Manager 可以驗證使用者。  

### <a name="enrollment-proxy-point"></a>註冊 Proxy 點

一種站台系統角色，可管理來自行動裝置和 macOS 電腦的 Configuration Manager 註冊要求。 雖然只在主要站台支援這個角色，但您可以在一個站台或是相同階層中的多個站台，安裝此角色的多個執行個體。  

支援網際網路上的行動裝置時，請將註冊 Proxy 點安裝在周邊網路中，並將註冊 Proxy 點安裝在內部網路上。

### <a name="exchange-server-connector"></a>Exchange Server 連接器

如需此角色的資訊，請參閱[使用 Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="fallback-status-point"></a>後援狀態點

一種站台系統角色，可協助您監視用戶端安裝。 它會識別因無法與其管理點通訊而未受控的用戶端。 雖然只在主要站台支援這個角色，但您可以在一個站台和在相同階層中的多個站台，安裝此角色的多個執行個體。

### <a name="management-point"></a>管理點

一種站台系統角色，可將原則和服務位置資訊提供給用戶端。 它也會接收來自用戶端的設定資料。  

根據預設，當您安裝新的主要或次要站台時，會在站台伺服器上安裝此角色。 主要站台支援此角色的多個執行個體。 次要站台支援單一管理點。 次要站台上的這個角色也稱為 Proxy 管理點，可提供本機連絡點，以讓用戶端取得電腦和使用者原則。  

設定管理點以支援 HTTP 或 HTTPs。 它們也可以支援您使用 Configuration Manager 內部部署行動裝置管理 (MDM) 所管理的行動裝置。 若要在管理點可服務來自用戶端的要求時，協助依管理點來減少站台資料庫伺服器上的處理負載，請使用[管理點的資料庫複本](../../servers/deploy/configure/database-replicas-for-management-points.md)。  

### <a name="reporting-services-point"></a>Reporting Services 點

此網站系統角色可與 SQL Server Reporting Services 整合，以建立及管理 Configuration Manager 的報告。 主要站台和管理中心網站支援這個角色，且您可以在支援的站台上安裝此角色的多個執行個體。 如需詳細資訊，請參閱[規劃報告](../../servers/manage/planning-for-reporting.md)。  

### <a name="service-connection-point"></a>服務連接點

從您的站台上傳使用資料的站台系統角色，並且需要有此角色才能讓 Configuration Manager 更新可在主控台中使用。 階層只支援此角色的單一執行個體，而且它必須位在您階層的頂層站台。 如果您將獨立主要站台擴充至較大的階層，則請從主要站台解除安裝此角色，然後在管理中心網站安裝此角色。 如需詳細資訊，請參閱 [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) (關於服務連接點)。  

### <a name="software-update-point"></a>軟體更新點

此網站系統角色可與 Windows Server Update Services (WSUS) 整合，以提供軟體更新給 Configuration Manager 用戶端。 所有站台都支援此角色︰  

- 在管理中心網站安裝此站台系統，以與 WSUS 同步。  

- 在子主要站台設定此角色的每個執行個體，以便與管理中心網站同步。  

- 跨網路傳輸資料速度變慢時，請考慮將軟體更新點安裝至次要站台。  

如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。  

### <a name="state-migration-point"></a>狀態移轉點

當您將電腦移轉至新的作業系統時，此站台系統角色會儲存使用者狀態資料。 主要站台和次要站台均支援此角色。 在站台以及相同階層中的多個站台，安裝此角色的多個執行個體。 如需部署作業系統時儲存使用者狀態的詳細資訊，請參閱[管理使用者狀態](../../../osd/get-started/manage-user-state.md)。  


## <a name="next-steps"></a>後續步驟

部分 Configuration Manager 站台系統角色需要連線至網際網路。 如果您的環境需要網際網路流量才能使用 Proxy 伺服器，則請設定這些站台系統角色以使用 Proxy。 如需詳細資訊，請參閱 [Proxy 伺服器支援](../network/proxy-server-support.md)。  
