---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1804 版中可用的新功能。
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b709d6ec0c0cda188502c314d945a70e8de71288
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905243"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Configuration Manager Technical Preview 1804 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Technical Preview for Configuration Manager 1804 中可用的功能。 您可以安裝此版本，以將新功能更新並新增至您的技術預覽版網站。 

請先檢閱[技術預覽版](technical-preview.md)文章，再安裝此更新。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 的已知問題

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a> 下載更新的安裝程式連結無法運作
<!--514334-->
如果您從媒體執行安裝程式，則初始頁面會包含標題為**取得最新的 Configuration Manager 更新**的連結，該連結在此版本中無法運作。 此連結用於下載安裝所需的檔案。

#### <a name="workaround"></a>因應措施
若要下載安裝所需的檔案，請執行安裝精靈。 在 [必要條件下載] 頁面上，使用 [下載必要檔案]  選項。 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a> 應用程式類別目錄 Web 服務點不能為已啟用 HTTPS
<!--512637-->
如果應用程式類別目錄 Web 服務點已啟用 HTTPS：

- 部署為供使用者使用的應用程式不會顯示在軟體中心  

- 下列錯誤會顯示在 awebsctl.log 中：  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>因應措施
重新設定應用程式類別目錄 Web 服務點，以使用 HTTP 連線進行通訊。  




</br>

**以下是您可以使用此版本試用的新功能。**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>針對站台伺服器設定遠端內容庫  
<!--1357525-->
若要釋放主要站台伺服器的硬碟空間，請將它的[內容庫](../plan-design/hierarchy/the-content-library.md)重新移至另一個儲存位置。 您可以將內容庫移至站台伺服器上的另一個磁碟機、個別的伺服器，或是存放區域網路 (SAN) 上的容錯磁碟。 我們建議使用 SAN，因為它能提供彈性的存放空間，可隨內容需求的變化而放大或壓縮。 

此遠端內容庫已是[站台伺服器角色高可用性](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)的新必要條件。 

> [!Note]  
> 此動作只會移動站台伺服器上的內容庫。 它不會影響內容庫在發佈點上的位置。 

### <a name="prerequisites"></a>先決條件  
- 針對您要移動內容庫的目標網路路徑，站台伺服器電腦帳戶需要擁有路徑的**讀取**和**寫入**權限。 遠端系統上不會安裝任何元件。 

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，切換至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  。 在詳細資料窗格底部的 [摘要]  索引標籤上，留意到 [內容庫]  會有一個新欄位。  

2. 按一下功能區上的 [管理內容庫]  。  

3. 選取 [在網路共用上]  並輸入有效的網路路徑。 此路徑是站台移動內容庫的目標位置。 按一下 [確定]  。  

4. 請注意到詳細資料窗格上 [內容庫] 欄位中的 [狀態]  屬性。 它會更新以顯示站台移動內容庫的進度。 它在移動期間會顯示完成百分比。 發生錯誤狀態時，它會顯示錯誤。 常見的錯誤包含 `access denied` 或 `disk full`。 完成時，它會顯示 `OK`。 如需詳細資料，請參閱 **distmgr.log**。 如需詳細資訊，請參閱[站台伺服器與站台系統伺服器記錄檔](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog)。  

如果您需要將內容庫移回站台伺服器，請重複此程序，但選取 [本機至站台伺服器]  選項。  

> [!Tip]  
> 若要將內容移至站台伺服器上的另一個磁碟機，請使用**內容庫傳輸**工具。 如需詳細資訊，請參閱 [Configuration Manager 工具組](#configuration-manager-toolkit)。  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a> 從 Configuration Manager 主控台傳送意見反應  
<!--1357542-->

傳送笑臉！ 您現在可以把自己的相關經驗直接告訴 Configuration Manager 小組。 從 Configuration Manager 主控台傳送意見反應很容易。 如果您有任何的讚美、問題或建議，請不吝告知。  

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送**意見反應**，讓我們知道後續結果。  

1. 在 Configuration Manager 主控台中，按一下功能區上方右上角的笑臉按鈕。  

2. 從下拉式清單中，選取其中一個可用選項：  

   - **傳送笑臉**：您很喜歡某個功能。 針對這個選項，請輸入您意見反應的詳細內容。 然後選擇性地附上螢幕擷取畫面和電子郵件地址。  

   - **傳送苦臉**：您在主控台中遇到問題，或某些功能未如預期般運作。 針對這個選項，請輸入潛在產品問題的詳細內容。 然後選擇性地附上螢幕擷取畫面、電子郵件地址及診斷資料。  

   - **傳送建議**：您有變更及改進 Configuration Manager 的想法。 此選項會在您的網頁瀏覽器中開啟我們的 [UserVoice](https://configurationmanager.uservoice.com) \(英文\) 網站。  

這個意見反應會直接傳送給 Microsoft 的 Configuration Manager 產品小組。 雖然我們仍支援使用 Windows 10 意見反應中樞，不過建議您使用主控台內建的意見反應機制。  

作為參考內容，意見反應一律會包含下列匿名資訊：  

- Configuration Manager 主控台版本和語言  

- Configuration Manager 站台版本  

- 支援識別碼，也稱為階層識別碼  

- 執行主控台所在系統的作業系統版本和語言  

- 您在主控台中按一下笑臉的確切位置  

此資料與我們所收集的診斷和使用方式資料為一致。 如需詳細資訊，請參閱[診斷和使用方式資料](../plan-design/diagnostics/diagnostics-and-usage-data.md)。

### <a name="known-issues"></a>已知問題

如果您嘗試從無法存取網際網路的裝置傳送意見反應，應用程式可能會未預期地關閉。 若要傳送笑臉或苦臉，請確定裝置能夠存取 petrol.office.microsoft.com。



## <a name="support-center"></a>支援中心
<!--1357489-->

使用支援中心來進行用戶端疑難排解、即時檢視記錄檔，或擷取 Configuration Manager 用戶端電腦的狀態，以於稍後進行分析。 支援中心為合併眾多系統管理員疑難排解工具的單一工具。 Technical Preview 中會提供支援中心預覽的最新版本，其中包含錯誤修正、增強功能，以及新記錄檔檢視器的預覽。 支援中心的安裝程式位於站台伺服器的 **cd.latest\SMSSETUP\Tools\SupportCenter** 資料夾中。


### <a name="new-support-center-features"></a>支援中心的新功能  

- 新記錄檔檢視器：OneTrace。 其運作方式類似 CMTrace，並包含各種增強功能，例如索引標籤式檢視，以及可停駐視窗。  

- 新的資料收集器功能會從本機或遠端 Configuration Manager 用戶端收集診斷記錄檔。 它能針對下列項目提供即時診斷：庫存 (取代 Client Spy)、原則 (取代 Policy Spy)，以及用戶端快取。  



## <a name="configuration-manager-toolkit"></a>Configuration Manager 工具組
<!--1357145-->

Configuration Manager 伺服器和用戶端工具現已包含在 Technical Preview 中。 它們位於站台伺服器的 **\cd.latest\SMSSETUP\TOOLS** 資料夾中。 不需要採取進一步的安裝。

#### <a name="server-tools"></a>伺服器工具  

- **DP 工作管理員**：對針對發佈點的內容發佈作業進行疑難排解  

- **集合評估檢視器**：檢視集合評估的詳細資料  

- **內容庫總管**：檢視內容庫單一執行個體存放區的內容  

- **內容庫傳輸**：在磁碟機之間傳送內容庫  

- **內容擁有權工具**：變更孤立套件的擁有權。 這些套件存在於站台中，但沒有擁有套件的站台伺服器。  

- **以角色為基礎的系統管理和稽核工具**：協助系統管理員對角色設定進行稽核  

#### <a name="client-tools"></a>用戶端工具

- **CMTrace**：檢視記錄檔  

- **部署監視工具**：對應用程式、更新和基準部署進行疑難排解  

- **原則監視**：檢視原則指派  

- **電源檢視器工具**：檢視電源管理功能的狀態  

- **傳送排程工具**：觸發 DCM 基準的排程和評估  

> [!Important]  
> 建議針對大部分的使用案例使用[支援中心](#support-center)，因為它包含和下列工具相同或改良的功能：  
> - Client Spy
> - CMTrace<sup>1</sup> 
> - 部署監視工具
> - Policy Spy
> - 傳送排程工具
> 
> <sup>1</sup> 由於 CMTrace 不需依賴 .NET 或 Windows Presentation Foundation (WPF)，因此仍用於 Windows PE 開機映像。

### <a name="known-issues"></a>已知問題
啟動時，某些用戶端與伺服器工具可能會意外結束。 此問題是由於媒體上遺漏檔案所致。 若要解決此問題，請將 AdminConsole\bin 目錄中的 **Microsoft.Diagnostics.Tracing.EventSource.dll** 檔案，同時複製到 SMSSETUP\Tools\ClientTools 和 ServerTools 目錄中。 此檔案必須是 Configuration Manager 主控台所使用的相同版本。 其他版本可能無法運作。 <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>在核准撤銷時解除安裝應用程式
<!--1357891-->

您撤銷應用程式核准時的行為已經變更。 現在，當您拒絕應用程式的要求時，用戶端會從使用者的裝置解除安裝該應用程式。 

### <a name="prerequisites"></a>先決條件
- 啟用 [針對每部裝置的使用者核准應用程式要求]  的功能。

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，將需要核准的應用程式部署到使用者。 在 [部署設定]  索引標籤上，啟用 [系統管理員必須在裝置上核准此應用程式的要求]  選項。  

2. 在軟體中心的 Configuration Manager 用戶端上，使用者會要求核准安裝應用程式。  

3. 在 Configuration Manager 主控台中核准該要求，讓使用者可在裝置上安裝該應用程式。 應用程式核准要求會顯示在 [核准要求]  節點中 [應用程式管理]  底下的 [軟體程式庫]  工作區中。  

4. 在軟體中心的用戶端上，該使用者會安裝該應用程式。  

5. 在 Configuration Manager 主控台中，拒絕使用者在裝置上安裝應用程式的要求。  

### <a name="known-issues"></a>已知問題
- 在使用者於用戶端上安裝應用程式之後，更新使用者原則。 在軟體中心中，切換至 [選項]  索引標籤，然後展開 [電腦維護]  ，並按一下 [同步處理原則]  。<!--480609-->  

- 應用程式類別目錄 Web 服務點必須為 HTTP。 如需詳細資訊，請參閱[此 Technical Preview 的已知問題](#bkmk_appcathttps)。<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>從探索排除 Active Directory 容器
<!--1358143-->
若要減少探索到的物件數目，您現在可以從 Active Directory 系統探索排除特定容器。 這項功能是源自使用者的 [UserVoice 意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery) \(英文\)。

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [階層設定]  ，然後選取 [探索方法]  。 選取 [Active Directory 系統探索]  ，然後按一下功能區中的 [內容]  。  

2. 選擇 [新增] 圖示來指定新的 Active Directory 容器。   

3. 在 [Active Directory 容器] 對話方塊中，在 [位置] 區段中瀏覽至或輸入 [路徑]  來開始探索。  

4. 在 [搜尋選項] 區段中，啟用 [以遞迴方式搜尋 Active Directory 子容器]  選項。 然後按一下 [新增]  來選取要從這個探索中排除的子容器。  

5. 在 [選取新的容器] 對話方塊中，選取要排除的子容器。 按一下 [確定]  來關閉 [選取新容器] 對話方塊。  

6. 按一下 [確定]  來關閉 [Active Directory 容器] 對話方塊。  

7. 在 [Active Directory 系統探索內容] 視窗中，查看系統會開始探索的 Active Directory 容器路徑。 [遞迴]  欄位會顯示 [是]  ，而新的 [有排除項目]  欄位也會顯示 [是]  。 按一下 [確定]  來關閉 [Active Directory 系統探索內容] 視窗。  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>在軟體中心中指定應用程式類別目錄網站連結的可見性
<!--1358214-->

您現在可以控制是否要將 [開啟應用程式類別目錄網站]  的連結顯示在軟體中心的 [安裝狀態]  節點上。  

> [!Note]  
> 對「應用程式類別目錄」網站使用者體驗的支援將在 2018 年 6 月 1 日後第一個更新發行之後結束。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。  

### <a name="try-it-out"></a>試試看！
 請嘗試完成工作。 然後傳送[意見反應](#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台之 [系統管理]  工作區的 [用戶端設定]  節點中，建立自訂的用戶端裝置設定原則。  

2. 選取 [軟體中心]  群組。  

3. 針對 [軟體中心設定]  ，按一下 [自訂]  。  

4. 啟用 [在軟體中心中隱藏應用程式類別目錄網站連結]  的選項。   

如需用戶端設定的詳細資訊，請參閱[設定用戶端設定](../clients/deploy/configure-client-settings.md)。




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>依軟體更新架構篩選自動部署規則
 <!--1322266-->
您現在可以篩選自動部署規則來排除架構 (例如 Itanium 和 ARM64)。

### <a name="try-it-out"></a>試試看！
請嘗試完成工作。 然後傳送[意見反應](#bkmk_feedback)，讓我們知道後續結果。

1. 在 Configuration Manager 主控台中，切換至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [自動部署規則]  。 在功能區上，選取 [建立自動部署規則]  。  

2. 針對 [一般]  索引標籤和 [部署設定]  索引標籤填入適當的設定。  

3. 在 [軟體更新]  索引標籤上，選取 [架構]  ，然後按一下 [搜尋條件]  中的 [要尋找的項目]  。  

4. 選取您想要包含在自動部署規則中的架構。  

5. 按一下 [下一步]  ，然後繼續建立自動部署規則。  

> [!IMPORTANT]  
> 請記住，64 位元 (x64) 系統上有執行 32 位元 (x86) 應用程式和元件。 除非您確定已不再需要 x86，否則請在選擇 [x64] 時一起啟用 [x86]。  

### <a name="known-issues"></a>已知問題
新增架構條件後，自動部署規則內容頁面會在搜尋條件中顯示 [標題]  。 自動部署規則仍會如預期般作用，並選取正確的軟體更新。 不過，目前您並無法同時包含 [架構]  和 [標題]  這兩個條件。 <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>改善 OS 部署
我們已對 OS 部署做出下列改善，有一些是根據 UserVoice 意見反應的結果。  

- [遮罩儲存在工作順序變數中的敏感性資料](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed) \(英文\)：在[設定工作順序變數](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步驟中，選取 [不要顯示此值]  的新選項。 例如，指定密碼時。<!--1358330--> 啟用此選項時，系統會套用下列行為：
  - 變數的值不會顯示在 smsts.log 中。
  - Configuration Manager 主控台和 SMS 提供者會以和處理其他祕密 (如密碼) 的相同方式處理這個值。
  - 當您匯出工作順序時，不會包含這個值。
  - 當您編輯步驟時，工作順序編輯器不會讀取這個值。 重新輸入完整的值來進行變更。

  > [!Important]  
  > 變數和其值會與工作順序一起儲存為 XML，並在資料庫中被模糊化。 當用戶端從管理點要求工作順序原則時，系統會在其傳輸期間及儲存在用戶端上時予以加密。 然而，在用戶端上的執行階段期間，所有變數值在記憶體中的工作順序環境中都會是純文字。 如果工作順序包含輸出變數值的步驟，這個輸出會是純文字。 這個行為需要系統管理員執行明確動作，以在工作順序中包含這個步驟。 


- [在工作順序的「執行命令」步驟期間遮罩程式名稱](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed) \(英文\)：若要防止顯示或記錄潛在的敏感性資料，請將工作順序變數 **OSDDoNotLogCommand** 設定為 `TRUE`。 這個變數會在[執行命令列](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)工作順序步驟期間，為 smsts.log 中的程式名稱加上遮罩。 <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Configuration Manager 主控台的改善
- 現在，在 [資產與合規性]  中的 [裝置集合]  底下檢視集合成員時，可以看到主要使用者資訊。<!--510252-->  



## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
