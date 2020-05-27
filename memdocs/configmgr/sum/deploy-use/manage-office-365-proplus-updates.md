---
title: 管理 Office 365 ProPlus 更新
titleSuffix: Configuration Manager
description: Configuration Manager 會將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器，讓更新能夠部署至用戶端。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 09d8f0a37e9ed4308c5c8ffcf005c788612be235
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709497"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus

適用於：Configuration Manager (最新分支)

> [!Note]
> 從 2020 年 4 月 21 日開始，「Office 365 專業增強版」會重新命名為「Microsoft 365 Apps 企業版」。 如需詳細資訊，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) \(部分機器翻譯\)。 在主控台正在進行更新時，您在 Configuration Manager 主控台與輔助文件中可能仍會看到提及舊名稱。

Configuration Manager 可讓您使用下列方式來管理 Office 365 專業增強版應用程式：

- [部署 Office 365 應用程式](#deploy-office-365-apps)：您可以從 [Office 365 用戶端管理儀表板](office-365-dashboard.md)來啟動 Office 365 安裝程式，讓初始的 Office 365 應用程式安裝體驗更簡單容易。 此精靈可讓您設定 Office 365 安裝設定，從 Office 內容傳遞網路 (CDN) 下載檔案，然後利用該內容來建立並部署指令碼應用程式。

- [部署 Office 365 更新](#deploy-office-365-updates)：您可以使用軟體更新管理工作流程來管理 Office 365 用戶端更新。 當 Microsoft 將新的 Office 365 用戶端更新發佈至 Office 內容傳遞網路 (CDN) 時，Microsoft 也會將更新套件發佈至 Windows Server Update Services (WSUS)。 當 Configuration Manager 將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器之後，更新就可以部署至用戶端。

   > [!NOTE]
   > 從 Configuration Manager 2002 版開始，可將 Office 365 更新匯入已中斷連線的環境。 如需詳細資訊，請參閱[從已中斷連線的 Office 365 更新點同步處理軟體更新](../get-started/synchronize-office-updates-disconnected.md)。   

- [新增 Office 365 更新下載的語言](#bkmk_o365_lang)：您可以為 Configuration Manager 新增支援，以下載 Office 365 所支援任一語言的更新。 這表示，只要 Office 365 支援語言，Configuration Manager 就不需要支援。 在 Configuration Manager 1610 版之前，您所下載及部署的更新，其語言必須與 Office 365 用戶端的語言相同。

- [變更更新頻道](#bkmk_channel)：您可以使用群組原則，將登錄機碼值變更發佈至 Office 365 用戶端，以變更更新通道。

若要檢閱 Office 365 用戶端資訊，並開始執行其中一些 Office 365 管理動作，請使用 [Office 365 用戶端管理儀表板](office-365-dashboard.md)。

## <a name="deploy-office-365-apps"></a>部署 Office 365 應用程式  
在 Office 365 用戶端管理儀表板中啟動 Office 365 安裝程式，便可進行初始的 Office 365 應用程式安裝。 此精靈可讓您設定 Office 365 安裝設定，從 Office 內容傳遞網路 (CDN) 下載檔案，然後針對檔案來建立並部署指令碼應用程式。 在用戶端上安裝 Office 365 並執行 [Office 自動更新工作](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus)之前，Office 365 更新不適用。 基於測試目的，您可以手動執行更新工作。

針對先前的 Configuration Manager 版本，在用戶端上首次安裝 Office 365 應用程式時，必須採取下列步驟：
- 下載 Office 365 部署工具 (ODT)
- 下載 Office 365 安裝來源檔案，包括所有需要的語言套件。
- 產生指定正確 Office 版本與頻道的 Configuration.xml。
- 建立和部署舊版套件或指令碼應用程式，以供用戶端安裝 Office 365 應用程式。

### <a name="requirements"></a>需求
- 執行 Office 365 安裝程式的電腦必須能夠存取網際網路。  
- 執行 Office 365 安裝程式的使用者必須具有精靈中所提供內容位置共用的**讀取**和**寫入**權限。
- 如果您收到 404 下載錯誤，請將下列檔案複製到使用者的 %temp% 資料夾︰
  - [releasehistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>使用 Configuration Manager 1806 版或更高版本部署 Office 365 應用程式： 
從 Configuration Manager 1806 開始，Office 自訂工具已於 Configuration Manager 主控台中與 Office 365 安裝程式整合。 為 Office 365 建立部署時，您可以動態設定最新的 Office 管理能力設定。 <!--1358149-->

1. 在 Configuration Manager 主控台中，巡覽至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。
2. 按一下右上方窗格中的 [Office 365 Installer]。 [Office 365 用戶端安裝精靈] 隨即開啟。
3. 在 [應用程式設定] 頁面上，提供應用程式的名稱和描述，輸入檔案的下載位置，然後按一下 [下一步]。 請使用 &#92;&#92;*server*&#92;*share* 格式來指定位置。
4. 在 [Office 設定] 頁面上，按一下 [移至 Office 自訂工具]。 這會開啟[適用於隨選即用的 Office 自訂工具](https://config.office.com)。
5. 指定 Office 365 安裝所需的設定。 當您完成設定時，請按一下頁面右上方的的 [提交]。 
6. 在 [部署] 頁面上，決定您想要立即部署或稍後部署。 如果您選擇稍後部署，則可以在 [軟體程式庫] > [應用程式管理] > [應用程式] 中找到應用程式。  
7. 確認 [摘要] 頁面中的設定。 
8. 按 [下一步]，然後在 [Office 365 用戶端安裝精靈] 完成後按一下 [關閉]。 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>使用 Configuration Manager 1802 版和先前版本部署 Office 365 應用程式：

1. 在 Configuration Manager 主控台中，巡覽至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。
2. 按一下右上方窗格中的 [Office 365 Installer]。 [Office 365 用戶端安裝精靈] 隨即開啟。
3. 在 [應用程式設定] 頁面上，提供應用程式的名稱和描述，輸入檔案的下載位置，然後按一下 [下一步]。 請使用 &#92;&#92;*server*&#92;*share* 格式來指定位置。
4. 在 [匯入用戶端設定] 頁面上，選擇要從現有的 XML 設定檔匯入 Office 365 用戶端設定，或是要手動指定設定。 完成時按一下 [下一步]。  

    如果您有現成的組態檔，請輸入檔案的位置，然後跳至步驟 7。 您必須以 &#92;&#92;伺服器&#92;共用&#92;檔案名稱.XML 格式來指定位置。
    > [!IMPORTANT]    
    > XML 設定檔中只可包含 [Office 365 ProPlus 用戶端所支援的語言](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016)。

5. 在 [用戶端產品] 頁面上，選取您使用的 Office 365 套件。 選取您想要包含的應用程式。 選取應該包含的任何其他 Office 產品，然後按一下 [下一步]。
6. 在 [用戶端設定] 頁面上，選擇要包含的設定，然後按一下 [下一步]。
7. 在 [部署] 頁面上，選擇是否要部署應用程式，然後按一下 [下一步]。 <br/>如果您選擇不要在精靈中部署套件，請跳至步驟 9。
8. 設定精靈頁面的其餘部分，就像是一般應用程式部署一樣。 如需詳細資訊，請參閱[建立和部署應用程式](../../apps/get-started/create-and-deploy-an-application.md)。
9. 完成精靈。
10. 從 [軟體程式庫] > [概觀] > [應用程式管理] > [應用程式]，可部署或編輯應用程式。    

在您使用 Office 365 安裝程式建立和部署 Office 365 應用程式之後，Configuration Manager 預設並不會管理 Office 更新。 若要讓 Office 365 用戶端收到來自 Configuration Manager 的更新，請參閱[使用 Configuration Manager 部署 Office 365 更新](#deploy-office-365-updates)。

部署 Office 365 應用程式之後，您可以建立自動部署規則，以維護應用程式。 若要建立適用於 Office 365 應用程式的自動部署規則，請從 [Office 365 用戶端管理儀表板](office-365-dashboard.md) 按一下 [建立 ADR]。 選擇產品時，請選取 [Office 365 用戶端]。 如需詳細資訊，請參閱[自動部署軟體更新](automatically-deploy-software-updates.md)。


## <a name="drill-through-required-office-365-updates"></a>鑽研必要的 Office 365 更新
<!--4224414-->
*(於 1906 版推出)*

您可以鑽研合規性統計資料，了解哪些裝置需要特定的 Office 365 軟體更新。 若要檢視裝置清單，您需要檢視更新及裝置所屬集合的權限。 向下切入至裝置清單：

1. 前往 [軟體程式庫] > [Office 365 用戶端管理] > [Office 365 更新]。
1. 選取至少一部裝置所需的任何更新。
1. 查看 [摘要] 索引標籤，然後尋找 [統計資料] 下方的圓形圖。
1. 選取圓形圖旁的 [需要檢視] 超連結，以向下切入至裝置清單。
1. 此動作會帶您前往 [裝置] 下方的臨時節點，以查看需要更新的裝置。 您也可以對節點採取動作，例如從清單建立新的集合。


## <a name="deploy-office-365-updates"></a>部署 Office 365 更新

使用下列步驟以 Configuration Manager 部署 Office 365 更新：

1. [驗證需求](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates)：請參閱文章的＜使用 Configuration Manager 管理 Office 365 用戶端更新的需求＞一節中有關使用 Configuration Manager 管理 Office 365 用戶端更新的需求。  

2. [設定軟體更新點](../get-started/configure-classifications-and-products.md)，以同步處理 Office 365 用戶端更新。 設定分類的 [更新]，然後針對產品選取 [Office 365 用戶端]。 設定軟體更新點使用 [更新] 分類之後，必須同步處理軟體更新。
3. 啟用 Office 365 用戶端從 Configuration Manager 接收更新。 使用 Configuration Manager 用戶端設定或群組原則來啟用用戶端。

    **方法 1**：從 Configuration Manager 1606 版開始，您可以使用 Configuration Manager 用戶端設定來管理 Office 365 用戶端代理程式。 在設定此設定並部署 Office 365 更新之後，Configuration Manager 用戶端代理程式會與 Office 365 用戶端代理程式進行通訊，從發佈點下載更新並安裝它們。 Configuration Manager 採用 Office 365 ProPlus 用戶端的清查設定。    

      1. 在 Configuration Manager 主控台中，按一下 [管理] > [概觀] > [用戶端設定]。  

      2. 開啟適當的裝置設定，以啟用用戶端代理程式。 如需預設和自訂的用戶端設定詳細資訊，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

      3. 按一下 [軟體更新]，然後針對 [啟用管理 Office 365 用戶端代理程式] 設定選取 [是]。  

    **方法 2**：使用 Office 部署工具或群組原則，[啟用 Office 365 用戶端以從 Configuration Manager 接收更新](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient)。  

4. [部署 Office 365 更新](deploy-software-updates.md)至用戶端。

> [!Important]
> - 從 Configuration Manager 1706 版開始，Office 365 用戶端更新已移至 [Office 365 用戶端管理] >[Office 365 更新] 節點。 此移動並不會影響您目前的 ADR 設定。 
> - 在 Configuration Manager 1610 版之前，您所下載及部署的更新，其語言必須與 Office 365 用戶端的語言相同。 例如，假設您的 Office 365 用戶端設定了 en-us 和 de-de 語言。 在站台伺服器上，您只為適用的 Office 365 更新下載和部署 en-us 內容。 使用者從軟體中心開始安裝此更新時，更新會在下載 de-de 內容時停止回應。 

> [!NOTE]  
>
> 如果最近安裝有 Office 365 ProPlus，根據其安裝方式，可能尚未設定更新管道。 在該情況下，會將已部署的更新偵測為不適用。 有一個安裝 Office 365 ProPlus 時建立的[排程自動更新工作](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus)。 在此情況下，這項工作必須至少執行一次，才能設定更新管道，並將更新偵測為適用。
>
> 如果最近安裝有 Office 365 ProPlus，而且未偵測到已部署的更新，基於測試目的，您可以手動啟動 [Office 自動更新] 工作，然後在用戶端上啟動[軟體更新部署評估週期](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process)。 如需有關如何使用工作順序執行此動作的指示，請參閱[使用工作順序更新 Office 365 專業增強版](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence)。

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Office 365 更新的重新啟動行為與用戶端通知
當您將更新部署到 Office 365 用戶端時，重新啟動行為與用戶端通知會根據 Configuration Manager 的版本而有所不同。 下表提供用戶端接收到 Office 365 更新時之終端使用者體驗的相關資訊：

|Configuration Manager 版本 |使用者體驗|  
|----------------|---------------------|
|1706、1710|在安裝更新之前，用戶端會接收到快顯和應用程式內通知，以及倒數計時對話方塊。|
|1802| 在安裝更新之前，用戶端會接收到快顯和應用程式內通知，以及倒數計時對話方塊。 </br>如果在 Office 365 用戶端更新強制執行期間有任何執行中的 Office 365 應用程式，則 Office 應用程式將不會被強制關閉。 相反地，更新安裝將會傳回需要重新啟動系統 <!--510006-->|


> [!Important]
>
>在 Configuration Manager 1706 版中，請注意下列詳細資料：
>
>- 如果必要應用程式的期限在未來 48 小時內並已下載更新內容，則通知圖示會顯示在其工作列的通知區域中。 
>- 如果必要應用程式的期限在未來 7.5 小時內並已下載更新，則會顯示其倒數計時對話方塊。 在期限之前，使用者最多可以延後倒數計時對話方塊三次。 延後時，會在兩小時之後重新顯示倒數計時。 如果未延後，則會有 30 分鐘的倒數計時，而且會在倒數計時到期時安裝更新。
>- 除非使用者按一下通知區域中的圖示，否則可能不會顯示快顯通知。 此外，如果通知區域的空間極小，則除非使用者開啟或展開通知區域，否則看不到通知圖示。 
>- 通知和倒數計時對話方塊可能會於使用者不在裝置上進行工作時啟動。 例如，當裝置整晚鎖定，則系統很可能會強制關閉裝置上正在執行的 Office 應用程式以安裝更新。 關閉應用程式之前，Office 會儲存應用程式資料，以避免資料遺失。 
>- 如果期限是過去時間，或設定成盡快啟動，則可能會強制關閉執行中的 Office 應用程式，而不進行通知。 
>- 如果使用者在期限之前安裝 Office 更新，則 Configuration Manager 會在達到期限時確認已安裝更新。 如果在裝置上偵測不到更新，則會安裝更新。 
>- 在下載更新之前執行的 Office 應用程式上，不會顯示應用程式內通知列。 下載更新之後，只會顯示新開啟之應用程式的應用程式內通知。
>- 針對服務視窗所觸發的 Office 更新或排定在非上班時間執行的 Office 更新，可能會強制關閉執行中的 Office 應用程式來安裝更新，而不進行通知。 
>- 如需詳細資訊，請參閱 [Office 365 的終端使用者更新通知](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a> 新增 Office 365 更新下載的語言
您可以為 Configuration Manager 新增支援，以下載 Office 365 所支援任一語言的更新。

### <a name="download-updates-for-additional-languages-in-version-1902"></a>下載版本 1902 中其他語言的更新
<!--3555955-->

從 Configuration Manager 版本 1902 開始，更新工作流程會從 **Office 365 用戶端更新**的諸多其他語言分成 **Windows Update** 的 38 種語言。

若要選取必要語言，請使用下列位置的 [語言選擇]：
- 建立自動部署規則精靈
- 部署軟體更新精靈
- 下載軟體更新精靈
- 自動部署規則內容

在 [語言選擇] 頁面中，選取 [Office 365 用戶端更新]，然後按一下 [編輯]。 為 Office 365 新增所需的語言，然後按一下 [確定]。

![為 Office 365 新增其他語言的螢幕擷取畫面](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>新增支援以下載版本 1810 和更早版本中其他語言的更新

請在管理中心網站或獨立主要站台中的軟體更新點，使用下列程序。

> [!IMPORTANT]  
> 設定其他 Office 365 更新語言是全站台設定。 使用下列程序新增語言之後，將會下載這些語言的所有 Office 365 更新，以及您在 [下載軟體更新] 或 [部署軟體更新精靈] 中 [語言選擇] 頁面內所選取的語言。

1. 從命令提示字元處，以系統管理使用者身分輸入 *wbemtest*，開啟 Windows Management Instrumentation 測試器。
2. 按一下 [連線]，然後輸入 *root\sms\site_<&lt;siteCode&gt;* 。
3. 按一下 [查詢]，然後執行下列查詢︰*select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI 查詢](../media/1-wmiquery.png)
4. 在 [結果] 窗格中，於具有管理中心網站或獨立主要站台的站台碼之物件上按兩下。
5. 選取 [內容] 屬性，按一下 [編輯內容]，然後按一下 [檢視內嵌項]。
   ![內容編輯器](../media/2-propeditor.png)
6. 從第一個查詢結果開始，開啟每個物件，直到找到 **PropertyName**屬性為 **AdditionalUpdateLanguagesForO365** 為止。
7. 選取 [Value2]，然後按一下 [編輯內容]。  
   ![編輯 Value2 內容](../media/3-queryresult.png)
8. 新增其他語言至 [Value2] 內容，然後按一下 [儲存內容]。 <br/> 例如，-pt-pt (葡萄牙文 - 葡萄牙)、af-za (南非荷蘭文 - 南非)、nn-no (挪威文 (耐諾斯克) - 挪威) 等等。您可鍵入 `pt-pt,af-za,nn-no` 作為範例語言。 請勿在語言之間使用空格。
 
   ![在內容編輯器中新增語言](../media/4-props.png)  
9. 依序按一下 [關閉]、[關閉]、[儲存內容]，然後按一下 [儲存物件] (如果您在此處按一下 [關閉]，將會捨棄值)。 按一下 [關閉]，然後按一下 [結束] 以結束 Windows Management Instrumentation 測試器。
10. 在 Configuration Manager 主控台中，前往 [軟體程式庫] > [概觀] > [Office 365 用戶端管理] > [Office 365 更新]。
11. 現在，下載 Office 365 更新時，將會下載您在精靈中選取及在此程序中所設定語言的更新。 為確認下載了正確語言的更新，請前往更新的套件來源，並尋找檔案名稱中有該語言代碼的檔案。  
    ![其他語言的檔名](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>使用工作順序更新 Office 365 ProPlus
使用[安裝軟體更新](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)工作順序步驟安裝 Office 365 更新時，可能會將已部署的更新偵測為不適用。  如果排定的 [Office 自動更新] 工作沒有至少執行一次，可能發生這個情況 (請參閱[部署 Office 365 更新](manage-office-365-proplus-updates.md#deploy-office-365-updates)中的附註)。 例如，如果在執行此步驟之前立即安裝 Office 365 ProPlus，可能會發生這個情況。

若要確保更新管道已妥善設定，以便正確地偵測到已部署的更新，請使用下列其中一種方法：

**方法 1：**
1. 在具有相同 Office 365 ProPlus 版本的電腦上，開啟 [工作排程器] (taskschd.msc)，並識別 Office 365 自動更新工作。 通常，它位於 [工作排程器程式庫] >[Microsoft]>[Office]下。
2. 以滑鼠右鍵按一下自動更新工作，然後選取 [屬性]。
3. 移至 [動作] 索引標籤，並按一下 [編輯]。 複製命令與任何引數。 
4. 在 Configuration Manager 主控台中，編輯您的工作順序。
5. 使用工作順序，將新的 [執行命令列] 步驟加入至 [安裝軟體更新] 步驟之前。 如果在相同的工作順序中安裝 Office 365 ProPlus，請確定此步驟會在安裝 Office 之後執行。
6. 在您從 Office 自動更新排程工作收集的命令和引數中複製。 
7. 按一下 [確定]。 

**方法 2：**
1. 在具有相同 Office 365 ProPlus 版本的電腦上，開啟 [工作排程器] (taskschd.msc)，並識別 Office 365 自動更新工作。 通常，它位於 [工作排程器程式庫] >[Microsoft]>[Office]下。
2. 在 Configuration Manager 主控台中，編輯您的工作順序。
3. 使用工作順序，將新的 [執行命令列] 步驟加入至 [安裝軟體更新] 步驟之前。 如果在相同的工作順序中安裝 Office 365 ProPlus，請確定此步驟會在安裝 Office 之後執行。
4. 在命令列欄位中，輸入將會執行排定工作的命令列。 請參閱下方的範例，確定引號中的字串與步驟 1 中識別之工作的路徑與名稱相符。  

    範例：`schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. 按一下 [確定]。 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a> Microsoft 365 Apps 的更新通道
<!--6298093-->
在 Office 365 ProPlus 重新命名為 **Microsoft 365 Apps for enterprise** 後，更新通道亦經重新命名。 如果使用自動部署規則 (ADR) 來部署更新，則當 ADR 依賴**標題**屬性時，您就必須對其進行變更。 這是因為 Microsoft Update 目錄中的更新套件名稱正在持續變更中。

在目前，Office 365 ProPlus 更新套件的標題會以 "Office 365 Client Update" 開頭，如下列範例所示：

&nbsp; &nbsp; Office 365 Client Update - x64 型版本的半年通道 1908 版 (組建 11929.20648)

對於在 6 月 9 日及之後發行的更新套件，其標題則會以 "Microsoft 365 Apps Update" 開頭，如下列範例所示：

&nbsp; &nbsp; Microsoft 365 Apps Update - x64 型版本的半年通道 1908 版 (組建11929.50000)
</br>
</br>

|新的通道名稱|舊的通道名稱|
|--|--|
|半年企業通道|半年通道|
|半年企業通道 (預覽)|半年通道 (已設定目標)|
|每月企業通道|NA|
|目前通道|每月通道|
|目前通道 (預覽)|每月通道 (已設定目標)|
|搶鮮版 (Beta) 通道|測試人員|

如需如何修改 ADR 的詳細資訊，請參閱[自動部署軟體更新](automatically-deploy-software-updates.md)。 如需名稱變更的詳細資訊，請參閱 [Office 365 ProPlus 的名稱變更](https://docs.microsoft.com/deployoffice/name-change) (機器翻譯)。


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>啟用 Office 365 用戶端之後變更更新頻道，可接收來自 Configuration Manager 的更新

部署 Office 365 專業增強版後，即可使用群組原則或 Office 部署工具 (ODT) 來變更更新通道。 例如，可將裝置從半年通道移至半年通道 (已設定目標)。 Office 會在變更頻道時自動更新，不需要重新安裝或下載完整版本。 如需詳細資訊，請參閱[變更組織中裝置的 Office 365 專業增強版更新通道](https://docs.microsoft.com//deployoffice/change-update-channels)。


## <a name="next-steps"></a>後續步驟

使用 Configuration Manager 中的 Office 365 用戶端管理儀表板，檢閱 Office 365 用戶端資訊並部署 Office 365 應用程式。 如需詳細資訊，請參閱 [Office 365 用戶端管理儀表板](office-365-dashboard.md)。
