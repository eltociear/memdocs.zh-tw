---
title: 設定分類和產品
titleSuffix: Configuration Manager
description: 請遵循下列步驟，在 Configuration Manager 主控台中設定要同步處理的軟體更新分類和產品。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 4f13ff305ba5fc2b5c5080bafb6fed2412ff8366
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84614072"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>設定要同步處理的分類和產品  

適用於：Configuration Manager (最新分支)

根據您在軟體更新點元件內容中指定的設定，Configuration Manager 在同步處理期間會擷取軟體更新中繼資料。 第一次同步處理軟體更新後，或發行新產品和分類時，您必須移至 [內容] 選取新的項目。 利用下列程序設定要同步處理的分類和產品。  

> [!NOTE]  
> 本節中的程序僅適用於頂層站台。  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>若要設定要同步處理的分類和產品  

1. 在 **Configuration Manager** 主控台中，瀏覽至 [管理] > [站台設定] > [站台]。

2. 選取管理中心網站或獨立主要站台。  

3. 在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件] ，然後按一下 [軟體更新點] 。

4. 在 [分類]  索引標籤上，指定要同步處理其軟體更新的軟體更新分類。  

    每個軟體更新都利用有助於組織不同類型更新的更新分類來加以定義。 在同步處理程序期間，將會同步處理指定分類的軟體更新中繼資料。 Configuration Manager 提供了同步處理下列更新分類之軟體更新的功能：  

     - **重大更新**：針對特定問題指定大規模發行的修正程式，以解決與安全性無關的重大 Bug。  
     - **定義更新**：指定大規模發行且經常性的軟體更新，其中包含新增至產品定義資料庫的項目。  
     - **Feature Pack**：指定產品版本範圍以外第一次發佈的新產品功能，以及一般包含在下一個完整產品版本的功能。  
     - **安全性更新**：針對產品特定、與安全相關的弱點，指定大規模發行的修正程式。  
     - **Service Pack**：指定經過測試的所有 Hotfix、安全性更新、重大更新和更新積存組合，全部都會套用至產品。 此外，Service Pack 也可能包含其他修正程式來解決從產品發行以來在內部發現的問題。  
     - **工具**：指定有助於完成一項或多項工作的公用程式或功能。  
     - **更新彙總套件**：指定經過測試的 Hotfix、安全性更新、重大更新和更新積存組合，全部封裝在一起以方便部署。 更新彙總套件一般處理特定領域，例如安全性或產品元件。  
     - **更新**：針對特定問題指定大規模發行的修正程式。 更新會解決與安全性無關的非重大 Bug。  
     - **升級**：指定 Windows 10 特性與功能的升級。 您的軟體更新點及網站至少須執行 WSUS 6.2 (含 [Hotfix 3095113](https://support.microsoft.com/kb/3095113))，才能取得**升級**分類。 如需安裝此更新和其他更新以進行**升級**的詳細資訊，請參閱[軟體更新的必要條件](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)。
    
    > [!NOTE]
    > 您可以選取 [Include Microsoft Surface drivers and firmware updates] \(包含 Microsoft Surface 驅動程式與韌體更新\) 核取方塊，以同步處理 Microsoft Surface 驅動程式。<!--1098490--> 所有軟體更新點必須都執行 Windows Server 2016 或更新版本，才能順利同步處理 Surface 驅動程式。 如果您在啟用 Surface 驅動程式之後，於執行 Windows Server 2012 的電腦上啟用軟體更新點，則驅動程式更新的掃描結果會不正確。 這會導致 Configuration Manager 主控台和 Configuration Manager 報告中顯示不正確的相容性資料。 如需詳細資訊，請參閱[使用 Configuration Manager 管理 Surface 驅動程式](../deploy-use/surface-drivers.md)。

5. 在 [產品]  索引標籤上，指定要同步處理其軟體更新的產品，然後按一下 [關閉] 。  

    - Configuration Manager 儲存了一份產品及產品系列清單，您第一次安裝軟體更新點時就是在這份清單中選擇。 在您完成軟體更新同步處理之前，可能無法選取在 Configuration Manager 發行後發行的產品和產品系列，因為同步處理會更新可供您選擇的可用產品和產品系列清單。  

    - 各個軟體更新的中繼資料會針對適用的更新定義產品。 產品即為特定版本的作業系統或應用程式 (例如 Windows Server 2012)。 而產品系列則是指衍生出個別產品的基礎作業系統或應用程式。 產品系列的範例有 Windows，Windows Server 2012 就是其中的成員。 您可以指定產品系列或產品系列中的個別產品。 您選取的產品越多，同步處理軟體更新的時間就越長。  

    - 當軟體更新適用於多項產品，而且至少已選取其中一項產品要進行同步處理時，即使您並未選取全部產品，Configuration Manager 主控台也會顯示所有產品。 例如，如果您只選取 Windows Server 2012 作業系統，而軟體更新適用於 Windows 8 和 Windows Server 2012，則這兩項產品都會顯示在 Configuration Manager 主控台中。  

    > [!NOTE]  
    > **Windows 10 1903 版及更新版本**已新增到 Microsoft Update 成為該產品的一部分，而不再像舊版，隸屬於 **Windows 10** 產品。 此變更導致您需要執行一些手動步驟以確保您的用戶端可看到這些更新。 我們已協助減少您必須為 Configuration Manager 1906 版新產品進行的手動步驟數量。 <!--4682946-->
    >
    > 當您更新至 Configuration Manager 1906 版並選取 **Windows 10** 產品進行同步處理時，下列動作會自動執行：
    > - 新增 **Windows 10 1903 版和更新版本**產品以進行同步處理。
    > - 包含 **Windows 10** 產品的[自動部署規則](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)將會更新，以包含 **Windows 10 1903 版和更新版本**。
    > - [服務方案](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)會更新以包含 **Windows 10 1903 版和更新**產品。


## <a name="configuring-products-for-versions-of-windows-10"></a>設定 Windows 10 各版本的產品

### <a name="windows-10-version-1909"></a>Windows 10 1909 版

Windows 10 1909 版與 Windows 10 1903 版共用通用的核心作業系統。 這兩個版本都由相同的累積更新服務。 如需 Windows 10 1909 版的詳細資訊，請參閱 [Windows 10 1909 版傳遞選項](https://aka.ms/1909mechanics) (英文) 部落格文章。

確保您的 Windows 10 1909 版和 Windows 10 1903 版用戶端從 Configuration Manager 安裝更新：

- 核准 Windows 10 1909 版和 1903 版的更新。
  - 針對每個作業系統版本，更新各有不同的標題和適用性規則。
  - 核准每個版本和每個 OS 架構的每項更新，會維護系統管理員的一般核准程序。
- Windows 10 1909 版和 1903 版的累積更新安裝檔案相同。
  - Configuration Manager 只會下載一次更新來源檔案。

#### <a name="feature-updates-for-windows-10-version-1909"></a>Windows 10 1909 版的功能更新

當核准 Windows 10 1909 版的功能更新時，您會看到幾個不同的選項：

- 2019 年 11 月 12 日發行的[啟用套件](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)，可供 Windows 10 1903 版用戶端使用。
  - 啟用套件是小型的快速安裝檔案，可啟用 Windows 10 1909 版的功能，且會重新啟動裝置。
  - 啟用套件的必要條件包括：
    - [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389) 的最小累積更新，發行於 2019 年 10 月 8 日。
    - [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390) 的最低服務堆疊更新，發行於 2019 年 9 月 24 日。
  - 此更新與任何其他功能更新一樣無法從 `https:\\catalog.update.microsoft.com` 匯入。
  - 如果您有 **Windows 10 1903 版及更新版本**的產品，並已選取要同步處理的 [升級] 分類，則更新會自動與 WSUS 同步。
  - 在 Configuration Manager 主控台中，前往 [軟體程式庫] 工作區、展開 [Windows 10 服務]，然後選取 [所有 Windows 10 更新] 節點。 搜尋「啟用」或 "4517245" 字詞。

    > [!TIP]
    > 由於這些是功能更新，所以不位於 [所有軟體更新] 節點中。

- Windows 10 1809 版及較舊版用戶端會透過單一直接功能更新進行升級。
  - 這就像是您為 Windows 10 安裝的所有其他先前功能更新一樣。

> [!NOTE]
> 不論使用哪一種路徑來安裝，啟用套件和 Windows 10 1909 版的傳統功能更新都會在報告中顯示為「已安裝」。

### <a name="windows-10-version-1903-and-later"></a>Windows 10 1903 版與更新版本

**Windows 10 1903 版和更新版本**已作為其專屬產品新增至 Microsoft Update，而不是像舊版一樣作為 **Windows 10** 產品的一部分。 此變更導致您需要執行一些手動步驟以確保您的用戶端可看到這些更新。 我們已協助減少您必須為 Configuration Manager 1906 版新產品進行的手動步驟數量。 <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>搭配 Configuration Manager 1906 版的 Windows 10 1903 版及更新版本
當您更新至 Configuration Manager 1906 版並選取 **Windows 10** 產品進行同步處理時，下列動作會自動執行：
- 新增 **Windows 10 1903 版和更新版本**產品以進行同步處理。
- 包含 **Windows 10** 產品的[自動部署規則](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)將會更新，以包含 **Windows 10 1903 版和更新版本**。
- [服務方案](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)會更新以包含 **Windows 10 1903 版和更新**產品。

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>搭配 Configuration Manager 1902 版的 Windows 10 1903 版及更新版本
如果您使用 Configuration Manager 1902 搭配 Windows 10 1903 版用戶端，則必須：
- 選取 [Windows 10 1903 及更新版本] 產品以進行同步。
- 更新 Windows 10 1903 版用戶端的任何[自動部署規則](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)。
- 更新 Windows 10 1903 版用戶端的[服務方案](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)。

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Windows 測試人員計畫
<!--3556023-->
從 2019 年 9 月開始，您可以使用 Configuration Manager 為執行 Windows Insider Preview 組建的裝置進行維護及更新。 此變更表示您可以在不變更您正常程序或啟用商務用 Windows Update 的情況下管理這些裝置。 您可以將適用於 Windows Insider Preview 組建的更新與累積更新下載到 Configuration Manager，就像任何其他 Windows 10 更新或升級一樣。 如需詳細資訊，請參閱[將發行前版本 Windows 10 功能更新發佈至 WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) (英文) 部落格文章。

如需 Configuration Manager 中 Windows 測試人員支援的詳細資訊，請參閱 [Windows 10 的支援](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support)。

### <a name="prerequisites"></a>先決條件

- 已針對[軟體更新管理](../plan-design/plan-for-software-updates.md)設定的 Configuration Manager 1906 版或更新版本。
- 執行 [Windows Insider Preview 組建](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started)的 Windows 10 裝置。
- 包含 Windows 測試人員裝置的集合。

### <a name="enable-windows-insider-upgrades-and-updates"></a>啟用 Windows 測試人員的升級和更新

您必須啟用產品和分類以進行 Windows 測試人員升級和更新。 Windows 測試人員的功能更新、累積更新和其他更新，都位於 **Windows 測試人員發行前版本**產品類別下方。

1. 在 **Configuration Manager** 主控台中，瀏覽至 [管理] > [站台設定] > [站台]。
2. 選取管理中心網站或獨立主要站台。  
3. 在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件] ，然後按一下 [軟體更新點] 。
4. 請確認已在 [產品] 索引標籤上選取下列產品進行同步處理：
    - Windows 測試人員發行前版本
    - Windows 10 1903 版與更新版本
5. 請確認已在 [分類] 索引標籤上選取下列分類進行同步處理：
    - 升級
    - 安全性更新
    - 更新 (選擇性)
6. 按一下 [確定]  以關閉 [軟體更新點元件內容] 。

### <a name="upgrading-windows-insider-devices"></a>升級 Windows 測試人員裝置

在同步處理 Windows 測試人員的升級後，您就可以從 [軟體程式庫] > [Windows 10 服務] > [所有 Windows 10 更新] 看到這些升級。

![Windows 10 服務的 Windows 測試人員功能更新](media/3556023-windows-insiders-pre-release-feature-update.png)

如同任何其他升級一樣，將 Windows 測試人員的功能更新部署到目標集合。 不過，建議您在部署這些功能更新時考量下列項目：

- 這些升級將適用於所有具有相符架構、版本和語言的 Windows 10 用戶端 1903 或較舊版本。
- 您的部署必須接受授權條款才能安裝。
- 請考慮使用[用戶端設定中的執行緒優先順序](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)。
- 動態更新會自動直接從 Microsoft Update 安裝重大更新，包括最新的累積更新。 此行為從 Windows 10 1903 版的功能更新開始。 
  - 您可以明確[在用戶端設定中停用動態更新](../../core/clients/deploy/about-client-settings.md#bkmk_du)，或使用 [setupconfig.ini 檔案](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。 
  - 如需詳細資訊，請參閱 [Windows 10 動態更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)部落格文章。

如需如何部署升級的詳細資訊，請參閱[管理 Windows 即服務](../../osd/deploy-use/manage-windows-as-a-service.md)。


### <a name="keeping-insider-devices-up-to-date"></a>將測試人員裝置保持在最新狀態

Windows 測試人員的累積更新將透過 Configuration Manager 延伸模組提供給 WSUS。 這些累積更新將會以類似於 Windows 10 1903 版累積更新的頻率來發行。 Windows 測試人員累積更新位於 **Windows 測試人員發行前版本**產品類別中，分類為**安全性更新**或**更新**。 您可以使用一般軟體更新程式 (例如使用[自動部署規則](../deploy-use/automatically-deploy-software-updates.md)或[階段式部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json))，以部署 Windows 測試人員的累積更新。

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> 延長安全性更新與 Configuration Manager

[延長安全性更新 (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) 計畫是需要在特定舊版 Microsoft 產品超過終止支援日期之後繼續使用該產品的最後選項。 它包括產品延伸支援終止日期之後最長三年的重大和/或重要安全性更新 (如 [Microsoft 安全回應中心 (MSRC)](https://www.microsoft.com/msrc) 所定義)。

已超出其支援生命週期的產品不支援搭配 Configuration Manager 使用。 這包括 ESU 計畫涵蓋的任何產品。 例如，Windows 7。 依 ESU 計畫發行的安全性更新將會發佈到 Windows Server Update Services (WSUS)。 這些更新將會出現在 Configuration Manager 主控台中。 雖然 ESU 計畫涵蓋的產品已不再支援搭配 Configuration Manager 使用，但 [Configuration Manager 最新分支的最新發行版本](../../core/servers/manage/updates.md#version-details)可用來部署及安裝依該計畫發行的 Windows 安全性更新。 最新發行版本也可以用來將 Windows 10 部署到執行 Windows 7 的裝置。

與 Windows 軟體更新管理或 OS 部署無關的用戶端管理功能，將不再於 ESU 計畫涵蓋的作業系統上測試，而且我們不保證這些功能將可繼續運作。 強烈建議您儘快升級或移轉到最新的作業系統版本，以接收用戶端管理支援。


## <a name="next-steps"></a>後續步驟

開始軟體更新同步處理，根據新準則擷取軟體更新。 如需詳細資訊，請參閱[同步處理軟體更新](synchronize-software-updates.md)。
