---
title: UUP 預覽
titleSuffix: Configuration Manager
description: UUP 整合預覽的指示
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702936"
---
# <a name="uup-private-preview-instructions"></a>UUP 個人預覽指示

> [!Note]  
> 這項資訊與預覽功能相關，可能會在正式發行之前進行大幅修改。 Microsoft 對於此處提供的資訊不做任何明示或暗示保證。  

## <a name="introduction"></a>簡介

Unified Update Platform (UUP) 是一種封裝和發佈平台，可供消費型裝置和企業裝置用來接收商務用 Windows Update 所發佈的更新。 UUP 個人預覽版計畫的適用客戶，必須已同意協助 Microsoft 驗證 UUP 更新在 Configuration Manager 中的使用情形，以協助解決客戶目前向服務 Windows 回報的問題。 這些更新目前並未公開推出。

如需 UUP 的詳細資訊，請參閱以下 Windows 部落格文章：[Unified Update Platform (UUP) 上的更新](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/)。

## <a name="benefits"></a>優點

Windows 10 UUP 功能與累積更新可協助解決客戶目前向服務 Windows 回報的多個問題。

### <a name="feature-updates"></a>功能更新

- 透過 UUP 功能更新，Windows 更新處理序可保留功能隨選 (FOD) 和語言套件。

- 直接更新為最新的安全性合規性層級。 您不需要在功能更新之後立即安裝安全性更新。 Microsoft 每個月都會發佈新的功能更新與最新的累積安全性更新。 您不需要每個月下載或散發大部分的功能更新內容。 您只需要下載 UUP 向累積更新分享的安全性更新。

### <a name="cumulative-updates"></a>累積更新

- 含 UUP 的累積更新包含服務堆疊更新 (SSU) 及每月的累積安全性更新。 此行為可解決協調這兩個更新的困難。 其可確保服務堆疊更新已準備就緒，而可安裝累積更新。 您不需要管理和協調這些關聯性。

- UUP 的累積更新可讓您離線散發 FOD 和語言套件內容。 此行為可讓使用者視需要加以新增。 使用者不需要從網際網路下載，您也不需要了解如何預先設置此內容。

## <a name="set-up"></a>設定

### <a name="1-send-your-wsus-id-to-microsoft"></a>1.將 WSUS 識別碼傳送給 Microsoft

若要參與 UUP 個人預覽版，請與 UUP 預覽連絡人分享您的 WSUS 識別碼。 Microsoft 會核准您的 WSUS 環境進入 UUP 預覽計畫。 若無此識別碼，您將無法取得任何 UUP 更新，直到預覽成為公開版本。

若要取得 WSUS 識別碼，請執行下列 PowerShell 指令碼：

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

**MUUrl** 屬性應為 `https://sws.update.microsoft.com`。 若要予以變更，請參閱以下支援文章中的解決方法：[WSUS 同步處理失敗，且出現 SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)。

### <a name="2-update-configuration-manager"></a>2.更新 Configuration Manager

對您的 Configuration Manager 站台進行下列變更，以支援此 UUP 預覽：

#### <a name="diagnostics-and-usage-data-level"></a>診斷和使用方式資料層級

請考慮在此預覽期間增加 Configuration Manager 診斷及資料使用方式層級。 **完整**層級可協助 Microsoft 使用此新功能更佳地針對問題進行分析及疑難排解。 如需詳細資訊，請參閱 [1906 版的診斷使用方式資料收集層級](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md)。

#### <a name="install-the-latest-update"></a>安裝最新的更新

1. 使用下列其中一個更新來更新網站：

    - 版本 1902 與[更新彙總套件](https://support.microsoft.com/help/4500571)
    - [1906 版](../../core/servers/manage/checklist-for-installing-update-1906.md)

    如需詳細資訊，請參閱[安裝主控台內的更新](../../core/servers/manage/install-in-console-updates.md)。

2. 更新用戶端。  

    - 如果要簡化此程序，請考慮使用自動用戶端升級。 如需詳細資訊，請參閱[升級用戶端](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。  

    - *不必要地下載大約 6 GB* 的未使用內容至用戶端，請針對更新您要安裝 UUP 更新的所有用戶端。

### <a name="3-update-windows-clients-to-a-supported-version"></a>3.將 Windows 用戶端更新為支援的版本

若要成功安裝 UUP 更新，請同時安裝下列更新：

1. 特定最小累積每月合規性層級。

2. Microsoft Update Catalog 所發佈的特定非累積、非安全性更新。 若要將更新匯入至 Configuration Manager 以供部署，請參閱[從 Microsoft Update Catalog 匯入更新](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)。

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>支援的 Windows 10 版本和必要的更新

| Windows 10 版本 | 最低合規性層級 | 其他類別目錄更新 |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10 1903 版** | RTM | 2019 年 11 月 7 日，[KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10 1809 版** | 2019 年 8 月，[KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 2019 年 11 月 7 日，[KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10 1803 版** | 2019 年 4 月，[KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 2019 年 11 月 7 日，[KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10 1709 版** | 2019 年 4 月，[KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 2019 年 11 月 7 日，[KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - 如果您先將 2019 年 11 月 12 日更新套用至用戶端，然後才套用 2019 年 11 月 7 日的額外類別目錄更新，則為了支援 UUP 所需的 Windows Update 代理程式變更會遭到覆寫。 若要對該案例下的用戶端進行補救，請在安裝 2019 年 11 月 12 日更新後，套用額外的類別目錄更新。
> - 如果您將功能更新套用至用戶端，則必須在升級完成後，重新安裝額外的類別目錄更新。
> - 若要讓功能更新的測試變得更容易，請將更新匯入至 Configuration Manager。 如需詳細資訊，請參閱[從 Microsoft Update Catalog 匯入更新](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)。 功能更新完成後，額外的類別目錄更新便會顯示為**必要**，而讓您自動部署到上層作業系統版本。

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4.讓用戶端得以在提供差異內容時，進行下載

若要正確下載 UUP 更新，請將用戶端設定啟用為 [讓用戶端得以在提供差異內容時，進行下載]  。 Configuration Manager 可透過此設定讓 Windows Update 代理程式 (WUA) 決定要下載至用戶端的必要內容。 此行為可代替預設值，亦即 Configuration Manager 用戶端會下載所有與 UUP 更新相關聯的內容。 當您啟用此設定時，WUA 會決定每個 UUP 更新所需的其他內容。 例如，只需要必要的 FOD 和語言套件。

啟用此設定時並不會影響從網際網路下載的伺服器內容。 此設定僅適用於用戶端的下載。 將 UUP 更新部署至用戶端之前，請先將此設定套用至符合所支援 UUP 版本的用戶端。 先決條件用戶端更新會修正 WSUS 和 Configuration Manager 中的 UUP 更新相容性問題。

如需有關此用戶端設定的詳細資訊，請參閱[關於用戶端設定 - 軟體更新](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)。

### <a name="5-review-your-software-update-infrastructure"></a>5.檢閱軟體更新基礎結構

同步處理 UUP 更新之前，請先檢閱自動部署規則 (ADR) 和服務方案。 如果您不想要自動部署這些更新，請修改 ADR 以將其篩選掉。如需詳細資訊，請參閱[如何尋找同步的 UUP 更新](#how-to-find-synced-uup-updates)。 根據預設，現有的服務方案只會部署非 UUP 的更新。 您可以修改服務方案來變更此行為。

檢閱合規性報告，並視需要進行修訂。 例如，如果您測量所有產品的合規性，則現在您會同時看到 UUP 和非 UUP 累積更新。 裝置會針對這兩種類型的更新來報告合規性。 請確定合規性報告可因應此變更。

## <a name="enable-uup-and-start-testing"></a>啟用 UUP 並開始測試

### <a name="select-products-and-classifications-to-sync"></a>選取產品和分類以進行同步

當您準備好開始同步處理 UUP 更新，而且 Microsoft 已核准您的 WSUS 識別碼之後，請啟用新產品：

1. [同步軟體更新](../get-started/synchronize-software-updates.md)以填寫新產品。  

2. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。

3. 選取您的頂層站台，它可以是管理中心網站 (CAS) 或獨立主要站台。

4. 在功能區中，選取 [設定站台元件]  ，然後選擇 [軟體更新點]  。

5. 切換至 [產品]  索引標籤，然後選取下列一或多項產品： 

    - **Windows 10 UUP 預覽**
    - **Windows Server UUP 預覽**

6. 切換至 [分類]  索引標籤，然後選取下列選項：  

    - **安全性更新**：查看 UUP 累積更新  
    - **升級**：查看 UUP 功能更新  

7. 再次同步軟體更新以查看新的 UUP 更新。

### <a name="how-to-find-synced-uup-updates"></a>如何尋找同步的 UUP 更新

將 UUP 更新同步處理至環境後，請在 Configuration Manager 主控台中找到這些更新以便進行測試。 有兩種方式可找到預覽更新：

- 由於這些預覽更新位於個別的產品中，因此請使用產品來篩選以尋找這些更新。 使用服務方案的產品篩選條件來部署 UUP 或非 UUP 功能更新。  

- 在 [軟體程式庫]  節點的 [所有軟體更新]  與 [所有 Windows 10 更新]  中，有一個新的選擇性欄 [標籤]  。 這個屬性也可以作為 ADR 中的篩選條件。 針對 UUP 更新，請在此欄位中搜尋 `UUP`。 針對非 UUP 更新，則為空白。  

### <a name="updates-available-during-preview"></a>預覽期間可用的更新

如需 Microsoft 所發行的所有 Windows 10 更新詳細資訊，請參閱 [Windows 10 版本資訊](https://docs.microsoft.com/windows/release-information/)。

#### <a name="cumulative-updates-to-test"></a>要測試的累積更新

雖然您可能會看到多個有 UUP 標籤的更新可供使用，但請從 **2019 年 9 月** (2019-09) 更新或更新版本來開始。 例如：

- 適用於 Windows 10 1809 版 (x64 型系統) 的 2019-09 累積更新 (KB4512578)
- 適用於 Windows 10 1803 版 (x64 型系統) 的 2019-09 累積更新 (KB4516058)
- 適用於 Windows 10 1709 版 (x64 型系統) 的 2019-09 累積更新 (KB4516066)

#### <a name="feature-updates-to-test"></a>要測試的功能更新

雖然您可能會看到多個有 UUP 標籤的更新可供使用，但請從 **2019 年 9 月** (2019-09B) 更新或更新版本來開始。 例如：

- Windows 10 1809 版 x64 2019-09B 的功能更新
- Windows 10 1803 版 x64 2019-09B 的功能更新

## <a name="scenarios-to-test"></a>要測試的案例

### <a name="test-feature-updates"></a>測試功能更新

- 直接更新為您選擇的安全性合規性層級  

- 請先安裝 FOD 和語言套件，再安裝更新。 請確定更新有保留這些元件。  

### <a name="test-cumulative-updates"></a>測試累積更新

在預覽期間，請為多個連續更新使用 UUP 類型更新，讓用戶端保持符合規範。 這項測試可協助您了解進行中的行為。

### <a name="test-content"></a>測試內容

每個主要版本 (1809、1803、1709)、架構和語言組合的第一個更新會顯得很大。 這個大小同時顯現在檔案和磁碟空間的數目上 (相較於您先前在非 UUP 更新中看到的數目)。 此額外內容主要針對所有 FOD 和語言套件的累積更新。 針對功能更新，該第一個更新會有其他大型內容。

針對未來的累積更新和功能更新，網站所下載和散發的新內容數量則會小很多。 UUP 會有智慧地在更新之間共用所有 FOD 和語言套件內容。 您不需要重新下載或重新散發此共用內容。 在預覽期間，Windows 10 1709 和 1803 版的這個每月下載大小，會與非 UUP 案例中的累積更新大小差不多。 在 Windows 10 1809 版和更新版本中，累積更新的每月累加下載則會小很多。

當您查看為期 12個月的期間所下載和散發的*非快速*內容總數時，沒有 UUP 的 Windows 10 1803 版大小應該會與有 UUP 的 1809 版大小差不多。 在有 UUP 的 1809 版中，整個發行生命週期內所下載和散發的內容總數則會較小。

### <a name="supported-content-channels"></a>支援的內容通道

請在預覽版中測試您的一般真實案例。 UUP 會支援所有內容通道，包括：

- Windows 傳遞最佳化 (DO)
  - 使用 DO 時，請確定其設定正確。 如需詳細資訊，請參閱[將 Windows 10 更新傳遞最佳化](optimize-windows-10-update-delivery.md)。
- Configuration Manager 對等快取
- Windows BranchCache
- 使用 [無部署套件]  選項，而且用戶端會直接從 Microsoft Update 下載。 請使用此選項來搭配傳遞最佳化。
- 協力廠商替代內容提供者

如需內容通道的詳細資訊，請參閱[將 Windows 10 更新傳遞最佳化](optimize-windows-10-update-delivery.md)。

<!-- TODO: Addlink to WSUS Perf documentation-->
