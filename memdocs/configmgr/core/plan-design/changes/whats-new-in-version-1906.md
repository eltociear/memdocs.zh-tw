---
title: 1906 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 最新分支 1906 版所引進之變更和新功能的詳細資料。
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 94ad19c2b405af75c7432bb4601098f980c1e821
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702326"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Configuration Manager 最新分支 1906 版的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 最新分支的更新 1906 可以透過主控台內更新的方式取得。 在執行 1802 版或更新版本的站台上套用此更新。 <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> 本文摘要說明 Configuration Manager 1906 版的變更和新功能。  

請一律檢閱適用於安裝此更新的最新檢查清單。 如需詳細資訊，請參閱[安裝更新 1906 的檢查清單](../../servers/manage/checklist-for-installing-update-1906.md)。 更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist)。

若要充分利用 Configuration Manager 的新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

> [!Tip]  
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>需求變更

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>1906 版用戶端需要 SHA-2 程式碼簽署支援

<!--SCCMDocs-pr#3404-->
由於 SHA-1 演算法的缺點以及為了符合業界標準，Microsoft 現在只會使用更安全的 SHA-2 演算法來簽署 Configuration Manager 二進位檔。 下列 Windows OS 版本需要更新 SHA-2 程式碼簽署支援：

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

如需詳細資訊，請參閱[適用於 Windows 用戶端的必要條件](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2)。


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> 站台基礎結構

### <a name="site-server-maintenance-task-improvements"></a>站台伺服器維護工作改進

<!--3555894-->
現在，您可以從站台伺服器詳細資料檢視中的索引標籤上檢視與編輯站台伺服器維護工作。 新的**維護工作**索引標籤可提供您如下資訊：

- 工作是否已啟用
- 工作排程
- 上次啟動時間
- 上次完成時間
- 工作是否已順利完成

![站台伺服器詳細資料檢視中維護工作的新索引標籤](./media/3555894-maintenance-tasks.png)

如需詳細資訊，請參閱[維護工作](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906)。

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Configuration Manager 更新資料庫升級監視

<!--4200581-->
套用 Configuration Manager 更新之後，您現在可以在安裝狀態視窗中看到**升級 ConfigMgr 資料庫**的狀態。

- 如果資料庫升級遭到封鎖，則您將會收到**進行中，需要注意**的警告。
   - cmupdate.log 會從封鎖資料庫升級的 SQL 中記錄程式名稱和 sessionid。
- 當資料庫升級不再受到封鎖時，狀態將會重設為 [進行中]  或 [完成]  。
   - 當資料庫升級受到封鎖時，會每隔 5 分鐘檢查一次以查看是否仍受到封鎖。

   ![安裝期間的資料庫升級監視](./media/4200581-database-upgrade-monitoring.png)

如需詳細資訊，請參閱[安裝主控台內的更新](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install)。

### <a name="management-insights-rule-for-ntlm-fallback"></a>NTLM 後援的管理見解規則

<!--4572953-->
管理見解包含新的規則，可偵測您是否已為站台啟用較不安全的 NTLM 驗證後援方法：**已啟用 NTLM 後援**。

如需詳細資訊，請參閱[管理見解](../../servers/manage/management-insights.md#security)。

### <a name="improvements-to-support-for-sql-always-on"></a>對 SQL Always On 的支援改進

- 從安裝程式新增同步複本<!--3127336-->:您現在可以將新的次要複本節點新增至現有的 SQL Always On 可用性群組。 不要使用手動程序，改用 Configuration Manager 安裝程式進行此變更。 如需詳細資訊，請參閱[設定 SQL Server Always On 可用性群組](../../servers/deploy/configure/configure-aoag.md#bkmk_sync)。

- 多重子網路容錯移轉<!-- SCCMDocs-pr#3734 -->:您現在可以在 SQL Server 中啟用 [MultiSubnetFailover 連接字串關鍵字](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover)。 您必須手動設定站台伺服器。 如需詳細資訊，請參閱[多重子網路容錯移轉](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover)必要條件。

- 對分散式檢視的支援<!-- SCCMDocs-pr#3792 -->:站台資料庫可裝載於 SQL Server Always On 可用性群組上，而您可以啟用資料庫複寫連結來使用[分散式檢視](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep)。

    > [!Note]  
    > 此變更不適用於 SQL Server 叢集。

- 站台復原可以在 SQL Always On 群組上重新建立資料庫。 此程序適用於手動和自動植入。<!-- SCCMDocs-pr#3846 -->

- 新的安裝程式必要條件會檢查：<!-- SCCMDocs-pr#3899 -->  

    - SQL 可用性群組複本必須全部具有相同的植入模式
    - SQL 可用性群組複本必須狀況良好

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> 雲端連結管理

### <a name="azure-active-directory-user-group-discovery"></a>Azure Active Directory 使用者群組探索

<!--3611956-->

您現在可以從 Azure Active Directory (Azure AD) 中探索使用者群組和那些群組的成員。 在站台先前未探索到之 Azure AD 群組中找到的使用者，會新增為 Configuration Manager 中的使用者資源。 當群組是安全性群組時，會建立使用者群組資源記錄。 此功能是[發行前版本功能](../../servers/manage/pre-release-features.md)且需要啟用。

如需詳細資訊，請參閱[設定探索方法](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)。

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>將集合成員資格結果同步至 Azure Active Directory 群組

<!--3607475-->

現在您可以啟用將集合成員資格同步至 Azure Active Directory (Azure AD) 群組。 此同步是發行前版本功能。 若要啟用此功能，請參閱[發行前版本功能](../../servers/manage/pre-release-features.md)。

此同步可讓您根據集合成員資格結果建立 Azure AD 群組成員資格，藉以在雲端中使用現有的內部部署群組規則。 只有含 Azure Active Directory 記錄的裝置會反映於 Azure AD 群組中。 同時支援混合式已加入 Azure AD 和已加入 Azure Active Directory 的裝置。

如需詳細資訊，請參閱[建立集合](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)。


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> 電腦分析

### <a name="readiness-insights-for-desktop-apps"></a>傳統型應用程式的整備見解

<!-- 4021225 -->

您現在可以取得傳統型應用程式的更詳細見解，包括企業營運應用程式。 先前的 App Health Analyzer 工具組現在已與 Configuration Manager 用戶端整合。 此整合簡化了電腦分析入口網站中應用程式整備見解的部署和管理性。

如需詳細資訊，請參閱[電腦分析中的相容性評量](../../../desktop-analytics/compat-assessment.md#advanced-insights)。


### <a name="dalogscollector-tool"></a>DALogsCollector 工具

<!--4622989-->
使用 Configuration Manager 安裝目錄中的 DesktopAnalyticsLogsCollector.ps1 工具，協助進行電腦分析的疑難排解。 它會執行一些基本的疑難排解步驟，並將相關記錄收集到單一工作目錄中。

如需詳細資訊，請參閱[記錄收集器](../../../desktop-analytics/log-collector.md)。


## <a name="real-time-management"></a><a name="bkmk_real"></a> 即時管理

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>在 CMPivot 中新增聯結、額外的運算子和彙總工具

<!--4054074-->

針對 CMPivot，您現在擁有額外的算術運算子、彙總工具，以及新增查詢聯結的能力，例如將登錄和檔案一起使用。

如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot1906)。

### <a name="cmpivot-standalone"></a>CMPivot 獨立

<!--3555890, 4619340, 4692885 -->

您現在可以將 CMPivot 作為獨立應用程式使用。 CMPivot 獨立是一個**發行前版本功能**，僅提供英文版。 在 Configuration Manager 主控台外部執行 CMPivot，以檢視環境中裝置的即時狀態。 這項變更可讓您無需先安裝主控台，即可在裝置上使用 CMPivot。

您可以與其他角色共用 CMPivot 的強大功能，例如技術服務人員或安全性系統管理員，他們的電腦上沒有安裝主控台。 這些其他角色可以使用 CMPivot 查詢 Configuration Manager 以及它們傳統上使用的其他工具。 藉由共用此豐富的管理資料，您可以共同協作以主動解決跨角色的商務問題。

如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) 和[發行前版本功能](../../servers/manage/pre-release-features.md#bkmk_table)。

### <a name="added-permissions-to-the-security-administrator-role"></a>為安全性系統管理員角色新增的權限

<!--4683130-->

下列權限已新增至 Configuration Manager 的內建[**安全性系統管理員**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles)角色：

- 讀取 SMS 指令碼
- 在集合上執行 CMPivot
- 讀取清查報表

如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot_secadmin1906)。


## <a name="content-management"></a><a name="bkmk_content"></a> 內容管理

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>用戶端資料來源儀表板中的傳遞最佳化下載資料

<!--3555759-->
用戶端資料來源儀表板現在包含[傳遞最佳化](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)資料。 此儀表板可協助您了解用戶端會從您環境中的何處取得內容。

如需詳細資訊，請參閱[用戶端資料來源儀表板](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)。

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>使用您的發佈點作為傳遞最佳化的網路內快取伺服器

<!--3555764-->
您現在可以在發佈點上安裝傳遞最佳化的網路內快取 (DOINC) 伺服器。 藉由快取此內部部署內容，您的用戶端就可以受益於傳遞最佳化功能，但您可以協助保護 WAN 連結。

此快取伺服器可視需要以透明方式快取傳遞最佳化所下載的內容。 使用用戶端設定可確保只將此伺服器提供給本機 Configuration Manager 界限群組的成員。

如需詳細資訊，請參閱 [Configuration Manager 中的傳遞最佳化網路內快取](../hierarchy/microsoft-connected-cache.md)。


## <a name="client-management"></a><a name="bkmk_client"></a> 用戶端管理

### <a name="support-for-windows-virtual-desktop"></a>適用於 Windows 虛擬桌面的支援

<!--3556025-->
[Windows 虛擬桌面](https://docs.microsoft.com/azure/virtual-desktop/)是 Microsoft Azure 和 Microsoft 365 的預覽功能。 您現在可以使用 Configuration Manager，來管理這些在 Azure 中執行 Windows 的虛擬裝置。

與終端伺服器類似，這些虛擬裝置允許多個並行的作用中使用者工作階段。 為了協助提升用戶端效能，Configuration Manager 現在可以在允許這些多個使用者工作階段的任何裝置上停用使用者原則。 即使您啟用使用者原則，用戶端也會根據預設在這些裝置 (包括 Windows 虛擬桌面和終端機伺服器) 上將其停用。

如需詳細資訊，請參閱[針對用戶端和裝置支援的 OS 版本](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers)。

### <a name="support-center-onetrace-preview"></a>支援中心 OneTrace (預覽)

<!--3555962-->
OneTrace 是支援中心的新記錄檢視器。 其運作方式與 CMTrace 相似，但改善了下列項目：

- 索引標籤式檢視
- 可停駐視窗
- 改善的搜尋功能
- 在不離開記錄檢視的情況下啟用篩選的功能
- 捲軸提示，可快速識別錯誤叢集
- 快速開啟大型檔案的記錄

![OneTrace 記錄檢視器的螢幕擷取畫面](./media/3555962-onetrace.png)

如需詳細資訊，請參閱[支援中心 OneTrace](../../support/support-center-onetrace.md)。

### <a name="configure-client-cache-minimum-retention-period"></a>設定用戶端快取保留期間下限

<!--4485509-->
您現在可以指定 Configuration Manager 用戶端保留快取內容的時間下限。 此用戶端設定定義 Configuration Manager 代理程式在將內容從快取中移除之前應等候的最小時間量。 在用戶端設定的 [用戶端快取設定]  群組中，進行下列設定：**可移除快取內容之前的持續時間下限 (分鐘)** 。

> [!Note]  
> 在相同的用戶端設定群組中，[Enable Configuration Manager client in full OS to share content] \(在完整作業系統中啟用 Configuration Manager 用戶端以共用內容\)  的現有設定現在已重新命名為 [Enable as peer cache source] \(啟用為對等快取來源\)  。 此設定的行為不會變更。  

如需詳細資訊，請參閱[用戶端快取設定](../../clients/deploy/about-client-settings.md#client-cache-settings)。


## <a name="co-management"></a><a name="bkmk_comgmt"></a> 共同管理

### <a name="improvements-to-co-management-auto-enrollment"></a>共同管理自動註冊的改進

- 新的共同管理裝置現在會根據其 Azure Active Directory (Azure AD)「裝置」  權杖自動註冊到 Microsoft Intune 服務。 不需要等待使用者登入裝置以啟動自動註冊。 此變更有助於減少[註冊狀態](../../../comanage/how-to-monitor.md#co-management-enrollment-status)為*擱置使用者登入*的裝置數目。<!-- 4454491 -->

- 針對已將裝置註冊到共同管理的客戶，新的裝置現在會在符合必要條件之後立即註冊。 例如，一旦裝置加入至 Azure AD 之後，就會安裝 Configuration Manager 用戶端。<!--4321130-->

如需詳細資訊，請參閱[啟用共同管理](../../../comanage/how-to-enable.md)。

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>共同管理工作負載的多個試驗群組

<!--3555750-->
您現在可以為每個共同管理工作負載設定不同的試驗集合。 使用不同的試驗集合，可讓您在轉移工作負載時採取更細微的方法。

- 您現在可以在 [啟用]  索引標籤上指定 [Intune 自動註冊]  集合。
    - [Intune 自動註冊]  集合應包含所有要上架到共同管理的用戶端。 其就本質上而言，是其他暫存集合的超集。

- 在 [暫存]  索引標籤上，您現在可以為每個工作負載選擇個別的集合，而不是將一個試驗集合用於所有工作負載。

    ![共同管理索引標籤可讓您為每個工作負載選擇集合](./media/3555750-co-management-staging-tab.png)

當您第一次啟用共同管理時，也會為您提供這些選項。

如需詳細資訊，請參閱[啟用共同管理](../../../comanage/how-to-enable.md)。

### <a name="co-management-support-for-government-cloud"></a>對政府雲端的共同管理支援

<!--4075452-->
美國政府客戶現在可將共同管理與 Azure 美國政府雲端 (portal.azure.us) 搭配使用。 如需詳細資訊，請參閱[啟用共同管理](../../../comanage/how-to-enable.md)。


## <a name="application-management"></a><a name="bkmk_app"></a> 應用程式管理

### <a name="filter-applications-deployed-to-devices"></a>篩選部署至裝置的應用程式

<!--4451056-->
裝置導向應用程式部署的使用者類別現在會在軟體中心內顯示為篩選。 在應用程式屬性的 [軟體中心]  頁面上，指定該應用程式的**使用者類別**。 接著在軟體中心開啟該應用程式，並查看可用的篩選。

如需詳細資訊，請參閱[手動指定應用程式資訊](../../../apps/deploy-use/create-applications.md#bkmk_manual-app)。

### <a name="application-groups"></a>應用程式群組

<!--3555907-->
建立您可以作為單一部署傳送給使用者或裝置集合的應用程式群組。 您所指定應用程式群組相關中繼資料會顯示為軟體中心內的單一實體。 您可以排序群組中的應用程式，讓用戶端依特定順序來安裝這些應用程式。

此功能是發行前版本。 若要啟用此功能，請參閱[發行前版本功能](../../servers/manage/pre-release-features.md)。

如需詳細資訊，請參閱[建立應用程式群組](../../../apps/deploy-use/create-app-groups.md)。

### <a name="retry-the-install-of-pre-approved-applications"></a>重試安裝預先核准的應用程式

<!--4336307-->
您現在可以重試安裝您先前為使用者或裝置核准的應用程式。 核准選項僅適用於可用的部署。 若使用者解除安裝應用程式，或是初始安裝流程失敗，Configuration Manager 不會重新評估其狀態，也不會重新安裝它。 這項功能可讓支援技術人員為請求協助的使用者快速重試應用程式安裝。

如需詳細資訊，請參閱[核准應用程式](../../../apps/deploy-use/app-approval.md)。

### <a name="install-an-application-for-a-device"></a>為裝置安裝應用程式

<!--4402180-->
從 Configuration Manager 主控台中，您現在可以將應用程式即時安裝到裝置。 這項功能可協助減少為每個應用程式區分集合的需求。

如需詳細資訊，請參閱[為裝置安裝應用程式](../../../apps/deploy-use/install-app-for-device.md)。

### <a name="improvements-to-app-approvals"></a>應用程式核准的改善

<!--4224910-->
此版本包含下列針對應用程式核准的增強功能：

- 如果您在主控台中核准應用程式要求，隨即拒絕該要求，您現在可以再次核准。 在您核准之後，應用程式會重新安裝於用戶端。  

- 在 Configuration Manager 主控台中，[軟體程式庫]  工作區的 [應用程式管理]  下方，已將 [核准要求]  節點重新命名為 [應用程式要求]  。<!-- SCCMDocs-pr#4028 -->

- 有一個新的 WMI 方法：**DeleteInstance** 可移除應用程式核准要求。 此動作不會解除安裝該裝置上的應用程式。 如果未安裝，使用者將無法從軟體中心安裝應用程式。

- 呼叫 **CreateApprovedRequest** API，以在裝置上建立應用程式的預先核准要求。 若要防止在用戶端上自動安裝應用程式，請將 **AutoInstall** 參數設為 `FALSE`。 使用者會看到在軟體中心內看到應用程式，但其並非自動安裝。

如需詳細資訊，請參閱[核准應用程式](../../../apps/deploy-use/app-approval.md)。


## <a name="os-deployment"></a><a name="bkmk_osd"></a> 作業系統部署

### <a name="task-sequence-debugger"></a>工作順序偵錯工具

<!--3612274-->
工作順序偵錯工具是一種新的疑難排解工具。 您可以在偵錯模式中部署工作順序至一個裝置的集合。 它可讓您以受控的形式逐步執行工作順序，協助進行疑難排解和調查。

![工作順序偵錯工具的螢幕擷取畫面](./media/3612274-tsdebug.png)

此功能是發行前版本。 若要啟用此功能，請參閱[發行前版本功能](../../servers/manage/pre-release-features.md)。

如需詳細資訊，請參閱[針對工作順序進行偵錯](../../../osd/deploy-use/debug-task-sequence.md)。

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>在工作順序期間從用戶端快取清除應用程式內容

<!--4485675-->
在 [安裝應用程式]  工作順序步驟中，您現在可以在執行步驟後從用戶端快取中刪除應用程式內容。

如需詳細資訊，請參閱[關於工作順序步驟](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)。

> [!Important]  
> 將目標用戶端更新至最新的版本以支援這項新功能。

### <a name="reclaim-sedo-lock-for-task-sequences"></a>回收工作順序的 SEDO 鎖定

<!--3699337-->
如果 Configuration Manager 主控台停止回應，則您可能遭到鎖定，無法進一步變更工作順序。 現在當您嘗試存取鎖定的工作順序時，您可以立即**捨棄變更**，然後繼續編輯物件。

如需詳細資訊，請參閱[使用工作順序編輯器](../../../osd/understand/task-sequence-editor.md#bkmk_sedo)。

### <a name="pre-cache-driver-packages-and-os-images"></a>預先快取驅動程式套件和 OS 映像

<!--4224642-->
工作順序預先快取現在會包含額外的內容類型。 預先快取內容之前只會套用至 OS 升級套件。 現在，您可以使用預先快取來降低下列項目的頻寬耗用量：

- OS 映像
- 驅動程式套件
- 套件

如需詳細資訊，請參閱[設定預先快取內容](../../../osd/deploy-use/configure-precache-content.md)。

### <a name="improvements-to-os-deployment"></a>改善 OS 部署

此版本包含下列針對 OS 部署的改善：

- 使用下列兩個 PowerShell Cmdlet 來建立和編輯[執行工作順序](../../../osd/understand/task-sequence-steps.md#child-task-sequence)步驟：<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- 您現在可以更輕鬆地在執行工作順序時編輯變數。 當您在 [工作順序精靈] 視窗選取工作順序後，用於編輯工作順序變數的頁面會包含 [編輯]  按鈕。<!-- 4668846 --> 如需詳細資訊，請參閱[如何使用工作順序變數](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz)。

- **停用 BitLocker** 工作順序步驟有一個新的重新啟動計數器。 使用此選項來指定重新啟動次數，以確保 BitLocker 停用。 此變更可協助您簡化工作順序。 您可以使用單一步驟，而不是新增此步驟的多個執行個體。 <!--4512937--> 如需詳細資訊，請參閱[停用 BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker)。

- 將新的工作順序變數 **SMSTSRebootDelayNext** 與現有的 [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) 變數搭配使用。 如果您想讓任何後續的重新啟動搭配與首次重新啟動不同的逾時來發生，請以秒為單位將此新變數設定為不同的值。 <!--4447680--> 如需詳細資訊，請參閱 [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext)。

- 工作順序會設定新的唯讀變數 **_SMSTSLastContentDownloadLocation**。 這個變數包含下載工作順序或嘗試下載內容的最後一個位置。 您現在只要檢查此變數即可，不再需要剖析用戶端記錄。<!-- 2840337 -->

- 當您建立工作順序媒體時，Configuration Manager 不會新增 autorun.inf 檔案。 此檔案通常會遭到反惡意程式碼軟體產品的封鎖。 如果情況需要，您仍然可以包含此檔案。<!-- 4090666 -->


## <a name="software-center"></a><a name="bkmk_userxp"></a> 軟體中心

### <a name="improvements-to-software-center-tab-customizations"></a>軟體中心索引標籤自訂的改善

<!--4063773-->
您現在可以在軟體中心內新增最多五個自訂索引標籤。 您也可以編輯這些索引標籤在軟體中心內出現的順序。

如需詳細資訊，請參閱[軟體中心用戶端設定](../../clients/deploy/about-client-settings.md#software-center)。

### <a name="software-center-infrastructure-improvements"></a>軟體中心基礎結構改善

<!--3555950-->

此版本包括下列軟體中心的基礎結構改進：

- 軟體中心現在會與使用者可使用之目標應用程式的管理點通訊。 它不會再使用應用程式類別目錄。 這項變更可讓您更輕鬆地從站台中移除應用程式類別目錄。

- 先前，軟體中心會從可用伺服器清單中挑選第一個管理點。 從此版本開始，它會使用用戶端所使用的相同管理點。 這項變更允許軟體中心從指派的主要站台，使用與用戶端所使用的相同的管理點。

> [!Important]  
> 這些軟體中心和管理點的反覆式改善是為了淘汰應用程式類別目錄角色。
>
> - 最新分支版本 1806 不支援 Silverlight 使用者體驗。
> - 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。
> - 1910 版會終止對應用程式類別目錄角色的支援。  

如需詳細資訊，請參閱[移除應用程式目錄](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)和[針對軟體中心進行規劃](../../../apps/plan-design/plan-for-software-center.md)。

### <a name="redesigned-notification-for-newly-available-software"></a>針對最新可用軟體重新設計的通知

<!--3555904-->
**新的軟體已可用**通知只會針對指定應用程式和修訂的使用者顯示一次。 使用者將不再於每次登入時都會看到通知。 如果應用程式已變更或重新部署，則使用者只會看到另一個通知。

如需詳細資訊，請參閱[建立和部署應用程式](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience)。

### <a name="more-frequent-countdown-notifications-for-restarts"></a>更頻繁的重新啟動倒數計時通知

<!--3976435-->

終端使用者現在會透過間歇倒數計時通知，更頻繁地收到重新啟動擱置中的提醒。 您可以在 [電腦重新啟動]  頁面上的 [用戶端設定]  中，定義間歇通知的間隔時間。 變更 [指定電腦重新啟動倒數通知的延遲持續時間 (分鐘)]  的值，以設定在最後一個倒數計時通知發生之前，使用者收到關於擱置重新啟動之提醒的頻率。

此外，**向使用者顯示短暫的通知，指出使用者登出或電腦重新啟動之前間隔 (分鐘)** 的最大值，已從 1440 分鐘 (24 小時) 增加到 20160 分鐘 (兩週)。

如需詳細資訊，請參閱[裝置重新啟動通知](../../clients/deploy/device-restart-notifications.md)和[關於用戶端設定](../../clients/deploy/about-client-settings.md#computer-restart)。

### <a name="direct-link-to-custom-tabs-in-software-center"></a>軟體中心內自訂索引標籤的直接連結

<!--4655176-->

您現可為使用者提供軟體中心內[自訂索引標籤](../../clients/deploy/about-client-settings.md#software-center-tab-visibility)的直接連結。

使用下列 URL 格式開啟軟體中心並連至特定索引標籤︰

`softwarecenter:page=CustomTab1`

字串 `CustomTab1` 是順序中的第一個自訂標籤。

舉例來說，在 Windows [執行]  視窗中鍵入此 URL。

您也可以使用此語法在軟體中心內開啟預設索引標籤：

|命令列  |索引標籤  |
|---------|---------|
|`AvailableSoftware`|應用程式|
|`Updates`|更新|
|`OSD`|作業系統|
|`InstallationStatus`|安裝狀態|
|`Compliance`|裝置相容性|
|`Options`|選項|

如需詳細資訊，請參閱[軟體中心索引標籤可見性](../../clients/deploy/about-client-settings.md#software-center-tab-visibility)。

## <a name="software-updates"></a><a name="bkmk_sum"></a> 軟體更新

### <a name="additional-options-for-wsus-maintenance"></a>WSUS 維護的其他選項

<!--4110109-->
您現在具有其他 WSUS 維護工作，可讓 Configuration Manager 執行來維護良好的軟體更新點。 在每次同步處理之後都會進行 WSUS 維護。 除了拒絕 WSUS 中的過期更新以外，Configuration Manager 現在還可以：

- 從 WSUS 資料庫移除已淘汰的更新。
- 將非叢集索引新增至 WSUS 資料庫，以改進 WSUS 清理效能。

如需詳細資訊，請參閱[軟體更新維護](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906)。

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>設定軟體更新的預設執行時間上限

<!--3734426-->

您現在可以指定時間上限，要求軟體更新安裝必須在這段時間內完成。 您可以在軟體更新點的 [執行時間上限]  索引標籤中指定下列項目：

- **Windows 功能更新的執行時間上限 (分鐘)**
- **Office 365 更新與 Windows 非功能更新的執行時間上限 (分鐘數)**

如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime)。

### <a name="configure-dynamic-update-during-feature-updates"></a>在功能更新期間設定動態更新

<!--4062619-->

使用新的用戶端設定，在 Windows 10 功能更新安裝期間設定[動態更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) \(英文\)。 動態更新會引導用戶端從網際網路下載這些更新，以在 Windows 安裝期間安裝語言套件、隨選功能、驅動程式和累積更新。

如需詳細資訊，請參閱[軟體更新用戶端設定](../../clients/deploy/about-client-settings.md#software-updates)和[管理 Windows 即服務](../../../osd/deploy-use/manage-windows-as-a-service.md)。

### <a name="new-windows-10-version-1903-and-later-product-category"></a>新的 Windows 10 1903 版和更新產品類別

<!--4682946-->

**Windows 10 1903 版和更新版本**已作為其專屬產品新增至 Microsoft Update，而不是像舊版一樣作為 **Windows 10** 產品的一部分。 此變更導致您需要執行一些手動步驟以確保您的用戶端可看到這些更新。 我們已協助減少您必須為新產品進行的手動步驟數量。

當您更新至 Configuration Manager 1906 版並選取 **Windows 10** 產品進行同步處理時，下列動作會自動執行：

- 新增 **Windows 10 1903 版和更新版本**產品以進行同步處理。
- 包含 **Windows 10** 產品的自動部署規則將會更新，以包含 **Windows 10 1903 版和更新版本**。
- 服務方案會更新以包含 **Windows 10 1903 版和更新版本**的產品。

如需詳細資訊，請參閱[設定要同步處理的分類和產品](../../../sum/get-started/configure-classifications-and-products.md)、[服務方案](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)及[自動部署規則](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)。

### <a name="drill-through-required-updates"></a>鑽研需要的更新

<!--4224414-->
您現在可以鑽研合規性統計資料，以了解哪些裝置需要特定的軟體更新。 若要檢視裝置清單，您需要檢視更新及裝置所屬集合的權限。 若要向下切入至裝置清單，請在更新的 [摘要]  索引標籤中，選取圓形圖旁的 [需要檢視]  超連結。 按一下超連結，即會帶您前往 [裝置]  下方的臨時節點，以查看需要更新的裝置。

[需要檢視]  超連結可用於下列位置：

   - [軟體程式庫]   > [軟體更新]   > [所有軟體更新] 
   - [軟體程式庫]   > [Windows 10 服務]   > [所有 Windows 10 更新] 
   - [軟體程式庫]   > [Office 365 用戶端管理]   > [Office 365 更新] 

如需詳細資訊，請參閱[監視軟體更新](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates)、[管理 Windows 即服務](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)及[管理 Office 365 ProPlus 更新](../../../sum/deploy-use/manage-office-365-proplus-updates.md#drill-through-required-office-365-updates)。


## <a name="office-management"></a><a name="bkmk_o365"></a> Office 管理

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 ProPlus 升級整備儀表板

<!--4021125-->

為了協助您判斷哪些裝置已準備好升級至 Office 365 ProPlus，需要一個新的整備儀表板。 它包含 Configuration Manager 最新分支 1902 版中發行的 **Office 365 ProPlus 升級整備**圖格。 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [Office 365 用戶端管理]  ，然後選取 [Office 365 ProPlus 升級整備]  節點。

如需儀表板、必要條件和使用此資料的詳細資訊，請參閱[與 Office 365 ProPlus 整備的整合](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash)。


## <a name="protection"></a><a name="bkmk_protect"></a>保護

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Windows Defender 應用程式防護檔案信任準則

<!--3555858-->

新增原則設定，讓使用者信任在 Windows Defender 應用程式防護 (WDAG) 中正常開啟的檔案。 成功完成時，檔案會在主機裝置上 (而非 WDAG 中) 開啟。

如需詳細資訊，請參閱[建立及部署 Windows Defender 應用程式防護原則](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM)。


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 主控台

### <a name="role-based-access-for-folders"></a>適用於資料夾的角色型存取

<!--3600867-->

您現在可以在資料夾上設定安全性範圍。 如果您在資料夾中擁有物件的存取權，但沒有資料夾的存取權，您將無法看到物件。 同樣地，如果您有資料夾存取權，但沒有其中物件的存取權，您將無法看到該物件。 以滑鼠右鍵按一下資料夾、選擇 [設定安全性範圍]  ，然後選擇您想要套用的安全性範圍。

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md#tips)和[設定以角色為基礎的系統管理](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder)。

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>將 SMBIOS GUID 資料行新增至裝置和裝置集合節點

<!--4526580-->
在 [裝置]  和 [裝置集合]  節點中，您現在可以新增 [SMBIOS GUID]  的新資料行。 這個值與系統資源類別的 **BIOS GUID** 屬性相同。 這是裝置硬體的唯一識別碼。

### <a name="administration-service-support-for-security-nodes"></a>對安全性節點的系統管理服務支援

<!--4223683-->
您現在可以啟用 Configuration Manager 主控台的部分節點，來使用系統管理服務。 這項變更使主控台得以透過 HTTPS 和簡訊提供者通訊，而非透過 Wi-Fi。

如需詳細資訊，請參閱[系統管理服務](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)。

> [!Note]
> 從 1906 版開始，站台屬性上的 [用戶端電腦通訊]  索引標籤現在稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>裝置節點中的 [集合] 索引標籤

<!--4616810-->
在 [資產與合規性]  工作區中，前往 [裝置]  節點，然後選取裝置。 在詳細資料窗格中，切換到新的 [集合]  索引標籤。此索引標籤清單會列出包含此裝置的集合。

> [!Note]  
> - 此索引標籤目前無法從 [裝置集合]  節點下的裝置子節點使用。 例如，當您在集合上選取選項來 [顯示成員]  時。
> - 針對某些使用者，此索引標籤可能不會如預期般填入。 若要查看裝置所屬集合的完整清單，您必須擁有 [系統高權限管理員]  安全性角色。 這是已知的問題。 <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>應用程式節點中的工作順序索引標籤

<!--4616810-->
在 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，前往 [應用程式]  節點，然後選取應用程式。 在詳細資料窗格中，切換到新的 [工作順序]  索引標籤。此索引標籤會列出參考此應用程式的工作順序。

### <a name="show-collection-name-for-scripts"></a>顯示指令碼的集合名稱

<!--4616810-->
在 [監視]  工作區中，選取 [指令碼狀態]  節點。 它現在除了識別碼之外，還會列出 [集合名稱]  。

### <a name="real-time-actions-from-device-lists"></a>從裝置清單進行即時動作

<!--4616810-->
有數種方式可以顯示 [資產與合規性]  工作區中 [裝置]  節點下的裝置清單。

- 在 [資產與合規性]  工作區中，選取 [裝置集合]  節點。 選取裝置集合，然後選擇動作來 [顯示成員]  。 此動作會開啟 [裝置]  節點的子節點，並具有該集合的裝置清單。  

  - 當您選取集合的子節點時，您現在可以從功能區的 [集合] 群組啟動  。  

- 在 [監視]  工作區中，選取 [部署]  節點。 選取任一部署，然後在功能區中選擇 [檢視狀態]  動作。 在部署狀態窗格中，按兩下總資產來鑽研裝置清單。  

  - 當您選取此清單中的裝置時，您現在可以從功能區的 [裝置] 群組啟動 [CMPivot]  及 [執行指令碼]  。  

### <a name="order-by-program-name-in-task-sequence"></a>在工作順序中依照程式名稱排序

<!--4616810-->
在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  節點。 編輯工作順序，然後選取或新增[安裝套件](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步驟。 若套件擁有超過一個程式，下拉式清單現在會根據程式名稱的字母順序進行排序。

### <a name="correct-names-for-client-operations"></a>用戶端作業的正確名稱

<!--4616810-->
在 [監視]  工作區中，選取 [用戶端作業]  。 [切換至下一個軟體更新點]  的選項現在已正確命名。


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> 已淘汰的功能和作業系統

在[已移除與已淘汰的項目](deprecated/removed-and-deprecated.md)中實作支援變更之前，請先了解這些變更。

1906 版已捨棄對下列功能的支援：  

- 您無法安裝新的應用程式目錄角色。 已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 如需詳細資訊，請參閱[針對軟體中心進行規劃](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)。

1906 版已淘汰對下列產品的支援：  

- Windows CE 7.0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>其他更新

從此版本開始，下列功能已不再是發行前版本：

- [SMS 提供者管理服務](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Windows Defender 應用程式控制管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 1906 版中變更的摘要](https://support.microsoft.com/help/4514258) \(機器翻譯\)。

如需適用於 Configuration Manager 之 Windows PowerShell Cmdlet 變更的詳細資訊，請參閱 [PowerShell 1906 版版本資訊](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps) \(部分機器翻譯\)。

自 2019 年 10 月 1 日起，就可在主控台中使用更新彙總套件 (4517869)：[適用於 Configuration Manager 目前分支 1906 版的更新彙總套件](https://support.microsoft.com/help/4517869) \(機器翻譯\)。

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>後續步驟

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
從 2019 年 8 月 16 日起，1906 版可供所有客戶安裝。

當您準備安裝此版本時，請參閱[安裝 Configuration Manager 的更新](../../servers/manage/updates.md)和[安裝更新 1906 的檢查清單](../../servers/manage/checklist-for-installing-update-1906.md)。

> [!TIP]  
> 若要安裝新的站台，請使用 Configuration Manager 的基準版本。  
>
> 深入了解：
>
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)  

如需已知的重大問題，請參閱[版本資訊](../../servers/deploy/install/release-notes.md)。

更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist)。
