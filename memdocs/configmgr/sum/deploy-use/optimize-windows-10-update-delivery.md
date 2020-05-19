---
title: 將 Windows 10 更新傳遞最佳化
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 來管理更新內容，讓 Windows 10 隨時保持最新狀態。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 835dcd0c86244c1731cb6c6e040d577160759614
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83267785"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>使用 Configuration Manager，將 Windows 10 更新傳遞最佳化

適用於：Configuration Manager (最新分支)

對很多客戶而言，使用 Configuration Manager 並套用適當的內容發佈策略，便能成功掌握最新的 Windows 10 每月更新。 對於大型組織而言，每月品質更新的大小乃是潛在的問題。 目前有一些技術能有效減少頻寬和網路負載，以將更新傳遞最佳化。 本文將介紹並比較這些技術及提供各種建議，以協助您決定要採用的技術。  
 
Windows 10 提供幾種更新類型。 如需詳細資訊，請參閱[商務用 Windows Update 中的更新類型](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business)。 本文重點介紹 Windows 10「品質」更新與 Configuration Manager 搭配使用。 


## <a name="express-update-delivery"></a>快速更新傳遞

Windows 10 品質更新下載可能會很龐大。 每個套件都包含所有以前發佈的修正，以確保一致性和簡單性。 Microsoft 已經能夠透過稱為「快速」的功能，減少每個用戶端下載的 Windows 10 更新內容大小。 如今，已經有數百萬台裝置利用「快速」功能，直接從 Windows Update 服務中提取更新，因而大幅減少了下載大小。 對於未直接從 Windows Update 服務下載的客戶，同樣享有這種優點。 

Configuration Manager 已能支援 Windows 10 品質更新版本 1702 的[快速安裝檔案](manage-express-installation-files-for-windows-10-updates.md)。 不過，為了獲得最佳體驗，建議您使用 Configuration Manager 版本 1802 或更新的版本。 為了實現最快的下載速度，也建議您使用 Windows 10 1703 版或更新的版本。 

> [!NOTE]  
> 快速版本內容比完整檔案版本大得多。 快速安裝檔案包含各個所要更新檔案的所有可能變體。 因此，當您在 Configuration Manager 中啟用快速支援時，更新套件來源裡面的更新以及發佈點上的更新，其所需的磁碟空間量會增加。 雖然發佈點所需的磁碟空間會增加，但用戶端從這些發佈點下載的內容大小反而會減少。 用戶端只是下載它們需要的部分 (差異)，不會下載整個更新。


## <a name="peer-to-peer-content-distribution"></a>點對點內容發佈

即使用戶端只下載所需要的內容部分，也可以利用點對點內容發佈，以加快環境中的 Windows 更新。 在某些環境中，遠端辦公室沒有本機發佈點，這時候將同儕節點當作品質更新的下載來源便會有優勢。 採用這種做法之後，所有用戶端就不必都透過慢速 WAN 連結從遠端發佈點下載內容。 當用戶端因故回到備用的 Windows Update 服務時，使用同儕節點也會有優勢。 只要有一個同儕節點從雲端下載更新內容，之後就可以將更新內容提供給其他裝置。

Configuration Manager 支援很多點對點技術，包括：
- Windows 傳遞最佳化
- Configuration Manager 對等快取
- Windows BranchCache  

後續小節將提供這些技術的詳細資訊。

### <a name="windows-delivery-optimization"></a>Windows 傳遞最佳化

[傳遞最佳化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是 Windows 10 內建的主要下載技術和點對點發佈方法。 如果區域網路的其他裝置已經下載相同的更新，Windows 10 用戶端便可以從這些裝置取得內容。 使用[傳遞最佳化可用的 Windows 選項](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options)時，您可以將用戶端分成不同的群組。 組織利用這種分組方法可以找出能完成點對點要求的最佳候選裝置。 「傳遞最佳化」能大幅降低讓裝置保持最新狀態所需的總體頻寬，還可以縮短下載時間。

> [!NOTE]  
> 「傳遞最佳化」是一種雲端管理解決方案。 若要使用「傳遞最佳化」的點對點功能，必須要能透過網際網路連線至「傳遞最佳化」雲端服務。 如需所必要網際網路端點的資訊，請參閱[傳遞最佳化的常見問題集](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。 

為了獲得最佳效果，您可能需要將「傳遞優化」[下載模式](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#download-mode)設定為**群組 (2)** 並定義「群組識別碼」。 在群組模式中，對等互連可以讓同一群組中的不同裝置 (包含遠端辦公室的裝置) 跨越內部子網路。 使用[群組識別碼](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids)選項，以建立與網域和 AD DS 站台無關的自訂群組。 對於大部分組織而言，若要透過「傳遞最佳化」實現頻寬最佳化，建議使用群組下載模式的選項。

當用戶端在不同網路中漫遊時，手動設定這些群組識別碼很麻煩。 Configuration Manager 版本 1802 增加了一個新功能，能[使用傳遞最佳化來整合界限群組](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)，以簡化此流程的管理。 當用戶端喚醒之後，會與其管理點進行溝通以取得原則，然後提供其網路和界限群組資訊。 Configuration Manager 會為每個界限群組建立獨一無二的識別碼。 站台會使用用戶端的位置資訊，以 Configuration Manager 界限識別碼來自動設定用戶端的「傳遞最佳化群組識別碼」。 當用戶端漫游到另一個界限群組時，便會與其管理點進行溝通，然後以新的界限群組識別碼來自動重新設定。 藉由此種整合，「傳遞最佳化」便可以利用 Configuration Manager 界限群組資訊來尋找可以從中下載更新的同儕節點。

### <a name="delivery-optimization-starting-in-version-1910"></a><a name="bkmk_DO-1910"></a> 傳遞最佳化 (從 1910 版開始)
<!--4699118-->
從 Configuration Manager 1910 版起，您可以使用「傳遞最佳化」來散發執行 Windows 10 1709 版或更新版本用戶端的所有 Windows 更新內容，而不是只有快速安裝檔案。

若要為所有 Windows 更新安裝檔案使用「傳遞最佳化」，請啟用下列[軟體更新用戶端設定](../../core/clients/deploy/about-client-settings.md#software-updates)：

- 將 [讓用戶端得以在提供差異內容時，進行下載] 設定為 [是]。
- 將 [用戶端用於接收差異內容要求的連接埠] 設定為 8005 (預設) 或自訂連接埠號碼。

> [!IMPORTANT]
> - 傳遞最佳化必須啟用 (預設值)，而非略過。 如需詳細資訊，請參閱 [Windows 傳遞最佳化參考](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-reference) \(部分機器翻譯\)。
> - 當您針對差異內容變更[軟體更新用戶端設定](../../core/clients/deploy/about-client-settings.md#software-updates)時，請驗證您的[傳遞最佳化用戶端設定](../../core/clients/deploy/about-client-settings.md#delivery-optimization)。
> - 如果啟用 Office COM，傳遞最佳化無法用於 Office 365 用戶端更新。 Configuration Manager 使用 Office COM 來管理 Office 365 用戶端的更新。 您可以取消註冊 Office COM，以允許為 Office 365 更新使用傳遞最佳化。 停用 Office COM 時，Office 365 的軟體更新是由預設的 Office 自動更新2.0 排程工作所管理。 這表示 Configuration Manager 不會聽寫或監視 Office 365 更新的安裝程序。 Configuration Manager 將會繼續從硬體清查收集資訊，以在主控台中填入 Office 365 用戶端管理儀表板。 如需有關如何取消註冊 Office COM 的詳細資訊，請參閱[啟用 Office 365 用戶端以透過 Office CDN 而非 Configuration Manager 接收更新](https://docs.microsoft.com/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager)。
> - 針對內容儲存體使用 CMG 時，如果已啟用 [下載可用的差異內容] [用戶端設定](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)，第三方更新的內容將不會下載至用戶端。 <!--6598587-->


### <a name="configuration-manager-peer-cache"></a>Configuration Manager 對等快取

[對等快取](../../core/plan-design/hierarchy/client-peer-cache.md)是 Configuration Manager 的一種功能，可讓用戶端直接從其本機 Configuration Manager 快取來分享其他用戶端內容。 對等快取不會取代 Windows BranchCache 之類的其他對等快取解決方案。 它會與其他這些解決方案搭配使用來提供更多的選項，以擴充傳統內容部署解決方案，例如發佈點。 對等快取不需要 BranchCache。 如果您未啟用或使用 BranchCache，則對等快取仍能運作。

> [!NOTE]  
> 用戶端只能從其目前界限群組中的對等快取用戶端下載內容。  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) 是 Windows 的一種頻寬最佳化技術。 每一個用戶端都有一個快取，可充當內容的替代來源。 同一網路上的裝置都可以要求此內容。 [Configuration Manager 可以使用 BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) 來允許同儕節點互相提供內容，而不需要一律都透過發佈點。 使用 BranchCache 時，檔案會快取至個別的用戶端上，其他用戶端可以在需要擷取這些檔案。 這個方法會分散快取，而不是安排一個單一的擷取點。 這種做法可節省大量頻寬，同時讓用戶端可以更快收到要求的內容。



## <a name="selecting-the-right-peer-caching-technology"></a>選擇正確的對等快取技術

為快速安裝檔案選取正確的對等快取技術，取決於您的環境和各項需求。 儘管 Configuration Manager 支援所有上述點對點技術，但您還是應該使用對環境最合適的技術。 對於大多數客戶而言，假設用戶端能滿足「傳遞最佳化」的網際網路需求，那麼 Windows 10 內建的對等快取功能搭配「傳遞最佳化」應該足夠了。 如果您的用戶端無法滿足這些網際網路需求，請考慮使用 Configuration Manager 對等快取功能。 如果您目前將 BranchCache 與 Configuration Manager 搭配使用，且滿足您的所有需求，那麼快速檔案搭配 BranchCache 或許是正確的選擇。 

### <a name="peer-cache-comparison-chart"></a>對等快取比較圖


| 功能  | 傳遞最佳化  | 對等快取  | BranchCache  |
|---------|---------|---------|---------|
| 支援跨子網路 | 是 | 是 | 否 |
| 頻寬節流設定 | 是 (原生) | 是 (透過 BITS) | 是 (透過 BITS) |
| 部分內容支援 | 是，適用於此欄的下一列中所列的所有支援內容類型。 | 僅適用於 Office 365 和快速更新 | 是，適用於此欄的下一列中所列的所有支援內容類型。 |
| 支援的內容類型 | **透過 ConfigMgr：** </br> - 快速更新 </br> - 所有 Windows 更新 (從 1910 版起)。 這不包括 Office 更新。</br> </br> **透過 Microsoft 雲端：**</br> - Windows 和安全性更新</br> - 驅動程式</br> - Windows 市集應用程式</br> - 商務用 Windows 市集應用程式 | 所有的 ConfigMgr 內容類型，包括在 [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) 下載的映像。 | 所有的 ConfigMgr 內容類型，但映像除外 |
| 磁碟控制的快取大小 | 是 | 是 | 是 |
| 探索同儕節點來源 | 自動 | 手動 (用戶端代理程式設定) | 自動 |
| 同儕節點探索 | 透過「傳遞最佳化」雲端服務 (需要網際網路連線) | 透過管理點 (以用戶端界限群組為基礎) | 多點傳送 |
| 報告 | 是 (使用電腦分析) | ConfigMgr 用戶端資料來源儀表板 | ConfigMgr 用戶端資料來源儀表板 |
| WAN 使用控制 | 是 (原生，可以透過群組原則設定來加以控制) | 界限群組 | 僅子網路支援 |
| 透過 ConfigMgr 管理 | 部分 (用戶端代理程式設定) | 是 (用戶端代理程式設定) | 是 (用戶端代理程式設定) |



## <a name="conclusion"></a>結論

Microsoft 建議您根據需要，將 Configuration Manager 與快速安裝檔案以及快取技術搭配使用，以便讓 Windows 10 品質更新傳遞最佳化。 針對 Windows 10 裝置下載大量內容來安裝品質更新的狀況，此方法應該能夠解決所遇到的各種難題。 另外也建議每月部署品質更新，讓 Windows 10 裝置保持最新的狀態。 這種做法會減少裝置每月所需的品質更新內容差異。 減少這種內容差異，會使得從發佈點或同儕節點來源下載較少的內容。 

由於快速安裝檔案的本質，其內容大小比傳統獨立式檔案大得多。 這種大小會導致要花更長的時間從 Windows Update 服務下載更新到 Configuration Manager 站台伺服器。 站台伺服器和發佈點所需的磁碟空間量也會增加。 下載和散發品質更新所需的總時間可能會更長。 但是，在 Windows 10 裝置下載和安裝品質更新的時候，裝置端的各種優點尤為明顯。 如需詳細資訊，請參閱[使用快速安裝檔案](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)?#using-express-installation-files) \(英文\)。

對於較大規模更新，如果權衡伺服器端因素之後而不採用快速支援，但裝置端的各種優點對業務和環境至關重要，則 Microsoft 建議使用[商務用 Windows Update](integrate-windows-update-for-business-windows-10.md) 搭配 Configuration Manager。 商務用 Windows Update 提供「快速」功能的一切優點，但無需在整個環境中下載、儲存和散發快速安裝檔案。 用戶端直接從 Windows Update 服務下載內容，因此仍可使用「傳遞最佳化」。



## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> 常見問題集

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Windows 快速下載如何與 Configuration Manager 搭配使用？

Windows Update 代理程式 (WUA) 會先要求快速內容。 如果安裝快速更新失敗，就會回到備用的完整檔案更新。  

1. Configuration Manager 用戶端會通知 WUA 下載更新內容。 當 WUA 起始快速下載時，首先會下載一個虛設常式 (例如，`Windows10.0-KB1234567-<platform>-express.cab`)，這是快速套件的一部分。  

2. WUA 會將這個虛設常式傳遞給 Windows Update 安裝程式，這是一個以元件為基礎的服務 (CBS)。 CBS 使用虛設常式來比較裝置上檔案與取得目前提供最新版本檔案的差異，以建立本機清查。  

3. CBS 之後會要求 WUA 從一個或多個快速 .psf 檔案下載所需的範圍。  

4. 如果已啟用「傳遞最佳化」且探索到的對等具有所需的範圍，則用戶端將會從與 ConfigMgr 用戶端分開的對等下載。 若已停用「傳遞最佳化」或沒有任何對等具有所需的範圍，則 ConfigMgr 用戶端將會從本機發佈點 (或對等或 Microsoft Update) 下載這些範圍。 範圍會傳遞至 Windows Update 代理程式，這樣讓其可供 CBS 用來套用範圍。


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>快速檔案 (.psf) 儲存在 Configuration Manager 同儕節點上 ccmcache 資料夾中時，為什麼檔案會這麼大？

快速檔案 (.psf) 是疏鬆檔案。 若要確定各個檔案實際使用的磁碟空間，請檢查檔案的**磁碟大小**屬性。 「磁碟大小」屬性應該比「大小值」小得的多。  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Configuration Manager 是否支援快速安裝檔案可與 Windows 10 功能更新搭配使用？

不支援，Configuration Manager 目前僅支援快速安裝檔案可與 Windows 10 品質更新搭配使用。  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>站台伺服器和發佈點上的每個品質更新需要多少磁碟空間？

要看情況而定。 以每個品質更新而言，其完整檔案版本和快速版本都是儲存在伺服務器上。 Windows 10 品質更新是累積的，因此這些檔案的大小每個月都會增加。 每種語言每個更新至少規劃 5 GB 空間。 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>在退回到備用的 Windows Update 服務時，Configuration Manager 用戶端是否仍然可以受益於快速安裝檔案？

是。 如果您使用以下軟體更新部署選項，則用戶端在退回到備用的雲端服務時，仍可使用快速更新和「傳遞最佳化」：  

**如果在目前、鄰近或站台群組的發佈點上找不到軟體更新，則會從 Microsoft Update 下載內容**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>啟用快速檔案支援後，為什麼不會針對現有的更新來下載快速檔案內容？ 

變更只會作用在啟用支援之後所同步和部署的新更新。


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>有沒有辦法了解有多少內容是從同儕節點使用「傳遞最佳化」下載的？
Windows 10，版本 1703 (以及更新的版本) 包括兩個新的 PowerShell Cmdlet：**Get-DeliveryOptimizationPerfSnap** 和 **Get-DeliveryOptimizationStatus**。 這些 Cmdlet 可以提供更深入的「傳遞最佳化」和快取使用情況。 如需詳細資訊，請參閱[適用於 Windows 10 更新的傳遞最佳化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network) \(部分機器翻譯\)


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>用戶端如何透過網路與「傳遞最佳化」通訊？
如需防火牆的網路連接埠、Proxy 需求以及主機名稱的詳細資訊，請參閱[傳遞最佳化的常見問題集](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。

## <a name="log-files"></a>記錄檔

使用下列記錄檔來監視差異下載：

- WUAHandler.log
- DeltaDownload.log

## <a name="next-steps"></a>後續步驟

- [部署軟體更新](deploy-software-updates.md)
- [自動部署軟體更新](automatically-deploy-software-updates.md)
