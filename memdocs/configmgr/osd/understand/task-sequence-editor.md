---
title: 使用工作順序編輯器
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 主控台中使用工作順序編輯器
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691146"
---
# <a name="use-the-task-sequence-editor"></a>使用工作順序編輯器

適用於：  Configuration Manager (最新分支)

使用**工作順序編輯器**，在 Configuration Manager 主控台中編輯工作順序。 使用編輯器來執行下列動作：  

- 開啟工作順序的唯讀檢視

- 從工作順序新增或移除步驟  

- 變更工作順序的步驟順序  

- 新增或移除步驟群組  

- 在工作順序之間複製並貼上步驟

- 設定步驟選項，例如當發生錯誤時工作順序是否要繼續執行  

- 為工作順序的步驟和群組新增條件  

- 在工作順序中的步驟之間複製及貼上條件

- 搜尋工作順序以快速找出步驟

必須先建立工作順序，才能開始編輯。 如需詳細資訊，請參閱[管理和建立工作順序](../deploy-use/manage-task-sequences-to-automate-tasks.md)。

## <a name="about-the-task-sequence-editor"></a>關於工作順序編輯器

工作順序編輯器包含下列元件：

![範例工作順序編輯器視窗的已標註螢幕擷取畫面](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. 工作順序的名稱
2. 搜尋。 如需詳細資訊，請參閱[搜尋](#bkmk_search)。
3. 順序中所選群組或步驟的 [屬性] 

    如需特定步驟其屬性與選項的詳細資訊，請參閱[關於工作順序步驟](task-sequence-steps.md)。

4. 順序中所選群組或步驟的 [選項] 

    如需所有步驟的一般選項，或特定步驟選項的詳細資訊，請參閱[關於工作順序步驟](task-sequence-steps.md)。

    如需如何設定條件的詳細資訊，請參閱[條件](#bkmk_conditions)。

5. [新增]  群組或步驟
6. [移除]  群組或步驟
7. 摺疊或展開所有群組
8. 移動序列中群組或步驟的位置 (上移、下移)
9. 工作順序：
    - 查看步驟和群組的順序。
    - 展開或摺疊群組。
    - 當在步驟或群組的 [選項]  中停用步驟或群組時，該項目在順序中會呈現灰色。
    - 如果步驟發生問題，則該步驟會變更為紅色的錯誤圖示。 例如，遺失某項必要值。
10. **確定**：儲存並關閉
11. **取消**：關閉但不儲存變更
12. [套用]  ：儲存變更並保持開啟

您可使用標準 Windows 控制項來調整工作順序編輯器的大小。 若要調整兩個主要窗格的寬度，請使用滑鼠選取工作順序和步驟屬性之間的橫條，然後將其向左或向右拖曳。

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a> 檢視工作順序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在 [工作順序]  清單中，選取要檢視的工作順序。  

3. 在功能區的 [首頁]  索引標籤上，選取 [工作順序]  群組中的 [檢視]  。

    > [!TIP]
    > 此動作為預設值。 如果按兩下工作順序，則可以**檢視**該工作順序。

此動作會以唯讀模式來開啟工作順序編輯器。 在此模式中，您可以執行下列動作：

- 檢視所有群組、步驟、屬性以及選項
- 展開和摺疊群組
- 搜尋工作順序
- 調整編輯器的視窗大小

在此唯讀模式中，無法進行任何變更，包括複製步驟或條件等。 此動作也不會鎖定工作順序以供編輯。 如需這些鎖定的詳細資訊，請參閱[解除鎖定以編輯工作順序](#bkmk_sedo)。

若要變更工作順序，請關閉在唯讀模式中開啟的工作順序編輯器。 然後[編輯](#bkmk_edit)工作順序。

> [!NOTE]  
> 當檢視或編輯由 [建立工作順序精靈] 建立的工作順序時，步驟的名稱可以是步驟的動作或類型。 例如，您可能會看到名稱「分割磁碟 0」，這就是 [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk) 類型步驟的動作。 系統會依工作順序步驟的「類型」  記載所有工作順序步驟，而不一定會依編輯器所顯示的步驟名稱記載。  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> 編輯工作順序

利用下列程序修改現有的工作順序：  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在 [工作順序]  清單中，選取要編輯的工作順序。  

3. 在功能區的 [首頁]  索引標籤上，在 [工作順序]  群組中，選取 [編輯]  。 接著，執行下列其中一個動作：  

    - **新增步驟**：依序選取 [新增]  、[類別]，以及要新增的步驟。 例如，若要新增[執行命令列](task-sequence-steps.md#BKMK_RunCommandLine)的步驟，請選取 [新增]  ，選擇 [一般]  類別，然後選取 [執行命令列]  。 此動作會在目前選取的步驟之後新增步驟。

    - **新增群組**：選取 [新增]  ，然後選擇 [新增群組]  。 新增群組後，即可將步驟新增至群組。  

    - **變更順序**：選取要重新排序的步驟或群組。 然後使用**上移**或**下移**圖示。 一次只能移動一個步驟或群組。 當以滑鼠右鍵按一下群組或步驟時，也可以使用這些動作。

        您可剪下、複製和貼上群組或步驟。 在項目上按一下滑鼠右鍵並選取 [動作]。 您也可以使用標準鍵盤快捷鍵來執行以下動作：

        - 剪下：**CTRL** + **X**
        - 複製：**CTRL** + **C**
        - 貼上：**CTRL** + **V**

    - **移除步驟或群組**：選取步驟或群組，然後選擇 [移除]  。  

4. 選取 [確定]  以儲存您的變更並關閉視窗。 選取 [取消]  以捨棄變更並關閉視窗。 選取 [套用]  以儲存變更，並保持工作順序編輯器開啟。  

如需可用工作順序步驟的清單，請參閱[工作順序步驟](task-sequence-steps.md)。  

> [!IMPORTANT]  
> 如果工作順序因編輯而對物件有任何未關聯的參考，編輯器會要求您先修正該參考，然後才能關閉編輯器。 可能的動作包括：  
>
> - 更正參考
> - 從工作順序中刪除未參考的物件  
> - 暫時停用失敗的工作順序步驟，直到修正或移除中斷的參考為止  

您可同時開啟一個以上工作順序編輯器的執行個體。 此行為可供比較多個工作順序，或在工作順序之間複製和貼上步驟。 您可**編輯**一個工作順序，並**檢視**另一個工作順序，但無法在相同的工作順序上同時執行這兩個動作。

## <a name="conditions"></a><a name="bkmk_conditions"></a> 條件

使用條件來控制工作順序的行為。 請將條件新增至單一步驟或一組步驟。 工作順序會在執行裝置上的步驟之前，先評估條件。 只有在條件評估為 True 時，才會執行該步驟。 如果條件評估為 False，則工作順序會略過該群組或步驟。

使用 [選項]  索引標籤來管理條件：

![在工作順序編輯器的 [選項] 索引標籤上管理條件](media/4621098-copy-paste-ts-condition.png)

下列為可用的條件類型：

- **If 陳述式**：使用 *if* 陳述式對條件進行分組。 您可評估 [所有條件]  、[任何條件]  ，或 [不評估條件]  。

- **工作順序變數**。 在工作順序環境中，評估所有內建、動作、自訂或唯讀[工作順序變數](task-sequence-variables.md)的目前值。 如需詳細資訊，請參閱[步驟條件](using-task-sequence-variables.md#bkmk_access-condition)。

    > [!NOTE]
    > 您可在此條件中使用陣列變數，但必須指定特定的陣列成員。 例如，`OSDAdapter0EnableDHCP` 可指定「第一個」  網路介面卡是否啟用 DHCP。 如需詳細資訊，請參閱[陣列變數](using-task-sequence-variables.md#bkmk_array)。

- **OS 版本**：評估工作順序執行所在裝置的 OS 版本。 這份清單是 Configuration Manager 所使用的所有一般 OS 版本。 若要評估更詳細的 OS 版本 (例如特定版本的 Windows 10)，請使用**查詢 WMI** 條件。

- **作業系統語言**：評估工作順序執行所在裝置的 OS 語言。 這份清單包含 Windows 支援的 257 種語言。

- **檔案屬性**：評估工作順序執行所在裝置上所有檔案的版本或時間戳記。

- **資料夾屬性**：評估工作順序執行所在裝置上所有資料夾的時間戳記。

- **登錄設定**：評估工作順序執行所在裝置上的所有登錄機碼值。

- **查詢 WMI**：指定要在工作順序執行所在裝置上評估的命名空間與查詢。

- **已安裝的軟體**：指定要載入產品資訊的 Windows Installer 檔案，以符合工作順序執行所在裝置。 您可針對特定產品或產品的任何版本進行比對。

### <a name="cmdlets-for-conditions"></a>條件 Cmdlet

使用下列 PowerShell Cmdlet 來管理條件：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>複製和貼上條件

<!-- 4621098 -->

從 1910 版開始，若想要在步驟之間重複使用條件，現在可在工作順序編輯器中複製及貼上條件。 選取要剪下或複製的條件。 如果條件有子系，則會複製整個區塊。 如果 [剪貼簿] 上有條件，您可以使用下列選項貼上條件：

- 在插入點之前貼上
- 在插入點之後貼上
- 在插入點底下貼上 (僅適用於巢狀條件)

使用標準鍵盤快速鍵來複製 (**CTRL** + **C**) 及剪下 (**CTRL** + **X**)。 標準 **CTRL** + **V** 鍵盤快速鍵會執行 [在插入點之後貼上]  動作。

還有新的選項可讓您在清單中向上或向下移動條件。

> [!Note]  
> 您可以在工作順序中的步驟之間複製及貼上條件。 它不支援在不同的工作順序之間執行此動作。

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> 回收鎖定以進行編輯

<!--3699337-->
如果 Configuration Manager 主控台停止回應，您可能遭到鎖定，而必須等候 30 分鐘鎖定逾時，才能做進一步變更。 此鎖定是 Configuration Manager SEDO (分散式物件序列化編輯) 系統的一部分。 如需詳細資訊，請參閱 [Configuration Manager SEDO](../../develop/core/understand/sedo.md)。

從 1906 版開始，可清除工作順序上的鎖定。 此動作僅適用於擁有鎖定的使用者帳戶，且必須在站台授與鎖定的相同來源裝置上進行。 當您嘗試存取鎖定的工作順序時，您現在可以**捨棄變更**，並繼續編輯物件。 反正這些變更在鎖定逾時後也會遺失。

> [!TIP]
> 從 1910 版開始，您現在可以在 Configuration Manager 主控台中清除任何物件上的鎖定。 如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../core/servers/manage/admin-console.md#bkmk_sedo)。<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> 搜尋

<!-- 4621085 -->

如果您有包含許多群組和步驟的大型工作順序，可能很難找到特定步驟。 從 1910 版開始，現在可在工作順序編輯器中進行搜尋。 這項動作可讓您更快地在工作順序中找到步驟。

![在工作順序編輯器中進行搜尋](media/4621085-task-sequence-search.png)

輸入字詞以開始搜尋。 您可使用下列類型來限定搜尋範圍：

- 步驟名稱
- 步驟描述
- 步驟類型
- 群組名稱
- 群組描述
- 變數名稱
- 條件
- 其他內容，例如變數值或命令列等字串

依預設會啟用所有範圍。

您也可以利用以下屬性篩選所有步驟：

- 發生錯誤時仍繼續
- 具有條件

依預設不會啟用任何一項篩選。

在您進行搜尋時，編輯器視窗會以黃色醒目提示符合您搜尋準則的步驟。

利用下列鍵盤快速鍵迅速存取這些搜尋欄位並巡覽搜尋結果：

- **CTRL** + **F**：輸入搜尋字串
- **CTRL** + **O**：選取搜尋選項來設定結果範圍
- **F3** 或 **Enter**：往下一個結果
- **SHIFT** + **F3**：返回上一個結果

## <a name="see-also"></a>請參閱

- [管理及建立工作順序](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [關於工作順序步驟](task-sequence-steps.md)

- [如何使用工作順序變數](using-task-sequence-variables.md)

- [使用 Configuration Manager 主控台](../../core/servers/manage/admin-console.md)
