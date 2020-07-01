---
title: 軟體中心使用者指南
titleSuffix: Configuration Manager
description: 了解「軟體中心」的特色和功能
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715400"
---
# <a name="software-center-user-guide"></a>軟體中心使用者指南

適用於：Configuration Manager (最新分支)

您組織的 IT 系統管理員會使用「軟體中心」來安裝應用程式、軟體更新，以及升級 Windows。 本使用者指南會為電腦使用者說明「軟體中心」的功能。

軟體中心會自動安裝在您 IT 組織所管理的 Windows 裝置上。 若要開始使用，請參閱[如何開啟軟體中心](#bkmk_open)。

軟體中心功能的一般相關注意事項：

- 本文將說明「軟體中心」的最新功能。 如果您的組織使用舊版但仍受支援的「軟體中心」版本，則並非所有功能都可供使用。 如需詳細資訊，請連絡 IT 系統管理員。

- IT 系統管理員可能會停用「軟體中心」的某些功能。 您的特定體驗可能會有所不同。

- 如果有多個使用者同時使用一部裝置，則工作階段識別碼最低的使用者會是唯一能在軟體中心看到所有可用部署的使用者。 例如，遠端桌面環境上的多個使用者。 工作階段識別碼較高的使用者可能無法在軟體中心看到某些部署。 例如，工作階段識別碼較高的使用者可能會看到已部署的應用程式，但無法看到未部署的套件或工作順序。 同時，工作階段識別碼最低的使用者會看到所有已部署的應用程式、套件和工作順序。 Windows 工作管理員的 [使用者] 索引標籤會顯示所有使用者與其工作階段識別碼。

- 您的 IT 系統管理員可能會變更軟體中心的色彩，並新增您組織的標誌。

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a> 如何開啟軟體中心

軟體中心會自動安裝在您 IT 組織所管理的 Windows 裝置上。 在 Windows 10 電腦上啟動「軟體中心」的最簡單方法就是按 [開始]，然後輸入 `Software Center`。 您不一定需要鍵入完整字串，Windows 就能找到最符合的結果。

:::image type="content" source="media/start-menu-software-center.png" alt-text="[開始] 功能表中的軟體中心最符合項":::

若要瀏覽 [開始] 功能表，請在 [Microsoft 端點管理員] 群組底下尋找**軟體中心**圖示。

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Microsoft 端點管理員 [開始] 功能表圖示":::

> [!NOTE]
> 上述 [開始] 功能表路徑適用於 2019 年 11 月 (1910 版) 或更新版本。 在更早版本中，資料夾名稱為 **Microsoft System Center**。

如果您在 [開始] 功能表中找不到 [軟體中心]，請連絡您的 IT 系統管理員。

## <a name="applications"></a>應用程式

:::image type="content" source="media/software-center-apps.png" alt-text="軟體中心 [應用程式] 索引標籤" lightbox="media/software-center-apps.png":::

選取 [應用程式] 索引標籤 (1)，以尋找並安裝 IT 系統管理員部署給您或此電腦的應用程式。

- **全部** (2)：顯示您可以安裝的所有可用應用程式。

- **必要** (3)：IT 系統管理員會強制安裝這些應用程式。 如果您將這其中一個應用程式解除安裝，「軟體中心」將會重新安裝它。

- **篩選** (4)：IT 系統管理員可能會建立應用程式類別。 如果可用，選取下拉式清單，即可將檢視篩選至僅限特定類別中的應用程式。 選取 [全部] 可顯示所有應用程式。

- **排序依據** (5)：重新排列應用程式清單。 此清單預設會依 [最新] 排序。 最近提供的應用程式列出時會顯示 [新增] 橫幅，而且會顯示七天。

- **搜尋** (6)：仍然找不到您要尋找的項目嗎？ 請在 [搜尋] 方塊中輸入關鍵字來尋找它！

- 切換檢視 (7)：選取圖示，即可在清單檢視與並排顯示檢視之間進行切換。 應用程式清單預設會以圖形並排方式顯示。

|圖示|檢視|說明|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**多重選取模式**|一次安裝多個應用程式。 如需詳細資訊，請參閱[安裝多個應用程式](#install-multiple-applications)。|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**清單檢視**|此檢視會顯示應用程式圖示、名稱、發行者、版本及狀態。|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**並排顯示檢視**|IT 系統管理員可以自訂圖示。 每個圖格底下都會顯示應用程式名稱、發行者及版本。|

### <a name="install-an-application"></a>安裝應用程式

從清單中選取應用程式，以查看其詳細資訊。 選取 [安裝] 來加以安裝。 如果已安裝應用程式，則有可以 [解除安裝] 的選項。

某些應用程式可能需要核准才能安裝。

- 當您嘗試安裝應用程式時，您可以輸入註解，然後**要求**該應用程式。

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="軟體中心應用程式安裝要求進行核准":::

- 軟體中心會顯示要求記錄，而且您可以取消要求。

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="軟體中心的已要求應用程式安裝":::

- 當系統管理員核准您的要求時，您即可安裝該應用程式。 如果您等待，軟體中心會在您的非上班時間自動安裝應用程式。

  :::image type="content" source="media/software-center-app-approved.png" alt-text="軟體中心的已核准應用程式安裝":::

### <a name="install-multiple-applications"></a>安裝多個應用程式

<!-- 1357126 -->
您可以一次安裝多個應用程式，而不是等到安裝完一個，再開始安裝下一個。 所選取的應用程式必須符合下列條件：

- 您可以看到該應用程式
- 該應用程式尚未下載或安裝
- IT 系統管理員不需要核准即可安裝該應用程式

一次安裝多個應用程式：

1. 選取右上角的多重選取圖示：:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. 選取要安裝的兩個或多個應用程式。 選取清單中每個應用程式左邊的核取方塊。

3. 選取 [安裝所選項目] 按鈕來開始。

應用程式正常安裝，只是現在會連續安裝。

### <a name="share-an-application"></a>共用應用程式

若要共用特定應用程式的連結，請在選取應用程式之後，選取右上角的**共用**圖示：:::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="從軟體中心共用應用程式":::

將字串**複製**並貼上到其他位置，例如電子郵件訊息。 例如 `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`。 您組織中使用軟體中心的其他任何人，都可以使用此連結來開啟相同的應用程式。

## <a name="updates"></a>更新

:::image type="content" source="media/software-center-updates.png" alt-text="軟體中心 [更新] 索引標籤" lightbox="media/software-center-updates.png":::

選取 [更新] 索引標籤 (1)，以檢視並安裝 IT 系統管理員部署至此電腦的軟體更新。  

- **全部** (2)：顯示您可以安裝的所有更新

- **必要** (3)：IT 系統管理員會強制安裝這些更新。

- **排序依據** (4)：重新排列更新清單。 此清單預設會依 [應用程式名稱:A 到 Z] 排序。

- **搜尋** (5)：仍然找不到您要尋找的項目嗎？ 請在 [搜尋] 方塊中輸入關鍵字來尋找它！

若要安裝更新，請選取 [安裝全部] \(6\)。

若只要安裝特定更新，請選取進入多重選取模式的圖示 (7)：:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
核取要安裝的更新，然後選取 [安裝所選項目]。

## <a name="operating-systems"></a>作業系統

:::image type="content" source="media/software-center-os.png" alt-text="軟體中心 [作業系統] 索引標籤" lightbox="media/software-center-os.png":::

選取 [作業系統] \(1\) 索引標籤，以檢視並安裝 IT 系統管理員部署至此電腦的 Windows 版本。  

- **全部** (2)：顯示您可以安裝的所有 Windows 版本

- **必要** (3)：IT 系統管理員會強制安裝這些升級。

- **排序依據** (4)：重新排列更新清單。 此清單預設會依 [應用程式名稱:A 到 Z] 排序。

- **搜尋** (5)：仍然找不到您要尋找的項目嗎？ 請在 [搜尋] 方塊中輸入關鍵字來尋找它！

## <a name="installation-status"></a>安裝狀態

選取 [安裝狀態] 索引標籤，以檢視應用程式的狀態。 您可能會看到下列狀態：

- **已安裝**：「軟體中心」已經在這部電腦上安裝此應用程式。

- **正在下載**：「軟體中心」正在下載要安裝在這部電腦上的軟體。

- **失敗**：軟體中心無法安裝軟體。

- **排程之後安裝時間**：顯示裝置下一個維護期間的日期和時間，用來安裝即將推出的軟體。 維護期間會由 IT 系統管理員定義。<!--1358131-->

  - 在 [全部] 和 [即將推出] 索引標籤中可以看到狀態。

  - 您可以在維護期間之前安裝，方法是選取 [立即安裝] 按鈕。

## <a name="device-compliance"></a>裝置相容性

選取 [裝置合規性] 索引標籤，以檢視這部電腦的合規性狀態。

選取 [檢查合規性]，以依據 IT 系統管理員所定義的安全性原則來評估此裝置的設定。

## <a name="options"></a>選項

選取 [選項] 索引標籤，以檢視這部電腦的額外設定。

### <a name="work-information"></a>工作資訊

指出您通常的工作時間。 IT 系統管理員可以排定在您的上班時間外進行軟體安裝。 請每天至少提供四小時來進行系統維護工作。 IT 系統管理員仍然可以在上班時間安裝重要的應用程式和軟體更新。

- 選取您使用此電腦的最早與最晚時間。 這些值預設會從 [上午 5:00 點] 到 [下午 10:00 點]。

- 選取您通常星期幾使用此電腦。 根據預設，軟體中心只會選取工作日。

指定您是否經常使用這部電腦工作。 您的系統管理員可能會自動安裝應用程式，或將其他應用程式提供給主要電腦使用。<!--3485366--> 如果您使用的電腦是主要電腦，請選取 [我經常使用這部電腦工作]。

### <a name="power-management"></a>電源管理

IT 系統管理員可以設定電源管理原則。 這些原則可協助您的組織在不使用這部電腦時節省電力。

若要讓此電腦不受這些原則管理，請選取 [請勿在這部電腦套用我 IT 部門的電源設定]。 根據預設，此設定為停用，且電腦會套用電源設定。

### <a name="computer-maintenance"></a>電腦維護

指定軟體中心在期限之前套用軟體變更的方式。

- **僅在指定的非工作時間自動安裝或解除安裝所需的軟體並重新啟動電腦**：預設會停用此設定。

- **當電腦在簡報模式時暫停軟體中心活動**：預設會啟用此設定。

當 IT 系統管理員指示時，請選取 [同步處理原則]。 此電腦會向伺服器確認是否有任何新項目，例如應用程式、軟體更新或作業系統。

### <a name="remote-control"></a>遠端控制

指定您電腦的遠端存取與遠端控制設定。

**使用您 IT 部門的遠端存取設定**：根據預設，您的 IT 部門會定義該設定，以便從遠端協助您。 此區段中的其他設定顯示您 IT 部門所定義設定的狀態。 若要變更任何設定，請先停用此選項。

- **允許的遠端存取層次**
  - **不允許遠端存取**：IT 系統管理員無法從遠端存取此電腦來協助您。
  - **僅限檢視**：IT 系統管理員只能從遠端檢視您的畫面。
  - **完整**：IT 系統管理員可以從遠端控制此電腦。 此設定是預設選項。

- **允許系統管理員在我離開時對這部電腦進行遠端控制**。 根據預設，此設定為 [是]。

- **當系統管理員嘗試遠端控制此電腦時**
  - **每次都要求權限**：此設定是預設選項。
  - **不要求權限**

- **遠端控制期間，顯示下列項目**：根據預設，這些視覺通知都已啟用，以便您知道系統管理員正在從遠端存取裝置。
  - **通知區域中的狀態圖示**
  - **桌面上的工作階段連線列**

- **播放音效**：此聲音通知可讓您知道系統管理員正在從遠端存取裝置。
  - **當工作階段開始及結束時**：此設定是預設選項。
  - **在工作階段期間重複提示**
  - **永不**

## <a name="custom-tabs"></a>自訂索引標籤

您的 IT 系統管理員可以移除預設索引標籤，或在軟體中心新增其他索引標籤。 自訂索引標籤是由您的系統管理員命名，而且那些標籤會開啟系統管理員指定的網站。 例如，您可能會有稱為「技術支援中心」的索引標籤，其會開啟您 IT 組織的技術支援中心網站。 <!--1358132-->

## <a name="more-information-for-it-administrators"></a>適用於 IT 系統管理員的詳細資訊

如需適用於 IT 系統管理員有關規劃及設定軟體中心的詳細資訊，請參閱下列文章：

- [針對軟體中心進行規劃](../../apps/plan-design/plan-for-software-center.md)
- [軟體中心用戶端設定](../clients/deploy/about-client-settings.md#software-center)
- [裝置重新啟動通知](../clients/deploy/device-restart-notifications.md)
- [遠端控制簡介](../clients/manage/remote-control/introduction-to-remote-control.md)
