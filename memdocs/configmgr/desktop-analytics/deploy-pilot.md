---
title: 如何部署至試驗
titleSuffix: Configuration Manager
description: 部署至電腦分析試驗群組的操作指南。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3aa722415248ad9275c6ad065f0120bfe78d3ce4
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311215"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>如何使用電腦分析部署至試驗

電腦分析優點之一是協助找出能提供最大因素涵蓋範圍的最小一組裝置。 其著重於對於 Windows 升級與更新試驗最重要的因素。 確定試驗更成功可讓您加快腳步，並大刀闊斧地部署生產環境。  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>識別裝置

第一步是找出要包含在試驗中的裝置。 電腦分析會根據回報的資料來建議裝置，您則負責納入或更換本清單中的裝置。

1. 請移至[電腦分析入口網站](https://aka.ms/desktopanalytics)，並在 [管理] 群組中選取 [部署計劃]。

1. 選取一項部署計劃。

1. 在 [部署計劃] 功能表的 [準備] 群組中，選取 [識別試驗]。

您會看到電腦分析的資料，其顯示建議的裝置數目，包括最佳涵蓋範圍。 此演算法主要基於重要和重大應用程式的使用方式，以及硬體設定的廣度。

針對其他建議的裝置清單採取下列動作：

- **全部新增至試驗**：將所有建議的裝置新增至試驗群組
- **新增至試驗**：僅新增個別裝置
- **更換**試驗中的任何特定裝置

當將**建議**的裝置新增至 [已包含] 試驗清單時，您試驗中的關鍵和重要資產涵蓋範圍和備援也會增。 較高程度的備援表示，所涵蓋資產在統計上有大量裝置屬於您的試驗。

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>全域試驗

您也可以制定試驗要包含或排除哪些 Configuration Manager 集合的全系統決策。 在主要 [電腦分析] 功能表的 [全域設定] 群組中，選取 [Global pilot] \(全域試驗\)。

如果您將多個 Configuration Manager 階層連線到相同的電腦分析執行個體，階層的顯示名稱會在通用試驗設定中的集合名稱之前加上首碼。 此名稱是 Configuration Manager 主控台中電腦分析連線上的 [顯示名稱] 屬性。<!-- 4814075 -->

> [!NOTE]
> 對多個階層的支援需要 Configuration Manager 1910 版或更新版本。

- 請不要包含超過已註冊裝置總數 20% 的集合至電腦分析。 如果您包含大型集合，入口網站會顯示警告。 您可以包含多個小型集合，而不讓系統發出警告，但仍應注意試驗中的裝置數目。 <!-- 6079184 -->

- 若要針對特定 Configuration Manager 階層中的部署計劃取得精確的試驗建議，請只包含來自該階層的集合。

### <a name="example"></a>範例

- 在 Configuration Manager 中設定電腦分析連線來鎖定**所有系統**集合為目標。 此動作會向服務註冊所有用戶端。

- 您也可以設定與電腦分析同步處理的其他集合：

  - 所有 Windows 10 用戶端 (3,000 部裝置)

  - 所有 IT 裝置 (總共 200 部裝置，其中 150 部執行 Windows 10)

  - CEO 辦公室 (20 部裝置)

- 在 [Global pilot] \(通用試驗\) 設定中，您包含**所有 Windows 10 用戶端**集合。 排除 **CEO 辦公室**集合。

- 您會建立部署計劃，並選取**所有 IT 裝置**集合作為您的**目標群組**。 您想要部署計劃僅用於 IT 部門中的裝置。

- [包含的試驗裝置] 清單包含您**目標群組**兩個集合中的部分裝置：**所有 IT 裝置**與全域試驗*包含* 清單：**所有 Windows 10 用戶端**。 此清單中有 150 部裝置，因為**所有 IT 裝置**集合中只有 150 部裝置執行 Windows 10。

- [其他建議的裝置] 清單包含來自您**目標群組**的一組裝置，可為重要資產提供最大涵蓋範圍和備援。 在這份清單中，電腦分析會排除全域試驗「排除」清單中的所有裝置：**CEO 辦公室**。

## <a name="address-issues"></a>處理問題

使用電腦分析入口網站檢閱任何報可能有礙部署的資產問題報告。 然後核准、拒絕或修改建議的修正。 在試驗部署開始之前，所有項目都必須標示為 [就緒] 或 [就緒 (有補救)]。

1. 請移至[電腦分析入口網站](https://aka.ms/desktopanalytics)，並在 [管理] 群組中選取 [部署計劃]。  

2. 選取一項部署計劃。  

3. 在 [部署計劃] 功能表的 [準備] 群組中，選取 [準備試驗]。  

4. 在 [應用程式] 索引標籤上，檢閱需要輸入的應用程式。  

5. 針對每項應用程式，選取應用程式名稱。 在 [資訊] 窗格中檢閱建議，然後選取升級決策。 如果您選擇 [未檢閱] 或 [無法]，則電腦分析不會在試驗部署中包含具有此應用程式的裝置。 如果您選擇  [就緒 (有補救)]，請使用**補救附註**來擷取處理問題時須採取的動作，例如「重新安裝」或「尋找製造商的建議版本」。

6. 針對其他資產重複此檢閱。  

如需協助進行此檢閱程序的詳細資訊，請參閱[相容性評量](compat-assessment.md)。

## <a name="create-software"></a>建立軟體

您必須先在 Configuration Manager 中建立軟體物件，才可以部署 Windows。 如需詳細資訊，請參閱 [Windows 10 就地升級工作順序](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)。

## <a name="deploy-to-pilot-devices"></a>部署至試用裝置

Configuration Manager 會使用電腦分析的資料來建立試驗和生產環境部署集合。 這些集合位於 [資產與合規性] 工作區，[裝置集合] 節點，[部署計劃] 資料夾。

> [!IMPORTANT]
> 這些集合是由電腦分析部署計劃的 Configuration Manager 管理的。 不支援手動變更。 如果您刪除其中一個集合，電腦分析將無法正常執行，而且您必須再次[連線 Configuration Manager](connect-configmgr.md)。<!--7208090-->

請使用下列程式建立電腦分析整合的階段式部署，以在每個部署階段後確定裝置狀況良好：

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]、展開 [電腦分析服務]，然後選取 [部署計劃] 節點。  

2. 選取您的部署計劃，然後在功能區中選取 [部署計劃詳細資料]。  

3. 選取功能區中的 [建立階段式部署]。 此動作會啟動建立階段式部署精靈。

    > [!Tip]  
    > 如果您只想為試驗集合建立傳統的工作順序部署，請在 [試驗狀態] 圖格中選取 [部署]。 此動作會啟動部署軟體精靈。 如需詳細資訊，請參閱 [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md)。  

4. 輸入部署名稱，然後選取要使用的工作順序。 使用 [自動建立預設的兩階段部署] 選項，然後設定下列集合：  

    - **第一個集合**：尋找並選取此部署計劃的**試驗**集合。 此集合的標準命名慣例為 `<deployment plan name> (Pilot)`。

    - **第二個集合**：尋找並選取此部署計劃的**生產環境**集合。 此集合的標準命名慣例為 `<deployment plan name> (Production)`。

    > [!Note]  
    > 透過電腦分析整合，Configuration Manager 可自動建立部署計劃的試驗和生產環境集合。 這些集合需要一些時間先行同步，才能供您使用。 如需詳細資訊，請參閱[疑難排解 - 資料延遲](troubleshooting.md#data-latency)。<!-- 4984639 -->
    >
    > 這些集合會保留供電腦分析部署計劃裝置使用。 不支援手動變更這些集合。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 請完成精靈以設定階段式部署。 如需詳細資訊，請參閱[建立階段式部署](../osd/deploy-use/create-phased-deployment-for-task-sequence.md)。

    > [!Note]  
    > 針對 [在延遲期間 (天) 之後自動開始此階段]，請使用預設設定 。 必須符合下列準則才能開始第二階段：
    >
    > 1. 第一階段達到成功的**部署成功百分比**準則。 您可以在階段式部署中設定此設定。
    > 1. 您需要在電腦分析中檢閱並制定升級決策，以將重要和重大資產標示為 [就緒]。 如需詳細資訊，請參閱[檢閱需要升級決策的資產](deploy-prod.md#bkmk_review)。
    > 1. 電腦分析會同步處理任何生產環境裝置符合*就緒*準則的 Configuration Manager 集合。

> [!Important]  
> 這些集合會隨著成員資格變更，繼續同步處理。 例如，如果您找出資產問題，並將其標示為 [無法]，則擁有該資產的裝置即不再符合*就緒*準則。 這些裝置會從生產環境部署集合中卸載。

## <a name="monitor"></a>監視

### <a name="configuration-manager-console"></a>Configuration Manager 主控台

開啟部署計劃。 [正在準備升級決策 - 整體狀態] 圖格會提供部署計劃的狀態摘要。 此狀態適用於試驗和生產環境集合。 裝置可能屬於下列其中一個類別：

- **最新**：已升級為此部署計劃目標 Windows 版本的裝置

- **升級決策完成**：下列狀態之一：

  - 狀態為 [就緒] 或 [就緒 (有補救)] 且有值得注意資產的裝置

  - 狀態為 [封鎖]、[[更換裝置]](about-deployment-plans.md#plan-assets) 或 [重新安裝裝置] 的裝置

- **未檢閱**：狀態為 [未檢閱] 或 [正在檢閱] 且有值得注意資產的裝置

使用下列動作更新 [試驗狀態] 及 [生產環境狀態] 圖格的裝置狀態：

- 變更相容性評定
- 裝置升級至目標 Windows 版本
- 部署進度

您也可以使用 Configuration Manager 部署監視，方式與任何其他工作順序部署相同。 如需詳細資訊，請參閱[監視 OS 部署](../osd/deploy-use/monitor-operating-system-deployments.md)。

### <a name="desktop-analytics-portal"></a>電腦分析入口網站

使用[電腦分析入口網站](https://aka.ms/desktopanalytics)檢視任何部署計劃的狀態。 選取部署計，然後選取 [計劃概觀]。

![電腦分析的部署計劃概觀螢幕擷取畫面](media/deployment-plan-overview.png)

選取 [試驗] 圖格。 它會摘要說明試驗部署目前的狀態。 此圖格也會顯示未啟動、進行中、已完成或傳回問題的裝置數目資料。

所有回報錯誤或其他問題的裝置，也會列在右側的試驗詳細資料區域中。 若要取得回報問題的詳細資料，請選取 [檢閱]。 此動作會將檢視變更為 [部署狀態] 頁面

[部署狀態] 頁面會列出下列類別的裝置：

- 未開始
- 進行中
- Completed
- 需要注意 - 裝置
- 需要注意 - 問題

[需要注意] 類別會顯示相同的資訊，但以不同方式排序。

選取任一檢視的特定列表方式，以取得更多有關已偵測到問題的詳細資料。

當處理這些部署問題時，儀表板會繼續顯示裝置的進度。 它會隨著裝置從**需要注意**移至**已完成**而更新。

## <a name="next-steps"></a>後續步驟

讓試驗執行一段時間，以收集操作資料。 鼓勵試驗裝置的使用者測試應用程式。

當試驗部署達到成功準則後，請移至下一篇文章來部署至生產環境。
> [!div class="nextstepaction"]  
> [部署至生產環境](deploy-prod.md)  
