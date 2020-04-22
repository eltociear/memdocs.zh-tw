---
title: 建立獨立媒體
titleSuffix: Configuration Manager
description: 使用獨立媒體來在沒有網路連線的電腦上部署 OS。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e477d08ed97fe46bbe51b62a0ed024d437c2626
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690566"
---
# <a name="create-stand-alone-media"></a>建立獨立媒體

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的獨立媒體包含在沒有網路連線的電腦上部署 OS 所需的所有內容。

搭配使用獨立媒體與下列 OS 部署案例：  

- [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

- [升級至最新版本的 Windows](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>使用方式

獨立媒體包含的工作順序會自動安裝作業系統和所有其他必要內容的步驟。 此內容包括開機映像、OS 映像及裝置驅動程式。 由於獨立媒體儲存用於部署 OS 的所有項目，因此它需要比其他類型媒體更多的磁碟空間。

當您在管理中心網站上建立獨立媒體時，用戶端會從 Active Directory 擷取其指派的站台碼。 建立於子站台上的獨立媒體會將該站台的站台碼自動指派給用戶端。  


## <a name="prerequisites"></a>先決條件

在使用 [建立工作順序媒體精靈] 建立獨立媒體之前，請先確定符合所有這些條件。

### <a name="create-a-task-sequence-to-deploy-an-os"></a>建立部署 OS 的工作順序

作為獨立媒體的一部分，請指定工作順序以部署 OS。 如需詳細資訊，請參閱[建立工作順序以安裝 OS](create-a-task-sequence-to-install-an-operating-system.md)。

#### <a name="unsupported-actions-for-stand-alone-media"></a>獨立媒體不支援的動作

獨立媒體不支援下列動作：

- 工作順序中的 [自動套用驅動程式](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) 步驟。 獨立媒體不支援從驅動程式類別目錄自動套用裝置驅動程式。 使用 [套用驅動程式套件](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) 步驟可讓 Windows 安裝程式使用一組指定的驅動程式。  

- 工作順序中的 [下載套件內容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) 步驟。 管理點資訊無法在獨立媒體上使用，因此嘗試列舉內容位置的步驟會失敗。  

- 安裝軟體更新。  

- 在部署 OS 之前安裝軟體。  

- 適用於非 OS 部署的自訂工作順序。  

- 為使用者與目的地電腦建立關聯，以支援使用者裝置親和性。  

- 動態套件會透過[安裝套件](../understand/task-sequence-steps.md#BKMK_InstallPackage)步驟進行安裝。  

- 動態應用程式會透過[安裝應用程式](../understand/task-sequence-steps.md#BKMK_InstallApplication)步驟進行安裝。

- [設定 Windows 和 ConfigMgr]  工作順序步驟中的 [使用生產前的用戶端封裝 (如可使用)]  設定。 如需此設定的詳細資訊，請參閱[設定 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。  

> [!NOTE]  
> 如果您的工作順序包含[安裝套件](../understand/task-sequence-steps.md#BKMK_InstallPackage)步驟，而且您在管理中心網站建立獨立媒體，就有可能會發生錯誤。 管理中心網站並沒有必要的用戶端設定原則。 需要這些原則才能在執行工作順序期間啟用軟體發佈代理程式。 在 **CreateTsMedia.log** 檔案中可能會出現下列錯誤：  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> 如果是包含 [安裝套件]  步驟的獨立媒體，請在已啟用軟體發佈代理程式的主要網站上建立獨立媒體。
>
> 或者，請使用自訂的[執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟。 將它加入至[設定 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) 步驟之後，以及 [安裝套件]  步驟之前。 [執行命令列]  步驟會執行下列 WMIC 命令，在第一個 [安裝套件] 步驟執行之前啟用軟體發佈代理程式：  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>發佈與工作順序相關聯的所有內容

將工作順序所需的所有內容都發佈到至少一個發佈點。 此內容包括開機映像、OS 映像，以及其他相關聯的檔案。 精靈會在建立媒體時從發佈點收集內容。

您的使用者帳戶至少需要該發佈點上內容庫的 [讀取]  存取。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

### <a name="prepare-the-removable-usb-drive"></a>準備卸除式 USB 磁碟機

如果您使用的是卸除式 USB 磁碟機，請將它連接到執行 [建立工作順序媒體精靈] 的電腦。 該 USB 磁碟機必須可由 Windows 偵測為卸除式裝置。 精靈會在建立媒體時直接寫入 USB 磁碟機。

獨立媒體使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 之檔案的卸除式 USB 磁碟機上建立獨立媒體。

### <a name="create-an-output-folder"></a>建立輸出資料夾

在您執行 [建立工作順序媒體精靈] 來針對 CD 或 DVD 組建立媒體之前，請先為精靈所建立的輸出檔案建立資料夾。 精靈針對 CD 或 DVD 組所建立的媒體會以 .ISO 檔案的形式直接寫入該資料夾中。


## <a name="process"></a>程序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序媒體]  。 這個動作會啟動 [建立工作順序媒體精靈]。  

3. 在 [選取媒體類型]  頁面上，指定下列選項：  

    - 選取 [獨立媒體]  。  

    - 如果您只想要允許部署 OS，而不需要使用者輸入，可以選擇性地選取 [允許自動部署作業系統]  。  

        > [!IMPORTANT]  
        > 當您選取此選項時，系統就不會提示使用者提供網路設定資訊或選擇性的工作順序。 如果媒體已設定密碼保護，系統仍然會提示使用者輸入密碼。  

4. 在 [媒體類型]  頁面上，指定媒體為 [卸除式 USB 磁碟機]  或 [CD/DVD 組]  。 然後，設定下列選項：  

    > [!IMPORTANT]  
    > 媒體會使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 之檔案的 USB 磁碟機上建立媒體。  

    - 如果您選取 [卸除式 USB 磁碟機]  ，請選取要在其中儲存內容的磁碟機。  

        - **格式化卸除式 USB 磁碟機 (FAT32) 並使其為可開機**：根據預設，讓 Configuration Manager 準備 USB 磁碟機。 許多較新的 UEFI 裝置需要可開機的 FAT32 磁碟分割。 不過，這個格式也會限制檔案大小和磁碟機的整體容量。 如果您已經格式化並設定卸除式磁碟機，請停用此選項。

    - 如果您選取 [CD/DVD 組]  ，請指定媒體的容量 ([媒體大小]  )，以及輸出檔案的名稱和路徑 ([媒體檔案]  )。 精靈會將輸出檔案寫入此位置。 例如：`\\servername\folder\outputfile.iso`  

        如果媒體容量太小而無法儲存整個內容，便會建立多個檔案。 然後，您需要將內容儲存在多個 CD 或 DVD 上。 當它需要多個媒體檔案時，Configuration Manager 會在其所建立的每個輸出檔案名稱上加入序號。  

        如果您同時部署應用程式與 OS，且該應用程式無法容納在單一媒體上，Configuration Manager 會將該應用程式存放在多個媒體上。 獨立媒體執行時，Configuration Manager 會提示使用者儲存應用程式的下一個媒體。  

        > [!IMPORTANT]  
        > 如果您選取現有的 .iso 映像，[工作順序媒體精靈] 會在您繼續進行精靈的下一頁時從磁碟機或共用刪除映像。 即使您取消精靈，還是會刪除現有映像。  

    - **複寫用快取資料夾**<!--1359388-->:媒體建立程序可能會需要大量的暫存磁碟機空間。 根據預設，這個位置類似於下列路徑：`%UserProfile%\AppData\Local\Temp`。 從 1902 版開始，為了提升這些暫存檔存放位置的彈性，您可以將此值變更為另一個磁碟機和路徑。  

    - **媒體標籤**<!--1359388-->:從 1902 版開始，可以將標籤新增至工作順序媒體。 此標籤可協助您在建立媒體之後更輕鬆識別媒體。 預設值為 `Configuration Manager`。 此文字欄位會出現在下列位置：  

        - 如果您掛接 ISO 檔案，Windows 就會顯示此標籤作為掛接的磁碟機名稱  

        - 如果您格式化 USB 磁碟機，它會使用標籤的前 11 個字元作為其名稱  

        - Configuration Manager 會將稱為 `MediaLabel.txt` 的文字檔案寫入媒體的根目錄。 根據預設，此檔案包含一行文字：`label=Configuration Manager`。 如果您自訂媒體標籤，則這一行文字會使用您的自訂標籤，而不是預設值。  

    - **將 autorun.inf 檔案加入媒體**<!-- 4090666 -->:從 1906 版開始，Configuration Manager 預設不會新增 autorun.inf 檔案。 此檔案通常會遭到反惡意程式碼軟體產品的封鎖。 如需 Windows 自動執行功能的詳細資訊，請參閱 [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (建立已啟用自動執行的 CD-ROM 應用程式)。 如果您的案例仍有此需要，請選取此選項來包含該檔案。  

5. 在 [安全性]  頁面上，指定下列選項：

    - **使用密碼保護媒體**：輸入強式密碼來協助防範他人未經授權存取媒體。 當您指定密碼時，使用者必須提供該密碼才能使用媒體。  

        > [!IMPORTANT]  
        > 基於安全性最佳作法，請一律指派密碼以協助保護媒體。  
        >
        > 在獨立媒體上，系統只會加密工作順序步驟與其變數。 系統不會加密其餘的媒體內容。 請不要在工作順序指令碼中包含任何敏感性資訊。 使用工作順序變數儲存與實作所有敏感資訊。  

    - **選取此獨立媒體的有效時間範圍**：在媒體上設定選擇性的開始和到期日期。 預設會停用此設定。 在獨立媒體執行之前，會將這些日期與電腦上的系統時間進行比較。 當系統時間早於開始時間或晚於到期時間時，獨立媒體便不會啟動。 使用 [New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) \(英文\) PowerShell Cmdlet 時也可以使用這些選項。  

6. 在 [獨立 CD/DVD]  頁面上，選取會部署 OS 的工作順序。 您只能選取那些與開機映像相關聯的工作順序。 確認由工作順序參考的內容清單。  

    - **偵測相關聯的應用程式相依性，並將其新增至此媒體**：同時也會針對應用程式相依性將內容新增至媒體。  

        > [!TIP]  
        > 如果您沒有看見預期的應用程式相依性，請取消選取此選項，然後再重新選取它以重新整理清單。  

7. 在 [選取應用程式]  頁面上，指定要包含為媒體檔案之一部分的額外應用程式內容。  

8. 在 [選取套件]  頁面上，指定要包含為媒體檔案之一部分的額外套件內容。  

9. 在 [選取驅動程式套件]  頁面上，指定要包含為媒體檔案之一部分的額外驅動程式套件內容。  

10. 在 [發佈點]  頁面上，指定包含必要內容的發佈點。  

    Configuration Manager 只會顯示擁有內容的發佈點。 先將所有與工作順序建立關聯的內容發佈到至少一個發佈點，才能繼續。 發佈內容之後，重新整理發佈點清單。 移除您已在這個頁面上選取的任何發佈點、移至上一頁，然後回到 [發佈點]  頁面。 或者，重新啟動精靈。 如需詳細資訊，請參閱[發佈工作順序所參考的內容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)和[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

11. 在 [自訂]  頁面上，指定下列選項：  

    - 加入工作順序會使用的任何變數。  

    - **啟用啟動前置命令**：指定您要在工作順序執行前執行的啟動前置命令。 啟動前置命令是在工作順序執行之前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 如需詳細資訊，請參閱[工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        > 在建立媒體時，工作順序會將套件識別碼和啟動前置命令列 (包括任何工作順序變數的值) 寫入執行 Configuration Manager 主控台之電腦的 **CreateTSMedia.log** 檔案中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

        如果啟動前置命令需要任何內容，請選取 [包含啟動前置命令的檔案]  的選項。  

12. 完成精靈。  

獨立媒體檔案 (.ISO) 已於目的地資料夾中建立。 如果您已選取 [CD/DVD 集]  ，請將輸出檔案複製到一組 CD 或 DVD。


## <a name="next-steps"></a>後續步驟

[使用獨立媒體，而不使用網路來部署 Windows](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
