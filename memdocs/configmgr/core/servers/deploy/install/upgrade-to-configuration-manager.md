---
title: 升級至最新分支
titleSuffix: Configuration Manager
description: 了解從執行 System Center 2012 Configuration Manager 的站台和階層中執行成功就地升級的步驟。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700406"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>升級到 Configuration Manager 最新分支

適用於：  Configuration Manager (最新分支)

從執行 System Center 2012 Configuration Manager 的站台和階層中就地升級至 Configuration Manager 最新分支。 在從 System Center 2012 Configuration Manager 升級之前，您必須準備站台。 這個準備作業要求您移除可能導致無法成功升級的特定設定。 然後，當涉及多個站台時，請依照升級的順序。  

> [!TIP]  
> 管理 Configuration Manager 站台及階層基礎結構時，「升級」  、「更新」  及「安裝」  等詞彙是用來描述三種不同的概念。 若要了解如何使用每個詞彙，請參閱[關於升級、更新和安裝](../../../understand/upgrade-update-install.md)。

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a> 就地升級路徑  

下列選項是目前支援的就地升級路徑：

### <a name="upgrade-to-version-2002"></a>升級至 2002 版

您可將下列產品升級至 Configuration Manager 最新分支 2002 版的「完整授權」  版本：

- Configuration Manager 最新分支 2002 版的「評估版」  安裝
- System Center 2012 Configuration Manager (含 Service Pack 1)
- System Center 2012 Configuration Manager (含 Service Pack 2)
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager (含 Service Pack 1)

如需詳細資訊，請參閱 [Configuration Manager 分支和授權常見問題集](../../../understand/product-and-licensing-faq.md)。

> [!TIP]  
> 當從 System Center 2012 Configuration Manager 版本升級至最新分支時，可能可以簡化升級程序。 如需詳細資訊，請參閱下列各項：  
>
> - [基準和更新版本](../../manage/updates.md#bkmk_Baselines)  
> - [CD.Latest 資料夾](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>不支援的路徑

不支援下列路徑：

- 不支援將 Technical Preview 分支升級到完整授權安裝。 Technical Preview 版本只能升級至較新版的 Technical Preview。  

- 不支援從 Technical Preview 移轉至完整授權版本。  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> 升級檢查清單  

下列檢查清單可協助您規劃順利升級至 Configuration Manager。  

### <a name="before-you-upgrade"></a>升級之前  

在升級至 Configuration Manager 之前，請檢閱這些步驟。

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>檢閱您的 System Center 2012 Configuration Manager 環境

解決下列 Microsoft 支援文章中所述的問題：[由於週期性重試工作，Configuration Manager 用戶端會每隔五小時重新安裝，而且可能會導致意外的用戶端升級](https://support.microsoft.com/help/4018655)。

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>請確定您的環境符合支援的設定

- 檢閱用來裝載站台系統角色的伺服器 OS 版本：  

  - Configuration Manager 最新分支不支援 System Center 2012 Configuration Manager 支援的某些舊版作業系統。 在升級之前，請移除這些 OS 版本上的站台系統角色。 如需詳細資訊，請參閱[站台系統伺服器支援的作業系統](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)。

  - Configuration Manager 的先決條件檢查程式不會驗證站台伺服器或遠端站台系統上的站台系統角色先決條件  

- 請檢閱裝載站台系統角色之每部電腦的先決條件。 例如，為了部署 OS，Configuration Manager 使用 Windows 10 評定及部署套件 (Windows ADK)。 在執行安裝程式之前，您必須在站台伺服器和執行 SMS 提供者執行個體的每部電腦上，下載並安裝 Windows 10 ADK。  

如需支援的平台和先決條件設定的詳細資訊，請參閱[支援的設定](../../../plan-design/configs/supported-configurations.md)。  

如需搭配使用 Windows ADK 與 Configuration Manager 的資訊，請參閱 [OS 部署的基礎結構需求](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>檢閱站台和階層狀態，並確認沒有任何未解決的問題

在升級網站之前，請先針對網站伺服器、網站資料庫伺服器，以及安裝在遠端電腦上的網站系統角色，解決所有操作問題。 站台升級會因為現有的操作問題而失敗。  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>為裝載站台、站台資料庫伺服器及遠端站台系統角色之電腦上的作業系統，安裝全部適用的重大更新

在升級網站之前，為每個適用的網站系統安裝任何重大更新。 如果您安裝的更新需要重新啟動，請先重新啟動適用的電腦再開始進行 Service Pack 更新。  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>解除安裝 Configuration Manager 不支援的站台系統角色

Configuration Manager 中不再使用下列站台系統角色。 從 System Center 2012 Configuration Manager 升級之前，先將它們解除安裝：  

- 超出訊號範圍管理點  

- 系統健全狀況驗證程式點  

- 應用程式類別目錄網站點與 Web 服務點

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>在主要站台上停用管理點的資料庫複本

Configuration Manager 無法升級具有管理點之資料庫複本的主要站台。 在下列情況之前先停用資料庫複寫：  

- 建立站台資料庫的備份以測試資料庫升級  

- 將生產站台升級至 Configuration Manager 最新分支  

如需詳細資訊，請參閱下列文章：  

- System Center 2012 Configuration Manager：[設定管理點的資料庫複本](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager，最新分支：[管理點的資料庫複本](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>重新設定使用 NLB 的軟體更新點

Configuration Manager 無法升級使用網路負載平衡 (NLB) 叢集來裝載軟體更新點的站台。  

如果您將 NLB 叢集用於軟體更新點，請使用 PowerShell 移除 NLB 叢集。 (從 System Center 2012 Configuration Manager SP1 開始，Configuration Manager 主控台中沒有選項可以設定 NLB 叢集)。  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>停用站台升級期間各站台的所有站台維護工作

在您升級至 Configuration Manager 之前，請停用任何可能在進行升級程序期間執行的站台維護工作。 此清單包括但不限於下列工作：  

- 備份網站伺服器  
- 刪除過時用戶端操作  
- 刪除過時探索資料  

如果站台資料庫維護工作在升級期間執行，站台升級可能會失敗。  

在停用工作前，請將工作的排程記錄下來，以便在網站升級完成後您可以還原其設定。

如需站台維護工作的詳細資訊，請參閱下列文章：  

- System Center 2012 Configuration Manager：[規劃站台作業](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager，最新分支：[維護工作的參考](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>執行安裝程式先決條件檢查程式

在升級站台之前，請在安裝程式之外獨立執行 [必要條件檢查程式]  ，以驗證站台是否符合必要條件。 稍後，在升級站台之前，必要條件檢查程式會再次執行。  

此獨立必要條件檢查會評估站台，以升級到 Configuration Manager 的最新分支和長期維護分支 (LTSB)。 因為 LTSB 不支援某些功能，所以您可能會在 **ConfigMgrPrereq.log** 中看到與下列範例類似的項目：

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

如果您想要升級至最新分支，則可以放心略過 LTSB 版本的錯誤。 只有在您想要升級至 LTSB 時，它們才適用。

稍後，當執行 Configuration Manager 安裝程式以進行升級時，必要條件檢查會再次執行。 它會根據您選擇安裝的 Configuration Manager 分支 (最新分支或 LTSB) 評估您的站台。 如果您選擇升級至最新分支，則不會執行 LTSB 不支援之功能的檢查。

如需詳細資訊，請參閱[先決條件檢查程式](prerequisite-checker.md)和[先決條件檢查清單](list-of-prerequisite-checks.md)。  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>為 Configuration Manager 下載先決條件檔案和可轉散發檔案

使用**安裝程式下載程式**以下載必要的可轉散發檔案、語言套件以及 Configuration Manager 的最新產品更新。  

如需詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。  

#### <a name="plan-to-manage-server-and-client-languages"></a>規劃伺服器和用戶端語言的管理

當您升級站台時，站台升級只會安裝您在升級期間選取的語言組件版本。  

- 安裝程式會檢閱站台目前的語言設定。 然後它會在儲存先前所下載之先決條件檔案的資料夾中，識別可用的語言套件。  

- 然後，您就可以確認目前選取的伺服器和用戶端語言套件，或變更這些選擇以新增或移除語言的支援。  

- 只能選取執行安裝程式時可用的語言套件。  

> [!NOTE]  
> 您無法使用 System Center 2012 Configuration Manager 的語言套件，來啟用 Configuration Manager 最新分支站台的語言。  

如需有關語言套件的詳細資訊，請參閱[語言套件](language-packs.md)。  

#### <a name="review-considerations-for-site-upgrades"></a>檢閱站台升級的考慮事項

當您升級網站時，部分功能和設定會重設為預設設定。 為了幫助您準備這些及相關的變更，請參閱[升級時的考量](#bkmk_considerations)。  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>在管理中心網站和主要站台上建立站台資料庫的備份

在升級站台之前，請備份站台資料庫以確認您已成功備份，以供災害復原使用。  

如需詳細資訊，請參閱[備份和復原](../../manage/backup-and-recovery.md)。  

#### <a name="back-up-a-customized-configurationmof-file"></a>備份自訂的 configuration.mof 檔案

如果使用自訂的 configuration.mof 檔案來定義您搭配硬體清查使用的資料類別，則請建立此檔案的備份。 在升級之後，將這個檔案還原到您的站台。 如需詳細資訊，請參閱[如何擴充硬體清查](../../../clients/manage/inventory/extend-hardware-inventory.md)。  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>在最新站台資料庫備份的複本上測試資料庫升級程序

在升級 Configuration Manager 管理中心網站或主要站台之前，請先在站台資料庫複本上進行站台資料庫升級程序的測試。  

- 測試站台資料庫升級程序。 升級站台時，可能會修改站台資料庫。  

- 雖然測試資料庫升級並非必要，但是可以在您的生產資料庫受到影響之前找出升級問題  

- 站台資料庫升級失敗可能會造成站台資料庫無法運作，且可能需要站台復原才能恢復功能  

- 雖然站台資料庫在階層中的網站之間共用，您仍需要在升級該網站之前先規劃每個適用站台上的資料庫測試  

- 如果您在主要站台上使用管理點的資料庫複本，請在建立站台資料庫的備份之前停用複寫  

Configuration Manager 不支援次要站台的備份或次要站台資料庫的測試升級。  

不支援在生產站台資料庫上執行測試資料庫升級。 在網站資料庫上進行這類升級可能會造成網站無法運作。  

如需詳細資訊，請參閱 [測試站台資料庫升級](#bkmk_test)。  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>重新啟動站台伺服器以及每部裝載站台系統角色的電腦

執行此操作以確保最近安裝的更新或先決條件中沒有擱置動作。  

#### <a name="upgrade-sites"></a>升級站台

從階層中的頂層站台開始，從 Configuration Manager 來源媒體執行 Setup.exe。  

頂層站台完成升級之後，您就可以開始升級每個子站台。 請先完成每個網站的升級，再開始升級下一個網站。  

在階層中的所有站台都升級至 Configuration Manager 之前，您的階層仍會以混合的版本模式運作。  

如需如何執行升級的資訊，請參閱[升級站台](#bkmk_upgrade)。  

### <a name="after-you-upgrade"></a>升級之後  

在升級至 Configuration Manager 之後，請檢閱這些步驟。

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>升級獨立 Configuration Manager 主控台

當您升級管理中心網站或主要站台時，安裝預設也會升級已安裝在站台伺服器上的 Configuration Manager 主控台。 請手動升級在站台伺服器以外的電腦上安裝的每個主控台。  

> [!TIP]  
> 在您啟動升級之前，請關閉已開啟的主控台。  

如需詳細資訊，請參閱[安裝 Configuration Manager 主控台](install-consoles.md)。  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>在主要站台上重新設定管理點的資料庫複本

如果您在主要站台上使用管理點的資料庫複本，請先解除安裝資料庫複本，再升級站台。 升級主要網站後，請重新設定管理點的資料庫複本。

如需詳細資訊，請參閱[管理點的資料庫複本](../configure/database-replicas-for-management-points.md)。  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>重新設定您在升級前停用的任何資料庫維護工作

如果您在升級前已停用站台的資料庫[維護工作](../../manage/reference-for-maintenance-tasks.md)，請使用升級前相同的設定值重新設定站台的這些工作。  

#### <a name="upgrade-clients"></a>升級用戶端

所有站台都升級至 Configuration Manager 之後，規劃升級用戶端。  

升級用戶端時會解除安裝目前的用戶端軟體，並且安裝新版的用戶端軟體。 若要升級用戶端，可以使用 Configuration Manager 支援的任何方法。  

> [!TIP]  
> 將階層的頂層網站升級為新的 Service Pack 時，也會更新階層中每個發佈點上的用戶端安裝套件。 升級主要站台時，會同時更新該主要站台提供的用戶端升級套件。  

如需詳細資訊，請參閱[如何升級 Windows 電腦的用戶端](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a> 升級時的考量  

### <a name="automatic-actions"></a>自動動作

當您升級至 Configuration Manager 時，會自動執行下列動作：  

- 站台重設。 此動作包括重新安裝所有站台系統角色。  

- 如果該網站為階層的頂層網站，便會更新階層中每個發佈點的用戶端安裝套件。 站台也會更新預設開機映像以使用包含於 Windows 評定及部署套件 10 的新版 Windows PE。 不過，該升級不會升級與映像部署搭配使用的現有媒體。  

- 如果網站為主要網站，則會更新該網站的用戶端升級套件。  

### <a name="manual-actions-after-an-upgrade"></a>升級後的手動動作

升級站台之後，請確定您已執行下列動作：  

- 確定指派至每個主要站台的用戶端皆升級並安裝新用戶端版本  

- 升級連線至該站台及在站台伺服器遠端之電腦上執行的每個 Configuration Manager 主控台。  

- 在使用管理點資料庫複本的主要站台上，重新設定資料庫複本  

- 站台升級之後，手動升級 CD、DVD 或 USB 快閃磁碟機的 ISO 檔案等實體媒體。 它還包括提供給硬體廠商的預先設置的媒體。 站台更新可更新預設開機映像，但它無法升級這些媒體檔案，或是使用於 Configuration Manager 外部的裝置。  

- 當您不需要舊版 Windows PE 時，規劃更新自訂的開機映像。  

### <a name="actions-that-affect-configurations-and-settings"></a>影響設定和設定值的動作

當站台升級至 Configuration Manager 時，有些設定和設定值會在升級後消失。 某些設定會設定為新的預設值。 下列清單包括一些已不存在或變更的設定：  

- **軟體中心**  
    下列軟體中心項目會重設為預設值：  

  - [工作資訊]  的工作時間會從星期一到星期五 [上午 5:00]  重設為 [下午 10:00]  。  

  - [電腦維護]  的值會設為 [當電腦在簡報模式時暫停軟體中心活動]  。  

  - [遠端控制]  的值會設為指派至電腦之用戶端設定中的值。  

- **軟體更新摘要排程**：軟體更新或軟體更新群組的自訂摘要排程會重設為預設值 (1 小時)。 升級結束後，請將自訂摘要值重設為所需的頻率。  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> 測試站台資料庫升級  

只有在將 System Center 2012 Configuration Manager 這類舊版本升級到 Configuration Manager 最新分支時，下列資訊才適用。

請先測試要進行升級的站台資料庫複本，再升級該站台。  

若要測試要進行升級的資料庫，可先將站台資料庫的複本還原至未裝載 Configuration Manager 站台的 SQL Server 執行個體。 您用來裝載資料庫複本的 SQL Server 版本，必須與 Configuration Manager 所支援的 SQL Server 版本相同。  

在還原站台資料庫後，請在 SQL Server 電腦上，從 Configuration Manager 的來源媒體資料夾執行 Configuration Manager 安裝程式。 使用 `/TESTDBUPGRADE` 命令列選項。  

如需詳細資訊，請參閱下列文章：

- [備份 Configuration Manager 站台](../../manage/backup-and-recovery.md)  

- [安裝程式的命令列選項](command-line-options-for-setup.md#bkmk_setup)  

- [SQL Server 版本支援](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> 如果您整合 Microsoft Intune 與 Configuration Manager：  
>
> 當您在 5 天或更多天的站台資料庫複本上執行測試資料庫升級時，可能會收到下列訊息：  
>
> - 警告：升級會強制完整同步至雲端。  
> - ERROR：資料庫升級會強制完整同步至雲端。  
>
> 在資料庫升級測試期間，可以放心忽略這兩者。 它們不表示測試升級失敗或發生問題。 相反地，它們表示在實際升級期間，來自 **Cloud** 資料庫複寫群組的資料可能與 Microsoft Intune 同步處理。  

### <a name="test-a-site-database-for-upgrade"></a>測試要進行升級的站台資料庫  

在您規劃升級的各個管理中心網站和主要站台上使用下列程序：  

1. 製作站台資料庫複本。 然後將該複本還原到與您的站台資料庫所使用相同的版本，且未裝載 Configuration Manager 站台的 SQL Server 執行個體。 例如，若站台資料庫執行於 Enterprise Edition 的 SQL Server 執行個體上，請務必將資料庫還原到也是執行 Enterprise Edition 之 SQL Server 的 SQL Server 執行個體。  

2. 在您還原資料庫複本後，請從 Configuration Manager 最新分支的來源媒體執行安裝程式。 當您執行安裝程式時，請使用 `/TESTDBUPGRADE` 命令列選項。 如果裝載資料庫複本的 SQL Server 執行個體不是預設的執行個體，也請提供命令列引數，以識別裝載站台資料庫複本的執行個體。  

    例如，您想要升級資料庫名稱為 SMS_ABC 的站台資料庫。 您會將此站台資料庫的複本，還原到執行個體名稱為 DBTest 的受支援 SQL Server 執行個體。 若要測試此站台資料庫複本的升級，請使用下列命令列：`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup.exe 位於 Configuration Manager 來源媒體的下列位置：`SMSSETUP\BIN\X64`  

3. 在您執行資料庫升級測試的 SQL Server 執行個體上，監視位於系統磁碟機根目錄中的 ConfigMgrSetup.log 以了解進度及成功與否：  

    - 如果測試升級失敗，請解決與站台資料庫升級失敗相關的任何問題。 然後，建立新的站台資料庫備份，並測試新站台資料庫複本的升級。  

    - 順利進行所有程序後，便可以刪除資料庫複本。  

        > [!NOTE]  
        > 不支援還原您用於測試升級的站台資料庫複本，以當成任何站台上的站台資料庫使用。  

在您順利升級站台資料庫複本後，請繼續進行 Configuration Manager 站台及其站台資料庫的升級。  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a> 升級站台  

完成下列工作後，您就可以升級您的 Configuration Manager 站台：

- 適用於您站台的升級前的設定
- 在資料庫複本上測試站台資料庫升級
- 下載您計劃安裝之版本的先決條件檔案和語言套件

當您升級階層中的某個站台時，會先升級階層的頂層站台。 這個頂層站台可能是管理中心網站或獨立主要站台。 在您完成管理中心網站的升級後，您可以依所需的任何順序，升級子主要站台。 升級主要站台後，您可以升級該站台的子次要站台，或先升級其他主要站台再升級次要站台。  

若要升級管理中心網站或主要站台，請從 Configuration Manager 來源媒體執行安裝程式。 請不要執行安裝程式來升級次要站台。 您可以在完成主要父站台的升級後，改用 Configuration Manager 主控台升級次要站台。  

在升級站台之前，先關閉站台伺服器上的 Configuration Manager 主控台，直到完成站台升級。 同時，也請關閉非站台伺服器電腦上執行的每個 Configuration Manager 主控台。 您可以在站台升級完成後，讓主控台重新連線。 不過，在將 Configuration Manager 主控台升級至 Configuration Manager 新版本後，該主控台才可以顯示 Configuration Manager 新版本中可用的部分物件和資訊。  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>升級管理中心網站或主要站台  

1. 確認執行安裝程式的使用者具有以下安全性權限：  

    - 站台伺服器上的本機**系統管理員**權限  

    - 如果站台資料庫伺服器在站台伺服器遠端，則需要其本機**系統管理員**權限。  

2. 在站台伺服器上，開啟下列程式：`<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`。 此動作會開啟 Configuration Manager 安裝精靈。  

3. 閱讀 [開始之前]  頁面上的資訊，然後選取 [下一步]  。  

4. 在 [開始使用]  頁面上，選取 [升級此 Configuration Manager 站台]  ，然後選取 [下一步]  。  

5. 在 [產品金鑰]  頁面上：  

    如果您先前安裝了 Configuration Manager 評估版，則可以選取 [安裝此產品的許可版本]  。 然後輸入完整安裝 Configuration Manager 的產品金鑰。 此動作會將站台轉換為完整版。  

    您也可以指定授權合約的「軟體保證到期日」  ，以方便提醒您該日期。 如果您未在安裝期間輸入此值，則稍後可以從 Configuration Manager 主控台指定它。  

    > [!NOTE]  
    > Microsoft 不會驗證您輸入的到期日，亦不會將這個日期用於授權驗證。 您可以將它作為到期日的提醒。 Configuration Manager 會定期檢查線上提供的新軟體更新，因此您應該維持最新的軟體保證授權狀態，才能保有使用其他更新的資格。

    如需詳細資訊，請參閱[授權和分支](../../../understand/learn-more-editions.md)。

6. 在 [Microsoft 軟體授權條款]  頁面上，閱讀並接受授權條款，然後選取 [下一步]  。  

7. 在 [必要條件授權]  頁面上，閱讀並接受先決條件軟體的授權條款，然後選取 [下一步]  。 安裝程式會在需要時，於站台系統或用戶端上下載並自動安裝軟體。 在繼續下一頁之前，請同意所有條款。  

8. 在 [必要條件下載]  頁面上，指定安裝程式必須從網際網路下載最新內容，或使用先前下載的檔案。 此內容包含必要的可轉散發檔案、語言套件以及最新產品更新。 如果您先前使用安裝程式下載程式下載檔案，請選取 [使用先前下載的檔案]  並指定下載資料夾。 如需詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。  

    > [!NOTE]  
    > 當您使用先前下載的檔案時，請確認下載資料夾的路徑內含最新版的檔案。  

9. 在 [伺服器語言選擇]  頁面上，檢視站台目前安裝的語言清單。 選取此站台上可用於 Configuration Manager 主控台和報表的其他語言。 您也可以清除此後不想於此站台支援的語言。 預設會選取英文，且無法移除。  

    > [!IMPORTANT]  
    > 各版本的 Configuration Manager 皆無法使用舊版 Configuration Manager 的語言套件。 若要在您升級的 Configuration Manager 站台啟用語言支援，您必須使用該新版本的語言套件版本。 例如，從 System Center 2012 Configuration Manager 升級至 Configuration Manager 最新分支期間，如果下載的先決條件檔案中未含最新分支版本的語言套件，則您無法安裝該語言的支援檔案。  

10. 在 [用戶端語言選擇]  頁面上，檢視站台目前安裝的語言清單。 選取此站台上可供用戶端電腦使用的其他語言，或清除不想再於此站台支援的語言。 指定是否要針對行動裝置用戶端啟用所有用戶端語言，然後按 [下一步]  。 預設會選取英文，且無法移除。  

11. 在 [設定摘要]  頁面上檢閱設定。 當您準備好時，選取 [下一步]  來啟動 [先決條件檢查程式]，以確認站台升級的伺服器整備。  

12. 在 [必要條件安裝檢查]  頁面上，若沒有列出任何問題，請選取 [下一步]  升級站台及站台系統角色。

    若 [先決條件檢查程式] 找出問題，請選取清單上的某個項目，以了解如何解決問題的詳細資訊。 請先解決清單中具 [錯誤]  狀態的所有項目，再繼續執行安裝程式。 解決問題後，請按一下 [執行檢查]  以重新開始必要條件檢查。 您也可以開啟系統磁碟機根目錄中的 ConfigMgrPrereq.log 檔案，檢閱必要條件檢查工具的結果。 記錄檔可能包含未在使用者介面中顯示的其他資訊。 如需取得安裝的必要條件規則清單與說明，請參閱[必要條件檢查工具](list-of-prerequisite-checks.md)。

安裝程式會在 [升級]  頁面上顯示整體的進度狀態。 安裝程式完成核心網站伺服器與網站系統安裝時，您就可以關閉精靈。 網站設定會繼續在背景中進行。  

### <a name="upgrade-a-secondary-site"></a>升級次要站台  

1. 確認執行安裝程式的系統管理使用者具有以下安全性權限：  

    - 次要站台伺服器上的本機**系統管理員**權限  

    - 父主要站台上的 [基礎結構系統管理員]  或 [系統高權限管理員]  安全性角色  

    - 次要站台之站台資料庫上的系統管理員 (**SA**) 權限  

2. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

3. 選取您要升級的次要站台。 在功能區 [常用]  索引標籤上的 [站台]  群組中，選取 [升級]  。  

4. 選取 [是]  確認您的決定，並開始升級次要站台。  

次要站台升級會在背景執行。 完成升級後，請在 Configuration Manager 主控台中確認狀態。 選取次要站台伺服器，然後在功能區 [常用]  索引標籤的 [站台]  群組中，選取 [顯示安裝狀態]  。  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a> 升級後工作  

升級站台後，可能必須完成其他工作，才能完成升級或重新設定站台。 這些工作可包括下列項目：

- 升級 Configuration Manager 用戶端
- 升級 Configuration Manager 主控台
- 重新啟用管理點的資料庫複本
- 還原您所使用且升級後不會保留之 Configuration Manager 功能的設定  
