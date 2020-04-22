---
title: 適用於 Intune 之 Microsoft Defender 防毒軟體的 Windows 10 防毒軟體原則設定 | Microsoft Docs
description: 查看適用於 Windows 10 的 Microsoft Defender 防毒軟體設定檔中的設定清單。 您可以在 Microsoft Intune 中，將這些設定設為端點安全性防毒軟體原則的一部分。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 554bc09aa57306010069df4a85baa70fafdc41a6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086672"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Microsoft Intune 中 Windows 10 Microsoft Defender 防毒軟體原則的設定

在 Microsoft Intune 中，檢視您可以為適用於 Windows 10 的 Microsoft Defender 防毒軟體設定檔設定的防毒軟體原則設定。

## <a name="cloud-protection"></a>雲端保護

- **開啟雲端提供的保護**  
  CSP：[AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  根據預設，Windows 10 Desktop 裝置上的 Defender 會將所發現的任何問題的相關資訊傳送給 Microsoft。 Microsoft 會分析該資訊，以深入了解影響您與其他客戶的問題，並提供改善的解決方案。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 開啟雲端提供的保護。  裝置使用者無法變更此設定。

- **雲端提供的保護層級**  
  CSP：[CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  設定 Defender 防毒軟體在封鎖及掃描可疑檔案方面的主動性。
  - **未設定** (*預設*) - 預設的 Defender 封鎖層級。
  - **高** - 主動地封鎖未知的檔案，同時最佳化用戶端效能 (極可能發生誤判)。
  - **極高** - 主動地封鎖未知的檔案，並套用可能會影響用戶端效能的額外保護措施。
  - **零容錯** - 封鎖所有未知的可執行檔。

- **Defender 雲端延長逾時 (秒)**  
  CSP：[CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender 防毒軟體會自動封鎖可疑的檔案 10 秒，使其可以掃描雲端的檔案，以確保其安全無虞。 使用此設定時，您最多可以對此逾時額外加上 50 秒。

## <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender 防毒軟體排除

針對此群組中的每個設定，您可以展開設定、選取 [新增]  ，然後為排除指定一個值。

- **Defender 要排除的處理序**  
  CSP：[ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  指定要在掃描期間忽略的處理序清單，掃描時會排除由這些處理序開啟的檔案。 處理序本身不會從掃描中排除。

- **不進行掃描和即時保護的副檔名**  
  CSP：[ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  指定掃描期間要忽略的檔案類型副檔名清單。

- **Defender 要排除的檔案及資料夾**  
  CSP：[ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  指定要在掃描期間忽略的檔案與目錄路徑清單。

## <a name="real-time-protection"></a>即時保護

- **開啟即時保護**  
  CSP：[AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  要求 Windows 10 Desktop 裝置上的 Defender 使用即時監視功能。
  - **未設定** (*預設*) - 此設定會還原為系統預設值
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 強制使用即時監視。 裝置使用者無法變更此設定。

- **啟用即時監視保護**  
  CSP：[AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  設定主動持續執行，而不是隨選執行的防毒保護。

  - **未設定** (*預設*) - 此原則不會改變此設定在裝置上的狀態。 裝置上的現有狀態會維持不變。
  - **否** - 在裝置上封鎖即時監視保護。 裝置使用者無法變更此設定。
  - **是** - 在裝置上啟用即時監視保護。

- **開啟行為監視**  
  CSP：[AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  根據預設，Windows 10 Desktop 裝置上的 Defender 使用行為監視功能。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 強制使用即時行為監視。 裝置使用者無法變更此設定。

- **開啟網路保護**  
  CSP：[EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  使用任何應用程式保護裝置使用者，使其無法存取網路釣魚詐騙、惡意探索網站，以及網際網路上的惡意內容。 保護包括防止第三方瀏覽器連線到危險的網站。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 網路保護已開啟。 裝置使用者無法變更此設定。

- **掃描所有已下載的檔案和附件**  
  CSP：[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)

  將 Defender 設定為掃描所有已下載的檔案和附件。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - Defender 會掃描所有已下載的檔案和附件。 裝置使用者無法變更此設定。

- **掃描在 Microsoft 瀏覽器中使用的指令碼**  
  CSP：[AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  將 Defender 設定為掃描指令碼。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - Defender 會掃描指令碼。 裝置使用者無法變更此設定。

- **掃描網路檔案**  
  CSP：[AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  將 Defender 設定為掃描網路檔案。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 開啟網路檔案的掃描。 裝置使用者無法變更此設定。

- **掃描電子郵件**  
  CSP：[AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  將 Defender 設定為掃描內送電子郵件。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 開啟電子郵件掃描。 裝置使用者無法變更此設定。

## <a name="remediation"></a>修復

- **隔離惡意程式碼後的保留天數 (0-90)**  
  CSP：[DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  指定系統儲存隔離項目的天數 (從 0 到 90)，超過這個指定的天數之後即會自動將其移除。 值為 0 時會將項目保留在隔離區中，而且系統不會自動加以移除。

- **提交同意範例**  

  - [未設定]  (預設  )
  - **自動傳送安全的樣本**
  - **一律提示**
  - **一律不傳送**
  - **自動傳送所有樣本**

- **要對潛在垃圾應用程式採取的動作**  
  CSP：[PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051&clcid=0x409)

  指定潛在垃圾應用程式 (PUA) 的偵測層級。 Defender 會在下載潛在垃圾軟體或嘗試安裝在裝置上時，對使用者發出警示。

  - **未設定** (*預設*) - 此設定會還原為系統預設值，亦即關閉 PUA 保護。
  - **停用**
  - **啟用** - 封鎖偵測到的項目，並與其他威脅一起顯示在歷程記錄中。
  - **稽核模式** - Defender 會偵測潛在的垃圾應用程式，但不採取任何動作。 您可以搜尋 [事件檢視器] 中由 Defender 建立的事件，以檢閱 Defender 會對其採取動作之應用程式的相關資訊。

- **偵測到威脅時的動作**  
  CSP：[ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938&clcid=0x409)

  根據惡意程式碼的威脅等級，指定 Defender 針對偵測到的惡意程式碼所採取的動作。
  
  Defender 會將偵測到的惡意程式碼分類為下列其中一個嚴重性等級：
  - **低嚴重性**
  - **中度嚴重性**
  - **高嚴重性**
  - **嚴重的嚴重性**

  針對每個等級，指定要採取的動作。 每個嚴重性等級的預設值都是 [未設定]  。

  - **未設定**
  - **清理** - 服務會嘗試復原檔案，並嘗試消毒。
  - **隔離** - 將檔案移至隔離區。
  - **移除** - 從裝置移除檔案。
  - **允許** - 允許檔案，而不會採取其他動作。
  - **使用者定義** - 裝置使用者會決定要採取的動作。
  - **封鎖** - 封鎖檔案執行。

## <a name="scan"></a>掃描

- **掃描封存檔**  
  CSP：[AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  將 Defender 設定為掃描封存檔，例如 ZIP 或 CAB 檔案。

  - **未設定** (*預設*) - 此設定會還原為用戶端預設值，也就是掃描封存檔，但是使用者可以停用此選項。
深入了解
  - **無** - 不掃描檔案封存。 裝置使用者無法變更此設定。
  - **是** - 啟用封存檔的掃描。 裝置使用者無法變更此設定。

- **為排程的掃描使用低 CPU 優先順序**  
  CSP：[EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944&clcid=0x409)

  為排程的掃描設定 CPU 優先順序。
  - **未設定** (*預設*) - 此設定會還原為系統預設值，而不會對 CPU 優先順序進行任何變更。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 在排程掃描期間，將會使用低 CPU 優先順序。 裝置使用者無法變更此設定。

- **停用追補完整掃描**  
  CSP：[DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042&clcid=0x409)

  為排程的完整掃描設定追補掃描。 追補掃描是因錯過定期排定的掃描而起始的掃描。 通常是因為電腦在排定的時間關機，才會錯過這些排定的掃描。

  - **未設定** (*預設*) - 此設定會還原為用戶端預設值，也就是為完整掃描啟用追捕掃描，不過使用者可以將其關閉。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 為排程的完整掃描強制執行追捕掃描，且使用者無法將其停用。 如果電腦連續在兩次排定的掃描離線，追補掃描會在下次有人登入電腦時啟動。 如果未設定排程的掃描，將不會執行追補掃描。 裝置使用者無法變更此設定。

- **停用追捕快速掃描**  
  CSP：[DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941&clcid=0x409)

  為排程的快速掃描設定追補掃描。 追補掃描是因錯過定期排定的掃描而起始的掃描。 通常是因為電腦在排定的時間關機，才會錯過這些排定的掃描。

  - **未設定** (*預設*) - 此設定會還原為用戶端預設值，也就是啟用追捕快速掃描，但是使用者可以將其關閉。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 為排程的快速掃描強制執行追捕掃描，且使用者無法將其停用。 如果電腦連續在兩次排定的掃描離線，追補掃描會在下次有人登入電腦時啟動。 如果未設定排程的掃描，將不會執行追補掃描。 裝置使用者無法變更此設定。

- **每次掃描的 CPU 使用量限制**  
  CSP：[AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  以百分比指定 0 到 100，也就是 Defender 掃描的平均 CPU 負載因數。

- **在完整掃描期間掃描對應的網路磁碟機**  
  CSP：[AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  將 Defender 設定為掃描對應的網路磁碟機。

  - **未設定** (*預設*) - 此設定會還原為系統預設值，亦即停用對應網路磁碟機的掃描。
  - **否** - 停用此設定。 裝置使用者無法變更此設定。
  - **是** - 啟用對應網路磁碟機的掃描。 裝置使用者無法變更此設定。

- **每日快速掃描的執行時間**  
  CSP：[ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)

  選取 Defender 快速掃描執行的當日時間。
  根據預設，此為 [未設定] 

- **掃描類型**  
  CSP：[ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  選取 Defender 執行的掃描類型。

  - **未設定** (*預設*)
  - **快速掃描**
  - **完整掃描**

- **執行排程掃描的星期幾**  
  - **未設定** (*預設*)

- **執行排程掃描的時間**  
  - **未設定** (*預設*)

- **執行掃描前先查看有無特徵標記更新**  
  - **未設定** (*預設*)
  - **否**
  - **是**

## <a name="updates"></a>更新

- **輸入檢查安全性情報更新的頻率 (0-24 小時)**  
  CSP：[SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  從 0 到 24 指定用來檢查特徵標記的間隔 (以小時為單位)。 值為 0 時，不會檢查新的特徵標記。 值為 2 時，將會每隔兩小時檢查一次，依此類推。

## <a name="user-experience"></a>使用者經驗

- **允許使用者存取 Microsoft Defender 應用程式**  
  CSP：[AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)  

  - **未設定** (*預設*) - 此設定會還原為用戶端預設值，其中允許 UI 與通知。
  - **否** - 無法存取 Defender 使用者介面 (UI)，而且會隱藏通知。
  - **是**

