1.  在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，然後選取 [軟體更新]  節點。  

2.  使用以下其中一種方式選擇要下載的軟體更新：  

    -   從 [軟體更新群組]  節點，選取一或多個軟體更新群組。 然後，按一下功能區中的 [下載]  。  

    -   從 [所有軟體更新]  節點，選取一或多個軟體更新。 然後，按一下功能區中的 [下載]  。  

        > [!NOTE]  
        >  在 [所有軟體更新]  節點中，Configuration Manager 只會顯示在過去 30 天內發行且分類為 [重大]  和 [安全性]  的軟體更新。  

        > [!TIP]  
        >  按一下 [新增準則]  以篩選顯示在 [所有軟體更新]  節點中的軟體更新。 儲存常用的搜尋準則，然後在 [搜尋]  索引標籤上管理已儲存的搜尋。  


3.  在 [下載軟體更新精靈] 的 [部署套件]  頁面上，設定下列設定：  

    -  **選取部署套件**：選擇此設定可針對部署中的軟體更新選取現有部署套件。  

        > [!NOTE]  
        >  站台已下載至所選取部署套件的軟體更新將不會再次下載。  

    -  **建立新部署套件**：選取此設定可針對部署中的軟體更新建立新的部署套件。 進行以下設定：  

        -   **名稱**：指定部署套件的名稱。 套件必須具有簡短描述套件內容的唯一名稱。 長度限制為 50 個字元。  

        -   **描述**：指定描述，提供部署套件的相關資訊。 選擇性描述限制為 127 個字元。    

        -   **套件來源**：指定軟體更新來源檔案的位置。 鍵入來源位置的網路路徑 (例如 `\\server\sharename\path`)，或按一下 [瀏覽]  尋找網路位置。 請先建立部署套件來源檔案的共用資料夾，再繼續前往下一個頁面。  

             - 您無法使用指定的位置作為另一個軟體部署套件的來源。  

             - 您可以在 Configuration Manager 建立部署套件之後，變更部署套件內容中的套件來源位置。 如果您這樣做，就需先將內容從原始套件來源複製到新的套件來源位置。  

             -  SMS 提供者電腦帳戶和執行精靈下載軟體更新的使用者，都必須具有下載位置的**寫入**權限。 限制存取下載位置。 這項限制可降低攻擊者竄改軟體更新來源檔案的風險。  

        - **啟用二進位差異複寫**：啟用此設定，可將站台間的網路流量降到最低。 二進位差異複寫 (BDR) 只會更新套件中已變更的內容，而不是更新整個套件內容。 如需詳細資訊，請參閱[二進位差異複寫](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication)。  

4.  在 [發佈點]  頁面上，指定將裝載軟體更新檔案的發佈點或發佈點群組。 如需發佈點的詳細資訊，請參閱 [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。 此頁面只有在您建立新的軟體更新部署套件時才可使用。  

5.  只有在您建立新的軟體更新部署套件時才能使用 [發佈設定]  頁面。 指定下列設定：  

    -   **發佈優先順序**：使用此設定可指定部署套件的發佈優先順序。 將部署套件傳送到子網站上的發佈點時，會套用發佈優先順序。 部署套件會依優先順序傳送：高、中或低。 優先順序相同的套件，會依照建立的順序傳送。 若沒有待處理項目，則無論套件的優先順序為何，系統都會立即處理它。 根據預設，站台會傳送優先順序為 [中]  的套件。  

    -   **Enable for on-demand distribution \(啟用依需求發佈\)** ：使用此設定可依需求將內容發佈至用戶端目前界限群組中為此功能設定的發佈點。 當您啟用此設定時，管理點會為發佈管理員建立觸發程序，在用戶端要求套件內容但內容無法使用時，將內容發佈至所有這類發佈點。 如需詳細資訊，請參閱[依需求發佈內容](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)。  

    -   **預先設置的發佈點設定**：使用此設定可指定您要如何將內容發佈至預先設置的發佈點。 選擇下列其中一個選項：  

        -   **當套件指派給發佈點時，自動下載內容**：使用此設定以忽略預先設置的設定，並將內容發佈到發佈點。   

        -   **僅下載發佈點的內容變更**：使用此設定可將初始內容預先設置至發佈點，再將內容變更發佈至發佈點。  

        -   **將此套件中的內容手動複製到發佈點**：使用此設定則一律在發佈點上預先設置內容。 此選項是預設值。  

        如需在發佈點上預先設置內容的詳細資訊，請參閱[使用預先設置的內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)。  


6.  在 [下載位置]  頁面上，指定 Configuration Manager 用來下載軟體更新來源檔案的位置。 使用下列其中一個選項：  

    -   **從網際網路下載軟體更新**：選取此設定可從網際網路上的位置下載軟體更新。 此選項是預設值。  

    -   **Download software updates from a location on my network /(從我的網路位置下載軟體更新/)** ：選取此設定可從本機目錄或共用資料夾下載軟體更新。 此設定在執行精靈的電腦沒有網際網路存取時很實用。 任何具有網際網路存取的電腦都可以預先下載軟體更新。 然後，將它們儲存在本機網路上執行精靈的電腦可存取的位置。  


7.  在 [語言選擇]  頁面上，選取站台下載已選取之軟體更新所使用的語言。 只有在軟體更新有提供所選取的語言時，站台才會進行下載。 無指定語言的軟體更新一律會下載。 根據預設，精靈會選取您在軟體更新點內容中設定的語言。 您必須至少選取一種語言才能繼續至下一頁。 如果您只選取軟體更新不支援的語言，則更新下載會失敗。  

8. 在 [摘要]  頁面上，確認您在精靈中選取的設定，然後按一下 [下一步]  下載軟體更新。  

9. 在 [完成]  頁面上，確認軟體更新已成功下載，然後按一下 [關閉]  。  