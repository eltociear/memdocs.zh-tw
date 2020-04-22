---
title: 如何使用工作順序變數
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 工作順序中使用變數。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c043cfabc411dbd5ae4984110fc2904d37669300
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700206"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>如何在 Configuration Manager 中使用工作順序變數

適用於：  Configuration Manager (最新分支)

 Configuration Manager 之 OS 部署功能中的工作順序引擎使用許多變數來控制其行為。 這些變數可用來：

- 針對步驟設定條件  
- 變更特定步驟的行為  
- 在指令碼中使用以執行更複雜的動作  

如需所有可用工作順序變數的參考，請參閱[工作順序變數](task-sequence-variables.md)。

## <a name="types-of-variables"></a><a name="bkmk_types"></a> 變數類型

變數類型有數種：  

- [內建](#bkmk_built-in)  
- [動作](#bkmk_action)  
- [自訂](#bkmk_custom)  
- [唯讀](#bkmk_read-only)  
- [陣列](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a> 內建變數

內建變數可提供工作順序執行環境的相關資訊。 其值可供整個工作順序使用。 一般而言，工作順序引擎會在執行任何步驟之前，先將內建變數初始化。

例如，`_SMSTSLogPath` 是指定 Configuration Manager 記錄檔寫入路徑的環境變數。 任何工作順序步驟都可以存取這個環境變數。

工作順序會在每個步驟之前評估一些變數。 例如，`_SMSTSCurrentActionName` 會列出目前步驟的名稱。

### <a name="action-variables"></a><a name="bkmk_action"></a> 動作變數

工作順序動作變數會指定單一工作順序步驟所使用的組態設定。 根據預設，步驟會在執行之前，將其設定初始化。 只有當相關聯的工作順序步驟執行時，才能使用這些設定。 工作順序會在執行步驟之前，將動作變數值新增至環境。 接著，在步驟執行之後，它就會從環境中移除該值。

例如，您將 [執行命令列]  步驟新增到工作順序中。 此步驟包含一個 [開始位置]  屬性。 工作順序會將此屬性的預設值儲存成 `WorkingDirectory` 變數。 工作順序會先將此值初始化，然後才執行 [執行命令列]  步驟。 在此步驟執行時，請從 `WorkingDirectory` 值存取 [開始位置]  屬性值。 步驟完成之後，工作順序會從環境移除 `WorkingDirectory` 變數的值。 如果工作順序包含另一個 [執行命令列]  步驟，其會將新的 `WorkingDirectory` 變數初始化。 屆時，工作順序會將該變數設定為目前步驟的起始值。 如需詳細資訊，請參閱 [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)。  

動作變數的「預設」  值會在步驟執行時存在。 如果您設定「新的」  值，它將可供工作順序中的多個步驟使用。 如果您覆寫預設值，新值則會留在環境中。 此新值會覆寫工作順序中其他步驟的預設值。 例如，您新增 [設定工作順序變數]  步驟作為工作順序的第一個步驟。 此步驟會將 `WorkingDirectory` 變數設定為 `C:\`。 工作順序中的所有 [執行命令列]  步驟都會使用新的起始目錄值。  

有些工作順序步驟會將特定動作變數標示為 *output*。 工作順序中稍後的動作會讀取這些輸出變數。

> [!Note]  
> 並非所有工作順序步驟都具有動作變數。 例如，雖然有與 [啟用 BitLocker]  動作相關聯的變數，但沒有與 [停用 BitLocker]  動作相關聯的變數。  

### <a name="custom-variables"></a><a name="bkmk_custom"></a> 自訂變數

這些是 Configuration Manager 不會建立的任何變數。 請將您自己的變數初始化，以當作條件使用、在命令列中使用，或在指令碼中使用。

當您為新工作順序變數指定名稱時，請依照下列指引進行：  

- 工作順序變數名稱可以包含字母、數字、底線字元 (`_`) 和連字號 (`-`)。  

- 工作順序變數名稱的最小長度為 1 個字元，最大長度為 256 個字元。  

- 使用者定義的變數開頭必須是字母 (`A-Z` 或 `a-z`)。  

- 使用者定義的變數名稱開頭不可以是底線字元。 只有唯讀工作順序變數的開頭會是底線字元。  

- 工作順序變數名稱不區分大小寫。 例如，`OSDVAR` 和 `osdvar` 是相同的工作順序變數。  

- 工作順序變數名稱的開頭或結尾不可以是空格。 此外，它們也不能包含內嵌的空格。 工作順序會忽略在變數名稱開頭或結尾的所有空格。  

針對您可建立的工作順序變數數目，並無任何已設定的限制。 不過，變數的數目則受限於工作順序環境的大小。 工作順序環境的大小總計限制為 32 MB。  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a> 唯讀變數

您無法變更某些變數的值，這些是唯讀變數。 通常名稱的開頭會是底線字元 (`_`)。 工作順序會使用它們來進行其作業。 唯讀變數是可在工作順序環境中看見的變數。

這些變數在指令碼或命令列中相當有用。 例如，執行命令列並透過管線將輸出傳送到含有其他記錄檔之 `_SMSTSLogPath` 中的記錄檔。

> [!NOTE]  
> 工作順序中的步驟可以讀取唯讀工作順序變數，但無法設定這些變數。 例如，請使用唯讀變數作為 [執行命令列]  步驟之命令列的一部分。 您無法使用 [設定工作順序變數]  步驟來設定唯讀變數。  

### <a name="array-variables"></a><a name="bkmk_array"></a> 陣列變數

工作順序會將某些變數儲存成陣列。 陣列中的每個項目都代表單一物件的設定。 當裝置有多個物件需要設定時，請使用這些變數。 下列工作順序步驟會使用陣列變數：

- [套用網路設定](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [格式化和分割磁碟](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a> 如何設定變數

針對自訂變數或非唯讀變數，有數種方法可將變數初始化並設定其值：  

- [設定工作順序變數](#bkmk_set-ts-step)步驟
- [設定動態變數](#bkmk_set-dyn-step)步驟
- [執行 PowerShell 指令碼](#bkmk_run-ps)步驟
- [集合和裝置變數](#bkmk_set-coll-var)  
- [TSEnvironment COM 物件](#bkmk_set-com)  
- [啟動前置命令](#bkmk_set-prestart)  
- [工作順序精靈](#bkmk_set-tswiz)
- [工作順序媒體精靈](#bkmk_set-media)  

請使用與建立變數時相同的方法，從環境中刪除變數。 若要刪除變數，請將變數值設定為空字串。  

您可以將方法合併，以針對相同順序將工作順序變數設定為不同的值。 例如，使用工作順序編輯器來設定預設值，然後使用指令碼來設定自訂值。

如果您透過不同的方法設定相同的變數，工作順序引擎將會使用以下順序：  

1. 它會先評估集合變數。  

2. 裝置特定變數會覆寫集合上設定的相同變數。  

3. 在工作順序期間透過任何方法設定的變數優先順序會高於集合或裝置變數。  

### <a name="general-limitations-for-task-sequence-variable-values"></a>工作序列變數值的一般限制

- 工作序列變數值不能超過 4,000 個字元。  

- 您無法變更唯讀的工作序列變數。 唯讀變數名稱的開頭會是底線字元 (`_`)。  

- 視值的用法而定，工作順序變數值可區分大小寫。 在大多數情況下，工作順序變數值不區分大小寫。 包含密碼的變數會區分大小寫。  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a> 設定工作順序變數

您可以在工作順序中使用此步驟，以將單一變數設定為單一值。

如需詳細資訊，請參閱[設定工作順序變數](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)。

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a> 設定動態變數

您可以在工作順序中使用此步驟，以設定一或多個工作順序變數。 您需在此步驟中定義規則，以決定要使用哪些變數和值。

如需詳細資訊，請參閱[設定動態變數](task-sequence-steps.md#BKMK_SetDynamicVariables)。

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a> 執行 PowerShell 指令碼

<!-- 6315548 -->

您可以在工作順序中使用此步驟，以使用 PowerShell 指令碼設定工作順序變數。

您可以從套件指定指令碼名稱，或直接在步驟中輸入 PowerShell 指令碼。 然後使用步驟屬性**輸出至工作順序變數**，將指令碼輸出儲存至自訂工作順序變數。

如需此步驟的詳細資訊，請參閱[執行 PowerShell 指令碼](task-sequence-steps.md#BKMK_RunPowerShellScript)。

> [!NOTE]
> 您也可以使用 PowerShell 指令碼，以 **TSEnvironment** 物件來設定一或多個變數。 如需詳細資訊，請參閱 Configuration Manager SDK 中的[如何在執行中的工作順序中使用變數](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)。

#### <a name="example-scenario-with-run-powershell-script-step"></a>執行 PowerShell 指令碼步驟的範例案例

您的環境中有多個國家/地區的使用者，因此您想要查詢 OS 語言，將其設定為多語言特定 [套用 OS]  步驟的條件。

1. 在 [套用 OS]  步驟之前，將 [執行 PowerShell 指令碼]  的執行個體新增至工作順序中。

1. 使用選項**輸入 PowerShell 指令碼**，以指定下列命令：

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    如需 Cmdlet 的詳細資訊，請參閱 [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture) \(英文\)。 如需雙字母 ISO 語言名稱的詳細資訊，請參閱 [ISO 639-1 代碼清單](https://wikipedia.org/wiki/List_of_ISO_639-1_codes) \(英文\)。

1. 如需**輸出至工作順序變數**的選項，請指定 `CurrentOSLanguage`。

    ![[執行 PowerShell 指令碼] 步驟範例的螢幕擷取畫面](media/run-powershell-script-example-language.png)

1. 在英文版映像的 [套用 OS]  步驟上，建立下列條件：`Task Sequence Variable CurrentOSLanguage equals "en"`

    ![[套用 OS] 步驟上範例條件的螢幕擷取畫面](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > 如需如何在步驟上建立條件的詳細資訊，請參閱[如何存取變數 - 步驟條件](#bkmk_access-condition)。

1. 儲存及部署工作順序。

當 [執行 PowerShell 指令碼]  步驟在英文版 Windows 的裝置上執行時，此命令會傳回值 `en`。 然後，其會將該值儲存到自訂變數中。 當英文版映像的 [套用 OS]  步驟在同一部裝置上執行時，條件會評估為 true。 如果您有多個不同語言之 [套用 OS]  步驟的執行個體，則工作順序會以動態方式執行符合 OS 語言的步驟。

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a> 集合和裝置變數

您可以為裝置與集合定義自訂工作順序變數。 您為裝置定義的變數稱為個別裝置工作順序變數。 針對集合所定義的變數會參照為個別集合的工作順序變數。 如果發生衝突，則個別裝置變數的優先順序會高於個別集合變數。 這個行為表示指派至特定裝置的工作順序變數，其優先順序會自動高於指派至集合 (其中包含裝置) 的變數。  

例如，XYZ 裝置是 ABC 集合的成員。 您將值為 1 的 MyVariable 指派給 ABC 集合。 您同時也將值為 2 的 MyVariable 指派給 XYZ 裝置。 指派給 XYZ 的變數，其優先順序會高於指派給 ABC 集合的變數。 當具有此變數的工作順序在 XYZ 上執行時，MyVariable 的值會是 2。

您可以隱藏個別裝置與個別集合變數，讓這些變數不會顯示在 Configuration Manager 主控台中。 當您使用 [不在 Configuration Manager 主控台中顯示此值]  選項時，主控台中就不會顯示變數的值。 工作順序執行時，仍可使用該變數。 如果您已不再想要隱藏這些值，請先將它們刪除。 然後重新定義變數，但不選取隱藏它們的選項。  

> [!WARNING]  
> [不要在 Configuration Manager 主控台中顯示此值]  設定僅適用於 Configuration Manager 主控台。 變數的值仍會顯示在工作順序記錄檔 (**smsts.log**) 中。

您可以在主要站台或是管理中心網站管理個別裝置的變數。 就一部裝置而言，Configuration Manager 不支援超過 1,000 個指派的變數。  

> [!IMPORTANT]  
> 針對工作順序使用個別集合的變數時，請考量下列行為：  
>
> - 一律會複寫整個階層中對集合的變更。 您對集合變數進行的任何變更不只會套用到目前站台的成員，還會套用到整個階層集合的所有成員。  
>  
> - 當您刪除集合時，此動作也會刪除您為集合設定的工作順序變數。  

#### <a name="create-task-sequence-variables-for-a-device"></a>建立「裝置」  的工作順序變數

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [裝置]  節點。  

2. 選取目標裝置，然後選取 [內容]  。  

3. 在 [內容]  對話方塊中，按一下 [變數]  索引標籤。  

4. 針對您想要建立的每個變數，選取 [新增]  圖示。 指定工作順序變數的 [名稱]  和 [值]  。 如果您想要隱藏變數，使其不顯示在 Configuration Manager 主控台中，請選取 [不在 Configuration Manager 主控台中顯示此值]  選項。  

5. 將所有變數都新增至裝置屬性之後，選取 [確定]  。  

#### <a name="create-task-sequence-variables-for-a-collection"></a>建立「集合」  的工作順序變數

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選擇 [裝置集合]  節點。 選取目標集合，然後選擇 [內容]  。  

2. 在 [內容]  對話方塊中，切換到 [集合變數]  索引標籤。  

3. 針對您想要建立的每個變數，選取 [新增]  圖示。 指定工作順序變數的 [名稱]  和 [值]  。 如果您想要隱藏變數，使其不顯示在 Configuration Manager 主控台中，請選取 [不在 Configuration Manager 主控台中顯示此值]  選項。  

4. 視需要指定評估工作順序變數時，Configuration Manager 所要使用的優先順序。  

5. 將所有變數都新增至集合內容之後，選取 [確定]  。  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a> TSEnvironment COM 物件

若要使用來自指令碼的變數，請使用 **TSEnvironment** 物件。

如需詳細資訊，請參閱 Configuration Manager SDK 中的[如何在執行中的工作順序中使用變數](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)。

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a> 啟動前置命令

啟動前置命令是在使用者選取工作順序之前，在 Windows PE 中執行的指令碼或可執行檔。 啟動前置命令可以查詢變數，或是提示使用者輸入資訊，然後將其儲存在環境中。 請使用 [TSEnvironment](#bkmk_set-com) COM 物件，以從啟動前置命令讀取和寫入變數。

如需詳細資訊，請參閱[工作順序媒體的啟動前置命令](prestart-commands-for-task-sequence-media.md)。

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a> 工作順序精靈

從 1906 版開始，當您在 [工作順序精靈] 視窗選取工作順序後，用於編輯工作順序變數的頁面會包含 [編輯]  按鈕。 您可以使用可存取的鍵盤快速鍵來編輯變數。 這項變更能協助解決無法使用滑鼠時所產生的問題。<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a> 工作順序媒體精靈

您可以針對從媒體執行的工作順序指定變數。 使用媒體來部署 OS 時，您需新增工作順序變數，並在建立媒體時指定其值。 變數及其值會儲存在媒體上。  

> [!NOTE]  
> 工作順序會儲存在獨立媒體上。 然而，其他所有類型的媒體如已預先設置的媒體，會從管理點擷取工作順序。  

從媒體執行工作順序時，您可以在精靈的 [自訂]  頁面上新增變數。

在每個集合或每部電腦變數的位置使用媒體變數。 如果從媒體執行工作順序，則不會套用及使用個別電腦和個別集合變數。  

> [!TIP]  
> 工作順序會將套件識別碼和啟動前置命令列寫入到執行 Configuration Manager 主控台之電腦上的 **CreateTSMedia.log** 檔案中。 此記錄檔會包含任何工作順序變數的值。 請檢閱這個記錄檔來驗證工作順序變數的值。  

如需詳細資訊，請參閱[建立工作順序媒體](../deploy-use/create-task-sequence-media.md)。

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a> 如何存取變數

在您使用前一節的其中一個方法來指定變數及其值之後，請在工作順序中使用它。 例如，存取內建工作順序變數的預設值，或將步驟設定為以變數值為依據的條件性步驟。  

請使用下列方法來存取工作順序環境中的變數值：

- [在步驟中使用](#bkmk_access-step)  
- [步驟條件](#bkmk_access-condition)  
- [自訂指令碼](#bkmk_access-script)  
- [Windows 安裝程式回應檔案](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a> 在步驟中使用

您可以為工作順序步驟中的設定指定變數值。 請在工作順序編輯器中編輯步驟，然後指定變數名稱作為欄位值。 以百分比符號 (`%`) 括住變數名稱。

例如，請使用變數名稱作為 [執行命令列]  步驟之 [命令列]  欄位的一部分。 以下命令列會將電腦名稱寫入到文字檔中。

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a> 步驟條件

您可以在步驟或群組上，使用內建或自訂的工作順序變數作為條件的一部分。 工作順序會在執行步驟或群組之前，先評估變數值。

若要新增會評估變數值的條件，請執行下列步驟：  

1. 在工作順序編輯器中，選取您想要新增條件的步驟或群組。  

2. 切換至步驟或群組的 [選項]  索引標籤。 按一下 [新增條件]  ，然後選取 [工作順序變數]  。  

3. 在 [工作順序變數]  對話方塊方塊中，指定下列設定：  

    - **變數**：變數的名稱。 例如 `_SMSTSInWinPE`。  

    - **條件**：用以評估變數值的條件。 例如，[等於]  。  

    - **值**：要檢查的變數值。 例如 `false`。  

上述三個範例可構成一個常見的條件，用來測試工作順序是否是從 Windows PE 中的開機映像執行的：

> **工作順序變數** `_SMSTSInWinPE equals "false"`

請參閱預設工作順序範本之 [擷取檔案和設定]  群組上的這個條件，以安裝現有的 OS 映像。

如需有關條件的詳細資訊，請參閱[工作順序編輯器 - 條件](task-sequence-editor.md#bkmk_conditions)。

### <a name="custom-script"></a><a name="bkmk_access-script"></a> 自訂指令碼

您可以在工作順序執行時，使用 **Microsoft.SMS.TSEnvironment** COM 物件來讀取和寫入變數。

以下 Windows PowerShell 範例會查詢 **_SMSTSLogPath** 變數，以取得目前的記錄位置。 指令碼也會設定自訂變數。

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a> Windows 安裝程式回應檔案

您提供的 Windows 安裝程式回應檔案可以包含內嵌的工作順序變數。 請使用 `%varname%` 格式，其中 *varname* 是變數的名稱。 [設定 Windows 和 ConfigMgr]  步驟會以實際的變數值取代變數名稱字串。 這些內嵌的工作順序變數不能用於 unattend.xml 回應檔案中的純數值欄位。

如需詳細資訊，請參閱[設定 Windows 和 ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。

## <a name="see-also"></a>請參閱

- [工作順序步驟](task-sequence-steps.md)

- [工作順序變數](task-sequence-variables.md)

- [自動化工作的規劃考量](../plan-design/planning-considerations-for-automating-tasks.md)

- [工作順序編輯器](task-sequence-editor.md)
