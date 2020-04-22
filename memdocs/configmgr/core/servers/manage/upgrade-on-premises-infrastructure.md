---
title: 升級內部部署基礎結構
titleSuffix: Configuration Manager
description: 了解如何升級基礎結構 (例如 SQL Server 和站台系統的作業系統)。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 033c5de1a85ce2fa8b11fe7a187fcc4d5c023931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704296"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>升級支援 Configuration Manager 的內部部署基礎結構

適用於：  Configuration Manager (最新分支)

使用本文中的資訊，協助您升級執行 Configuration Manager 的伺服器基礎結構。  

- 若希望從舊版*升級*為 Configuration Manager 目前的分支，請參閱[升級至 Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md)。  

- 若希望將 Configuration Manager 目前分支的基礎結構，*更新*至新版，請參閱 [Configuration Manager 的更新](updates.md)。  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> 升級站台系統的作業系統  

Configuration Manager 在下列情況中，支援就地升級裝載站台伺服器的伺服器作業系統，以及站台系統角色︰  

- 若 Configuration Manager 仍然支援所產生的 Windows Service Pack 層級，其即支援就地升級至更新版本的 Windows Server Service Pack。  

- 就地升級方向：  

    - Windows Server 2016 至 Windows Server 2019  

    - Windows Server 2012 R2 至 Windows Server 2019  

    - Windows Server 2012 R2 至 Windows Server 2016  

    - Windows Server 2012 至 Windows Server 2016  

    - Windows Server 2012 到 Windows Server 2012 R2  

    - Windows Server 2008 R2 至 Windows Server 2012 R2  

若要升級伺服器，請使用您要升級的目標作業系統所提供的升級程序。 請參閱下列文章：  

- [Windows Server 升級中心](https://aka.ms/upgradecenter)  

- [Windows Server 2016 的升級與轉換選項](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Windows Server 2012 R2 的升級選項](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> 升級至 Windows Server 2016 或 2019

請為所有下列升級案例使用本節中的步驟：  

- 將 Windows Server 2012 R2 或 Windows Server 2016 升級至 Windows Server 2019  

- 將 Windows Server 2012 或 Windows Server 2012 R2 升級至 Windows Server 2016  

#### <a name="before-upgrade"></a>升級之前

- (Windows Server 2012 或 Windows Server 2012 R2)：移除 System Center Endpoint Protection (SCEP) 用戶端。 Windows Server 現已內建有取代 SCEP 用戶端的 Windows Defender。 若有 SCEP 用戶端，可能會無法升級至 Windows Server。  

- 若已安裝 WSUS 角色，請從伺服器上移除。 您可以保留 SUSDB，並在將 WSUS 重新安裝之後進行重新連結。  

- 如果您要升級站台伺服器的 OS，請確定站台的[檔案型複寫](../../plan-design/hierarchy/file-based-replication.md)狀況良好。 檢查所有收件匣以確認傳送和接收站台上是否有待處理項目。 如果有許多停滯或擱置的複寫作業，請等候系統清除它們。<!-- SCCMDocs#1792 -->
    - 在傳送站台上，請檢閱 **sender.log**。
    - 在接收站台上，請檢閱 **despooler.log**。

#### <a name="after-upgrade"></a>升級之後

- 請確定 Windows Defender 已啟用且設為自動啟動，同時在執行中。  

- 請確定下列 Configuration Manager 服務正在執行中︰  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- 請確定 **Windows 處理序啟用**與 **WWW/W3svc** 服務皆已啟用，且已設定為自動啟動。 升級處理序會停用這些服務，因此請確定已對下列站台系統角色執行了這些服務：  

    - 網站伺服器  

    - 管理點  

    - 應用程式類別目錄 Web 服務點  

    - 應用程式類別目錄網站點  

- 請確定每部裝載站台系統角色的伺服器，都能繼續符合所有[必要條件](../../plan-design/configs/site-and-site-system-prerequisites.md)。 例如，您可能需要重新安裝 BITS、WSUS，或設定 IIS 的特定設定。  

- 還原所有缺少的必要條件之後，請再重新啟動一次伺服器，確認服務已啟動且在運作中。  

- 若目前升級的是主要站台伺服器，請[執行站台重設](modify-your-infrastructure.md#bkmk_reset)。  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>遠端 Configuration Manager 主控台的已知問題

升級站台伺服器或 SMS 提供者的執行個體之後，即無法與 Configuration Manager 主控台連線。 若要解決這個問題，請手動還原 WMI 中 **SMS Admins** 群組的權限。 必須設定站台伺服器以及每部裝載 SMS 提供者執行個體之遠端伺服器的權限︰

1. 在適用的伺服器上，開啟 Microsoft Management Console (MMC)，再新增 **WMI 控制** 的嵌入式管理單元，然後選取 [本機電腦]  。  

2. 在 MMC 中，開啟 [WMI 控制 (本機)]  的 [內容]  ，然後選取 [安全性]  索引標籤。  

3. 展開根目錄下的樹狀結構，再選取 [SMS]  節點，然後選擇 [安全性]  。  請確定 **SMS Admins** 群組具有下列權限︰  

    - 啟用帳戶  

    - 遠端啟用  

4. 在 [SMS]  節點下的 [安全性]  索引標籤上，選取 [站台_&lt;站台碼>]  節點，然後選擇 [安全性]  。 請確定 **SMS Admins** 群組具有下列權限︰  

    - 執行方法  

    - 提供者寫入  

    - 啟用帳戶  

    - 遠端啟用  

5. 儲存可還原 Configuration Manager 主控台存取權的權限。  

#### <a name="known-issue-for-remote-site-systems"></a>遠端站台系統的已知問題

在您升級裝載了站台系統角色的伺服器之後，值 `Software\Microsoft\SMS` 可能會從下列登錄機碼中遺失：`HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

若此值在您升級伺服器上的 Windows 之後遺失，請手動新增。 否則，站台系統角色在將檔案上傳到站台伺服器收件匣時可能會遇到問題。

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> 升級至 Windows Server 2012 R2

當您從 Windows Server 2008 R2 或 Windows Server 2012 升級至 Windows Server 2012 R2 時，會出現下列情況：

#### <a name="before-upgrade"></a>升級之前

- 在 Windows Server 2012 上：若已安裝 WSUS 角色，請從伺服器上移除。 您可以保留 SUSDB，並在將 WSUS 重新安裝之後進行重新連結。  

- 在 Windows Server 2008 R2 上：在升級到 Windows Server 2012 R2 之前，您必須解除安裝伺服器的 WSUS 3.2。 您可以保留 SUSDB，並在將 WSUS 重新安裝之後進行重新連結。 如需詳細資訊，請參閱 [Windows Server Update Services 概觀](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality) \(英文\)。  

- 如果您要升級站台伺服器的 OS，請確定站台的[檔案型複寫](../../plan-design/hierarchy/file-based-replication.md)狀況良好。 檢查所有收件匣以確認傳送和接收站台上是否有待處理項目。 如果有許多停滯或擱置的複寫作業，請等候系統清除它們。<!-- SCCMDocs#1792 -->
    - 在傳送站台上，請檢閱 **sender.log**。
    - 在接收站台上，請檢閱 **despooler.log**。

#### <a name="after-upgrade"></a>升級之後

- 升級處理序會停用 Windows 部署服務。 請確定下列站台系統角色的此服務已啟動且在執行中：  

    - 網站伺服器  

    - 管理點  

    - 應用程式類別目錄 Web 服務點  

    - 應用程式類別目錄網站點  

- 請確定 **Windows 處理序啟用**與 **WWW/W3svc** 服務皆已啟用，且已設定為自動啟動。 升級處理序會停用這些服務，因此請確定已對下列站台系統角色執行了這些服務：  

    - 網站伺服器  

    - 管理點  

    - 應用程式類別目錄 Web 服務點  

    - 應用程式類別目錄網站點  

- 請確定每部裝載站台系統角色的伺服器，都能繼續符合所有[必要條件](../../plan-design/configs/site-and-site-system-prerequisites.md)。 例如，您可能需要重新安裝 BITS、WSUS，或設定 IIS 的特定設定。  

    還原所有缺少的必要條件之後，請再重新啟動一次伺服器，確認服務已啟動且在運作中。  

### <a name="unsupported-upgrade-scenarios"></a>不支援的升級案例

下列是一般會問及的 Windows Server 升級案例，但不受 Configuration Manager 支援：  

- Windows Server 2008 到 Windows Server 2012 或更新版本  

- Windows Server 2008 R2 到 Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> 升級用戶端的作業系統  

在下列情況下，Configuration Manager 支援 Configuration Manager 用戶端的作業系統就地升級：  

- 若 Configuration Manager 支援所產生的 Service Pack 層級，其即支援就地升級為更新版本的 Windows Service Pack。  

- 將 Windows 從支援的版本就地升級到 Windows 10。 如需詳細資訊，請參閱[將 Windows 升級至最新版本](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

- Windows 10 的組建至組建維護升級。 如需詳細資訊，請參閱[管理 Windows 即服務](../../../osd/deploy-use/manage-windows-as-a-service.md)。  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> 升級 SQL Server  

Configuration Manager 支援在站台資料庫伺服器上，就地升級 SQL Server。

如需 Configuration Manager 所支援 SQL Server 版本的相關資訊，請參閱 [SQL Server 版本支援](../../plan-design/configs/support-for-sql-server-versions.md)。  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>升級 SQL Server 的 Service Pack 版本

若 Configuration Manager 仍然支援所產生的 SQL Server Service Pack 層級，其即支援將 SQL Server 就地升級為更新版本的 Service Pack。

在階層中有多個 Configuration Manager 站台時，每個站台都可以執行不同 Service Pack 版本的 SQL Server。 對站台升級 SQL Server Service Pack 版本的順序沒有限制。

### <a name="upgrade-to-a-new-version-of-sql-server"></a>升級到新版 SQL Server

Configuration Manager 支援將 SQL Server 就地升級至下列版本：

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

這包括在次要站台將 SQL Server Express 升級到較新版本的 SQL Server Express。

當您升級裝載站台資料庫的 SQL Server 版本時，必須以下列順序升級站台上使用的 SQL Server 版本：

1. 先升級管理中心站台的 SQL Server  

2. 在升級次要站台的父主要站台之前，請先升級次要站台  

3. 最後升級父主要站台。 這些站台包括向管理中心網站報告的二個子主要站台，以及階層頂層站台的獨立主要站台。  

### <a name="sql-server-cardinality-estimation-level"></a>SQL Server 基數估計層級

從舊版 SQL Server 升級站台資料庫時，資料庫會保留其現有的 SQL 基數估計層級 (若其為該 SQL Server 執行個體所允許的最小層級)。 升級 SQL Server 時，若其資料庫相容性層級低於允許的層級，會自動將該資料庫設定成 SQL Server 所允許的最低相容性層級。

下表識別 Configuration Manager 站台資料庫的建議相容性層級︰

|SQL Server 版本 | 支援的相容性層級 | 建議層級 |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

若要識別站台資料庫使用中的 SQL Server 基數估計相容性層級，請在站台資料庫伺服器上執行下列 SQL 查詢：  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

如需 SQL CE 相容性層級和其設定方式的詳細資訊，請參閱 [ALTER DATABASE 相容性層級 (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017)。

如需升級 SQL Server 的詳細資訊，請參閱下列 SQL Server 文章：  

- [升級到 SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [升級到 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [升級到 SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>在站台資料庫伺服器升級 SQL Server  

1. 停止站台上的所有 Configuration Manager 服務  

2. 將 SQL Server 升級至支援的版本  

3. 重新啟動 Configuration Manager 服務  

> [!NOTE]  
> 當您從 Standard 的管理中心站台使用中的 SQL Server 版本，變更至 Datacenter 或 Enterprise 時，資料庫分割不會變更。 此資料庫分割會限制階層所支援的用戶端數目。  
