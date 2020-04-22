---
title: 即時資料的 CMPivot
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 CMPivot 即時查詢用戶端。
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702086"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>Configuration Manager 中即時資料的 CMPivot

<!--1358456-->

適用於：  Configuration Manager (最新分支)

Configuration Manager 一律提供大型中央裝置資料存放區，供客戶處理報表時使用。 站台通常會每週收集此資料。 從 1806 版本開始，CMPivot 是新的主控台內公用程式，現在可存取環境中裝置的即時狀態。 它能立即在目標集合中，所有目前已連線的裝置上執行查詢，然後傳回結果。 然後，使用這個工具來篩選此資料並進行分組。 提供線上用戶端的即時資料，讓您更快速地回答事務問題、解決問題，並回應安全性事件。

例如，在[修補投機性執行端通道漏洞](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)中，其中一項需求是更新系統 BIOS。 您可以使用 CMPivot 快速地查詢系統 BIOS 資訊，並找出不合規的用戶端。

 > [!IMPORTANT]  
 > - 某些安全性軟體可能會封鎖從 c:\windows\ccm\scriptstore 執行的指令碼。 這可能會使 CMPivot 查詢無法順利執行。 某些安全性軟體也可能會在執行 CMPivot PowerShell 時產生稽核事件或警示。
 > - 某些反惡意程式碼軟體可能會不小心針對 Configuration Manager 執行指令碼或 CMPivot 功能觸發事件。 建議排除 %windir%\CCM\ScriptStore，讓反惡意程式碼軟體允許這些功能執行而不會受到干擾。


## <a name="prerequisites"></a>先決條件

若要使用 CMPivot 需要下列元件：

- 將目標裝置升級至 Configuration Manager 用戶端的最新版本。  

- 目標用戶端至少需要 PowerShell 4 版。

- 若要收集下列實體的資料，目標用戶端需要 PowerShell 5.0 版：  
  - Administrators
  - 連線
  - IPConfig
  - SMBConfig


- CMPivot 的權限：
  - **SMS 指令碼**物件的**讀取**權限
  - **集合**的**執行指令碼**權限
    - 或者，從 1906 版開始，您可以在 [集合]  上使用 [執行 CMPivot]  。
  - **清查報告**的**讀取**權限
  - 預設範圍。

>[!NOTE]
> [執行指令碼]  是 [執行 CMPivot]  權限的超集。
 
## <a name="limitations"></a>限制

- 在階層中，將 Configuration Manager 主控台連線至「主要站台」  以執行 CMPivot。 **啟動 CMPivot**動作在連線至管理中心網站 (CAS) 時，將不會出現在主控台。
  - 從 Configuration Manager 1902 版開始，您可以從 CAS 執行 CMPivot。 在某些環境中，需要額外的權限。 如需詳細資訊，請參閱[從 1902 版開始的 CMPivot](#bkmk_cmpivot1902)。

- CMPivot 只會傳回已連線到目前站台的用戶端資料。  

- 如果集合包含來自另一個站台的裝置，CMPivot 結果只會來自目前站台的裝置。  

- 您無法自訂實體屬性、結果的資料行，或裝置上的動作。  

- 在同一時間，只有一個 CMPivot 執行個體可以在執行 Configuration Manager 主控台的電腦上執行。  

- 在 1806 版中，只有當群組名稱為 "Administrators" 時，查詢 **Administrators** 實體才有作用。 如果群組名稱已當地語系化，則沒有作用。 例如，法文的 "Administrateurs"。<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>啟動 CMPivot

1. 在 Configuration Manager 主控台中，連線至主要站台。 移至 [資產與合規性]  工作區，然後選擇 [裝置集合]  節點。 選取一個目標集合，然後按一下功能區中的 [啟動 CMPivot]  來啟動這個工具。  

    > [!Tip]  
    > 如果您沒有看到此選項，請檢查下列設定：  
    > 
    > - 與站台系統管理員確認您的帳戶具有必要權限。 如需詳細資訊，請參閱[必要條件](#prerequisites)。  
    > 
    > - 將主控台連線至「主要站台」  。  

2. 這個介面提供工具更詳細的操作方法。  

     - 在上方手動輸入查詢字串，或按一下內嵌文件中的連結。  

     - 按一下其中一個 [實體]  ，將它加入查詢字串。  

     - **資料表運算子**，**彙總函式**和**純量函式**的連結會在瀏覽器中開啟語言參考文件。 CMPivot 會使用 [Kusto 查詢語言 (KQL)](https://docs.microsoft.com/azure/kusto/query/) \(英文\)。  

3. 保持 CMPivot 視窗開啟以檢視來自用戶端的結果。 當您關閉 CMPivot 視窗時，工作階段便完成。  

    > [!Note]  
    > 如果已傳送查詢，則用戶端仍會傳送狀態訊息回應給伺服器。  



## <a name="how-to-use-cmpivot"></a>如何使用 CMPivot

![CMPivot 視窗範例](media/1358456-cmpivot-sample.png)

CMPivot 視窗包含下列項目：  

1. CMPivot 目前設為目標的集合位於頂端的標題列，以及視窗底部的狀態列。 例如，上面螢幕擷取畫面中的 "PM_Team_Machines"。  

2. 左側的窗格列出用戶端上可用的 [實體]  。 有些實體會依賴 WMI，有些則會使用 PowerShell，從用戶端取得資料。   

    - 以滑鼠右鍵按一下實體，即可執行下列動作：  

       - **插入**：將實體新增至查詢的目前游標位置。 查詢不會自動執行。 此動作是當您按兩下實體時的預設值。 建置查詢時，請使用此動作。  

       - **查詢全部**：針對此實體執行查詢，包括所有屬性。 使用此動作以快速地查詢單一實體。  

       - **依裝置查詢**：針對此實體執行查詢，並將結果分組。 例如， `Disk | summarize dcount( Device ) by Name`  

    - 展開實體以查看每個實體可用的特定屬性。 按兩下屬性可將它新增至查詢的目前游標位置。  

3. [首頁]  索引標籤會顯示 CMPivot 的一般資訊，包括查詢範例和支援文件的連結。  

4. [查詢]  索引標籤會顯示 [查詢] 窗格、[結果] 窗格和狀態列。 上述螢幕擷取畫面範例中，已選取 [查詢] 索引標籤。  

5. [查詢] 窗格可讓您建置或鍵入查詢，以在集合中的用戶端上執行。  

    - CMPivot 會使用 [Kusto 查詢語言 (KQL)](https://docs.microsoft.com/azure/kusto/query/) \(英文\) 的子集。  

    - 請在 [查詢] 窗格中剪下、複製或貼上內容。  
    <!-- markdownlint-disable MD038 -->
    - 根據預設，此窗格會使用 IntelliSense。 例如，如果您開始輸入 `D`，IntelliSense 會建議所有以該字母開頭的實體。 選取一個選項，並按 Tab 鍵插入它。 鍵入直立線符號字元和空格 `| `，IntelliSense 會建議所有資料表運算子。 插入 `summarize` 並鍵入一個空格，IntelliSense 會建議所有彙總函式。 如需這些運算子和函式的詳細資訊，請按一下 CMPivot 中的 [首頁]  索引標籤。  

    - [查詢] 窗格也會提供下列選項：  

        - 執行查詢。  

        - 在查詢的歷程記錄清單中前後移動。  

        - 建立直接成員資格集合。  

        - 將查詢結果匯出至 CSV 或剪貼簿。  

6. [結果] 窗格會顯示作用中用戶端針對查詢所傳回的資料。  

   - 可用的資料行會視實體及查詢而有所不同。  

   - 按一下資料行名稱，依據該內容排序結果。  

   - 以滑鼠右鍵按一下任何資料行名稱，以該資料行的相同資訊將結果分組，或排序結果。  

   - 以滑鼠右鍵按一下裝置名稱，以在裝置上採取下列額外動作：  

      - **樞紐至**：查詢此裝置上的另一個實體。  

      - **執行指令碼**：啟動 [執行指令碼精靈]，在此裝置上執行現有的 PowerShell 指令碼。 如需詳細資訊，請參閱[執行指令碼](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script)。  

      - **遠端控制**：啟動此裝置上的 Configuration Manager 遠端控制工作階段。 如需詳細資訊，請參閱[如何從遠端管理 Windows 用戶端電腦](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)。  

      - **資源總管**：啟動此裝置的 Configuration Manager 資源總管。 如需詳細資訊，請參閱[檢視硬體清查](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)或[檢視軟體清查](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

   - 以滑鼠右鍵按一下任何非裝置資料格，以採取下列額外動作：  

     - **複製**：將資料格的文字複製到剪貼簿。  

     - **顯示具有以下項目的裝置**：查詢此屬性具有此值的裝置。 例如，從 `OS` 查詢的結果中，在版本資料列的資料格上選取這個選項：`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **顯示不具以下項目的裝置**：查詢此屬性不具有此值的裝置。 例如，從 `OS` 查詢的結果中，在版本資料列的資料格上選取這個選項：`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing 一下**：啟動預設網頁瀏覽器前往 https://www.bing.com ，並以這個值作為查詢字串。  

   - 按一下任何超連結的文字，以樞紐轉換該特定資訊的檢視。  

   - [結果] 窗格不會顯示超過 20,000 個資料列。 請調整查詢，以進一步篩選資料，或在較小的集合上重新啟動 CMPivot。  

7. 狀態列會顯示下列資訊 (從左到右)：  

   - 對目標集合的目前查詢狀態。 此狀態包含：  
     - 完成查詢的作用中用戶端數目 (3)  
     - 用戶端總數 (5)  
     - 離線用戶端數目 (2)  
     - 傳回失敗的任何用戶端 (0)  

       例如：`Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - 用戶端作業的識別碼。 例如：`id(16780221)`  

   - 目前的集合。 例如：`PM_Team_Machines`  

   - [結果] 窗格中的資料列總數。 例如， `1 objects`  



## <a name="example-scenarios"></a>範例案例

下列各節提供如何在環境中使用 CMPivot 的範例：


### <a name="example-1-stop-a-running-service"></a>範例 1：停止執行中的服務

安全性系統管理員要求您儘快停止並停用會計部門中所有裝置上的 Computer Browser 服務。 您在會計部門所有裝置的集合上啟動 CMPivot，並選取 [服務]  實體上的 [查詢全部]  。 

`Service`

結果顯示時，您以滑鼠右鍵按一下 [名稱]  資料行，然後選取 [分組依據]  。 

`Service | summarize dcount( Device ) by Name`

在 [Browser]  服務的資料列中，按一下 [dcount_]  資料行中的超連結數字。 

`Service | where (Name == 'Browser') | summarize count() by Device`

多重選取所有的裝置、以滑鼠右鍵按一下選取範圍，然後選擇 [執行指令碼]  。 這個動作會啟動 [執行指令碼精靈]，您從該處執行現有的指令碼，以停止及停用服務。 您使用 CMPivot 快速地回應所有使用中電腦的安全性事件，並在 [執行指令碼精靈] 中檢視結果。 接著後續追蹤來建立設定基準，以便當集合中的其他電腦在未來變成使用中時加以補救。 

![Browser 服務和執行指令碼動作的 CMPivot 範例](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>範例 2：主動解決應用程式失敗  

為主動處理維護作業，您每週一次針對您管理的伺服器集合執行 CMPivot，並在 **AppCrash** 實體上選取 [查詢全部]  。 您以滑鼠右鍵按一下 [檔名]  資料行，然後選取 [遞增排序]  。 一部裝置在每天會針對 sqlsqm.exe 傳回七個結果，時間戳記大約是 03:00。 您在其中一個資料列中選取檔案名稱、以滑鼠右鍵按一下，然後選取 [Bing 一下]  。 在網頁瀏覽器中瀏覽搜尋結果，即可找到此問題的 Microsoft 技術支援文件，其中有詳細資訊及解決方法。 


### <a name="example-3-bios-version"></a>範例 3：BIOS 版本

若要[修補投機性執行端通道漏洞](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)，其中一項需求是更新系統 BIOS。 首先要查詢 **BIOS** 實體。 然後依據 **Version** 屬性進行 [分組]  。 然後以滑鼠右鍵按一下特定值，例如 "LENOVO - 1140"，並選取 [顯示具有以下項目的裝置]  。  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>範例 4：可用磁碟空間

您需要暫時在網路檔案伺服器上儲存一個大型檔案，但不確定哪一個有足夠的容量。 針對檔案伺服器集合啟動 CMPivot，並查詢 **Disk** 實體。 修改 CMPivot 的查詢，以快速傳回一份作用中伺服器與即時儲存體資料的清單：  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a> 從 1810 版開始的 CMPivot
<!--1359068, 3607759-->

從 Configuration Manager 1810 版開始，CMPivot 包含下列改善：

- [CMPivot 公用程式與效能](#bkmk_cmpivot-perf)
- [純量函式](#bkmk_cmpivot-functions)  
- [轉譯視覺效果](#bkmk_cmpivot-charts)  
- [硬體清查](#bkmk_cmpivot-hinv)  
- [純量運算子](#bkmk_cmpivot-operators)  
- [查詢摘要](#bkmk_cmpivot-summary)  
- [稽核狀態訊息](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a> CMPivot 公用程式與效能

- CMPivot 最多會傳回 100,000 個資料格，而不是 20,000 個資料列。
  - 如果實體有 5 個屬性，這表示 5 個資料行，最多會顯示 20,000 個資料列。
  - 如果實體有 10 個屬性，則最多會顯示 10,000 個資料列。
  - 顯示的總資料量會小於或等於 100,000 個資料格。
- 在 [查詢摘要] 索引標籤上，選取失敗或離線裝置計數，然後選取 [建立集合]  選項。 此選項讓您更容易以具有補救部署的裝置為目標。
- 按一下資料夾圖示以儲存**最常用**查詢。
   ![在 CMPivot 中儲存最常用查詢的範例](media/cmpivot-favorite.png)

- 已更新為 1810 版的用戶端會透過快速通訊通道，將小於 80 KB 的輸出傳回給站台。
  - 這項變更可提高檢視指令碼或查詢輸出的效能。
  - 如果指令碼或查詢輸出大於 80 KB，則用戶端會透過狀態訊息來傳送資料。
  - 如果用戶端未更新為 1810 用戶端版本，則會繼續使用狀態訊息。

- 當您啟動 CMPivot 時，可能會看到下列錯誤：**您目前無法使用 CMPivot，因為指令碼版本不相容。此問題可能是因為階層正處於升級站台的程序。請等候升級完成，然後再試一次。**

  - 如果您看到此訊息，這可能表示：
    - 未正確設定安全性範圍。
    - 升級程序中發生問題。
    - 底層 CMPivot 指令碼不相容。


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a> 純量函式
CMPivot 支援下列純量函式：
- **ago()** ：從目前的 UTC 時鐘時間減去所指定時間範圍  
- **datetime_diff()** ：計算兩個日期時間值的日曆差距  
- **now()** ：傳回目前的 UTC 時鐘時間  
- **bin()** ：將值無條件捨去為指定間隔大小的整數倍數  

> [!Note]  
> 日期時間資料類型表示瞬間時間，通常是以日期和一天當中的時間表示。 時間值是以 1 秒為測量單位。 日期時間值一律採用 UTC 時區。 請務必以 ISO 8601 格式表示日期時間常值，例如 `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>範例
- `datetime(2015-12-31 23:59:59.9)`：特定日期時間常值   
- `now()`：目前時間  
- `ago(1d)`：目前時間減去一天  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a> 轉譯視覺效果

CMPivot 現在包含對 KQL [render 運算子](https://docs.microsoft.com/azure/kusto/query/renderoperator) \(英文\) 的基本支援。 這項支援包含下列類型：  
- **barchart**：第一個資料行是 X 軸，且可以是文字、日期時間或數值。 第二個資料行必須是數值，而且會顯示為橫條。  
- **columnchart**：類似 barchart，但以直條取代橫條。  
- **piechart**：第一個資料行是色彩座標軸，第二個資料行是數值。  
- **timechart**：折線圖。 第一個資料行是 X 軸，而且應該是日期時間。 第二個資料行是 Y 軸。  

#### <a name="example-bar-chart"></a>範例：橫條圖
下列查詢會將最近使用的應用程式轉譯為橫條圖：

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![CMPivot 橫條圖視覺效果範例](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>範例：時間圖
若要轉譯時間圖，請使用新的 **bin()** 運算子依時間分組事件。 下列查詢會顯示裝置在過去七天何時啟動：

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![CMPivot 時間圖視覺效果範例](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>範例：圓形圖
下列查詢會以圓形圖顯示所有作業系統版本：

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![CMPivot 圓形圖視覺效果範例](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a> 硬體清查
使用 CMPivot 查詢任何硬體清查類別。 這些類別包含您對硬體清查所做的任何自訂延伸。 CMPivot 會立即傳回儲存在站台資料庫中上次硬體清查掃描所快取的結果。 同時，它會視需要以來自任何線上用戶端的即時資料更新結果。

結果資料表或圖表中的資料色彩飽和度指出資料為即時或快取。 例如，深藍色表示來自線上用戶端的即時資料。 淺藍色表示快取資料。

#### <a name="example"></a>範例

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![CMPivot 清查查詢與直條圖視覺效果範例](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>限制
- 不支援下列硬體清查實體：  
    - 陣列屬性，例如 IP 位址  
    - Real32/Real64 <!--example?-->  
    - 內嵌物件屬性 <!--example?-->  
- 清查實體名稱必須以字元開頭
- 您無法透過建立相同名稱的清查實體來覆寫內建實體  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a> 純量運算子
CMPivot 包含下列純量運算子：  

> [!Note]  
> - LHS：運算子左邊的字串  
> - RHS：運算子右邊的字串  


|運算子|說明|範例 (產生 true)|
|--------|-----------|---------------------|
|==|等於|`"aBc" == "aBc"`|
|!=|不等於|`"abc" != "ABC"`|
|like|LHS 包含 RHS 的相符項目|`"FabriKam" like "%Brik%"`|
|!like|LHS 不包含 RHS 的相符項目|`"Fabrikam" !like "%xyz%"`|
|包含|RHS 作為 LHS 的子序列發生|`"FabriKam" contains "BRik"`|
|!contains|RHS 未在 LHS 中發生|`"Fabrikam" !contains "xyz"`|
|startswith|RHS 是 LHS 的起始子序列|`"Fabrikam" startswith "fab"`|
|!startswith|RHS 不是 LHS 的起始子序列|`"Fabrikam" !startswith "kam"`|
|endswith|RHS 是 LHS 的右子序列|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS 不是 LHS 的右子序列|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a> 查詢摘要

選取 CMPivot 視窗底部的 [查詢摘要]  索引標籤。 此狀態可協助您識別離線的用戶端，或針對可能發生的錯誤進行疑難排解。 在 [計數] 欄中選取值，以開啟具有該狀態的特定裝置清單。 

例如，選取具有 [失敗] 狀態的裝置計數。 請參閱特定錯誤訊息，並匯出這些裝置的清單。 如果錯誤是無法辨識特定 Cmdlet，請從匯出的裝置清單建立集合，以部署 Windows PowerShell 更新。  

### <a name="cmpivot-audit-status-messages"></a>CMPivot 稽核狀態訊息

從 1810 版開始，當您執行 CMPivot 時，會建立一則稽核狀態訊息，**MessageID 為 40805**。 您可以移至 [監視]   > [系統狀態]   > [狀態訊息查詢]  來檢視狀態訊息。 您可以執行 [特定使用者的所有稽核狀態訊息]  、[特定站台的所有稽核狀態訊息]  ，或建立您自己的狀態訊息查詢。

訊息使用下列格式：

MessageId 40805：使用者 &lt;UserName> 已在集合 &lt;Collection-ID> 上執行具有雜湊 &lt;Script-Hash> 的指令碼 &lt;Script-Guid>。

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 是 CMPivot 的 Script-Guid。
- 您可以在用戶端的 scripts.log 檔案中查看 Script-Hash。
- 您也可以查看儲存在用戶端指令碼存放區中的雜湊。 用戶端上的檔案名稱是 &lt;Script-Guid>_&lt;Script-Hash>。
    - 範例檔案名稱：C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![CMPivot 稽核狀態訊息範例](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a> 從 1902 版開始的 CMPivot
<!--3610960-->
從 Configuration Manager 1902 版開始，您可以從管理中心網站 (CAS) 的階層中執行 CMPivot。 主要站台仍會處理與用戶端的通訊。 從管理中心網站執行 CMPivot 時，它會通過高速的訊息訂閱通道與主要站台進行通訊。 此通訊不依賴站台之間的標準 SQL 複寫。

當 SQL 或提供者不在相同的電腦時，或在 SQL Always On 設定中，於 CAS 上執行 CMPivot 需要額外的權限。 透過這些遠端設定，即可允許 CMPivot 的「雙躍點情節」。

若要讓 CMPivot 在這種「雙躍點情節」中運作，可定義限制委派。 若要了解此設定的安全性含意，請閱讀 [Kerberos 限制委派](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)一文。 Kerberos 必須處理機器之間的所有躍點。<!--5746133--> 如果您有多個遠端設定 (例如 SQL 或 SMS 提供者是否與 CAS 共置，或有多個信任樹系)，您可能需要結合多項權限設定。 以下是您可能需要採取的步驟：

### <a name="cas-has-a-remote-sql-server"></a>CAS 具有遠端 SQL Server

1. 移至每個主要站台的 SQL Server。
   1. 將 CAS 遠端 SQL Server 和 CAS 站台伺服器新增至 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 群組。
   ![主要站台 SQL Server 上的 Configmgr_DviewAccess 群組](media/cmpivot-dviewaccess-group.png)
1. 移至 [Active Directory 使用者和電腦]。
   1. 針對每個主要站台伺服器，按一下滑鼠右鍵並選取 [屬性]  。
      1. 在 [委派] 索引標籤中，選擇第三個選項 [信任這台電腦，但只委派指定的服務]  。 
      1. 選擇 [只使用 Kerberos]  。
      1. 使用連接埠和執行個體，新增 CAS 的 SQL Server 服務。
      1. 確定這些變更符合您公司的安全性原則！
   1. 針對 CAS 站台，按一下滑鼠右鍵並選取 [屬性]  。
      1. 在 [委派] 索引標籤中，選擇第三個選項 [信任這台電腦，但只委派指定的服務]  。 
      1. 選擇 [只使用 Kerberos]  。
      1. 使用連接埠和執行個體，新增每個主要站台的 SQL Server 服務。
      1. 確定這些變更符合您公司的安全性原則！

   ![雙躍點的 CMPivot AD 委派範例](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS 具有遠端提供者

1. 移至每個主要站台的 SQL Server。
   1. 將 CAS 提供者電腦帳戶和 CAS 站台伺服器新增至 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 群組。
1. 移至 [Active Directory 使用者和電腦]。
   1. 選取 CAS 提供者電腦，按一下滑鼠右鍵並選取 [屬性]  。
      1. 在 [委派] 索引標籤中，選擇第三個選項 [信任這台電腦，但只委派指定的服務]  。 
      1. 選擇 [只使用 Kerberos]  。
      1. 使用連接埠和執行個體，新增每個主要站台的 SQL Server 服務。
      1. 確定這些變更符合您公司的安全性原則！
   1. 選取 CAS 站台伺服器，按一下滑鼠右鍵並選取 [屬性]  。
      1. 在 [委派] 索引標籤中，選擇第三個選項 [信任這台電腦，但只委派指定的服務]  。 
      1. 選擇 [只使用 Kerberos]  。
      1. 使用連接埠和執行個體，新增每個主要站台的 SQL Server 服務。
      1. 確定這些變更符合您公司的安全性原則！
1. 重新啟動 CAS 遠端提供者電腦。

### <a name="sql-always-on"></a>SQL Always On

1. 移至每個主要站台的 SQL Server。
   1. 將 CAS 站台伺服器新增至 [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) 群組。
1. 移至 [Active Directory 使用者和電腦]。
   1. 針對每個主要站台伺服器，按一下滑鼠右鍵並選取 [屬性]  。
      1. 在 [委派] 索引標籤中，選擇第三個選項 [信任這台電腦，但只委派指定的服務]  。 
      1. 選擇 [只使用 Kerberos]  。
      1. 使用連接埠和執行個體，新增 CAS 的 SQL Server 服務帳戶作為 SQL 節點。
      1. 確定這些變更符合您公司的安全性原則！
   1. 選取 CAS 站台伺服器，按一下滑鼠右鍵並選取 [屬性]  。
      1. 在 [委派] 索引標籤中，選擇第三個選項 [信任這台電腦，但只委派指定的服務]  。 
      1. 選擇 [只使用 Kerberos]  。
      1. 使用連接埠和執行個體，新增每個主要站台的 SQL Server 服務。
      1. 確定這些變更符合您公司的安全性原則！
1. 確定針對 CAS SQL 接聽程式名稱和每個主要 SQL 接聽程式名稱[發佈 SPN](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs)。
1. 重新啟動主要 SQL Server。
1. 重新啟動 CAS 站台伺服器和 CAS SQL Server。

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a> 從 1906 版開始的 CMPivot

從 1906 版開始，已將下列項目新增至 CMPivot：

- [聯結、其他運算子和彙總工具](#bkmk_cmpivot_joins)
- [為安全性系統管理員角色新增的 CMPivot 權限](#bkmk_cmpivot_secadmin1906)
- [CMPivot 獨立](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a> 在 CMPivot 中新增聯結、其他運算子和彙總工具
<!--4054074-->
您現在擁有額外的算術運算子、彙總工具，以及新增查詢聯結的能力，例如將登錄和檔案一起使用。 已新增下列項目：

#### <a name="table-operators"></a>資料表運算子

|資料表運算子| 說明|
|-----|-----|
| [join](https://docs.microsoft.com/azure/kusto/query/joinoperator)| 透過比對相同裝置的資料列，合併兩個資料表的資料列以形成新資料表|
|轉譯|將結果轉譯為圖形輸出|

CMPivot 已經有轉譯運算子。 已新增 **with** 陳述式及多個數列的支援。 如需詳細資訊，請參閱[範例](#bkmk_cmpivot_examples1906)一節和 Kusto 的[聯結運算子](https://docs.microsoft.com/azure/kusto/query/joinoperator)一文。

#### <a name="limitations-for-joins"></a>聯結的限制

1. 聯結資料行會一律在 [裝置]  欄位上以隱含方式完成。
1. 您最多可以針對每個查詢使用 5 個聯結。
1. 您最多可以使用 64 個合併資料行。

#### <a name="scalar-operators"></a>純量運算子

|運算子| 說明|範例|
|-----|-----|-----|
| + | 新增| `2 + 1, now() + 1d`|
| - |  減去| `2 - 1, now() - 1d`|
| * | 乘以| `2 * 2`|
| / | 除以 | `2 / 1`|
| % | 模數 | `2 % 1`

#### <a name="aggregation-functions"></a>彙總函式

|函式| 說明|
|-----|-----|
| percentile()| 返回由運算式定義之母體的指定最近百分位數估計值|
| sumif() | 傳回述詞評估為 True 的運算式總和|

#### <a name="scalar-functions"></a>純量函式

|函式| 說明|
|-----|-----|
| case()| 評估述詞的清單，並傳回符合述詞的第一個結果運算式 |
| iff() | 評估第一個引數並傳回第二個或第三個引數的值，取決於述詞評估為 True (第二個) 或 False (第三個)|
 | indexof() | 函式回報輸入字串中第一次出現之指定字串以零起始的索引|
| strcat() | 串連 1 到 64 個引數 |
| strlen()| 傳回輸入字串的長度 (以字元為單位)|
| substring() | 從某個索引開始到字串結尾的來源字串中擷取子字串 |
| tostring() | 將輸入轉換為字串作業 |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a> 範例

- 顯示裝置、製造商、型號及 OSVersion：

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- 顯示裝置的開機時間圖形：

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![堆疊橫條圖顯示裝置的開機時間 (毫秒)](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a> 為安全性系統管理員角色新增的 CMPivot 權限
<!--4683130-->

從 1906 版開始，下列權限已新增至 Configuration Manager 的內建**安全性系統管理員**角色：

 - **讀取** SMS 指令碼
 - 在集合上**執行 CMPivot**
 - **讀取**清查報告

>[!NOTE]
> [執行指令碼]  是 [執行 CMPivot]  權限的超集。
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> CMPivot 獨立
<!--3555890, 4619340, 4683130 -->

從 1906 版開始，您可以使用 CMPivot 作為獨立應用程式。 CMPivot 獨立僅提供英文版本。 在 Configuration Manager 主控台外部執行 CMPivot，以檢視環境中裝置的即時狀態。 這項變更可讓您無需先安裝主控台，即可在裝置上使用 CMPivot。

> [!Tip]  
> 此功能最初是在 1906 版中引進作為[發行前版本功能](pre-release-features.md)。 從 2002 版開始，該功能不再是發行前版本功能。  

您可與其他角色共用 CMPivot 的強大功能，例如沒有在電腦上安裝主控台的技術服務人員或安全性系統管理員。 這些其他角色可以使用 CMPivot 查詢 Configuration Manager 以及它們傳統上使用的其他工具。 藉由共用此豐富的管理資料，您可以共同協作以主動解決跨角色的商務問題。

#### <a name="install-cmpivot-standalone"></a>安裝 CMPivot 獨立

1. 設定執行 CMPivot 所需的權限。 如需詳細資訊，請參閱[必要條件](#prerequisites)。 如果權限適用於使用者，您也可以使用[安全性系統管理員角色](#bkmk_cmpivot_secadmin1906)。
2. 在下列路徑中尋找 CMPivot 應用程式安裝程式：`<site install path>\tools\CMPivot\CMPivot.msi`。 您可以從該路徑中執行它，或將其複製到另一個位置。
3. 當您執行 CMPivot 獨立應用程式時，系統會要求您連線至網站。 請指定管理中心或主要站台伺服器的完整網域名稱或電腦名稱。
   - 每次您開啟 CMPivot 獨立時，系統都會提示您連線至站台伺服器。
4. 瀏覽至您要在其上執行 CMPivot 的集合，然後執行您的查詢。

   ![瀏覽至您想要對其執行查詢的集合](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> 以滑鼠右鍵按一下動作 (例如，[執行指令碼]  、[資源總管]  和 Web 搜尋) 無法在 CMPivot 獨立中使用。 CMPivot 獨立的主要用途是於 Configuration Manager 基礎結構進行獨立查詢。 為了協助安全性系統管理員，CMpivot 獨立的功能包含連線至 Microsoft Defender 資訊安全中心。 <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a>從 1910 版開始的 CMPivot
<!--5410930, 3197353-->
從 1910 版開始，CMPivot 已大幅最佳化，以減少伺服器上的網路流量和負載。 此外，也新增了一些實體與實體增強功能，協助您進行疑難排解和搜捕。 1910 版的 CMPivot 引進了下列變更：

- [對 CMPivot 引擎的最佳化](#bkmk_optimization)
- 其他實體與實體增強：
  - Windows 事件記錄檔 ([WinEvent](#bkmk_WinEvent))
  - 檔案內容 ([FileContent](#bkmk_File))
  - 由處理序載入的 Dll ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory 資訊 ([AADStatus](#bkmk_AadStatus))
  - Endpoint Protection 狀態 ([EPStatus](#bkmk_EPStatus))
- [使用 CMPivot 獨立的本機裝置查詢評估](#bkmk_local-eval)
- [其他對 CMPivot 的增強](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a>對 CMPivot 引擎的最佳化
<!--3197353-->
為了減少伺服器上的網路流量和負載，CMPivot 已於 1910 中最佳化。 許多查詢作業現在會直接在用戶端上執行，而非在伺服器上執行。 這種變更也表示某些 CMPivot 作業會從第一個查詢傳回最少的資料。 如果您決定深入探索資料以取得詳細資訊，則可能會執行新的查詢，以從用戶端擷取額外的資料。 例如在先前，當執行「摘要的計數」查詢時，則會將大型資料集傳回給伺服器。  雖然傳回大型資料集可提供立即向下切入，但多數情況下只需要摘要的計數。 在 1910 版中，當選擇深入探索特定用戶端時，會具有另一個資料的集合，以傳回所要求的其他資料。 這項變更可針對大量用戶端的查詢帶來更佳效能和延展性。 <!--3197353, 5458337-->

#### <a name="examples"></a>範例

CMPivot 最佳化會大幅減少執行 CMPivot 查詢所需的網路和伺服器 CPU 負載。 藉由這些最佳化，我們現在可以即時對數 GB 的用戶端資料進行 sift 檢查。 下列查詢說明這些最佳化：

- 搜尋企業中所有用戶端上的所有事件記錄檔，以尋找驗證失敗。

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- 依雜湊搜尋檔案。

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a> WinEvent(\<logname>,[\<timespan>])

此實體是用來從記錄檔與事件追蹤記錄檔取得事件。 實體會從 Windows 事件記錄檔技術產生的事件記錄檔取得資料。 實體也會取得 Windows 事件追蹤 (ETW) 產生的記錄檔取得事件。 WinEvent 預設會搜尋在過去 24 小時內發生的事件。 不過，24 小時的預設值可透過包括時間範圍來覆寫。

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a> FileContent(\<filename>)

FileContent 是用來取得文字檔的內容。

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a> ProcessModule(\<processname>)  

此實體是用來列舉給定處理序載入的模組 (dll)。 當搜捕隱藏在合法處理序中的惡意程式碼時，ProcessModule 很有用。  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a> AadStatus

此實體可用來從裝置取得目前的 Azure Active Directory 身分識別資訊。

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a> EPStatus

EPStatus 可用來取得電腦上安裝之反惡意程式碼軟體的狀態。

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a>使用 CMPivot 獨立的本機裝置查詢評估
<!--3197353-->
在 Configuration Manager 主控台之外使用 CMPivot 時，您可以只查詢本機裝置，而不需要 Configuration Manager 基礎結構。 您現在可以利用 CMPivot Azure Log Analytics 查詢，快速地在本機裝置上檢視 WMI 資訊。 這也可以讓您在較大的環境中執行 CMPivot 查詢之前，先對其進行驗證及改善。 CMPivot 獨立僅提供英文版本。 如需安裝 CMPivot 獨立的詳細資訊，請參閱[安裝 CMPivot 獨立](#install-cmpivot-standalone)。

#### <a name="known-issues-for-local-device-query-evaluation"></a>本機裝置查詢評估的已知問題

 - 如果您在**這部電腦**上對不具存取權的 WMI 實體進行查詢，例如鎖定的 WMI 類別，則您可能會在 CMPivot 中看到損毀。 使用具有較高權限的帳戶來執行 CMPivot，以查詢這些實體。 <!--5753242-->
- 如果您在**這部電腦**上查詢非 WMI 實體，則會看到**無效的命名空間**或不明確的例外狀況。
- 請從 [開始] 功能表捷徑執行 CMPivot 獨立，而非直接從可執行檔的路徑執行。 <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a> 其他增強功能

- 您可以使用新的 `like` 運算子來執行規則運算式類型查詢。 例如：<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- 我們已更新 **CcmLog()** 與 **EventLog()** 實體，它們現在預設只會查看過去 24 小時內的訊息。 您可以透過傳入選擇性的時間範圍來覆寫此行為。 例如，下列查詢會查看過去 1 小時內的事件：

   ```kusto
   CcmLog('Scripts',1h)
   ```

- **File()** 實體已更新為收集有關隱藏與系統檔案的資訊，且包括 MD5 雜湊。 雖然 MD5 不如 SHA256 雜湊精確，但有大部分惡意程式碼布告欄越來越常使用它作為回報的雜湊。  

- 您可以在查詢中新增註解。<!-- 5431463 --> 當共用查詢時，此行為很有用。 例如：

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot 會自動連線到上一個站台。<!-- 5420395 --> 當您啟動 CMPivot 之後，您可以視需要連線到新的站台。

- 從 [匯出]  功能表，選取新的選項以 [查詢連結到剪貼簿]  。<!-- 5431577 --> 此動作會將連結複製到剪貼簿，以方便您與其他人共用。 例如：

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    此連結可使用下列查詢獨立開啟 CMPivot：

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > 若要讓此連結運作，請[安裝 CMPivot 獨立版](#install-cmpivot-standalone)。

- 在查詢結果中，若裝置已在 Microsoft Defender 進階威脅防護 (ATP) 中註冊，請以滑鼠右鍵按一下裝置以啟動 **Microsoft Defender 資訊安全中心**線上入口網站。

### <a name="known-issues-for-cmpivot-in-version-1910"></a>1910 版中 CMPivot 的已知問題

- 達到限制時，可能不會顯示結果橫幅上限。 <!--5431427-->
  - 每個用戶端的每個查詢限制為 128 KB 大小的資料。
  - 如果查詢的結果超過 128 KB，其結果可能會被截斷。
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a>從 2002 版開始的 CMPivot
<!--5870934-->
我們讓巡覽 CMPivot 實體變得更容易。 從 Configuration Manager 2002 版開始，可搜尋 CMPivot 實體， 並已新增圖示，可供輕鬆區分實體與實體物件類型。

![搜尋 CMPivot 實體](./media/5870934-search-cmpivot-entities.png)

 
## <a name="inside-cmpivot"></a>深入探討 CMPivot

CMPivot 使用 Configuration Manager「快速通道」將查詢傳送至用戶端。 其他功能也使用這個從伺服器到用戶端的通訊通道，例如用戶端通知動作、用戶端狀態和 Endpoint Protection。 用戶端透過同樣快速的狀態訊息系統傳回結果。 狀態訊息會暫時儲存在資料庫中。 如需用於用戶端通知的連接埠詳細資訊，請參閱[連接埠](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP)一文。

查詢和結果全都只是文字。 實體 **InstallSoftware** 和 **Process** 會傳回一些最大的結果集。 在效能測試期間，針對這些查詢，來自一個用戶端的最大狀態訊息檔案大小小於 **1KB**。 調整為具有 50,000 個作用中用戶端的大型環境之後，這項一次性查詢會在網路上產生不超過 50 MB 的資料。 歡迎頁面上所有加上底線的項目針對每個用戶端會傳回不到 1k 的資訊。

![CMPivot 中加上底線的實體範例](media/cmpivot-underlined-entities.png)

從 Configuration Manager 1810 開始，CMPivot 可以查詢硬體清查資料，包括擴充的硬體清查類別。 這些新實體 (歡迎頁面上未加上底線的實體) 可能會傳回較大的資料集，視您為指定硬體清查屬性定義的資料量而定。 例如，"InstalledExecutable" 實體針對每個用戶端可能會傳回數 MB 的資料，視所查詢的特定資料而定。 使用 CMPivot 從較大集合傳回較大的硬體清查資料集時，請留意系統的效能和延展性。

查詢會在一小時後逾時。 例如，集合具有 500 部裝置，450 個用戶端目前在線上。 這些作用中裝置收到查詢，並且近乎立即傳回結果。 如果您保持 CMPivot 視窗開啟，則當其他 50 個用戶端上線時，它們也會收到查詢並傳回結果。 

## <a name="log-files"></a>記錄檔

 CMPivot 互動會記錄至下列記錄檔中：

**伺服器端：**
- SmsProv.log
- BgbServer.log
- StateSys.log

**用戶端：**
- CCMNotificationAgent.log
- Scripts.log
- StateMessage.log

如需詳細資訊，請參閱[記錄檔](../../plan-design/hierarchy/log-files.md)和[針對 CMPivot 進行疑難排解](cmpivot-tsg.md)。

## <a name="next-steps"></a>後續步驟
 
[針對 CMPivot 進行疑難排解](cmpivot-tsg.md)

[建立並執行 Powershell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)


