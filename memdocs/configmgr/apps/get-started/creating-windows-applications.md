---
title: 建立 Windows 應用程式
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中建立和部署 Windows 應用程式的相關資訊。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9e59d850a78a8f45f93769003e7a1de99e5634b3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906393"
---
# <a name="create-windows-applications-in-configuration-manager"></a>在 Configuration Manager 中建立 Windows 應用程式

適用於：  Configuration Manager (最新分支)

建立和部署 Windows 裝置的應用程式時，除了[建立應用程式](../deploy-use/create-applications.md)的其他 Configuration Manager 需求和程序之外，還要考慮下列項目。  

## <a name="general-considerations"></a><a name="bkmk_general"></a> 一般考量  

Configuration Manager 支援部署適用於 Windows 8.1 和 Windows 10 裝置的 Windows 應用程式套件 (.appx) 與應用程式套件組合 (.appxbundle) 格式。

當您在 Configuration Manager 主控台中建立應用程式時，請將應用程式安裝檔案的 [類型]  選取為 [Windows 應用程式套件 (\*.appx、\*.appxbundle、\*.msix、\*.msixbundle)]  。 如需有關建立應用程式的詳細資訊，請參閱[建立應用程式](../deploy-use/create-applications.md)。 如需有關 MSIX 格式的詳細資訊，請參閱[對 MSIX 格式的支援](#bkmk_msix)。

> [!Note]  
> 若要利用 Configuration Manager 的新功能，請先將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a> 為裝置上的所有使用者佈建 Windows 應用程式套件
<!--1358310-->
針對裝置上的所有使用者，使用 Windows 應用程式套件佈建應用程式。 此案例的其中一個常見範例是從商務用和教育用 Microsoft Store，向學校學生所使用的所有裝置佈建應用程式，例如 Minecraft：教育版。 之前，Configuration Manager 只支援針對每位使用者安裝這些應用程式。 在登入新裝置之後，學生就必須等候存取應用程式。 現在，應用程式會針對所有使用者佈建到裝置，讓他們能夠更快速地提高生產力。

> [!Important]  
> 在裝置上安裝、佈建和更新相同 Windows 應用程式套件的不同版本時，請謹慎處理，因為這可能會造成非預期的結果。 使用 Configuration Manager 佈建應用程式，但接著允許使用者從 Microsoft Store 更新應用程式時，可能會發生這種行為。 如需詳細資訊，請參閱[管理從商務用 Microsoft Store 購買的應用程式](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)時的下一個步驟指引。  

佈建離線授權應用程式時，Configuration Manager 不會讓 Windows 從 Microsoft Store 自動進行更新。  

Configuration Manager 支援在所有支援的 Windows 10 版本上佈建應用程式。<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

若要設定這項功能的 Windows 應用程式部署類型，請啟用 [在裝置上為所有使用者佈建此應用程式]  的選項。 如需詳細資訊，請參閱[建立應用程式](../deploy-use/create-applications.md)。

> [!Note]  
> 如果您需要從使用者已登入的裝置解除安裝佈建的應用程式，則需要建立兩個解除安裝部署。 將第一個解除安裝部署的目標設為包含裝置的裝置集合。 將第二個解除安裝部署的目標設為包含使用者的使用者集合，且這些使用者已登入具有佈建應用程式的裝置。 在裝置上解除安裝佈建的應用程式時，Windows 目前也不會為使用者解除安裝該應用程式。

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a> 對 MSIX 格式的支援
<!--1357427-->

Configuration Manager 支援 Windows 10 應用程式套件 (.msix) 與應用程式套件組合 (.msixbundle) 格式。 Windows 10 1809 版或更新版本支援這些格式。

- 如需 MSIX 的概觀，請參閱[深入了解 MSIX](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix) \(英文\)。  

- 如需如何建立新的 MSIX 應用程式，請參閱 [Insider 組建 17682 中引進的 MSIX 支援](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) \(英文\)。  

### <a name="convert-applications-to-msix"></a>將應用程式轉換為 MSIX
<!--3607729, fka 1359029-->

將現有的 Windows Installer (.msi) 應用程式轉換為 MSIX 格式。

#### <a name="prerequisites-for-msix"></a>MSIX 的先決條件

- 執行 Windows 10 1809 版或更新版本的參考裝置  

- 以具備本機系統管理權限的使用者身分在此裝置上登入 Windows  

- 在此裝置上安裝下列應用程式：  

  - Configuration Manager 主控台  

  - 從 Microsoft 網上商店安裝 [MSIX Packaging Tool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF)  

  - 安裝 [MSIX 封裝工具驅動程式](https://docs.microsoft.com/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

請勿在此裝置上安裝任何其他應用程式或服務。 它是您的參考系統。

#### <a name="process-to-convert-applications-to-msix-format"></a>將應用程式轉換為 MSIX 格式的程序

1. 提高 Configuration Manager 主控台權限，移至 [軟體程式庫]  工作區，展開 [應用程式管理]  ，然後選取 [應用程式]  節點。  

2. 選取具備 Windows Installer (.msi) 部署類型的應用程式。  

    > [!Note]  
    > 您需要能夠從參考裝置存取應用程式的來源內容。  
    >
    > 應用程式名稱中不能包含任何特殊字元。 Configuration Manager 會使用應用程式名稱做為輸出檔的名稱。  
    >
    > 請勿在參考裝置上預先安裝此應用程式。  

3. 在功能區中選取 [轉換成 .MSIX]  。

當精靈完成時，MSIX Packaging Tool 會在您於精靈中指定的位置建立一個 MSIX 檔案。 在此過程中，Configuration Manager 會以無訊息方式在參照裝置上安裝應用程式。

如果此程序失敗，[摘要] 頁面就會指向包含詳細資訊的記錄檔。 如果發生與擷取使用者狀態有關的錯誤，請登出 Windows。 再次登入可能會解決此問題。

若要使用此 MSIX 應用程式，您必須先以數位方式簽署它，用戶端才會信任它。 如需有關此程序的詳細資訊，請參閱下列文章：

- [MSIX – MSIX Packaging Tool – 簽署 MSIX 套件](https://docs.microsoft.com/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package) \(英文\)
- [如何使用 SignTool 簽署應用程式套件](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool) \(英文\)

簽署應用程式之後，請在 Configuration Manager 中的應用程式上建立新的部署類型。 如需詳細資訊，請參閱[建立應用程式的部署類型](../deploy-use/create-applications.md#bkmk_create-dt)。

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a> 工作順序部署類型

<!--3555953-->

> [!Note]  
> 在這個版本的 Configuration Manager 中，工作順序部署類型是發行前版本功能。 若要啟用此功能，請參閱[發行前版本功能](../../core/servers/manage/pre-release-features.md)。  

從 2002 版開始，可透過應用程式模型以使用工作順序來安裝複雜的應用程式。 將工作順序部署類型新增至應用程式，以安裝或解除安裝應用程式。 此部署類型提供下列行為：

<!-- - Deploy an app task sequence to a user collection -->

- 在軟體中心內使用圖示顯示應用程式工作順序。 圖示可讓使用者更輕易地尋找和識別應用程式工作順序。

- 定義應用程式工作順序的額外中繼資料，包括當地語系化資訊

您只能將非 OS 部署工作順序作新增為應用程式上的部署類型。 不支援具強烈影響性、OS 部署或 OS 升級工作順序。 <!--A user-targeted deployment still runs in the user context of the local System account.-->

當將此部署類型新增至應用程式時，請在 [工作順序]  頁面上設定其屬性。 如需詳細資訊，請參閱[部署類型的 [工作順序]  選項](../deploy-use/create-applications.md#bkmk_dt-ts)。

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>工作順序部署類型的先決條件

建立自訂工作順序：

- 僅使用非 OS 部署步驟，例如：**安裝套件**、**執行命令列**，或**執行 PowerShell 指令碼**。 如需詳細資訊 (包括支援步驟的完整清單)，請參閱[建立非 OS 部署的工作順序](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)。

- 在工作順序屬性的 [使用者通知]  索引標籤上，請不要選取具強烈影響性的工作順序選項。

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

當建立應用程式時，若要新增工作順序部署類型，則使用者帳戶需要讀取工作順序的權限。<!-- 6348976 --> 請使用下列其中一個選項來設定這些權限：

- 將應用程式系統管理員的使用者帳戶新增至內建**唯讀分析師**角色。 此角色可讓使用者檢視所有 Configuration Manager 物件。

- 複製內建的**應用程式系統管理員**角色，以建立自訂角色。 在**工作順序套件**物件上新增**讀取**權限。

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>工作順序部署類型的已知問題

- 您還無法將應用程式工作順序部署到使用者集合

- 請勿使用此工作順序中的**安裝應用程式**步驟。 請使用[安裝套件](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步驟來安裝應用程式。

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a> 支援通用 Windows 平台 (UWP) 應用程式  

Windows 10 裝置不需要側載金鑰，即可安裝企業營運應用程式。 不過，若要在 Windows 上啟用側載，登錄機碼 `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` 的值必須是 **1**。  

如果您未設定此登錄機碼，Configuration Manager 就會在您初次將應用程式部署到裝置時，自動將此值設為 **1**。 如果您已將此值設為 **0**，Configuration Manager 即無法自動變更此值，而企業營運應用程式部署就會失敗。  

數位簽署 UWP 企業營運應用程式。 使用您要部署應用程式之每個裝置上受信任的程式碼簽署憑證。 使用來自組織 PKI 的憑證，或從 Windows 已信任其公用根憑證的協力廠商提供者購買憑證。  

若要簽署行動裝置應用程式套件，請使用下表來判斷要使用之程式碼簽署憑證的類型：

| 套件  | Symantec  | 非 Symantec  |
|---------|---------|---------|
| Windows 10 行動裝置版裝置上的通用 **.appx** 套件 | 是 | 是 |
| **.xap** 套件 | 是 | 否 |
| 針對 Windows Phone 8.1 建置以安裝在 Windows 10 行動裝置版裝置的 **.appx** 套件 | 是 | 否 |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a> 將 Windows Installer 應用程式部署到已註冊 MDM 的 Windows 10 裝置  

**透過 MDM 的 Windows Installer (\*.msi)** 部署類型可讓您建立以 Windows Installer 為基礎的應用程式，並將其部署到執行 Windows 10 之已註冊 MDM 的裝置上。  

當您使用這個部署類型時，請考慮下列幾點：

- 只能上傳副檔名為 MSI 的單一檔案。  

- Configuration Manager 使用檔案的產品代碼和產品版本來偵測應用程式。  

- Windows 使用應用程式的預設重新啟動行為。 Configuration Manager 不會控制應用程式的重新啟動行為。  

- 針對單一使用者安裝每個使用者的 MSI 套件。  

- 針對裝置上的所有使用者安裝每部電腦的 MSI 套件。  

- Configuration Manager 支援應用程式更新。 每個版本的 MSI 產品代碼都必須相同。  
