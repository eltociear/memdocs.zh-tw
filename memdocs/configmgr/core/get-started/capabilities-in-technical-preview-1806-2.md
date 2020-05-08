---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1806.2 版中可用的新功能。
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b7643c73d2e9dad00e926bdc3db905016c45860a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905209"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Configuration Manager Technical Preview 1806.2 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1806.2 版中可用的功能。 您可以安裝此版本，以將新功能更新並新增至您的技術預覽版網站。 

請先檢閱[技術預覽版](technical-preview.md)文章，再安裝此更新。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 的已知問題

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a> 用戶端不會自動更新
<!--518760-->
更新為 1806.2 版時，站台也會更新 SQL Native Client，這樣可能會在站台伺服器上導致擱置重新啟動。 此延遲會導致特定檔案無法更新，這會影響用戶端自動升級。

#### <a name="workarounds"></a>因應措施
將 Configuration Manager 更新到 1806.2 版「之前」  ，先手動升級 SQL Native Client，以避免這個問題。 如需詳細資訊，請參閱[適用於 SQL Server 2012 Native Client 的最新服務更新](https://www.microsoft.com/download/details.aspx?id=50402)。

如果您已經更新站台，自動用戶端升級和用戶端推入將無法運作。 您需要更新用戶端，才能完整測試最新功能。 使用下列程序，以手動方式更新您的技術預覽用戶端：  

1. 在站台伺服器上 Configuration Manager 安裝目錄的 **CMUClient** 資料夾中找出用戶端來源檔案。 例如， `C:\Program Files\Configuration Manager\CMUClient`  

2. 將整個 CMUClient 資料夾複製到用戶端裝置。 例如， `C:\Temp\CMUClient`  

    此位置可以是可從用戶端存取的網路共用。  

3. 從已提升權限的命令提示字元執行下列命令列：`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

如果您在 Technical Preview 1806.2 版的站台上安裝新用戶端，請使用這個相同程序。 

> [!Important]  
> 請勿在此案例中使用 `/MP` 命令列參數。 此參數的優先順序高於 `/source`，並會導致 ccmsetup 從管理點或發佈點下載用戶端內容。
> 
> 可以使用命令列屬性 (例如 SMSSITECODE 或 CCMLOGLEVEL)，但在升級現有用戶端時並非必要。 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a> 版本 1806.2 在 [關於 Configuration Manager] 中顯示為版本 1806
<!--518148-->
升級為 Technical Preview 1806.2 版之後，如果從主控台左上角開啟 [關於 Configuration Manager]  視窗，它仍會顯示 [版本 1806]  。 

#### <a name="workaround"></a>因應措施
使用 [站台版本]  內容來判斷 1806 和 1806.2 之間的差異：

| 站台版本  | 版本
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**以下是您可以使用此版本試用的新功能。**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a> 階段式部署的改善

此版本包含下列[階段式部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)的改善：
- [階段式部署狀態](#bkmk_pod-monitor)
- [應用程式的階段式部署](#bkmk_pod-app)
- [在階段式部署期間逐步推出](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a> 階段式部署狀態
<!--1358577-->
階段式部署現在具有原生的監視體驗。 從 [監視]  工作區中的 [部署]  節點，選取階段式部署，然後按一下功能區中的 [階段式部署狀態]  。

![顯示兩個階段狀態的階段式部署狀態儀表板](media/1358577-phased-deployment-status.png)

此儀表板會針對部署中的每個階段顯示下列資訊：  

- **裝置數總計**：有多少個由此階段設為目標的裝置。  

- **狀態**：此階段的目前狀態。 每個階段均可處於下列其中一種狀態：  

    - **已建立部署**：階段式部署會針對此階段的集合，建立軟體部署。 會主動將用戶端設為此軟體的目標。  

    - **等待中**：上一個階段尚未達到繼續進行此階段部署的成功準則。  

    - **已暫停**：系統管理員已暫停部署。  

- **進度**：來自用戶端且以色彩標示的部署狀態。 例如：成功、進行中、錯誤、不符合需求及未知。 


#### <a name="known-issue"></a>已知問題
階段式部署狀態儀表板可能會針對相同階段顯示多列。<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a> 應用程式的階段式部署
<!--1358147-->
建立應用程式的階段式部署。 階段式部署可讓您根據可自訂的準則與群組，以組織協調且循序的軟體推出。

在 Configuration Manager 主控台中，移至 [軟體程式庫]  、展開 [應用程式管理]  ，然後選取 [應用程式]  。 選取應用程式，然後按一下功能區中的 [建立階段式部署]  。 

應用程式階段式部署的行為與工作順序的行為相同。 如需詳細資訊，請參閱[建立工作順序的階段式部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)。

#### <a name="prerequisite"></a>必要條件
建立階段式部署之前，先將應用程式的內容發佈至發佈點。<!--518293-->

#### <a name="known-issue"></a>已知問題
您無法手動建立應用程式的階段。 精靈會自動建立兩個階段以供應用程式部署使用。


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a> 在階段式部署期間逐步推出
<!--1358578-->
在階段式部署期間，現在可在每個階段中逐步推出。 此行為有助於減緩部署問題的風險，並降低因將內容發佈到用戶端而導致的網路負載。 依據每個階段的設定而定，站台可以逐步開放軟體以供使用。 階段中的每個用戶端都有一個相對於軟體可供使用時間的期限。 可用時間與期限之間的時間範圍，對於階段中的所有用戶端而言都一樣。 

當您建立階段式部署並手動設定階段時，請在 [新增階段精靈] 的 [階段設定]  頁面上，或在 [建立階段式部署精靈] 的 [設定]  頁面上，設定此選項：**讓此軟體在這段期間逐漸可供使用 (天)** 。 此設定的預設值為 **0**，因此，預設不會對部署進行節流處理。

> [!Note]  
> 此選項目前只適用於工作順序的階段式部署。  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a> 支援新的 Windows 應用程式套件格式
<!--1357427-->
Configuration Manager 現在支援部署新的 Windows 10 應用程式套件 (.msix) 與應用程式套件組合 (.msixbundle) 格式。 最新的 [Windows Insider Preview](https://insider.windows.com/) 組建目前支援這些新格式。

如需 MSIX 的概觀，請參閱[深入了解 MSIX](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix) \(英文\)。

如需如何建立新的 MSIX 應用程式，請參閱 [Insider 組建 17682 中引進的 MSIX 支援](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) \(英文\)。

### <a name="prerequisites"></a>先決條件
- 至少執行 Windows Insider Preview 組建 17682 的 Windows 10 用戶端
- MSIX 格式的 Windows 應用程式套件

### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中[建立應用程式](../../apps/deploy-use/create-applications.md)。 
2. 針對應用程式安裝檔案的**類型**選取 [Windows 應用程式套件 (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)]  。
3. [部署應用程式](../../apps/deploy-use/deploy-applications.md)到執行最新 Windows Insider Preview 組建的用戶端。



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a> 用戶端推入安全性的改善
<!--1358204-->
使用安裝 Configuration Manager 用戶端的[用戶端推入](../clients/deploy/plan/client-installation-methods.md#client-push-installation)方法時，站台伺服器會建立與用戶端的遠端連線以開始安裝。 從這個版本開始，站台可以藉由在建立連線之前不允許回復為 NTLM 來要求 Kerberos 相互驗證。 此增強功能有助於保護伺服器和用戶端之間的通訊。 

根據安全性原則而定，您的環境可能已經偏好使用或需要 Kerberos，而不是較舊 NTLM 驗證。 如需這些驗證通訊協定的安全性考量詳細資訊，請參閱[用來限制 NTLM 的 Windows 安全性原則設定](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations) \(英文\)。


### <a name="prerequisite"></a>必要條件

若要使用此功能，用戶端必須位於信任的 Active Directory 樹系中。 Windows 中的 Kerberos 依賴 Active Directory 進行相互驗證。 


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

當您升級站台時，會保存現有的行為。 一旦您「開啟」  用戶端推入安裝內容之後，站台即會自動啟用 Kerberos 檢查。 如有必要，您可以允許連線回復為使用較不安全的 NTLM 連線，但不建議這樣做。 

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  。 選取目標站台。 在功能區中，按一下 [用戶端安裝設定]  ，然後選取 [用戶端推入安裝]  。  

2. 站台現在已針對用戶端推入啟用 Kerberos 檢查。 按一下 [確定]  以關閉視窗。  

3. 若您的環境有需要，請在 [用戶端推入安裝內容] 視窗的 [一般]  索引標籤上，查看 [允許連線回復為NTLM]  的選項。 預設會停用這個選項。 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a> 主動式維護的管理見解
<!--1352184,et al-->
此版本中提供額外的管理見解以突顯潛在設定問題。 在新的 [主動式維護]  群組中檢閱下列規則：  

- **未使用的設定項目**：不是設定基準一部分且已過時逾 30 天的設定項目。  

- **未使用的開機映像**：未用於供 PXE 開機或工作順序參考的開機映像。  

- **未獲指派站台系統的界限群組**：界限群組若無指派的站台系統，則僅適用於站台指派。  

- **不含成員的界限群組**：如果界限群組沒有任何成員，則不適用站台指派或內容查閱。  

- **未提供內容給用戶端的發佈點**：在過去 30 天未提供內容給用戶端的發佈點。 此資料會以來自用戶端下載歷程記錄的報告為基礎。  

- **找到過期的更新**：過期的更新不適用於部署。   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a> 轉換共同管理裝置的行動應用程式工作負載
<!--1357892-->
使用 Microsoft Intune 管理行動應用程式，同時繼續使用 Configuration Manager 部署 Windows 傳統型應用程式。 若要轉換新式應用程式工作負載，請移至共同管理內容頁面。 將滑桿從 Configuration Manager 移至 [試驗] 或 [全部]。 

轉換此工作負載之後，從 Intune 部署的所有可用應用程式均可在公司入口網站中使用。 您從 Configuration Manager 部署的應用程式可在軟體中心使用。 

如需詳細資訊，請參閱下列文章：  

- [Windows 10 裝置的共同管理](../../comanage/overview.md)  

- [什麼是 Microsoft Intune 應用程式管理？](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a> 適用於對等下載的界限群組選項
<!--1356193-->
界限群組現在包含其他設定，使您更能掌握環境中的內容發佈。 此版本新增下列選項：  

- **允許此界限群組中的對等下載**：預設會啟用此設定。 管理點會為用戶端提供內容位置清單，其中包含對等來源。 <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    您應該考慮停用此選項的常見案例有兩種：  

    - 如果您的界限群組包含來自地理位置分散位置的界限，例如 VPN。 兩個用戶端可能位於相同的界限群組，因為它們可透過 VPN 來連線，但位於完全不同的位置，不適用於內容的對等共用。  

    - 如果您使用單一的大型界限群組進行站台指派，但未參考任何發佈點。  

- **對等下載期間，僅使用相同子網路中的對等**：此設定取決於上方的設定。 如果您啟用此選項，管理點只會包含於內容位置清單對等來源中，而這些來源位於與用戶端相同的子網路。

    啟用此選項的常見案例：

    - 針對內容發佈所設計的界限群組包括一個大型界限群組，此群組會重疊其他較小的界限群組。 使用這個新設定時，管理點提供給用戶端的內容來源清單只包括來自相同子網路的對等來源。

    - 您擁有適用於所有遠端辦公室位置的單一大型界限群組。 啟用此選項時，用戶端只會在遠端辦公室位置上的子網路內共用內容，而不需承擔在位置之間共用內容的風險。


### <a name="known-issue"></a>已知問題
如果對等來源用戶端具有多個 IP 位址 (IPv4、IPv6 或兩者)，則對等快取無法運作。 如果對等來源具有多個 IP 位址，則新選項 [對等下載期間，僅使用相同子網路中的對等]  不會有任何作用。<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a> 協力廠商軟體更新支援自訂類別目錄
<!--1358714-->
針對您提出的 [UserVoice 意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)，此版本會進一步反覆支援協力廠商軟軟體更新。 [Technical Preview 1806 版](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)已提供對「夥伴類別目錄」  的支援，其為軟體廠商已註冊的類別目錄。 您提供且未向 Microsoft 註冊的類別目錄稱為「使用者類別目錄」  。 在 Configuration Manager 主控台中新增自訂類別目錄。  


### <a name="prerequisites"></a>先決條件 

- 設定[協力廠商軟體更新](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)。 完成階段 1：啟用和設定功能。   

- 數位簽署的自訂類別目錄，其中包含數位簽署的軟體更新。  

- 系統管理員需要下列權限：  

    - 站台：建立、修改  


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 然後傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區、展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。 按一下功能區中的 [新增自訂類別目錄]  。  

2. 在 [一般]  頁面上，指定下列詳細資料：  

    - **下載 URL**：自訂類別目錄的有效 HTTPS 位址。  

    - **發行者**：發行類別目錄的組織名稱。  

    - **名稱**：要在 Configuration Manager 主控台中顯示的類別目錄名稱。  

    - **描述**：類別目錄的描述。  

    - **支援 URL** (選擇性)：網站的有效 HTTPS 位址，可取得類別目錄的協助。  

    - **支援連絡人** (選擇性)：取得類別目錄協助的連絡資訊。  

3. 完成精靈。 精靈會以取消訂閱的狀態加入新的類別目錄。  

4. 使用現有的 [訂閱類別目錄]  動作來訂閱自訂的類別目錄。 如需詳細資訊，請參閱 [階段 2：訂閱協力廠商類別目錄和同步更新](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates)。  

> [!Note]  
> 您無法使用相同的下載 URL 加入類別目錄，而且無法編輯類別目錄內容。 如果您為自訂類別目錄指定不正確的內容，請先刪除該類別目錄，然後才能再次加入它。  


#### <a name="unsubscribe-from-a-catalog"></a>取消訂閱類別目錄
若要取消訂類別目錄，請在清單中選取所需的類別目錄，然後按一下功能區中的 [取消訂閱類別目錄]  。 如果您取消訂閱類別目錄，就發生下列動作和行為： 
- 站台會停止同步處理新的更新 
- 站台會封鎖用於類別目錄簽署和更新內容的相關聯憑證。 
- 不會移除現有的更新，但您可能無法發行或部署這些現有的更新。

#### <a name="delete-a-custom-catalog"></a>刪除自訂類別目錄
從主控台的同一個節點刪除自訂類別目錄。 選取處於「取消訂閱」  狀態的自訂類別目錄，然後按一下 [刪除自訂類別目錄]  。 若您已經訂閱類別目錄，請先取消訂閱，然後再加以刪除。 您無法刪除夥伴類別目錄。 刪除自訂類別目錄會從類別目錄清單中移除它。 此動作不會影響您已發行到軟體更新點的任何軟體更新。


### <a name="known-issue"></a>已知問題
自訂類別目錄中的刪除動作會呈現灰色，因此您無法從主控台刪除自訂類別目錄。 若要解決此問題，請使用站台伺服器上的 **wbemtest** 工具。 使用名稱或下載 URL 來查詢您想要刪除的執行個體，例如：`select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`。 在查詢結果視窗中，選取該物件，然後按一下 [刪除]  。<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a> 雲端管理功能的改善

此版本包含下列改善：  

- 下列功能現在支援使用 Azure 美國政府雲端：<!--511980-->  

    - 透過 [Azure 服務](../servers/deploy/configure/azure-services-wizard.md)來使**雲端管理**的站台上線  

    - 使用 Azure Resource Manager 來部署[雲端管理閘道](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - 使用 Azure Resource Manager 來部署[雲端發佈點](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- 客戶使用 Windows AutoPilot，在連線到內部部署網路且已加入 Azure Active Directory 的裝置上佈建 Windows 10。 若要安裝或升級這些裝置上的 Configuration Manager 用戶端，您現在不需要設定為**允許用戶端以匿名方式連線**的雲端發佈點或內部部署發佈點。 而是改為啟用站台選項來**為 HTTP 站台系統使用 Configuration Manager 產生的憑證**，讓已加入雲端網域的用戶端可與已啟用 HTTP 的內部部署發佈點進行通訊。 如需詳細資訊，請參閱[改善的安全用戶端通訊](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications)。<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a> 新的軟體更新合規性報告
<!--1357775-->
檢視軟體更新合規性的報告所包含的資料通常包含來自最近尚未連絡站台的用戶端。 新的報告可讓您依「狀況良好」的用戶端，針對特定的軟體更新群組來篩選合規性結果。 此報告會針對您環境內的有效用戶端顯示更真實的合規性狀態。 
 
若要檢視此報告，請前往 [監視]  工作區、依序展開 [報告]  、 [報告]  、[軟體更新 - A 合規性]  ，然後選取 [合規性 9 - 整體健全狀況和合規性]  。 指定**更新群組**、**集合名稱**和**用戶端健全狀況**狀態。

此報告包含下列部分：
- **狀況良好的用戶端與用戶端總計**：這個橫條圖會比較已在指定期間與站台通訊的「狀況良好」用戶端，以及指定集合中的用戶端總數。
- **合規性概觀**：這個圓形圖顯示在指定的集合內，有效用戶端上特定軟體更新群組的整體合規性狀態。
- **依發行項識別碼顯示前 5 個不符合規範的項目**：這個橫條圖會針對指定集合內有效用戶端上不符合規範者，顯示指定群組中的前五名軟體更新。
- 報告底部有一個含進一步詳細資料的表格，其中列出指定群組中的軟體更新。



## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
