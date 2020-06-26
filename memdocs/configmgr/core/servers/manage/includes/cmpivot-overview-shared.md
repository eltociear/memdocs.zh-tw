---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 06/05/2020
ms.openlocfilehash: 3672127798b66d857b4a1dbd5014c02dfed8a7ee
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84466825"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>查詢

查詢可用於搜尋字詞、找出趨勢、分析模式及依據您的資料提供其他許多見解。 CMPivot 會針對表格式運算式陳述式使用 [Azure 記錄分析](https://docs.microsoft.com/azure/kusto/query)資料流程模型的子集。 表格式運算式陳述式的典型結構是用戶端實體和表格式資料運算子 (例如篩選條件和投影) 的組合。 此組合是以直立線字元 (|) 表示，可為陳述式提供一般形式，進而以視覺方式表示表格式資料的流程 (從左至右)。 每個運算子都會接受「來自直立線」的表格式資料集，以及來自運算子主體的其他輸入 (包括其他表格式資料集)，然後將表格式資料集發出至緊接在後的下一個運算子：`entity | operator1 | operator2 | ...`

在下列範例中，實體是 `CCMRecentlyUsedApplications` (目前所用應用程式的參考)，而運算子為 where (其會依據幾個以記錄為根據的述詞，從其輸入中篩選掉記錄)：

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%'
```

## <a name="entities"></a>實體

實體是可從用戶端進行查詢的物件。 我們目前支援下列實體：


|實體|說明|
|---|---|
|AadStatus|Azure Active Directory 的狀態|
|Administrators|本機系統管理員群組的成員|
|AppCrash|近期應用程式損毀報告|
|AppVClientApplication|AppV 用戶端應用程式|
|AppVClientPackage|AppV 用戶端套件|
|AutoStartSoftware|隨著作業系統自動啟動或緊接其後啟動的軟體|
|基板|基板|
|電池|電池|
|Bios|系統 BIOS 資訊|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|BitLocker 加密詳細資料|
|BitLockerPolicy|BitLocker 原則|
|BootConfiguration|開機設定|
|BrowserHelperObject|瀏覽器協助程式物件|
|BrowserUsage|瀏覽器使用量|
|CcmLog()|Ccm 記錄檔 24 小時內的行 (預設)|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|最近使用過的應用程式|
|CCMWebAppInstallInfo|Web 應用程式|
|CDROM|CDROM 光碟機|
|ClientEvents|用戶端事件|
|ComputerSystem|電腦系統|
|ComputerSystemEx|電腦系統 Ex|
|ComputerSystemProduct|電腦系統產品|
|ConnectedDevice|連線的裝置|
|連線|連入或連出裝置的作用中 TCP 連線|
|桌面|桌面|
|DesktopMonitor|桌上型監視器|
|裝置|裝置的基本資訊|
|磁碟|在執行 Windows 的電腦系統上的本機存放裝置資訊|
|DMA|DMA|
|DMAChannel|DMA 通道|
|DriverVxD|驅動程式 - VxD|
|EmbeddedDeviceInformation|內嵌的裝置資訊|
|環境|環境|
|EPStatus|電腦上反惡意程式碼軟體的狀態|
|EventLog()|事件記錄中 24 小時內的事件 (預設)|
|File()|特定檔案的相關資訊|
|FileShare|作用中檔案共用資訊|
|韌體|韌體|
|IDEController|IDE 控制器|
|InstalledExecutable|已安裝的可執行檔|
|InstalledSoftware|裝置上安裝的應用程式|
|IPConfig|取得網路設定，包括可使用的介面、IP 位址與 DNS 伺服器|
|IRQTable|IRQ 表|
|鍵盤|鍵盤|
|LoadOrderGroup|載入順序群組|
|LogicalDisk|邏輯磁碟|
|MDMDevDetail|裝置資訊|
|記憶體|記憶體|
|數據機|數據機|
|主機板|主機板|
|NetworkAdapter|網路介面卡|
|NetworkAdapterConfiguration|網路介面卡設定|
|NetworkClient|網路用戶端|
|NetworkLoginProfile|網路登入設定檔|
|NTEventlogFile|NT Eventlog 檔案|
|Office365ProPlusConfigurations|Office 365 專業增強版設定|
|OfficeAddin|Office 增益集|
|OfficeClientMetric|Office 用戶端度量|
|OfficeDeviceSummary|Office 裝置摘要|
|OfficeDocumentMetric|Office 文件計量|
|OfficeDocumentSolution|Office 文件解決方案|
|OfficeMacroError|Office 巨集錯誤|
|OfficeProductInfo|Office 產品資訊|
|OfficeVbaRuleViolation|違反 Office VBA 規則|
|OfficeVbaSummary|Office VBA 掃描摘要|
|OperatingSystem|作業系統|
|OperatingSystemEx|作業系統 EX|
|OperatingSystemRecoveryConfiguration|作業系統復原設定|
|OptionalFeature|選用功能|
|OS|作業系統的基本資訊|
|PageFileSetting|分頁檔案設定|
|ParallelPort|平行埠|
|分割區|磁碟分割|
|PCMCIAController|PCMCIA 控制器|
|PhysicalDisk|PhysicalDisk|
|PhysicalMemory|實體記憶體|
|PNPDEVICEDRIVER|PNP 裝置驅動程式|
|PointingDevice|指標裝置|
|PortableBattery|可攜式電池|
|連接埠|連接埠|
|PowerCapabilities|電池容量|
|PowerClientOptOutSettings|電源管理排除設定|
|PowerConfigurations|電源設定|
|PowerManagementDaily|電源管理每日資料|
|PowerManagementInsomniaReasons|電源無法休眠原因|
|PowerManagementMonthly|電源管理每月資料|
|PowerSettings|電源設定|
|PrinterConfiguration|印表機設定|
|PrinterDevice|印表機裝置|
|PrintJobs|列印工作|
|程序|作業系統上的程序|
|ProcessModule()|指定程序所載入的模組|
|處理器|處理器|
|ProtectedVolumeInformation|受保護的磁碟區資訊|
|通訊協定|通訊協定|
|QuickFixEngineering|快速檢修|
|SCSIController|SCSI 控制器|
|SerialPortConfiguration|序列埠設定|
|SerialPorts|序列埠|
|ServerFeature|伺服器功能|
|Service|在執行 Windows 的電腦系統上的服務|
|服務|服務|
|共用|共用|
|SMBConfig|裝置的 SMB 設定|
|SMSAdvancedClientPorts|Configuration Manager 用戶端連接埠|
|SMSAdvancedClientSSLConfigurations|Configuration Manager 用戶端 SSL 設定|
|SMSAdvancedClientState|Configuration Manager 用戶端狀態|
|SMSDefaultBrowser|預設瀏覽器|
|SMSSoftwareTag|軟體標記|
|SMSWindows8Application|Windows 應用程式|
|SMSWindows8ApplicationUserInfo|Windows 應用程式使用者資訊|
|SoftwareShortcut|軟體捷徑|
|SoftwareUpdate|適用於但未安裝在裝置上的軟體更新|
|SoundDevices|音效裝置|
|SWLicensingProduct|軟體授權產品|
|SWLicensingService|軟體授權服務|
|SystemAccount|系統帳戶|
|SystemBootData|系統開機資料|
|SystemBootSummary|系統開機摘要|
|SystemConsoleUsage|系統主控台使用方式|
|SystemConsoleUser|系統主控台使用者|
|SystemDevices|系統裝置|
|SystemDrivers|系統驅動程式|
|SystemEnclosure|系統機殼|
|TapeDrive|磁帶機|
|TimeZone|時區|
|TPM|TPM|
|TPMStatus|TPM 狀態|
|TSIssuedLicense|TS 核發的授權|
|TSLicenseKeyPack|TS 授權金鑰包|
|UninterruptiblePowerSupply|不斷電供應系統|
|USBController|USB 控制器|
|USBDevice|USB 裝置|
|User|與裝置之間有作用中連線的使用者帳戶|
|USMFolderRedirectionHealth|資料夾重新導向健康情況|
|USMUserProfile|使用者設定檔健康情況|
|VideoController|視訊控制卡|
|VirtualMachine|虛擬機器|
|VirtualMachine64|虛擬機器 (64)|
|磁碟區|磁碟區|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Windows Update 代理程式版本|
|WinEvent()|Windows 事件記錄中 24 小時內的事件 (預設)|
|WriteFilterState|寫入篩選器狀態|

## <a name="table-operators"></a>資料表運算子

資料表運算子可用來篩選、彙總及轉換資料流。 目前支援下列運算子：

|資料表運算子|說明|
|---|---|
|count|傳回資料表，其中有包含記錄數目的單一記錄|
|distinct|產生資料表，其中以不同方式結合提供的輸入資料表資料列|
|join|透過比對相同裝置的資料列，合併兩個資料表的資料列以形成新資料表|
|order by|依據一或多個資料列，排序輸入資料表的資料列|
|project|選取要包含的資料行、重新命名或置放，然後插入新的計算資料行|
|summarize|產生可彙總輸入資料表內容的資料表|
|take|最多傳回指定的資料列數目|
|top|傳回依指定資料行排序的前 N 個記錄|
|其中|將資料表篩選為滿足述詞的資料列子集|

## <a name="scalar-operators"></a>純量運算子

下表摘要說明運算子：

|運算子|說明|範例
|---|---|---|
|==|等於|`1 == 1, 'aBc' == 'AbC'`|
|!=|不等於|`1 != 2, 'abc' != 'abcd'`|
|< |小於|`1 < 2, 'abc' < 'DEF'`|
|> |大於|`2 > 1, 'xyz' > 'XYZ'`|
|<=|小於或等於|`1 <= 2, 'abc' <= 'abc'`|
|>=|大於或等於|`2 >= 1, 'abc' >= 'ABC'`|
|+|新增|`2 + 1, now() + 1d`|
|-|減去|`2 - 1, now() - 1h`|
|*|乘以|`2 * 2`|
|/|除以|`2 / 1`|
|%|模數|`2 % 1`|
|like|左邊 (LHS) 包含右邊 (RHS) 的相符項目|`'abc' like '%B%'`|
|!like|LHS 不包含 RHS 的相符項目|`'abc' !like '_d_'`|
|包含|RHS 作為 LHS 的子序列發生|`'abc' contains 'b'`|
|!contains|RHS 未在 LHS 中發生|`'team' !contains 'i'`|
|startswith|RHS 是 LHS 的起始子序列|`'team' startswith 'tea'`|
|!startswith|RHS 不是 LHS 的起始子序列|`'abc' !startswith 'bc'`|
|endswith|RHS 是 LHS 的右子序列|`'abc' endswith 'bc'`|
|!endswith|RHS 不是 LHS 的右子序列|`'abc' !endswith 'a'`|
|及|True 若且唯若 RHS 與 LHS 均為 true|`(1 == 1) and (2 == 2)`|
|或|True 若且唯若 RHS 或 LHS 為 true|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>彙總函式

彙總函式可搭配 summarize 資料表運算子使用，以計算彙總值。 目前支援下列彙總函式：

|函式|說明|
|---|---|
|avg()|傳回整個群組的值平均|
|count()|傳回每個彙總群組的記錄計數|
|countif()|傳回述詞評估為 true 的資料列計數|
|dcount()|傳回群組中的相異值數目|
|max()|傳回整個群組的最大值|
|min()|傳回整個群組的最小值|
|percentile()|返回由運算式定義之母體的指定最近百分位數估計值|
|sum()|傳回整個群組的值加總|
|sumif()|傳回述詞評估為 True 的運算式總和|

## <a name="scalar-functions"></a>純量函式

純量函式可以在運算式中使用。 目前支援下列純量函式：

|函式|說明|
|---|---|
|ago()|從目前的 UTC 時鐘時間減去所指定時間範圍|
|bin()|將值無條件捨去為日期時間的數字，並為指定間隔大小的倍數|
|case()|評估述詞的清單，並傳回符合述詞的第一個結果運算式|
|datetime_add()|計算新的日期時間：將乘以指定數量的指定日期部分加至指定的日期時間|
|datetime_diff()|計算兩個日期時間值之間的差異|
|iif()|評估第一個引數並傳回第二個或第三個引數的值，取決於述詞評估為 True (第二個) 或 False (第三個)|
|indexof()|函式回報輸入字串中第一次出現之指定字串以零起始的索引|
|isnotnull()|評估其唯一引數，並傳回布林值，指出引數是否會評估為非 null 值|
|isnull()|評估其唯一引數，並傳回布林值，指出引數是否會評估為 null 值|
|now()|傳回目前的 UTC 時鐘時間|
|strcat()|串連 1 到 64 個引數|
|strlen()|傳回輸入字串的長度 (以字元為單位)|
|substring()|從某個索引開始到字串結尾的來源字串中擷取子字串|
|tostring()|將輸入轉換成字串表示法|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a> Configuration Manager 中 CMPivot 的其他實體、運算子和函式

> [!Important]
> 當您從 Microsoft 端點管理員系統管理中心執行 CMPivot 時，不支援下列項目。

|類型|項目|說明|
|--|--|---|
|實體|AccountSID|帳戶 SID|
|實體|FileContent()|特定檔案的內容|
|實體|NAPClient|NAP 用戶端|
|實體|NAPSystemHealthAgent|NAP 系統健全狀況代理程式|
|實體|Registry()|特定登錄機碼的所有值<!--7371183-->|
|資料表運算子|轉譯|將結果轉譯為圖形輸出|
