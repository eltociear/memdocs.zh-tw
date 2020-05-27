---
title: 工作順序變數參考
titleSuffix: Configuration Manager
description: 了解用以控制和自訂 Configuration Manager 工作順序的變數。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3ddd1a4b59ba750e9fca5f8386762b4a5dddb13
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429846"
---
# <a name="task-sequence-variables"></a>工作順序變數

適用於：Configuration Manager (最新分支)

本文是所有可用變數 (依字母順序排列) 的參考。 請使用瀏覽器 [尋找] 功能 (通常是 **CTRL** + **F**) 來尋找特定變數。 變數會註明它是否是特定步驟的特定變數。 [工作順序步驟](task-sequence-steps.md)文章包含了每個步驟的特定變數清單。

如需詳細資訊，請參閱[使用工作順序變數](using-task-sequence-variables.md)。

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a> 工作順序變數參考

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

當 Windows PE 啟動時，工作順序會掃描電腦的硬碟以取得舊版作業系統安裝。 [Windows] 資料夾位置會儲存在此變數中。 您可以設定工作順序從環境中擷取這個值，並用它來指定相同的 [Windows] 資料夾位置以用於新的作業系統安裝。

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

當 Windows PE 啟動時，工作順序會掃描電腦的硬碟以取得舊版作業系統安裝。 作業系統安裝所在的硬碟位置會儲存在此變數中。 您可以設定工作順序從環境中擷取這個值，並用它來指定相同的硬碟位置以用於新的作業系統。

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*適用於[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)步驟。*

(input)

指定包含 USMT 檔案之 Configuration Manager 套件的套件識別碼。 這是必要變數。

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*適用於[還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)步驟。*

(input)

指定包含 USMT 檔案之 Configuration Manager 套件的套件識別碼。 這是必要變數。

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a> _SMSTSAdvertID

儲存目前正在執行的工作順序部署唯一識別碼。 它會使用與 Configuration Manager 軟體發佈部署識別碼相同的格式。 如果從獨立媒體執行工作順序，這個變數為未定義。

#### <a name="example"></a>範例

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定電腦的資產標記。

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a> _SMSTSBootImageID

如果目前正在執行的工作順序參考開機映像套件，則這個環境變數會儲存開機映像套件識別碼。 如果工作順序未參考開機映像套件，則不會設定此變數。

#### <a name="example"></a>範例

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

工作順序會在偵測到處於 UEFI 模式的電腦時，設定此變數。

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
當工作順序在本機磁碟上快取內容時，它會設定此變數。 該變數包含快取路徑。 如果次變數不存在，則沒有快取。

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a> _SMSTSClientGUID

儲存 Configuration Manager 用戶端 GUID 的值。 如果是從獨立媒體執行工作順序，則不會設定此變數。

#### <a name="example"></a>範例

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

指定目前正在執行之工作順序步驟的名稱。 工作順序管理員執行每個步驟之前，會設定這個變數。

#### <a name="example"></a>範例

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定的電腦所使用的預設閘道。

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

如果目前工作順序的執行模式為視需要下載，此變數便為 `true`。 隨選下載模式表示工作順序管理員只有在必須存取內容時，才會在本機下載內容。

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a> _SMSTSInWinPE

當目前的工作順序步驟是在 Windows PE 中執行時，此變數便為 `true`。 請測試這個工作順序變數，以判斷目前的 OS 環境。

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定的電腦所使用的 IP 位址。

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a> _SMSTSLastActionName

儲存已執行之最後動作的名稱。 此變數與 **_SMSTSLastActionRetCode** 相關。 工作順序會將這些值記錄在 smsts.log 檔案中。 此變數對工作順序的疑難排解很有幫助。 當步驟失敗時，自訂指令碼會包含步驟名稱及傳回碼。

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

儲存來自上一個執行動作的傳回碼。 這個變數可做為決定是否要執行下一個步驟的條件。

#### <a name="example"></a>範例

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- 如果上一個步驟成功，此變數便為 `true`。  

- 如果上一個步驟失敗，則為 `false`。  

- 如果工作順序因步驟已被停用或相關聯的條件評估為 **false** 而略過上一個動作，系統並不會重設此變數。 它仍會保留上一個動作的值。  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a> _SMSTSLastContentDownloadLocation

<!-- 2840337 -->
從 1906 版開始，這個變數包含下載工作順序或嘗試下載內容的最後一個位置。 您只要檢查此變數即可，而不需要剖析此內容位置的用戶端記錄。

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

指定透過下列其中一種方法啟動工作順序：  

- **SMS**：Configuration Manager 用戶端，例如當使用者從「軟體中心」予以啟動時
- **UFD**：舊版 USB 媒體
- **UFD+FORMAT**：較新版 USB 媒體
- **CD**：可開機的 CD
- **DVD**：可開機的 DVD
- **PXE**：搭配 PXE 的網路開機
- **HD**：硬碟上預先設置的媒體

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a> _SMSTSLogPath

儲存記錄檔目錄的完整路徑。 請使用此值來決定工作順序步驟記錄其動作的位置。 沒有可用的硬碟時，則不會設定此值。

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定的電腦所使用的 MAC 位址。

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a> _SMSTSMachineName

儲存並指定電腦名稱。 儲存工作順序用來記錄所有狀態訊息之電腦的名稱。 若要變更新 OS 中的電腦名稱，請使用 [OSDComputerName](#OSDComputerName-input) 變數。

### <a name="_smstsmake"></a><a name="SMSTSMake"></a> _SMSTSMake

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定的電腦。

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a> _SMSTSMDataPath

指定 [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) 變數所定義的路徑。 此路徑指定工作順序在執行時，會將暫存快取檔案儲存在目的地電腦上的哪個位置。 如果您在工作順序啟動之前定義 SMSTSLocalDataDrive (例如透過設定集合變數)，Configuration Manager 便會在工作順序啟動之後定義 _SMSTSMDataPath 變數。

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a> _SMSTSMediaType

指定用來起始安裝的媒體類型。 媒體類型範例包括開機媒體、完整媒體、PXE 和預先設置的媒體。

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a> _SMSTSModel

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定電腦的型號。

### <a name="_smstsmp"></a><a name="SMSTSMP"></a> _SMSTSMP

儲存 Configuration Manager 管理點的 URL 或 IP 位址。

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a> _SMSTSMPPort

儲存 Configuration Manager 管理點的連接埠號碼。

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a> _SMSTSOrgName

儲存工作順序顯示在進度對話方塊中的商標標題名稱。

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*適用於[升級作業系統](task-sequence-steps.md#BKMK_UpgradeOS)步驟。*

儲存 Windows 安裝程式傳回的結束代碼值，以表示成功或失敗。 這個變數與 `/Compat` 命令列選項搭配使用時，相當有用。

#### <a name="example"></a>範例

完成純相容性掃描時，請依據失敗或成功結束代碼來採取後續步驟動作。 成功時，請啟動升級。 或是在環境中設定標記來收集硬體清查。 例如，新增檔案或設定登錄機碼。 使用此標記來建立備妥升級的電腦集合，或是必須採取動作才能升級的電腦集合。

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a> _SMSTSPackageID

儲存目前正在執行的工作順序識別碼。 此識別碼使用的格式與 Configuration Manager 套件識別碼相同。

#### <a name="example"></a>範例

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a> _SMSTSPackageName

儲存目前正在執行的工作順序名稱。 Configuration Manager 系統管理員會在建立工作順序時指定此名稱。

#### <a name="example"></a>範例

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

如果目前工作順序的執行模式為從發佈點執行，請設為 `true`。 此模式意謂著工作順序管理員會從發佈點取得必要的套件共用。

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定電腦的序號。

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

指定 Windows 安裝程式是否在就地升級期間執行了復原作業。 此變數值可以是 `true` 或 `false`。

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a> _SMSTSSiteCode

儲存 Configuration Manager 站台的站台碼。

#### <a name="example"></a>範例

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a> _SMSTSTimezone

此變數會以下列格式儲存時區資訊：

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>範例

針對**東部時間 (美國和加拿大)** 時區：

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a> _SMSTSType

指定目前正在執行的工作順序類型。 其值可以是下列其中一個值：  

- **1**：一般工作順序
- **2**：OS 部署工作順序

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a> _SMSTSUseCRL

當工作順序使用 HTTPS 來與管理點進行通訊時，此變數可指定是否使用憑證撤銷清單 (CRL)。

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a> _SMSTSUserStarted

指定使用者是否已啟動工作順序。 只有在從「軟體中心」啟動工作順序時，才會設定此變數。 例如，當 [_SMSTSLaunchMode](#SMSTSLaunchMode) 設定為 `SMS` 時。

此變數可以包含下列值：  

- `true`：指定由使用者從「軟體中心」手動啟動工作順序。  

- `false`：指定由 Configuration Manager 排程器自動起始工作順序。

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a> _SMSTSUseSSL

指定工作順序是否使用 SSL 來與 Configuration Manager 管理點通訊。 如果您針對 HTTPS 設定您的站台系統，此值便會設定為 `true`。

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a> _SMSTSUUID

*適用於[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)步驟。*

指定電腦的 UUID。

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a> _SMSTSWTG

指定電腦是否以 Windows To Go 裝置執行。

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a> _TS_CRMEMORY

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[記憶體下限 (MB)] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a> _TS_CRSPEED

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[最低處理器速度 (MHz)] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a> _TS_CRDISK

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[最小可用磁碟空間 (MB)] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a> _TS_CROSTYPE

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[要重新整理的目前 OS 為] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a> _TS_CRARCH

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[目前 OS 的架構] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a> _TS_CRMINOSVER

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[最低 OS 版本] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a> _TS_CRMAXOSVER

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[最高 OS 版本] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a> _TS_CRCLIENTMINVER

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[用戶端最低版本] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a> _TS_CROSLANGUAGE

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[目前 OS 的語言] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a> _TS_CRACPOWER

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[AC 電源已插入] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a> _TS_CRNETWORK

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[網路介面卡已連線] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a> _TS_CRWIRED

「從 2002 版開始」 <!--6005561-->  
「適用於[檢查整備程度](task-sequence-steps.md#BKMK_CheckReadiness)步驟。」

[網路介面卡並非無線] 檢查是否已傳回 True (`1`) 或 False (`0`) 的唯讀變數。 若未啟用該檢查，則此唯讀變數的值為空白。

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a> _TSAppInstallStatus

工作順序會以[安裝應用程式](task-sequence-steps.md#BKMK_InstallApplication)步驟期間的應用程式安裝狀態來設定此變數。 它會設定下列其中一個值：  

- **未定義**：尚未執行 [安裝應用程式] 步驟。  

- **錯誤**：在 [安裝應用程式] 步驟期間，因發生錯誤而使至少一個應用程式失敗。  

- **警告**：在 [安裝應用程式] 步驟期間未發生任何錯誤。 未安裝一或多個應用程式或必要的相依性，因為不符合需求。  

- **成功**：在 [安裝應用程式] 步驟期間未偵測到錯誤或警告。  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a> _TSSecureBoot

「從 2002 版開始」 <!--5842295-->  

請使用此變數來判斷安全開機在已啟用 UEFI 裝置上的狀態。 這個變數可具有下列其中一個值：

- `NA`：已建立關聯的登錄值不存在，這表示裝置不支援安全開機。
- `Enabled`：裝置已啟用安全開機。
- `Disabled`：裝置已停用安全開機。

### <a name="osdadapter"></a><a name="OSDAdapter"></a> OSDAdapter

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

這個工作順序變數是「陣列」變數。 陣列中的每個項目都代表電腦上單一網路介面卡的設定。 藉由合併具有以零為起始之網路介面卡索引的陣列變數名稱與屬性名稱，存取每個介面卡的設定。

如果 [套用網路設定] 步驟會設定多個網路介面卡，它會使用變數名稱中的索引 **1** 來定義「第二個」網路介面卡的內容。 例如：OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList 及 OSDAdapter1DNSDomain。

請使用下列變數名稱來定義此步驟要設定之「第一個」網路介面卡的內容：

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

需要此設定。 可能的值為 `True` 或 `False`。 例如：

`true`：為介面卡啟用「動態主機設定通訊協定」(DHCP)

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

介面卡的 IP 位址清單 (以逗號分隔)。 除非 **EnableDHCP** 設定為 `false`，否則會忽略此屬性。 需要此設定。

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

子網路遮罩清單 (以逗號分隔)。 除非 **EnableDHCP** 設定為 `false`，否則會忽略此屬性。 需要此設定。

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

IP 閘道位址清單 (以逗號分隔)。 除非 **EnableDHCP** 設定為 `false`，否則會忽略此屬性。 需要此設定。

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

介面卡的「網域名稱系統」(DNS) 網域。

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

介面卡的 DNS 伺服器清單 (以逗號分隔)。 需要此設定。

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

設定為 `true` 以在 DNS 中登錄介面卡的 IP 位址。

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

設定為 `true` 以在 DNS 中電腦的完整 DNS 名稱下登錄介面卡的 IP 位址。

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

設定為 `true` 以在介面卡上啟用 IP 通訊協定篩選。

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

允許透過 IP 執行的通訊協定清單 (以逗號分隔)。 如果 **EnableIPProtocolFiltering** 設定為 `false`，則會忽略此屬性。

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

設定為 `true` 以啟用介面卡的 TCP 連接埠篩選。

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

要授與 TCP 之存取權限的連接埠清單 (以逗號分隔)。 如果 **EnableTCPFiltering** 設定為 `false`，則會忽略此屬性。

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

NetBIOS over TCP/IP 的選項。 可能值如下所示：  

- `0`：使用來自 DHCP 伺服器的 NetBIOS 設定  
- `1`：啟用 NetBIOS over TCP/IP  
- `2`：停用 NetBIOS over TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

設定為 `true` 以使用 WINS 來進行名稱解析。

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

WINS 伺服器 IP 位址清單 (以逗號分隔)。 除非 **EnableWINS** 設定為 `true`，否則會忽略此屬性。

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

用來將設定與實體網路介面卡進行比對的 MAC 位址。

#### <a name="osdadapter0name"></a>OSDAdapter0Name

出現在網路連線控制台程式中的網路連線名稱。 此名稱的長度介於 0 到 255 個字元之間。

#### <a name="osdadapter0index"></a>OSDAdapter0Index

設定陣列中的網路介面卡設定索引。

#### <a name="example"></a>範例

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a> OSDAdapterCount

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的地電腦上安裝的網路介面卡數目。 設定 **OSDAdapterCount** 值時，請一併設定每個介面卡的所有設定選項。

例如，如果您設定第一個介面卡的 **OSDAdapter0TCPIPNetbiosOptions** 值，就必須設定該介面卡的所有值。

如果未指定此值，工作順序就會忽略所有 **OSDAdapter** 值。

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*適用於[套用驅動程式套件](task-sequence-steps.md#BKMK_ApplyDriverPackage)步驟。*

(input)

指定要從驅動程式封裝安裝之大型儲存裝置驅動程式的內容識別碼。 如果未指定此變數，則不會安裝任何大型存放驅動程式。

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*適用於[套用驅動程式套件](task-sequence-steps.md#BKMK_ApplyDriverPackage)步驟。*

(input)

指定是否安裝大量存放裝置驅動程式，這個變數必須是 **scsi**。

如果設定 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID)，則需要此變數。

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*適用於[套用驅動程式套件](task-sequence-steps.md#BKMK_ApplyDriverPackage)步驟。*

(input)

指定要安裝之大型儲存裝置驅動程式的開機關鍵識別碼。 這個識別碼會列在裝置驅動程式之 txtsetup.oem 檔案的 **scsi** 區段中。

如果設定 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID)，則需要此變數。

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*適用於[套用驅動程式套件](task-sequence-steps.md#BKMK_ApplyDriverPackage)步驟。*

(input)

指定要安裝之大型存放驅動程式的 INF 檔案。

如果設定 [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID)，則需要此變數。

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*適用於[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)步驟。*

(input)

如果驅動程式類別目錄中有多個與硬體裝置相容的裝置驅動程式，此變數會決定步驟的動作。

#### <a name="valid-values"></a>有效值

- `true` (預設)：只安裝最佳裝置驅動程式  

- `false`：安裝所有相容的裝置驅動程式，Windows 會選擇最佳的驅動程式來使用  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*適用於[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)步驟。*

(input)

驅動程式類別目錄類別唯一識別碼清單 (以逗號分隔)。 [自動套用驅動程式] 步驟只會考慮至少在其中一個指定類別中的驅動程式。 此值為選擇性，預設並不會設定此值。 列舉站台上的 **SMS_CategoryInstance** 物件清單，即可取得可用的類別識別碼。

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a> OSDBitLockerRebootCount

*適用於[停用 BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker)步驟。*

<!-- 4512937 -->
從 1906 版開始，請使用此變數來設定繼續保護的重新啟動次數。

#### <a name="valid-values"></a>有效值

從 `1` 到 `15` 的整數。

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a> OSDBitLockerRebootCountOverride

*適用於[停用 BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker)步驟。*

<!-- 4512937 -->
從 1906 版開始，設定此值以覆寫由該步驟或  [OSDBitLockerRebootCount](#OSDBitLockerRebootCount) 變數設定的計數。 雖然其他方法只接受值 1 至 15，但如果您將此變數設為 0，BitLocker 就會永久保持在停用狀態。 當工作順序設定了一個值，但您想以每一裝置或每一集合的基礎來設定個別值時，這個變數就相當實用。

#### <a name="valid-values"></a>有效值

從 `0` 到 `15` 的整數。

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*適用於[啟用 BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker)步驟。*

(input)

[啟用 BitLocker] 步驟會使用指定的值作為修復密碼，而不會產生隨機修復密碼。 值必須是有效的數值 BitLocker 修復密碼。

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*適用於[啟用 BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker)步驟。*

(input)

[啟用 BitLocker] 步驟會使用信賴平台模組 (TPM) 作為啟動金鑰，而不是針對金鑰管理選項 [僅 USB 上的啟動金鑰] 產生隨機啟動金鑰。 值必須是有效的 256 位元 Base64 編碼的 BitLocker 啟動金鑰。

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a> OSDCaptureAccount

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

(input)

指定具有在網路共用 ([OSDCaptureDestination](#OSDCaptureDestination)) 上儲存所擷取映像之權限的 Windows 帳戶名稱。 請一併指定 [OSDCaptureAccountPassword](#OSDCaptureAccountPassword)。

如需有關擷取 OS 映像帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account)。

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

(input)

指定用來在網路共用 ([OSDCaptureDestination](#OSDCaptureDestination)) 上儲存所擷取映像之 Windows 帳戶 ([OSDCaptureAccount](#OSDCaptureAccount)) 的密碼。

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a> OSDCaptureDestination

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

(input)

指定工作順序儲存所擷取 OS 映像的位置。 目錄名稱長度上限為 255 個字元。 如果網路共用需要驗證，請指定 [OSDCaptureAccount](#OSDCaptureAccount) 和 [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) 變數。

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a> OSDComputerName (input)

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定目的地電腦的名稱。

#### <a name="example"></a>範例

`%_SMSTSMachineName%` (預設)

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a> OSDComputerName (output)

*適用於[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步驟。*

設為電腦的 NetBIOS 名稱。 只有在 [OSDMigrateComputerName](#OSDMigrateComputerName)設定為 `true` 時，才會設定此值。

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a> OSDConfigFileName

*適用於[套用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步驟。*

(input)

指定與 OS 部署映像套件相關聯之 OS 部署回應檔案的檔案名稱。  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a> OSDDataImageIndex

*適用於[套用資料映像](task-sequence-steps.md#BKMK_ApplyDataImage)步驟。*

(input)

指定套用至目的地電腦之映像的索引值。

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a> OSDDiskIndex

*適用於[格式化和分割磁碟](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步驟。*

(input)

指定要分割的實體磁碟編號。

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a> OSDDNSDomain

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的地電腦所使用的主要 DNS 伺服器。

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的地電腦的 DNS 搜尋順序。

### <a name="osddomainname"></a><a name="OSDDomainName"></a> OSDDomainName

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的電腦所加入之 Active Directory 網域的名稱。 指定的值必須是有效的 Active Directory 網域服務網域名稱。

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a> OSDDomainOUName

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的地電腦所加入之組織單位 (OU) 的 RFC 1779 格式名稱。 指定時，值必須包含完整路徑。

#### <a name="example"></a>範例

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
適用於[安裝套件](task-sequence-steps.md#BKMK_InstallPackage)步驟。

從 1902 版開始  
*適用於[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)步驟。*

(input)

若要防止顯示或記錄潛在的機密資料，請將此變數設定為 `TRUE`。 此變數會在 [安裝套件] 步驟期間，為 **smsts.log** 中的程式名稱加上遮罩。

從 1902 版開始，當您將此變數設為 `TRUE` 時，它也會隱藏記錄檔的 [執行命令列] 步驟中的命令列。<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定是否啟用 TCP/IP 篩選。

#### <a name="valid-values"></a>有效值

- `true`  
- `false` (預設)  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*適用於[格式化和分割磁碟](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步驟。*

(input)

指定是否要在 GPT 硬碟上建立 EFI 磁碟分割。 EFI 型電腦使用此磁碟分割作為啟動磁碟。

#### <a name="valid-values"></a>有效值

- `true`  
- `false` (預設)

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a> OSDImageCreator

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

(input)

已建立映像之使用者的選用名稱。 這個名稱儲存在 WIM 檔案中。 使用者名稱長度上限為 255 個字元。

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a> OSDImageDescription

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

(input)

所擷取 OS 映像的使用者定義描述 (選擇性)。 這個描述儲存在 WIM 檔案中。 描述長度上限為 255 個字元。

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a> OSDImageIndex

*適用於[套用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步驟。*

(input)

指定套用至目的地電腦之 WIM 檔案的映像索引值。

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a> OSDImageVersion

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

(input)

要指派給所擷取 OS 映像的使用者定義版本號碼 (選擇性)。 這個版本號碼儲存在 WIM 檔案中。 此值可以是英數字元的任意組合，長度上限為 32 個字元。

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*適用於[套用驅動程式套件](task-sequence-steps.md#BKMK_ApplyDriverPackage)步驟。*

(input)

指定套用驅動程式套件時，要新增至 DISM 命令列的額外選項。 工作順序不會驗證命令列選項。

若要使用此變數，請在 [套用驅動程式套件] 步驟上，啟用 [透過以遞迴選項執行 DISM 的套件安裝驅動程式] 設定。

如需詳細資訊，請參閱 [Windows 10 DSIM 命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options) \(英文\)。

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a> OSDJoinAccount

*適用於下列步驟：*  

- [套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(input)

指定用來將目的地電腦新增至網域的網路使用者帳戶。 加入網域時，這是必要變數。

如需有關工作順序網域連接帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)。

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a> OSDJoinDomainName

*適用於[加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步驟。*

(input)

指定目的電腦所加入之 Active Directory 網域的名稱。 網域名稱的長度必須介於 1 到 255 個字元。

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*適用於[加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步驟。*

(input)

指定目的地電腦所加入之組織單位 (OU) 的 RFC 1779 格式名稱。 指定時，值必須包含完整路徑。 OU 名稱的長度必須介於 0 到 32,767 個字元。 如果 [OSDJoinType](#OSDJoinType) 變數設定為 `1` (加入工作群組)，則不會設定此值。

#### <a name="example"></a>範例

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a> OSDJoinPassword

*適用於下列步驟：*  

- [套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(input)

指定目的電腦用來加入 Active Directory 網域之 [OSDJoinAccount](#OSDJoinAccount) 的密碼。 如果工作順序環境未包含此變數，Windows 安裝程式就會嘗試使用空白密碼。 如果 [OSDJoinType](#OSDJoinType) 變數設定為 `0`(加入網域)，則這是必要值。

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*適用於[加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步驟。*

(input)

指定是否要在目的地電腦加入網域或工作群組之後略過重新啟動。

#### <a name="valid-values"></a>有效值

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a> OSDJoinType

*適用於[加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步驟。*

(input)

指定目的地電腦是否加入 Windows 網域或工作群組。

#### <a name="valid-values"></a>有效值

- `0`：將目的電腦加入 Windows 網域  
- `1`：將目的電腦加入工作群組  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*適用於[加入網域或工作群組](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)步驟。*

(input)

指定目的地電腦所加入之工作群組的名稱。 工作群組名稱的長度必須介於 1 到 32 個字元。

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a> OSDKeepActivation

*適用於[準備 Windows 以進行擷取](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)步驟。*

(input)

指定 sysprep 保留或重設產品啟用旗標。

#### <a name="valid-values"></a>有效值

- `true`：保留啟用旗標
- `false` (預設值)：重設啟用旗標

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

(input)

指定本機系統管理員帳戶密碼。 如果您啟用 [隨機產生本機系統管理員密碼並在所有支援的平台上停用帳戶] 選項，則此步驟會忽略這個變數。 指定的值必須介於 1 到 255 個字元。

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
從 1902 版開始  
適用於[執行 PowerShell 指令碼](task-sequence-steps.md#BKMK_RunPowerShellScript)步驟。

(input)

為了防止可能記錄敏感資料，[執行 PowerShell 指令碼] 步驟不會在 **smsts.log** 檔案中記錄指令碼參數。 若要在工作順序記錄中包含指令碼參數，請將此變數設定為 [TRUE]。

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*適用於[擷取網路設定](task-sequence-steps.md#BKMK_CaptureNetworkSettings)步驟。*

(input)

指定工作順序是否會擷取網路介面卡資訊。 此資訊包括 TCP/IP、DNS 及 WINS 的組態設定。

#### <a name="valid-values"></a>有效值

- `true` (預設)
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*適用於[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)步驟。*

(input)

指定工作順序用來擷取使用者狀態的使用者狀態移轉工具 (USMT) 額外命令列選項。 步驟不會在工作順序編輯器中公開這些設定。 請以字串形式指定這些選項，工作順序會將此字串附加至為 ScanState 自動產生的 USMT 命令列。

在執行工作順序之前，不會驗證以此工作順序變數指定之 USMT 選項的正確性。

如需有關可用選項的詳細資訊，請參閱 [ScanState 語法](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax) \(英文\)。

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*適用於[還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)步驟。*

(input)

指定工作順序在還原使用者狀態時，所使用的使用者狀態移轉工具 (USMT) 額外命令列選項。 請以字串形式指定這些額外選項，工作順序會將此字串附加至為 LoadState 自動產生的 USMT 命令列。

在執行工作順序之前，不會驗證以此工作順序變數指定之 USMT 選項的正確性。

如需有關可用選項的詳細資訊，請參閱 [LoadState 語法](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax) \(英文\)。

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*適用於[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步驟。*

(input)

指定是否移轉電腦名稱。

#### <a name="valid-values"></a>有效值

- `true` (預設)。 [OSDComputerName (output)](#OSDComputerName-output) 變數會設定為電腦的 NetBIOS 名稱。  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*適用於[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)步驟。*

(input)

指定用來控制使用者設定檔擷取的組態檔案。 只有在 [OSDMigrateMode](#OSDMigrateMode) 設定為 `Advanced` 時，才會使用此變數。 這個逗號分隔的清單值設為執行自訂的使用者設定檔移轉。

#### <a name="example"></a>範例

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*適用於[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)步驟。*

(input)

如果 USMT 無法擷取某些檔案，此變數可讓使用者狀態擷取繼續進行。

#### <a name="valid-values"></a>有效值

- `true` (預設)  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*適用於[還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)步驟。*

(input)

即使 USMT 無法還原某些檔案，仍繼續進行。

#### <a name="valid-values"></a>有效值

- `true` (預設)  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*適用於下列步驟：*  

- [擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)  
- [還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)  

(input)

啟用 USMT 的詳細資訊記錄。 步驟需要此值。

#### <a name="valid-values"></a>有效值

- `true`  
- `false` (預設)  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*適用於[還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)步驟。*

(input)

指定是否還原本機電腦帳戶。

#### <a name="valid-values"></a>有效值

- `true`  
- `false` (預設)  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*適用於[還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)步驟。*

(input)

如果 [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) 變數為 `true`，此變數就必須包含指派給「所有」已移轉之本機帳戶的密碼。 USMT 會將相同的密碼指派給所有已移轉的本機帳戶。 將此密碼視為暫時性的密碼，並在稍後以某種其他方法變更。

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a> OSDMigrateMode

*適用於[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)步驟。*

(input)

可讓您自訂 USMT 所擷取的檔案。

#### <a name="valid-values"></a>有效值

- `Simple`：工作順序只會使用標準 USMT 設定檔  

- `Advanced`：工作順序變數 [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) 會指定 USMT 所使用的設定檔  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*適用於[擷取網路設定](task-sequence-steps.md#BKMK_CaptureNetworkSettings)步驟。*

(input)

指定工作順序是否會移轉工作群組或網域成員資格資訊。

#### <a name="valid-values"></a>有效值

- `true` (預設)
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*適用於[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步驟。*

(input)

指定步驟是否移轉使用者和組織資訊。

#### <a name="valid-values"></a>有效值

- `true` (預設)。 [OSDRegisteredOrgName (output)](#OSDRegisteredOrgName-output) 變數會設定為已登錄的電腦組織名稱。  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*適用於[擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)步驟。*

(input)

指定是否擷取加密檔案。

#### <a name="valid-values"></a>有效值

- `true`  
- `false` (預設)  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*適用於[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步驟。*

(input)

指定是否移轉電腦時區。

#### <a name="valid-values"></a>有效值

- `true` (預設)。 [OSDTimeZone (output)](#OSDTimeZone-output) 變數會設定為電腦的時區。  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的地電腦會加入 Active Directory 網域還是工作群組。

#### <a name="value-values"></a>有效值

- `0`：加入 Active Directory 網域  
- `1`：加入工作群組

### <a name="osdpartitions"></a><a name="OSDPartitions"></a> OSDPartitions

*適用於[格式化和分割磁碟](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步驟。*

(input)

此工作順序變數是磁碟分割設定的陣列變數。 陣列中的每個項目都代表硬碟上單一磁碟分割的設定。 藉由合併具有以零為起始之磁碟分割編號的陣列變數名稱與屬性名稱，存取為每個磁碟分割所定義的設定。

請使用下列變數名稱來定義此步驟在硬碟上所建立「第一個」磁碟分割的屬性：

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

指定磁碟分割的類型。 這是必要屬性。 有效值為 `Primary`、`Extended``Logical` 及 `Hidden`。

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

指定將磁碟分割格式化時，所要使用的檔案系統類型。 這是選用屬性。 如果您未指定檔案系統，步驟就不會將磁碟分割格式化。 有效值為 `FAT32` 和 `NTFS`。

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

指定磁碟分割是否可開機。 這是必要屬性。 如果將 MBR 磁碟的這個值設定為 `TRUE`，則步驟會將此磁碟分割標示為作用中。

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

指定所使用格式的類型。 這是必要屬性。 如果將此值設定為 `TRUE`，步驟就會執行快速格式化。 否則，步驟會執行完整格式化。

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

指定將磁碟區格式化時，指派給磁碟區的名稱。 這是選用屬性。

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

指定磁碟分割的大小。 這是選用屬性。 如果未指定此屬性，則會使用所有剩餘的可用空間來建立磁碟分割。 單位是透過 **OSDPartitions0SizeUnits** 變數所指定。

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

步驟會使用這些單位來解譯 **OSDPartitions0Size** 變數。 這是選用屬性。 有效值為 `MB` (預設)、`GB` 及 `Percent`。

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

當此步驟建立磁碟分割時，一律會使用 Windows PE 中的下一個可用磁碟機代號。 使用這個選擇性屬性來指定另一個工作順序變數的名稱。 步驟會使用這個變數來儲存新的磁碟機代號，供日後參考。

如果您使用此工作順序步驟來定義多個磁碟分割，則會使用變數名稱中的 **1**索引來定義「第二個」磁碟分割的屬性。 例如：**OSDPartitions1Type**、**OSDPartitions1FileSystem**、**OSDPartitions1Bootable**、**OSDPartitions1QuickFormat** 及 **OSDPartitions1VolumeName**。

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a> OSDPartitionStyle

*適用於[格式化和分割磁碟](task-sequence-steps.md#BKMK_FormatandPartitionDisk)步驟。*

(input)

指定分割磁碟時要使用的磁碟分割樣式。

#### <a name="valid-values"></a>有效值

- `GPT`：使用「GUID 磁碟分割表格」樣式
- `MBR`：使用主開機記錄磁碟分割樣式

### <a name="osdproductkey"></a><a name="OSDProductKey"></a> OSDProductKey

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

(input)

指定 Windows 產品金鑰。 指定的值必須介於 1 到 255 個字元。

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

(input)

指定新 OS 中本機系統管理員帳戶的隨機產生密碼。

#### <a name="valid-values"></a>有效值

- `true` (預設)：Windows 安裝程式會停用目標電腦上的本機系統管理員帳戶  

- `false`：Windows 安裝程式會啟用目標電腦上的本機系統管理員帳戶，並將帳戶密碼設定為 [OSDLocalAdminPassword](#OSDLocalAdminPassword) 的值  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (input)

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中的預設登錄組織名稱。 指定的值必須介於 1 到 255 個字元。

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (output)

*適用於[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步驟。*

設為電腦的註冊組織名稱。 只有在 [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) 變數設定為 `true` 時，才會設定此值。

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

(input)

指定新 OS 中的預設登錄使用者名稱。 指定的值必須介於 1 到 255 個字元。

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

(input)

指定允許的連線次數上限。 指定的數字必須在 5 到 9999 個連線的範圍內。

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

(input)

指定所使用的 Windows Server 授權模式。

#### <a name="valid-values"></a>有效值

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*適用於[升級作業系統](task-sequence-steps.md#BKMK_UpgradeOS)步驟。*

(input)

指定在 Windows 10 升級期間新增至 Windows 安裝程式的其他命令列選項。 工作順序不會驗證命令列選項。

如需詳細資訊，請參閱 [Windows 安裝程式命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*適用於[要求狀態存放區](task-sequence-steps.md#BKMK_RequestStateStore)步驟。*

(input)

當電腦帳戶無法連線到狀態移轉點時，這個變數會指定工作順序是否回復使用網路存取帳戶 (NAA)。

如需有關網路存取帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#network-access-account)。

#### <a name="valid-values"></a>有效值

- `true`  
- `false` (預設)  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*適用於[要求狀態存放區](task-sequence-steps.md#BKMK_RequestStateStore)步驟。*

(input)

指定工作順序步驟在步驟失敗之前嘗試尋找狀態移轉點的次數。 指定的計數必須介於 0 到 600。

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*適用於[要求狀態存放區](task-sequence-steps.md#BKMK_RequestStateStore)步驟。*

(input)

指定工作順序步驟在重試嘗試之間的秒數。 秒數上限為 30 個字元。

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a> OSDStateStorePath

*適用於下列步驟：*  

- [擷取使用者狀態](task-sequence-steps.md#BKMK_CaptureUserState)  
- [釋放狀態存放區](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [要求狀態存放區](task-sequence-steps.md#BKMK_RequestStateStore)  
- [還原使用者狀態](task-sequence-steps.md#BKMK_RestoreUserState)  

(input)

工作順序儲存或還原使用者狀態的網路共用或資料夾本機路徑名稱。 沒有任何預設值。

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*適用於[套用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步驟。*

(output)

指定套用映像之後，包含 OS 檔案的磁碟分割磁碟機代號。

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (input)

*適用於[擷取 OS 映像](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)步驟。*

指定參照電腦上所安裝 OS 的 Windows 目錄路徑。 工作順序會確認它是否是可供 Configuration Manager 擷取的受支援 OS。

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (output)

*適用於[準備 Windows 以進行擷取](task-sequence-steps.md#BKMK_PrepareWindowsforCapture)步驟。*

指定參照電腦上所安裝 OS 的 Windows 目錄路徑。 工作順序會確認它是否是可供 Configuration Manager 擷取的受支援 OS。

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a> OSDTimeZone (input)

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中所使用的預設時區設定。

將此變數的值設定為時區的語言不變名稱。 例如，使用下列登錄機碼下時區之 `Std` 值中的字串： `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`。

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a> OSDTimeZone (output)

*適用於[擷取 Windows 設定](task-sequence-steps.md#BKMK_CaptureWindowsSettings)步驟。*

設為電腦的時區。 只有在 [OSDMigrateTimeZone](#OSDMigrateTimeZone) 變數設定為 `true` 時，才會設定此值。

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a> OSDWindowsSettingsInputLocale

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中所使用的預設輸入地區設定。

如需這些 Windows 安裝程式回應檔案值的詳細資訊，請參閱 [Microsoft-Windows-International-Core - InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale)。

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a> OSDWindowsSettingsSystemLocale

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中所使用的預設系統地區設定。

如需這些 Windows 安裝程式回應檔案值的詳細資訊，請參閱 [Microsoft-Windows-International-Core - SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale)。

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a> OSDWindowsSettingsUILanguage

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中所使用的預設使用者介面語言。

如需這些 Windows 安裝程式回應檔案值的詳細資訊，請參閱 [Microsoft-Windows-International-Core - UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage)。

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a> OSDWindowsSettingsUILanguageFallback

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中所使用的後援使用者介面語言。

如需這些 Windows 安裝程式回應檔案值的詳細資訊，請參閱 [Microsoft-Windows-International-Core - UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback)。

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a> OSDWindowsSettingsUserLocale

*適用於[套用 Windows 設定](task-sequence-steps.md#BKMK_ApplyWindowsSettings)步驟。*

指定新 OS 中所使用的預設使用者地區設定。

如需這些 Windows 安裝程式回應檔案值的詳細資訊，請參閱 [Microsoft-Windows-International-Core - UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale)。

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*適用於[套用資料映像](task-sequence-steps.md#BKMK_ApplyDataImage)步驟。*

(input)

指定是否刪除目的地磁碟分割上的檔案。

#### <a name="valid-values"></a>有效值

- `true` (預設)
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a> OSDWorkgroupName

*適用於[套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟。*

(input)

指定目的地電腦所加入之工作群組的名稱。

請指定此變數或 [OSDDomainName](#OSDDomainName)變數。 工作群組名稱不可超過 32 個字元。

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a> SetupCompletePause

*適用於[升級作業系統](task-sequence-steps.md#BKMK_UpgradeOS)步驟。*

<!-- 4680263 -->

從 1910 版開始，使用此變數來處理高效能裝置上 Windows 安裝程式完成時發生 Window 10 就地升級工作順序的時間問題。 當您以秒為單位為此變數指派值時，Windows 安裝程式程序會在啟動工作順序之前延遲該時間量。 此逾時可讓 Configuration Manager 用戶端有額外的時間可初始化。

下列記錄項目是此問題的常見範例，您可以使用此變數來進行補救：

- TSManager 元件會在 **smsts.log** 中記錄類似下列錯誤的項目：

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Windows 安裝程式會在 **setupcomplete.cmd .log** 中記錄類似下列錯誤的項目：

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*適用於[設定 Windows 和 ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)步驟。*

(input)

指定安裝 Configuration Manager 用戶端時，工作順序所使用的用戶端安裝屬性。

如需詳細資訊，請參閱[關於用戶端安裝參數和內容](../../core/clients/deploy/about-client-installation-properties.md)。

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*適用於[連線至網路資料夾](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步驟。*

(input)

指定使用者帳戶，此帳戶會用來連線至 [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) 中的網路共用。 請使用 [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) 值來指定帳戶密碼。

如需有關工作順序網路資料夾連線帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)。

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*適用於[連線至網路資料夾](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步驟。*

(input)

指定要連線的目標網路磁碟機代號。 這是選擇性的值。 如果未指定，網路連線就不會對應至磁碟機代號。 如果指定此值，則值必須在從 D 到 Z 的範圍內。請勿使用 X，這是 Windows PE 在 Windows PE 階段所使用的磁碟機代號。

#### <a name="examples"></a>範例

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*適用於[連線至網路資料夾](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步驟。*

(input)

指定 [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) 的密碼，此帳戶會用來連線至 [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath) 中的網路共用。

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*適用於[連線至網路資料夾](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步驟。*

(input)

指定連線的網路路徑。 如果您需要將此路徑對應至磁碟機代號，請使用 [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) 值。

#### <a name="example"></a>範例

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*適用於[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步驟。*

(input)

指定安裝所有更新還是只安裝必要更新。

#### <a name="valid-values"></a>有效值

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a> SMSRebootMessage

*適用於[重新啟動電腦](task-sequence-steps.md#BKMK_RestartComputer)步驟。*

(input)

指定重新啟動目的地電腦之前要顯示給使用者的訊息。 如果未設定此變數，則會顯示預設訊息文字。 指定的訊息不可超過 512 個字元。

#### <a name="example"></a>範例

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a> SMSRebootTimeout

*適用於[重新啟動電腦](task-sequence-steps.md#BKMK_RestartComputer)步驟。*

(input)

指定重新啟動電腦之前向使用者顯示之警告的秒數。

#### <a name="examples"></a>範例

- `0` (預設)：不顯示重新開機訊息  
- `60`：顯示警告達一分鐘  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

用戶端在上次未傳回原則的嘗試之後，再次嘗試下載原則所需等待的秒數。 用戶端預設會等待 **0** 秒後再重試。

您可以從媒體或 PXE 使用啟動前置命令來設定此變數。

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

用戶端在第一次嘗試而找不到任何原則之後，會再嘗試下載原則的次數。 用戶端預設會重試 **0** 次。

您可以從媒體或 PXE 使用啟動前置命令來設定此變數。

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

指定工作順序如何將使用者和目的地電腦產生關聯。 將變數設定為下列其中一個值：  

- **Auto**：工作順序在將 OS 部署至目的電腦時，會在所指定使用者與目的電腦之間建立關聯性。  

- **Pending**：工作順序會在所指定使用者與目的電腦之間建立關聯性。 系統管理員必須核准關聯性才能設定它。  

- **Disabled**：工作順序在部署 OS 時，不會將使用者與目的電腦建立關聯。

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
在中斷連線的情況下，工作順序引擎會重複地嘗試傳送狀態訊息到管理點。 這種情況中的這個行為會造成工作順序處理的延遲。

請將此變數設定為 `true`，如此一來，工作順序引擎在第一則訊息傳送失敗之後，就不會再嘗試傳送狀態訊息。 第一次嘗試包含多次重試。

重新啟動工作順序時，這個變數的值會一直保存。 不過，工作順序會嘗試傳送初始狀態訊息。 第一次嘗試包含多次重試。 如果成功的話，工作順序會繼續傳送狀態，而不論這個變數的值為何。 如果無法傳送狀態，工作順序即會使用這個變數的值。

> [!NOTE]  
> [工作順序狀態報告](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status)依賴這些狀態訊息來顯示每個步驟的進度、歷程記錄和詳細資料。 如果狀態訊息無法傳送，系統就不會將其排入佇列。 當連線還原至管理點時，不會在稍後加以傳送。 此行為會導致工作順序狀態報告不完整且遺漏項目。

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*適用於[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)步驟。*

(input)

根據預設，在 64 位元 OS 上，工作順序會在命令列中使用 WOW64 檔案系統重新導向器來尋找並執行程式。 此行為可讓命令尋找 32 位元版本的 OS 程式和 DLL。 將此變數設定為 `true` 會停用 WOW64 檔案系統重新導向器。 命令會尋找原生 64 位元版本的 OS 程式和 DLL。 在 32 位元 OS 上執行時，此變數沒有作用。

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

此變數包含外部程式下載程式的中止字碼值。 此程式是在 [SMSTSDownloadProgram](#SMSTSDownloadProgram) 變數中指定的。 如果程式傳回等於 SMSTSDownloadAbortCode 變數值的錯誤碼，則內容下載會失敗，並且不再嘗試其他下載方法。

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

您可以使用此變數來指定替代內容提供者 (ACP)。 ACP 是一個用來下載內容的下載程式。 工作順序會使用 ACP，而不是預設的 Configuration Manager 下載程式。 在內容下載過程中，工作順序會檢查此變數。 如果已指定，工作順序就會執行程式來下載內容。

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

Configuration Manager 嘗試從發佈點下載內容的次數。 用戶端預設會重試 **2** 次。

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

Configuration Manager 在重新嘗試從發佈點下載內容之前等待的秒數。 用戶端預設會等待 **15** 秒後再重試。

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*適用於[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)步驟。*

當要求驅動程式類別目錄時，此變數是工作順序等待 HTTP 伺服器連線的秒數。 如果連線時間超過逾時設定，工作順序便會取消要求。 根據預設，逾時設定為 **60** 秒。

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*適用於[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)步驟。*

當要求驅動程式類別目錄時，此變數是工作順序等待回應的秒數。 如果連線時間超過逾時設定，工作順序便會取消要求。 根據預設，逾時設定為 **480** 秒。

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*適用於[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)步驟。*

當要求驅動程式類別目錄時，此變數是工作順序等待 HTTP 名稱解析的秒數。 如果連線時間超過逾時設定，工作順序便會取消要求。 根據預設，逾時設定為 **60** 秒。

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*適用於[自動套用驅動程式](task-sequence-steps.md#BKMK_AutoApplyDrivers)步驟。*

當傳送驅動程式類別目錄的要求時，此變數是工作順序等待傳送要求的秒數。 如果要求時間超過逾時設定，工作順序便會取消要求。 根據預設，逾時設定為 **60** 秒。

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

工作順序中發生錯誤時，它會顯示包含錯誤的對話方塊。 在這個變數所指定的秒數之後，工作順序會自動解除它。 此值預設為 **900** 秒 (15 分鐘)。

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

使用此變數變更非語言相關開機映像的顯示語言。

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

指定工作順序在執行時，會將暫存快取檔案儲存在目的地電腦上的哪個位置。

請在工作順序啟動之前設定此變數，例如藉由設定集合變數。 工作順序啟動之後，Configuration Manager 會根據定義 SMSTSLocalDataDrive 變數的內容，定義 [_SMSTSMDataPath](#SMSTSMDataPath) 變數。

### <a name="smstsmp"></a><a name="SMSTSMP"></a> SMSTSMP

使用此變數指定 Configuration Manager 管理點的 URL 或 IP 位址。

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*適用於下列步驟：*  

- [安裝應用程式](task-sequence-steps.md#BKMK_InstallApplication)  
- [安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(input)

如果用戶端不在內部網路上，請使用此變數來啟用重複的 MPList 要求，以重新整理用戶端。 此變數預設會設定為 `True`。

當用戶端在網際網路上時，請將此變數設定為 `False`，以避免不必要的延遲。

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*適用於下列步驟：*  

- [安裝應用程式](task-sequence-steps.md#BKMK_InstallApplication)  
- [安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(input)

如果工作順序無法從位置服務擷取管理點清單 (MPList)，此變數可指定工作順序在重試此步驟之前，所需等候的毫秒數。 工作順序預設會等候 `60000` 毫秒 (60 秒)，然後才進行重試。 最多會重試 3 次。

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

您可以使用此變數來讓用戶端能夠使用 Windows PE 對等快取。 將此變數設定為 `true` 可啟用此功能。

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Windows PE 對等快取為初始廣播所使用的自訂網路連接埠。 用戶端設定中設定的預設連接埠是 **8004**。

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a> SMSTSPersistContent

使用此變數暫時將內容保留在工作順序快取中。 此變數與 [SMSTSPreserveContent](#SMSTSPreserveContent) 不同，後者會在工作順序完成之後，將內容保留在 Configuration Manager 用戶端快取中。 SMSTSPersistContent 使用工作順序快取，SMSTSPreserveContent 使用 Configuration Manager 用戶端快取。

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a> SMSTSPostAction

指定在工作順序完成後執行的命令。 例如，指定 `shutdown.exe /r /t 30 /f` 在工作順序完成後 30 秒將電腦重新開機。

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

強制工作順序在目的電腦上執行特定目標部署。 從媒體或 PXE 使用啟動前置命令來設定這個變數。 如果設定這個變數，工作順序會覆寫任何所需的部署。

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

此變數會標幟工作順序中要在部署後保留在 Configuration Manager 用戶端快取中的內容。 此變數與 [SMSTSPersistContent](#SMSTSPersistContent) 不同，後者只會在工作順序持續期間保留內容。 SMSTSPersistContent 使用工作順序快取，SMSTSPreserveContent 使用 Configuration Manager 用戶端快取。 將 SMSTSPreserveContent 設定為 `true`，即可啟用此功能。

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

指定在電腦重新啟動之前要等待的秒數。 如果此變數為零 (0)，工作順序管理員便不會在重新開機前顯示通知對話方塊。

#### <a name="example"></a>範例

- `0`：不顯示通知  

- `60`：顯示通知達一分鐘  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a> SMSTSRebootDelayNext

<!--4447680-->
從 1906 版開始，請搭配現有的 [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) 變數使用此變數。 如果您想讓後續的重新開機搭配與首次重新開機不同的逾時來發生，請將 set SMSTSRebootDelayNext 以秒為單位設定為不同的值。

#### <a name="example"></a>範例

假設您想在 Windows 10 就地升級工作順序的一開始，為使用者提供 60 分鐘的重新開機通知。 在第一次長時間的逾時之後，您想讓後續的逾時僅歷時 60 秒。 請將 SMSTSRebootDelay 設定為 `3600`，然後將 SMSTSRebootDelayNext 設定為 `60`。  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

指定要在重新啟動通知對話方塊中顯示的訊息。 如果未設定此變數，則會顯示預設訊息。

#### <a name="example"></a>範例

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

表示完成目前的工作順序步驟之後會要求重新啟動。 如果工作順序步驟需要重新啟動以完成動作，請設定此變數。 電腦重新啟動之後，工作順序會從下一個工作順序步驟繼續執行。

- `HD`：重新啟動至已安裝的 OS
- `WinPE`：重新啟動至相關聯的開機映像

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

完成目前的工作順序步驟之後，要求重試。 如果設定此工作順序變數，請一併將 [SMSTSRebootRequested](#SMSTSRebootRequested) 設定為 `true`。 重新啟動電腦之後，工作順序管理員會重新執行相同的工作順序步驟。

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a> SMSTSRunCommandLineAsUser

「從 2002 版開始」 <!-- 5573175 -->  
*適用於[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)步驟。*

使用工作順序變數以設定 [執行命令列] 步驟的使用者內容。 您不需要使用預留位置帳戶來設定 [執行命令列] 步驟，即可使用 [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) 和 [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) 變數。

使用下列其中一個值來設定 `SMSTSRunCommandLineAsUser`：

- `true`：任何進一步的**執行命令列**步驟都會在使用者於 `SMSTSRunCommandLineUserName` 所指定內容中執行。

- `false`：任何進一步的**執行命令列**步驟都會在您於步驟上所設定內容中執行。

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*適用於[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)步驟。*

(input)

指定用來執行命令列的帳戶。 值是「使用者名稱」或「網域\使用者名稱」形式的字串。 請使用 [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) 變數來指定帳戶密碼。

> [!NOTE]
> 從 2002 版開始，請使用 [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) 變數搭配此變數來設定此步驟的使用者內容。
>
> 在 1910 版和更早版本中，請使用 [以下列帳戶的身分執行此步驟] 的設定來設定 [執行命令列] 步驟。 當您啟用此選項時，如果您要使用變數來設定使用者名稱與密碼，請指定帳戶的任何值。

如需有關工作順序執行身分帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)。

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword

*適用於[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)步驟。*

(input)

指定 [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) 變數所指定帳戶的密碼。

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a> SMSTSRunPowerShellAsUser

「從 2002 版開始」 <!-- 5573175 -->  
適用於[執行 PowerShell 指令碼](task-sequence-steps.md#BKMK_RunPowerShellScript)步驟。

使用工作順序變數以設定 [執行 PowerShell 指令碼] 步驟的使用者內容。 您不需要使用預留位置帳戶來設定 [執行 PowerShell 指令碼] 步驟，即可使用 [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) 和 [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) 變數。

使用下列其中一個值來設定 `SMSTSRunPowerShellAsUser`：

- `true`：任何進一步的 [執行 PowerShell 指令碼] 步驟都會在 `SMSTSRunPowerShellUserName` 中所指定的使用者內容中執行。

- `false`：任何進一步的 [執行 PowerShell 指令碼] 步驟都會在您於此步驟上所設定的內容中執行。

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a> SMSTSRunPowerShellUserName

適用於[執行 PowerShell 指令碼](task-sequence-steps.md#BKMK_RunPowerShellScript)步驟。

(input)

指定用來執行 PowerShell 指令碼的帳戶。 值是「使用者名稱」或「網域\使用者名稱」形式的字串。 使用 [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) 變數來指定帳戶密碼。

> [!NOTE]
> 若要使用這些變數，請使用設定來設定 [執行 PowerShell 指令碼] 步驟，以 [以下列帳戶的身分執行此步驟]。 當您啟用此選項時，如果您要使用變數來設定使用者名稱與密碼，請指定帳戶的任何值。

如需有關工作順序執行身分帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)。

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a> SMSTSRunPowerShellUserPassword

適用於[執行 PowerShell 指令碼](task-sequence-steps.md#BKMK_RunPowerShellScript)步驟。

(input)

指定 [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) 變數所指定帳戶的密碼。

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*適用於[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步驟。*

(input)

控制在此步驟期間的軟體更新掃描逾時。 例如，如果您預期在掃描期間會有許多更新，請增加此值。 預設值為 `3600` 秒 (60 分鐘)。 變數值以秒為單位進行設定。

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

使用下列格式來指定目的電腦的主要使用者：`<DomainName>\<UserName>`。 請使用逗號 (`,`) 來分隔多個使用者。 如需詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。

#### <a name="example"></a>範例

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*適用於[安裝軟體更新](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)步驟。*

(input)

當軟體更新安裝需要兩次重新啟動時，這個選用的工作順序變數可控制用戶端行為。 在此步驟前先設定此變數，以防止工作順序因為軟體更新安裝的第二次重新啟動而失敗。

以秒為單位設定 SMSTSWaitForSecondReboot 值，可指定重新啟動電腦時，工作順序要暫停在此步驟的秒數。 請提供足夠的時間，以防有第二次重新啟動。

例如，如果您將 SMSTSWaitForSecondReboot 設定為 `600`，工作順序就會在重新啟動後先暫停 10 分鐘，然後才執行其他步驟。 當單一 [安裝軟體更新] 工作順序步驟安裝數百個軟體更新時，這個變數非常有用。

> [!Note]
> 此變數只適用於部署 OS 的工作順序， 而不適用於自訂工作順序。 <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a> TSDebugMode

<!--3612274-->
從 1906 版開始，在集合或工作順序部署所在的電腦物件上，將此變數設定為 `TRUE`。 已設定此變數的任何裝置會將部署到其中的所有工作順序設為偵錯模式。

如需詳細資訊，請參閱[針對工作順序進行偵錯](../deploy-use/debug-task-sequence.md)。

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a> TSDebugOnError

<!-- 5012536 -->
從 1910 版開始，將此變數設定為 `TRUE`，以在工作順序傳回錯誤時自動啟動[工作順序偵錯工具](../deploy-use/debug-task-sequence.md)。

使用下列內容設定此變數：

- [設定工作順序變數](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步驟

- 集合變數。 如需詳細資訊，請參閱[如何設定變數](using-task-sequence-variables.md#bkmk_set)。

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
您可以使用此變數來控制工作順序向使用者顯示進度的時機。 您可以為工作順序中的這個變數設定多個時間點，來隱藏或顯示不同時間點的進度。  

- `true`：隱藏工作順序進度  

- `false`：顯示工作順序進度  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a> TSErrorOnWarning

*適用於[安裝應用程式](task-sequence-steps.md#BKMK_InstallApplication)步驟。*

(input)

指定工作順序引擎是否會在此步驟中將偵測到的警告視為錯誤。 當一或多個應用程式或必要的相依性因不符合需求而未安裝時，工作順序會將 [_TSAppInstallStatus](#TSAppInstallStatus) 變數設定為 `Warning`。 當您將此變數設定為 `True`，而工作順序將 **_TSAppInstallStatus** 設定為 `Warning` 時，結果是會發生錯誤。 預設行為是 `False` 值。

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a> TSProgressInfoLevel

「從 2002 版開始」<!--5932692-->  

指定此變數來控制工作順序進度視窗所顯示的資訊類型。 針對此變數使用下列值：

- `1`：將目前步驟與步驟總數包含在進度文字中。 例如，**2/10**。
- `2`：將目前步驟、步驟總數以及已完成的百分比包含在其中。 例如，**2/10 (完成20%)** 。
- `3`：將已完成的百分比包含在其中。 例如， **(完成20%)** 。

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a> TSUEFIDrive

用於 [變數] 欄位中的 FAT32 磁碟分割屬性。 當工作順序偵測到此變數時，即會準備轉換為 UEFI 的磁碟，然後重新啟動電腦。 如需詳細資訊，請參閱[管理將 BIOS 轉換為 UEFI 的工作順序步驟](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)。

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a> WorkingDirectory

*適用於[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)步驟。*

(input)

指定命令列動作的起始目錄。 指定的目錄名稱不可超過 255 個字元。

#### <a name="examples"></a>範例

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>已過時的變數

以下是已過時的變數：

- **OSDAllowUnsignedDriver**：部署 Windows Vista 和更新版本的作業系統時不使用
- **OSDBuildStorageDriverList**：僅適用於 Windows XP 和 Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**：只有部署 Windows XP 或 Windows Server 2003 時才需要
- **OSDInstallEditionIndex**：Windows Vista 之後的版本不需要
- **OSDPreserveDriveLetter**：如需詳細資訊，請參閱 [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> 這個工作順序變數已被取代。
>
> 在 OS 部署期間，Windows 安裝程式預設會決定要使用的最佳磁碟機代號 (通常是 C:)。

*先前的行為*：套用映像時，OSDPreserveDriveLetter 變數會決定工作順序是否要使用映像檔 (WIM) 中所擷取的磁碟機代號。 將此變數的值設定為 `false`，即可使用您在 [套用作業系統] 工作順序步驟中為 [目的地] 設定指定的位置。 如需詳細資訊，請參閱[套用 OS 映像](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。


## <a name="see-also"></a>請參閱

- [工作順序步驟](task-sequence-steps.md)
- [使用工作順序變數](using-task-sequence-variables.md)
- [自動化工作的規劃考量](../plan-design/planning-considerations-for-automating-tasks.md)
