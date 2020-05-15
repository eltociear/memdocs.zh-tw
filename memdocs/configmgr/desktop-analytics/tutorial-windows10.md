---
title: 教學課程 - 部署 Windows 10
titleSuffix: Configuration Manager
description: 有關使用電腦分析與 Configuration Manager 將 Windows 10 部署到試驗群組的教學課程。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b991c2ddd0ea121251eb19afbdb032844be8738d
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268193"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>教學課程：將 Windows 10 部署至試驗

本教學課程使用電腦分析與 Configuration Manager 將 Windows 10 部署到試驗群組。 其強調透過整合雲端服務來提供見解，以搭配內部部署產品部署 Windows。 您可以使用電腦分析，判斷要放入試驗群組中的最佳裝置。 然後使用 Configuration Manager 讓 Windows 保持最新狀態。

在本教學課程中，您將了解如何：  

> [!div class="checklist"]  
> * 在 Azure 入口網站中設定電腦分析  
> * 連線 Configuration Manager 並進行裝置設定  
> * 建立適用於 Windows 10 的電腦分析部署計劃  
> * 使用 Configuration Manager 將 Windows 10 部署到試驗群組  

如果您沒有 Azure 訂用帳戶，請先建立[免費帳戶](https://azure.microsoft.com/free)，再開始進行。 若正確設定，使用電腦分析並不會產生任何 Azure 費用。

電腦分析使用 Azure 訂用帳戶中的「Log Analytics 工作區」  。 工作區本質上是一個容器，包含帳戶資訊和帳戶的簡單設定資訊。 如需詳細資訊，請參閱[管理工作區](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json)。



## <a name="prerequisites"></a>先決條件

開始進行本教學課程之前，請確定您具有下列必要條件：  

- 具有[**全域管理員**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)權限的使用中 Azure 訂用帳戶  

    如需詳細資訊，請參閱[電腦分析必要條件](overview.md#prerequisites)。

- 具有**系統高權限管理員**角色的 Configuration Manager 1902 版含更新彙總套件 (4500571) 或更新版本  

- 最新版 Windows 10 的安裝媒體

- 至少一部具有下列設定的 Windows 10 裝置：  

    - Windows 10 1709 版或更新版本，但低於您打算使用的安裝媒體版本

    - 最新的 Windows 10 累積品質更新  

    - Configuration Manager 用戶端 1902 版含更新彙總套件 (4500571) 或更新版本  

- 將試驗裝置上的 Windows 診斷資料層級設定為 [增強 (受限)]  的商務核准  

    如需詳細資訊，請參閱[電腦分析隱私權](privacy.md)。

- 從裝置到下列網際網路端點的網路連線：

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (僅限在 Configuration Manager 伺服器角色上)
    - `https://*.manage.microsoft.com` (僅限在 Configuration Manager 伺服器角色上)

    如需詳細資訊，請參閱[如何啟用電腦分析的資料共用](enable-data-sharing.md#endpoints)。  

> [!Important]  
> 這些必要條件適用於本教學課程的目的。 如需電腦分析與 Configuration Manager 的一般必要條件詳細資訊，請參閱[必要條件](overview.md#prerequisites)。  



## <a name="set-up-desktop-analytics"></a>設定電腦分析

使用此程序登入電腦分析，並在您的訂用帳戶中加以設定。 此程序是為您組織設定電腦分析的一次性程序。  

1. 以具有**全域管理員**權限的使用者身分，在 Microsoft 365 裝置管理中開啟[電腦分析入口網站](https://aka.ms/desktopanalytics)。 選取 [開始]  。  

2. 在 [接受服務合約]  頁面上檢閱服務合約，然後選取 [接受]  。  

3. 在 [確認您的訂閱]  頁面上，會列出所需的合格授權，以便使用電腦分析的 Windows 裝置健康情況功能。 選取 [下一步]  以繼續進行操作。  

4. 在 [Give users access] \(授與使用者存取權\)  頁面上：

    - **讓電腦分析代表您管理目錄角色**：電腦分析會自動為**工作區擁有者**指派**電腦分析系統管理員**角色。 如果這些群組已經是**全域管理員**，就不會有任何變更。  

        如果您未選取此選項，電腦分析仍會將使用者新增為安全性群組的成員。 **全域管理員**需要手動為使用者指派**電腦分析系統管理員**角色。  

        如需在 Azure Active Directory 中指派系統管理員角色權限的詳細資訊，以及指派給**電腦分析系統管理員**的權限，請參閱 [Administrator role permissions in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) (Azure Active Directory 中的系統管理員角色權限)。  

    - 電腦分析在 Azure Active Directory 中預先設定了**工作區擁有者**安全性群組，以建立及管理工作區和部署計劃。 

        若要將使用者新增至群組，請在 [輸入名稱或電子郵件地址]  區段中，鍵入其名稱或電子郵件地址。 完成後，選取 [下一步]  。

5. 在 [設定您的工作區]  頁面上：  

    > [!Note]  
    > 若要完成此步驟，使用者需要**工作區擁有者**權限，以及 Azure 訂用帳戶和資源群組的其他存取權。 如需詳細資訊，請參閱[必要條件](overview.md#prerequisites)。  

    - 選取您的 Azure 訂用帳戶。  

    - 若要使用電腦分析的現有工作區，請加以選取，然後繼續下一個步驟。  

    - 若要為電腦分析建立工作區，請選取 [新增工作區]  。  

        1. 輸入 [工作區名稱]  。  

        2. 選取 [Select the Azure subscription name for this workspace] \(選取此工作區的 Azure 訂用帳戶名稱\)  的下拉式清單，然後選擇此工作區的 Azure 訂用帳戶。  

        3. [新建]  資源群組或 [使用現有的]  資源群組。  

        4. 從清單中選取 [區域]  ，然後選取 [新增]  。  

6. 選取新的或現有的工作區，然後選取 [設為電腦分析工作區]  。  然後在 [確認並授與存取]  對話方塊中選取 [繼續]  。  

7. 在新的瀏覽器索引標籤中，選擇要登入的帳戶。 選取 [代表您的組織同意]  選項，然後選取 [接受]  。  


    > [!Note]  
    > 此同意允許將工作區的 Log Analytics 讀取者角色指派給 MALogAnalyticsReader 應用程式。 電腦分析需要此應用程式角色。 如需詳細資訊，請參閱 [MALogAnalyticsReader 應用程式角色](troubleshooting.md#bkmk_MALogAnalyticsReader)。  

8. 回到 [設定您的工作區]  頁面，並選取 [下一步]  。  

9. 在 [最後步驟]  頁面上，選取 [移至電腦分析]  。 Azure 入口網站會顯示電腦分析 [首頁]  頁面。  



## <a name="connect-configuration-manager"></a>連線 Configuration Manager

使用此程序更新 Configuration Manager、連線到電腦分析，並進行裝置設定。 此程序是將您的階層附加至雲端服務的一次性程序。  

### <a name="update-configuration-manager"></a>更新 Configuration Manager

安裝 Configuration Manager 1902 版更新彙總套件 (4500571)，以支援與電腦分析的整合。 如需此更新的詳細資訊，請參閱 [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4500571) (Configuration Manager 最新分支 1902 版的更新彙總套件)。

1. 使用 1902 版的更新彙總套件來更新站台。 如需詳細資訊，請參閱[安裝主控台內的更新](../core/servers/manage/install-in-console-updates.md)。  

2. 更新用戶端。 如果要簡化此程序，請考慮使用自動用戶端升級。 如需詳細資訊，請參閱[升級用戶端](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。  


### <a name="connect-to-the-service"></a>連線到服務

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。 選取功能區中的 [設定 Azure 服務]  。  

2. 在 [Azure 服務精靈] 的 [Azure 服務]  頁面上，進行下列設定：  

    - 為 Configuration Manager 中的物件指定 [名稱]   

    - 指定選用 [描述]  ，協助您識別服務  

    - 從可用的服務清單中選取 [電腦分析]   
  
   選取 [下一步]  。  

3. 在 [應用程式]  頁面上，選取適當的 **Azure 環境**。 然後針對 Web 應用程式選取 [瀏覽]  。

4. 選取 [建立]  ，輕鬆地新增要進行電腦分析連線的 Azure AD 應用程式。

5. 在 [建立伺服器應用程式]  視窗中進行下列設定：  

    - **應用程式名稱**：Azure AD 中應用程式的易記名稱。

    - **首頁 URL**：Configuration Manager 不使用此值，但卻是 Azure AD 的必要值。 根據預設，此值為 `https://ConfigMgrService`。  

    - **App 識別碼 URI**：這在 Azure AD 租用戶中必須是唯一的值。 其位於 Configuration Manager 用戶端用來要求存取服務的存取權杖中。 根據預設，此值為 `https://ConfigMgrService`。  

    - **祕密金鑰有效期間**：從下拉式清單中選擇 [1 年]  或 [2 年]  。 預設值為一年。  

    選取 [登入]  。 向 Azure 成功驗證身分後，頁面會顯示 [Azure AD 租用戶名稱]  以供參考。

    > [!Note]  
    > 以**全域管理員**身分完成此步驟。Configuration Manager 不會儲存這些認證。 此角色在 Configuration Manager 中不需要權限，而且不需要為執行 Azure 服務精靈的相同帳戶。  

    選取 [確定]  以在 Azure AD 中建立 Web 應用程式，然後關閉 [建立伺服器應用程式] 對話方塊。 在 [伺服器應用程式] 對話方塊上，選取 [確定]  。 然後在 [Azure 服務精靈] 的 [應用程式] 頁面上，選取 [下一步]  。  

6. 在 [診斷資料]  頁面上，進行下列設定：  

    - **商業識別碼**：此值應該會自動填入您的組織識別碼  

    - **Windows 10 診斷資料層級**：至少選取 [增強 (受限)]   

    - **允許診斷資料中的裝置名稱**：選取 [啟用]   
  
   選取 [下一步]  。 [可用的功能]  頁面會顯示可用的電腦分析功能，其中包含上一頁中的診斷資料設定。 選取 [下一步]  。  

7. 在 [集合]  頁面上，進行下列設定：  

    - **顯示名稱**：電腦分析入口網站會使用此名稱來顯示此 Configuration Manager 連線。 其可用來區別不同的階層。 例如，「測試實驗室」  或「生產環境」  。  

    - **目標集合**：此集合包含 Configuration Manager 使用商業識別碼與診斷資料設定來進行設定的所有裝置。 這是一組由 Configuration Manager 連線至電腦分析服務的完整裝置。  

    - **目標集合中的裝置使用使用者已驗證 Proxy 進行輸出通訊**：根據預設，此值為 [否]  。 視環境需要，請將其設定為 [是]  。  

    - **選取要與電腦分析同步的特定集合**：選取 [新增]  以包含其他集合。 這些集合可以在電腦分析入口網站中使用，並與部署計劃組成群組。 請確保此新增包含試驗與試驗排除集合。  

        這些集合會隨著成員資格的變更，持續同步。 例如，部署計劃使用含有 Windows 7 成員資格規則的集合。 當這些裝置升級至 Windows 10，且 Configuration Manager 評估集合成員資格時，這些裝置將會從集合與部署計劃中移出。  

8. 完成精靈。  

Configuration Manager 會建立設定原則來設定目標集合中的裝置。 此原則包括可讓裝置將資料傳送至 Microsoft 的診斷資料設定。 根據預設，用戶端會每小時更新原則一次。 收到新的設定之後，可能需要數小時的時間，資料才可供電腦分析使用。

> [!Note]  
> 如需這些設定的詳細資訊，請參閱 [Windows 設定](enroll-devices.md#windows-settings)。  

監視裝置的設定以進行電腦分析。 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [電腦分析服務]  節點，然後選取 [連線健康情況]  儀表板。  

Configuration Manager 會在建立連線的 60 分鐘內同步集合。 在電腦分析入口網站中，前往 [通用試驗]  ，然後查看 Configuration Manager 裝置集合。 入口網站的其餘部分可能需要兩到三天才會顯示完整資料。 如需詳細資訊，請參閱[資料延遲](troubleshooting.md#data-latency)。

## <a name="create-a-desktop-analytics-deployment-plan"></a>建立電腦分析部署計劃

使用此程序在電腦分析中建立部署計劃。

1. 開啟[電腦分析入口網站](https://aka.ms/desktopanalytics)。 請使用至少具有**工作區參與者**權限的認證。  

2. 選取 [管理] 群組中的 [部署計劃]  。  

3. 在 [部署計劃]  窗格中，選取 [建立]  。  

4. 在 [建立部署計劃]  窗格中，進行下列設定：  

    - **名稱**：部署計劃的唯一名稱，例如 `Windows 10 pilot`  

    - **產品與版本**：選取 [Windows]  產品，以及最新的可用建議版本。 例如，**Windows 10 1809 版 (建議使用)** 。  

    - **裝置群組**：從 [Configuration Manager] 索引標籤選取一或多個群組，然後選取 [設定為目標群組]  。 這些群組是從 Configuration Manager 同步的集合。  

    - **整備規則**：這些規則有助於您判斷哪些裝置符合升級資格。 選取 [Windows OS]  並進行下列設定：  

        - **我的電腦會自動從 Windows Update 取得驅動程式**：預設設定為 [關閉]  ，這是使用 Configuration Manager 進行部署時的建議做法。  

        - **定義應用程式的低安裝計數閾值**：預設設定為 `2%`。 低於此閾值的應用程式會自動設定為 [低安裝計數]  。 電腦分析在試驗期間不會驗證這些增益集。  

            如果安裝此應用程式的電腦百分比高於此閾值，部署計劃會將應用程式標示為 [值得注意]  。 然後您可以決定應用程式在試驗階段期間對測試的重要性。  

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



## <a name="deploy-windows-10-in-configuration-manager"></a>在 Configuration Manager 中部署 Windows 10

使用此程序在 Configuration Manager 中將 Windows 10 部署到試驗群組。

- 如果還沒有，請先[建立 Windows 10 的 OS 升級套件](#bkmk_create-package)  

- 如果還沒有，請[建立 Windows 10 的 OS 升級工作順序](#bkmk_create-ts)  

- 使用電腦分析部署計劃[部署工作順序](#bkmk_deploy-ts)  

- 從軟體中心在目標裝置上[安裝工作順序](#bkmk_install-ts)  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> 建立 Windows 10 的 OS 升級套件

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [作業系統升級套件]  節點。  

2. 在功能區索引標籤 [首頁]  上的 [建立]  群組中，選取 [新增作業系統升級套件]  。 此動作會啟動 [新增作業系統升級精靈]。  

3. 在 [資料來源]  頁面上，指定 OS 升級套件安裝來源檔案的網路 [路徑]  。 例如 `\\server\share\path`。  

    > [!NOTE]  
    > 安裝來源檔案包含 setup.exe 和其他檔案及資料夾，以便安裝 OS。  

4. 在 [一般]  頁面上，指定 OS 升級套件的唯一 [名稱]  。  

5. 完成 [新增作業系統升級套件精靈]。  

#### <a name="distribute-content"></a>發佈內容

接下來，將 OS 升級套件發佈至發佈點。  

1. 選取清單中的 OS 升級套件。 在功能區 [常用]  索引標籤上的 [部署]  群組中，選取 [發佈內容]  。 [發佈內容精靈] 隨即開啟。  

2. 在 [一般]  頁面上，確認列出的內容是您要發佈的內容，然後選取 [下一步]  。  

3. 在 [內容目的地]  頁面上，選取 [新增]  ，然後選擇 [發佈點]  。 選取現有的發佈點，然後選取 [確定]  。 完成新增內容目的地後，選取 [下一步]  。  

4. 完成 [發佈內容精靈]。  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a> 建立 Windows 10 的 OS 升級工作順序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序]  。  

3. 在 [建立工作順序精靈] 的 [建立新的工作順序]  頁面上，選取 [從升級套件升級作業系統]  ，然後選取 [下一步]  。  

4. 在 [工作順序資訊]  頁面上，指定識別工作順序的 [工作順序名稱]  。  

5. 在 [升級 Windows 作業系統]  頁面上，指定下列設定，然後選取 [下一步]  ：  

    - **升級套件**：指定包含 OS 升級來源檔案的升級套件。  

    - **版本索引**：如果套件中有多個 OS 版本索引，請選取所需的版本索引。 根據預設，精靈會選取第一個索引。  

    - **產品金鑰**：指定所要安裝 OS 的 Windows 產品金鑰。 請指定編碼的大量授權金鑰或標準產品金鑰。 如果您使用標準產品金鑰，請以虛線 (-) 分隔五個字元的每個群組。 例如：*XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*。 當大量授權版本進行升級時，可能不需要產品金鑰。  

        > [!Note]  
        > 此產品金鑰可為多次啟用金鑰 (MAK) 或泛型的大量授權金鑰 (GVLK)。 GVLK 也稱為金鑰管理服務 (KMS) 的用戶端安裝金鑰。 如需詳細資訊，請參閱[大量啟用計劃](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 用戶端安裝金鑰的清單，請參閱＜Windows Server 啟用指南 ＞的[附錄 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。

6. 在 [包含更新]  頁面上，選取 [下一步]  不要安裝任何軟體更新。  

7. 在 [安裝應用程式]  頁面上，選取 [下一步]  不要安裝任何應用程式。

8. 完成 [建立工作順序精靈]。  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> 使用電腦分析部署計劃部署工作順序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  ，展開 [電腦分析服務]  ，然後選取 [部署計劃]  節點。  

2. 選取您的 Windows 10 試驗部署計劃，然後在功能區中選取 [部署計劃詳細資料]  。  

3. 從 [試驗狀態]  磚的下拉式清單中選擇 [工作順序]  ，然後選取 [部署]  。  

4. 在 [部署軟體精靈] 的 [一般]  頁面上，選取 [軟體]  欄位旁的 [瀏覽]  。 選取您的 Windows 10 就地升級工作順序，然後選取 [下一步]  。  

    > [!Note]  
    > 透過電腦分析整合，Configuration Manager 可自動建立部署計劃的試驗和生產環境集合。 這些集合需要一些時間先行同步，才能供您使用。 如需詳細資訊，請參閱[疑難排解 - 資料延遲](troubleshooting.md#data-latency)。<!-- 4984639 -->
    >
    > 此集合會保留供電腦分析部署計劃裝置使用。 不支援手動變更此集合。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 在 [內容]  頁面上，選取 [新增]  ，然後選取 [發佈點]  。 選取可用的發佈點來裝載安裝內容，然後選取 [確定]  。 然後選取 [下一步]  。  

6. 在 [部署設定]  頁面上，選取 [下一步]  接受預設設定 (可用的安裝)。  

7. 在 [排程]  頁面上，選取 [下一步]  接受預設設定 (即將推出)。  

8. 在 [使用者體驗]  頁面上，選取 [下一步]  接受預設設定 (顯示在軟體中心中並僅顯示電腦重新啟動通知)。  

9. 在 [警示]  頁面上，選取 [下一步]  接受預設設定。  

10. 完成精靈。  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> 從軟體中心安裝工作順序

1. 登入屬於試驗部署計劃成員的裝置。  

2. 開啟 [軟體中心]  並安裝 Windows 10 的可用作業系統。  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>後續步驟

前往下一篇文章，深入了解電腦分析部署計劃。
> [!div class="nextstepaction"]  
> [部署計劃](about-deployment-plans.md)
