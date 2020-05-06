---
title: 建立和執行指令碼
titleSuffix: Configuration Manager
description: 在用戶端裝置上建立並執行 PowerShell 指令碼。
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2113baf43c377379a2a996c59fd13e55072cf898
ms.sourcegitcommit: d05b1472385c775ebc0b226e8b465dbeb5bf1f40
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605179"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台建立及執行 PowerShell 指令碼

適用於：  Configuration Manager (最新分支)

<!--1236459-->
Configuration Manager 已整合執行 PowerShell 指令碼的能力。 PowerShell 的優勢是建立複雜自動化指令碼，其可供較大的社群了解與共用。 指令碼簡化了建置自訂工具來管理軟體的程序，而且可以讓您快速完成無趣的日常工作，以便更輕鬆且一致地完成大量工作。  

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  


使用 Configuration Manager 的這個整合功能，您就可以使用「執行指令碼」  功能來執行下列動作：

- 建立與編輯搭配 Configuration Manager 使用的指令碼。
- 透過角色和安全性範圍來管理指令碼的使用方式。 
- 在集合或個別內部部署受管理 Windows 電腦上執行指令碼。
- 從用戶端裝置取得快速彙總的指令碼結果。
- 監視指令碼執行和檢視指令碼輸出的報告結果。

> [!WARNING]
> - 鑒於指令碼的強大，提醒您要謹慎使用。 我們有內建的額外保護措施可以協助您：隔離的角色和範圍。 請務必先驗證指令碼的精確度再執行，並確認它們來自受信任的來源，以避免非預期的指令碼執行。 留意擴充字元或其他模糊化，並自學保護指令碼安全。 [深入了解 PowerShell 指令碼安全性](learn-script-security.md)
> - 某些反惡意程式碼軟體可能會不小心針對 Configuration Manager 執行指令碼或 CMPivot 功能觸發事件。 建議排除 %windir%\CCM\ScriptStore，讓反惡意程式碼軟體允許這些功能執行而不會受到干擾。

## <a name="prerequisites"></a>先決條件

- 若要執行 PowerShell 指令碼，用戶端必須執行 PowerShell 3.0 版或更新版本。 不過，如果您執行的指令碼包含較新版 PowerShell 中的功能，執行指令碼所在的用戶端上必須執行該版本的 PowerShell。
- Configuration Manager 用戶端必須執行至少 1706 版或更新版的用戶端，才能執行指令碼。
- 若要使用指令碼，您必須是適當 Configuration Manager 安全性角色的成員。
- 若要匯入及撰寫指令碼，您的帳戶必須具備 **SMS 指令碼**的**建立**權限。
- 若要核准或拒絕指令碼，您的帳戶必須具備 **SMS 指令碼**的**核准**權限。
- 若要執行指令碼，您的帳戶必須具備**集合**的**執行指令碼**權限。

如需有關 Configuration Manager 安全性角色的詳細資訊：</br>
[執行指令碼的安全性範圍](#security-scopes)</br>
[執行指令碼的安全性角色](#bkmk_ScriptRoles)</br>
[以角色為基礎的系統管理基本概念](../../core/understand/fundamentals-of-role-based-administration.md)。

## <a name="limitations"></a>限制

執行指令碼目前支援：

- 指令碼語言：PowerShell
- 參數類型：整數、字串和清單。


>[!WARNING]
>使用參數時請特別小心，它會開啟有潛在 PowerShell 插入式攻擊風險的介面區。 有許多方法可降低和處理此風險，例如使用規則運算式來驗證參數輸入，或使用預先定義的參數。 常見的最佳做法是不要在 PowerShell 指令碼中包含機密資訊 (不要包含密碼等)。 [深入了解 PowerShell 指令碼安全性](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>執行指令碼作者和核准者

執行指令碼使用將「指令碼作者」  和「指令碼核准者」  當作不同角色的概念來實作和執行指令碼。 分離作者和核准者角色可以進行執行指令碼之強大工具的重要程序檢查。 有額外的「指令碼執行者」  角色可執行指令碼，但無法建立或核准指令碼。 請參閱[建立指令碼的安全性角色](#bkmk_ScriptRoles)。

### <a name="scripts-roles-control"></a>指令碼角色控制項

使用者預設無法核准自己所撰寫的指令碼。 由於指令碼相當強大、用途廣泛且可部署至許多裝置，您可以將指令碼作者與指令碼核准者的角色分開。 這些角色可針對執行指令碼而未受監督的情況提供一層額外的安全性。 為簡化測試，您可以關閉次要核准。

### <a name="approve-or-deny-a-script"></a>核准或拒絕指令碼

指令碼必須先經過「指令碼核准者」  核准才能執行。 核准指令碼：

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。
2. 在 [軟體程式庫]  工作區中，按一下 [指令碼]  。
3. 在 [指令碼]  清單中，選擇您想要核准或拒絕的指令碼，然後在 [首頁]  索引標籤上的 [指令碼]  群組中，按一下 [核准/拒絕]  。
4. 在 [核准或拒絕指令碼]  對話方塊中，選取 [核准]  或 [拒絕]  指令碼。 您可以選擇性地輸入有關您決策的註解。  如果您拒絕某個指令碼，它就無法在用戶端裝置上執行。 <br>
![指令碼 - 核准](./media/run-scripts/RS-approval.png)
1. 完成精靈。 在 [指令碼]  清單中，[核准狀態]  資料行會隨著您採取的動作而發生變更。

### <a name="allow-users-to-approve-their-own-scripts"></a>允許使用者核准自己的指令碼

此核准主要用於指令碼開發的測試階段。

1. 在 Configuration Manager 主控台中，按一下 [系統管理]  。
2. 在 [系統管理]  工作區中，展開 [網站設定]  ，然後按一下 [網站]  。
3. 在站台清單中，選擇您的站台，然後在 [首頁]  索引標籤上的 [站台]  群組中，按一下 [階層設定]  。
4. 在 [階層設定屬性]  對話方塊的 [一般]  索引標籤上，取消選取 [指令碼作者需要其他指令碼核准者]  。

>[!IMPORTANT]
>最佳做法不該允許指令碼作者核准自己的指令碼。 只有在實驗室設定中才允許這樣做。 請仔細考慮變更此設定對生產環境可能的影響。

## <a name="security-scopes"></a>安全性範圍
  
執行指令碼會使用安全性範圍，此為 Configuration Manager 的現有功能，透過代表使用者群組的指派標記，控制指令碼的撰寫與執行。 如需使用安全性範圍的詳細資訊，請參閱[為 Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> 建立指令碼的安全性角色
在 Configuration Manager 中，預設並未建立用來執行指令碼的三個安全性角色。 若要建立指令碼執行者、指令碼作者和指令碼核准者角色，請遵循下列所述步驟。

1. 在 Configuration Manager 主控台中，移至 [系統管理]   >[安全性]   >[安全性角色] 
2. 以滑鼠右鍵按一下角色，然後按一下 [複製]  。 您複製的角色具有已指派的權限。 請確認您只取得所需的權限。 
3. 為自訂角色提供**名稱**和**描述**。 
4. 為安全性角色指派下面所述的權限。  

### <a name="security-role-permissions"></a>安全性角色權限  

**角色名稱**：指令碼執行者  
- **描述**：這些權限可讓此角色僅執行先前由其他角色建立並核准的指令碼。  
- **權限：** 確認下列項目已設定為 [是]  。  

|類別|權限|狀況|
|---|---|---|
|集合|執行指令碼|是|
|網站|讀取|是|
|SMS 指令碼|讀取|是|


**角色名稱**：指令碼作者  
- **描述**：這些權限可讓此角色撰寫指令碼，但無法予以核准或執行。  
- **權限**：確認已設定下列權限。
 
|類別|權限|狀況|
|---|---|---|
|集合|執行指令碼|否|
|網站|讀取|是|
|SMS 指令碼|建立|是|
|SMS 指令碼|讀取|是|
|SMS 指令碼|刪除|是|
|SMS 指令碼|修改|是|


**角色名稱**：指令碼核准者  
- **描述**：這些權限可讓此角色核准指令碼，但無法予以建立或執行。  
- **權限：** 確認已設定下列權限。  

|類別|權限|狀況|
|---|---|---|
|集合|執行指令碼|否|
|網站|讀取|是|
|SMS 指令碼|讀取|是|
|SMS 指令碼|核准|是|
|SMS 指令碼|修改|是|

     
**指令碼作者角色的 SMS 指令碼權限範例**  

 ![指令碼作者角色的 SMS 指令碼權限範例](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>建立指令碼

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。
2. 在 [軟體程式庫]  工作區中，按一下 [指令碼]  。
3. 在 [首頁]  索引標籤上的 [建立]  群組中，按一下 [建立指令碼]  。
4. 在 [建立指令碼]  精靈的 [指令碼]  頁面上，設定下列設定：
    - **指令碼名稱** - 輸入指令碼的名稱。 雖然可以使用相同名稱來建立多個指令碼，但使用重複名稱會讓您更難在 Configuration Manager 主控台中找出所需的指令碼。
    - **指令碼語言** - 目前僅支援 PowerShell 指令碼。
    - **匯入** - 將 PowerShell 指令碼匯入到主控台。 指令碼會顯示在 [指令碼]  欄位中。
    - **清除** - 將目前的指令碼從 [指令碼] 欄位中移除。
    - **指令碼** - 顯示目前已匯入的指令碼。 您可以視需要編輯此欄位中的指令碼。
5. 完成精靈。 新指令碼會顯示在 [指令碼]  清單中，其狀態為 [等候核准]  。 您必須先核准此指令碼，才能在用戶端裝置上執行它。 

> [!IMPORTANT]
> 使用執行指令碼功能時，避免以指令碼處理裝置重新開機或是重新啟動 Configuration Manager 代理程式。 這麼做可能會造成不斷重新開機的狀態。 如有需要，目前用戶端通知功能已有所加強，可重新啟動裝置。 [擱置重新啟動欄](../../core/clients/manage/manage-clients.md#restart-clients)可協助找出需要重新啟動的裝置。 
> <!--SMS503978  -->

## <a name="script-parameters"></a>指令碼參數

將參數新增至指令碼可提高工作的彈性。 您最多可以包括 10 個參數。 以下列出執行指令碼功能目前能夠使用的指令碼參數：「字串」  、「整數」  資料類型。 也提供預設值的清單。 如果您的指令碼有不支援的資料類型，您會收到警告。

在 [建立指令碼]  對話方塊中，按一下 [指令碼]  下的 [指令碼參數]  。

每個指令碼參數都有自己的對話方塊，以供新增進一步的詳細資料和驗證。 若指令碼中有預設參數，它將會列在參數 UI 中，而且您可以設定它。 Configuration Manager 將不會覆寫預設值，因為它將不會直接修改指令碼。 您可將此想像成「預先填寫的建議值」已在 UI 中提供，但 Configuration Manager 在執行階段未提供對「預設」值的存取。 編輯指令碼並輸入正確的值即可解決此問題。 <!--17694323-->

>[!IMPORTANT]
> 參數值不能包含單引號。 </br></br>
> 有一個已知問題，其會使包含或括在單引號中的參數值無法正確傳遞到指令碼。 指定在指令碼中包含空格的預設參數值時，請改為使用雙引號。 在建立或執行**指令碼**期間指定預設參數值時，無論值是否包含空格，將預設值括在雙引號或單引號中都不是必要操作。

### <a name="parameter-validation"></a>參數驗證

您指令碼中的每個參數都有 [Script Parameter Properties ] \(指令碼參數內容)  對話方塊，讓您新增該參數的驗證。 新增驗證之後，如果輸入的參數值與驗證不符，應該會收到錯誤。

#### <a name="example-firstname"></a>範例：*FirstName*

在此範例中，您可以設定字串參數 *FirstName* 的內容。

![指令碼參數 - 字串](./media/run-scripts/RS-parameters-string.png)


[指令碼參數屬性]  對話方塊的 [驗證] 區段包含下列可供您使用的欄位：

- **最小長度**：*FirstName* 欄位的最小字元數。
- **最大長度**：*FirstName* 欄位的最大字元數。
- **RegEx**：規則運算式 (*Regular Expression*) 的縮寫。 如需使用規則運算式的詳細資訊，請參閱下一節＜使用規則運算式驗證＞  。
- **自訂錯誤**：可讓您自行新增錯誤訊息，以取代任何系統驗證錯誤訊息。

#### <a name="using-regular-expression-validation"></a>使用規則運算式驗證

規則運算式是一種簡明的程式設計形式，適用於針對編碼驗證檢查字元字串。 例如，您可以在 *RegEx* 欄位中放入 `[^A-Z]`，來檢查 *FirstName* 欄位中是否缺少大寫字母字元。

此對話方塊的規則運算式處理是由 .NET Framework 支援。 如需使用規則運算式的指導，請參閱 [.NET 規則運算式](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions) (機器翻譯) 和[規則運算式語言](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference) (機器翻譯)。


## <a name="script-examples"></a>指令碼範例

以下數個範例示範的指令碼，您可能想要使用它們的這項功能。

### <a name="create-a-new-folder-and-file"></a>建立新資料夾和檔案

此指令碼會根據您的命名輸入來建立新資料夾和位於資料夾中的檔案。

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>取得 OS 版本

此指令碼會使用 WMI 來查詢機器的 OS 版本。

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> 編輯或複製 PowerShell 指令碼
<!--3705507-->
*(隨 1902 版推出)*  
您可以**編輯**或**複製**與「執行指令碼」  功能搭配使用的現有 PowerShell 指令碼。 現在您可以直接編輯指令碼，而不必重新建立需要變更的指令碼。 這兩個動作都使用您建立新指令碼時所使用的相同精靈體驗。 當您編輯或複製指令碼時，Configuration Manager 不會保存核准狀態。

> [!Tip]  
> 請勿編輯正在用戶端上執行的指令碼。 它們會無法完成原始指令碼的執行，而您則可能無法從這些用戶端取得想要的結果。  

### <a name="edit-a-script"></a>編輯指令碼

1. 移至 [軟體程式庫]  工作區下的 [指令碼]  節點。
1. 選取要編輯的指令碼，然後按一下功能區中的 [編輯]  。 
1. 在 [指令碼詳細資料]  頁面中，變更或重新匯入指令碼。
1. 按一下 [下一步]  以檢視 [摘要]  ，然後在完成編輯時，按一下 [關閉]  。

### <a name="copy-a-script"></a>複製指令碼

1. 移至 [軟體程式庫]  工作區下的 [指令碼]  節點。
1. 選取要複製的指令碼，然後按一下功能區中的 [複製]  。
1. 在 [指令碼名稱]  欄位中重新命名指令碼，並進行任何其他可能需要的編輯。
1. 按一下 [下一步]  以檢視 [摘要]  ，然後在完成編輯時，按一下 [關閉]  。


## <a name="run-a-script"></a>執行指令碼

指令碼經核准後，就能針對單一裝置或集合執行。 指令碼一旦開始執行，就會透過在一個小時後逾時的高優先權系統快速啟動。 然後指令碼的結果會使用狀態訊息系統傳回。

若要針對指令碼選取目標集合：

1. 在 Configuration Manager 主控台中，按一下 [資產與合規性]  。
2. 在 [資產與相容性] 工作區中，按一下 [裝置集合]  。
3. 在 [裝置集合]  清單中，按一下要用來作為指令碼執行位置的裝置集合。
4. 選取您所需的集合，按一下 [執行指令碼]  。
5. 在 [執行指令碼]  精靈的 [指令碼]  頁面上，從清單中選擇一個指令碼。 此清單只會顯示已核准的指令碼。
6. 按一下 [下一步]  完成精靈。

> [!IMPORTANT]
> 如果指令碼未執行 (例如因為目標裝置在該一個小時的時段內為關閉狀態)，您便必須再次執行指令碼。

### <a name="target-machine-execution"></a>Target machine execution

當「系統」  或「電腦」  帳戶位在目標用戶端上時，會執行此指令碼。 這個帳戶的網路存取權限很低。 您必須相應佈建指令碼對遠端系統及位置的任何存取。

## <a name="script-monitoring"></a>指令碼監視

在您於裝置集合上起始執行指令碼之後，請使用下列程序來監視作業。 您可在執行期間即時監視指令碼，也可以之後再返回所指定 [執行指令碼] 執行的狀態和結果。 指令碼狀態資料已在[刪除過時用戶端作業維護工作](../../core/servers/manage/reference-for-maintenance-tasks.md)期間或刪除指令碼時清除。<br>

![指令碼監視 - 指令碼執行狀態](./media/run-scripts/RS-monitoring-three-bar.png)

1. 在 Configuration Manager 主控台中，按一下 [監視]  。
2. 在 [監視]  工作區中，按一下 [指令碼狀態]  。
3. 在 [指令碼狀態]  清單中，您可以檢視在用戶端裝置上執行之每個指令碼的結果。 指令碼結束代碼 **0** 通常表示指令碼已成功執行。

 
   ![指令碼監視器 - 截斷的指令碼](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>指令碼輸出

用戶端的傳回指令碼輸出，透過將指令碼的結果輸送到 [ConvertTo-Json](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/convertto-json) Cmdlet 來格式化成 JSON。 JSON 格式會一致傳回可讀取的指令碼輸出。 針對不會傳回物件作為輸出的指令碼，ConvertTo-Json Cmdlet 會將輸出轉換成用戶端傳回的簡易字串，而非 JSON。  

- 得到未知結果的指令碼或離線的用戶端，皆不會出現在圖表或資料集中。 <!--507179-->
- 請避免傳回大型指令碼輸出，因為它會被截斷為 4 KB。 <!--508488-->
- 將指令碼中的列舉物件轉換為字串值，以正確地以 JSON 格式加以顯示。 <!--508377-->

   ![將列舉物件轉換為字串值](./media/run-scripts/enum-tostring-JSON.png)

您可以使用原始或結構化的 JSON 格式來檢視詳細指令碼輸出。 此格式可讓輸出變得更容易讀取與分析。 如果指令碼傳回有效的 JSON 格式文字，或輸出可使用 [ConvertTo-Json](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/convertto-json) PowerShell Cmdlet 來轉換成 JSON，則請將詳細輸出作為 **JSON 輸出**或**原始輸出**來檢視。 否則，唯一的選項是**指令碼輸出**。

### <a name="example-script-output-is-convertible-to-valid-json"></a>範例：指令碼輸出可轉換成有效的 JSON

命令：`$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>範例：指令碼輸出不是有效的 JSON

命令：`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>記錄檔

- 在用戶端上，根據預設位於 C:\Windows\CCM\logs：  
  - **Scripts.log**  
  - **CcmMessaging.log**  

- 在 MP 上，預設位於 C:\SMS_CCM\Logs：
  - **MP_RelayMsgMgr.log**  

- 在站台伺服器上，預設位於 C:\Program Files\Configuration Manager\Logs：
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>另請參閱

- [為 Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [以角色為基礎的系統管理基本概念](../../core/understand/fundamentals-of-role-based-administration.md)
