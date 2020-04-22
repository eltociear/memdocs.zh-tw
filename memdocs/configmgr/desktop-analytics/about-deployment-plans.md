---
title: 電腦分析的部署計劃
titleSuffix: Configuration Manager
description: 了解電腦分析的部署計劃
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c14eb9127b096f7fc4e4680735867913ea877f54
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706626"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>關於電腦分析的部署計劃

電腦分析會收集並分析組織中的裝置、應用程式和驅動程式資料。 以此分析和您的輸入為基礎，您可使用服務來建立適合 Windows 10 的部署計劃。 部署計劃包含下列功能：  

- 自動建議要包含在試驗中的裝置  

- 找出相容性問題並建議緩和措施  

- 在更新前後及更新期間，評定部署的健全狀況  

- 追蹤部署進度  

您要執行下列動作以完善部署計劃：  

- 定義想要部署的 Windows 10 版本  

- 選擇想要部署的目標裝置群組  

- 建立部署的整備規則  

- 定義應用程式的重要性  

- 根據自動建議選擇試驗裝置  

- 決定如何根據電腦分析的建議修正應用程式問題  

根據預設，電腦分析每天都會重新整理部署計劃資料。 對部署計劃進行的任何變更 (例如指派應用程式的重要性或選擇要包含在試驗中的裝置，處理時間最多需要 24小時。 若要加速處理，請要求重新整理隨選資料。 如需詳細資訊，請參閱[電腦分析常見問題集](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

將電腦分析連線到 Configuration Manager 之後，請在部署計劃中選取集合。 然後，此整合可讓您根據電腦分析的資料，將 Windows 部署至集合。



## <a name="readiness-rules"></a>整備規則

部署計劃中可使用下列整備規則：

- 裝置是否自動從 Windows Update 取得驅動程式。 如果裝置從 Windows Update 獲得驅動程式更新，則在整備評定期間發現的任何驅動程式問題都會自動標示為 [就緒]  。  

- Windows 應用程式的低安裝計數閾值。 如果安裝此應用程式的電腦百分比高於此閾值，則部署計劃會將應用程式標示為 [值得注意]  。 此標籤表示您可以決定應用程式在試驗階段中對測試的重要程度。  


## <a name="plan-assets"></a>規劃資產

<!-- 4670224 -->

雖然 [[資產]](about-assets.md) 區域也會顯示裝置和應用程式，但特定部署計劃下的 [規劃資產]  區域會包含其他資訊。

### <a name="devices"></a>裝置

請參閱部署計劃中每部裝置的 **Windows 升級決策**。

Windows 升級決策為**更換裝置**的可能原因如下：

- 未通過 Windows 10 的必要處理器檢查。 如需詳細資訊，請參閱[最小硬體需求](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor)。
- 有 BIOS 區塊
- 記憶體不足
- 系統上的開機關鍵元件驅動程式遭到封鎖
- 無法升級特定的品牌和型號
- 某個顯示類別元件的驅動程式區塊，包含下列所有屬性：
    - 您未覆寫
    - 新的 OS 版本中沒有驅動程式
    - Windows Update 尚不提供
- 系統上另一個隨插即用元件阻礙升級
- 有某個無線元件使用 XP 模擬驅動程式
- 某個具有使用中連線的網路元件將失去驅動程式。 換言之，升級後可能會失去網路連線的能力。

**重新安裝**的 Windows 升級決策指出升級需要重新安裝，而不是就地升級。 

**已封鎖**的 Windows 升級決策可能是由下列原因所造成：

- 您可以將一或多個資產的升級決策設定為**無法**。

- 該裝置的清查資料不完整，電腦分析無法執行完整的相容性評定。

### <a name="apps"></a>應用程式

在此部署計劃中，設定此應用程式的 [升級決策]  和 [重要性]  。 如需詳細資訊，請參閱[如何建立部署計劃](create-deployment-plans.md)。

在應用程式的詳細資料中，您也可以查看下列資訊：建議、相容性風險因素和 Microsoft 已知問題。 使用此資訊以利設定**升級決策**。 如需詳細資訊，請參閱[相容性評定](compat-assessment.md)。

電腦分析所顯示為「值得注意」  應用程式是以部署計劃整備規則的低安裝計數閾值為基礎。 如需詳細資訊，請參閱[整備規則](create-deployment-plans.md#readiness-rules)。

   > [!Tip]
   > 如需「不重要」應用程式類別的詳細資訊，請參閱[系統和 Store 應用程式的自動升級決策](about-assets.md#bkmk_plan-autoapp)。 <!-- 3587232 -->


### <a name="drivers"></a>驅動程式

請參閱此部署計劃所附的驅動程式清單。 設定 [升級決策]  、檢閱 Microsoft 的建議，並查看相容性風險因素。


## <a name="importance"></a>重要性

設定應用程式的「重要性」  是部署計劃的一部分。 電腦分析偵測到這些應用程式已安裝在目標裝置上。 此設定有助於電腦分析判斷在部署試驗階段中包含了哪些裝置。

如果某應用程式僅安裝在不到 2% 的目標裝置上，則會標示為 [低安裝計數]  。 預設值為百分之二。 您可以將整備設定的閾值從 0% 調整至 10%。 電腦分析會自動將這些應用程式標示為 [準備升級]**準備好升級**。  

針對應用程式，選擇 [重大]  、[重要]  或 [不重要]  等重要性。 如果將某個應用程式標示為 [重大] 或 [重要]，電腦分析即會在試驗部署中包含一些使用該應用程式的裝置。 服務在試驗中會包含較多重大應用程式的執行個體。 如果將應用程式標示為 [不重要]，電腦分析會自動將它設定為 [準備升級]  。



## <a name="pilot-devices"></a>試驗裝置

電腦分析會合併重要性資訊及全域試驗設定。 然後建立試驗部署應該包含哪些裝置的建議。 建議的試驗部署包括具有不同硬體設定的裝置，以及所有重大和重要應用程式的一或多個執行個體。 如果應用程式標示為 [重大]，服務即會建議更多試驗裝置配備該應用程式。



## <a name="deployment-plans-in-configuration-manager"></a>Configuration Manager 中的部署計劃

建立部署計劃之後，使用 Configuration Manager 來部署產品。 部署開始之後，電腦分析就會根據計劃設定監視部署。


## <a name="next-steps"></a>後續步驟

- [了解電腦分析資產](about-assets.md)：裝置、驅動程式和應用程式  

- [了解安全性和功能更新](about-updates.md)  

- [建立部署計劃](create-deployment-plans.md)  
