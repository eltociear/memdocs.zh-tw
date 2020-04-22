---
title: 適用於現有裝置的 Windows Autopilot
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 工作順序，針對 Windows Autopilot 使用者驅動模式對 Windows 7 裝置重新安裝映像並進行佈建
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709016"
---
# <a name="windows-autopilot-for-existing-devices"></a>適用於現有裝置的 Windows Autopilot
<!--3607717, fka 1358333-->

適用於：  Configuration Manager (最新分支)

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) 可讓組織直接將全新、未被使用的 Windows 10 裝置提供給使用者，並定義使用者須完成的佈建流程，以確保該 Windows 10 裝置的安全性與生產力。 該裝置會向 Windows Autopilot 服務註冊，因此您可以指派必要的 Windows Autopilot 設定檔。 此設定檔會定義該裝置的首次體驗 (OOBE)。 

[適用於現有裝置的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) \(英文\) 可搭配 Windows 10 1809 版或更新版本取得。 此功能可讓您使用單一、原生的 Configuration Manager 工作順序，針對 [Windows Autopilot 使用者驅動模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) \(部分機器翻譯\) 對 Windows 7 裝置重新安裝映像並進行佈建。 



## <a name="prerequisites"></a>先決條件

- 取得 Windows 10 1809 版或更新版本的安裝媒體。 然後，建立 Configuration Manager 作業系統映像。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。

- 在 Microsoft Intune 中，建立適用於 Windows Autopilot 的設定檔。 如需詳細資訊，請參閱[使用 Windows Autopilot 在 Intune 中註冊 Windows 裝置](https://docs.microsoft.com/intune/enrollment-autopilot)。

- 尚未註冊 Windows Autopilot 服務的裝置。 如果裝置已註冊，則將會優先使用指派的設定檔。 現有裝置設定檔的 Autopilot 僅適用於線上設定檔逾時的情況。



## <a name="create-the-configuration-file"></a>建立設定檔

1. 在具有網際網路連線能力的 Windows 裝置上，開啟具系統管理權限的 PowerShell 命令視窗，然後執行下列命令：  

    1. 安裝必要的模組，然後接受提示以繼續  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. 以系統管理員認證登入 Intune  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. 擷取所有與您 Intune 租用戶相關的 Windows Autopilot 設定檔  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. 針對每個設定檔 (Profile) 建立設定檔 (Configuration File)。 這些檔案會命名為設定檔的顯示名稱，並會儲存在目前的使用者桌面上。<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > 每個設定檔 (Configuration File) 只能包含單一設定檔 (Profile)。 每個設定檔 (Profile) 都應該被包含在大括號 `{}` 內。  

2. 將其中一個設定檔儲存至名為 **AutopilotConfigurationFile.json** 的 ANSI 編碼檔案。 將它儲存至適當位置作為 Configuration Manager 套件來源。  

    > [!Tip]  
    > 如果您是使用 PowerShell Cmdlet **Out-File** 來將 JSON 輸出重新導向至某個檔案，它預設會使用 Unicode 編碼。 此 Cmdlet 也可能會截斷較長的行。 請使用 **Set-Content** Cmdlet 搭配 `-Encoding ASCII` 參數來設定正確的文字編碼。   
    > 
    > Windows 記事本預設使用 ANSI 編碼。  

3. 建立包含此檔案的 Configuration Manager 套件。 此套件不需要程式。 如需詳細資訊，請參閱[建立套件](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)。  

    > [!NOTE]  
    > Windows 要求將此檔案命名為 **AutopilotConfigurationFile.json**。 若要使用超過一個 Autopilot 設定檔，請建立個別的 Configuration Manager 套件。  



## <a name="create-the-task-sequence"></a>建立工作順序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。 在功能區中選取 [建立工作順序]  。  

2. 在 [建立新工作順序]  頁面上，選取 [為現有的裝置部署 Windows Autopilot]  的選項。  

3. 在 [工作順序資訊]  頁面中，指定名稱、選擇性新增描述，然後選取開機映像。 如需支援哪些開機映像版本的詳細資訊，請參閱 [Windows 10 支援](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)。  

4. 在 [安裝 Windows]  頁面上，針對 [映像套件]  選取 [Windows 10]。 然後設定以下設定：  

    - **映像索引**：依您組織的需求，選取 [企業版]、[教育版] 或 [專業版]  

    - 啟用 [安裝作業系統之前先分割和格式化目標電腦]  的選項  

    - **設定工作順序以搭配 BitLocker 使用**：如果您啟用這個選項，工作順序將會包含啟用 BitLocker 的必要步驟  

    - **產品金鑰**：如果您需要指定用來啟用 Windows 的產品金鑰，請在此輸入它  

    - 選取下列其中一個選項以設定 Windows 10 中的本機系統管理員帳戶：  
        - **隨機產生本機系統管理員密碼並在所有支援的平台上停用帳戶 (建議)**
        - **啟用帳戶並指定本機系統管理員密碼**

5. 在 [設定網路]  頁面上，選取 [加入工作群組]  的選項。 此工作順序會使用 Windows 系統準備工具 (sysprep)。 如果裝置已加入某個網域，sysprep 將會失敗。  

6. 在 [安裝 Configuration Manager]  頁面中，新增您的環境所需的任何必要安裝內容。  

    > [!Tip]  
    > 只有在 sysprep 執行之前的工作順序期間需要 Configuration Manager 用戶端元件的情況下，工作順序才會需要此資訊。 例如安裝軟體更新或應用程式。 如果您不需要執行這些動作，便不需要該用戶端。 系統會在工作順序執行 sysprep 之前將它解除安裝。  

7. [包含更新]  頁面會預設選取 [不要安裝任何軟體更新]  選項。  

    > [!Tip]  
    > 使用離線映像服務保留包含最新 Windows 10 品質更新的最新映像。 如需詳細資訊，請參閱[部署軟體更新至作業系統映像](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)。  

8. 在 [安裝應用程式]  頁面上，您可以選取要在工作順序期間安裝的應用程式。 但 Microsoft 建議您在這個案例中採用鏡像簽章映像方法。 使用 Autopilot 部署裝置之後，請套用 Microsoft Intune 或 Configuration Manager 共同管理的所有應用程式與組態。 此程序可為接收新裝置和使用現有裝置適用的 Windows Autopilot 的使用者提供一致的體驗。  

8. 在 [系統準備]  頁面上，選取包含 Autopilot 設定檔的套件。 根據預設，工作順序會在電腦執行 Windows Sysprep 之後重新啟動電腦。 您也可以選取 [在此工作順序完成後將電腦關機]  選項。 此選項可讓您準備裝置，然後將它交付給使用者，以提供一致的 Autopilot 體驗。  

9. 完成精靈。  

如果編輯工作順序，就類似於套用現有作業系統映像的預設工作順序。 此工作順序包括下列額外步驟：  

- **套用 Windows Autopilot 設定**：此步驟會套用指定套件中的 Autopilot 設定檔。 它不是新的步驟類型，而是用來複製檔案的 [執行命令列]  步驟。  

- **準備 Windows 以進行擷取**：此步驟會執行 Windows Sysprep，且具有 [在執行此動作後將電腦關機]  的選項。 如需詳細資訊，請參閱[準備 Windows 以進行擷取](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)。  

適用於現有裝置的 Windows Autopilot 工作順序會導致裝置加入 Azure Active Directory (Azure AD)。 

> [!NOTE]  
> 使用 Windows 10 1903 與 1909 版時，Autopilot 有一個已知問題，那就是 Sysprep 會刪除 **AutopilotConfigurationFile.json** 檔案。 如果您使用此方法來部署 Windows 10 1903 或 1909 版，請編輯此工作順序，並進行下列變更：
>
> 1. 停用 [準備 Windows 以進行擷取]  步驟。
> 2. 停用 [準備 Windows 以進行擷取]  步驟之後，立即新增 [執行命令列]  步驟。 設定該步驟以執行下列命令列：`c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> 如需詳細資訊，請參閱 [Windows Autopilot - 已知問題](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues) \(部分機器翻譯\)。

使用商務用 OneDrive [已知資料夾移動](https://docs.microsoft.com/onedrive/redirect-known-folders) \(機器翻譯\) 來確保在升級 Windows 10 之前已備份使用者的資料。



## <a name="next-steps"></a>後續步驟

使用共同管理來強化 Windows 10 裝置的管理功能。 進行共同管理的第二個路徑，是搭配 Windows Autopilot 進行新式佈建。 如需詳細資訊，請參閱下列文章：

- [什麼是共同管理？](../../comanage/overview.md)
- [共同管理的路徑](../../comanage/quickstart-paths.md)
- [搭配共同管理的 Windows Autopilot](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>請參閱

- [使用 Windows AutoPilot 註冊在 Intune 中註冊 Windows 裝置](https://docs.microsoft.com/intune/enrollment-autopilot)
