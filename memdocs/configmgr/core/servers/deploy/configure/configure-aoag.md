---
title: 設定可用性群組
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 設定與管理 SQL Server AlwaysOn 可用性群組
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12753b3800b3b304bd13c992b57d22bf9e1bfad8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704796"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>針對 Configuration Manager 來設定 SQL Server Always On 可用性群組

適用於：  Configuration Manager (最新分支)

使用本文中的資訊，設定和管理您搭配 Configuration Manager 使用的可用性群組。

在開始之前：  

- 熟悉[透過 Configuration Manager 準備使用 SQL Server Always On 可用性群組](sql-server-alwayson-for-a-highly-available-site-database.md)的資訊。
- 熟悉 SQL Server 的文件，其中涵蓋可用性群組的使用方式及相關程序。 該資訊是完成下列案例所需資訊。


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> 建立和設定可用性群組

使用下列程序建立可用性群組，然後將站台資料庫的複本移至該可用性群組。

1. 使用下列命令來停止 Configuration Manager 站台：

    `preinst.exe /stopsite`

    如需詳細資訊，請參閱[階層維護工具](../../manage/hierarchy-maintenance-tool-preinst.exe.md)。

2. 將站台資料庫的備份模式從 [簡單]  變更為 [完整]  ：

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    可用性群組僅支援 [完整] 備份模式。 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)。

3. 使用 SQL Server 來建立您站台資料庫的完整備份。 選擇下列其中一個選項：

    - **將會是可用性群組的成員**：如果您使用此伺服器作為可用性群組的初始主要複本成員，則不需要將站台資料庫的複本還原至此伺服器或群組中的其他伺服器。 資料庫已在主要複本上。 SQL Server 在稍後的步驟中，會將資料庫複寫至次要複本。  

    - **將不會是可用性群組的成員**：將站台資料庫複本還原至將裝載群組主要複本的伺服器。

    如需詳細資訊，請參閱 SQL Server 文件中的下列文章：

    - [建立完整資料庫備份](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [使用 SSMS 還原資料庫備份](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > 如果您打算從可用性群組移至現有複本上的獨立項目，請先從可用性群組移除資料庫。

4. 在將裝載群組之初始主要複本的伺服器上，使用[新增可用性群組精靈](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio)來建立可用性群組。 在精靈中：

    - 在 [選取資料庫]  頁面上，為您的 Configuration Manager 站台選取資料庫。  

    - 在 **[指定複本]** 頁面上，設定︰

        - **複本：** 指定將裝載次要複本的伺服器。

        - **接聽程式：** 將 [接聽程式 DNS 名稱]  指定為完整的 DNS 名稱，例如 `<listener_server>.fabrikam.com`。 當您設定 Configuration Manager 使用可用性群組中的資料庫時，將會使用此名稱。

    - 在 **[選取初始資料同步處理]** 頁面上，選取 **[完整]** 。 在精靈建立可用性群組之後，精靈會備份主要資料庫和交易記錄檔， 然後在裝載次要複本的每部伺服器上還原它們。

        > [!Note]  
        > 如果您不使用此步驟，請將站台資料庫的複本還原到裝載次要複本的每部伺服器。 接著，手動將該資料庫加入群組。

5. 檢查每個複本上的設定：

    1. 確定站台伺服器的電腦帳戶是每部可用性群組成員電腦上的本機 **Administrators** 群組成員。  

    2. 執行[驗證指令碼](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites)，以確認每個複本上的站台資料庫都設定正確。

    3. 如果必須設定次要複本的設定，請先將主要複本容錯移轉至次要複本，然後才能繼續進行。 您只能設定主要複本的資料庫。 如需詳細資訊，請參閱 SQL Server 文件中的[執行可用性群組規劃的手動容錯移轉](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server)。

6. 所有複本都符合需求之後，可用性群組就已準備好可搭配使用 Configuration Manager。


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> 設定站台使用可用性群組

[建立並設定可用性群組](#bkmk_create)之後，請使用 Configuration Manager 站台維護來設定站台，以使用可用性群組裝載的資料庫。

不支援在可用性群組中安裝附有資料庫的新站台。 例如，如果您使用基準媒體，則必須使用 SQL Server 的單一執行個體來安裝站台。 安裝站台之後，接著便可以將站台資料庫移動至可用性群組。

1. 從 Configuration Manager 站台安裝資料夾執行 **Configuration Manager 安裝程式**：`\BIN\X64\setup.exe`。

2. 在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台]  ，然後選取 [下一步]  。

3. 選取 [修改 SQL Server 設定]  ，然後選取 [下一步]  。

4. 為站台資料庫重新設定下列各項︰

    - **SQL Server 名稱**：輸入可用性群組*接聽程式*的虛擬名稱。 您在建立可用性群組時設定了接聽程式。 這個虛擬名稱應該是完整 DNS 名稱，例如 `<Listener_Server>.fabrikam.com`。  

    - **執行個體：** 若要指定可用性群組*接聽程式*的預設執行個體，此值必須為空白。 如果目前的站台資料庫是在具名執行個體上執行，請清除目前的具名執行個體。

    - **資料庫：** 保留顯示的名稱。 此名稱是目前的站台資料庫。

5. 提供新資料庫位置的資訊之後，請使用您的一般程序和設定來完成安裝。


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> 同步複本成員  

當站台資料庫裝載於可用性群組中時，可使用下列程序來新增或移除同步複本成員。 如需有關支援的複本類型和數目的詳細資訊，請參閱[可用性群組設定](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations)。

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> 新增同步複本成員

<!--3127336-->
從 1906 版開始，請執行 Configuration Manager 安裝程式來新增同步複本成員。

1. 使用 SQL Server 程序新增次要複本。

    1. [將次要複本新增至 Always On 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)。

    1. 在 SQL Management Studio 中監視狀態。 等待可用性群組回復到完整健全狀況。

1. 執行 Configuration Manager 安裝程式，然後選取選項以修改站台。

1. 指定可用性群組接聽程式名稱作為資料庫名稱。 如果接聽程式使用非標準網路連接埠，也請指定該連接埠。 這個動作會使安裝程式確定每個節點均已正確設定。 它也會啟動資料庫復原程序。

Configuration Manager 安裝程式會使用 SQL 資料庫移動作業，並確定已正確設定節點。

如需有關如何在 1902 版或更舊版本中手動執行此程式的詳細資訊，請參閱 [ConfigMgr 1702：將新節點 (次要複本) 新增至現有 SQL AO AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960)。

### <a name="remove-a-replica-member"></a>移除複本成員

從 1906 版開始，您可以使用 Configuration Manager 安裝程式移除複本成員。 請使用與[新增同步複本成員](#bkmk_sync-add)相同的程序。

如需有關如何在 1902 版或更舊版本中手動執行此程序的詳細資訊，請參閱[將次要複本從可用性群組移除](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)。  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> 非同步複本

您可以使用與 Configuration Manager 搭配使用之可用性群組中的非同步複本。 您不需要執行設定同步複本所需的設定指令碼，因為站台資料庫不支援非同步複本。

### <a name="configure-an-asynchronous-commit-replica"></a>設定非同步認可複本

如需詳細資訊，請參閱[將次要複本加入至可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)。

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>使用非同步複本來復原您的站台

使用非同步複本復原您的站台資料庫。

1. 請停止使用中的主要站台，以防止其他寫入站台資料庫的活動。 若要停止站台，請使用[階層維護工具](../../manage/hierarchy-maintenance-tool-preinst.exe.md)：`preinst.exe /stopsite`

1. 停止該站台之後，使用非同步複本，而非[手動復原的資料庫](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered)。


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> 停止使用可用性群組

當您不想再將站台資料庫裝載在可用性群組中時，請使用下列程序。 透過此程序，您會將站台資料庫移回 SQL Server 的單一執行個體。

1. 使用下列命令來停止 Configuration Manager 站台：`preinst.exe /stopsite`。 如需詳細資訊，請參閱[階層維護工具](../../manage/hierarchy-maintenance-tool-preinst.exe.md)。

2. 使用 SQL Server 從主要複本建立站台資料庫的完整備份。 如需詳細資訊，請參閱[建立完整資料庫備份](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)。

3. 使用 SQL Server 將站台資料庫備份還原到將裝載站台資料庫的伺服器。 如需詳細資訊，請參閱[使用 SSMS 還原資料庫備份](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

    > [!Note]  
    > 如果可用性群組的主要複本伺服器將裝載站台資料庫的單一執行個體，請略過此步驟。

4. 在將裝載站台資料庫的伺服器上，將站台資料庫的備份模式從 [完整]  變更為 [簡單]  。 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)。

5. 從 Configuration Manager 站台安裝資料夾執行 **Configuration Manager 安裝程式**：`\BIN\X64\setup.exe`。

6. 在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台]  ，然後選取 [下一步]  。  

7. 選取 [修改 SQL Server 設定]  ，然後選取 [下一步]  。  

8. 為站台資料庫重新設定下列各項︰

    - **SQL Server 名稱：** 輸入現在裝載站台資料庫的伺服器名稱。

    - **執行個體：** 指定裝載站台資料庫的具名執行個體。 如果資料庫位於預設執行個體上，請將此欄位留空。

    - **資料庫：** 保留顯示的名稱。 此名稱是目前的站台資料庫。

9. 提供新資料庫位置的資訊之後，請使用您的一般程序和設定來完成安裝。 當安裝完成時，站台會重新啟動並開始使用新的資料庫位置。

10. 若要清除具備可用性群組成員身分的伺服器，請遵循[移除可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server)中的指引進行。
