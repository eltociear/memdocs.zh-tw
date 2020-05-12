---
title: Endpoint Protection 用戶端常見問題集
titleSuffix: Configuration Manager
description: 取得 Windows Defender 和 Endpoint Protection 常見問題的解答。
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906838"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Endpoint Protection 用戶端常見問題集

適用於：  Configuration Manager (最新分支)


這個 FAQ 適用於 IT 系統管理員已將 Windows Defender 或 Endpoint Protection 部署至其受管理電腦的電腦使用者。 這裡的內容可能不適用於其他反惡意程式碼軟體。 Microsoft System Center Endpoint Protection 管理 Windows 10 上的 Windows Defender。 它也可以部署和管理 Windows 10 之前電腦的 Endpoint Protection 用戶端。 雖然本文描述 Windows Defender，但是它的資訊也適用於 Endpoint Protection。  

-   [為什麼需要防毒和反間諜功能軟體？](#why-do-i-need-antivirus-and-antispyware-software)  
-   [如何判斷我的電腦是否遭到惡意軟體感染？](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [如何尋找 Windows Defender 的版本？](#how-can-i-find-the-version-of-windows-defender)
-   [如果 Windows Defender 或 Endpoint Protection 在電腦上偵測到惡意軟體，該怎麼辦？](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [何謂病毒？](#what-is-a-virus)  
-   [何謂間諜軟體？](#what-is-spyware)  
-   [病毒、間諜軟體與其他潛在有害軟體的差異為何？](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [病毒、間諜軟體與其他潛在垃圾軟體來自何處？](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [我可能會收到惡意軟體，而不知情嗎？](#can-i-get-malicious-software-without-knowing-it)  
-   [先檢閱授權合約，再安裝軟體，為何如此重要？](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Endpoint Protection 與 Windows Defender 的差異為何？](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Windows Defender 為什麼偵測不到 Cookie?](#why-doesnt-windows-defender-detect-cookies)  
-   [如何防止惡意程式碼？](#how-can-i-prevent-malware)  
-   [什麼是病毒和間諜軟體定義？](#what-are-virus-and-spyware-definitions)  
-   [如何讓病毒和間諜軟體定義保持最新狀態？](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [如何移除或還原 Windows Defender 或 Endpoint Protection 已隔離的項目？](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [何謂即時保護？](#what-is-real-time-protection)  
-   [如何得知 Windows Defender 或 Endpoint Protection 正在電腦上執行？](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [如何設定 Windows Defender 或 Endpoint Protection 警示？](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>為什麼需要防毒和反間諜功能軟體？  

 務必確認電腦上有保護電腦免受惡意軟體威脅的軟體。 惡意軟體包含病毒、間諜軟體或其他潛在垃圾軟體，會在您連線到網際網路的任何時候嘗試安裝在電腦上。 此外，也會在您使用 CD、DVD 或其他卸除式媒體安裝程式時感染電腦。 惡意軟體也會程式化，在非預期的時間執行，而不只是在安裝時執行。  

 Windows Defender 或 Endpoint Protection 提供三種協助防止惡意軟體感染電腦的方式：  

-   **使用即時防護** - 即時防護能讓 Windows Defender 隨時監控電腦，並在惡意軟體 (包括病毒、間諜軟體或其他潛在垃圾軟體) 嘗試在電腦上安裝或執行時發出警示。 然後，Windows Defender 會暫停軟體，並讓您依照軟體建議執行或執行其他動作。

-   **掃描選項** - 您可以使用 Windows Defender 掃描潛在威脅，例如病毒、間諜軟體和其他可能讓電腦面臨風險的惡意軟體。 您也可以使用它排程定期掃描，以及移除掃描期間偵測到的惡意軟體。  

-   **Microsoft Active Protection Service 社群** - 線上 Microsoft Active Protection Service 社群可協助您了解其他人如何回應還沒有進行風險分類的軟體。 您可以利用社群上的資訊協助您選擇是否要在電腦上允許此軟體執行。 相對的，如果您加入社群，您的選擇也會新增至社群分級，協助其他人採取因應的動作。  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>如何判斷我的電腦是否遭到惡意軟體感染？  

 您的電腦上可能有某種形式的惡意軟體 (包含病毒、間諜軟體或其他潛在垃圾軟體)，如果：  

-   您注意到未刻意新增到網頁瀏覽器的新工具列、連結或我的最愛。  

-   您的首頁、滑鼠指標或搜尋程式未預期地變更。  

-   您輸入特定站台 (例如搜尋引擎) 的位址，但將您帶到不同的網站，而未先行通知。  

-   從您的電腦自動刪除檔案。  

-   您的電腦用來攻擊其他電腦。  

-   即使您不是在網際網路上，還是會看到快顯廣告。  

-   您電腦的執行速度突然變得比平常慢。 並非所有電腦效能問題都是惡意軟體所造成，但是惡意軟體 (特別是間諜軟體) 可能會導致明顯地變化。  

即使看不到任何徵兆，您的電腦上可能還是有惡意軟體。 這類型的軟體可以在您不知道或未同意的情況下收集有關您和您電腦的資訊。 為了協助保護您的隱私權和電腦，您應該隨時都執行 Windows Defender 或 Endpoint Protection。  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>如何尋找 Windows Defender 的版本？
 若要檢視在電腦上執行之 Windows Defender 的版本，請開啟 Windows Defender (按一下 [啟動]  ，然後搜尋 **Windows Defender**)，按一下 [設定]  ，再捲動到 Windows Defender 設定的底部以尋找 [版本資訊]  。

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>如果 Windows Defender 或 Endpoint Protection 在電腦上偵測到惡意軟體，該怎麼辦？  

 如果 Windows Defender 偵測到電腦有惡意軟體或潛在垃圾軟體 (在使用即時保護監視電腦時或在執行掃描之後)，則會在螢幕右下角顯示通知訊息，通知您偵測到的項目。  

 通知訊息包含 [ **清理電腦** ] 按鈕，以及用來檢視已偵測到項目之詳細資訊的 [ **顯示詳細資料** ] 連結。 按一下 [顯示詳細資料]  連結開啟 [潛在的威脅詳細資料]  視窗，取得已偵測到項目的詳細資訊。 您現在可以選擇要套用至項目的動作，或按一下 [ **清理電腦**]。 如果您需要判斷何種動作要套用至已偵測到項目的說明，請使用 Windows Defender 指派給項目的警示等級作為指南 (如需詳細資訊，請參閱＜了解警示等級＞)。  

 警示等級可協助您選擇回應病毒、間諜軟體和其他潛在垃圾軟體的方式。 雖然 Windows Defender 建議您移除所有病毒和間諜軟體，但並非所有已加上標幟的軟體都是惡意或垃圾軟體。 下列資訊可協助您決定當 Windows Defender 偵測到電腦上有潛在垃圾軟體時要執行的動作。  

 根據警示等級，您可以選擇下列其中一個動作套用至已偵測到的項目：  

- **移除** - 此動作會從電腦永久刪除軟體。  

- **隔離** - 此動作會隔離軟體，使軟體無法執行。 Windows Defender 隔離軟體時，會將軟體移至電腦上的另一個位置，然後阻止軟體執行，直到您選擇還原或從電腦移除軟體為止。  

- **允許** - 此動作會將軟體加入 Windows Defender 允許清單，並允許在電腦上執行。 Windows Defender 將停止警告您該軟體可能對隱私權或電腦造成的風險。  

  如果您對某個項目 (例如軟體) 選擇 [允許]  ，Windows Defender 會停止顯示軟體可能對隱私權或電腦造成風險的警示。 因此，只有在您信任軟體和軟體發行者時，才將軟體新增至允許清單。  

### <a name="how-to-remove-potentially-harmful-software"></a>如何移除潛在有害軟體

若要快速輕鬆地移除 Windows Defender 偵測到的所有垃圾或可能有害項目，請使用 [清理電腦]  選項。  

1.  當您看到它偵測到潛在威脅之後，於通知區域顯示的通知訊息時，請按一下 [清理電腦]  。  

2.  Windows Defender 會移除潛在威脅，然後在完成清理電腦時通知您。  

3.  若要深入了解已偵測到的威脅，請按一下 [ **歷程記錄** ] 索引標籤，然後選取 [ **全部已偵測到的項目**]。  

4.  如果您沒有看到所有偵測到的項目，請按一下 [ **檢視詳細資料**]。 如果系統提示您輸入系統管理員密碼或確認資訊，請輸入密碼或確認動作。

> [!NOTE]  
>  電腦清理期間，Windows Defender 會盡可能只移除檔案受感染的部分，而不是整個檔案。  

##  <a name="what-is-a-virus"></a>何謂病毒？  
 電腦病毒是軟體程式，故意設計來干擾電腦作業；記錄、損毀或刪除資料；或是感染網際網路上的其他電腦。 病毒通常會讓作業變慢，並在過程中造成其他問題。  

##  <a name="what-is-spyware"></a>何謂間諜軟體？  
 間諜軟體是可以在電腦上自行安裝或執行的軟體，並不需要得到您的同意或提供您足夠的通知或控制權。 間諜軟體在感染您的電腦之後可能不會有任何徵兆，但許多惡意或垃圾程式可能會影響您電腦的執行方式。 例如，間諜軟體可以監視您的線上行為或收集您的資訊 (包括可用來辨識您的資訊或其他機密資訊)、變更您電腦上的設定，或讓電腦執行速度變慢。  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>病毒、間諜軟體與其他潛在有害軟體的差異為何？  
 病毒和間諜軟體是在您不知道的情況下安裝於電腦上，而且兩者可能會干擾並具破壞性。 它們也可以擷取您電腦的相關資訊，並且損毀或刪除該資訊。 它們都會對電腦效能造成負面影響。  

 病毒與間諜軟體的主要差異，在於它們在電腦上的行為。 病毒 (就像現存生物體) 想要感染電腦、複寫，然後盡可能散佈到最多的其他電腦。 不過，間諜軟體更像鼴鼠，它想要「進入」您的電腦且盡可能留在該位置最長的時間，並將電腦的重要資訊傳送到外部來源。  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>病毒、間諜軟體與其他潛在垃圾軟體來自何處？  
 網站、所下載程式或使用 CD、DVD、外接式硬碟或裝置所安裝的程式都可以安裝垃圾軟體 (例如病毒)。 間諜軟體最常透過免費軟體 (例如檔案共用、螢幕保護裝置或搜尋工具列) 進行安裝。  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>我可能會收到惡意軟體，而不知道它嗎？  
 是，可以透過網頁中的內嵌指令碼或程式，從網站安裝部分惡意軟體。 部分惡意軟體需要您的協助才能進行安裝。 這個軟體使用需要您接受可下載檔案的網頁快顯視窗或免費軟體。 不過，如果您具有最新版的 Microsoft Windows®，並且未降低您的安全性設定，則可以將感染的機會降到最低。  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>先檢閱授權合約，再安裝軟體，為何如此重要？  
 當您瀏覽網站時，請不要同意自動下載網站提供的任何項目。 如果您下載免費軟體 (例如檔案共用程式或螢幕保護裝置)，請仔細閱讀授權合約。 請尋找句子，這些句子指出您必須接受公司的廣告和快顯視窗，或軟體會將特定資訊傳回給軟體發行者。  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Endpoint Protection 與 Windows Defender 的差異為何？  
 Endpoint Protection 是一個反惡意程式碼軟體，表示它的設計是偵測並協助保護電腦免於各種惡意軟體 (包括病毒、間諜軟體和其他潛在垃圾軟體)。 Windows Defender (與 Windows 作業系統一起自動安裝) 是偵測並停止間諜軟體的軟體。  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Windows Defender 為什麼偵測不到 Cookie?  
 Cookie 是網站放在您電腦上的小型文字檔，用來儲存您和您喜好設定的資訊。 網站會使用 Cookie 來提供您個人化的體驗，以及收集網站使用資訊。 Windows Defender 偵測不到 Cookie，因為它不會將它們視為對您隱私權或電腦安全性的威脅。 大部分網際網路瀏覽器程式都可讓您封鎖 Cookie。  

##  <a name="how-can-i-prevent-malware"></a>如何防止惡意程式碼？  
 電腦使用者現在的兩個最大考量是病毒和間諜軟體。 在這兩種情況下，雖然這些可能發生問題，但是您只要進行一些規劃，就可以輕鬆地自行防禦它們：  

-   讓您電腦的軟體保持最新，並且記得安裝所有修補程式。 請記得定期更新作業系統。  

-   請確定您的防毒和反間諜軟體 (Windows Defender) 使用潛在威脅的最新更新 (請參閱＜如何讓病毒和間諜軟體定義保持最新狀態？＞)。 也請確定您一律使用最新版的 Windows Defender。  

-   僅從信譽良好的來源下載更新。 針對 Windows 作業系統，請一律移至 [Microsoft Update 目錄](https://catalog.update.microsoft.com) \(英文\)。  針對其他軟體，請一律使用生產該軟體之公司或人員的合法網站。

-   如果您收到內含附件的電子郵件，但不確定來源，則應該立即予以刪除。 請不要從不明來源下載任何應用程式或檔案，而且與其他使用者交易檔案時請小心。  

-   安裝並使用防火牆。 建議您啟用 Windows 防火牆。  

##  <a name="what-are-virus-and-spyware-definitions"></a>什麼是病毒和間諜軟體定義？  
 當您使用 Windows Defender 或 Endpoint Protection 時，它一定要有最新的病毒和間諜軟體定義。 定義為檔案，其行為類似不斷成長之潛在軟體威脅的百科全書。 Windows Defender 或 Endpoint Protection 會使用定義來判斷它偵測到的軟體是病毒、間諜軟體還是其他潛在垃圾軟體，然後在出現潛在風險時發出警示。 為了協助具有定義的最新資訊，Windows Defender 或 Endpoint Protection 會與 Microsoft Update 搭配運作，以在新定義發行時自動進行安裝。 您也可以設定 Windows Defender 或 Endpoint Protection 先線上檢查已更新的定義，再進行掃描。  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>如何讓病毒和間諜軟體定義保持最新狀態？  
 病毒和間諜軟體定義是作為已知惡意軟體 (包括病毒、間諜軟體和其他潛在垃圾軟體) 百科全書的檔案。 因為不斷有人開發惡意軟體，所以 Windows Defender 或 Endpoint Protection 依賴最新定義來判斷嘗試在電腦上安裝、執行，或變更設定的軟體是病毒、間諜軟體還是其他潛在垃圾軟體。  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>先自動檢查新的定義，再進行排定的掃描 (建議)  

1.  按一下通知區域中的圖示，或從 [開始]  功能表中啟動 Windows Defender 或 Endpoint Protection 用戶端，即可開啟 Windows Defender 或 Endpoint Protection 用戶端。  

2.  按一下 [設定]  ，然後按一下 [排定的掃描]  。  

3.  請確定已選取 [在執行排定的掃描前，檢查最新的病毒及間諜軟體定義]  核取方塊，然後按一下 [儲存變更]  。 如果系統提示您輸入系統管理員密碼或確認資訊，請輸入密碼或確認動作。  

### <a name="to-check-for-new-definitions-manually"></a>手動檢查新的定義

 Windows Defender 或 Endpoint Protection 會自動更新電腦上的病毒和間諜軟體定義。 如果超過七天尚未更新定義 (例如，如果一週未開啟您的電腦)，則 Windows Defender 或 Endpoint Protection 會通知您定義已過期。  

1.  按一下通知區域中的圖示，或從 [開始]  功能表中啟動 Windows Defender 或 Endpoint Protection 用戶端，即可開啟 Windows Defender 或 Endpoint Protection 用戶端。  

2.  若要手動檢查新的定義，請按一下 [更新]  索引標籤，然後按一下 [更新定義]  。  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>如何移除或還原 Windows Defender 或 Endpoint Protection 已隔離的項目？  

 Windows Defender 或 Endpoint Protection 隔離軟體時，會將軟體移至電腦上的另一個位置，然後阻止軟體執行，直到您選擇還原或從電腦移除軟體為止。  

 在此程序提及的所有步驟中，如果系統提示您輸入系統管理員密碼或確認資訊，請輸入密碼或提供確認資訊。  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>移除或還原 Windows Defender 或 Endpoint Protection 已隔離的項目


1.  按一下 [歷程記錄]  索引標籤，並選取 [已隔離的項目]  ，然後選取 [已隔離的項目]  選項。  

2.  按一下 [檢視詳細資料]  查看所有項目。  

3.  檢閱每個項目，然後針對每個項目按一下 [ **移除** ] 或 [ **還原**]。 如果要從電腦移除所有已隔離的項目，請按一下 [ **全部移除**]。  

##  <a name="what-is-real-time-protection"></a>何謂即時保護？  

 即時保護可讓 Windows Defender 隨時監視電腦，並在潛在威脅 (例如病毒和間諜軟體) 嘗試在電腦上自行安裝或執行時發出警示。 因為這項功能是 Windows Defender 協助保護您電腦之方式的重要項目，所以您應該確定一律開啟即時保護。 如果關閉了即時保護，Windows Defender 就會通知您，並將電腦的狀態變更為**危險**。  

 只要即時保護偵測到威脅或潛在威脅，Windows Defender 就會顯示通知。 您現在可以選擇下列選項：  

- 按一下 [清理電腦]  移除偵測到的項目。 Windows Defender 將自動從電腦移除該項目。  

- 按一下 [顯示詳細資料]  連結以顯示 [潛在的威脅詳細資料] 視窗，然後選擇要套用至偵測到項目的動作。  

  您可以選擇想要 Windows Defender 監視的軟體和設定，但建議您開啟即時保護，並啟用所有即時保護選項。 下表說明可用選項。  

|||  
|-|-|  
|**即時保護選項**|**目的**|  
|掃描所有下載|這個選項會監視所下載的檔案和程式，包括透過 Windows Internet Explorer 和 Microsoft Outlook® Express (例如 ActiveX ® 控制項和軟體安裝程式) 自動下載的檔案。 瀏覽器本身可以下載、安裝或執行這些檔案。 這些檔案可能包含惡意軟體 (包括病毒、間諜軟體和其他潛在垃圾軟體)，並在您不知道的情況下進行安裝。<br /><br /> 使用即時保護選項，Windows Defender 會隨時監視您的電腦，並檢查是否有任何您可能已下載的惡意檔案或程式。 這個監視功能表示 Windows Defender 不會因要求檢查您可能要下載的任何檔案或程式，而減慢瀏覽或電子郵件經驗。|  
|監視電腦上的檔案和程式活動|這個選項會監視檔案和程式何時開始在電腦上執行，然後將其執行的任何動作以及對其採取的動作發出警示給您。 這十分重要，因為惡意軟體可以在您不知道的情況下使用已安裝程式中的弱點來執行惡意或垃圾軟體。 例如，在您啟動經常使用的程式時，間諜軟體可以自行在背景執行。 Windows Defender 會監視您的程式，並在偵測到可疑活動時發出警示。|  
|啟用行為監視|這個選項可監視傳統防毒偵測方法可能偵測不到的可疑模式行為集合。|  
|啟用網路檢查系統|這個選項可協助保護您的電腦不受已知弱點的「零時差」漏洞攻擊，進而減少發現到弱點時與套用更新時之間的時間範圍。|  

### <a name="to-turn-off-real-time-protection"></a>開啟即時保護  

1.  按一下 [ **設定**]，然後按一下 [ **即時防護**]。  

2.  清除您要關閉的即時保護選項，然後按一下 [儲存變更]  。 如果系統提示您輸入系統管理員密碼或確認資訊，請輸入密碼或確認動作。  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>如何得知 Windows Defender 或 Endpoint Protection 正在電腦上執行？  

 在電腦上安裝 Windows Defender 之後，即可關閉主要視窗，並讓 Windows Defender 在背景安靜地執行。 Windows Defender 將繼續在電腦上執行及監視，並協助防範威脅。  

 當然，Windows Defender 在通知區域中顯示通知訊息時，即表示它正在執行。 這些通知代表 Windows Defender 已偵測到潛在威脅的警示。  

 此外，您也會收到其他警示通知，例如，如果由於某些原因即時防護已關閉、或者病毒及間諜軟體定義檔已經好多天未更新，或者有可用的程式升級時。 Windows Defender 也會短暫顯示通知，告知您它正在掃描電腦。  

> [!TIP]
> 
> 如果在通知區域看不到 Windows Defender 圖示，則按一下通知區域中的箭號，即可顯示隱藏的圖示 (包括 Windows Defender 圖示)。  


 圖示色彩取決於電腦的目前狀態：  

-   綠色表示電腦狀態是「受保護」。  

-   黃色表示電腦狀態是「可能未受保護」。  

-   紅色表示電腦狀態是「有風險」。  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>如何設定 Windows Defender 或 Endpoint Protection 警示？  
 在電腦上執行 Windows Defender 時，如果偵測到病毒、間諜軟體或其他潛在垃圾軟體，它會自動發出警示。 您也可以設定 Windows Defender 在您執行尚未分析的軟體時以及軟體變更電腦設定時，發出警示。  

### <a name="to-set-up-alerts"></a>設定警示  

1.  按一下 [ **設定**]，然後按一下 [ **即時防護**]。  

2.  確定已選取 [ **開啟即時防護 (建議)** ] 核取方塊。  

3.  選取您要執行之即時防護選項旁邊的核取方塊，然後按一下 [ **儲存變更**]。 如果系統提示您輸入系統管理員密碼或確認資訊，請輸入密碼或確認動作。  

### <a name="see-also"></a>請參閱  
 [Windows Defender 或 Endpoint Protection 用戶端疑難排解](troubleshoot-endpoint-client.md)   

 [Endpoint Protection 用戶端說明](endpoint-protection-client-help.md)
