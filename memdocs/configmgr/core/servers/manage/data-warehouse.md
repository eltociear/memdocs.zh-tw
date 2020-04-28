---
title: 資料倉儲
titleSuffix: Configuration Manager
description: Configuration Manager 的資料倉儲服務點與資料庫
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: abe6b05d24955959e1d08defc2c5054c4499d756
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075586"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Configuration Manager 的資料倉儲服務點

適用於：  Configuration Manager (最新分支)

<!--1277922-->
使用資料倉儲服務點來儲存並報告您的 Configuration Manager 部署的長期歷程記錄資料。

> [!Note]  
> 在 1910 版中，Configuration Manager 預設會啟用此功能。 在 1906 版或更早版本中，Configuration Manager 預設不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](install-in-console-updates.md#bkmk_options)。<!--505213-->  


資料倉儲支援高達 2 TB 的資料，其含有變更追蹤的時間戳記。 資料倉儲儲存資料的方式是將 Configuration Manager 站台資料庫自動同步至資料倉儲資料庫。 然後您就可以從 Reporting Services 點存取此資訊。 同步到資料倉儲資料庫的資料會保留三年。 內建工作會定期移除超過三年的資料。

同步處理的資料包括來自全域資料和站台資料群組的下列資料：
- 基礎結構健全狀況
- 安全性
- 合規性
- 惡意程式碼   
- 軟體部署
- 清查詳細資料 (但不同步清查歷程記錄)

當站台系統角色安裝時，它會安裝並設定資料倉儲資料庫。 它也會安裝數個報告，以便您可以輕鬆地搜尋資料並報告。

自 1810 版開始，您可以將站台資料庫的更多資料表同步至資料倉儲。 這項變更可讓您根據業務需求建立更多報表。<!--1358870--> 



## <a name="prerequisites"></a>先決條件

- 僅階層中的頂層站台才支援資料倉儲站台系統角色。 例如，管理中心網站或獨立的主要站台。  

- 您安裝站台系統角色的電腦需要 .NET Framework 4.5.2 或更新版本。  

- 將資料倉儲資料庫的 **db_datareader** 權限授與 **Reporting Services 點帳戶**。  

- Configuration Manager 使用站台系統角色的電腦帳戶，同步資料與資料倉儲資料庫。 此帳戶需要下列權限：  

    - 裝載資料倉儲資料庫之電腦上的 **Administrator**。  

    - 資料倉儲資料庫上的 **DB_Creator** 權限。  

    - 頂層站台資料庫有**執行**權限的 **DB_owner** 或 **DB_reader**。  

- 資料倉儲資料庫需要使用 SQL Server 2012 或更新版本。 可以是 Standard、Enterprise 或 Datacenter 版本。 資料倉儲和站台資料庫伺服器的 SQL Server 版本不必相同。<!--SCCMDocs issue 662-->  

- 倉儲資料庫支援下列 SQL Server 設定：  

    - 預設或具名執行個體  

    - SQL Server AlwaysOn 可用性群組  

    - SQL Server 容錯移轉叢集  

- 如果您使用[分散式檢視](../../plan-design/hierarchy/database-replication.md#bkmk_distviews)，則必須在裝載管理中心網站資料庫的伺服器上安裝資料倉儲服務點。  

如需 SQL Server 授權的詳細資訊，請參閱[產品與授權常見問題集](../../understand/product-and-licensing-faq.md)。 <!-- sms500967 -->

將資料倉儲資料庫的大小調整至與站台資料庫相同。 雖然資料倉儲一開始比較小，但會隨著時間成長。 <!--SCCMDocs issue 756-->



## <a name="install"></a>安裝

每個階層都支援此角色的單一執行個體，位於該頂層站台的任何站台系統上。 裝載倉儲資料庫的 SQL Server 可以是本機站台系統角色，或者遠端站台系統角色。 資料倉儲可以搭配安裝在相同網站上的 Reporting Services 點使用。 您不需要在同一部伺服器上安裝兩個站台系統角色。   

若要安裝角色，使用「新增站台系統角色精靈」  或「建立站台系統伺服器精靈」  。 如需詳細資訊，請參閱[安裝站台系統角色](../deploy/configure/install-site-system-roles.md)。 在精靈的 [系統角色選取]  頁面中，選取**資料倉儲服務點**角色。 

當您安裝此角色時，Configuration Manager 會在您指定的 SQL Server 執行個體上為您建立資料倉儲資料庫。 如果您指定現有資料庫的名稱，Configuration Manager 就不會建立新資料庫。 而會使用您指定的資料庫。 這和您[將資料倉儲資料庫移至新的 SQL Server](#move-the-database) 時所用的程序相同。


### <a name="configure-properties"></a>設定內容

#### <a name="general-page"></a>一般頁面

- **SQL Server 完整網域名稱**：指定裝載資料倉儲服務點資料庫之伺服器的完整網域名稱 (FQDN)。  

- **SQL Server 執行個體名稱 (如適用)** ：如果您沒有使用 SQL Server 的預設執行個體，請指定具名執行個體。  

- **資料庫名稱**：指定資料倉儲資料庫的名稱。 Configuration Manager 會以此名稱建立資料倉儲資料庫。 如果您指定的資料庫名稱已存在於 SQL Server 執行個體上，Configuration Manager 會使用該資料庫。  

- **連線時要使用的 SQL Server 連接埠**：指定裝載資料倉儲資料庫之 SQL Server 所使用的 TCP/IP 通訊埠號碼。 資料倉儲同步服務會使用此連接埠連線到資料倉儲資料庫。 通訊預設使用 SQL Server 連接埠 **1433**。  

- **資料倉儲服務點帳戶**：從 1802 版開始，設定 SQL Server Reporting Services 連線到資料倉儲資料庫時所用的**使用者名稱**。  


#### <a name="synchronization-schedule-page"></a>同步排程頁面
適用於 1806 版與較舊版本 

- **開始時間**：指定您想要啟動資料倉儲同步處理的時間。  

- **循環模式**

    - **每日**：指定每日執行同步處理。  

    - **每週**：指定每週一天，每週定期同步處理。


#### <a name="synchronization-settings-page"></a>同步設定頁面
*適用於 1810 版和更新版本*

- **資料同步自訂設定**：選擇 [選取資料表]  選項。 在資料庫資料表視窗中，選取要同步至資料倉儲資料庫的資料表名稱。 使用篩選依名稱搜尋，或選取下拉式清單以選擇特定群組。 選取 [確定]  完成儲存。  

    > [!Note]  
    > 您無法移除角色預設選取的資料表。  

- **開始時間**：指定您想要啟動資料倉儲同步處理的時間。  

- **循環模式**

    - **每日**：指定每日執行同步處理。  

    - **每週**：指定每週一天，每週定期同步處理。



## <a name="reporting"></a>報告

安裝資料倉儲服務點後，站台的 Reporting Services 點上即會有數份報告可用。 如果您在安裝 Reporting Services 點之前安裝資料倉儲服務點，在您稍後安裝 Reporting Services 點時會自動加入這些報告。

> [!WARNING]  
> 從 1802 版開始，資料倉儲點支援替代認證。<!--507334--> 如果從舊版 Configuration Manager 升級，您必須指定 SQL Server Reporting Services 連線到資料倉儲資料庫所用的認證。 新增認證後才能開啟資料倉儲報表。 
> 
> 若要指定帳戶，請在角色 [內容] 中設定資料倉儲服務點帳戶的 [使用者名稱]  。 如需詳細資訊，請參閱[設定內容](#configure-properties)。 

資料倉儲站台系統角色包含下列報表，位在 [資料倉儲]  類別下：  

- **應用程式部署 - 歷程記錄**：檢視特定應用程式和電腦之應用程式部署的詳細資料。  

- **Endpoint Protection 及軟體更新合規性 - 歷程記錄**：檢視遺失軟體更新的電腦。  

- **一般硬體清查 - 歷程記錄**：檢視特定電腦的所有硬體清查。  

- **一般軟體清查 - 歷程記錄**：檢視特定電腦的所有軟體清查。  

- **基礎結構健康情況概觀 - 歷程記錄**：顯示您 Configuration Manager 基礎結構健全狀況的概觀。  

- **偵測到的惡意程式碼清單 - 歷程記錄**：檢視組織中已偵測到的惡意程式碼。  

- **軟體發佈摘要 - 歷程記錄**:特定公告和電腦的軟體發佈摘要。  



## <a name="site-expansion"></a>站台擴充

您必須先解除安裝資料倉儲服務點角色，才能安裝管理中心網站以擴充現有的獨立主要站台。 安裝管理中心網站之後，您可以在管理中心網站安裝站台系統角色。  

不同於移動資料倉儲資料庫，此變更會導致您先前在主要站台上同步處理的歷程資料遺失。 不支援從主要站台備份資料庫，並在管理中心網站還原資料庫。



## <a name="move-the-database"></a>移動資料庫

您可以使用下列步驟將資料倉儲資料庫移至新的 SQL Server：  

1. 使用 SQL Server Management Studio 備份資料倉儲資料庫。 然後，將該資料庫還原到裝載資料倉儲的新電腦上的 SQL Server。  

    > [!NOTE]  
    > 當您將資料庫還原到新的伺服器之後，請確定新資料倉儲資料庫的資料庫存取權限與原始資料倉儲資料庫的權限相同。  

2. 使用 Configuration Manager 主控台移除目前伺服器上的資料倉儲服務點角色。  

3. 重新安裝資料倉儲服務點。 指定裝載已還原資料倉儲資料庫的新 SQL Server 和執行個體名稱。  

4. 安裝站台系統角色之後，即完成移動。  



## <a name="troubleshooting"></a>疑難排解 

### <a name="log-files"></a>記錄檔 

您可以使用下列記錄來調查安裝資料倉儲服務點或同步處理資料的問題：

- **DWSSMSI.log** 和 **DWSSSetup.log**：使用這些記錄調查安裝資料倉儲服務點時發生的錯誤。  

- **Microsoft.ConfigMgrDataWarehouse.log**：使用此記錄調查站台資料庫與資料倉儲資料庫之間的資料同步。  


### <a name="set-up-failure"></a>安裝失敗 

當資料倉儲服務點角色是您在遠端伺服器上安裝的第一個角色時，資料倉儲的安裝會失敗。  

#### <a name="workaround"></a>因應措施 
請確定您要安裝資料倉儲服務點的電腦已至少裝載一個其他角色。  


### <a name="synchronization-failed-to-populate-schema-objects"></a>同步無法填入結構描述物件 

同步失敗，**Microsoft.ConfigMgrDataWarehouse.log** 顯示下列訊息：`failed to populate schema objects`

#### <a name="workaround"></a>因應措施 
確定資料倉儲資料庫上的站台系統角色電腦帳戶是 **db_owner**。


### <a name="reports-fail-to-open"></a>報表無法開啟

當資料倉儲資料庫和 Reporting Service 點位在不同的站台系統上時，無法開啟資料倉儲報告。  

#### <a name="workaround"></a>因應措施
將資料倉儲資料庫的 **db_datareader** 權限授與 **Reporting Services 點帳戶**。


### <a name="error-opening-reports"></a>開啟報表時發生錯誤

當您開啟資料倉儲報表時，傳回下列錯誤︰

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>因應措施 
使用下列步驟設定憑證：

1. 在裝載資料倉儲資料庫的電腦上︰  

    1. 開啟 IIS，選取 [伺服器憑證]  ，然後以滑鼠右鍵按一下 [建立自我簽署憑證]  。 然後指定憑證名稱的「易記名稱」為**資料倉儲 SQL Server 識別憑證**。 選取憑證存放區為 [個人]  。  

    2. 開啟 [SQL Server 組態管理員]  。 在 [SQL Server 網路組態]  底下以滑鼠右鍵按一下選取 [MSSQLSERVER 的通訊協定]  下的 [內容]  。 切換至 [憑證]  索引標籤，選取 [資料倉儲 SQL Server 識別憑證]  作為憑證，然後儲存變更。  

    3. 在 [SQL Server 組態管理員]  的 [SQL Server 服務]  下，重新啟動 **SQL Server 服務**。 若 SQL Reporting Services 也安裝於裝載資料倉儲資料庫的伺服器上，請重新啟動 **Reporting Service** 服務。  

    4. 開啟 Microsoft Management Console (MMC)，並新增**憑證**嵌入式管理單元。 選取本機電腦的 [電腦帳戶]  。 展開 **Personal** 資料夾，然後選取 [憑證]  。 將**資料倉儲 SQL Server 識別憑證**匯出為 **DER 編碼二進位 X.509 (.CER)** 檔案。  

2. 在裝載 SQL Server Reporting Services 的電腦上，開啟 MMC 並新增**憑證**嵌入式管理單元。 選取 [電腦帳戶]  。 在 [信任的根憑證授權單位]  資料夾底下，匯入**資料倉儲 SQL Server 識別憑證**。  



## <a name="data-flow"></a>資料流程   

![顯示資料倉儲的站台元件之間的邏輯資料流程的圖表](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>資料儲存與同步

| 步驟   | 詳細資料  |
|--------|----------|  
| **1**  | 站台伺服器將資料傳送並儲存在站台資料庫。 |  
| **2**  | 資料倉儲服務點根據其排程和設定，從站台資料庫取得資料。 |  
| **3**  | 資料倉儲服務點將同步處理的資料複本傳送並儲存在資料倉儲資料庫。 |  


#### <a name="reporting"></a>報告

| 步驟   | 詳細資料  |
|--------|----------|  
| **A**  | 使用者使用內建報表要求資料。 此要求會使用 SQL Server Reporting Services 傳遞到 Reporting Services 點。 |  
| **B**  | 大部分報告是針對目前的資訊，並會對站台資料庫執行這些要求。 |  
| **C**  | 當報表使用以其中一個 [類別]  為 [資料倉儲]  的報表要求歷程資料時，會對資料倉儲資料庫執行要求。 |  
