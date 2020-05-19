---
title: 相容性評定
titleSuffix: Configuration Manager
description: 了解電腦分析中針對 Windows 應用程式和驅動程式的相容性評定。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7b2bff4f8365693c86540c9b0578307340f13a49
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268890"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>電腦分析中的相容性評定

先前解決方案中的升級評定是一般性的，例如：需要注意或有可用的修正。 其不會針對如何優先處理發生問題或包含升級見解的應用程式或驅動程式，提供任何視覺指示器。 電腦分析會以**相容性風險**取代此功能。 電腦分析只會在升級前案例的部署檢視中，顯示應用程式的評定。 其會根據 Microsoft 從包含在目前部署計劃中電腦取得的見解來分類應用程式。

電腦分析會使用下列相容性評定類別：

- **低**：針對 Windows 升級，服務找不到任何可能會將此應用程式置於風險下的訊號。 其可能會在目標 OS 上依照現況運作。

- **中等**：分析指出雖然應用程式可以進行補救，但其功能可能會受到影響。

- **高**：應用程式幾乎確定會在升級期間或升級後失敗。 該應用程式可能需要補救。

- **未知**：未評定應用程式。 其中沒有其他如 *MS 已知問題*或 *Ready for Windows* 等見解。

在部署計劃的應用程式或驅動程式資產清單中，您將會在 [相容性風險] 欄中看到每個資產的此值。

## <a name="app-risk-assessment"></a>應用程式風險評定

![應用程式風險評定來源的圖表](media/app-risk-assessment-sources.png)

電腦分析會運用數種來源，產生應用程式的評定評等：

- [Microsoft 已知問題](#microsoft-known-issues)
- [Ready for Windows](#ready-for-windows)
- [進階見解](#advanced-insights)

您可以在電腦分析中的應用程式上找到每個來源的評定。 在部署計劃中的應用程式資產清單中，請選取個別應用程式來開啟其屬性飛出視窗窗格。 您將會看到整體建議和評定層級。 **相容性風險因素**區段會顯示這些評定的詳細資料。

> [!TIP]
> 如果應用程式詳細資料窗格未顯示相容性評量，可能是因為已將 [應用程式版本詳細資料] 設定為 [關閉]。 預設為關閉，並會合併所有具備相同名稱與發行者的應用程式版本。 此服務仍會針對每個版本進行相容性風險評量。 開啟 [應用程式版本詳細資料]，以查看特定應用程式版本的相容性風險評量。 如需詳細資訊，請參閱[規劃資產](about-deployment-plans.md#plan-assets)。

## <a name="microsoft-known-issues"></a>Microsoft 已知問題

電腦分析會在 Microsoft 應用程式相容性資料庫中尋找任何已知問題。 其會使用此資料庫，判斷 Microsoft 或其他發行者公開提供應用程式的任何現有相容性封鎖。 這項檢查只適用於您所選取部署計劃的目標 OS。

您將會在應用程式屬性窗格上，看到下列問題顯示為 **MS 已知問題**：

### <a name="asset-is-removed-during-upgrade"></a>資產已在升級期間遭到移除

Windows 偵測到應用程式或驅動程式具有相容性問題。 資產不會遷移至新的 OS 版本。 無須採取任何動作，升級也能繼續進行。 請在新的 OS 版本上，安裝應用程式或驅動程式的相容版本。

<!-- 3594545 -->
Windows 可以部分或完全移除這些資產：

- 完全移除：Windows 安裝會在升級期間，從裝置完全移除應用程式或驅動程式。
- 部分移除：Windows 安裝會從裝置部分移除應用程式或驅動程式。 您需要在升級 Windows 後手動解除安裝。

在這兩種情況下，在您升級 Windows 後，使用者即無法使用應用程式或與驅動程式建立關聯的硬體。

在電腦分析入口網站中查看此建議：

1. 在部署計劃中，選取 [準備試驗]。
1. 選取 [應用程式] 索引標籤。
1. 選取一個應用程式，然後在側邊窗格中檢視相容性風險因素和建議。

[![電腦分析入口網站中的資產建議螢幕擷取畫面](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>封鎖升級

Windows 偵測到執行問題，且無法在升級期間移除應用程式。 該應用程式可能無法在新的 OS 版本上運作。 請在升級前移除應用程式。 在新的 OS 版本上重新安裝並進行測試。

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>封鎖升級，但仍然可以在升級後重新安裝

應用程式與新的 OS 版本相容，但不會遷移。 請在升級 Windows 前移除應用程式。 在新的 OS 版本上重新安裝。

### <a name="blocking-upgrade-update-application-to-newest-version"></a>封鎖升級，將應用程式更新至最新版本

應用程式的現有版本與新的 OS 版本不相容，因此不會遷移。 有可用的應用程式相容版本。 請在升級前更新應用程式。

### <a name="disk-encryption-blocking-upgrade"></a>磁碟加密封鎖升級

應用程式的加密功能封鎖了升級。 請在升級 Windows 前停用加密功能，並於升級後啟用。

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>無法與新的 OS 搭配運作，但不會封鎖升級

應用程式與新的 OS 版本不相容，但不會封鎖升級。 無須採取任何動作，升級也能繼續進行。 請在新的 OS 版本上安裝應用程式的相容版本。

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>無法與新的 OS 搭配運作，且會封鎖升級

應用程式與新的 OS 版本不相容，且將會封鎖升級。 請在升級前移除應用程式。 可能會有可用的應用程式相容版本。

### <a name="evaluate-application-on-new-os"></a>在新的 OS 上評估應用程式

Windows 將會遷移應用程式，但其偵測到問題，可能影響應用程式在新 OS 版本上的效能。 無須採取任何動作，升級也能繼續進行。 請在新的 OS 版本上測試應用程式。

### <a name="may-block-upgrade-test-application"></a>可能會封鎖升級，測試應用程式

Windows 偵測到問題，可能會影響升級，但需要進一步的調查。 請在升級期間測試應用程式的行為。 若其封鎖了升級，請在升級前移除該應用程式。 然後在新的 OS 版本上重新安裝並進行測試。

### <a name="multiple"></a>多個

多個問題影響了應用程式。 請選取 [查詢]，查看 Windows 所偵測到的問題詳細資料。

### <a name="reinstall-application-after-upgrading"></a>請在升級後重新安裝應用程式

應用程式與新的 OS 版本相容，但您需要在升級 Windows 後重新安裝。 升級流程會移除應用程式。 無須採取任何動作，升級也能繼續進行。 請在新的 OS 版本上重新安裝應用程式。

### <a name="safeguards"></a>保護

<!-- 5746559 -->

Windows 相容性資料會使用「保護」來分類某些應用程式與驅動程式，這可能會導致更新至 Windows 10 失敗或復原。 Windows 可能也會升級，但會移除應用程式或驅動程式。 電腦分析現在可以協助您事先識別這些保護，讓您可以在部署更新之前先對資產進行補救。

1. 在電腦分析入口網站中，選取部署計劃。

1. 在功能表中選取 [計劃資產]，然後切換至 [應用程式] 索引標籤。

1. 篩選 [名稱] 欄以顯示值包含 `Safeguard` 文字的項目。 選取結果以查看詳細資訊。

    > [!NOTE]
    > 此項目不是安裝在您裝置上的實際應用程式。 其是預留位置，用來協助識別您環境中具有保護相容性標籤的應用程式或驅動程式。

1. 在 [建議] 區段中，選取 [深入了解] 連結。 此連結會開啟 Windows 網站，其中包含具有保護標籤的目前應用程式或驅動程式清單。

1. 比較目前已發行的清單與您環境中的資產清單。 透過更新為相容版本，來針對任何可能有問題的應用程式或驅動程式進行補救。

[![電腦分析中保護應用程式的螢幕擷取畫面](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Ready for Windows

採用狀態會以與 Microsoft 共用資料之商業裝置的資訊為基礎。 此狀態會與軟體廠商的支援聲明整合。

電腦分析則為在商業裝置中找到的每個資產版本提供採用狀態。 此狀態不包含取用者裝置的資料或不共用資料的裝置資料。 而且此狀態並不代表所有 Windows 10 裝置的採用率。

可能的類別包括：

- **已高度採用**：至少有 100,000 部商業 Windows 10 裝置安裝此應用程式。

- **已採用**：至少有 10,000 部商業 Windows 10 裝置安裝此應用程式。

- **資料不足**：共用此應用程式資訊的商業 Windows 10 裝置太少，因此 Microsoft 無法分類其採用狀況。

- **連絡開發人員**：此應用程式版本可能有相容性問題。 Microsoft 建議連絡軟體提供者以深入了解。

- **未知**：此應用程式的此版本沒有可用的資訊。 應用程式的其他版本可能會提供資訊。

### <a name="support-statement"></a>支援聲明

若軟體提供者在 Windows 10 上支援一或多個此應用程式的版本，您會在應用程式屬性窗格中看到此聲明。 請在相容性風險因素區段，查看 [支援聲明]。

## <a name="advanced-insights"></a>進階見解

電腦分析也可以使用下列其他見解來偵測問題：

### <a name="adopted-version-available"></a>有可用的已採用版本

此應用程式有另一個已由其他客戶高度採用的版本。 此訊號使用來自 Windows 生態系統的採用資料。 若您目前的版本有任何升級封鎖程式，請考慮部署替代版本。 若要尋找替代的應用程式採用版本，請參閱 [準備生產環境] 下的應用程式健康情況。

### <a name="driver-dependency"></a>驅動程式相依性

此應用程式相依於驅動程式。 電腦分析會建議進行試驗測試的應用程式，來探索任何迴歸。 若您有任何問題，請連絡發行者，要求與 Windows 10 相容的版本。

### <a name="additional-insights"></a>其他見解

<!-- 4021225 -->
當您將 Configuration Manager 站台和用戶端更新至版本 1906 時，若診斷資料層級已設為 [增強 (受限)]，用戶端也會報告這些其他見解：

> [!Important]  
> 若要充分利用 Configuration Manager 的新功能，請在更新站台之後，也將用戶端更新為最新版本。 除非用戶端版本也是最新版本，否則此案例無法運作。

#### <a name="16-bit-apps"></a>16 位元應用程式

從應用程式中移除所有 16 位元元件，並替換成 32 位元或 64 位元的對等項目。 如需詳細資訊，請參閱 [Windows Vista 和 Windows Server 2008 開發人員案例：應用程式相容性逐步指南](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\))。

另一個選項是啟用 NT 虛擬 DOS 機器 (NTVDM) 以在 Windows 10 上提供支援。

#### <a name="requires-admin-privileges"></a>需要管理員權限

應用程式需要使用者具備裝置的系統管理存取。 請針對需要系統管理員權限的這些應用程式，使用應用程式資訊清單。 如需詳細資訊，請參閱[建立及內嵌應用程式資訊清單](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))。

電腦分析會建議進行試驗測試的應用程式，來探索任何迴歸。

#### <a name="java-dependency"></a>Java 相依性

許多 Java 應用程式都依賴個別安裝的 Java Runtime Environment (JRE)。 較舊的 JRE 版本可能會繼續在 Windows 10 上運作，而 Oracle 只支援最新的 JRE 版本。 使用舊版且不受支援的 JRE 可能會有資訊安全漏洞。 請檢查您的應用程式是在最新的 JRE 版本上執行。

#### <a name="not-dpi-aware"></a>非 DPI 感知

應用程式在 Windows 10 上可能會有進階螢幕解析度的顯示問題。 請使用應用程式資訊清單，避免任何與高 DPI 解析度有關的問題。 如需詳細資訊，請參閱[應用程式資訊清單](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests)。

電腦分析會建議進行試驗測試的應用程式，來探索任何迴歸。

#### <a name="silverlight-framework"></a>Silverlight 架構

Microsoft 建議不是以瀏覽器為基礎的應用程式不要使用 Silverlight。 Silverlight 5 的支援結束日期為 2021 年 10 月。

目前大多數的網頁瀏覽器都不支援 Silverlight。

| 瀏覽器 | 支援 |
|---------|---------|
| Google Chrome | 終止支援：2015 年 9 月 |
| Firefox | 終止支援：2017 年 3 月 |
| Microsoft Edge | 沒有可用的外掛程式 |

電腦分析會建議進行試驗測試的應用程式，來探索任何迴歸。

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

Windows 10 上不支援 .NET Framework 1.0 版本。 版本 1.1 與 Windows 10 不相容。 若應用程式是來自協力廠商發行者，請連絡廠商，要求與 Windows 10 相容的版本。 否則，請重新開發應用程式，以使用支援的 .NET 版本。

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

Windows 10 支援 .NET 2.0 及 3.5 架構。 您可能需要啟用 Windows 功能。 如需詳細資訊，請參閱[在 Windows 10 上安裝 .NET Framework 3.5](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10)。

#### <a name="ui-access"></a>UI 存取

具有 UI 存取的應用程式可以略過使用者介面控制層級，將輸入傳送到桌面上具備更高權限的視窗。 請只針對使用者介面輔助技術應用程式使用此設定。

若您並未在您的應用程式中使用協助工具功能，請在應用程式資訊清單中將 UI 存取旗標設為 False。 如需詳細資訊，請參閱[建立及內嵌應用程式資訊清單](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))。

電腦分析會建議進行試驗測試的應用程式，來探索任何迴歸。

## <a name="driver-risk-assessment"></a>驅動程式風險評定

電腦分析也會依據可用性，列出及分組任何不會遷移至 OS 版本的驅動程式。

您可以在電腦分析中找到驅動程式的評定。 在部署計劃中的驅動程式資產清單內，選取個別驅動程式來開啟其屬性飛出視窗窗格。 您將會看到整體建議和評定層級。 **相容性風險因素**區段會顯示這些評定的詳細資料。

| 驅動程式可用性 | 需要採取動作嗎？ | 代表的意義 | 指導 |
|---------------------|------------------|---------------|----------|
| 隨附可用 | 否，僅適用於感知 | 目前安裝的應用程式或驅動程式版本將不會遷移至新的 OS 版本。 已針對新的 OS 版本安裝相容版本。 | 無須採取任何動作，升級也能繼續進行。 |
| 從 Windows Update 匯入 | 是 | 目前安裝的驅動程式版本將不會遷移至新的 OS 版本。 Windows Update 提供相容的版本。 | 若電腦會自動從 Windows Update 接收更新，則無須採取任何動作。 否則，請在您升級 Windows 後從 Windows Update 匯入新的驅動程式。 |
| 隨附可用以及可以從 Windows Update 取得 | 是 | 目前安裝的驅動程式版本將不會遷移至新的 OS 版本。 雖然在升級期間已安裝了新的驅動程式，Windows Update 提供了更新的版本。 | 若電腦會自動從 Windows Update 接收更新，則無須採取任何動作。 否則，請在您升級 Windows 後從 Windows Update 匯入新的驅動程式。 |
| 向廠商確認 | 是 | 驅動程式將不會遷移至新的 OS 版本，且電腦分析找不到相容版本。 | 如需解決方案，請向製造驅動程式的獨立硬體廠商 (IHV) 確認，或是向提供裝置的原始設備製造商確認。 |

## <a name="see-also"></a>請參閱

適用於 Windows 10 的 FastTrack 中心權益提供存取**桌面應用程式保證**。 此權益是一個新的服務，旨在解決 Windows 10 與 Microsoft 365 Apps 企業版的相容性問題。 如需詳細資訊，請參閱[桌面應用程式保證](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure)。
