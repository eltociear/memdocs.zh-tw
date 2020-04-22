---
title: 自動復原
titleSuffix: Configuration Manager
description: 使用指令碼在 Configuration Manager 中復原站台。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704396"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Configuration Manager 的自動站台復原   

適用於：  Configuration Manager (最新分支)

 若要執行 Configuration Manager 管理中心網站或主要站台的[自動復原](recover-sites.md#site-recovery-procedures)，您可以建立自動安裝指令碼，然後使用安裝程式搭配 **/script** 命令選項。 指令碼提供與安裝精靈提示相同的資訊類型，不過沒有預設設定。 所有值必須針對適用於您所使用之復原類型的安裝識別碼進行指定。

 若要使用 /script 安裝命令列選項，您必須建立初始設定檔案。 然後，在 /script 選項之後指定此檔案名稱。 檔案名稱並不重要，只要檔案名稱的副檔名為 **.ini** 即可。 當您參照來自命令列的安裝初始設定檔案時，您必須提供檔案的完整路徑。 例如，若您將安裝程式初始化檔案命名為 *setup.ini*，並儲存於 *C:\setup* 資料夾，則命令列為：

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  您必須具有系統管理員權限才能執行安裝程式。 使用自動指令碼執行安裝程式時，請使用 [以系統管理員身分執行]  ，在 [系統管理員] 內容中啟動 [命令提示字元]。

 指令碼包含區段名稱、索引鍵名稱與值。 根據您進行指令碼處理時的復原類型，所需的區段索引鍵名稱也不同。 區段中索引鍵的順序與檔案內區段的順序都不重要。 索引鍵不區分大小寫。 提供索引鍵的值時，索引鍵名稱後必須加上等號 (=) 與索引鍵的值。

 使用以下區段來協助您建立自動網站復原的指令碼。 下表列出可用的安裝指令碼索引鍵、其對應的值、是否為必要、用於何種安裝類型，以及該索引鍵的簡單說明。

## <a name="recover-a-central-administration-site-unattended"></a>自動復原管理中心網站
 使用下列資訊設定自動安裝指令碼檔案來復原管理中心網站。

 **識別**

-   **機碼名稱：** 動作

    -   **必要：** 是
    -   **值：** RecoverCCAR
    -   **詳細資料:** 復原管理中心網站


-   **機碼名稱：** CDLatest

    -   **必要：** 是 (只有在使用來自 CD.Latest 資料夾的媒體時)。
    -   **值：** 1 (1 以外的任何值都會被視為不使用 CD.Latest)。
    -   **詳細資料:** 當您從 CD.Latest 資料夾中的媒體執行安裝程式，以安裝主要站台或管理中心網站，或是復原主要站台或管理中心網站時，您的指令碼必須包含此機碼和值。 這個值會通知安裝程式目前正在使用來自 CD.Latest 的媒體。

**RecoveryOptions**   
-   **機碼名稱：** ServerRecoveryOptions   

    -   **必要：** 是
    -   **值：** 1、2 或 4  
         1 = 復原網站伺服器和 SQL Server。   
         2 = 僅復原網站伺服器。  
         4 = 僅復原 SQL Server。
    -   **詳細資料:** 指定安裝程式是要復原站台伺服器、SQL Server，還是同時復原兩者。 針對 ServerRecoveryOptions 設定以下值時，需要關聯的索引鍵：  
        -   **值 = 1** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。

             將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。

        -   **值 = 2** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。

        -   **值 = 4** 將 **BackupLocation** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。

-   **機碼名稱：** DatabaseRecoveryOptions

    -   **必要：** 可能
    -   **值：**   
         - **10** = 從備份還原站台資料庫。  
         - **20** = 使用以另一種方式手動復原的站台資料庫。   
         - **40** = 為網站建立新的資料庫。 若無可用網站資料庫備份，請使用此選項。 透過從其他網站複寫來復原全域和網站資料。  
         - **80** = 略過資料庫復原。
    -   **詳細資料:** 指定安裝程式如何復原 SQL Server 中的站台資料庫。 **ServerRecoveryOptions** 設定值為 **1** 或 **4**時，需要此索引鍵。


-   **機碼名稱：** ReferenceSite  

    -   **必要：** 可能
    -   **值：** &lt;ReferenceSiteFQDN\>
    -   **詳細資料:** 指定參照主要站台。 若資料庫備份比變更追蹤保留期間還舊，或不使用備份復原網站時，管理中心網站會使用參照站台復原全域資料。

         若沒有指定參考站台，且備份又比變更追蹤保留期間還舊，所有主要站台都會以來自管理中心網站的還原資料重新初始化。

         若您並未指定參考站台，且備份是在變更追蹤保留期間內，則只會從主要站台複寫備份後的變更。 若不同主要網站間的變更發生衝突，則管理中心網站會使用第一個收到的變更。

         **DatabaseRecoveryOptions** 設定值為 **40**時，需要此索引鍵。

-   **機碼名稱：** SiteServerBackupLocation

    -   **必要：** 否
    -   **值：** &lt;PathToSiteServerBackupSet\>
    -   **詳細資料:** 指定網站伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2** 時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。


-   **機碼名稱：** BackupLocation

    -   **必要：** 可能
    -   **值：** &lt;PathToSiteDatabaseBackupSet\>
    -   **詳細資料:** 指定站台資料庫備份組的路徑。 **ServerRecoveryOptions** 索引鍵的設定值為 **1** 或 **4** ，且 **DatabaseRecoveryOptions** 索引鍵的設定值為 **10** 時，需要 **BackupLocation** 索引鍵。


**選項**

- **機碼名稱：** ProductID
  -   **必要：** 是
  -   **值：**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - 評估版
  -   **詳細資料:** Configuration Manager 安裝產品金鑰 (包括破折號)。 輸入 **Eval** 可安裝 Configuration Manager 的評估版。  


- **機碼名稱：** SiteCode

  -   **必要：** 是
  -   **值：** &lt;站台碼\>
  -   **詳細資料:** 可在階層中唯一識別站台的三個英數字元。 指定失敗前網站所使用的站台碼。


- **機碼名稱：** SiteName

  -   **必要：** 是
  -   **值：** SiteName
  -   **詳細資料:** 此站台的描述。


- **機碼名稱：** SMSInstallDir

  - **必要：** 是
  - **值：** &lt;*ConfigMgrInstallationPath*>
  - **詳細資料:** 指定 Configuration Manager 程式檔案的安裝資料夾。
    > [!NOTE]   
    >  您可以指定用於 Configuration Manager 安裝的原始路徑或新路徑。

- **機碼名稱：** SDKServer

  -   **必要：** 是
  -   **值：** &lt;*SMS 提供者的 FQDN*>
  -   **詳細資料:** 指定裝載「SMS 提供者」的伺服器 FQDN。 指定失敗前裝載「SMS 提供者」的伺服器。

       您可以在初始安裝後設定站台的其他 SMS 提供者。

- **機碼名稱：** PrerequisiteComp

  -   **必要：** 是
  -   **值：** 0 或 1  
       0 = 下載   
       1 = 已下載
  -   **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式就會下載檔案。  


- **機碼名稱：** PrerequisitePath

  -   **必要：** 是
  -   **值：** &lt;*PathToSetupPrerequisiteFiles*>
  -   **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。

- **機碼名稱：** AdminConsole

  -   **必要：** 可能
  -   **值：** 0 或 1 0 = 不安裝   
       1 = 安裝
  -   **詳細資料:** 指定是否安裝 Configuration Manager 主控台。 此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。


- **機碼名稱：** JoinCEIP   
  > [!Note]  
  > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

  -   **必要：** 是
  -   **值：** 0 或 1  
       0 = 不加入  
       1 = 加入
  -   **詳細資料:** 指定是否加入「客戶經驗改進計畫」。

**SQLConfigOptions**

-   **機碼名稱：** SQLServerName

    -   **必要：** 是
    -   **值：** *&lt;SQLServerName\>*
    -   **詳細資料:** 執行裝載站台資料庫之 SQL Server 的伺服器名稱或叢集執行個體名稱。 請指定失敗前裝載站台資料庫的相同伺服器。


-   **機碼名稱：** DatabaseName

    -   **必要：** 是
    -   **值：** *&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>* \\ *&lt;SiteDatabaseName\>*
    -   **詳細資料:** 要建立或用來安裝管理中心網站資料庫的 SQL Server 資料庫的名稱。 請指定失敗前所使用的相同資料庫名稱。

        > [!IMPORTANT]  
        >  如果您未使用預設執行個體，就必須指定執行個體名稱及站台資料庫名稱。

-   **機碼名稱：** SQLSSBPort

    -   **必要：** 否
    -   **值：** &lt;*SSBPortNumber*>
    -   **詳細資料:** 指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022，但也支援其他連接埠。 請指定失敗前所使用的相同 SSB 連接埠。

## <a name="recover-a-primary-site-unattended"></a>自動復原主要網站
 使用下列資訊設定自動安裝指令碼檔案來復原管理中心網站。

 **識別**

-   **機碼名稱：** 動作

    -   **必要：** 是
    -   **值：** RecoverPrimarySite
    -   **詳細資料:** 復原主要站台


-   **機碼名稱：** CDLatest

    -   **必要：** 是 (只有在使用來自 CD.Latest 資料夾的媒體時)。
    -   **值：** 1 (1 以外的任何值都會被視為不使用 CD.Latest)。
    -   **詳細資料:** 當您從 CD.Latest 資料夾中的媒體執行安裝程式，以安裝主要站台或管理中心網站，或是復原主要站台或管理中心網站時，您的指令碼必須包含此機碼和值。 這個值會通知安裝程式目前正在使用來自 CD.Latest 的媒體。

**RecoveryOptions**

-   **機碼名稱：** ServerRecoveryOptions

    -   **必要：** 是
    -   **值：** 1、2 或 4    
         1 = 復原網站伺服器和 SQL Server。   
         2 = 僅復原網站伺服器。  
         4 = 僅復原 SQL Server。
    -   **詳細資料:** 指定安裝程式是要復原站台伺服器、SQL Server，還是同時復原兩者。 針對 ServerRecoveryOptions 設定以下值時，需要關聯的索引鍵：

        -   **值 = 1** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。

             將 **DatabaseRecoveryOptions** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。

        -   **值 = 2** ：您可以選擇為 **SiteServerBackupLocation** 索引鍵指定值，以使用站台備份來復原站台。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。

        -   **值 = 4** 將 **BackupLocation** 索引鍵的值設定為 **10** 時，就需要 **BackupLocation** 索引鍵，這會從備份還原網站資料庫。

-   **機碼名稱：** DatabaseRecoveryOptions

    -   **必要：** 可能
    -   **值：**   
         - **10** = 從備份還原站台資料庫。  
         - **20** = 使用以另一種方式手動復原的站台資料庫。     
         - **40** = 為網站建立新的資料庫。 若無可用網站資料庫備份，請使用此選項。 透過從其他網站複寫來復原全域和網站資料。  
         - **80** = 略過資料庫復原。
    -   **詳細資料:** 指定安裝程式如何復原 SQL Server 中的站台資料庫。 **ServerRecoveryOptions** 設定值為 **1** 或 **4**時，需要此索引鍵。


-   **機碼名稱：** SiteServerBackupLocation

    -   **必要：** 否
    -   **值：** &lt;PathToSiteServerBackupSet\>
    -   **詳細資料:** 指定網站伺服器備份集的路徑。 **ServerRecoveryOptions** 設定值為 **1** 或 **2** 時，可選擇是否要使用此索引鍵。 指定 **SiteServerBackupLocation** 索引鍵值，藉此使用網站備份來復原網站。 若沒有指定值，重新安裝網站時就不會從備份集還原網站。     


-   **機碼名稱：** BackupLocation

    -   **必要：** 可能
    -   **值：** &lt;PathToSiteDatabaseBackupSet\>
    -   **詳細資料:** 指定站台資料庫備份組的路徑。 **ServerRecoveryOptions** 索引鍵的設定值為 **1** 或 **4** ，且 **DatabaseRecoveryOptions** 索引鍵的設定值為 **10** 時，需要 **BackupLocation** 索引鍵。

**選項**

-   **機碼名稱：** ProductID

    -   **必要：** 是
    -   **值：**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - 評估版     
    -   **詳細資料:** Configuration Manager 安裝產品金鑰 (包括破折號)。 輸入 **Eval** 可安裝 Configuration Manager 的評估版。  


-   **機碼名稱：** SiteCode

    -   **必要：** 是
    -   **值：** &lt;站台碼\>
    -   **詳細資料:** 可在階層中唯一識別站台的三個英數字元。 指定失敗前網站所使用的站台碼。


-   **機碼名稱：** SiteName

    -   **必要：** 是
    -   **值：** SiteName
    -   **詳細資料:** 此站台的描述。


-   **機碼名稱：** SMSInstallDir

    -   **必要：** 是
    -   **值：** &lt;*ConfigMgrInstallationPath*>
    -   **詳細資料:** 指定 Configuration Manager 程式檔案的安裝資料夾。

        > [!NOTE]   
        >  您可以指定用於 Configuration Manager 安裝的原始路徑或新路徑。

-   **機碼名稱：** SDKServer

    -   **必要：** 是
    -   **值：** &lt;*SMS 提供者的 FQDN*>
    -   **詳細資料:** 指定裝載「SMS 提供者」的伺服器 FQDN。 指定失敗前裝載「SMS 提供者」的伺服器。

         您可以在初始安裝後設定站台的其他 SMS 提供者。

-   **機碼名稱：** PrerequisiteComp

    -   **必要：** 是
    -   **值：** 0 或 1    
         0 = 下載   
         1 = 已下載   
    -   **詳細資料:** 指定是否已下載安裝程式必要條件檔案。 例如，如果您使用 0 值，安裝程式就會下載檔案。


-   **機碼名稱：** PrerequisitePath

    -   **必要：** 是
    -   **值：** &lt;*PathToSetupPrerequisiteFiles*>
    -   **詳細資料:** 指定安裝程式必要條件檔案的路徑。 根據 **PrerequisiteComp** 值而定，安裝程式會使用此路徑來儲存下載的檔案或尋找之前下載的檔案。


-   **機碼名稱：** AdminConsole

    -   **必要：** 可能
    -   **值：** 0 或 1  
         0 = 不安裝   
         1 = 安裝  
    -   **詳細資料:** 指定是否安裝 Configuration Manager 主控台。 此索引鍵為必要，除非 **ServerRecoveryOptions** 設定的值為 **4**。

-   **機碼名稱：** JoinCEIP  
    > [!Note]  
    > 從 Configuration Manager 1802 版開始，已從產品中移除 CEIP 功能。

    -   **必要：** 是
    -   **值：** 0 或 1    
         0 = 不加入  
         1 = 加入
    -   **詳細資料:** 指定是否加入「客戶經驗改進計畫」。


**SQLConfigOptions**

-   **機碼名稱：** SQLServerName

    -   **必要：** 是
    -   **值：** *&lt;SQLServerName\>*
    -   **詳細資料:** 執行裝載站台資料庫之 SQL Server 的伺服器名稱或叢集執行個體名稱。 請指定失敗前裝載站台資料庫的相同伺服器。


-   **機碼名稱：** DatabaseName

    -   **必要：** 是
    -   **值：** *&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>* \\ *&lt;SiteDatabaseName\>*
    -   **詳細資料:** 要建立或用來安裝管理中心網站資料庫的 SQL Server 資料庫的名稱。 請指定失敗前所使用的相同資料庫名稱。

        > [!IMPORTANT]    
        >  如果您未使用預設執行個體，就必須指定執行個體名稱及站台資料庫名稱。

-   **機碼名稱：** SQLSSBPort

    -   **必要：** 否
    -   **值：** &lt;*SSBPortNumber*>
    -   **詳細資料:** 指定 SQL Server 所使用的 SQL Server Service Broker (SSB) 連接埠。 通常 SSB 是設定為使用 TCP 連接埠 4022，但也支援其他連接埠。 請指定失敗前所使用的相同 SSB 連接埠。

**階層 ExpansionOption**

-   **機碼名稱：** CCARSiteServer

    -   **必要：** 可能
    -   **值：** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **詳細資料:** 指定主要站台在加入 Configuration Manager 階層時要連結的管理中心網站。 如果主要網站在失敗前連接至管理中心網站，則此設定為必要。 請指定失敗前用於管理中心網站的站台碼。

-   **機碼名稱：** CASRetryInterval

    -   **必要：** 否
    -   **值：** &lt;*間隔*>
    -   **詳細資料:** 指定連線失敗後，嘗試連線至管理中心網站的重試間隔 (以分計算)。 例如，如果與管理中心網站的連線失敗，主要站台會等待您針對 CASRetryInterval 指定的分鐘數，然後重試連線。


-   **機碼名稱：** WaitForCASTimeout

    -   **必要：** 否
    -   **值：** &lt;*逾時*>
    -   **詳細資料:** 指定主要站台連線至管理中心網站的逾時上限值 (單位分鐘)。 例如，如果主要網站連線至管理中心網站失敗，則主要網站會依據 CASRetryInterval 重試與管理中心網站的連線，直到達到 WaitForCASTimeout 期間。 您可以指定 0 到 100 的值。
