---
title: 更新與服務
titleSuffix: Configuration Manager
description: 了解稱為更新與服務的主控台內服務方法，可讓您輕鬆尋找並安裝建議的更新。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f38b8662d4d7b5e7897d0c43560a5e2a4672eee6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704316"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Configuration Manager 的更新與服務

適用於：*Configuration Manager (最新分支)*

Configuration Manager 使用稱為**更新與服務**的主控台內服務方法。 此主控台內方法可針對您的 Configuration Manager 基礎結構，輕鬆地尋找並安裝建議的更新。 主控台內的服務會以頻外更新的方式進行增補，例如 Hotfix。 這些頻外更新適用於需要解決其環境特有問題的客戶。  

> [!TIP]  
> 「升級」  、「更新」  及「安裝」  等詞彙是用來描述 Configuration Manager 中的三種不同概念。 如需如何使用每個詞彙的詳細資訊，請參閱[關於升級、更新及安裝](../../understand/upgrade-update-install.md)。  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> 基準和更新版本  

在新階層中安裝新的站台時，請使用最新的基準版本。

- 同時使用基準版本從 System Center 2012 Configuration Manager 進行升級。  

- 升級至 Configuration Manager 最新分支之後，請勿使用基準版本來保持在最新狀態。 相反地，只有使用[主控台內更新](install-in-console-updates.md)才能更新為最新版本。  

- 會定期發行額外的基準版本。 當您使用最新的基準版本安裝新的階層時，請避免在額外的升級基礎結構以更新到最新狀態之後，安裝 Configuration Manager 的過期或不支援版本。  

安裝基準版本之後，其他的 Configuration Manager 版本會在主控台內的更新中提供。 主控台內更新會將您的基礎結構更新為最新版本的 Configuration Manager。  

- 您安裝主控台內更新以更新頂層站台的版本。  

- 您在管理中心網站所安裝的更新會自動在子主要站台中安裝。 使用主要站台的維護視窗可控制此時間。  

- 在主控台中手動將次要站台更新為新版本。  

當您安裝更新時，更新會在站台伺服器名為 **CD.Latest** 的資料夾中儲存該版本的安裝檔案。 如需這些檔案的詳細資訊，請參閱 [CD.Latest 資料夾](the-cd.latest-folder.md)。  

- 在站台復原期間使用 CD.Latest 資料夾中的檔案。 此外，當您的階層不再執行基準版本時，使用這些檔案來安裝其他站台。  

- 您無法使用 CD.Latest 中的安裝檔案來安裝新階層的第一個站台，或從 System Center 2012 Configuration Manager 升級站台。  

### <a name="version-details"></a>版本詳細資料

部分 Configuration Manager 的更新會在針對現有基礎結構的主控台內更新版本，及新的基準版本中提供。  

#### <a name="supported-versions"></a>支援的版本

下列支援的 Configuration Manager 版本目前提供基準版本、更新版本或這兩個版本：  

| 版本 | 可用時間 | [支援結束日期](current-branch-versions-supported.md) | 基準 | 主控台內更新 |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 2020 年 5 月 | 2021 年 10 月 1 日 | 是<sup>[附註 1](#bkmk_note1)</sup> | 是 |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 2019 年 11 月 29 日 | 2021 年 5 月 29 日 | 否 | 是 |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 2019 年 7 月 26 日 | 2021 年 1 月 26 日 | 否 | 是 |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 2019 年 3 月 27 日 | 2020 年 9 月 27 日 | 是<sup>[附註 1](#bkmk_note1)</sup> | 是 |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 2018 年 11 月 27 日 | 2020 年 12 月 1 日 | 否 | 是 |

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**附註 1：** </sup>基準媒體會當作[大量授權服務中心](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) 的下列版本一部分來提供：
>
> - System Center Config Mgr (最新分支)
> - System Center 2016 Datacenter
> - System Center 2016 Standard  
>
> 例如，在 VLSC 中搜尋 `System Center Config Mgr (current branch)`。 在檔案清單中尋找基準媒體，然後下載該版本。  

#### <a name="historical-versions"></a>歷程記錄版本

下表列出不受支援之 Configuration Manager 最新分支的歷程記錄版本：

| 版本 | 可用時間 | 支援結束日期 | 基準 | 主控台內更新 |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 2018 年 7 月 31 日 | 2020 年 1 月 31 日 | 否 | 是 |
| **1802** <br /> (5.00.8634) | 2018 年 3 月 22 日 | 2019 年 9 月 22 日 | 是 | 是 |
| **1710** <br /> (5.00.8577) | 2017 年 11 月 20 日 | 2019 年 5 月 20 日 | 否 | 是 |
| **1706** <br /> (5.00.8540) | 2017 年 7 月 31 日 | 2018 年 7 月 31 日 | 否 | 是 |
| **1702** <br /> (5.00.8498) | 2017 年 3 月 27 日 | 2018 年 3 月 27 日 | 是 | 是 |
| **1610** <br /> (5.00.8458) | 2016 年 11 月 18 日 | 2017 年 11 月 18 日 | 否 | 是 |
| **1606** <br /> (5.00.8412.1000) | 2016 年 7 月 22 日 | 2017 年 7 月 22 日 | 否 | 是 |
| **1606 含 KB3186654** <br />(5.00.8412.1307) | 2016 年 10 月 12 日 | 2017 年 10 月 12 日 | 是 | 否 |
| **1602** <br /> (5.00.8355) | 2016 年 3 月 11 日 | 2017 年 3 月 11 日 | 否 | 是 |
| **1511** <br /> (5.00.8325) | 2015 年 12 月 8 日 | 2016 年 12 月 8 日 | 是 | 否 |  

#### <a name="how-to-check-the-version"></a>如何檢查版本

若要檢查 Configuration Manager 站台的版本，請在主控台中，移至主控台左上角的 [關於 Configuration Manager]  。 此對話方塊會顯示站台和主控台版本。  

> [!Note]  
> 主控台版本與站台版本稍有不同。 主控台的次要版本會對應至 Configuration Manager 發行版本。 例如，在 Configuration Manager 1802 版中，初始站台版本是 5.0.8634.1000，而初始主控台版本為 5.**1802**.1082.1700。 組建 (1082) 和修訂 (1700) 編號可能會隨未來的 Hotfix 而有所變更。

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> 主控台內更新及服務  

當您使用 Configuration Manager 最新分支的生產環境就緒安裝時，大部分更新在**更新及服務**通道中均有提供。 這個方法會識別、下載和提供適用於您目前基礎結構版本和設定的更新。 其中只會包含 Microsoft 建議所有客戶進行的更新。

這些更新包括：  

- 新版本，例如 1906、1910 或 2002 版。

- 更新，包括您目前版本的新功能。

- 適用於您 Configuration Manager 版本的 Hotfix，所有客戶均應安裝。

    > [!Note]  
    > 從 1902 版開始，主控台內的 Hotfix 現在已取代關聯性。 如需詳細資訊，請參閱[主控台內 Hotfix 的取代](#bkmk_supersede)。

主控台內更新可提供更高的穩定性，並可解決常見的問題。 這些更新會取代舊版產品所看到的更新類型，例如 Service Pack、累積更新、適用於所有客戶的 Hotfix 以及Microsoft Intune 的延伸模組。

這些主控台內更新可適用於以下一或多個系統：  

- 主要和管理中心網站伺服器  

- 站台系統角色和站台系統伺服器  

- SMS 提供者執行個體  

- Configuration Manager 主控台  

- Configuration Manager 用戶端  

Configuration Manager 會為您探索新的更新。 當您同步處理 Configuration Manager 服務連接點與 Microsoft 雲端服務時，請注意下列行為：  

- 當您的服務連接點處於線上模式時，您的站台會每天與 Microsoft 同步處理。 它會自動識別適用於您基礎結構的新更新。 若要下載更新和可轉散發檔案，裝載服務連點站台系統角色的電腦會使用**系統**內容來存取下列網際網路位置︰go.microsoft.com 和 download.microsoft.com。 如需服務連接點所使用之其他位置的詳細資訊，請參閱[網際網路存取需求](../deploy/configure/about-the-service-connection-point.md#bkmk_urls)。  

- 當您的服務連接點處於離線模式時，請使用服務連線工具來手動與 Microsoft 雲端進行同步。 如需詳細資訊，請參閱[使用服務連線工具](use-the-service-connection-tool.md)。  

- 主控台內更新會取代需要個別尋找和安裝個別更新、Service Packs 及新功能的需求。  

- 只安裝您所選擇的主控台內更新。 安裝某些更新時，您可以選取要啟用及使用的個別功能。 如需詳細資訊，請參閱[從更新啟用選擇性功能](install-in-console-updates.md#bkmk_options)。  

當您安裝主控台內更新時，會發生下列流程：  

- 會自動執行必要條件檢查。 您也可以在開始安裝前手動先執行這項檢查。  

- 它會在您環境中的頂層站台安裝。 如果有的話，此站台會是管理中心網站。 在階層中，會自動在主要站台上安裝更新。 使用[站台伺服器的服務保留時間](service-windows.md)，控制每個主要站台伺服器可以更新的時間。  

- 站台伺服器更新後，所有受影響的站台系統角色都會自動更新。 這些角色包括 SMS 提供者的執行個體。 站台安裝更新之後，Configuration Manager 主控台也會提示主控台使用者更新主控台。  

- 如果更新包括 Configuration Manager 用戶端，您可以選擇在進入生產階段前環境中測試更新，或立即將更新套用到所有用戶端。  

- 更新主要站台之後，次要站台不會自動更新。 相反地，您必須手動起始次要站台的更新。  

> [!NOTE]  
> Configuration Manager 最新分支、長期維護分支和 Technical Preview 分支是不同的版本。 適用於一個分支的更新無法作為其他分支的主控台內更新。 如需有關可用分支的詳細資訊，請參閱[我應該使用哪個 Configuration Manager 分支？](../../understand/which-branch-should-i-use.md)。

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a> 主控台內 Hotfix 的取代

<!-- 3229613 -->
從 1902 版開始，主控台內的 Hotfix 現在已取代關聯性。 當 Microsoft 發佈新的 Configuration Manager Hotfix 時，主控台不會顯示這個新 Hotfix 所取代的任何 Hotfix。 這個新行為可協助您更充分地判斷要安裝的 Hotfix。

### <a name="supersedence-example"></a>取代範例

有可用的三個 Hotfix：Hotfix-A、Hotfix-B 和 Hotfix-C。 Hotfix-B 取代 Hotfix-A，Hotfix-C 取代 Hotfix-B。

|Hotfix-A|Hotfix-B|Hotfix-C|主控台內檢視|
|--------|--------|--------|---------------|
|未安裝|未安裝|未安裝|顯示所有三個 Hotfix|
|已安裝|已安裝|未安裝|Hotfix-B 顯示為已安裝<br/>Hotfix C 顯示為已準備好安裝|
|未安裝|未安裝|已安裝|Hotfix-C 顯示為已安裝|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> 頻外 Hotfix  

某些 Hotfix 是針對解決特定問題而發行，因此可用性十分有限。 其他 Hotfix 適用於所有客戶，但無法使用主控台內的方法來安裝。 這些修正程式是以頻外方式傳送，並不會在 Microsoft 雲端服務中出現。  

一般而言，當您想要修正或解決 Configuration Manager 部署問題時，您可以在 Microsoft 客戶支援服務、Microsoft 支援知識庫文章或 [Configuration Manager 小組部落格](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog)中了解頻外 Hotfix。

請使用下列兩個方法之一，手動安裝這些修正程式：  

### <a name="update-registration-tool"></a>更新註冊工具

此工具可手動將 Hotfix 匯入您的 Configuration Manager 主控台。 然後安裝更新，如同自動探索的主控台內更新。  

使用下列檔案名稱結構的 Hotfix 會使用此方法：  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

如需詳細資訊，請參閱[使用更新註冊工具來匯入 Hotfix](use-the-update-registration-tool-to-import-hotfixes.md)。  

### <a name="hotfix-installer"></a>Hotfix 安裝程式

使用此工具手動安裝無法使用主控台內方法安裝的 Hotfix。  

使用下列檔案名稱結構的修正程式會使用此方法：  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

如需詳細資訊，請參閱[使用 Hotfix 安裝程式來安裝更新](use-the-hotfix-installer-to-install-updates.md)。  

## <a name="next-steps"></a>後續步驟

下列文章可協助您了解如何尋找並安裝 Configuration Manager 的不同更新類型：  

- [安裝主控台內更新](install-in-console-updates.md)  

- [使用服務連線工具](use-the-service-connection-tool.md)  

- [使用更新註冊工具來匯入 Hotfix](use-the-update-registration-tool-to-import-hotfixes.md)  

- [使用 Hotfix 安裝程式來安裝更新](use-the-hotfix-installer-to-install-updates.md)  

如需 Technical Preview 分支的詳細資訊，請參閱 [Technical Preview](../../get-started/technical-preview.md)。
