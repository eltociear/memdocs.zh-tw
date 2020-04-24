---
title: 1511 的診斷資料
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 1511 版所收集的診斷及使用資料層級。
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eaebab1e3c03ad2ffbcebf57bbccf88ce151923e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697106"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-configuration-manager"></a>Configuration Manager 1511 版的診斷使用資料收集層級

適用於：  Configuration Manager (最新分支)

Configuration Manager 1511 版會收集三個層級的診斷及使用方式資料：[基本]  、[增強]  和 [完整]  。 這項功能預設會設定為增強層級。 下列各節提供有關每個層級所收集之資料的詳細說明。  

> [!IMPORTANT]  
>  Configuration Manager 不會收集「基本」層級或「增強」層級中的站台碼、站台名稱、IP 位址、使用者名稱、電腦名稱、實體位址或電子郵件地址。 而在「完整」層級中收集到的任何上述資訊並不具有目的性；因為這些資訊可能包含在記錄檔或記憶體快照等進階診斷資訊中。 Microsoft 不會將這項資訊用於廣告目的，亦不會用來辨識您的身分或與您連絡。  

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> 如何變更層級  
 如果系統管理員具有以角色為基礎的系統管理範圍 (包含 [站台]  物件類別的 [修改]  權限)，則可以變更 Configuration Manager 主控台中 [診斷及使用方式資料] 設定所收集的資料層級。

 若要這麼做，請在主控台中移至 [Backstage] 索引標籤 (左上角含下拉式箭頭的索引標籤)，並選取 [使用方式資料]  ，然後選取您要使用的資料層級。  


##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> 層級 1 - 基本  
 「基本」層級包含您階層的相關資料，我們必須要有這些資料才能協助改善安裝或升級體驗，以及協助判斷哪些 Configuration Manager 更新適用於您的階層。  

 從 Configuration Manager 1511 版開始，這個層級包括下列內容：  


-   安裝資訊
    - 組建、安裝類型、語言套件以及您啟用的功能

    - 更新套件的部署狀態和錯誤  

-   資料庫效能標準 (複寫處理資訊、依處理器和磁碟使用量列出前幾個 SQL Server 預存程序)  

-   基本資料庫設定 (處理器、叢集設定和分散式檢視的設定)  

-   Configuration Manager 資料庫結構描述 (所有物件定義的雜湊)  

-   Configuration Manager 用戶端版本和作業系統版本的計數  

-   受管理裝置作業系統和 Exchange Connector 所設定原則的計數  

-   用戶端語言和地區設定的計數

-   Windows 10 裝置的計數 (依分支和組建)  

-   基本 Configuration Manager 站台階層資料 (站台清單、類型、版本、狀態、用戶端計數和時區)  

-   基本站台系統伺服器資訊 (所使用的站台系統角色、網際網路和 SSL 狀態、作業系統、處理器，以及實體機器或虛擬機器)  

-   基本使用者探索統計資料 (使用者探索計數以及最小/最大/平均群組大小)  

-   基本 Endpoint Protection 資訊 (反惡意程式碼用戶端版本)  

-   基本應用程式和部署類型計數 (應用程式總數、具有多個部署類型的應用程式總數、具有相依性的應用程式總數、已取代的應用程式總數，以及使用中部署技術的計數)  

-   基本作業系統部署 (OSD) 計數 (映像)  

-   發佈點和管理點類型和基本設定資訊 (受保護、前置階段、PXE、多點傳送、SSL 狀態、提取/對等發佈點、啟用 MDM、啟用 SSL 等)  

-   遙測統計資料 (執行時、執行階段，以及錯誤)  

##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> 層級 2 - 增強  
「增強」層級是安裝完成後的預設值。 這個層級包含在「基本」層級中收集的資料以及功能的特定資料 (使用的頻率和持續時間)、Configuration Manager 用戶端設定 (元件名稱、狀態、輪詢間隔等特定設定) 和軟體更新的基本資訊。  

建議使用這個層級，因為它會提供 Microsoft 必要的基本資料，以在未來的產品和服務版本中做出實用的改進。 這個層級不會收集物件名稱 (站台、使用者、電腦或物件)、安全性相關物件的詳細資料或漏洞 (例如需要軟體更新的系統計數)。  

從 Configuration Manager 1511 版開始，這個層級包括下列內容：  

-   **應用程式管理：**  

    -   組織內所使用之部署類型的基本使用方式/目標資訊 (使用者與目標裝置、需要與可用項目的比較)  

    -   應用程式部署資訊 (安裝/解除安裝、需要核准，以及啟用/停用使用者互動)  

    -   可用的應用程式要求統計資料  

    -   封裝的計數 (依類型)  

    -   應用程式適用性的計數 (依作業系統)  

    -   封裝/程式部署的計數  

    -   App-V 環境和部署內容的計數  

    -   Windows 10 已授權應用程式的授權計數  

    -   每個使用者/裝置的最小/最大/平均應用程式部署數目  

    -   維護期間類型和持續時間  

-   **用戶端：**  

    -   已啟用的用戶端代理程式清單/計數  

    -   每個來源位置類型的用戶端安裝計數  

    -   用戶端安裝失敗的計數  

-   **相容性設定：**  

    -   設定項目的計數 (依類型)  

    -   基本設定基準資訊 (計數、部署數目和參考數目)  

    -   參考內建設定的部署計數 (不會擷取設定值)  

    -   針對自訂設定所建立的規則和部署計數  

    -   已部署的簡單憑證註冊通訊協定範本計數  

-   **內容：**  

    -   界限的計數 (依類型)  

    -   界限群組資訊 (指派給每個界限群組的界限和站台系統計數)  

    -   發佈點群組資訊 (指派給每個發佈點群組的套件和發佈點計數)  

    -   發佈點設定資訊 (分支快取的使用以及發佈點監視)  

    -   發佈管理員設定資訊 (執行緒、重試延遲、重試次數和提取發佈點設定)  

-   **Endpoint Protection：**  

    -   Endpoint Protection 反惡意程式碼和 Windows 防火牆原則使用方式 (指派給群組的唯一原則數目)<br /><br />這不包括原則所含設定的任何資訊。  

    -   Endpoint Protection 部署錯誤 (Endpoint Protection 原則部署錯誤碼的計數)  

    -   選取要在 Endpoint Protection 儀表板中顯示的集合計數  

    -   針對 Endpoint Protection 功能所設定的警示計數  

-   **行動應用程式管理 (MAM)：**  

    -   啟用 MAM 的 Office 應用程式、企業營運系統應用程式以及原則的計數 (依作業系統)  

    -   MAM 應用程式/原則部署的計數  

    -   每項 MAM 設定所建立的規則計數  

-   **行動裝置管理(MDM)：**  

    -   所發出行動裝置動作的計數：鎖定、pin rest、抹除和淘汰命令

    -   受 Configuration Manager 和 Microsoft Intune 管理的行動裝置計數，以及其註冊方式 (大量或以使用者為基礎)  

    -   行動裝置輪詢排程，以及行動裝置簽入持續時間的統計資料  

    -   行動裝置原則的計數  

    -   擁有多部已註冊行動裝置的使用者計數  

-   **Microsoft Intune 疑難排解︰**  

    -   可從 Microsoft Intune 下載之狀態 (State 和 Status)、清查、RDR、DDR、UDX、租用戶狀態、POL、LOG、Cert、CRP、重新同步、CFD、RDO、BEX、ISM 和合規性訊息的計數和大小  

    -   複寫至 Microsoft Intune 之裝置動作 (抹除、淘汰、鎖定)、遙測和資料訊息的計數和大小  

    -   Microsoft Intune 的完整和差異使用者同步處理統計資料  

-   **內部部署行動裝置管理 (MDM)：**  

    -   內部部署 MDM 應用程式部署的部署成功/失敗統計資料  

    -   Windows 10 大量註冊封裝和設定檔的計數  

-   **作業系統部署：**  

    -   開機映像、驅動程式、驅動程式套件、啟用多點傳送的發佈點、啟用 PXE 的發佈點和工作順序的計數  

-   **軟體更新：**  

    -   具有軟體更新部署的集合總數/平均數，以及已部署更新的最大/平均數目  

    -   與同步處理相關的自動部署規則數目  

    -   建立新的更新或將更新新增至現有群組的自動部署規則數目  

    -   自動部署規則中所使用的可用和期限差異  

    -   每個更新的平均和最大指派數目  

    -   System Center Update Publisher 所建立和部署的更新計數  

    -   更新群組和指派的計數  

    -   更新套件的計數，以及套件之目標發佈點的最大/最小/平均數目  

    -   更新群組數目，以及每個群組的最小/最大/平均更新數目  

    -   已部署、到期、取代、下載及包含 EULA 的更新數目和百分比  

    -   更新掃描錯誤碼和電腦計數  

    -   用戶端更新評估和掃描排程  

    -   軟體更新點同步處理排程  

    -   具有多個部署的自動部署規則數目  

    -   作用中 Windows 10 服務方案所使用的設定  

    -   Windows 10 儀表板內容版本  

    -   使用 Windows Update for Business 的 Windows 10 用戶端計數  

    -   叢集修補統計資料  

    -   已部署的 Office 365 更新計數  

-   **SQL/效能資料：**  

    -   最大資料庫資料表的計數  

    -   SQL AlwaysOn 複本資訊  

    -   集合的計數 (依類型)  

##  <a name="level-3---full"></a><a name="bkmk_level3"></a> 層級 3 - 完整  
「完整」層級包含「基本」和「增強」層級中的所有資料。 它也包含 Endpoint Protection、更新相容性百分比和軟體更新資訊的其他資訊。 這個層級也會包含進階診斷資訊 (例如系統檔案和記憶體快照)，其中可能含有擷取時存在於記憶體或記錄檔中的個人資訊。  

從 Configuration Manager 1511 版開始，這個層級包括下列內容：  

-   集合評估和重新整理統計資料  

-   Endpoint Protection 健全狀況摘要 (包括受保護、有風險、不明和不受支援的用戶端計數)  

-   Endpoint Protection 原則設定  

-   軟體更新部署資訊 (以用戶端為目標/以 UTC 時間為目標、必要/選擇性/無訊息以及重新啟動歸併的對比部署百分比)  

-   軟體更新部署的整體相容性  

-   自動部署規則評估排程資訊  

-   具有網路存取保護原則的用戶端數目  

-   軟體更新部署錯誤碼和計數  

-   軟體更新部署集合內非使用中用戶端的最小/最大/平均數目  

-   具有過期軟體更新的群組計數  

-   每個封裝的最小/最大/平均軟體更新數目  

-   軟體更新掃描成功百分比  

-   上次軟體更新掃描後經過的最小/最大/平均時數  