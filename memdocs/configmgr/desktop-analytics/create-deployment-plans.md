---
title: 如何建立部署計劃
titleSuffix: Configuration Manager
description: 電腦分析中的建立部署計劃操作指南。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268754"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>如何在電腦分析中建立部署計劃

本文提供在電腦分析中建立部署計劃的步驟。 開始之前，請先[了解部署計劃](about-deployment-plans.md)。

## <a name="create-a-plan-for-windows-10"></a>建立適用於 Windows 10 的計劃

遵循本節中的步驟，使用電腦分析建立部署 Windows 10 的計劃。

1. 開啟[電腦分析入口網站](https://aka.ms/desktopanalytics)。 請使用至少具有**工作區參與者**權限的認證。  

2. 選取 [管理] 群組中的 [部署計劃]  。  

3. 在 [部署計劃]  窗格中，選取 [建立]  。  

4. 在 [建立部署計劃]  窗格中，進行下列設定：  

    - **名稱**：部署計劃的唯一名稱  

    - **產品和版本**：選擇要部署的 Windows 10 版本。 Microsoft 建議建立使用最新版本的部署計劃。  

    - **裝置群組**：從同一階層中選取一或多個群組。 這些群組是從 Configuration Manager 同步的[裝置集合](connect-configmgr.md#bkmk_Collections)。

        如果您將多個 Configuration Manager 階層連線到相同的電腦分析執行個體，階層的顯示名稱會在通用試驗設定中的集合名稱之前加上首碼。 此名稱是 Configuration Manager 主控台中電腦分析連線上的 [顯示名稱]  屬性。<!-- 4814075 -->

        > [!NOTE]
        > 對多個階層的支援需要 Configuration Manager 1910 版或更新版本。
        >
        > 如果您選取多個階層的集合，入口網站會顯示警告。 您無法使用來自多個階層的集合來建立部署計劃。<!-- 4814075 -->

    - **整備規則**：這些規則有助於您判斷哪些裝置符合升級資格。 如需詳細資訊，請參閱[整備規則](#readiness-rules)。  

    - **完成日期**：選擇 Windows 應完全部署至所有目標裝置的日期。  

5. 選取 [建立]  。 新計劃會出現在正在處理的部署計劃清單中。 若要加速處理，請要求隨選資料重新整理。 如需詳細資訊，請參閱[電腦分析常見問題集](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。  

6. 選取部署計劃的名稱，開啟部署計劃。  

7. 在 [部署計劃] 功能表的 [準備]  群組中，選取 [識別重要性]  。  

    1. 在 [應用程式]  索引標籤上，選取僅顯示 [未檢閱]  的資產。  

    2. 選取每個應用程式，然後選取 [編輯]  。 您可以同時選取多個應用程式進行編輯。  

    3. 從 [重要性]  清單中選擇重要性等級。 如果您希望電腦分析在試驗期間驗證應用程式，請選取 [重大]  或 [重要]  。 其不會驗證標示為 [不重要]  的應用程式。 在指派重要性等級時，評定其[相容性](compat-assessment.md)及其他計劃見解。  

        指派重要性等級時，您也可以選擇升級決策。  

    4. 完成時選取 [儲存]  。  

8. 在 [部署計劃] 功能表的 [準備]  群組中，選取 [識別試驗]  。  

    1. 檢閱試驗的建議裝置。  

    2. 選取每部裝置，然後選取 [新增至試驗]  。 如不同意建議，請選取 [取代]  。  

        如需電腦分析如何提出這些建議的詳細資訊，請選取 [識別試驗]  窗格右上角的資訊圖示。

## <a name="readiness-rules"></a>整備規則

這些規則有助於您判斷哪些裝置符合就地升級資格。 您可以在建立部署計劃時設定這些規則，或稍後再行編輯。

若要變更整備規則：

1. 在電腦分析入口網站中，選取部署計劃。
1. 選取名稱旁的 [編輯]  。
1. 選取 [整備規則]  。
1. 選取 [Windows OS]  。
1. 視需要變更並選取 [儲存]  。

**Windows OS** 升級有兩條可用的規則：裝置驅動程式和 Windows 應用程式。

### <a name="device-drivers"></a>裝置驅動程式

設定裝置是否從 Windows Update 取得驅動程式。 根據預設，此值為 [關閉]  。 當您使用商務用 Windows Update 來管理包括驅動程式在內的更新時，請啟用此規則。 如要使用 Configuration Manager 管理軟體更新，請將此規則設定為 [關閉]  。

### <a name="windows-applications"></a>Windows 應用程式

電腦分析顯示為「值得注意」  的應用程式是以低安裝計數閾值為基礎。 在部署計劃的整備規則中設定此閾值。 此閾值預設為 **2.0%** 。 您可將此值從 `0.0` 變更為 `10.0`。


## <a name="next-steps"></a>後續步驟

請前往下一篇文章來部署至試驗裝置。
> [!div class="nextstepaction"]  
> [部署至試驗](deploy-pilot.md)  
