---
title: Configuration Manager 主控台
titleSuffix: Configuration Manager
description: 了解如何巡覽 Configuration Manager 主控台。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6bcd0bc06721fbd6ea3ce1226867db522bb2560
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700336"
---
# <a name="how-to-use-the-configuration-manager-console"></a>如何使用 Configuration Manager 主控台

適用於：  Configuration Manager (最新分支)

系統管理員會使用 Configuration Manager 主控台來管理 Configuration Manager 環境。 本文涵蓋巡覽主控台的基本概念。  

## <a name="open-the-console"></a><a name="bkmk_open"></a> 開啟主控台

Configuration Manager 主控台一律會安裝在所有站台伺服器上。 您也可以將其安裝在其他電腦上。 如需詳細資訊，請參閱[安裝 Configuration Manager 主控台](../deploy/install/install-consoles.md)。

在 Windows 10 電腦上啟動主控台的最簡單方法就是按 [開始]  ，然後開始鍵入 `Configuration Manager console`。 您不一定需要鍵入完整字串，Windows 就能找到最符合的結果。

如果您瀏覽 [開始] 功能表，請在 [Microsoft 端點管理員]  群組中尋找 **Configuration Manager 主控台**圖示。

![Microsoft 端點管理員 [開始] 功能表圖示](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> 1910 版的 [開始] 功能表路徑已變更。 在 1906 版和更早版本中，資料夾名稱是 **System Center**。 在將 Configuration Manager 更新為 1910 版或更新版本時，請務必更新您維護的所有內部文件，以納入這些新的位置。

## <a name="connect-to-a-site-server"></a>連線至站台伺服器

主控台會連線至管理中心網站伺服器或主要站台伺服器。 不過，您無法將 Configuration Manager 主控台連線至次要站台。 在安裝期間，您已指定主控台所連線之站台伺服器的完整網域名稱 (FQDN)。

若要連線至不同的站台伺服器，請使用下列步驟：

1. 選取[功能區](#ribbon)頂端的箭號，然後選擇 [連線至新站台]  。  

    ![將主控台連線至新站台](media/connect-to-a-new-site.png)  

2. 輸入站台伺服器的 FQDN。 如果您先前已連線至站台伺服器，則請從下拉式清單中選取伺服器。  

    ![在 [站台連線] 視窗中，輸入站台伺服器的 FQDN](media/site-server-fqdn.png)  

3. 選取 [連線]  。  

從 1810 版開始，您可以指定系統管理員存取 Configuration Manager 站台的最低驗證層級。 這項功能會強制系統管理員以必要層級登入 Windows。 如需詳細資訊，請參閱[規劃 SMS 提供者](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)。 <!--1357013-->  

## <a name="navigation"></a>導覽

根據您的已指派安全性角色，可能無法顯示主控台的某些區域。 如需角色的詳細資訊，請參閱[以角色為基礎的系統管理基本概念](../../understand/fundamentals-of-role-based-administration.md)。

### <a name="workspaces"></a>工作區

Configuration Manager 主控台有四個**工作區**：  

- **資產和合規性**  

- **軟體程式庫**  

- **監視**  

- **系統管理**  

![包含操作功能表的 Configuration Manager 工作區](media/configuration-manager-workspaces.png)  

選取向下鍵，然後選擇 [瀏覽窗格選項]  ，以重新排序工作區按鈕。 選取要 [上移]  或 [下移]  的項目。 選取 [重設]  還原預設按鈕順序。  

![重新排序工作區的 [瀏覽窗格選項] 視窗](media/navigation-pane-options.png)  

選取 [顯示較少按鈕]  ，以將工作區按鈕最小化。 會先將清單中的最後一個工作區最小化。 選取最小化按鈕，然後選擇 [顯示更多按鈕]  將按鈕還原回其原始大小。

![Configuration Manager 主控台中最小化的工作區](media/workspace-buttons.png)  

### <a name="nodes"></a>節點

工作區是**節點**的集合。 其中一個節點範例是 [軟體程式庫]  工作區中的 [軟體更新群組]  節點。

當您在節點中時，可以選取箭號以將瀏覽窗格最小化。  

![範例節點和醒目提示最小化箭號](media/software-update-groups-node.png)  

將您的瀏覽窗格最小化時，使用**瀏覽列**來移動主控台。  

![Configuration Manager 最小化瀏覽窗格](media/minimized-navigation-pane.png)  

在主控台中，節點有時會組織成資料夾。 當您選取資料夾時，通常會顯示**瀏覽索引**或**儀表板**。  

![Configuration Manager 軟體更新瀏覽索引](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>功能區

功能區位於 Configuration Manager 主控台頂端。 功能區可以有多個索引標籤，而且可以使用右側的箭號最小化。 根據節點，功能區上的按鈕會變更。 操作功能表也會提供功能區中的大部分按鈕。  

![範例功能區，醒目提示多個索引標籤和最小化箭號](media/ribbon.png)

### <a name="details-pane"></a>[詳細資料] 窗格

您可以檢閱 [詳細資料] 窗格，以取得項目的其他資訊。 [詳細資料] 窗格可以有一或多個索引標籤。 這些索引標籤會根據節點而不同。  

![Configuration Manager 範例詳細資料窗格](media/details-pane.png)

### <a name="columns"></a>資料行

您可以新增、移除、重新排列以及調整資料行大小。 這些動作可讓您顯示偏好的資料。 可用的資料行會根據節點而不同。 若要在檢視中新增或移除資料行，請以滑鼠右鍵按一下現有資料行標題並選取項目。 拖曳您要放置資料行的資料行標題，以重新排序資料行。  

![Configuration Manager 新增資料行](media/add-columns.png)  

在資料行操作功能表底端，您可以依資料行排序或群組。 此外，您可以選取資料行的標頭，以依資料行排序。  

![Configuration Manager 依資料行群組](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> 回收編輯物件的鎖定

<!--4786915-->

如果 Configuration Manager 主控台停止回應，您可能遭到鎖定，而必須等候 30 分鐘鎖定逾時，才能做進一步變更。 此鎖定是 Configuration Manager SEDO (分散式物件序列化編輯) 系統的一部分。 如需詳細資訊，請參閱 [Configuration Manager SEDO](../../../develop/core/understand/sedo.md)。

從[最新分支 1906 版](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)開始，您可以清除工作順序上的鎖定。 從 1910 版開始，您現在可以在 Configuration Manager 主控台中清除任何物件上的鎖定。

此動作僅適用於擁有鎖定的使用者帳戶，且必須在站台授與鎖定的相同來源裝置上進行。 當您嘗試存取鎖定的物件時，您現在可以**捨棄變更**，並繼續編輯物件。 反正這些變更在鎖定逾時後也會遺失。

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> 檢視最近連線的主控台

<!--3699367-->
從 1902 版開始，您可以檢視 Configuration Manager 主控台的最近連線。 此檢視包含使用中的連線，以及最近進行的連線。 您一律會在清單中看到目前的主控台連線，且您只會看到 Configuration Manager 主控台的連線。 您不會看到對 SMS 提供者的 PowerShell 或其他 SDK 型連線。 此站台會從清單中移除舊於 30 天的執行個體。

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> 檢視連線主控台的必要條件

- 您的帳戶需要 **SMS_Site** 物件的**讀取**權限。

- 設定系統管理服務 REST API。 如需詳細資訊，請參閱[什麼是系統管理服務？](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>檢視連線的主控台

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。  

2. 展開 [安全性]  然後選取 [主控台連線]  節點。  

3. 透過以下內容檢視最近的連線：  

    - 使用者名稱
    - 電腦名稱
    - 連線的站台碼
    - 主控台版本
    - 上次連線的時間：使用者最後開啟  主控台的時間
    - 從 1910 版開始，[上次主控台活動訊號]  欄已取代 [上次連線時間]  欄。 <!--4923997-->
       - 在前景中開啟的主控台每 10 分鐘會傳送一次活動訊號。

![檢視 Configuration Manager 主控台連線](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> 從主控台連線開始 Microsoft Teams 聊天
<!--4923997-->
*(於 1910 版引進)*

從 1910 版開始，您可以使用 Microsoft Teams 從 [主控台連線]  節點傳送訊息給其他 Configuration Manager 系統管理員。 當您選擇與系統管理員 [開始 Microsoft Teams 聊天]  時，系統即會啟動 Microsoft Teams，並針對該使用者開啟聊天。

### <a name="prerequisites"></a>先決條件

- 若要開始與系統管理員的聊天，您想要進行聊天的帳戶必須已透過 [Azure AD 或 AD 使用者探索](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)進行探索。
- Microsoft Teams 已安裝在執行主控台的裝置上。
注意
- 所有[檢視連線主控台的必要條件](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>開始 Microsoft Teams 聊天

1. 移至 [系統管理]   > [安全性]   > [主控台連線]  。
1. 以滑鼠右鍵按一下使用者的主控台連線，然後選取 [開始 Microsoft Teams 聊天]  。
    - 如果找不到所選系統管理員的使用者主體名稱，則 [開始 Microsoft Teams 聊天]  會呈現灰色。
    - 如果 Microsoft Teams 未安裝在您執行主控台的裝置上，便會顯示包括下載連結的錯誤訊息。
    - 如果 Microsoft Teams 已安裝在您執行主控台的裝置上，它將會開啟與該使用者的聊天。

### <a name="known-issues"></a>已知問題

如果下列登錄機碼不存在，便不會顯示通知您 Microsoft Teams 尚未安裝的錯誤訊息：

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

此問題的因應措施是手動建立該登錄機碼。

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a> Configuration Manager 主控台通知

<!--3556016, fka 1318035-->
從 Configuration Manager 1902 版開始，主控台會通知您下列事件：

- Configuration Manager 本身有可用的更新
- 當環境中發生生命週期和維護事件

這個通知列位於功能區下方的主控台視窗頂端。 它會取代先前提供 Configuration Manager 更新的體驗。 這些主控台內通知仍會顯示重大資訊，但不會影響您在主控台中的工作。 您無法關閉重大通知。 主控台會在標題列的新通知區域中顯示所有通知。

![主控台中的通知列和旗標](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>將站台設定為顯示非重大通知

您可以將每個站台設定為在站台的屬性中顯示非重大通知。

1. 在 [系統管理]  工作區中，展開 [站台設定]  ，然後選取 [站台]  節點。
1. 選取您想要設定非重大通知的站台。
1. 在功能區中，選取 [內容]  。
1. 在 [警示]  索引標籤上，選取 [允許主控台通知非重大的站台健全狀況變更]  選項。
   - 如果您啟用此設定，則所有主控台使用者都會看到重大、警告和資訊通知。 預設會啟用此設定。  
   - 如果您停用此設定，主控台使用者就只會看到重大通知。  

大部分的主控台通知都是按照每個工作階段區分。 當使用者啟動主控台時，主控台就會評估查詢。 若要查看通知中的變更，請重新啟動主控台。 如果使用者關閉非重大通知，則在主控台重新啟動時仍會再次通知 (若仍適用的話)。

下列通知會每隔五分鐘重新評估一次：

- 站台處於維護模式  
- 站台處於修復模式  
- 站台處於升級模式  

通知會遵循以角色為基礎的系統管理權限。 舉例來說，如果使用者不具查看 Configuration Manager 更新的權限，他們就看不到這些通知。

有些通知會有相關動作。 舉例來說，如果主控台版本與站台版本不符，請選取 [安裝新的主控台版本]  。 這個動作會啟動主控台安裝程式。

下列通知最適用於 Technical Preview 分支：  

- 評估版將於 30 天內到期 (警告)：目前日期仍在評估版的 30 天到期日內  
- 評估版已過期 (重大)：目前日期已逾評估版的到期日  
- 主控台版本不符 (重大)：主控台版本與站台的版本不符  
- 站台升級可供使用 (警告)：有新的更新套件可供使用  

如需詳細資訊和疑難排解協助，請參閱主控台電腦上的 **SmsAdminUI.log** 檔案。 根據預設，這個記錄檔位於下列路徑：`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`。


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> 主控台內的文件儀表板

<!--3556019 FKA 1357546-->
從 Configuration Manager 1902 版開始，新的 [社群]  工作區中會有一個 [文件]  節點。 此節點包含 Configuration Manager 文件和支援文章的最新資訊。 它包含下列各節：  

### <a name="product-documentation-library"></a>產品文件庫

- **建議**：手動策劃的重要文章清單。
- **趨勢**：過去一個月最受歡迎的文章。
- **最近更新**：在上個月中修訂的文章。

### <a name="support-articles"></a>支援文章

- **針對文章進行疑難排解**：引導式逐步解說可協助針對 Configuration Manager 元件和功能進行疑難排解。
- **新增與更新的支援文章**：過去兩個月中新增或更新的支援文章。

### <a name="troubleshooting-connection-errors"></a>對連線錯誤進行疑難排解
[文件]  節點沒有明確的 Proxy 設定。 它會使用 [網際網路選項]  控制台小程式中任何 OS 定義的 Proxy。 若要在連線錯誤之後重試，請重新整理 [文件]**Documentation** 節點。


## <a name="command-line-options"></a>命令列選項

Configuration Manager 主控台有下列命令列選項：

|選項|說明|  
|------------|-----------------|  
|`/sms:debugview=1`|所有指定檢視的 ResultViews 中都包含 DebugView。 DebugView 會顯示未經處理的屬性 (名稱和值)。|  
|`/sms:NamespaceView=1`|會在主控台中顯示命名空間檢視。|  
|`/sms:ResetSettings`|主控台會忽略使用者保存的連線和檢視狀態。 不會重設視窗大小。|  
|`/sms:IgnoreExtensions`|停用任何 Configuration Manager 延伸模組。|  
|`/sms:NoRestore`|主控台會忽略先前保存的節點瀏覽。|  


## <a name="tips"></a>提示

### <a name="general"></a>一般

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> 針對主控台搜尋所做的改進
<!--4640570-->
*(於 1910 版引進)*

- 您可以使用 [驅動程式套件]  與 [查詢]  節點的 [所有子資料夾]  搜尋選項。<!--2841181,5424892--> 從 2002 版開始，另請從 [設定項目]  和 [設定基準]  節點使用此選項。<!--5891241-->

- 當搜尋傳回超過 1,000 個結果時，請選取通知列上的 [確定]  按鈕來檢視更多結果。<!--4640570-->

    ![太多搜尋結果的通知列螢幕擷取畫面](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > 搜尋結果的預設限制是 1,000 個。 您可以變更此預設值。 在 Configuration Manager 主控台中，移至功能區的 [搜尋]  索引標籤。 在 [選項]  群組中，選取 [搜尋設定]  。 變更 [搜尋結果]  值。 大量搜尋結果可能需要很長的時間才能顯示。
    >
    > 根據預設，上限是 100,000 個。 若要變更此限制，請設定下列登錄機碼中的 DWORD 值 **QueryResultCountMaximum**：
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > 主控台中的設定對應到相同機碼中的 **QueryResultCountLimit** 值。 系統管理員可以針對裝置的所有使用者，在 HKLM 登錄區中設定這些值。 HKCU 值會覆寫 HKLM 設定。

#### <a name="role-based-administration-for-folders"></a>資料夾的角色型系統管理
<!--3600867-->
*(於 1906 版推出)*

您可以在資料夾上設定安全性範圍。 如果您在資料夾中擁有物件的存取權，但沒有資料夾的存取權，您將無法看到物件。 同樣地，如果您有資料夾存取權，但沒有其中物件的存取權，您將無法看到該物件。 以滑鼠右鍵按一下資料夾、選擇 [設定安全性範圍]  ，然後選擇您想要套用的安全性範圍。

#### <a name="views-sort-by-integer-values"></a>依據整數值排序的檢視

(於 1902 版引進) 

我們已改進各種檢視排序資料的方式。 例如，在 [監視]  工作區的 [部署]  節點中，下列資料行會根據數字來排序，而不是字串值：  

- 錯誤數目
- 進行中的數目
- 其他數目
- 成功數目
- 未知的數目  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>移動大量結果的警告

(於 1902 版引進) 

當您在主控台中選取的節點會傳回超過 1,000 個結果時，Configuration Manager 會顯示下列警告：

> Configuration Manager 傳回大量結果。 您可以使用搜尋來縮小結果的範圍。 或者，請按一下這裡，檢視最多 100000 筆結果。

此警告和搜尋欄位之間現在有額外空白。 這樣移動有助於防止不小心選取警告而顯示更多結果。

#### <a name="send-feedback"></a>傳送意見反應

*(於 1806 版推出)*
<!--1357542-->

從主控台提交產品意見反應。  

- **傳送笑臉**：針對您喜歡的功能傳送意見反應  

- **傳送苦臉**：針對您不喜歡的功能傳送意見反應  

- **傳送建議**：將您帶往 UserVoice，以分享您的想法  

如需詳細資訊，請參閱[產品意見反應](../../understand/find-help.md#BKMK_1806Feedback)。


### <a name="assets-and-compliance-workspace"></a>[資產與相容性] 工作區

#### <a name="real-time-actions-from-device-lists"></a>從裝置清單進行即時動作
<!--4616810-->
*(於 1906 版推出)*

有數種方式可以顯示 [資產與合規性]  工作區中 [裝置]  節點下的裝置清單。

- 在 [資產與合規性]  工作區中，選取 [裝置集合]  節點。 選取裝置集合，然後選擇動作來 [顯示成員]  。 此動作會開啟 [裝置]  節點的子節點，並具有該集合的裝置清單。  

  - 當您選取集合的子節點時，您現在可以從功能區的 [集合] 群組啟動  。  

- 在 [監視]  工作區中，選取 [部署]  節點。 選取任一部署，然後在功能區中選擇 [檢視狀態]  動作。 在部署狀態窗格中，按兩下總資產來鑽研裝置清單。  

  - 當您選取此清單中的裝置時，您現在可以從功能區的 [裝置] 群組啟動 [CMPivot]  及 [執行指令碼]  。  


#### <a name="collections-tab-in-devices-node"></a>裝置節點中的 [集合] 索引標籤
<!--4616810-->
*(於 1906 版推出)*

在 [資產與合規性]  工作區中，前往 [裝置]  節點，然後選取裝置。 在詳細資料窗格中，切換到新的 [集合]  索引標籤。此索引標籤清單會列出包含此裝置的集合。 

> [!Note]  
> - 此索引標籤目前無法從 [裝置集合]  節點下的裝置子節點使用。 例如，當您在集合上選取選項來 [顯示成員]  時。
> - 針對某些使用者，此索引標籤可能不會如預期般填入。 若要查看裝置所屬集合的完整清單，您必須擁有 [系統高權限管理員]  安全性角色。 這是已知的問題。 <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>將 SMBIOS GUID 資料行新增至裝置和裝置集合節點

*(於 1906 版推出)*

<!--4526580-->
在 [裝置]  和 [裝置集合]  節點中，您現在可以新增 [SMBIOS GUID]  的資料行。 這個值與系統資源類別的 **BIOS GUID** 屬性相同。 這是裝置硬體的唯一識別碼。

#### <a name="search-device-views-using-mac-address"></a>使用 MAC 位址搜尋裝置檢視

<!--3600878-->
(於 1902 版引進) 

您可以在 Configuration Manager 主控台的裝置檢視中搜尋 MAC 位址。 在針對 PXE 型部署進行疑難排解時，這個屬性對於 OS 部署管理員來說非常有用。 當您檢視裝置的清單時，請將 [MAC 位址]  資料行新增至檢視。 使用 [搜尋] 欄位即可新增 [MAC 位址]  搜尋準則。

#### <a name="view-users-for-a-device"></a>檢視裝置的使用者

從 1806 版開始，可以在 [裝置]  節點中使用下列資料行：  

- **主要使用者** <!--1357280-->  

- **目前登入的使用者** <!--1358202-->  

    > [!NOTE]  
    > 檢視目前登入的使用者需要[使用者探索](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud)和[使用者裝置親和性](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

如需如何顯示非預設資料行的詳細資訊，請參閱[資料行](#columns)。

#### <a name="improvement-to-device-search-performance"></a>裝置搜尋效能的改進

<!-- 3614690 -->
從 1806 版開始，當系統在裝置集合中搜尋時，它不會對所有物件屬性搜尋關鍵字。 當您要搜尋的項目不明確時，它會在下列四個屬性之間搜尋：

- Name
- 主要使用者
- 目前登入的使用者
- 上次登入使用者名稱

此行為大幅改進依名稱搜尋所花費的時間，尤其是在大型環境中。 根據特定準則的自訂搜尋不受此變更影響。


### <a name="software-library-workspace"></a>軟體程式庫工作區

#### <a name="order-by-program-name-in-task-sequence"></a>在工作順序中依照程式名稱排序
<!--4616810-->
*(於 1906 版推出)*

在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  節點。 編輯工作順序，然後選取或新增[安裝套件](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步驟。 若套件擁有超過一個程式，下拉式清單現在會根據程式名稱的字母順序進行排序。

#### <a name="task-sequences-tab-in-applications-node"></a>應用程式節點中的工作順序索引標籤
<!--4616810-->
*(於 1906 版推出)*

在 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，前往 [應用程式]  節點，然後選取應用程式。 在詳細資料窗格中，切換到新的 [工作順序]  索引標籤。此索引標籤會列出參考此應用程式的工作順序。

#### <a name="drill-through-required-updates"></a>鑽研需要的更新
<!--4224414-->
*(於 1906 版推出)*

1. 移至 Configuration Manager 主控台的下列其中一個位置：

   - [軟體程式庫]   > [軟體更新]   > [所有軟體更新] 
   - [軟體程式庫]   > [Windows 10 服務]   > [所有 Windows 10 更新] 
   - [軟體程式庫]   > [Office 365 用戶端管理]   > [Office 365 更新] 

1. 選取至少一部裝置所需的任何更新。
1. 查看 [摘要]  索引標籤，然後尋找 [統計資料]  下方的圓形圖。
1. 選取圓形圖旁的 [需要檢視]  超連結，以向下切入至裝置清單。
1. 此動作會帶您前往 [裝置]  下方的臨時節點，以查看需要更新的裝置。 您也可以對節點採取動作，例如從清單建立新的集合。


#### <a name="maximize-the-browse-registry-window"></a>最大化瀏覽登錄視窗

<!--3594151 includes all MMS 1902 console changes-->
*(已於 1902 版引進)*

1. 在 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後選取 [應用程式]  節點。
1. 使用偵測方法選取有部署類型的應用程式。 例如，Windows Installer 偵測方法。
1. 在詳細資料窗格中，切換至 [部署類型]  索引標籤。
1. 開啟部署類型的屬性，然後切換到 [偵測方法]  索引標籤。選取 [新增子句]  。
1. 將 [設定類型]  變更為 [登錄]  ，然選取 [瀏覽]  以開啟 [瀏覽登錄]  視窗。 您現在可以將此視窗最大化。  

#### <a name="edit-a-task-sequence-by-default"></a>預設為編輯工作順序

(於 1902 版引進) 

在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  節點。 [編輯]  現已為開啟工作順序時的預設動作。 先前的預設動作是 [屬性]  。  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>從應用程式部署移至集合

(於 1902 版引進) 

1. 在 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後選取 [應用程式]  節點。
1. 選取應用程式。 在詳細資料窗格中，切換至 [部署]  索引標籤。
1. 選取部署，然後選擇功能區中 [部署] 索引標籤上新的 [集合]  選項。此動作會將檢視切換到該部署的目標集合。
   - 在此檢視中，此動作也可從部署上的滑鼠右鍵操作功能表中取得。


### <a name="monitoring-workspace"></a>監視工作區

#### <a name="correct-names-for-client-operations"></a>用戶端作業的正確名稱
<!--4616810-->
*(於 1906 版推出)*

在 [監視]  工作區中，選取 [用戶端作業]  。 [切換至下一個軟體更新點]  的選項現在已正確命名。

#### <a name="show-collection-name-for-scripts"></a>顯示指令碼的集合名稱
<!--4616810-->
*(於 1906 版推出)*

在 [監視]  工作區中，選取 [指令碼狀態]  節點。 它現在除了識別碼之外，還會列出 [集合名稱]  。

#### <a name="remove-content-from-monitoring-status"></a>從監視狀態移除內容

(於 1902 版引進) 

1. 在 [監視]  工作區中，展開 [發佈狀態]  ，然後選取 [內容狀態]  。
1. 在清單中選取項目，然後選擇功能區中的 [檢視狀態]  選項。
1. 在 [資產詳細資料] 窗格中，以滑鼠右鍵按一下發佈點，然後選取新的 [移除]  選項。 此動作會將選取的發佈點從此內容中移除。

#### <a name="copy-details-in-monitoring-views"></a>從監視檢視複製詳細資料

*(於 1806 版推出)*
<!--1357856-->
從下列監視節點的 [資產詳細資料]  窗格複製資訊：  

- **內容發佈狀態**  

- **部署狀態**  

![部署狀態檢視，複製資產詳細資料](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>系統管理工作區

<!--4223683-->
從 1906 版開始，您可以在 [安全性]  節點底下啟用某些節點，以使用系統管理服務。 這項變更使主控台得以透過 HTTPS 和簡訊提供者通訊，而非透過 Wi-Fi。 如需詳細資訊，請參閱[設定系統管理服務](../../../develop/adminservice/set-up.md#bkmk_console)。

## <a name="next-steps"></a>後續步驟

[協助工具功能](../../understand/accessibility-features.md)

[工作順序編輯器](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
