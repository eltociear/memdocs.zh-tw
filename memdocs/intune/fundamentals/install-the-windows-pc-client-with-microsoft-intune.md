---
title: 安裝電腦用戶端軟體
description: 使用本指南可協助您透過 Microsoft Intune 用戶端軟體管理 Windows 電腦。
keywords: ''
author: ErikjeMS
ms.author: erikje
ms.date: 07/13/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 99dcf916-d80f-42c5-863b-a4595e1ec67a
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: a1641efe6899c46a797a8ccf7979b533cb620d19
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79358958"
---
# <a name="install-the-intune-software-client-on-windows-pcs"></a>在 Windows 電腦上安裝 Intune 軟體用戶端

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> 您可以使用 Microsoft Intune 來管理 Windows 電腦，[其方式包括使用行動裝置管理 (MDM) 作為行動裝置來管理](../enrollment/windows-enroll.md)，或使用 Intune 軟體用戶端作為電腦來管理，如下所述。 不過，Microsoft 建議客戶如有可能盡量[使用 MDM 管理解決方案](../enrollment/windows-enroll.md)。 如需詳細資訊，請參閱[比較作為電腦或行動裝置來管理 Windows 電腦](pc-management-comparison.md) 


Windows 電腦可藉由安裝 Intune 用戶端軟體進行註冊。 Intune 用戶端軟體可以使用下列方式安裝：

- 透過 IT 系統管理員，使用下列其中一種方法：手動安裝、群組原則或磁碟映像中所含的安裝

- 由手動安裝用戶端軟體的使用者安裝

Intune 用戶端軟體包含在 Intune 管理中註冊電腦所需的基本軟體。 註冊電腦之後，Intune 用戶端軟體接著會下載管理電腦時所需的完整用戶端軟體。

此系列下載可降低對網路頻寬的影響，並將在 Intune 中初次註冊電腦時所需的時間縮到最短。 同時也可確保第二個下載完成之後，用戶端都是安裝最新可用的軟體。

一個 Intune 授權可允許在最多五部電腦上安裝 Intune 用戶端軟體。

## <a name="download-the-intune-client-software"></a>下載 Intune 用戶端軟體

除了使用者自行安裝 Intune 用戶端軟體以外的所有方法，都必須由 IT 管理員先下載軟體，然後才能部署至使用者。

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，按一下 [系統管理]  &gt; [用戶端軟體下載]  。

   ![下載 Intune 電腦用戶端](./media/install-the-windows-pc-client-with-microsoft-intune/pc-sa-client-download.png)

2. 在 [用戶端軟體下載]  頁面上，按一下 [下載用戶端軟體]  。 接著將包含軟體的 **Microsoft_Intune_Setup.zip** 套件儲存到網路上的安全位置。

   Intune 用戶端軟體安裝套件包含和您的帳戶有關的唯一且專屬的資訊，並可透過內嵌憑證取得。 若未經授權的使用者能夠取該安裝套件，其便能將電腦註冊到其內嵌憑證所代表的帳戶，從而獲取存取公司資源的權限。

3. 將安裝套件的內容解壓縮到您的網路上安全的位置。

    > [!IMPORTANT]
    > 請不要重新命名或移除已解壓縮的 **ACCOUNTCERT** 檔案，否則用戶端軟體安裝將會失敗。

## <a name="deploy-the-client-software-manually"></a>手動部署用戶端軟體

在將要安裝用戶端軟體的電腦上，移至用戶端軟體安裝檔案所在的資料夾。 接著執行 **Microsoft_Intune_Setup.exe** 安裝用戶端軟體。

> [!NOTE]
> 當您將游標停留在用戶端電腦上工作列中的圖示上時，即可顯示安裝的狀態。

## <a name="deploy-the-client-software-by-using-group-policy"></a>使用群組原則部署用戶端軟體

1. 在包含 **Microsoft_Intune_Setup.exe** 和 **MicrosoftIntune.accountcert** 檔案的資料夾中，執行下列命令以解壓縮適用於 32 位元和 64 位元電腦的 Windows Installer 安裝程式：

    ```
    Microsoft_Intune_Setup.exe/Extract <destination folder>
    ```

2. 將 **Microsoft_Intune_x86.msi** 檔案、**Microsoft_Intune_x64.msi** 檔案及 **MicrosoftIntune.accountcert** 檔案複製到要安裝用戶端軟體，並可供所有電腦可存取的網路位置。

    > [!IMPORTANT]
    > 請勿將這些檔案分開或重新命名，否則用戶端軟體安裝將會失敗。

3. 使用群組原則將軟體部署到您網路上的電腦。

    如需有關如何使用群組原則來自動部署軟體的詳細資訊，請參閱[適用於新手的群組原則](https://technet.microsoft.com/library/hh147307.aspx)。

## <a name="deploy-the-client-software-as-part-of-an-image"></a>隨映像一起部署用戶端軟體
您可以使用下列程序作為前導，將 Intune 用戶端軟體隨著作業系統映像一起部署到電腦：

1. 將用戶端安裝檔案 **Microsoft_Intune_Setup.exe** 及 **MicrosoftIntune.accountcert** 複製到參考電腦的 **%系統磁碟機%\Temp\Microsoft_Intune_Setup** 資料夾。

2. 將下列命令新增至 **SetupComplete.cmd** 指令碼，以建立 **WindowsIntuneEnrollPending** 登錄項目：

    ```cmd
    %windir%\system32\reg.exe add HKEY_LOCAL_MACHINE\Software\Microsoft\Onlinemanagement\Deployment /v
    WindowsIntuneEnrollPending /t REG_DWORD /d 1
    ```

3. 將下列命令新增至 **setupcomplete.cmd**，以使用 /PrepareEnroll 命令列引數執行註冊套件：

    ```cmd
    %systemdrive%\temp\Microsoft_Intune_Setup\Microsoft_Intune_Setup.exe /PrepareEnroll
    ```

    > [!TIP]
    > **SetupComplete.cmd** 指令碼可讓 Windows 安裝程式在使用者登入之前修改系統。 **/PrepareEnroll** 命令列引數會準備目標電腦，以在 Windows 安裝程式完成後自動註冊到 Intune 中。

4. 將 **SetupComplete.cmd** 放在參照電腦的 **%Windir%\Setup\Scripts** 資料夾中。

5. 擷取參照電腦的映像，然後將映像部署到目標電腦。

    當目標電腦在 Windows 安裝程式完成後重新啟動時，便會建立 **WindowsIntuneEnrollPending** 登錄機碼。 註冊套件會檢查電腦是否已經註冊。 如果電腦已註冊，將不會採取進一步的動作。 如果電腦未註冊，註冊套件會建立「Microsoft Intune 自動註冊工作」。

    當自動註冊工作在下次排程時間執行時，會檢查 **WindowsIntuneEnrollPending** 登錄值是否存在，並會嘗試在 Intune 中註冊目標電腦。 如果註冊因為任何原因失敗，工作下次執行時會重新嘗試註冊。 重試會持續一個月。

    當註冊成功或經過一個月之後 (取先達到者)，將會從目標電腦刪除 Intune 自動註冊工作、**WindowsIntuneEnrollPending** 登錄值與帳戶憑證。

## <a name="instruct-users-to-self-enroll"></a>指示使用者自行註冊

使用者前往[公司入口網站](https://portal.manage.microsoft.com)安裝 Intune 用戶端軟體。 使用者在 Web 入口網站中看到的實際資訊可能有所不同，視您帳戶的 MDM 授權單位以及使用者電腦的作業系統平台/版本而定。

如果使用者尚未獲指派 Intune 授權，或者組織的 MDM 授權單位尚未設定為 Intune，則使用者看不到任何註冊選項。

如果使用者已獲指派 Intune 授權，而且組織的 MDM 授權單位已設定為 Intune：

- Windows 7 或 Windows 8 電腦使用者下載並安裝組織特有的電腦用戶端軟體，才會看到註冊 Intune 選項。

- 會向 Windows 10 或 Windows 8.1 電腦使用者顯示兩個註冊選項︰

  - **將電腦註冊為行動裝置**：使用者選擇 [了解如何註冊]  按鈕，並取得如何將其電腦註冊為行動裝置的指示。 因為會將 MDM 註冊視為預設和慣用註冊選項，所以會以醒目方式顯示此按鈕。 不過，MDM 選項不適用於本主題，本主題僅涵蓋用戶端軟體安裝。
  - **使用 Intune 用戶端軟體註冊電腦**︰您需要告訴使用者選取 [Click here to download it]\(按一下這裡下載)  連結，以引導他們進行用戶端軟體安裝。

下表摘要說明選項。

  ![每個平台的預設註冊選項](./media/install-the-windows-pc-client-with-microsoft-intune/default-enrollment-options-table.png)

下列螢幕擷取畫面顯示使用者在使用軟體用戶端註冊其裝置時看到的內容。

系統會先提示使用者識別或註冊其裝置。

  ![識別或註冊裝置](./media/install-the-windows-pc-client-with-microsoft-intune/identify-device-or-enroll.png)

若要讓使用者安裝電腦用戶端軟體，則需要告訴他們選取 [Click here to download it]\(按一下這裡下載)  連結，讓使用者下載電腦用戶端軟體，並帶領他們進行安裝程序。 [了解如何註冊]  按鈕會將使用者帶至有關如何使用 MDM 註冊來註冊的文件，而這與這些軟體用戶端指示無關。

  ![選擇 [Click here to download it]\(按一下這裡下載) 連結](./media/install-the-windows-pc-client-with-microsoft-intune/enroll-your-windows-device.png)

使用者按一下連結時，就會看到 [下載軟體]  按鈕，只要選取它就會啟動電腦用戶端軟體安裝。

  ![選擇 [下載軟體] 更新](./media/install-the-windows-pc-client-with-microsoft-intune/download-pc-client-software.png)

系統接著會要求使用者使用其公司認證登入。

  ![使用您的認證登入](./media/install-the-windows-pc-client-with-microsoft-intune/sign-in-to-intune.png)

系統會將使用者帶至安裝的 [歡迎使用] 頁面。

  ![電腦用戶端安裝的歡迎使用頁面](./media/install-the-windows-pc-client-with-microsoft-intune/welcome-to-pc-agent-install-wizard.png)

使用者選擇 [下一步]  ，然後安裝開始。

  ![電腦用戶端安裝的歡迎使用頁面](./media/install-the-windows-pc-client-with-microsoft-intune/welcome-to-pc-agent-install-wizard.png)

安裝完成時，使用者選擇 [完成]  。

  ![完成電腦用戶端安裝](./media/install-the-windows-pc-client-with-microsoft-intune/completed-the-setup-wizard.png)

如果使用者嘗試在已使用 Intune 電腦用戶端軟體註冊之後將電腦註冊為行動裝置，則會看到下列錯誤畫面。

  ![顯示是否已註冊電腦的畫面](./media/install-the-windows-pc-client-with-microsoft-intune/page-shown-if-pc-already-enrolled.png)

## <a name="monitor-and-validate-successful-client-deployment"></a>監視並驗證成功的用戶端部署
請使用下列其中一個程序協助您監視及驗證成功的用戶端部署。

### <a name="to-verify-the-installation-of-the-client-software-from-the-microsoft-intune-administrator-console"></a>若要從 Microsoft Intune 系統管理員主控台確認用戶端軟體的安裝

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，按一下 [群組]  &gt; [所有裝置]  &gt; [所有電腦]  。

2. 在清單中，尋找正與 Intune 通訊的受管理電腦，或在 [搜尋裝置]  方塊中，輸入電腦名稱或局部名稱來搜尋特定的受管理電腦。

3. 從主控台的下方窗格中，查看電腦的狀態。 解決任何錯誤。

### <a name="to-create-a-computer-inventory-report-to-display-all-enrolled-computers"></a>若要建立電腦清查報表以顯示所有已註冊的電腦

1. 在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，按一下 [報表]  &gt; [電腦清查報表]  。

2. 在 [建立新報表]  頁面上，保留所有欄位的預設值 (除非您要套用篩選器)，然後按一下 [檢視報表]  。

3. [電腦清查報表]  頁面會隨即在新視窗中開啟，顯示已在 Intune 中註冊成功的所有電腦。

    > [!TIP]
    > 按一下報表中的任意欄標題，依該欄的內容排序清單。

## <a name="uninstall-the-windows-client-software"></a>將 Windows 用戶端軟體解除安裝

有兩種方法可以取消註冊 Windows 用戶端軟體：

- 從 Intune 管理主控台 (建議的方法)
- 從用戶端的命令提示字元

### <a name="unenroll-by-using-the-intune-admin-console"></a>使用 Intune 管理主控台取消註冊

若要使用 Intune 管理主控台取消註冊軟體用戶端，請移至 [群組]   >  [所有電腦]   >  [裝置]  。 以滑鼠右鍵按一下用戶端，然後選取 [淘汰/抹除]  。

### <a name="unenroll-by-using-a-command-prompt-on-the-client"></a>使用用戶端上的命令提示字元取消註冊

使用已提高權限的命令提示字元執行下其中一個命令。

**方法 1**：

    "C:\Program Files\Microsoft\OnlineManagement\Common\ProvisioningUtil.exe" /UninstallAgents /MicrosoftIntune

**方法 2** 請注意，並非每個 Windows 的 SKU 上都已安裝這些代理程式：

    wmic product where name="Microsoft Endpoint Protection Management Components" call uninstall
    wmic product where name="Microsoft Intune Notification Service" call uninstall
    wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
    wmic product where name="Microsoft Online Management Policy Agent" call uninstall
    wmic product where name="Microsoft Policy Platform" call uninstall
    wmic product where name="Microsoft Security Client" call uninstall
    wmic product where name="Microsoft Online Management Client" call uninstall
    wmic product where name="Microsoft Online Management Client Service" call uninstall
    wmic product where name="Microsoft Easy Assist v2" call uninstall
    wmic product where name="Microsoft Intune Monitoring Agent" call uninstall
    wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
    wmic product where name="Windows Firewall Configuration Provider" call uninstall
    wmic product where name="Microsoft Intune Center" call uninstall
    wmic product where name="Microsoft Online Management Update Manager" call uninstall
    wmic product where name="Microsoft Online Management Agent Installer" call uninstall
    wmic product where name="Microsoft Intune" call uninstall
    wmic product where name="Windows Endpoint Protection Management Components" call uninstall
    wmic product where name="Windows Intune Notification Service" call uninstall
    wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
    wmic product where name="Windows Online Management Policy Agent" call uninstall
    wmic product where name="Windows Policy Platform" call uninstall
    wmic product where name="Windows Security Client" call uninstall
    wmic product where name="Windows Online Management Client" call uninstall
    wmic product where name="Windows Online Management Client Service" call uninstall
    wmic product where name="Windows Easy Assist v2" call uninstall
    wmic product where name="Windows Intune Monitoring Agent" call uninstall
    wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
    wmic product where name="Windows Firewall Configuration Provider" call uninstall
    wmic product where name="Windows Intune Center" call uninstall
    wmic product where name="Windows Online Management Update Manager" call uninstall
    wmic product where name="Windows Online Management Agent Installer" call uninstall
    wmic product where name="Windows Intune" call uninstall

> [!TIP]
> 取消註冊用戶端時，會針對受影響用戶端留下伺服器端過時記錄。 取消註冊是非同步的，且有九個代理程式要解除安裝，因此最多可能需要 30 分鐘才能完成。

### <a name="check-the-unenrollment-status"></a>檢查取消註冊狀態

檢查 "%ProgramFiles%\Microsoft\OnlineManagement"，並確認左側只有顯示下列目錄：

- AgentInstaller
- 記錄
- Updates
- Common

### <a name="remove-the-onlinemanagement-folder"></a>移除 OnlineManagement 資料夾

取消註冊程序不會移除 [OnlineManagement] 資料夾。 解除安裝之後請等候 30 分鐘，然後執行此命令。 如果太早執行，解除安裝程序可能會停留在未知狀態。 若要移除資料夾，請啟動已提高權限的命令提示字元並執行：

    "rd /s /q %ProgramFiles%\Microsoft\OnlineManagement".

## <a name="next-steps"></a>後續步驟
[使用 Intune 軟體用戶端執行的一般 Windows 電腦管理工作](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
