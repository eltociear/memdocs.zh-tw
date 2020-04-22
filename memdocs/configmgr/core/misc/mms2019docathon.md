---
title: MMS 2019 Docathon
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8fe2ecfc-f5c1-4fa6-8703-245339400723
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e671118578d059e2b8416e6854a701ce7c405c0f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701206"
---
# <a name="mms-2019-docathon"></a>MMS 2019 Docathon

在 Midwest Management Summit (MMS) 2019 期間，Microsoft Configuration Manager 和 Microsoft Intune 的內容小組正在執行 Docathon。 如果您要參加 5 月 6 日星期一的 [Docs.microsoft.com 實作教室](https://sched.co/N6fd)會議，那麼該時間會藉由 Microsoft 作者的支援來處理參與內容。 Docathon 會負責整個會議的運作，而且任何已經報名的 MMS 2019 出席者都可以參與。

為什麼您應該參與？ Docs.microsoft.com 是用於 Microsoft 產品文件的開放原始碼平台，由 GitHub 提供技術支援。 Microsoft 鼓勵所有人都能夠參與文件！ 當您參與時，平台會在每篇文章上的參與者名單中列出您的姓名。 以下是社群可以提供的一些參與類型：

- 錯字
- 釐清內容
- 範例
- 真實世界的指引和祕訣
- 內容檢閱、時效性

## <a name="set-up"></a>設定

如果您還未設定為參與，請事先進行下列步驟。

### <a name="github-account"></a>GitHub 帳戶

建立一個 [GitHub 帳戶](https://github.com/join)

- 識別設定檔中的任何聯繫  

- 啟用雙因素驗證  

#### <a name="additional-considerations"></a>其他考量

- 檢查貴公司有關開放原始碼參與的原則  

    > [!Note]  
    > 參與程度比較大時，將會要求您接受 Microsoft 開放原始碼的[參與者授權合約 (CLA)](https://cla.opensource.microsoft.com/)。 請事先檢閱本合約。  

- 對 docs.microsoft.com 的參與將會計入 MVP 獎項的考量  

- Microsoft 員工還有一些必要的一次性步驟，以及稍有不同的參與程序  

如需詳細資訊，請參閱 docs.microsoft.com 參與者指南中的 [GitHub 帳戶設定](https://docs.microsoft.com/contribute/get-started-setup-github)。

## <a name="scope"></a>領域

此活動僅涵蓋下列 GitHub 存放庫：

- [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs)
- [SCCMDocs](https://github.com/MicrosoftDocs/SCCMdocs)
- [sccm-docs-powershell-ref](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref)

我們也歡迎並鼓勵您對其他 docs.microsoft.com 內容進行變更，但不會因此歸功於此活動。

## <a name="learn-the-process"></a>了解程序

請閱讀[如何提出問題](../understand/use-docs.md#bkmk_docfeedback)及[如何參與](../understand/use-docs.md#bkmk_contribute)的相關資訊。 大部分的基本變更都可以透過 GitHub 瀏覽器體驗完成。  

> [!Note]  
> 如果您對更複雜的 git 和 VSCode 工作流程有興趣，請參閱[安裝內容撰寫工具](https://docs.microsoft.com/contribute/get-started-setup-tools)。 並/或向 Aaron/Erik 尋求協助。 下列動作是使用更複雜的工作流程的一些原因：
>
> - 建立新的文章
> - 加入影像
> - 字串搜尋和取代，包括規則運算式
> - 更大、更複雜的變更  

## <a name="determine-your-goals"></a>決定您的目標

開始思考與規劃您對此活動的目標。 您要完成什麼？

- 查看範圍內的存放庫中的現有問題。 諸如 **good-first-issue** 或 **help-wanted** 這類標籤都可以識別良好的起點。 如果您想要處理這些問題中的一個問題，請使用 **#MMS2019Docathon** 對其發表留言，並加上 @author 標籤，要求他們將問題指派給您。 換句話說，對該問題[要求權利](https://www.merriam-webster.com/words-at-play/word-origin-dibs)。 根據需要，重複此程序。  
    例如，在 SCCMDocs 中，Aaron 為文章作者：`@aczechowski I'm claiming this issue for #MMS2019Docathon`

- 您知道某篇文章存在問題，但尚未提出任何意見反應。 換句話說，文章底部的 [意見反應]  區段沒有任何內容。 提出新的問題，然後使用上述相同的指示來宣告該問題。  

    - 例如，加入程式碼範例、真實世界範例，或常見的提示。  

    - 除非事先洽詢 Aaron/Erik，否則請避免文法或樣式上的變更。  

    - 您最喜歡的文章其日期超過 90 天，在 2019 年 2 月 6 日之前。 您可以檢閱該文章，然後您編輯的內容會在 **ms.date** 中繼資料屬性。 該參與意味著：「我已經檢閱此文章，仍然是技術上正確，因此重新整理日期。」 提出問題以宣告它。  

    - 請先檢查文章意見反應，以確定是否有其他人已經宣告的未決問題。 這個動作在技術上不是必要的。 如果您不這樣做，而且有其他人先提交了，我們將只會採用第一個參與內容。  

- 星期一的一小時午餐會是專門為實現這些目標而設的時間。 Aaron 與 Erik 可協助處理疑問或問題。

## <a name="contest-summary"></a>內容摘要

比賽將在 5 月 6 日至 9 日這整個星期舉行。 任何已經報名的 MMS 2019 出席者都可以參與。 於 2019 年 5 月 9 日星期四中部時間下午 3:00 前提交參賽作品。 5 月 9 日星期四的 [ConfigMgr 產品小組問答階段](https://sched.co/N6ge)之後，將頒發獎品。 您必須參加 MMS 2019 才有獲獎資格，但不需要參與該會議。 如果您沒有參加會議，請在星期五早上離開之前，向 Aaron 領獎。

> [!Important]  
> 您必須在所有參與內容中加上 **#MMS2019Docathon** 主題標籤才能獲得功勞。

### <a name="award-categories"></a>獎項類別

#### <a name="grand-prize"></a>大獎

- **影響最大**：根據下列準則，由 Aaron 與 Erik 來判斷。 如果您認為您提交的內容應該符合資格，請在您的提取要求中加上註解來說服我們原因。

    - 對社群有益 (50%)
    - 遵循 Microsoft 樣式 (25%)
    - 適當的 Markdown (25%)  

大獎獲獎者將會獲得下列獎品：

- 由 MMS 指導委員會提供的 [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html) 一個註冊通行證，價值 1799 美元！
- 一個正版 Yeti Rambler 30 盎司冰霸杯
- 一個正版 Popsocket 汽車通風口支架 + 把手

#### <a name="first-place-prizes"></a>第一名獎品

下列獎項是以對範圍內存放庫合法參與的次數來計算。 不需要合併也不需要發佈，只要在會議結束前當作提取要求提交即可。 對於玩弄制度者，我們將保留取消資格權利。 每個類別的獲獎者都會獲得一個正版 Yeti Rambler 30 盎司冰霸杯，以及一個正版 Popsocket 汽車通風口支架 + 把手。 每個類別一名獲獎者。

- **提交最多認可者**

- **變更最多行數者**

- **觸及最多篇文章者**

> [!Note]  
> 我們不會將獎品頒發給提出最多問題者。 意見回應對我們很有幫助，但這個活動的重點是參與。

## <a name="resources"></a>資源

- [Microsoft 樣式](https://aka.ms/MicrosoftStyle)

    - [快速入門](https://docs.microsoft.com/contribute/style-quick-start)

    - [適用於 Microsoft 樣式和語氣的 10 個重要秘訣](https://docs.microsoft.com/style-guide/top-10-tips-style-voice) \(英文\)

- [參與者指南](https://docs.microsoft.com/contribute)

- [如何使用 Markdown 來撰寫 Docs](https://docs.microsoft.com/contribute/markdown-reference)

## <a name="official-rules"></a>正式規則

Microsoft Cloud + AI Developer Relations Content & Learning MMS 2019 Docathon 活動比賽正式規則

1. 贊助商

    這些正式規則 (以下簡稱為「規則」) 會控制 Microsoft C+AI DevRel Content MMS 2019 Docathon 活動比賽 (以下簡稱為「比賽」) 的運作。 Microsoft Corporation 是贊助商 (以下簡稱為「贊助商」)。

2. 定義

    在這些規則中，「Microsoft」、「我們」、「我們的」和「我們」指的都是「贊助商」。 「您」和「您自己」指的是比賽參與者。 「活動」指的是在明尼亞波利斯 (MN) 舉辦的 MMS 2019 Docathon 活動。 參賽表示您同意遵守這些規則。

3. 出賽時間

    比賽將於 2019 年 5 月 6 日至 2019 年 5 月 9 日 (以下簡稱為「出賽時間」) 的正規活動時間內舉行。

4. 資格

    開放給美國 50 個州 (包括哥倫比亞特區) 18 歲以上合法居民所有已報名的活動參與者。 Microsoft Corporation 及其子公司的員工和主管、參與執行或管理此促銷活動的人員及其各自家庭成員 (家屬、直系親屬和居住在同一個家庭的個人) 都不符合資格。 禁止地區無效。

    若是商業/商展活動：如果您以員工身分參加此活動，則您有責任遵循雇主的受贈政策。 Microsoft 不會參與任何與此活動相關的任何爭議或行動。 包括教育工作者在內的政府機關雇員：Microsoft 承諾遵循政府機關的受贈和道德規則，因此政府機關和公家機關員工不符合此促銷資格。

5. 如何參賽

    若要建立一個項目，請將編輯提交到下列 GitHub 存放庫中的文章：IntuneDocs、SCCMDocs、sccm-docs-powershell-ref。如需有關提交流程的詳細資訊，請參閱[如何參與](https://docs.microsoft.com/sccm/core/understand/use-docs#bkmk_contribute)。

    若要提交參賽作品，請在 GitHub 上提交一個提取要求。

    您可以提交無限數量的參賽作品。 我們每個人每個類別只會頒發一個獎品。

    對於過多、遺失、延遲、損毀，或不完整的參賽作品，我們概不負責。 如有爭議，參賽作品將會被視為由 GitHub 帳戶的授權帳戶持有人所提交。

6. 符合資格的參賽作品

    為符合資格，參賽作品必須符合下列內容/技術需求：

    - 您的參賽作品必須是您自己的原創作品；而且
    - 您的參賽作品不得已入選為其他任何比賽獲獎作品；而且
    - 您必須已經獲得提交參賽作品所需的任何和所有同意、批准或許可；而且
    - 如果參賽作品需要提交使用者產生的內容 (例如，軟體、相片、影片、音樂、藝術作品、論文等)，參賽者要保證他們的參賽作品為其原創作品，在未經許可或明顯權利的情況下，不得複製其他人的作品，且不侵犯其他任何人或實體的隱私、智慧財產權或其他權利。 您可以包含 Microsoft 商標、標誌和設計，讓 Microsoft 授予您有限授權，以用於提交本次參賽作品的唯一目的；而且
    - 我們得以全權酌情決定您的參賽作品「不可」包含任何淫穢或冒犯、暴力、誹謗、輕蔑或非法內容，或包含促銷酒類、非法毒品、菸草或特定政治議程的內容，或包含傳達可能會對 Microsoft 的善意產生負面影響訊息的內容。

7. 參賽作品的使用

    我們並未宣稱對您提交作品的擁有權。 然而，透過提交參賽作品，表示您授與我們不可撤銷、免版稅的全球權利和授權，以使用、審查、評估、測試和分析您的參賽作品以及其與本次比賽相關所有內容，並在現在已知或以後為任何非商業或商業用途所發明任何媒體中使用您的參賽作品，包括但不限於在未經您進一步許可的情況下，行銷、銷售或促銷 Microsoft 產品或服務。 除了這些正式規則中所述的內容之外，您不會因為使用您的參賽作品而獲得任何補償或點數。

    參賽表示您確認我們可能已經開發或委託與您參賽作品類似或相同的材料，且您放棄因與您參賽作品有任何相似之處而產生的任何索賠。 此外，您了解我們將不會限制有權存取您參賽作品的代表指派工作，且您同意根據此合約或著作權或營業秘密法，我們憑藉代表獨立記憶中的資訊，開發或部署我們的產品或服務對我們不會產生任何責任。

    您的參賽作品可能會被張貼在公開網站上。 對於本網站訪客未經授權使用您的參賽作品，我們概不負責。 即使已入選為獲獎參賽作品，我們還是沒有義務將您的參賽作品用於任何用途。

8. 獲獎者入選和通知

    在確認資格之前，Microsoft 或其代理人或合格的評審小組將根據下列評審標準，從所有符合資格的參賽作品中選出可能獲獎者：

    - 大獎：根據下列標準，影響最大者：
        - 50% - 對社群有益
        - 25% - 遵循 Microsoft 樣式
        - 25% - 適當的 Markdown
    - 以下的第一名獎品是以對範圍內存放庫合法參與的次數來計算。 不需要合併也不需要發佈，只要在會議結束前當作提取要求提交即可。 對於玩弄制度者，我們將保留取消資格權利。
        - 提交最多認可者
        - 變更最多行數者
        - 觸及最多篇文章者

    2019 年 5 月 9 日星期四中部時間下午 3:00 之後將會選取獲獎者。

    獲獎者將會在活動當中收到通知，而且必須在活動結束前領取獎品。

    如果任何符合資格的參賽作品打成平手，額外的評審將會根據上述評審標準打破平局。 評審的決定最具關鍵性，而且具有約束力。 如果我們沒有收到符合參賽要求的足夠數量參賽作品，我們可以自行決定選擇少於以下所述比賽獎品數量的獲獎者。

    獲獎者將會透過參賽期間提供的連絡資訊獲得通知，而且可能需要填寫獎品領取和納稅表 (以下簡稱為「表格」)。 如果無法聯繫到入選的獲獎者、入選的獲獎者資格不符、未能領獎或未能傳回任何表格，則入選的獲獎者將喪失領獎資格，並在時間允許的情況下，選取候補獲獎者。 此活動將只選出三名候補獲獎者，之後若無人領取獎品，將不再頒發。  

9. 獎品

    此活動將頒發下列獎品：

    - 大獎一 (1) 名。 獎品包含下列項目：
        - [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html) 的註冊通行證 (由 MMS 指導委員會提供)。 大約零售價值 (ARV) 為 1799 美元。
        - 一個 Yeti Rambler 30 盎司冰霸杯。 大約零售價值 (ARV) 為 35.00 美元。
        - 一個 Popsocket 汽車通風口支架 + 把手。 大約零售價值 (ARV) 為 15.00 美元。

        以上全部獎品的大約零售價值總計 (ARV) 為 1849 美元。

    - 一獎三 (3) 名。 獎品包含下列項目：
        - 一個 Yeti Rambler 30 盎司冰霸杯。 大約零售價值 (ARV) 為 35.00 美元。
        - 一個 Popsocket 汽車通風口支架 + 把手。 大約零售價值 (ARV) 為 15.00 美元。

        以上全部獎品的大約零售價值總計 (ARV) 為 50 美元。

    全部獎品的大約零售價值總計 (ARV) 為 1999 美元

    我們每人只頒發一 (1) 個獎品。 所頒發的獎品將不會超過規定的獎品數量。 不允許替換、轉讓或指派獎品，但 Microsoft 保留在無法取得所提供的獎品時，替換等值或更高價值獎品的權利。 獎品按「現狀」頒發，不作任何明示或默示的擔保，包括但不限於針對特定用途之適售性、適用性及未侵權的默示擔保責任。 獲獎者可能需要在獲獎者通知中規定的截止日期內，填寫並返回獎品領取和/或納稅表 (以下簡稱為「表格」)。 獎品的稅金 (如果有的話) 是獲獎者的唯一責任，建議獲獎者尋求獨立法律顧問，諮詢接受獎品所涉及的稅金。 接受獎品即表示您同意 Microsoft 可以在線上、印刷品上或其他任何媒體上使用您與本次比賽相關的參賽作品、姓名、圖像和出生地，除非法律禁止，否則將無需向您支付任何費用或賠償金。

10. 機率

    獲獎的機率取決於收到的合格參賽作品數量和品質。

11. 一般條件和責任免除

    在法律允許的範圍內，參賽即表示您同意免除並維護 Microsoft 及其各自的母公司、合作夥伴、子公司、關係企業、員工和代理商免受任何和所有與此比賽或所贏得任何獎品相關的責任或任何傷害、損失或損害。

    所有當地法律均適用。 Microsoft 的決定最具關鍵性，而且具有約束力。

    我們保留因任何原因而取消、更改或暫停本次比賽的權利，包括作弊、技術失敗、災難、戰爭或影響本次比賽完整性 (無論是人為還是操作) 的其他任何未預見或非預期事件。 如果無法恢復比賽的完整性，我們可能會在取消、更改或暫停比賽之前，從所有符合資格的參賽作品中選出獲獎者。 違規者將依法受到起訴，而且可能會被禁止參與 Microsoft 比賽。

12. 獲獎者名單

    獲獎者名單將會在 2019 年 5 月 9 日起的 30 天內張貼到 https://aka.ms/mms2019docathon 。

13. 隱私權

    在 Microsoft，我們致力於保護您的隱私權。 Microsoft 會使用您在此表格上提供的資訊，向您通知有關我們的產品、升級和增強功能的重要資訊，並將其他 Microsoft 產品和服務的相關資訊發送給您。 未經您的許可，除非是完成您所要求服務或交易所需，或法律要求，否則 Microsoft 將不會與第三方分享您所提供的資訊。 Microsoft 致力於保護您個人資訊的安全性。 我們會應用各種安全性技術與程序，防止未經授權而存取、使用或洩漏您的個人資訊。 未經您的許可，除非在上述條件下，否則絕不會在公司外部分享您的個人資訊。

    如果您認為 Microsoft 未遵守此聲明，請透過將電子郵件發送至 privrc@microsoft.com，或將郵件郵寄至 Microsoft Privacy Response Center, Microsoft Corporation, One Microsoft Way, Redmond, WA 98052，藉此與 Microsoft 聯繫。
