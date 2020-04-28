---
title: 管理和監視階段式部署
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理和監視軟體的階段式部署。
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 419b91365d80062baabc289d0dbcf064c89b71a0
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110469"
---
# <a name="manage-and-monitor-phased-deployments"></a>管理和監視階段式部署

本文描述如何管理和監視階段式部署。 管理工作包含手動開始下一個階段，以及暫止或繼續階段。 

首先，您需要建立階段式部署： 
- [應用程式](create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [軟體更新](create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [工作順序](create-phased-deployment-for-task-sequence.md)  



## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> 移至下一個階段

當您選取 [Manually begin the second phase of deployment] \(手動開始第二個部署階段\)  設定時，站台不會根據成功準則來自動啟動下一個階段。 您需要將階段式部署移至下一個階段。  

1. 根據已部署軟體的類型啟動此動作的方式會不同：  

    - [應用程式]  (僅在 1806 版或更新版本中)：移至 [軟體程式庫]  工作區，並展開 [應用程式管理]  ，然後選取 [應用程式]  。   

    - [軟體更新]  (僅在 1810 版或更新版本中)：移至 [軟體程式庫]  工作區，然後選取下列其中一個節點：    
        - 軟體更新  
            - **所有軟體更新**  
            - **軟體更新群組**   
        - Windows 10 服務：**所有 Windows 10 更新**  
        - Office 365 用戶端管理：**Office 365 更新**  

    - **工作順序**：移至 [軟體程式庫]  工作區中，並展開 [作業系統]  ，然後選取 [工作順序]  。   

2. 選取具有階段式部署的軟體。  

3. 在詳細資料窗格中，切換至 [階段式部署]  索引標籤。  

4. 選取階段式部署，然後按一下功能區中的 [移至下一個階段]  。  

    ![顯示階段式部署上之動作的右鍵功能表](media/Suspend-phased-deployment.PNG)



## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> 暫止和繼續階段 

您可以手動暫止或繼續階段式部署。 例如，您可以建立工作順序的階段式部署。 監視試驗小組的階段時，您會注意到大量失敗。 您暫停階段式部署，以停止未來的裝置執行工作順序。 解決此問題之後，即可繼續階段式部署以繼續推出。 

1. 根據已部署軟體的類型啟動此動作的方式會不同：  

    - [應用程式]  (僅在 1806 版或更新版本中)：移至 [軟體程式庫]  工作區，並展開 [應用程式管理]  ，然後選取 [應用程式]  。   

    - [軟體更新]  (僅在 1810 版或更新版本中)：移至 [軟體程式庫]  工作區，然後選取下列其中一個節點：    
        - 軟體更新  
            - **所有軟體更新**  
            - **軟體更新群組**   
        - Windows 10 服務：**所有 Windows 10 更新**  
        - Office 365 用戶端管理：**Office 365 更新**  

    - **工作順序**：移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。 選取現有的工作順序，然後按一下功能區中的 [建立階段式部署]  。  

2. 選取具有階段式部署的軟體。  

3. 在詳細資料窗格中，切換至 [階段式部署]  索引標籤。  

4. 選取階段式部署，然後按一下功能區中的 [暫止]  或 [繼續]  。 

> [!NOTE]
> 從 2020 年 4 月 21 日開始，「Office 365 專業增強版」會重新命名為「Microsoft 365 Apps 企業版」  。 如需詳細資訊，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) \(部分機器翻譯\)。 在主控台正在進行更新時，您在 Configuration Manager 產品與文件中可能仍會看到舊名稱。 

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="monitor"></a><a name="bkmk_monitor"></a> 監視
<!--1358577-->
從 1902 版開始，階段式部署會有其本身的專用監視節點，讓您可以更輕鬆地找出已建立的階段式部署，以及瀏覽至階段式部署監視檢視。 從 [監視]  工作區，選取 [階段式部署]  ，然後按兩下其中一個階段式部署來查看狀態。 <!--3555949-->

在 Configuration Manager 1806 和 1810 中，您可以查看適用於階段式部署的原生監視體驗。 從 [監視]  工作區中的 [部署]  節點，選取階段式部署，然後按一下功能區中的 [階段式部署狀態]  。

![顯示兩個階段狀態的階段式部署狀態儀表板](media/1358577-phased-deployment-status.png)

此儀表板會針對部署中的每個階段顯示下列資訊：  

- **裝置數總計**或**資源數總計**：有多少個由此階段設為目標的裝置。  

- **狀態**：此階段的目前狀態。 每個階段均可處於下列其中一種狀態：  

    - **已建立部署**：階段式部署會針對此階段的集合，建立軟體部署。 會主動將用戶端設為此軟體的目標。  

    - **等待中**：上一個階段尚未達到繼續進行此階段部署的成功準則。  

    - **已暫停**：系統管理員已暫停部署。  

- **進度**：來自用戶端且以色彩標示的部署狀態。 例如：成功、進行中、錯誤、不符合需求及未知。 

#### <a name="success-criteria-tile"></a>成功準則圖格

使用 [選取階段]  下拉式清單來變更 [成功準則]  圖格的顯示。 此圖格會比較 [Phase Goal] \(階段目標\)  與部署的目前合規性。 使用預設設定時，階段目標為 95%。 此值表示部署需要 95%合規性，才能移至下一個階段。

在此範例中，階段目標為 65%，而目前的合規性為 66.7%。 因為第一個階段符合成功準則，所以階段式部署會自動移至第二個階段。  

   ![來自階段式部署狀態的範例成功準則磚，其中目標為 65%](media/pod-status-success-criteria-tile.png)

階段目標與「下一個」  階段之 [階段設定] 的 [Deployment success percentage] \(部署成功百分比\)  相同。 若要讓階段式部署開始下一個階段，該第二個階段會定義第一個階段的成功準則。 檢視此設定： 

1. 移至軟體上的階段式部署物件，然後開啟 [階段式部署屬性]。  

2. 切換至 [階段]  索引標籤。選取 [Phase 2] \(第 2 階段\)  ，然後按一下 [檢視]  。  

3. 在 [階段屬性] 視窗中，切換至 [階段設定]  索引標籤。  

4. 檢視 [前一階段的成功準則]  群組中的 [Deployment success percentage] \(部署成功百分比\)  值。  

例如，下列屬性適用於與準則為 65% 之上述成功準則圖格相同的階段：  
![[階段屬性] 上的 [階段設定] 索引標籤](media/phase-properties-phase-settings.png)

