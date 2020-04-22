---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1805 版中可用的新功能。
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 88234bb3117850bc3280242671ae459308a5262e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696026"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Configuration Manager Technical Preview 1805 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Technical Preview for Configuration Manager 1805 中可用的功能。 您可以安裝此版本，以將新功能更新並新增至您的技術預覽版網站。 

請先檢閱[技術預覽版](technical-preview.md)文章，再安裝此更新。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**以下是您可以使用此版本試用的新功能。**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>建立分階段部署以及手動設定工作順序的不同階段
<!--1358148-->
您現在可以[建立分階段部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)，而且還能手動設定工作順序的不同階段。 您可以從「建立分階段部署」精靈的 [階段]  索引標籤，新增多達 10 個額外的階段。 


### <a name="try-it-out"></a>試試看！
請依照下列指示建立分階段部署，讓您可以手動設定所有的階段。 傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。 

1. 在 [軟體程式庫]  工作區中，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 以滑鼠右鍵按一下現有的工作順序，然後選取 [Create Phased Deployment] \(建立分階段部署)  。  

3. 在 [一般]  索引標籤上，指定分階段部署的名稱、描述 (選擇性)，然後選取 [手動設定所有的階段]  。  

4. 在 [階段]  索引標籤上，按一下 [新增]  。  

5. 指定階段的 [名稱]  ，接著瀏覽至目標 [階段集合]  。  

6. 在 [階段設定]  索引標籤上，針對每個排程設定選擇一個選項，然後在完成時選取 [下一步]  。  

    - 上一個階段的成功條件 (此選項已會在第一個階段停用)。
        - **部署成功百分比**：指定有多少百分比的裝置符合前一個階段成功準則，屬於已成功完成部署。  

    - 在前一個階段成功後，應當在何種條條之下開始這個部署階段  
        - **在一段延遲期間 (天) 之後自動開始此階段**：選擇前一個階段成功之後，須先等待多少天時間過後，才能開始下一個階段。 
        - **手動開始這個階段部署**：在前一個階段成功之後，不要自動開始這個個階段。  

    - 裝置一設為目標後就安裝該軟體
        - **盡快**：裝置一設為目標後，盡快在裝置上設定安裝期限。
        - **期限時間 (相對於將裝置設為目標的時間)** ：設定要在將裝置設為目標後的特定天數內進行安裝的期限。  
     
7. 完成階段設定精靈。

8. 在「建立分階段部署」精靈的 [階段]  索引標籤中，您現在可以新增、移除、重新排列或編輯不同的部署階段。  

9. 完成「建立分階段部署」精靈。  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Azure Resource Manager 的支援雲端發佈點支援
<!--1322209-->
建立[雲端發佈點](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)的執行個體時，精靈現在會提供此選項來建立 **Azure Resource Manager 部署**。 [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) 是可將所有解決方案資源當作單一實體 (稱為[資源群組](/azure/azure-resource-manager/resource-group-overview#resource-groups)) 來管理的新式平台。 使用 Azure Resource Manager 部署雲端發佈點時，站台會使用 Azure Active Directory (Azure AD) 來驗證並建立必要的雲端資源。 這個現代化的部署不需要傳統的 Azure 管理憑證。  

雲端發佈點精靈仍會使用 Azure 管理憑證來提供**傳統服務部署**的選項。 若要簡化資源的部署與管理，我們建議針對所有新的雲端發佈點執行個體使用 Azure Resource Manager 部署模型。 如果可能，請透過 Resource Manager 重新部署現有的雲端發佈點執行個體。

Configuration Manager 不會將現有的傳統雲端發佈點執行個體移轉至 Azure Resource Manager 部署模型。 使用 Azure Resource Manager 部署來建立新的雲端發佈點，然後移除傳統雲端發佈點。 

> [!IMPORTANT]  
> 此功能不會啟用對 Azure 雲端服務提供者 (CSP) 的支援。 使用 Azure Resource Manager 的雲端發佈點部署會繼續使用 CSP 不支援的傳統雲端服務。 如需詳細資訊，請參閱 [Azure CSP 中可用的 Azure 服務](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  


### <a name="prerequisites"></a>先決條件  
- 與 [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md) 整合。 不需要 Azure AD 使用者探索。  

- 相同的[雲端發佈點需求](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements)，但 Azure 管理憑證除外。  


### <a name="try-it-out"></a>試試看！  
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台的 [系統管理]  工作區中，展開 [雲端服務]  ，然後選取 [雲端發佈點]  。 按一下功能區中的 [建立雲端發佈點]  。   

2. 在 [一般]  頁面上，選取 [Azure Resource Manager 部署]  。 按一下 [登入]  ，使用 Azure 訂用帳戶系統管理員帳戶進行驗證。 精靈會使用整合先決條件期間所儲存的 Azure AD 訂用帳戶資訊，自動填入其餘欄位。 如果您擁有多個訂用帳戶，請選取需要使用的訂用帳戶。 按一下 [下一步]  。  

3. 在 [設定]  頁面上，如往常般提供伺服器 PKI **憑證檔案**。 此憑證會定義 Azure 使用的雲端發佈點**服務 FQDN**。 選取 [區域]  ，然後針對資源群組選項選取 [新建]  或 [使用現有的]  。 輸入新的資源群組名稱，或從下拉式清單中選取現有的資源群組。  

4. 完成精靈。  

> [!NOTE]  
> 針對選取的 Azure AD 伺服器應用程式，Azure 會指派訂用帳戶**參與者**權限。  

在服務連接點上，使用 **cloudmgr.log** 監視服務部署進度。



## <a name="take-actions-based-on-management-insights"></a>根據管理見解採取動作
<!--1357930-->
某些[管理見解](../servers/manage/management-insights.md)現在會選擇採取動作。 根據規則，此動作會表現出以下其中一種行為：  

- 自動瀏覽至主控台中，您可以採取進一步動作的節點。 例如，如果管理見解建議變更用戶端設定，則採取動作會瀏覽至 [用戶端設定] 節點。 您可以修改預設或自訂的用戶端設定物件，採取進一步的動作。  

- 瀏覽至根據查詢而篩選的檢視。 例如，根據空集合規則而採取動作，只會顯示集合清單中的這些集合。 這裡您可以採取進一步的動作，例如刪除集合或修改其成員資格規則。  

下列管理見解規則會有此版本的動作：
- 安全性
    - 不受支援的反惡意程式碼用戶端版本
- 軟體中心
    - 使用新版的軟體中心
- 應用程式
    - 沒有部署的應用程式
- 簡化的管理
    - 非 CB 用戶端版本
- 集合
    - 空集合 
- 雲端服務
    - 將用戶端更新為最新的 Windows 10 版本



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>使用共同管理將裝置設定工作負載轉換至 Intune
<!--1357903-->

您現在可以在啟用共同管理之後，將裝置設定工作負載，從 Configuration Manager 轉換至 Intune。 轉換此工作負載可讓您使用 Intune 部署 MDM 原則，同時繼續使用 Configuration Manager 部署應用程式。 

若要轉換此工作負載，請前往共同管理內容頁面，然後將滑動軸從 [Configuration Manager] 移至 [試驗]  或 [所有]  。 如需詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../comanage/overview.md)。

> [!Note]  
> 移動此工作負載也會移動**資源存取**和**Endpoint Protection**工作負載，也就是裝置組態工作負載的子集。

當您轉換此工作負載時，即使 Intune 是裝置設定授權單位，仍可以將設定從 Configuration Manager 部署至共同管理的裝置。 這個例外狀況可能會用來配置您的組織會用到，但 Intune 目前還沒有的設定。 在 Configuration Manager 的組態基準上，指定這個例外狀況。 建立基準或者在現有基準內容的 [一般]  索引標籤上，啟用**即便是共同管理的用戶端也一律套用此基準**的選項。 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>啟用要使用網路壅塞控制的發佈點
<!--1358112-->

Windows 低額外延遲背景傳輸 (LEDBAT) 是 Windows Server 的一個功能，能協助管理背景網路傳輸。 至於在所支援 Windows Server 版本上執行的發佈點，您可以啟用一個選項來協助調整網路流量。 有的話，用戶端只會使用網路頻寬。 

如需有關 Windows LEDBAT 的詳細資訊，請參閱[新的傳輸功能改進](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) \(New transport advancements\) 部落格文章。


### <a name="prerequisites"></a>先決條件
- Windows Server 版本 1709 上的發佈點。  

- 沒有用戶端必要條件。<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 選取 [發佈點]  節點。 選取目標發佈點，然後按一下功能區中的 [屬性]  。  

2. 在 [一般]  索引標籤上，啟用此選項來**調整下載速度來使用未使用的網路頻寬 (Windows LEDBAT)** 。  



## <a name="cloud-management-dashboard"></a>雲端管理儀表板
<!--1358461-->
新的**雲端管理儀表板**提供集中式檢視，它能顯示雲端管理閘道 (CMG) 使用量。 當站台配合 Azure AD 時，它也會顯示雲端使用者和裝置相關資料。  

下列螢幕擷取畫面顯示雲端管理儀表板的某個部分顯示兩個可用的圖格：  
![雲端管理儀表板圖格 CMG 流量和目前的線上用戶端](media/1358461-cmg-dashboard.png)

這項功能也包括 **CMG 連線分析器**，它能即時驗證，以協助解決問題。 主控台內的公用程式會檢查目前狀態的服務，以及檢查 CMG 連接點與任何允許 CMG 流量的管理點，二者之間通訊頻道。


### <a name="prerequisites"></a>先決條件
- 網際網路用戶端可以使用的有效[雲端管理閘道](../clients/manage/cmg/plan-cloud-management-gateway.md)。  

- 該站台配合 [Azure 服務](../servers/deploy/configure/azure-services-wizard.md)以進行雲端管理。  


### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

#### <a name="cloud-management-dashboard"></a>雲端管理儀表板

在 Configuration Manager 主控台中，按一下 [監視]  工作區。 選取 [雲端管理]  節點，並檢視儀表板圖格。  

#### <a name="cmg-connection-analyzer"></a>CMG 連接分析器

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [雲端服務]  ，然後選取 [雲端管理閘道]  。  

2. 選取目標 CMG 執行個體，然後選取功能區中的 [連接分析器]  。  

3. 在 CMG 連接分析器視窗中，選取下列其中一個選項，向服務進行驗證：  

     1. **Azure AD 使用者**：使用此選項來模擬以雲端使用者身分登入已加入 Azure AD 的 Windows 10 裝置通訊。 按一下 [登入]  ，放心輸入這個 Azure AD 使用者帳戶的認證。  

     2. **用戶端憑證**：使用此選項來模擬利用[用戶端驗證憑證](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth)的 Configuration Manager 用戶端通訊。  

4. 按一下 [啟動]  ，啟動應用程式集區。 結果會顯示在分析器視窗中。 選取一個項目，然後在 [描述] 欄位查看更多的詳細資訊。  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager 一律提供大型中央裝置資料存放區，供客戶處理報表時使用。 不過，資料的好壞與否，取決於它從用戶端收集的時間。 

CMPivot 是新的主控台內部公用程式，能存取環境中的裝置即時狀態。 它能立即在目標集合中，所有目前已連線的裝置上執行查詢，然後傳回結果。 然後，您可以使用這個工具來篩選此資料並進行分組。 提供線上用戶端的即時資料，讓您更快速地回答事務問題、解決問題，並回應安全性事件。

例如，在[修補投機性執行端通道漏洞](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)中，其中一項需求是更新系統 BIOS。 您可以使用 CMPivot 快速地查詢系統 BIOS 資訊，並找出不符合規範的用戶端。 

在這個螢幕擷取畫面中，CMPivot 會顯示兩個不同的 BIOS 版本，而且每一個都有一個裝置計數。 當您試著操作 CMPivot 時，可以使用這個範例查詢：  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![CMPivot 視窗以及 BIOSVersion 的範例查詢](media/1358456-cmpivot-biosversion.png)

您可以按一下裝置計數，即可向下切入來查看特定的裝置。 在 CMPivot 中顯示裝置時，您可以在裝置上按一下滑鼠右鍵，然後選取下列的[用戶端通知動作](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode):
- 執行指令碼
- 遠端控制
- 資源總管

在特定的裝置按滑鼠右鍵後，您也可以將特定裝置的檢視轉換成下列其中一個：
- 自動啟動命令
- 已安裝的產品
- Processes
- 服務
- 使用者
- 作用中的連線
- 遺失更新

### <a name="prerequisites"></a>先決條件
- 目標用戶端必須更新至最新版本。  

- Configuration Manager 系統管理員需要執行指令碼的權限。 如需詳細資訊，請參閱[指令碼的安全角色](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles)。  

### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選擇 [裝置集合]  。 選取一個目標集合，然後按一下功能區中的 [啟動 CMPivot]  來啟動這個工具。  

2. 這個介面提供工具更詳細的操作方法。 
     - 您可以在上方手動輸入查詢字串，或按一下內嵌文件中的連結。
     - 按一下其中一個 [實體]  ，將它加入查詢字串。 
     - **資料表運算子**，**彙總函式**和**純量函式**的連結會在瀏覽器中開啟語言參考文件。 CMPivot 使用與 [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/) 相同的查詢語言。



## <a name="improved-secure-client-communications"></a>改善的安全用戶端通訊
<!--1356889,1358228,1358460-->
建立所有 Configuration Manager 通訊路徑都使用 HTTPS 通訊，不過管理 PKI 憑證需付出額外的人力物力，對於某些客戶而言實難以辦到。 Azure Active Directory (Azure AD) 整合功能的引進，可減少一些憑證需求，但無法根除。 

此版本在用戶端與網站系統通訊方面，增強很多的功能。 這些增強的功能，目前有兩個主要的目標：  

- 您可以保護用戶端通訊，而不需要 PKI 伺服器驗證憑證。  

- 用戶端可以安全地從發佈點存取內容，而不需要網路存取帳戶。  

> [!Note]  
> 對於需要的客戶而言，PKI 憑證仍是有效的選項。  


### <a name="scenarios"></a><a name="bkmk_token"></a> 案例
以下案例會因為這些增強的功能而獲益：  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a> 案例 1：用戶端對管理點
<!--1356889-->
[已加入 Azure AD 的裝置](/azure/active-directory/devices/concept-azure-ad-join)可以透過雲端管理閘道 (CMG)，與某一個為 HTTP 設定的管理點進行通訊。 站台伺服器會為管理點產生一個憑證，讓它可以透過安全通道進行通訊。   

> [!Note]  
> 此行為是從 Configuration Manager 目前的分支版本 1802 變更的，在此案例中，它需要一個啟用 HTTPS 的管理點。 如需詳細資訊，請參閱[啟用 HTTPS 的管理點](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a> 案例 2：複製到發佈點
<!--1358228-->
工作群組或已加入 Azure AD 的用戶端，可以從一個為 HTTP 設定的發佈點，透過安全通道來下載內容。   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a> 案例 3 Azure AD 裝置識別 
<!--1358460-->
已加入 Azure AD 或沒有 Azure AD 使用者登入的 [Azure AD 混合式裝置](/azure/active-directory/devices/concept-azure-ad-join-hybrid)，可以安全地與其指派的站台通訊。 現在只要有雲端裝置識別，便能到 CMG 和管理點進行驗證。  


### <a name="prerequisites"></a>先決條件  

- 為 HTTP 用戶端連線設定的管理點。 請到站台系統角色屬性的 [一般]  索引標籤設定此選項。  

- 為 HTTP 用戶端連線設定的發佈點。 請到站台系統角色屬性的 [一般]  索引標籤設定此選項。 不要啟用此選項來**允許用戶端以匿名方式連線**。  

- 雲端管理閘道。  

- 將站台與 Azure AD 搭配以進行雲端管理。  

    - 如果您的站台已符合此項必要條件，則您需要更新 Azure AD 應用程式。 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure Active Directory 租用戶]  。 選取 Azure AD 租用戶，接著選取 [應用程式]  窗格中的 web 應用程式，然後再按一下功能區中的 [更新應用程式設定]  。  

- 執行 Windows 10 版本 1803 而且已加入 Azure AD 的用戶端。 (嚴格來說，此需求僅適用於[案例 3](#bkmk_token3))。 


### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  。 選取站台，然後按一下功能區中的 [內容]  。  

2. 切換至 [用戶端電腦通訊]  索引標籤。選取 **HTTPS 或 HTTP** 的選項，然後啟用新選項來**讓 HTTP 網站系統使用 Configuration Manager 產生的憑證**。  

請參閱前文的[案例清單](#bkmk_token)，逐一驗證。

> [!Tip]
> 在此版本中，等候 30 分鐘的時間，讓管理點接收和設定站台的新憑證。

您可以在 Configuration Manager 主控台中查看這些憑證。 移至 [系統管理]  工作空間，展開 [安全性]  ，然後選取 [憑證]  節點。 尋找 **SMS 發行**根憑證，以及 SMS 發行根簽發的站台伺服器角色憑證。


### <a name="known-issues"></a>已知問題
- 使用者無法在軟體中心檢視任何以他們為使用對象的應用程式。  

- 作業系統部署案例仍然需要網路存取帳戶。  

- 快速且重複地啟用和停用此選項來**讓 HTTP 網站系統使用 Configuration Manager 產生的憑證**，可能會導致憑證無法正確地繫結至站台系統角色。 沒有「SMS 發行」憑證所簽發的憑證繫結至 Windows Server Internet Information Services (IIS) 中的網站。 若要解決此問題，請從 Windows 的 **SMS** 憑證存放區刪除「SMS 發行」簽發的所有憑證，然後再重新啟動 smsexec 服務。



## <a name="improvements-for-enabling-third-party-software-update-support"></a>各種能啟用協力廠商軟體更新支援的增強功能
<!--1357605-->
針對您在 [協力廠商軟體更新支援](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)上提出 UserVoice 意見，此版本會進一步反覆運用 System Center Updates Publisher (SCUP) 的整合功能。 Configuration Manager Technical Preview [版本 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) 新增一項功能，該功能可以從 WSUS 讀取憑證來取得協力廠商更新，然後將該憑證部署至用戶端。 但您仍需要使用 SCUP 工具來建立及管理憑證，以便簽署協力廠商軟體更新。

在此版本中，您可以啟用 Configuration Manager 站台來自動設定憑證。 站台會與 WSUS 通訊，以產生一個用於此用途的憑證。 Configuration Manager 接著會繼續將該憑證部署至用戶端。 這個反覆項目不需要使用 SCUP 工具來建立及管理憑證。 

如需深入了解 SCUP 工具的一般用途，請參閱 [Systems Center Updates Publisher](../../sum/tools/updates-publisher.md)。

### <a name="prerequisites"></a>先決條件
- 啟用並部署用戶端設定 [軟體更新]  群組中的 **[啟用協力廠商軟體更新]** 用戶端設定。
- 如果 WSUS 不是與軟體更新點位於同一個伺服器上，您必須在遠端 WSUS 伺服器上執行以下其中一個選項：
    - 啟用 Windows中的遠端登錄服務  
    或
    - 在登錄機碼 `HKLM\Software\Microsoft\Update Services\Server\Setup` 中，建立名為 **EnableSelfSignedCertificates** 的新 DWORD，而且它有一個值為 `1`。 

### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  。 選取最上層站台，請按一下功能區中的 [設定站台元件]  ，然後選取 [軟體更新點]  。  

2. 切換至 [協力廠商更新]  索引標籤。選取此選項來**啟用協力廠商軟體更新**，然後選取 **Configuration Manager 會自動管理憑證**的選項。

3. 繼續進行一般 SCUP 工作流程的其餘部分來匯入協力廠商軟體更新類別目錄，然後將更新部署至用戶端。



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Windows 10 就地升級工作順序的改善
<!--1358500-->

Windows 10 就地升級的預設工作順序範本，現在包含其他群組並附帶新增的建議動作，以防萬一升級程序失敗。 有了這些動作，解決問題就簡單多了。

### <a name="new-groups-under-run-actions-on-failure"></a>**失敗時執行的動作**底下的新群組
- **收集記錄檔**：若要從用戶端收集記錄檔，請將步驟加入此群組中。 
    - 常見的作法是將記錄檔複製到網路共享位置。 若要建立此連線，請使用[連線到網路資料夾](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步驟。 
    - 若要執行複製作業，請使用自訂的指令碼或公用程式並配合[執行命令列](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)或[執行 PowerShell 指令碼](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)步驟。
    - 要收集的檔案可能包含下列記錄檔：  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - 如需有關 setupact.log 和其他 Windows 安裝程式記錄檔的詳細資訊，請參閱 [Windows 安裝程式記錄檔](/windows/deployment/upgrade/log-files)。
    - 如需有關 Configuration Manager 用戶端記錄檔的詳細資訊，請參閱 [Configuration Manager 用戶端記錄檔](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)
    - 如需有關 _SMSTSLogPath 和其他實用的變數，請參閱[工作順序內建變數](../../osd/understand/task-sequence-variables.md)。

- **執行診斷工具**：若要執行其他診斷工具，請將步驟加入此群組中。 在失敗之後，這些工具應該儘早自動從系統收集其他資訊。
    - Windows [SetupDiag](/windows/deployment/upgrade/setupdiag) 就是這種工具之一。 它是獨立的診斷工具，您可用來取得有關 Windows 10 升級為何失敗的具體原因。
         - 在 Configuration Manager 中，為工具[建立套件](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)。
         - 將[執行命令列](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟新增至此工作順序群組。 使用 [套件]  選項來參考此工具。 下列字串是一個**範例命令列**範例：  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>與用戶端一起安裝的 CMTrace
<!--1357971-->

CMTrace 檢視工具現在會與 Configuration Manager 用戶端一起自動安裝。 它會被新增至用戶端安裝目錄，根據預設，就是 `%WinDir%\ccm\cmtrace.exe`。

> [!Note]  
> CMTrace *不會*自動註冊到 Windows 中來開啟.log 副檔名。



## <a name="improvement-to-the-configuration-manager-console"></a>Configuration Manager 主控台的改善
<!--1358202-->
我們已經針對 Configuration Manager 主控台做了以下的改善：

- 根據預設，[資產與合規性]、[裝置] 底下列出的裝置，現在會顯示目前登入的使用者。 這個值是[用戶端狀態](../clients/manage/monitor-clients.md#bkmk_indStatus)目前的值。 當使用者登出時，會清除這個值。 如果沒有使用者登入，則值會是空白。 

### <a name="known-issues"></a>已知問題
在 [裝置] 節點或者檢視 [裝置集合] 節點底下的裝置清單時，目前登入的使用者值為空白。 若要解決此問題，請下載這 [SQL 指令碼](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c)。 在站台資料庫伺服器上，執行 sp_BgbUpdateLiveData.sql，然後重新啟動管理點上的 smsexec 和 sms_notification_server 服務。<!--514471-->



## <a name="improvements-to-console-feedback"></a>針對主控台意見反應所做的改進
<!--1357542-->
此版本包含針對 Configuration Manager 主控台的新[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)機制所做的改進：  

- 意見反應對話方塊現在會記住先前的設定，例如選取的選項和電子郵件地址。  

- 它現在支援離線的意見反應。 從主控台儲存您的意見反應，然後從連線至網際網路的系統上傳到 Microsoft。 使用新的離線意見反應上載程式工具，網址是 `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`。 若要查看可用及必要的命令列選項，執行該工具並搭配 `--help` 選項。 連接的系統必須能夠存取 **petrol.office.microsoft.com**。

### <a name="known-issues"></a>已知問題
當在具備網際網路連線之電腦上的主控台使用 [傳送笑臉]  或 [傳送苦臉]  時，可能會傳回下列訊息：[傳送意見反應時發生錯誤。] 如果您按一下 [詳細資訊]  ，它會顯示下列文字：`{"Message":""}`。 這個錯誤是因為來自後端意見反應系統之回應的已知問題。 您可以關閉錯誤。 Microsoft 仍會收到您的意見反應。 (如果詳細資料顯示不同的訊息，請使用 [離線意見反應] 選項，稍後重新傳送您的意見反應)。



## <a name="improvements-to-pxe-enabled-distribution-points"></a>支援 PXE 的發佈點改善
<!--1357580-->

當您在發佈點上使用此選項來[**啟用 PXE 回應者而不使用 Windows Deployment Service**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) 時，此版本包含以下的其他改進：  

- 當您啟用此選項時，會自動在發佈點上建立 Windows 防火牆規則  
- 元件記錄的改進



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>大整數值的硬體清查改進
<!--1357880-->
硬體清查目前對於大於 4,294,967,296 (2^32) 的整數有一個限制。 硬碟大小 (位元組) 此類的屬性，可能會達到此限制。 管理點無法處理超過此限的整數值，因此沒有值儲存在資料庫中。 在此版本中，現在的限制已增加至 18,446,744,073,709,551,616 (2^64)。 

如果屬性帶有一個不會變更的值，例如磁碟大小總計，在升級站台之後，您可能無法立即看到該值。 大部分的硬體清查是一種差異報表。 用戶端只會傳送能變更的值。 若要解決此問題，請加入另一個屬性至相同的類別。 這個動作會導致用戶端將類別中所有已變更的屬性，予以更新。 



## <a name="improvement-to-wsus-maintenance"></a>WSUS 維護的改進
<!--1357898-->

WSUS 清理精靈現在會根據取代規則，拒絕那些已過期或被取代的更新。 這些規則是定義在軟體更新點元件內容中。

### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  。 選取最上層站台，請按一下功能區中的 [設定站台元件]  ，然後選取 [軟體更新點]  。  

2. 切換至 [取代規則]  索引標籤。啟用此選項來**執行 WSUS 清理精靈**。 指定所要的取代的行為。  

3. 檢閱 WSyncMgr.log 檔案。



## <a name="improvement-to-support-for-cng-certificates"></a>CNG 憑證支援的改進
<!--1357314-->
在這個版本中，針對以下啟用 HTTPS 的伺服器角色，使用 [CNG 憑證](../plan-design/network/cng-certificates-overview.md)：  
- 憑證登錄點，包括自帶 Configuration Manager 原則模組的 NDES 伺服器



## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
