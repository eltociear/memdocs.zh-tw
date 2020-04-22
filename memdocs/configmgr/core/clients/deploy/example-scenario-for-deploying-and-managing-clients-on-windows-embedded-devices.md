---
title: 範例案例 - 部署 Windows Embedded 用戶端
titleSuffix: Configuration Manager
description: 請參閱在 Windows Embedded 裝置上部署及管理 Configuration Manager 用戶端的示範案例。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693866"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>在 Windows Embedded 裝置上部署及管理 Configuration Manager 用戶端的示範案例

適用於：  Configuration Manager (最新分支)

此案例示範如何使用 Configuration Manager 管理啟用寫入篩選器的 Windows Embedded 裝置。如果您的內嵌裝置不支援寫入篩選器，則會以標準 Configuration Manager 用戶端運作，而且這些程序不適用。  

Coho Vineyard & Winery 開闢了一個遊客中心，需要在執行 Windows Embedded 的 kiosk 中執行互動式簡報。 新遊客中心大樓與 IT 部門有點距離，所以必須從遠端管理 kiosk。 除了執行簡報的軟體之外，這些裝置必須執行最新的反惡意程式碼保護軟體，以符合公司的安全性原則。 kiosk 必須於每週 7 天執行，而且在遊客中心開放時完全不停機。  

 Coho 已執行 Configuration Manager 管理網路上的裝置。 Configuration Manager 已設定為執行 Endpoint Protection，並安裝軟體更新及應用程式。 不過，因為 IT 小組先前不曾管理過 Windows Embedded 裝置，所以 Configuration Manager 系統管理員做了一項試驗，就是管理接待大廳中的兩部 kiosk。   

 為了管理這些啟用寫入篩選器的 Windows Embedded 裝置，Configuration Manager 系統管理員執行下列步驟來安裝 Configuration Manager 用戶端，使用 Endpoint Protection 保護用戶端，以及安裝互動式簡報軟體。  

1. Configuration Manager 系統管理員 (以下簡稱管理員) 閱讀 Windows Embedded 裝置使用寫入篩選器的方式，以及 Configuration Manager 如何藉由自動停用然後再重新啟用寫入篩選器，使持續安裝軟體更加容易。  

    如需詳細資訊，請參閱[規劃將用戶端部署至 Windows Embedded 裝置](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

2. 在管理員安裝 Configuration Manager 用戶端之前，管理員先為 Windows Embedded 裝置建立一個新的查詢式裝置集合。 由於公司使用標準命名格式來識別電腦，因此管理員可以透過電腦名稱的前六個字母來唯一識別 Windows Embedded 裝置：**WEMDVC**。 管理員使用下列 WQL 查詢建立此集合： **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

    此集合可讓管理員使用不同的設定選項，從其他裝置管理 Windows Embedded 裝置。 管理員將會使用此集合來控制重新啟動、以用戶端設定部署 Endpoint Protection，以及部署互動式簡報應用程式。  

    請參閱[如何建立集合](../../../core/clients/manage/collections/create-collections.md)。  

3. 管理員設定一個維護期間的集合，可確保在遊客中心開放期間，安裝簡報應用程式和任何升級時不需要重新啟動裝置。 開放時間為星期一到星期六的 09:00 到 18:00。 管理員將維護期間設定為每天 18:30 到 06:00。  

4. 如需詳細資訊，請參閱[如何使用維護期間](../../../core/clients/manage/collections/use-maintenance-windows.md)。  

5. 管理員接著設定自訂裝置用戶端設定，針對下列設定選取 [是]  來安裝 Endpoint Protection 用戶端，然後將此自訂用戶端設定部署至 Windows Embedded 裝置集合：  

   - **在用戶端電腦上安裝 Endpoint Protection 用戶端**  

   - **針對具有寫入篩選器的 Windows Embedded 裝置，認可 Endpoint Protection 用戶端安裝 (需要重新啟動)**  

   - **允許在維護期間以外執行 Endpoint Protection 用戶端安裝和重新啟動**  

     安裝 Configuration Manager 用戶端時，這些設定會安裝 Endpoint Protection 用戶端，並確保其保存於安裝的作業系統之中，而不是只寫入至重疊。 由於公司安全性原則要求一律要安裝反惡意程式碼軟體，所以管理員即使是在重新啟動的非常短時間內，也不想要冒著讓 kiosk 未受保護的風險。  

   > [!NOTE]  
   >  安裝 Endpoint Protection 用戶端需要在裝置的安裝期間，以及在遊客中心運作前重新啟動一次。 和應用程式或軟體定義更新的定期部署不同的是，下一次當公司升級至新版的 Configuration Manager 時，可能會在相同裝置上安裝 Endpoint Protection 用戶端。  

    如需詳細資訊，請參閱[設定 Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)。  

6. 此時用戶端的組態設定已就緒，管理員準備要安裝 Configuration Manager 用戶端。 管理員必須先手動停用 Windows Embedded 裝置上的寫入篩選器，才能安裝用戶端。 管理員閱讀 kiosk 隨附的 OEM 文件，並遵循指示停用寫入篩選器。  

    管理員使用公司標準命名格式重新命名裝置，然後使用下列命令，從保留用戶端來源檔案的對應磁碟執行 CCMSetup，藉以手動安裝用戶端：**CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    此命令會安裝用戶端，指派用戶端給內部網路 FQDN 為 **mpserver.cohovineyardandwinery.com**的管理點，並將用戶端指派給名為 **CO1**的主要站台。  

    管理員知道需要一些時間來安裝用戶端，並將其狀態傳送回站台。 因此，管理員等待用戶端順利安裝，指派給站台，並在管理員為 Windows Embedded 裝置所建立的集合中顯示為用戶端後才進行確認。  

    為了再次確認，管理員在裝置上的 [控制台] 中檢查 Configuration Manager 內容，並將這些內容與站台所管理的標準 Windows 電腦進行比對。 例如，在 [元件]  索引標籤上，[硬體清查代理程式]  顯示為 [已啟用]  ，而在 [動作]  索引標籤上有 11 個可用的動作，其中包括 [應用程式部署評估週期]  和 [探索資料收集週期]  。  

    確認用戶端已順利安裝、指派，以及從管理點接收用戶端原則後，管理員接著會遵循 OEM 的指示來手動啟用寫入篩選器。  

    如需詳細資訊，請參閱：  

   -   [如何將用戶端部署至 Windows 電腦](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [如何將用戶端指派至站台](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. 現在 Configuration Manager 用戶端已安裝在 Windows Embedded 裝置上，管理員確認可以使用與管理標準 Windows 用戶端相同的方式來管理這些裝置。 例如，管理員可以從 Configuration Manager 主控台使用遠端控制從遠端管理這些裝置，為這些裝置起始用戶端原則，且檢視用戶端內容和硬體清查。  

    由於這些裝置已加入至 Active Directory 網域，管理員不需要手動將這些裝置核准為受信任用戶端，以及從 Configuration Manager 主控台確認這些裝置已獲得核准。  

    如需詳細資訊，請參閱[如何管理用戶端](../../../core/clients/manage/manage-clients.md)。  

8. 為了要安裝互動式簡報軟體，管理員執行 [部署軟體精靈]  ，並設定必要的應用程式。 在精靈 [使用者體驗]  頁面的 [Windows Embedded 裝置的寫入篩選器處理]  區段中，管理員接受選取 [在到期時或在維護期間認可變更 (需要重新啟動)]  的預設選項。  

    管理員保留此寫入篩選器的預設選項，確保應用程式在重新啟動後仍然存在，以方便使用 kiosk 的訪客能隨時使用。 日常維護期間為安裝及任何更新時可能會發生的重新啟動狀況，提供了一段安全的期間。  

    管理員將應用程式部署至 Windows Embedded 裝置集合。  

    如需詳細資訊，請參閱[如何使用 Configuration Manager 部署應用程式](../../../apps/deploy-use/deploy-applications.md)。  

9. 為了要設定 Endpoint Protection 定義更新，管理員使用軟體更新並執行 [建立自動部署規則精靈]。 管理員選取 [定義更新]  範本，將適用於 Endpoint Protection 的設定預先填入精靈。  

     這些設定包括精靈之 [使用者經驗]  頁面的下列各項：  

   - **期限行為**：未選取 [軟體安裝]  核取方塊。  

   - **Windows Embedded 裝置的寫入篩選處理**：未選取 [在到期時或在維護時段認可變更 (需要重新啟動)]  核取方塊。  

     管理員保留這些預設設定。 總之，這兩個選項與此設定允許於白天在重疊中安裝 Endpoint Protection 的任何軟體更新定義，並且不在維護期間等待安裝及認可。 此設定最符合讓電腦執行最新反惡意程式碼防護的公司安全性原則。  

     > [!NOTE]  
     >  和應用程式的軟體安裝不同的是，Endpoint Protection 的軟體更新定義可能會非常頻繁地發生，甚至是一天多次。 這些通常是小檔案。 這些類型的安全性相關部署通常有益於安裝到重疊，而不是等到維護期間才進行部署。 如果裝置因為此動作起始評估檢查而重新啟動，並且未等到下一次排程的評估，Configuration Manager 用戶端將會快速重新安裝軟體定義更新。  

     管理員選取自動部署規則的 Windows Embedded 裝置集合。  

     如需詳細資訊，請參閱  
               步驟 3：如[設定 Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md) 中所述，將 Configuration Manager 軟體更新設定為傳遞定義更新至用戶端電腦  

10. 管理員決定設定一個定期認可重疊上所有變更的維護工作。 此工作是在每一次裝置重新啟動時支援軟體更新定義部署，以降低累積且必須重新安裝的更新數目。 在管理員的體驗中，此工作可讓反惡意軟體程式更有效地執行。  

    > [!NOTE]  
    >  如果內嵌裝置執行其他支援認可變更的管理工作，可能會自動將這些軟體更新定義認可至映像。 例如，安裝新版本的互動式簡報軟體可能也會認可軟體更新定義的變更。 或者，每個月在維護期間安裝的標準軟體更新，也會認可軟體更新定義的變更。 不過，此案例不會執行標準軟體更新，而且也不太可能經常更新互動式簡報軟體，因此可能要幾個月時間才會自動將軟體定義更新認可至映像。  

     管理員先建立一個只有名稱而沒有任何設定的自訂工作順序。 管理員執行 [建立工作順序精靈]：  

    1. 管理員在 [建立新的工作順序]  頁面選取 [建立新的自訂工作順序]  ，然後按一下 [下一步]  。  

    2. 管理員在 [工作順序資訊]  頁面上輸入 **Maintenance task to commit changes on embedded devices** 作為工作順序名稱，然後按一下 [下一步]  。  

    3. 管理員在 [摘要]  頁面選取 [下一步]  並完成精靈。  

       管理員接著將此自訂工作順序部署至 Windows Embedded 裝置集合，並將排程設定為每個月執行。 進行部署設定時，管理員選取 [在到期時或在維護期間認可變更 (需要重新啟動)]  核取方塊，以便在重新啟動後保存變更。 為了要設定此部署，管理員選取剛才建立的自訂工作順序，然後在 [首頁]  索引標籤的 [部署]  群組中按一下 [部署]  ，啟動 [部署軟體精靈]：  

    4. 管理員在 [一般]  頁面選取 Windows Embedded 裝置集合，然後按一下 [下一步]  。  

    5. 管理員在 [部署設定]  頁面選取 [必要]  的 [目的]  ，然後按一下 [下一步]  。  

    6. 管理員在 [排程]  頁面按一下 [新增]  以指定維護期間的每週排程，然後按一下 [下一步]  。  

    7. 管理員完成精靈，未做進一步變更。  

       如需詳細資訊，請參閱  
                 [管理工作順序以自動化工作](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)。  

11. 為了讓 kiosk 能夠自動執行，管理員寫撰寫指令碼來設定裝置的下列設定值：  

    - 使用不需密碼的來賓帳戶自動登入。  

    - 在啟動時自動執行互動式簡報軟體。  

      管理員使用套件和程式，將此指令碼部署至 Windows Embedded 裝置集合。 執行部署軟體精靈時，管理員再次選取 [在到期時或在維護期間認可變更 (需要重新啟動)]  核取方塊，在重新啟動後繼續變更。  

      如需詳細資訊，請參閱[套件和程式](../../../apps/deploy-use/packages-and-programs.md)。  

12. 隔天早上，管理員檢查 Windows Embedded 裝置。 並確認下列項目：  

    - 使用來賓帳戶可以自動登入 Kiosk。  

    - 互動式簡報軟體可順利執行。  

    - 已安裝 Endpoint Protection 用戶端，且裝有最新的軟體更新定義。  

    - 裝置會在維修期間自動啟動。  

      如需詳細資訊，請參閱：  

    - [如何監視 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [使用 Configuration Manager 監視應用程式](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. 管理員監視 kiosk 並向主管報告能夠成功進行管理。 因此，遊客中心訂購了 20 台 Kiosk。  

     手動安裝 Configuration Manager 用戶端必須手動停用寫入篩選器後再啟用，為避免此作業，管理員確認訂單包含自訂映像，該映像內含 Configuration Manager 用戶端的安裝與站台指派。 此外，裝置的命名一律以公司命名格式為準。  

     遊客中心開幕前一週，Kiosk 送到了。 在這段時間，Kiosk 連線上網，所有裝置管理作業均自動執行，不需要現場管理員操作。 管理員確認 kiosk 能夠按照需求執行功能：  

    -   Kiosk 上的用戶端可以完成站台指派，並且從 Active Directory 網域服務下載信任的根金鑰。  

    -   Kiosk 上的用戶端會自動新增至 Windows Embedded 裝置集合，並且完成維護期間設定。  

    -   已安裝 Endpoint Protection 用戶端，且裝有最新的反惡意程式防護軟體更新定義。  

    -   已安裝互動式簡報軟體並可自動執行，隨時可供遊客使用。  

14. 初始設定完成後，如必須重新啟動以進行更新，只會在遊客中心關閉後進行。  
