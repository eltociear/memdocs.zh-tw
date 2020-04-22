---
title: 備份站台
titleSuffix: Configuration Manager
description: 了解如何在失敗或資料遺失之前，在 Configuration Manager 中備份您的站台。
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 824eaeb939249e1bcc2ed21d5815a0a72dc54797
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700266"
---
# <a name="back-up-a-configuration-manager-site"></a>備份 Configuration Manager 站台

適用於：  Configuration Manager (最新分支)

準備備份和復原方法，以避免資料遺失。 對於 Configuration Manager 站台，備份和復原方法有助於您在遺失最少資料的情況下更快復原站台和階層。  

本文中的各節可協助您備份站台。 若要復原站台，請參閱 [Configuration Manager 的復原](recover-sites.md)。  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> Configuration Manager 站台復原支援以下兩種備份方法：
>
> - 來自**備份站台伺服器**維護工作的成功備份
> - 手動復原的站台資料庫備份


## <a name="considerations-before-creating-a-backup"></a>建立備份前的考量  

-   如果您使用 SQL Server Always On 可用性群組來裝載站台資料庫：請根據[準備使用 SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup) 中所述來修改備份和復原方案。  

-   Configuration Manager 可以從 Configuration Manager 備份工作復原站台資料庫。 它也可以使用您利用另一個程序所建立之站台資料庫的備份。   

     例如，您可以使用 Microsoft SQL Server 維護方案所建立的備份來還原站台資料庫。 您也可以使用以 Data Protection Manager 建立的備份來備份站台資料庫。  

-   從 1806 版開始，安裝「被動」  模式的額外站台伺服器。 被動模式的站台伺服器，是您現有「主動」  模式的站台伺服器以外的站台伺服器。 被動模式的站台伺服器可在有需要時立即使用。 如需詳細資訊，請參閱[站台伺服器高可用性](../deploy/configure/site-server-high-availability.md)。 雖然此角色不需要規劃和練習備份與復原作業，但可在必要時大幅減少復原站台所需的心力。  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>使用 Data Protection Manager 備份網站資料庫
您可以使用 System Center Data Protection Manager (DPM) 來備份 Configuration Manager 站台資料庫。

在站台資料庫電腦的 DPM 中建立新的保護群組。 在 [建立新保護群組精靈] 的 [選擇群組成員]  頁面上，您可以從資料來源清單選取 SMS 寫入器服務。 然後選取站台資料庫作為適當的成員。 如需使用 DPM 的詳細資訊，請參閱 [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) 文件庫。  

> [!IMPORTANT]  
>  Configuration Manager 不支援針對使用具名執行個體的 SQL Server 叢集執行 DPM 備份。 它確實支援在使用預設 SQL Server 執行個體的 SQL Server 叢集上執行 DPM 備份。  

在您還原站台資料庫後，請依照安裝程式中的步驟復原站台。 若要使用利用 Data Protection Manager 所備份的站台資料庫，請選取復原選項以**使用已手動復原的站台資料庫**。  



## <a name="backup-maintenance-task"></a>備份維護工作
您可以藉由排程預先定義的「備份站台伺服器」維護工作，自動備份 Configuration Manager 站台。 此工作具有下列功能：

-   依排程執行
-   備份站台資料庫
-   備份特定的登錄機碼
-   備份特定的資料夾和檔案
-   備份 [CD.Latest 資料夾](the-cd.latest-folder.md)   

規劃至少每隔五天執行預設站台備份工作。 此排程是因為 Configuration Manager 使用五天的「SQL Server 變更追蹤保留期間」  。 如需詳細資訊，請參閱 [SQL Server 變更追蹤保留期間](recover-sites.md#sql-server-change-tracking-retention-period)。

若要簡化備份程序，您可以建立 **AfterBackup.bat** 檔案。 備份工作順利完成之後，此指令碼會自動執行備份後動作。 使用 AfterBackup.bat 檔案，將備份快照封存至安全位置。 您也可以使用 AfterBackup.bat 檔案將檔案複製至備份資料夾，或啟動其他備份工作。  

您可以備份管理中心網站和主要站台。 次要站台或站台系統伺服器不需要備份工作。

Configuration Manager 備份服務執行時，會遵循備份控制檔案中所定義的指示：`<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`。 您可以修改備份控制檔案，以變更備份服務的行為。  
> [!NOTE]
> 在站台伺服器上重新啟動服務 SMS_SITE_VSS_WRITER 後，將會套用 **Smsbkup.ctl** 的修改。

站台備份狀態資訊會寫入至 **Smsbkup.log** 檔案。 此檔案會在您於「備份站台伺服器」維護工作屬性中指定的目的地資料夾中建立。  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>啟用網站備份維護工作  
1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2.  選取您要啟用站台備份維護工作的站台。  

3.  按一下功能區中的 [站台維護工作]  。  

4.  選取 [備份站台伺服器]  工作，然後按一下 [編輯]  。  

5.  選取 [Enable this task] \(啟用此工作\)  的選項。 按一下 [設定路徑]  以指定備份目的地。 下列選項可供您選擇：  

    > [!IMPORTANT]  
    >  若要預防備份檔案遭到竄改，請將檔案儲存在安全的位置。 最安全的備份路徑是本機磁碟機，因此您可以在資料夾上設定 NTFS 檔案權限。 Configuration Manager 不會加密備份路徑中所儲存的備份資料。  

    -   **用於站台資料和資料庫的站台伺服器本機磁碟機**：指定工作將站台和站台資料庫的備份檔案儲存在站台伺服器本機磁碟上所指定路徑。 先建立本機資料夾，再執行備份工作。 站台伺服器的本機系統帳戶必須擁有站台伺服器備份本機資料夾的**寫入** NTFS 檔案權限。 電腦若是執行 SQL Server，其本機系統帳戶必須擁有站台資料庫備份資料夾的**寫入** NTFS 權限。  

    -   **用於站台資料和資料庫的網路路徑 (UNC 名稱)** ：指定工作將站台和站台資料庫的備份檔案儲存在所指定網路路徑。 先建立共用，再執行備份工作。 站台伺服器的電腦帳戶必須擁有**寫入** NTFS，並共用與共用網路資料夾的權限。 如果另一部電腦安裝 SQL Server，則 SQL Server 的電腦帳戶必須具有相同的權限。  

    -   **站台伺服器和 SQL Server 本機磁碟機**：指定工作將站台的備份檔案儲存在站台伺服器本機磁碟機上所指定路徑。 工作將站台資料庫的備份檔案儲存在站台資料庫伺服器本機磁碟上指定的路徑。 先建立本機資料夾，再執行備份工作。 網站伺服器的電腦帳戶必須擁有您在網站伺服器上建立之資料夾的 **寫入** NTFS 權限。 SQL Server 的電腦帳戶必須擁有您在網站資料庫伺服器上建立之資料夾的 **寫入** NTFS 權限。 此選項僅在站台伺服器上未安裝站台資料庫時適用。  

    > [!NOTE]  
    > 只有在您指定備份目的地的網路路徑時，才能使用瀏覽備份目的地的選項。  
    >  
    > 用於不支援使用 Unicode 字元之備份目的地的資料夾名稱或共用名稱。  

6.  為站台備份工作設定排程。 請考慮將備份排定在非工作時間執行。 如果您有階層，請考慮一週至少執行兩次的排程。 如果站台失敗，則此排程可確保具有最大資料保留期。  

    當您在針對備份所設定的相同站台伺服器上執行 Configuration Manager 主控台時，備份工作會針對排程使用當地時間。 當您從另一部電腦執行 Configuration Manager 主控台時，備份工作會針對排程使用國際標準時間 (UTC)。  

7.  選擇是否要在站台備份工作失敗時建立警示。 選取時，Configuration Manager 會建立備份失敗的重大警示。 您可以在 [監視]  工作區的 [警示]  節點中檢閱這些警示。  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>確認「備份站台伺服器」維護工作正在執行  

-   檢查此工作所建立備份目的地資料夾中檔案的時間戳記。 確認時間戳記更新為上次排定執行工作的時間。  

-   移至 [監視]  工作區的 [元件狀態]  節點。 檢閱 **SMS_SITE_BACKUP** 的狀態訊息。 站台備份順利完成時，您會看到訊息識別碼 **5035**。 此訊息指出站台備份已完成，未發生任何錯誤。  

-   如果您設定備份工作以在失敗時建立警示，則請在 [監視]  工作區的 [警示]  節點中尋找備份失敗警示。  

-   在站台伺服器上開啟 Windows 檔案總管，並瀏覽至 `<ConfigMgrInstallationFolder>\Logs`。 檢閱 **Smsbkup.log** 中的警告和錯誤。 站台備份順利完成時，記錄會顯示 `Backup completed`，訊息識別碼為 `STATMSG: ID=5035`。  

    > [!TIP]  
    >  備份維護工作失敗時，請停止再重新啟動 **SMS_SITE_BACKUP** Windows 服務，重新啟動備份工作。  



## <a name="archive-the-backup-snapshot"></a>封存備份快照  
備份工作會在第一次執行時建立備份快照。 如果站台伺服器失敗，則您可以使用此快照復原站台伺服器。 備份工作在根據排程再次執行時，會建立可覆寫前一個快照的新備份快照。 因此，站台只有一個備份快照，您無法擷取舊版的備份快照。  

請針對下列原因保留多個備份快照封存：  

-   備份媒體失敗、錯置，或僅包含部分備份，都是常見狀況。 從過去的備份復原失敗的獨立主要網站總比完全沒有備份要來得好。 對於階層中的站台伺服器，備份必須是在 SQL Server 變更追蹤保留期間內，否則不需要備份。  

-   有可能在數個備份週期中都偵測不到網站損毀。 您可能必須使用站台損毀前的備份快照。 此原因適用於獨立主要站台以及其備份是在 SQL Server 變更追蹤保留期間內階層中的站台。  

-   站台可能完全沒有備份快照。 例如，「備份站台伺服器」維護工作失敗時。 因為備份工作會在開始備份目前資料前移除先前的備份快照，所以沒有有效的備份快照。  



## <a name="using-the-afterbackupbat-file"></a>使用 AfterBackup.bat 檔案  
順利備份站台之後，備份工作會自動嘗試執行名為 **AfterBackup.bat** 的指令碼。 在站台伺服器的 `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box` 中手動建立 AfterBackup.bat 檔案。 如果 AfterBackup.bat 檔案存在於正確的資料夾中，則會在備份工作完成後自動執行。

AfterBackup.bat 檔案可讓您在每個備份作業結束時封存備份快照。 它可以自動執行非「備份站台伺服器」維護工作一部分的其他備份後工作。 AfterBackup.bat 檔案會整合封存與備份操作，如此即可確保封存每個新的備份快照。

如果 AfterBackup.bat 檔案不存在，則備份工作會將其略過，而不影響備份作業。 若要確認備份工作是否已成功執行此指令碼，請移至 [監視]  工作區中的 [元件狀態]  節點，並檢閱 **SMS_SITE_BACKUP** 的狀態訊息。 工作成功啟動 Afterbackup.bat 命令檔時，您會看見訊息識別碼 **5040**。  

> [!TIP]  
>  若要使用 AfterBackup.bat 封存您的站台伺服器備份檔案，您必須在批次檔中使用複製命令工具。 Windows Server 的其中一個這類工具是 [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy)。 例如，使用下列命令建立 AfterBackup.bat 檔案：`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

雖然 AfterBackup.bat 的用途是封存備份快照，但您也可以建立 AfterBackup.bat 檔案，在每次備份作業結束時執行額外工作。  



##  <a name="supplemental-backup-tasks"></a>增補的備份工作  
「備份站台伺服器」維護工作提供站台伺服器檔案和站台資料庫的備份快照。 當您建立備份策略時，必須考慮其他未備份的項目。 使用下列各節可協助您完成 Configuration Manager 備份策略。  

### <a name="back-up-custom-reports"></a>備份自訂報表   
如果您在 SQL Server Reporting Services 中修改預先定義或建立的自訂報表，則請建立報表伺服器資料庫檔案的備份。 報表伺服器備份必須包含下列元件：
- 報表和模型的來源檔案
- 加密金鑰
- 自訂組件或延伸模組
- 設定檔
- 自訂報表中所使用的自訂 SQL Server 檢視
- 自訂預存程序  

> [!IMPORTANT]  
>  Configuration Manager 升級到較新版本時，新報告可能會覆寫預先定義的報告。 如果您修改預先定義的報表，請務必先備份報表，然後在 Reporting Services 中予以還原。  

如需備份 Reporting Services 中自訂報表的詳細資訊，請參閱 [Reporting Services 的備份與還原作業](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)。  

### <a name="back-up-content-files"></a>備份內容檔案  
Configuration Manager 中的內容庫是儲存所有軟體部署之所有內容檔案的位置。 內容庫位於站台伺服器和每個發佈點上。 「備份站台伺服器」維護工作不會備份內容庫或套件來源檔案。 站台伺服器失敗時，內容庫相關資訊會還原至站台資料庫，但您必須還原內容庫和套件來源檔案。  

-   必須先還原內容庫，您才能將內容重新發佈至發佈點。 當您開始重新發佈內容時，Configuration Manager 會將檔案從站台伺服器的內容庫複製至發佈點。 如需詳細資訊，請參閱[內容庫](../../plan-design/hierarchy/the-content-library.md)。  

-   必須先還原套件來源檔案，您才能在發佈點上更新內容。 當您開始更新內容時，Configuration Manager 會將新的或修改過的檔案從套件來源複製到內容庫。 它接著會將檔案複製至相關聯的發佈點。 對站台資料庫執行下列 SQL Server 查詢，找出所有套件和應用程式的套件來源位置：`SELECT * FROM v_Package`。 您可以查看封裝識別碼的前三個字元，藉此識別封裝來源站台。 例如，如果封裝識別碼為 CEN00001，則來源站台的站台碼為 CEN。 當您還原套件來源檔案時，檔案必須還原到失敗前所在的相同位置。  

確認您在站台伺服器的檔案系統備份中同時包含內容庫和套件來源檔案。  

### <a name="back-up-custom-software-updates"></a>備份自訂的軟體更新  
System Center Updates Publisher 是一種獨立工具，可讓您管理自訂軟體更新。 Updates Publisher 會使用本機資料庫作為其軟體更新存放庫。 使用 Updates Publisher 管理自訂軟體更新時，需判斷是否應將 Updates Publisher 資料庫納入備份計畫中。 如需詳細資訊，請參閱 [System Center Updates Publisher](../../../sum/tools/updates-publisher.md)。  

使用以下程序來備份 Updates Publisher 資料庫。  

#### <a name="back-up-the-updates-publisher-database"></a>備份 Updates Publisher 資料庫  

1.  在執行 Updates Publisher 的電腦上，瀏覽至 `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` 中的 Updates Publisher 資料庫檔案 **Scupdb.sdf**。 每位執行 Updates Publisher 的使用者都有不同的資料庫檔案。  

2.  將資料庫檔案複製到備份目的地。 例如，如果備份目的地是 `E:\ConfigMgr_Backup`，則您可以將 Updates Publisher 資料庫檔案複製至 `E:\ConfigMgr_Backup\SCUP`。  

    > [!TIP]  
    >  電腦上有多個資料庫檔案時，請考慮將檔案儲存於指出與資料庫檔案建立關聯之使用者設定檔的子資料夾中。 例如，在 `E:\ConfigMgr_Backup\SCUP\User1` 中可以有一個資料庫檔案，而 `E:\ConfigMgr_Backup\SCUP\User2` 中有另一個資料庫檔案。  



## <a name="user-state-migration-data"></a>使用者狀態移轉資料  
您可以使用 Configuration Manager 工作順序來擷取和還原作業系統部署情節中的使用者狀態資料。 狀態移轉點的屬性會列出儲存使用者狀態資料的資料夾。 此資料不會備份為「站台伺服器備份」維護工作的一部分。 作為您備份計畫的一部分，您必須手動備份所指定用來儲存使用者狀態移轉資料的資料夾。   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>判斷用來儲存使用者狀態移轉資料的資料夾  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，並展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。  

2.  選取可裝載狀態移轉角色的站台系統。 然後選取 [站台系統角色]  窗格中的 [狀態移轉點]  。  

3.  在功能區中，按一下 [屬性]  。  

4.  儲存使用者狀態移轉資料的資料夾會列在 [一般]  索引標籤上的 [資料夾詳細資料]  區段中。  



## <a name="about-the-sms-writer-service"></a>關於 SMS 寫入器服務  
SMS 寫入器是一種服務，可在備份程序期間與 Windows 磁碟區陰影複製服務 (VSS) 互動。 Configuration Manager 站台備份必須執行 SMS 寫入器服務才可以順利完成。  

### <a name="process"></a>程序  
1. SMS 寫入器會登錄至 VSS 服務，並繫結至其介面和事件。 
2. 當 VSS 廣播事件或傳送特定通知到 SMS 寫入器時，SMS 寫入器會回應通知，並採取適當的動作。 
3. SMS 寫入器會讀取位於 `<ConfigMgrInstallationPath>\inboxes\smsbkup.box` 的備份控制檔案 **smsbkup.ctl**，並判斷要備份的檔案和資料。 
4. SMS 寫入器會建置包含各種元件的中繼資料 (包含來自 SMS 登錄機碼及子機碼的特定資料)。 
    a. 它會在收到要求時將中繼資料傳送至 VSS。 
    b. VSS 接著會將中繼資料傳送給提出要求的應用程式，即 Configuration Manager 備份管理員。 
5. 備份管理員會選取要備份的資料，並透過 VSS 將此資料傳送給 SMS 寫入器。 
6. SMS 寫入器會採取適當的步驟來進行備份的準備。 
7. 稍後，VSS 準備好建立快照時：a。 它會傳送事件 b。 SMS 寫入器會停止所有 Configuration Manager 服務 c。 它確保在建立快照時凍結 Configuration Manager 活動。 
8. 在快照建立完成後，SMS 寫入器會重新啟動服務和活動。

SMS 寫入器服務會自動進行安裝。 當 VSS 應用程式要求備份或還原時，SMS 寫入器必須處於執行中狀態。  

### <a name="writer-id"></a>寫入器 ID  
SMS 寫入器的寫入器識別碼為 **03ba67dd-dc6d-4729-a038-251f7018463b**。  

### <a name="permissions"></a>權限  
SMS 寫入器服務必須在本機系統帳號戶下執行。  

### <a name="volume-shadow-copy-service"></a>磁碟區陰影複製服務  
VSS 是一組 COM API，其中實作了一個架構以允許進行磁碟區備份時系統上的應用程式仍能繼續寫入磁碟區。 VSS 提供一致的介面，可在磁碟上更新資料的使用者應用程式 (SMS 寫入器服務) 與備份應用程式 (備份管理員服務) 之間進行協調。 如需詳細資訊，請參閱[磁碟區陰影複製服務](https://go.microsoft.com/fwlink/p/?LinkId=241968)。  



## <a name="next-steps"></a>後續步驟
建立備份之後，請使用該備份來練習[站台復原](recover-sites.md)。 這種做法可協助您先熟悉復原程序，再依賴它。 它也可協助確認預定用途的備份成功。  
