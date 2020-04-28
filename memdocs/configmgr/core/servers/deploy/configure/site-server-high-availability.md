---
title: 站台伺服器的高可用性
titleSuffix: Configuration Manager
description: 如何藉由新增被動模式的站台伺服器，為 Configuration Manager 站台伺服器設定高可用性。
ms.date: 02/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 395504f5ccc3635f580bca739f1c4b7273861123
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700896"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Configuration Manager 的站台伺服器高可用性

適用於：  Configuration Manager (最新分支)

<!--1128774-->

在過去，您可以透過在您的環境中擁有這些角色的多個執行個體，來為 Configuration Manager 中的大多數角色新增備援。 除了站台伺服器本身。 站台伺服器角色的高可用性是以 Configuration Manager 為基礎的解決方案，能夠以「被動」  模式安裝額外的站台伺服器。 管理中心網站和子主要站台現在可擁有其他的被動模式站台伺服器。 被動模式的站台伺服器可以是內部部署的站台伺服器，也可以是 Azure 中的雲端式站台伺服器。

這項功能提供了下列優點

- 站台伺服器角色的備援性和高可用性  
- 更輕鬆地變更站台伺服器的硬體或 OS  
- 更輕鬆地將站台伺服器移至 Azure IaaS  

被動模式的站台伺服器，是您在「主動」  模式現有站台伺服器以外的站台伺服器。 被動模式的站台伺服器可在有需要時立即使用。 在您的整體設計中包含此額外的站台伺服器，可讓 Configuration Manager 服務具備[高可用性](high-availability-options.md)。  

被動模式的站台伺服器：

- 使用與您主動模式站台伺服器相同的站台資料庫。
- 被動模式中不會將資料寫入站台資料庫。
- 使用與您主動模式站台伺服器相同的內容庫。

若要讓被動模式的站台伺服器變成主動模式，您要手動「升階」  它。 此動作會將主動模式的站台伺服器切換成被動模式的站台伺服器。 原始主動模式站台伺服器上可用的站台系統角色仍然可供使用，只要該電腦可供存取即可。 在主動與被動模式之間切換的只有站台伺服器角色。

Microsoft Core Services Engineering and Operations 使用此功能將其管理中心網站移轉至 Microsoft Azure。 如需詳細資訊，請參閱 [Microsoft IT Showcase 文章](https://www.microsoft.com/itshowcase/Article/Content/1065/Migrating-System-Center-Configuration-Manager-onpremises-infrastructure-to-Microsoft-Azure)。

## <a name="prerequisites"></a>先決條件

- 站台的內容庫必須位於遠端網路共用上。 這兩部站台伺服器都需要共用及其內容的完全控制權限。 如需詳細資訊，請參閱[管理內容庫](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote)。<!--1357525-->  

  - 針對您要移動內容庫的目標網路路徑，站台伺服器電腦帳戶需要擁有路徑的**完全控制**權限。 此權限適用於共用及檔案系統。 遠端系統上不會安裝任何元件。

  - 站台伺服器不能有發佈點角色。 發佈點也會使用內容庫，且此角色不支援遠端內容庫。 移動內容庫之後，您即無法將發佈點角色新增至站台伺服器。  

- 被動模式的站台伺服器可以是內部部署的站台伺服器，也可以是 Azure 中的雲端式站台伺服器。  

    > [!NOTE]
    > 被動模式的雲端式站台伺服器會使用 Azure 基礎結構即服務 (IaaS)。 如需詳細資訊，請參閱下列文章：
    >
    >   - [Azure 虛擬機器 (適用於雲端式基礎結構)](../../../understand/use-cloud-services.md#azure-virtual-machines-for-cloud-based-infrastructure)
    >   - [Azure 上的 Configuration Manager 常見問題集](../../../understand/configuration-manager-on-azure.md)  

- 這兩部站台伺服器都必須加入相同的 Active Directory 網域。  

- Configuration Manager 支援階層中處於被動模式的站台伺服器。 管理中心網站和子主要站台現在可擁有其他的被動模式站台伺服器。<!-- 3607755 -->  

- 這兩個站台伺服器必須使用相同的站台資料庫。  

  - 資料庫可位於每部站台伺服器的遠端。 從 1810 版開始，Configuration Manager 安裝程序不會再封鎖在具有容錯移轉叢集 Windows 角色的電腦上安裝站台伺服器角色。 SQL Always On 需要此角色，因此先前您無法將站台資料庫共置在站台伺服器上。 透過這項變更，您可以使用較少的伺服器建立高可用性的站台，方法是被動模式中使用 SQL AlwaysOn 和站台伺服器。<!-- SCCMDocs issue 1074 -->  

  - 裝載站台資料庫的 SQL Server 可以使用預設的執行個體、具名執行個體、[SQL Server 叢集](use-a-sql-server-cluster-for-the-site-database.md)或 [SQL Server Always On 可用性群組](sql-server-alwayson-for-a-highly-available-site-database.md)。  

  - 兩部站台伺服器在裝載站台資料庫之 SQL Server 執行個體上都需要有 **sysadmin** 安全性角色。 原始的站台伺服器應該已經具有這些角色，因此請針對新的站台伺服器新增這些角色。 例如，下列 SQL 指令碼為 Contoso 網域中的新站台伺服器 **VM2** 新增下列角色：  

    ```SQL
    USE [master]
    GO
    CREATE LOGIN [contoso\vm2$] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[us_english]
    GO
    ALTER SERVER ROLE [sysadmin] ADD MEMBER [contoso\vm2$]
    GO
    ```

  - 這兩個站台伺服器都需要 SQL Server 執行個體上的站台資料庫的存取權。 原始的站台伺服器應該已經具有此存取權，因此請針對新的站台伺服器新增此存取權。 例如，下列 SQL 指令碼為 Contoso 網域中新站台伺服器 **VM2** 的 **CM_ABC** 資料庫新增了登入：  

    ```SQL
    USE [CM_ABC]
    GO
    CREATE USER [contoso\vm2$] FOR LOGIN [contoso\vm2$] WITH DEFAULT_SCHEMA=[dbo]
    GO
    ```

  - 被動模式的站台伺服器已設定為使用與主動模式站台伺服器相同的站台資料庫。 被動模式的站台伺服器只會從資料庫讀取。 升階到主動模式之前都不會寫入資料庫。  

- 被動模式的站台伺服器：  

  - 必須符合安裝主要站台的必要條件。 例如，.NET Framework、遠端差異壓縮和 Windows ADK。 如需完整清單，請參閱[站台和站台系統必要條件](../../../plan-design/configs/site-and-site-system-prerequisites.md)。<!-- SCCMDocs issue 765 -->  

    > [!NOTE]
    > 請務必安裝 SQL Server Native Client。 如果您未安裝，Configuration Manager 安裝期間的必要條件檢查程式會回報缺少 SQL Server 權限的錯誤。<!-- SCCMDocs#2290 -->

  - 主動模式站台伺服器的本機 Administrators 群組中必須有其電腦帳戶。<!--516036-->

  - 必須使用與主動模式站台伺服器版本相符的來源檔案來安裝。  

  - 安裝被動模式角色的站台伺服器之前，不能有來自任何安裝之任何站台的站台系統角色。  

- 兩部站台伺服器可以執行不同的作業系統或 Service Pack 版本，只要 [Configuration Manager 支援](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)它們。  

- 不要在針對高可用性設定的任一站台伺服器上裝載服務連接點角色。 如果它目前位於原始站台伺服器上，請將其移除，然後將它安裝在另一個站台系統伺服器上。 如需詳細資訊，請參閱 [About the service connection point](about-the-service-connection-point.md) (關於服務連接點)。  

- [網站系統安裝帳戶](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)的權限  

  - 根據預設，許多客戶會使用站台伺服器的電腦帳戶來安裝新的站台系統。 然後，需要將站台伺服器的電腦帳戶新增至遠端站台系統上的本機**系統管理員**群組。 如果您的環境使用這項設定，請務必將新站台伺服器的電腦帳戶新增至所有遠端站台系統上的此本機群組。 例如，所有的遠端發佈點。  

  - 更安全且建議的設定是使用服務帳戶來安裝站台系統。 最安全的設定是使用本機服務帳戶。 如果您的環境使用這項設定，則不需要變更。  

## <a name="limitations"></a>限制

- 每個主要站台僅支援一個被動模式的站台伺服器。  

- 次要站台中不支援被動模式的站台伺服器。<!--SCCMDocs issue 680-->  

    > [!NOTE]  
    > 在具有高可用性站台伺服器的主要站台下仍然支援次要站台。

- 被動模式的站台伺服器需要以手動方式升階為主動模式。 並沒有任何自動容錯移轉機制。  

- 在您新增被動模式的站台伺服器之前，不能在新的伺服器上安裝站台系統角色。  

    > [!NOTE]
    > 安裝被動模式的站台伺服器之後，您就可以視需要新增其他角色。 例如，位於主要站台的管理點。

- 針對類似使用資料庫之報告點的角色，在這兩部站台伺服器的遠端伺服器上裝載資料庫。  

- Configuration Manager 主控台不會在被動模式的站台伺服器上執行自動安裝作業。  

## <a name="add-a-site-server-in-passive-mode"></a>新增被動模式的站台伺服器

如需新增角色一般程序的詳細資訊，請參閱[安裝站台系統角色](install-site-system-roles.md)。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點，再按一下功能區中的 [建立站台系統伺服器]  。

2. 在 [建立站台系統伺服器精靈] 的 [一般]  頁面中，指定要裝載被動模式站台伺服器的伺服器。 您指定的伺服器在安裝被動模式的站台伺服器之前，不能裝載任何站台系統角色。  

3. 在 [系統角色選取]  頁面上，僅選取 [被動模式的站台伺服器]  。  

    > [!NOTE]  
    > 此精靈會在此頁面執行下列初始必要條件檢查：
    >
    > - 選取的伺服器不是次要站台伺服器
    > - 所選伺服器還不是被動模式的站台伺服器
    > - 站台的內容庫位於遠端位置  
    >  
    > 如果這些初始必要條件檢查失敗，您無法略過此精靈頁面繼續作業。  

4. 在 [被動模式的站台伺服器]  頁面中提供下列資訊，這些資訊會用在指定的伺服器上，執行安裝程式並安裝站台伺服器角色：

     - 選擇下列其中一個選項：  

         - **透過網路從在主動模式中的站台伺服器複製安裝來源檔案**：此選項會建立壓縮的套件，並將它傳送到新的站台伺服器。  

         - **將位於下列位置之來源檔案用於被動模式中的站台伺服器**：例如，已複製來源檔案的本機路徑。 請確定此內容和主動模式的站台伺服器版本相同。  

         - (建議  ) **使用位於下列網路位置的來源檔案**：指定從主動模式站台伺服器到 **CD.Latest** 資料夾內容的直接路徑。 例如，`\\Server\SMS_ABC\CD.Latest` 中的 "*Server*" 是主動模式的站台伺服器名稱，而 "*ABC*" 是站台碼。  

     - 指定新站台伺服器上安裝 Configuration Manager 的本機路徑。 例如：`C:\Program Files\Configuration Manager`  

5. 完成精靈。 Configuration Manager 會接著在指定的伺服器上安裝被動模式的站台伺服器。

如需詳細的安裝狀態，請在主控台中移至 [監視]  工作區，然後選取 [站台伺服器狀態]  節點。 被動模式站台伺服器的狀態會顯示為 [正在安裝]  。 如需詳細資訊，請選取伺服器，然後按一下 [顯示狀態]  。 這個動作會開啟 [站台伺服器安裝狀態] 視窗。 此程序完成時，兩部伺服器的狀態都會顯示 [正常]  。

如需安裝程序的詳細資訊，請參閱[流程圖 - 設定被動模式的站台伺服器](passive-site-server-flowchart.md)。

在您新增被動模式的站台伺服器之後，請在主控台 [站台]  節點的 [節點]  索引標籤中查看這兩部站台伺服器。

在被動模式的站台伺服器上，所有的 Configuration Manager 站台伺服器元件都處於待命狀態。 Windows 服務仍在執行。

## <a name="site-server-promotion"></a>站台伺服器升階  

備份和復原亦同，規劃並練習您變更站台伺服器的程序。 升階計劃請考慮下列幾點：  

- 練習兩部站台伺服器都在線上的計劃升階。 也要藉由強制中斷連線或關閉主動模式的站台伺服器，練習非計劃性的容錯移轉。  

- 決定容錯移轉期間的作業程序，以及與其他 Configuration Manager 系統管理員溝通的內容。  

- 執行計劃升階之前，請先：  

  - 檢查站台和站台元件的整體狀態。 確定您的環境一切正常。  

  - 檢查站台間主動複寫之任何套件的內容狀態。  

  - 檢查次要站台狀態和站台複寫。

  - 不要在子站台伺服器或次要站台伺服器上啟動任何新的內容發佈作業或維護。

    > [!NOTE]
    > 如果在容錯移轉期間，站台之間正在複寫檔案或資料庫，新的站台伺服器可能不會收到複寫的內容。 如果發生這種情況，請在站台伺服器啟動後重新發佈軟體內容。<!--515436--> 對於資料庫複寫，您可能需要在容錯移轉之後重新初始化次要站台。<!-- SCCMDocs issue 808 -->

  - 同時減少或移除其他排程活動。 例如，在將站台更新為新版本之後，請勿計劃立即升級站台伺服器。 站台更新包含可能與站台伺服器升階衝突的其他工作。

    > [!TIP]
    > 以下是其他活動如何與站台伺服器升階衝突的範例：
    >
    > - 星期一：將站台更新為最新版本。 啟用包含用戶端試驗的自動用戶端升級。
    > - 星期二：將被動模式的站台伺服器升階為主動站台伺服器。
    >
    > 在星期三或星期四之前，此動作可能會導致「所有」  用戶端升級，而不只是試驗集合。 這種行為可能會造成發佈點上的大量網路使用量及非預期的負載。<!-- SCCMDocs-pr#4794 -->

### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>將被動模式的站台伺服器升階為主動模式的程序

本節描述如何將被動模式的站台伺服器變更為主動模式。 您需要能存取 SMS 提供者的執行個體，才能存取該站台執行這項變更。 如需詳細資訊，請參閱[使用多重 SMS 提供者](../../../plan-design/hierarchy/plan-for-the-sms-provider.md#BKMK_MultiSMSProv)。  

> [!IMPORTANT]  
> 如果 SMS 提供者的所有執行個體均離線，您就會因為沒有提供者可用而無法連線到站台。 以被動模式角色新增站台伺服器時，安裝程式會在此伺服器上安裝 SMS 提供者的執行個體。<!-- SCCMDocs#1613 -->
>
> Configuration Manager 主控台要求來自站台伺服器 WMI 的可用 SMS 提供者清單。 當您在站台上安裝多重 SMS 提供者時，站台會隨機指派每個新連線要求，以使用安裝的 SMS 提供者。 您無法指定 SMS 提供者位置搭配使用特定的連線工作階段。 如果您的主控台因為目前的站台伺服器已離線而無法連線到站台，請在 [站台連線] 視窗中指定其他站台伺服器。  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取站台，然後切換至 [節點]  索引標籤。選取被動模式的站台伺服器，然後按一下功能區的 [升階為主動]  。 按一下 [是]  確認並繼續作業。
  
2. 重新整理主控台節點。 您正在升階的伺服器 [狀態]  欄在 [節點]  索引標籤中顯示為 [升階]  。  

3. 完成升階後，主動模式的新站台伺服器和被動模式的新站台伺服器的 [狀態]  資料行都會顯示 [正常]  。 新台的 [伺服器名稱]  欄現可顯示主動模式新站台伺服器的名稱。

如需詳細的狀態，請移至 [監視]  工作區，然後選取 [站台伺服器狀態]  節點。 [模式]  資料行會指出哪一部伺服器為 [主動]  或 [被動]  。 當您將伺服器從被動模式升階為主動模式時，請選取要升階為主動的站台伺服器，然後從功能區中選擇 [顯示狀態]  。 此動作會開啟 [站台伺服器升階狀態] 視窗，當中會顯示有關該程序的其他詳細資料。

當主動模式的站台伺服器切換到被動模式時，只有站台系統角色會變成被動。 所有安裝在該電腦上的其他站台系統角色仍然保持主動，並且可供其他用戶端存取。

如需「規劃的」  升階程序詳細資訊，請參閱[流程圖 - 升階站台伺服器 (已規劃)](promote-site-server-flowchart.md)。

### <a name="unplanned-failover"></a>未規劃的容錯移轉

如果目前的主動模式站台伺服器已離線，要升階的站台伺服器會嘗試連絡目前的主動模式站台伺服器，為時 30 分鐘。 如果離線的伺服器在此時間之前上線，就會順利收到通知，依正常程序繼續變更。 否則，要升階的站台伺服器會強制更新站台設定，讓它成為主動的伺服器。 如果離線的伺服器在此時間之後上線，它會先檢查網站資料庫的目前狀態。 它接著會將本身降級至被動模式的站台伺服器。

在等候的這 30 分鐘內，站台沒有任何主動模式的站台伺服器。 用戶端仍然與管理點、軟體更新點和發佈點等用戶端對向角色通訊。 使用者可以安裝已部署的軟體。 這段時間內無法管理站台。 如需詳細資訊，請參閱[站台失敗影響](../../manage/site-failure-impacts.md)。  

離線的伺服器如已損毀，以致無法上線，請從主控台刪除此站台伺服器。 然後建立被動模式的新站台伺服器，以還原高可用性服務。

如需「未規劃的」  容錯移轉程序詳細資訊，請參閱[流程圖 - 升階站台伺服器 (未規劃)](promote-site-server-unplanned-flowchart.md)。

### <a name="additional-tasks-after-site-server-promotion"></a>站台伺服器升階後的其他工作  

切換站台伺服器之後，您不必執行在[復原站台](../../manage/recover-sites.md#post-recovery-tasks)時必須執行的大部分其他工作。 例如，您不需要重設密碼，或者重新連線您的 Microsoft Intune 訂閱。

在您的環境中如為必要，您可能需要執行下列步驟：  

- 如果您匯入用於發佈點的 PKI 憑證，請重新匯入受影響的伺服器憑證。 如需詳細資訊，請參閱[重新產生用於發佈點的憑證](../../manage/recover-sites.md#regenerate-the-certificates-for-distribution-points)。  

- 如要整合 Confguration Manager 與商務用 Microsoft Store，請重新設定該連線。 如需詳細資訊，請參閱[管理從商務用 Microsoft Store 購買的應用程式](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。  

## <a name="daily-monitoring"></a>每天監視

當您有被動模式的站台伺服器時，請每天監視。 確定其狀態保持 [正常]，並可供使用。 在 Configuration Manager 主控台中，移至 [監視]  工作區，然後選取 [站台伺服器狀態]  節點。 檢視兩部站台伺服器及其目前的狀態。 也檢視 [管理]  工作區中的狀態。 展開 [站台設定]  ，然後選取 [站台]  節點。 選取站台，然後切換至 [節點]  索引標籤。

> [!NOTE]
> 當您將站台更新為新版 Configuration Manager 時，這也會以被動模式更新站台伺服器。 <!-- SCCMDocs-pr#4293 -->