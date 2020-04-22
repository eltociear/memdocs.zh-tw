---
title: Asset Intelligence 簡介
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的 Asset Intelligence 來清查和管理整個企業的軟體授權使用情形。
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25deb098f6e1f4ce275a0c0a0817249cd36558f7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695086"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Configuration Manager 中的 Asset Intelligence 簡介

適用於：  Configuration Manager (最新分支)

使用 Asset Intelligence 類別目錄來清查和管理整個企業的軟體授權使用情形。 Asset Intelligence 能加入硬體清查類別來提升 Configuration Manager 所收集之資訊的範圍。 此資訊包括用於您環境中的硬體和軟體標題。 超過 60 個報告都會以簡單易用的格式呈現此資訊。 這些報告有許多會連結到更加特定的報告。 針對一般資訊進行查詢，並向下切入到更加詳細的資訊。 

將自訂資訊新增至 Asset Intelligence 類別目錄。 例如自訂軟體類別、軟體系列、軟體標籤，以及硬體需求。 若要以可用的最新資訊來動態更新 Asset Intelligence 類別目錄，請將它連線至 Microsoft Cloud。 

使用 Asset Intelligence 來協助協調您企業的軟體授權使用情形。 將軟體授權資訊匯入至 Configuration Manager 站台資料庫，以針對正在使用的軟體來檢視它。  



## <a name="asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a> Asset Intelligence 類別目錄  

Asset Intelligence 類別目錄是儲存在站台資料庫中的一系列資料庫資料表。 這些資料表包含超過 300,000 個軟體標題和版本的分類和識別資訊。 它們也可用來管理特定軟體標題的硬體需求。  

Asset Intelligence 能提供正在使用之軟體標題的軟體授權資訊，包括 Microsoft 和非 Microsoft 軟體。 Asset Intelligence 類別目錄提供一組預先定義的軟體標題硬體需求，而您則可以建立新的使用者定義硬體需求資訊以符合自訂需求。 您也可以自訂 Asset Intelligence 類別目錄中的資訊，並將軟體標題資訊上傳至 Microsoft Cloud 以進行分類。  

您可以定期下載內含新發行軟體的 Asset Intelligence 類別目錄更新，以執行大量類別目錄更新。 您也可以使用 Asset Intelligence 同步處理點來動態更新它。  


### <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a> 軟體類別  

Asset Intelligence 軟體類別已被用來廣泛分類已清查的軟體標題，也被用於進行更特定軟體系列的高階分組。 例如，軟體類別可能是能源公司，而該軟體類別內的軟體系列可能是石油與天然氣或水力電氣。 許多軟體類別都已預先定義於 Asset Intelligence 類別目錄中。 您可以建立使用者定義類別來額外定義已清查的軟體。 所有預先定義軟體類別的驗證狀態一律是 [已驗證]  。 新增至 Asset Intelligence 類別目錄的自訂軟體類別資訊則是 [使用者定義]  。 

如需如何管理軟體類別的詳細資訊，請參閱[設定 Asset Intelligence](configuring-asset-intelligence.md)。  

> [!NOTE]  
> Asset Intelligence 類別目錄中儲存的預先定義軟體類別資訊是唯讀。 您無法變更或刪除它。 系統管理使用者可以新增、修改或刪除使用者定義的軟體類別。  


### <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a> 軟體系列  

Asset Intelligence 軟體系列可用來定義軟體類別內已清查的軟體標題。 許多軟體系列皆已預先定義於 Asset Intelligence 類別目錄中。 您可以建立使用者定義類別來額外定義已清查的軟體。 所有預先定義軟體系列的驗證狀態一律是 [已驗證]  。 新增至 Asset Intelligence 類別目錄的自訂軟體系列資訊則是 [使用者定義]  。 

如需如何管理軟體系列的詳細資訊，請參閱[設定 Asset Intelligence](configuring-asset-intelligence.md)。  

> [!NOTE]  
> 預先定義的軟體系列資訊是唯讀，而且無法變更。 系統管理使用者可以新增、修改或刪除使用者定義的軟體系列。  


### <a name="software-labels"></a><a name="BKMK_CustomLabels"></a> 軟體標籤  

Asset Intelligence 自訂軟體標籤可讓您建立篩選器以將軟體標題分組，並在 Asset Intelligence 報告中檢視它們。 使用軟體標籤來建立共用相同屬性之軟體標題的使用者定義群組。 比方說，您可以建立一個稱為「共享軟體」的軟體標籤，將它與已清查的共享軟體標題建立關聯，然後執行報告以顯示具有該標籤的所有軟體標題。 沒有預先定義的標籤。 因此，軟體標籤的驗證狀態一律是 [使用者定義]  。 

如需如何管理軟體標籤的詳細資訊，請參閱[設定 Asset Intelligence](configuring-asset-intelligence.md)。  


### <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> 硬體需求  

使用硬體需求資訊來先確認電腦是否符合軟體標題的硬體需求，再將它們設為軟體部署的目標。 您可以在 [資產與合規性]  工作區中 [Asset Intelligence]  節點下的 [硬體需求]  節點下，管理軟體標題的硬體需求。 

許多硬體需求皆已預先定義於 Asset Intelligence 類別目錄中。 建立新的使用者定義硬體需求資訊以符合自訂需求。 所有預先定義硬體需求的驗證狀態一律是 [已驗證]  。 新增至 Asset Intelligence 類別目錄的使用者定義硬體需求資訊則是 [使用者定義]  。 

如需如何管理硬體需求的詳細資訊，請參閱[設定 Asset Intelligence](configuring-asset-intelligence.md)。  

> [!NOTE]  
> 顯示在 Configuration Manager 主控台中的硬體需求是擷取自 Asset Intelligence 類別目錄。 它們不是基於來自用戶端的已清查軟體標題資訊。 
> 
> 硬體需求資訊不會與 Microsoft 同步處理程序一起更新。 
> 
> 針對沒有相關聯硬體需求的已清查軟體，您可以建立使用者定義的硬體需求。  

根據預設，每個列出的硬體需求會顯示下列資訊：  

- **軟體標題**：與硬體需求相關聯的軟體標題  

- **CPU 下限 (MHz)** ：軟體標題所需的最低處理器速度，以百萬赫茲 (MHz) 為單位  

- **RAM 下限 (KB)** ：軟體標題所需的最小 RAM，以千位元組 (KB) 為單位  

- **磁碟空間下限 (KB)** ：軟體標題所需的最小可用硬碟空間，以 KB 為單位  

- **磁碟大小下限 (KB)** ：軟體標題所需的最小硬碟大小，以 KB 為單位  

- **驗證狀態**：硬體需求的驗證狀態  

儲存在 Asset Intelligence 類別目錄中的預先定義硬體需求是唯讀，而且無法刪除。 系統管理使用者可以新增、修改或刪除未儲存在 Asset Intelligence 類別目錄中的使用者定義軟體標題硬體需求。  



## <a name="inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> 已清查的軟體項目  

若要在 Configuration Manager 主控台中檢視已清查的軟體標題資訊，請移至 [資產與合規性]  工作區，展開 [Asset Intelligence]  節點，然後選取 [已清查的軟體]  節點。 硬體清查代理程式會依據儲存在 Asset Intelligence 類別目錄中的軟體標題，從 Configuration Manager 用戶端收集已清查的軟體資訊。  

> [!Note]  
> 硬體清查代理程式會根據您啟用的 Asset Intelligence 硬體清查報告類別來收集清查項目。 如需如何啟用報告類別的詳細資訊，請參閱[設定 Asset Intelligence](configuring-asset-intelligence.md)。  

根據預設，每個列出的已清查軟體項目會顯示下列資訊：  

- **名稱**：已清查軟體標題的名稱  

- **廠商**：開發已清查軟體標題的廠商名稱  

- **版本**：已清查軟體標題的產品版本  

- **類別**：目前指派給已清查軟體標題的軟體類別  

- **系列**：目前指派給已清查軟體標題的軟體系列  

- **標籤** [**1**、**2** 和 **3**]：與軟體標題相關聯的自訂標籤。 已清查的軟體項目最多可以有三個與其相關聯的自訂標籤。  

- **計數**：已對軟體標題進行清查的 Configuration Manager 用戶端數目  

- **狀態**：已清查軟體標題的驗證狀態  

> [!NOTE]  
> 您只能在階層中的頂層站台變更已清查軟體的分類資訊。 此資訊包含產品名稱、廠商、軟體類別與軟體系列。 修改預先定義的軟體分類資訊之後，軟體的驗證狀態會從 [已驗證]  變更為 [使用者定義]  。  



## <a name="asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a> Asset Intelligence 同步處理點  

Asset Intelligence 同步處理點是 Configuration Manager 站台系統角色。 它是用來透過 TCP 通訊埠 443 連線到 Microsoft Cloud，以管理動態類別目錄資訊更新。 只能在階層的頂層站台上安裝此站台角色。 使用連線至頂層站台的 Configuration Manager 主控台，來設定所有 Asset Intelligence 類別目錄的自訂項目。 

雖然您是在頂層站台中設定所有更新，但系統會將類別目錄資訊複寫到階層中的其他站台。 此站台角色可讓您向 Microsoft 要求進行隨選類別目錄同步處理，或排程自動類別目錄同步處理。 除了下載新的類別目錄資訊之外，Asset Intelligence 同步處理點還可以將自訂軟體標題資訊上傳至 Microsoft 以進行分類。 Microsoft 會將所有上傳的軟體標題視為公用資訊。 請確認您的自訂軟體標題沒有包含機密或專利資訊。  

在您提交未分類的軟體標題之後，在針對相同的軟體標題至少有四個來自客戶的分類要求之前，Microsoft 將不會檢閱它。 在那之後，Microsoft 研究人員將會進行識別與分類，然後將該軟體標題的分類資訊提供給所有使用線上服務的客戶。 分類要求數最多的軟體項目，其分類優先順序最高。 自訂軟體和企業營運應用程式不太可能會收到類別。 請不要將這些軟體標題傳送給 Microsoft 以進行分類。  

需具備 Asset Intelligence 同步處理點，才能連線到 Microsoft Cloud。 如需如何安裝該角色的相關資訊，請參閱[設定 Asset Intelligence](configuring-asset-intelligence.md)。  



## <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence 首頁  

[資產與合規性]  工作區中的 [Asset Intelligence]  節點，是 Asset Intelligence 在 Configuration Manager 中的首頁。 此首頁會顯示 Asset Intelligence 類別目錄資訊的摘要儀表板檢視。  

> [!NOTE]  
> 在檢視 [Asset Intelligence]  首頁期間，首頁不會自動更新。  

[Asset Intelligence]  首頁包括下列區段：  

- **類別目錄同步處理**：提供 Asset Intelligence 是否已啟用，以及 Asset Intelligence 同步處理點目前狀態的相關資訊。  

    > [!NOTE]  
    > 首頁只會在您已安裝 Asset Intelligence 同步處理點的情況下顯示此區段。  

    該區段也會提供下列資訊：  

    - 同步處理排程  

    - 如果您已匯入客戶授權聲明   

    - 上次狀態更新  

    - 下一個已排程更新的時間  

    - 安裝 Asset Intelligence 同步處理點之後的變更數目   

- **已清查的軟體狀態**：由 Microsoft 所識別、由系統管理員所識別、等待線上識別，或無法辨識且未擱置的已清查軟體、軟體類別目錄，以及軟體系列的計數和百分比。 以表格格式顯示的資訊會顯示針對每個，計數和圖表中顯示的資訊顯示每個百分比。  



## <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence 報告  

在 Configuration Manager 主控台中，Asset Intelligence 報告位於 [監視]  工作區之 [報告]  節點下的 **Asset Intelligence** 資料夾中。 這份報告提供硬體、授權管理和軟體的相關資訊。 如需 Configuration Manager 中報告的詳細資訊，請參閱[報告簡介](../../../servers/manage/introduction-to-reporting.md)。  

> [!NOTE]  
> 顯示在 Asset Intelligence 報告中的已安裝軟體標題數量及授權資訊的精確度，可能會與已安裝軟體標題的實際數量或用於環境中的授權數量有所不同。 因為要清查企業環境中安裝的軟體項目之軟體授權資訊涉及到複雜的相依性與限制，因此會造成這項差異。 請不要將 Asset Intelligence 報告作為判斷已購買軟體授權合規性的唯一來源。  


### <a name="hardware-reports"></a><a name="BKMK_HardwareReports"></a> 硬體報告  

Asset Intelligence 硬體報告能提供組織中硬體資產的相關資訊。 Asset Intelligence 硬體報告可藉由使用速度、記憶體及週邊裝置等硬體清查資訊，呈現 USB 裝置與必須升級之硬體的相關資訊，甚至是尚未準備好進行特定軟體升級之電腦的相關資訊。  

> [!NOTE]  
> Asset Intelligence 硬體報告中的部分使用者資料是從 Windows 安全性事件記錄檔中收集。 為保障較佳的報告精確度，請在將電腦重新指派給新使用者時清除此記錄檔。  


### <a name="license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a> 授權管理報告  

Asset Intelligence 授權管理報告能提供正在被使用之授權的相關資料。 [授權分類帳]  報告會使用與 Microsoft 授權聲明 (MLS) 一致的格式列出已安裝的 Microsoft 應用程式。 此格式能讓您方便將已使用的授權與所購買的授權進行比對。 其他授權管理報告則提供作為執行金鑰管理服務 (KMS) 的伺服器以取得 Windows 啟用統計資料之電腦的相關資訊。  

> [!IMPORTANT]  
> 若干 Asset Intelligence 授權管理報告會顯示 KMS (管理大量授權方法之一) 功能的相關資訊。 如果您尚未實作 KMS 伺服器，有些報告可能不會傳回任何資料。  


### <a name="software-reports"></a><a name="BKMK_SoftwareReports"></a> 軟體報告  

Asset Intelligence 軟體報告能提供安裝在組織電腦上的軟體系列、類別以及特定軟體標題的相關資訊。 軟體報告能顯示瀏覽器協助程式物件與會自動啟動的軟體等的相關資訊。 這些報告可以用來識別廣告軟體、間諜軟體及其他惡意程式碼。 您也可以使用它們來識別軟體備援，以協助簡化軟體購買和支援。  


### <a name="software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a> 軟體識別標記報告  

Asset Intelligence 軟體識別標記報告會提供包含符合 ISO/IEC 19770-2 的軟體識別標記之軟體的相關資訊。 該軟體識別標記能提供用來識別已安裝之軟體的授權資訊。 在您啟用 **SMS_SoftwareTag** 硬體清查報告類別時，Configuration Manager 即會收集包含軟體識別標記之軟體的相關資訊。 

下列報告提供軟體相關資訊：  

- **軟體 14A - 搜尋已啟用軟體識別標記的軟體**：已啟用軟體識別標記的已安裝軟體計數  

- **軟體 14B - 安裝啟用特定軟體識別標記之軟體的電腦**：安裝已啟用特定軟體識別標記之軟體的所有電腦  

- **軟體 14C - 特定電腦上安裝的已啟用軟體識別標記的軟體**：特定電腦上安裝的所有已啟用特定軟體識別標記的軟體  


### <a name="reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a> 報告限制  

Asset Intelligence 報告可以提供正在被使用的已安裝軟體標題及已購買軟體授權的大量相關資訊。 請不要將此資訊作為判斷已購買軟體授權合規性的唯一來源。  

#### <a name="example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> 相依性範例  
Asset Intelligence 報告中針對已安裝軟體標題和授權資訊所顯示的數量精確度，可能會和目前所使用的實際數量有所差異。 因為要清查企業環境中所使用的軟體項目之軟體授權資訊涉及到複雜的相依性，因此會造成這項差異。 下列範例說明使用 Asset Intelligence 清查企業中已安裝軟體所涉及的相依性，其可能會影響 Asset Intelligence 報告的精確度：  

- **用戶端硬體清查相依性**：Asset Intelligence 已安裝軟體報告是以收集自 Configuration Manager 用戶端的資料作為根據，其作法是藉由擴充硬體清查來啟用 Asset Intelligence 報告。 這種對硬體清查報告的相依性，會導致 Asset Intelligence 報告僅會反映來自順利完成硬體清查處理程序且已啟用必要 Asset Intelligence WMI 報告類別的用戶端。 由於 Configuration Manager 用戶端會依據系統管理使用者所定義的排程執行硬體清查處理程序，因此資料報告可能會發生延遲並影響 Asset Intelligence 報告的精確度。 

    比方說，在用戶端成功完成硬體清查週期後，其中某個已清查的授權軟體項目可能被解除安裝。 Asset Intelligence 報告會將軟體標題顯示為已安裝，直到用戶端下一個排定的硬體清查報告週期為止。  

- **軟體封裝相依性**：Asset Intelligence 報告是依據使用標準 Configuration Manager 用戶端硬體清查程序所收集的已安裝軟體標題資料。 部分軟體標題資料的收集可能有誤。 以下是可能會造成 Asset Intelligence 報告不正確的範例：  

    - 沒有符合標準安裝程序的軟體安裝  

    - 在安裝前變更的軟體安裝   

#### <a name="legal-limitations"></a><a name="BKMK_LegalLimitations"></a> 法律限制  
顯示在 Asset Intelligence 報告中的資訊受限於許多限制。 顯示於其中的資訊並無法作為法律、會計或其他專業意見。 由 Asset Intelligence 報告所提供的資訊僅供參考。 請不要將它作為判斷軟體授權使用情形合規性的唯一資訊來源。  

下列限制為可能會影響報告精確度的 Asset Intelligence 使用範例：  

- **Microsoft 授權使用量數量限制**：  

    - 已購買之 Microsoft 軟體授權的數量，是以系統管理員所提供的資訊作為基礎。 請仔細檢閱它，以確認其所提供的軟體授權數目是正確的。  

    - 所報告的 Microsoft 軟體授權數量僅包含透過大量授權方案取得的 Microsoft 軟體授權的相關資訊。 它不會反映透過零售、OEM 或其他軟體授權銷售通路取得之軟體授權的資訊。  

    - 由於軟體轉銷商的報告需求和排程所致，回報的 Microsoft 軟體授權數量可能不會納入前 45 天內取得的軟體授權。  

    - 因公司合併或收購導致的軟體授權移轉可能不會反映在 Microsoft 軟體授權數量中。  

    - Microsoft 大量授權 (MVLS) 協議中的非標準條款及條件可能會影響報告的軟體授權數目。 它們可能需由 Microsoft 代表再行審閱。  

- **安裝的軟體標題數量限制**：Configuration Manager 用戶端必須成功完成硬體清查報告週期，Asset Intelligence 報告才能準確地回報已安裝軟體標題的數量。 在成功完成硬體清查報告週期之後，已授權軟體標題的安裝或解除安裝之間可能會出現延遲。 在用戶端報告其下一個排程的硬體清查之前，此動作可能不會反映在 Asset Intelligence 報告執行中。  

- **授權對帳限制**：針對已購買軟體授權的數量與已安裝軟體標題的數量之間的對帳，是透過比較由系統管理員所指定的授權數量，以及根據系統管理員所設定的排程從 Configuration Manager 用戶端硬體清查收集的已安裝軟體標題數量來計算。 此比較不代表 Microsoft 的最終授權定位結論。 實際的授權位置取決於特定軟體標題授權和使用權限授與的授權條款。  



## <a name="asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a> Asset Intelligence 驗證狀態  

Asset Intelligence 驗證狀態代表 Asset Intelligence 類別目錄資訊的來源和目前驗證狀態。 下表說明可能的 Asset Intelligence 驗證狀態，以及可能會造成這些狀態的系統管理員動作。  

| 狀況 | 定義 | 系統管理員動作 | 註解 |  
|---------------|--------------------|------------------------------|-----------------|  
|**已驗證**|Microsoft 研究人員已定義類別目錄項目|無|最佳狀態|  
|**使用者定義**|Microsoft 研究人員尚未定義類別目錄項目|自訂本機類別目錄資訊|此狀態會顯示在 Asset Intelligence 報告中|  
|**擱置**|Microsoft 研究人員尚未定義類別目錄項目，但您已將該項目提交給 Microsoft 以進行分類|要求分類後無需進行任何進一步動作|類別目錄項目會維持此狀態，直到 Microsoft 研究人員分類該項目，且您同步處理您的 Asset Intelligence 類別目錄為止|  
|**可更新**|Microsoft 在類別目錄同步處理期間，已使用不同的方式分類使用者定義的類別目錄項目。|使用 [解決衝突]  動作來決定要使用新的分類資訊或使用之前的使用者定義值。 如需如何解決衝突的詳細資訊，請參閱 [Asset Intelligence 的作業](operations-for-asset-intelligence.md)。|解決分類衝突後，該項目便不會被驗證為衝突，直到之後的分類更新導入有關該項目的新資訊為止。|  
|**未分類**|Microsoft 研究人員尚未定義類別目錄項目、該項目未提交至 Microsoft 以進行分類，以及系統管理員尚未指派使用者定義的分類值。|要求分類或自訂本機類別目錄資訊。 如需詳細資訊，請參閱 [Asset Intelligence 的作業](operations-for-asset-intelligence.md)。|無|  

> [!NOTE]  
> 提交至 Microsoft 以進行分類的類別目錄項目，在管理中心網站上的驗證狀態皆會是 [擱置中]  ，但會在子主要站台上會繼續顯示 [未分類]  的驗證狀態。  

如需驗證狀態何時可能會從一個狀態轉換到另一個狀態的範例，請參閱 [Asset Intelligence 驗證狀態轉換範例](example-validation-state-transitions-for-asset-intelligence.md)。  
