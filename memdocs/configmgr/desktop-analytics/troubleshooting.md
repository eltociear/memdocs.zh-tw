---
title: 針對電腦分析進行疑難排解
titleSuffix: Configuration Manager
description: 可協助您針對電腦分析問題進行疑難排解的技術詳細資料。
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 68506ba11e356a1e9f14d58880a80bdf3cfcb5f4
ms.sourcegitcommit: fb03634b8494903fc6855ad7f86c8694ffada8df
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85828970"
---
# <a name="troubleshoot-desktop-analytics"></a>針對電腦分析進行疑難排解

使用本文中的詳細資料，協助您對與 Configuration Manager 整合的電腦分析問題進行疑難排解。

## <a name="confirm-prerequisites"></a>確認必要條件

許多常見問題都是由於缺少必要條件所造成。 請先確認下列設定：

- [先決條件](overview.md#prerequisites)  

- [Windows 元件更新](enroll-devices.md#update-devices)  

- [如何啟用資料共用](enable-data-sharing.md)，其中涵蓋下列主題：  

  - 用戶端需要連線的網際網路端點  

  - Proxy 伺服器驗證  

  - 診斷資料層級  

## <a name="monitor-connection-health"></a>監視連線健康情況

使用 Configuration Manager 中的 [連線健全狀況] 儀表板，依裝置健全狀況向下切入到各類別。 在 Configuration Manager 主控台中，前往 [軟體程式庫] 工作區，展開 [電腦分析服務] 節點，然後選取 [連線健全狀況] 儀表板。  

如需詳細資訊，請參閱[監視連線健全狀況](monitor-connection-health.md)。

> [!NOTE]
> 電腦分析的 Configuration Manager 連線會依賴服務連接點。 對此站台系統角色所做的任何變更，可能會影響與雲端服務的同步處理。 如需詳細資訊，請參閱 [About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move) (關於服務連接點)。

從 2002 版開始，如果 Configuration Manager 站台無法連線至雲端服務的必要端點，就會引發重大狀態訊息識別碼 11488。 當無法連線至服務時，SMS_SERVICE_CONNECTOR 元件狀態會變更為重大。 在 Configuration Manager 主控台的 [[元件狀態]](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) 節點中，查看詳細狀態。<!-- 5566763 -->

## <a name="log-files"></a>記錄檔

如需詳細資訊，請參閱[電腦分析記錄檔](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

從 Configuration Manager 1906 版開始，您可以使用 Configuration Manager 安裝目錄中的 **DesktopAnalyticsLogsCollector.ps1** 工具，協助針對電腦分析進行疑難排解。 它會執行一些基本的疑難排解步驟，並將相關記錄收集到單一工作目錄中。 如需詳細資訊，請參閱[記錄收集器](log-collector.md)。

### <a name="enable-verbose-logging"></a>啟用詳細資訊記錄

1. 在服務連接點上，移至下列登錄機碼：`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. 將 [LoggingLevel] 值設定為 `0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a> Azure AD 應用程式

電腦分析會將下列應用程式新增至您的 Azure AD：

- **Configuration Manager 微服務**：連線 Configuration Manager 與電腦分析。 此應用程式沒有存取需求。  

- **MALogAnalyticsReader**：監視 Azure Log Analytics 工作區以確保成功複製每日快照集。 如需詳細資訊，請參閱 [MALogAnalyticsReader 應用程式角色](#bkmk_MALogAnalyticsReader)。  

- **電腦分析**：讓 Configuration Manager 從電腦分析擷取部署計劃資訊和裝置整備狀態。

如果您需要在完成設定之後佈建這些應用程式，請移至 [已連線的服務] 窗格。 選取 [Configure users and apps access] \(設定使用者與應用程式存取\)，然後佈建應用程式。  

- **適用於 Configuration Manager 的 Azure AD 應用程式**。 如果您需要在完成設定之後佈建，或針對連線問題進行疑難排解，請參閱[建立和匯入適用於 Configuration Manager 的應用程式](#create-and-import-app-for-configuration-manager)。 此應用程式需要 **Configuration Manager 服務** API 上的 [寫入 CM 集合資料] 和 [讀取 CM 集合資料]。  

### <a name="create-and-import-app-for-configuration-manager"></a>建立和匯入適用於 Configuration Manager 的應用程式

如果您無法從「設定 Azure 服務精靈」建立適用於 Configuration Manager 的 Azure AD 應用程式，或想要重複使用現有的應用程式，則需要手動建立並匯入應用程式。 完成電腦分析入口網站上的[初始上線](set-up.md#initial-onboarding)之後，請使用下列步驟：

#### <a name="create-app-in-azure-ad"></a>在 Azure AD 中建立應用程式

1. 以具有「全域管理員」權限的使用者身分開啟 [Azure 入口網站](https://portal.azure.com)，移至 [Azure Active Directory]，並選取 [應用程式註冊]。 然後選取 [新增註冊]。  

2. 在 [建立] 面板中，進行下列設定：  

    - **名稱**：用來識別應用程式的唯一名稱，例如：`Desktop-Analytics-Connection`  

    - **支援的帳戶類型**：**僅此組織目錄中的帳戶 (Contoso)**

    - **重新導向 URI (選用)** ：**Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    選取 [註冊]。  

3. 選取應用程式，並記下 [應用程式 (用戶端) 識別碼] 和 [目錄 (租用戶) 識別碼]。 這些值是用來設定 Configuration Manager 連線的 GUID。  

4. 在 [管理] 功能表中，選取 [憑證及祕密]。 選取 [新增用戶端密碼]。 輸入 [描述]，指定到期期間，然後選取 [新增]。 複製金鑰的 [值]，該值可用來設定 Configuration Manager 連線。

    > [!Important]  
    > 這是複製金鑰值的唯一機會。 如果您現在未複製，則需要建立另一個金鑰。  
    >
    > 將金鑰值儲存在安全的位置。  

5. 在 [管理] 功能表中，選取 [API 權限]。  

    1. 在 [API 權限] 面板上，選取 [新增權限]。  

    2. 在 [要求 API 權限] 面板中，切換至 [我的組織使用的 API]。  

    3. 搜尋並選取 **Configuration Manager 微服務** API。  

    4. 選取 [應用程式權限] 群組。 展開 [CmCollectionData]，然後選取下列兩個權限：[寫入 CM 集合資料] 和 [讀取 CM 集合資料]。  

    5. 選取 [新增權限]。  

6. 在 [API 權限] 面板上，選取 [授與管理員同意...]。選取 [是]。  

#### <a name="import-app-in-configuration-manager"></a>在 Configuration Manager 中匯入應用程式

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，展開 [雲端服務]，然後選取 [Azure 服務] 節點。 選取功能區中的 [設定 Azure 服務]。  

2. 在 [Azure 服務精靈] 的 [Azure 服務] 頁面上，進行下列設定：  

    - 為 Configuration Manager 中的物件指定 [名稱]。  

    - 指定選用 [描述] 以協助您識別服務。  

    - 從可用的服務清單中選取 [電腦分析]。  
  
   選取 [下一步]。  

3. 在 [應用程式] 頁面上，選取適當的 [Azure 環境]。 然後針對 Web 應用程式選取 [匯入]。 在 [匯入應用程式] 視窗中進行下列設定：  

    - **Azure AD 租用戶名稱**：此名稱是其在 Configuration Manager 中的命名方式  

    - **Azure AD 租用戶識別碼**：您從 Azure AD 複製的 [目錄識別碼]  

    - **用戶端識別碼**：您從 Azure AD 應用程式複製的 [應用程式識別碼]  

    - **祕密金鑰**：您從 Azure AD 應用程式複製的金鑰 [值]  

    - **祕密金鑰的到期日**：與金鑰的到期日相同  

    - **App 識別碼 URI**：這項設定應該會自動填入下列值：`https://cmmicrosvc.manage.microsoft.com/`  
  
   選取 [驗證]，然後選取 [確定]，關閉 [匯入應用程式] 視窗。 在 [Azure 服務精靈] 的 [應用程式] 頁面上，選取 [下一步]。  

若要在 [診斷資料] 頁面上繼續進行精靈的其餘部分，請參閱[連線到服務](connect-configmgr.md#bkmk_connect)。

#### <a name="troubleshoot-app-in-configuration-manager"></a>針對 Configuration Manager 中的應用程式進行疑難排解

如果您在建立或匯入應用程式時遇到問題，請先檢查 **SMSAdminUI.log** 中是否有特定錯誤。 然後檢查下列設定：

- 您已成功向電腦分析服務註冊租用戶。 如需詳細資訊，請參閱[如何設定電腦分析](set-up.md)。

- 所有必要端點都可供存取。 如需詳細資訊，請參閱[端點](enable-data-sharing.md#endpoints)。

- 確認登入的使用者具有正確的權限。 如需詳細資訊，請參閱[必要條件](overview.md#prerequisites)。

- 確認使用者可以透過一般方式登入 Azure。 此動作可判斷是否有任何一般 Azure AD 驗證問題。

- 檢查有關「電腦分析背景工作角色」的 **SMS_SERVICE_CONNECTOR** 元件狀態訊息。

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a> MALogAnalyticsReader 應用程式角色

當您設定電腦分析時，即代表您的組織同意。 此同意允許將工作區的 Log Analytics 讀取者角色指派給 MALogAnalyticsReader 應用程式。 電腦分析需要此應用程式角色。

如果此程序在設定期間發生問題，請使用下列程序手動新增此權限：

1. 前往 [Azure 入口網站](https://portal.azure.com)，然後選取 [所有資源]。 選取 [Log Analytics] 類型的工作區。  

2. 在工作區功能表中，選取 [存取控制 (IAM)]，然後選取 [新增]。  

3. 在 [新增權限] 面板中，進行下列設定：  

    - **角色**：**讀取者**  

    - **存取權指派對象為**：**Azure AD 使用者、群組或應用程式**  

    - **選取**：**MALogAnalyticsReader**  

4. 選取 [儲存]。

入口網站會顯示已新增角色指派的通知。

## <a name="data-latency"></a>資料延遲

<!-- 3846531 -->
當您第一次設定電腦分析、註冊新的用戶端或設定新的部署計劃時，Configuration Manager 和電腦分析入口網站中的報告可能不會立即顯示完整資料。 可能需要 2-3 天的時間執行下列步驟：

- 使用中裝置將診斷資料傳送至電腦分析服務
- 服務處理資料
- 服務與您的 Configuration Manager 網站同步

將 Configuration Manager 階層中的裝置集合同步到電腦分析時，最多可能需要一小時的時間，這些集合才會出現在電腦分析入口網站中。 同樣地，當您在電腦分析中建立部署計劃時，最多可能需要一小時的時間，與部署計劃相關聯的新集合才會出現在您的 Configuration Manager 階層中。 主要站台會建立集合，而管理中心網站會與電腦分析同步。 Configuration Manager 最多可能需要 24 小時的時間，評估和更新集合成員資格。 若要加速此程序，請手動更新集合成員資格。<!-- 4984639 -->

> [!Note]
> SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker 元件必須先同步，手動集合更新才會反映變更。 此程序最多可能需要一小時的時間執行。 如需詳細資訊，請參閱 **M365ADeploymentPlanWorker.log**。

在電腦分析入口網站中，有兩種類型的資料：**系統管理員資料**與**診斷資料**：

- **系統管理員資料**是指您對工作區設定所做的任何變更。 例如，當您變更資產的 [升級決策] 或 [重要性] 時，您將變更系統管理員資料。 這些變更通常具有複合效應，因為可能會改變已安裝問題資產的裝置整備狀態。

- **診斷資料**是指從用戶端裝置上傳到 Microsoft 的系統中繼資料。 此資料會驅動電腦分析。 其中包含裝置清查之類的屬性，以及安全性和功能更新狀態。

根據預設，電腦分析入口網站中的所有資料都會每天自動重新整理。 此重新整理包括 2 天前診斷資料的變更，以及對設定所做的任何變更 (系統管理員資料)。 重新整理後的資料應該會在每天上午 08:00 UTC 於您的電腦分析入口網站中顯示。

當您對系統管理員資料進行變更時，可能會在工作區中觸發系統管理員資料的隨選重新整理。 從電腦分析入口網站中的任何頁面，開啟資料流通飛出視窗：

![電腦分析入口網站中資料流通飛出視窗索引標籤的螢幕擷取畫面](media/data-currency-flyout.png)

然後選取 [套用變更]：

![電腦分析入口網站中已展開資料流通飛出視窗的螢幕擷取畫面](media/data-currency-flyout-expand.png)

此程序通常需要 15-60 分鐘的時間。 其花費時間取決於您的工作區大小與需要處理的變更範圍。 當您要求隨選資料重新整理時，不會造成任何診斷資料變更。  如需詳細資訊，請參閱[電腦分析常見問題集](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。

如果您在上述時間範圍內未看到變更更新，請再等候 24 小時進行下一次的每日重新整理。 如果您發現延遲時間較長，請檢查服務健康情況儀表板。 如果服務回報為狀況良好，請連絡 Microsoft 支援服務。<!-- 3896921 -->

> [!IMPORTANT]
> **檢視最近的資料**的 [電腦分析] 選項已被取代。 此動作將在未來的 [電腦分析] 服務版本中移除。 如需詳細資訊，請參閱[已淘汰的功能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。<!--7080949-->  

## <a name="service-notifications"></a>服務通知

<!-- 4982509 -->

電腦分析入口網站會向系統管理員顯示通知橫幅。 這些通知可供 Microsoft 與您溝通重要的事件和問題。 下列各節將詳述您可能會看到的通知。

### <a name="see-whats-new-this-month-in-desktop-analytics"></a>查看這個月的電腦分析新功能

這個資訊通知可讓您注意到服務的變更。 如需詳細資訊，請參閱[電腦分析的新功能](whats-new.md) (`https://aka.ms/danews`)。

### <a name="there-are-new-prerequisites-to-continue-using-desktop-analytics-review-the-new-requirements"></a>沒有新的必要條件。 若要繼續使用電腦分析，請檢閱新的需求

這個資訊通知可讓您注意到必要條件的變更。 例如，新的網際網路端點或軟體更新。 如需詳細資訊，請參閱[必要條件](overview.md#prerequisites) (`https://aka.ms/daprereqs`)。

### <a name="were-investigating-an-issue-that-impacts-desktop-analytics"></a>我們正在調查影響電腦分析的問題

這個警告通知表示 Microsoft 發現到影響電腦分析服務的問題。 問題通常是與快照集的產生有關。 當看到這個通知時，Microsoft 正在調查問題以判斷影響範圍和原因。 您不需要連絡 Microsoft 支援服務。 如需詳細資訊，請參閱[資料流程](privacy.md#data-flow)。

### <a name="were-investigating-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>我們正在調查資料延遲的問題。 如果在過去 24 小時內註冊了新的裝置或變更了任何資產，這些裝置或資產可能不會立即顯示

這個警告通知表示 Microsoft 發現到影響電腦分析服務的問題。 Microsoft 會持續監視服務，以確認所有元件都在正確的時間更新快照集。 在此監視期間，其中一個元件未如預期般完成。 當看到這個通知時，Microsoft 正在調查問題。 您不需要連絡 Microsoft 支援服務。 如需詳細資訊，請參閱[資料流程](privacy.md#data-flow)。

如果最近[註冊裝置](enroll-devices.md)或變更[資產](about-assets.md)，請等候 Microsoft 解決問題。 您不需要重複任何動作。

### <a name="weve-resolved-a-temporary-issue-with-data-latency-daily-refresh-of-portal-data-is-delayed"></a>我們解決了資料延遲的暫時性問題。 入口網站資料的每日重新整理發生延遲

這個通知會告知發生資料延遲的問題。 服務仍持續處理快照集，但資料的重新整理發生延遲。 如需詳細資訊，請參閱[資料延遲](#data-latency)。

### <a name="weve-resolved-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>我們解決了資料延遲的問題。 如果在過去 24 小時內註冊了新的裝置或變更了任何資產，這些裝置或資產可能不會立即顯示

這個通知會告知有關 Microsoft 已解決先前回報的資料延遲問題。 您可能會看到明天的快照集有過時資料。 如果在過去 24 小時內[註冊裝置](enroll-devices.md)或變更了任何裝置設定，入口網站可能不會立即顯示這些內容。 您可繼續使用電腦分析來分類[資產](about-assets.md)，並準備[部署計劃](about-deployment-plans.md)。 這些動作可使用上一個快照集中的資料。

### <a name="weve-resolved-an-issue-with-desktop-analytics-daily-refresh-of-the-portal-data-is-on-track"></a>我們解決了電腦分析的問題。 入口網站資料的每日重新整理已按照進度執行

這個通知會告知有關 Microsoft 已找出在處理期間停止運作的快照集元件。 Microsoft 已重新啟動元件，因此需要一些時間來處理快照集。 Microsoft 會持續監視服務，以確認所有元件都在正確的時間更新快照集。
