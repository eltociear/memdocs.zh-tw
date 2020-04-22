---
title: CMTrace
titleSuffix: Configuration Manager
description: 深入了解如何使用 CMTrace 工具檢視 Configuration Manager 的記錄檔。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707896"
---
# <a name="cmtrace"></a>CMTrace

適用於：  Configuration Manager (最新分支)

CMTrace 是 [Configuration Manager 工具](tools.md)的其中之一。 它可讓您檢視和監視記錄檔，包括下列類型：  

- 使用 Configuration Manager 或用戶端元件管理員 (CCM) 格式的記錄檔  

- 純 ASCII 或 Unicode 文字檔，例如 Windows Installer 記錄檔  

此工具藉由醒目提示、篩選和錯誤查詢協助分析記錄檔。

自 1806 版開始，CMTrace 檢視工具會自動與 Configuration Manager 用戶端一起安裝。 它會被新增至用戶端安裝目錄，根據預設，就是 `%WinDir%\CCM\CMTrace.exe`。<!--1357971-->

> [!Note]  
> CMTrace 不會自動註冊到 Windows 中以開啟副檔名為 .log 的檔案。 如需詳細資訊，請參閱[檔案關聯](#file-associations)。  

從 1906 版開始，**OneTrace** 是支援中心的新記錄檢視器。 其運作方式與 CMTrace 類似，但包含改良功能。 如需詳細資訊，請參閱[支援中心 OneTrace](support-center-onetrace.md)。

## <a name="usage"></a>使用方式

執行 **CMTrace.exe**。 您第一次執行此工具時，會看到檔案關聯的提示。 如需詳細資訊，請參閱[檔案關聯](#file-associations)。

您採用的大部分 CMTrace 動作是來自下列功能表：

- [File](#file-menu)
- [工具](#tools-menu)

### <a name="file-menu"></a>[檔案] 功能表

[檔案]  功能表提供下列動作：  

- [開啟](#open)
- [在伺服器中開啓](#open-on-server)
- [列印](#print)
- [喜好設定](#preferences)

[檔案] 功能表也會列出八個最近使用過的檔案。 從 [檔案] 功能表中選取其中一個記錄檔，可快速重新開啟它。

#### <a name="open"></a>開啟

顯示 [開啟] 對話方塊以瀏覽記錄檔。

篩選檢視下列類型的檔案：

- 記錄檔 (\*.log)  
- 舊的記錄檔 (\*.lo_)
- 所有檔案 (\*.\*)

預設不選取下列兩個選項：  

- **略過現有行**：選取後，CMTrace 會忽略所選取記錄檔的現有內容，只顯示新增的新行。 當您不需要完整的記錄檔記錄時，使用此選項可只監視新的動作。  

- **合併選取的檔案**：如果啟用此選項並選取一個以上的記錄檔，CMTrace 會在檢視中合併選取的記錄檔。 顯示內容看起來像是一個記錄檔。 合併的記錄檔更新也一樣，並且支援所有其他 CMTrace 功能，就像它是一個記錄檔。  

#### <a name="open-on-server"></a>在伺服器中開啓

在站台系統電腦上使用標準的 [瀏覽] 對話方塊，瀏覽 Configuration Manager 記錄檔資料夾。 您也可以瀏覽遠端電腦的網路。

當您選取要瀏覽的遠端電腦時，CMTrace 會檢查是否有 Configuration Manager 共用。 如果它在 Configuration Manager 記錄檔中找不到共用，就會顯示錯誤訊息。  

若不要瀏覽而是直接連線到已知電腦，請使用[開啓](#open)動作。 然後以 UNC 格式輸入伺服器名稱及共用。

#### <a name="print"></a>列印

顯示標準的 Windows [列印] 對話方塊。 此動作會將目前的記錄檔傳送至印表機。 其會根據 CMTrace [喜好設定] 中 [列印] 索引標籤上的設定來格式化輸出。

#### <a name="preferences"></a>喜好設定

設定 CMTrace 設定。 有下列選項可供使用：  

- [一般]  索引標籤  

    - **更新間隔**：控制 CMTrace 檢查記錄檔變更並載入新行的頻率。 根據預設，此值為 500 毫秒。  

    - **醒目提示**：設定 CMTrace 醒目提示所選擇記錄行時所用的色彩。 根據預設，此色彩是基本的黃色 (紅色：255、綠色：255、藍色：0)。  

    - **資料行**：設定記錄檢視中可見的資料行，以及其顯示順序。 根據預設，它會顯示 [記錄檔文字]、[元件]、[日期/時間] 和 [執行緒]。  

- [列印]  索引標籤  

    - **資料行**：設定列印記錄檔時所用的資料行，以及其顯示順序。 根據預設，列印和顯示的資料行相同。  

    - **方向**：設定列印記錄檔時的預設列印方向。 在 [列印] 對話方塊中覆寫此設定。 根據預設，它會使用直式方向。  

- [進階]  索引標籤  

    - **重新整理間隔**：強制 CMTrace 在載入大量記錄行時，依指定的間隔更新記錄檢視。 根據預設，此選項已停用，其值為零。  

        > [!Note]  
        > 一般情況下，不會修改 [重新整理的間隔]  。 開啟大型記錄檔時會大幅增加所需要的時間。

### <a name="tools-menu"></a>[工具] 功能表

[工具]  功能表提供下列動作：

- [尋找](#find)
- [尋找下一個](#find-next)
- [複製到剪貼簿](#copy-to-clipboard)
- [醒目提示](#highlight)
- [篩選](#filter)
- [錯誤查詢](#error-lookup)
- [暫停](#pause)
- [顯示/隱藏詳細資料](#showhide-details)
- [顯示/隱藏資訊窗格](#showhide-info-pane)

#### <a name="find"></a>尋找

在開啟的記錄檔中搜尋指定的文字字串。  

#### <a name="find-next"></a>尋找下一個

依您之前在 [尋找] 對話方塊中指定的內容，尋找下一個符合的字串。  

#### <a name="copy-to-clipboard"></a>複製到剪貼簿

將選取的記錄行以純文字複製到 Windows 剪貼簿。 如果您正在檢查 Configuration Manager 和 CCM 記錄檔，複製的資料行順序和檢視相同。 每個資料行以定位字元分隔。 將記錄檔複製到電子郵件訊息或其他文件時，請使用此動作。  

#### <a name="highlight"></a>醒目提示

輸入 CMTrace 搜尋每個記錄項目文字時所用的字串。 然後醒目提示符合輸入字串的任何記錄檔文字。  

- 醒目提示使用您在 [喜好設定] 中指定的色彩。  

- 若要關閉醒目提示，請清除此欄位中的字串。  

- 如果輸入十進位或十六進位的數字，CMTrace 就會嘗試比對 [執行緒] 資料行的值。 使用此行為可以醒目提示單一執行緒的處理，不需要篩選出可能與它互動的其他執行緒。  

- 若要依大小寫比較字串，請啟用 [區分大小寫]  的選項。  

#### <a name="filter"></a>篩選器

根據指定的準則，顯示或隱藏記錄行內容。 將篩選套用至四個資料行的任一個，無論它們是否顯示。 這些設定會套用到每個已開啟的記錄檔。

範例：
<!--SCCMDocs issue #603-->

- 篩選出 **smsts.log** 中包含 "the action" 或 "the group" 的項目文字。
- 篩選出 **InventoryAgent.log** 中包含 "destination" 的項目文字。

#### <a name="error-lookup"></a>錯誤查詢

鍵入或貼上十進位或十六進位格式的錯誤碼，以顯示描述。 可能的錯誤來源包括：Windows、WMI 或 Winhttp。

#### <a name="pause"></a>暫停

暫停或重新啟動記錄檔監視。 下列使用案例是使用這項動作的一些可能原因：  

- 當 CMTrace 顯示記錄檔資訊過快時  

- 當您暫停記錄監視時，如果目前的檔案彙總到新的記錄檔，CMTrace 不會遺失顯示的資訊  

- 當您想要在檢查記錄檔的同時，阻止 CMTrace 顯示新資料時  

#### <a name="showhide-details"></a>顯示/隱藏詳細資料

顯示或隱藏記錄檔文字以外的所有資料行。 同時將記錄檔文字資料行展開至視窗的寬度。 當您在低解析度的電腦上檢視記錄檔時，請使用此動作。 它會顯示更多的記錄檔文字。  

> [!Note]  
> 檢視純文字檔時，CMTrace 會自動隱藏詳細資料，因為它們一律空白。  

#### <a name="showhide-info-pane"></a>顯示/隱藏資訊窗格

顯示或隱藏 [資訊] 窗格。 當您在低解析度的電腦上檢視記錄檔時，請使用此動作。 它會顯示更多的記錄詳細資料。  


## <a name="log-pane"></a>[記錄檔] 窗格

[記錄檔] 窗格位在 CMTrace 視窗的頂端。 它會顯示記錄檔的內容。

當您選取一行記錄時，它會暫時使用 Windows 選取範圍色彩配置醒目提示。

醒目提示的記錄符合您在 [工具]  功能表之 [醒目提示]  選項中定義的準則。 醒目提示使用您在 [喜好設定]  中指定的色彩。

CMTrace 使用紅底黃字顯示有錯誤的記錄行。 在使用 CCM 格式的記錄檔中，記錄項目有明確的類型值，能指出項目為錯誤。 至於其他記錄檔格式，CMTrace 會在每個項目中執行區分大小寫的搜尋，找出所有符合 "error" 的文字字串。

它會使用黃色背景顯示有警告的記錄行。 在使用 CCM 格式的記錄檔中，記錄項目有明確的類型值，能指出項目為警告。 至於其他記錄檔格式，CMTrace 會在每個項目中執行區分大小寫的搜尋，找出所有符合 "warn" 的文字字串。


## <a name="info-pane"></a>[資訊] 窗格

[資訊] 窗格位在 CMTrace 視窗的底端。 其中包含下列功能：

- 目前選取的記錄檔項目詳細資料  

- 顯示記錄檔文字的文字方塊  

- 它會顯示換行字元，方便您輕鬆閱讀格式化的文字  

- 更容易閱讀 [記錄檔] 窗格中未完整顯示的長項目  

使用 [工具]  功能表的 [顯示/隱藏資訊窗格]  選項來顯示或隱藏 [資訊] 窗格。 如果 [資訊] 窗格佔用了一半以上的記錄視窗，CMTrace 就會自動隱藏它。

### <a name="progress-bar"></a>進度列

當您第一次開啟記錄檔時，CMTrace 會以進度列取代 [資訊] 窗格。 這個進度會指出已載入多少現有的檔案內容。 當進度百分比達到 100% 時，CMTrace 就會移除進度列，並將其取代為 [資訊] 窗格。 當您載入大型檔案時，此行為會向您提供負載可能需要的時間。

### <a name="status-bar"></a>狀態列

對於使用 Configuration Manager 格式和 CCM 格式的記錄檔，狀態列會顯示所選記錄項目的經過時間。 如果您選取單一項目，此工具會顯示從第一個記錄項目到所選項目的時間。 如果您選取多個項目，它會計算從最上層選取項目到最下層選取項目的時間。 CMTrace 會格式化此資訊，如下所示：

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Windows Shell 整合

CMTrace 支援[檔案關聯](#file-associations)和[拖放](#drag-and-drop)。

### <a name="file-associations"></a>檔案關聯

CMTrace 可以建立其本身與 .log 和 .lo_ 副檔名的關聯。 當程式啟動時，它會檢查登錄，以判斷它是否已與這些副檔名建立關聯。 如果 CMTrace 尚未與任何副檔名建立關聯，系統會提示您建立副檔名與 CMTrace 的關聯。 如果您選取 [不要再詢問此問題]  ，CMTrace 每次在這部電腦上執行時，都會略過這項檢查。

### <a name="drag-and-drop"></a>拖放

CMTrace 支援基本的拖放功能。 將檔案從 Windows 檔案總管拖放到 CMTrace 以開啟。


## <a name="other-tips"></a>其他祕訣

### <a name="last-directory-registry-key"></a>Last Directory 登錄機碼

<!--511280-->
根據預設，CMTrace 會儲存您所開啟的最後一個記錄檔位置。 此行為在站台伺服器上很有用，因為它每次都會預設為記錄檔路徑。

您第一次在用戶端啟動它時，它就預設為目前的工作目錄。 這個位置可能是您儲存 CMTrace 的路徑，或是類似`%userprofile%\Desktop` 的路徑。

登錄機碼 `HKEY_CURRENT_USER\Software\Microsoft\Trace32` 中的 **Last Directory** 值控制此預設位置。 如果您在用戶端將此值設定為 `%windir%\CCM\Logs`，則 CMTrace 就會在您第一次執行它時開啟用戶端記錄檔位置的檔案。


## <a name="see-also"></a>請參閱

- [記錄檔](../plan-design/hierarchy/log-files.md)

- [支援中心記錄檔檢視器](support-center.md#support-center-log-file-viewer)

- [支援中心 OneTrace](support-center-onetrace.md)
