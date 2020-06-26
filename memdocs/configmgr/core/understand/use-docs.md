---
title: 如何使用 Docs
titleSuffix: Configuration Manager
description: 了解使用 Configuration Manager 技術文件庫的祕訣。
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31f9b1cb083400abd36858a177e87804a916362c
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746506"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>如何使用 Configuration Manager Docs

適用於：Configuration Manager (最新分支)

此文章提供使用 Configuration Manager 文件庫的資源和祕訣。

- 如何搜尋
- 提交文件的錯誤 (Bug)、增強功能、問題與新構想
- 如何取得變更的通知
- 如何參與 Docs

如需產品的一般說明，請參閱[尋找說明](find-help.md)。

## <a name="search"></a><a name="bkmk_searchtips"></a> 搜尋

使用下列搜尋秘訣有助於尋找所需的資訊：

- 當您使用慣用的搜尋引擎尋找 Configuration Manager 的內容時，請在搜尋關鍵字中包括 `ConfigMgr`。

  - 尋找來自 `docs.microsoft.com/mem/configmgr` 的 Configuration Manager 最新分支結果。 來自 `docs.microsoft.com/previous-versions` 的結果適用於較舊的產品版本。

  - 若要進一步將焦點放在目前內容庫的搜尋結果，可在搜尋時包括 `site:docs.microsoft.com` 以限定搜尋引擎的範圍。

- 使用符合使用者介面和線上文件中術語的搜尋字詞。 請避免您可能會在社群內容中看到的非官方字詞或縮寫。 例如，搜尋：

  - 「管理點」而非 "MP"
  - 「部署類型」而非 "DT"
  - 「軟體更新」而非 "SUM"

- 若要在目前文章中搜尋，請使用瀏覽器的**尋找**功能。 使用大多數的新式網頁瀏覽器時，您可以按 **Ctrl**+**F**，然後輸入搜尋文字。

- `docs.microsoft.com` 上的每篇文章都包含下列欄位，可協助搜尋內容：

  - 右上角的 [搜尋]。 若要搜尋所有文章，請在此欄位中輸入字詞。 Configuration Manager 文件庫中的文章會自動包含 `ConfigMgr` 範圍，以便只搜尋此文件庫。

  - 左目錄上方的 [依標題篩選]。 若要搜尋目前的目錄，請在此欄位中輸入字詞。 此欄位只會比對目前節點的文章標題中所顯示的字詞。 例如，**核心基礎結構** (`docs.microsoft.com/configmgr/core`) 或**應用程式管理** (`docs.microsoft.com/configmgr/apps`)。

- 尋找時發生問題嗎？ [歡迎提出意見反應！](#bkmk_docfeedback) 當您提出問題時，請提供所使用的搜尋引擎、嘗試的關鍵字和目標文件。 您的意見反應可協助 Microsoft 最佳化內容，以確保更有效率的搜尋。

> [!TIP]
> 從 Configuration Manager 1902 版開始，Configuration Manager 主控台的新 [社群] 工作區中會有一個 [文件] 節點。 此節點包含 Configuration Manager 文件和支援文章的最新資訊。 如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../servers/manage/admin-console.md#bkmk_doc-dashboard)。

## <a name="feedback"></a><a name="bkmk_docfeedback"></a> 意見反應

選取任一篇文章右上角的 [意見反應] 連結，以移至底部的 [意見反應] 區段。 此區段會與 GitHub 問題整合。 如需整合 GitHub 問題的詳細資訊，請參閱 [Docs 平台部落格文章](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs)。

若要分享有關 Configuration Manager 產品本身的意見反應，選取 [產品意見反應]。 如需詳細資訊，請參閱[產品意見反應](find-help.md#product-feedback)。

若要提供文件的意見反應，您必須具備 [GitHub 帳戶](https://github.com/join)。 一旦您登入之後，即會有 Microsoft Docs 組織的一次性授權。 接著，當您選取 [內容意見反應] 時，輸入標題和留言，然後選取 [提交意見反應]。 這個動作會在 [SCCMdocs 存放庫](https://github.com/MicrosoftDocs/SCCMdocs/issues)中的目標文件提出一個新問題。

這項整合也會顯示目標文件任何現有的未結案或已結案問題。 如果有的話，請先檢閱這些內容後，再提交新的問題。 如果您找到相關的問題，選取笑臉圖示以新增回應，或展開問題即可新增留言。

#### <a name="types-of-feedback"></a>意見反應的類型

您可以使用 GitHub 問題，提交下列類型的意見反應：

- 文件 Bug：內容過時、不清楚、使人混淆或損毀。
- 文件的增強：改善文章的建議。
- 文件問題：您需要協助尋找現有文件。
- 文件構想：針對新文章的建議。 若要對文件提出意見反應，請使用這個方法，而不是 UserVoice。
- 讚美：針對實用或資訊性文章給予正面的意見反應！
- 當地語系化：針對內容翻譯的意見反應。
- 搜尋引擎最佳化 (SEO)：搜尋內容問題的相關意見反應。 請在意見中提及搜尋引擎、關鍵字和目標文章。

如果您針對非文件相關的主題建立問題，Microsoft 將會關閉這類問題。 例如：

- [產品意見反應](find-help.md#product-feedback)
- [產品問題](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [支援要求](https://aka.ms/cmcbsupport)

若要分享有關基本 docs.microsoft.com 平台的意見反應，請參閱 [Docs 意見反應](https://aka.ms/sitefeedback) \(英文\)。 平台包括所有包裝函式元件，例如標頭、目錄和右側功能表列， 以及文章在瀏覽器中的呈現方式，例如字型、警示和頁面錨定。

## <a name="notifications"></a><a name="bkmk_notifications"></a> 通知

若要在文件庫的內容變更時接收通知，請使用下列步驟：

1. 使用 [Docs 搜尋](https://docs.microsoft.com/search/index?scope=ConfigMgr)，尋找某篇文章或一組文章。 例如：

    - 依標題搜尋單一文章：[「可用來進行疑難排解的記錄檔 - Configuration Manager」](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - 搜尋任何有關 [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr) 的文章

2. 選取右上角的 [RSS] 連結。

3. 在任何 RSS 應用程式中使用此摘要，以在任何搜尋結果有變更時收到通知。

> [!TIP]
> 您也可以選擇 [Watch] \(追蹤\) GitHub 上的 [SCCMdocs 存放庫](https://github.com/MicrosoftDocs/SCCMdocs)。 此方法會產生許多通知。 其中也不包含來自 Microsoft 所使用的私人存放庫變更。

## <a name="contribute"></a><a name="bkmk_contribute"></a> 參與

Configuration Manager 文件庫和大部分的 docs.microsoft.com 內容一樣，都是在 GitHub 上提供的開放來源版本。 本文件庫接受並鼓勵社群參與。 如需如何開始的詳細資訊，請參閱[參與者指南](https://docs.microsoft.com/contribute)。 唯一的先決條件是建立 [GitHub 帳戶](https://github.com/join) \(英文\)。

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>參與 SCCMdocs 的基本步驟

1. 從目標文章中，選取 [編輯]。 這個動作會在 GitHub 中開啟來源檔案。

2. 若要編輯來源檔案，選取鉛筆圖示。

3. 在 Markdown 來源中進行變更。 如需詳細資訊，請參閱[如何使用 Markdown 來撰寫 Docs](https://docs.microsoft.com/contribute/markdown-reference)。

4. 在 [提議檔案變更] 區段中，輸入公開修訂的意見，以說明您要變更的「具體內容」。 然後，選取 [提議檔案變更]。

5. 向下捲動並確認您所做的變更。 選取 [建立提取要求] 以開啟表單。 請說明要進行這項變更的「具體原因」。 標記文章作者，並要求他們檢閱。 選取 [建立提取要求]。

### <a name="what-to-contribute"></a>可參與的項目

如果您想要參與，但不知從何處著手，請參閱下列建議：

- 搜尋問題清單中鎖定社群的標籤：

  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft 作者會將這些標籤指派給適合進行社群參與的各類問題。

- 檢閱文章的精確度。 接著，使用 `mm/dd/yyyy` 格式更新 **ms.date** 中繼資料。 這麼做有助於保持內容的最新狀態。

- 依據您的經驗，新增更正、範例或指引。 這麼做可藉由社群的力量來分享知識。

- 修正非英文語言的翻譯。 這麼做可提升當地語系化內容的可用性。

> [!NOTE]
> 如果您不是 Microsoft 員工，大幅度參與則需簽署貢獻授權合約 (CLA)。 當參與符合閾值時，GitHub 會自動要求您簽署此合約。

### <a name="tips"></a>提示

當您參與 Configuration Manager Docs 時，請遵循這些一般指導方針：

- 請勿透過大量提取要求來讓我們感到驚訝。 相反地，請[提出問題](#bkmk_docfeedback)並開始討論。 然後我們可以在您投入大量時間之前就方向達成共識。

- 閱讀 [Microsoft 樣式指南](https://aka.ms/MicrosoftStyle)。 了解[適用於 Microsoft 樣式和語氣的 10 個重要秘訣](https://docs.microsoft.com/style-guide/top-10-tips-style-voice) \(英文\)。

- 使用[提取要求範本](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md)作為工作的起點。

- 遵循 [GitHub 流程的工作流程](https://guides.github.com/introduction/flow/) \(英文\)。

- 經常在部落格及推文 (或任何其他管道) 提及您的投稿內容！

(這份清單取自 [.NET 參與指南](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts) \(英文\)。)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Microsoft Endpoint Manager 檔的彙總

為了進一步支援 Intune 和 Configuration Manager 的結合案例，其文件庫會合併到 [Microsoft 端點管理員網站](https://docs.microsoft.com/mem)上。 Intune 文件現在位於 [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune)，Configuration Manager 文件現在則位於 [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr)。 如果您還在使用舊的 URL，該 URL 會自動重新導向，因此不需要進行任何變更即可閱讀此內容。

如果您提供意見反應或參與文章，則需要進行一些變更：

- 現有的 GitHub 問題仍會留在原始存放庫 [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) 或 [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues) 中。

  - 這些問題不會在連結文章的＜意見反應＞一節中顯示為開啟或關閉問題。

  - 我們將繼續努力解決這些問題。

  - 在某些情況下，我們可能會做出困難的決策，關閉我們不認為能夠處理的問題。

  - 如果您在現有的存放庫有某個問題，且熱衷於其相關資訊，請對 [MEMDocs 存放庫](https://github.com/MicrosoftDocs/MEMDocs)中的已遷移文章提出意見反應。

- 現在當您提出意見反應或編輯文章時，問題或提取要求會進入 MEMDocs 存放庫。
