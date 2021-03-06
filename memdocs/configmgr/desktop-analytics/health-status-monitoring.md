---
title: 健康情況狀態監視
titleSuffix: Configuration Manager
description: 了解電腦分析中健康情況狀態監視的運作方式。
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 119f787f15b8c907d0c760a12b973ca984f4348c
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268533"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>電腦分析中的健康情況狀態監視

當您[將更新部署到生產環境](deploy-prod.md)時，請使用電腦分析來協助監視裝置的健康情況狀態。 本文詳細說明健康情況監視的運作方式。

如需如何使用這項功能的詳細資訊，請參閱[監視已更新裝置的健康情況](deploy-prod.md#bkmk_monitor)。

![電腦分析中 [監視健康情況] 頁面的螢幕擷取畫面](media/monitor-health.png)

> [!NOTE]  
> 電腦分析只會從裝置收集健康情況資料，以提供可作為基準的使用方式資料。 這表示其不會包含未設定為在 [增強 (受限)] 層級共用診斷資料的 Windows 7 和 Windows 10 裝置。 如果執行 Windows 10 的裝置超過 10% 設定為在 [增強 (受限)] 以外層級共用診斷資料，則 [監視健康情況]  頁面會在橫幅區域中顯示警告。  

若要檢視特定應用程式的詳細資訊，請在清單中選取該應用程式。

## <a name="apps"></a>應用程式

### <a name="health-status-factors"></a>健全狀況狀態因素

![電腦分析中應用程式的健康情況狀態因素](media/monitor-health-status-factors.png)

電腦分析會監視應用程式的下列健康情況狀態因素：

- **發生損毀的裝置百分比**：在過去兩週，此特定應用程式已損毀的裝置數目除以已使用應用程式的裝置數目。 此檢視可讓您查看應用程式穩定性在新的 OS 版本上已增加或減少。 電腦分析會針對下列集合計算此百分比：  

  - **更新後**：已更新為部署計劃中所指定目標 OS 版本的裝置。 為減少資料不足的資產數目，電腦分析會針對您所有已更新的裝置收集這項資料。 此集合包含不在部署計劃中的裝置。  

  - **更新前**：配有早於部署計劃所指定之 OS 版本的裝置。 此清單不包含執行 Windows 7 的裝置。  

  - **商業平均**：所有商業裝置上的平均損毀率。 此平均是跨「所有」  版本的應用程式計算而來。 如果您的版本顯示高於商業平均的損毀率，則可能有更穩定的版本可供使用。  

- **發生損毀的工作階段百分比**：與上述類似，但會計算過去兩週發生損毀的工作階段百分比。  

為判斷應用程式的健康情況狀態，電腦分析需要至少 20 部裝置的資料。 否則會回報應用程式的**資料不足**。 該服務會根據這些裝置的「工作階段損毀率」  ，計算健康情況狀態。 裝置當機率則僅供參考。 不會用於健康情況狀態計算中。

### <a name="usage"></a>使用方式

<!-- 5533890 -->

- **使用中的裝置**：這個值是過去兩週內，使用者啟動所選應用程式的裝置計數。 其以所選部署計劃中執行 Windows 10 目標版本的裝置為基礎。

- **工作階段**：這個值是使用者在目標 Windows 版本上啟動所選應用程式的總次數。

### <a name="additional-tabs"></a>其他索引標籤

[應用程式詳細資料] 頁面底部的下列三個索引標籤可協助您進行疑難排解：

- **其他版本**：此應用程式的替代版本清單。 針對每個版本，會顯示您組織中損毀率的相對變更與商業平均。 如果您發現具有較低損毀率的更新版應用程式，則更新應用程式可能會有所幫助。  

    該清單也會顯示版本是否有進階見解。 如需詳細資訊，請參閱[相容性評定](compat-assessment.md)。  

- **常見問題**：依執行個體計數的最常見失敗識別碼清單。 失敗識別碼會識別與損毀相關聯的堆疊追蹤。 當您連絡應用程式廠商尋求支援時，可以使用此識別碼。  

- **最近的損毀**：應用程式最近損毀的裝置清單。 您可以依失敗識別碼和其他準則進行篩選。 使用此資訊透過收集記錄檔或嘗試在特定裝置上進行修正，來對問題進行疑難排解，再嘗試進行更廣泛的部署。  

如果您發現無法修正的嚴重健康情況迴歸，請將應用程式的 [升級決策]  變更為 [無法]  。 此動作可防止日後將更新部署到具有此資產的裝置。

## <a name="see-also"></a>請參閱

- [電腦分析中的相容性評估](compat-assessment.md)  

- [如何使用電腦分析部署到生產環境](deploy-prod.md)  
