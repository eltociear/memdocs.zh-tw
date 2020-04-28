---
title: 建立分階段部署
titleSuffix: Configuration Manager
description: 使用階段式部署，自動執行將軟體推出到數個集合的作業。
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5af0b7c90225a1f42d55767a0296d7e2263f956f
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110452"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>使用 Configuration Manager 建立階段式部署

適用於：  Configuration Manager (最新分支)

分階段部署可在多個集合中，將協調且循序的軟體推出作業自動化。 例如，將軟體部署至試驗集合，然後根據成功準則自動繼續推出。 請使用預設的兩個階段，或以手動方式設定多個階段來建立階段式部署。 

建立下列物件的階段式部署：
- **工作順序**  
    - 工作順序的階段式部署不支援 PXE 或媒體安裝   
- **應用程式** (從 1806 版開始) <!--1358147-->  
- **軟體更新** (從 1810 版開始) <!--1358146-->  
    - 使用階段式部署時，您無法使用自動部署規則

> [!Tip]  
> 階段式部署功能最初是在 1802 版以[發行前版本功能](../../core/servers/manage/pre-release-features.md)的形式引進。 從 1806 版開始，它不再是發行前版本功能。<!--1356837-->  



## <a name="prerequisites"></a>先決條件

#### <a name="security-scope"></a>安全性範圍
階段式部署所建立的部署無法供不具**所有**安全性範圍的任何系統管理使用者檢視。 如需詳細資訊，請參閱 [安全性範圍](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)。

#### <a name="distribute-content"></a>發佈內容
建立階段式部署之前，請先將相關聯的內容發佈至發佈點。<!--518293-->  

- **應用程式**：在主控台中選取目標應用程式，然後使用功能區中的 [發佈內容]  動作。 如需詳細資訊，請參閱[部署及管理內容](../../core/servers/deploy/configure/deploy-and-manage-content.md)。   

- **工作順序**：您必須先建立參考的物件 (例如 OS 升級套件)，再建立工作順序。 在建立部署之前發佈這些物件。 在每個物件上使用 [發佈內容]  動作，或使用工作順序。 若要檢視所有參考內容的狀態，請選取工作順序，然後在詳細資料窗格中切換至 [參考]  索引標籤。 如需詳細資訊，請參閱[準備 OS 部署](../get-started/prepare-for-operating-system-deployment.md)中的特定物件類型。   

- **軟體更新**：建立並發佈部署套件。 使用 [下載軟體更新精靈]。 如需詳細資訊，請參閱[下載軟體更新](../../sum/deploy-use/download-software-updates.md)。  



## <a name="phase-settings"></a><a name="bkmk_settings"></a> 階段設定

這些設定對階段式部署是唯一的。 建立或編輯階段時指定這些設定，以控制階段式部署程序的排程和行為。 


#### <a name="criteria-for-success-of-the-first-phase"></a>第一個階段的成功準則  

- **部署成功百分比**：指定需要有多少百分比的裝置成功完成部署，才能讓第一個階段成功。 根據預設，此值為 95%。 換句話說，當此部署之 95% 的裝置合規性狀態為 [成功]  時，站台就會將第一個階段視為成功。 接著，站台會繼續進行第二個階段，並建立下一個集合的軟體部署。  
- **成功部署的裝置數**：已在 Configuration Manager 1902 版中新增。 指定需要有多少數目的裝置成功完成部署，才能讓第一個階段成功。 當集合的大小可變時，此選項很有用，而且而且您在移至下一個階段之前有特定是木的裝置可顯示成功。 <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>在第一個階段成功後開始第二個階段部署的條件  

- **在一段延遲期間 (天) 之後自動開始此階段**：選擇在第一個階段成功之後，開始第二個階段之前要等待的天數。 根據預設，此值為 1 天。  

- **手動開始第二個階段部署**：站台不會在第一個階段成功後自動開始第二個階段。 此選項需要您手動開始第二個階段。 如需詳細資訊，請參閱[移到下一個階段](manage-monitor-phased-deployments.md#bkmk_move)。  

    > [!Note]  
    > 此選項不適用於應用程式的階段式部署。  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>讓此軟體在這段期間逐漸可供使用 (天)
<!--1358578-->
從 1806 版開始，指定這個設定來使每個階段的推出作業會逐步進行。 此行為有助於減緩部署問題的風險，並降低因將內容散發到用戶端而導致的網路負載。 依據每個階段的設定而定，站台會逐步開放軟體以供使用。 階段中的每個用戶端都有一個相對於軟體可供使用時間的期限。 可用時間與期限之間的時間範圍，對於階段中的所有用戶端而言都一樣。 此設定的預設值為 0；因此，預設不會對部署進行節流處理。 請勿指定高於 30 的值。<!--SCCMDocs-pr issue 2767--> 

![階段式部署成功準則設定](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>設定相對於軟體可供使用時的期限行為  

- **必須盡快安裝**：設定在裝置設為目標後盡快在裝置上安裝的期限。  

- **必須在這段時間後安裝**：設定在裝置設為目標後的特定天數內安裝的期限。 根據預設，此值為 7 天。   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a> 自動建立預設的兩階段部署

1. 在 Configuration Manager 主控台中啟動 [建立階段式部署精靈]。 此動作根據所部署軟體的類型而有所不同：  

    - **應用程式** (僅在 1806 版或更新版本中)：移至 [軟體程式庫]  ，展開 [應用程式管理]  ，然後選取 [應用程式]  。 選取現有的應用程式，然後選擇功能區中的 [建立階段式部署]  。  

    - **軟體更新** (僅在 1810 版或更新版本中)：移至 [軟體程式庫]  ，展開 [軟體更新]  ，然後選取 [所有軟體更新]  。 選取一或多個更新，然後選擇功能區中的 [建立階段式部署]  。  

        此動作適用於下列節點的軟體更新：  
        - 軟體更新  
            - **所有軟體更新**  
            - **軟體更新群組**   
        - Windows 10 服務：**所有 Windows 10 更新**  
        - Office 365 用戶端管理：**Office 365 更新**  

    - **工作順序**：移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。 選取現有的工作順序，然後選擇功能區中的 [建立階段式部署]  。  

2. 在 [一般]  頁面上，指定階段式部署的 [名稱]  、[描述]  (選擇性)，然後選取 [自動建立預設的兩階段部署]  。  

3. 選取 [瀏覽]  ，然後為 [第一個集合]  和 [第二個集合]  這兩個欄位選擇目標集合。 若為工作順序和軟體更新，請從裝置集合中選取。 若為應用程式，則從使用者或裝置集合中選取。 選取 [下一步]  。  

    > [!Important]  
    > 如果部署可能具有高風險，[建立階段式部署精靈] 不會通知您。 如需詳細資訊，請參閱[管理高風險部署的設定](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)，以及當您[部署工作順序](deploy-a-task-sequence.md)時的注意事項。  

4. 在 [設定]  頁面上，針對每個排程設定選擇一個選項。 如需詳細資訊，請參閱[階段設定](#bkmk_settings)。 完成時選取 [下一步]  。  

5. 在 [階段]  頁面上，查看精靈為指定集合所建立的兩個階段。 選取 [下一步]  。 這些指示涵蓋自動建立預設兩階段部署的程序。 此精靈可讓您新增、移除、重新排列、編輯或檢視階段式部署的階段。 如需這些其他動作的詳細資訊，請參閱[建立具有手動設定階段的階段式部署](#bkmk_manual)。  

6. 在 [摘要]  索引標籤上確認您的選擇，然後選取 [下一步]  完成精靈。  

> [!NOTE]
> 從 2020 年 4 月 21 日開始，「Office 365 專業增強版」會重新命名為「Microsoft 365 Apps 企業版」  。 如需詳細資訊，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) \(部分機器翻譯\)。 在主控台正在進行更新時，您在 Configuration Manager 產品與文件中可能仍會看到舊名稱。  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a> 建立具有手動設定階段的階段式部署
<!--1358148--> 

從 1806 版開始，為工作順序建立具有手動設定階段的階段式部署。 從 [建立階段式部署精靈] 的 [階段]  索引標籤，新增多達 10 個額外階段。 

> [!Note]  
> 您目前無法手動建立應用程式的階段。 精靈會自動建立兩個階段以供應用程式部署使用。


1. 若為工作順序或軟體更新，請啟動 [建立階段式部署精靈]。  

2. 在[建立階段式部署精靈] 的 [一般]  頁面上，指定階段式部署的 [名稱]  、[描述]  (選擇性)，然後選取 [手動設定所有階段]  。  

3. 從 [建立階段式部署精靈] 的 [階段]  頁面中，可以使用下列動作：  

    - [篩選]  部署階段的清單。 針對 [順序]、[名稱] 或 [集合] 資料行的不區分大小寫相符項，輸入字元字串。 

    - [新增]  階段：  

        1. 在 [新增階段精靈] 的 [一般]  頁面上，指定階段的 [名稱]  ，然後瀏覽至目標 [階段集合]  。 此頁面上的其他設定與正常部署工作順序或軟體更新時的設定相同。  

        2. 在 [新增階段精靈] 的 [階段設定]  頁面上，指定排程設定，然後在完成時選取 [下一步]  。 如需詳細資訊，請參閱[設定](#bkmk_settings)。   

            > [!Note]  
            > 您無法在第一個階段設定階段設定 [部署成功百分比]  或 [成功部署的裝置數]  (1902 版或更新版本)。 此設定僅適用於具有前一個階段的階段。  

        3. [新增階段精靈] 之 [使用者體驗]  和 [發佈點]  頁面上的設定與正常部署工作順序或軟體更新時的設定相同。  

        4. 檢閱 [摘要]  頁面上的設定，然後完成 [新增階段精靈]。  

    - **編輯**：這個動作會開啟所選階段的 [內容] 視窗，其中所含索引標籤與 [新增階段精靈] 的頁面相同。  

    - **移除**：這個動作會刪除所選階段。  

       > [!Warning]  
       > 不會進行確認，也無法復原此動作。  

    - **上移**或**下移**：精靈會依照階段的新增方式來排序階段。 最近新增的階段是清單中的最後一個項目。 若要變更順序，請選取某個階段，然後使用這些按鈕來移動該階段在清單中的位置。  

       > [!Important]  
       > 檢閱變更順序之後的階段設定。 確定下列設定仍與此階段式部署的需求保持一致：  
       > 
       > - 前一個階段的成功準則  
       > - 在前一個階段成功後，應當在何種條條之下開始這個部署階段   

5. 選取 [下一步]  。 檢閱 [摘要]  頁面上的設定，然後完成 [建立階段式部署精靈]。  


建立階段式部署之後，開啟其內容以進行變更：  

- 將其他階段 [新增]  至現有的階段式部署。  

- 如果階段不在使用中，您可以進行 [編輯]  、[移除]  ，或者向上或向下 [移動]  。 您無法在使用中的階段之前移動它。  

- 當階段在使用中時，它是唯讀。 您無法予以編輯、移除，或移動它在清單中的位置。 唯一的選項是 [檢視]  階段的內容。  

- 應用程式的階段式部署一律為唯讀。  



## <a name="next-steps"></a>後續步驟

管理和監視階段式部署：
- [應用程式](manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)
- [軟體更新](manage-monitor-phased-deployments.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [工作順序](manage-monitor-phased-deployments.md)  

