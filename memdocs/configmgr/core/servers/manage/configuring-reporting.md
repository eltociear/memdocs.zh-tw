---
title: 設定報告
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 階層中設定報告，包括 SQL Server Reporting Services 的相關資訊。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b7ada6f54a7642817a321937a4d7128994d5538
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823974"
---
# <a name="configure-reporting-in-configuration-manager"></a>在 Configuration Manager 中設定報告

適用於：Configuration Manager (最新分支)

您必須先完成數個設定工作，才能在 Configuration Manager 主控台中建立、修改和執行報告。 使用本文來協助您在 Configuration Manager 階層中設定報告。  

在於階層中安裝及設定 SQL Server Reporting Services 之前，請先檢閱下列 Configuration Manager 報告文章：  

- [報告簡介](introduction-to-reporting.md)  

- [規劃報告](planning-for-reporting.md)  

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services 是一個以伺服器為基礎的報告平台，可針對不同類型的資料來源提供完整的報告功能。 Configuration Manager 中的 Reporting Services 點會與 SQL Server Reporting Services 通訊以執行下列動作：

- 將 Configuration Manager 報告複製到指定的報告資料夾
- 設定 Reporting Services 設定
- 設定 Reporting Services 安全性設定

當您執行報告時，Reporting Services 元件會連線至 Configuration Manager 站台資料庫以擷取資料。  

在您可以於 Configuration Manager 站台中安裝 Reporting Services 點之前，請先在目標站台系統上安裝及設定 SQL Server Reporting Services。 如需詳細資訊，請參閱[安裝 SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services) \(部分機器翻譯\)。  

### <a name="verify-sql-server-reporting-services-installation"></a>確認 SQL Server Reporting Services 安裝

使用下列程序，確認是否已安裝及正確執行 SQL Server Reporting Services。

1. 移至站台系統上的 [開始] 功能表，然後開啟 [Reporting Services 組態管理員]。 您可以在 [Microsoft SQL Server] 群組的 [組態工具] 區段中找到它。

2. 在 [Reporting Services 組態連接] 視窗中，輸入裝載 SQL Server Reporting Services 的伺服器名稱。 選取您已安裝 SQL Reporting Services 的 SQL Server 執行個體。 然後選取 [連線] 以開啟 Reporting Services 組態管理員。  

3. 在 [報表伺服器狀態] 頁面上，確認 [報表伺服器狀態] 為 [已啟動]。 如果它不是處於此狀態，請選取 [啟動]。  

4. 在 [Web 服務 URL] 頁面上，選取 [報表伺服器 Web 服務 URL] 中的 URL。 此動作會測試針對報告資料夾的連線。 瀏覽器可能會提示您輸入認證。 確認已順利開啟該網頁。

5. 在 [資料庫] 頁面上，確認 [報表伺服器模式] 已設定為 [原生]。  

6. 在 [報表管理員 URL] 頁面上，選取 [報表管理員網站識別] 中的 URL。 此動作會測試報表管理員針對虛擬目錄的連線。 瀏覽器可能會提示您輸入認證。 確認已順利開啟該網頁。

    > [!NOTE]  
    > Configuration Manager 中的報告並不需要 Reporting Services 報表管理員。 您只有在想要於瀏覽器中執行報告，或是使用報表管理員來管理報告時才會需要它。  

7. 選取 [結束] 來關閉 Reporting Services 組態管理員。  

## <a name="configure-reporting-to-use-report-builder-30"></a>設定報告以使用報表產生器 3.0

1. 在執行 Configuration Manager 主控台的電腦上，開啟 Windows 登錄編輯程式。  

2. 瀏覽至 `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ConfigMgr10\AdminUI\Reporting` 。

3. 開啟 [ReportBuilderApplicationManifestName] 機碼以編輯值資料。  

4. 將此值變更為 `ReportBuilder_3_0_0_0.application`，然後選取 [確定] 以儲存。

5. 關閉 Windows 登錄編輯程式。  

## <a name="install-a-reporting-services-point"></a>安裝 Reporting Services 點

若要在站台上管理報告，請安裝 Reporting Services 點。 Reporting Services 點會：

- 將報告資料夾及報告複製到 SQL Server Reporting Services
- 針對報告及資料夾套用安全性原則
- 在 Reporting Services 中設定組態設定

### <a name="requirements-and-limitations"></a>需求及限制

在您可以於 Configuration Manager 主控台中檢視或管理報告之前，您需要先有 Reporting Services 點。 在具有 Microsoft SQL Server Reporting Services 的伺服器上設定此站台系統角色。 如需詳細資訊，請參閱[報告的必要條件](prerequisites-for-reporting.md)。  

- 選取站台以安裝 Reporting Services 點時，將存取報告的使用者必須位於與安裝該角色的站台相同的安全性範圍。  

- 在您於站台伺服器上安裝 Reporting Services 點之後，請勿變更報表伺服器的 URL。

    例如，您建立 Reporting Services 點。 您接著在 Reporting Services 組態管理員中修改報表伺服器的 URL。 Configuration Manager 主控台繼續使用舊的 URL。 您無法從主控台執行、編輯或建立報告。

    如果您需要變更報表伺服器 URL，請先移除現有的 Reporting Services 點。 變更 URL，然後重新安裝 Reporting Services 點。  

- 當您安裝 Reporting Services 點時，請指定 [Reporting Services 點帳戶](../../plan-design/hierarchy/accounts.md#reporting-services-point-account)。 若要讓來自不同網域的使用者執行報告，請在網域之間建立雙向信任。 否則報告將會無法執行。

### <a name="install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> 在站台系統上安裝 Reporting Services 點  

如需設定站台系統的詳細資訊，請參閱[安裝站台系統角色](../deploy/configure/install-site-system-roles.md)。  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，並展開 [站台設定]，然後選取 [伺服器和站台系統角色] 節點。  

1. 將 Reporting Services 點加入新的或現有的站台系統伺服器：  

    - *新增站台系統*：在功能區的 [常用] 索引標籤上，於 [建立] 群組中，選取 [建立站台系統伺服器]。 隨即開啟 [建立站台系統伺服器精靈]  。  

    - *現有的站台系統*：選取目標伺服器。 在功能區的 [常用] 索引標籤上，於 [伺服器] 群組中，選取 [新增站台系統角色]。 隨即開啟 [新增站台系統角色精靈]  。  

1. 在 [一般]  頁面上，指定網站系統伺服器的一般設定。 將 Reporting Services 點加入現有伺服器時，請確認您之前設定的值。  

1. 在 [系統角色選取] 頁面上，於可用角色清單中選取 [Reporting Services 點]，然後選取 [下一步]。  

1. 在 [Reporting Services 點] 頁面上，設定下列設定：  

    - **站台資料庫伺服器名稱**：指定裝載 Configuration Manager 站台資料庫的伺服器名稱。 精靈通常會擷取伺服器的完整網域名稱 (FQDN)。 若要指定資料庫執行個體，請使用 &lt;*伺服器名稱*>\&lt;*執行個體名稱*> 的格式。 例如 `sqlserver\named1`。

    - **資料庫名稱**：指定 Configuration Manager 站台資料庫名稱。 選取 [確認] 以確認精靈可以存取站台資料庫。  

        > [!IMPORTANT]  
        > 您用來建立 Reporting Services 點的使用者帳戶必須具有站台資料庫的**讀取**存取權限。 如果連線測試失敗，則會顯示紅色警告圖示。 圖示上的內容相關暫留文字具有失敗的詳細資料。 更正錯誤，然後再次選取 [測試]。  

    - **資料夾名稱**：指定要在 Reporting Services 中建立及用於 Configuration Manager 報告的資料夾名稱。  

    - **Reporting Services 伺服器執行個體**：選取 Reporting Services 的 SQL Server 執行個體。 如果此頁面未列出任何執行個體，請確認已安裝、設定及啟動 SQL Server Reporting Services。  

        > [!IMPORTANT]  
        > Configuration Manager 會以目前使用者的內容對選取站台系統上的 WMI 建立連線。 它會使用此連線來擷取 Reporting Services 的 SQL Server 執行個體。 目前的使用者必須擁有站台系統上 WMI 的**讀取**權限，否則精靈會無法取得 Reporting Services 執行個體。  

    - **Reporting Services 點帳戶**：選取 [設定]，然後選取要使用的帳戶。 Reporting Services 點上的 SQL Server Reporting Services 會使用此帳戶來連線至 Configuration Manager 站台資料庫。 此連線是用來擷取報告的資料。 選取 [現有的帳戶] 來指定您先前設定為 Configuration Manager 帳戶的 Windows 使用者帳戶。 選取 [新增帳戶] 來指定目前尚未設定使用的 Windows 使用者帳戶。 Configuration Manager 會自動授與指定之使用者存取站台資料庫的權限。  

        執行 Reporting Services 的帳戶必須屬於網域本機安全性群組 [Windows Authorization Access Group]。 這會授與帳戶網域內所有使用者物件上之 **tokenGroupsGlobalAndUniversal** 屬性的 [允許讀取] 權限。 針對位於和 Reporting Services 點帳戶不同網域的使用者，需要在網域之間建立雙向信任，他們才能成功執行報告。

        指定的 Windows 使用者帳戶和密碼會經過加密，並儲存於 Reporting Services 資料庫中。 Reporting Services 會使用此帳戶和密碼，擷取來自站台資料庫的報告資料。  

        > [!IMPORTANT]  
        > 您所指定的帳戶在裝載 Reporting Services 資料庫的電腦上，必須擁有**本機登入**權限。  

1. 完成精靈。

在精靈完成之後，Configuration Manager 會在 Reporting Services 中建立報告資料夾。 它接著會將其報告複製到指定的報告資料夾。  

> [!TIP]  
> 若只要列出裝載 Reporting Services 點站台角色的站台系統，請以滑鼠右鍵按一下 [伺服器和站台系統角色]，然後選取 [Reporting Services 點]。  

### <a name="languages-for-reports"></a><a name="bkmk_languages" /> 報表的語言

<!-- SCCMDocs#1067 -->

當 Configuration Manager 建立報告資料夾，並將報告複製到報表伺服器時，它會判斷物件的適當語言。

- 建立報告資料夾，複製報告

  - 使用站台伺服器 OS 的地區設定來建立物件

  - 如果無法使用特定的語言套件，便會預設為英文 (ENU)

- 在網頁瀏覽器中檢視報告

  - 資料夾和報告名稱：與站台伺服器相同的地區設定
  
  - 報告內容：根據瀏覽器地區設定來動態設定

- 在 Configuration Manager 主控台中檢視報告

  - 資料夾和報告名稱：根據主控台的地區設定來動態設定
  
  - 報告內容：根據主控台的地區設定來動態設定

當您在不含語言套件的站台上安裝 Reporting Services 點時，會安裝英文版的報告。 如果在安裝 Reporting Services 點後安裝語言套件，您必須先解除安裝再重新安裝 Reporting Serivces 點，才能使用具適當語言套件的報告。  

如需詳細資訊，請參閱[語言套件](../deploy/install/language-packs.md)。

### <a name="file-installation-and-report-folder-security-rights"></a>檔案安裝與報表資料夾安全性權限

Configuration Manager 會執行下列動作，以安裝 Reporting Services 點和設定 Reporting Services：  

> [!IMPORTANT]  
> 站台會以針對 SMS_Executive 服務設定的帳戶作為內容來執行這些動作。 通常，此帳戶會是站台伺服器本機 System 帳戶。  

- 安裝 Reporting Services 點站台角色。  

- 在 Reporting Services 中，搭配您在精靈中指定的預存認證來建立資料來源。 此帳戶是 Reporting Services 在您執行報告時用於連線到站台資料庫的 Windows 使用者帳戶和密碼。  

- 在 Reporting Services 中建立 Configuration Manager 根資料夾。  

- 在 Reporting Services 中新增 [ConfigMgr 報告使用者] 和 [ConfigMgr 報告系統管理員] 安全性角色。  

- 建立子資料夾，然後將站台伺服器上 `%ProgramFiles%\SMS_SRSRP` 中的 Configuration Manager 報告部署到 Reporting Services。  

- 將 Reporting Services 中的 [ConfigMgr 報告使用者] 角色新增至 Configuration Manager 中具有 [站台讀取] 權限之所有使用者帳戶的根目錄。  

- 將 Reporting Services 中的 [ConfigMgr 報告系統管理員] 角色新增至 Configuration Manager 中具有 [站台修改] 權限之所有使用者帳戶的根目錄。  

- 擷取報告資料夾及 Configuration Manager 安全物件類型之間的對應。 Configuration Manager 會在站台資料庫中維護此對應。  

- 將 Configuration Manager 中系統管理使用者的下列權限，設定至 Reporting Services 中的特定報告資料夾：  

  - 新增使用者，並將 [ConfigMgr 報告使用者] 角色指派給針對 Configuration Manager 物件具有 [執行報告] 權限之系統管理使用者的相關聯報告資料夾。  

  - 新增使用者，並將 [ConfigMgr 報告系統管理員] 角色指派給針對 Configuration Manager 物件具有 [修改報告] 權限之系統管理使用者的相關聯報告資料夾。  

Configuration Manager 會連接至 Reporting Services，並設定使用者對 Configuration Manager 及 Reporting Services 根資料夾與特定報告資料夾的權限。 在 Reporting Services 點初始安裝完成後，Configuration Manager 每 10 分鐘會連線至 Reporting Services 一次，以確認報告資料夾上所設定的使用者權限會與針對 Configuration Manager 使用者所設定的權限相關聯。 使用 Reporting Services 報表管理員在報告資料夾上新增使用者或修改使用者權限時，Configuration Manager 會使用儲存在站台資料庫中以角色為基礎的指派來覆寫這些變更。 Configuration Manager 也會移除在 Configuration Manager 中沒有報告權限的使用者。  

### <a name="reporting-services-security-roles"></a>Reporting Services 安全性角色

當 Configuration Manager 安裝 Reporting Services 點時，它會在 Reporting Services 中新增下列安全性角色：  

- **ConfigMgr 報告使用者**：獲派此安全性角色的使用者，只可執行 Configuration Manager 報告。  

- **ConfigMgr 報告系統管理員**：獲派此安全性角色的使用者，可以在 Configuration Manager 中執行與報告相關的所有工作。  

## <a name="verify-installation"></a><a name="bkmk_verify"></a> 確認安裝

查看特定狀態訊息及記錄檔項目，來確認 Reporting Services 點的安裝。 利用下列程序確認 Reporting Services 點安裝成功。  

> [!Note]  
> 如果您在 Configuration Manager 主控台 [監視] 工作區之 [報告] 節點的 [報告] 子資料夾中看見報告，則可略過這個程序。

### <a name="verify-installation-by-status-message"></a>依狀態訊息確認安裝

1. 在 Configuration Manager 主控台中，移至 [監視] 工作區，展開 [系統狀態]，然後選取 [元件狀態] 節點。  

1. 選取 **SMS_SRS_REPORTING_POINT** 元件。  

1. 在功能區的 [常用] 索引標籤上，於 [元件] 群組中，選取 [顯示訊息]，然後選擇 [全部]。  

1. 指定安裝 Reporting Services 點之前某一段期間的日期及時間，然後選取 [確定]。  

1. 確認狀態訊息識別碼 **1015**。 此狀態訊息表示 Reporting Services 點已成功安裝。

### <a name="verify-installation-by-log-file"></a>依記錄檔確認安裝

開啟 **Srsrp.log** 檔案 (位於 Configuration Manager 安裝路徑的 **Logs** 目錄中)。 尋找字串 `Installation was successful`。

在此記錄檔中，從 Reporting Services 點成功安裝的時間開始逐步查看。 確認報告資料夾已建立，報告已部署，且每個資料夾上的安全性原則已確認。 在安全性原則確認的最後一行之後，尋找字串 `Successfully checked that the SRS web service is healthy on server`。  

## <a name="configure-a-certificate-to-author-reports"></a>設定憑證以撰寫報告

您有許多選項可用來在 SQL Server Reporting Services 中撰寫報告。 當您在 Configuration Manager 主控台中建立或編輯報告時，Configuration Manager 會開啟報表產生器作為撰寫環境使用。 無論您撰寫 Configuration Manager 報告的方式為何，您都需要自我簽署憑證才能針對站台資料庫伺服器進行伺服器驗證。

> [!NOTE]  
> 如需搭配 SQL Server Reporting Services 撰寫報告的詳細資訊，請參閱[報表產生器撰寫環境](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs) \(部分機器翻譯\)。  

Configuration Manager 會在站台伺服器及任何 SMS 提供者角色上自動安裝憑證。 當您從這些伺服器之一執行 Configuration Manager 主控台時，便可以從中建立或編輯報告。

當您從不同電腦上的 Configuration Manager 主控台建立或修改報告時，請從站台伺服器匯出憑證。 特定憑證的易記名稱是本機電腦 [受信任的人] 憑證存放區中站台伺服器的 FQDN。 在執行 Configuration Manager 主控台之電腦上的 [受信任的人] 憑證存放區中新增此憑證。  

## <a name="modify-reporting-services-point-settings"></a>修改 Reporting Services 點設定

安裝此角色之後，您可以在 Reporting Services 點的內容中修改站台資料庫連接及驗證設定。

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，展開 [站台設定]，然後選取 [伺服器和站台系統角色] 節點。  

    > [!TIP]  
    > 若只要列出裝載 Reporting Services 點的站台系統，請以滑鼠右鍵按一下 [伺服器和站台系統角色] 節點，然後選取 [Reporting Services 點]。  

1. 選取裝載 Reporting Services 點的站台系統。 然後在詳細資料窗格中選取 [Reporting Services 點] 站台系統角色。

1. 在功能區的 [站台角色] 索引標籤上，於 [內容] 群組中，選取 [內容]。  

1. 您可以在 [Reporting Services 點內容] 中修改下列設定：  

    - **站台資料庫伺服器名稱**

    - **資料庫名稱**

    - **使用者帳戶**

1. 選取 [確定] 以儲存變更並關閉內容。  

如需這些設定的詳細資訊，請參閱[在站台系統上安裝 Reporting Services 點](#bkmk_install)一節中的描述。

## <a name="power-bi-report-server"></a>Power BI 報表伺服器

從 2002 版開始，可將報告與 Power BI 報表伺服器整合。 如需如何設定的詳細資訊，請參閱[與 Power BI 報表伺服器整合](powerbi-report-server.md)。

## <a name="upgrade-sql-server"></a>升級 SQL Server

若要升級 SQL Server 和 SQL Server Reporting Services，請先從站台移除 Reporting Services 點。 在您升級 SQL Server 之後，請在 Configuration Manager 中重新安裝 Reporting Services 點。

如果您不遵循此程序，您在從 Configuration Manager 主控台執行或編輯報告時將會看到錯誤。 您可以繼續從網頁瀏覽器成功執行及編輯報告。  

## <a name="configure-report-options"></a>設定報表選項

您可以選取用來管理報告的預設 Reporting Services 點。 站台可以有多個 Reporting Services 點，但它只會使用預設的伺服器來管理報告。 利用下列程序設定站台的報告選項。  

1. 在 Configuration Manager 主控台中，移至 [監視] 工作區，展開 [報告]，然後選取 [報告] 節點。  

1. 在功能區的 [常用] 索引標籤上，於 [設定] 群組中，選取 [報告選項]。  

1. 在清單中選取預設報告伺服器，然後選取 [確定]。

如果未顯示任何伺服器，請確認您已在站台中安裝及設定 Reporting Services 點。 如需詳細資訊，請參閱[確認安裝](#bkmk_verify)。

確定您電腦執行的 SQL Server 報表產生器版本，與您用於報表伺服器的 SQL Server 版本相符。 否則您將會看見錯誤、預設報表伺服器將不會儲存，且您會無法建立或編輯報告。<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>後續步驟

[報告作業和維護](operations-and-maintenance-for-reporting.md)
