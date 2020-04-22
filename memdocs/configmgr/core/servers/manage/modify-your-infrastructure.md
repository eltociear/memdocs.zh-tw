---
title: 修改基礎結構
titleSuffix: Configuration Manager
description: 變更或採取可影響 Configuration Manager 基礎結構的動作。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694356"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>修改 Configuration Manager 基礎結構

適用於：  Configuration Manager (最新分支)

安裝一或多個站台之後，您可能需要修改設定，或採取會影響您基礎結構的動作。

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> 管理 SMS 提供者

SMS 提供者會為一或多個 Configuration Manager 主控台提供系統管理連絡點。 當您安裝多個 SMS 提供者時，可為連絡點提供備援，以管理站台與階層。

在每個 Configuration Manager 站台上，您可以重新執行安裝程式，以：

- 新增 SMS 提供者的其他執行個體。 每個 SMS 提供者的其他執行個體都必須位於個別的電腦上。

- 移除 SMS 提供者的執行個體。 若要移除站台的最後一個 SMS 提供者，您必須將站台解除安裝。

在執行安裝程式的站台伺服器根資料夾中檢視 **ConfigMgrSetup.log**，以監視 SMS 提供者的安裝或移除。

修改站台上的 SMS 提供者之前，請參閱[規劃 SMS 提供者](../../plan-design/hierarchy/plan-for-the-sms-provider.md)。

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>管理站台的 SMS 提供者設定  

1. 從 Configuration Manager 站台安裝資料夾中的 `\BIN\X64\setup.exe`，執行 **Configuration Manager 安裝程式**。

1. 在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台]  。

1. 在 [站台維護]  頁面上，選取 [修改 SMS 提供者設定]  。

1. 在 [管理 SMS 提供者]  頁面上，選取下列其中一個選項：

    - **新增 SMS 提供者**：指定電腦的 FQDN，以裝載目前未加以裝載的 SMS 提供者。

    - **解除安裝指定的 SMS 提供者**：選取您要從中移除 SMS 提供者之電腦的名稱。

    > [!TIP]  
    > 若要在兩部電腦間移動 SMS 提供者，請先將其安裝到新電腦上。 接著，將其從原始位置移除。 沒有任何選項可在電腦之間移動 SMS 提供者。

安裝精靈完成後，就會完成 SMS 提供者設定。 在站台 [內容]  的 [一般]  索引標籤上，確認是否有已為站台安裝 SMS 提供者的電腦。

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a> 管理 Configuration Manager 主控台

下列工作可協助您管理 Configuration Manager 主控台：

- 若要修改 Configuration Manager 主控台中顯示的語言，請參閱[管理 Configuration Manager 主控台語言](#BKMK_ManageConsoleLanguages)一節。

- 若要安裝其他主控台，請參閱[安裝 Configuration Manager 主控台](../deploy/install/install-consoles.md)。

- 若要設定 DCOM 權限以啟用站台伺服器的遠端主控台，請參閱[設定遠端 Configuration Manager 主控台的 DCOM 權限](#BKMK_ConfigDCOMforRemoteConsole)一節。

- 若要修改系統管理權限，限制使用者可以在主控台中查看並執行的項目，請參閱[修改系統管理使用者的系統管理範圍](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)。

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a> 管理 Configuration Manager 主控台語言

在站台伺服器安裝期間，Configuration Manager 主控台安裝檔案與站台的支援語言套件，皆會複製到站台伺服器上 Configuration Manager 安裝路徑的 `\Tools\ConsoleSetup` 子資料夾。

- 當您從站台伺服器的這個資料夾啟動 Configuration Manager 主控台安裝時，其會將 Configuration Manager 主控台與支援的語言套件檔案複製到電腦。

- 當語言套件可供電腦上的目前語言設定使用時，Configuration Manager 主控台會以該語言開啟。

- 如果 Configuration Manager 主控台無法使用相關聯的語言套件，則主控台便會以英文 (美國) 開啟。

例如，您可以從支援英文、德文與法文的站台伺服器安裝 Configuration Manager 主控台。 如果您在設定之語言設定為法文的電腦上開啟 Configuration Manager 主控台，主控台會以法文開啟。 如果您在設定之語言為日文的電腦上開啟 Configuration Manager 主控台，則主控台會以英文開啟，因為未提供日文語言套件。  

每次 Configuration Manager 主控台開啟時：

- 其會決定電腦已設定的語言設定
- 確認 Configuration Manager 主控台是否可以使用相關聯的語言套件
- 使用適當的語言套件開啟主控台

如果您想要以英文開啟 Configuration Manager 主控台，則無論電腦上已設定的語言設定為何，都請移除或重新命名電腦上的語言套件檔案。

無論電腦上已設定的地區設定為何，都可使用下列程序以英文啟動 Configuration Manager 主控台。  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>在電腦上安裝僅英文版的 Configuration Manager 主控台  

1. 在 [Windows 檔案總管] 中，瀏覽至 Configuration Manager 安裝路徑中的 `\Tools\ConsoleSetup\LanguagePack`。

1. 重新命名 **.msp** 和 **.mst** 檔案。 例如，您可以將 **&lt;檔案名稱\>.MSP** 變更為 **&lt;檔案名稱\>.MSP.disabled**。

1. 在電腦上安裝 Configuration Manager 主控台。

    > [!IMPORTANT]
    > 為站台伺服器設定新的伺服器語言時，會將 .msp 與 .mst 檔案重新複製到 **LanguagePack** 資料夾，而您必須重複此程序，僅以英文安裝新的 Configuration Manager 主控台。  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>在現有 Configuration Manager 主控台安裝時暫時停用主控台語言

1. 在執行 Configuration Manager 主控台的電腦上，關閉 Configuration Manager 主控台。

1. 在 Windows 檔案總管中，瀏覽至 Configuration Manager 主控台電腦上的 &lt;*ConsoleInstallationPath*>\Bin\。  

1. 針對電腦上已設定的語言，重新命名適當的語言資料夾。 例如，若電腦的語言設定已設為德文，您可以將 [de]  資料夾重新命名為 [de.disabled]  。  

1. 若要以為電腦設定的語言開啟 Configuration Manager 主控台，請將資料夾重新命名為原始名稱。 例如，將 [de.disabled]  重新命名為 [de]  。  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> 設定遠端主控台的 DCOM 權限

執行 Configuration Manager 主控台的使用者帳戶，需要擁有可以使用 SMS 提供者存取站台資料庫的權限。 不過，使用遠端 Configuration Manager 主控台的系統管理使用者，在下列電腦上也需要 [遠端啟用]  DCOM 權限：

- 網站伺服器電腦

- 裝載 SMS 提供者執行個體的每部電腦

名為 **SMS Admins** 的安全性群組會授與在電腦上存取 SMS 提供者的權限，也可用於授與必要的 DCOM 權限。 當 SMS 提供者在成員伺服器上執行時，此群組位於電腦的本機。 當 SMS 提供者在網域控制站上執行時，其為網域本機群組。

> [!IMPORTANT]
> Configuration Manager 主控台會使用 WMI 連線到 SMS 提供者，而 WMI 內部則會使用 DCOM。 如果 Configuration Manager 主控台在與 SMS 提供者電腦不同的電腦上執行，則其需要權限，才能在 SMS 提供者電腦上啟動 DCOM 伺服器。 根據預設，遠端啟用只會授與內建 Administrators 群組的成員。
>
> 如果您允許 SMS Admins 群組擁有遠端啟用權限，此群組的成員可能會對 SMS 提供者電腦進行 DCOM 攻擊。 此設定也會增加電腦的攻擊面。 若要減輕威脅，請仔細監視 SMS Admins 群組的成員資格。

使用下列程序，設定各管理中心網站 (CAS)、主要站台伺服器，以及安裝 SMS 提供者的電腦，以授與系統管理使用者遠端 Configuration Manager 主控台存取權。

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>設定遠端 Configuration Manager 主控台連線的 DCOM 權限

1. 以目標電腦上的系統管理員身分，執行 `Dcomcnfg.exe` 以開啟 [元件服務]  。

1. 依序展開 [元件服務]  、[電腦]  ，然後選取 [我的電腦]  。 選取 [動作]  功能表上的 [內容]  。

1. 在 [我的電腦內容]  視窗中，切換至 [COM 安全性]  索引標籤。在 [啟動和啟用權限]  區段中，選取 [編輯限制]  。

1. 在 [啟動和啟用權限]  視窗中，選取 [新增]  。

1. 在 [選取使用者、電腦、服務帳戶或群組]  視窗的 [輸入要選取的物件名稱]  欄位中，輸入 `SMS Admins`，然後選取 [確定]  。

   > [!TIP]
   > 若要找出 SMS Admins 群組，您可能必須變更下列設定：**從這個位置**。 當 SMS 提供者在成員伺服器上執行時，此群組位於電腦本機，而當 SMS 提供者在網域控制站上執行時，此群組便會是網域本機群組。

1. 在 [SMS Admins 的權限]  區段中，若要允許遠端啟用，請選取 [遠端啟用]  列的 [允許]  欄。

1. 選取 [確定]  以儲存變更並關閉所有視窗。

您的電腦現在已設定為允許遠端 Configuration Manager 主控台存取 SMS Admins 群組的成員。

在支援遠端 Configuration Manager 主控台的每一部 SMS 提供者電腦上，重複執行此程序。

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a> 修改站台資料庫組態

安裝站台之後，您可以修改站台資料庫與站台資料庫伺服器的設定。 在 CAS 伺服器或主要站台伺服器上執行 Configuration Manager 安裝程式，以進行變更。 您可以將站台資料庫移到相同電腦上的 SQL Server 新執行個體，或移到執行受支援 SQL Server 版本的另一台電腦上。 次要站台的資料庫設定不支援這些變更。

如需支援限制的詳細資訊，請參閱 [Support policy for manual database changes in a Configuration Manager environment](https://support.microsoft.com/kb/3106512)(在 Configuration Manager 環境中手動變更資料庫的支援原則)。  

> [!NOTE]
> 修改站台的資料庫設定時，Configuration Manager 會在與資料庫通訊的站台伺服器和遠端站台系統伺服器上，重新啟動或重新安裝 Configuration Manager 服務。

### <a name="modify-the-database-configuration"></a>修改資料庫設定

在站台伺服器上執行 Configuration Manager 安裝程式，然後選取 [執行站台維護或重設此站台]  選項。 接著，選取 [修改 SQL Server 設定]  選項。 您可以變更以下站台資料庫設定：

- 裝載資料庫的 Windows 伺服器。

- 在裝載 SQL Server 資料庫的伺服器上使用的 SQL Server 執行個體。

- 資料庫名稱。

- Configuration Manager 正在使用 SQL Server 連接埠。

- Configuration Manager 正在使用 SQL Server Service Broker 連接埠。

### <a name="move-the-site-database"></a>移動站台資料庫

如果您移動站台資料庫，也必須檢閱下列設定：

- 將站台資料庫移到新電腦時，請將站台伺服器的電腦帳戶新增至執行 SQL Server 之電腦上的本機 **Administrators** 群組。 如果您使用站台資料庫的 SQL Server 叢集，請將電腦帳戶新增至每部 Windows Server 叢集節點電腦的本機 **Administrators** 群組。

- 當您將資料庫移到 SQL Server 上的新執行個體，或移到新的 SQL Server 電腦時，啟用 Common Language Runtime (CLR) 整合。 使用 **SQL Server Management Studio** 連線到裝載站台資料庫之 SQL Server 的執行個體。 接著，將下列預存程序當作查詢執行：`sp_configure 'clr enabled',1; reconfigure`

- 確認新的 SQL Server 可存取備份位置。 將資料庫移至新的伺服器之後，當您使用 UNC 儲存站台資料庫備份時，請確定新 SQL Server 的電腦帳戶具有 UNC 位置的**寫入** 權限。 此設定包含您移至 SQL Server AlwaysOn 可用性群組或 SQL Server 叢集的時機。

> [!IMPORTANT]
> 移動管理點有一或多個資料庫複本的資料庫時，請先移除資料庫複本。 完成資料庫移動後，就可以重新設定資料庫複本。 如需詳細資訊，請參閱[管理點的資料庫複本](../deploy/configure/database-replicas-for-management-points.md)。

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a> 管理站台資料庫伺服器的 SPN

您可以選擇執行該站台資料庫之 SQL 服務的帳戶：

- 使用電腦系統帳戶執行服務時，將會自動為您註冊服務主體名稱 (SPN)。

- 使用網域本機使用者帳戶執行服務時，請手動註冊 SPN。 SPN 可讓 SQL 用戶端與其他站台系統使用 Kerberos 進行驗證。 若無 Kerberos 驗證，與資料庫的通訊可能會失敗。

如需有關 SPN 與 Kerberos 連線的詳細資訊，請參閱[註冊 Kerberos 連線的服務主體名稱](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections)。

使用 **Setspn** 工具註冊站台資料庫伺服器的 SQL Server 服務帳戶 SPN。 在與 SQL Server 位於相同網域的電腦上，以網域系統管理員的身分執行 Setspn。

以下程序是如何管理 SQL Server 服務帳戶之 SPN 的範例。 如需有關 SetSPN 的詳細資訊，請參閱 [SetSPN 概觀](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\))。

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>手動建立 SQL Server 服務帳戶的網域使用者 SPN

1. 以系統管理員身分開啟命令提示字元。

1. 輸入有效的命令，以建立 NetBIOS 名稱與 FQDN 的 SPN：

    > [!IMPORTANT]
    > 建立叢集 SQL Server 的 SPN 時，請將 SQL Server 叢集的虛擬名稱指定為 SQL Server 電腦名稱。

    - NetBIOS 名稱：`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        例如：`setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN：`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        例如：`setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > 註冊 SQL Server 具名執行個體之 SPN 的命令，與您註冊預設執行個體之 SPN 時所使用的命令相同。 唯一的例外是，連接埠號碼必須與具名執行個體所使用的連接埠相符。

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>確認網域使用者 SPN 是否正確註冊

1. 以系統管理員身分開啟命令提示字元。

1. 輸入下列命令：`setspn -L <domain\SQL service account>`

    例如：`setspn -L contoso\sqlservice`

1. 檢閱已註冊的 **ServicePrincipalName**。 請確定您已為 SQL Server 建立有效的 SPN。

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>將 SQL Server 服務帳戶從本機系統變更至網域使用者帳戶

1. 建立或選取您要用作 SQL Server 服務帳戶的網域或本機系統使用者帳戶。

1. 開啟 [SQL Server 組態管理員]  。

1. 選取 [SQL Server 服務]  ，然後開啟 [SQL Server&lt;執行個體名稱\>]  。

1. 切換至 [登入]  索引標籤。選取 [此帳戶]  ，然後輸入步驟 1 中網域使用者帳戶的使用者名稱與密碼。

1. 確認服務帳戶變更，然後重新啟動 SQL Server 服務。

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a> 執行站台重設

當站台重設在 CAS 或主要站台執行時，此站台：

- 重新套用預設 Configuration Manager 檔案和登錄權限

- 重新所有站台元件與所有站台系統角色

次要站台不支援站台重設。

您可以手動重設站台。 這些也可以在您修改站台設定之後自動執行。 例如：

- 如果 Configuration Manager 元件所使用的帳戶有所變更，請考慮手動站台重設。 此動作可確保站台元件更新為使用新的帳戶詳細資料。

- 如果您修改站台上的用戶端或伺服器語言，Configuration Manager 會自動執行站台重設。 站台需要重設，才能使用新的語言。

> [!NOTE]
> 站台重設並不會重設非 Configuration Manager 物件的存取權限。

### <a name="what-happens-during-a-site-reset"></a>站台重設期間會發生什麼情況

當站台重設執行時：

1. 會停止安裝程式，並重新啟動 [SMS_SITE_COMPONENT_MANAGER]  服務與 [SMS_EXECUTIVE]  服務的執行緒元件。

1. 安裝程式會移除後再重新建立本機電腦與遠端站台系統電腦上的站台系統共用資料夾與 **SMS Executive** 元件。

1. 安裝程式會重新啟動 **SMS_SITE_COMPONENT_MANAGER** 服務，這會安裝 **SMS_EXECUTIVE** 與 **SMS_SQL_MONITOR** 服務。

站台重設會還原下列物件：

- [SMS]  或 [NAL]  登錄機碼，以及這些機碼下的任何預設子機碼。

- Configuration Manager 檔案目錄樹狀結構，以及此檔案目錄樹狀結構中的任何預設檔案或子目錄。

### <a name="prerequisites-for-site-reset"></a>站台重設的先決條件

您用來重設站台的帳戶必須具備下列權限：

- 重設 CAS：

  - CAS 伺服器的本機 [系統管理員] 

  - 相當於 [系統高權限管理員]  角色型系統管理安全性角色的權限

- 重設主要站台：

  - 主要站台伺服器的本機 [系統管理員] 

  - 相當於 [系統高權限管理員]  角色型系統管理安全性角色的權限
  
  - 如果主要站台位於 CAS 階層中，則此帳戶也必須是該 CAS 伺服器上的本機**系統管理員**。

### <a name="limitations-for-a-site-reset"></a>站台重設的限制

如果階層設定為支援[測試進入生產階段前集合中的用戶端升級](../../clients/manage/upgrade/test-client-upgrades.md)，您就無法使用站台重設來變更站台上的伺服器或用戶端語言套件。

### <a name="run-a-site-reset"></a>執行站台重設

1. 使用下列其中一種方法，在站台伺服器上啟動 Configuration Manager 安裝程式：

    - 在 [開始]  功能表上，選取 [Configuration Manager 安裝程式]  。

    - 在 Configuration Manager 的「安裝媒體」  目錄中，開啟 `\SMSSETUP\BIN\X64\setup.exe`。 請確定此版本與站台版本相同。

    - 在*安裝* Configuration Manager 的目錄中，開啟 `\BIN\X64\setup.exe`。

1. 在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台]  。

1. 在 [站台維護]  頁面上，選取 [在不變更設定的情況下重設站台]  。

1. 選取 [是]  以開始站台重設。

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a> 管理站台的語言套件

在站台安裝之後，您可以變更使用中的伺服器與用戶端語言套件。

### <a name="server-language-packs"></a>伺服器語言套件

適用於：*Configuration Manager 主控台安裝，適用站台系統角色的新安裝*

更新站台上的伺服器語言套件後，可以將語言套件支援新增至 Configuration Manager 主控台。

若要將伺服器語言套件的支援新增至 Configuration Manager 主控台，請從站台伺服器的 **ConsoleSetup** 資料夾 (其中包含您要使用的語言套件) 安裝 Configuration Manager 主控台。 如果已安裝 Configuration Manager 主控台，必須先解除安裝，新的安裝程式才能識別目前可支援的語言套件清單。

### <a name="client-language-packs"></a>用戶端語言套件

變更用戶端語言套件會更新用戶端安裝來源檔案。 新的用戶端安裝和升級會新增對用戶端語言更新清單的支援。

更新站台上的用戶端語言套件之後，使用包含用戶端語言套件的來源檔案安裝每個將使用這些語言套件的用戶端。

如需有關 Configuration Manager 所支援用戶端與伺服器語言的詳細資訊，請參閱[語言套件](../deploy/install/language-packs.md)。

### <a name="modify-the-supported-language-packs-at-a-site"></a>修改站台上支援的語言套件

1. 使用下列其中一種方法，在站台伺服器上啟動 Configuration Manager 安裝程式：

    - 在 [開始]  功能表上，選取 [Configuration Manager 安裝程式]  。

    - 在 Configuration Manager 的「安裝媒體」  目錄中，開啟 `\SMSSETUP\BIN\X64\setup.exe`。 請確定此版本與站台版本相同。

    - 在*安裝* Configuration Manager 的目錄中，開啟 `\BIN\X64\setup.exe`。

1. 在 [開始使用]  頁面上，選取 [執行站台維護或重設此站台]  。

1. 在 [站台維護]  頁面上，選取 [修改語言設定]  。

1. 在 [必要條件下載]  頁面上，選取下列其中一個選項：

    - **下載所需檔案**：取得語言套件的更新。

    - **使用先前下載的檔案**：使用先前下載的檔案，其中包含您要新增至站台的語言套件。

1. 在 [伺服器語言選擇]  頁面上，選取此站台支援的伺服器語言。

1. 在 [用戶端語言選擇]  頁面上，選取此站台支援的用戶端語言。

1. 完成精靈以修改站台上的語言支援。

    > [!NOTE]
    > Configuration Manager 會起始站台重設，同時重新安裝站台上的所有站台系統角色。

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a> 修改資料庫伺服器警示閾值

根據預設，Configuration Manager 會在站台資料庫伺服器的可用磁碟空間不足時產生警示：

- 可用磁碟空間為 10 GB 或以下時產生警告
- 可用磁碟空間為 5 GB 或以下時產生重大警示

您可以針對每個站台修改這些值或是停用警示：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。

1. 選取您要設定的站台。 在功能區中，選取 [內容]  。

1. 切換至 [警示]  索引標籤，然後編輯設定。

## <a name="uninstall-sites-and-hierarchies"></a>解除安裝站台和階層

您可能需要解除安裝 Configuration Manager 站台系統角色、站台或階層。 如需詳細資訊，請參閱[解除安裝角色、站台與階層](../deploy/install/uninstall-sites-and-hierarchies.md)。

從 2002 版開始，您也可以從階層移除 CAS，但保留主要站台。 如需詳細資訊，請參閱[移除 CAS](../deploy/install/remove-central-administration-site.md)。
