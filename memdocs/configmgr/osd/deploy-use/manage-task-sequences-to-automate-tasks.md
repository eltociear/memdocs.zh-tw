---
title: 管理工作順序
titleSuffix: Configuration Manager
description: 建立、編輯、部署、匯入和匯出工作順序，以在環境中管理它們並自動化工作。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5871ac29f8b5d4adb9866e091042300df1d64832
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690526"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>管理工作順序，將工作自動化

適用於：  Configuration Manager (最新分支)

使用工作順序，以在 Configuration Manager 環境中自動化步驟。 這些步驟可將 OS 映像部署至目的地電腦，從一組 OS 安裝檔中建立及擷取 OS 映像，以及擷取和還原使用者狀態資訊。 工作順序位於 Configuration Manager 主控台中。 在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  。 [工作順序]  節點包括您建立的子資料夾，會在整個 Configuration Manager 階層中重複。 如需規劃資訊，請參閱[自動化工作的規劃考量](../plan-design/planning-considerations-for-automating-tasks.md)。  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a> 建立

使用 [建立工作順序精靈] 建立工作順序。 此精靈可建立下列類型的工作順序：  

- [安裝 OS 的工作順序](create-a-task-sequence-to-install-an-operating-system.md)：建立安裝 OS 的步驟。 它也包括移轉使用者資料、包含軟體更新及安裝應用程式的選項。

- [升級 OS 的工作順序](create-a-task-sequence-to-upgrade-an-operating-system.md)：建立升級 OS 的步驟。 它也包括包含軟體更新和安裝應用程式的選項。

- [用於擷取 OS 的工作順序](create-a-task-sequence-to-capture-an-operating-system.md)：建立從參照電腦建置和擷取 OS 的步驟。 您可以包含軟體更新，並在參照電腦上安裝應用程式，然後才擷取映像。

- [擷取和還原使用者狀態的工作順序](create-a-task-sequence-to-capture-and-restore-user-state.md)：將步驟新增至現有的工作順序，以擷取和還原使用者狀態資料。

- [自訂工作順序](create-a-custom-task-sequence.md)：此類型不會為工作順序新增任何步驟。 在您建立此工作順序之後，請編輯它並新增步驟。

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a> 編輯  

請藉由新增或移除步驟、新增或移除群組，或變更步驟的順序，來修改工作順序。 如需詳細資訊，請參閱[使用工作順序編輯器](../understand/task-sequence-editor.md)。

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a> 軟體中心屬性

使用下列程序設定軟體中心中所顯示工作順序的詳細資料。 這些詳細資料僅供參考。  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 選取要編輯的工作順序，然後選取 [內容]  。  

3. 在 [一般]  索引標籤上，可以使用下列軟體中心設定︰  

    - **需要重新啟動**：讓使用者知道在安裝期間是否需要重新啟動。  

    - **下載大小 (MB)** ：指定軟體中心內針對工作順序顯示的 MB 數。  

    - **估計執行時間 (分鐘)** ：指定軟體中心內針對工作順序顯示的估計執行時間 (分鐘)。  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a> 進階設定

請使用下列程序來設定 Configuration Manager 用戶端上的工作順序行為。  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 選取要編輯的工作順序，然後選取 [內容]  。  

3. 在 [進階]  索引標籤上，可用的設定如下：  

    - **先執行其他程式**：選取此選項即可在工作順序執行之前，先執行另一個套件中的程式。 根據預設，會清除此核取方塊。 您不需要個別部署您指定要先執行的程式。  

        > [!IMPORTANT]
        > 此設定僅適用於在完整 OS 中執行的工作順序。 如果您使用 PXE 或開機媒體來啟動工作順序，則 Configuration Manager 會忽略此設定。  

        - **套件**：瀏覽包含要在此工作順序前執行之程式的套件。  

        - **程式**：選取要在此工作順序前執行的程式。  

        > [!NOTE]  
        > 如果選取的程式無法在用戶端上執行，工作順序就不會執行。 如果成功執行選取的程式，該程式並不會再次執行，即使在相同的用戶端上重新執行工作順序也一樣。  

    - **工作順序通知**：選取此選項以隱藏 [有新的軟體可供使用]  快顯通知。 您仍然會在軟體中心的通知區域中看到「新軟體」  圖示。 預設會停用這個選項。  

    - **在部署的電腦上停用此工作順序**：如果您選取此選項，Configuration Manager 會暫時停用包含此工作順序的所有部署。 它也會從可供執行的部署清單中移除此工作順序。 此工作順序將等到您啟用它之後，才會執行。 預設會停用這個選項。  

    - **允許的執行時間上限**：指定您預期工作順序在目的地電腦上執行的時間上限 (以分鐘為單位)。 使用等於或大於零的整數。 此值預設為 120 分鐘。  

        > [!IMPORTANT]  
        > 如果您使用您部署此工作順序之集合的維護期間，當 [允許的執行時間上限]  比排定的維護期間長時，可能會發生衝突。 如果您將執行時間上限設定為 [0]  ，則工作順序會在維護期間啟動。 它會繼續執行，直到維護期間關閉後完成或失敗為止。 因此，執行時間上限設定為 **0** 的工作順序可能會在其維護期間結束後繼續執行。 如果您將執行時間上限設定為超過任何可用維護期間長度的特定期間 (非零)，則該工作順序將不會執行。 如需詳細資訊，請參閱[如何使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

        如果您將此值設定為 [0]  ，Configuration Manager 就會將允許的執行時間上限評估為 **12** 小時 (720 分鐘) 以監視進度。 不過，只要倒數的持續時間不超過維護期間值的長度，工作順序就會啟動。  

        > [!NOTE]
        > 當其達到執行時間上限時，如果您不允許使用者與所需的部署互動，則 Configuration Manager 會停止該工作順序。 如果工作順序本身並未停止，Configuration Manager 就會在達到允許的執行時間上限之後，停止監視該工作順序。

    - **使用開機映像**：在工作順序執行時，使用選取的開機映像。 選取 [瀏覽]  以選取不同的開機映像。 將此選項取消選取，即可在工作順序執行時，停用選取的開機映像。  

    - **此工作順序可以在任何平台上執行**：如果您選取此選項，工作順序執行時，Configuration Manager 將不會檢查目的地電腦的平台類型。 預設會選取這個選項。  

    - **此工作順序只能在指定的用戶端平台上執行**：這個選項可指定能執行此工作順序的處理器、OS 版本和 Service Pack。 當您選取此選項時，請從清單中至少選取一個平台。 預設不會選取任何平台。 Configuration Manager 會將此資訊用於評估集合中哪部目的地電腦會接收已部署的工作順序。  

        > [!NOTE]  
        > 如果您從開機媒體或 PXE 來執行工作順序，則 Configuration Manager 會忽略此選項。 工作順序會以就像已選取 [此程式可以在任何平台上執行]  選項的方式執行。  

## <a name="high-impact-settings"></a>高影響力設定

您可以將工作順序設定為有高影響力，並自訂要讓使用者在執行工作順序時收到的訊息。

> [!WARNING]
> 如果您使用 PXE 部署，並以網路介面卡作為第一個開機裝置來設定裝置硬體，則這些裝置就可以自動啟動 OS 部署工作順序，而不需要使用者互動。 部署驗證不會管理此設定。 雖然此設定可以簡化處理程序並減少使用者互動，但會將裝置置於意外重新安裝映像的更高風險中。

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>將工作順序設定為具有強烈影響的工作順序

使用下列程序將工作順序設定為具有強烈影響。

> [!NOTE]  
> 任何符合特定條件的工作順序都會自動定義為具有強烈影響。 如需詳細資訊，請參閱[管理高風險部署](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 選取要編輯的工作順序，然後選取 [內容]  。  

3. 在 [使用者通知]  索引標籤上，選取 [這是具有強烈影響的工作順序]  。  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>建立高風險部署的自訂通知

使用下列程序來為具有強烈影響的部署建立自訂通知。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 選取要編輯的工作順序，然後選取 [內容]  。  

3. 在 [使用者通知]  索引標籤上，選取 [使用自訂文字]  。  

    > [!NOTE]
    > 選取 [這是影響很高的工作順序]  時，您只能設定使用者通知文字。  

4. 進行以下設定：  

    > [!Note]  
    > 每個文字方塊的上限為 255 個字元。  

    - **使用者通知標題文字**：指定在軟體中心使用者通知上顯示的藍色文字。 例如，在預設使用者通知中，本節包含：「請確認是否要升級這部電腦的作業系統」。  

    - **使用者通知訊息文字**：有三個文字方塊提供自訂通知的內文。 所有文字方塊都會要求您加入文字。  

        - 第一個文字方塊：指定本文，通常包含使用者指示。 例如，在預設使用者通知中，本節包含：「升級作業系統需要一些時間，而且您的電腦可能會重新啟動數次」。  

        - 第二個文字方塊：指定本文下的粗體文字。 例如，在預設使用者通知中，本節包含：「這項就地升級會安裝新的作業系統，並自動遷移您的應用程式、資料和設定」。  

        - 第三個文字方塊：指定粗體文字下的最後一行文字。 例如，在預設使用者通知中，本節包含：「按一下 [安裝] 開始安裝。 否則，請按一下 [取消]。」  

#### <a name="example"></a>範例

假設您在內容中設定下列自訂通知。

![工作順序內容的自訂 [使用者通知] 索引標籤](../media/user-notification.png)

終端使用者從軟體中心開啟安裝時，會顯示下列通知訊息。

![軟體中心發給終端使用者的自訂工作順序通知](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a> 電源計劃的效能改善

<!--3555926-->

從 1910 版開始，您現在可以使用 [高效能] 電源計劃來執行工作順序。 此選項可改善工作順序的整體速度。 它會將 Windows 設定為使用內建的高效能電源計劃，以更高的耗電量來提供最大的效能。 針對新的工作順序，此選項預設為開啟。

在大多數情況下，當工作順序啟動時，會記錄目前啟用的電源計劃。 然後，它會將使用中的電源計劃切換為 Windows 預設**高效能**計劃。 如果工作順序重新啟動電腦，它會重複此程序。 在工作順序結束時，它會將電源計劃重設為儲存的值。 此功能同時適用於 Windows 與 Windows PE，但對虛擬機器不會有任何影響。

- 如果在 Windows PE 中啟動工作順序，則工作順序不會記錄目前啟用的電源計劃供日後重複使用。

- 將電腦重新安裝映像的 OS 部署工作順序 (抹除和載入) 不會保留舊 OS 電源計劃設定。 工作順序結束時，會還原預設的**平衡**電源計劃。

> [!Important]
> 若要利用這個 Configuration Manager 新功能，請在更新站台之後，也將用戶端更新為最新版本。 此外，也請更新開機映像以包括最新的用戶端元件。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [作業系統]  ，然後選取 [工作順序]  節點。

1. 建立或選擇現有的工作順序，然後選取 [屬性]  。

1. 切換至 [效能]  索引標籤。

1. 啟用 [以高效能電源計劃執行]  選項。

> [!Warning]
> 在低效能硬體上，請謹慎使用此設定。 長時間執行密集的系統作業可能會造成低端硬體的負擔。 請洽詢您的硬體製造商以取得特定指導方針。

### <a name="known-issue"></a>已知問題

<!-- 5554928 -->

您必須建立新的工作順序部署來啟用或停用此設定，以獲得高效能。 新設定顯示在現有的部署上，但無法套用。<!-- SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a> 發佈參考的內容  

在用戶端執行會參考內容的工作順序之前，請先將該內容發佈到發佈點。 您隨時都可以選取工作順序並發佈其內容，以便建立要發佈的新參照套件清單。 如果您以更新過的內容變更工作順序，則在重新發佈內容之後，用戶端才能使用該內容。 利用下列程序，發佈由工作順序所參照的內容。  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>將參照的內容發佈到發佈點的流程  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在 [工作順序]  清單中，選取要發佈的工作順序。  

3. 在功能區 [常用]  索引標籤上的 [部署]  群組中，選取 [發佈內容]  。 此動作會啟動 [發佈內容精靈]。  

4. 在 [一般]  頁面上，確認已針對發佈選取正確的工作順序。  

5. 在 [內容]  頁面上，確認要發佈的內容 (例如工作順序所參照的開機映像)。  

6. 在 [內容目的地]  頁面上，指定您要發佈工作順序內容的集合、發佈點或目的地點群組。  

    > [!IMPORTANT]  
    > 如果所選工作順序會參考已發佈到特定發佈點的內容，精靈就不會列出該發佈點。  

7. 完成精靈。  

您也可以預先設置工作順序中所參考的內容。 Configuration Manager 可建立壓縮的預先設置內容檔案，其中包含您所選內容的檔案、相關聯的相依性及相關聯的中繼資料。 然後您就可以在站台伺服器、次要站台或發佈點，手動匯入該內容。 如需如何預先設置內容檔案的詳細資訊，請參閱[預先設置內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a> 部署  

如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md)。

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a> 匯出和匯入  

不論是否使用其相關物件，都可以匯出和匯入工作順序。 這個參考的內容包含下列物件：  

- OS 映像  
- 開機映像  
- 套件 (例如用戶端安裝套件)  
- 驅動程式套件  
- 具有相依性的應用程式  

將工作順序匯出和匯入時，請考量下列幾點：  

- Configuration Manager 不會匯出工作順序中的密碼。 如果您將包含密碼的工作順序匯出和匯入，請編輯匯入的工作順序，以重新輸入所有密碼。 請檢閱下列可能包含密碼的步驟：  

  - [加入網域或工作群組](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [連線到網路資料夾](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- 當您使用 [設定動態變數]  步驟來匯出工作順序時，Configuration Manager 不會匯出您以 [密碼值]  設定來設定的變數值。 您匯入工作順序之後，請重新輸入這些變數的值。  

- 當您有多個主要站台時，請在管理中心網站匯入工作順序。  

### <a name="process-to-export-task-sequences"></a>匯出工作順序的流程  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在 [工作順序]  清單中選取要匯出的工作順序。 如果您選取多個工作順序，它們將會全部儲存在一個匯出檔中。  

3. 在功能區的 [首頁]  索引標籤上，在 [工作順序]  群組中，選取 [匯出]  。 這個動作會啟動 [匯出工作順序精靈]。  

4. 在 [一般]  頁面上，指定以下設定：  

    - **檔案**：指定匯出檔案的位置和名稱。 若您直接輸入檔案名稱，請確定在檔案名稱中含有 .zip 副檔名。 若您瀏覽搜尋匯出檔案，精靈會自動新增檔案副檔名。  

    - 如果您不想要匯出工作順序相依性，請取消選取 [匯出所有工作順序相依性]  選項。 根據預設，精靈會掃描所有相關物件，並連同工作順序一起匯出。 這些相依性包括應用程式的任何相依性。  

    - 如果您不想要從套件來源將內容複製到匯出位置，請取消選取 [匯出所選工作順序和相依性的所有內容]  選項。 如果您選取此選項，[匯入工作順序精靈] 就會使用匯入路徑作為新套件來源位置。  

    - **系統管理員註解**：新增要匯出之工作順序的描述。  

5. 完成精靈。  

精靈會建立以下輸出檔案：  

- 如果您未匯出內容：一個 .zip 檔案。  

- 如果您有匯出內容：一個 .zip 檔案，以及名為 *export*_files 的資料夾，此處 *export* 是包含所匯出內容的 .zip 檔名稱。  

若您在匯出工作順序時包含內容，請確認您已複製 .zip 檔案和 export  _files 資料夾，否則匯入動作會失敗。  

### <a name="process-to-import-task-sequences"></a>匯入工作順序的流程  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [匯入工作順序]  。 這個動作會啟動 [匯入工作順序精靈]。  

3. 在功能區的 [一般]  頁面上，指定匯出的 .zip 檔。  

4. 在 [檔案內容]  頁面上，針對您要匯入的每個物件，選取您要求的動作。 此頁會顯示 Configuration Manager 所找到要匯入的所有物件。  

    - 若該物件從未匯入，請選取 [新建]  。  

    - 若過去已經匯入該物件，請選取以下其中一種動作：  

        - **忽略重複項目** (預設)：此動作不會匯入物件。 精靈會將現有物件連結到工作順序。  

        - **覆寫**：此動作會以匯入的物件覆寫現有物件。 若為應用程式，您可以新增修訂版來更新現有應用程式，或建立新的應用程式。  

5. 完成精靈。  

匯入工作順序後，編輯工作順序以指定任何原先位於原始工作順序內的密碼。 基於安全考量，將不會匯出密碼。  

## <a name="return-to-previous-page-on-failure"></a>失敗時返回上一頁

當您執行工作順序但失敗時，則可返回該工作順序精靈的上一頁。 在先前版本的 Configuration Manager 中，您必須在失敗時重新啟動工作順序。 在下列情況下使用 [上一步]  按鈕：

- 當電腦在 Windows PE 中啟動時，在工作順序可用之前，可能會顯示工作順序啟動程序對話方塊。 當您在此情況下選取 [下一步] 時，工作順序的最後一頁會顯示訊息，指出沒有工作順序可用。 現在，您可以選取 [上一步]  重新搜尋可用的工作順序。 您可以重複此程序直到工作順序可用為止。  

- 當您執行工作順序，但發佈點上尚未提供相依內容套件時，工作順序將會失敗。 如果遺失的內容尚未發佈，請立即發佈。 或是等候內容可在發佈點上使用。 然後選取 [上一頁]  讓工作順序再次搜尋內容。

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a> 集合和裝置變數

您可以為電腦與集合定義自訂工作順序變數。 您為電腦定義的變數稱為個別電腦工作順序變數。 針對集合所定義的變數會參照為個別集合的工作順序變數。 如需詳細資訊，請參閱[集合和裝置變數](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)。

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a> 其他動作  

當您選取工作順序時，可使用其他動作來管理工作順序。  

### <a name="edit"></a>編輯

如需詳細資訊，請參閱[使用工作順序編輯器](../understand/task-sequence-editor.md#bkmk_edit)。

### <a name="enable"></a>啟用

啟用工作順序，以便讓用戶端執行該工作順序。 您不需要在啟用工作順序之後，重新部署該工作順序。  

### <a name="disable"></a>停用

停用工作順序，使其無法在電腦上執行。 您可以部署已停用的工作順序，但必須等到您啟用該工作順序之後，電腦才會執行它。  

### <a name="export"></a>匯出

如需詳細資訊，請參閱[匯出和匯入工作順序](#BKMK_ExportImport)。

### <a name="copy"></a>複製

製作選定工作順序的複本。 若要建立以現有工作順序為基礎的新工作順序，此動作會相當有用。

在資料夾內製作工作順序複本時，複本會列在該資料夾內，直到您重新整理工作順序節點。 重新整理後，負本會顯示在根資料夾中。  

### <a name="refresh"></a>重新整理

重新整理所選工作順序的詳細資料。

### <a name="delete"></a>刪除

刪除選取的工作順序。

### <a name="create-phased-deployment"></a>建立階段式部署

如需詳細資訊，請參閱[建立階段式部署](create-phased-deployment-for-task-sequence.md)。

### <a name="deploy"></a>部署

如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md)。

### <a name="distribute-content"></a>發佈內容

啟動 [發佈內容精靈] 以將參考的物件傳送至發佈點。

### <a name="create-prestaged-content-file"></a>建立預先設置的內容檔案

啟動建立預先設置的內容檔案精靈，以預先設置工作順序內容。 如需如何建立預先設置的內容檔案的詳細資訊，請參閱[預先設置的內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。

### <a name="move"></a>移動

將選取的工作順序移至 [工作順序]  節點中的另一個資料夾。

### <a name="set-security-scopes"></a>設定安全性範圍

選取所選工作順序的安全性範圍。 如需詳細資訊，請參閱 [安全性範圍](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)。

### <a name="properties"></a>屬性

如需詳細資訊，請參閱[設定軟體中心內容](#bkmk_prop-general)和[設定進階的工作順序設定](#bkmk_prop-advanced)。

### <a name="view"></a>檢視

<!--3633146-->
從版本 1902 開始，工作順序上的 [檢視]  動作是預設值。 此動作可讓您查看工作順序步驟，而無需將其鎖定以進行編輯。 如需詳細資訊，請參閱[使用工作順序編輯器](../understand/task-sequence-editor.md#bkmk_view)。

## <a name="see-also"></a>請參閱

- [部署企業作業系統的案例](scenarios-to-deploy-enterprise-operating-systems.md)

- [使用工作順序編輯器](../understand/task-sequence-editor.md)

- [部署工作順序](deploy-a-task-sequence.md)

- [工作順序步驟](../understand/task-sequence-steps.md)

- [集合和裝置變數](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [建立分階段部署](create-phased-deployment-for-task-sequence.md)
