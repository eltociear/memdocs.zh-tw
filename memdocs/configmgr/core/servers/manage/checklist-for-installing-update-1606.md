---
title: 1606 的檢查清單
titleSuffix: Configuration Manager
description: 了解從 Configuration Manager 1511 版或 1602 版更新至 1606 版之前所採取的動作。
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707406"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>安裝 Configuration Manager 1606 版更新的檢查清單

適用於：  Configuration Manager (最新分支)

您可以使用 Configuration Manager 1606 版最新分支這項更新，從 1511 或 1602 版進行更新。

安裝 1606 版作為更新之前，請檢閱下列資訊和檢查清單，以了解開始更新之前應採取的動作。

如需基準版本的資訊，請參閱 [Configuration Manager 的更新](../../../core/servers/manage/updates.md)中的[基準和更新版本](../../../core/servers/manage/updates.md#bkmk_Baselines)。

## <a name="about-installing-update-1606"></a>關於安裝更新 1606

作為「更新」  ，1606 只能安裝在階層的頂層站台。 這表示您從管理中心網站 (如果有的話) 或獨立主要站台起始安裝。  

- 管理中心網站完成安裝更新之後，子主要站台會自動安裝更新。 您可以使用服務保留時間來控制站台安裝更新的時間。 在 1606 版之前，維護時段稱為維護期間。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](service-windows.md)。  

- 在主要父站台完成安裝更新後，您必須從 Configuration Manager 主控台內手動更新次要站台。 不支援次要站台伺服器的自動更新。  

當站台伺服器安裝更新時，安裝在站台伺服器上及遠端電腦上的站台系統角色會自動更新。 因此，安裝更新之前，請確定每個站台系統伺服器都符合任何使用新更新版本的新必要條件。  

在安裝更新後第一次使用 Configuration Manager 主控台時，系統會提示您更新該主控台。  若要這麼做，您必須在裝載該主控台的電腦上執行 Configuration Manager 安裝程式，並選擇更新主控台的選項。 建議您不要延遲安裝主控台更新。

**此更新的已知問題**   
下列問題適用於檢視更新套件安裝狀態時：
- 從 1602 版更新至 1606 版時，[解壓縮更新套件裝載]  步驟會顯示 [未開始]  狀態，即使下載已完成亦然。
- 從 1511 版更新至 1606 版時，某些步驟會顯示 [已完成]  狀態，但不會顯示 [上次更新時間]  的值。


## <a name="checklist"></a>檢查清單  

**請確保所有站台都執行支援版本的 Configuration Manager：** 階層中的每個站台伺服器皆必須執行相同版本的 Configuration Manager，您才能開始安裝更新 1606：1511 或 1602 版。

**檢閱站台系統伺服器上已安裝的 Microsoft .NET 版本：** 當站台安裝更新 1606 時，Configuration Manager 會自動在每一部裝載下列其中一個站台系統角色的電腦上安裝 .NET Framework 4.5.2 (當尚未安裝 .NET Framework 4.5 或更新版本時)：  

- 註冊 Proxy 點  

- 註冊點  

- 管理點  

- 服務連接點  

這項安裝會讓站台系統伺服器處於重新開機擱置中狀態，並將錯誤回報給 Configuration Manager 元件狀態檢視器。 此外，伺服器上的 .NET 應用程式於伺服器重新開機之前可能會有隨機失敗。  

如需詳細資訊，請參閱[站台和站台系統先決條件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

**檢閱站台和階層狀態，並確認沒有任何未解決的問題：** 在更新站台之前，請先針對站台伺服器、站台資料庫伺服器，以及安裝在遠端電腦上的站台系統角色，解決所有操作問題。 網站更新會因為現有的操作問題而失敗。

如需詳細資訊，請參閱[使用 Configuration Manager 的警示和狀態系統](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

**檢閱站台間的檔案和資料複寫︰** 確認站台之間的檔案和資料庫複寫正在運作且為最新狀態。 延遲或待辦項目可能會造成無法順暢並成功地更新。    

針對資料庫複寫，您可以使用「複寫連結分析師」來協助您解決問題，再開始更新。 如需詳細資訊，請參閱[關於複寫連結分析師](monitor-replication.md#BKMK_RLA)。  


**為裝載站台、站台資料庫伺服器及遠端站台系統角色之電腦上的作業系統，安裝全部適用的重大更新：** 在為 Configuration Manager 安裝更新之前，請先為每個適用的站台系統安裝所有重大更新。 如果您安裝的更新需要重新啟動，請先重新啟動適用的電腦再開始進行更新。  

**在主要站台上停用管理點的資料庫複本：** Configuration Manager 無法成功更新具有已啟用管理點之資料庫複本的主要站台。 請停用資料庫複寫後，再安裝 Configuration Manager 的更新。  

如需詳細資訊，請參閱 [Configuration Manager 的管理點資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

**將 SQL Server AlwaysOn 可用性群組設定為手動容錯移轉：**  
安裝更新之前 (像是 1606 版本)，請確定可用性群組已設為手動容錯移轉。 站台更新之後，您可以還原為自動容錯移轉。 如需詳細資訊，請參閱[站台資料庫的 SQL Server AlwaysOn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

**重新設定使用 NLB 的軟體更新點：** Configuration Manager 無法更新使用網路負載平衡 (NLB) 叢集的站台以裝載軟體更新點。  

如果您將 NLB 叢集用於軟體更新點，請使用 Windows PowerShell 移除 NLB 叢集。    

如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。  

**停用該站台更新安裝期間，各站台的所有站台維護工作：** 在您安裝更新之前，請停用任何可能在進行更新程序期間執行的站台維護工作。 這包括但不限於下列項目：  

- 備份網站伺服器  

- 刪除過時用戶端操作  

- 刪除過時探索資料  

於更新安裝期間執行站台資料庫維護工作，更新安裝可能會失敗。 在停用工作前，請將工作的排程記錄下來，以便在安裝更新後還原其設定。  

如需詳細資訊，請參閱 [Configuration Manager 的維護工作](../../../core/servers/manage/maintenance-tasks.md)和 [Configuration Manager 的維護工作參考](../../../core/servers/manage/reference-for-maintenance-tasks.md)。 

**暫時停止 Configuration Manager 伺服器上的所有防毒軟體：** 更新站台之前，請先確定您已停止 Configuration Manager 伺服器上的防毒軟體。 <!--SMS.503481--> 

**在管理中心網站和主要站台上建立站台資料庫的備份：** 更新站台之前，請先備份站台資料庫，以確保您有成功的備份可供災害復原使用。   

如需詳細資訊，請參閱 [Configuration Manager 備份和復原](backup-and-recovery.md)。  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**規劃用戶端試驗：** 當您安裝更新用戶端的更新時，可以在進入生產階段前先測試新的用戶端更新，再部署並升級所有使用中的用戶端。   

若要利用這個選項，在開始安裝更新之前，您必須將您的站台設定為支援進入生產階段前自動升級。 如需詳細資訊，請參閱[升級用戶端](../../../core/clients/manage/upgrade/upgrade-clients.md)和   
[如何在生產階段前集合中測試用戶端升級](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

**規劃使用服務保留時間來控制站台伺服器安裝更新的時間：** 您可以使用服務保留時間定義站台伺服器的更新要安裝的時段。

這可協助您控制階層中的站台要於何時安裝更新。
在 1606 版之前，維護時段稱為維護期間。 如需詳細資訊，請參閱[站台伺服器的服務保留時間](service-windows.md)。  

**執行安裝程式先決條件檢查程式：** 在安裝更新 1606 之前，您可以在安裝更新程序之外，獨立執行必要條件檢查程式。 當您在站台上安裝更新時，會再次執行必要條件檢查工具。  

如需詳細資訊，請參閱**步驟 3:安裝更新之前執行必要條件檢查工具**中的 [Configuration Manager 的更新](../../../core/servers/manage/install-in-console-updates.md)主題。  

> [!IMPORTANT]  
> 當必要條件檢查工具獨立執行時，或作為更新安裝的一部分執行時，處理序會更新站台維護作業所使用的部分產品來源檔案。 因此，在執行必要條件檢查程式之後、安裝 1606 更新之前，如果您必須執行站台維護工作，請從站台伺服器上的 CD.Latest 資料夾執行 **Setupwpf.exe** (Configuration Manager 安裝程式)。  

**更新站台：** 您現在已準備好開始安裝階層的更新。  
建議您規劃在正常上班以外的時間對各個站台安裝更新，在這些時間內安裝更新的程序及其重新安裝站台元件和站台系統角色的動作，對您的商務營運所產生的影響最小。

如需詳細資訊，請參閱 [Configuration Manager 的更新](../../../core/servers/manage/updates.md)。  
