---
title: 1806 的診斷和使用方式資料
titleSuffix: Configuration Manager
description: 深入了解 Configuration Manager 在 1806 版每個層級收集的特定資料。
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0287beb-70a9-4b57-a627-e7bfba27fd3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e47d9ac210d4af25070c6a9cd4b710c383370f54
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506293"
---
# <a name="diagnostic-and-usage-data-for-1806"></a>1806 的診斷和使用方式資料

適用於：Configuration Manager (最新分支)

下列各節提供有關在每個層級所收集資料的額外詳細資料。 如需層級和其變更方式的詳細資訊，請參閱[診斷使用方式資料的層級](levels-overview.md)。

來自舊版的變更會以 ***[新增]***、***[已更新]***、***[已移除]*** 或 ***[已移動]*** 註明。

> [!IMPORTANT]
> Configuration Manager 不會在「基本」層級或「增強」層級上收集站台碼、站台名稱、IP 位址、使用者名稱、電腦名稱、實體位址或電子郵件地址。 在「完整」層級上對此資訊所做的任何收集都不具目的性。 在記錄檔或記憶體快照等進階診斷資訊中即潛在地包含此資訊。 Microsoft 不會使用這項資訊來辨識或連絡您，也不會用作廣告用途。

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> 層級 1 - 基本

針對 Configuration Manager 1806 版，這個層級包括下列資料：

- Configuration Manager 主控台連線的相關統計資料：OS 版本、語言、SKU 和架構、系統記憶體、邏輯處理器計數、Connect 站台識別碼、已安裝的 .NET 版本，以及主控台語言套件

- 基本應用程式和部署類型計數：應用程式總數、具有多個部署類型的應用程式總數、具有相依性的應用程式總數、已被取代的應用程式總數，以及使用中部署技術的計數

- 基本 Configuration Manager 站台階層資料：站台清單、類型、版本、狀態、用戶端計數，以及時區

- [已更新] 基本資料庫設定：處理器、記憶體大小、記憶體設定、Configuration Manager 資料庫設定、Configuration Manager 資料庫大小、叢集設定，以及分散式檢視的設定

- 基本探索統計資料：探索計數、最小/最大/平均群組大小，以及站台完全以 Azure Active Directory 服務執行時的資料

- 有關反惡意程式碼用戶端版本的基本 Endpoint Protection 資訊

- 基本映像 OS 部署計數

- 基本站台系統伺服器資訊：所使用的站台系統角色、網際網路和 SSL 狀態、OS、處理器、實體或虛擬機器，以及站台伺服器高可用性的使用情況

- Configuration Manager 資料庫結構描述 (所有物件定義的雜湊)

- 所設定的診斷和使用方式資料層級、線上或離線模式，以及快速更新設定

- 用戶端語言和地區設定的計數

- Configuration Manager 用戶端版本、OS 版本及 Office 版本的計數

- 受管理裝置作業系統和 Exchange Connector 所設定原則的計數

- Windows 10 裝置的計數 (依分支和組建)

- 使用 Windows Update for Business 的 Windows 10 用戶端計數  

- 資料庫效能指標：複寫處理資訊、前幾名 SQL Server 預存程序 (依處理器)，以及磁碟使用量

- 發佈點和管理點類型及基本設定資訊：受保護、預先設置、PXE、多點傳送、SSL 狀態、提取/對等發佈點、啟用 MDM，以及啟用 SSL

- 管理主控台屬性頁與精靈的延伸模組雜湊清單

- 安裝程式資訊：
     - 組建、安裝類型、語言套件以及您啟用的功能   

     - 發行前版本的使用、安裝媒體類型及分支類型

     - 軟體保證到期日      

     - 更新套件部署狀態和錯誤、下載進度和必要條件錯誤 

     - 使用更新快速通道 (Fast Ring)

     - 升級後的指令碼版本

- SQL 版本、Service Pack 層級、版本、定序識別碼和字元集     

- 診斷和使用方式資料的統計資料：執行時、執行階段、錯誤

- 啟用或停用網路探索

- 加入 Azure Active Directory 的用戶端計數

- 已建立的階段式部署計數 (依類型)

- 延伸互通性用戶端的計數

- 長度超過 255 個字元的硬體清查內容雜湊清單

- [已移動] 用戶端計數 (依共同管理註冊方法)  

- [已移動] 共同管理註冊的錯誤統計資料  

- [新增] 最接近三個月間隔的用戶端計數 (依 Windows OS 存留期)  

- [新增] 用戶端上使用的前 10 個處理器名稱  

- [新增] 重要 Configuration Manager 物件的計數和處理速率：資料探索記錄 (DDR)、狀態訊息、硬體清查、軟體清查和收件匣中的檔案總數  

- [新增] 站台伺服器磁碟和處理器效能資訊  

- [新增] Configuration Manager 站台伺服器處理序的執行時間和記憶體使用量資訊  

- [新增] Configuration Manager 站台伺服器處理序的損毀計數和 Watson 簽章識別碼 (如果有的話)  



## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> 層級 2 - 增強

針對 Configuration Manager 1806 版，這個層級包括下列資料：

### <a name="application-management"></a>應用程式管理  

- 應用程式需求：部署技術所參考的內建條件計數

- 應用程式取代、最大鏈結深度

- 應用程式核准統計資料及使用頻率

- 應用程式內容大小統計資料

- 應用程式部署資訊：安裝與解除安裝的使用比較、需要核准、啟用/停用使用者互動、相依性、取代，以及安裝行為功能的使用計數  

- 應用程式原則大小與複雜性統計資料

- 可用的應用程式要求統計資料

- 套件和程式的基本設定資訊：部署選項和程式旗標

- 部署類型的基本使用方式/目標資訊：使用者與目標裝置的比較、必要與可用的比較，以及通用應用程式

- App-V 環境和部署內容的計數

- 應用程式適用性計數 (依 OS)  

- 工作順序所參照之應用程式的計數

- 應用程式目錄的相異商標計數

- 使用儀表板建立的 Office 365 應用程式計數

- 封裝的計數 (依類型)  

- 封裝/程式部署的計數  

- Windows 10 已授權應用程式的授權計數  

- 依解除安裝內容設定的 Windows Installer 部署類型計數

- 商務用 Microsoft Store 應用程式計數和同步統計資料：應用程式的摘要類型、已授權應用程式狀態，以及線上和離線的已授權應用程式數目  

- 維護期間類型和持續時間  

- 每個使用者/裝置每段時間的最小/最大/平均應用程式部署數目

- 依部署技術分類的最常見應用程式安裝錯誤碼

- MSI 設定選項和計數

- 具有必要軟體部署之通知的使用者互動統計資料   

- Universal Data Access 使用方式、建立方式

- 彙總的「使用者裝置親和性」統計資料 

- 每一裝置的主要使用者最大值和平均值  

- [新增] 應用程式的全域條件使用量 (依類型)  

- [新增] 軟體中心自訂設定  

- [新增] Package Conversion Manager 整備程度和計數  

- [新增] 應用程式偵測方法的計數 (依類型)  

- [新增] 應用程式強制執行錯誤的計數  

- [新增] MSI 安裝程式內容 

- [新增] 使用者安裝要求的統計資料



### <a name="client"></a>用戶端  

- 主動管理技術 (AMT) 用戶端版本

- BIOS 存留期 (以年為單位)

- 已啟用安全開機的裝置計數

- 依 TPM 狀態的裝置計數

- 用戶端自動升級：部署設定，包括用戶端試驗和排除使用 (擴充相互操作的用戶端)

- 用戶端快取大小設定

- 用戶端部署下載錯誤

- [已更新] 用戶端健全狀況統計資料和熱門問題摘要 (依用戶端版本)

- 用戶端通知作業動作狀態：每個動作的執行次數、目標用戶端的最大數目，以及平均成功率

- 每個來源位置類型的用戶端安裝計數  

- 用戶端安裝失敗的計數  

- 使用 Hyper-V 或 Azure 虛擬化的裝置計數  

- 軟體中心動作計數   

- 啟用 UEFI 裝置的計數

- 用戶端所使用的部署方法，以及每個部署方法的用戶端計數

- 已啟用的用戶端代理程式清單/計數  

- 作業系統存留期 (以月為單位)

- 硬體清查類別、軟體清查規則和檔案集合規則的數目

- 裝置健康情況證明統計資料：最常見的錯誤碼、內部部署伺服器數目，以及處於各種狀態的裝置計數。

- 裝置計數 (依預設瀏覽器)  

- [新增] Configuration Manager 產生之伺服器驗證憑證的計數  

- [新增] Microsoft Surface 裝置的計數 (依模型)  


### <a name="cloud-services"></a>雲端服務  

- Azure Active Directory 探索統計資料

- 雲端管理閘道的設定和使用方式統計資料：區域和環境的計數，以及驗證/授權統計資料

- 連線至 Configuration Manager 的 Azure Active Directory 應用程式與服務計數

- 同步處理至 Azure Log Analytics 的集合計數

- Upgrade Analytics 連接器計數

- 是否已啟用 Azure Log Analytics 雲端連接器  

- [新增] 將雲端發佈點作為來源位置之提取發佈點的計數  


### <a name="co-management"></a>共同管理  
- 彙總的共同管理使用方式統計資料：已註冊的用戶端數目、接收原則的用戶端、工作負載狀態、試驗/排除集合大小，以及註冊錯誤  

- 註冊排程和歷程記錄統計資料  

- 符合共同管理資格的用戶端計數  

- 相關的 Microsoft Intune 租用戶


### <a name="collections"></a>集合  

- 集合識別碼使用方式 (識別碼未用盡)

- 集合評估統計資料：查詢時間、已指派與未指派計數的比較、計數 (依類型)、識別碼變換，以及規則使用方式

- 沒有部署的集合


### <a name="compliance-settings"></a>相容性設定  

- 基本設定基準資訊：計數、部署數目，以及參考數目

- 合規性原則錯誤統計資料

- 設定項目的計數 (依類型)  

- 參考內建設定的部署計數，包括修復設定  

- 針對自訂設定建立的規則和部署計數，包括修復設定  

- 所部署之簡單憑證註冊通訊協定 (SCEP)、VPN、Wi-Fi、憑證 (.pfx) 及合規性政策範本的計數

- SCEP 憑證、VPN、Wi-Fi、憑證 (.pfx) 及合規性政策部署的計數 (依平台)

- Windows Hello 企業版原則 (已建立、已部署)  

- ***[新增]*** 已部署的 Microsoft Edge 舊版瀏覽器原則計數  


### <a name="content"></a>Content  

- 界限群組統計資料：有多少個是快的、有多少個是慢的、每一群組計數，以及後援關聯性

- 界限群組資訊：指派給每個界限群組的界限和站台系統計數  

- 界限群組關聯性和後援設定

- 用戶端內容下載統計資料

- 界限的計數 (依類型)  

- 對等快取用戶端、使用方式統計資料及部分下載統計資料的計數

- 發佈管理員設定資訊：執行緒、重試延遲、重試次數，以及提取發佈點設定  

- 發佈點設定資訊：分支快取和發佈點監視的使用

- 發佈點群組資訊：指派給每個發佈點群組的套件和發佈點計數  

- [新增] 不論是本機或遠端的內容庫類型  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Microsoft Defender 進階威脅防護 (ATP) 原則 (前稱為 Windows Defender ATP)：原則的計數，以及是否部署原則。

- 針對 Endpoint Protection 功能所設定的警示計數  

- 選取要在 Endpoint Protection 儀表板中顯示的集合計數  

- Windows Defender 惡意探索防護原則、部署及目標用戶端的計數

- Endpoint Protection 部署錯誤、Endpoint Protection 原則部署錯誤碼計數  

- Endpoint Protection 反惡意程式碼和 Windows 防火牆原則使用方式 (指派給群組的唯一原則數目)<br /><br /> 此資料不包括原則所含設定的任何相關資訊。  


### <a name="migration"></a>移轉  

- 已移轉物件計數 (使用移轉精靈)


### <a name="mobile-device-management-mdm"></a>行動裝置管理 (MDM)  

- 所發出行動裝置動作的計數：鎖定、pin rest、抹除、淘汰，以及立即同步命令

- 行動裝置原則的計數  

- 受 Configuration Manager 和 Microsoft Intune 管理的行動裝置計數，以及其註冊方式 (大量、以使用者為基礎)  

- 擁有多部已註冊行動裝置的使用者計數  

- 行動裝置輪詢排程，以及行動裝置簽入持續時間的統計資料  


### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune 疑難排解  

- 複寫至 Microsoft Intune 之裝置動作 (抹除、淘汰、鎖定)、使用方式資料和資料訊息的計數和大小

- 可從 Microsoft Intune 下載之狀態 (State 和 Status)、清查、RDR、DDR、UDX、租用戶狀態、POL、LOG、Cert、CRP、重新同步、CFD、RDO、BEX、ISM 和合規性訊息的計數和大小

- Microsoft Intune 的完整和差異使用者同步處理統計資料


### <a name="on-premises-mobile-device-management-mdm"></a>內部部署行動裝置管理 (MDM)  

- Windows 10 大量註冊封裝和設定檔的計數  

- 內部部署 MDM 應用程式部署的部署成功/失敗統計資料  


### <a name="os-deployment"></a>OS 部署  

- 開機映像、驅動程式、驅動程式套件、啟用多點傳送的發佈點、啟用 PXE 的發佈點和工作順序的計數  

- 依據 Configuration Manager 用戶端版本的開機映像計數

- 依據 Windows PE 版本的開機映像計數

- 版本升級原則計數

- 從 PXE 排除的硬體識別碼計數

- OS 部署計數 (依 OS 版本)

- 一段時間內的 OS 升級計數

- 使用預先下載內容選項的工作順序部署計數

- 工作順序步驟使用的計數

- 已安裝的 Windows ADK 版本  

- [新增] 映像服務工作的計數  


### <a name="site-updates"></a>站台更新  

- 已安裝的 Configuraton Manager Hotfix 版本


### <a name="software-updates"></a>軟體更新  

- 自動部署規則中所使用的可用和期限差異  

- 每個更新的平均和最大指派數目  

- 用戶端更新評估和掃描排程  

- 軟體更新點所同步的分類

- 叢集修補統計資料  

- Windows 10 快速更新設定

- 作用中 Windows 10 服務方案所使用的設定  

- 已部署的 Office 365 更新計數  

- 同步的 Microsoft Surface 驅動程式計數

- 更新群組和指派的計數  

- 更新套件的計數，以及套件之目標發佈點的最大/最小/平均數目  

- System Center Update Publisher 所建立和部署的更新計數  

- 已建立和部署的商務用 Windows Update 原則計數

- 彙總的「商務用 Windows Update」設定統計資料

- 與同步處理相關的自動部署規則數目  

- 建立新的更新或將更新新增至現有群組的自動部署規則數目  

- 具有多個部署的自動部署規則數目  

- 更新群組數目，以及每個群組的最小/最大/平均更新數目  

- 已部署、到期、取代、下載及包含 EULA 的更新數目和百分比  

- 軟體更新點負載平衡統計資料

- 軟體更新點同步處理排程  

- 具有軟體更新部署的集合總數/平均數，以及已部署更新的最大/平均數目  

- 更新掃描錯誤碼和電腦計數  

- Windows 10 儀表板內容版本  

- [新增] 協力廠商軟體更新類別目錄訂閱和使用量計數  

- [新增] 部署包含或不含內容的軟體更新計數  


### <a name="sqlperformance-data"></a>SQL/效能資料  

- 站台摘要的設定和持續時間

- 最大資料庫資料表的計數  

- 探索操作統計資料 (找到的物件計數)

- 探索類型、已啟用及排程 (完整、累加)

- SQL AlwaysOn 複本資訊、使用方式和健全狀況狀態

- SQL 變更追蹤效能問題、保留期間和自動清除狀態

- SQL Server 變更追蹤保留期間

- 狀況及狀態訊息效能統計資料，包括最常見和成本最高的訊息類型


### <a name="miscellaneous"></a>其他  

- 資料倉儲服務點的設定，包括同步處理排程和平均時間

- 指令碼計數和執行統計資料

- 具有網路喚醒 (WOL) 的站台計數

- 報表使用方式和效能統計資料

- 階段式部署使用方式統計資料  

- [新增] CMPivot 使用量統計資料  

- [新增] 管理見解項目計數和進度  

- [新增] 站台伺服器上唯一非 Configuration Manager 處理序的損毀計數和 Watson 簽章識別碼 (如果有的話)



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> 層級 3 - 完整

針對 Configuration Manager 1806 版，這個層級包括下列資料：

- 自動部署規則評估排程資訊

- ATP 健全狀況摘要

- 集合評估和重新整理統計資料

- 有關合規性及錯誤的合規性政策統計資料

- 合規性設定：SCEP、VPN、Wi-Fi 及合規性政策範本設定詳細資料

- Configuration Manager 使用方式的 DCM 設定套件

- 詳細的用戶端部署安裝錯誤

- Endpoint Protection 健全狀況摘要：包括受保護、有風險、不明及不支援的用戶端計數

- Endpoint Protection 原則設定

- 設定應用程式安裝行為的處理序清單

- 上次軟體更新掃描後經過的最小/最大/平均時數

- 軟體更新部署集合內非使用中用戶端的最小/最大/平均數目

- 每個封裝的最小/最大/平均軟體更新數目

- MSI 產品代碼部署統計資料 

- 軟體更新部署的整體相容性

- 具有過期軟體更新的群組計數

- 軟體更新部署錯誤碼和計數

- 軟體更新部署資訊：下列各項部署的比較百分比 - 以用戶端為目標/以 UTC 時間為目標、必要/選擇性/無訊息，以及抑制重新啟動

- 軟體更新點所同步的軟體更新產品

- 軟體更新掃描成功百分比

- 環境中的前 50 個 CPU

- Microsoft Intune 所管理之裝置的 Exchange Active Sync (EAS) 條件式存取原則類型 (封鎖或隔離)

- 商務用 Microsoft Store 應用程式詳細資料：已同步應用程式的非彙總清單，包括 AppID、線上狀態或離線狀態，以及已購買的授權總數
