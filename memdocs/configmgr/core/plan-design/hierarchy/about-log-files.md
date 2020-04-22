---
title: 關於檢視記錄檔
titleSuffix: Configuration Manager
description: 使用記錄檔，對 Configuration Manager 用戶端和站台系統的問題進行疑難排解。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6be23adc7ac082545bffeef59ed52d3455d9931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703746"
---
# <a name="about-log-files-in-configuration-manager"></a>關於 Configuration Manager 中的記錄檔

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中，用戶端和站台伺服器元件會在個別記錄檔中記錄處理程序資訊。 利用這些記錄檔中的資訊，可幫助您針對可能發生的問題進行疑難排解。 根據預設，Configuration Manager 會針對用戶端和伺服器元件啟用記錄。

本文提供有關 Configuration Manager 記錄檔的一般資訊。 其中包含要使用的工具、如何設定記錄檔，以及要在哪裡尋找記錄檔。 如需有關特定記錄檔的詳細資訊，請參閱[記錄檔參考](log-files.md)。


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a> 運作方式

Configuration Manager 中大部分程序會將操作資訊寫入該程序專用的記錄檔中。 這些記錄檔是透過 **.log** 或 **.lo_** 副檔名來識別。 Configuration Manager 會寫入 .log 檔，直到記錄檔到達大小上限。 記錄檔已滿時，.log 檔就會複製到同名的檔案，但副檔名為 .lo_，而程序或元件會繼續寫入 .log 檔中。 當 .log 檔再次達到其大小上限時，就會覆寫 .lo_ 檔，且此程序會重複。 某些元件會將日期和時間戳記附加至記錄檔名稱，並且保留 .log 副檔名，藉此建立記錄檔歷程記錄。


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a> 記錄檢視器工具

所有 Configuration Manager 記錄檔都是純文字，因此您可以使用 [記事本] 之類的任何文字讀取器來檢視這些檔案。 這些記錄檔會使用最適合檢視的唯一格式搭配下列其中一種特殊化工具：

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [支援中心記錄檢視器](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

若要檢視記錄檔，請使用 Configuration Manager 記錄檢視器工具 **CMTrace**。 其位於 Configuration Manager 來源媒體的 `\SMSSetup\Tools` 資料夾中。 CMTrace 工具會新增至所有 [軟體程式庫]中新增的開機映像內。 CMTrace 檢視工具會與 Configuration Manager 用戶端一起自動安裝。<!--1357971--> 如需詳細資訊，請參閱 [CMTrace](../../support/cmtrace.md)。

### <a name="onetrace"></a>OneTrace

從 1906 版開始，**OneTrace** 是支援中心的新記錄檢視器。 其運作方式與 CMTrace 類似，但包含改良功能。 如需詳細資訊，請參閱[支援中心 OneTrace](../../support/support-center-onetrace.md)。

### <a name="support-center-log-viewer"></a>支援中心記錄檢視器

**支援中心**包含新型記錄檢視器。 此工具取代 OneTrace 並提供可自訂的介面及索引標籤和可停駐視窗支援。 它有快速的簡報層，並可在數秒內載入大型的記錄檔。 如需詳細資訊，請參閱[支援中心記錄檢視器參考](../../support/support-center-ui-reference.md#bkmk_log-viewer)。

> [!Note]  
> 支援中心和 OneTrace 使用 Windows Presentation Foundation (WPF)。 此元件不適用於 Windows PE。 繼續在開機映像中，搭配工作順序部署使用 CMTrace。


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a> 設定記錄選項

您可以變更記錄檔的設定，例如詳細資訊層級、大小和歷程記錄。 有幾種方式可以變更這些設定：

- [在用戶端安裝期間](#bkmk_logoptions-clientprop)
- [使用 Configuration Manager Service Manager](#bkmk_logoptions-sm)
- [使用 Windows 登錄](#bkmk_logoptions-registry)
- [在 Configuration Manager 主控台中](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a> 在安裝用戶端期間設定記錄選項

您可以在安裝期間設定用戶端記錄檔的設定。 使用下列屬性：

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

如需詳細資訊，請參閱[用戶端安裝屬性](../../clients/deploy/about-client-installation-properties.md#clientMsiProps)。

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a> 使用 Configuration Manager Service Manager 設定記錄選項

您可以變更 Configuration Manager 儲存記錄檔所在位置及其大小。  

若要修改記錄檔大小、變更記錄檔的名稱和位置，或強制將多個元件寫入單一記錄檔，請執行下列步驟：  

#### <a name="modify-logging-for-a-component"></a>修改元件的記錄  

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [系統狀態]  ，然後選取 [站台狀態]  或 [元件狀態]  節點。  

2. 在功能區中，選取 [開始]  ，然後選取 [Configuration Manager Service Manager]  。  

3. Configuration Manager Service Manager 開啟時，連線至您要管理的站台。 如果未顯示您要管理的站台，請依序選取 [站台]  和 [連線]  ，然後輸入正確站台的站台伺服器名稱。  

4. 展開站台，然後根據您要管理之元件所在的位置，移至 [元件]  或 [伺服器]  。  

5. 在右側窗格中，選取一個或多個元件。  

6. 在 [元件]  功能表上，選取 [記錄]  。  

7. 在 [Configuration Manager 元件記錄]  對話方塊中，完成您選取的可用設定選項。  

8. 選取 [確定]  儲存設定。  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a> 使用 Windows 登錄設定記錄選項

<!-- SCCMDocs#992 -->
使用伺服器或用戶端上的 Windows 登錄來變更下列記錄選項：

- 詳細資訊層級
- 歷程記錄上限
- 大小上限

針對問題進行疑難排解時，您可以啟用 Configuration Manager 的詳細資訊記錄，以便在記錄檔中寫入額外的詳細資料。

> [!Warning]
> 這些設定的設定不正確可能會導致 Configuration Manager 記錄大量資訊，或完全不記錄任何資訊。 雖然這項資料可能有助於疑難排解，但在生產站台中變更這些值時，請務必謹慎。 請一律先在實驗室環境中測試這些變更。 可能發生過多記錄，讓您難以在記錄檔中尋找相關資訊。

對這些登錄設定進行變更之後，請重新啟動元件：

- 如果您變更用戶端設定，請重新啟動 **SMS Agent Host** 服務 (CcmExec)。
- 如果您變更伺服器設定，請重新啟動 **SMS Executive** 服務。

登錄設定會根據元件而有所不同：

- [用戶端和管理點](#bkmk_reg-client)
- [站台伺服器](#bkmk_reg-site)
- [站台系統角色](#bkmk_reg-role)
- [Configuration Manager 主控台](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a> 用戶端和管理點記錄選項

若要為用戶端或管理點站台系統上的所有元件設定記錄選項，請在下列 Windows 登錄機碼底下設定這些 **REG_DWORD** 值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Name  |值  |說明  |
|---------|---------|---------|
|LogLevel|`0`：詳細資訊<br>`1`：預設值<br>`2`：警告和錯誤<br>`3`：僅錯誤|要寫入至記錄檔的詳細資料層級。|
|LogMaxHistory|大於或等於零的任何整數，例如：<br>`0`：沒有歷程記錄<br>`1`：預設值|當記錄檔達到大小上限時，用戶端會將它重新命名以當作備份，並建立新的記錄檔。 指定要保留的舊版本數目。|
|LogMaxSize|大於或等於 10,000 的任何整數，例如：<br>250000|最大的記錄檔大小 (以位元組為單位)。 當記錄成長到指定大小時，用戶端會將它重新命名以當作歷程記錄檔案，並建立新檔案。 預設值為 250000 個位元組。|

> [!Note]  
> 請勿變更可能存在於此登錄機碼中的其他值。

如需進階偵錯，您也可以在下列 Windows 登錄機碼底下，加入此 **REG_SZ** 值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Name  |值  |說明  |
|---------|---------|---------|
|已啟用 | `True`：啟用偵錯記錄檔<br>`False`：停用偵錯記錄檔 |啟用偵錯記錄檔，以供疑難排解之用。|

此設定可讓用戶端記錄用於疑難排解的低階資訊。 請避免在生產站台中使用此設定。 可能發生過多記錄，讓您難以在記錄檔中尋找相關資訊。 解決問題之後，請務必關閉此設定。

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a> 站台伺服器記錄選項

您可以進行全域設定，或對 Configuration Manager 站台伺服器上的特定元件進行設定。

在下列 Windows 登錄機碼底下設定這些值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Name  |值  |類型  |說明
|---------|---------|---------|---------|
|SqlEnabled| `1`：啟用 SQL 追蹤<br> `0`：停用 SQL 追蹤 |REG_DWORD|將 SQL 追蹤記錄加入至所有站台伺服器記錄檔。|
|ArchiveEnabled| `1`：啟用記錄檔封存<br> `0`：停用記錄檔封存 | REG_DWORD |將站台伺服器記錄檔封存到不同的位置，以保留歷程記錄。|
|ArchivePath| 有效的資料夾路徑，例如 `C:\Logs\Archive` | REG_SZ |封存站台伺服器記錄檔的路徑。|

僅啟用 SQL 追蹤以供疑難排解之用。 請避免在生產站台中使用它。 可能發生過多記錄，讓您難以在記錄檔中尋找相關資訊。 解決問題之後，請務必關閉此設定。

> [!Note]  
> 請勿變更可能存在於此登錄機碼中的其他值。

若要為特定的元件設定記錄選項，請在下列 Windows 登錄機碼底下設定這些 **REG_DWORD** 值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Name  |值  |說明  |
|---------|---------|---------|
|LoggingLevel|`0`：詳細資訊<br>`1`：預設值<br>`2`：警告和錯誤<br>`3`：僅錯誤|要寫入至記錄檔的詳細資料層級。|
|LogMaxHistory|大於或等於零的任何整數，例如：<br>`0`：沒有歷程記錄<br>`1`：預設值|當記錄檔達到大小上限時，伺服器會將它重新命名以當作備份，並建立新的記錄檔。 指定要保留的舊版本數目。|
|MaxFileSize|大於或等於 10,000 的任何整數，例如：<br>250000|最大的記錄檔大小 (以位元組為單位)。 當記錄成長到指定大小時，用戶端會將它重新命名以當作歷程記錄檔案，並建立新檔案。 預設值為 250000 個位元組。|
|DebugLogging| `1`：啟用偵錯記錄檔<br>`0`：停用偵錯記錄檔 |啟用偵錯記錄檔，以供疑難排解之用。|

DebugLogging 設定可讓伺服器記錄用於疑難排解的低階資訊。 請避免在生產站台中使用此設定。 可能發生過多記錄，讓您難以在記錄檔中尋找相關資訊。 解決問題之後，請務必關閉此設定。

> [!Note]  
> 請勿變更可能存在於此登錄機碼中的其他值。

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a> 站台系統角色記錄選項

您可以進行全域設定，或對站台系統上，裝載 Configuration Manager 伺服器角色的特定元件進行設定。

若要為特定的元件設定記錄選項，請在下列 Windows 登錄機碼底下設定這些 **REG_DWORD** 值：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

例如，針對發佈點角色：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Name  |值  |說明  |
|---------|---------|---------|
|LogLevel|`0`：詳細資訊<br>`1`：預設值<br>`2`：警告和錯誤<br>`3`：僅錯誤|要寫入至記錄檔的詳細資料層級。|
|LogMaxHistory|大於或等於零的任何整數，例如：<br>`0`：沒有歷程記錄<br>`1`：預設值|當記錄檔達到大小上限時，伺服器會將它重新命名以當作備份，並建立新的記錄檔。 指定要保留的舊版本數目。|
|LogMaxSize|大於或等於 10,000 的任何整數，例如：<br>250000|最大的記錄檔大小 (以位元組為單位)。 當記錄檔成長到指定的大小時，伺服器會將它重新命名以當作歷程記錄檔案，並建立新檔案。 預設值為 250000 個位元組。|

> [!Note]  
> 請勿變更可能存在於此登錄機碼中的其他值。

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a> Configuration Manager 主控台記錄選項

若要變更 Configuration Manager 主控台的 AdminUI.log 詳細資訊層級，請使用下列程序：

1. 在 XML 編輯器 (如 [記事本]) 中，開啟主控台設定檔 **Microsoft.ConfigurationManagement.exe.config**。 預設設定檔位於下列位置：`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. 在 **system.diagnostics** > **sources** > **source** 元素底下，將 **switchValue** 屬性從 `Error` 變更為 `Verbose`。 例如：

    原始：`<source name="SmsAdminUISnapIn" switchValue="Error">`新增：`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. 儲存檔案，然後重新啟動主控台。

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a> 在 Configuration Manager 主控台中設定記錄選項

<!-- 4433455 -->

從 1910 版開始，從主控台啟用或停用用戶端或集合的詳細資訊記錄：

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，選取 [裝置]  節點，然後選擇目標裝置。

1. 在功能區的 [常用]  索引標籤上 [裝置]  群組中，選取 [用戶端診斷]  。 選擇其中一個可用的動作。

如需詳細資訊，請參閱[用戶端診斷](../../clients/manage/client-notification.md#client-diagnostics)。

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a> 尋找記錄檔

Configuration Manager 和相依元件會將記錄檔儲存在不同的位置。 這些位置取決於建立記錄檔的程序以及環境的設定。

下列位置是預設值。 如果您在環境中自訂安裝目錄，實際的路徑可能會有所不同。

- 用戶端：`C:\Windows\CCM\logs`
- 伺服器：`C:\Program Files\Microsoft Configuration Manager\Logs`
- 管理點：`C:\SMS_CCM\Logs`
- Configuration Manager 主控台：`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog`
- IIS：`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>工作順序記錄檔位置

工作順序記錄檔 **smsts.log** 的位置會依據工作順序的階段而有所不同：

- 在 Windows PE 中，於[格式化和分割磁碟](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk)步驟之前：`X:\Windows\temp\smstslog\smsts.log` (X 是 Windows PE RAM 磁碟機)
- 在 Windows PE 中，於**格式化和分割磁碟**步驟之後：`X:\smstslog\smsts.log`，然後在磁碟機就緒時複製到 `C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- 在新的 Windows 作業系統中安裝用戶端之前：`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- 在 Windows 中安裝用戶端之後：`C:\Windows\CCM\Logs\smstslog\smsts.log`
- 在 Windows 中，於工作順序完成之後：`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> 唯讀工作順序變數 [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) 一律包含目前記錄檔的路徑。


## <a name="see-also"></a>請參閱

- [記錄檔參考](log-files.md)

- [支援中心 OneTrace](../../support/support-center-onetrace.md)

- [支援中心記錄檔檢視器](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
