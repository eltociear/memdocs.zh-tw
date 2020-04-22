---
title: 設定命令列選項
titleSuffix: Configuration Manager
description: 建立自動化指令碼以從命令列安裝 Configuration Manager。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700816"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Configuration Manager 安裝程式的命令列選項

適用於：  Configuration Manager (最新分支)

使用下列資訊設定指令碼，或從命令列安裝 Configuration Manager。  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a> 安裝程式的命令列選項

請從站台伺服器上 Configuration Manager 安裝路徑的 `\BIN\X64` 目錄執行安裝程式。

### `/DEINSTALL`

解除安裝網站。 從站台伺服器電腦執行安裝程式。  

### `/DONTSTARTSITECOMP`

安裝站台，但防止站台元件管理員服務啟動。 在啟動站台元件管理員服務之前，網站不會作用。 站台元件管理員負責安裝與啟動 SMS_Executive 服務，以及站台的其他處理序。 在完成站台安裝後，當您啟動站台元件管理員服務時，便會安裝 SMS_Executive 服務以及其他站台運作所需的處理序。  

### `/HIDDEN`

在安裝期間隱藏使用者介面。 使用此選項只能搭配 **/SCRIPT** 選項。 自動安裝指令碼檔必須提供所有必要的選項，否則安裝程式會失敗。  

### `/NOUSERINPUT`

在安裝期間停用使用者輸入，但顯示安裝精靈。 使用此選項只能搭配 **/SCRIPT** 選項。 自動安裝指令碼檔必須提供所有必要的選項，否則安裝程式會失敗。  

### `/RESETSITE`

執行站台重設，這會重設站台的資料庫與服務帳戶。

如需詳細資訊，請參閱[執行站台重設](../../manage/modify-your-infrastructure.md#bkmk_reset)。  

### `/TESTDBUPGRADE`

在站台資料庫備份上執行測試以確定資料庫可以升級。

> [!IMPORTANT]  
> 請勿在生產站台資料庫上執行此命令列選項。 在生產站台資料庫執行此命令列選項會升級站台資料庫，並且可能會造成站台無法運作。

#### <a name="usage"></a>使用方式

請提供站台資料庫的執行個體名稱和資料庫名稱。 如果只指定資料庫名稱，安裝程式就會使用預設的執行個體名稱。  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

執行站台的自動升級。 指定產品金鑰，包括破折號 (`-`)。 此外，您也必須指定先前所下載安裝程式先決條件檔案的路徑。  

如需有關安裝程式必要條件檔案的詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。  

#### <a name="usage"></a>使用方式

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

執行自動安裝。 搭配此選項使用安裝程式初始化檔案。 如需有關如何自動執行安裝程式的詳細資訊，請參閱[使用命令列來安裝站台](use-a-command-line-to-install-sites.md)。  

#### <a name="usage"></a>使用方式

`/SCRIPT <setup script path>`

### `/SDKINST`

在指定的電腦上安裝 SMS 提供者。 請提供「SMS 提供者」電腦的完整網域名稱 (FQDN)。 如需有關「SMS 提供者」的詳細資訊，請參閱[為 SMS 提供者作規劃](../../../plan-design/hierarchy/plan-for-the-sms-provider.md)。  

#### <a name="usage"></a>使用方式

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

在指定的電腦上解除安裝 SMS 提供者。 請提供「SMS 提供者」電腦的 FQDN。  

#### <a name="usage"></a>使用方式

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

管理之前已安裝站台所安裝的語言。 請提供包含語言設定的語言指令碼檔位置。 如需詳細資訊，請參閱[用以管理語言的命令列選項](#bkmk_Lang)一節。  

#### <a name="usage"></a>使用方式

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> 用以管理語言的命令列選項

### <a name="identification"></a>識別

- **機碼名稱：** 動作  

    - **必要：** 是  

    - **值：** `ManageLanguages`  

    - **詳細資料:** 管理站台的伺服器、用戶端及行動用戶端語言支援。  

### <a name="options"></a>選項

- **機碼名稱：** AddServerLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定可用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的伺服器語言。 依預設使用英文版。  

- **機碼名稱：** AddClientLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定將可用於用戶端電腦的語言。 依預設使用英文版。  

- **機碼名稱：** DeleteServerLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定將移除且無法再用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的語言。 預設使用英文，且您無法將它無法移除。  

- **機碼名稱：** DeleteClientLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定將移除且無法再用於用戶端電腦的語言。 預設使用英文，且您無法將它無法移除。  

- **機碼名稱：** MobileDeviceLanguage  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝行動裝置用戶端語言。  

- **機碼名稱：** PrerequisiteComp  

    - **必要：** 是  

    - **值：**

        - `0` = 下載  

        - `1` = 已下載  

    - **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 `0` 值，安裝程式就會下載檔案。  

- **機碼名稱：** PrerequisitePath  

    - **必要：** 是  

    - **值：**  <*安裝程式必要條件檔案的路徑*>  

    - **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> 自動安裝程式指令碼檔索引鍵

請使用以下各節來協助您建立用於自動安裝的指令碼。 清單顯示：

- 可用的安裝指令碼機碼與其對應的值
- 它們是否為必要
- 它們用於哪種類型的安裝
- 機碼的簡短描述

### <a name="unattended-install-for-a-central-administration-site-cas"></a>管理中心網站 (CAS) 的自動安裝

使用下列詳細資料，透過使用自動安裝指令碼檔案來安裝 CAS。  

#### <a name="identification"></a>識別

- **機碼名稱：** 動作  

    - **必要：** 是  

    - **值：** `InstallCAS`  

    - **詳細資料:** 安裝 CAS。  

- **機碼名稱：** CDLatest  

    - **必要：** 是 (只有在使用來自 CD.Latest 資料夾的媒體時)。

    - **值：**

        - `1` = 您使用的是來自 CD.Latest 的媒體

        - 1 以外的任何值 = 您不是使用 CD.Latest 媒體

    - **詳細資料:** 當您安裝或復原主要站台或 CAS ，而且您從 CD.Latest 資料夾執行安裝程式時，請包括此機碼與值。 此值會通知安裝程式您正在使用來自 CD.Latest 的媒體。

#### <a name="options"></a>選項

- **機碼名稱：** ProductID  

    - **必要：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 含破折號的有效產品金鑰

        - `Eval` = 安裝 Configuration Manager 評估版

    - **詳細資料:** 指定 Configuration Manager 安裝產品金鑰，含破折號。

- **機碼名稱：** SiteCode  

    - **必要：** 是  

    - **值：**  <*站台碼*>，例如 `ABC`

    - **詳細資料:** 指定可唯一識別出階層中站台的三個英數字元。  

- **機碼名稱：** 站台名稱  

    - **必要：** 是  

    - **值：**  <站台名稱  >  

    - **詳細資料:** 指定此站台的名稱。  

- **機碼名稱：** SMSInstallDir  

    - **必要：** 是  

    - **值：**  <*Configuration Manager 安裝路徑*>  

    - **詳細資料:** 指定 Configuration Manager 程式檔案的安裝資料夾。  

- **機碼名稱：** SDKServer  

    - **必要：** 是  

    - **值：**  <*SMS 提供者 FQDN*>  

    - **詳細資料:** 指定將裝載 SMS 提供者的伺服器 FQDN。 您可以在初始安裝後設定站台的其他 SMS 提供者。  

- **機碼名稱：** PrerequisiteComp  

    - **必要：** 是  

    - **值：**

        - `0` = 下載  

        - `1` = 已下載  

    - **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 `0` 值，安裝程式就會下載檔案。  

- **機碼名稱：** PrerequisitePath  

    - **必要：** 是  

    - **值：**  <*安裝程式必要條件檔案的路徑*>  

    - **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。  

- **機碼名稱：** AdminConsole  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝 Configuration Manager 主控台。  

- **機碼名稱：** JoinCEIP  

    > [!Note]  
    > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

    - **必要：** 是  

    - **值：**

        - `0` = 不加入  

        - `1` = 加入  

    - **詳細資料:** 指定是否加入客戶經驗改進計畫 (CEIP)。  

- **機碼名稱：** AddServerLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定可用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的伺服器語言。 依預設使用英文版。  

- **機碼名稱：** AddClientLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定將可用於用戶端電腦的語言。 依預設使用英文版。  

- **機碼名稱：** DeleteServerLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 在安裝之後修改站台。 指定將移除且無法再用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的語言。 預設使用英文，且您無法將它無法移除。  

- **機碼名稱：** DeleteClientLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 在安裝之後修改站台。 指定將移除且無法再用於用戶端電腦的語言。 預設使用英文，且您無法將它無法移除。  

- **機碼名稱：** MobileDeviceLanguage  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝行動裝置用戶端語言。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **機碼名稱：** SQLServerName  

    - **必要：** 是  

    - **值︰**  <SQL Server 名稱  >  

    - **詳細資料:** 指定執行 SQL Server 以裝載站台資料庫之伺服器或叢集執行個體的名稱。  

- **機碼名稱：** DatabaseName  

    - **必要：** 是  

    - **值︰**  <*站台資料庫名稱*> 或 <*執行個體名稱*>\\<*站台資料庫名稱*>  

    - **詳細資料:** 指定要建立的 SQL Server 資料庫名稱，或安裝程式安裝 CAS 資料庫時所要使用的 SQL Server 資料庫名稱。  

        > [!IMPORTANT]  
        > 如果您未使用預設執行個體，就必須指定執行個體名稱與站台資料庫名稱。  

- **機碼名稱：** SQLSSBPort  

    - **必要：** 否  

    - **值︰**  <*SSB 連接埠號碼*>  

    - **詳細資料:** 指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 根據預設，SSB 會使用 TCP 連接埠 4022，但您可以使用不同的連接埠。  

- **機碼名稱：** SQLDataFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .mdb 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .mdb 檔案的替代位置。  

- **機碼名稱：** SQLLogFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .ldf 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .ldf 檔案的替代位置。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **機碼名稱：** CloudConnector  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否在這個站台安裝服務連接點。 因為您只能在階層的頂層站台安裝服務連接點，所以請將子主要站台的此值設定為 `1`。  

- **機碼名稱：** CloudConnectorServer  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值︰**  <*服務連接點伺服器 FQDN*>  

    - **詳細資料:** 指定將裝載服務連接點站台系統角色的伺服器 FQDN。  

- **機碼名稱：** UseProxy  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定服務連接點是否使用 Proxy 伺服器。  

- **機碼名稱：** ProxyName  

    - **必要：** **UseProxy** 等於 1 時為必要  

    - **值︰**  <*Proxy 伺服器 FQDN*>  

    - **詳細資料:** 指定服務連接點所使用 Proxy 伺服器的 FQDN。  

- **機碼名稱：** ProxyPort  

    - **必要：** **UseProxy** 等於 1 時為必要  

    - **值：**  <連接埠號碼  >  

    - **詳細資料:** 指定要用於 Proxy 連接埠的連接埠號碼。  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **機碼名稱：** SAActive

    - **必要：** 否

    - **值：**

        - `0` = 您沒有軟體保證

        - `1` = 軟體保證有效

    - **詳細資料:** 指定您是否有有效的軟體保證。 如需詳細資訊，請參閱[產品與授權常見問題集](../../../understand/product-and-licensing-faq.md)。

- **機碼名稱：** CurrentBranch

    - **必要：** 否

    - **值：**

        - `0` = 安裝 LTSB

        - `1` = 安裝最新分支

    - **詳細資料:** 指定要使用 Configuration Manager 最新分支或長期維護分支 (LTSB)。 如需詳細資訊，請參閱[我應該使用哪個 Configuration Manager 分支？](../../../understand/which-branch-should-i-use.md)。

### <a name="unattended-install-for-a-primary-site"></a>主要站台的自動安裝

請使用以下詳細資料，透過使用自動安裝指令碼檔來安裝主要站台。  

#### <a name="identification"></a>識別

- **機碼名稱：** 動作  

    - **必要：** 是  

    - **值：** `InstallPrimarySite`  

    - **詳細資料:** 安裝主要站台。  

- **機碼名稱：** CDLatest  

    - **必要：** 是 (只有在使用來自 CD.Latest 資料夾的媒體時)。

    - **值：**

        - `1` = 您使用的是來自 CD.Latest 的媒體

        - 1 以外的任何值 = 您不是使用 CD.Latest 媒體

    - **詳細資料:** 當您安裝或復原主要站台或 CAS ，而且您從 CD.Latest 資料夾執行安裝程式時，請包括此機碼與值。 此值會通知安裝程式您正在使用來自 CD.Latest 的媒體。

#### <a name="options"></a>選項

- **機碼名稱：** ProductID  

    - **必要：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 含破折號的有效產品金鑰

        - `Eval` = 安裝 Configuration Manager 評估版

    - **詳細資料:** 指定 Configuration Manager 安裝產品金鑰，含破折號。

- **機碼名稱：** SiteCode  

    - **必要：** 是  

    - **值：**  <站台碼  >  

    - **詳細資料:** 指定可唯一識別出階層中站台的三個英數字元。  

- **機碼名稱：** SiteName  

    - **必要：** 是  

    - **值：**  <站台名稱  >  

    - **詳細資料:** 指定此站台的名稱。  

- **機碼名稱：** SMSInstallDir  

    - **必要：** 是  

    - **值：**  <*Configuration Manager 安裝路徑*>

    - **詳細資料:** 指定 Configuration Manager 程式檔案的安裝資料夾。  

- **機碼名稱：** SDKServer  

    - **必要：** 是  

    - **值：**  <*SMS 提供者 FQDN*>  

    - **詳細資料:** 指定將裝載 SMS 提供者的伺服器 FQDN。 您可以在初始安裝後設定站台的其他 SMS 提供者。  

- **機碼名稱：** PrerequisiteComp  

    - **必要：** 是  

    - **值：**

        - `0` = 下載  

        - `1` = 已下載  

    - **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 `0` 值，安裝程式就會下載檔案。  

- **機碼名稱：** PrerequisitePath  

    - **必要：** 是  

    - **值：**  <*安裝程式必要條件檔案的路徑*>  

    - **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。  

- **機碼名稱：** AdminConsole  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝 Configuration Manager 主控台。  

- **機碼名稱：** JoinCEIP  

    > [!Note]  
    > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

    - **必要：** 是  

    - **值：**

        - `0` = 不加入  

        - `1` = 加入  

    - **詳細資料:** 指定是否加入 CEIP。  

- **機碼名稱：** ManagementPoint  

    - **必要：** 否  

    - **值：**  <管理點站台伺服器 FQDN  >  

    - **詳細資料:** 指定將作為管理點站台系統角色的伺服器的 FQDN。  

- **機碼名稱：** ManagementPointProtocol  

    - **必要：** 否  

    - **值：** `HTTPS` 或 `HTTP`  

    - **詳細資料:** 指定用於管理點的通訊協定。  

- **機碼名稱：** DistributionPoint  

    - **必要：** 否  

    - **值：**  <*發佈點站台伺服器 FQDN*>  

    - **詳細資料:** 指定將作為發佈點站台系統角色之伺服器的 FQDN。  

- **機碼名稱：** DistributionPointProtocol  

    - **必要：** 否  

    - **值：** `HTTPS` 或 `HTTP`  

    - **詳細資料:** 指定用於發佈點的通訊協定。  

- **機碼名稱：** RoleCommunicationProtocol  

    - **必要：** 是  

    - **值：** `EnforceHTTPS` 或 `HTTPorHTTPS`  

    - **詳細資料:** 指定要設定所有站台系統以僅接受來自用戶端的 HTTPS 通訊，或是要針對每個站台系統角色設定通訊方法。 選取 `EnforceHTTPS` 時，用戶端電腦必須具有用於用戶端驗證的有效公開金鑰基礎結構 (PKI) 憑證。  

- **機碼名稱：** ClientsUsePKICertificate  

    - **必要：** 是  

    - **值：**

        - `0` = 不使用  

        - `1` = 使用  

    - **詳細資料:** 指定用戶端是否使用用戶端 PKI 憑證以與站台系統角色通訊。  

- **機碼名稱：** AddServerLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定可用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的伺服器語言。 依預設使用英文版。  

- **機碼名稱：** AddClientLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 指定將可用於用戶端電腦的語言。 依預設使用英文版。  

- **機碼名稱：** DeleteServerLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 在安裝之後修改站台。 指定將移除且無法再用於 Configuration Manager 主控台、報告及 Configuration Manager 物件的語言。 預設使用英文，且您無法將它無法移除。  

- **機碼名稱：** DeleteClientLanguages  

    - **必要：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **詳細資料:** 在安裝之後修改站台。 指定將移除且無法再用於用戶端電腦的語言。 預設使用英文，且您無法將它無法移除。  

- **機碼名稱：** MobileDeviceLanguage  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝行動裝置用戶端語言。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **機碼名稱：** SQLServerName  

    - **必要：** 是  

    - **值︰**  <SQL Server 名稱  >  

    - **詳細資料:** 指定執行 SQL Server 以裝載站台資料庫之伺服器或叢集執行個體的名稱。  

- **機碼名稱：** DatabaseName  

    - **必要：** 是  

    - **值︰**  <*站台資料庫名稱*> 或 <*執行個體名稱*>\\<*站台資料庫名稱*>  

    - **詳細資料:** 指定要建立的 SQL Server 資料庫名稱，或用來安裝主要站台資料庫的 SQL Server 資料庫名稱。  

        > [!IMPORTANT]  
        > 如果您未使用預設執行個體，就必須指定執行個體名稱與站台資料庫名稱。  

- **機碼名稱：** SQLSSBPort  

    - **必要：** 否  

    - **值︰**  <*SSB 連接埠號碼*>  

    - **詳細資料:** 指定 SQL Server 所使用的 SSB 連接埠。 根據預設，SSB 會使用 TCP 連接埠 4022，但您可以使用不同的連接埠。  

- **機碼名稱：** SQLDataFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .mdb 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .mdb 檔案的替代位置。  

- **機碼名稱：** SQLLogFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .ldf 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .ldf 檔案的替代位置。  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **機碼名稱：** CCARSiteServer  

    - **必要：** 否  

    - **值：**  <*管理中心網站 FQDN*>  

    - **詳細資料:** 指定主要站台在加入 Configuration Manager 階層時要連結的 CAS。 在安裝期間指定 CAS。  

- **機碼名稱：** CASRetryInterval  

    - **必要：** 否  

    - **值：**  <*以分鐘為單位的間隔時間*>  

    - **詳細資料:** 指定連線失敗後，嘗試連線至 CAS 的重試間隔 (單位為分鐘)。 例如，如果與 CAS 的連線失敗，主要站台會等待您為 **CASRetryInterval** 值指定的分鐘數，然後重試連線。  

- **機碼名稱：** WaitForCASTimeout  

    - **必要：** 否  

    - **值：**  <*以分鐘表示的逾時 (0 到 100)* >  

    - **詳細資料:** 指定主要站台連線至 CAS 的逾時上限值 (單位分鐘)。 例如，如果主要站台連線至 CAS 失敗，則主要站台會依據 **CASRetryInterval** 值重試與 CAS 的連線，直到達到 **WaitForCASTimeout** 期間。 您可以指定介於 `0` 到 `100` 之間的值。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **機碼名稱：** CloudConnector  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否在這個站台安裝服務連接點。 因為您只能在階層的頂層站台安裝服務連接點，所以請將子主要站台的此值設定為 `0`。  

- **機碼名稱：** CloudConnectorServer  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值︰**  <*服務連接點伺服器 FQDN*\>  

    - **詳細資料:** 指定將裝載服務連接點站台系統角色的伺服器 FQDN。  

- **機碼名稱：** UseProxy  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定服務連接點是否使用 Proxy 伺服器。  

- **機碼名稱：** ProxyName  

    - **必要：** **UseProxy** 等於 1 時為必要  

    - **值︰**  <*Proxy 伺服器 FQDN*>  

    - **詳細資料:** 指定服務連接點所使用 Proxy 伺服器的 FQDN。  

- **機碼名稱：** ProxyPort  

    - **必要：** **UseProxy** 等於 1 時為必要  

    - **值：**  <連接埠號碼  >  

    - **詳細資料:** 指定要用於 Proxy 連接埠的連接埠號碼。  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **機碼名稱：** SAActive

    - **必要：** 否

    - **值：**

        - `0` = 您沒有軟體保證

        - `1` = 軟體保證有效

    - **詳細資料:** 指定您是否有有效的軟體保證。 如需詳細資訊，請參閱[產品與授權常見問題集](../../../understand/product-and-licensing-faq.md)。

- **機碼名稱：** CurrentBranch

    - **必要：** 否

    - **值：**

        - `0` = 安裝 LTSB

        - `1` = 安裝最新分支

    - **詳細資料:** 指定要使用 Configuration Manager 最新分支或長期維護分支 (LTSB)。 如需詳細資訊，請參閱[我應該使用哪個 Configuration Manager 分支？](../../../understand/which-branch-should-i-use.md)。

### <a name="unattended-recovery-for-a-cas"></a>CAS 的自動復原

使用下列詳細資料，透過使用自動安裝指令碼檔案來復原 CAS。  

#### <a name="identification"></a>識別

- **機碼名稱：** 動作  

    - **必要：** 是  

    - **值：** `RecoverCCAR`  

    - **詳細資料:** 復原 CAS。  

- **機碼名稱：** CDLatest  

    - **必要：** 是 (只有在使用來自 CD.Latest 資料夾的媒體時)。

    - **值：**

        - `1` = 您使用的是來自 CD.Latest 的媒體

        - 1 以外的任何值 = 您不是使用 CD.Latest 媒體

    - **詳細資料:** 當您安裝或復原主要站台或 CAS ，而且您從 CD.Latest 資料夾執行安裝程式時，請包括此機碼與值。 此值會通知安裝程式您正在使用來自 CD.Latest 的媒體。

#### <a name="recoveryoptions"></a>RecoveryOptions

- **機碼名稱：** ServerRecoveryOptions  

    - **必要：** 是  

    - **值：**

        - `1` = 復原站台伺服器和 SQL Server

        - `2` = 僅復原站台伺服器

        - `4` = 僅復原 SQL Server  

    - **詳細資料:** 指定安裝程式是要復原站台伺服器、SQL Server，還是同時復原兩者。 根據指定的值，也必須要有下列選項：  

        - **1** 或 **2**：若要使用站台備份來復原站台，請為 **SiteServerBackupLocation** 指定值。 若沒有指定值，安裝程式會重新安裝站台，而不會從備份組還原它。  

        - **4**：將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。  

- **機碼名稱：** DatabaseRecoveryOptions  

    - **必要：** **ServerRecoveryOptions** 設定值為 **1** 或 **4**時，需要此索引鍵。  

    - **值：**

        - `10` = 從備份還原站台資料庫。  

        - `20` = 使用以另一種方式手動復原的站台資料庫。  

        - `40` = 為站台建立新的資料庫。 若無可用站台資料庫備份，請使用此選項。 站台會透過來自其他站台的複寫來復原全域與站台資料。  

        - `80` = 略過資料庫復原。  

    - **詳細資料:** 指定安裝程式如何復原 SQL Server 中的站台資料庫。  

- **機碼名稱：** ReferenceSite  

    - **必要：** **DatabaseRecoveryOptions** 設定值為 **40**時，需要此索引鍵。  

    - **值︰**  <參照站台 FQDN  >  

    - **詳細資料:** 若資料庫備份比變更追蹤保留期間還舊，或未使用備份復原站台，請指定 CAS 用來復原全域資料的參照主要站台。  

        若沒有指定參照站台，且備份又比變更追蹤保留期間還舊，所有主要站台都會以來自 CAS 的已還原資料重新初始化。  

        若您並未指定參照站台，且備份是在變更追蹤保留期間內，則只會從主要站台複寫備份後的變更。 若不同主要站台間的變更發生衝突，則 CAS 會使用第一個收到的變更。  

- **機碼名稱：** SiteServerBackupLocation  

    - **必要：** 否  

    - **值︰**  <*站台伺服器備份組的路徑*>  

    - **詳細資料:** 指定網站伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2** 時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，安裝程式會重新安裝站台，而不會從備份組還原它。  

- **機碼名稱：** BackupLocation  

    - **必要：** 當您將 **ServerRecoveryOptions** 索引鍵的值設定為 **1** 或 **4**，並將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，需要此索引鍵。  

    - **值︰**  <站台資料庫備份組的路徑  >  

    - **詳細資料:** 指定站台資料庫備份組的路徑。  

#### <a name="options"></a>選項

- **機碼名稱：** ProductID  

    - **必要：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 含破折號的有效產品金鑰

        - `Eval` = 安裝 Configuration Manager 評估版

    - **詳細資料:** 指定 Configuration Manager 安裝產品金鑰，含破折號。

- **機碼名稱：** SiteCode  

    - **必要：** 是  

    - **值：**  <站台碼  >  

    - **詳細資料:** 指定可唯一識別出階層中站台的三個英數字元。 請指定失敗前站台所使用的站台碼。

- **機碼名稱：** SiteName  

    - **必要：** 否  

    - **值：**  <站台名稱  >  

    - **詳細資料:** 指定此站台的名稱。  

- **機碼名稱：** SMSInstallDir  

    - **必要：** 是  

    - **值：**  <*Configuration Manager 安裝路徑*>  

    - **詳細資料:** 指定 Configuration Manager 程式檔案的安裝資料夾。  

- **機碼名稱：** SDKServer  

    - **必要：** 是  

    - **值：**  <*SMS 提供者 FQDN*>  

    - **詳細資料:** 指定裝載「SMS 提供者」的伺服器 FQDN。 指定失敗前裝載「SMS 提供者」的伺服器。  

        在初始安裝之後，您可以設定站台的其他 SMS 提供者。 如需有關「SMS 提供者」的詳細資訊，請參閱[為 SMS 提供者作規劃](../../../plan-design/hierarchy/plan-for-the-sms-provider.md)。  

- **機碼名稱：** PrerequisiteComp  

    - **必要：** 是  

    - **值：**

        - `0` = 下載  

        - `1` = 已下載  

    - **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 **0** 值，安裝程式就會下載檔案。  

- **機碼名稱：** PrerequisitePath  

    - **必要：** 是  

    - **值：**  <*安裝程式必要條件檔案的路徑*>  

    - **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。  

- **機碼名稱：** AdminConsole  

    - **必要：** 此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝 Configuration Manager 主控台。  

- **機碼名稱：** JoinCEIP  

    > [!Note]  
    > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

    - **必要：** 是  

    - **值：**

        - `0` = 不加入  

        - `1` = 加入  

    - **詳細資料:** 指定是否加入 CEIP。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **機碼名稱：** SQLServerName  

    - **必要：** 是  

    - **值︰**  <SQL Server 名稱  >  

    - **詳細資料:** 指定執行 SQL Server 且裝載站台資料庫的伺服器或叢集執行個體名稱。 請指定失敗前裝載站台資料庫的相同伺服器。  

- **機碼名稱：** DatabaseName  

    - **必要：** 是  

    - **值︰**  <*站台資料庫名稱*> 或 <*執行個體名稱*>\\<*站台資料庫名稱*>  

    - **詳細資料:** 指定要建立的 SQL Server 資料庫名稱，或安裝 CAS 資料庫時要使用的 SQL Server 資料庫名稱。 請指定失敗前所使用的相同資料庫名稱。  

        > [!IMPORTANT]  
        > 如果您未使用預設執行個體，就必須指定執行個體名稱與站台資料庫名稱。  

- **機碼名稱：** SQLSSBPort  

    - **必要：** 是  

    - **值︰**  <*SSB 連接埠號碼*>  

    - **詳細資料:** 指定 SQL Server 所使用的 SSB 連接埠。 根據預設，SSB 會使用 TCP 連接埠 4022。 請指定失敗前所使用的相同 SSB 連接埠。  

- **機碼名稱：** SQLDataFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .mdb 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .mdb 檔案的替代位置。  

- **機碼名稱：** SQLLogFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .ldf 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .ldf 檔案的替代位置。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **機碼名稱：** CloudConnector  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否在這個站台安裝服務連接點。 因為您只能在階層的頂層站台安裝服務連接點，所以子主要站台的此值必須設定為 **0**。  

- **機碼名稱：** CloudConnectorServer  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值︰**  <*服務連接點伺服器 FQDN*>  

    - **詳細資料:** 指定將裝載服務連接點站台系統角色的伺服器 FQDN。  

- **機碼名稱：** UseProxy  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定服務連接點是否使用 Proxy 伺服器。  

- **機碼名稱：** ProxyName  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值︰**  <*Proxy 伺服器 FQDN*>  

    - **詳細資料:** 指定服務連接點所使用 Proxy 伺服器的 FQDN。  

- **機碼名稱：** ProxyPort  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值：**  <連接埠號碼  >  

    - **詳細資料:** 指定要用於 Proxy 連接埠的連接埠號碼。  

### <a name="unattended-recovery-for-a-primary-site"></a>主要站台的自動復原

請使用以下詳細資料，透過使用自動安裝指令碼檔來復原主要站台。  

#### <a name="identification"></a>識別

- **機碼名稱：** 動作  

    - **必要：** 是  

    - **值：** `RecoverPrimarySite`  

    - **詳細資料:** 復原主要站台。  

- **機碼名稱：** CDLatest  

    - **必要：** 是 (只有在使用來自 CD.Latest 資料夾的媒體時)。

    - **值：**

        - `1` = 您使用的是來自 CD.Latest 的媒體

        - 1 以外的任何值 = 您不是使用 CD.Latest 媒體

    - **詳細資料:** 當您安裝或復原主要站台或 CAS ，而且您從 CD.Latest 資料夾執行安裝程式時，請包括此機碼與值。 此值會通知安裝程式您正在使用來自 CD.Latest 的媒體。

#### <a name="recoveryoptions"></a>RecoveryOptions

- **機碼名稱：** ServerRecoveryOptions  

    - **必要：** 是  

    - **值：**

        - `1` = 復原站台伺服器和 SQL Server

        - `2` = 僅復原站台伺服器

        - `4` = 僅復原 SQL Server  

    - **詳細資料:** 指定安裝程式是要復原站台伺服器、SQL Server，還是同時復原兩者。 根據指定的值，也必須要有下列選項：  

        - **1** 或 **2**：若要使用站台備份來復原站台，請為 **SiteServerBackupLocation** 指定值。 若沒有指定值，安裝程式會重新安裝站台，而不會從備份組還原它。  

        - **4**：將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。  

- **機碼名稱：** DatabaseRecoveryOptions  

    - **必要：** **ServerRecoveryOptions** 設定值為 **1** 或 **4**時，需要此索引鍵。  

    - **值：**

        - `10` = 從備份還原站台資料庫。  

        - `20` = 使用以另一種方式手動復原的站台資料庫。  

        - `40` = 為站台建立新的資料庫。 若無可用站台資料庫備份，請使用此選項。 站台會透過來自其他站台的複寫來復原全域與站台資料。  

        - `80` = 略過資料庫復原。  

    - **詳細資料:** 指定安裝程式如何復原 SQL Server 中的站台資料庫。  

- **機碼名稱：** SiteServerBackupLocation  

    - **必要：** 否  

    - **值︰**  <*站台伺服器備份組的路徑*>  

    - **詳細資料:** 指定網站伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2** 時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，安裝程式會重新安裝站台，而不會從備份組還原它。  

- **機碼名稱：** BackupLocation  

    - **必要：** 當您將 **ServerRecoveryOptions** 索引鍵的值設定為 **1** 或 **4**，並將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，需要此索引鍵。  

    - **值︰**  <站台資料庫備份組的路徑  >  

    - **詳細資料:** 指定站台資料庫備份組的路徑。  

#### <a name="options"></a>選項

- **機碼名稱：** ProductID  

    - **必要：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 含破折號的有效產品金鑰

        - `Eval` = 安裝 Configuration Manager 評估版

    - **詳細資料:** 指定 Configuration Manager 安裝產品金鑰，含破折號。

- **機碼名稱：** SiteCode  

    - **必要：** 是  

    - **值：**  <站台碼  >  

    - **詳細資料:** 指定可唯一識別出階層中站台的三個英數字元。 請指定失敗前站台所使用的站台碼。

- **機碼名稱：** SiteName  

    - **必要：** 否  

    - **值：**  <站台名稱  >  

    - **詳細資料:** 指定此站台的名稱。  

- **機碼名稱：** SMSInstallDir  

    - **必要：** 是  

    - **值：**  <*Configuration Manager 安裝路徑*>  

    - **詳細資料:** 指定 Configuration Manager 程式檔案的安裝資料夾。  

- **機碼名稱：** SDKServer  

    - **必要：** 是  

    - **值：**  <*SMS 提供者 FQDN*>  

    - **詳細資料:** 指定裝載「SMS 提供者」的伺服器 FQDN。 指定失敗前裝載「SMS 提供者」的伺服器。 在初始安裝之後，您可以設定站台的其他 SMS 提供者。 如需有關「SMS 提供者」的詳細資訊，請參閱[為 SMS 提供者作規劃](../../../plan-design/hierarchy/plan-for-the-sms-provider.md)。  

- **機碼名稱：** PrerequisiteComp  

    - **必要：** 是  

    - **值：**

        - `0` = 下載  

        - `1` = 已下載  

    - **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 **0** 值，安裝程式就會下載檔案。  

- **機碼名稱：** PrerequisitePath  

    - **必要：** 是  

    - **值：**  <*安裝程式必要條件檔案的路徑*>  

    - **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。  

- **機碼名稱：** AdminConsole  

    - **必要：** 此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否安裝 Configuration Manager 主控台。  

- **機碼名稱：** JoinCEIP  

    > [!Note]  
    > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

    - **必要：** 是  

    - **值：**

        - `0` = 不加入  

        - `1` = 加入  

    - **詳細資料:** 指定是否加入 CEIP。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **機碼名稱：** SQLServerName  

    - **必要：** 是  

    - **值︰**  <SQL Server 名稱  >  

    - **詳細資料:** 指定執行 SQL Server 以裝載站台資料庫之伺服器或叢集執行個體的名稱。 請指定失敗前裝載站台資料庫的相同伺服器。  

- **機碼名稱：** DatabaseName  

    - **必要：** 是  

    - **值︰**  <*站台資料庫名稱*> 或 <*執行個體名稱*>\\<*站台資料庫名稱*>

    - **詳細資料:** 指定要建立的 SQL Server 資料庫名稱，或安裝 CAS 資料庫時要使用的 SQL Server 資料庫名稱。 請指定失敗前所使用的相同資料庫名稱。  

        > [!IMPORTANT]  
        > 如果您未使用預設執行個體，就必須指定執行個體名稱與站台資料庫名稱。  

- **機碼名稱：** SQLSSBPort  

    - **必要：** 是  

    - **值︰**  <*SSB 連接埠號碼*>  

    - **詳細資料:** 指定 SQL Server 所使用的 SSB 連接埠。 根據預設，SSB 會使用 TCP 連接埠 4022。 請指定失敗前所使用的相同 SSB 連接埠。  

- **機碼名稱：** SQLDataFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .mdb 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .mdb 檔案的替代位置。  

- **機碼名稱：** SQLLogFilePath  

    - **必要：** 否  

    - **值︰**  <*資料庫 .ldf 檔案的路徑*>  

    - **詳細資料:** 指定建立資料庫 .ldf 檔案的替代位置。  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **機碼名稱：** CCARSiteServer  

    - **必要：** 查看詳細資料。  

    - **值：**  <*CAS 的站台碼*>  

    - **詳細資料:** 指定主要站台在加入 Configuration Manager 階層時要連結的 CAS。 如果主要網站在失敗前連結至 CAS，則此設定為必要。 指定失敗前用於 CAS 的站台碼。  

- **機碼名稱：** CASRetryInterval  

    - **必要：** 否  

    - **值：**  <*以分鐘為單位的間隔時間*>  

    - **詳細資料:** 指定連線失敗後，嘗試連線至 CAS 的重試間隔 (單位為分鐘)。 例如，如果與 CAS 的連線失敗，主要站台會等待您為 **CASRetryInterval** 值指定的分鐘數，然後重試連線。  

- **機碼名稱：** WaitForCASTimeout  

    - **必要：** 否  

    - **值：**  <*以分鐘表示的逾時*>  

    - **詳細資料:** 指定主要站台連線至 CAS 的逾時上限值 (單位分鐘)。 例如，如果主要站台連線至 CAS 失敗，則主要站台會依據 **CASRetryInterval** 值重試與 CAS 的連線，直到達到 **WaitForCASTimeout** 期間。 您可以指定介於 `0` 到 `100` 之間的值。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **機碼名稱：** CloudConnector  

    - **必要：** 是  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定是否在這個站台安裝服務連接點。 因為您只能在階層的頂層站台安裝服務連接點，所以子主要站台的此值必須設定為 `0`。  

- **機碼名稱：** CloudConnectorServer  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值︰**  <*服務連接點伺服器 FQDN*>  

    - **詳細資料:** 指定將裝載服務連接點站台系統角色的伺服器 FQDN。  

- **機碼名稱：** UseProxy  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值：**

        - `0` = 不要安裝  

        - `1` = 安裝  

    - **詳細資料:** 指定服務連接點是否使用 Proxy 伺服器。  

- **機碼名稱：** ProxyName  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值︰**  <*Proxy 伺服器 FQDN*>  

    - **詳細資料:** 指定服務連接點所使用 Proxy 伺服器的 FQDN。  

- **機碼名稱：** ProxyPort  

    - **必要：** **CloudConnector** 等於 1 時為必要  

    - **值：**  <連接埠號碼  >  

    - **詳細資料:** 指定要用於 Proxy 連接埠的連接埠號碼。  
