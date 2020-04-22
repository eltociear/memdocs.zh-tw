---
title: 建立 OS 升級工作順序
titleSuffix: Configuration Manager
description: 使用工作順序，從 Windows 7 或更新版本自動升級到 Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b11e0a1747cb8303c14f5971b98d337ae7b2a834
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707296"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>在 Configuration Manager 中建立工作順序以升級 OS

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager 中的工作順序，在目的地電腦上自動升級 OS。 這項升級可以從 Windows 7 或更新版本到 Windows 10，或從 Windows Server 2012 或更新版本到 Windows Server 2016。 建立可參考 OS 升級套件以及要安裝之任何其他內容 (例如應用程式或軟體更新) 的工作順序。 升級 OS 的工作順序是[將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)案例的一部分。  


## <a name="prerequisites"></a>先決條件

建立工作順序之前，必須備妥下列需求：

### <a name="required"></a>必要

- Configuration Manager 主控台中必須有 [OS 升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

- 升級到 Windows Server 2016 時，請在 [升級作業系統] 工作順序步驟中選取 [忽略任何可解除的相容性訊息]  設定。 否則，升級會失敗。  

### <a name="required-if-used"></a>必要 (如果有用到)  

- [軟體更新](../../sum/get-started/synchronize-software-updates.md)必須在 Configuration Manager 主控台中進行同步處理。  

- Configuration Manager 主控台中必須新增[應用程式](../../apps/deploy-use/create-applications.md)。  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a> 建立工作順序以升級 OS  

若要升級用戶端上的 OS，請建立工作順序，並在 [建立工作順序精靈] 中選取 [從升級套件升級作業系統]  。 該精靈會新增工作順序步驟以升級 OS、套用軟體更新，以及安裝應用程式。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序]  。  

3. 在 [建立工作順序精靈] 的 [建立新的工作順序]  頁面上，選取 [從升級套件升級作業系統]  ，然後選取 [下一步]  。  

4. 在 [工作順序資訊]  頁面上指定下列設定：  

    - **工作順序名稱**：指定識別工作順序的名稱。  

    - **描述**：選擇性指定描述。  

5. 在 [升級 Windows 作業系統]  頁面上，指定下列設定：  

    - **升級套件**：指定包含 OS 升級來源檔案的升級套件。 查看 [內容]  窗格的資訊，以確認已選取正確的升級套件。 如需詳細資訊，請參閱[管理 OS 升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

    - **版本索引**：如果套件中有多個 OS 版本索引，請選取所需的版本索引。 根據預設，精靈會選取第一個索引。  

    - **產品金鑰**：指定所要安裝 OS 的 Windows 產品金鑰。 請指定編碼的大量授權金鑰或標準產品金鑰。 如果您使用標準產品金鑰，請以虛線 (`-`) 分隔五個字元的每個群組。 例如：`XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`。 當大量授權版本進行升級時，可能不需要產品金鑰。  

        > [!Note]  
        > 此產品金鑰可為多次啟用金鑰 (MAK) 或泛型的大量授權金鑰 (GVLK)。 GVLK 也稱為金鑰管理服務 (KMS) 的用戶端安裝金鑰。 如需詳細資訊，請參閱[大量啟用計劃](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 用戶端安裝金鑰的清單，請參閱＜Windows Server 啟用指南 ＞的[附錄 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。

    - **忽略任何可解除的相容性訊息**：如果要升級到 Windows Server 2016，請選取此設定。 如果您未選取此設定，則工作順序將會失敗，因為 Windows 安裝程式會等待使用者選取 Windows 應用程式相容性對話方塊中的 [確認]  。  

6. 在 [包含更新]  頁面上，指定是否要安裝必要或全部的軟體更新，或者不要安裝任何軟體更新。 然後選取 [下一步]  。 如果您指定安裝軟體更新，Configuration Manager 只會將目標更新安裝至目的地電腦為其成員的集合。  

7. 在 [安裝應用程式]  頁面上，指定要安裝在目的地電腦上的應用程式，然後選取 [下一步]  。 如果您選取多個應用程式，也可以指定工作順序應在特定應用程式安裝失敗時繼續執行。  

8. 完成精靈。  

> [!Important]  
> 在裝置上執行工作順序時，Configuration Manager 用戶端會建立數個指令碼，以控制各種案例中的工作順序行為。 完成工作順序後，除非重新啟動電腦，否則用戶端並不會移除這些指令碼。 這些指令檔未包含機密資訊。  

Windows 10 就地升級的預設工作順序範本包含其他群組，其中具有要在升級程序前後新增的建議動作。 這些動作在許多已順利升級到 Windows 10 裝置的客戶之間是通用的。 如需詳細資訊，請參閱建議的工作順序步驟來[準備升級](#recommended-task-sequence-steps-to-prepare-for-upgrade)和[進行後續處理](#recommended-task-sequence-steps-for-post-processing)。

從 1806 版開始，此工作順序範本也包含一個群組並附帶新增的建議動作，以防升級程序失敗。 有了這些動作，解決問題就簡單多了。 如需詳細資訊，請參閱[失敗時建議的工作順序步驟](#recommended-task-sequence-steps-on-failure)。<!--1358500-->  


## <a name="configure-pre-cache-content"></a>設定預先快取內容

<!--1021244-->
工作順序之可用部署的預先快取功能，可讓用戶端在使用者安裝工作順序之前下載相關 OS 升級套件內容。  

如需詳細資訊，請參閱[設定預先快取內容](configure-precache-content.md)。


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>建議的準備升級工作順序步驟

Windows 10 就地升級的預設工作順序範本包含其他群組，其中具有要在升級程序前新增的建議動作。 **準備升級**群組中的這些動作，在許多已順利升級到 Windows 10 裝置的客戶之間是通用的。 如果您的現有工作順序尚未具備這些動作，請手動將其新增至您工作順序中的 [準備升級]  群組。  

### <a name="battery-checks"></a>電池檢查

在此群組中新增步驟，以確認電腦是使用電池還是電線。 此動作需要自訂指令碼或公用程式來執行這項檢查。

#### <a name="battery-check-example"></a>電池檢查範例

使用 WbemTest 並連線到 `root\cimv2` 命名空間。 接著執行下列查詢：

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

若它傳回任何結果，則裝置是以電池電力執行。 否則，裝置已連接到市電。  

### <a name="networkwired-connection-checks"></a>網路/有線連線檢查

在此群組中新增步驟，以確認電腦是否連線到網路，且未使用無線連線。 此動作需要自訂指令碼或公用程式來執行這項檢查。

#### <a name="network-check-example"></a>網路檢查範例

使用 WbemTest 並連線到 `root\cimv2` 命名空間。 接著執行下列查詢：

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

若它傳回任何結果，則裝置是以 Wi-Fi 執行。 否則，裝置已連線到有線網路連線。

### <a name="remove-incompatible-applications"></a>移除不相容的應用程式

在此群組中新增步驟，以移除與此版本 Windows 10 不相容的任何應用程式。 將應用程式解除安裝的方法各不相同。  

如果應用程式使用 Windows Installer，請從應用程式之 Windows Installer 部署類型內容的 [程式]  索引標籤中複製**解除安裝程式**命令列。 然後使用解除安裝程式命令列，在此群組中新增**執行命令列**步驟。 例如：

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>移除不相容的驅動程式

在此群組中新增步驟，以移除與此版本 Windows 10 不相容的任何驅動程式。  

### <a name="removesuspend-third-party-security"></a>移除/暫止協力廠商安全性

在此群組中新增步驟，以移除或暫止協力廠商安全性程式，例如防毒軟體。  

如果您使用協力廠商的磁碟加密程式，請使用 `/ReflectDrivers` [命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers) \(部分機器翻譯\)，將其加密驅動程式提供給 Windows 安裝程式。 在此群組的工作順序中，新增[設定工作順序變數](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步驟。 將工作順序變數設為 **OSDSetupAdditionalUpgradeOptions**。 搭配驅動程式的路徑來將值設為 `/ReflectDrivers`。 這個[工作順序變數](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)會附加工作順序所使用的 Windows 安裝程式命令列。 如需這個程序的任何其他指引，請連絡您的軟體廠商。  

### <a name="download-package-content-task-sequence-step"></a>下載套件內容的工作順序步驟  

在下列案例中的 [升級作業系統]  步驟之前，使用[下載套件內容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)步驟：  

- 您使用同時適用於 x86 和 x64 平台的單一升級工作順序。 [準備升級]  群組中包含兩個 [下載套件內容]  步驟。 在每個步驟上設定條件來偵測用戶端架構。 此條件會導致只下載適當 OS 升級套件的步驟。 將每個 **下載套件內容** 步驟設定為使用相同的變數，並使用該變數來代表 **升級作業系統** 步驟中的媒體路徑。  

- 若要動態下載適用的驅動程式套件，請使用兩個 **下載套件內容** 步驟，並設定條件來偵測每個驅動程式套件適用的硬體類型。 設定每個 [下載套件內容]  步驟，以使用相同的變數。 然後將該變數用於 [升級作業系統]  步驟上驅動程式區段中的 [分段內容]  值。  

    > [!NOTE]  
    > Configuration Manager 會在變數名稱後面加上數值尾碼。 例如，如果您將 `%mycontent%` 指定為自訂變數，則用戶端會在此位置儲存所有參考的內容。 當您在後續步驟 (例如 [升級作業系統]  ) 中參考此變數時，請使用加上數值尾碼的變數。 在這個範例中，`%mycontent01%` 或 `%mycontent02%` 中的數字會對應 [下載套件內容]  步驟列出此特定內容的順序。  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>建議的後續處理工作順序步驟

建立工作順序之後，在工作順序的**後續處理**群組中新增其他步驟。  

> [!NOTE]  
> 此工作順序並非線性順序。 步驟中有一些可能會影響工作順序結果的條件。 此行為取決於是否成功升級用戶端電腦，或者是否必須將用戶端電腦回復到原始的 OS。  

Windows 10 就地升級的預設工作順序範本包含其他群組，其中具有要在升級程序後新增的建議動作。 **後續處理**群組中的這些動作，在許多已順利升級到 Windows 10 裝置的客戶之間是通用的。 如果您的現有工作順序尚未具備這些動作，請手動將其新增至您工作順序的 [後續處理]  群組。  

### <a name="apply-setup-based-drivers"></a>套用以安裝程式為基礎的驅動程式

在此群組中新增步驟以從套件安裝以安裝程式為基礎的驅動程式 (.exe)。  

### <a name="installenable-third-party-security"></a>安裝/啟用協力廠商安全性

在此群組中新增步驟，以安裝或啟用協力廠商安全性程式，例如防毒軟體。  

### <a name="set-windows-default-apps-and-associations"></a>設定 Windows 預設應用程式與關聯

在此群組中新增步驟以設定 Windows 預設應用程式與檔案關聯。

1. 使用您所需的應用程式關聯來準備參照電腦。
1. 執行下列命令列來匯出：  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. 將 XML 檔案新增至套件。
1. 在此群組中新增[執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟。 指定包含 XML 檔案的套件，然後指定下列命令列：  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

如需詳細資訊，請參閱[匯出或匯入預設應用程式關聯](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)。

### <a name="apply-customizations-and-personalization"></a>套用自訂項目與個人化項目

在此群組中新增步驟以套用 [開始] 功能表自訂項目，例如組織程式群組。 如需詳細資訊，請參閱[自訂開始畫面](/windows-hardware/manufacture/desktop/customize-the-start-screen)。  


## <a name="optional-task-sequence-steps-for-rollback"></a>選擇性的復原工作順序步驟  

重新啟動電腦之後若升級程序出錯，Windows 安裝程式會將系統復原為先前的 OS。 工作順序接著會繼續執行**復原**群組中的任何步驟。 建立工作順序之後，請視需要此群組中新增選擇性步驟。 例如，回復在準備升級群組中對系統所做的任何變更，例如，解除安裝不相容的軟體。


## <a name="recommended-task-sequence-steps-on-failure"></a>失敗時的建議工作順序步驟

<!--1358500-->
從 1806 版開始，Windows 10 就地升級的預設工作順序範本會包含一個群組，以**在失敗時執行動作**。 此群組包含要新增以防升級程序失敗的建議動作。 有了這些動作，解決問題就簡單多了。

### <a name="collect-logs"></a>收集記錄檔

若要從用戶端收集記錄檔，請將步驟加入此群組中。  

- 常見的作法是將記錄檔複製到網路共享位置。 若要建立此連線，請使用[連線到網路資料夾](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)步驟。  

- 若要執行複製作業，請使用自訂的指令碼或公用程式並配合[執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)或[執行 PowerShell 指令碼](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)步驟。  

- 要收集的檔案可能包含下列記錄檔：  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- 如需有關 setupact.log 和其他 Windows 安裝程式記錄檔的詳細資訊，請參閱 [Windows 安裝程式記錄檔](https://docs.microsoft.com/windows/deployment/upgrade/log-files)。  

- 如需 Configuration Manager 用戶端記錄檔的詳細資訊，請參閱 [Configuration Manager 用戶端記錄檔](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs)。  

- 如需有關 **_SMSTSLogPath** 及其他實用變數的詳細資訊，請參閱[工作順序變數](../understand/task-sequence-variables.md)。  

### <a name="run-diagnostic-tools"></a>執行診斷工具

若要執行其他診斷工具，請將步驟加入此群組中。 自動執行這些工具，以便在失敗後立即從系統收集其他資訊。  

Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) 就是這種工具之一。 它是獨立診斷工具，可用來取得 Windows 10 升級為何失敗的詳細資料。  

- 在 Configuration Manager 中，為工具[建立套件](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program)。  

- 將[執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟新增至此工作順序群組。 使用 [套件]  選項來參考此工具。 下列字串是一個**範例命令列**範例：  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  


## <a name="additional-recommendations"></a>其他建議

### <a name="windows-documentation"></a>Windows 文件

檢閱 Windows 文件以[解決 Windows 10 升級錯誤](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)。 這篇文章也包含有關升級程序的詳細資訊。  

### <a name="check-minimum-disk-space"></a>檢查磁碟空間下限

在預設的**檢查整備程度**步驟中，啟用 [確認最小可用磁碟空間 (MB)]  。 針對 32 位元作業系統升級套件，將值設為至少 **16384** (16 GB)，或針對 64 位元設為 **20480** (20 GB)。  

### <a name="retry-downloading-policy"></a>重試下載原則

使用 **SMSTSDownloadRetryCount** [工作順序變數](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount)來重新嘗試下載原則。 目前依預設，用戶端會重試兩次；已將此變數設為二 (2)。 如果您的用戶端不在有線的內部網路連線上，額外的重試次數可協助用戶端取得原則。 使用此變數，如果它無法下載原則，除了延遲失敗以外，不會造成任何負面的副作用。<!--501016--> 此外，從預設的 15 秒增加 **SMSTSDownloadRetryDelay** 變數。  

### <a name="perform-an-inline-compatibility-assessment"></a>執行內嵌相容性指派

1. 提早在**準備升級**群組中新增第二個**升級作業系統**步驟。  

    1. 將其命名為「升級評估」  。
    1. 指定相同的升級套件，然後啟用**執行 Windows 安裝程式相容性掃描但不啟動升級**的選項。
    1. 啟用 [選項] 索引標籤上的 [發生錯誤時繼續]  。  

1. 緊接這個*升級評估*步驟，新增**執行命令列**步驟。 指定下列命令列：

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. 在 [選項]  索引標籤上，新增下列條件：

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

此傳回碼是 MOSETUP_E_COMPAT_SCANONLY (0xC1900210) 的十進位對等項，表示此為成功的相容性掃描，沒有任何問題。 如果「升級評估」  步驟成功並傳回此代碼，工作順序即會略過此步驟。 否則，如果評估步驟傳回任何其他傳回碼，此步驟就會使用Windows 安裝程式相容性掃描的傳回碼來使工作順序失敗。 如需有關 **_SMSTSOSUpgradeActionReturnCode** 的詳細資訊，請參閱[工作順序變數](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)。

如需詳細資訊，請參閱[升級作業系統](../understand/task-sequence-steps.md#BKMK_UpgradeOS)。  

### <a name="convert-from-bios-to-uefi"></a>從 BIOS 轉換至 UEFI

如果您想要在此工作順序期間將裝置從 BIOS 變更為 UEFI，請參閱[在就地升級期間從 BIOS 轉換至 UEFI](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade)。  

### <a name="manage-bitlocker"></a>管理 BitLocker

<!--SCCMDocs issue #494-->
如果您使用 BitLocker 磁碟加密，則根據預設，Windows 安裝程式會在升級期間自動予以暫停。 從 Windows 10 1803 版開始，Windows 安裝程式包含 `/BitLocker` 命令列參數來控制這個行為。 如果您的安全性需求需要一直保持作用中的磁碟加密，則請在 [準備升級]  群組中使用 **OSDSetupAdditionalUpgradeOptions** [工作順序變數](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)來包含 `/BitLocker TryKeepActive`。 如需詳細資訊，請參閱 [Windows 安裝程式命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker)。

### <a name="remove-default-apps"></a>移除預設應用程式

<!--SCCMDocs issue #526-->
有些客戶會移除 Windows 10 中佈建的預設應用程式。 例如，Bing 天氣應用程式或 Microsoft Solitaire Collection。 在某些情況下，這些應用程式會在更新 Windows 10 之後回復。 如需詳細資訊，請參閱[如何讓應用程式從 Windows 10 移除](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update)。

將 [執行命令列]  步驟新增至 [準備升級]  群組中的工作順序。 指定與下列範例類似的命令列：

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
