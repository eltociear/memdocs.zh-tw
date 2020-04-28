---
title: 安裝精靈
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e32956d2ca9385c22e9073cfa2665e1f61b3ebd3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078629"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>使用安裝精靈安裝 Configuration Manager 站台

適用於：  Configuration Manager (最新分支)

若要使用引導式使用者介面安裝新的 Configuration Manager 站台，請使用 Configuration Manager 安裝精靈 (setup.exe)。 這個精靈支援安裝主要站台或管理中心網站。 您也可以使用精靈，針對 Configuration Manager 將[評估安裝升級](upgrade-an-evaluation-install-to-a-full-install.md)至完整授權安裝。 當您不想要使用這個精靈時，可以改成使用[安裝指令碼](use-a-command-line-to-install-sites.md)，然後執行自動命令列安裝。

從 Configuration Manager 主控台內安裝次要站台。 次要站台不支援指令碼命令列安裝。

> [!Note]  
> 從 1906 版開始，**splash.hta** 檔案已不再存在於安裝媒體的根目錄。 它會提供下列資訊的連結：<!--SCCMDocs-pr#3545-->
>
> - **安裝站台**：`smssetup\bin\x64\setup.exe`。 如需詳細資訊，請參閱[安裝管理中心或主要站台](#bkmk_primary)。
> - **開始之前**：[設計站台階層](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **評估伺服器整備程度**：[必要條件檢查工具](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **下載所需的必要條件檔案**：`smssetup\bin\x64\setupdl.exe`。 如需詳細資訊，請參閱[安裝程式下載程式](setup-downloader.md)。
> - **安裝 Configuration Manager 主控台**：`smssetup\bin\i386\consolesetup.exe`。 如需詳細資訊，請參閱[安裝主控台](install-consoles.md)。
> - [**下載 System Center Updates Publisher**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **下載適用於其他作業系統的用戶端**： <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft Endpoint Configuration Manager - macOS 用戶端 (64 位元)](https://www.microsoft.com/download/details.aspx?id=100850) \(英文\)
>   - [適用於 UNIX 和 Linux 的用戶端](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**版本資訊**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**閱讀說明文件**](https://docs.microsoft.com/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **取得安裝協助**：[TechNet 論壇：Configuration Manager (最新分支) – 站台和用戶端部署](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Configuration Manager 社群**：[System Center 社群：如何參與](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Configuration Manager 首頁**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> 安裝管理中心或主要站台

使用以下程序安裝管理中心網站或主要站台。 也請使用它將評估站台升級為完整授權版的 Configuration Manager 站台。

開始站台安裝之前，請先熟悉下列各文中的詳細資料︰

- [準備安裝站台](prepare-to-install-sites.md)
- [安裝站台的必要條件](prerequisites-for-installing-sites.md)

如果您要將管理中心網站安裝為站台擴充案例的一部分，請先檢閱[擴充獨立主要站台](use-the-setup-wizard-to-install-sites.md#bkmk_expand)，再使用下列程序。

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> 安裝主要站台或管理中心網站的流程

1. 在您要安裝站台的電腦上，執行 `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` 以啟動 [Configuration Manager 安裝精靈]  。  

    > [!NOTE]  
    > 如果您安裝管理中心網站以在獨立主要站台上進行擴充，或在現有階層中安裝新的子主要站台，請使用符合一或多個現有站台版本的安裝媒體 (原始程式檔)。 如果您所安裝的主控台內更新已變更先前安裝站台的版本，請不要使用原始安裝媒體。 而是改成使用已更新站台之 [CD.Latest 資料夾](../../manage/the-cd.latest-folder.md)中的來源檔案。 Configuration Manager 要求您使用的來源檔案，必須符合新站台所要連線的現有站台版本。  

2. 在 [開始之前]  頁面上，選擇 [下一步]  。  

3. 在 [開始使用]  頁面上，選取您要安裝的站台類型：  

    - **管理中心網站**，作為新階層的第一個站台，或擴充獨立主要站台時：  

        選取 [安裝 Configuration Manager 管理中心網站]  。  

        在此程序稍後的步驟中，我們將提供您安裝管理中心網站的選擇，以將其作為新階層的第一個站台，或安裝管理中心網站以擴充獨立主要站台。  

    - **主要站台**，作為新階層中第一個站台的獨立主要站台，或作為子主要站台：  

        選取 [安裝 Configuration Manager 主要站台]  。  

        > [!TIP]  
        > 當您想要在測試環境中安裝獨立主要站台時，通常只要選取選項 [為獨立主要站台使用一般安裝選項]  即可。 選取此選項時，安裝程式會執行下列動作：  
        >
        > - 自動將該站台設定為獨立主要站台。  
        > - 使用預設安裝路徑。  
        > - 為該站台資料庫使用預設 SQL Server 執行個體的本機安裝。  
        > - 在站台伺服器電腦上安裝管理點和發佈點。  
        > - 使用英文與主要站台伺服器 OS 的顯示語言 (若它符合 Configuration Manager 支援的其中一個語言) 設定站台。  

4. 在 [產品金鑰]  頁面上：  

    - 選擇是否將 Configuration Manager 安裝為評估版或授權版。  

        - 如果您選取授權版，請輸入產品金鑰，然後選擇 [下一步]  。  

        - 如果您選取評估版，請選擇 [下一步]  。 (您稍後可以將評估安裝升級為完整安裝)。  

    - 您也可以指定授權合約的**軟體保證到期日**。 這是一個方便的提醒日期。 如果您未在安裝期間輸入此日期，則稍後可以從 Configuration Manager 主控台指定它。  

        > [!NOTE]  
        > Microsoft 不會驗證您輸入的到期日，亦不會將這個日期用於授權驗證。 您可以將它作為到期日的提醒。 此日期非常有用，因為 Configuration Manager 會定期檢查線上提供的新軟體更新。 您的軟體保證授權狀態應該是最新的，以便您有資格使用其他更新。  

    如需詳細資訊，請參閱[授權和分支](../../../understand/learn-more-editions.md)。  

5. 在 [Microsoft 軟體授權條款]  頁面上，閱讀並接受授權條款。  

6. 在 [必要條件授權]  頁面上，閱讀並接受軟體必要條件的授權條款。 安裝程式會在需要時，於站台系統或用戶端上下載並自動安裝軟體。 在繼續進行下一個頁面之前，接受所有的條款。  

7. 在 [必要條件下載]  頁面上，指定安裝程式必須從網際網路下載最新版先決條件可轉散發檔案，或使用先前下載的檔案：  

    - 若希望安裝程式此時下載這些檔案，請選取 [下載必要檔案]  。 然後指定要儲存檔案的位置。  

    - 如果您先前使用[安裝程式下載程式](setup-downloader.md)下載檔案，請選取 [使用先前下載的檔案]  。 然後指定下載資料夾。  

        > [!TIP]  
        > 若使用先前下載的檔案，請確認下載資料夾的路徑，內含最新版的檔案。  

8. 在 [伺服器語言選擇]  頁面上，選取可供 Configuration Manager 主控台和報表使用的語言 (預設會選取英文，且無法移除)。如需詳細資訊，請參閱[語言套件](language-packs.md)。  

9. 在 [用戶端語言選擇]  頁面上，選取用戶端電腦可用的語言。 也請指定是否要針對行動裝置用戶端啟用所有用戶端語言。 (預設會選取英文，且無法移除)。  

    > [!IMPORTANT]  
    > 當您使用管理中心網站時，請確定您在管理中心網站設定的用戶端語言包含您在每個子主要站台設定的所有用戶端語言。 從發佈點安裝的用戶端可以從頂層站台存取用戶端語言，而從管理點安裝的用戶端可以從其指派的主要站台存取用戶端語言。  

10. 在 [站台和安裝設定]  頁面上，為目前所安裝的新站台，指定下列項目：  

    - **站台碼**：[階層中的每個站台碼都必須是唯一的](prepare-to-install-sites.md#bkmk_sitecodes)。 使用三個英數字元：A 到 Z 以及 0 到 9。 因為站台碼會用於資料夾名稱中，所以請勿使用 Windows 的保留名稱，包括：  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > 安裝程式不會驗證指定的站台碼是否已在使用中，或其是否為保留名稱。  

    - **站台名稱**：每個站台都需要此易記名稱，協助您識別站台。  

    - **安裝資料夾**：此資料夾是 Configuration Manager 安裝的路徑。 安裝站台之後，即無法變更位置。 路徑不能包含 Unicode 字元或結尾空格。  

        > [!NOTE]  
        > 請考慮您是否想要使用預設的安裝資料夾。 如果您在生產環境中使用預設的 OS 磁碟分割，則您未來可能會遇到下列問題：  
        >
        > - 如果 Configuration Manager 使用 OS 磁碟分割上的其他可用磁碟空間，則 Windows 和 Configuration Manager 將不會正常運作。 如果您在不同的磁碟分割上安裝 Configuration Manager，其磁碟耗用量將不會對 OS 產生影響。
        > - Configuration Manager 效能優於快速磁碟。 有些伺服器設計不會基於速度而將 OS 磁碟最佳化。
        > - 您可以檢修、還原或重新安裝 OS，而不會影響您的 Configuration Manager 安裝。  

11. 在 [站台安裝]  頁面上，使用符合您案例的下列選項：  

    - **我正在安裝管理中心網站：**  

        在 [管理中心網站安裝]  頁面上，選取 [安裝成新階層中的第一個站台]  ，然後選擇 [下一步]  繼續。  

    - **我正在將獨立主要站台擴充為擁有管理中心網站的階層：**  

        在 [管理中心網站安裝]  頁面上，選取 [將現有的獨立主要站台擴充到階層中]  。 接著指定獨立主要站台伺服器的 FQDN，然後選擇 [下一步]  以繼續。  

        您用來安裝新管理中心網站的媒體必須符合主要站台的版本。  

    - **我正在安裝獨立主要站台：**  

        在 [主要站台安裝]  頁面上，選取 [將主要站台安裝為獨立站台]  ，然後選擇 [下一步]  。  

    - **我正在安裝子主要站台：**  

        在 [主要站台安裝]  頁面上，選取 [將主要站台加入現有的階層中]  。 然後指定管理中心網站的 FQDN，並選擇 [下一步]  。  

12. 在 [資料庫資訊]  頁面上，指定下列資訊：  

    - **SQL Server 名稱 (FQDN)** ：根據預設，此值會設定為站台伺服器電腦。  

        如果您使用自訂連接埠，請將該連接埠新增至 SQL Server 的 FQDN。 請在 SQL Server 的 FQDN 後方加上逗號，再加上連接埠號碼。 例如，針對伺服器 *SQLServer1.fabrikam.com*，請使用下列方式指定連接埠 *1551*：`SQLServer1.fabrikam.com,1551`  

    - **執行個體名稱**：根據預設，此值為空白。 它會使用站台伺服器電腦上的預設 SQL 執行個體。  

    - **資料庫名稱**：根據預設，此值是設定為 `CM_<Sitecode>`。 您可以自訂此值。  

    - **Service Broker 連接埠**：根據預設，此值會設定為使用預設的 SQL Server Service Broker (SSB) 連接埠 4022。 SQL 使用它直接與其他站台的站台資料庫進行通訊。  

13. 在第二個 [資料庫資訊]  頁面上，您可以指定 SQL Server 資料檔以及站台資料庫的 SQL Server 記錄檔的自訂位置：  

    - 根據預設，它會使用 SQL Server 的預設檔案位置。  

    - 當您使用 SQL Server 叢集時，無法使用指定自訂檔案位置的選項。  

    - 先決條件檢查程式不會對自訂的檔案位置執行可用磁碟空間檢查。  

14. 在 [SMS 提供者設定]  頁面上，為想要安裝 SMS 提供者的伺服器，指定 FQDN。  

    - 根據預設，它會指定站台伺服器。  

    - 安裝站台之後，可設定其他 SMS 提供者。 如需詳細資訊，請參閱[規劃 SMS 提供者](../../../plan-design/hierarchy/plan-for-the-sms-provider.md)。  

15. 在 [用戶端通訊設定]  頁面上，選擇是否要將所有站台系統設定為僅接受來自於用戶端的 HTTPS 通訊，或為每個站台系統角色設定通訊方法。  

    選取 [所有站台系統角色僅能接受用戶端傳來的 HTTPS 通訊]  時，用戶端電腦必須具備有效的 PKI 憑證以進行用戶端驗證。 如需詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。  

    > [!NOTE]  
    > 只有在您安裝主要站台時，才需進行此步驟。 若是安裝管理中心網站，請略過此步驟。  

16. 在 [網站系統角色]  頁面上，選擇是否要安裝管理點或發佈點。 為每個選擇要由安裝程式安裝的角色：  

    - 輸入將裝載角色的伺服器 **FQDN**。 然後選擇伺服器將支援的用戶端連線方式：HTTP 或 HTTPS。  

    - 若在前一頁已選取 [所有站台系統角色僅能接受用戶端傳來的 HTTPS 通訊]  ，就會為 HTTPS 自動設定用戶端連線設定。 除非您返回到上一頁，否則無法變更此設定。  

    > [!NOTE]  
    > 只有在您安裝主要站台時，才需進行此步驟。 若是安裝管理中心網站，請略過此步驟。  

    > [!NOTE]  
    > 若要安裝站台系統角色，安裝程式會使用 **站台系統安裝帳戶**。 根據預設，這會使用主要站台的電腦帳戶。 此帳戶必須是遠端電腦上的本機系統管理員，才可安裝此站台系統角色。 如果此帳戶沒有必要的權限，則請取消核取站台系統角色，並稍後在設定其他帳戶用作站台系統安裝帳戶之後，從 Configuration Manager 主控台中進行安裝。 如需詳細資訊，請參閱[帳戶](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)。  

17. 在 [使用方式資料]  頁面上，檢閱 Microsoft 所收集資料的相關資訊，然後選擇 [下一步]  。 如需詳細資訊，請參閱[診斷和使用方式資料](../../../plan-design/diagnostics/diagnostics-and-usage-data.md)。  

18. 只有在下列情況下才能使用 [服務連接點設定]  頁面：  

    - 當您要安裝獨立主要站台時。  

    - 當您要安裝管理中心網站時。  

    > [!NOTE]  
    > 如果您要安裝子主要站台，請略過此步驟。  

     如果您要將管理中心網站安裝為站台擴充案例的一部分，並且已在獨立主要站台安裝此角色，請先從獨立主要站台解除安裝此角色。 此角色執行個體在階層中只能有一個，且僅於該階層的頂層站台支援。  

     選取 [服務連接點]  的設定之後，請選擇 [下一步]  。 安裝程式完成之後，可以從 Configuration Manager 主控台變更此設定。 如需詳細資訊，請參閱 [About the service connection point](../configure/about-the-service-connection-point.md) (關於服務連接點)。  

19. 在 [設定摘要]  頁面上，檢閱您已選取的設定。 當您準備好時，請選擇 [下一步]  啟動先決條件檢查程式。  

20. 在 [先決條件安裝檢查] 頁面上，它會列出檢查程式可識別的所有問題。   

    - 先決條件檢查程式找到問題時，請選擇清單中的項目，以查看如何解決問題的詳細資料。  

    - 在您可以繼續安裝站台之前，請解決**失敗**項目。 此外，請嘗試解決狀態為 [警告]  的項目，但這些項目不會讓站台無法安裝。  

    - 解決問題之後，請選擇 [執行檢查]  ，重新執行先決條件檢查程式。  

        如果執行先決條件檢查程式，但沒有任何檢查收到**失敗**狀態，則可以選擇 [開始安裝]  啟動站台安裝。  

    > [!TIP]  
    > 除了精靈所提供的意見反應，您還可以在 **ConfigMgrPrereq.log** 檔案中找到有關先決條件問題的其他資訊。 它位於您要安裝站台之電腦系統磁碟機的根目錄中。 如需詳細資訊，請參閱[先決條件檢查清單](list-of-prerequisite-checks.md)。  

21. 在 [安裝]  頁面上，安裝程式會顯示安裝狀態。 核心站台伺服器安裝完成時，您可以 [關閉]  安裝精靈。 當您關閉精靈時，安裝與初始站台設定會於背景繼續執行。  

    - 安裝程式完成之前，可以將 Configuration Manager 主控台連線至站台。 這個主控台會以唯讀方式連線，且可供您檢視物件與設定，但您無法進行修改。  

    - 安裝程式完成之後，您可以連線能編輯物件與設定的主控台。  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> 擴充獨立主要站台

將獨立主要站台安裝為第一個站台時，稍後可以選擇安裝管理中心網站，將該站台擴充到較大的階層。

當您擴充獨立主要站台時，將會安裝新的管理中心網站，其使用現有獨立主要站台的資料庫作為參考。 安裝新的管理中心網站之後，獨立主要站台會作為子主要站台。

- 您只能將獨立主要站台擴充到新的階層。  

- 您只能將一個獨立主要站台擴充到特定的階層中。 您無法使用此選項將其他獨立主要站台加入相同的階層中。 相反地，使用「移轉精靈」將資料從一個階層移轉至另一個階層。 如需詳細資訊，請參閱[在階層間移轉資料](../../../migration/migrate-data-between-hierarchies.md)。  

- 將獨立站台擴充到管理中心網站的階層中之後，即可新增其他子主要站台。  

- 若要利用管理中心網站從階層中移除主要站台，請先解除安裝主要站台。  

若要展開該站台，請使用「Configuration Manager 安裝精靈」安裝新的管理中心網站，但請注意下列事項：  

- 請使用與獨立主要站台相同的 Configuration Manager 版本來安裝管理中心網站。  

- 在安裝精靈的 [開始使用]  頁面上，請選取安裝管理中心網站的選項。 在安裝程式稍後的階段中，將要選擇擴充現有獨立主要站台的選項。  

- 當您為新的管理中心網站設定 [用戶端語言選擇]  頁面時，請選取與為擴充之獨立主要站台所設定的用戶端語言相同的用戶端語言。  

- 在 [站台安裝]  頁面上，請選取擴充獨立主要站台的選項。  

若要擴充獨立主要站台，請先查看[擴充站台的先決條件](prerequisites-for-installing-sites.md#bkmk_expand)。 然後，請使用此文章前面的[安裝主要站台或管理中心網站](use-the-setup-wizard-to-install-sites.md#bkmk_installpri)程序。


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> 安裝次要站台

請使用 Configuration Manager 主控台來安裝次要站台。  

- 如果您使用的主控台未連線至新次要站台之父站台的主要站台，則安裝該站台的命令會複寫至正確的主要站台。  

- 在開始安裝站台之前，請確定您的使用者帳戶具有必要的權限。 也請確定將裝載新次要站台的伺服器，符合做為次要站台伺服器使用的所有先決條件。  

- 安裝次要站台時，Configuration Manager 會將新的站台設定為使用在父主要站台所設定的用戶端通訊連接埠。  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> 安裝次要站台的流程  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取將為新次要站台之父主要站台的站台。  

2. 若要啟動 [建立次要站台精靈]  ，請在功能區中選擇 [建立次要站台]  。  

3. 在 [開始之前]  頁面上，確認列出的主要站台是您要使其成為新次要站台之父站台的站台。 然後選擇 [下一步]  。  

4. 在 [一般]  頁面上，指定以下設定：  

    - **站台碼**：階層中的每個站台碼必須是唯一的。 使用三個英數字元：A 到 Z 以及 0 到 9。 因為站台碼會用於資料夾名稱中，所以請勿使用 Windows 的保留名稱，包括：  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > 安裝程式不會驗證指定的站台碼是否已在使用中，或其是否為保留名稱。  

    - **站台伺服器名稱**：此值為安裝新次要站台之伺服器的 FQDN。  

    - **站台名稱**：每個站台都需要此易記名稱，協助您識別站台。  

    - **安裝資料夾**：此資料夾是 Configuration Manager 安裝的路徑。 安裝站台之後，即無法變更位置。 路徑不能包含 Unicode 字元或結尾空格。  

    > [!IMPORTANT]  
    > 在此頁面指定詳細資料之後，您可以選擇 [摘要]  直接轉到精靈的 [摘要]  頁面。 此動作會使用其餘次要站台選項的預設設定。  
    > 
    > - 如果您熟悉此精靈中的預設設定，而且這些預設設定是您想要使用的設定，才會使用此選項。  
    > - 當您使用預設設定時，界限群組不會與發佈點建立關聯。 在您設定包含次要站台伺服器的界限群組之前，用戶端不會使用安裝在此次要站台作為內容來源位置的發佈點。  

5. 在 [安裝來源檔]  頁面上，選擇次要站台電腦要如何取得原始程式檔以安裝該站台。  

    使用在網路上共用或本機複製至目標次要站台伺服器的 CD.Latest 來源檔案時：  

    - **1802 版與較舊版本**

        - CD.Latest 來源檔案位置包括名為 **Redist** 的資料夾。 將此 **Redist** 資料夾作為子資料夾移動到 **SMSSETUP** 資料夾下。  

            > [!Note]  
            > 如果安裝期間出現雜湊不符的錯誤，請更新 **Redist** 資料夾。 使用[安裝程式下載程式](setup-downloader.md)取得最新的檔案。 對於導致雜湊不相符錯誤的任何檔案，還要將它們從更新的 **Redist** 資料夾複製到 **SMSSETUP\BIN\X64** 資料夾。

    - **1806 版和更新版本**<!-- SCCMDocs-pr issue 3164 -->

        - CD.Latest 來源檔案位置包括名為 **Redist** 的資料夾。 將此 **Redist** 資料夾作為子資料夾移動到 **SMSSETUP** 資料夾下。  

        - 將下列檔案從 **Redist** 資料夾複製到 **SMSSETUP\BIN\X64** 資料夾：  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - 如果任何來自 **Redist** 的檔案都無法使用，則安裝程式無法安裝次要站台。  

    - 次要站台伺服器的電腦帳戶，必須要有原始程式檔資料夾與共用的**讀取**權限。  

6. 在 [SQL Server 設定]  頁面上，指定要使用的 SQL Server 版本，然後設定相關的設定。  

    > [!NOTE]  
    > 安裝開始前，安裝程式不會驗證您在此頁輸入的資訊。 在繼續之前，請確認這些設定。  

    - **在次要站台電腦上安裝和設定 SQL Express 的本機複本**  

        - **SQL Server 服務連接埠**：指定 SQL Server Express 使用的 SQL Server 服務連接埠。 服務連接埠一般會設定為使用 TCP 連接埠 1433，不過您可以設定另一個連接埠。  

        - **SQL Server Broker 連接埠**：指定 SQL Server Express 使用的 SQL Server Service Broker (SSB) 連接埠。 Service Broker 一般會設定為使用 TCP 連接埠 4022，不過您可以設定不同的連接埠。 請指定沒有其他站台或服務使用且不會因防火牆限制而被封鎖的有效連接埠。  

    - **使用現有 SQL Server 執行個體**  

        - **SQL Server FQDN**：檢閱執行 SQL Server 之電腦的 FQDN。 您必須使用執行 SQL Server 的本機伺服器來裝載次要站台資料庫，且不能修改這個設定。  

        - **SQL Server 執行個體**：指定作為次要站台資料庫使用的 SQL Server 執行個體。 讓此選項保持空白，以使用預設執行個體。  

        - **ConfigMgr 站台資料庫名稱**：指定用於次要站台資料庫的名稱。  

        - **SQL Server Broker 連接埠**：指定 SQL Server 使用的 SQL Server Service Broker (SSB) 連接埠。 請指定沒有其他網站或服務在使用，且不會因防火牆限制而被封鎖的有效連接埠。  

    > [!TIP]  
    > 如需 Configuration Manager 所支援的 SQL Server 版本清單，請參閱[支援的 SQL Server 版本](../../../plan-design/configs/support-for-sql-server-versions.md)。  

7. 在 [發佈點]  頁面上，為將會安裝在次要站台伺服器的發佈點進行設定。  

    - **必要設定：**  

        - **指定用戶端裝置與發佈點通訊的方式**：選擇 HTTP 與 HTTPS。  

        - **建立自我簽署憑證或匯入 PKI 用戶端憑證**：選擇使用自我簽署憑證，或從您的 PKI 匯入憑證。 自我簽署憑證讓您也可允許從 Configuration Manager 用戶端以匿名方式非同步連線到內容庫。 憑證可用於在發佈點傳送狀態訊息之前，對管理點驗證發佈點。 如需詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。  

    - **選擇性設定：**  

        - **在 Configuration Manager 需要時安裝並設定 IIS**：選取此設定，讓 Configuration Manager 在伺服器上安裝及設定 Internet Information Services (IIS) (如果尚未安裝)。 所有發佈點都需要 IIS。  

            > [!NOTE]  
            > 雖然這項設定為選擇性，但 IIS 必須安裝在伺服器上，才可順利安裝發佈點。  

        - **啟用並設定此發佈點的 BranchCache**  

        - **描述**：此值是發佈點的易記描述，可協助您辨識它。  

        - **啟用此發佈點供預先設置的內容使用**  

8. 在 [磁碟機設定]  頁面上，為次要站台發佈點指定磁碟機設定。  

    您可以為內容庫設定最多兩部磁碟機，以及為套件共用設定兩部磁碟機。 不過，當前兩部磁碟機達到設定的磁碟機空間保留時，Configuration Manager 可以使用其他磁碟機。 您可以在 [磁碟機設定]  頁面設定磁碟機的優先順序，以及每個磁碟機上能保留的可用磁碟空間量。  

    - **磁碟機空間保留 (MB)** ：您為此設定所設的值，可在 Configuration Manager 選擇不同磁碟機並繼續對該磁碟進行複製程序前，判斷磁碟機上的可用空間數量。 內容檔案可以跨越多個磁碟機。  

    - **內容位置**：指定內容庫和套件共用的內容位置。 Configuration Manager 會將內容複製到主要內容位置，直到可用空間量達到 [磁碟機空間保留 (MB)]  指定的值為止。  

    根據預設，內容位置會設定為 [自動]  。 主要內容位置會設定為在安裝時擁有最多磁碟空間的磁碟機。 次要位置則會設定為在主要磁碟機之後擁有最多可用磁碟空間的磁碟機。 當主要和次要磁碟機都達到磁碟機空間保留的設定時，Configuration Manager 會選取其他具備最多可用磁碟空間的磁碟機，然後繼續進行複製程序。  

9. 在 [內容驗證]  頁面上，指定是否驗證發佈點上內容檔的完整性。  

    - 當您依照排程啟用內容驗證時，Configuration Manager 會於排程的時間啟動程序。 發佈點上的所有內容都會進行驗證。  

    - 您也可以設定 **內容驗證優先順序**。  

    - 若要檢視內容驗證程序的結果，請在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [發佈狀態]  ，然後按一下 [內容狀態]  節點。 它會顯示每個套件類型的內容。 這些類型包括應用程式、軟體更新套件和開機映像。  

10. 在 [界限群組]  頁面上，管理已指派此發佈點的界限群組：  

    - 部署內容期間，用戶端必須存在於與發佈點關聯的界限群組之中，才能將界限群組當成內容的來源位置使用。  

    - 您可以選取 [允許內容的後援來源位置]  選項，讓這些界限群組外的用戶端在沒有可用的慣用發佈點時，退回並使用發佈點作為內容來源位置。  

        如需詳細資訊，請參閱[內容管理的基本概念](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

11. 在 [摘要]  頁面上驗證設定，然後選擇 [下一步]  安裝次要站台。 當精靈出現 [完成]  頁面時，即可關閉精靈。 次要站台安裝會繼續於背景執行。  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> 如何驗證次要站台安裝狀態  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取您要安裝的次要站台，然後選擇功能區中的 [顯示安裝狀態]  。  

    > [!TIP]  
    > 當您一次安裝多個次要站台時，先決條件檢查程式一次只能檢查一個站台。 它必須在開始檢查下一個站台之前完成一個站台。  
