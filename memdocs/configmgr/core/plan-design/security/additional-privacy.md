---
title: 其他隱私權資訊
titleSuffix: Configuration Manager
description: 了解 Microsoft 如何收集和使用 Configuration Manager 的資料。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6891a46050bb83e54fb34b97d9129fcb5873785
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701416"
---
# <a name="additional-information-about-privacy-for-configuration-manager"></a>Configuration Manager 隱私權的其他資訊

適用於：  Configuration Manager (最新分支)


## <a name="updates-and-servicing"></a>更新與服務

Configuration Manager 會使用更新模型，利用最新的更新和功能來協助讓您的環境保持最新狀態。 此功能使用稱為服務連接點的站台系統角色。 您選擇安裝此角色的伺服器。 

如需所收集資訊及其使用方式的詳細資訊，請參閱[使用方式資料](#usage-data)。



## <a name="usage-data"></a>使用方式資料

Configuration Manager 收集與其本身相關的診斷和使用方式資料，Microsoft 會使用這些資料來改進未來版本的安裝體驗、品質及安全性。
系統會針對每個 System Center Configuration Manager 階層啟用診斷和使用方式資料。 它是由每週在每個主要站台和管理中心網站上執行的 SQL Server 查詢所組成。 當階層使用管理中心網站時，系統會從主要站台將資料複寫到該站台。 在您階層的頂層站台，服務連接點會在檢查更新時提交此資訊。 如果服務連接點處於離線模式，則會使用服務連線工具來傳送此資訊。

Configuration Manager 只會從站台的 SQL Server 資料庫收集資料，而不會直接從用戶端或站台伺服器收集資料。

系統管理員可以在 Configuration Manager 主控台的 [使用方式資料]  區段中，變更所收集資料的層級。

如需使用方式資料層級和設定的詳細資訊，請參閱[診斷和使用方式資料](../diagnostics/diagnostics-and-usage-data.md)。



## <a name="log-analytics-connector"></a>Log Analytics 連接器

Log Analytics 連接器會將資料 (例如集合) 從 Configuration Manager 同步處理到 Azure 雲端服務。 當系統管理員設定功能時，Azure 訂用帳戶識別碼和祕密金鑰都會儲存於 Configuration Manager 資料庫中。 Azure Active Directory 用戶端密碼和 Azure 工作區共用金鑰都會儲存於內部部署 Configuration Manager 資料庫中。 Configuration Manager 與 Azure 之間的所有通訊都會使用 HTTPS。 除了隨機的診斷和使用方式資料外，不會將有關集合的任何其他資訊提供給 Microsoft。 

如需 Log Analytics 所收集資訊的詳細資訊，請參閱 [Log Analytics 資料安全性](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-security)。



## <a name="asset-intelligence"></a>Asset Intelligence

Asset Intelligence 可讓系統管理員定義、追蹤以及主動管理設定標準的符合度。 針對部署進行測量與報告以及使用實體與虛擬應用程式，可協助組織對於軟體授權以及維護授權合約的履行做出更妥善的商業決策。 從 Configuration Manager 用戶端收集使用方式資料之後，您就可以使用各種不同功能來檢視資料，包括收集、查詢與報告。

在各個同步處理期間，會從 Microsoft 下載已知軟體的類別目錄。 您可以選擇將有關組織中所發現之未分類軟體標題 (有待研究並新增至類別目錄) 的資訊傳送給 Microsoft。 上傳此資訊之前，會有對話方塊顯示要上傳的資料。 資料一旦上傳就無法回收。 Asset Intelligence 不會將有關使用者和電腦或授權使用方式的資訊傳送給 Microsoft。

在上傳軟體標題之後，Microsoft 研究人員會進行識別、分類，然後將該知識提供給所有其他使用此功能的客戶以及其他該類別目錄的客戶。 任何上傳的軟體標題皆會公開。 應用程式與其分類會成為類別目錄的一部分，並可供下載到類別目錄的其他取用者。 在您設定 Asset Intelligence 資料收集並且決定是否將資訊提交給 Microsoft 之前，請考慮貴組織的隱私權需求。

Configuration Manager 中預設並未啟用 Asset Intelligence。 上傳未分類標題絕不會自動發生，而且系統並未設計為自動完成此工作。 您必須手動選取以及核准各個軟體標題的上傳。



## <a name="endpoint-protection"></a>Endpoint Protection

Microsoft 雲端保護服務的前稱為 Microsoft Active Protection Service 或 MAPS。

適用的產品有 System Center Endpoint Protection 和 Configuration Manager 的 Endpoint Protection 功能 (用於管理 System Center Endpoint Protection 和 Windows Defender for Windows 10)。 此功能並未針對 System Center Endpoint Protection for Linux 或 System Center Endpoint Protection for Mac 加以實作。

Microsoft 雲端保護服務反惡意程式碼社群是自發的全球線上社群，包括 System Center Endpoint Protection 使用者。 當您加入 Microsoft 雲端保護服務時，System Center Endpoint Protection 會自動將資訊傳送給 Microsoft。 Microsoft 會使用此資訊來判斷要調查潛在威脅的軟體，並協助改善 System Center Endpoint Protection 的效益。 這個社群有助於阻止新惡意軟體感染的擴散。 如果 Microsoft 雲端保護服務報告中包含 Endpoint Protection 用戶端可能可以移除之惡意程式碼或潛在垃圾軟體的詳細資料，Microsoft 雲端保護服務會下載最新的特徵來處理該軟體。 Microsoft 雲端保護服務也可以找出「誤判」情況並加以修正。 (誤判為原先識別為惡意程式碼但結果並非如此的情況)。 

Microsoft 雲端保護服務報告包含潛在的惡意程式碼檔案資訊，例如檔案名稱、加密編譯雜湊、廠商、大小和日期戳記。 此外，Microsoft 雲端保護服務可能會收集完整的 URL，以指出檔案的來源。 這些 URL 有時可能會有個人資訊，例如搜尋字詞或在表單中輸入的資料。 報告也可能包含當 Endpoint Protection 通知您有垃圾軟體時，您所採取的動作。 Microsoft 雲端保護服務報告包含此資訊以幫助 Microsoft 評估 Endpoint Protection 如何有效地偵測和移除惡意程式碼和潛在的垃圾軟體，並嘗試識別新的惡意程式碼。

如果您有基本或進階成員資格，即可加入 Microsoft 雲端保護服務。 基本成員報告具有前述資訊。 進階成員報告較為完備，而且可包含 Endpoint Protection 偵測到之軟體的其他詳細資料，例如此類軟體的位置、檔案名稱、軟體的運作方式，以及它對您的電腦造成哪些影響。 這些報告，和參與 Microsoft 雲端保護服務的其他 Endpoint Protection 使用者所提供的報告，將可幫助 Microsoft 研究人員更快發現新威脅。 接著，研究人員將會建立符合分析準則之程式的惡意程式碼定義，並透過 Microsoft Update 將更新的定義提供給所有使用者。

為了協助偵測及修正特定的惡意程式碼感染類型，產品會定期將有關電腦安全性狀態的資訊傳送給 Microsoft 雲端保護服務。 這些資訊包括電腦安全性設定和記錄檔 (描述電腦開機時載入的驅動程式和其他軟體) 的相關資訊。

也會傳送可唯一識別您電腦的編號。 此外，Microsoft 雲端保護服務可能也會收集潛在惡意程式碼檔案連線的目標 IP 位址。

Microsoft 雲端保護服務報告可用來改善 Microsoft 軟體和服務。 這些報告也可用於統計或其他測試或分析用途，並用於產生定義。 只有具有相關業務需求的 Microsoft 員工、約聘人員、合作夥伴和廠商可以存取這些報告。

Microsoft 雲端保護服務不會刻意收集個人資訊。 在 Microsoft 雲端保護服務收集任何個人資訊的情況下，Microsoft 不會利用這項資訊來識別您的身分或與您連絡。

如需詳細資訊，請參閱 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。



## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>網站階層 – 使用 Bing 地圖服務進行地理檢視

在 Configuration Manager 主控台中，移至 [監視]  工作區、選取 [站台階層]  節點，然後切換到 [地理檢視]  。 此檢視可讓您使用 Microsoft Bing 地圖服務所提供的地圖，來檢視您的 Configuration Manager 實體伺服器拓撲。 為了啟用此功能，您所提供的位置資訊會從您的伺服器傳送至 Bing 地圖服務的網路服務。

Microsoft 使用此資訊來運作和改進 Microsoft Bing 地圖服務以及其他 Microsoft 網站和服務。 如需詳細資訊，請參閱 [Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=823548)。

您可以選擇不使用網站階層的地理檢視。 預設的「階層圖」檢視可讓您查看階層而不使用 Bing 地圖服務。
