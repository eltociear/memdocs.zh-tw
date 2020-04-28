---
title: Office 365 用戶端管理儀表板
titleSuffix: Configuration Manager
description: 在 Office 365 用戶端管理儀表板中檢閱 Office 365 用戶端資訊
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: 7e6ed38d0f4217bfc70d3ddb196527d421e5d7c1
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110384"
---
# <a name="office-365-client-management-dashboard"></a>Office 365 用戶端管理儀表板

適用於：  Configuration Manager (最新分支)

> [!Note]
> 從 2020 年 4 月 21 日開始，「Office 365 專業增強版」會重新命名為「Microsoft 365 Apps 企業版」  。 如需詳細資訊，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) \(部分機器翻譯\)。 在主控台正在進行更新時，您在 Configuration Manager 主控台與輔助文件中可能仍會看到提及舊名稱。

從 Configuration Manager 1802 版開始，您可以在 Office 365 用戶端管理儀表板中檢閱 Office 365 用戶端資訊。 當選取圖形區段時，Office 365 用戶端管理儀表板會顯示相關裝置的清單。 <!--1357281 -->

## <a name="prerequisites"></a>先決條件

### <a name="enable-hardware-inventory"></a>啟用硬體清查

[Office 365 用戶端管理] 儀表板中所顯示的資料來自硬體清查。 啟用硬體清查，並選取 [Office 365 ProPlus 設定]  硬體清查類別，資料才會顯示在儀表板中。
 
1. 啟用硬體清查 (如果尚未啟用)。 如需詳細資料，請參閱[設定硬體清查](../../core/clients/manage/inventory/configure-hardware-inventory.md)。
2. 在 Configuration Manager 主控台中，瀏覽至 [系統管理]   > [用戶端設定]   > [預設用戶端設定]  。  
3. 在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容]  。  
4. 在 **預設用戶端設定**  對話方塊中按一下 **硬體清查**。  
5. 在 **裝置設定** 清單中，按一下 **設定類別**。  
6. 在 [硬體清查類別]  對話方塊中，選取 [Office 365 ProPlus Configurations]\(Office 365 ProPlus 設定)  。  
7. 按一下 **確定** 以儲存您的變更並關閉 **硬體清查類別** 對話方塊。

Office 365 用戶端管理儀表板將在報告硬體清查時開始顯示資料。

### <a name="connectivity-for-top-level-site-server"></a>最上層站台伺服器的連線能力

*(在 1906 版中引入為必要條件)*

您的最上層站台伺服器需要存取下列端點才能下載整備檔案：

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> 針對這些情況，用戶端裝置不需要網際網路連線能力。

### <a name="enable-data-collection-for-office-365-proplus"></a>啟用 Office 365 專業增強版的資料收集

*(在 1910 版中引入為必要條件)*

從 1910 版開始，您必須啟用 Office 365 專業增強版的資料收集，以在 **Office 365 專業增強版試驗和健全狀況儀表板**中填入資訊。 資料會儲存在 Configuration Manager 站台資料庫，且不會傳送到 Microsoft。

這項資料與診斷資料 (在[從 Office 365 專業增強版傳送到 Microsoft 的診斷資料](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft)中描述) 不同。

您可以使用群組原則，或透過編輯登錄來啟用資料收集。

#### <a name="enable-data-collection-from-group-policy"></a>從群組原則啟用收集資料

1. 從 Microsoft 下載中心[下載最新的系統管理範本檔案](https://www.microsoft.com/download/details.aspx?id=49030)。
2. 在 `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard` 下方啟用 [開啟遙測資料收集]  原則設定。
    - 或者，您也可以使用 [Office 雲端原則服務](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service)來套用原則設定。
    - [Office 遙測儀表板] 也會使用此原則設定 (您不需要為此資料收集部署此原則設定)。

#### <a name="enable-data-collection-from-the-registry"></a>從登錄啟用資料收集

下列命令是從登錄啟用資料收集的範例：

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>檢視 Office 365 用戶端管理儀表板

若要在 Configuration Manager 主控台中檢視 Office 365 用戶端管理儀表板，請移至 [軟體程式庫]   > [概觀]   > [Office 365 用戶端管理]  。 使用儀表板頂端的 [集合]  下拉式清單設定，依特定集合成員篩選儀表板資料。 從 Configuration Manager 1802 版開始，選取圖表區段時，Office 365 用戶端管理儀表板會顯示相關裝置的清單。

Office 365 用戶端管理儀表板提供下列資訊的圖表：

- Office 365 用戶端數目
- Office 365 用戶端版本
- Office 365 用戶端語言
- Office 365 用戶端通道 如需詳細資訊，請參閱 [Office 365 ProPlus 更新通道的概觀](/DeployOffice/overview-of-update-channels-for-office-365-proplus)。


## <a name="integration-for-office-365-proplus-readiness"></a><a name="bkmk_o365_readiness"></a> 與 Office 365 ProPlus 整備的整合
<!--3735402-->
從 Configuration Manager 版本 1902 開始，您可以使用儀表板來識別具有高信賴度準備升級到 Office 365 ProPlus 的裝置。 此整合提供有關您環境中 Office 增益集與巨集之潛在相容性問題的見解。 接著，使用 Configuration Manager 將 Office 部署到已就緒的裝置。

Office 365 用戶端管理儀表板包括新的 [Office 365 ProPlus 更新整備小幫手]  圖格。 此圖格是處於下列狀態之裝置的橫條圖：
- 未評估
- 準備升級
- 需要檢閱

選取狀態以鑽研至裝置清單。 這個整備報告顯示有關裝置的更多詳細資料。 它包括 Office 增益集與巨集之相容性狀態的欄。

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Office 365 ProPlus 整備整合的先決條件

- 在用戶端設定中啟用硬體清查。 如需詳細資訊，請參閱[先決條件](#prerequisites)一節。  

- 裝置必須能夠連線到 Office 內容傳遞網路 (CDN)，才能下載增益集整備檔案。 如需詳細資訊，請參閱[內容傳遞網路](https://docs.microsoft.com/office365/enterprise/content-delivery-networks)。 若裝置無法下載此檔案，增益集狀態為「需要檢閱」  。  

    > [!Note]  
    > 針對此功能，不會有任何資料傳送到 Microsoft。  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a> 詳細的巨集整備

根據預設，掃描代理程式會在每部裝置上尋找最近使用的 (MRU) 檔案清單。 它會計算此清單中支援巨集的檔案數目。 這些檔案包括下列類型：
- 啟用巨集的 Office 檔案格式、例如 Excel 啟用巨集的活頁簿 (.xlsm) 或 Word 啟用巨集的文件 (.docm)  
- 未指出是否有巨集內容的較舊 Office 格式。 例如，Excel 97-2003 活頁簿 (.xls)。

如果您需要巨集相容性的詳細資訊，請部署 **Readiness Toolkit for Office** 以分析巨集檔案內的程式碼。 它會檢查是否有任何潛在的相容性顧慮。 例如，檔案使用在較新的 Office 版本中已變更的函式。 在您執行 Readiness Toolkit for Office 並選取 [Most recently used Office documents and installed add-ins on this computer] \(這部電腦上最近使用過的 Office 文件和已安裝增益集\)  選項，或在命令列中使用 `-mru` 旗標之後，Configuration Manager 的硬體清查代理程式就可以挑選結果。 這個額外資料可以加強裝置整備計算。 如需詳細資訊，請參閱[使用 Readiness Toolkit for Office 365 ProPlus 評估應用程式相容性](https://aka.ms/readinesstoolkit)。

請注意，您不需要在每部目標裝置上安裝 Readiness Toolkit 也可以執行掃描。 您可以使用以下範例命令列選項來掃描每個所需的裝置。  輸出旗標為必要，但檔案不會用來在儀表板中產生結果，因此您可以選取任何有效的位置。

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

如需詳細資訊，請參閱[取得企業中多位使用者的整備資訊](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise)。

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a> Office 365 ProPlus 升級整備儀表板

*(於 1906 版推出)*

<!--4021125-->
為了協助您判斷哪些裝置已準備好升級至 Office 365 ProPlus，我們從 1906 版開始提供一個新的整備儀表板。 它包含 Configuration Manager 最新分支 1902 版中發行的 **Office 365 ProPlus 升級整備**圖格。 此儀表板上的下列新圖格可協助您評估 Office 增益集和巨集整備：

- 部署
- 裝置整備
- 增益集整備
- 增益集的支援陳述式
- 依版本計數的最上層增益集
- 具有巨集的裝置數目
- 巨集整備
- 巨集諮詢

下列影片來自 Ignite 2019 的研討會，其中包含詳細資訊：

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[相容性評定的最佳做法，以及使用 Configuration Manager 中 Office 整備程度的 Microsoft Office 365 專業增強版升級](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions) (英文)

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>使用 Office 365 ProPlus 升級整備儀表板

在確認您具備[必要條件](#prerequisites)之後，請利用下列指示來使用儀表板：
 
1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，然後展開 [Office 365 用戶端管理]  。
1. 選取 [Office 365 專業增強版升級整備小幫手]  節點。
1. 變更**集合**和**目標 Office 架構**，以變更在儀表板中轉送的資訊。

![Office 365 ProPlus 升級整備儀表板](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Office 365 ProPlus 升級整備儀表板](./media/4021125-office-365-to-add-ins.png)

![Office 365 ProPlus 升級整備儀表板](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>裝置整備資訊

在評估每部裝置上的增益集和巨集清查之後，裝置會根據該資訊來分組。 狀態列為**準備升級**的裝置，不太會發生相容性問題。

若選取圖表上的 [準備升級]  類別，則會顯示限制集合中裝置的詳細資料。 您可以檢閱裝置清單、根據業務需求進行選取，並從選取項目建立新的裝置集合。 使用新集合來部署具備 Configuration Manager 的 Office 365 專業增強版。

可能具有相容性問題風險的裝置會標示為**需要檢閱**。 您可能需要對這些裝置採取動作，才能將其升級至 Office 365 專業增強版。 例如，您可能需要將關鍵增益集更新為較新的版本。

### <a name="add-in-information"></a>增益集資訊

 在每部裝置上，會收集所有已安裝增益集的清查。 然後，清查會與 Microsoft 對於 Office 365 專業增強版的增益集效能相關資訊進行比較。 如果找到可能會在升級後造成問題的增益集，則會標示具有該增益集的所有裝置以進行檢閱。

### <a name="macro-information"></a>巨集資訊

Configuration Manager 會查看每部裝置上最近使用的檔案。 Configuration Manager 會計算此清單中支援巨集的檔案，包括下列類型：

- 啟用巨集的 Office 檔案格式。
- 較舊的 Office 格式，不會指出是否有巨集內容。

這份報告可以用來識別哪些裝置最近使用的檔案可能包含巨集。 然後，您可以使用 Configuration Manager 來部署 **Readiness Toolkit for Office**，以掃描任何需要更詳細資訊的裝置，並檢查是否有任何潛在的相容性問題。 例如，如果檔案使用的函式在較新版 Office 中有變更。

如需如何執行掃描的詳細資訊，請參閱[詳細的巨集整備](#bkmk_ort)。

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a> Office 365 專業增強版試驗與健全狀況儀表板
<!--4488272, 4488301-->
*(於 1910 版引進)*

從 1910 版開始，**Office 365 專業增強版試驗和健全狀況儀表板**可協助您規劃、試驗及執行 Office 365 專業增強版部署。 儀表板會對含有 Office 365 專業增強版的裝置提供健康情況見解，為您找出可能會影響部署計劃的問題。 **Office 365 專業增強版試驗與健康情況儀表板**會根據增益集清查提供試驗裝置的建議。 儀表板中有下列圖格：

- 產生試驗
- 建議的試驗裝置
- 部署試驗
- 傳送健全狀況資料的裝置
- 裝置未滿足健康情況目標
- 未滿足健康情況目標的增益集
- 巨集未滿足健康情況目標

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>使用 Office 365 專業增強版試驗與健全狀況儀表板

在確認您具備[必要條件](#prerequisites)之後，請利用下列指示來使用儀表板：

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，然後展開 [Office 365 用戶端管理]  。
1. 選取 [Office 365 試驗和健全狀況]  節點。

![Office 365 專業增強版試驗與健全狀況儀表板](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>產生試驗

在按一下按鈕之後從有限的集合產生試驗建議。 啟動動作之後，背景工作便會開始計算您的試驗集合。 您限制集合至少必須包含一部已安裝 Office 但非專業增強版的裝置。

### <a name="recommended-pilot-devices"></a>建議的試驗裝置

**建議的試驗裝置**是一組數目最低的裝置，代表產生試驗時使用之有限集合中所有已安裝的增益集。 向下切入以取得這些裝置的清單。 接著，使用詳細資料視需要從試驗中排除任何裝置。 如果所有增益集都已在 Office 365 ProPlus 裝置上，則具有這些增益集的裝置將不會包含在計算中。 這也表示您可能不會在試驗集合中得到任何結果，因為您已在安裝了 Office 365 ProPlus 的裝置上看到所有增益集。

### <a name="deploy-pilot"></a>部署試驗

一旦您接受試驗裝置，請使用階段式部署精靈，將 Office 365 專業增強版部署到試驗集合。 系統管理員可以在精靈中定義試驗與受限集合以管理部署。

### <a name="health-data"></a>健康情況資料

安裝 Office 365 專業增強版之後，請在您的試驗裝置上啟用健康情況資料。 健康情況資料可讓取得哪些增益集與巨集不符合健康情況目標的見解。 [已準備好部署的裝置]  圖識別可透過使用健康情況見解來部署的非試驗裝置。 從 [傳送健康情況資料的裝置]  圖取得正在傳送健康情況資料的裝置計數。

### <a name="devices-not-meeting-health-goals"></a>裝置未滿足健康情況目標

此圖格會摘述增益集、巨集或兩者有問題的裝置。

### <a name="add-ins-not-meeting-health-goals"></a>未滿足健康情況目標的增益集

- 載入失敗：增益集無法啟動。
- 當機：增益集執行時失敗。
- 錯誤：增益集回報錯誤。
- 多個問題：增益集有多個上述問題。

### <a name="macros-not-meeting-health-goals"></a>巨集未滿足健康情況目標

- 載入失敗：文件無法載入。
- 執行階段錯誤：巨集執行時發生錯誤。 這些錯誤取決於輸入，因此不見得一律會發生。
- 編譯錯誤：巨集未正確編譯，因此它將不會嘗試執行。
- 多個問題：巨集有多個上述問題。

> [!NOTE]
> 巨集清查中會填入來自 Readiness Toolkit for Office 和最近所使用資料檔的資料。 巨集健全狀況中會填入健全狀況資料。 由於有不同的資料來源，因此當巨集清查的狀態為 [未掃描]  時，巨集健全狀態便可能為 [需要審核]  。 <!--5922845-->

### <a name="known-issues"></a>已知問題

[部署試驗]  磚有一個已知問題。 目前無法用來部署至試驗。 因應措施是使用 [階段式部署精靈] 來部署應用程式的現有工作流程。 <!--5525871-->

## <a name="next-steps"></a>後續步驟

[使用 Configuration Manager 管理 Office 365 ProPlus](manage-office-365-proplus-updates.md)
