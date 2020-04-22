---
title: 軟體更新維護
titleSuffix: Configuration Manager
description: 若要在 Configuration Manager 中維護更新，您可以排程 WSUS 清理工作，也可以手動進行執行。
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 560b432bb90f99207fd15bc07e7aff98ffd59ebf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703006"
---
# <a name="software-updates-maintenance"></a>軟體更新維護

適用於：  Configuration Manager (最新分支)

您可以從 Configuration Manager 主控台的軟體更新點元件內容排程及執行 WSUS 清理工作。 當您第一次選取執行 WSUS 清理工作時，它會在下一次軟體更新同步處理之後執行。  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>進行排程及執行 WSUS 清理工作

執行下列步驟來排程 WSUS 清理工作：

1. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [概觀]   > [站台設定]   > [站台]  。
2. 選取您 Configuration Manager 階層頂端的站台。

3. 按一下 [設定]  群組中的 [設定站台元件]  ，然後按一下 [軟體更新點]  開啟軟體更新點元件屬性。  

4. 檢閱 [取代行為]  。 視需要修改行為。

   ![取代行為螢幕擷取畫面](media/supersedence-behavior.png)

5. 按一下 [取代規則]  索引標籤，然後選取 [執行 WSUS 清理精靈]  。 在 1806 版中，選項已重新命名為 [在同步處理後執行 WSUS 清理]  。

6. 按一下 [確定]  (如果您正在執行 1806 版，請按一下 [關閉]  )。

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>1802 版和更早版本的 WSUS 清理行為

在 Configuration Manager 1806 版之前，WSUS 清理選項會執行下列項目：

- 僅限頂層站台之 WSUS 伺服器上 [WSUS 清理精靈] 中的 [過期的更新]  選項。

  ![WSUS 過期的更新清理螢幕擷取畫面](media/wsus-cleanup-expired.PNG)

- Configuration Manager 資料庫中軟體更新設定項目的清理會每七天發生一次，並從主控台移除不需要的更新。
  - 此清理不會從 Configuration Manager 主控台移除目前未部署的過期更新。

環境中的頂層 WSUS 資料庫及所有其他 WSUS 資料庫仍需要額外的維護。 如需詳細資訊和指示，請參閱 [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Microsoft WSUS 和 Configuration Manager SUP 維護的完整指南) 部落格文章。

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>從 1806 版開始的 WSUS 清理行為

從 1806 版開始，WSUS 清理選項會在每次同步之後發生，並執行下列清理項目：
<!--1357898 -->

- CAS 和主要站台上 WSUS 伺服器的 [過期的更新]  選項。
  - 次要站台的 WSUS 伺服器不會對過期的更新執行 WSUS 清理。
- Configuration Manager 會從其資料庫建立一份被取代的更新清單。 該清單是根據軟體更新點元件內容中的取代行為而來。
  - 符合取代行為準則的更新設定項目在 Configuration Manager 中已過期。
  - 更新會在 CAS 和主要站台的 WSUS 中遭拒，但次要站台則不會。
- Configuration Manager 資料庫中軟體更新設定項目的清理會每七天發生一次，並從主控台移除不需要的更新。
  - 此清理不會從 Configuration Manager 主控台移除目前未部署的過期更新。

> [!NOTE]
> 「遭到取代的更新失效之前等待的月數」是以取代的更新建立日期為依據。 例如，如果您針對此設定使用 2 個月，則已被取代的更新會在 WSUS 中遭拒，並在取代的更新經過 2 個月後於 Configuration Manager 中過期。

所有 WSUS 維護都必須以手動方式在次要站台 WSUS 資料庫上執行。 下列 [WSUS 伺服器清理精靈]  選項不會在 CAS 和主要站台上執行：

- 未使用的更新和更新修訂版
- 未連絡伺服器的電腦
- 不需要的更新檔案

  如需詳細資訊和指示，請參閱 [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Microsoft WSUS 和 Configuration Manager SUP 維護的完整指南) 部落格文章。

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>從 1810 版開始的 WSUS 清理行為

從 1810 版開始，您可以在 [軟體更新點] 元件屬性中，指定功能更新的取代規則 (與非功能更新分開)。 WSUS 清理選項會在每次同步之後發生，並執行下列清理項目：
<!--2839349,3098809, 2977644-->

- CAS、主要站台和次要站台上 WSUS 伺服器的 [過期的更新]  選項。
- Configuration Manager 會從其資料庫建立一份被取代的更新清單。 該清單是根據軟體更新點元件內容中的取代行為而來。
  - 符合取代行為準則的更新設定項目在 Configuration Manager 中已過期。
  - 更新會在 CAS、主要站台和次要站台的 WSUS 中遭拒。
- Configuration Manager 資料庫中軟體更新設定項目的清理會每七天發生一次，並從主控台移除不需要的更新。
  - 此清理不會從 Configuration Manager 主控台移除目前未部署的過期更新。

> [!NOTE]
> 「遭到取代的更新失效之前等待的月數」是以取代的更新建立日期為依據。 例如，如果您針對此設定使用 2 個月，則已被取代的更新會在 WSUS 中遭拒，並在取代的更新經過 2 個月後於 Configuration Manager 中過期。

下列 [WSUS 伺服器清理精靈]  選項不會在 CAS、主要站台和次要站台上執行：

- 未使用的更新和更新修訂版
- 未連絡伺服器的電腦
- 不需要的更新檔案

  如需詳細資訊和指示，請參閱 [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Microsoft WSUS 和 Configuration Manager SUP 維護的完整指南) 部落格文章。

## <a name="wsus-cleanup-starting-in-version-1906"></a>從 1906 版開始的 WSUS 清除
<!--41101009-->

 您友其他 WSUS 維護工作，可讓 Configuration Manager 執行來維護健康情況良好的軟體更新點。 除了拒絕 WSUS 中的過期更新以外，Configuration Manager 還可以將非叢集索引新增至 WSUS 資料庫，並從 WSUS 資料庫中移除已淘汰的更新。 在每次同步處理之後都會進行 WSUS 維護。

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>根據取代規則拒絕 WSUS 中過期的更新

在 WSUS 中拒絕更新可從傳送給用戶端的目錄移除那些更新，藉此改善效能。 拒絕 Configuration Manager 標示為已取代的更新，會進一步將目錄降到最低，並改善效能。

1. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [概觀]   > [站台設定]   > [站台]  。
2. 選取您 Configuration Manager 階層頂端的站台。
3. 按一下 [設定] 群組中的 [設定站台元件]  ，然後按一下 [軟體更新點]  開啟軟體更新點元件屬性。
4. 在 [WSUS 維護]  索引標籤中，選取 [根據取代規則拒絕 WSUS 中過期的更新]  。

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>將非叢集索引新增至 WSUS 資料庫以改進 WSUS 清理效能

新增非叢集索引可改善 Configuration Manager 執行的 WSUS 清除效能。

1. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [概觀]   > [站台設定]   > [站台]  。
2. 選取您 Configuration Manager 階層頂端的站台。
3. 按一下 [設定] 群組中的 [設定站台元件]  ，然後按一下 [軟體更新點]  開啟軟體更新點元件屬性。
4. 在 [WSUS 維護]  索引標籤上，選取 [將非叢集索引新增至 WSUS 資料庫]  。
5. 在 Configuration Manager 使用的每個 SUSDB 上，索引會加入至下列資料表：
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>建立索引的 SQL 權限

當 WSUS 資料庫位於遠端 SQL Server 上時，您可能需要在 SQL 中新增權限來建立索引。 用來連線到 WSUS 資料庫和建立索引的帳戶可能會有所不同。 如果您[在軟體更新點內容中指定 WSUS 伺服器連線帳戶](../get-started/install-a-software-update-point.md#wsus-server-connection-account)，請確定連線帳戶具有 SQL 權限。 如果您未指定 WSUS 伺服器連線帳戶，則站台伺服器的電腦帳戶需要 SQL 權限。

- 建立索引時需要有資料表或檢視表的 `ALTER` 權限。 此帳戶必須是 `sysadmin` 固定伺服器角色的成員，或是 `db_ddladmin` 和 `db_owner` 固定資料庫角色的成員。 如需有關建立索引和權限的詳細資訊，請參閱 [CREATE INDEX (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions)。
- 必須將 `CONNECT SQL` 伺服器權限授與此帳戶。 如需詳細資訊，請參閱 [GRANT 伺服器權限 (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)。

> [!NOTE]  
>  如果 WSUS 資料庫位於使用非預設連接埠的遠端 SQL Server 上，則可能不會加入索引。 針對此案例，您可以[使用 SQL Server Configuration Manager 建立伺服器別名](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017)。 一旦新增別名，且 Configuration Manager 可以建立與 WSUS 資料庫的連線，將會加入索引。

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>從 WSUS 資料庫移除已淘汰的更新

已淘汰更新是 WSUS 資料庫中未使用的更新和更新修訂版。 一般來說，一旦更新不再位於 [Microsoft Update Catalog](https://www.catalog.update.microsoft.com/)，且其他更新不需要此更新作為必要條件或相依性之後，此更新將視為已淘汰。

1. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [概觀]   > [站台設定]   > [站台]  。
2. 選取您 Configuration Manager 階層頂端的站台。
3. 按一下 [設定] 群組中的 [設定站台元件]  ，然後按一下 [軟體更新點]  開啟軟體更新點元件屬性。
4. 在 [WSUS 維護]  索引標籤中選取 [從 WSUS 資料庫移除已淘汰的更新]  。
   - 移除已淘汰的更新最長可以執行 30 分鐘才會停止。 在下一次同步處理後，會再次開始。  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>移除已淘汰更新的 SQL 權限

當遠端 SQL Server 上的 WSUS 資料庫啟動時，站台伺服器的電腦帳戶需要下列 SQL 權限：

- `db_datareader` 和 `db_datawriter` 固定資料庫角色。 如需詳細資訊，請參閱[資料庫層級角色](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles)。
- 必須將 `CONNECT SQL` 伺服器權限授與站台伺服器的電腦帳戶。 如需詳細資訊，請參閱 [GRANT 伺服器權限 (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)。

#### <a name="wsus-cleanup-wizard"></a>WSUS 清除精靈

從 1906 版開始，下列 [WSUS 伺服器清理精靈]  選項不會在 CAS、主要站台與次要站台上執行：

- 未連絡伺服器的電腦
- 不需要的更新檔案

  如需詳細資訊和指示，請參閱 [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) (Microsoft WSUS 和 Configuration Manager SUP 維護的完整指南) 部落格文章。


### <a name="known-issues-for-version-1906"></a>1906 版的已知問題

考慮下列案例：
<!--5418148-->
- 您使用的是 Configuration Manager 1906 版
- 您有使用 Windows 內部資料庫的遠端軟體更新點
- 在 [軟體更新點元件內容]  中，您可以在 [ WSUS 維護]  索引標籤下選取下列任何選項：
   - 將非叢集索引新增至 WSUS 資料庫
   - 從 WSUS 資料庫移除已淘汰的更新

在此情況下，Configuration Manager 無法使用 Windows 內部資料庫來執行遠端軟體更新點的上述 WSUS 維護工作。 發生這個問題的原因是 Windows 內部資料庫不允許遠端連線。 您會在站台伺服器上的 `WSyncMgr.log` 中看到下列錯誤：

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

若要解決此問題，您可以使用 Windows 內部資料庫，將遠端軟體更新點的 WSUS 維護作業自動化。 如需有關詳細步驟的詳細資訊，請參閱 [Microsoft WSUS 和 Configuration Manager SUP 維護的完整指南](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)。

## <a name="updates-cleanup-log-entries"></a>更新清理記錄項目

您可以檢閱 wsyncmgr.log 中的下列項目來確認此清理：

- 當您看到此記錄項目時，WSUS 中被取代的更新拒絕已完成：`Cleanup processed <number> total updates and declined <number>`
- 當您看到此項目時，WSUS 清理正在啟動：`Calling WSUS Cleanup.`
- 當您看到此項目時，過期更新的 WSUS 清理已完成：`Successfully completed WSUS Cleanup.`
- 當您看到此項目時，Configuration Manager 過期的更新設定項目清理正在啟動：`Deleting old expired updates...`
- 當您看到此項目時，Configuration Manager 過期的更新設定項目清理已完成：`Deleted <number> expired updates total`
