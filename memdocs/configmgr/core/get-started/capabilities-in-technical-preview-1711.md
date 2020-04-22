---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1711 版中可用的功能。
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705096"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Configuration Manager Technical Preview 1711 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

此文章介紹 Configuration Manager 技術預覽 1711 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 的已知問題：**
- **對 Windows 10 1709 版 (也稱為 Fall Creators Update) 的支援**。  從這個 Windows 版本開始，Windows 媒體會包含數個版本。 設定工作順序以使用作業系統升級套件或作業系統映像時，請務必選取[支援由 Configuration Manager 使用的版本](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)。
- **當您有以被動模式執行的站台伺服器時，更新到新的預覽版本會失敗**。 當您執行具有[以被動模式執行的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)的預覽版本時，必須先將被動模式站台伺服器解除安裝，才能順利將預覽站台更新到這個新的預覽版本。 當您的站台完成更新之後，就可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。

**以下是您可以使用此版本試用的新功能。**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>改善執行工作順序
<!-- 1261338 -->

此 Technical Preview 將會改善執行工作順序步驟。 這些改善包含下列項目：

- 軟體中心、PXE 和媒體中的所有作業系統部署案例支援。
- 改善主控台動作，例如複製、匯入、匯出，以及物件刪除期間的警告。
- [建立預先設置內容精靈]  支援。
- 與部署驗證的整合。
- 執行工作順序步驟現在可以跨多層的工作順序使用，而不只是單一父子式關聯性。 多層關聯性會增加複雜度，因此請謹慎使用。 仍然會檢查這些關聯性的循環參考。

### <a name="try-it-out"></a>試試看！  

請嘗試完成下列工作，然後從功能區的 [首頁]  索引標籤中傳送 [意見反應]  給我們，讓我們了解運作情況：

1. 在工作順序編輯器中，按一下 [新增]  ，選取 [一般]  ，然後按一下 [執行工作順序]  。
2. 按一下 [瀏覽]  以選取子工作順序。

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>在安裝應用程式時允許使用者互動 <!-- 1356976 -->

在本預覽版中，您可以允許終端使用者在執行工作順序期間與應用程式安裝互動。 例如，執行安裝程序，以向終端使用者提示各種選項。 有些應用程式安裝程式無法讓使用者提示靜音，或安裝程序可能需要只有使用者才知道的特定設定值。 這項功能可讓您處理這些安裝案例。

### <a name="try-it-out"></a>試試看！

請嘗試完成下列工作，然後從功能區的 [首頁]  索引標籤中傳送 [意見反應]  ，讓我們了解運作情況：

1.  建立或編輯應用程式。 如需詳細資訊，請參閱[使用 Configuration Manager 建立應用程式](../../apps/deploy-use/create-applications.md)。

    a. 在 [Windows Installer (\*msi 檔案) 內容]  中，選擇 [使用者體驗]  索引標籤。

    b. 針對 [安裝行為]  ，選取 [針對系統安裝]  。

    c. 針對 [登入需求]  ，選取 [無論使用者是否登入]  。

    d. 針對 [安裝程式可見度]  ，選取 [標準]  。 您可以從三個選項選擇：**最小化**、**一般**或**最大化**。

    e. 選取 [Allow users to interact with the program installation]\ (允許使用者與程式安裝互動)  方塊。

2.  建立或編輯工作順序，以使用**安裝應用程式**步驟來安裝應用程式。 如需詳細資訊，請參閱[工作順序步驟](../../osd/understand/task-sequence-steps.md)中的[安裝應用程式](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)。

    a. 在安裝 Windows 和 Configuration Manager 步驟之後的映像處理工作順序。

    b. 後續處理群組中的就地升級工作順序。

3.  將工作順序部署至用戶端。
4.  從軟體中心安裝工作順序。

在工作順序進行期間，應用程式安裝介面會出現在目標終端使用者裝置上。 工作順序進度會暫停，直到終端使用者完成應用程式安裝工作流程。

### <a name="install-using-the-wizard"></a>使用精靈進行安裝

使用精靈部署應用程式時，您也可以使用這項功能。

1. 建立或編輯應用程式。
2. 將應用程式部署至用戶端。
3. 從軟體中心安裝應用程式。 應用程式安裝介面應該會出現。 終端使用者應該遵循應用程式安裝精靈，並已成功安裝應用程式。




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
