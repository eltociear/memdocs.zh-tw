---
title: Management Insights
titleSuffix: Configuration Manager
description: 了解可在 Configuration Manager 主控台中使用的管理見解功能。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694446"
---
# <a name="management-insights-in-configuration-manager"></a>Configuration Manager 中的管理見解

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的管理見解提供您環境目前狀態的相關資訊。 此資訊是以站台資料庫的資料分析為基礎。 深入解析可協助您進一步了解您的環境，並據以採取行動。 <!--1353967-->

## <a name="review-management-insights"></a>檢閱管理見解

若要檢視規則，您的帳戶需要**站台**物件的**讀取**權限。

1. 開啟 Configuration Manager 主控台。  

2. 前往 [管理]  工作區，展開 [管理見解]  ，然後選取 [所有見解]  。  

    > [!Note]  
    > 當選取 [管理見解]  節點時，會顯示[管理見解儀表板](#bkmk_insights)。  

3. 開啟您想要檢閱的管理見解群組名稱。 選取功能區中的 [顯示見解]  。  

下列四個索引標籤可供檢閱：

- **所有規則**：提供可供管理深入解析群組選擇的完整規則清單。  

- **完成**：列出無須採取任何動作的規則。  

- **進行中**：顯示的規則只完成其中一些必要條件，但非全部都已完成。  

- **需要的動作**：列出需要採取動作的規則。 選取 [更多詳細資料]  ，擷取需要採取動作的特定項目。  

[必要條件]  窗格會列出執行此規則所需的必要項目。

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>所有規則和雲端服務群組的必要條件

![管理見解 - 所有規則和雲端服務群組的必要條件](./media/Management-insights-all-cloud-rules.png)

選取規則並選取 [更多詳細資料]  以查看規則詳細資料。

## <a name="operations"></a>作業

Management Insights 規則每週都會重新評估其適用性。 若要視需要重新評估規則，請以滑鼠右鍵按一下規則，並選取 [重新評估]  。

管理見解規則記錄檔是站台伺服器上的 **SMS_DataEngine.log**。

<!--1357930-->
某些規則可讓您採取動作。 選取規則，選取 [更多詳細資料]  ，然後在可用時選取 [採取動作]  。

根據規則，此動作會有下列其中一種行為：  

- 自動瀏覽至主控台中，您可以採取進一步動作的節點。 例如，如果管理見解建議變更用戶端設定，則採取動作會瀏覽至 [用戶端設定] 節點。 然後，請修改預設或自訂的用戶端設定物件，以採取進一步的動作。  

- 瀏覽至根據查詢而篩選的檢視。 例如，根據空集合規則而採取動作，只會顯示集合清單中的這些集合。 然後採取進一步的動作，例如刪除集合或修改其成員資格規則。  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a> 管理見解儀表板

<!--1357979-->

[管理見解]  節點包含圖形化儀表板。 此儀表板會顯示規則狀態的概觀，讓您更輕鬆地顯示進度。

使用儀表板頂端的下列篩選來調整檢視：

- 顯示已完成的工作
- 選用
- 建議
- 重大

儀表板包含以下磚：  

- **管理見解索引**：追蹤管理見解規則的整體進度。 索引是加權平均值。 重大規則最為值得。 此索引提供選擇性規則的最小加權。  

- **管理見解群組**：顯示每個群組中接受篩選的規則百分比。 選取群組，以向下鑽研到此群組中的特定規則。  

- **管理見解優先順序**：依優先順序顯示接受篩選的規則百分比。  

- **所有見解**：包含優先順序和狀態的見解表。 使用資料表頂端的 [篩選]  欄位，比對任何可用資料行中的字串。 儀表板會以下列順序來排序資料表：

  - 狀態：所需的動作、已完成、未知  
  - 優先順序：重大、建議、選用  
  - 最後一項變更：較舊的日期在最上層  

![管理見解儀表板的螢幕擷取畫面](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>群組和規則

規則會分成下列管理見解群組：

- [應用程式](#applications)
- [雲端服務](#cloud-services)
- [集合](#collections)
- [Configuration Manager 評定](#configuration-manager-assessment)
- [主動式維護](#proactive-maintenance)
- [Security](#security)
- [簡化的管理](#simplified-management)
- [軟體中心](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>應用程式

應用程式管理的見解。

- **沒有部署的應用程式**：列出環境中沒有作用中部署的應用程式。 此規則可協助您尋找並刪除未使用的應用程式，以簡化主控台中顯示的應用程式清單。 如需詳細資訊，請參閱[部署應用程式](../../../apps/deploy-use/deploy-applications.md)。  

### <a name="cloud-services"></a>雲端服務

協助您與多個雲端服務整合，這可啟用裝置的新式管理。

- **評估共同管理整備程度**：協助您了解需要哪些步驟來啟用共同管理。 此規則有必要條件。 如需詳細資訊，請參閱[共同管理概觀](../../../comanage/overview.md)。  

- **未上傳至 Azure AD 的裝置**：從 2002 版開始，此規則會列出因站台未針對 HTTPS 正確設定，而未上傳至 Azure AD 的裝置。<!--6268489--> 設定[增強式 HTTP](../../plan-design/hierarchy/enhanced-http.md)，或為 HTTPS 至少啟用一個管理點。 如果已針對 HTTPS 通訊設定站台，則不會顯示此規則。

- **將 Azure 服務設定為與 Configuration Manager 一起使用**：此規則可協助您將 Configuration Manager 上架到 Azure AD，這可讓用戶端使用 Azure AD 向站台進行驗證。 如需詳細資訊，請參閱[設定 Azure 服務](../deploy/configure/azure-services-wizard.md)。  

- **啟用裝置為已加入混合式 Azure Active Directory** ：已加入 Azure AD 的裝置可讓使用者使用其網域認證登入，同時確保裝置符合組織的安全性和合規性標準。 如需詳細資訊，請參閱 [Azure AD 混合式身分識別設計考量](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)。  

- **沒有正確 HTTPS 設定的站台**：從 2002 版開始，此規則會列出階層中未針對 HTTPS 正確設定的站台。 此設定可防止站台[將集合成員資格結果同步至 Azure Active Directory (Azure AD) 群組](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)。 這可能會導致 Azure AD 同步不會上傳所有裝置。 這些用戶端的管理可能無法正常運作。<!--6268489--> 設定[增強式 HTTP](../../plan-design/hierarchy/enhanced-http.md)，或為 HTTPS 至少啟用一個管理點。 如果已針對 HTTPS 通訊設定站台，則不會顯示此規則。

- **將用戶端更新為最新的 Windows 10 版本**：Windows 10 1709 版或更新版本可改善使用者運算體驗並將其現代化。 如需詳細資訊，請參閱[採用 Windows 即服務的重要文章](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)。  

### <a name="collections"></a>集合

可透過清除和重新設定集合協助簡化管理的見解。

- **空集合**：列出環境中沒有成員的集合。 如需詳細資訊，請參閱[如何管理集合](../../clients/manage/collections/manage-collections.md)。  

從 1902 版開始，有新的規則，並提供有關管理集合的建議。<!--3555752--> 使用這些見解可簡化管理並改善效能：

- **不含查詢規則和直接成員的集合**：若要簡化階層中的集合清單，請刪除這些集合。  

- **具有相同重新評估開始時間的集合**：這些集合具有與其他集合相同的重新評估時間。 請修改重新評估時間，使它們不會發生衝突。  

- **查詢時間超過兩秒的集合**：檢閱此集合的查詢規則。 請考慮修改或刪除集合。

- 下列規則包含可能導致站台上產生不必要負載的設定。 請檢閱這些集合，然後加以刪除或停用規則評估：  

  - **不含查詢規則且已啟用累加式更新的集合**  

  - **不含查詢規則且已針對排程或增量評估啟用的集合**  

  - **不含查詢規則並為所選完整評估進行排程的集合**  

### <a name="configuration-manager-assessment"></a>Configuration Manager 評定

<!--3607758-->

從 2002 版開始，此群組會由 Microsoft 頂級支援欄位工程提供。 這些規則是 Microsoft 頂級支援在[服務中樞](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments)提供的許多其他檢查範例。

- **Active Directory 安全性群組探索設定的執行頻率過高**：您通常不需要將 Active Directory 安全性群組探索設定為比每三小時一次還高的頻率。 對 Active Directory、網路及 Configuration Manager 而言，較頻繁的設定可能會對效能產生負面影響。 請啟用累加式同步處理，而不是使用完整同步處理排程。 如需詳細資訊，請參閱 [Active Directory 群組探索](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)。

- **Active Directory 系統探索設定的執行頻率過高**：您通常不需要將 Active Directory 系統探索設定為比每三小時一次還高的頻率。 對 Active Directory、網路及 Configuration Manager 而言，較頻繁的設定可能會對效能產生負面影響。 請啟用累加式同步處理，而不是使用完整同步處理排程。 如需詳細資訊，請參閱 [Active Directory 系統探索](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)。

- **Active Directory 使用者探索設定的執行頻率過高**：您通常不需要將 Active Directory 使用者探索設定為比每三小時一次還高的頻率。 對 Active Directory、網路及 Configuration Manager 而言，較頻繁的設定可能會對效能產生負面影響。 請啟用累加式同步處理，而不是使用完整同步處理排程。 如需詳細資訊，請參閱 [Active Directory 使用者探索](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。

- **集合僅限於所有系統或所有使用者**：請檢閱使用 [所有系統]  或 [所有使用者]  集合作為限制集合的任何集合。 Configuration Manager 會使用來自 Active Directory 探索方法的資料，來更新這些預設集合的成員資格。 此資料可能不是 Configuration Manager 用戶端的有效資訊。

- **已停用活動訊號探索**：活動訊號探索需要您在裝置上安裝 Configuration Manager 用戶端。 這是用戶端起始的唯一探索方法。 所有其他方法都發生在站台伺服器上。 活動訊號探索是保持最新用戶端活動狀態的必要條件。 其可確保站台不會意外讓站台資料庫的資源記錄過期。 如需詳細資訊，請參閱[活動訊號探索](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。

- **為累加式更新啟用長時間執行的集合查詢**：上次累加式重新整理時間大於 30 秒的集合會使用站台伺服器和資料庫資源，這可能會影響整體 Configuration Manager 效能。 如需詳細資訊，請參閱[集合的最佳做法](../../clients/manage/collections/best-practices-for-collections.md)。

- **減少發佈點上的應用程式和套件數目**：Microsoft 在發佈點上正式支援最多共 10,000 個套件和應用程式的組合。 超過這個總計數目可能會導致操作問題。 如需詳細資訊，請參閱[大小和縮放比例 - 發佈點](../../plan-design/configs/size-and-scale-numbers.md#distribution-point)。

- **次要站台安裝問題**：部分次要站台的安裝狀態為 [擱置]  或 [失敗]  。 這些狀態表示您已開始安裝，但未成功完成。 在次要站台安裝完成之前，用戶端可能無法與主要站台正確通訊。 請檢查 [監視]  工作區，然後重試安裝。 如需詳細資訊，請參閱[重試失敗更新的安裝](install-in-console-updates.md#bkmk_retry)。

- **將所有站台更新為相同版本**：在階層中使用相同版本的 Configuration Manager。 此設定會確定所有站台都提供相同的功能。 相同階層如有不同版本的站台會導致互通性問題。 更新版本的 Configuration Manager 會包含新功能並解決已知問題。 如需詳細資訊，請參閱[不同版本之間的互通性](../../plan-design/hierarchy/interoperability-between-different-versions.md)。

如需這些規則的詳細資訊，請參閱 [Configuration Manager 管理見解的補救步驟](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr)。

> [!TIP]
> 如果您已經是 Microsoft 統一支援或 Microsoft 頂級支援的客戶，請登入[服務中樞](https://serviceshub.microsoft.com/assessments/)以進行其他隨選評量。
>
> 如需 Microsoft 服務的詳細資訊，請參閱[支援解決方案](https://www.microsoft.com/enterprise/services/support)。

### <a name="proactive-maintenance"></a>主動式維護

<!--1352184-->
此群組中的規則強調透過維護 Configuration Manager 物件可避免的潛在設定問題。

- **未獲指派站台系統的界限群組**：界限群組若無指派的站台系統，則僅適用於站台指派。 如需詳細資訊，請參閱[設定界限群組](../deploy/configure/boundary-groups.md)。  

- **不含成員的界限群組**：如果界限群組沒有任何成員，則不適用站台指派或內容查閱。 如需詳細資訊，請參閱[設定界限群組](../deploy/configure/boundary-groups.md)。  

- **未提供內容給用戶端的發佈點**：在過去 30 天未提供內容給用戶端的發佈點。 此資料會以來自用戶端下載歷程記錄的報告為基礎。 如需詳細資訊，請參閱[安裝及設定發佈點](../deploy/configure/install-and-configure-distribution-points.md)。  

- **啟用 WSUS 清除**：驗證您已啟用對軟體更新點元件屬性執行 WSUS 清除的選項。 此選項有助於改善 WSUS 效能。 如需詳細資訊，請參閱[軟體更新維護](../../../sum/deploy-use/software-updates-maintenance.md)。  

- **未使用的開機映像**：未用於供 PXE 開機或工作順序參考的開機映像。 如需詳細資訊，請參閱[管理開機映像](../../../osd/get-started/manage-boot-images.md)。  

- **未使用的設定項目**：不是設定基準一部分且已過時逾 30 天的設定項目。 如需詳細資訊，請參閱[建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)。  

- **將對等快取來源升級為 Configuration Manager 用戶端的最新版本**：識別作為對等快取來源但尚未從 1806 之前的用戶端版本升級的用戶端。 1806 之前的用戶端無法作為執行 1806 或更新版本之用戶端的對等快取來源。 請選取 [採取動作]  以開啟顯示用戶端清單的裝置檢視。<!--1358008-->  

### <a name="security"></a>安全性

改善基礎結構與裝置之安全性的見解。

- **已啟用 NTLM 後援**：<!--4572953--> 從 1906 版開始，此規則會偵測您是否已為站台啟用較不安全的 NTLM 驗證後援方法。 使用用戶端推送方法安裝 Configuration Manager 用戶端時，站台可以要求 Kerberos 相互驗證。 此增強功能有助於保護伺服器和用戶端之間的通訊。 如需詳細資訊，請參閱[如何使用用戶端推入來安裝用戶端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。

- **不受支援的反惡意程式碼用戶端版本**：超過 10% 的用戶端正在執行不受支援的 System Center Endpoint Protection 版本。 如需詳細資訊，請參閱 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

### <a name="simplified-management"></a>簡化的管理

可協助您簡化環境日常管理的見解。

- **將網站連線到 Microsoft Cloud 以進行 Configuration Manager 更新**：此規則可確保您的 Configuration Manager 服務連接點在過去七天內已連線到 Microsoft Cloud。 此連線的目的是下載定期更新的內容。 檢閱 DMPDownloader.log 與 hman.log。 如需詳細資訊，請參閱[網際網路存取需求](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates)。

- **非 CB 用戶端版本**：列出其版本不是最新分支 (CB) 組建的所有用戶端。 如需詳細資訊，請參閱[升級用戶端](../../clients/manage/upgrade/upgrade-clients.md)。  

- **將用戶端更新為支援的 Windows 10 版本**：從 1902 版開始，此規則會報告執行不再受支援之 Windows 10 版本的用戶端。 它也包含服務即將結束 (三個月) 的 Windows 10 版本。<!--3897268-->  

### <a name="software-center"></a>軟體中心

管理軟體中心的見解。

- **將使用者導向到軟體中心，而不是應用程式類別目錄**：檢查使用者在過去 14 天是否已安裝或要求應用程式類別目錄中的應用程式。 應用程式類別目錄的主要功能現在已包含在「軟體中心」內。 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[已淘汰的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features)。  

- **使用新版的軟體中心**：不再支援舊版軟體中心。 啟用 [電腦代理程式]  群組中的用戶端設定 [使用新的軟體中心]  ，藉以設定用戶端使用新的軟體中心。 如需詳細資訊，請參閱[關於用戶端設定](../../clients/deploy/about-client-settings.md#use-new-software-center)。  

### <a name="software-updates"></a>軟體更新

- **用戶端設定未設為允許用戶端下載差異內容**：在環境中同步的部分軟體更新包含差異內容。 請啟用用戶端設定 [允許用戶端在可取得差異內容時予以下載]  。 若您未啟用此設定，當您部署這些更新時，用戶端會下載超出本身需求的非必要內容。 如需詳細資訊，請參閱[用戶端設定 - 軟體更新](../../clients/deploy/about-client-settings.md#software-updates)。

- **啟用軟體更新產品類別「Windows 10 1903 版本與更新版本」** ：Windows 10 1903 版和更新版本中，有新的軟體更新產品類別。 如果您同步處理 Windows 10 更新以及 Windows 10 1903 版本或更高用戶端，請選取軟體更新點元件屬性的 [Windows 10 1903 版本或更高]  產品類別。 如需詳細資訊，請參閱[設定要同步處理的分類和產品](../../../sum/get-started/configure-classifications-and-products.md)。

### <a name="windows-10"></a>Windows 10

Windows 10 部署及維護的相關見解。 只有在一半以上的用戶端在執行 Windows 7、Windows 8 或 Windows 8.1 時，才可使用 Windows 10 管理見解群組。

- **設定 Windows 診斷資料及商業識別碼金鑰**：若要使用電腦分析中的資料，請以商業識別碼金鑰來設定裝置並啟用診斷資料的集合。 將 Windows 10 裝置設定為 [增強式 (有限)]  層級或更高層級。 如需詳細資訊，請參閱[啟用電腦分析的資料共用](../../../desktop-analytics/enable-data-sharing.md)。

#### <a name="windows-10-management-insights-rules"></a>Windows 10 管理見解規則

![管理見解 - 適用於 Windows 10 的規則](./media/Windows-10-insights-group.png)
