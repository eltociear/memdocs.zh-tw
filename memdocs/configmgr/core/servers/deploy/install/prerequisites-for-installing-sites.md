---
title: 站台的必要條件
titleSuffix: Configuration Manager
description: 了解安裝不同類型 Configuration Manager 站台的必要條件。
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8362dbf5cf7264c19f683ce5a224f1e0ec348b36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700666"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>安裝 Configuration Manager 站台的必要條件

適用於：  Configuration Manager (最新分支)

開始站台安裝之前，請先了解安裝不同類型 Configuration Manager 站台的必要條件。


## <a name="primary-sites-and-the-central-administration-site"></a>主要站台和管理中心網站

下列必要條件適用於安裝下列其中一個類型：

- 作為階層中第一個站台的管理中心網站
- 獨立主要站台
- 子主要站台

如果您要在階層擴充期間安裝管理中心網站，請參閱[擴充獨立主要站台](#bkmk_expand)。

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a> 安裝主要站台或管理中心網站的必要條件  

- 必須安裝所需的 Windows Server 角色、功能和 Windows 元件。 如需詳細資訊，請參閱[站台系統必要條件](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq)  

- 安裝站台的使用者帳戶必須擁有下列權限：  

    - 下列伺服器上的**系統管理員**：  
        - 站台伺服器  
        - 裝載**站台資料庫**的每部伺服器  
        - 適用於該站台的每個 **SMS 提供者** 執行個體  

    - 在裝載站台資料庫之 SQL Server 執行個體上的 **Sysadmin**  

        > [!IMPORTANT]  
        > 當 Configuration Manager 安裝完成之後，站台伺服器電腦帳戶都必須保留 SQL Server 的 sysadmin 權限。 請不要從此帳戶移除 SQL sysadmin 權限。  

- 如果您正在安裝主要站台，則需要下列額外的權限：  

    - 位於您安裝初始管理點與發佈點之其他伺服器上的**系統管理員** (如果不在站台伺服器上)  

- 如果您要在管理中心網站下方安裝新的子主要站台，則需要下列額外的權限：  

    - 裝載管理中心網站之伺服器上的**系統管理員**  

    - Configuration Manager 內以角色為基礎的系統管理權限，相當於 [基礎結構系統管理員]  或 [系統高權限管理員]  安全性角色  

- 使用正確的安裝來源檔案，並從該位置執行安裝程式。 如需用來安裝不同類型站台之正確來源檔案的相關資訊，請參閱[安裝不同類型站台的選項](prepare-to-install-sites.md#bkmk_options)。  

- 站台伺服器必須可透過下列其中一種方式，從 Microsoft 存取更新的安裝程式檔案：  

    - 開始安裝之前，請下載這些檔案，並將其複本儲存於您的本機網路上。 如需詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。  

    - 如果這些檔案的本機複本無法使用，站台伺服器就必須能夠存取網際網路。 它會在安裝期間從 Microsoft 下載這些檔案。  

- 站台伺服器與站台資料庫伺服器都必須符合所有的必要條件設定。 開始安裝 Configuration Manager 之前，請[手動執行必要條件檢查程式](prerequisite-checker.md)來找出問題並加以修正。  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> 擴充獨立主要站台的必要條件

獨立主要站台必須符合以下必要條件，您才能將獨立主要站台擴充到具有管理中心網站的階層：

#### <a name="source-file-version-matches-site-version"></a>來源檔案版本符合站台版本

使用來自符合獨立主要站台版本之 CD.Latest 資料夾的媒體，來安裝新的管理中心網站。 為確保版本相符，請使用可在獨立主要站台上的 [CD.Latest 資料夾](../../manage/the-cd.latest-folder.md)中找到的來源檔案。

如需用來安裝不同站台之正確來源檔案的詳細資訊，請參閱[安裝不同類型站台的選項](prepare-to-install-sites.md#bkmk_options)。  

#### <a name="stop-active-migration-from-another-hierarchy"></a>停止來自另一個階層的作用中移轉

您無法將獨立主要站台設定為從另一個 Configuration Manager 階層移轉資料。 停止從其他 Configuration Manager 階層進行至獨立主要站台的作用中移轉，並移除所有移轉設定。 這些設定包括：

- 尚未完成的移轉作業  
- 資料收集  
- 作用中來源階層的設定  

此設定是必要的，因為 Configuration Manager 會從階層的頂層站台移轉資料。 當您擴充獨立主要站台時，用於移轉的設定不會傳輸到管理中心網站。  

擴充獨立主要站台之後，如果您在主要站台上重新設定移轉，則管理中心網站會執行移轉作業。

如需如何設定移轉的詳細資訊，請參閱[設定來源階層和來源站台以進行移轉](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md)。  

#### <a name="computer-account-as-administrator"></a>具系統管理員身分的電腦帳戶

裝載新管理中心網站之伺服器的電腦帳戶，必須是獨立主要站台伺服器的**系統管理員**群組成員。

若要成功擴充獨立主要站台，新管理中心網站的電腦帳戶必須具有獨立主要站台的 [系統管理員]  權限。 這只有在站台擴充期間才需要這個做。 站台擴充完成之後，您可以從主要站台的使用者群組中移除該帳戶。  

#### <a name="installation-account-permissions"></a>安裝帳戶權限

執行 Configuration Manager 安裝程式以安裝新管理中心網站的使用者帳戶，必須具有獨立主要站台上以角色為基礎的系統管理權限。

若要在擴充站台期間安裝管理中心網站，執行安裝程式以安裝管理中心網站的使用者帳戶，必須在獨立主要站台上以角色為基礎的系統管理中定義為**系統高權限管理員**或**基礎結構系統管理員**。

如需詳細資訊，包括必要權限的完整清單，請參閱[站台安裝帳戶](../../../plan-design/hierarchy/accounts.md#site-installation-account)。

#### <a name="top-level-site-roles"></a>頂層站台角色

擴充站台之前，先從獨立主要站台解除安裝下列站台系統角色：

- Asset Intelligence 同步處理點  
- Endpoint Protection 點  
- 服務連接點  

Configuration Manager 僅在階層的頂層站台支援這些角色。 擴充獨立主要站台之前，請先解除安裝這些站台系統角色。 擴充站台之後，在管理中心網站重新安裝這些站台系統角色。  

主要站台上所有其他站台系統角色則仍可維持安裝狀態。  

#### <a name="open-the-sql-server-service-broker-port"></a>開啟 SQL Server Service Broker 連接埠

您必須針對獨立主要站台與管理中心網站伺服器之間的 SQL Server Service Broker (SSB)，開啟網路連接埠。  

為了在管理中心網站與主要站台之間成功複寫資料，Configuration Manager 要求兩個站台之間要有開啟連接埠以供 SSB 使用。 當您安裝管理中心網站並擴充獨立主要站台時，必要條件檢查不會驗證您為 SSB 指定的連接埠是否已在主要站台上開啟。  

#### <a name="known-issues-with-azure-services"></a>Azure 服務的已知問題

擴充站台之後，您必須使用 Configuration Manager 重新設定下列 Azure 服務：

- [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  
- [商務用 Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [雲端管理閘道](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

在 1806 版和更新版本上，更新 Azure Active Directory 租用戶秘密金鑰。 如需詳細資訊，請參閱[更新秘密金鑰](../configure/azure-services-wizard.md#bkmk_renew)。

或者，移除後再重新建立與該服務的連線：

1. 在 Configuration Manager 主控台中，刪除 [Azure 服務]  節點中的 Azure 服務。  

2. 在 Azure 入口網站中，從 Azure Active Directory 租用戶節點上刪除已與服務建立關聯的租用戶。 這個動作也會刪除已與服務建立關聯的 Azure AD Web 應用程式。  

3. 重新設定對 Azure 服務的連線，以搭配 Configuration Manager 使用。  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a> 次要站台

下列是安裝次要站台的必要條件：  

- 必須安裝所需的 Windows Server 角色、功能和 Windows 元件。 如需詳細資訊，請參閱[站台系統必要條件](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq)  

- 在 Configuration Manager 主控台中設定安裝次要站台的系統管理員，必須具備以角色為基礎的系統管理權限，相當於 [基礎結構系統管理員]  或 [系統高權限管理員]  安全性角色。  

- 父主要站台的電腦帳戶必須是次要站台伺服器上的**系統管理員**。  

- 次要網站使用先前安裝的 SQL Server 執行個體來裝載次要網站資料庫時：  

    - 父主要站台的電腦帳戶必須在次要站台伺服器的 SQL Server 執行個體上具備 **sysadmin** 權限。  

    - 次要站台伺服器電腦的**本機系統**帳戶必須在次要站台伺服器的 SQL Server 執行個體上具備 **sysadmin** 權限。  

        > [!IMPORTANT]  
        > 當 Configuration Manager 安裝程式完成時，這兩個帳戶都必須保有 SQL Server 的 sysadmin 權限。 請不要從這些帳戶移除 sysadmin 權限。  

- 次要站台伺服器必須符合所有的必要條件設定。 這些設定包括 SQL Server 以及管理點和發佈點的預設站台系統角色。  


## <a name="next-steps"></a>後續步驟

確認必要條件之後，您就可以開始執行安裝程式。 如需詳細資訊，請參閱[使用安裝精靈安裝 Configuration Manager 站台](use-the-setup-wizard-to-install-sites.md)。
