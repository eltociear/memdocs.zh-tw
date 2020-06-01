---
title: 將 Windows 作為服務管理
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 檢視 Windows 即服務 (WaaS) 的狀態、建立服務方案以形成部署環節，以及在 Windows 10 用戶端支援即將結束時檢視警示。
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690326"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>使用 Configuration Manager 管理 Windows 即服務

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中，您可以檢視環境中的 Windows 即服務 (WaaS) 狀態。 建立服務方案以形成部署環節，並確保在新組建發行時，Windows 10 系統會保持為最新狀態。 您也可以在 Windows 10 用戶端的半年通道組建支援即將結束時檢視警示。

如需 Windows 10 服務選項的詳細資訊，請參閱 [Windows 即服務概觀](/windows/deployment/update/waas-overview#servicing-channels)。

使用下列各節來管理 Windows 即服務。

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> 先決條件

若要查看 Windows 10 服務儀表板中的資料，您必須執行下列動作：

- Windows 10 電腦都必須使用 Configuration Manager 軟體更新，並以 Windows Server Update Services (WSUS) 進行軟體更新管理。 當電腦使用商務用 Windows Update (或 Windows Insiders) 來進行軟體更新管理時，電腦不會在 Windows 10 服務方案中評估。 如需詳細資訊，請參閱 [與 Windows 10 中的 Windows Update for Business 整合](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)。

- 使用支援的 WSUS 版本：
  - WSUS 10.0.14393 (Windows Server 2016 中的角色)
  - WSUS 10.0.17763 (Windows Server 2019 中的角色) (需要 Configuration Manager 1810 或更新版本)
  - WSUS 6.2 和 6.3 (Windows Server 2012 和 Windows Server 2012 R2 中的角色)
    - 您必須在 WSUS 6.2 和 6.3 上[安裝 KB 3095113 與 KB 3159706 (或同等更新)](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)。

- 啟用活動訊號探索。 您可使用探索功能，找到 Windows 10 服務儀表板中所顯示的資料。 如需詳細資訊，請參閱 [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc)。

    系統會發現下列 Windows 10 通道和組建資訊並將其儲存在下列屬性：  

    - **作業系統就緒分支**：指定作業系統通道。 例如，**0** = 半年通道 - 已設定目標 (不延後更新)、**1** = 半年通道 (延後更新)、**2** = 長期維護通道 (LTSC)

    - **作業系統組建**：指定作業系統組建。 例如，**10.0.10240** (RTM) 或 **10.0.10586** (1511 版)

- 必須安裝服務連線點，並針對 [線上，持續連線]  模式設定，才能在 Windows 10 服務儀表板上看到資料。 處於離線模式時，將無法看到儀表板中的資料更新，直到您獲得 Configuration Manager 服務更新為止。 如需詳細資訊，請參閱 [About the service connection point](../../core/servers/deploy/configure/about-the-service-connection-point.md) (關於服務連接點)。

- 執行 Configuration Manager 主控台的電腦上必須安裝 Internet Explorer 9 或更新版本。

- 必須設定並同步處理軟體更新。 先選取 [升級]  分類並同步軟體更新，Configuration Manager 主控台中才會顯示可用的 Windows 10 功能升級。 如需詳細資訊，請參閱 [Prepare for software updates management](../../sum/get-started/prepare-for-software-updates-management.md) (準備軟體更新管理)。

- 從 Configuration Manager 1902 版開始，驗證 [指定功能更新的執行緒優先順序]  [用戶端設定](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)，以確定它適合您的環境。

- 從 Configuration Manager 1906 版開始，驗證 [啟用功能更新的動態更新]  [用戶端設定](../../core/clients/deploy/about-client-settings.md#bkmk_du)，以確定它適合您的環境。 <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Windows 10 服務儀表板

Windows 10 服務儀表板可提供您環境中 Windows 10 電腦的相關資訊、使用中的服務方案、相容性資訊等等。 Windows 10 服務儀表板中的資料取決於已安裝的服務連線點。 儀表板具有以下磚：

- **Windows 10 使用方式磚**：提供 Windows 10 公開組建的細分。 您站台尚不知道的組建，以及 Windows 測試人員組建均會列為 [其他]  。 服務連線點會下載能通知它關於 Windows 組建的中繼資料，然後系統會將此資料與探索資料比較。

- **Windows 10 更新步調磚**：提供依通道和整備狀態分組的 Windows 10 細分。 LTSC 區段包含所有 LTSC 版本。 第一個磚會細分特定的版本，例如 Windows 10 LTSC 2015。

- **建立服務方案磚**：提供快速建立服務方案的方法。 您指定名稱、集合 (只顯示依大小排列的前 10 個集合，最小的最先)、部署套件 (只顯示依最近修改時間排列的前 10 個套件) 和整備狀態。 其他設定會使用預設值。 按一下 [進階設定]  啟動 [建立服務方案精靈]，您可於此處設定所有服務方案設定。

- **已過期磚**：顯示屬於 Windows 10 組建且已超出其生命週期結束的裝置百分比。 Configuration Manager 會以服務連線點下載並與探索資料相比較的中繼資料來判斷百分比。 已超出其生命週期結束的組建不會再收到每月累計更新，其中包括安全性更新。 此分類中的電腦應該升級至下一個組建版本。 Configuration Manager 會無條件進位到下一個整數。 例如，如果您有 10,000 部電腦，且只有一部使用已過期的組建，磚便會顯示 1%。

- **即將過期磚**：顯示屬於接近生命週期結束 (大約四個月內) 之組建的電腦百分比，類似於 **已過期** 磚。 Configuration Manager 會無條件進位到下一個整數。

- **警示磚**：顯示作用中的警示。

- **服務方案監視磚**：顯示您所建立的服務方案和每個方案的合規性圖表。 此磚可讓您快速獲得服務方案部署的目前狀態概觀。 如果先前的部署環符合您預期的相容性，則您可以選取稍後的服務方案 (部署環)，然後按一下 [立即部署]  而不要等待服務方案規則自動觸發。

- **Windows 10 組建磚**：顯示固定的映像時間表，提供您目前發行 Windows 10 組建的概觀，並讓您大概了解組建何時會轉換為不同的狀態。 由於在[產品生命週期儀表板](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md)中提供了更詳細的資訊，因此從 Configuration Manager 版本 1902 開始已移除此圖格。 <!--3446861-->

> [!IMPORTANT]
> Windows 10 服務儀表板中顯示的資訊 (例如 Windows 10 版本的支援生命週期) 僅為了您的方便起見而提供，並僅供在貴公司內部使用。 您不應完全依賴這項資訊來確認更新相容性。 請務必驗證提供給您的資訊是否正確。

## <a name="drill-through-required-updates"></a>鑽研需要的更新
<!--4224414-->
*(於 1906 版推出)*

您可以鑽研合規性統計資料，了解哪些裝置需要特定的 Windows 10 功能更新。 若要檢視裝置清單，您需要檢視更新及裝置所屬集合的權限。 向下切入至裝置清單：

1. 前往 [軟體程式庫]   > [Windows 10 服務]   > [所有 Windows 10 更新]  。
1. 選取至少一部裝置所需的任何更新。
1. 查看 [摘要]  索引標籤，然後尋找 [統計資料]  下方的圓形圖。
1. 選取圓形圖旁的 [需要檢視]  超連結，以向下切入至裝置清單。
1. 此動作會帶您前往 [裝置]  下方的臨時節點，以查看需要更新的裝置。 您也可以對節點採取動作，例如從清單建立新的集合。

## <a name="servicing-plan-workflow"></a>服務方案工作流程

Configuration Manager 中的 Windows 10 服務方案非常類似於軟體更新的自動部署規則。 建立服務方案時使用 Configuration Manager 評估的下列準則：

- **升級分類**：只會評估**升級**分類中的更新。

- **整備狀態**：服務方案中定義的整備狀態會與升級的整備狀態比較。 當服務連線點時檢查是否有更新時，會擷取升級的中繼資料。

- **時間延遲**：您在服務方案中為 [您希望在 Microsoft 發行新版升級的幾天後，部署至您的環境]  指定的天數。 如果目前的日期是在發行日期加上設定天數之後，Configuration Manager 會評估是否要在部署中包含升級。

  當升級符合準則時，服務方案會將升級新增到部署套件、將套件發佈到發佈點，並根據您在服務方案中進行的設定將升級部署至集合。 您可以在 Windows 10 服務儀表板上的 [服務方案監視] 磚監視部署。 如需詳細資訊，請參閱 [Monitor software updates](../../sum/deploy-use/monitor-software-updates.md) (監視軟體更新)。

> [!NOTE]
> **Windows 10 1903 版及更新版本**已新增到 Microsoft Update 成為該產品的一部分，而不再像舊版，隸屬於 **Windows 10** 產品。 此變更導致您需要執行一些手動步驟以確保您的用戶端可看到這些更新。 我們已協助減少您必須為 Configuration Manager 1906 版新產品進行的手動步驟數量。 如需詳細資訊，請參閱[設定 Windows 10 各版本的產品](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later)。<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Windows 10 服務方案

部署 Windows 10 半年通道時，您可以建立一個或多個服務方案，以定義環境中想要的部署環，然後在 Windows 10 服務儀表板中監視它們。 服務方案只會使用 **升級** 軟體更新分類，而不會使用 Windows 10 的累積更新。 針對那些更新，您仍需要使用軟體更新工作流程進行部署。 服務方案的使用者經驗和軟體更新相同，包括您在服務方案中進行的設定。  

> [!NOTE]
> 您可以使用工作順序部署每個 Windows 10 組建的升級，但它需要更多的手動工作。 您必須匯入更新的來源檔案作為作業系統升級套件，然後建立工作順序並部署到適當的電腦集合。 不過，工作順序會提供其他自訂的選項，例如預先部署和部署後動作。

您可以透過 Windows 10 服務儀表板建立基本服務方案。 指定名稱、集合 (只顯示依大小排列的前 10 個集合，最小的最先列出)、部署套件 (只顯示依最近修改時間排列的前 10 個套件) 和整備狀態之後，Configuration Manager 會針對其他設定使用預設值來建立服務方案。 您也可以啟動 [建立服務方案精靈]，進行所有設定。 使用下列程序，以 [建立服務方案精靈] 建立服務方案。  

> [!NOTE]  
> 您可以管理高風險部署的行為。 高風險部署是一種會自動安裝的部署，而且可能會造成不需要的結果。 例如部署 Windows 10 的工作順序，其用途若為 **必要** ，就會被視為高風險的部署。 如需詳細資訊，請參閱 [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (高風險部署的管理設定)。

### <a name="to-create-a-windows-10-servicing-plan"></a>建立 Windows 10 服務方案

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。

1. 在 [軟體程式庫] 工作區中，展開 [Windows 10 服務]  ，然後按一下 [服務方案]  。

1. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立服務方案]  。 [建立服務方案精靈] 隨即開啟。

1. 在 [一般]  頁面，設定以下設定：

    - **名稱**：指定服務方案的名稱。 名稱必須是唯一的，且能協助描述規則目標，並能在 Configuration Manager 網站上從其他名稱中輕易找出。

    - **描述**：指定服務方案的描述。 描述應提供服務方案的概觀，以及任何其他可協助您在 Configuration Manager 網站內找出並區分方案的相關資訊。 描述欄位是選用欄位，長度限制為 256 字元，預設為空白值。

1. 在 [服務方案] 頁面上，指定 [目標集合]  。 集合內的成員會收到服務方案中定義的 Windows 10 升級。

    - 當您部署服務方案之類的高風險部署時，[選取集合]  視窗僅會顯示符合該站台內容中所設定之部署驗證設定的自訂集合。

    - 高風險的部署一律限制於自訂集合、您建立的集合，以及內建的 [未知的電腦]  集合。 當您建立高風險的部署時，您無法選取 [所有系統]  這類的內建集合。 取消核取 [隱藏成員計數大於網站大小下限設定的集合]  ，即可查看所含用戶端少於設定之大小上限的所有自訂集合。 如需詳細資訊，請參閱 [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (高風險部署的管理設定)。

    - 部署驗證設定會以目前的集合成員資格為依據。 在您部署服務方案之後，系統並不會針對高風險的部署設定重新評估集合成員資格。

      - 例如，假設您將 [預設大小]  設為 100，而 [最大值]  設為 1000。 當您建立高風險部署時，[選取集合]  視窗只會顯示所含用戶端少於 100 個的集合。 如果您清除 [隱藏成員計數大於站台大小下限設定的集合]  設定，則此視窗會顯示所含用戶端少於 1000 個的集合。  
      當您選取包含站台角色的集合時，會套用下列條件：
        - 如果集合包含站台系統伺服器，而在部署驗證設定中，您設定要封鎖包含站台系統伺服器的集合，則會發生錯誤而無法繼續。
        - 如果集合包含站台系統伺服器，而在部署驗證設定中，您設定如果集合具有站台系統伺服器、如果集合超過預設大小值或集合包含伺服器時要提出警告，則 [部署軟體精靈 ] 會顯示高風險的警告。 您必須同意建立高風險部署，即會建立一則稽核狀態訊息。

1. 在 [部署環] 頁面上，進行下列設定：

   - **指定應套用此服務方案的 Windows 整備狀態**：選取下列其中一個選項：

      - **半年通道 (已設定目標)** ：在此服務模型中，功能更新在 Microsoft 發行它們之後即可供使用。

      - **半年通道**：此服務通道通常用於廣泛部署。 「半年通道」中的 Windows 10 用戶端會接收到和「已設定目標通道」裝置相同的 Windows 10 組建，只是時間較晚。

        針對服務通道及最適合您使用的選項，如需相關詳細資訊，請參閱[服務通道](/windows/deployment/update/waas-overview#servicing-channels)。

   - **Microsoft 發行新的升級之後，您想要在您的環境中部署之前等待的天數**：如果目前的日期是發行日期加上您為此設定所設定的天數之後，Configuration Manager 會評估是否要在部署中包含升級。

1. 在 [升級] 頁面上，設定搜尋準則以篩選已新增至服務方案的升級。 只有符合指定準則的升級才會新增至相關聯的部署。 可使用下列內容篩選器： <!--3098809, 3113836, 3204570 -->

   - **架構** (從版本 1810 開始)
   - **語言**
   - **產品類別** (從版本 1810 開始)
   - **必要**
      > [!IMPORTANT]
      > 我們建議將搜尋準則 [必要]  欄位的值設定為 **>=1**。 使用此準則能確保只會將適用的更新新增至服務方案。
   - **已被取代** (從版本 1810 開始)
   - **標題**

    按一下 **[預覽]** 可檢視符合指定準則的升級。

1. 在 [部署排程] 頁面，指定以下設定：

   - **排程評估**：指定 Configuration Manager 是否要使用 UTC 或執行 Configuration Manager 主控台之電腦上的本機時間，來評估可用的時間和安裝期限時間。

       > [!NOTE]
       > 當您選取本機時間，然後針對 [軟體可用時間]  或 [安裝期限]  選取 [盡快]  時，就會使用執行 Configuration Manager 主控台之電腦上的目前時間，來評估更新可用時間或更新安裝於用戶端的時間。 如果在用戶端位於其他時區，則會在用戶端的時間達到評估時間時，執行這些動作。

   - **軟體可用時間**：選取以下其中一種設定來指定用戶端何時可以使用軟體更新：

        - **盡快**：選取此設定來使用戶端電腦能在最短時間內使用包含在部署中的軟體更新。 利用選取的設定建立部署時，Configuration Manager 會更新用戶端原則。 接著，在下一個用戶端原則輪詢循環中，用戶端將會察覺該部署並取得安裝可用的更新。

        - **特定時間**：選取此設定來使用戶端電腦能在特定日期和時間使用包含在部署中的軟體更新。 建立部署時啟用此設定，Configuration Manager 會更新用戶端原則。 接著，在下一個用戶端原則輪詢循環中，用戶端將會察覺該部署。 不過，在設定的日期和時間之前，無法使用部署中的軟體更新進行安裝。

   - **安裝期限**：選取下列其中一個設定，以指定部署中軟體更新的安裝期限：

        - **盡快**：選取此設定，以自動在最短時間內安裝部署中的軟體更新。

        - **特定時間**：選取此設定，以在特定日期和時間自動安裝部署中的軟體更新。 將已設定的 [特定時間]  間隔新增到 [軟體可用時間]  ，Configuration Manager 藉此判斷安裝軟體更新的期限。

           > [!NOTE]
           > 實際安裝的期限時間是顯示的期限時間，加上最多 2 小時的隨機總時間。 這能減少對同時在部署中安裝更新之目的地集合裡所有用戶端電腦的潛在影響。
           >
           > 您可以設定 [電腦代理程式]  用戶端設定的 [停用期限隨機設定]  ，針對必要的更新停用安裝隨機延遲。 如需詳細資訊，請參閱 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)。

        - **根據使用者喜好延遲實行此部署，最多延後至用戶端上定義的寬限期**：選取此選項可採用 [延後到部署期限後施行的寬限期 (小時)  用戶端設定](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours)。

1. 在 [使用者經驗] 頁面，設定以下設定：  

    - **使用者通知**：指定是否要在設定的 [軟體可用時間]  內，顯示用戶端電腦上 [軟體中心] 內更新的通知，以及是否要在用戶端電腦上顯示使用者通知。

    - **期限行為**：指定到達更新部署期限時會出現的行為。 指定是否安裝部署中的更新。 同時也指定是否於無論設定之維護期間為何的狀況下，只要更新安裝完成，就執行系統重新啟動。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    - **裝置重新啟動行為**：於安裝更新，且需要重新啟動系統才能完成安裝的狀況下，指定是否抑制在伺服器和工作站上重新啟動系統。

    - **Windows Embedded 裝置的寫入篩選處理**：將更新部署至啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝更新，並於稍後再認可變更，或是在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。
        - 當您將更新部署至 Windows Enbedded 裝置時，請確認裝置是已設定維護期間之集合的成員。

    - **重新啟動時的軟體更新部署重新評估行為**：若要在重新啟動後強制執行其他更新部署評估週期，請選取 [If any update in this deployment requires a system restart, run updates deployment evaluation cycle after restart] \(若此部署中的任何更新需要重新啟動系統，請在重新啟動後執行更新部署評估週期)\  選項。

1. 在 [部署套件] 頁面上選取現有的部署套件或沒有部署套件，或進行下列設定以建立新的部署套件：

    1. **名稱**：指定部署套件的名稱。 此名稱必須是唯一且能描述套件內容。 長度限制為 50 個字元。

    1. **描述**：指定描述，提供有關部署套件的資訊。 描述限制為 127 個字元。

    1. **套件來源**：指定軟體更新來源檔案的位置。 鍵入來源位置的網路路徑，例如 **\\\伺服器\\共用名稱\\路徑**，或按一下 [瀏覽]  尋找網路位置。 請先建立部署套件來源檔案的共用資料夾，再繼續執行下一個頁面。
        - 您指定的部署套件來源位置不能供另一個軟體部署套件使用。
        - SMS 提供者電腦帳戶和執行精靈下載軟體更新的使用者，都必須具有下載位置的 **寫入** NTFS 權限。 您應謹慎限制下載位置的存取權，以降低攻擊者竄改軟體更新來源檔案的風險。
        - 您可以在 Configuration Manager 建立部署套件之後，變更部署套件內容中的套件來源位置。 不過，如果您這樣做，則必須先將內容從原始套件來源複製到新的套件來源位置。

    1. **傳送優先順序**：指定部署套件的傳送優先順序。 Configuration Manager 將套件傳送到發佈點時，會針對部署套件使用傳送優先順序。 部署套件會依照下列優先順序傳送：高、中或低。 優先順序相同的套件，會依照建立的順序傳送。 若沒有待處理項目，則無論套件的優先順序為何，系統都會立即處理它。

    1. **啟用二進位差異複寫**：如果想要使用二進位差異複寫，請啟用此選項。

1. 在 [發佈點] 頁面上，指定裝載更新檔案的發佈點或發佈點群組。 如需發佈點的詳細資訊，請參閱[設定發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。

    > [!NOTE]
    > 此頁面只有在您建立新的軟體更新部署套件時才可使用。  

1. 在 [下載位置] 頁面上，指定要從網際網路或您的區域網路下載更新檔案。 進行以下設定：

    - **從網際網路下載軟體更新**：選取此設定會從網際網路上指定的位置下載更新。 預設會啟用此設定。

    - **從區域網路上的位置下載軟體更新**：選取此設定會從本機目錄或共用資料夾下載更新。 此設定在執行精靈的電腦沒有網際網路存取時很實用。 有網際網路存取的任何電腦都可預先下載更新，並將其儲存到區域網路上可從執行精靈的電腦存取的位置。

1. 在 [語言選擇] 頁面上，選取下載選定更新的語言。 更新只會在有提供所選語言時才能下載。 無指定語言的更新一律會下載。 根據預設，精靈會選取您在軟體更新點內容中設定的語言。 您必須至少選取一種語言才能繼續至下一頁。 如果您只選取更新不支援的語言，則更新下載會失敗。

1. 在 [摘要] 頁面上，檢閱設定，然後按一下 [下一步]  建立服務方案。  

在您完成精靈後，服務方案就會執行。 它會將符合指定準則的更新新增至軟體更新群組，將更新下載至站台伺服器上的內容庫，將更新發佈至設定的發佈點，然後將軟體更新群組部署至目標集合中的用戶端。

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> 修改服務方案

您從 Windows 10 服務儀表板建立基本服務方案之後，或是需要變更現有服務方案的設定時，可以移至服務方案的內容。

> [!NOTE]
> 當您建立服務方案時，您可以在無法於精靈中使用的服務方案內容中進行設定。 精靈會針對下列各項的設定使用預設設定：下載設定、部署設定，以及警示。  

利用下列程序修改服務方案的內容。 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>修改服務方案的內容

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。

1. 在 [軟體程式庫] 工作區中，展開 [Windows 10 服務]  、按一下 [服務方案]  ，然後選取要修改的服務方案。

1. 在 [首頁]  索引標籤上，按一下 [內容]  以開啟所選服務方案的內容。

    以下設定可用於無法在精靈中設定的服務方案內容：

    **部署設定**：在 [部署設定] 索引標籤上，設定下列設定：

    - **使用網路喚醒來喚醒用戶端以進行必要部署**：指定是否要在抵達期限時啟用網路喚醒，以將喚醒封包傳送到在部署中需要一或多個軟體更新的電腦。 安裝期限時處於睡眠模式的任何電腦都會被喚醒，以起始軟體更新安裝。 在部署中處於睡眠狀態且不需要任何軟體更新的用戶端並不會啟動。 根據預設不會啟用此設定。

        > [!WARNING]
        > 您必須為電腦和網路設定 [網路喚醒] 後，才可以使用此選項。

    - **詳細等級**：指定由用戶端電腦報告之狀態訊息的詳細等級。

    **下載設定**：在 [下載設定] 索引標籤上，設定下列設定：

    - 指定當用戶端連線到速度較慢的網路，或使用後援內容位置時，是否要下載並安裝軟體更新。

    - 指定無法在慣用發佈點使用軟體更新內容時，是否要讓用戶端從後援發佈點下載並安裝軟體更新。

    - **允許用戶端與同一個子網路上的其他用戶端共用內容**：指定是否要針對內容下載啟用 BranchCache 的使用。 如需 BranchCache 的詳細資訊，請參閱[內容管理的基本概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。

    - 指定無法在發佈點上使用軟體更新時，是否允許用戶端從 Microsoft Update 下載軟體更新。
        > [!IMPORTANT]
        > Windows 10 服務更新請勿使用此設定。 Configuration Manager (至少到 1610 版) 無法從 Microsoft Update 下載 Windows 10 服務更新。

    - 指定當用戶端使用計量付費網際網路連線時，是否在過了安裝期限後仍允許用戶端進行下載。 在您處於計量付費網際網路連線時，網際網路提供者有時會根據您傳送和接收的資料量來收取費用。

    **警示**：於 [警示] 索引標籤上設定 Configuration Manager 和 System Center Operations Manager 針對此部署產生警示的方式。
    - 您可經由 [軟體程式庫]  工作區中的 [軟體更新]  節點檢閱最新的軟體更新警示。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [Configuration Manager 即服務與 Windows 即服務的基本概念](../../core/understand/configuration-manager-and-windows-as-service.md)。
