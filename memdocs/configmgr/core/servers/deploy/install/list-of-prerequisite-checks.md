---
title: 先決條件檢查
titleSuffix: Configuration Manager
description: Configuration Manager 更新之特定先決條件檢查的參考。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d8fc9abfc9fc09bc3011a3fee30b258023d04c8a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700736"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Configuration Manager 先決條件檢查的清單

適用於：  Configuration Manager (最新分支)

本文詳述當您安裝或更新 Configuration Manager 時所執行的必要條件檢查。 如需詳細資訊，請參閱[先決條件檢查程式](prerequisite-checker.md)。  



## <a name="errors"></a>錯誤

### <a name="active-migration-mappings-on-the-target-primary-site"></a>目標主要網站上作用中的移轉對應

適用於：*管理中心網站*

沒有主要站台的使用中移轉對應。

### <a name="active-replica-mp"></a>使用中的複本 MP

適用於：*主要站台*

具有使用中的管理點複本。

### <a name="administrative-rights-on-expand-primary-site"></a>擴充主要網站的系統管理權限

適用於：*管理中心網站*

當您將主要站台擴充到階層時，執行安裝程式的使用者帳戶具有獨立主要站台伺服器上的 [系統管理員]  權限。

### <a name="administrative-rights-on-site-system"></a>網站系統的系統管理權限

適用於：*管理中心網站、主要站台、次要站台*

執行 Configuration Manager 安裝程式的使用者帳戶具有站台伺服器上的 [系統管理員]  權限。

### <a name="administrator-rights-on-central-administration-site"></a>管理中心網站上的系統管理員權限

適用於：*主要站台*

執行 Configuration Manager 安裝程式的使用者帳戶具有管理中心網站伺服器上的 [系統管理員]  權限。

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>所擴充主要站台上的 Asset Intelligence 同步處理點

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台上並未安裝 Asset Intelligence 同步處理點角色。

### <a name="bits-enabled"></a>BITS 已啟用

適用於：*管理點*

管理點上已安裝背景智慧型傳送服務 (BITS)。 這項檢查可能會因為下列其中一個原因而失敗：

- 未安裝 BITS  

- 伺服器或遠端 IIS 主機上未安裝適用於 IIS 7.0 的 IIS 6.0 WMI 相容性元件  

- 安裝程式無法確認遠端 IIS 設定。 站台伺服器上未安裝 IIS 通用元件。  

### <a name="case-insensitive-collation-on-sql-server"></a>SQL Server 上的不區分大小寫定序

適用於：  站台資料庫伺服器

SQL Server 安裝使用不區分大小寫定序，例如 **SQL_Latin1_General_CP1_CI_AS**。

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>擴充主要站台上的管理中心網站伺服器系統管理權限

適用於：*管理中心網站*

當您將主要站台擴充到階層時，管理中心網站伺服器的電腦帳戶具有獨立主要站台伺服器上 [系統管理員]  權限。

### <a name="client-version-on-management-point-computer"></a>管理點電腦上的用戶端版本

適用於：*管理點*

您要安裝管理點的伺服器並未安裝不同版本的 Configuration Manager 用戶端。

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>所擴充主要站台上的雲端管理閘道

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台上並未安裝雲端管理閘道角色。

### <a name="connection-to-sql-server-on-central-administration-site"></a>管理中心網站上的 SQL Server 連線

適用於：*主要站台*

在要加入現有階層之主要站台上執行 Configuration Manager 安裝程式的使用者帳戶，具有管理中心網站上 SQL Server 執行個體的 [系統管理員]  角色。

### <a name="custom-client-agent-settings-have-nap-enabled"></a>自訂用戶端代理程式設定已啟用 NAP

適用於：*管理中心網站、主要站台*

沒有啟用網路存取保護 (NAP) 的自訂用戶端設定。

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>所擴充主要站台上的資料倉儲服務點

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台上並未安裝資料倉儲服務點角色。

### <a name="dedicated-sql-server-instance"></a>專用的 SQL Server 執行個體

適用於：*管理中心網站、主要站台、次要站台*

您已設定專用的 SQL Server 執行個體來裝載 Configuration Manager 站台資料庫。

如果另一個站台使用執行個體，則您必須為新站台選取不同的執行個體。 您也可以解除安裝另一個站台，或將其資料庫移至不同的 SQL Server 執行個體。

### <a name="default-client-agent-settings-have-nap-enabled"></a>預設用戶端代理程式設定已啟用 NAP

適用於：*管理中心網站、主要站台*

預設用戶端設定未啟用網路存取保護 (NAP)。

### <a name="domain-membership-error"></a>網域成員資格 (錯誤)

適用於：*管理中心網站、主要站台、次要站台、SMS 提供者、SQL Server*

Configuration Manager 電腦是 Windows 網域的成員。

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>所擴充主要站台上的 Endpoint Protection 點

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台上並未安裝 Endpoint Protection 點角色。

### <a name="existing-configuration-manager-server-components-on-server"></a>伺服器上現有的 Configuration Manager 伺服器元件

適用於：*管理中心網站、主要站台、次要站台*

所選取要進行站台安裝的伺服器上尚未安裝站台伺服器或站台系統角色。

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>現有獨立主要站台的版本及站台碼

適用於：*管理中心網站、主要站台*

您要擴充的主要站台是獨立主要站台。 其 Configuration Manager 版本與要安裝的管理中心網站相同，但站台碼不同。

### <a name="firewall-exception-for-sql-server"></a>SQL Server 的防火牆例外狀況

適用於：*管理中心網站、主要站台、次要站台、管理點*

Windows 防火牆已停用，或存在 SQL Server 的相關 Windows 防火牆例外。

允許從遠端存取 Sqlservr.exe 或必要的 TCP 通訊埠。 根據預設，SQL Server 會接聽 TCP 通訊埠 1433，SQL Server Service Broker 則使用 TCP 通訊埠 4022。

### <a name="free-disk-space-on-site-server"></a>網站伺服器上的可用磁碟空間

適用於：*管理中心網站、主要站台、次要站台*

若要安裝站台伺服器，必須至少有 15 GB 的可用磁碟空間。 如果您在同一部伺服器上安裝 SMS 提供者，則需要額外 1 GB 的可用空間。

### <a name="iis-service-running"></a>IIS 服務執行中

適用於：*管理點、發佈點*

用於管理點或發佈點的伺服器上已安裝並執行 IIS。

### <a name="incompatible-collection-references"></a>不相容的集合參考

適用於：*管理中心網站*

在升級期間，集合只會參考相同類型的其他集合。

### <a name="match-collation-of-expand-primary-site"></a>比對擴充主要站台的定序

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台和管理中心網站的站台資料庫擁有相同定序。

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性群組的最大文字複寫大小

適用於：  站台資料庫伺服器

使用 SQL Server Always On 時，必須正確設定 [最大文字複寫大小]  設定。 如需詳細資訊，請參閱[準備將 SQL Server Always On 可用性群組與 Configuration Manager 搭配使用](../configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>所擴充主要站台上的 Microsoft Intune 連接器

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台上並未安裝 Microsoft Intune 連接器角色。

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>已登錄 Microsoft 遠端差異壓縮 (RDC) 程式庫

適用於：*管理中心網站、主要站台、次要站台*

Configuration Manager 站台伺服器上已登錄 RDC 程式庫。

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

適用於：*管理中心網站、主要站台、次要站台*

確認 Windows Installer 版本。

這項檢查失敗時，表示安裝程式無法確認版本，或安裝的版本不符合 Windows Installer 4.5 的最低需求。

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Configuration Manager 主控台的最低 .NET Framework 版本

適用於：*Configuration Manager 主控台*

Configuration Manager 主控台電腦上已安裝 Microsoft .NET Framework 4.0。

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Configuration Manager 站台伺服器的最低 .NET Framework 版本

適用於：*管理中心網站、主要站台、次要站台*

Configuration Manager 站台伺服器上已安裝或啟用 .NET Framework 3.5。

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Configuration Manager 次要站台之 SQL Server Express Edition 安裝的最低 .NET Framework 版本

適用於：*次要站台*

Configuration Manager 次要站台伺服器上已安裝或啟用 .NET Framework 4.0。 SQL Server Express 需要此版本。

### <a name="parent-database-collation"></a>父資料庫定序

適用於：*主要站台、次要站台*

站台資料庫的定序符合父站台資料庫的定序。 階層中的所有網站都必須使用相同的資料庫定序。

### <a name="parent-site-replication-status"></a>父網站複寫狀態

適用於：*管理中心網站、主要站台*

父站台的複寫狀態是 [複寫使用中]  (狀態 **125**)。

### <a name="pending-system-restart"></a>系統重新啟動擱置中

適用於：*管理中心網站、主要站台、次要站台*

執行安裝程式之前，有其他程式要求重新啟動伺服器。

從 1810 版開始，這項檢查的彈性更高。 為了查看電腦是否處於暫止重新啟動狀態，它會檢查下列登錄位置：<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>主要 FQDN

適用於：*管理中心網站、主要站台、次要站台、站台資料庫伺服器*

電腦的 NetBIOS 名稱符合完整網域名稱 (FQDN) 的本機主機名稱。

### <a name="read-only-domain-controller"></a>唯讀網域控制站

適用於：*管理中心網站、主要站台、次要站台*

唯讀網域控制站 (RODC) 上不支援站台資料庫伺服器和次要站台伺服器。

如需詳細資訊，請參閱 Microsoft 支援服務的 [Problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911) (在網域控制站上安裝 SQL Server 時會發生的問題)。

### <a name="required-sql-server-collation"></a>必要的 SQL Server 定序

適用於：*管理中心網站、主要站台、次要站台*

已設定 SQL Server 執行個體使用 **SQL_Latin1_General_CP1_CI_AS** 定序。

如果已安裝 Configuration Manager 站台資料庫，這項檢查也適用於資料庫。 如需變更 SQL Server 執行個體和資料庫定序的資訊，請參閱 [SQL 定序和 Unicode 支援](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support)。

如果您使用中文 OS 並需要 GB18030 支援，則不適用這項檢查。 如需啟用 GB18030 支援的詳細資訊，請參閱[多語系支援](../../../plan-design/hierarchy/international-support.md)。

### <a name="server-service-is-running"></a>Server 服務執行中

適用於：*管理中心網站、主要站台、次要站台*

已啟動並執行 Server 服務。

### <a name="setup-source-folder"></a>安裝程式來源資料夾

適用於：*次要站台*

次要站台電腦帳戶具有安裝程式來源資料夾與共用的下列權限：

- **讀取**：NTFS 檔案系統權限  

- **讀取**：共用權限  

> [!Note]  
> 如果您使用系統管理共用 (例如 C$ 和 D$)，則次要站台電腦帳戶必須是伺服器上的 [系統管理員]  。  

### <a name="setup-source-version"></a>安裝程式來源版本

適用於：*次要站台*

為次要站台安裝指定來源資料夾中的 Configuration Manager 版本符合主要站台 Configuration Manager 版本。

### <a name="site-code-in-use"></a>使用中的網站碼

適用於：*主要站台*

指定的站台碼尚未在 Configuration Manager 階層中使用。 請為此站台指定唯一的站台碼。

### <a name="site-server-computer-account-administrative-rights"></a>網站伺服器電腦帳戶系統管理權限

適用於：*主要站台、站台資料庫伺服器*

站台伺服器電腦帳戶具有 SQL Server 及管理點上的 [系統管理員]  權限。

### <a name="site-server-fqdn-length"></a>站台伺服器 FQDN 長度

適用於：*管理中心網站、主要站台、次要站台*

站台伺服器的 FQDN 長度。

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>所擴充主要站台上處於被動模式的站台伺服器

適用於：*管理中心網站*

當您將主要站台擴充到階層時，獨立主要站台上並未安裝處於被動模式的站台伺服器角色。

### <a name="sms-provider-in-same-domain-as-site-server"></a>SMS 提供者與站台伺服器位於相同的網域

適用於：*SMS 提供者*

所有 SMS 提供者執行個體都與站台伺服器位於相同的網域。

### <a name="software-update-point-in-nlb-configuration"></a>NLB 設定中的軟體更新點

適用於：*軟體更新點*

站台未將網路負載平衡 (NLB) 用於使用中軟體更新點的任何虛擬位置。

### <a name="software-update-point-using-a-load-balancer"></a>使用負載平衡器的軟體更新點

適用於：*軟體更新點*

Configuration Manager 不支援網路負載平衡器 (NLB) 或硬體負載平衡器 (HLB) 上的軟體更新點。

### <a name="sql-server-always-on-availability-groups"></a>SQL Server Always On 可用性群組

適用於：  站台資料庫伺服器

使用 SQL Server Always On 時，必須符合裝載可用性群組的最低需求。 如需詳細資訊，請參閱[準備將 SQL Server Always On 可用性群組與 Configuration Manager 搭配使用](../configure/sql-server-alwayson-for-a-highly-available-site-database.md)。

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>SQL Server 可用性群組已設定為可讀取次要

適用於：  站台資料庫伺服器

使用 SQL Server Always On 時，檢查可用性群組複本的次要讀取狀態。

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>SQL Server 可用性群組已設定為手動容錯移轉

適用於：  站台資料庫伺服器

使用 SQL Server Always On 時，可用性群組複本已設定為手動容錯移轉。

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>預設執行個體上的 SQL Server 可用性群組複本

適用於：  站台資料庫伺服器

使用 SQL Server Always On 時，可用性群組複本位於預設執行個體上。

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>SQL 可用性群組複本必須全部具有相同的植入模式

<!-- SCCMDocs-pr#3899 -->
適用於：  站台資料庫伺服器

從 1906 版開始，使用 SQL Server Always On 時，您必須以相同的[植入模式](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)設定可用性群組複本。

### <a name="sql-availability-group-replicas-must-be-healthy"></a>SQL 可用性群組複本必須狀況良好

<!-- SCCMDocs-pr#3899 -->
適用於：  站台資料庫伺服器

從 1906 版開始，使用 SQL Server Always On 時，可用性群組複本處於狀況良好的狀態。

### <a name="sql-server-configuration-for-site-upgrade"></a>適用於站台升級的 SQL Server 設定

適用於：  站台資料庫伺服器

SQL Server 符合站台升級的最低需求。 如需詳細資訊，請參閱[支援的 SQL Server 版本](../../../plan-design/configs/support-for-sql-server-versions.md)。

### <a name="sql-server-edition"></a>SQL Server 版本

適用於：  站台資料庫伺服器

站台上的 SQL Server 不是 SQL Server Express。

### <a name="sql-server-express-on-secondary-site"></a>次要站台上的 SQL Server Express

適用於：*次要站台*

SQL Server Express 可成功安裝在次要站台伺服器上。

### <a name="sql-server-on-the-secondary-site-server"></a>次要站台伺服器上的 SQL Server

適用於：*次要站台*

次要站台伺服器上已安裝 SQL Server。 您無法在遠端站台系統上安裝作為次要站台的 SQL Server。

> [!Warning]  
> 這項檢查只有在您選取讓安裝程式使用現有 SQL Server 執行個體時才適用。  

### <a name="sql-server-service-running-account"></a>SQL Server 服務執行帳戶

適用於：*管理中心網站、主要站台、次要站台*

SQL Server 服務的登入帳戶不是本機使用者帳戶或 **LOCAL SERVICE**。

請將 SQL Server 服務設定為使用有效的網域帳戶、**NETWORK SERVICE** 或 **LOCAL SYSTEM**。

### <a name="sql-server-site-database-consistency"></a>SQL Server 站台資料庫一致性

適用於：  站台資料庫伺服器

確認資料庫一致性。

### <a name="sql-server-sysadmin-rights"></a>SQL Server sysadmin 權限

適用於：  站台資料庫伺服器

執行 Configuration Manager 安裝程式的使用者帳戶，具有為站台資料庫安裝選取之 SQL Server 執行個體上的 [系統管理員]  角色。 如果安裝程式無法存取 SQL Server 執行個體以確認權限，這項檢查也會失敗。

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>參照網站的 SQL Server sysadmin 權限

適用於：  站台資料庫伺服器

執行 Configuration Manager 安裝程式的使用者帳戶，具有選取為參照站台資料庫之 SQL Server 角色執行個體上的 [系統管理員]  角色。 需要有 SQL Server **sysadmin** 角色權限才能修改站台資料庫。

### <a name="sql-server-tcp-port"></a>SQL Server TCP 通訊埠

適用於：  站台資料庫伺服器

已啟用 SQL Server 執行個體的 TCP，並設定為使用靜態通訊埠。

### <a name="sql-server-version"></a>SQL Server 版本

適用於：  站台資料庫伺服器

所指定站台資料庫伺服器上已安裝支援的 SQL Server 版本。

如需詳細資訊，請參閱 [SQL Server 版本的支援](../../../plan-design/configs/support-for-sql-server-versions.md)。

### <a name="unsupported-os-for-configuration-manager-console"></a>Configuration Manager 主控台不支援的 OS

適用於：*Configuration Manager 主控台*

在執行支援 OS 版本的電腦上安裝 Configuration Manager 主控台。

如需詳細資訊，請參閱 [Configuration Manager 主控台的支援 OS 版本](../../../plan-design/configs/supported-operating-systems-consoles.md)。

### <a name="unsupported-os-for-site-server"></a>站台伺服器不支援的 OS

適用於：*管理中心網站、主要站台、次要站台、Configuration Manager 主控台、管理點、發佈點*

伺服器執行支援的 OS 版本。

如需詳細資訊，請參閱 [Configuration Manager 站台系統伺服器支援的 OS 版本](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)。

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>不支援的站台系統角色：頻外服務點

適用於：*主要站台*

未安裝頻外服務點站台系統角色。

### <a name="unsupported-site-system-role-system-health-validation-point"></a>不支援的站台系統角色：系統健全狀況驗證點

適用於：*主要站台*

未安裝系統健全狀況驗證點站台系統角色。

### <a name="unsupported-upgrade-path"></a>不支援的升級路徑

適用於：*管理中心網站、主要站台*

階層中所有站台伺服器都符合升級所需的 Configuration Manager 最低版本。

### <a name="usmt-installed"></a>已安裝 USMT

適用於：*管理中心網站、主要站台 (僅限獨立)*

已安裝 Windows 適用之 Windows 評定及部署套件 (ADK) 的使用者狀態移轉工具 (USMT) 元件。

### <a name="validate-fqdn-of-sql-server"></a>驗證 SQL Server 的 FQDN

適用於：  站台資料庫伺服器

您已為 SQL Server 電腦指定有效的 FQDN。

### <a name="verify-central-administration-site-version"></a>確認管理中心網站版本

適用於：*主要站台*

管理中心網站具有相同版本的 Configuration Manager。

### <a name="verify-database-consistency"></a>確認資料庫一致性

適用於：*管理中心網站、主要站台*

確認 SQL Server 中站台資料庫的一致性。  

### <a name="windows-deployment-tools-installed"></a>已安裝 Windows 部署工具

適用於：*SMS 提供者*

已安裝 Windows ADK 的 Windows 部署工具元件。

### <a name="windows-failover-cluster"></a>Windows 容錯移轉叢集

適用於：*站台伺服器、管理點、發佈點*

具有站台伺服器、管理點或發佈點角色之伺服器不是 Windows 叢集的一部分。

從 1810 版開始，Configuration Manager 安裝程序不會再封鎖在具有容錯移轉叢集 Windows 角色的電腦上安裝站台伺服器角色。 SQL Always On 需要此角色，因此先前您無法將站台資料庫共置在站台伺服器上。 透過這項變更，您可以使用較少的伺服器建立高可用性的站台，方法是被動模式中使用 SQL AlwaysOn 和站台伺服器。 如需詳細資訊，請參閱[高可用性選項](../configure/high-availability-options.md)。 <!--1359132-->  

### <a name="windows-pe-installed"></a>已安裝 Windows PE

適用於：*SMS 提供者*

已安裝 Windows ADK 的 Windows 預先安裝環境 (PE) 元件。



## <a name="warnings"></a>警告

### <a name="active-directory-domain-functional-level"></a>Active Directory 網域功能等級

適用於：*管理中心網站、主要站台*

Active Directory 網域與樹系功能等級至少為 Windows Server 2008 R2。 如需詳細資訊，請參閱[對 Active Directory 網域的支援](../../../plan-design/configs/support-for-active-directory-domains.md)。

### <a name="administrative-rights-on-distribution-point"></a>發佈點上的系統管理權限

適用於：*發佈點*

執行安裝程式之使用者帳戶具有發佈點上的 [系統管理員]  權限。

### <a name="administrative-rights-on-management-point"></a>管理點上的系統管理權限

適用於：*管理點、發佈點*

站台伺服器電腦帳戶具有管理點及發佈點上的 [系統管理員]  權限。

### <a name="administrative-share-site-system"></a>系統管理共用 (站台系統)

適用於：*管理點*

站台系統電腦上有必要的系統管理共用。

### <a name="application-compatibility"></a>應用程式相容性

適用於：*管理中心網站、主要站台*

目前的應用程式與應用程式架構相容。

### <a name="backlogged-inboxes"></a>積存的收件匣

適用於：*管理中心網站、主要站台*

站台伺服器正在及時處理重要的收件匣。 收件匣未包含晚於一天的檔案。

它會檢查下列收件匣資料夾：

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

若要解決這個警告，請檢查 Despooler 和排程器站台系統元件是否正在執行。

### <a name="bits-installed"></a>BITS 已安裝

適用於：*管理點*

IIS 中已安裝並啟用背景智慧型傳送服務 (BITS)。

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>檢查站台是否使用更新整備小幫手雲端服務連接器

適用於：*管理中心網站、主要站台*

更新整備小幫手服務已於 2020 年 1 月 31 日淘汰。 如需詳細資訊，請參閱 [KB 4521815：Windows Analytics 於 2020 年 1 月 31 日淘汰](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。

電腦分析是 Windows Analytics 的演進。 如需詳細資訊，請參閱[什麼是電腦分析](../../../../desktop-analytics/overview.md)。

如果您的 Configuration Manager 站台與更新整備小幫手相連，則必須將其移除並重新設定用戶端。 如需詳細資訊，請參閱[移除更新整備小幫手連線](../../../clients/manage/upgrade-readiness.md#bkmk_remove)。

如果忽略此必要條件警告，Configuration Manager 安裝程式即會自動移除更新整備小幫手連接器。<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>雲端管理閘道需要權杖型驗證或 HTTPS 管理點

適用於：*雲端管理閘道*

在某些 Configuration Manager 版本中，您無法搭配雲端管理閘道 (CMG) 使用 HTTP 管理點。 請設定 CMG 使用 HTTPS，或設定站台使用增強 HTTP。 如需詳細資訊，請參閱[規劃雲端管理閘道](../../../clients/manage/cmg/plan-cloud-management-gateway.md)。

### <a name="configuration-for-sql-server-memory-usage"></a>設定 SQL Server 記憶體使用量

適用於：  站台資料庫伺服器

SQL Server 的記憶體使用量已設定為無限制。 請將 SQL Server 記憶體設定為具有上限。

### <a name="distribution-point-package-version"></a>發佈點套件版本

適用於：*發佈點*

網站中所有發佈點具有最新版本的軟體發佈套件。

### <a name="domain-membership-warning"></a>網域成員資格 (警告)

適用於：*管理點、發佈點*

Configuration Manager 電腦是 Windows 網域的成員。

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>SQL Server 的防火牆例外 (獨立主要站台)

適用於：*主要站台 (僅限獨立)*

Windows 防火牆已停用，或存在 SQL Server 的相關 Windows 防火牆例外。

允許從遠端存取 Sqlservr.exe 或必要的 TCP 通訊埠。 根據預設，SQL Server 會接聽 TCP 通訊埠 1433，Server Service Broker 則使用 TCP 通訊埠 4022。

### <a name="firewall-exception-for-sql-server-for-management-point"></a>管理點的 SQL Server 防火牆例外狀況

適用於：*管理點*

Windows 防火牆已停用，或存在 SQL Server 的相關 Windows 防火牆例外。

### <a name="iis-https-configuration"></a>IIS HTTPS 設定

適用於：*管理點、發佈點*

IIS 網站具有 HTTPS 通訊協定的繫結。

當您安裝需要 HTTPS 的站台角色時，請在所指定的伺服器上使用有效的公開金鑰基礎結構 (PKI) 憑證來設定 IIS 網站繫結。

### <a name="invalid-discovery-records"></a>探索記錄無效

適用於：管理中心網站 

有不再有效的探索記錄。 這些記錄將會標示為待刪除。

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60)

適用對象：管理中心網站、主要站台、次要站台、Configuration Manager 主控台、管理點、發佈點 

確認已安裝 MSXML 6.0 或更新版本。

### <a name="network-access-protection-nap-is-no-longer-supported"></a>已不再支援網路存取保護 (NAP)

適用於：*主要站台*

沒有啟用 NAP 的軟體更新。

### <a name="ntfs-drive-on-site-server"></a>站台伺服器上的 NTFS 磁碟機

適用於：*主要站台*

磁碟機已使用 NTFS 檔案系統進行格式化。 在使用 NTFS 檔案系統格式化的磁碟機上安裝站台伺服器元件可獲得較高的安全性。

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> 暫止的設定項目原則更新

<!--SCCMDocs-pr issue 2814-->

適用於：*主要站台*

從 1806 版開始，當您要從 1706 或更新版本更新時，如果您有許多應用程式部署，且至少其中一個需要核准，可能會看到此警告。

您有兩個選項：  

- 忽略警告並繼續更新。 這個動作會導致站台伺服器在更新期間因處理原則而增加處理。 您可能也會在更新後，在管理點上看到更多處理器負載。  

- 修改其中一個不具任何需求或具特定 OS 需求的應用程式。 在該時間預先處理站台伺服器上某些負載。 檢閱 **objreplmgr.log**，然後在管理點上監視處理器。 處理完成後，請更新站台。 更新後，仍有一些額外的處理，但比使用第一個選項忽略警告還少。  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>遠端 SQL Server 上的暫止系統重新啟動

適用於：*1902 版和更新版本，遠端 SQL Server*

執行安裝程式之前，有其他程式要求重新啟動伺服器。

為了查看電腦是否處於暫止重新啟動狀態，它會檢查下列登錄位置：<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>網站伺服器上的 PowerShell 2.0

適用於：*具有 Exchange 連接器的主要站台*

Configuration Manager Exchange Connector 的站台伺服器上已安裝 Windows PowerShell 2.0 或更新版本。

### <a name="remote-connection-to-wmi-on-secondary-site"></a>次要站台上的 WMI 遠端連線

適用於：*次要站台*

安裝程式可與次要站台伺服器上的 WMI 建立遠端連線。

### <a name="schema-extensions"></a>架構延伸模組

適用於：*管理中心網站、主要站台*

已擴充 Active Directory 架構。 如果已擴充，則會使用架構延伸模組的版本。

Configuration Manager 不需要 Active Directory 架構延伸模組來安裝站台伺服器。 Microsoft 建議使用它們以完整使用所有 Configuration Manager 功能。 如需擴充架構之優點的詳細資訊，請參閱[準備 Active Directory 以發行站台](../../../plan-design/network/extend-the-active-directory-schema.md)。

### <a name="share-name-in-package"></a>套件中的共用名稱

適用於：*管理中心網站、主要站台*

套件的共用名稱中沒有無效字元，例如 `#`。

### <a name="site-system-to-sql-server-communication"></a>站台系統與 SQL Server 的通訊

適用於：*次要站台、管理點*

您設定為針對站台資料庫執行個體執行 SQL Server 服務的帳戶，具有 Active Directory 網域服務中的有效服務主體名稱 (SPN)。 請在 Active Directory 中註冊有效的 SPN 以支援 Kerberos 驗證。

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> SQL Server 變更追蹤清除

適用於：*站台資料庫伺服器*

從 1810 版開始，檢查站台資料庫是否有 SQL 變更追蹤資料的待辦項目。<!--SCCMDocs-pr issue 3023-->  

若要手動確認這項檢查，請在站台資料庫中執行診斷預存程序。 首先，建立站台資料庫的[診斷連接](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017)。 最簡單的方法是使用 SQL Server Management Studio 的「資料庫引擎查詢編輯器」，然後連線至 `admin:<instance name>`。

在專用管理員連接查詢視窗中，執行下列命令：

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

視您的資料庫大小和待辦項目大小而定，此預存程序可能需要數分鐘或數小時的時間來執行。 當查詢完成時，您會看到兩個與待辦項目相關的資料區段。 請先檢視 **CT_Days_Old**。 此值會告訴您 syscommittab 資料表中最舊項目的存留期 (天)。 它應該是五天，這是 Configuration Manager 預設值。 請勿變更此預設值。 有時候會發生大量資料處理或複寫，此時 syscommittab 中的最舊項目可能會超過五天。 如果此值超過七天，請對變更追蹤資料執行手動清除。  

若要清除變更追蹤資料，請在專用管理連接中執行下列命令：

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

此命令會開始清除 syscommittab 及所有相關聯的子資料表。 它可能需要數分鐘或數小時的時間來執行。 若要監視其進度，請查詢 **vLogs** 檢視。 若要查看目前進度，請執行下列查詢：

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 更新 SQL Server Native Client 可能需要重新啟動，這可能會影響站台安裝程序。

此檢查可確保站台具有支援的 SQL Native Client 版本。 從 1810 版開始，最低版本是 SQL 2012 SP4 (`11.*.7001.0`)。

這個 SQL Native Client 版本支援 TLS 1.2。 如需詳細資訊，請參閱下列文章：

- [Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [如何啟用 Configuration Manager 的 TLS 1.2](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager 會在下列站台系統角色上使用 SQL Server Native Client：<!-- SCCMDocs issue 1150 -->

- 網站資料庫伺服器
- 站台伺服器：管理中心網站、主要站台或次要站台
- 管理點
- 裝置管理點
- 狀態移轉點
- SMS 提供者
- 軟體更新點
- 啟用多點傳送的發佈點
- Asset Intelligence 更新服務點
- Reporting Services 點
- 應用程式類別目錄 Web 服務
- 註冊點
- Endpoint Protection 點
- 服務連接點
- 憑證登錄點
- 資料倉儲服務點

### <a name="sql-server-process-memory-allocation"></a>SQL Server 處理程序記憶體配置

適用於：  站台資料庫伺服器

SQL Server 至少保留 8 GB 記憶體給管理中心網站和主要站台，以及至少 4 GB 記憶體給次要站台。

如需詳細資訊，請參閱[如何使用 SQL Server Management Studio 設定記憶體選項](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-)。

> [!NOTE]  
> 這項檢查不適用次要站台上的 SQL Server Express。 此版本的保留記憶體僅限於 1 GB。  

### <a name="sql-server-security-mode"></a>SQL Server 安全性模式

適用於：  站台資料庫伺服器

已針對 Windows 驗證安全性設定 SQL Server。

### <a name="unsupported-site-system-os-version-for-upgrade"></a>不支援升級的站台系統 OS 版本

適用於：*主要站台、次要站台*

在執行 Windows Server 2012 或更新版本的伺服器上安裝了發佈點以外的站台系統角色。

如需詳細資訊，請參閱 [Configuration Manager 站台系統伺服器支援的作業系統](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)。

> [!NOTE]  
> 這項檢查無法解析安裝在 Azure 中的站台系統角色狀態，也無法解析 Microsoft Intune 所使用的雲端儲存空間。 請將這些角色的警告視為誤判而予以忽略。

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>不支援升級評定工具組

適用於：*管理中心網站、主要站台*

未安裝升級評定工具組。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>確認站台伺服器發佈至 Active Directory 的權限

適用於：*管理中心網站、主要站台、次要站台*

站台伺服器的電腦帳戶對其 Active Directory 網域中的 [系統管理]  容器具有 [完全控制]  權限。

如需詳細資訊，請參閱[準備 Active Directory 以發佈站台](../../../plan-design/network/extend-the-active-directory-schema.md)。

> [!NOTE]  
> 如果您要手動確認權限，則可忽略此警告。

### <a name="windows-remote-management-winrm-v11"></a>Windows 遠端管理 (WinRM) v1.1

適用於：*主要站台、Configuration Manager 主控台*

主要站台伺服器或 Configuration Manager 主控台電腦上已安裝 WinRM 1.1，以執行頻外管理主控台。

目前支援的所有 Windows 版本會自動安裝 WinRM。 如需詳細資訊，請參閱 [Installation and Configuration for Windows Remote Management](https://docs.microsoft.com/windows/win32/winrm/installation-and-configuration-for-windows-remote-management) (Windows 遠端管理的安裝和設定)。

### <a name="wsus-on-site-server"></a>網站伺服器上的 WSUS

適用於：*管理中心網站、主要站台*

站台伺服器上已安裝支援的 Windows Server Update Services (WSUS) 版本。

當您在站台伺服器以外的伺服器上使用軟體更新點時，必須在站台伺服器上安裝 WSUS 管理主控台。 如需 WSUS 的詳細資訊，請參閱 [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)。
