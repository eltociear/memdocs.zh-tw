---
title: 尋找說明
titleSuffix: Configuration Manager
description: 尋找資源以取得 Configuration Manager 的其他資訊。
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bae98a8df1d8b8ff843bd333083c4c6ad68848c
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343179"
---
# <a name="find-help-for-using-configuration-manager"></a>尋找使用 Configuration Manager 的說明

適用於：Configuration Manager (最新分支)

本文提供下列各節，其中包含多個資源可尋找使用 Configuration Manager 的說明：  

- [產品文件](#bkmk_Info)  

- [分享產品意見反應](#product-feedback)  

- [關注 Configuration Manager 小組部落格](#BKMK_ProductGroupBlog)  

- [支援選項和社群資源](#BKMK_SupportOptions)  

如需產品協助工具功能的說明，請參閱[協助工具功能](accessibility-features.md)。  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a> 產品文件  

若要存取最新的產品文件，請從[程式庫索引](https://docs.microsoft.com/sccm/)開始。  

<a name="BKMK_SearchTips"></a>  

如需搜尋、提供意見反應的祕訣，以及使用產品文件的詳細資訊，請參閱[如何使用文件](use-docs.md)。  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a> 產品意見反應 (從 1806 版開始)

從 Configuration Manager 1806 版開始，您可以直接從主控台傳送產品意見反應。 如果您需要附加記錄，請使用[意見反應中樞](#BKMK_FeedbackHub)。 您可以執行下列作業： <!--1357542-->

- **傳送笑臉**：針對您喜歡的功能傳送意見反應。
- **傳送苦臉**：針對您不喜歡的功能傳送意見反應。
- **傳送建議**：將您帶往 [UserVoice 網站](https://configurationmanager.uservoice.com/)，以分享您的想法。

  ![在 Configuration Manager 1806 中提交意見反應](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>傳送笑臉或傳送苦臉

請遵循下列指示，傳送您喜歡之功能的意見反應：

1. 在主控台的右上角，按一下笑臉。
2. 在下拉式功能表中，選取 [傳送笑臉] 或 [傳送苦臉]。
3. 使用文字方塊來說明您喜歡或不喜歡的功能。 
4. 選擇您是否想要分享電子郵件地址和螢幕擷取畫面。
5. 按一下 [提交意見反應]
     - 如果您沒有網際網路連線，請按一下底部的 [儲存]。 請遵循[傳送您儲存以供稍後提交的意見反應](#BKMK_NoInternet)一節中的指示，將它傳送至 Microsoft。 

![在 Configuration Manager 1806 中提交回函表單](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>傳送笑臉的狀態訊息
<!--5891852-->
自 Configuration Manager 2002 起，當您**傳送笑臉**或**傳送苦臉**時，會在提交意見反應時建立狀態訊息。 這項改善會提供下列記錄：
- 提交意見反應的時間
- 提交意見反應的人員
- 意見反應識別碼
- 是否成功提交意見反應
   - 提交成功的訊息識別碼為 53900。
   - 提交失敗的訊息識別碼為 53901。

若要檢視狀態訊息，請選取 [監視] > [系統狀態] > [狀態訊息查詢]。 請先從 [所有狀態訊息] 查詢開始，然後選取您的時間範圍。 當訊息載入時，按一下 [篩選訊息] 按鈕，然後篩選出訊息識別碼 53900 或 53901。

如果您[傳送儲存的意見反應以供稍後提交](find-help.md#BKMK_NoInternet)，則不會建立狀態訊息。

[![成功提交意見反應的狀態訊息](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>傳送建議

當您**傳送建議**時，您會被導向至協力廠商網站 [UserVoice](https://configurationmanager.uservoice.com/)，以分享您的想法。 Configuration Manager 產品小組使用下列 UserVoice 狀態值：

- **Noted** (已記錄) - 我們了解要求且要求很合理。 我們已將要求新增至待辦項目。
- **Planned** (已規劃) - 我們已針對這項功能開始撰寫程式碼，並預期未來幾個月會出現在技術預覽組建中。
- **Started** (已開始) - 這項功能現在處於技術預覽階段。 歡迎試用並提供意見反應。 讓我們知道這項功能是否朝正確方向進行。 將其他意見反應放入原始要求的評論區段中，讓其他人可以查看並進行評論。 我們將閱讀該則評論，並嘗試據以改進此功能。
- **Completed** (已完成) - 這項功能的第一個版本已進入生產組建。 此狀態不表示這項功能已經全部完工，日後不再加以改進。 而是表示已正式推出這項功能的第一個版本，且您可以開始實際使用它。 我們將狀態設為已完成，因為：
  - 我們希望您知道這項功能已準備好用於生產環境。
  - 我們想要回報您的 UserVoice 投票，讓您可以在其他項目上使用這些功能。
  - 您可以針對這項功能提出新的設計變更要求，協助我們了解這項功能的下一個最重要改善。

### <a name="information-sent-with-feedback"></a>連同意見反應一起傳送的資訊

當您**傳送笑臉**或**傳送苦臉**時，會連同意見反應一起傳送下列資訊：

- OS 組建資訊
- Configuration Manager 階層識別碼
- 產品組建資訊
- 語言資訊
- 裝置識別碼 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a> 您儲存以供稍後提交的意見反應

1. 在 [提供意見反應] 視窗底部，按一下 [儲存] 。 
2. 儲存 .zip 檔案。 如果本機電腦沒有網際網路存取，請將檔案複製到連線到網際網路的電腦。 
3. 如有需要，請複製位於 `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\` 的 [UploadOfflineFeedback] 資料夾
    - 如需 cd.latest 資料夾的詳細資訊，請參閱 [CD.Latest 資料夾](../servers/manage/the-cd.latest-folder.md)

4. 在連線到網際網路的電腦上，開啟命令提示字元。 
5. 執行下列命令：`UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - 您可以選擇性指定下列參數：
        -  `-t, --timeout`：傳送資料時逾時 (秒)。 0 為無限制。 預設為 30。
        - `-s --silent`：未記錄到主控台 (無法結合 --verbose)
        - `-v, --verbose`：將詳細資訊記錄輸出到主控台 (無法結合 --silent)
        - `--help`：顯示 [說明] 畫面
    
    - 從 1910 版開始，UploadOfflineFeedback 公用程式支援使用 Proxy 伺服器。 您可以指定下列參數：
        - `-x, --proxy`：指定要連線網際網路的 Proxy 伺服器。
        - `-o, --port`：針對要連線網際網路的 Proxy 伺服器指定連接埠。
        - `-u, --user`：針對要連線網際網路的 Proxy 伺服器指定使用者名稱。
        - `-w, --password`：針對要連線網際網路的 Proxy 伺服器指定密碼。 輸入星號 (&#42;) 以產生密碼的提示。 當您在密碼提示字元中輸入密碼時，不會顯示該密碼。 強烈建議您使用星號 (&#42;) 來產生密碼輸入的提示，因為命令列上的純文字較不安全。
        - `-i`：略過連線檢查：略過網路連線檢查，只上傳具有指定設定的意見反應。

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a> 確認主控台的意見反應

<!--3556010-->
從 1902 版開始，當您透過 Configuration Manager 主控台或 UploadOfflineFeedback.exe 傳送意見反應時，它會顯示確認訊息。 此訊息包含**意見反應識別碼**，您可以將其提供給 Microsoft 作為追蹤識別碼。

- 若要複製**意見反應識別碼**，請選取識別碼旁邊的複製圖示，或使用 **CTRL** + **C** 快速鍵。
  - 此識別碼不會儲存在您的電腦上，因此請務必先予以複製，再關閉視窗。
- 按一下 [不要再顯示此訊息] 會隱藏此對話方塊，使其不會在未來顯示。

   ![在 Configuration Manager 1902 中透過主控台確認意見反應](media/1902-feedback-id-example.png)
- 除非使用 -s 或 --silent，否則 **UploadOfflineFeedback** 命令工具會將 **FeedbackID** 寫入主控台。

  ![在 Configuration Manager 1902 中透過 UploadOfflineFeedback.exe 確認意見反應](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a> 產品意見反應 (適用於 1802 版和更新版本)

透過 Windows 10 內建的[意見反應中樞應用程式](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)，來回報潛在的產品瑕疵。 當您 [新增意見反應] 時，請務必選取 [企業管理] 類別，然後選擇下列其中一個子類別：
- Configuration Manager 用戶端
- Configuration Manager 主控台
- Configuration Manager 作業系統部署
- Configuration Manager 伺服器

繼續使用 [UserVoice 頁面](https://configurationmanager.uservoice.com/)，對 Configuration Manager 的新功能構想進行投票。 Configuration Manager 產品小組使用下列 UserVoice 狀態值：

- **Noted** (已記錄) - 我們了解要求且要求很合理。 我們已將要求新增至待辦項目。
- **Planned** (已規劃) - 我們已針對這項功能開始撰寫程式碼，並預期未來幾個月會出現在技術預覽組建中。
- **Started** (已開始) - 這項功能現在處於技術預覽階段。 歡迎試用並提供意見反應。 讓我們知道這項功能是否朝正確方向進行。 將其他意見反應放入原始要求的評論區段中，讓其他人可以查看並進行評論。 我們將閱讀該則評論，並嘗試據以改進此功能。
- **Completed** (已完成) - 這項功能的第一個版本已進入生產組建。 此狀態不表示這項功能已經全部完工，日後不再加以改進。 而是表示已正式推出這項功能的第一個版本，且您可以開始實際使用它。 我們將狀態設為已完成，因為：
  - 我們希望您知道這項功能已準備好用於生產環境。
  - 我們想要回報您的 UserVoice 投票，讓您可以在其他項目上使用這些功能。
  - 您可以針對這項功能提出新的設計變更要求，協助我們了解這項功能的下一個最重要改善。

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a> Configuration Manager 小組部落格  

Configuration Manager 工程及夥伴小組使用 [Enterprise Mobility + Security 部落格](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager)為您提供技術資訊和其他關於 Configuration Manager 的新聞及相關技術。 我們的部落格會張貼產品文件和支援資訊等補充資訊。  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a> 支援選項和社群資源  

下列連結提供與支援選項和社群資源相關的資訊：  

-   [Microsoft 支援服務](https://aka.ms/cmcbsupport)  

-   [Configuration Manager 社群：Configuration Manager (Current Branch) Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx ) (Configuration Manager (最新分支) 求生指南)  

-   [Configuration Manager 論壇網頁](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
