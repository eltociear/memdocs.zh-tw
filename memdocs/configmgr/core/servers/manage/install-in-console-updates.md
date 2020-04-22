---
title: 主控台內更新
titleSuffix: Configuration Manager
description: 從 Microsoft 雲端將更新安裝至 Configuration Manager
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fee0cdf72ae8975d26bebd4da765941116421c25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694586"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>安裝適用於 Configuration Manager 的主控台內更新

適用於：  Configuration Manager (最新分支)

Configuration Manager 會與 Microsoft 雲端服務同步以取得更新。 接著在 Configuration Manager 主控台內安裝這些更新。

## <a name="get-available-updates"></a>取得可用的更新

站台只會下載適用於您基礎結構和版本的更新。 根據您設定階層服務連接點的方式而定，此同步處理可以自動或手動執行︰

- 在 **線上模式**中，服務連接點會自動連線到 Microsoft 雲端服務，並下載適用的更新。  

    根據預設，Configuration Manager 每隔 24 小時就會檢查新的更新。 您可以在 Configuration Manager 中手動檢查更新。 請移至 [系統管理]  工作區，選取 [更新與服務]  節點，然後選擇功能區中的 [檢查更新]  。  

- 在**離線模式**中，服務連接點不會連線到 Microsoft 雲端服務。 若要在下載後匯入可用的更新，請[使用服務連線工具](use-the-service-connection-tool.md)。  

> [!NOTE]  
> 如有必要，請將頻外修正程式匯入您的主控台。 若要這樣做，可使用[更新註冊工具](use-the-update-registration-tool-to-import-hotfixes.md)。 這些頻外修正程式可補充您與 Microsoft 雲端服務同步處理時取得的更新。  

同步更新之後，您便可以在 Configuration Manager 主控台中進行檢視。 請移至 [系統管理]  工作區，然後選取 [更新與服務]  節點。  

- 您尚未安裝的更新會顯示為 [可用]  。  

- 您已安裝的更新會顯示為 [已安裝]  。 只顯示最近安裝的更新。 若要檢視先前安裝的更新，選取功能區中的 [歷程記錄]  。  

請先了解並規劃服務連接點的其他用途，再設定服務連接點。 下列使用可能會影響您如何設定此站台系統角色︰  

- 站台使用服務連接點來上傳您站台的使用資訊。 這項資訊可協助 Microsoft 雲端服務找出適用於您基礎結構之目前版本的更新。 如需詳細資訊，請參閱[診斷和使用方式資料](../../plan-design/diagnostics/diagnostics-and-usage-data.md)。  

若要進一步了解下載更新時會發生什麼情況，請參閱下列流程圖：  

- [流程圖 - 下載更新](download-updates-flowchart.md)  

- [流程圖 - 更新複寫](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>指派檢視及管理更新和功能的權限

若要在主控台中檢視更新，使用者必須具備以角色為基礎的系統管理安全性角色，其中包含安全性類別「更新套件」  。 此類別會授與您存取權，在 Configuration Manager 主控台中檢視和管理更新。

### <a name="about-the-update-packages-class"></a>關於更新套件類別

依預設，[更新套件]  類別 (SMS_CM_Updatepackages) 屬於下列內建安全性角色的一部分，並具有所列的權限︰  

- 具有**修改** 和 **讀取** 權限的 **系統高權限管理員** ：  

  - 如果使用者具有此安全性角色和「所有」  安全性範圍的存取權限，即可檢視和安裝更新。 使用者也可以在安裝期間啟用功能，並在站台更新之後啟用個別功能。  

  - 如果使用者具有此安全性角色和「預設」  安全性範圍的存取權限，即可檢視和安裝更新。 使用者也可以在安裝期間啟用功能，並在站台更新之後檢視功能。 但此使用者無法在站台更新之後啟用這些功能。  

- 具有**讀取** 權限的 **唯讀分析師** ：  

  - 如果使用者具有此安全性角色和**預設**範圍的存取權限，即可檢視更新，但不能安裝更新。 此使用者也可以在站台更新之後檢視功能，但不能加以啟用。  

### <a name="permissions-required-for-updates-and-servicing"></a>更新和服務的必要權限

- 使用您指派安全性角色的帳戶，其包含具有 [修改]  和 [讀取]  權限的 [更新套件]  類別。  

- 將帳戶指派給 [預設]  範圍。  

### <a name="permissions-to-only-view-updates"></a>僅檢視更新的權限

- 使用您指派安全性角色的帳戶，其包含僅具有 [讀取]  權限的 [更新套件]  類別。  

- 將帳戶指派給 [預設]  範圍。  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>站台更新後啟用功能所需的權限

- 使用您指派安全性角色的帳戶，其包含具有 [修改]  和 [讀取]  權限的 [更新套件]  類別。  

- 將帳戶指派給 [全部]  範圍。  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> 安裝主控台內更新之前  

在 Configuration Manager 主控台內安裝更新之前，請檢閱下列步驟。  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> 步驟 1：檢閱更新檢查清單  

請檢閱適用的更新檢查清單，以了解開始更新之前應採取的動作︰

- [安裝更新 2002 的檢查清單](checklist-for-installing-update-2002.md)

- [安裝更新 1910 的檢查清單](checklist-for-installing-update-1910.md)  

- [安裝更新 1906 的檢查清單](checklist-for-installing-update-1906.md)  

- [安裝更新 1902 的檢查清單](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a> 步驟 2：安裝更新之前先執行必要條件檢查工具  

安裝更新之前，請考慮執行該更新的必要條件檢查。 如果您在安裝更新之前先執行必要條件：  

- 站台會在安裝更新之前將更新檔案複寫到其他站台。  

- 當您選擇安裝更新時，必要條件檢查會再次自動執行。  

> [!NOTE]  
> 當您啟動必要條件檢查並檢視狀態時，[安裝]  階段看似作用中。 不過，站台實際上並未安裝更新。 為執行必要條件檢查，更新程序會從內容庫擷取套件。 然後，它會將套件放到複寫用快取資料夾，以便可在其中存取目前的必要條件檢查。 當您安裝更新時，會執行這個相同程序。 此行為是造成安裝階段顯示為 [進行中]  的原因。 只有 [擷取更新套件]  步驟會顯示在安裝類別中。  

稍後在安裝更新時，您可以設定更新以忽略先決條件檢查警告。  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>安裝更新之前先執行必要條件檢查工具  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [更新與服務]  節點。  

2. 選取您要執行必要條件檢查的更新套件。  

3. 選取功能區中的 [執行先決條件檢查]  。  

    當您執行必要條件檢查時，更新的內容會複寫到子站台。 檢視站台伺服器上的 **distmgr.log**，確認該內容複寫成功。  

4. 若要檢視必要條件檢查的結果：  

    1. 在 Configuration Manager 主控台中，按一下 [監視]  工作區。  

    2. 選取 [更新與服務狀態]  節點，然後尋找必要條件狀態。  

    3. 如需詳細資訊，請參閱站台伺服器上的 **ConfigMgrPrereq.log**。  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> 安裝主控台內更新  

當您準備好從 Configuration Manager 主控台內安裝更新時，請先由階層的頂層站台開始。 此站台可能是管理中心網站或獨立主要站台。  

請在正常上班時間以外針對各個站台安裝更新，以將對企業營運的影響降到最低。 安裝更新可能包含重新安裝站台元件和站台系統角色之類的動作。  

- 當管理中心網站完成安裝更新之後，子主要站台就會自動啟動更新。 此程序是預設的建議程序。 若要控制主要站台安裝更新的時間，請使用[站台伺服器的服務保留時間](service-windows.md)。  

- 當主要父站台更新完成之後，請從 Configuration Manager 主控台內手動更新次要站台。 不支援次要站台伺服器的自動更新。  

- 當您在站台更新之後使用 Configuration Manager 主控台時，系統會提示您更新主控台。  

- 站台伺服器已成功完成更新安裝之後，便會自動更新所有適用的站台系統角色。 不過，所有的發佈點不會同時重新安裝和離線更新。 反之，站台伺服器會使用站台的內容發佈設定，逐一將更新發佈至發佈點子集。 這樣一來，只有部分發佈點會離線安裝更新。 未開始更新或已完成更新的發佈點可保持線上狀態，以提供內容給用戶端。

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> 主控台內更新安裝概觀  

#### <a name="1-when-the-update-installation-starts"></a>1.開始安裝更新時

您會看到 [更新精靈]，其中顯示更新所適用的產品區域清單。  

- 在精靈的 [一般]  頁面上，視需要設定 [必要條件警告]  ：  

  - 必要條件錯誤一律會停止安裝更新。 先修正錯誤，才能成功重試更新安裝。 如需詳細資訊，請參閱[重試失敗更新的安裝](#bkmk_retry)。  

  - 必要條件警告也會停止安裝更新。 請先修正警告，再重試安裝更新。 如需詳細資訊，請參閱[重試失敗更新的安裝](#bkmk_retry)。  

  - **忽略任何必要條件檢查警告並安裝此更新 (不管遺漏的必要項)** ：將更新安裝的條件設定為忽略必要條件警告。 此選項允許繼續安裝更新。 如果您未選取此選項，更新安裝會在程序遇到警告時停止。 除非您先前已針對某個站台執行必要條件檢查並修正必要條件警告，否則請勿使用此選項。  

    [系統管理]  和 [監視]  兩工作區的 [更新與服務] 節點，其功能區中皆包含名為 [忽略必要條件警告]  的按鈕。 當更新套件無法完成安裝時，會產生先決條件檢查警告，此按鈕即變成可用。 例如，您從 [更新精靈] 安裝更新時未使用忽略必要條件警告的選項。 該更新安裝會停止並處於先決條件警告 (但不含錯誤) 的狀態。 稍後，您可以選取功能區中的 [忽略先決條件警告]  。 此動作會觸發自動接續該更新安裝，並忽略必要條件警告。 使用此選項時，會在幾分鐘後自動繼續安裝更新。  

- 當有適用於 Configuration Manager 用戶端的更新時，選擇透過一組有限的用戶端來測試用戶端更新。 如需詳細資訊，請參閱[如何測試進入生產階段前集合用戶端升級](../../clients/manage/upgrade/test-client-upgrades.md)。  

#### <a name="2-during-the-update-installation"></a>2.安裝更新期間

在安裝更新期間，Configuration Manager 會執行下列動作：  

- 重新安裝站台系統角色或 Configuration Manager 主控台這類任何受影響的元件。  

- 依據您為試驗用戶端以及[自動用戶端升級](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)所選的項目，來管理用戶端的更新。  

- 站台系統伺服器通常不需要在更新期間重新啟動。 如果角色使用 .NET，而且套件更新了該必要元件，則站台系統可能會重新啟動。  

> [!TIP]  
> 當您安裝 Configuration Manager 更新時，站台也會更新 CD.Latest 資料夾。 如需詳細資訊，請參閱 [CD.Latest 資料夾](the-cd.latest-folder.md)。  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3.安裝更新時，監視更新的進度

使用下列步驟來監視進度：  

- 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [更新與服務]  節點。 此節點會顯示所有更新套件的安裝狀態。  

- 在 Configuration Manager 主控台中，移至 [監視]  工作區，然後選取 [更新與服務狀態]  節點。 此節點只會顯示站台所安裝之目前更新套件的安裝狀態。  

    更新安裝會分成幾個階段以便監視。 針對下列每個階段，安裝狀態中的額外詳細資料包括檢視哪個記錄檔以取得詳細資訊：  

  - **下載**：這個階段僅適用於具有服務連接點的頂層站台。

  - **複寫**

  - **必要條件檢查**

  - **安裝**

  - **後續安裝**：如需詳細資訊，請參閱[後續安裝工作](#post-installation-tasks)。  

- 檢視站台伺服器上 `<ConfigMgr_Installation_Directory>\Logs` 中的 **CMUpdate.log** 檔案。  

>[!NOTE]
> 從 1906 版開始，您可以在**安裝**階段看到 [升級 ConfigMgr資料庫]  工作的狀態。
>
> - 如果資料庫升級受到封鎖，則您會收到**進行中，需要注意**的警告。
>   - cmupdate.log 會從封鎖資料庫升級的 SQL 中記錄程式名稱和 sessionid。
> - 當資料庫升級不再受到封鎖時，狀態將會重設為 [進行中]  或 [完成]  。
>   - 當資料庫升級受到封鎖時，會每隔 5 分鐘檢查一次以查看是否仍受到封鎖。

#### <a name="4-when-the-update-installation-completes"></a>4.安裝更新完成時

當第一個站台更新完成安裝之後︰  

- 子主要站台會自動安裝更新。 不需要進行其他動作。  

- 從 Configuration Manager 主控台內手動更新次要站台。 如需詳細資訊，請參閱[在次要站台上開始安裝更新](#bkmk_secondary)。  

- 在階層中的所有站台都更新至新版本之前，您的階層仍會以混合版本模式運作。 如需詳細資訊，請參閱[不同版本之間的互通性](../../plan-design/hierarchy/interoperability-between-different-versions.md)。  

#### <a name="5-update-configuration-manager-consoles"></a>5.更新 Configuration Manager 主控台

在管理中心網站或主要站台更新之後，連線至該站台的每個 Configuration Manager 主控台也必須更新。 系統會提示您更新主控台：  

- 當您開啟主控台時  

- 當您在開啟的主控台中移至新節點時  

在站台更新之後立即更新主控台。  

當主控台更新完成之後，確認主控台和站台版本是正確的。 請移至主控台左上角的 [關於 Configuration Manager]  。  

> [!Note]  
> 主控台版本與站台版本稍有不同。 主控台的次要版本會對應至 Configuration Manager 發行版本。 例如，在 Configuration Manager 1802 版中，初始站台版本是 5.0.8634.1000，而初始主控台版本為 5.**1802**.1082.1700。 組建 (1082) 和修訂 (1700) 編號可能會隨未來的 Hotfix 而有所變更。

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a> 在頂層站台上開始安裝更新  

在您階層的頂層站台上，於 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [更新與服務]  節點。 選取狀態為 [可用]  的更新，然後選擇功能區中的 [安裝更新套件]  。  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> 在次要站台上開始安裝更新  

在更新次要站台的父主要站台之後，從 Configuration Manager 主控台內更新次要站台。 若要這樣做，您可以使用 **[升級次要站台精靈]** 。  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取您要更新的次要站台，然後選擇功能區中的 [升級]  。  

2. 選取 [是]  以開始更新次要站台。  

若要監視次要站台上的更新安裝，請選取次要站台，然後選擇功能區中的 [顯示安裝狀態]  。 也請將 [版本]  欄新增至 [站台] 節點，讓您能夠檢視每個次要站台的版本。  

在某些執行個體中，主控台中的狀態未重新整理或建議更新失敗。 在次要站台成功更新之後，請使用 [重試安裝]  選項。 這個選項不會重新為次要站台安裝已成功安裝的更新，但會強制主控台更新狀態。

### <a name="post-installation-tasks"></a>後續安裝工作

當站台安裝更新時，有幾項工作在更新於站台伺服器上完成安裝之前都無法啟動。 此清單包含對站台與階層作業至關重要的後續安裝工作。 它們非常重要，所以會主動予以監視。 未直接監視的其他工作包括重新安裝站台系統角色。 若要檢視重要的後續安裝工作狀態，請在監視站台的更新安裝時，選取 [後續安裝]  工作。

並非所有的工作都會立即完成。 有些工作在每個站台完成安裝更新之前並不會啟動。 您預期的新功能可能會延遲到這些工作完成之後才會顯示。 在所有站台完成更新安裝之前，開啟的新功能並不會啟動，因此有段時間可能看不到新的功能。

後續安裝工作包括：

- **安裝 SMS_EXECUTIVE 服務**

  - 在站台伺服器上執行的重要服務。
  - 重新安裝此服務應會快速完成。

- **安裝 SMS_DATABASE_NOTIFICATION_MONITOR 元件**

  - SMS_EXECUTIVE 服務的重要站台元件執行緒。
  - 重新安裝此服務應會快速完成。

- **安裝 SMS_HIERARCHY_MANAGER 元件**

  - 在站台伺服器上執行的重要站台元件。
  - 負責在站台系統伺服器上重新安裝角色。 不會顯示重新安裝個別站台系統角色的狀態。
  - 重新安裝此服務應會快速完成。

    > [!Note]
    > 某些 Configuration Manager 站台角色會共用用戶端架構。 例如，管理點和提取發佈點。 當這些角色更新時，這些伺服器上的用戶端版本也會一起更新。 如需詳細資訊，請參閱[如何升級用戶端](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。

- **安裝 SMS_REPLICATION_CONFIGURATION_MONITOR 元件**

  - 在站台伺服器上執行的重要站台元件。
  - 重新安裝此服務應會快速完成。

- **安裝 SMS_POLICY_PROVIDER 元件**

  - 只在主要站台上執行的重要站台元件。
  - 重新安裝此服務應會快速完成。

- **正在監視複寫初始化**

  - 此工作只會顯示在管理中心網站和子主要站台。
  - 依存於 SMS_REPLICATION_CONFIGURATION_MONITOR。
  - 應會快速完成。

- **更新 Configuration Manager 用戶端生產階段前套件**

  - 此工作即使在用戶端生產階段前 (也稱為用戶端試驗) 還不能使用時也會顯示。
  - 在階層中的所有站台都完成安裝更新之前無法啟動。

- **更新站台伺服器上的用戶端資料夾**

  - 如果您在生產階段前使用用戶端，則不會顯示此工作。  
  - 應會快速完成。

- **更新 Configuration Manager 用戶端套件**

  - 如果您在生產階段前使用用戶端，則不會顯示此工作。  
  - 只有在所有站台都安裝更新之後，才會完成。  

- **開啟功能**

  - 此工作只會在階層的頂層站台顯示。
  - 在階層中的所有站台都完成安裝更新之前無法啟動。
  - 不會顯示個別功能。

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> 重試失敗更新的安裝  

當更新安裝失敗時，檢閱主控台內的回饋，以找出適用於警告和錯誤的解決方式。 如需詳細資訊，請檢視站台伺服器上的 **ConfigMgrPrereq.log**。 重試安裝更新之前，您必須先修正錯誤，並且應該修正警告。  

> [!TIP]  
> 如果無法下載或複寫某個更新，請使用[更新重設工具](update-reset-tool.md)。  

當您準備好要重試安裝更新時，請選取失敗的更新，然後選擇適用的選項。 更新安裝重試行為取決於您啟動重試的節點以及所使用的重試選項。  

### <a name="retry-installation-for-the-hierarchy"></a>重試階層安裝

當更新處於下列其中一種狀態時，重試整個階層的更新安裝：  

- 已通過必要條件檢查，但有一或多個警告。[更新精靈] 中未設定選項可以讓使用者忽略必要條件檢查警告 ([更新與服務]  節點中 [忽略必要條件警告]  的更新值為 [否]  )。

- 必要條件失敗

- 安裝失敗  

- 將內容複寫至站台失敗

請移至 [系統管理]  工作區，然後選取 [更新與服務]  節點。 選取更新，然後選擇下列其中一個選項：  

- **重試**：當您從 [更新與服務]  選擇 [重試]  時，更新安裝會再次啟動，並自動忽略必要條件警告。 如果先前內容複寫失敗，則會重新複寫更新的內容。  

- **忽略必要條件警告**：如果因為警告導致更新安裝停止，您可以接著選擇 [忽略必要條件警告]  。 此動作會在幾分鐘後繼續安裝更新，並使用 [忽略必要條件警告] 選項。

### <a name="retry-installation-for-the-site"></a>重試站台的安裝

當更新處於下列其中一種狀態時，在特定站台上重試更新安裝：  

- 已通過必要條件檢查，但有一或多個警告。[更新精靈] 中未設定選項可以讓使用者忽略必要條件檢查警告 ([更新與服務] 節點中 [忽略必要條件警告]  的更新值為 [否]  )。  

- 必要條件失敗

- 安裝失敗

移至 [監視]  工作區，然後選取 [Site Servicing Status] \(站台服務狀態\)  節點。 選取更新，然後選擇下列其中一個選項：  

- **重試**：當您從 [Site Servicing Status] \(站台服務狀態\)  選擇 [重試]  時，只會重新啟動該站台的更新安裝。 但這項重試與從 [更新與服務]  節點中執行 [重試]  不同，其不會忽略必要條件警告。  

- **忽略必要條件警告**：如果因為警告導致更新安裝停止，您可以接著選取 [忽略先決條件警告]  。 此動作會在幾分鐘後繼續安裝更新，並使用 [忽略必要條件警告] 選項。  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> 當站台安裝更新之後  

進行站台更新之後，請檢閱適用版本的更新後檢查清單：  

- [2002 版的更新後檢查清單](checklist-for-installing-update-2002.md#post-update-checklist)

- [1910 版的更新後檢查清單](checklist-for-installing-update-1910.md#post-update-checklist)  

- [1906 版的更新後檢查清單](checklist-for-installing-update-1906.md#post-update-checklist)  

- [1902 版的更新後檢查清單](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> 從更新啟用選擇性功能  

更新包含一或多個選擇性功能時，有機會在您的階層中啟用這些功能。 在安裝更新時啟用功能，或者稍後返回主控台以啟用選擇性功能。

若要檢視可用功能及其狀態，請在主控台中，移至 [系統管理]  工作區，展開 [更新與服務]  ，然後選取 [功能]  節點。

非選擇性功能會自動予以安裝。 這類功能不會出現在 [功能]  節點上。  

> [!Important]  
> 在多站台階層中，只從系統管理中心網站啟用選擇性或發行前版本的功能。 此行為可避免整個階層中不會發生衝突。 <!--507197-->  

當您啟用新功能或發行前功能時，Configuration Manager 階層管理員 (HMAN) 必須在該功能提供使用前，先處理變更。 變更通常要立即處理。 完成時間最多需要 30 分鐘，視 HMAN 處理週期而定。 處理好變更之後，請重新啟動主控台，之後才能使用功能。

從 2002 版開始，<!--5834830--> 當 Microsoft 端點管理員系統管理中心或內部部署 Configuration Manager 安裝的其他附加雲端服務中有新雲端式功能可用時，現在即可在 Configuration Manager 主控台中加入這些新功能。

### <a name="list-of-optional-features"></a>選擇性功能清單

下列是最新版 Configuration Manager 中的選擇性功能：<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [BitLocker 管理](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [將集合成員資格結果同步至 Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Azure Active Directory 使用者群組探索](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [ 應用程式群組](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [工作順序偵錯工具](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [套件轉換管理員](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [共同受控裝置的用戶端應用程式](../../../comanage/workloads.md#client-apps) (先前稱為*適用於共同受控裝置的行動應用程式*) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [協力廠商軟體更新](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [針對每部裝置的使用者核准應用程式要求](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [建立及執行指令碼](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Surface 驅動程式更新](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [PFX 建立](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics 連接器](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender 惡意探索防護原則](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN for Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [服務叢集感知集合 (伺服器群組)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello 企業版](../../../protect/deploy-use/windows-hello-for-business-settings.md) (先前稱為 *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> 如需需要同意才能啟用之功能的詳細資訊，請參閱[發行前版本功能](pre-release-features.md)。  
>
> 如需僅在技術預覽分支提供之功能的詳細資訊，請參閱[技術預覽](../../get-started/technical-preview.md)。

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> 使用更新的發行前版本功能

最新分支包含發行前版本功能，可用來在生產環境中進行早期測試。 如需詳細資訊，請參閱[發行前版本功能](pre-release-features.md)。

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> 常見問題集

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>為什麼我在主控台中看不到特定的更新？

如果您在與 Microsoft 雲端服務成功同步之後在主控台中找不到特定更新，這個行為可能是因為下列其中一個原因所造成：  

- 更新需要您的基礎結構未使用的設定，或者目前的產品版本未滿足接收更新的必要條件。  

    如果您認為已具備某項更新的必要設定和必要條件，但仍缺少該項更新，請確認服務連接點處於線上模式。 然後使用 [更新與服務]  節點中的 [檢查更新]  選項來強制執行檢查。 如果您的服務連接點處於離線模式，請使用服務連線工具來手動與雲端服務進行同步。  

- 您的帳戶缺少以角色為基礎的正確系統管理權限，無法在 Configuration Manager 主控台中檢視更新。 如需詳細資訊，請參閱[管理更新的權限](#assign-permissions-to-view-and-manage-updates-and-features)。  
