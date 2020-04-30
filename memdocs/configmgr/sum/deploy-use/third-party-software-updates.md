---
title: 啟用協力廠商更新
titleSuffix: Configuration Manager
description: 啟用 Configuration Manager 中的協力廠商更新
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f430979a2189494e977c501a36f9f039f860ca7a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771433"
---
# <a name="enable-third-party-updates"></a>啟用協力廠商更新 

適用於：  Configuration Manager (最新分支)

自 1806 版開始，Configuration Manager 主控台中的 [協力廠商軟體更新類別目錄]  節點可讓您訂閱協力廠商的類別目錄，將其更新發佈到您的軟體更新點 (SUP)，然後將其部署至用戶端。  <!--1357605, 1352101, 1358714-->

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此功能。 使用此功能之前，請先啟用 [啟用用戶端上協力廠商更新的支援]  選擇性功能。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。


## <a name="prerequisites"></a>先決條件 
- 最上層軟體更新點的 WSUSContent 資料夾上有足夠的磁碟空間來儲存協力廠商軟體更新的來源二進位檔案內容。
    - 必要的儲存體數量因廠商、更新類型以及您為部署所發佈的特定更新而異。
    - 如果您需要將 WSUSContent 資料夾移至具有更多可用空間的另一個磁碟機，請參閱 [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/) (如何變更 WSUS 在本機儲存更新的位置) 部落格文章。
- 協力廠商軟體更新同步處理服務需要存取網際網路。
    - 如需合作夥伴類別目錄清單，需要透過 HTTPS 連接埠 443 連線至 download.microsoft.com。 
    -  從網際網路存取任何協力廠商的類別目錄和更新內容檔案。 可能需要 443 以外的其他連接埠。
    - 協力廠商更新使用和 SUP 相同的 Proxy 設定。


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>當 SUP 距離最上層站台伺服器很遠時的其他需求 

1. 當 SUP 不在遠端時，必須啟用 SUP 上的 SSL。 這需要從內部憑證授權單位或透過公用提供者產生伺服器驗證憑證。
    - [Configure SSL on WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) (在 WSUS 上設定 SSL)
        - 當您在 WSUS 上設定 SSL 時，請注意有些 Web 服務和虛擬目錄一律是 HTTP 而非 HTTPS。 
        - Configuration Manager 會透過 HTTP 從您的 WSUS 內容目錄下載軟體更新套件的協力廠商內容。   
    - [在 SUP 上設定 SSL](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. 若在 [軟體更新點元件內容] 中，將協力廠商更新 WSUS 簽署憑證設定設為 **Configuration Manager 管理憑證**，則需要下列設定，才能建立自我簽署的 WSUS 簽署憑證： 
   - 應該在 SUP 伺服器上啟用遠端登錄。
   -  **WSUS 伺服器連線帳戶**應該有 SUP/WSUS 伺服器的遠端登錄權限。 


3. 在 Configuration Manager 站台伺服器上建立下列登錄機碼： 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`，會建立名為 **EnableSelfSignedCertificates** 的新 DWORD，其值為 `1`。 

4. 若要將自我簽署的 WSUS 簽署憑證安裝到遠端 SUP 伺服器上受信任發行者存放區和受信任根目錄存放區：
   - **WSUS 伺服器連線帳戶**應該有 SUP 伺服器的遠端管理權限。

     如果此項目不可行，請將本機電腦 WSUS 存放區中的憑證匯出至信任的發行者存放區和信任的根目錄存放區。 

> [!NOTE] 
>**WSUS 伺服器連線帳戶**可以藉由檢視 SUP 站台系統角色屬性上的 [Proxy 和帳戶設定]  索引標籤予以識別。 如不指定帳戶，則使用站台伺服器的電腦帳戶。

## <a name="enable-third-party-updates-on-the-sup"></a>在 SUP 上啟用協力廠商更新
如果您啟用此選項，您可在 Configuration Manager 主控台中訂閱協力廠商更新類別目錄。 然後將這些更新發佈至 WSUS，並將其部署至用戶端。 每個階層都應該執行一次下列步驟，以啟用和設定要使用的功能。 如果您曾經更換最上層的 SUP WSUS 伺服器，可能需要重新執行這些步驟。 

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  節點。
2. 選取階層中的頂層站台。 在功能區中，按一下 [設定站台元件]  ，然後選取 [軟體更新點]  。
3. 切換至 [協力廠商更新]  索引標籤。選取 [啟用協力廠商軟體更新]  選項。

    ![協力廠商更新 SUP 屬性的螢幕擷取畫面](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>設定 WSUS 簽署憑證
您需要決定要設定管理員使用自我簽署憑證自動管理協力廠商 WSUS 簽署憑證，還是需要手動設定憑證。 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>自動管理 WSUS 簽署憑證
如果沒有使用 PKI 憑證的需求，您可以選擇自動管理協力廠商更新的簽署憑證。 WSUS 憑證管理的完成是同步處理週期的一部分，且會記錄在 `wsyncmgr.log` 中。 

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  節點。
2. 選取階層中的頂層站台。 在功能區中，按一下 [設定站台元件]  ，然後選取 [軟體更新點]  。
3. 切換至 [協力廠商更新]  索引標籤。選取 [Configuration Manager 管理憑證]  選項。 
4. 類型為 [協力廠商 WSUS 簽署]  的新憑證會在 [管理]  工作區之 [安全性]  底下的 [憑證]  節點中建立。  

### <a name="manually-manage-the-wsus-signing-certificate"></a>手動管理 WSUS 簽署憑證
如果您需要手動設定憑證，例如需要使用 PKI 憑證，您即需要使用 [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) 或其他工具來執行這項操作。  

1. 使用 [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) 設定簽署憑證。
2. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [站台]  節點。
3. 選取階層中的頂層站台。 在功能區中，按一下 [設定站台元件]  ，然後選取 [軟體更新點]  。
4. 切換至 [協力廠商更新]  索引標籤。選取 [手動管理憑證]  選項。


## <a name="enable-third-party-updates-on-the-clients"></a>在用戶端上啟用協力廠商更新
在用戶端的用戶端設定中啟用協力廠商更新。 此設定會設定 Windows Update代理程式原則，以 [Allow signed updates for an intranet Microsoft update service location](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location) (允許內部網路 Microsoft 更新服務位置的已簽署更新)。 此用戶端設定也會將 WSUS 簽署憑證安裝至用戶端上信任的發行者存放區。 憑證管理記錄會顯示在用戶端的 `updatesdeployment.log`。  請為每個想要使用協力廠商更新的自訂用戶端設定執行這些步驟。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)一文。

1. 在 Configuration Manager 主控台中，移至 [管理]  工作區，然後選取 [用戶端設定]  節點。
2. 選取現有的自訂用戶端設定，或建立新的設定。 
3. 選取左側的 [軟體更新]  索引標籤。 如果您沒有此索引標籤，請確定是否啟用 [軟體更新]  方塊。
4. 將 [啟用協力廠商軟體更新]  設為 [是]  。 


## <a name="add-a-custom-catalog"></a>新增自訂的類別目錄
「合作夥伴類別目錄」  是已向 Microsoft 註冊資訊的軟體廠商類別目錄。 使用合作夥伴類別目錄，您不必指定任何其他資訊即可訂閱它們。 您新增的類別目錄稱為「自訂類別目錄」  。 您可以將協力廠商更新廠商的自訂類別目錄新增至 Configuration Manager。 自訂的類別目錄必須使用 https，而且更新必須經過數位簽署。 

1. 移至 [Software Updates Library] \(軟體更新程式庫\)  工作區，展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。 
   
     ![協力廠商更新節點的螢幕擷取畫面](media/third-party-updates-node.PNG)
2. 按一下功能區中的 [新增自訂類別目錄]  。 

     ![協力廠商更新新增自訂的類別目錄](media/third-party-updates-custom-catalog.png)
1. 在 [一般]  頁面上，指定下列項目： 
    - **下載 URL**：自訂類別目錄的有效 HTTPS 位址。
    - **發行者**：發行類別目錄的組織名稱。 
    - **名稱**：要在 Configuration Manager 主控台中顯示的類別目錄名稱。 
    - **描述**：類別目錄的描述。 
    - **支援 URL** (選擇性)：網站的有效 HTTPS 位址，可取得類別目錄的協助。 
    - **支援連絡人** (選擇性)：取得類別目錄協助的連絡資訊。 
2. 按一下 [下一步]  檢閱類別目錄摘要，並繼續完成 [協力廠商軟體更新的自訂類別目錄精靈]  。


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>訂閱協力廠商類別目錄和同步處理更新
當您在 Configuration Manager 主控台中訂閱協力廠商類別目錄時，類別目錄中每項更新的中繼資料都會同步處理到您 SUP 的 WSUS 伺服器。 同步處理中繼資料可讓用戶端判斷是否有任何更新可用。 針對您要訂閱的每個協力廠商類別目錄執行下列步驟：  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。  
2. 選取要訂閱的類別目錄，然後按一下功能區中的 [訂閱類別目錄]  。 
    ![協力廠商更新新增自訂的類別目錄](media/third-party-updates-subscribe.png)
3. 檢閱並核准類別目錄的憑證。  
   > [!NOTE]
   > 
   > 當您訂閱協力廠商軟體更新類別目錄時，您在此精靈中檢閱並核准的憑證就會新增至站台。 此憑證的類型是 [協力廠商軟體更新類別目錄]  。 您可以從 [管理]  工作區之 [安全性]  底下的 [憑證]  節點中管理憑證。  
4. 完成精靈。 初次訂閱之後，應該會在幾分鐘內開始下載類別目錄。 
    - 類別目錄每 7 天會自動同步處理。
    - 按一下功能區中的 [立即同步處理]  強制同步處理。
5. 下載類別目錄之後，產品的中繼資料需要從 WSUS 資料庫同步處理到 Configuration Manager 資料庫。 [手動開始軟體更新同步處理](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization)以同步處理產品資訊。
6. 同步處理產品資訊後，[設定 SUP 同步處理所需的產品](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize)至 Configuration Manager。  
7. [手動開始軟體更新同步處理](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization)，將新產品的更新同步處理至 Configuration Manager。  
8. 同步處理完成時，您可以在 [所有更新]  節點中看到協力廠商更新。 這些更新都會發佈為**僅中繼資料**更新，直到您選擇發佈它們為止。 
     - 具有藍色箭號的圖示代表僅中繼資料軟體更新。 ![僅中繼資料軟體更新圖示](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>發佈與部署協力廠商軟體更新 
一旦協力廠商更新進入 [所有更新]  節點，您就可以選擇應該發佈用於部署的更新。 當您發佈更新時，從廠商下載的二進位檔就會放入最上層 SUP 的 WSUSContent 目錄。 

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [所有軟體更新]  節點。
2. 按一下 [新增準則]  來篩選更新清單。 例如，為 **HP** 新增**廠商**。 檢視 HP 的所有更新。  
3. 選取您組織需要的更新。 按一下 [發佈協力廠商軟體更新內容]  。
    - 此動作會從廠商下載更新二進位檔案，然後將它們儲存在最上層軟體更新點上的 WSUSContent 資料夾中。 
4. [手動開始軟體更新同步處理](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization)，將已發佈的更新狀態從僅中繼資料變更為可部署的更新內容。 
    >[!NOTE]
    >當您發佈協力廠商軟體更新內容時，用來簽署內容的任何憑證都會新增至站台。 這些憑證的類型是 [協力廠商軟體更新內容]  。 您可以從 [管理]  工作區之 [安全性]  底下的 [憑證]  節點中管理這些憑證。  

5. 檢閱 SMS_ISVUPDATES_SYNCAGENT.log 的進度。 記錄檔位於站台系統 Logs 資料夾中最上層的軟體更新點。
6. 使用[部署軟體更新](../deploy-use/deploy-software-updates.md)程序來部署更新。 
7. 在 [部署軟體更新精靈]  的 [下載位置]  頁面中，選取 [從網際網路下載軟體更新]  的預設選項。 在此案例中，內容已經發佈到軟體更新點，該軟體更新點可用來下載部署套件的內容。
8. 在您可以看到合規性結果之前，用戶端需要執行掃描並評估更新。  您可以從用戶端的 Configuration Manager 控制台中執行 [軟體更新掃描週期]  動作，以手動方式觸發此週期。


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a> 從 1910 開始的協力廠商更新改良
<!--4469002-->
針對協力廠商更新目錄的同步處理，您現在擁有更精細的控制能力。 從 Configuration Manager 1910 版開始，您可以個別設定每個目錄的同步處理排程。 在使用包含分類更新的目錄時，您可以將同步處理設為僅包含特定的更新類別，以避免同步處理整個目錄。 使用分類目錄時，如果您確定將會部署類別，則可以將其設定為自動下載並發佈至 WSUS。

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>在新的目錄訂用帳戶中設定目錄的排程

1. 前往 [軟體程式庫]  工作區，展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。
1. 選取要訂閱的類別目錄，然後按一下功能區中的 [訂閱類別目錄]  。
1. 若要覆寫預設同步處理排程，請在 [排程]  頁面上選擇選項：
   - **簡易排程**：選擇 [小時]、[天] 或 [月] 間隔。
   - **自訂排程**：設定複雜的排程。

### <a name="update-the-schedule-per-catalog"></a>更新每個目錄的排程

1. 前往 [軟體程式庫]  工作區，展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。
1. 以滑鼠右鍵按一下類別目錄，然後選取 [內容]  。
1. 在 [排程] 索引標籤上選擇選項： 
   - **簡易排程**：選擇 [小時]、[天] 或 [月] 間隔。
   - **自訂排程**：設定複雜的排程。

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>將訂閱新增至協力廠商 v3 類別目錄

> [!IMPORTANT]
> 此選項僅適用於 v3 協力廠商更新類別目錄，其支援更新的類別。 針對未以新 v3 格式發佈的類別目錄，這些選項會停用。


1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。
1. 選取要訂閱的類別目錄，然後按一下功能區中的 [訂閱類別目錄]  。
1. 於 [選取類別]  頁面選擇您的選項：

   - **同步處理所有更新類別** (預設)
       - 將協力廠商更新類別目錄中的所有更新同步處理至 Configuration Manager 中。
   -  **選取同步處理的類別**
       - 選取要同步處理至 Configuration Manager 中的類別和子項目。

      ![選取要同步處理至 Configuration Manager 中的更新類別](./media/4469002-select-categories-for-sync.png)
1. 選擇您是否要為類別目錄**暫存更新內容**。 當您暫存內容時，會將所選類別中的所有更新自動下載至您的最上層軟體更新點，這代表您在部署前不需要確認它們是否已下載完成。 建議您僅自動暫存可能部署的更新內容，以避免過度使用頻寬以及儲存體需求的問題。

   - **不要暫存內容，僅針對掃描同步處理 (建議)**
     - 不要下載協力廠商類別目錄中更新的任何內容
   - **自動暫存所選類別的內容**
     - 選擇將自動下載內容的更新類別。
     - 所選類別中更新的內容將下載至最上層軟體更新點的 WSUS 內容目錄中。
      ![選取要暫存內容的更新類別](./media/4469002-stage-content.png)
1. 設定目錄同步處理**排程**，然後完成精靈。

 

### <a name="edit-an-existing-subscription"></a>編輯現有的訂用帳戶

> [!IMPORTANT]
> 此選項僅適用於 v3 協力廠商更新類別目錄，其支援更新的類別。 針對未以新 v3 格式發佈的類別目錄，這些選項會停用。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [協力廠商軟體更新類別目錄]  節點。
1. 以滑鼠右鍵按一下類別目錄，然後選取 [內容]  。
1. 於 [選取類別]  索引標籤選擇您的選項。
   - **同步處理所有更新類別** (預設)
       - 將協力廠商更新類別目錄中的所有更新同步處理至 Configuration Manager 中。
   -  **選取同步處理的類別**
       - 選取要同步處理至 Configuration Manager 中的類別和子項目。
1. 針對 [暫存更新內容]  索引標籤選擇您的選項。
   - **不要暫存內容，僅針對掃描同步處理 (建議)**
     - 不要下載協力廠商類別目錄中更新的任何內容
   - **自動暫存所選類別的內容**
     - 選擇將自動下載內容的更新類別。
     - 所選類別中更新的內容將下載至最上層軟體更新點的 WSUS 內容目錄中。 

## <a name="monitoring-progress-of-third-party-software-updates"></a>監視協力廠商軟體更新的進度 

協力廠商軟體更新的同步處理是由最上層預設軟體更新點的 SMS_ISVUPDATES_SYNCAGENT 元件處理。 您可以檢視來自此元件的狀態訊息，或參閱 SMS_ISVUPDATES_SYNCAGENT.log 中更詳細的狀態。 此記錄檔位於站台系統 Logs 資料夾中最上層的軟體更新點。 此路徑預設為 C:\Program Files\Microsoft Configuration Manager\Logs。 如需監視一般軟體更新管理程序的詳細資訊，請參閱[監視軟體更新](../deploy-use/monitor-software-updates.md) 

## <a name="known-issues"></a>已知問題

- 使用執行主控台的電腦從 WSUS 下載更新，並將它新增至更新套件。 主控台電腦必須信任 WSUS 簽章憑證。 如果不信任，下載協力廠商更新期間可能會發生簽章檢查的問題。 
- 協力廠商軟體更新同步處理服務無法將內容發佈至僅有中繼資料的更新，此更新是透過另一個應用程式、工具或指令碼 (例如 SCUP) 新增至 WSUS。 對這些更新執行的 [發佈協力廠商軟體更新內容]  動作會失敗。 如果您需要部署此功能尚未支援的協力廠商更新，請完整使用現有的程序來部署這些更新。  
-  Configuration Manager 有新版的類別目錄 cab 檔案格式。 新的版本包括廠商的二進位檔憑證。 只要您核准並信任類別目錄，這些憑證就會新增至 [管理]  工作區之 [安全性]  下的 [憑證]  節點中。  
     - 只要下載的 URL 是 https 且更新經過簽署，您仍然可以使用較舊的類別目錄 cab 檔案版本。 因為二進位檔憑證不在 cab 檔中，也未經核准，所以無法發佈內容。 您可在 [憑證]  節點中找到憑證，解除封鎖後再次發佈更新來暫時解決此問題。 如果您要發佈使用不同憑證簽署的多項更新，每個要用到的憑證都需要解除封鎖。
     - 如需詳細資訊，請參閱下列狀態訊息表中的狀態訊息 11523 和 11524。
-  當頂層軟體更新點上的協力廠商軟體更新同步處理服務需要 Proxy 伺服器來進行網際網路存取時，數位簽章檢查可能會失敗。 若要解決此問題，請在站台系統上設定 WinHTTP Proxy 設定。 如需詳細資訊，請參閱[適用於 WinHTTP 的 Netsh 命令](https://go.microsoft.com/fwlink/p/?linkid=199086) \(英文\)。
- 針對內容儲存體使用 CMG 時，如果已啟用 [下載可用的差異內容]  [用戶端設定](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)，第三方更新的內容將不會下載至用戶端。 <!--6598587-->

## <a name="status-messages"></a>狀態訊息

| MessageID       | 嚴重性           | 說明 | 可能的原因| 可能的解決方法
| ------------- |-------------| -----|----|----|
| 11516     | 錯誤 |無法發佈更新「更新識別碼」的內容，因為內容未經簽署。  您只能發佈具有有效簽章的內容。  |Configuration Manager 不允許發佈未經簽署的更新。| 以替代方式發佈更新。 </br></br>查看廠商是否提供經過簽署的更新。|
| 11523  | 警告 |  類別目錄 "X" 不包含內容簽署憑證，新增並核准內容簽署憑證之前，嘗試發佈此類別目錄更新的更新內容可能會失敗。 | 當您匯入使用舊版 cab 檔案格式的類別目錄時，可能會出現此訊息。|請連絡此類別目錄提供者，以取得包含內容簽署憑證的更新類別目錄。 </br> </br> 因為二進位檔憑證不在 cab 檔中，所以無法發佈內容。 您可在 [憑證]  節點中找到憑證，解除封鎖後再次發佈更新來暫時解決此問題。 如果您要發佈使用不同憑證簽署的多項更新，每個要用到的憑證都需要解除封鎖。|
| 11524| 錯誤  | 因為遺漏更新中繼資料，所以無法發佈更新「識別碼」。 | 更新可能已同步處理至 Configuration Manager 以外的 WSUS。| 請先使用 Configuration Manager 同步處理更新，再嘗試發佈其內容。  </br> </br>如已使用外部工具發佈更新為**僅限中繼資料**，請使用相同的工具發佈更新內容。|



## <a name="working-with-third-party-updates-video"></a>使用協力廠商更新影片
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>後續步驟
> [!div class="nextstepaction"]
> [部署軟體更新](./deploy-software-updates.md)
