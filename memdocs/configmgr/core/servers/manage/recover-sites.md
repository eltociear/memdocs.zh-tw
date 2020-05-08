---
title: 站台復原
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中復原站台。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b17c8c9ed0c1f6f9a5aeb487e07ad3d3dc66cbae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903966"
---
# <a name="recover-a-configuration-manager-site"></a>復原 Configuration Manager 站台

適用於：  Configuration Manager (最新分支)

在站台資料庫發生站台失敗或資料遺失的狀況之後，執行 Configuration Manager 站台復原。 修復和重新同步處理資料是網站復原的核心工作，也是避免操作中斷的必要手段。

本文中的各節可協助您復原 Configuration Manager 站台。 若要建立備份，請參閱[備份 Configuration Manager](backup-and-recovery.md)。

## <a name="considerations-before-recovering-a-site"></a>復原站台前的考量

> [!Important]  
> 這項資訊僅適用於站台復原案例。 如果您要升級內部部署基礎結構，但不主動復原故障的站台，請檢閱下列文章中的資訊：
>
> - [升級內部部署基礎結構](upgrade-on-premises-infrastructure.md)
> - [修改基礎結構](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>準備伺服器硬體

<!-- 2841893 -->

請確定現有設定不存在於站台伺服器上。 任何先前設定可能會在站台復原期間造成衝突。 針對伺服器硬體，請使用下列其中一個選項：

- 使用符合一般和復原需求的新伺服器。

- 將磁碟格式化，然後在現有伺服器上重新安裝 OS。 請確定它符合一般和復原需求。

- 重複使用您已清除的現有伺服器

使用下列其中一個程序來清除現有伺服器：

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>僅針對站台伺服器復原清除現有伺服器

1. 刪除 SMS 登錄機碼：`HKLM\Software\Microsoft\SMS`
2. 將任何開頭是 `SMS` 的登錄項目從 `HKLM\System\CurrentControlSet\Services` 刪除。 例如：
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. 將 Configuration Manager 用戶端解除安裝
4. 重新啟動伺服器
5. 確認所有上述登錄機碼都已刪除。

伺服器現在已準備就緒，可進行 Configuration Manager 還原程序。

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>僅針對站台資料庫復原清除現有伺服器

1. 備份站台資料庫。 也請備份任何其他支援的資料庫，像是 WSUS。
2. 請務必記下 SQL 伺服器名稱和執行個體名稱
3. 將站台資料庫從 SQL Server 手動刪除
4. 重新啟動 SQL Server

伺服器現在已準備就緒，可進行 Configuration Manager 還原程序。

#### <a name="clean-an-existing-server-for-full-recovery"></a>清除現有伺服器以進行完整復原

1. 備份站台資料庫。 也請備份任何其他支援的資料庫，像是 WSUS。
2. 製作內容庫複本
3. 將站台資料庫從 SQL Server 手動刪除
4. 將 Configuration Manager 站台解除安裝
5. 手動刪除 Configuration Manager 安裝資料夾，以及任何其他 Configuration Manager 資料夾
6. 重新啟動伺服器
7. 還原內容庫和 WSUS 等其他資料庫

伺服器現在已準備就緒，可進行 Configuration Manager 還原程序。

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>使用支援的版本和相同版本的 SQL Server

<!-- SCCMDocs#751 -->

可能的話，請使用相同版本的 SQL Server。 不過，系統支援將資料庫還原到較新版本。

請勿變更 SQL Server 版本。 不支援將站台資料庫從 Standard Edition 還原至 Enterprise Edition。

其他 SQL Server 設定需求：

- SQL Server 不能設為**單一使用者模式**。
- 確定 MDF 和 LDF 檔案都有效。 復原站台時，不會檢查檔案的狀態。  

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性群組

如果您使用 SQL Server Always On 可用性群組裝載站台資料庫，請根據[準備使用 SQL Server Always On](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery) 中所述來修改復原計劃。

### <a name="database-replicas"></a>資料庫複本

還原您為資料庫複本所設定的站台資料庫後，請重新設定每個複本。 您要先重新建立發行集和訂閱，才可以使用資料庫複本。

## <a name="determine-your-recovery-options"></a>決定您的復原選項

針對 Configuration Manager 主要站台伺服器和管理中心網站 (CAS) 復原，有兩大重點考量：**站台伺服器**與**站台資料庫**。
下列各節可協助您為復原案例選取最佳選項。

> [!NOTE]  
> 當 Configuration Manager 安裝程式在伺服器上偵測到現有的站台時，您就可以啟動站台復原，不過站台伺服器的復原選項有限。 例如，若您在現有網站伺服器上執行安裝程式，當您選擇復原時，就可以復原網站資料庫伺服器，但會停用復原網站伺服器的選項。

### <a name="site-server-recovery-options"></a>站台伺服器復原選項

從您在 Configuration Manager 安裝資料夾外部所建立的 **CD.Latest** 資料夾複本中啟動 Configuration Manager 安裝程式。  

- 如果您從站台伺服器的 [開始]  功能表執行安裝程式，就無法使用 [復原站台]  選項。  

- 如果在您建立備份之前，已在 Configuration Manager 主控台內安裝任何更新，即無法從下列位置使用安裝程式重新安裝站台：

  - 安裝媒體
  - Configuration Manager 安裝路徑

然後選取 [復原站台]  選項。 針對失敗的站台伺服器，您有以下復原選項：  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>使用現有備份復原站台伺服器

當您有站台失敗前的站台伺服器 Configuration Manager 備份時，請使用此選項。 站台會將此備份建立為**備份站台伺服器**維護工作的一部分。 此時會重新安裝網站，並根據備份的網站來設定網站設定。  

#### <a name="reinstall-the-site-server"></a>重新安裝站台伺服器

若您沒有站台伺服器的備份時，使用這個選項。 此時會重新安裝站台伺服器，且您必須指定網站設定，如同您進行初始安裝時一樣。  

- 請使用失敗的站台第一次安裝時使用的相同站台碼和站台資料庫名稱。  

- 您可以在執行新作業系統版本的新電腦上重新安裝站台。  

- 伺服器必須使用與原始站台伺服器相同的主機名稱和完整網域名稱 (FQDN)。

### <a name="site-database-recovery-options"></a>網站資料庫復原選項

執行 Configuration Manager 安裝程式時，針對站台資料庫，您有下列復原選項：  

#### <a name="recover-the-site-database-using-a-backup-set"></a>使用備份集復原站台資料庫

當您有資料庫失敗前的站台資料庫 Configuration Manager 備份時，請使用此選項。 站台會將此備份建立為**備份站台伺服器**維護工作的一部分。 在階層中還原主要站台時，復原程序會擷取上次備份後，CAS 對站台資料庫所做的任何變更。 還原 CAS 時，復原程序會從參照主要站台擷取這些變更。 當您復原獨立主要站台的站台資料庫時，您會遺失最後一次備份後的網站變更。  

當您復原階層中某個站台的站台資料庫時，CAS 與主要站台的復原行為不同。 當上次備份是在 SQL Server 變更追蹤保留期間內或保留期間外，其行為也不一樣。 如需詳細資訊，請參閱本文中的[站台資料庫復原案例](#site-database-recovery-scenarios)一節。  

> [!NOTE]  
> 若您選取使用備份集來還原站台資料庫，但站台資料庫已經存在，復原就會失敗。  

#### <a name="create-a-new-database-for-this-site"></a>為此網站建立新資料庫

當您沒有站台資料庫的備份時，請使用這個選項。 在階層中，復原程序會建立新的站台資料庫。 還原子主要站台時，它會從 CAS 複寫來復原資料。 還原 CAS 時，它會從參照主要站台複寫資料。 若您復原獨立主要站台或沒有主要站台的 CAS，就無法使用此選項。  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>使用手動復原的站台資料庫

如果您已復原 Configuration Manager site 站台資料庫，但需要完成復原程序，請使用這個選項。  

- Configuration Manager 可以從下列任何程序來復原站台資料庫：  

  - Configuration Manager 備份維護工作  
  - 使用 Data Protection Manager (DPM) 的站台資料庫備份  
  - 另一項備份程序  

    在您使用 Configuration Manager 以外的方法復原站台資料庫後，請執行安裝程式，然後選取這個選項來完成站台資料庫復原。  

    > [!NOTE]  
    > 使用 DPM 備份站台資料庫時，在 Configuration Manager 中繼續還原程序前，請使用 DPM 程序將站台資料庫還原到指定的位置。 如需 DPM 的詳細資訊，請參閱 [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) 文件庫。  

- 在階層中還原主要站台資料庫時，復原程序會擷取上次備份後，CAS 對站台資料庫所做的任何變更。 還原 CAS 時，復原程序會從參照主要站台擷取這些變更。 當您復原獨立主要站台的站台資料庫時，您會遺失最後一次備份後的網站變更。  

#### <a name="skip-database-recovery"></a>略過資料庫復原

若 Configuration Manager 站台資料庫伺服器上並沒出現資料遺失的狀況，請使用此選項。 只有在站台資料庫位於不同電腦而不是在您正在復原的站台伺服器上時，這個選項才有效。  

### <a name="sql-server-change-tracking-retention-period"></a>SQL Server 變更追蹤保留期間

Configuration Manager 可對 SQL Server 的站台資料庫執行變更追蹤。 變更追蹤可讓 Configuration Manager 查詢有關上次時間點後，資料庫資料表中出現的變更資訊。 保留期間會指定保留變更追蹤資訊的時間長度。 根據預設，站台資料庫的保留期間設定為五天。 復原網站資料庫時，您的備份是在保留期間內或保留期間外，復原程序的進行方式也隨之不同。 例如，若 SQL server 失敗，而上次備份是七天以前，表示備份是在保留期間外。

如需 SQL Server 變更追蹤本質的詳細資訊，請參閱來自 SQL Server 小組的下列部落格文章：[Change Tracking Cleanup - part 1](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) (變更追蹤清除 - 第 1 部分) 和 [Change Tracking Cleanup - part 2](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-2) (變更追蹤清除 - 第 2 部分)。

### <a name="reinitialization-of-site-or-global-data"></a>重新初始化站台或全域資料

重新初始化網站或全域資料的程序，會以來自另一個網站資料庫的資料取代網站資料庫中的現有資料。 例如，若網站 ABC 重新初始化來自網站 XYZ 的資料，會發生以下步驟：

- 資料從網站 XYZ 複製到 ABC。
- 網站 XYZ 的現有資料會從網站 ABC 上的網站資料庫中移除。
- 從網站 XYZ 複製的資料會插入網站 ABC 的網站資料庫。

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>範例案例 1：主要站台重新初始化來自 CAS 的全域資料

復原程序會從主要站台資料庫移除主要站台的現有全域資料，並取代為從 CAS 複製的全域資料。

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>範例案例 2：CAS 重新初始化來自主要站台的站台資料

復原程序會從 CAS 資料庫中移除該主要站台的現有站台資料。 其會以從主要站台複製的站台資料來取代資料。 其他主要站台的站台資料則不受影響。

### <a name="site-database-recovery-scenarios"></a>網站資料庫復原案例

從備份還原站台資料庫後，Configuration Manager 會嘗試還原站台內上次資料庫備份後的變更以及全域資料。 Configuration Manager 會在從備份還原站台資料庫之後，啟動下列動作：  

#### <a name="recovered-site-is-a-cas"></a>復原的站台是 CAS

- 變更追蹤保留期間內的資料庫備份  

  - **全域資料**：備份後全域資料中的變更是從所有主要站台複製的。  

  - **站台資料**：備份後站台資料中的變更是從所有主要站台複製的。  

- 比變更追蹤保留期間還舊的資料庫備份  

  - **全域資料**：若您指定，CAS 會重新初始化來自參照主要站台的全域資料。 接著，所有其他主要站台會重新初始化來自 CAS 的全域資料。 您若不指定參考站台，則所有主要站台都會重新初始化來自 CAS 的全域資料。 這份資料是您從備份還原的內容。  

  - **站台資料**：CAS 重新初始化來自每個主要站台的站台資料。  

#### <a name="recovered-site-is-a-primary-site"></a>復原的站台是主要站台

- 變更追蹤保留期間內的資料庫備份  

  - **全域資料**：備份後全域資料中的變更是從 CAS 複製的。  

  - **站台資料**：CAS 重新初始化來自主要站台的站台資料。 備份後的變更都會遺失。 當用戶端將資訊傳送至主要站台時，會重新產生大部分的資料。  

- 比變更追蹤保留期間還舊的資料庫備份  

  - **全域資料**：主要站台重新初始化來自 CAS 的全域資料。  

  - **站台資料**：CAS 重新初始化來自主要站台的站台資料。 備份後的變更都會遺失。 當用戶端將資訊傳送至主要站台時，會重新產生大部分的資料。  

## <a name="site-recovery-procedures"></a>網站復原程序

使用下列其中一個程序來協助您復原站台伺服器和站台資料庫：

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>在安裝精靈中啟動站台復原

1. 將 [CD.Latest 資料夾](the-cd.latest-folder.md)複製到 Configuration Manager 安裝資料夾外部的位置。 從 CD.Latest 資料夾的複本執行 [Configuration Manager 安裝精靈]。  

2. 在 [開始使用]  頁面上，選取 [復原站台]  ，然後選取 [下一步]  。  

3. 使用適合復原網站的選項來完成精靈。  

     - 在復原期間，安裝程式會識別 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 在復原期間，請勿變更此連接埠設定，否則在復原完成後，會無法正常執行資料複寫。  

     - 您可以在 [安裝精靈] 中指定用於 Configuration Manager 安裝的原始或新路徑。  

### <a name="start-an-unattended-site-recovery"></a>啟動自動站台復原

1. 針對復原網站時所需的選項，準備自動安裝指令碼。 如需詳細資訊，請參閱[自動站台復原](unattended-recovery.md)。  

2. 使用 `/script` 命令列選項執行 Configuration Manager 安裝程式。 例如，您建立安裝程式初始設定檔案 **ConfigMgrUnattend.ini**。 將它儲存在執行安裝程式之電腦的 `C:\Temp` 目錄中。 使用下列命令：  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> 復原 CAS 後，可能無法建立某些從子站台複寫過來的站台資料。 此資料可包括硬體清查、軟體清查和狀態訊息。
>
> 如果發生這個問題，請為資料庫複寫重新初始化 **ConfigMgrDRSSiteQueue**。 使用 **SQL Server Manager** 對 CAS 的站台資料庫執行下列查詢：
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>復原後的工作

復原網站後，您要先考量幾項後續復原工作，網站復原才算完成。 利用下面各節可幫助您完成網站復原程序。

### <a name="reenter-user-account-passwords"></a>重新輸入使用者帳戶密碼

復原站台伺服器後，請重新輸入網站中任何使用者帳戶的密碼。 這些密碼會在站台復原期間重設。 站台復原完成後，這些帳戶會列在安裝精靈的 [已完成]  頁面。 清單也會儲存到已復原站台伺服器的 `C:\ConfigMgrPostRecoveryActions.html`。

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>在網站復原後重新輸入使用者帳戶的密碼

1. 開啟 Configuration Manager 主控台並連線至復原的站台。  

2. 移至 [管理]  工作區，展開 [安全性]  ，然後選取 [帳戶]  。  

3. 為每個帳戶執行下列步驟來重新輸入密碼：  

     1. 從網站復原後找到的清單中選取帳戶。  

     2. 在功能區中，選取 [內容]  。  

     3. 在 [一般]  索引標籤上，選取 [設定]  ，然後重新輸入帳戶的密碼。  

     4. 選取 [驗證]  ，為所選使用者帳戶選擇適當的資料來源，然後選取 [測試連線]  。 此步驟可測試使用者帳戶能否連線到資料來源，並驗證認證。  

     5. 選取 [確定]  儲存密碼變更，然後選取 [確定]  關閉帳戶的 [內容] 頁面。  

#### <a name="reenter-pxe-passwords"></a>重新輸入 PXE 密碼

<!-- SCCMDocs#1683 -->

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [發佈點]  節點。 [PXE]  欄為 [是]  的任何內部部署發佈點都已啟用 PXE，而且可能要重新輸入密碼。

1. 選取支援 PXE 的發佈點，然後在功能區中選取 [內容]  。

1. 切換至 [PXE]  索引標籤。

1. 如果已啟用 [電腦使用 PXE 時需要密碼]  選項，請輸入並確認密碼。

1. 選取 [確定]  以儲存並關閉屬性。

針對任何其他已啟用 PXE 的內部部署發佈點重複此程序。

#### <a name="reenter-task-sequence-passwords"></a>重新輸入工作順序密碼

<!-- SCCMDocs#1683 -->

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。

1. 選取工作順序，然後在功能區中選取 [編輯]  。

1. 請針對要重新輸入的密碼檢閱下列步驟：

    - **套用 Windows 設定**：如果您啟用並指定本機系統管理員密碼，請重新輸入並確認密碼。

    - **套用網路設定**：針對有權限加入網域的帳戶，選取[設定]  。 輸入並確認密碼，然後選取 [驗證]  。

    - **擷取作業系統映像**：針對用來存取目的地的帳戶，選取 [設定]  。 輸入並確認密碼，然後選取 [驗證]  。

    - **連線到網路資料夾**：針對用來連線到網路資料夾的帳戶，選取 [設定]  。 輸入並確認密碼，然後選取 [驗證]  。

    - **啟用 BitLocker**：如果您使用金鑰管理選項 [TPM 和 PIN]  ，請重新輸入 PIN。

    - **加入網域或工作群組**：針對有權限加入網域的帳戶，選取[設定]  。 輸入並確認密碼，然後選取 [驗證]  。

    - **執行命令列**：如果您使用 [以下列帳戶的身分執行此步驟]  選項，請選取 [設定]  。 輸入並確認密碼，然後選取 [驗證]  。

    - **執行 PowerShell 指令碼**：如果您使用 [以下列帳戶的身分執行此步驟]  選項，請選取 [設定]  。 輸入並確認密碼，然後選取 [驗證]  。

針對所有工作順序重複此程序。

### <a name="reenter-sideloading-keys"></a>重新輸入側載金鑰

復原站台伺服器後，請重新輸入為站台指定的 Windows 側載金鑰。 站台復原期間會重設這些金鑰。 重新輸入側載金鑰之後，站台會重設 Windows 側載金鑰 [已使用的啟用數量]  欄中的計數。

例如，在站台失敗前，[啟用總數]  計數會顯示為 **100**。 裝置已使用的金鑰數目或 [已使用的啟用數量]  為 **90**。 復原站台之後，[啟用總數]  值仍顯示 **100**，但是 [已使用的啟用數量]  欄會不正確顯示 **0**。 在 10 部新裝置使用側載金鑰之後，就不再有側載金鑰，從第 11 部裝置開始即無法再套用側載金鑰。

### <a name="recreate-azure-services"></a>重新建立 Azure 服務

<!-- SCCMDocs#1022 -->

在 Configuration Manager 1806 版中，於站台復原之後，您會在 cloudmgr.log 中看到下列錯誤：

`Index (zero-based) must be greater than or equal to zero`

若要解決此問題，請為每個 Azure 租用戶連線[更新秘密金鑰](../deploy/configure/azure-services-wizard.md#bkmk_renew)。

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>為使用 IIS 的網站系統角色設定 SSL

當您復原執行 IIS 且為 HTTPS 設定的網站系統時，請重新設定 IIS 使用 Web 伺服器憑證。

### <a name="reinstall-hotfixes"></a>重新安裝 Hotfix

網站復原後，您必須重新安裝之前套用至網站伺服器的任何[額外 Hotfix](updates.md#bkmk_outofband)。 復原站台之後，在 [安裝精靈] 的 [已完成]  頁面上檢視先前所安裝 Hotfix 的清單。 此清單也會儲存到已復原站台伺服器的 `C:\ConfigMgrPostRecoveryActions.html`。

### <a name="recover-custom-reports"></a>復原自訂報表

有些客戶會在 SQL Server Reporting Services 中建立自訂報表。 當此元件失敗時，請從報表伺服器的備份復原報表。 如需還原 Reporting Services 中自訂報表的詳細資訊，請參閱 [Reporting Services 的備份與還原作業](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)。

### <a name="recover-content-files"></a>復原內容檔案

站台資料庫會追蹤站台伺服器儲存內容檔案的位置。 內容檔案本身不會備份或還原為備份和復原程序的一部分。 若要完整復原內容檔案，請將內容庫及套件來源檔案還原至原始位置。 有幾種方法可復原內容檔案。 最簡單的方法是從站台伺服器的檔案系統備份還原檔案。

如果您沒有套件來源檔案的檔案系統備份，請手動複製或下載它們。 此程序類似您最初建立套件的時候。 在 SQL Server 中執行下列查詢，找出所有套件和應用程式的套件來源位置：`SELECT * FROM v_Package`。 查看套件識別碼的前三個字元，藉此識別套件來源站台。 例如，如果封裝識別碼為 CEN00001，則來源站台的站台碼為 CEN。 當您還原套件來源檔案時，檔案必須還原到失敗前所在的相同位置。

您若沒有包含內容庫的檔案系統備份，您可以選擇下列還原方式：  

- **匯入預先設置的內容檔案**：在 Configuration Manager 階層中，您可以建立預先設置的內容檔案，包含來自其他位置的所有套件及應用程式。 然後匯入預先設置的內容檔案，復原站台伺服器上的內容庫。  

- **更新內容**：Configuration Manager 會將套件來源的內容複製到內容庫。 原始位置中必須有套件來源檔案，此動作才能成功完成。 在每個套件和應用程式上執行此動作。

### <a name="recover-custom-software-updates"></a>復原自訂的軟體更新

您的備份計劃若已包含 System Center Updates Publisher 資料庫檔案，當 Updates Publisher 電腦發生故障時，即可復原該資料庫。 如需 Updates Publisher 的詳細資訊，請參閱 [System Center Updates Publisher](../../../sum/tools/updates-publisher.md)。

#### <a name="restore-the-updates-publisher-database"></a>還原 Updates Publisher 資料庫

1. 在復原的電腦上重新安裝 Updates Publisher。  

2. 將資料庫檔案 **Scupdb.sdf** 從備份目的地複製到執行 Updates Publisher 之電腦的 `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`。  

3. 如果電腦中有一位以上的使用者執行 Updates Publisher，請將每個資料庫檔案複製到適當的使用者設定檔位置。  

### <a name="user-state-migration-data"></a>使用者狀態移轉資料

您要指定儲存使用者狀態資料的資料夾，作為狀態移轉點內容的一部分。 復原狀態移轉點之後，請手動還原伺服器的使用者狀態資料。 將它還原到失敗前儲存資料的相同資料夾。

### <a name="regenerate-the-certificates-for-distribution-points"></a>重新產生用於發佈點的憑證

還原站台後，**distmgr.log** 可能會列出一或多個發佈點的下列項目：`Failed to decrypt cert PFX data`。 此項目指出站台無法解密發佈點憑證資料。 若要解決此問題，請針對受影響的發佈點重新產生或重新匯入憑證。 使用 [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell Cmdlet。

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>更新用於雲端發佈點的憑證

Configuration Manager 需要 Azure 管理憑證，以讓站台伺服器與雲端發佈點通訊。 復原網站後，請更新用於雲端發佈點的憑證。

## <a name="recover-a-secondary-site"></a>復原次要站台

Configuration Manager 不支援次要站台的資料庫備份，但可透過重新安裝次要站台來支援復原。 Configuration Manager 次要站台故障時，必須復原次要站台。

### <a name="requirements"></a>需求

- 伺服器必須符合所有次要網站必要條件，而且必須設定適當的安全性權限。  

- 使用先前在故障網站中使用的安裝路徑。  

- 使用與故障伺服器具有相同設定的伺服器。 這項設定包括其完整網域名稱 (FQDN)。  

- 伺服器必須和故障的站台擁有相同的 SQL Server 設定。  

  - 復原次要站台時，如果電腦中尚未安裝 SQL Server Express，則 Configuration Manager 不會安裝 SQL Server Express。  

  - 使用次要站台資料庫故障前所使用的 SQL Server 版本及相同的 SQL Server 執行個體。  

### <a name="procedure"></a>程序

從 Configuration Manager主控台的 [站台]  節點，使用 [復原次要站台]  動作。 與其他類型的站台不同，次要站台的復原不使用備份檔案。 此程序會在故障的伺服器上重新安裝次要站台檔案。 重新安裝站台之後，會從父主要站台重新初始化次要站台的資料。

復原過程中，Configuration Manager 會驗證次要站台伺服器上是否有內容庫。 它也會檢查是否有適當的內容可供使用。 如果現有的內容庫包含適當的內容，次要站台就會使用現有的內容庫。 否則，請重新發佈或預先設置伺服器的內容，以復原內容庫。

當您的發佈點不在次要站台伺服器上時，您不需要在次要站台復原期間重新安裝發佈點。 復原次要網站後，網站會自動與發佈點同步。

您可以從 Configuration Manager 主控台的 [站台]  節點，使用 [顯示安裝狀態]  動作來確認次要站台復原的狀態。
