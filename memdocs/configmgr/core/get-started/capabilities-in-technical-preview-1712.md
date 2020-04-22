---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1712 版中可用的功能。
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 65e0a1f39cb4347b78c8c10186df7be4aa527bea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705076"
---
# <a name="capabilities-in-technical-preview-1712-for-configuration-manager"></a>Configuration Manager Technical Preview 1712 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

此文章介紹 Configuration Manager 技術預覽 1712 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 

安裝本版的 Technical Preview 之前，請先參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何更新版本，以及如何提供 Technical Preview 的功能意見反應。     


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
  <!--sms489412-->


**以下是您可以使用此版本試用的新功能。**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>不會自動升級已取代的應用程式
<!-- 1351266 -->
根據您的[使用者語音意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior)，在此版本中，您可以選擇設定應用程式部署不自動升級任何已取代的版本。 現在在建立部署時，在 [部署軟體精靈]  的 [部署設定]  頁面中，基於**可用**或**必要**安裝目的，您可以啟用或停用 [自動升級此應用程式的任何已取代版本]  選項。


## <a name="install-multiple-applications-in-software-center"></a>在軟體中心安裝多個應用程式
<!-- 1357126 -->
如果使用者或桌面電腦技術人員需要在裝置上安裝多個應用程式，軟體中心現在支援安裝多個選取的應用程式。 因為不用等待安裝完一項後再開始下一項，所以這可以讓使用者更有效率。

使用 [應用程式]  索引標籤的多重選取模式時，下列準則會決定軟體中心可以多重選取的應用程式：
- 使用者可以看到應用程式
- 尚未安裝的應用程式
- 不需要系統管理員核准或已授權
- 應用程式狀態為可供使用 (例如，尚未下載的內容)

### <a name="try-it-out"></a>試試看！
**在 Configuration Manager 主控台中：** 為使用者或裝置部署多項 (截止日期在未來的) 可用或必要應用程式以供安裝。 不需要系統管理員核准。 如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。

**在軟體中心：**
 1. 預設應該開啟 [應用程式]  索引標籤。 
 2. 若要進入清單檢視中的多重選取模式，請按一下新增圖示 ![軟體中心多重選取圖示](media/software-center-multi-select-apps.png) 在右上角。
 3. 按一下清單中應用程式左邊的核取方塊，即可選取安裝兩個或多個應用程式。
 4. 按一下 [Install Selected] \(安裝選取項目)  按鈕。

應用程式正常安裝，只是現在會連續安裝。


## <a name="client-based-pxe-responder-service"></a>用戶端的 PXE 回應程式服務
<!-- 1357148 -->
客戶常遇見的困難是在很少或完全沒有伺服器基礎結構的遠端/分公司提供 PXE 服務。 發佈點角色支援用戶端作業系統，但因為 Windows 部署服務相依性的原因而無法啟用 PXE。

現有新的用戶端設定，可在 Configuration Manager 用戶端啟用 PXE 回應程式服務。 啟用 PXE 的開機映像必須位於 PXE 回應程式的用戶端快取中。

### <a name="try-it-out"></a>試試看！
請確定測試環境中目前沒有任何已啟用 PXE 的發佈點或其他 PXE 伺服器，可能與此用戶端 PXE 回應程式發生衝突。

在 Configuration Manager 主控台中：
1. 在 [作業系統]  下 [軟體程式庫]  工作區中的 [工作順序]  ：使用自訂範本建立工作順序。
   1. 按一下 [新增]  ，依序選取 [一般]  和 [設定工作順序變數]  步驟。 輸入 **SMSTSPersistContent** 作為工作順序變數，並輸入值 **TRUE**。
   1. 按一下 [新增]  ，依序選取 [軟體]  和 [下載套件內容]  步驟。 按一下金色星號，然後選取啟用 PXE 的開機映像。 包括 x86 和 x64 開機映像。 設定步驟，將它放入 **Configuration Manager 用戶端快取**。
   1. 按一下 [新增]  ，依序選取 [一般]  和 [設定工作順序變數]  步驟。 輸入 **SMSTSPreserveContent** 作為工作順序變數，並輸入值 **TRUE**。
2. 在 [用戶端設定]  下的 [系統管理]  工作區中：建立自訂用戶端裝置設定原則。
   1. 選取**用戶端快取設定**群組。
   1. 將 [Enable Configuration Manager client in full OS to share content] \(在完整作業系統中啟用 Configuration Manager 用戶端以共用內容)  設定設為 [是]  。
   1. 將 [Enable PXE responder service] \(啟用 PXE 回應程式服務)  設定設為 [是]  。
   1. 在 [建立自我簽署憑證或匯入 PKI 用戶端憑證]  設定按一下 [Provide a certificate]\ (提供憑證)  。 如果您的測試環境有 PKI，請選取 [匯入憑證]  ，否則按一下 [確定]  建立自我簽署的憑證。 
   1. 視測試環境的需要設定其餘設定。 (除非有特定的網路或安全性需求，否則預設設定應該會作用。)
3. 將工作順序和自訂用戶端設定部署到要成為 PXE 回應程式目標用戶端的集合。 等待要套用的原則和要執行的工作順序。
4. 啟動位於相同子網路的另一個用戶端，照常進行 PXE/網路開機。

### <a name="known-issues"></a>已知問題
- 工作順序編輯器在您新增開機映像時，雖已成功儲存工作順序，但在 [下載套件內容]  步驟會顯示紅色錯誤圖示。 在編輯器中再次重新開啟此工作順序，也會顯示找不到參考物件的無害警告。 <!-- sms427542 -->
- [下載套件內容] 步驟中的開機映像不會顯示在參考的自訂工作順序清單中。 也無法使用 [發佈內容]  動作。 <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Configuration Manager 用戶端安裝中的變更  
由於使用者語音意見反應，[Silverlight 不再自動安裝在用戶端。](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>變更為 Surface 裝置儀表板
Surface 儀表板現在會顯示 Surface 裝置的韌體版本，而不是作業系統版本。 在主控台中，移至 [監視]   > [Surface Devices] \(Surface 裝置)  。 您可以檢視下列項目：
- Surface 百分比
- Surface 模型的百分比
- 前五個韌體版本
 <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Office 365 用戶端管理儀表板的改善 
選取圖形區段時，Office 365 用戶端管理儀表板現在會顯示相關裝置的清單。 在主控台中，移至 [軟體程式庫]   >[概觀]   >[Office 365 用戶端管理]  。 儀表板顯示在右邊。 從圖表中選取準則會顯示裝置清單。  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager 主控台的改善 
我們已針對使用者意見反應，對 Configuration Manager 主控台進行下列改善。

- [裝置清單會顯示主要使用者](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user)：[資產與合規性]、[裝置] 底下列出的裝置，現在預設會顯示主要使用者。 最後登入的使用者也會新增為選擇性資料行。 <!-- 1357280 -->
- [重新命名的集合會顯示在現有集合成員資格規則中](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections)：如果集合是另一個集合的成員且重新命名時，會依成員資格規則來更新新名稱。<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>作業系統部署增強功能
我們已對作業系統部署進行下列改善，有一些是使用者語音意見反應的結果。
- [開機映像中的預設記錄檢視器](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a)：在 Windows PE 中，當啟動 cmtrace.exe 時，不會再提示您選擇是否要將此程式設定為預設的記錄檔檢視器。 <!-- SMS 500897 -->
- [下載套件內容] 步驟：您現在可在此工作順序步驟中新增開機映像。


## <a name="windows-10-feedback-hub-app-integration"></a>Windows 10 回饋中樞應用程式整合

我們熱烈歡迎您提出意見，所以透過 Windows 10 內建的[回饋中樞應用程式](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)讓您反應意見。 當您 [新增意見反應]  時，請務必選取 [企業管理]  類別，然後選擇下列其中一個子類別：
- Configuration Manager 用戶端
- Configuration Manager 主控台
- Configuration Manager 作業系統部署
- Configuration Manager 伺服器

繼續使用我們的[使用者語音頁面](https://configurationmanager.uservoice.com/)，對 Configuration Manager 的新功能構想進行投票。


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
