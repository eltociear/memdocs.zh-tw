---
title: 1902 的檢查清單
titleSuffix: Configuration Manager
description: 了解更新至 Configuration Manager 1902 版之前要採取的動作。
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 150194be4d7d2fa07fb868e9a5f65f52f3bdd768
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707666"
---
# <a name="checklist-for-installing-update-1902-for-configuration-manager"></a>安裝 Configuration Manager 1902 版更新的檢查清單

適用於：  Configuration Manager (最新分支)

當您使用 Configuration Manager 的最新分支時，可以安裝 1902 版的主控台內更新，以更新您舊版的階層。 <!-- baseline only statement:-->(因為 1902 版也可作為[基準媒體](updates.md#bkmk_Baselines)，所以您可以使用安裝媒體來安裝新階層的第一個站台)。

若要取得 1902 版的更新，您必須在階層的頂層站台使用服務連接點。 這個站台系統角色可以是線上或離線模式。 您的階層從 Microsoft 下載更新套件之後，就能在主控台中找到它。 請在 [系統管理]  工作區中，選取 [更新與服務]  節點。

-   當更新列為 [可用]  時，即表示更新已準備好安裝。 安裝 1902 版之前，請檢閱下列[關於安裝 1902 版更新](#about-installing-update-1902)和[檢查清單](#checklist)的資訊，以了解開始更新之前應進行的設定。

-   如果更新顯示為 [正在下載]  且未變更，請檢閱 **hman.log** 和 **dmpdownloader.log** 中的錯誤。

    -   dmpdownloader.log 可能指出 dmpdownloader 處理序在檢查更新之前會等候間隔的時間。 若要重新開始下載更新的重新發佈檔案，請在站台伺服器上重新啟動 **SMS_Executive** 服務。

    -   另一個常見的下載問題發生於 Proxy 伺服器設定防止從 `silverlight.dlservice.microsoft.com`、`download.microsoft.com` 和 `go.microsoft.com` 下載時。

如需安裝更新的詳細資訊，請參閱[主控台內更新及服務](updates.md#bkmk_inconsole)。

如需最新分支版本的詳細資訊，請參閱[基準和更新版本](updates.md#bkmk_Baselines)。



## <a name="about-installing-update-1902"></a>關於安裝 1902 版更新

#### <a name="sites"></a>網站
1902 版的更新會安裝在您階層的頂層站台上。 請從管理中心網站或獨立主要站台開始安裝。 在頂層站台安裝更新之後，子站台會有下列更新行為：

-   當管理中心網站完成安裝更新之後，子主要站台就會自動安裝更新。 您可以使用服務保留時間來控制站台安裝更新的時間。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](service-windows.md)。

-   在主要父站台完成更新安裝後，從 Configuration Manager 主控台內手動更新每一個次要站台。 不支援次要站台伺服器的自動更新。

#### <a name="site-system-roles"></a>網站系統角色
當站台伺服器安裝更新時，它會自動更新所有的站台系統角色。 這些角色位在站台伺服器上，或安裝在遠端伺服器上。 在安裝更新之前，請確定每個站台系統伺服器都符合新更新版本的最新必要條件。

#### <a name="configuration-manager-consoles"></a>Configuration Manager 主控台   
在完成更新後第一次使用 Configuration Manager 主控台時，系統會提示您更新該主控台。 您也可以在裝載該主控台的電腦上執行 Configuration Manager 安裝程式，並選擇更新主控台的選項。 盡快在主控台中安裝更新。 如需詳細資訊，請參閱[安裝 Configuration Manager 主控台](../deploy/install/install-consoles.md)。

> [!IMPORTANT]  
> 當您在管理中心網站安裝更新時，在所有子主要站台也都完成更新安裝之前，請注意下列限制和存在的延遲︰    
> - **用戶端升級**不會開始。 這包括自動更新用戶端與進入生產階段前的用戶端。 此外，在最後一個站台完成更新安裝之前，您無法升級到進入生產階段前的用戶端。 最後一個站台完成更新安裝之後，才會根據您的組態選擇開始用戶端升級。   
> - 您透過更新啟用的「新功能」  無法使用。 這是為了防止將與該功能相關資料複寫到尚未安裝該功能支援的網站。 所有主要站台都安裝更新之後，才能夠使用該功能。   
> - 管理中心網站與子主要站台間的**複寫連結**會顯示為未升級。 這會在更新套件安裝狀態中顯示為 [已完成] 狀態，但出現 [正在監視複寫初始化] 的警告。 在主控台的 [監視] 節點中，這會顯示為 [正在設定連結]  。


## <a name="checklist"></a>檢查清單

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>所有站台執行支援的 Configuration Manager 版本  
階層中的每個站台伺服器都必須執行 Configuration Manager 相同版本，您才能開始安裝 1902 版更新。 若要更新至 1902 版，您必須使用 1802、1806 或 1810 版。

#### <a name="review-the-status-of-your-product-licensing"></a>檢閱您的產品授權狀態 
您必須擁有作用中的「軟體保證 (SA) 合約」或對等訂閱權限，才能安裝此更新。 當您更新此站台時，[授權]  頁面會顯示選項以確認您的 [軟體保證到期日]  。

這是選擇性的值。 您可以視授權到期日提醒需要加以指定。 當您安裝未來的更新時，會顯示這個日期。 您之前可能已在設定或安裝更新期間指定此值。 您也可以在 Configuration Manager 主控台中指定此值。 在 [系統管理]  工作區中，展開 [站台設定]  ，然後選取 [站台]  。 選取功能區中的 [階層設定]  ，並切換至 [授權]  索引標籤。

如需詳細資訊，請參閱[授權和分支](../../understand/learn-more-editions.md)。

#### <a name="review-microsoft-net-versions"></a>檢閱 Microsoft .NET 版本 
當網站安裝此更新時，若沒有安裝最低需求的 .NET Framework 4.5，Configuration Manager 將會自動安裝 .NET Framework 4.5.2。 尚未安裝這項必要條件時，站台會將其安裝在裝載下列其中一個站台系統角色的每一部伺服器上：

-   管理點
-   服務連接點
-   註冊 Proxy 點
-   註冊點

這項安裝會讓站台系統伺服器處於重新開機擱置中狀態，並將錯誤回報給 Configuration Manager 元件狀態檢視器。 此外，伺服器上的 .NET 應用程式於伺服器重新啟動之前可能遇到隨機失敗。

如需詳細資訊，請參閱 [站台和站台系統必要條件](../../plan-design/configs/site-and-site-system-prerequisites.md)。

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>檢閱適用於 Windows 10 的 Windows ADK 版本
Configuration Manager 1902 版應該支援 Windows 10 評定及部署套件 (ADK) 的版本。 如需支援的 Windows ADK 版本詳細資訊，請參閱 [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk)。 如果您必須更新 Windows ADK，請在開始更新 Configuration Manager 之前進行。 此順序可確保預設開機映像會自動更新至最新版的 Windows PE。 在更新站台後手動更新任何自訂開機映像。

如果您在更新 Windows ADK 之前更新站台，請參閱[使用開機映像更新發佈點](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)。

#### <a name="review-sql-server-native-client-version"></a>檢閱 SQL Server Native Client 版本
SQL Server 2012 Native Client 的最低版本，而且必須安裝對 TLS 1.2 的支援。 如需詳細資訊，請參閱[先決條件檢查清單](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>檢閱站台和階層狀態以找出未解決的問題 
網站更新會因為現有的操作問題而失敗。 更新站台之前，請先針對下列系統解決所有操作問題：  
- 站台伺服器  
- 站台資料庫伺服器  
- 其他伺服器上的遠端站台系統角色   

如需詳細資訊，請參閱 [使用警示和狀態系統](use-alerts-and-the-status-system.md)。

#### <a name="review-file-and-data-replication-between-sites"></a>檢閱站台之間的檔案和資料複寫   
確認站台之間的檔案和資料庫複寫正在運作且為最新狀態。 延遲或待辦項目可能會造成無法順暢並成功地更新。 針對資料庫複寫，您可以使用「複寫連結分析師」來協助您解決問題，再開始更新。

如需詳細資訊，請參閱[關於複寫連結分析師](monitor-replication.md#BKMK_RLA)。

#### <a name="install-all-applicable-critical-windows-updates"></a>安裝所有適用的重大 Windows 更新
在安裝 Configuration Manager 的更新之前，請針對每一個適用的站台系統安裝任何重大 OS 更新。 這些伺服器包括站台伺服器、站台資料庫伺服器，以及遠端站台系統角色。 如果您安裝的更新需要重新啟動，請先重新啟動適用的伺服器，再開始進行更新。

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>在主要站台上停用管理點的資料庫複本   
Configuration Manager 無法成功更新具有已啟用管理點之資料庫複本的主要站台。 在安裝 Configuration Manager 的更新之前，請停用資料庫複寫。

如需詳細資訊，請參閱[管理點的資料庫複本](../deploy/configure/database-replicas-for-management-points.md)。

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>將 SQL Server AlwaysOn 可用性群組設定為手動容錯移轉   
如果您使用可用性群組，請務必在開始安裝更新之前，將可用性群組設定為手動容錯移轉。 站台更新之後，您可以還原為自動容錯移轉。 如需詳細資訊，請參閱 [站台資料庫的 SQL Server AlwaysOn](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>停用每個站台的站台維護工作
在您安裝更新之前，請停用任何可能在進行更新程序期間執行的站台維護工作。 例如 (但不限於)：

-   備份網站伺服器
-   刪除過時用戶端操作
-   刪除過時探索資料

於更新安裝期間執行站台資料庫維護工作，更新安裝可能會失敗。 在停用工作前，請將工作的排程記錄下來，以便在安裝更新後還原其設定。

如需詳細資訊，請參閱 [維護工作](maintenance-tasks.md) 和[維護工作的參考](reference-for-maintenance-tasks.md)。

#### <a name="temporarily-stop-any-antivirus-software"></a>暫時停止任何防毒軟體 
在更新站台之前，請在 Configuration Manager 伺服器上停止防毒軟體。 防毒軟體可以鎖定一些需要更新的檔案，導致我們的更新失敗。 <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>建立站台資料庫的備份 
在更新站台之前，請在管理中心網站和主要站台上備份站台資料庫。 此備份可確保您擁有可供災害復原使用的成功備份。

如需詳細資訊，請參閱 [備份和復原](backup-and-recovery.md)。

#### <a name="plan-for-client-piloting"></a>規劃用戶端試驗   
當您安裝更新用戶端的更新時，可以在進入生產階段前先測試新的用戶端更新，再部署並升級所有使用中的用戶端。 若要利用這個選項，在開始安裝更新之前，您必須將您的站台設定為支援進入生產階段前自動升級。

如需詳細資訊，請參閱 [升級用戶端](../../clients/manage/upgrade/upgrade-clients.md) 和[如何測試進入生產階段前集合的用戶端升級](../../clients/manage/upgrade/test-client-upgrades.md)。

#### <a name="plan-to-use-service-windows"></a>規劃使用維護時段   
若要定義安裝站台伺服器更新的時段，請使用維護時段。 這可協助您控制階層中的站台要於何時安裝更新。 如需詳細資訊，請參閱 [站台伺服器的服務保留時間](service-windows.md)。

#### <a name="review-supported-extensions"></a>檢閱支援的延伸模組
<!--SCCMdocs#587-->
如果您使用 Microsoft 或 Microsoft 合作夥伴的其他產品來擴充 Configuration Manager，請確認這些產品都支援 1902 版。 請與產品廠商確認這項資訊。 例如，請參閱 Microsoft Deployment Toolkit [版本資訊](../../../mdt/release-notes.md)。

#### <a name="run-the-setup-prerequisite-checker"></a>執行安裝程式必要條件檢查工具   
當更新在主控台中列為 [可用]  時，您可以單獨執行必要條件檢查程式，再安裝更新 (當您在站台上安裝更新時，會再次執行必要條件檢查工具)。

若要從主控台執行必要條件檢查，請前往 [管理]  工作區，然後選取 [更新與服務]  。 選取 **Configuration Manager 1902** 更新套件，然後選取功能區中的 [執行先決條件檢查]  。

如需詳細資訊，請參閱[安裝主控台內更新之前](install-in-console-updates.md#bkmk_beforeinstall)中的**安裝更新之前先執行必要條件檢查工具**。

> [!IMPORTANT]  
> 當必要條件檢查工具執行時，處理序會更新站台維護工作所使用的部分產品來源檔案。 因此，執行必要條件檢查程式之後與安裝更新之前，如果您必須執行站台維護工作，請從站台伺服器上的 CD.Latest 資料夾執行  **Setupwpf.exe**  (Configuration Manager 安裝程式)。

#### <a name="update-sites"></a>更新站台   
您現在已準備好開始安裝階層的更新。 如需安裝更新的詳細資訊，請參閱[安裝主控台內更新](install-in-console-updates.md#bkmk_install)。

您可以規劃在正常營業時間以外安裝更新。 判定何時該處理序對企業營運的影響最小。 安裝更新及其動作會重新安裝站台元件和站台系統角色。

如需詳細資訊，請參閱  [Configuration Manager 的更新](updates.md)。



## <a name="post-update-checklist"></a>更新後檢查清單

進行站台更新之後，請使用下列檢查清單來完成常見的工作和設定。


#### <a name="confirm-version-and-restart-if-necessary"></a>確認版本並重新啟動 (如有必要)
請確定每個站台伺服器和站台系統角色均已更新為 1902 版。 在主控台中，將 [版本]  資料行新增至 [管理]  工作區中的 [站台]  和 [發佈點]  節點。 必要時，站台系統角色會自動重新安裝以更新為新版本。 

請考慮將一開始未成功更新的遠端站台系統重新啟動。 檢閱您的站台基礎結構，並確保適用的站台伺服器和遠端站台系統伺服器已成功重新啟動。 通常只有在 Configuration Manager 將 .NET 安裝為站台系統角色的必要項目時，站台伺服器才會重新啟動。


#### <a name="confirm-site-to-site-replication-is-active"></a>確認站台對站台複寫正在作用中
在 Configuration Manager 主控台中，移至下列位置來檢視狀態，並確認複寫處於作用中：  

-   [監視]  工作區、[站台階層]  節點  

-   [監視]  工作區、[資料庫複寫]  節點  

如需詳細資訊，請參閱下列文章：  

- [監視階層](monitor-hierarchy.md)
- [監視複寫](monitor-replication.md)
- [關於複寫連結分析師](monitor-replication.md#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>更新 Configuration Manager 主控台
將所有遠端 Configuration Manager 主控台更新為相同的版本。 系統會在下列時機提示您更新主控台：  

-   您開啟主控台。  

-   您在主控台中移至新節點。  


#### <a name="reconfigure-database-replicas-for-management-points"></a>為管理點重新設定資料庫複本
更新主要站台之後，請針對您更新站台前所解除安裝的管理點，重新設定資料庫複本。 如需詳細資訊，請參閱[管理點的資料庫複本](../deploy/configure/database-replicas-for-management-points.md)。  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>重新設定任何已停用的維護工作
如果您在安裝更新之前已停用站台上資料庫的[維護工作](maintenance-tasks.md)，請重新設定這些工作。 請使用更新前已存在的相同設定。  


#### <a name="update-clients"></a>更新用戶端
請依據您所建立的方案來更新用戶端，尤其是如果您在安裝更新之前已設定用戶端試驗的話。 如需詳細資訊，請參閱[如何升級 Windows 電腦的用戶端](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  


#### <a name="third-party-extensions"></a>協力廠商延伸模組
如果您使用 Configuration Manager 的任何延伸模組，請將其更新為最新版本以支援 Configuration Manager 1902 版。 


#### <a name="update-custom-boot-images-and-media"></a>更新自訂開機映像和媒體
<!--SCCMDocs issue 775-->

請針對您使用的任何開機映像 (不論是預設還是自訂開機映像)，使用 [更新發佈點]  動作。 此動作會確保用戶端能夠使用最新版本。 即使沒有新版的 Windows ADK，Configuration Manager 用戶端元件仍可能因更新而變更。 如果您未更新開機映像和媒體，工作順序部署就可能在裝置上發生失敗。 

當您更新站台時，Configuration Manager 會自動更新「預設」  開機映像。 它不會自動將更新過的內容散發至發佈點。 當您已準備好要將此內容散發至整個網路時，請在特定的開機映像上使用 [更新發佈點]  動作。 

在更新站台之後，請手動更新任何「自訂」  開機映像。 此動作會為開機映像更新最少的用戶端元件 (如有必要)、視需要為其重新載入目前的 Windows PE 版本，然後將內容重新散發至發佈點。 

如需詳細資訊，請參閱[使用開機映像更新發佈點](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)。 
