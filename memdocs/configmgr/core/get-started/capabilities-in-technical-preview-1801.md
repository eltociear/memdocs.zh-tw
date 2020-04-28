---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1801 版中可用的功能。
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074209"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Configuration Manager Technical Preview 1801 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1801 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 

安裝本版的 Technical Preview 之前，請先參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**此 Technical Preview 的已知問題：**
- **當您有以被動模式執行的站台伺服器時，更新到新的預覽版本會失敗**。 如果您有[被動模式下的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)，則您必須先解除安裝被動模式站台伺服器，再更新成這個新的預覽版本。 當您的站台完成更新之後，就可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在 Configuration Manager 主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。
  <!--sms 489412-->


**以下是您可以使用此版本試用的新功能。**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>建立分階段部署
<!-- 1357405 -->
分階段部署可自動化協調且循序的軟體推出作業，而不需要建立多個部署。 在此 Technical Preview 版本中，您可以在管理主控台中針對工作順序完成分階段部署精靈。 不過，不會建立部署。 

### <a name="try-it-out"></a>試試看！  
  請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。
 
**建立工作順序的分階段部署** </br>
1. 在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  。
2. 以滑鼠右鍵按一下現有的工作順序，然後選取 [Create Phased Deployment] \(建立分階段部署)  。 
3. 在 [一般]  索引標籤上，指定分階段部署的名稱、描述 (選擇性)，然後選取 [Automatically create default pilot and production phases]\ (自動建立預設試驗和生產階段)  。 
4. 填入 [試驗集合]  和 [生產集合]  欄位。 選取 [下一步]  。
5. 在 [設定]  索引標籤上，針對每個排程設定選擇一個選項，然後在完成時選取 [下一步]  。 
6. 在 [階段]  索引標籤上，視需要編輯任一階段，然後按一下 [下一步]  。
7. 在 [摘要]  索引標籤上確認您的選擇，然後按一下 [下一步]  繼續進行。

## <a name="co-management-reporting"></a>共同管理報告
<!-- 1356648 -->
如果使用[共同管理](../../comanage/overview.md)功能，您現在就可以檢視儀表板，從中查看您環境中共同管理的相關資訊。 在 Configuration Manager 主控台中，巡覽至 [監視]  工作區，展開 [更新整備小幫手]  ，然後選取 [Co-management]\ (共同管理)  儀表板。 儀表板包含以下磚：
- **共同管理的裝置**：您在環境中已啟用共同管理的裝置百分比
- **作業系統發佈**：依照版本之作業系統 (OS) 的細項。 這個圖表會使用下列群組：
  - Windows 7 和 8.x
  - 低於 1709 的 Windows 10
  - Windows 10 1709 和更高版本
    > [!NOTE] 
    > Windows 10 1709 版和更新版本是共同管理的必要條件
- **共同管理狀態**：裝置成功或失敗的細項，其類別如下：
   - 成功，已加入混合式 Azure AD
   - 成功，已加入 Azure AD
   - 失敗：自動註冊失敗
- **工作負載轉換**：此橫條圖顯示您針對三個可用的工作負載轉換到 Microsoft Intune 的裝置數目： 
   - 相容性原則
   - 資源存取
   - Windows Update for Business

### <a name="prerequisites"></a>先決條件
- 執行 Configuration Manager 主控台的電腦需要有 Internet Explorer 9 或更新版本。



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>自動部署規則評估排程的改善
<!-- 1357133 -->
依據[使用者意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)，您現在可以將自動部署規則 (ADR) 評估排程為從基礎日位移。 例如，若在當月的第二個星期二之後位移兩天，就會在星期四評估規則。 

### <a name="try-it-out"></a>試試看！  
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。 <br/>

**建立從基礎日位移並評估 ADR 的自訂排程** </br>
1.  在 [軟體程式庫]  工作區中，展開 [軟體更新]  ，然後選取 [自動部署規則]  。
2. 以滑鼠右鍵按一下 [自動部署規則]  ，然後選擇 [建立自動部署規則]  。 
3. 請遵循下列提示來完成 [一般]  、[部署設定]  和 [軟體更新]  索引標籤。 
4. 在 [評估排程]  索引標籤上，選取 [依排程執行規則]  和 [自訂]  。
5. 針對自訂的排程，請選取 [每月]  並放入基礎日，例如第二個星期二。 
6. 勾選 [位移 (天)]  和位移天數，然後在完成時按一下 [確定]  。  
7. 完成**建立自動部署規則精靈**的其餘部分。 



## <a name="reassign-distribution-point"></a>重新指派發佈點
<!-- 1306937 -->
許多客戶擁有大型的 Configuration Manager 基礎結構，並會減少主要或次要站台，以簡化其環境。 他們仍然需要保留分公司位置的發佈點，以提供內容給受控的用戶端。 這些發佈點通常包含數 TB 以上的內容。 此內容在散發到這些遠端伺服器時會耗用大量時間和網路頻寬。 

這項功能可讓您將發佈點重新指派給其他主要站台，而不需要重新發佈內容。 此動作會更新站台系統指派，同時保存伺服器上的所有內容。 如果您需要重新指派多個發佈點，請先在單一發佈點上執行此動作，然後逐一處理其他伺服器。

> [!IMPORTANT]
> 站台系統伺服器只能裝載發佈點角色。 如果站台系統伺服器裝載其他 Configuration Manager 伺服器角色 (例如狀態移轉點)，就無法重新指派發佈點。 您無法重新指派雲端發佈點。 

由於單一主要站台的 Technical Preview 限制之故，此選項不適用於這一版。 請考慮此案例，然後從功能區的 [首頁]  索引標籤中，傳送有關此動作功能的**意見反應**。
1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [發佈點]  節點。
2. 以滑鼠右鍵按一下目標發佈點，然後選取 [重新指派發佈點]  。 
  ![重新指派發佈點](media/1306937-reassign-dp.png)
3. 選取您要重新指派這個發佈點的目標站台伺服器和站台碼。 
  ![選取站台伺服器](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>硬體清查的改善
<!-- 1357389 -->
如果是新增的類別，您可以針對不是索引鍵的硬體清查屬性，指定超過 255 個字元的字串長度。

### <a name="try-it-out"></a>試試看！  
請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。<br/>

1. 在 [系統管理]  工作區中，按一下 [用戶端設定]  反白顯示要編輯的用戶端裝置設定，按一下滑鼠右鍵後選取 [屬性]  。 
2. 選取 [硬體清查]  ，然後選取 [設定類別]  和 [新增]  。
3. 按一下 [連線]  按鈕。
4. 填寫 [電腦名稱]  、[WMI 命名空間]  ，視需要選取 [遞迴]  。 提供連線所需的認證。 按一下 [連線]  以檢視命名空間類別。
5. 選取新的類別，然後按一下 [編輯]  。
6. 將索引鍵以外之至少一個屬性的 [長度]  \ (其為字串)，變更為大於 255。 按一下 [確定]  。 
7. 確定已針對 [新增硬體清查類別]  選取編輯的屬性，然後按一下 [確定]  。 
8. 收集硬體清查，其中新增的類別包含長度超過 255 個字元的屬性。 



## <a name="improvements-to-client-settings-for-software-center"></a>軟體中心之用戶端設定的改善
<!-- 1351224 & 1355146 -->
在這一版的 Technical Preview 中，已改善用戶端設定底下的軟體中心自訂。 

1. 軟體中心的用戶端設定現在有 [自訂]  按鈕。
2. 已新增預覽來顯示軟體中心橫幅的外觀。<!--1351224-->
    - 如果未選取標誌，預覽會顯示公司名稱文字和色彩。
    - 如果選取了標誌，預覽便會顯示標誌和公司名稱文字。  
3.  [Hide unapproved applications in Software Center]\ (隱藏軟體中心內未核准的應用程式)  是軟體中心的新設定。 啟用此選項時，需要核准的使用者可用應用程式會隱藏在軟體中心內。<!--1355146-->

### <a name="try-it-out"></a>試試看！  
 請嘗試完成工作。 然後，從功能區的 [首頁]  索引標籤中傳送**意見反應**，讓我們知道它的運作方式。

1. 在 [系統管理]  工作區中，按一下 [用戶端設定]  。 選取要編輯的用戶端裝置設定。 以滑鼠右鍵按一下它，然後依序選取 [屬性]  和 [軟體中心]  。
2.  按一下 [自訂]  按鈕。 嘗試不同的自訂設定，包括預覽。
3. 啟用 [Hide unapproved applications in Software Center]\ (隱藏軟體中心內未核准的應用程式)  設定。 觀察軟體中心內的變更。 



## <a name="new-settings-for-windows-defender-application-guard"></a>Windows Defender 應用程式防護的新設定
<!-- 1356256 -->
如果是 Windows 10 1709 版和更新版本的裝置，[Windows Defender 應用程式防護](../../protect/deploy-use/create-deploy-application-guard-policy.md)有兩個新的主機互動設定。 
1. 網站可獲授與主機虛擬圖形處理器的存取權。 
2. 容器內下載的檔案就可保存在主機上。 </br>



## <a name="improvements-to-run-scripts"></a>執行指令碼的改善
<!-- 1236459 -->
[**執行指令碼**功能](../../apps/deploy-use/create-deploy-scripts.md)現在可讓您匯入和執行已簽署的 PowerShell 指令碼。 
- 若要保持指令碼的完整性，簽署的指令碼必須加以匯入，而不是使用複製/貼上。 
- 匯入之後，便無法編輯已匯入的簽署指令碼。
    
>[!IMPORTANT]
>在此 Technical Preview 中，有兩項暫時性的限制。
>- 指令碼只能在 [執行指令碼] 功能中匯入，而且無法直接從主控台進行編輯。
>- 使用非 Unicode 編碼匯入的指令碼可能無法正確顯示在主控台中。 指令碼仍會依照原始撰寫內容執行。





## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
