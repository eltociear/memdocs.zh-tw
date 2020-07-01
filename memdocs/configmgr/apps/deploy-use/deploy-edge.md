---
title: 部署和更新 Microsoft Edge 77 版與更新版本
titleSuffix: Configuration Manager
description: 如何使用 Configuration Manager 部署和更新 Microsoft Edge 77 版和更新版本
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 141a60a72038156fff2579419e92e558dab5a9b8
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776928"
---
# <a name="microsoft-edge-management"></a>Microsoft Edge 管理

適用於：Configuration Manager (最新分支)

全新 Microsoft Edge 已準備好供企業使用。 從 Configuration Manager 1910 版開始，您可將 [Microsoft Edge 77 版和更新版本](https://docs.microsoft.com/deployedge/)部署至使用者。 PowerShell 指令碼可用來安裝選取的 Edge 組建。 此指令碼也會關閉 Edge 的自動更新，以便使用 Configuration Manager 來加以管理。

## <a name="deploy-microsoft-edge"></a><a name="bkmk_Microsoft_Edge"></a>部署 Microsoft Edge
<!--4561024-->
系統管理員可以選擇搶鮮版 (Beta)、Dev 或穩定通道 ，以及要部署的 Microsoft Edge 用戶端版本。 每個版本都納入了客戶和社群的學習與改良功能。

### <a name="prerequisites-for-deploying"></a>部署的必要條件

以 Microsoft Edge 部署為目標的用戶端：

- PowerShell [執行原則](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies)無法設定為 [受限制]。
  - 執行 PowerShell 的目的是為了執行安裝。

執行用 Configuration Manager 主控台的裝置需要下列項目的存取權：

|位置|用途|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Microsoft Edge 版本資訊|
|`http://dl.delivery.mp.microsoft.com`|Microsoft Edge 版本內容|

### <a name="verify-microsoft-edge-update-policies"></a><a name="bkmk_autoupdate"></a> 驗證 Microsoft Edge 更新原則

#### <a name="configuration-manager-version-1910"></a>Configuration Manager 1910 版

在 1910 版中，部署 Microsoft Edge 時，安裝指令碼會關閉 Microsoft Edge 的自動更新，以便能夠使用 Configuration Manager 進行管理。 您可以使用群組原則來變更此行為。 如需詳細資訊，請參閱[規劃 Microsoft Edge 部署](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies)和 [Microsoft Edge 更新原則](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies)。

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager 2002 版和更新版本
<!--4561024-->
自 2002 版開始，可建立設定為接收自動更新的 Microsoft Edge 應用程式，而非停用自動更新。 此變更可讓您選擇搭配 Configuration Manager 管理 Microsoft Edge 的更新，或允許 Microsoft Edge 自動更新。 建立應用程式時，請在 [Microsoft Edge 設定] 頁面上選取 [允許 Microsoft Edge 自動更新終端使用者裝置上的用戶端版本]。 如果曾經使用群組原則變更此行為，群組原則就會覆寫 Configuration Manager 在 Microsoft Edge 安裝期間所建立的設定。

[![Microsoft Edge 自動更新設定](./media/4561024-autoupdate-edge.png)](./media/4561024-autoupdate-edge.png#lightbox)

### <a name="create-a-deployment"></a>建立部署

使用內建的應用程式體驗建立 Microsoft Edge 應用程式，讓 Microsoft Edge 更易於管理：

1. 在主控台中的 [軟體程式庫] 下，有一個稱為 [Microsoft Edge 管理] 的新節點。
1. 從功能區選取 [建立 Microsoft Edge 應用程式]，或以滑鼠右鍵按一下 [Microsoft Edge 管理] 節點。

   ![Microsoft Edge 管理節點以滑鼠右鍵按一下動作](./media/4561024-create-microsoft-edge-application.png)

1. 在精靈 [應用程式設定] 頁面上，指定應用程式內容的名稱、描述與位置。 請確定您所指定內容位置資料夾是空的。
1. 在 [Microsoft Edge 設定] 頁面中，選取：
   - 要部署的通道
   - 要部署的版本
   - 若要**允許 Microsoft Edge 自動更新使用者裝置上的用戶端版本** (2002 版新增功能)
1. 在 [部署] 頁面上，決定是否要部署應用程式。 如果您選取 [是]，則可以指定應用程式的部署設定。 如需部署設定的詳細資訊，請參閱[部署應用程式](deploy-applications.md#bkmk_deploy-general)。
1. 在用戶端裝置上的 [軟體中心] 中，使用者可以查看並安裝應用程式。

   ![部署精靈中的 [Microsoft Edge 設定] 頁面](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>部署記錄檔

|位置|記錄檔|用途|
|---|---|---|
| 網站伺服器|SMSProv.log|若建立應用程式或部署失敗，則顯示詳細資料。|
| [變動](../../core/plan-design/hierarchy/log-files.md)|PatchDownloader.log| 若內容下載失敗，則顯示詳細資料。|
| 用戶端|  AppEnforce.log|顯示安裝資訊|

## <a name="update-microsoft-edge"></a>更新 Microsoft Edge
<!--4831871-->

從 Configuration Manager 1910 版開始，您會在 [Microsoft Edge 管理] 下看到稱為 [所有 Microsoft Edge 更新] 的節點。 此節點可協助您管理所有 Microsoft Edge 通道的更新。<!--initial edge updates released Jan 15,2020-->

1. 若要取得 Microsoft Edge 的更新，請務必針對[同步處理選取](../../sum/get-started/configure-classifications-and-products.md) [更新] 分類和 [Microsoft Edge] 產品。

   [![在軟體更新點內容中選取 Microsoft Edge 作為產品](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. 在 [軟體程式庫] 工作區中，展開 [Microsoft Edge 管理]，然後按一下 [所有 Microsoft Edge 更新] 節點。

1. 如有需要，請按一下功能區中的 [同步處理軟體更新]，開始同步處理。 如需詳細資訊，請參閱[同步處理軟體更新](../../sum/get-started/synchronize-software-updates.md)。

   ![所有 Microsoft Edge 更新節點](./media/4831871-all-microsoft-edge-updates.png)

1. 像對任何其他更新一樣地管理及部署 Microsoft Edge 更新，例如將其新增至[自動部署規則](../../sum/deploy-use/automatically-deploy-software-updates.md)。 您可以從 [所有 Microsoft Edge 更新] 節點執行的一些常見更新工作包括：

   - [建立階段式部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)
   - [手動部署軟體更新](../../sum/deploy-use/manually-deploy-software-updates.md)
   - [下載軟體更新](../../sum/deploy-use/download-software-updates.md)

## <a name="microsoft-edge-management-dashboard"></a><a name="bkmk_edge-dash"></a> Microsoft Edge 管理儀表板
<!--3871913-->
*(在 2002 版中引進)*

自 Configuration Manager 2002 開始，Microsoft Edge 管理儀表板會提供 Microsoft Edge 和其他瀏覽器使用方式的見解。 在此儀表板中，您可以：

- 查看有多少裝置已安裝 Microsoft Edge
- 查看有多少用戶端安裝了不同版本的 Microsoft Edge。
   - 此圖表不包含 Canary 通道。
- 在不同裝置上查看已安裝的瀏覽器
- 檢視裝置慣用的瀏覽器 <!--5907383-->
   - 2002 版目前的這張圖表為空白。

### <a name="prerequisites-for-the-dashboard"></a>儀表板的必要條件

在下列 Microsoft Edge 管理儀表板的[硬體清查](../../core/clients/manage/inventory/extend-hardware-inventory.md)類別中，啟用下列屬性：

- **已安裝的軟體 - Asset Intelligence (SMS_InstalledSoftware)**
   - 軟體代碼
   - 產品名稱
   - 產品版本

- **預設瀏覽器 (SMS_DefaultBrowser)**
   - 瀏覽器程式識別碼

- **瀏覽器使用量 (SMS_BrowserUsage)**
   - BrowserName
   - UsagePercentage

### <a name="view-the-dashboard"></a>檢視儀表板

從 [軟體程式庫] 工作區中，按一下 [Microsoft Edge 管理] 以查看儀表板。 按一下 [瀏覽] 並選擇另一個集合，以變更圖形資料的集合。 根據預設，下拉式清單會列出五個最大的集合。 當您選取不在清單中的集合時，新選取的集合即會佔據下拉式清單中最後一位。

[![Microsoft Edge 管理儀表板](./media/3871913-microsoft-edge-dashboard.png)](./media/3871913-microsoft-edge-dashboard.png#lightbox)

## <a name="next-steps"></a>後續步驟

[監視應用程式](monitor-applications-from-the-console.md)

[監視軟體更新](../../sum/deploy-use/monitor-software-updates.md)

[管理及監視階段式部署](../../osd/deploy-use/manage-monitor-phased-deployments.md)
