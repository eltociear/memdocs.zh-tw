---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1708 版中可用的功能。
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705156"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Configuration Manager Technical Preview 1708 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1708 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 的已知問題：**
- **當您有以被動模式執行的站台伺服器時，更新到預覽版 1708 失敗**。 當您執行預覽版 1706 或 1707 且有[以被動模式執行的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)時，必須先將被動模式站台伺服器解除安裝，才能順利將預覽站台更新到 1708 版。 當您的站台執行 1708 版之後，就可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。




**以下是您可以使用此版本試用的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>從 Configuration Manager 部署 PowerShell 指令碼時，改善指令碼參數的指定
<!-- 1236459 -->

從 Configuration Manager 1706 開始，您可以[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](../../apps/deploy-use/create-deploy-scripts.md)。

[Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) 擴充了此功能，讓 Configuration Manager 可以從指令碼讀取參數。

此 Technical Preview 擴充了指令碼參數功能，可偵測何者為強制參數，何者為選擇性參數，並提示您輸入這些參數。

### <a name="try-it-out"></a>試試看！

1. 遵循[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](../../apps/deploy-use/create-deploy-scripts.md)的指示。
2. 在 [建立指令碼精靈]  的新 [指令碼參數]  頁面上選擇參數，然後編輯參數的值。
精靈會顯示何者為強制參數，何者為選擇性參數。
4. 完成編輯參數之後，請完成精靈。

指令碼執行時，會使用您所設定的任何參數值。 若未設定強制參數，則指令碼執行時將會要求使用者提供參數。

## <a name="management-insights"></a>Management Insights
<!-- 1353967 -->
您現在可以根據站台資料庫中的資料分析，取得環境目前狀態的深入解析。 深入解析可協助您進一步了解您的環境，並據以採取行動。 在 [管理]   > [Management Insights]   > [所有 Insights]  中，可以在 Configuration Manager 主控台中檢閱 Management Insights。 此版本目前提供下列深入解析：

- **沒有部署的應用程式**：列出環境中沒有作用中部署的應用程式。 如此可協助您尋找並刪除未使用的應用程式，以簡化主控台中顯示的應用程式清單。
- **空集合**：列出環境中沒有成員的集合。 您可以刪除這些集合，其目的像是簡化部署物件時顯示的集合清單。


## <a name="restart-computers-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台重新啟動電腦   
<!-- 1356283 -->
從此版本開始，您可以使用 Configuration Manager 主控台來識別需要重新啟動的用戶端裝置，然後使用用戶端通知動作來重新啟動這些裝置。

若要識別擱置重新啟動的裝置，請移至 [資產與合規性]   > [裝置]  ，並選取包含需要重新啟動裝置的集合。 選取集合之後，可以在名為 [擱置重新開機]  的新欄中，於詳細資料窗格中檢視每個裝置的狀態。 每個裝置的值為 [是]  或 [否]  。

若要建立重新啟動裝置的用戶端通知：
1. 在主控台的 [裝置] 節點中，找出您想要重新啟動的裝置。
2. 以滑鼠右鍵按一下裝置，選取 [用戶端通知]  ，然後選取 [重新開機]  。 如此會開啟有關重新啟動的 [資訊] 視窗。 按一下 [確定]  以確認重新啟動要求。

當通知抵達用戶端時，會開啟 [軟體中心]  通知視窗，以通知使用者有關重新啟動一事。 根據預設，將會在 90 分鐘後重新啟動。 您可以設定[用戶端設定](../clients/deploy/configure-client-settings.md)，以修改重新啟動時間。 重新啟動行為的設定位於預設設定的[電腦重新啟動](../clients/deploy/about-client-settings.md#computer-restart)索引標籤上。


### <a name="try-it-out"></a>試試看！
請嘗試完成下列工作，然後從功能區的 [首頁]  索引標籤中傳送 [意見反應]  給我們，讓我們了解運作情況：
1. 在裝置上部署應用程式或更新，將會需要裝置重新啟動才能完成安裝。
2. 在主控台的 [資產與合規性]   > [裝置]  節點中找出裝置，並確認 [擱置重新開機]  欄中顯示 [是]  。 [擱置重新開機] 狀態最多可能需要 20 分鐘的時間，才會反映在主控台中。
3. 監視裝置以確認 [軟體中心] 通知會隨之開啟，且裝置順利重新啟動。


## <a name="software-center-customization"></a>軟體中心自訂
<!-- 1351224 -->
您可以在 [軟體中心] 上加入企業品牌元素，以及指定索引標籤的可見性。 您可以加入 [軟體中心] 特定的公司名稱、設定 [軟體中心] 組態色彩佈景主題、設定公司標誌，以及設定用戶端裝置的可見索引標籤。

### <a name="customize-software-center"></a>自訂軟體中心

若要修改軟體中心：

1. 在 Configuration Manager  主控台中，選擇 [系統管理]   > [用戶端設定]  。 按一下想要的用戶端設定執行個體。
2. 在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。
3. 在 [預設設定]  對話方塊中，選擇 [軟體中心]  。
4. 選取 [是]  以 [選取新設定以指定公司資訊]  ，以便啟用 [軟體中心] 自訂設定。
5. 輸入您的 [公司名稱]  。
6. 選取您的 [軟體中心色彩配置]  。
7. 按一下 [瀏覽]  以移至您的 [軟體中心] 標誌。 標誌必須是 400 x 100 像素的 JPEG 或 PNG，且大小上限為 750 KB。
8. 選取 [是]  來讓索引標籤顯示在用戶端裝置的 [軟體中心] 中。 至少要有一個可見的索引標籤：

    -  [啟用應用程式] 索引標籤
    -  [啟用更新] 索引標籤
    -  [啟用作業系統] 索引標籤
    -  [啟用安裝狀態] 索引標籤
    -  [啟用裝置合規性] 索引標籤
    -  [啟用選項] 索引標籤

### <a name="next-steps"></a>後續步驟

若要深入了解 Configuration Manager 中的應用程式管理，請參閱[應用程式管理簡介](../../apps/understand/introduction-to-application-management.md)。
