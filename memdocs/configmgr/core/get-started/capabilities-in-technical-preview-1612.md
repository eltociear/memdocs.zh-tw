---
title: Technical Preview 1612 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1612 版中可用的功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0c2464bfba05d640868af7d5c8be7c32c0999946
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705406"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Configuration Manager Technical Preview 1612 中的功能

適用於：  Configuration Manager (Technical Preview 分支)



此文章介紹 Configuration Manager 技術預覽 1612 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  

## <a name="the-data-warehouse-service-point"></a>資料倉儲服務點
從 Technical Preview 1612 版開始，資料倉儲服務點可讓您儲存及報告 Configuration Manager 部署的長期歷程記錄資料。 這可透過從 Configuration Manager 站台資料庫自動同步處理至資料倉儲資料庫來完成。 然後即可從您的 Reporting Services 點存取這項資訊。

根據預設，當您安裝新的站台系統角色時，Configuration Manager 會在您指定的 SQL Server 執行個體上為您建立資料倉儲資料庫。 資料倉儲支援高達 2 TB 的資料，其含有變更追蹤的時間戳記。  根據預設，從站台資料庫同步處理的資料會包含全域資料、站台資料、Global_Proxy、雲端資料和資料庫檢視的資料群組。 您也可以修改同步處理的內容，以包含其他資料表，或從預設複寫設定排除特定資料表。
同步處理的預設資料包含下列資訊：
- 基礎結構健全狀況
- 安全性
- 合規性
- 惡意程式碼   
- 軟體部署
- 清查詳細資料 (但不會同步處理清查歷程記錄)

除了安裝及設定資料倉儲資料庫，還安裝數個新報告，讓您可以輕鬆地搜尋並報告此資料。

### <a name="data-warehouse-dataflow"></a>資料倉儲資料流程   
![資料倉儲流程](./media/datawarehouse.png)

| 步驟         | 詳細資料  |
|:------:|-----------|  
| **1** | 站台伺服器將資料傳送並儲存在站台資料庫。  |  
| **2** | 資料倉儲服務點根據其排程和設定，從站台資料庫取得資料。  |  
| **3** | 資料倉儲服務點將同步處理的資料複本傳送並儲存在資料倉儲資料庫。 |  
| **A** | 使用內建報告，將提出的資料要求傳遞到使用 SQL Server Reporting Services 的 Reporting Services 點。 |  
| **B** | 大部分報告是針對目前的資訊，並會對站台資料庫執行這些要求。 |  
| **C** | 當報告要求歷程記錄資料時，使用其中一個 [類別]  為 [資料倉儲]  的報告，對資料倉儲資料庫執行要求。   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>資料倉儲服務點和資料庫的必要條件
- 您的階層必須已安裝 Reporting Services 點站台系統角色。
- 您安裝站台系統角色的電腦需要 .NET Framework 4.5.2 或更新版本。
- 您安裝站台系統角色的電腦帳戶必須具有將裝載資料倉儲資料庫之電腦的本機系統管理員權限。
- 您用來安裝站台系統角色的系統管理帳戶必須是將裝載資料倉儲資料庫之 SQL Server 執行個體上的 DBO。  
- 支援下列資料庫：
  - 具有 SQL Server 2012 或更新版本 (Enterprise 或 Datacenter Edition)。
  - 在預設或具名執行個體上
  - 在「SQL Server 叢集」  上。 雖然這項設定應該可行，但尚未經過測試，因此最好提供支援。
  - 與站台資料庫或 Reporting Services 點資料庫共置時。 不過，建議將它安裝在不同的伺服器上。  
- 作為「Reporting Services 點帳戶」  的帳戶必須具有資料倉儲資料庫的 **db_datareader** 權限。  
- 「SQL Server AlwaysOn 可用性群組」  不支援此資料庫。

### <a name="install-the-data-warehouse"></a>安裝資料倉儲
您可以使用 [新增站台系統角色精靈]  或 [建立站台系統伺服器精靈]  ，在管理中心網站或主要站台上安裝資料倉儲站台系統角色。 如需詳細資訊，請參閱[安裝站台系統角色](../servers/deploy/configure/install-site-system-roles.md)。 一個階層支援此角色的多個執行個體，但每個站台只支援一個執行個體。  

當您安裝此角色時，Configuration Manager 會在您指定的 SQL Server 執行個體上為您建立資料倉儲資料庫。 如果您指定現有資料庫的名稱 (就像是在[將資料倉儲資料庫移至新的 SQL Server](#move-the-data-warehouse-database) 時所執行的動作)，Configuration Manager 不會建立新的資料庫，而是會使用您指定的資料庫。

#### <a name="configurations-used-during-installation"></a>安裝期間所使用的設定
您可以使用下列資訊來完成站台系統角色的安裝：

[系統角色選取]  頁面：  
您必須已安裝 Reporting Services 點，此精靈才會顯示選取及安裝資料倉儲服務點的選項。

[一般]  頁面：需要下列一般資訊：
- **Configuration Manager 資料庫設定：**   
  - **伺服器名稱** - 指定裝載站台資料庫之伺服器的 FQDN。 如果您未使用 SQL Server 的預設執行個體，則必須以下列格式在 FQDN 之後指定執行個體︰***&lt;SQL Server FQDN>\&lt;執行個體名稱>***
  - **資料庫名稱** - 指定站台資料庫的名稱。
  - **確認** - 按一下 [確認]  確定成功連線到站台資料庫。
</br></br>
- **資料倉儲資料庫設定：**
  - **伺服器名稱** - 指定裝載資料倉儲服務點和資料庫之伺服器的 FQDN。 如果您未使用 SQL Server 的預設執行個體，則必須以下列格式在 FQDN 之後指定執行個體︰***&lt;SQL Server FQDN>\&lt;執行個體名稱>***
  - **資料庫名稱** - 指定資料倉儲資料庫的 FQDN。  Configuration Manager 會使用此名稱來建立資料庫。 如果您指定的資料庫名稱已存在於 SQL Server 執行個體上，Configuration Manager 會使用該資料庫。
  - **確認** - 按一下 [確認]  確定成功連線到站台資料庫。

[同步處理設定]  頁面：   
- **資料設定︰**
  - **要同步處理的複寫群組** - 選取您要同步處理的資料群組。 如需不同資料群組類型的資訊，請參閱[站台間的資料傳輸](../plan-design/hierarchy/data-transfers-between-sites.md)中的[資料庫複寫](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep)和**分散式檢視**。
  - **加入同步處理的資料表** - 指定您要同步處理之每個額外資料表的名稱。 使用逗號分隔多個資料表。 這些資料表將會從站台資料庫及您選取的複寫群組進行同步處理。
  - **排除同步處理的資料表** - 指定您同步處理之來源複寫群組中的個別資料表名稱。 您指定的資料表將遭到排除。 使用逗號分隔多個資料表。
- **同步處理設定：**
  - **同步處理間隔 (分鐘)** - 指定以分鐘為單位的值。 到達間隔之後，便會開始新的同步處理。 這項設定支援的時間範圍為 60 到 1440 分鐘 (24 小時)。
  - **排程** - 指定您要執行同步處理的日期。

**報告點存取**：   
安裝資料倉儲角色之後，作為「Reporting Services 點帳戶」  的帳戶會具有資料倉儲資料庫的 **db_datareader** 權限。

#### <a name="troubleshoot-installation-and-data-synchronization"></a>針對安裝和資料同步處理進行疑難排解
您可以使用下列記錄來調查安裝資料倉儲服務點或同步處理資料的問題：
- **DWSSMSI.log** 和 **DWSSSetup.log** - 使用這些記錄可調查安裝資料倉儲服務點時所發生的錯誤。
- **Microsoft.ConfigMgrDataWarehouse.log** - 使用此記錄可調查站台資料庫與資料倉儲資料庫之間的資料同步處理。

### <a name="reporting"></a>報告
安裝資料倉儲站台系統角色之後，Reporting Services 點會提供下列 [類別]  為 [資料倉儲]  的報告：

|報表                   | 詳細資料                                  |
|-------------------------|------------------------------------------|
| **應用程式部署報告** | 檢視特定應用程式和電腦之應用程式部署的詳細資料。|
| **Endpoint Protection 和軟體更新合規性報告**   | 檢視遺失軟體更新的電腦。|
| **一般硬體清查報告**  | 檢視特定電腦的所有硬體清查。|
| **一般軟體清查報告**  | 檢視特定電腦的所有軟體清查。|
| **基礎結構健全狀況概觀**  |顯示您 Configuration Manager 基礎結構健全狀況的概觀。|
| **偵測到的惡意程式碼清單**  |檢視組織中已偵測到的惡意程式碼。|
| **軟體發佈摘要報告** | 特定公告和電腦的軟體發佈摘要。|

### <a name="move-the-data-warehouse-database"></a>移動資料倉儲資料庫
您可以使用下列步驟將資料倉儲資料庫移至新的 SQL Server：

1. 檢閱目前的資料庫設定並記錄設定詳細資料，包括：  
   - 同步處理的資料群組
   - 加入或排除同步處理的資料表       

   當您將資料庫還原到新的伺服器並重新安裝站台系統角色之後，您會重新設定這些資料群組和資料表。  

2. 使用 SQL Server Management Studio 備份資料倉儲資料庫，然後再次將該資料庫還原到將裝載資料倉儲之新電腦上的 SQL Server。

   當您將資料庫還原到新的伺服器之後，請確定新資料倉儲資料庫的資料庫存取權限與原始資料倉儲資料庫的權限相同。

3. 使用 Configuration Manager 主控台從目前的伺服器移除資料倉儲服務點站台系統角色。

4. 安裝新的資料倉儲服務點，並指定裝載您還原之資料倉儲資料庫的新 SQL Server 和執行個體名稱。

5. 安裝站台系統角色之後，即完成移動。

您可以檢閱下列 Configuration Manager 記錄，確認已成功重新安裝站台系統角色：  
- **DWSSMSI.log** 和 **DWSSSetup.log** - 使用這些記錄可調查安裝資料倉儲服務點時所發生的錯誤。
- **Microsoft.ConfigMgrDataWarehouse.log** - 使用此記錄可調查站台資料庫與資料倉儲資料庫之間的資料同步處理。


## <a name="content-library-cleanup-tool"></a>內容庫清理工具
從 Technical Preview 1612 版開始，您可以使用新的命令列工具 (**ContentLibraryCleanup.exe**) 從發佈點移除不再與任何套件或應用程式相關聯的內容 (孤立的內容)。 這項工具稱為內容庫清理工具。

此工具只會影響您在執行工具時所指定之發佈點上的內容，而不會從站台伺服器上的內容庫移除內容。

安裝 Technical Preview 1612 之後，您可以在 Technical Preview 站台伺服器上的 *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* 資料夾中找到 **ContentLibraryCleanup.exe**。

隨此 Technical Preview 發行的工具是為了取代針對過去 Configuration Manager 產品所發行的類似舊版工具。 雖然此工具版本將在 2017 年 3 月 1 日之後停止運作，但在未來 Technical Preview 發行新版本之前，此工具會當作最新分支的一部分或已準備好用於生產環境的頻外版本發行。

### <a name="requirements"></a>需求  
- 您可以在裝載發佈點的電腦上直接執行此工具，或從另一部伺服器遠端執行此工具。 一次只能針對單一發佈點執行此工具。
- 執行此工具的使用者帳戶必須直接具有相當於 Configuration Manager 階層上系統高權限管理員之以角色為基礎的系統管理權限。  如果將具有系統高權限管理員權限的 Windows 安全性群組成員權限授與使用者帳戶，此工具將無法運作。

### <a name="modes-of-operation"></a>作業模式
此工具可以在下列兩種模式中執行：
1. **假設狀況模式**：   
   如果您未指定 **/delete** 參數，此工具會在假設狀況模式中執行，並識別要從發佈點刪除的內容，但不會實際刪除任何資料。

   - 當此工具在此模式中執行時，要刪除之內容的相關資訊會自動寫入至工具記錄檔。 系統不會提示使用者確認每個可能的刪除動作。
   - 根據預設，記錄檔會寫入至您執行工具之電腦上的使用者暫存資料夾，不過您可以使用 /log 參數將記錄檔重新導向至其他位置。  
   </br>

   建議您在此模式中執行工具並檢閱產生的記錄檔，再搭配 /delete 參數執行此工具。  

2. **刪除模式**：當您搭配 **/delete** 參數執行此工具時，此工具會在刪除模式中執行。

   - 當工具在此模式中執行時，您可以從發佈點的內容庫刪除指定發佈點上所發現的孤立內容。
   -  在刪除每個檔案之前，系統會提示使用者確認應刪除檔案。  您可以選取 **Y** 表示是、選取 **N** 表示否，或選取 [全部皆是]  略過接下來的提示並刪除所有孤立的內容。  
   </br>

   建議您在假設狀況模式中執行工具並檢閱產生的記錄檔，再搭配 /delete 參數執行此工具。  

當內容庫清理工具在任一種模式中執行時，它會自動建立記錄，其名稱包含此工具的執行模式、發佈點名稱、操作的日期和時間。 當工具完成時，會自動開啟記錄檔。 根據預設，此記錄會寫入至您執行工具之電腦上的使用者**暫存**資料夾。不過，您可以使用命令列參數將記錄檔重新導向至其他位置，包括網路共用。   


### <a name="run-the-tool"></a>執行工具
執行工具：
1. 請在包含 **ContentLibraryCleanup.exe** 的資料夾開啟系統管理命令提示字元。  
2. 接著輸入命令列，其中包含必要的命令列參數及您要使用的選擇性參數。

**已知問題** 執行此工具時，如果有任何套件或部署失敗或正在進行中，可能會傳回類似下列錯誤︰
-  *System.InvalidOperationException：因為套件 \<packageID> 未完全安裝，所以目前無法清除此內容庫。*

**因應措施：** 無。 正在進行部署或無法部署內容時，此工具無法可靠識別孤立的檔案。 因此，在解決該問題之前，此工具不允許您清除內容。



### <a name="command-line-switches"></a>命令列參數  
您可以依任何順序使用下列命令列參數。   

|參數|詳細資料|
|---------|-------|
|**/delete**  |**選擇性** </br> 當您要從發佈點刪除內容時，請使用此參數。 刪除內容之前，您會收到提示。 </br></br> 未使用此參數時，工具會記錄要刪除之內容的相關結果，但不會從發佈點刪除任何內容。 </br></br> 範例：***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**選擇性** </br> 以無訊息模式執行此工具會隱藏所有提示 (例如刪除內容時的提示)，而且不會自動開啟記錄檔。 </br></br> 範例：***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;發佈點 FQDN>**  | **必要** </br> 指定您要清除之發佈點的完整網域名稱 (FQDN)。 </br></br> 範例：***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;主要站台 FQDN>**       | 從主要站台的發佈點清除內容時為**選擇性**。</br>從次要站台的發佈點清除內容時為**必要**。 </br></br> 指定發佈點所屬之主要站台的 FQDN，或發佈點在次要站台時之父主要站台的 FQDN。 </br></br> 範例：***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;主要站台碼>**  | 從主要站台的發佈點清除內容時為**選擇性**。</br>從次要站台的發佈點清除內容時為**必要**。 </br></br> 指定發佈點所屬之主要站台的站台碼，或發佈點在次要站台時之父主要站台的站台碼。</br></br> 範例：***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log \<記錄檔目錄>**       |**選擇性** </br> 指定要放置記錄檔的目錄。 這可以是本機磁碟機或在網路共用上。</br></br> 未使用此參數時，記錄檔會自動放在使用者暫存資料夾中。</br></br> 本機磁碟機的範例：***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>網路共用的範例：***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;共用>\&lt;資料夾>***|


## <a name="improvements-for-in-console-search"></a>主控台內搜尋的新增功能
根據 UserVoice 意見反應，我們新增了主控台內搜尋的下列新增功能：
- **物件路徑︰**  
  許多物件現在支援名為 [物件路徑]  的新欄位。  當您搜尋並將此欄位包含在顯示結果時，您可以檢視每個物件的路徑。 例如，如果您對 [應用程式] 節點中的應用程式執行搜尋，而且也要搜尋子節點，結果窗格中的 [物件路徑]  欄會顯示所傳回之每個物件的路徑。   

- **保留搜尋文字︰**  
  當您在搜尋文字方塊中輸入文字，並切換搜尋子節點和目前的節點時，所輸入的文字現在會保存並可供新搜尋使用，而不必重新輸入。

- **保留搜尋子節點的決定︰**  
  當您變更所使用的節點時，現在會保存您選取用來搜尋「目前節點」  或「所有子節點」  的選項。   此新行為表示當您在主控台中四處移動時，不需要不斷地重設決定。  根據預設，當您開啟主控台時，會選擇只搜尋目前的節點。

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>防止在指定的程式正在執行時安裝應用程式
您現在可以在部署類型內容中設定可執行檔清單 (副檔名為 .exe)，執行時將會封鎖安裝應用程式。 嘗試安裝之後，使用者會看到對話方塊，要求他們關閉封鎖安裝的處理程序。

### <a name="try-it-out"></a>試試看
設定可執行檔清單
1. 在任何部署類型的內容頁面上，選擇 「Installer Handling」 (安裝程式處理)  索引標籤。
2. 按一下 [新增]  將其中一個可執行檔新增至清單 (例如 **Edge.exe**)
3. 按一下 [確定]  關閉部署類型內容對話方塊。

現在，當您將此應用程式部署給使用者或裝置，而且您新增的其中一個可執行檔正在執行時，使用者會看到 [軟體中心] 對話方塊，告訴他們因為應用程式正在執行，所以安裝失敗。

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>新增針對使用者的 Windows Hello 企業版通知

新的 Windows 10 通知會告知使用者為完成 Windows Hello 企業版安裝程式所需採取的其他動作 (例如設定 PIN 碼)。

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Configuration Manager 中的商務用 Windows 市集支援

您現在可以將商務用 Windows 市集中部署目的為 [可用]  的線上授權應用程式，部署到執行 Configuration Manager 用戶端的電腦。
如需詳細資訊，請參閱[使用 Configuration Manager 管理從商務用 Windows 市集購買的應用程式](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。

目前只會將這項功能的支援提供給執行 Windows 10 RS2 預覽版的電腦。

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>工作順序失敗時返回上一頁
當您執行工作順序並失敗時，現在可以返回上一頁。 在此版本之前，您必須在失敗時重新啟動工作順序。 例如，您可以在下列情況下使用 [上一步]  按鈕：

- 當電腦在 Windows PE 中啟動時，在工作順序可用之前，可能會顯示工作順序啟動程序對話方塊。 當您在此情況下按一下 [下一步] 時，工作順序的最後一頁會顯示訊息，指出沒有工作順序可用。 現在，您可以按一下 [上一步]  重新搜尋可用的工作順序。 您可以重複此程序直到工作順序可用為止。
- 當您執行工作順序，但發佈點上尚未提供相依內容套件時，工作順序將會失敗。 您現在可以發佈遺失內容 (如果尚未發佈) 或等候發佈點上的內容可供使用，然後按一下 [上一步]  讓工作順序再次搜尋內容。

## <a name="express-installation-files-support-for-windows-10-updates"></a>Windows 10 更新的快速安裝檔案支援
我們在 Configuration Manager 中新增了 Windows 10 更新的快速安裝檔案支援。 當您使用支援的 Windows 10 版本時，您現在可以使用 Configuration Manager 設定，只下載目前月份的 Windows 10 累積更新與上個月更新之間的差異。 目前在 Configuration Manager 最新分支中，每個月會下載完整 Windows 10 累積更新 (包括過去幾個月的所有更新)。 使用快速安裝檔案可在用戶端提供較小的下載項目及更快速的安裝時間。

> [!IMPORTANT]
> 雖然 Configuration Manager 提供支援使用快速安裝檔案的設定，但是只有套用 2017 年 1 月 10 日所發行更新 (Patch Tuesday) 隨附之 Windows Update 代理程式更新的 Windows 10 1607 版才支援這項功能。 如需這些更新的詳細資訊，請參閱[支援文章 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693)。 在 2017 年 2 月 14 日發行下一組更新時，您可以利用快速安裝檔案。 不含更新的 Windows 10 1607 版和舊版不支援快速安裝檔案。


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>在伺服器上下載 Windows 10 更新的快速安裝檔案
若要啟動 Windows 10 快速安裝檔案的中繼資料同步處理，您必須在 [軟體更新點內容] 中將它啟用。
1. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [站台設定]   > [站台]  。
2. 選取管理中心網站或獨立主要站台。
3. 在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件]  ，然後按一下 [軟體更新點]  。 在 [更新檔案]  索引標籤上，選取 [Download full files for all approved updates and express installation files for Windows 10] \(下載所有核准更新的完整檔案和 Windows 10 的快速安裝檔案)  。

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>啟用用戶端支援以下載並安裝快速安裝檔案
若要啟用用戶端的快速安裝檔案支援，您必須在用戶端設定的 [軟體更新] 區段中，啟用用戶端的快速安裝檔案。 這會建立新的 HTTP 接聽程式，以在您指定的連接埠上接聽下載快速安裝檔案的要求。 在您部署用戶端設定以在用戶端上啟用這項功能之後，該功能會嘗試下載目前月份的 Windows 10 累積更新與上個月更新之間的差異 (用戶端必須執行支援快速安裝檔案的 Windows 10 版本)。
1. 在 [軟體更新點元件內容] \(上一個程序) 中啟用快速安裝檔案的支援。
2. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [用戶端設定]  。
3. 選取適當的用戶端設定，然後在 [首頁]  索引標籤上，按一下 [內容]  。
4. 選取 [軟體更新]  頁面，在 [啟用安裝用戶端上的 Express Updates]  設定中設定 [是]  ，然後在 [Port used to download content for Express Updates] \(連接埠, 用來下載 Express Updates 的內容)  設定中設定用戶端上的 HTTP 接聽程式所使用的連接埠。


## <a name="odata-endpoint-data-access"></a>OData 端點資料存取

 Configuration Manager 現在提供用於存取 Configuration Manager 資料的 RESTful OData 端點。 此端點與 Odata 第 4 版相容，可讓 Excel 和 Power BI 等工具輕鬆地透過單一端點存取 Configuration Manager 資料。 Technical Preview 1612 只支援 Configuration Manager 中物件的讀取存取權。  

[Configuration Manager WMI 提供者](../../develop/reference/configuration-manager-reference.md)中目前可用的資料現在也可透過新的 OData RESTful 端點存取。 OData 端點所公開的實體集可讓您列舉使用 WMI 提供者所能查詢的相同資料。

### <a name="try-it-out"></a>試試看

您必須針對站台啟用 OData 端點，才能使用端點。

1.  移至 [系統管理]   > [站台設定]   > [站台]  。
2.  選取主要站台，然後按一下 [內容]  。
3.  在 [主要站台內容] 工作表的 [一般] 索引標籤上，按一下 [Enable REST endpoint for all providers on this site] \(為此站台上的所有提供者啟用 REST 端點)  ，然後按一下 [確定]  。

在您最愛的 OData 查詢檢視器中，嘗試類似下列範例的查詢，以傳回 Configuration Manager 中的各種物件：

| 目的 | OData 查詢 |
|---|---|
| 取得所有集合 | `http://localhost/CMRestProvider/Collection` |
| 取得一個集合 | `http://localhost/CMRestProvider/Collection('SMS00001')`
| 取得集合中的前 100 部裝置 | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| 取得集合中具有資源識別碼的裝置 | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| 取得集合中之裝置的作業系統 | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| 取得集合中的使用者 | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> 表格中所顯示的範例查詢使用 *localhost* 作為 URL 中的主機名稱，可在執行 SMS 提供者的電腦上使用。 如果您要從其他電腦執行查詢，請以安裝 SMS 提供者之伺服器的 FQDN 來取代 localhost。

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory 上架

Azure Active Directory (AD) 上架會建立 Configuration Manager 與 Azure Active Directory 之間的連線，以供其他雲端服務使用。 這目前可用於建立雲端管理閘道所需的連線。

請以 Azure 系統管理員身分執行此工作，因為您將需要 Azure 系統管理認證。

#### <a name="to-create-the-connection"></a>若要建立連線：

2. 在 [系統管理]  工作區中，選擇 [雲端服務]   > [Azure Active Directory]   > [新增 Azure Active Directory]  。
2. 選擇 [登入]  建立與 Azure AD 的連線。

#### <a name="configuration-manager-client-requirements"></a>Configuration Manager 用戶端需求

在雲端管理閘道中建立使用者原則有幾個需求。

- 您必須完成 Azure AD 上架程序，而且必須先將用戶端連線到公司網路以取得連線資訊。
- 用戶端必須同時加入網域 (已在 Active Directory 中登錄) 和雲端網域 (已在 Azure AD 中登錄)。
- 您必須執行 [Active Directory 使用者探索](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。
- 您必須修改 Configuration Manager 用戶端，以允許透過網際網路提出使用者原則要求，並將變更部署至用戶端。 因為用戶端的這項變更是在「用戶端裝置」  上進行，所以可透過雲端管理閘道進行部署，不過您尚未完成使用者原則所需的設定變更。
- 您的管理點必須設定為使用 HTTPS 保護網路上的權杖，而且必須安裝 .NET 4.5。

在您進行這些設定變更之後，即可建立使用者原則，並將用戶端移至網際網路以測試原則。 透過雲端管理閘道的使用者原則要求會使用 Azure AD 權杖型驗證進行驗證。

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>設定裝置註冊之 Multi-Factor Authentication 的變更

現在，您可以在 Azure 入口網站中設定裝置註冊的 Multi-Factor Authentication (MFA)，Configuration Manager 主控台中已移除 MFA 選項。 您可以在[此 Microsoft Intune 主題](/mem/intune/enrollment/multi-factor-authentication)中，找到有關設定註冊之 MFA 的詳細資訊。
