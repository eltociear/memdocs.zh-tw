---
title: 如何取得 Microsoft Intune 支援
titleSuffix: Microsoft Intune
description: 取得 Microsoft Intune 付費和試用訂閱的線上和電話支援。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7fc95d17-098e-4da5-8a09-a96476569dd9
ms.reviewer: crisk
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6fef418394a37f0074ddb17cc170a61603b1d7f8
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093125"
---
# <a name="how-to-get-support-for-microsoft-intune"></a>如何取得 Microsoft Intune 支援

Microsoft 為 Microsoft Intune 提供全球的技術、售前、帳單及訂閱支援。 付費及試用訂閱可透過網路和電話兩種途徑取得支援服務。 線上技術支援提供英文與日文服務。 電話支援與線上帳單支援提供其他語言服務。

如果您是 Intune 系統管理員，可以使用 [說明及支援] 選項提交 Azure 入口網站發出的 Intune 線上支援票證。 若要建立及管理支援事件，則帳戶必須具有包含「動作」**microsoft.office365.supportTickets** 的 Azure Active Directory (Azure AD) 角色。 如需建立支援票證時所需 Azure AD 角色和權限的資訊，請參閱 [Azure Active Directory 中的系統管理員角色](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)。

>[!IMPORTANT]
> 針對與 Intune 搭配使用但不是由 Microsoft 所開發之產品 (例如 Saaswedo、Cisco 或 Lookout) 的技術支援，請先連絡該產品的供應商。 在向 Intune 支援開啟要求之前，請確定您已正確設定其他產品。
>
> 如需針對 Microsoft Intune 相關問題進行疑難排解的資訊，請參閱 Intune 文件的[疑難排解](help-desk-operators.md)一節。

## <a name="help-and-support-experience"></a>說明及支援體驗

Intune 的說明及支援體驗可以從 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，以及從 Azure 入口網站中 Intune 下的所有刀鋒視窗 (或頁面) 存取。

「說明及支援」體驗與 [Microsoft 365 系統管理中心](https://admin.microsoft.com/)中所看見的體驗類似，並取代了先前的「說明 + 支援」，其對於 Azure 中的其他服務而言會維持不變。

### <a name="options-to-access-help-and-support"></a>存取 [說明及支援] 的選項

當您針對 Intune 使用新建立的租用戶時，可能無法開啟 [說明及支援]，並傳回下列訊息：

- 「我們遇到未知的問題。請重新整理頁面。如果問題仍然存在，請透過 [M365 系統管理中心](https://admin.microsoft.com)建立案例並參考所提供的工作階段識別碼。」

錯誤詳細資料會包含「工作階段識別碼」、「擴充」詳細資料等。

此問題會在您尚未透過 **M365 系統管理中心** (位於 https://admin.microsoft.com ) 或 **Office 365 入口網站** (位於 https://portal.office.com ) 驗證新的租用戶帳戶時發生。 若要解決此問題，請選取訊息中的「M365 系統管理中心」連結，或是造訪 https://portal.office.com ，然後登入。 在任一網站上完成驗證之後，Intune 的 [說明及支援] 便可供存取。

**存取說明及支援**：

- **在 Azure 入口網站中**

  - 從任何 Intune 刀鋒視窗或頁面選取 [說明及支援]。

  > [!NOTE]  
  > 如果您的 Intune 執行個體裝載於如 Azure Government 之類的政府私人雲端 (也稱為主權雲端) 中，請參閱此文章後段的[適用於政府私人雲端的 Intune 支援](#intune-support-for-private-cloud-for-government)。 Intune 的 [說明及支援] 體驗要到明年才會在政府私人雲端上提供。

- **從 Microsoft 端點管理員系統管理中心**

  - 從 Microsoft 端點管理員系統管理中心的任何節點內，選取 [?] 圖示，其位於入口網站右上角，可開啟 [說明] 窗格。 選取 [說明 + 支援] 以開啟 [選取管理類型] 頁面。

    > [!div class="mx-imgBorder"]
    > ![開啟 [選取管理類型] 頁面](./media/get-support/management-types.png)

    使用下拉式選單選取您要協助的管理類型，這會開啟適用的 [說明及支援] 頁面。 Microsoft 端點管理員系統管理中心支援下列管理類型，而您必須選取所需要協助的管理類型 (例如 Intune)：

    - Configuration Manager
    - Intune
    - 共同管理

    > [!div class="mx-imgBorder"]
    > ![選取您的管理類型](./media/get-support/select-management-type.png)

    選取管理類型之後，隨即開啟適用的 [說明及支援] 頁面，您可在此針對特定問題指定詳細資料來[尋找解決方案](#find-solutions)。 詳細資料會根據您選取的管理類型進行篩選。

     若未選取正確的管理類型 **(1)** ，請按一下 [選取管理類型] **(2)** ，返回 [選取管理類型] 下拉式清單：

    > [!div class="mx-imgBorder"]
    > ![確認您的管理類型](./media/get-support/confirm-management-selection.png)

  - 如果您從 [疑難排解 + 支援] > [說明及支援] 開啟 [說明及支援]，將不會看到您選取的管理類型列於 [說明及支援] 下方。

  - 如果您深入探索任何其他節點 (例如 [裝置]、[應用程式] 或 [使用者])，然後選取 [說明及支援]，則不會有機會選取管理類型，該類型也不會顯示於 [說明及支援] 下方。 在此案例中為 *Intune*。 如果您不想要將內容設定為 Intune，請使用 [?] 選項，讓您可以選取不同的管理類型。

### <a name="the-support-experience"></a>支援體驗

  開啟 [說明及支援] 時，入口網站會顯示 [需要協助嗎?] 視窗：

  ![檢視需要協助嗎視窗](./media/get-support/need-help.png)

  左上角有三個圖示可供您選取，來開啟 [需要協助嗎?] 視窗的不同窗格。 您檢視的窗格會以底線識別。

  具備**頂級**或**統一**支援合約的客戶可享有[額外支援選項](#premier-and-unified-support-customers)，並且會在 [需要協助嗎?] 中看到構成下列影像的橫幅：![頂級橫幅](./media/get-support/premier-banner.png)

  [需要協助嗎?] 會對 [尋找解決方案] 窗格開啟。 不過，如果您有正在進行的支援案例，視窗就會對 [服務要求] 窗格開啟，您可在其中檢視正在進行和已關閉支援案例的詳細資料。

#### <a name="find-solutions"></a>尋找解決方案

![選取尋找解決方案窗格](./media/get-support/find-solutions.png)

請在 [尋找解決方案] 窗格中，於提供的文字方塊內指定一些有關問題的詳細資料。 根據您對問題提供的文字，窗格會填入可能符合的見解。 您也會獲得建議文章的連結，可能能夠協助您解決問題。

如果有相當符合您描述之詳細資料的項目，疑難排解提示就會顯示在 [需要協助嗎?] 視窗內。

舉例來說，如果您輸入**密碼同步處理錯誤**， 結果就會直接在窗格中包含疑難排解指導，以及連至我們文件庫建議文章的連結。

![檢視疑難排解見解](./media/get-support/troubleshooting-insights.png)

#### <a name="contact-support"></a>請連絡支援部門

![選取連絡支援人員窗格](./media/get-support/contact-support.png)

您可以從 [連絡支援人員] 窗格提交協助要求。 當您在 [尋找解決方案] 窗格提供一些基本關鍵字後，就能使用此窗格。

要求協助時，請盡可能提供詳盡的問題描述。  確認手機和電子郵件連絡人資訊後，請選取您偏好的連絡方法。 視窗會顯示各種連絡方法的回應時間，這能讓您了解大概的連絡時間。 提交要求前，請附上記錄檔或螢幕擷取畫面等能夠詳述問題的檔案。

![連絡支援表單](./media/get-support/contact-support-form.png)

填完必要資訊後，請選取 [連絡我] 來提交要求。

#### <a name="service-requests"></a>服務要求

![選取服務要求窗格](./media/get-support/service-requests.png)

[服務要求] 窗格會顯示您的案例歷程記錄。 進行中的案例會顯示在清單頂端，已關閉的問題也能供您檢閱。

![檢閱服務要求清單](./media/get-support/service-requests-pane.png)

如果您有進行中的支援案例編號，可以在此輸入該編號來跳到該問題，或是在包含進行中與已關閉問題的清單選取任何事件，來檢視有關事件的詳細資訊。

當您完成檢視事件的詳細資料之後，請在三個 [需要協助嗎?] 窗格圖示正上方的服務要求頂端，選取顯示的向左箭號。 向後箭頭會返回您開啟的支援事件清單。

#### <a name="premier-and-unified-support-customers"></a>頂級與統一支援客戶

具有**頂級**或**統一**支援合約的客戶可以指定問題的嚴重性，並為特定時間和日期排程支援回電。 當您開啟或提交新問題，或是編輯進行中的支援案例時，就能使用這些選項。

**嚴重性** - 根據支援合約來指定問題嚴重性的選項：

- 頂級：A、B 或 C 嚴重性
- 統一：重大或非重大

選取嚴重性 **A** 或**重大**問題會限制您使用手機支援案例，這是最快獲得支援的選項。

**回電排程** - 您可以要求在特定日期和時間回電。

## <a name="azure-help--support-experience"></a>Azure 說明 + 支援體驗

除非您的訂用帳戶是位於政府的私人雲端上，否則您無法再使用 Azure 的 [說明 + 支援] 體驗來取得 Intune 的協助。
如果您的 Intune 執行個體未在政府的私人雲端上執行，瀏覽 Azure 的 [說明 + 支援] 會將您重新導向至 Intune 的 [說明及支援] 體驗，以建立及管理支援事件：

當您使用左側瀏覽窗格的 [說明 + 支援]，或使用 Azure 入口網站右上角的 [?] 開啟 [說明] 窗格，然後選取 [說明 + 支援] 的選項，您可以開啟 Azure [說明 + 支援] 頁面。

從此頁面選取 [+ 新增支援要求] 以開啟 [說明 + 支援 + 新增支援要求] 頁面的 [基本] 索引標籤。

![說明 + 支援](./media/get-support/help-plus-support.png)

在此頁面上：

- 針對 [問題類型]，請選取 [技術]。
- 針對 [服務]，請選取 [Microsoft Intune]。

  然後您會看到連結，將您重新導向至 [Intune 說明及支援頁面](https://aka.ms/intunehelpsupport)。
  
  ![新增支援要求](./media/get-support/new-request.png)

## <a name="intune-support-for-private-cloud-for-government"></a>適用於政府私人雲端的 Intune 支援

當您的 Intune 訂用帳戶裝載於如 Azure Government 的政府私人雲端 (也稱為主權雲端) 時，您還無法存取較新的 Intune [說明及支援] 體驗。  請改用下列資訊來取得 Intune 的支援。

### <a name="create-an-online-support-ticket"></a>建立線上支援票證

>[!IMPORTANT]
> 由於「說明及支援」正在轉換至尚未提供給政府私人雲端使用的新系統，因此當您建立支援事件時，入口網站會識別使用 15 位數識別碼的支援案例。 建立 15 位數案例時，會建立該案例的鏡像以供 Microsoft 支援服務使用。 這個鏡像案例會建立於新的支援系統中、使用 8 位數案例識別碼，並由支援服務用來追蹤您支援事件的所有工作和通訊。 在建立 15 位數案例之後不久，您將會收到一封電子郵件，可識別支援服務所使用的 8 位數鏡像支援案例識別碼。
>
> 從 8 位數支援案例支援個人工作並進行通訊，而且只會使用 8 位數支援案例來記錄通訊並追蹤事件進度。 因此，您將收到來自該 8 位數支援案例的電子郵件更新，以用來做為您的案例-工作追蹤記錄。 不會在 15 位數支援事件中記錄任何詳細資料。 當支援終止且 8 位數支援案例關閉時，該狀態就會反映於您可在 Azure 入口網站中檢視的 15 位數支援案例。  您不應預期會對 15 位數支援案例進行任何其他更新或狀態變更。
>
> 當支援工具之間的轉換在今年下半年完成時，Intune 裝載於政府雲端的支援體驗將類似目前可供裝載於公用雲端之 Intune 訂用帳戶使用的預設「說明及支援」體驗。

1. 使用您的 Intune 系統管理員認證來登入 Azure 入口網站 (<https://portal.azure.us>)，然後選取 **?** 圖示，然後選取 [說明 + 支援] 以移至 [Azure 說明 + 支援](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)頁面。

   ![醒目提示 [說明 + 支援] 連結的問號連結影像](./media/get-support/azure-get-support.png)

2. 在 Azure [說明 + 支援] 頁面上，選取 [新增支援要求]。

   ![[說明及支援] 頁面上醒目提示 [新增支援要求] 連結的影像](./media/get-support/azure-support-ticket-link.png)

3. 在 [基本] 索引標籤上，針對大多數 Intune 技術支援問題選擇下列選項：
   - **問題類型**：**技術**
   - **訂用帳戶**：<*您的訂用帳戶*>
   - **服務**：**Microsoft Intune**
   - **問題類型**：從下拉式功能表中選擇您的問題類型。
   - **問題子類型**：從下拉式功能表中選擇問題子類型。
   - **主旨**：簡要描述您需要協助解決的問題。

   ![[說明 + 支援] - [新增支援要求] 頁面上的 [基本] 索引標籤影像](./media/get-support/help-new-support-case-basics.png)

   選擇 [下一步:解決方案] 以繼續操作。
4. 在 [解決方案] 索引標籤上，檢閱或許能協助您無須提出票證即可解決問題的建議步驟。 如果在瀏覽過這些步驟之後，您仍然想要建立支援要求，請按 [下一步:詳細資料]。

   ![[說明 + 支援] - [新增支援要求] 頁面上的 [解決方案] 索引標籤影像](./media/get-support/help-new-support-case-solutions.png)
5. 在 [詳細資料] 索引標籤上，填寫問題的詳細資料、支援方法、您的連絡資訊，然後按 [下一步:檢閱 + 建立]。

   ![[說明 + 支援] - [新增支援要求] 頁面上的 [詳細資料] 索引標籤影像](./media/get-support/help-new-support-case-details.png)
6. 檢閱資訊、確認資訊正確，然後選擇 [建立] 以提交支援要求。

   ![[新增支援要求] 頁面上的 [檢閱 + 建立] 索引標籤影像](./media/get-support/help-new-support-case-create.png)

>[!IMPORTANT]
>如果有帳單或訂閱問題，您可以透過 [Microsoft 365 系統管理中心](https://admin.microsoft.com/Support/SupportEntry.aspx)開啟案例來取得支援。

### <a name="view-support-requests"></a>檢視支援要求  

您可以在 Azure 入口網站中檢視您的支援要求。 不過，所提供的資訊有限。  檢視您的事件：

1. 使用您的 Intune 系統管理員認證來登入 Azure (<https://portal.azure.com>)，然後選取 **?** 圖示，然後選取 [說明 + 支援] 以移至 [Azure 說明 + 支援](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)頁面。

2. 在 [說明 + 支援] 頁面上，您可以檢視 [最近的支援要求] 清單。

   > [!IMPORTANT]  
   > 政府私人雲端客戶只能檢視 15 位數支援案例號碼，以及事件狀態。 工作或警示的所有案例通訊和追蹤都會透過電子郵件傳送，並參考 8 位數支援案例識別碼，此識別碼會建立來作為從 Intune 主控台中開啟的支援案例鏡像。

## <a name="additional-resources"></a>其他資源  

- [帳單和訂閱管理支援](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)
- [大量授權](https://go.microsoft.com/fwlink/p/?LinkID=282015)
- [針對 Intune 問題進行疑難排解](help-desk-operators.md)
