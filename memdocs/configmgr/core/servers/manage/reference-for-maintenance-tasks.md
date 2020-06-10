---
title: 維護工作的參考
titleSuffix: Configuration Manager
description: 每個 Configuration Manager 站台維護工作的詳細資料
ms.date: 06/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e989de5acab778374c233862d0ab4d7077899d28
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428600"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Configuration Manager 中的維護工作參考

適用於：Configuration Manager (最新分支)

此文章列出每個 Configuration Manager 站台維護工作的詳細資料。 每個項目都會指定可使用工作的站台類型，以及是否預設為啟用。

如需詳細資訊，請參閱[設定維護工作](maintenance-tasks.md#set-up-maintenance-tasks)。  

## <a name="tasks"></a>工作

### <a name="backup-site-server"></a>備份網站伺服器

使用此工作建立重要資訊的備份，以還原站台及 Configuration Manager 資料庫。 如需詳細資訊，請參閱[備份 Configuration Manager 站台](backup-and-recovery.md)。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|未啟用|
|次要網站|無法使用|

### <a name="check-application-title-with-inventory-information"></a>使用清查資訊檢查應用程式標題

使用此工作維護在軟體清查和 Asset Intelligence 類別目錄之間軟體標題的一致性。 如需詳細資訊，請參閱 [Asset Intelligence 簡介](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|主要網站|無法使用|
|次要網站|無法使用|

### <a name="clear-undiscovered-clients"></a>清除未探索的用戶端

> [!Tip]
> 您也可以在主控台中看到名為 [清除安裝旗標] 的這個工作。

若要針對在**用戶端重新探索**期間並未提交「活動訊號探索」記錄的用戶端移除已安裝的旗標，請使用此工作。 已安裝旗標可避免在已具備作用中 Configuration Manager 用戶端的電腦上進行自動用戶端推入安裝。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|未啟用|
|次要網站|無法使用|

### <a name="delete-aged-application-request-data"></a>刪除過時應用程式要求資料

使用此工作從資料庫刪除過時應用程式要求。 如需詳細資訊，請參閱[建立和部署應用程式](../../../apps/get-started/create-and-deploy-an-application.md)。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-application-revisions"></a>刪除過時應用程式修訂

使用此工作刪除不再參照的應用程式版本。 如需詳細資訊，請參閱[如何修改和取代應用程式](../../../apps/deploy-use/revise-and-supersede-applications.md)。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-client-download-history"></a>刪除過時用戶端下載歷程記錄

若要刪除有關用戶端所使用下載來源的歷史資料，請使用此工作。 站台會使用下載來源資訊來填入[用戶端資料來源儀表板](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-client-operations"></a>刪除過時用戶端操作

若要從站台資料庫刪除所有過時的用戶端作業資料，請使用此工作。 例如，此資料包含下列作業：

- 過時或過期的用戶端通知，例如電腦或使用者原則的下載要求
- Endpoint Protection，例如系統管理使用者針對用戶端所提出，執行掃描或下載更新定義的要求
- 執行指令碼狀態結果

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-client-presence-history"></a>刪除過時用戶端顯示狀態歷程記錄
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
若要刪除由用戶端通知所記錄，與用戶端線上狀態相關的歷程資訊，請使用此工作。 它會刪除狀態比指定時間還舊的用戶端資訊。 如需詳細資訊，請參閱[如何監視用戶端](../../clients/manage/monitor-clients.md)。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>刪除過時雲端管理閘道流量資料

若要從站台資料庫中刪除與通過[雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)的流量相關的所有過時資料，請使用此工作。 此資料包括：

- 要求數目
- 要求位元組總計
- 回應位元組總計
- 失敗要求數目
- 並存要求的數目上限

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-cmpivot-results"></a>刪除過時 CMPivot 結果

若要從站台資料庫刪除 CMPivot 查詢中的用戶端過時資訊，請使用此工作。 如需詳細資訊，請參閱[即時資料的 CMPivot](cmpivot.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-collected-files"></a>刪除過時收集檔案

若要從資料庫刪除有關收集檔案的過時資訊，請使用此工作。 此工作也會從選定網站的網站伺服器資料夾結構中刪除收集檔案。 根據預設，會將 5 個收集檔案的最新複本儲存在 **Inboxes\sinv.box\FileCol** 目錄的網站伺服器上。 如需詳細資訊，請參閱[軟體清查簡介](../../clients/manage/inventory/introduction-to-software-inventory.md)。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-computer-association-data"></a>刪除過時電腦關聯資料

若要從資料庫刪除過時作業系統部署電腦關聯資料，請使用此工作。 在工作順序期間還原使用者狀態時，會使用此資訊。 如需詳細資訊，請參閱[管理使用者狀態](../../../osd/get-started/manage-user-state.md)。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-console-connection-data"></a>刪除過時主控台連線資料

此工作會從站台資料庫刪除與站台的主控台連線相關的資料。<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-delete-detection-data"></a>刪除過時刪除偵測資料

若要從以「擷取檢視」建立的資料庫刪除過時資料，請使用此工作。 它會刪除外部系統用來從資料庫擷取資料的舊資料變更資訊。<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-device-wipe-record"></a>刪除過時裝置抹除記錄

若要從資料庫刪除與行動裝置抹除動作有關的過時資料，請使用此工作。 如需詳細資訊，請參閱[透過遠端抹除、鎖定或密碼重設來保護資料](../../../mdm/deploy-use/wipe-lock-reset-devices.md)。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-discovery-data"></a>刪除過時探索資料

使用此工作從資料庫刪除過時探索資料。 此資料可以包含下列記錄：

- 活動訊號探索
- 網路探索
- Active Directory 探索方法：系統、使用者和群組

此工作也會移除標示為已解除任務的過時裝置。 在某個站台執行這項工作時，會刪除與該站台關聯的資料，並且這些變更會複寫到其他站台。 如需詳細資訊，請參閱[執行探索](../deploy/configure/run-discovery.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-distribution-point-usage-stats"></a>刪除過時發佈點使用量統計資料

請使用此工作從資料庫刪除儲存時間超過指定時間的發佈點過時資料。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-enrolled-devices"></a>刪除過時已註冊裝置

若要從站台資料庫刪除有一段指定時間尚未對站台回報任何資訊之行動裝置有關的過時資料，請使用此工作。

此工作適用於使用 Configuration Manager [內部部署 MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) 註冊的裝置。 如需有關這些裝置的詳細資訊，請參閱[用戶端和裝置的支援作業系統](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|未啟用|
|次要網站|無法使用|

### <a name="delete-aged-ep-health-status-history-data"></a>刪除過時 EP 健全狀況狀態歷程記錄資料

若要從資料庫刪除 Endpoint Protection (EP) 的過時狀態資訊，請使用此工作。 如需詳細資訊，請參閱[如何監視 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-exchange-partnership"></a>刪除過時 Exchange 合作關係

> [!Tip]
> > 您也可以在主控台中看到此工作，名稱為 [刪除受 Exchange Server 連接器管理的過時裝置]。

使用此工作，刪除有關由 Exchange Server 連接器管理之行動裝置的過時資料。 站台會根據 Exchange Server 連接器內容之 [探索] 索引標籤上的 [略過未使用達指定天數以上的行動裝置] 設定刪除此資料。 如需詳細資訊，請參閱[使用 Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-inventory-history"></a>刪除過時清查歷程記錄

若要從資料庫刪除儲存時間超過指定時間的清查資料，請使用此工作。 如需詳細資訊，請參閱[如何使用 [資源總管] 檢視硬體清查](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-log-data"></a>刪除過時記錄檔資料

若要從資料庫刪除用來進行疑難排解的過時記錄檔資料，請使用此工作。 此一資料與 Configuration Manager 元件運作無關。  

> [!IMPORTANT]  
> 根據預設，此一工作會在每個網站上每日執行。 在管理中心網站與主要站台上，這個工作會刪除超過 30 天的資料。 在次要站台上使用 SQL Server Express 時，請確保這個工作每日執行，並刪除 7 天未使用的資料。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|**次要站台**|已啟用|

### <a name="delete-aged-metering-data"></a>刪除過時計量資料

若要從資料庫刪除儲存時間超過指定時間的軟體計量過時資料，請使用此工作。 如需詳細資訊，請參閱[軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-metering-summary-data"></a>刪除過時計量摘要資料

若要從資料庫刪除儲存時間超過指定時間的軟體計量過時摘要資料，請使用此工作。 如需詳細資訊，請參閱[軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-notification-server-history"></a>刪除過時通知伺服器歷程記錄

此工作會刪除過時用戶端顯示狀態歷程記錄。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-notification-task-history"></a>刪除過時通知工作歷程記錄

若要從站台資料庫刪除有關用戶端通知工作的資訊，請使用此工作。 此工作適用於在指定時間內未更新的資料。 如需詳細資訊，請參閱[用戶端通知](../../clients/manage/client-notification.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-passcode-records"></a>刪除過時的密碼記錄

若要刪除 Windows Phone 裝置的過時「密碼重設」資料，請在階層的頂層站台使用此工作。 「密碼重設」資料會經過加密，但不會包含裝置的 PIN 碼。 預設會啟用此工作，並刪除超過 1 天的資料。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-replication-data"></a>刪除過時複寫資料

使用此工作從資料庫刪除與 Configuration Manager 站台間資料庫複寫相關的過時資料。 變更這項維護工作的設定時，設定會套用到階層中的每個可應用網站。 如需詳細資訊，請參閱[監視資料庫複寫](monitor-replication.md)。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|**次要站台**|已啟用|

### <a name="delete-aged-replication-summary-data"></a>刪除過時複寫摘要資料

若要從站台資料庫刪除在指定時間內未更新的過時複寫摘要資料，請使用此工作。 如需詳細資訊，請參閱[監視資料庫複寫](monitor-replication.md)。  

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|**次要站台**|已啟用|

### <a name="delete-aged-status-messages"></a>刪除過時狀態訊息

若要從資料庫刪除過時狀態訊息資料 (如狀態篩選規則中所設定)，請使用此工作。 如需詳細資訊，請參閱[監視 Configuration Manager 的狀態系統](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-threat-data"></a>刪除過時威脅資料

若要從資料庫刪除儲存時間超過指定時間的 Endpoint Protection 威脅資料，請使用此工作。 如需詳細資訊，請參閱 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-unknown-computers"></a>刪除過時未知電腦

若要從站台資料庫中，刪除與在指定時間內未更新的未知電腦相關的資訊，請使用此工作。 如需詳細資訊，請參閱[準備未知電腦部署](../../../osd/get-started/prepare-for-unknown-computer-deployments.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-aged-user-device-affinity-data"></a>刪除過時使用者裝置親和性資料

使用此工作從資料庫刪除過時使用者裝置親和性資料。 如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-duplicate-system-discovery-data"></a>刪除重複的系統探索資料

若要從站台資料庫刪除由系統探索所產生的任何重複記錄，請使用此工作。<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**管理中心網站**|已啟用|
|主要網站|無法使用|
|次要網站|無法使用|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>刪除過期的 MDM 大量註冊封裝記錄

若要在註冊憑證過期後，刪除舊的「大量註冊」憑證及對應的設定檔，請使用此工作。 如需詳細資訊，請參閱[建立憑證設定檔](../../../protect/deploy-use/create-certificate-profiles.md)。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-inactive-client-discovery-data"></a>刪除非使用中用戶端探索資料

若要從資料庫刪除非使用中用戶端的探索資料，請使用此工作。 當用戶端被標示為已過時，站台會將用戶端標示為非使用中 (依針對用戶端狀態進行的設定)。

此工作僅會在 Configuration Manager 用戶端資源上運作。 這與刪除任何過時探索資料記錄的**刪除過時探索資料**工作不同。 在某個網站上執行此工作時，會從階層內所有網站的資料庫內移除資料。 如需詳細資訊，請參閱[如何設定用戶端狀態](../../clients/deploy/configure-client-status.md)。

> [!IMPORTANT]  
> 啟用此工作時，請設定此工作以大於 [活動訊號探索] 排程的間隔執行。 此設定會讓使用中用戶端傳送活動訊號探索記錄，將其用戶端記錄標記為使用中，以便此工作不會將它們刪除。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|未啟用|
|次要網站|無法使用|

### <a name="delete-obsolete-alerts"></a>刪除已過時警示

若要從資料庫刪除儲存時間超過指定時間的逾時警示，請使用此工作。 如需詳細資訊，請參閱[使用警示和狀態系統](use-alerts-and-the-status-system.md)。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-obsolete-client-discovery-data"></a>刪除過時用戶端探索資料

使用此工作從資料庫刪除過時用戶端記錄。 標示為過時的記錄通常會由相同用戶端較新的記錄取代。 新的記錄就會成為用戶端目前的記錄。 如需有關探索的詳細資訊，請參閱[執行探索](../deploy/configure/run-discovery.md)。

> [!IMPORTANT]  
> 啟用此工作時，請將此工作的間隔執行設定為超過活動訊號探索的排程。 此設定會讓用戶端傳送正確設定過時狀態的活動訊號探索記錄。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|未啟用|
|次要網站|無法使用|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>刪除過時樹系探索站台和子網路

若要刪除 Active Directory 網站、子網和網域的相關資料，請使用此工作。 它會移除過去 30 天內 Active Directory 樹系探索方法未發現的該站台資料。 此工作會移除探索資料，但不會影響您從此探索資料建立的界限。 如需詳細資訊，請參閱[執行探索](../deploy/configure/run-discovery.md)。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="delete-orphaned-client-deployment-state-records"></a>刪除孤立的用戶端部署狀態記錄

若要定期清除包含用戶端部署狀態資訊的資料表，請使用此工作。 此工作可清理有關已淘汰或已退役裝置的記錄。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="evaluate-collection-members"></a>評估集合成員

您可將「集合成員評估」設定為站台元件。 如需詳細資訊，請參閱[站台元件](../deploy/configure/site-components.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="monitor-keys"></a>監視索引鍵

若要監視 Configuration Manager 資料庫主索引鍵的完整性，請使用此工作。 主索引鍵是可唯一識別一個資料列的一個資料行或多個資料行組合。 索引鍵會區分資料列與 Microsoft SQL Server 資料庫資料表中的任何其他資料列。

|||
|---------|---------|
|**管理中心網站**|已啟用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="rebuild-indexes"></a>重建索引

若要重建 Configuration Manager 資料庫索引，請使用此工作。 索引是建立在資料庫資料表上以加速資料擷取的資料庫結構。 例如，搜尋索引欄通常會比搜尋未索引的欄還快。

為了改善效能，系統會經常更新 Configuration Manager 資料庫索引，以與儲存在資料庫內經常變更的資料同步。 這項工作：

- 在資料庫資料行上建立至少 50% 唯一的索引
- 在資料行上卸除小於 50% 唯一的索引
- 重建所有符合資料唯一性準則的現有索引

|||
|---------|---------|
|**管理中心網站**|未啟用|
|**主要站台**|未啟用|
|**次要站台**|未啟用|

### <a name="summarize-file-usage-metering-data"></a>摘述檔案使用量計量資料

此工作會將多個記錄的軟體計量檔案使用狀況摘述成一個一般記錄。 資料摘要可以壓縮儲存在 Configuration Manager 資料庫中的資料量。

若要摘要說明軟體計量資料並節省資料庫中的磁碟空間，請搭配 [摘述軟體計量每月使用資料] 工作使用此工作。 如需詳細資訊，請參閱[軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="summarize-installed-software-data"></a>摘述已安裝的軟體資料

使用此工作可透過摘述從硬體清查所收集之資產智慧軟體資訊的資料，將多筆記錄合併成一筆一般記錄。 資料摘要可以壓縮儲存在 Configuration Manager 資料庫中的資料量。 如需詳細資訊，請參閱[設定 Asset Intelligence 維護工作](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="summarize-monthly-usage-metering-data"></a>摘述每月使用量計量資料

此工作會將多個記錄的軟體計量每月使用狀況摘述成一個一般記錄。 資料摘要可以壓縮儲存在 Configuration Manager 資料庫中的資料量。

若要摘要說明軟體計量資料並節省資料庫中的空間，請搭配 [摘述軟體計量檔案使用資料] 工作使用此工作。 如需詳細資訊，請參閱[軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="update-application-available-targeting"></a>更新應用程式可用目標

若要讓 Configuration Manager 重新計算原則和應用程式部署與集合中資源的對應，請使用此工作。 當您將原則或應用程式部署到集合時，Configuration Manager 會在您部署的物件與集合成員之間建立初始對應。

這些對應會儲存在資料表中以供快速參考。 當集合成員資格變更時，站台會更新這些預存對應以反映那些變更。 但這些對應有可能會變得不同步。例如，如果站台無法正確地處理通知檔案，該項變更可能就不會反映在對對應所做的變更中。 此工作會根據目前的集合成員資格來重新整理該對應。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|

### <a name="update-application-catalog-tables"></a>更新應用程式類別目錄資料表

使用此工作以最新應用程式資訊同步處理應用程式類別目錄網站資料庫快取。 變更此維護工作的設定時，它會套用到階層中的所有主要站台。  

|||
|---------|---------|
|管理中心網站|無法使用|
|**主要站台**|已啟用|
|次要網站|無法使用|


## <a name="see-also"></a>請參閱

[維護工作](maintenance-tasks.md)
