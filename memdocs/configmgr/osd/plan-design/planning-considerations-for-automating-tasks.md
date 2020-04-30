---
title: 針對工作自動化進行規劃
titleSuffix: Configuration Manager
description: 在您使用 Configuration Manager 來建立工作順序以將工作自動化之前先進行規劃。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0348cc245efdfd5e4d1e0bad25a457ea3b1ca609
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708096"
---
# <a name="plan-for-automating-tasks-in-configuration-manager"></a>規劃在 Configuration Manager 中自動執行工作

適用於：  Configuration Manager (最新分支)

您可以在 Configuration Manager 環境中建立工作順序，以將工作自動化。 這些工作的範圍涵蓋從擷取參照電腦上的 OS，到將 OS 部署至一或多部目的地電腦。 工作順序的動作，會在順序的個別步驟中定義。 當工作順序執行時，會在「本機系統」內容的命令列層級執行每個步驟的動作。 此行為意謂著工作順序完全以自動化方式執行，無須任何使用者介入。

## <a name="task-sequence-steps-and-actions"></a><a name="BKMK_TSStepsActions"></a> 工作順序的步驟和動作  

步驟是工作順序的基本元件。 它們可以包含諸如以下的命令：

- 設定和擷取參照電腦的 OS
- 在目的地電腦上安裝 Windows、硬體驅動程式、Configuration Manager 用戶端及軟體

步驟的動作會定義工作順序步驟的命令。 動作類型有兩種：  

- 一種是您使用命令列字串來定義的動作，稱為「自訂動作」   
- 一種是由 Configuration Manager 預先定義的動作，稱為「內建動作」  。  

工作順序可以執行任何組合的自訂和內建動作。  

工作順序步驟也可包含控制步驟行為的條件。 這些行為包括在發生錯誤時是要停止工作順序，還是繼續工作順序。 其中一種條件是工作順序變數。 例如，使用 **SMSTSLastActionRetCode** 變數可測試上一個步驟的條件。 請將條件新增至單一步驟或一組步驟。  

工作順序會循序處理步驟。 此順序包括步驟的動作，以及該步驟上的任何條件。 當 Configuration Manager 開始處理工作順序步驟時，會等到上一個動作完成後，才開始下一個步驟。

當工作順序符合下列情況時，就會被視為完成：

- 工作順序的所有步驟都完成  
- 某個失敗的步驟導致 Configuration Manager 在工作順序的所有步驟都完成前，停止執行該工作順序。  

例如，如果工作順序的步驟在發佈點上找不到參考的映像或套件，即表示工作順序包含中斷的參考。 Configuration Manager 會在該時間點停止執行該工作順序，除非失敗的步驟具有在發生錯誤時仍繼續執行的條件。  

> [!IMPORTANT]  
> 根據預設，若某個步驟或動作失敗，則工作順序會失敗。 如果想要在步驟失敗後繼續執行工作順序，請編輯工作順序，並切換到 [選項]  索引標籤，然後選取 [發生錯誤時仍繼續]  。  

如需可新增至工作順序之步驟的詳細資訊，請參閱[工作順序步驟](../understand/task-sequence-steps.md)。  

## <a name="task-sequence-groups"></a><a name="BKMK_TSGroups"></a> 工作順序群組  

您可以將多個步驟群集在一個工作順序內。 工作順序群組會由名稱、選擇性描述及任何選擇性條件所組成。 工作順序會先將群組條件當作一個單位進行評估，然後才繼續進行下一個步驟。 請將群組嵌入彼此的巢狀結構內，或包含步驟和子群組的混合組合。 群組非常適用於合併多個共用一般條件的步驟。  

請為工作順序群組指派名稱。 此名稱不一定要具有唯一性。 您也可以為工作順序群組提供選擇性描述。  

> [!IMPORTANT]  
> 根據預設，當群組中的任何步驟或內嵌群組失敗時，工作順序群組也會失敗。 如果您想要讓工作順序在步驟或內嵌的群組失敗後繼續執行，請在步驟或群組上設定 [發生錯誤時仍繼續]  選項。  

下表顯示當您組成步驟時，[發生錯誤時仍繼續]  選項的運作方式。  

在此範例中，有兩個工作順序群組，每個群組皆包含三個工作順序步驟。  

|工作順序群組或步驟|發生錯誤時仍繼續設定|  
|---------------------------------|-------------------------------|  
|**工作順序群組 1**|**[發生錯誤時仍繼續]** 已選取。|  
|工作順序步驟 1|**[發生錯誤時仍繼續]** 已選取。|  
|工作順序步驟 2|未設定。|  
|工作順序步驟 3|未設定。|  
|**工作順序群組 2**|未設定。|  
|工作順序步驟 4|未設定。|  
|工作順序步驟 5|未設定。|  
|工作順序步驟 6|未設定。|  

- 如果工作順序步驟 1 失敗，工作順序會繼續執行工作順序步驟 2。  

- 如果工作順序步驟 2 失敗，工作順序不會執行工作順序步驟 3。 由於工作順序群組 1 已設定為 [發生錯誤時仍繼續]  ，因此工作順序會繼續執行工作順序群組 2。 它會接著執行工作順序步驟 4。  

- 如果工作順序步驟 4 失敗，則不會再執行任何其他步驟。 工作順序之所以會失敗，是因為並未針對工作順序群組 2 設定 [發生錯誤時仍繼續]  設定。  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>將子工作順序新增至工作順序

<!--1261338-->

新增會執行另一個工作順序的新工作順序步驟。 此步驟會建立工作順序之間的父子關聯性。 使用此步驟可讓您建立更多可以重複使用的模組化工作順序。  

如需詳細資訊，請參閱[執行工作順序](../understand/task-sequence-steps.md#child-task-sequence)。

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

## <a name="task-sequence-variables"></a><a name="BKMK_TSVariables"></a> 工作順序變數  

工作順序變數是一組成對的名稱和值。 它們可為電腦、OS 及 Configuration Manager 用戶端上的使用者狀態設定工作，提供設定和 OS 部署設定。 工作順序變數提供一種機制，可設定及自訂工作順序中的步驟。  

當您執行工作順序時，它會將許多工作順序設定儲存成環境變數。 您可以存取或變更內建工作順序變數的值。 您也可以建立新的工作順序變數，以自訂工作順序在目的地電腦上執行的方式。  

請使用工作順序變數來執行下列動作：  

- 設定工作順序動作的設定  

- 為工作順序步驟提供命令列引數  

- 評估一個可決定是否執行工作順序或群組的條件  

- 提供工作順序中使用的自訂指令碼值  

例如，您有一個包含 [加入網域或工作群組]  工作順序步驟的工作順序。 請將該工作順序部署至不同的集合，其中集合的成員資格取決於網域成員資格。 為每個集合的網域名稱指定個別集合工作順序變數。 然後使用該工作順序變數，在工作順序中提供適當的網域名稱。  

如需詳細資訊，請參閱[如何使用工作順序變數](../understand/using-task-sequence-variables.md)。

## <a name="create-a-task-sequence"></a><a name="BKMK_TSCreate"></a> 建立工作順序  

使用 [建立工作順序精靈] 建立工作順序。 該精靈會建立執行特定工作的內建工作順序，或執行許多不同工作的自訂工作順序。 此精靈可讓您建立下列類型的工作順序：

- 在目的地電腦上安裝現有 OS 映像  

- 建置和擷取參照電腦的 OS 映像  

- 在目的地電腦上從 OS 升級套件升級至 Windows 10

- 建立會執行自訂工作或特製化 OS 部署的自訂工作順序  

如需詳細資訊，請參閱[建立工作順序](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence)。  

## <a name="edit-a-task-sequence"></a><a name="BKMK_TSEdit"></a> 編輯工作順序  

請使用 [工作順序編輯器]  來編輯工作順序。 編輯器可以對工作順序做以下變更：  

- 從工作順序新增或移除步驟  

- 變更工作順序的步驟順序  

- 新增或移除步驟群組  

- 指定當發生錯誤時工作順序是否要繼續執行  

- 為工作順序的步驟和群組新增條件  

> [!IMPORTANT]  
> 如果工作順序因編輯而對物件有任何未關聯的參考，編輯器會要求您先修正該參考，然後才能關閉編輯器。 可能的動作包括：  
>
> - 更正參考
> - 從工作順序中刪除未參考的物件  
> - 暫時停用失敗的工作順序步驟，直到修正或移除中斷的參考為止  

如需如何編輯工作順序的詳細資訊，請參閱[使用工作順序編輯器](../understand/task-sequence-editor.md)。  

## <a name="deploy-a-task-sequence"></a><a name="BKMK_TSDeploy"></a> 部署工作順序  

您可以將工作順序部署到位於任何 Configuration Manager 集合中的目的地電腦。 請使用內建的 [所有未知電腦]  集合，以將作業系統部署到未知的電腦。 您無法將工作順序部署到使用者集合。  

> [!IMPORTANT]  
> 請勿部署會將作業系統安裝到不適當集合的工作順序。 請確定您要對其部署工作順序的集合僅包含您要安裝 OS 的電腦。 為了協助防止進行不必要的 OS 部署，請設定適用於高風險部署的設定。 如需詳細資訊，請參閱 [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (高風險部署的管理設定)。  

每一部接收工作順序的目的地電腦，會根據部署中所指定的設定執行工作順序。 工作順序本身並不包含相關聯的檔案或程式。 工作順序所參考的任何檔案都必須已經存在於目的地電腦上，或儲存於用戶端可存取的發佈點上。

> [!NOTE]  
> 工作順序會安裝程式所參考的套件，即使目的地電腦上已經安裝該程式或套件也一樣。
>
> 如果工作順序會安裝應用程式，則只有在下列情況下，才會安裝應用程式：符合應用程式的需求規則，且根據為應用程式指定的偵測方法，尚未安裝該應用程式。  

當 Configuration Manager 用戶端下載用戶端原則時，Configuration Manager 用戶端會執行工作順序部署。 若要觸發此動作，而不等到下一個輪詢週期才執行，請參閱 [起始 Configuration Manager 用戶端的原則抓取](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

將工作順序部署到啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定是否要在部署期間停用裝置上的寫入篩選器，然後在部署後再重新啟動該裝置。 如果未停用寫入篩選器，工作順序就會部署至暫時重疊，而在裝置重新啟動時將無法供使用。  

> [!NOTE]  
> 當您將工作順序部署到 Windows Embedded 裝置時，請確定該裝置是具有已設定之維護期間的集合成員。 這可讓您在停用並啟用寫入篩選器時，以及當重新啟動裝置時進行管理。  
>
> 如果用戶端在維護期間外下載工作順序，便會下載兩次工作順序。 在此情況下，用戶端會下載工作順序、停用寫入篩選器、重新啟動電腦，然後再次下載工作順序。 之所以會有此行為，是因為原先將工作順序下載至暫時重疊，而在裝置重新啟動時會清除此重疊。  

如需如何部署工作順序的詳細資訊，請參閱[部署工作順序](../deploy-use/deploy-a-task-sequence.md)。  

## <a name="export-and-import"></a><a name="BKMK_TSExportImport"></a> 匯出和匯入

Configuration Manager 可讓您匯出和匯入工作順序。 當您匯出工作順序時，可將工作順序所參照的物件包含進去。

如需詳細資訊，請參閱[匯出和匯入工作順序](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport)。  

## <a name="run-a-task-sequence"></a><a name="BKMK_TSRun"></a> 執行工作順序  

執行工作順序時，一律是使用「本機系統」帳戶。 當工作順序執行時，Configuration Manager 用戶端會先檢查是否有任何參考的套件，然後才啟動工作順序的步驟。 如果它無法驗證或下載所參考的套件，工作順序就會針對相關聯的工作順序步驟傳回錯誤。  

> [!Note]  
> [執行命令列]  工作順序步驟可讓您以不同的帳戶執行命令。  

如果您設定讓某個工作順序部署進行下載和執行，Configuration Manager 用戶端會將所有相依內容下載至其快取。 如果用戶端快取大小太小，或找不到內容，工作順序就會失敗。 用戶端會產生狀態訊息。

您也可以指定讓用戶端只在需要內容時才下載內容。 若要執行此動作，請在工作順序部署中，選取 [視執行工作順序所需，將內容下載到本機]  。 另一個選項是 [從發佈點執行程式]  。 使用此選項時，用戶端會直接從發佈點安裝檔案，而不先將檔案下載至快取。

當您將工作順序部署設定為 [可供使用]  時，用戶端如果找不到工作順序的相依內容，就會立即傳送錯誤。 針對 [必要]  部署，Configuration Manager 用戶端在此情況下則會等候。 它會重新嘗試下載內容，直到期限到期為止，以因應內容尚未複寫到用戶端可存取之內容位置的狀況。  

當工作順序成功完成或失敗時，Configuration Manager 會將此狀態記錄在用戶端歷程記錄中。

在工作順序於電腦上啟動之後，您便無法將它取消或停止。  

> [!IMPORTANT]  
> 如果工作順序步驟會要求電腦重新啟動，用戶端就必須能夠在開機時進入已格式化的磁碟分割。 否則，不論您在工作順序中指定何種錯誤處理方式，工作順序都會失敗。  

當工作順序的相依物件更新至較新版本時，所有參考該套件的工作順序都會自動更新。 不論您已部署多少個更新，都會參考最新版本。  

## <a name="use-maintenance-windows"></a><a name="BKMK_TSMaintenanceWindow"></a> 使用維護視窗

您可以藉由為裝置集合定義一個維護期間，指定工作順序何時可以執行。 您需為維護期間設定開始日期、開始和完成時間，以及定期模式。 為維護期間設定排程時，您可以指定維護期間僅套用至工作順序。 如需詳細資訊，請參閱[如何使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

> [!IMPORTANT]  
> 設定維護期間執行工作順序時，一旦工作順序開始之後，即使將維護期間關閉，該順序仍會持續執行。  

如果裝置已套用多個維護視窗，則用戶端可能會忽略**所有部署**維護視窗。 從 1810 版開始，請使用下列用戶端設定來控制此行為：**當 [軟體更新] 維護視窗可以使用時，允許安裝 [所有部署] 維護視窗中的軟體更新**。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint)<!-- SCCMDocs-pr #4596 -->


## <a name="task-sequences-and-the-network-access-account"></a><a name="BKMK_TSNetworkAccessAccount"></a> 工作順序和網路存取帳戶  

> [!Important]  
> 某些 OS 部署案例不需要使用網路存取帳戶。 如需詳細資訊，請參閱[Enhanced HTTP](#enhanced-http) (增強 HTTP)。

雖然工作順序只會在「本機系統」帳戶的環境中執行，但在下列情況下，您可能需要設定[網路存取帳戶](../../core/plan-design/hierarchy/accounts.md#network-access-account)：  

- 如果工作順序嘗試存取發佈點上的 Configuration Manager 內容。 請正確設定網路存取帳戶，否則工作順序將會失敗。

- 使用開機映像來起始 OS 部署時。 在此情況下，Configuration Manager 會使用 Windows PE 環境 (並非完整 OS)。 Windows PE 環境會使用自動產生的隨機名稱，而此名稱不是任何網域的成員。 如果您未正確設定網路存取帳戶，電腦便無法存取工作順序所需的內容。  

> [!NOTE]  
> 網路存取帳戶一律不用來作為執行應用程式、安裝應用程式、安裝更新或執行工作順序的安全性內容。 網路存取帳戶只用來存取網路上的相關資源。  

如需有關網路存取帳戶的詳細資訊，請參閱[網路存取帳戶](../../core/plan-design/hierarchy/accounts.md#network-access-account)。  

### <a name="enhanced-http"></a>增強 HTTP
<!--1358278-->

當啟用 [增強 HTTP]  時，下列案例不需要網路存取帳戶即可從發佈點下載內容：

- 從開機媒體或 PXE 執行的工作順序  
- 從軟體中心執行的工作順序  

這些工作順序可以是 OS 部署或自訂。 它也支援工作群組電腦。

如需詳細資訊，請參閱[Enhanced HTTP](../../core/plan-design/hierarchy/enhanced-http.md) (增強 HTTP)。  

> [!Note]  
> 下列 OS 部署案例仍然需要使用網路存取帳戶：
>  
> - 工作順序[部署選項](../deploy-use/deploy-a-task-sequence.md)為：**執行工作順序以視需要直接從發佈點存取內容**
> - [要求狀態存放區](../understand/task-sequence-steps.md#BKMK_RequestStateStore)步驟選項為：**如果電腦帳戶無法連線到狀態存放區，則使用網路存取帳戶**
> - 連線到不信任的網域或跨 Active Directory 樹系時
> - [套用 OS 映像](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)步驟選項為：**直接從發佈點存取內容**
> - 工作順序[進階設定](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced)為：**先執行其他程式**
> - [多點傳送](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)  

## <a name="create-media"></a><a name="BKMK_TSCreateMedia"></a> 建立媒體

您可寫入工作順序與其相關檔案以及數種媒體類型的相依性。 Configuration Manager 支援使用卸除式媒體 (例如 DVD 或 USB 快閃磁碟機) 作為擷取、獨立及可開機媒體。 預先設置的媒體則使用 Windows 映像檔 (WIM)。  

建立媒體時，請指定密碼來控制存取。 然後使用者必須在目標電腦上輸入該密碼，才能執行工作順序。  

當您從媒體執行工作順序時，系統不會辨識該媒體的指定處理器架構。 如果指定的架構與目標電腦不相符，工作順序仍然會嘗試執行。 如果媒體的架構與目標電腦的架構不相符，工作順序則會失敗。  

如需詳細資訊，請參閱[建立工作順序媒體](../deploy-use/create-task-sequence-media.md)。  

### <a name="media-types"></a>媒體類型

Configuration Manager 支援下列媒體類型：  

#### <a name="capture-media"></a>擷取媒體

此媒體會擷取您在 Configuration Manager 基礎結構外設定及建立的 OS 映像。 擷取媒體可以包含在工作順序執行前執行的自訂程式。 自訂程式可以與桌面互動、提示使用者輸入數值，或是建立由工作順序使用的變數。  

如需詳細資訊，請參閱[建立擷取媒體](../deploy-use/create-capture-media.md)。  

#### <a name="stand-alone-media"></a>獨立媒體

獨立媒體包含工作順序與可讓工作順序執行的所有必要相關物件。 獨立媒體工作順序可在 Configuration Manager 受到限制或沒有網路連線時執行。 請以下列方式執行獨立媒體：  

- 如果目的地電腦未開機，將會從獨立媒體使用與工作順序相關的 Windows PE 映像，然後工作順序便會開始進行。  

- 手動啟動獨立媒體。 如果使用者已登入電腦，他們便可以從媒體起始工作順序。  

> [!IMPORTANT]  
> 獨立媒體工作順序的步驟必須能夠在不從網路擷取任何資料的情況下執行。 否則，嘗試擷取資料的工作順序步驟將會失敗。 例如，需要發佈點來取得套件的工作順序步驟便會失敗。 如果獨立媒體包含必要的套件，工作順序步驟就會成功。  

如需詳細資訊，請參閱[建立獨立媒體](../deploy-use/create-stand-alone-media.md)。  

#### <a name="bootable-media"></a>可開機媒體

可開機媒體包含啟動目的地電腦時所需的檔案，以便連線到 Configuration Manager 基礎結構。 它會接著根據其集合成員資格來判斷要執行哪些工作順序。 此媒體並未包含工作順序或相依物件。 取而代之的是，用戶端會透過網路下載內容。 當目的地電腦上沒有任何 OS 時，此方法對於新電腦或裸機部署來說，都相當有用。  

如需詳細資訊，請參閱[建立可開機媒體](../deploy-use/create-bootable-media.md)。  

#### <a name="prestaged-media"></a>預先設置的媒體

預先設置的媒體會將 OS 映像部署到未佈建的目的地電腦。 預先設置的媒體會儲存成 Windows 映像檔 (WIM)。 此檔案可由製造商安裝在裸機電腦上，或是安裝在企業預備中心。 預先設置的媒體有一個優點，就是這些位置不需要與您的 Configuration Manager 環境連線。  

如需詳細資訊，請參閱[建立預先設置的媒體](../deploy-use/create-prestaged-media.md)。  

## <a name="next-steps"></a>後續步驟

- [OS 部署的安全性與隱私權](security-and-privacy-for-operating-system-deployment.md)

- [針對 OS 部署做好站台系統角色準備](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
