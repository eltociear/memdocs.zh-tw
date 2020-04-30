---
title: 工作順序步驟
titleSuffix: Configuration Manager
description: 了解您可新增至 Configuration Manager 工作順序的步驟。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 385a7222b33275951de294554a870d8e490a5ddc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702016"
---
# <a name="task-sequence-steps"></a>工作順序步驟

適用於：  Configuration Manager (最新分支)

下列工作順序步驟可以新增至 Configuration Manager 工作順序。 如需詳細資訊，請參閱[使用工作順序編輯器](task-sequence-editor.md)。  

## <a name="common-settings"></a>一般設定

下列是所有工作順序步驟的通用設定：

### <a name="properties-for-all-steps"></a>適用於所有步驟的屬性

- **名稱**：工作順序編輯器會要求您指定簡短名稱來描述此步驟。 當您新增新的步驟時，工作順序編輯器預設會將名稱設定為 [類型]。 [名稱]  長度不能超過 50 個字元。  

- **描述**：選擇性地指定此步驟的更多詳細資訊。 [描述]  長度不能超過 256 個字元。  

本文的其餘部分描述每個工作順序步驟的 [屬性]  索引標籤上的其他設定。

### <a name="options-for-all-steps"></a>適用於所有步驟的選項

- **停用此步驟**：工作順序在電腦上執行時，會略過此步驟。 此步驟中的圖示在工作順序編輯器中將會呈現灰色。  

- **發生錯誤時仍繼續**：如果執行步驟時發生錯誤，工作順序仍會繼續。 如需詳細資訊，請參閱[自動化工作的規劃考量](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups)。  

- **新增條件**：工作順序會評估這些條件陳述式來判斷它是否執行此步驟。 如需使用工作順序變數作為條件的範例，請參閱[如何使用工作順序變數](using-task-sequence-variables.md#bkmk_access-condition)。 如需有關條件的詳細資訊，請參閱[工作順序編輯器 - 條件](task-sequence-editor.md#bkmk_conditions)。

適用於特定工作順序步驟的下列各節描述 [選項]  索引標籤上的其他可能設定。



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> 套用資料映像

您可以使用此步驟，將資料映像複製到指定的目的地磁碟分割。  

此步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [套用資料映像]  。

### <a name="variables-for-apply-data-image"></a>適用於 [套用資料映像] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>適用於 [套用資料映像] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage?view=sccm-ps) \(英文\)
- [New-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDataImage?view=sccm-ps) \(英文\)
- [Remove-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage?view=sccm-ps) \(英文\)
- [Set-CMTSStepApplyDataImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage?view=sccm-ps) \(英文\)

### <a name="properties-for-apply-data-image"></a>適用於 [套用資料映像] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="image-package"></a>映像套件

選取 [瀏覽]  以指定此工作順序所使用的 [映像套件]  。 在 [選取套件]  對話方塊中，選取您想要安裝的套件。 此對話方塊底部會顯示每個現有映像套件的相關內容資訊。 從所選取的 [映像套件]  ，使用下拉式清單來選取您想要安裝的 [映像]  。  

> [!NOTE]  
> 此工作順序動作會將映像視為資料檔案。 此動作不會進行任何設定來將映像當作 OS 進行啟動。  

#### <a name="destination"></a>Destination

設定下列其中一個選項：

- **下一個可用的磁碟分割**：使用這個工作順序中的 [套用作業系統]  或 [套用資料映像]  步驟尚未設為目標的下一個循序磁碟分割。  

- **特定磁碟和磁碟分割**：選取 [磁碟]  編號 (從 0 開始) 和 [磁碟分割]  編號 (從 1 開始)。  

- **特定邏輯磁碟機代號**：指定 Windows PE 指派給磁碟分割的 [磁碟機代號]  。 這個磁碟機代號可以不同於新部署之 OS 所指派的磁碟機代號。  

- **儲存在變數中的邏輯磁碟機代號**：指定工作順序變數，其中包含 Windows PE 指派給磁碟分割的磁碟機代號。 通常會在 [格式化和分割磁碟]  工作順序步驟之 [磁碟分割內容]  對話方塊的 [進階] 區段中，設定此變數。  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>套用映像之前，先刪除磁碟分割上的所有內容  

指定工作順序會在安裝映像之前，刪除目標磁碟分割上的所有檔案。 若不刪除磁碟分割的內容，便可使用此動作將額外內容套用至先前設為目標的磁碟分割。  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> 套用驅動程式套件  

您可以使用此步驟來下載驅動程式套件中的所有驅動程式，並將其安裝在 Windows OS 上。

[套用驅動程式套件]  工作順序步驟讓驅動程式套件中的所有裝置驅動程式皆可供 Windows 使用。 請在 [套用作業系統]  與 [設定 Windows 和 ConfigMgr]  步驟之間新增此步驟，讓套件中的驅動程式可以供 Windows 使用。 [套用驅動程式套件]  工作順序步驟也適合用於獨立媒體部署案例。  

請將相似的裝置驅動程式放在驅動程式套件中，然後將其散發至適當的發佈點。 例如，將某個製造商的所有驅動程式放入一個驅動程式套件。 然後將該套件散發到相關聯的電腦可以存取的發佈點。

[套用驅動程式套件]  步驟適用於獨立媒體。 若要安裝一組特定的驅動程式，此步驟也很有用。 這些類型的驅動程式包括 Windows 隨插即用偵測不到的裝置，例如網路印表機。  

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [驅動程式]  ，然後選取 [套用驅動程式套件]  。

> [!TIP]
> 如需 Configuration Manager 中驅動程式的概觀，請參閱[使用工作順序來安裝驅動程式](../get-started/manage-drivers.md#BKMK_TSDrivers) \(部分機器翻譯\)。
>
> 在使用者安裝工作順序之前，請使用內容預先快取來下載適用的驅動程式套件。 如需詳細資訊，請參閱[設定預先快取內容](../deploy-use/configure-precache-content.md)。

### <a name="variables-for-apply-driver-package"></a>適用於 [套用驅動程式套件] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>適用於 [套用驅動程式套件] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage?view=sccm-ps) \(英文\)
- [New-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage?view=sccm-ps) \(英文\)
- [Remove-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage?view=sccm-ps) \(英文\)
- [Set-CMTSStepApplyDriverPackage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage?view=sccm-ps) \(英文\)

### <a name="properties-for-apply-driver-package"></a>適用於 [套用驅動程式套件] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="driver-package"></a>驅動程式套件

指定包含所需裝置驅動程式的驅動程式套件。 選取 [瀏覽]  來啟動 [選取套件]  對話方塊。 選取一個現有的驅動程式套件來進行套用。 對話方塊的底部會顯示相關聯的套件內容。  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>透過以遞迴選項執行 DISM 的套件安裝驅動程式

選取此選項以在 Windows 套用驅動程式套件時，將 `/recurse` 參數新增至 DISM 命令列。

當您啟用此選項時，您也可以指定其他 DISM 命令列參數。 使用 [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) 工作順序變數來包含更多選項。 如需詳細資訊，請參閱 [Windows 10 DSIM 命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options) \(英文\)。<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>選取在 Windows Vista 前版作業系統部署上設定之前，必須安裝之套件的大型存放驅動程式

指定安裝傳統 OS 所需的任何大型存放驅動程式。  

##### <a name="driver"></a>驅動程式

選取要在安裝傳統 OS 之前安裝的大型存放驅動程式檔案。 下拉式清單中會填入所指定的套件。  

##### <a name="model"></a>型號

指定進行 Windows Vista OS 部署前所需的開機必備裝置。  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>在允許的 Windows 版本上執行自動安裝未簽署的驅動程式

此選項可讓 Windows 安裝沒有數位簽章的驅動程式。  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> 套用網路設定  

您可以使用此步驟來指定目的地電腦的網路或工作群組設定資訊。 工作順序會將這些值儲存在適當的回應檔案中。 Windows 安裝程式則會在 [設定 Windows 和 ConfigMgr]  動作期間使用這個回應檔案。  

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [設定]  ，然後選取 [套用網路設定]  。

> [!NOTE]
> 如果您在工作順序中包含此步驟的多個執行個體，則不會套用條件。 系統只會將工作順序中此步驟之最後一個執行個體的設定套用至裝置。 若要解決此行為，請將每個步驟包含於個別群組中，並在該群組上設定條件。

### <a name="variables-for-apply-network-settings"></a>適用於 [套用網路設定] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>適用於 [套用網路設定] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting?view=sccm-ps) \(英文\)
- [New-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting?view=sccm-ps) \(英文\)
- [Remove-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting?view=sccm-ps) \(英文\)
- [Set-CMTSStepApplyNetworkSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting?view=sccm-ps) \(英文\)

### <a name="properties-for-apply-network-settings"></a>適用於 [套用網路設定] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="join-a-workgroup"></a>加入工作群組

選取此選項可讓目的地電腦加入指定的工作群組。 在 [工作群組]  列上輸入工作群組的名稱。 [擷取網路設定]  工作順序步驟所擷取的值可覆寫此值。

#### <a name="join-a-domain"></a>加入網域

選取此選項可讓目的地電腦加入指定的網域。 指定或瀏覽至網域，例如 `fabricam.com`。 指定或瀏覽至組織單位的輕量型目錄存取通訊協定 (LDAP) 路徑。 例如：`LDAP//OU=computers, DC=Fabricam.com, C=com`。  

#### <a name="account"></a>帳戶

選取 [設定]  ，指定具有將電腦加入網域所需權限的帳戶。 在 [Windows 使用者帳戶]  對話方塊中，以下列格式輸入使用者名稱：`Domain\User`。 如需詳細資訊，請參閱[網域加入帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)。

#### <a name="adapter-settings"></a>介面卡設定

為電腦中的每個網路介面卡指定網路組態。 選取 [新增]  以開啟 [網路設定]  對話方塊，然後指定網路設定。

- 如果您同時使用 [擷取網路設定]  步驟，則工作順序會將先前擷取的設定套用至網路介面卡。
- 如果工作順序先前並未擷取網路設定，它就會套用您在此步驟中指定的設定。
- 工作順序會依照 Windows 裝置列舉順序將這些設定套用至網路介面卡。  
- 工作順序不會將您在此步驟中指定的設定立即套用至電腦。



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> 套用作業系統映像  

您可以使用此步驟，在目的地電腦上安裝 OS。

在 [套用作業系統]  動作執行之後，它會將 **OSDTargetSystemDrive** 變數設定為包含 OS 檔案之磁碟分割的磁碟機代號。  

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [套用作業系統映像]  。

> [!TIP]
> 從 Windows 10 1709 版開始，媒體包含多個版本。 當您設定工作順序以使用作業系統升級套件或作業系統映像時，請務必選取[支援的版本](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)。  
>
> 在使用者安裝工作順序之前，請使用內容預先快取來下載適用的 OS 升級套件。 如需詳細資訊，請參閱[設定預先快取內容](../deploy-use/configure-precache-content.md)。
>
> [設定 Windows 和 ConfigMgr]  步驟會開始安裝 Windows。

### <a name="variables-for-apply-os-image"></a>適用於 [套用 OS 映像] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>適用於 [套用 OS 映像] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem?view=sccm-ps) \(英文\)
- [New-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem?view=sccm-ps) \(英文\)
- [Remove-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem?view=sccm-ps) \(英文\)
- [Set-CMTSStepApplyOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem?view=sccm-ps) \(英文\)

### <a name="behaviors-for-apply-os-image"></a>適用於 [套用 OS 映像] 的行為

此步驟會根據其使用的是 OS 映像或 OS 升級套件來執行不同動作。  

#### <a name="os-image-actions"></a>OS 映像動作

使用作業系統映像時，[套用作業系統映像]  步驟會執行下列動作：  

1. 刪除目標磁碟區上的所有內容，但 **\_SMSTSUserStatePath** 變數所指定資料夾中的檔案除外。  

2. 將指定之 .wim 檔案的內容，擷取至指定的目的地磁碟分割。  

3. 準備回應檔案：  

    1. 針對所部署的 OS，建立新的預設 Windows 安裝程式回應檔案 (sysprep.inf 或 unattend.xml)。  

    2. 將使用者提供的回應檔案中的任何值合併。  

4. 將 Windows 開機載入器複製到使用中的磁碟分割。  

5. 設定 boot.ini 或「開機設定資料庫」(BCD) 來參考新安裝的 OS。  

#### <a name="os-upgrade-package-actions"></a>作業系統升級套件動作

使用作業系統升級套件時，[套用作業系統映像]  步驟會執行下列動作：  

1. 刪除目標磁碟區上的所有內容，但 **\_SMSTSUserStatePath** 變數所指定資料夾中的檔案除外。  

2. 準備回應檔案：  

    1. 使用 Configuration Manager 所建立的標準值，建立一個全新的回應檔案。  

    2. 將使用者提供的回應檔案中的任何值合併。  

### <a name="properties-for-apply-os-image"></a>適用於 [套用 OS 映像] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="apply-operating-system-from-a-captured-image"></a>從擷取的映像套用作業系統

安裝您已擷取的 OS 映像。 選取 [瀏覽]  來開啟 [選取套件]  對話方塊。 然後選取您想要安裝的現有映像套件。 如果有多個映像與指定的 [映像套件]  相關聯，請從下拉式清單中選取要用於此部署的相關聯映像。 您可以選取每個現有映像，來檢視與其相關的基本資訊。  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>從原始安裝來源套用作業系統映像

使用 OS 升級套件 (這也是原始安裝來源) 來安裝 OS。 選取 [瀏覽]  以開啟 [選取作業系統升級套件]  對話方塊。 然後選取您想要使用的現有作業系統升級套件。 您可以選取每個現有映像來源，來檢視與其相關的基本資訊。 對話方塊底部的結果窗格會顯示相關聯的映像來源內容。 如果有多個版本與指定的套件相關聯，請使用下拉式清單來選取您想要使用的 [版本]  。  

> [!NOTE]  
> **作業系統升級套件**主要用於就地升級，而非安裝新的 Windows。 部署新的 Windows 安裝時，請使用 [從擷取的映像套用作業系統]  選項與來自安裝來源檔案的 **install.wim**。
>
> 仍支援透過**作業系統升級套件**部署新的 Windows 安裝，但驅動程式必須與此方法相容。 從 OS 升級套件安裝 Windows 時，會安裝驅動程式，但驅動程式仍在 Windows PE 中，而不是像在 Windows PE 中只是插入。 某些驅動程式不相容，因此無法安裝在 Windows PE 中。
>
> 在 Windows PE 中，若驅動程式不相容而無法安裝，請使用來自原始安裝來源檔案的 **install.wim** 建立**作業系統映像**。 接著，改為透過 [從擷取的映像套用作業系統]  選項來部署。

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>使用自動安裝或 sysprep 回應檔案進行自訂安裝

根據 OS 版本和安裝方法，使用此選項來提供 Windows 安裝程式回應檔案 (**unattend.xml**、**unattend.txt** 或 **sysprep.inf**)。 您指定的檔案可以包含 Windows 回應檔案所支援的任何標準組態選項。 例如，您可以用它來指定預設 Internet Explorer 首頁。 指定包含回應檔案的套件，以及該檔案在套件中的關聯路徑。  

> [!NOTE]  
> 您提供的 Windows 安裝程式回應檔案可以包含 `%varname%` 形式的內嵌工作順序變數，其中 *varname* 是變數的名稱。 [設定 Windows 和 ConfigMgr]  步驟會將變數字串取代為實際的變數值。 您無法在 unattend.xml 回應檔案的純數字欄位中，使用這些內嵌的工作順序變數。  

如果您未提供 Windows 安裝程式回應檔案，此工作順序就會自動產生回應檔案。  

#### <a name="destination"></a>Destination

設定下列其中一個選項：  

- **下一個可用的磁碟分割**：使用這個工作順序中的 [套用作業系統]  或 [套用資料映像]  步驟尚未設為目標的下一個循序磁碟分割。  

- **特定磁碟和磁碟分割**：選取 [磁碟]  編號 (從 0 開始) 和 [磁碟分割]  編號 (從 1 開始)。  

- **特定邏輯磁碟機代號**：指定 Windows PE 指派給磁碟分割的 [磁碟機代號]  。 這個磁碟機代號可以不同於新部署之 OS 所指派的磁碟機代號。  

- **儲存在變數中的邏輯磁碟機代號**：指定工作順序變數，其中包含 Windows PE 指派給磁碟分割的磁碟機代號。 通常會在 [格式化和分割磁碟]  工作順序步驟之 [磁碟分割內容]  對話方塊的 [進階] 區段中，設定此變數。  

### <a name="options-for-apply-os-image"></a>適用於 [套用 OS 映像] 的選項

除了預設選項之外，請在此工作順序步驟的 [選項]  索引標籤上設定下列其他設定：  

#### <a name="access-content-directly-from-the-distribution-point"></a>直接從發佈點存取內容

將工作順序設定為直接從發佈點存取 OS 映像。 例如，當您將作業系統部署到儲存容量有限的內嵌裝置時，請使用此選項。 選取此選項時，請一併在 OS 映像內容的 [資料存取]  索引標籤上，設定套件共用設定。  

> [!NOTE]  
> 此設定會覆寫您在 [部署軟體精靈]  的 [發佈點]  頁面上設定的部署選項。 這項覆寫僅適用於此步驟指定的作業系統映像，而不是針對所有工作順序內容。  

> [!IMPORTANT]  
> 為了最好的安全性，強烈建議不選取此選項。 設計此選項的目的，主要是為了在儲存體容量有限的裝置上使用。 此選項的用意不是協助加快工作順序速度。 選取此選項時，系統不會驗證作業系統套件的套件雜湊。 因此，無法確保套件完整性，因為有系統管理權限的使用者可能變更或竄改套件內容。



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> 套用 Windows 設定

您可以使用此步驟來設定目的地電腦的 Windows 設定。 工作順序會將這些值儲存在適當的回應檔案中。 Windows 安裝程式則會在進行 [設定 Windows 和 ConfigMgr]  步驟時，使用這個回應檔案。  

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [設定]  ，然後選取 [套用 Windows 設定]  。

### <a name="variables-for-apply-windows-settings"></a>適用於 [套用 Windows 設定] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>適用於 [套用 Windows 設定] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps) \(英文\)
- [New-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting?view=sccm-ps) \(英文\)
- [Remove-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting?view=sccm-ps) \(英文\)
- [Set-CMTSStepApplyWindowsSetting](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting?view=sccm-ps) \(英文\)

### <a name="properties-for-apply-windows-settings"></a>適用於 [套用 Windows 設定] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="user-name"></a>使用者名稱

指定要與目的地電腦建立關聯的已登錄使用者名稱。 [擷取 Windows 設定]  工作順序步驟所擷取的值可覆寫此值。  

#### <a name="organization-name"></a>組織名稱

指定要與目的地電腦建立關聯的已登錄組織名稱。 [擷取 Windows 設定]  工作順序步驟所擷取的值可覆寫此值。  

#### <a name="product-key"></a>產品金鑰  

指定在目的地電腦上進行 Windows 安裝時，所使用的產品金鑰。  

#### <a name="server-licensing"></a>伺服器授權

指定伺服器授權模式。

- 選取 [按照伺服器]  或 [每個使用者]  作為授權模式。  
- 如果您選取 [每部伺服器]  ，則也必須指定每個授權合約所允許的連線數目上限。  
- 如果目的地電腦不是伺服器，或您不想要指定授權模式，則請選取 [不要指定]  。  

#### <a name="maximum-connections"></a>連線數目上限

> [!NOTE]
> 此設定僅適用於不再支援的舊版 Windows。<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>隨機產生本機系統管理員密碼，並在所有支援的平台上停用帳戶 (建議)  

選取此選項可將本機系統管理員密碼設定為隨機產生的字串。 此選項也會停用這項功能之支援平台上的本機系統管理員帳戶。  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>啟用帳戶並指定本機系統管理員密碼  

選取此選項可使用指定的密碼來啟用本機系統管理員帳戶。 在 [密碼]  列上輸入密碼，並在 [確認密碼]  列上確認密碼。  

#### <a name="time-zone"></a>時區

指定要在目的地電腦上設定的時區。 [擷取 Windows 設定]  工作順序步驟所擷取的值可覆寫此值。  

#### <a name="language-settings"></a>語言設定

<!--5411057, 5138936-->

從 1910 版起，可控制 OS 部署期間的語言設定。 若您已套用這些語言設定，此變更可協助您簡化您的 OS 部署工作順序。 您只需要為此步驟的每個語言使用一個執行個體 (使用該語言的條件)，而不需要為每個語言使用多個步驟或使用獨立的指令碼。

進行以下設定：

- 輸入法地區設定 (預設鍵盤配置)
- 系統地區設定
- UI 語言
- UI 語言後援
- 使用者地區設定

如需有關這些 Windows 安裝程式回應檔案值的詳細資訊，請參閱 [Microsoft-Windows-International-Core](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core) \(部分機器翻譯\)。

> [!NOTE]
> 若您建立自訂 Windows 安裝程式回應檔案 (unattend.xml)，此步驟會覆寫任何現有值。 若要將這些設定的動態程序自動化，請使用相關的工作順序變數。 例如，[OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)。 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> 自動套用驅動程式

您可以使用此步驟，在部署 OS 時一併比對並安裝驅動程式。  

> [!IMPORTANT]  
> 獨立媒體無法使用 [自動套用驅動程式]  步驟。 在此情況下，工作順序便不會與 Configuration Manager 站台連線。  

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [驅動程式]  ，然後選取 [自動套用驅動程式]  。

> [!TIP]
> 如需 Configuration Manager 中驅動程式的概觀，請參閱[使用工作順序來安裝驅動程式](../get-started/manage-drivers.md#BKMK_TSDrivers) \(部分機器翻譯\)。

### <a name="behaviors-for-auto-apply-drivers"></a>適用於 [自動套用驅動程式] 的行為

[自動套用驅動程式]  工作順序步驟會執行下列動作：  

1. 掃描硬體，並尋找存在於系統上之所有裝置的隨插即用識別碼。  

2. 將裝置及其隨插即用識別碼的清單傳送至管理點。 管理點會從每個硬體裝置的驅動程式類別目錄傳回相容的驅動程式清單。 此清單包含所有已啟用的驅動程式 (不論它們位於哪個驅動程式套件中)，以及標有所指定驅動程式類別的驅動程式。  

3. 針對每個硬體裝置，工作順序都會挑選最適合的驅動程式。 此驅動程式適用於已部署的 OS，且位於可存取的發佈點上。  

4. 工作順序會從發佈點下載所選取的驅動程式，然後在目標 OS 上預備這些驅動程式。  

    1. 使用 OS 映像時，工作順序會將驅動程式放入 OS 驅動程式存放區中。  

    2. 使用 OS 升級套件作為原始安裝來源時，工作順序則是會為 Windows 安裝程式設定驅動程式的位置。  

5. 在工作順序的 [設定 Windows 和 ConfigMgr]  步驟期間，Windows 安裝程式會尋找此步驟所預備的驅動程式。  

### <a name="variables-for-auto-apply-drivers"></a>適用於 [自動套用驅動程式] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>適用於 [自動套用驅動程式] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver?view=sccm-ps) \(英文\)
- [New-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver?view=sccm-ps) \(英文\)
- [Remove-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver?view=sccm-ps) \(英文\)
- [Set-CMTSStepAutoApplyDriver](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver?view=sccm-ps) \(英文\)

### <a name="properties-for-auto-apply-drivers"></a>適用於 [自動套用驅動程式] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>只安裝最符合的相容驅動程式

指定工作順序步驟只針對所偵測到的每個硬體裝置，安裝最符合的驅動程式。  

#### <a name="install-all-compatible-drivers"></a>安裝所有相容的驅動程式

工作順序會針對每個偵測到的硬體裝置，安裝所有相容的驅動程式。 然後，Windows 安裝程式會選擇最適合的驅動程式。 這個選項需要較多的網路頻寬和磁碟空間。 工作順序會下載較多的驅動程式，但 Windows 可以選取較佳的驅動程式。  

#### <a name="consider-drivers-from-all-categories"></a>考量所有類別的驅動程式

工作順序會在所有可用的驅動程式類別中搜尋適當的裝置驅動程式。  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>將驅動程式比對僅限於考量所選類別中的驅動程式

工作順序會在指定的驅動程式類別中搜尋適當的裝置驅動程式。  

如果您選取多個類別，它會傳回出現在任何類別中所有符合的驅動程式。 它相當於 `OR` 作業。<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>在允許的 Windows 版本上執行自動安裝未簽署的驅動程式

此選項可讓 Windows 安裝沒有數位簽章的驅動程式。  

> [!IMPORTANT]  
> 此選項不適用於您無法設定驅動程式簽署原則的作業系統。  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> 擷取網路設定

您可以使用此步驟，從執行工作順序的電腦擷取 Microsoft 網路設定。 工作順序會將這些設定儲存在工作順序變數中。 這些設定會覆寫您在 [套用網路設定]  步驟中設定的預設設定。  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [設定]  ，然後選取 [擷取網路設定]  。

### <a name="variables-for-capture-network-settings"></a>適用於 [擷取網路設定] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>適用於 [擷取網路設定] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings?view=sccm-ps) \(英文\)
- [New-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings?view=sccm-ps) \(英文\)
- [Remove-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings?view=sccm-ps) \(英文\)
- [Set-CMTSStepCaptureNetworkSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings?view=sccm-ps) \(英文\)

### <a name="properties-for-capture-network-settings"></a>適用於 [擷取網路設定] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="migrate-domain-and-workgroup-membership"></a>移轉網域和工作群組成員資格

擷取目的地電腦的網域和工作群組成員資格資訊。  

#### <a name="migrate-network-adapter-configuration"></a>移轉網路介面卡組態

擷取目的地電腦的網路介面卡組態。 它會擷取下列資訊：

- 全域網路設定  
- 介面卡數目  
- 下列網路設定與每個介面卡相關聯：DNS、WINS、IP 及連接埠篩選



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> 擷取作業系統映像

此步驟會擷取參照電腦中的一或多個映像。 工作順序會在指定的網路共用上建立 Windows 映像檔 (.wim)。 接著，請使用 [新增作業系統映像套件]  精靈，將此映像匯入至 Configuration Manager，來進行以映像為基礎的 OS 部署。  

Configuration Manager 會將參照電腦中的每個磁碟區 (磁碟機) 擷取至 .wim 檔案內的個別映像。 如果參照的電腦中有多個磁碟區，所產生的 .wim 檔案將包含每個磁碟區的個別映像。 此步驟只會擷取格式化成 NTFS 或 FAT32 的磁碟區。 它會略過其他格式的磁碟區及 USB 磁碟區。  

參照電腦上所安裝的 OS 必須是 Configuration Manager 支援的 Windows 版本。 請使用 SysPrep 工具來準備參照電腦上的 OS。 所安裝的 OS 磁碟區和開機磁碟區必須是相同的磁碟區。  

指定具有所選取網路共用寫入權限的帳戶。 如需有關擷取 OS 映像帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account)。

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [擷取作業系統映像]  。

### <a name="variables-for-capture-os-image"></a>適用於 [擷取 OS 映像] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>適用於 [擷取 OS 映像] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage?view=sccm-ps) \(英文\)
- [New-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage?view=sccm-ps) \(英文\)
- [Remove-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage?view=sccm-ps) \(英文\)
- [Set-CMTSStepCaptureSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage?view=sccm-ps) \(英文\)

### <a name="properties-for-capture-os-image"></a>適用於 [擷取 OS 映像] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="target"></a>目標  

Configuration Manager 在儲存所擷取 OS 映像時，所使用位置的檔案系統路徑。  

#### <a name="description"></a>說明  

儲存在映像檔中之所擷取 OS 映像的使用者定義描述 (選擇性)。  

#### <a name="version"></a>版本  

要指派給所擷取 OS 映像的使用者定義版本號碼 (選擇性)。 此值可以是字母和數字的任意組合。 它會儲存在映像檔中。  

#### <a name="created-by"></a>建立者  

建立 OS 映像的使用者名稱 (選擇性)。 它會儲存在映像檔中。  

#### <a name="capture-operating-system-image-account"></a>擷取作業系統映像帳戶  

輸入對所指定網路共用具有權限的 Windows 帳戶。 選取 [設定]  來指定 Windows 帳戶的名稱。  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> 擷取使用者狀態

此步驟會使用「使用者狀態移轉工具」(USMT)，從執行工作順序的電腦擷取使用者狀態和設定。 這個工作順序步驟會與 [還原使用者狀態]  工作順序步驟搭配使用。 此步驟會一律使用 Configuration Manager 所產生和管理的加密金鑰，來加密 USMT 狀態存放區。  

如需在部署作業系統時管理使用者狀態的詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

如果您想要從狀態移轉點儲存及還原使用者狀態設定，請將此步驟與 [要求狀態存放區]  和 [釋放狀態存放區]  步驟搭配使用。  

此步驟可讓您控制一部分有限的最常用 USMT 選項。 請使用 **OSDMigrateAdditionalCaptureOptions** 工作順序變數，來指定額外的命令列選項。  

此工作順序步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。  

若要在工作順序編輯器中新增此步驟，請按選取 [新增]  、選取 [使用者狀態]  ，然後選取 [擷取使用者狀態]  。

### <a name="variables-for-capture-user-state"></a>適用於 [擷取使用者狀態] 的變數

請搭配此步驟使用下列工作順序變數：  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>適用於 [擷取使用者狀態] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState?view=sccm-ps) \(英文\)
- [New-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureUserState?view=sccm-ps) \(英文\)
- [Remove-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState?view=sccm-ps) \(英文\)
- [Set-CMTSStepCaptureUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState?view=sccm-ps) \(英文\)

### <a name="properties-for-capture-user-state"></a>適用於 [擷取使用者狀態] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="user-state-migration-tool-package"></a>使用者狀態移轉工具套件

指定包含使用者狀態移轉工具 (USMT) 的套件。 工作順序會使用這個版本的 USMT 來擷取使用者狀態和設定。 此套件不需要程式。 指定包含 USMT 的 32 位元或 64 位元版本的套件。 USMT 的架構取決於工作順序擷取狀態時來源 OS 的架構。  

#### <a name="capture-all-user-profiles-with-standard-options"></a>以標準選項擷取所有使用者設定檔

移轉所有使用者設定檔資訊。 此選項是預設值。  

如果您選取此選項，但未選取 [還原使用者狀態]  步驟中的 [還原本機使用者設定檔]  ，工作順序就會失敗。 Configuration Manager 無法在不為新帳戶指派密碼的情況下移轉新帳戶。

當您使用 [New Task Sequence Wizard]\ (新工作順序精靈)  的 [安裝現有的映像套件]  選項時，產生的工作順序預設為 [Capture all user profiles with standard options]\ (以標準選項擷取所有使用者設定檔)  。 此預設工作順序不會選取用以**還原本機使用者設定檔** (或非網域使用者帳戶) 的選項。  

請選取 [還原本機使用者設定檔]  ，並為要移轉的帳戶提供密碼。 在手動建立的工作順序中，可以在 [還原使用者狀態]  步驟底下找到此設定。 在由 [新增工作順序精靈]  建立的工作順序中，可以在 [還原使用者檔案和設定精靈]  步驟頁面底下找到這項設定。  

如果您沒有本機使用者帳戶，此設定便不適用。  

#### <a name="customize-how-user-profiles-are-captured"></a>自訂如何擷取使用者設定檔

選取此選項來指定用於移轉的自訂設定檔檔案。 選取 [檔案]  ，選取要用於此步驟的 USMT 組態檔。 指定自訂的 .xml 檔案，其中包含定義所要移轉之使用者狀態檔案的規則。  

#### <a name="click-here-to-select-configuration-files"></a>按一下此處選取設定檔案

選取這個選項，以選取您要在 USMT 套件中用來擷取使用者設定檔的組態檔。 選取 [檔案]  按鈕，以啟動 [組態檔]  對話方塊。 若要指定組態檔，請在 [檔案名稱]  列上輸入檔案名稱，並選取 [新增]  按鈕。  

#### <a name="enable-verbose-logging"></a>啟用詳細資訊記錄

啟用此選項可產生較詳細的記錄檔資訊。 擷取狀態時，工作順序預設會在 `%WinDir%\ccm\logs` 工作順序記錄檔資料夾中產生 **ScanState.log**。  

#### <a name="skip-files-using-encrypted-file-system"></a>略過使用加密檔案系統的檔案

啟用此選項可略過擷取以加密檔案系統 (EFS) 加密的檔案。 這些檔案包括使用者設定檔。 視 OS 和 USMT 版本而定，在還原加密的檔案之後，可能會無法讀取這些加密的檔案。 如需詳細資訊，請參閱 USMT 說明文件。  

#### <a name="copy-by-using-file-system-access"></a>使用檔案系統存取進行複製

啟用此選項可指定下列任何設定：  

- **無法擷取部分檔案時仍繼續**：啟用此設定時，在即使無法擷取部分檔案的情況下，仍可繼續執行移轉程序。 如果停用這個選項，當無法擷取某個檔案時，此步驟就會失敗。 這個選項預設為啟用。  

- **藉由使用連結而非複製檔案在本機擷取**：啟用此設定以使用 NTFS 永久連結來擷取檔案。  

    如需有關使用永久連結來移轉資料的詳細資訊，請參閱[永久連結移轉存放區](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store) \(英文\)。  

- **以離線模式擷取 (僅限 Windows PE)** ：啟用此設定，可以在 Windows PE (而不是完整 OS) 中時，擷取使用者狀態。  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>使用磁碟區陰影複製服務 (VSS) 來擷取

此選項可讓您在即使檔案被鎖定以供另一個應用程式編輯的情況下，仍可擷取那些檔案。  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> 擷取 Windows 設定

您可以使用此步驟，從執行工作順序的電腦擷取 Windows 設定。 工作順序會將這些設定儲存在工作順序變數中。 這些擷取的設定會覆寫您在 [套用 Windows 設定]  步驟中設定的預設設定。  

此工作順序步驟可在 Windows PE 或完整 OS 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [設定]  ，然後選取 [擷取 Windows 設定]  。

### <a name="variables-for-capture-windows-settings"></a>適用於 [擷取 Windows 設定] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>適用於 [擷取 Windows 設定] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings?view=sccm-ps) \(英文\)
- [New-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings?view=sccm-ps) \(英文\)
- [Remove-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings?view=sccm-ps) \(英文\)
- [Set-CMTSStepCaptureWindowsSettings](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings?view=sccm-ps) \(英文\)

### <a name="properties-for-capture-windows-settings"></a>適用於 [擷取 Windows 設定] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="migrate-computer-name"></a>移轉電腦名稱

擷取電腦的 NetBIOS 電腦名稱。  

#### <a name="migrate-registered-user-and-organization-names"></a>移轉已註冊的使用者和組織名稱

從電腦擷取已註冊的使用者和組織名稱。  

#### <a name="migrate-time-zone"></a>移轉時區

擷取電腦上的時區設定。  



## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> 檢查整備程度

您可以使用此步驟來確認目標電腦是否符合指定的部署必要條件。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [一般]  ，然後選取 [檢查整備程度]  。

從 2002 版開始，此步驟包含八個新檢查。 根據預設，此步驟的新或現有執行個體概未選取這些新檢查項目。<!--6005561--> 如需每個檢查的詳細資訊，請參閱以下的特定小節。

- **目前 OS 的架構**
- **最低 OS 版本**
- **最高 OS 版本**
- **用戶端最低版本**
- **目前 OS 的語言**
- **AC 電源已插入**
- **網路介面卡已連線**
  - **網路介面卡並非無線**

> [!IMPORTANT]
> 若要利用此 Configuration Manager 新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

**smsts.log** 包含所有檢查的結果。 如有一項檢查失敗，則工作順序引擎會繼續評估其他檢查。 完成所有檢查後此步驟才會失敗。 如有至少一項檢查失敗，則此步驟會失敗並傳回錯誤碼 **4316**。 此錯誤碼意為「這個操作必需的資源不存在」。

### <a name="variables-for-check-readiness"></a>適用於 [檢查整備程度] 的變數

請搭配此步驟使用下列工作順序變數：  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED)

### <a name="cmdlets-for-check-readiness"></a>適用於 [檢查整備程度] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck?view=sccm-ps) \(英文\)
- [New-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrestartCheck?view=sccm-ps) \(英文\)
- [Remove-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck?view=sccm-ps) \(英文\)
- [Set-CMTSStepPrestartCheck](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck?view=sccm-ps) \(英文\)

### <a name="properties-for-check-readiness"></a>適用於 [檢查整備程度] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="minimum-memory-mb"></a>記憶體下限 (MB)

確認記憶體數量 (以 MB 為單位) 符合或超過指定的數量。 此步驟預設會啟用這個設定。  

#### <a name="minimum-processor-speed-mhz"></a>處理器速度下限 (MHz)  

確認處理器的速度 (以 MHz 為單位) 符合或超過指定的數量。 此步驟預設會啟用這個設定。  

#### <a name="minimum-free-disk-space-mb"></a>最小可用磁碟空間 (MB)

確認可用磁碟空間的數量 (以 MB 為單位) 符合或超過指定的數量。  

#### <a name="current-os-to-be-refreshed-is"></a>要重新整理的目前 OS 為

確認安裝在目標電腦上的 OS 符合指定的需求。 此步驟預設會將此設定設為 [用戶端]  。  

#### <a name="architecture-of-current-os"></a>目前 OS 的架構

從 2002 版開始，確認目前的 OS 為 **32 位元**或 **64 位元**。

#### <a name="minimum-os-version"></a>最低 OS 版本

從 2002 版開始，確認目前 OS 執行的版本比指定的版本還要新。 使用主要版本、次要版本和組建編號來指定版本。 例如 `10.0.16299`。

#### <a name="maximum-os-version"></a>最高 OS 版本

從 2002 版開始，確認目前 OS 執行的版本比指定的版本還要早。 使用主要版本、次要版本和組建編號來指定版本。 例如 `10.0.18356`。

#### <a name="minimum-client-version"></a>用戶端最低版本

從 2002 版開始，確認 Configuration Manager 用戶端版本至少是指定的版本。 依下列格式指定用戶端版本：`5.00.8913.1005`。

#### <a name="language-of-current-os"></a>目前 OS 的語言

從 2002 版開始，確認目前的 OS 語言與您指定的語言相符。 選取語言名稱，此步驟即會比較相關聯的語言代碼。 此檢查會比較您選取的語言與用戶端上 **Win32_OperatingSystem** WMI 類別的 **OSLanguage** 屬性。

#### <a name="ac-power-plugged-in"></a>AC 電源已插入

從 2002 版開始，確認已為裝置插上電源，而不是使用電池。

#### <a name="network-adapter-connected"></a>網路介面卡已連線

從 2002 版開始，確認裝置具有已連線到網路的網路介面卡。 您也可以選取相依檢查，以確認 [網路介面卡並非無線]  。

### <a name="options-for-check-readiness"></a>適用於 [檢查整備程度] 的選項

> [!NOTE]  
> 如果您在此步驟的 [選項]  索引標籤上啟用 [發生錯誤時仍繼續]  設定，它只會記錄整備檢查結果。 如果檢查失敗，工作順序並不會停止。  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> 連線到網路資料夾

您可以使用此步驟來建立與共用網路資料夾的連線。  

此工作順序步驟可在完整 OS 或 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [一般]  ，然後選取 [連線至網路資料夾]  。

### <a name="variables-for-connect-to-network-folder"></a>適用於 [連線至網路資料夾] 的變數

請搭配此步驟使用下列工作順序變數：  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>適用於 [連線至網路資料夾] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder?view=sccm-ps) \(英文\)
- [New-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder?view=sccm-ps) \(英文\)
- [Remove-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder?view=sccm-ps) \(英文\)
- [Set-CMTSStepConnectNetworkFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder?view=sccm-ps) \(英文\)

### <a name="properties-for-connect-to-network-folder"></a>適用於 [連線至網路資料夾] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="path"></a>路徑  

選取 [瀏覽]  以指定網路資料夾路徑。 請使用 `\\server\share` 格式。

#### <a name="drive"></a>磁碟機  

選取要為此連線指派的本機磁碟機代號。

#### <a name="account"></a>帳戶

選取 [設定]  以指定有權連線到此網路資料夾的使用者帳戶。 如需有關工作順序網路資料夾連線帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)。



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> 停用 BitLocker

您可以使用此步驟來停用目前 OS 磁碟機或特定磁碟機上的 BitLocker 加密。 此動作會讓金鑰保護裝置在該硬碟上維持純文字的可見形式。 它不會將磁碟機的內容解密。 此動作幾乎是立即完成的。  

> [!NOTE]  
> BitLocker 磁碟機加密提供磁碟區內容的低階加密。  

如果您有多個加密的磁碟機，請先停用任何資料磁碟機上的 BitLocker，然後才停用 OS 磁碟機上的 BitLocker。  

此步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [磁碟]  ，然後選取 [停用 BitLocker]  。

### <a name="variables-for-disable-bitlocker"></a>適用於 [停用 BitLocker] 的變數

從 1906 版起，請搭配此步驟使用下列工作順序變數：  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>適用於 [停用 BitLocker] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker?view=sccm-ps) \(英文\)
- [New-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker?view=sccm-ps) \(英文\)
- [Remove-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker?view=sccm-ps) \(英文\)
- [Set-CMTSStepDisableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker?view=sccm-ps) \(英文\)

### <a name="properties-for-disable-bitlocker"></a>適用於 [停用 BitLocker] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="current-operating-system-drive"></a>目前的作業系統磁碟機

停用目前 OS 磁碟機上的 BitLocker。  

#### <a name="specific-drive"></a>特定磁碟機  

在特定磁碟機上停用 BitLocker。 使用下拉式清單來指定要停用 BitLocker 的磁碟機。  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>在重新啟動 Windows 達指定次數後繼續保護

<!-- 4512937 -->
從 1906 版開始，使用此選項來指定重新啟動次數，以確保 BitLocker 停用。 您可以設定介於 1 (預設) 到 15 之間的值，而不是新增此步驟的多個執行個體。

您可以使用工作順序變數 [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) 與 [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride) 來設定及修改此行為。


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> 下載封裝內容

您可以使用此步驟來下載下列任何的套件類型：  

- OS 映像  
- OS 升級套件  
- 驅動程式套件  
- 套件  
- 開機映像<sup>[附註 1](#bkmk_note1)</sup>  

此步驟適用於要在下列情況下升級 OS 的工作順序：  

- 若要使用可同時搭配 x86 和 x64 平台使用的單一升級工作順序。 [準備升級]  群組中包含兩個 [下載套件內容]  步驟。 在 [選項]  索引標籤上指定條件來偵測用戶端架構，然後只下載適當的 OS 升級套件。 設定每個 [下載套件內容]  步驟，以使用相同的變數。 將該變數用於 [升級作業系統]  步驟中的媒體路徑。  

- 若要動態下載適用的驅動程式套件，請使用兩個 **下載套件內容** 步驟，並設定條件來偵測每個驅動程式套件適用的硬體類型。 設定每個 [下載套件內容]  步驟，以使用相同的變數。 將該變數用於 [升級作業系統]  步驟上驅動程式區段中的 [分段內容]  值。  

> [!NOTE]  
> 當您部署包含此步驟的工作順序時，針對 [部署軟體精靈] 之 [發佈點]  頁面上的 [部署選項]  ，請勿選取 [啟動工作順序之前下載所有內容到本機]  或 [直接從發佈點存取內容]  。  

此步驟可在完整 OS 或 Windows PE 中執行。 Windows PE 不支援在 Configuration Manager 用戶端快取中儲存套件的選項。

> [!NOTE]  
> **下載套件內容**工作不支援搭配獨立媒體使用。 如需詳細資訊，請參閱[獨立媒體不支援的動作](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media)。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [軟體]  ，然後選取 [下載套件內容]  。

### <a name="cmdlets-for-download-package-content"></a>適用於 [下載套件內容] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent?view=sccm-ps) \(英文\)
- [New-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent?view=sccm-ps) \(英文\)
- [Remove-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent?view=sccm-ps) \(英文\)
- [Set-CMTSStepDownloadPackageContent](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent?view=sccm-ps) \(英文\)

### <a name="properties-for-download-package-content"></a>適用於 [下載套件內容] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="select-package"></a>選取套件  

選取圖示可選擇要下載的套件。 在您選擇套件之後，再次選取圖示，即可選擇另一個套件。  

#### <a name="place-into-the-following-location"></a>放入下列位置

選擇此選項以將套件儲存在下列其中一個位置：  

- **工作順序工作目錄**：此位置也稱為工作順序快取。  

- **Configuration Manager 用戶端快取**：使用此選項可將內容儲存在用戶端快取中。 此路徑預設為 `%WinDir%\ccmcache`。  

- **自訂路徑**：工作順序引擎會先將套件下載到工作順序工作目錄。 然後再將內容移至您指定的這個路徑。 工作順序引擎會在套件識別碼前附加此路徑。  

#### <a name="save-path-as-a-variable"></a>將路徑儲存為變數

將套件的路徑儲存至自訂工作順序變數中。 然後在另一個工作順序步驟中使用此變數。

Configuration Manager 會在變數名稱後面加上數值尾碼。 例如，您指定一個 `%MyContent%` 變數作為自訂變數。 它是工作順序為此步驟儲存所有參考內容的位置根目錄。 此內容可能包含多個套件。 當您參考變數時，請新增一個數值尾碼。 針對第一個套件，請參考 `%MyContent01%`。 當您在後續步驟 (例如 [升級作業系統]  ) 中參考該變數時，請使用 `%MyContent02%` 或 `%MyContent03%`，其中數字與 [下載套件內容]  步驟列出套件的順序對應。  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>如有封裝下載失敗，繼續下載清單中的其他封裝

如果工作順序無法下載套件，它會開始下載清單中的下一個套件。  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> 附註 1：在「下載套件內容」步驟中使用開機映像

*適用於 1910 版和更新版本*<!-- SCCMDocs-pr #4202 -->

如果您將[工作順序內容](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced)設定為 [使用開機映像]  ，則將開機映像新增到此步驟是多餘的。 只有未在工作順序內容上指定開機映像時，才新增開機映像到此步驟。

#### <a name="example-use-case"></a>範例使用案例

- 預先下載內容的單一工作順序：
  - 沒有相關聯的開機映像。
  - 只在完整 OS 中執行，應該不需要使用者互動。
  - 搭配條件使用多個**下載套件內容**步驟。 視特定語言與架構而定，其會將內容下載至用戶端快取，以針對 OS 部署工作順序做準備。
  - 此工作順序只有一個執行個體，其中包含所有可能的內容選項。

- 多個 OS 部署工作順序：
  - 一般 OS 部署工作順序。
  - 在其內容中參考開機映像。
  - 此工作順序有多個執行個體，其中架構與語言需要不同的開機映像

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> 啟用 BitLocker

您可以使用此步驟，至少在硬碟的兩個磁碟分割上啟用 BitLocker 加密。 第一個作用中磁碟分割包含 Windows 開機程式碼。 另一個磁碟分割包含 OS。 開機磁碟分割必須保持未加密狀態。  

請使用 [預先佈建 BitLocker]  步驟，以在處於 Windows PE 中時，在磁碟機上啟用 BitLocker。 如需詳細資訊，請參閱[預先佈建 BitLocker](#BKMK_PreProvisionBitLocker)。  

> [!NOTE]  
> BitLocker 磁碟機加密提供磁碟區內容的低階加密。  

此步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [磁碟]  ，然後選取 [啟用 BitLocker]  。

當您指定 [僅 TPM]  、[TPM 和 USB 上的啟動金鑰]  或 [TPM 和 PIN]  時，可信賴平台模組 (TPM) 必須處於下列狀態，才能執行 [啟用 BitLocker]  步驟：  

- 已啟用  
- 已啟動  
- 允許的擁有權  

這個步驟會完成任何其餘的 TPM 初始化作業。 其餘步驟無須使用者親自操作或重新開機。 如有必要，[啟用 BitLocker]  步驟會在背景中完成下列其餘 TPM 初始化步驟：  

- 建立簽署金鑰組  
- 建立擁有者授權值和委付至 Active Directory，Active Directory 必須已擴充為支援此值  
- 取得擁有權  
- 建立儲存根金鑰，或者如果已經存在，但不相容，則重設  

如果您想要工作順序等待 [啟用 BitLocker]  步驟完成磁碟機加密程序，則請選取 [等候]  選項。 如果您未選取 [等候]  選項，磁碟機加密程序就會在背景中執行。 工作順序則會立即繼續進行下一個步驟。  

BitLocker 可用來將電腦系統上的多個磁碟機加密 (包括 OS 和資料磁碟機)。 若要將資料磁碟機加密，請先將 OS 磁碟機加密，並完成加密程序。 之所以會有此需求，是因為 OS 磁碟機會儲存資料磁碟機的金鑰保護裝置。 如果您在相同的工作順序中將 OS 磁碟機和資料磁碟機加密，請針對 OS 磁碟機，在 [啟用 BitLocker]  步驟中選取 [等候]  選項。  

如果硬碟機已加密，但停用了 BitLocker，則 [啟用 BitLocker]  步驟會重新啟用金鑰保護裝置，並快速完成。 在此情況下，並不需要重新加密硬碟。  

### <a name="variables-for-enable-bitlocker"></a>適用於 [啟用 BitLocker] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>適用於 [啟用 BitLocker] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker?view=sccm-ps) \(英文\)
- [New-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker?view=sccm-ps) \(英文\)
- [Remove-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker?view=sccm-ps) \(英文\)
- [Set-CMTSStepEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker?view=sccm-ps) \(英文\)

### <a name="properties-for-enable-bitlocker"></a>適用於 [啟用 BitLocker] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="choose-the-drive-to-encrypt"></a>選擇要加密的磁碟機

指定要加密的磁碟機。 若要加密目前的 OS 磁碟機，請選取 [目前的作業系統磁碟機]  。 然後設定下列其中一個金鑰管理選項：  

- **僅 TPM**：選取此選項來僅使用信賴平台模組 (TPM)。  

- **僅 USB 上的啟動金鑰**：選取此選項來使用存放在 USB 快閃磁碟機上的啟動金鑰。 當您選取此選項時，BitLocker 會鎖定一般開機程序，直到有包含 BitLocker 啟動金鑰的 USB 裝置連接到電腦為止。  

- **TPM 和 USB 上的啟動金鑰**：選取此選項來使用 TPM 和存放在 USB 快閃磁碟機上的啟動金鑰。 當您選取此選項時，BitLocker 會鎖定一般開機程序，直到有包含 BitLocker 啟動金鑰的 USB 裝置連接到電腦為止。  

- **TPM 和 PIN**：選取這個選項可使用 TPM 和個人識別碼 (PIN)。 當您選取此選項時，BitLocker 會鎖定一般開機程序，直到使用者提供 PIN。  

若要加密特定的非 OS 資料磁碟機，請選取 [特定磁碟機]  。 然後從清單中選取磁碟機。  

#### <a name="use-full-disk-encryption"></a>使用完整磁碟加密

<!--SCCMDocs-pr issue 2671-->
此步驟預設只會加密磁碟機上已使用的空間。 建議使用此預設行為，因為它的速度更快且更具效率。 如果您的組織需要在安裝期間加密整個磁碟機，則請啟用此選項。 Windows 安裝程式會等待整個磁碟機加密，這需要很長的時間，特別是在大型磁碟機上。

> [!TIP]
> 從 1910 版起，您可以建立及部署使用「完整磁碟」  加密的 BitLocker 管理原則。 若要在工作順序部署 OS 之後管理裝置上的 BitLocker，請啟用此選項。 如需詳細資訊，請參閱[規劃 BitLocker 管理](../../protect/plan-design/bitlocker-management.md)。

#### <a name="choose-where-to-create-the-recovery-key"></a>選擇建立修復金鑰的位置

若要指定讓 BitLocker 建立修復密碼並將其委付在 Active Directory 中，請選取 [在 Active Directory 中]  。 此選項會要求您延伸 Active Directory 以進行 BitLocker 金鑰委付。 然後 BitLocker 就可以將相關聯的復原資訊儲存在 Active Directory 中。 選取 [Do not create recovery key]\(不要建立修復金鑰)  ，表示不要建立密碼。 建立密碼是一個建議選項。  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>等候 BitLocker 在所有磁碟機上完成磁碟機加密程序，再繼續執行工作順序

選取此選項可讓 BitLocker 磁碟機加密先完成後，再執行工作順序中的下一個步驟。 如果選取此選項，BitLocker 會先將整個磁碟區加密，然後使用者才能登入電腦。  

在加密大型硬碟機時，加密程序可能需要數小時才能完成。 若未選取此選項，則會讓工作順序立即繼續進行。  



## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> 格式化和分割磁碟

您可以使用此步驟，將目的地電腦上的指定磁碟格式化和分割。  

> [!IMPORTANT]  
> 您為此步驟指定的每個設定都會套用至單一指定磁碟。 若要將目的地電腦上的另一個磁碟格式化和分割，請將另一個 [格式化和分割磁碟]  步驟新增至工作順序。  

此步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [磁碟]  ，然後選取 [格式化和分割磁碟]  。

### <a name="variables-for-format-and-partition-disk"></a>適用於 [格式化和分割磁碟] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>適用於 [格式化和分割磁碟] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteppartitiondisk?view=sccm-ps) \(英文\)
- [New-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteppartitiondisk?view=sccm-ps) \(英文\)
- [Remove-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteppartitiondisk?view=sccm-ps) \(英文\)
- [Set-CMTSStepPartitionDisk](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteppartitiondisk?view=sccm-ps) \(英文\)

### <a name="properties-for-format-and-partition-disk"></a>適用於 [格式化和分割磁碟] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="disk-number"></a>磁碟編號

要格式化之磁碟的實體磁碟編號。 該編號取決於 Windows 磁碟列舉排序。  

#### <a name="disk-type"></a>磁碟類型

要格式化的磁碟類型。 下拉式清單中有兩個選項可供選取：

- **標準 (MBR)** ：主開機記錄  
- **GPT**：GUID 磁碟分割表格  

> [!NOTE]  
> 如果您將磁碟類型從 [標準 (MBR)]  變更為 [GPT]  ，而且磁碟分割配置包含延伸磁碟分割，則工作順序會從配置中移除所有延伸及邏輯磁碟分割。 在變更磁碟類型之前，工作順序會提示您確認此動作。  

#### <a name="volume"></a>磁碟區

工作順序建立之磁碟分割或磁碟區的特定相關資訊，包括下列屬性：  

- Name  
- 剩餘的磁碟空間  

若要建立新的磁碟分割，請選取 [新增]  以啟動 [磁碟分割內容]  對話方塊。 請指定磁碟分割類型和大小，以及它是否為開機磁碟分割。 若要修改現有的磁碟分割，請選取要修改的磁碟分割，然後選取 [內容]  按鈕。 如需如何設定硬碟分割的詳細資訊，請參閱下列其中一篇文章：  

- [以 UEFI/GPT 為基礎的硬碟分割](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions) \(英文\)  
- [以 BIOS/MBR 為基礎的硬碟分割](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions) \(英文\)  

若要刪除某個磁碟分割，請選擇該磁碟分割，然後選取 [刪除]  。  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> 安裝應用程式

這個步驟將安裝指定的應用程式，或由工作順序變數的動態清單所定義的一組應用程式。 當工作順序執行此步驟時，應用程式安裝會立即開始，而不會等候原則輪詢間隔。  

應用程式必須符合下列準則：  

- 應用程式的部署類型必須是 [Windows Installer]  或 [指令碼]  安裝程式。 不支援 Windows 應用程式套件 (.appx 檔案) 部署類型。  

- 必須以「本機系統」帳戶而不是使用者帳戶來執行。  

- 它不能與桌面互動。 必須以無訊息模式或自動模式來執行程式。  

- 絕不能自行初始化重新啟動。 應用程式必須使用標準重新啟動代碼 3010 來要求重新啟動。 此行為可確保此步驟會正確處理重新啟動。 如果應用程式傳回 3010 結束代碼，工作順序引擎就會重新啟動電腦。 重新啟動之後，工作順序會自動繼續進行。  

> [!Note]
> 如果應用程式[檢查執行中的可執行檔](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check)，則工作順序將無法安裝該應用程式。 如果您未將此步驟設定為在發生錯誤時繼續執行，則整個工作順序會失敗。

當此步驟執行時，應用程式會檢查是否可在其部署類型上套用需求規則和偵測方法。 根據這項檢查的結果，應用程式會安裝適用的部署類型。 如果部署類型包含相依性，在此步驟中就會一併評估並安裝相依的部署類型。 針對獨立媒體，不支援應用程式相依性。  

> [!NOTE]  
> 如果所要安裝的應用程式會取代另一個應用程式，被取代的應用程式的內容檔案必須可供使用。 否則，此工作順序步驟將會失敗。 例如，Microsoft Visio 2010 已安裝在用戶端或擷取的映像中。 執行 [安裝應用程式]  步驟來安裝 Microsoft Visio 2013 時，發佈點上必須要有 Microsoft Visio 2010 (被取代的應用程式) 的內容檔案。 如果未在用戶端或擷取的映像上安裝 Microsoft Visio，工作順序就會安裝 Microsoft Visio 2013，而不會檢查 Microsoft Visio 2010 內容檔案。  
>
> 如果您淘汰已過時的應用程式，並在工作順序中參考新的應用程式，工作順序將無法啟動。
這是預設行為：工作順序需要所有應用程式參考。<!-- SCCMDocs 1711 -->  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [軟體]  ，然後選取 [安裝應用程式]  。

### <a name="variables-for-install-application"></a>適用於 [安裝應用程式] 的變數

請搭配此步驟使用下列工作順序變數：  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> 如果用戶端無法從位置服務擷取管理點清單，請使用 **SMSTSMPListRequestTimeoutEnabled** 和 **SMSTSMPListRequestTimeout** 工作順序變數。 這些變數可指定工作順序在重新嘗試安裝應用程式之前，需等候多少毫秒。 如需詳細資訊，請參閱[工作順序變數](task-sequence-variables.md)。

### <a name="cmdlets-for-install-application"></a>適用於 [安裝應用程式] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallapplication?view=sccm-ps) \(英文\)
- [New-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallapplication?view=sccm-ps) \(英文\)
- [Remove-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallapplication?view=sccm-ps) \(英文\)
- [Set-CMTSStepInstallApplication](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallapplication?view=sccm-ps) \(英文\)

### <a name="properties-for-install-application"></a>適用於 [安裝應用程式] 的屬性

在這個步驟的 [內容]  索引標籤上，請設定本節中所描述的設定。  

#### <a name="install-the-following-applications"></a>安裝下列應用程式

工作順序會依照指定的順序來安裝這些應用程式。  

Configuration Manager 會篩選掉任何停用的應用程式，或是具有下列設定的任何應用程式：  

- 只有在使用者登入時  
- 以使用者權限執行  

這些應用程式不會出現在 [選取要安裝的應用程式]  對話方塊中。

#### <a name="install-applications-according-to-dynamic-variable-list"></a>根據動態變數清單安裝應用程式

工作順序會使用這個基底變數名稱來安裝應用程式。 基底變數名稱是用於一組為集合或電腦所定義的工作順序變數。 這些變數可指定工作順序為該集合或電腦安裝的應用程式。 每個變數名稱都是由其一般基底名稱加上從 01 開始的數字尾碼所組成。 每個變數的值都必須只包含應用程式的名稱。  

針對要使用動態變數清單安裝應用程式的工作順序，要在應用程式 [內容]  的 [一般]  索引標籤上啟用下列設定：**允許從 [安裝應用程式] 工作順序動作來安裝此應用程式，而不是手動部署**。  

> [!NOTE]  
> 針對獨立媒體部署，您無法使用動態變數清單來安裝應用程式。  

例如，若要使用名為 AA01 的工作順序變數來安裝單一應用程式，請指定下列變數：  

|變數名稱|變數值|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

若要安裝兩個應用程式，請指定下列變數：  

|變數名稱|變數值|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

下列狀況會影響工作順序所安裝的應用程式：  

- 如果變數的值包含應用程式名稱以外的任何資訊， 工作順序不會安裝該應用程式，且工作順序會繼續進行。  

- 如果工作順序找不到具有指定基底名稱和 "01" 尾碼的變數，工作順序便不會安裝任何應用程式。  

> [!Important]  
> 這些值會區分大小寫。 例如，"install" 不同於 "Install"。 如果您需要變更值，工作順序編輯器不會偵測到大小寫的變更。 請同時進行另一個編輯，例如修改步驟描述。<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>如果某個應用程式失敗，繼續安裝清單中的其他應用程式

此設定指定當個別應用程式安裝失敗時，步驟將繼續進行。 如果您指定此設定，則不論發生任何安裝錯誤，工作順序都會繼續進行。 如果您未指定此設定，而且安裝失敗，步驟就會立即結束。  

#### <a name="clear-application-content-from-cache-after-installing"></a>安裝後從快取清除應用程式內容

<!--4485675-->
從 1906 版起，在步驟執行之後，從用戶端快取刪除應用程式內容。 此行為對於具有小型硬碟機的裝置或在連續安裝多個大型應用程式時十分有用。


### <a name="options-for-install-application"></a>適用於 [安裝應用程式] 的選項

> [!NOTE]  
> 如果您在此步驟的 [選項]  索引標籤上選取 [發生錯誤時仍繼續]  ，當應用程式安裝失敗時，工作順序會繼續進行。 如果您未啟用此選項，工作順序便會失敗，而且不會安裝其餘應用程式。  

除了預設選項之外，請在此工作順序步驟的 [選項]  索引標籤上設定下列其他設定：  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>如果電腦非預期地重新啟動則重試此步驟

如果其中一個應用程式安裝非預期地重新啟動電腦，請重試這個步驟。 根據預設，此步驟會以兩次重試次數啟用這個設定。 您可以指定一到五次的重試次數。  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> 安裝套件

您可以使用此步驟，安裝軟體套件作為工作順序的一部分。 當此步驟執行時，安裝會立即開始，而不會等候原則輪詢間隔。  

套件必須符合下列準則：  

- 必須以本機系統帳戶而不是使用者帳戶來執行。  

- 不應與桌面互動。 必須以無訊息模式或自動模式來執行程式。  

- 絕不能自行初始化重新啟動。 軟體必須使用標準重新啟動代碼 3010 來要求重新啟動。 此行為可確保工作順序步驟會正確處理重新啟動。 如果軟體確實傳回 3010 結束代碼，工作順序引擎就會重新啟動電腦。 重新啟動之後，工作順序會自動繼續進行。  

部署 OS 時，不支援使用 [先執行其他程式]  選項來安裝相依程式的程式。 如果您啟用套件選項 [先執行另一個程式]  ，並且已經在目的地電腦上執行相依程式，則會執行相依程式，且工作順序將會繼續進行。 不過，如果相依程式尚未在目的地電腦上執行，工作順序步驟就會失敗。  

> [!NOTE]  
> 管理中心網站並不具有在工作順序期間啟用軟體發佈代理程式時，所需的必要用戶端設定原則。 若在管理中心網站建立工作順序的獨立媒體，且該工作順序包含 [安裝套件]  步驟，CreateTsMedia.log 檔案中可能會出現下列錯誤：  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> 如果是包含 [安裝套件]  步驟的獨立媒體，請在已啟用軟體發佈代理程式的主要網站上建立獨立媒體。 或者，在 [設定 Windows 和 ConfigMgr]  步驟之後，以及在第一個 [安裝套件]  步驟之前，新增 [執行命令列]  步驟。 [執行命令列]  步驟會執行 WMIC 命令，在第一個 [安裝套件]  步驟執行之前啟用軟體發佈代理程式。 請在 [執行命令列]  步驟中使用下列命令：  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> 如需建立獨立媒體的詳細資訊，請參閱[建立獨立媒體](../deploy-use/create-stand-alone-media.md)。  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [軟體]  ，然後選取 [安裝套件]  。

### <a name="variables-for-install-package"></a>適用於 [安裝套件] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>適用於 [安裝套件] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallsoftware?view=sccm-ps) \(英文\)
- [New-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallsoftware?view=sccm-ps) \(英文\)
- [Remove-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware?view=sccm-ps) \(英文\)
- [Set-CMTSStepInstallSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallsoftware?view=sccm-ps) \(英文\)

> [!TIP]
> 在使用者安裝工作順序之前，請使用內容預先快取來下載適用的 OS 升級套件。 如需詳細資訊，請參閱[設定預先快取內容](../deploy-use/configure-precache-content.md)。

### <a name="properties-for-install-package"></a>適用於 [安裝套件] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="install-a-single-software-package"></a>安裝單一軟體套件

此設定會指定 Configuration Manager 軟體套件。 此步驟會等待安裝完成。  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>根據動態變數清單安裝軟體套件

工作順序會使用這個基底變數名稱來安裝套件。 基底變數名稱是用於一組為集合或電腦所定義的工作順序變數。 這些變數可指定工作順序為該集合或電腦安裝的套件。 每個變數名稱都是由其一般基底名稱加上從 001 開始的數字尾碼所組成。 每個變數的值都必須包含封裝識別碼和軟體名稱，並以分號分隔。  

針對要使用動態變數清單安裝軟體的工作順序，要在套件 [內容]  的 [進階]  索引標籤上啟用下列設定：**允許在未部署此程式的情況下，從安裝套件工作順序安裝此程式**。  

> [!NOTE]  
> 針對獨立媒體部署，您無法使用動態變數清單來安裝軟體套件。  

例如，若要使用名為 AA001 的工作順序變數來安裝單一軟體套件，您要指定下列變數：  

|變數名稱|變數值|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

若要安裝三個軟體套件，您要指定下列變數：  

|變數名稱|變數值|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

下列狀況會影響工作順序所安裝的套件：  

- 如果您未以正確格式建立變數的值，或該值未指定有效的套件識別碼和名稱，軟體安裝將會失敗。  

- 如果套件識別碼包含小寫字元，軟體安裝將會失敗。  

- 如果工作順序找不到具有指定基底名稱和 "001" 尾碼的變數，工作順序便不會安裝任何套件。 工作順序會繼續進行。  

> [!Important]  
> 這些值會區分大小寫。 例如，"install" 不同於 "Install"。 如果您需要變更值，工作順序編輯器不會偵測到大小寫的變更。 請同時進行另一個編輯，例如修改步驟描述。<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>如果某個軟體套件安裝失敗，繼續安裝清單中其他套件

此設定指定如果個別軟體套件安裝失敗，步驟將繼續進行。 如果您指定此設定，則不論發生任何安裝錯誤，工作順序都會繼續進行。 如果您未指定此設定，而且安裝失敗，步驟就會立即結束。  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> 安裝軟體更新

您可以使用此步驟，在目的地電腦上安裝軟體更新。 直到此工作順序步驟執行之後，才會評估目的地電腦是否有適用的軟體更新。 執行之後，才會評估目的地電腦適用的軟體更新，就像任何其他 Configuration Manager 用戶端一樣。 若要讓此步驟安裝軟體更新，請先將更新部署到目標電腦所屬的集合。  

> [!IMPORTANT]  
> 為了獲得最佳效能，請安裝最新版的「Windows Update 代理程式」。  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [軟體]  ，然後選取 [安裝軟體更新]  。

### <a name="variables-for-install-software-updates"></a>適用於 [安裝軟體更新] 的變數

請搭配此步驟使用下列工作順序變數：  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> 如果用戶端無法從位置服務擷取管理點清單，請使用 **SMSTSMPListRequestTimeoutEnabled** 和 **SMSTSMPListRequestTimeout** 變數。 這些變數可指定工作順序在重新嘗試安裝應用程式或軟體更新之前，需等候多少毫秒。 如需詳細資訊，請參閱[工作順序變數](task-sequence-variables.md)。  

### <a name="cmdlets-for-install-software-updates"></a>適用於 [安裝軟體更新] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepinstallupdate?view=sccm-ps) \(英文\)
- [New-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepinstallupdate?view=sccm-ps) \(英文\)
- [Remove-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepinstallupdate?view=sccm-ps) \(英文\)
- [Set-CMTSStepInstallUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepinstallupdate?view=sccm-ps) \(英文\)

如需更多建議與此步驟的技術流程圖表，請參閱[安裝軟體更新](install-software-updates.md)。

### <a name="properties-for-install-software-updates"></a>適用於 [安裝軟體更新] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>安裝必備 - 僅限強制軟體更新

選取此選項可使用系統管理員定義的安裝期限，安裝所有必要的軟體更新。  

#### <a name="available-for-installation---all-software-updates"></a>可供安裝 - 所有軟體更新

選取此選項可安裝所有可用的軟體更新。 請先將這些更新部署到電腦所屬的集合。 工作順序會將所有可用的軟體更新安裝在目的地電腦上。  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>從快取掃描結果評估軟體更新

此步驟預設會使用來自「Windows Update 代理程式」的快取掃描結果。 停用此選項可指示「Windows Update 代理程式」從軟體更新點下載最新的類別目錄。 使用工作順序來[擷取並建立 OS 映像](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)時，請啟用此選項。 在此情況下，可能會有大量的軟體更新。

這些更新中有許多都具有相依性。 例如，必須先安裝 ABC 更新，XYZ 更新才會顯示為適用。 停用此設定並將工作順序部署到許多用戶端時，所有用戶端都會同時連線至軟體更新點。 此行為會導致在處理和下載更新類別目錄時，發生效能問題。

在大多數情況下，請使用預設設定以使用快取掃描結果。

**SMSTSSoftwareUpdateScanTimeout** 變數可在此步驟期間控制軟體更新掃描逾時。 預設值為 60 分鐘。 如需詳細資訊，請參閱[工作順序變數](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)。

### <a name="options-for-install-software-updates"></a>適用於 [安裝軟體更新] 的選項

除了預設選項之外，請在此工作順序步驟的 [選項]  索引標籤上設定下列其他設定：  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>如果電腦非預期地重新啟動則重試此步驟

如果其中一個更新非預期地重新啟動電腦，請重試這個步驟。 根據預設，此步驟會以兩次重試次數啟用這個設定。 您可以指定一到五次的重試次數。  

> [!NOTE]  
> 設定 **SMSTSWaitForSecondReboot** 變數可指定在此情況下重新啟動電腦之後，工作順序要暫停的秒數。 如需詳細資訊，請參閱[工作順序變數](task-sequence-variables.md#SMSTSWaitForSecondReboot)。  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> 加入網域或工作群組

您可以使用此步驟，將目的地電腦新增至工作群組或網域。  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [一般]  ，然後選取 [加入網域或工作群組]  。

### <a name="variables-for-join-domain-or-workgroup"></a>適用於 [加入網域或工作群組] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>適用於 [加入網域或工作群組] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup?view=sccm-ps) \(英文\)
- [New-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup?view=sccm-ps) \(英文\)
- [Remove-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup?view=sccm-ps) \(英文\)
- [Set-CMTSStepJoinDomainWorkgroup](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup?view=sccm-ps) \(英文\)

### <a name="properties-for-join-domain-or-workgroup"></a>適用於 [加入網域或工作群組] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="join-a-workgroup"></a>加入工作群組

選取此選項可讓目的地電腦加入指定的工作群組。 如果電腦目前是網域的成員，選取此選項會導致電腦重新開機。  

#### <a name="join-a-domain"></a>加入網域

選取此選項可讓目的地電腦加入指定的網域。  

您可以選擇輸入或瀏覽指定網域中的組織單位 (OU)，以讓電腦加入。 如果電腦目前是某個其他網域或工作群組的成員，此選項會導致電腦重新開機。 如果電腦已經是另一個 OU 的成員，由於 Active Directory Domain Services 不允許透過這個方法來變更 OU，因此 Windows 安裝程式會忽略此設定。  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>輸入有權加入網域的帳戶

選取 [設定]  以輸入有權加入網域之帳戶的使用者名稱與密碼。 請使用下列格式來輸入帳戶：`Domain\account`。 如需有關工作順序網域連接帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)。  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> 準備 ConfigMgr 用戶端以進行擷取

您可以使用此步驟，在參照電腦上移除或設定 Configuration Manager 用戶端。 這個動作會準備電腦以供擷取作為映像處理程序的一部分。

此步驟會完全移除 Configuration Manager 用戶端，而不只是移除金鑰資訊。 當工作順序部署所擷取的 OS 映像時，每次都會安裝新的 Configuration Manager 用戶端。  

> [!Note]  
> 工作順序引擎只會在 [建立並擷取參照作業系統映像]  工作順序期間移除用戶端。 工作順序引擎不會在其他擷取方法 (例如擷取媒體或自訂工作順序) 期間移除用戶端。  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [準備 ConfigMgr 用戶端以進行擷取]  。

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>適用於 [準備 ConfigMgr 用戶端以進行擷取] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient?view=sccm-ps) \(英文\)
- [New-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient?view=sccm-ps) \(英文\)
- [Remove-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient?view=sccm-ps) \(英文\)
- [Set-CMTSStepPrepareConfigMgrClient](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient?view=sccm-ps) \(英文\)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> 準備 Windows 以進行擷取

您可以使用此步驟，在擷取參照電腦上的 OS 映像時，指定 Sysprep 選項。 此步驟會執行 Sysprep，然後讓電腦在重新開機時進入為工作順序指定的 Windows PE 開機映像。 如果參照電腦已加入網域，此動作將會失敗。  

此步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [準備 Windows 以進行擷取]  。

### <a name="variables-for-prepare-windows-for-capture"></a>適用於 [準備 Windows 以進行擷取] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>適用於 [準備 Windows 以進行擷取] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows?view=sccm-ps) \(英文\)
- [New-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepPrepareWindows?view=sccm-ps) \(英文\)
- [Remove-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows?view=sccm-ps) \(英文\)
- [Set-CMTSStepPrepareWindows](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows?view=sccm-ps) \(英文\)

### <a name="properties-for-prepare-windows-for-capture"></a>適用於 [準備 Windows 以進行擷取] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="automatically-build-mass-storage-driver-list"></a>自動建置大型存放驅動程式清單

選取此選項，讓 Sysprep 自動從參照電腦建置大型存放驅動程式清單。 此選項會在參照電腦上的 sysprep.inf 檔案中，啟用 [建置大型存放驅動程式] 選項。 如需此設定的詳細資訊，請參閱 Sysprep 文件。  

#### <a name="do-not-reset-activation-flag"></a>不要重設啟動旗標

選取此選項可防止 Sysprep 重設產品啟動旗標。  

#### <a name="shutdown-the-computer-after-running-this-action"></a>在執行此動作後將電腦關機

<!--SCCMDocs-pr issue 2695-->
此選項會指示 Sysprep 將電腦關機，而不是執行其預設的重新啟動行為。

[適用於現有裝置的 Windows Autopilot](../deploy-use/windows-autopilot-for-existing-devices.md) 工作順序會搭配此選項使用此步驟。

- 若要讓工作順序重新整理裝置並立即啟動適用於 Autopilot 的 OOBE ，請將此選項維持為關閉狀態。  

- 在建立映像之後啟用此選項以將裝置關機。 接著，您可以將裝置提供給使用者，讓使用者在第一次開啟裝置電源時啟動具有 Autopilot 的 OOBE。  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> 預先佈建 BitLocker

您可以使用此步驟，在 Windows PE 中啟用磁碟機上的 BitLocker。 預設只會加密已使用的磁碟空間，因此加密速度快許多。 您可以在安裝 OS 之後，使用[啟用 BitLocker](#BKMK_EnableBitLocker) 步驟來套用金鑰管理選項。

> [!IMPORTANT]
> 預先佈建的 BitLocker 需要電腦具有已支援且啟用的信賴平台模組 (TPM)。

此步驟只會在 Windows PE 中執行。 它不會在完整 OS 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [磁碟]  ，然後選取 [預先佈建 BitLocker]  。

### <a name="cmdlets-for-pre-provision-bitlocker"></a>適用於 [預先佈建 BitLocker] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker?view=sccm-ps) \(英文\)
- [New-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker?view=sccm-ps) \(英文\)
- [Remove-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker?view=sccm-ps) \(英文\)
- [Set-CMTSStepOfflineEnableBitLocker](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker?view=sccm-ps) \(英文\)

### <a name="properties-for-pre-provision-bitlocker"></a>適用於 [預先佈建 BitLocker] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>將 BitLocker 套用至指定的磁碟機

指定您要啟用 BitLocker 的磁碟機。 BitLocker 只會加密磁碟機上已使用的空間。  

#### <a name="use-full-disk-encryption"></a>使用完整磁碟加密

<!--SCCMDocs-pr issue 2671-->
此步驟預設只會加密磁碟機上已使用的空間。 建議使用此預設行為，因為它的速度更快且更具效率。 如果您的組織需要在安裝期間加密整個磁碟機，則請啟用此選項。 Windows 安裝程式會等待整個磁碟機加密，這需要很長的時間，特別是在大型磁碟機上。

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>針對沒有 TPM 的電腦，或是未啟用 TPM 時，略過此步驟

選取此選項可在未包含已支援或啟用之 TPM 的電腦上，略過磁碟機加密。 例如，將 OS 部署至虛擬機器時，請使用此選項。  



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> 和 [釋放狀態存放區]

您可以使用此步驟來通知狀態移轉點，擷取或還原動作已完成。 此步驟可與 [要求狀態存放區]  、[擷取使用者狀態]  和 [還原使用者狀態]  步驟搭配使用。 請使用這些步驟，利用狀態移轉點和使用者狀態移轉工具 (USMT) 來移轉使用者狀態資料。  

如需在部署作業系統時管理使用者狀態的詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

如果您使用 [要求狀態存放區]  步驟來要求存取狀態移轉點以「擷取」  使用者狀態，此步驟會通知狀態移轉點擷取程序已完成。 狀態移轉點隨後會將使用者狀態資料標示為可供還原。 狀態移轉點會針對使用者狀態資料設定存取控制權限，只讓進行還原的電腦擁有唯讀存取權。  

如果您使用 [要求狀態存放區]  步驟來要求存取狀態移轉點以「還原」  使用者狀態，此步驟會通知狀態移轉點還原程序已完成。 狀態移轉點接著就會啟動其設定的資料保留設定。  

> [!IMPORTANT]  
> 請為 [要求狀態存放區]  和 [釋放狀態存放區]  步驟間的所有步驟，設定 [發生錯誤時仍繼續]  選項。 每個 [要求狀態存放區]  步驟都必須具有相符的 [釋放狀態存放區]  步驟。  

此步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [使用者狀態]  ，然後選取 [釋放狀態存放區]  。

### <a name="variables-for-release-state-store"></a>適用於 [釋放狀態存放區] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>適用於 [釋放狀態存放區] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore?view=sccm-ps) \(英文\)
- [New-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore?view=sccm-ps) \(英文\)
- [Remove-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore?view=sccm-ps) \(英文\)
- [Set-CMTSStepReleaseStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore?view=sccm-ps) \(英文\)

### <a name="properties-for-release-state-store"></a>適用於 [釋放狀態存放區] 的屬性

此步驟不需要在 [內容]  索引標籤上進行任何設定。



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> 工作順序步驟來搭配 [要求狀態存放區]

您可以使用此步驟，在擷取或還原狀態時，要求存取狀態移轉點。  

如需在部署作業系統時管理使用者狀態的詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

此步驟可與 [釋放狀態存放區]  、[擷取使用者狀態]  和 [還原使用者狀態]  步驟搭配使用。 請使用這些步驟，利用狀態移轉點和使用者狀態移轉工具 (USMT) 來移轉電腦狀態。  

> [!NOTE]  
> 建立新的狀態移轉點時，最長會有一小時無法使用使用者狀態存放裝置。 若要加速使其可用，請調整狀態移轉點的任何內容設定，以觸發網站控制檔案更新。  

就離線 USMT 而言，此步驟可在完整 OS 和 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [使用者狀態]  ，然後選取 [要求狀態存放區]  。

### <a name="variables-for-request-state-store"></a>適用於 [要求狀態存放區] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>適用於 [要求狀態存放區] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore?view=sccm-ps) \(英文\)
- [New-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRequestStateStore?view=sccm-ps) \(英文\)
- [Remove-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore?view=sccm-ps) \(英文\)
- [Set-CMTSStepRequestStateStore](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore?view=sccm-ps) \(英文\)

### <a name="properties-for-request-state-store"></a>適用於 [要求狀態存放區] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="capture-state-from-the-computer"></a>從電腦擷取狀態

尋找符合狀態移轉點設定中設定之最低需求的狀態移轉點。 例如，[用戶端數目上限]  和 [可用磁碟空間數量下限]  。 此選項不保證在移轉狀態時會有足夠的空間可用。 此選項會要求存取狀態移轉點，以從電腦擷取使用者狀態和設定。  

如果 Configuration Manager 站台有多個使用中的狀態移轉點，此步驟會尋找含有可用磁碟空間的狀態移轉點。 工作順序會向管理點查詢狀態移轉點的清單，然後評估每個狀態移轉點，直到找到符合最低需求的狀態移轉點為止。  

#### <a name="restore-state-from-another-computer"></a>從另一部電腦還原狀態

要求存取狀態移轉點，以將先前擷取的使用者狀態和設定還原至目的地電腦。  

如果有多個狀態移轉點，此步驟會尋找具有目的地電腦之狀態的狀態移轉點。  

#### <a name="number-of-retries"></a>重試次數

此步驟將嘗試尋找適當狀態移轉點的次數，超過即失敗。  

#### <a name="retry-delay-in-seconds"></a>重試延遲 (以秒為單位)

工作順序步驟嘗試重試的時間間隔，以秒為單位。  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>如果電腦帳戶無法連線到狀態存放區，則使用網路存取帳戶

如果工作順序無法使用電腦帳戶來存取狀態移轉點，它會使用網路存取帳戶認證來進行連線。 這是較不安全的選項，因為其他電腦可以使用網路存取帳戶來存取儲存的狀態。 如果目的地電腦未加入網域，則可能必須使用這個選項。  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> 重新啟動電腦

您可以使用此步驟來重新啟動執行工作順序的電腦。 重新啟動之後，電腦會自動繼續執行工作順序中的下一個步驟。  

此步驟可在完整 OS 或 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [使用者狀態]  ，然後選取 [要求狀態存放區]  。

### <a name="variables-for-restart-computer"></a>適用於 [重新啟動電腦] 的變數

請搭配此步驟使用下列工作順序變數：  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>適用於 [重新啟動電腦] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepreboot?view=sccm-ps) \(英文\)
- [New-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepreboot?view=sccm-ps) \(英文\)
- [Remove-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepreboot?view=sccm-ps) \(英文\)
- [Set-CMTSStepReboot](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepreboot?view=sccm-ps) \(英文\)

### <a name="properties-for-restart-computer"></a>適用於 [重新啟動電腦] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>指派給此工作順序的開機映像

為目的地電腦選取此選項，以使用指派給工作順序的開機映像。 工作順序會使用開機映像，在 Windows PE 中執行後續步驟。  

#### <a name="the-currently-installed-default-operating-system"></a>目前已安裝的預設作業系統

為目標電腦選取此選項，即可在重新開機時進入已安裝的 OS。  

#### <a name="notify-the-user-before-restarting"></a>重新啟動之前通知使用者

選取此選項可在重新啟動目的地電腦之前，對使用者顯示通知。 此步驟預設會選取這個選項。  

#### <a name="notification-message"></a>通知訊息

輸入在重新啟動目的地電腦之前，要對使用者顯示的通知訊息。  

#### <a name="message-display-time-out"></a>訊息顯示逾時

指定在重新啟動目的地電腦之前的時間量 (以秒為單位)。 預設值是 60 秒。  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> 還原使用者狀態

您可以使用此步驟來起始使用者狀態移轉工具 (USMT)，將使用者狀態和設定還原至目的地電腦。 請將此步驟與 [擷取使用者狀態]  步驟搭配使用。  

如需在部署作業系統時管理使用者狀態的詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

將此步驟與 [要求狀態存放區]  和 [釋放狀態存放區]  步驟搭配使用，可使用狀態移轉點儲存或還原狀態設定。 此步驟會一律使用 Configuration Manager 所產生和管理的加密金鑰，來將 USMT 狀態存放區解密。  

[還原使用者狀態]  步驟可讓您控制最常用的 USMT 選項的有限子集。 請使用 **OSDMigrateAdditionalRestoreOptions** 變數來指定額外的命令列選項。  

> [!IMPORTANT]  
> 如果您將此步驟用於與 OS 部署案例無關的用途，請在 [還原使用者狀態]  步驟後面，緊接著新增[重新啟動電腦](#BKMK_RestartComputer)步驟。  

此步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  ，選取 [使用者狀態]  ，然後選取 [還原使用者狀態]  。

### <a name="variables-for-restore-user-state"></a>適用於 [還原使用者狀態] 的變數

請搭配此步驟使用下列工作順序變數：  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>適用於 [還原使用者狀態] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState?view=sccm-ps) \(英文\)
- [New-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepRestoreUserState?view=sccm-ps) \(英文\)
- [Remove-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState?view=sccm-ps) \(英文\)
- [Set-CMTSStepRestoreUserState](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState?view=sccm-ps) \(英文\)

### <a name="properties-for-restore-user-state"></a>適用於 [還原使用者狀態] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="user-state-migration-tool-package"></a>使用者狀態移轉工具套件

指定包含此步驟要使用之 USMT 版本的套件。 此套件不需要程式。 執行此步驟時，工作順序會使用指定套件中的 USMT 版本。 指定包含 USMT 的 32 位元或 64 位元版本的套件。 USMT 的架構取決於工作順序還原狀態時目的地 OS 的架構。

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>以標準選項還原所有擷取的使用者設定檔

以標準選項還原所擷取的使用者設定檔。 若要自訂 USMT 還原的選項，請選取 [自訂使用者設定檔擷取]  。  

#### <a name="customize-how-user-profiles-are-restored"></a>自訂如何還原使用者設定檔

可讓您自訂您要還原至目的地電腦的檔案。 選取 [檔案]  ，以指定您要在 USMT 套件中用來還原使用者設定檔的組態檔。 若要新增組態檔，請在 [檔案名稱]  方塊中輸入檔案名稱，然後選取 [新增]  。 [檔案] 窗格會列出 USMT 所使用的設定檔。 您指定的 .xml 檔案會定義 USMT 將還原哪些使用者檔案。  

#### <a name="restore-local-computer-user-profiles"></a>還原本機電腦使用者設定檔

還原本機電腦使用者設定檔。 這些設定檔不適用於網域使用者。 請指派新密碼給所還原的本機使用者帳戶。 USMT 無法移轉原始密碼。 在 [密碼]  方塊中輸入新密碼，然後在 [確認密碼]  方塊中確認密碼。  

#### <a name="continue-if-some-files-cannot-be-restored"></a>無法還原部分檔案時仍繼續

即使 USMT 無法還原某些檔案，仍繼續還原使用者狀態和設定。 此步驟預設會啟用這個選項。 如果停用這個選項，而且 USMT 在還原檔案時發生錯誤，此步驟會立即失敗。 USMT 不會還原所有檔案。

#### <a name="enable-verbose-logging"></a>啟用詳細資訊記錄

啟用此選項可產生較詳細的記錄檔資訊。 還原狀態時，工作順序預設會在 `%WinDir%\ccm\logs` 工作順序記錄檔資料夾中產生 **Loadstate.log**。  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> 執行命令列

您可以使用此步驟來執行指定的命令列。  

此步驟可在完整 OS 或 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  ，選取 [一般]  ，然後選取 [執行命令列]  。

### <a name="variables-for-run-command-line"></a>適用於 [執行命令列] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (從 1902 版開始)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (從 2002 版開始)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>適用於 [執行命令列] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepruncommandline?view=sccm-ps) \(英文\)
- [New-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepruncommandline?view=sccm-ps) \(英文\)
- [Remove-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepruncommandline?view=sccm-ps) \(英文\)
- [Set-CMTSStepRunCommandLine](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepruncommandline?view=sccm-ps) \(英文\)

### <a name="properties-for-run-command-line"></a>適用於 [執行命令列] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="command-line"></a>命令列

指定工作順序所執行的命令列。 此為必要欄位。 請包括副檔名，例如 .vbs 和 .exe。 請包括所有必要的設定檔案和命令列選項。  

如果您未指定副檔名，Configuration Manager 會嘗試使用 .com、.exe 及 .bat。 如果檔案名稱的副檔名不是可執行檔類型，Configuration Manager 就會嘗試套用本機關聯。 例如，如果命令列是 readme.gif，則 Configuration Manager 會啟動目的地電腦上指定的應用程式，以開啟 .gif 檔案。  

範例：  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> 若要成功執行，請在命令列動作前面加上 **cmd.exe /c** 命令。 這些動作的範例包括輸出重新導向、管線以及複製命令。  

#### <a name="output-to-task-sequence-variable"></a>輸出為工作順序變數

<!--user story 4977616/bug 4798352-->

從 1910 版開始，可以將命令輸出儲存至自訂工作順序變數中。

> [!Note]  
> Configuration Manager 會將此輸出限制為最後 1000 個字元。

#### <a name="disable-64-bit-file-system-redirection"></a>停用 64 位元檔案系統重新導向

64 位元作業系統預設會使用 WOW64 檔案系統重新導向器來執行命令列。 此行為是為了正確找到 32 位元版本的 OS 可執行檔和程式庫。 選取此選項可停用 WOW64 檔案系統重新導向器。 Windows 會使用原生的 64 位元版 OS 可執行檔和程式庫來執行命令。 在 32 位元 OS 上執行時，此選項沒有作用。  

#### <a name="start-in"></a>啟動位置

指定程式的可執行檔資料夾，最多 127 個字元。 此資料夾可以是目的地電腦上的絕對路徑，或是含有套件之發佈點資料夾的相對路徑。 此為選擇性欄位。  

範例：  

`c:\officexp`  

`i386`  

> [!NOTE]  
> [瀏覽]  按鈕會瀏覽本機電腦中的檔案和資料夾。 您選取的任何項目都必須也存在於目的地電腦上。 它必須存在於相同的位置中，且具有相同的檔案和資料夾名稱。  

#### <a name="package"></a>套件

當您在命令列上指定目的地電腦中尚未存在的檔案或程式時，請選取此選項來指定含有必要檔案的 Configuration Manager 套件。 此套件不需要程式。 如果指定的檔案存在於目的地電腦上，則無須使用這個選項。  

#### <a name="time-out"></a>逾時

指定一個值，用來表示 Configuration Manager 允許命令列執行多久。 這個值可以從 1 分鐘到 999 分鐘。 預設值為 15 分鐘。 預設會停用這個選項。  

> [!IMPORTANT]  
> 如果您輸入的值未提供足夠的時間讓指定的命令順利完成，此步驟將會失敗。 視步驟或群組條件而定，整個工作順序可能會失敗。 如果超過逾時值，Configuration Manager 會終止命令列程序。  

#### <a name="run-this-step-as-the-following-account"></a>以下列帳戶執行這個步驟

指定以 Windows 使用者帳戶而非本機系統帳戶身分來執行命令列。  

> [!NOTE]  
> 若要在安裝 OS 之後，以另一個帳戶執行簡單的指令碼或命令，請先將該帳戶新增至電腦。 此外，您可能必須還原 Windows 使用者設定檔，才能執行較複雜的程式，例如 Windows Installer。  

#### <a name="account"></a>帳戶

指定此步驟用來執行命令列的 Windows 使用者帳戶。 將會以指定帳戶的權限來執行命令列。 選取 [設定]  指定本機使用者或網域帳戶。 如需有關工作順序執行身分帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)。

> [!IMPORTANT]  
> 如果這個步驟指定使用者帳戶，並在 Windows PE 中執行，此動作將會失敗。 您無法將 Windows PE 加入網域。 **smsts.log** 檔案中會記錄此失敗。  

### <a name="options-for-run-command-line"></a>適用於 [執行命令列] 的選項

除了預設選項之外，請在此工作順序步驟的 [選項]  索引標籤上設定下列其他設定：  

#### <a name="success-codes"></a>成功碼

包含其他的結束代碼，這些結束代碼來自步驟應評估為成功的指令碼。



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> 執行 PowerShell 指令碼

您可以使用此步驟來執行指定的 Windows PowerShell 指令碼。  

此步驟可在完整 OS 或 Windows PE 中執行。 若要在 Windows PE 中執行此步驟，請在開機映像中啟用 PowerShell。 請從開機映像內容中的 [選用元件]  索引標籤啟用 WinPE-PowerShell 元件。 如需如何修改開機映像的詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

> [!NOTE]  
> 在 Windows Embedded 作業系統上，預設不會啟用 PowerShell。  

> [!WARNING]
> 某些反惡意程式碼軟體可能會不小心針對「Configuration Manager 執行 PowerShell 指令碼」工作順序步驟觸發事件。 建議排除 %windir%\temp\smstspowershellscripts，讓反惡意程式碼軟體允許這些指令碼執行而不會受到干擾。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [一般]  ，然後選取 [執行 PowerShell 指令碼]  。

### <a name="variables-for-run-powershell-script"></a>適用於 [執行 PowerShell 指令碼] 的變數

請搭配此步驟使用下列工作順序變數：  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (從 1902 版開始)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (從 2002 版開始)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>適用於 [執行 PowerShell 指令碼] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtssteprunpowershellscript?view=sccm-ps) \(英文\)
- [New-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtssteprunpowershellscript?view=sccm-ps) \(英文\)
- [Remove-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript?view=sccm-ps) \(英文\)
- [Set-CMTSStepRunPowerShellScript](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtssteprunpowershellscript?view=sccm-ps) \(英文\)

> [!Note]  
> 請使用已簽屬且格式為 Unicode 的 PowerShell 指令碼。 預設的 ANSI 格式不適用於此步驟。

### <a name="properties-for-run-powershell-script"></a>適用於 [執行 PowerShell 指令碼] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="package"></a>套件

指定包含 PowerShell 指令碼的 Configuration Manager 套件。 一個套件可以包含多個 PowerShell 指令碼。  

#### <a name="script-name"></a>指令碼名稱

指定所要執行的 PowerShell 指令碼名稱。 此為必要欄位。  

#### <a name="enter-a-powershell-script"></a>輸入 PowerShell 指令碼

<!-- 3556028 -->
從 1902 版開始，可以在此步驟中直接輸入 Windows PowerShell 程式碼。 此功能可讓您在工作順序期間執行 PowerShell 命令，而不需要先使用指令碼來建立和發佈套件。

當您新增或編輯指令碼時，PowerShell 指令碼視窗會提供下列動作：  

- 直接編輯指令碼  

- 從檔案開啟現有的指令碼  

- 瀏覽至 Configuration Manager 中現有的已核准[指令碼](../../apps/deploy-use/create-deploy-scripts.md)

> [!Important]  
> 若要利用此 Configuration Manager 新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

#### <a name="parameters"></a>參數

指定傳遞給 PowerShell 指令碼的參數。 這些參數與命令列上的 PowerShell 指令碼參數相同。  

提供指令碼所使用的參數，而不是要用於 Windows PowerShell 命令列。  
下列範例包含有效的參數：  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

下列範例包含無效的參數： 前兩個項目是 Windows PowerShell 命令列參數 ( **-NoLogo** 和 **-ExecutionPolicy Unrestricted**)。 指令碼不會使用這些參數。  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
如果參數值包含特殊字元，請使用單引號 (`'`) 括住值。 使用雙引號 (`"`) 可能會導致工作順序步驟不正確地處理參數。

例如：`-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

從 2002 版開始，請將此屬性設定為變數。<!-- 5690481 --> 例如，若您指定 `%MyScriptVariable%`則會在工作順序執行指令碼時，將此自訂變數的值新增至 PowerShell 命令列。

#### <a name="powershell-execution-policy"></a>PowerShell 執行原則

決定您允許在電腦上執行的 PowerShell 指令碼 (如果有的話)。 選擇下列其中一個執行原則：  

- **所有已簽署項目**：僅執行由受信任的發行者簽署的指令碼  

- **未定義**：不定義任何執行原則  

- **略過**：載入所有設定檔，並執行所有指令碼。 如果您從網際網路下載未簽署的指令碼，Windows PowerShell 在執行該指令碼之前，不會提示您許可。  

> [!IMPORTANT]  
> PowerShell 1.0 不支援 [未定義] 和 [略過] 執行原則。  

#### <a name="output-to-task-sequence-variable"></a>輸出為工作順序變數

<!-- 3556028 -->
從 1902 版開始，可以將指令碼輸出儲存至自訂工作順序變數中。

> [!Note]  
> 從 1910 版開始，Configuration Manager 會將此輸出限制為最後 1000 個字元。

如需如何使用此步驟屬性的範例，請參閱[如何設定變數](using-task-sequence-variables.md#bkmk_run-ps)。

#### <a name="start-in"></a>啟動位置

<!-- 3556028 -->
從 1902 版開始，可以指定指令碼的起始資料夾，最多 127 個字元。 此資料夾可以是目的地電腦上的絕對路徑，或是含有套件之發佈點資料夾的相對路徑。 此為選擇性欄位。  

> [!NOTE]  
> [瀏覽]  按鈕會瀏覽本機電腦中的檔案和資料夾。 您選取的任何項目都必須也存在於目的地電腦上。 它必須存在於相同的位置中，且具有相同的檔案和資料夾名稱。  

#### <a name="time-out"></a>逾時

<!-- 3556028 -->
從 1902 版開始，指定一個值，用來表示 Configuration Manager 允許 PowerShell 指令碼執行多久。 這個值可以從 1 分鐘到 999 分鐘。 預設值為 15 分鐘。 預設會停用這個選項。  

> [!IMPORTANT]  
> 如果您輸入的值未提供足夠的時間讓指定的指令碼順利完成，此步驟將會失敗。 視步驟或群組條件而定，整個工作順序可能會失敗。 如果超過逾時值，Configuration Manager 會終止 PowerShell 處理序。  

#### <a name="run-this-step-as-the-following-account"></a>以下列帳戶執行這個步驟

<!-- 3556028 -->
從 1902 版開始，指定以 Windows 使用者帳戶而非本機系統帳戶身分來執行 PowerShell 指令碼。  

> [!NOTE]  
> 若要在安裝 OS 之後，以另一個帳戶執行簡單的指令碼或命令，請先將該帳戶新增至電腦。 此外，您可能必須還原 Windows 使用者設定檔，才能執行較複雜的動作。  

#### <a name="account"></a>帳戶

<!-- 3556028 -->
從 1902 版開始，可以指定此步驟用來執行 PowerShell 指令碼的 Windows 使用者帳戶。 指定的帳戶必須是系統上的本機系統管理員，而且指令碼會以此帳戶的權限執行。 選取 [設定]  指定本機使用者或網域帳戶。 如需有關工作順序執行身分帳戶的詳細資訊，請參閱[帳戶](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)。

> [!IMPORTANT]  
> 如果這個步驟指定使用者帳戶，並在 Windows PE 中執行，此動作將會失敗。 您無法將 Windows PE 加入網域。 **smsts.log** 檔案中會記錄此失敗。  

### <a name="options-for-run-powershell-script"></a>適用於 [執行 PowerShell 指令碼] 的選項

除了預設選項之外，請在此工作順序步驟的 [選項]  索引標籤上設定下列其他設定：  

#### <a name="success-codes"></a>成功碼

<!-- 3556028 -->
從 1902 版開始，包含其他的結束代碼，這些結束代碼來自步驟應評估為成功的指令碼。



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> 執行工作順序

> [!Note]  
> 在 1910 版中，Configuration Manager 預設會啟用此功能。 在 1906 版或更早版本中，Configuration Manager 預設不會啟用此選擇性功能。 請先啟用這項功能再使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。

此步驟會執行其他工作順序。 它會建立工作順序之間的父子關聯性。 您可利用子工作順序來建立更多模組化且可重複使用的工作順序。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  ，選取 [一般]  ，然後選取 [執行工作順序]  。

### <a name="specifications-and-limitations-for-run-task-sequence"></a>適用於 [執行工作順序] 的規格和限制

為工作順序新增子工作順序時，請考慮下列幾點：  

- 父工作順序和子工作順序會有效地結合成用戶端執行的單一原則。  

- 環境是全域的。 如果父工作順序設定某個變數，而子工作順序接著變更該變數，它會保留最新的值。 如果子工作順序會建立新變數，該變數將可供父工作順序的其餘部分使用。  

- 針對單一工作順序作業，將會按一般的方式傳送狀態訊息。  

- 工作順序會將項目寫入 **smsts.log** 檔案中，其中會有可清楚交代子工作順序何時開始的新記錄項目。  

<!--the following points are from SCCMdocs issue #1079-->

- 您無法選取具有開機映像參考的工作順序。 針對需要開機映像的任何部署，請在父工作順序上指定它。  

- 若子工作順序已停用，則部署會失敗。 您無法使用 [錯誤時繼續]  選項來規避此限制。  

- 若子工作順序包含被認為具有高影響力  ，則軟體中心不會偵測到它並顯示高影響力通知。 在 [使用者通知] 索引標籤上修改父工作順序的屬性，以指定 [這是影響很高的工作順序]  。  

- 若子工作順序具有遺失的套件參考，檢閱父工作順序不會偵測到此狀態。 若您編輯父工作順序，當您變更父工作順序時，它會偵測子工作順序中任何遺失的參考。  

### <a name="cmdlets-for-run-task-sequence"></a>適用於 [執行工作順序] 的 Cmdlet

從 1906 版起，使用下列 PowerShell Cmdlet 來管理此步驟：<!-- 2839943, SCCMDocs#1118 -->

- **Get-CMTSStepRunTaskSequence**
- **New-CMTSStepRunTaskSequence**
- **Remove-CMTSStepRunTaskSequence**
- **Set-CMTSStepRunTaskSequence**

如需詳細資訊，請參閱 [1906 版本資訊 - 新的 Cmdlet](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps#new-cmdlets) \(部分機器翻譯\)。

### <a name="properties-for-run-task-sequence"></a>適用於 [執行工作順序] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="select-task-sequence-to-run"></a>選取要執行的工作順序

選取 [瀏覽]  以選取子工作順序。 [選取工作順序]  對話方塊不會顯示父工作順序。



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> 設定動態變數

您可以使用此步驟來執行下列動作：  

1. 從電腦及其環境收集資訊。 然後使用該資訊來設定指定的工作順序變數。  

2. 評估已定義的規則。 根據評估為 true 的規則來設定工作順序變數。  

此步驟可在完整 OS 或 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [一般]  ，然後選取 [設定動態變數]  。

### <a name="variables-for-set-dynamic-variables"></a>適用於 [設定動態變數] 的變數

工作順序會自動設定下列唯讀的工作順序變數：  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>適用於 [設定動態變數] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable?view=sccm-ps) \(英文\)
- [New-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable?view=sccm-ps) \(英文\)
- [Remove-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable?view=sccm-ps) \(英文\)
- [Set-CMTSStepSetDynamicVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable?view=sccm-ps) \(英文\)

### <a name="properties-for-set-dynamic-variables"></a>適用於 [設定動態變數] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="dynamic-rules-and-variables"></a>動態規則和變數

若要設定動態變數，以便在工作順序中使用，請新增規則。 接著，為規則中指定的每個變數設定一個值。 此外，新增一或多個變數，而不新增規則。 當您新增規則時，請從下列類別中進行選擇：  

- **電腦**：評估硬體資產標籤、UUID、序號或 MAC 位址的值。 視需要設定多個值。 如果任何值為 true，規則就會評估為 true。 例如，如果裝置序號是 5892087，且 MAC 位址是 22-A4-5A-13-78-26，下列規則就會評估為 true：  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **位置：** 評估預設網路閘道的值  

- **廠牌與型號**：評估電腦廠牌和型號的值。 製造商和型號都必須評估為 true，規則才會評估為 true。

    請指定星號 (`*`) 和問號 (`?`) 作為萬用字元。 星號可比對多個字元，而問號則可比對單一字元。 例如，`DELL*900?` 字串可比對出 `DELL-ABC-9001` 和 `DELL9009`。  

- **工作順序變數**：新增工作順序變數、條件和要評估的值。 當為變數設定的值符合指定的條件時，規則會評估為 true。  

    指定要針對評估為 true 的規則設定的一或多個變數，或是設定變數而不使用規則。 選取現有的變數或建立自訂變數。  

    - **現有的工作順序變數**：從現有的工作順序變數清單中選取一或多個變數。 陣列變數不可供選取。  

    - **自訂工作順序變數**：定義自訂工作順序變數。 您也可以指定現有的工作順序變數。 此設定適合用來指定現有的變數陣列 (例如 **OSDAdapter**)，因為變數陣列不在現有的工作順序變數清單中。  

在為規則選取變數之後，請為每個變數提供一個值。 當規則評估為 true 時，變數會設為所指定的值。 您可以針對每個變數，選取 [祕密值]  來隱藏變數的值。 某些現有的變數預設會隱藏值，例如 **OSDCaptureAccountPassword** 變數。  

> [!IMPORTANT]  
> 當您使用 [設定動態變數]  步驟匯入工作順序時，Configuration Manager 會移除任何標示為 [祕密值]  的變數值。 在您匯入工作順序之後，請重新輸入動態變數的值。  



## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> 設定工作順序變數

您可以使用此步驟來設定與工作順序搭配使用的變數值。  

此步驟可在完整 OS 或 Windows PE 中執行。

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [一般]  ，然後選取 [設定工作順序變數]  。

### <a name="variables-for-set-task-sequence-variable"></a>適用於 [設定工作順序變數] 的變數

工作順序變數會被工作順序動作讀取，並指定那些動作的行為。 如需有關特定工作順序變數的詳細資訊及其用法，請參閱下列文章：  

- [如何使用工作順序變數](using-task-sequence-variables.md)  
- [工作順序變數](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>適用於 [設定工作順序變數] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetvariable?view=sccm-ps) \(英文\)
- [New-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetvariable?view=sccm-ps) \(英文\)
- [Remove-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetvariable?view=sccm-ps) \(英文\)
- [Set-CMTSStepSetVariable](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetvariable?view=sccm-ps) \(英文\)

### <a name="properties-for-set-task-sequence-variable"></a>適用於 [設定工作順序變數] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="task-sequence-variable"></a>工作順序變數

指定工作順序內建或動作變數的名稱，或指定您的使用者定義變數名稱。  

#### <a name="do-not-display-this-value"></a>不要顯示此值

<!--1358330-->
啟用此選項可遮罩儲存在工作順序變數中的敏感性資料。 例如，指定密碼時。

> [!Note]  
> 啟用此選項，然後設定工作順序變數的值。 否則，變數值不會依您想要的方式設定，這可能會在工作順序執行時導致非預期的行為。<!--SCCMdocs issue #800-->

#### <a name="value"></a>值  

工作順序會將變數設定為這個值。 請使用 `%varname%` 語法，將此工作順序變數設定為另一個工作順序變數的值。  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> varname

您可以使用此步驟從 Windows PE 轉換為新的 OS。 此工作順序步驟是部署任何 OS 的必要部分。 它會將 Configuration Manager 用戶端安裝到新的 OS 中，並做好讓工作順序繼續在新 OS 中執行的準備。  

此步驟負責將工作順序從 Windows PE 轉換為完整 OS。 因為此轉換，該步驟會在 Windows PE 與完整 OS 中執行。 不過，因為轉換是從 Windows PE 開始，所以只能在工作順序的 Windows PE 部分期間新增。  

此步驟會以 Windows PE 安裝目錄 `X:\Windows`取代 sysprep.inf 或 unattend.xml 目錄變數 (例如 `%WINDIR%` 和 `%ProgramFiles%`)。 工作順序會忽略使用這些環境變數指定的變數。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [設定 Windows 和 ConfigMgr]  。

### <a name="behaviors-for-setup-windows-and-configmgr"></a>適用於 [設定 Windows 和 ConfigMgr] 的行為

此步驟會執行下列動作：  

#### <a name="preliminaries-windows-pe"></a>準備工作：Windows PE  

1. 替代 unattend.xml 檔案中的工作順序變數。  

2. 下載包含 Configuration Manager 用戶端的套件。 將套件新增至已部署的映像。  

#### <a name="set-up-windows"></a>設定 Windows  

- 以映像為基礎的安裝  

    1. 停用映像中的 Configuration Manager 用戶端 (如果存在的話)。 亦即，針對 Configuration Manager 用戶端服務停用自動啟動。  

    2. 更新已部署映像中的登錄，以使用與參照電腦相同的磁碟機代號來啟動已部署的 OS。  

    3. 重新啟動到已部署的 OS。  

    4. 執行 Windows 迷你安裝時，會使用先前指定的 sysprep.inf 或 unattend.xml 回應檔案，這些檔案會抑制所有使用者互動。 如果您使用 [套用網路設定]  步驟來加入網域，則該資訊位在回應檔案中。 Windows 迷你安裝會將電腦加入網域。  

- 以 Setup.exe 為基礎的安裝。 遵循一般 Windows 安裝程序來執行 Setup.exe：  

    1. 將 [套用作業系統]  步驟中指定的作業系統升級套件複製到硬碟上。  

    2. 重新啟動到新部署的 OS。  

    3. 執行 Windows 迷你安裝時，會使用先前指定的 sysprep.inf 或 unattend.xml 回應檔案，這些檔案會抑制所有使用者介面設定。 如果您使用 [套用網路設定]  步驟來加入網域，則該資訊位在回應檔案中。 Windows 迷你安裝會將電腦加入網域。  

#### <a name="set-up-the-configuration-manager-client"></a>設定 Configuration Manager 用戶端  

1. Windows 迷你安裝完成之後，工作順序會使用 setupcomplete.cmd 來繼續進行。 如需詳細資訊，請參閱[在安裝程式完成後執行指令碼 (SetupComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd) \(部分機器翻譯\)。  

2. 根據在 [套用 Windows 設定]  步驟中選取的選項，啟用或停用本機系統管理員帳戶。  

3. 使用先前下載的套件，以及此步驟中指定的安裝內容，來安裝 Configuration Manager 用戶端。 用戶端會以「佈建模式」進行安裝。 此模式可防止用戶端在工作順序完成前處理新的原則要求。 如需詳細資訊，請參閱[佈建模式](provisioning-mode.md)。  

4. 等候用戶端完全正常運作。  

#### <a name="the-step-completes"></a>步驟完成

工作順序會繼續執行下一個步驟。  

> [!Note]  
> 通常直到工作順序完成之後才會處理 Windows 群組原則。 此行為在不同 Windows 版本之間是一致的。 工作順序期間其他自訂動作可以觸發群組原則評估。 如需作業順序的詳細資訊，請參閱[在安裝程式完成後執行指令碼 (SetupComplete.cmd)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd) \(部分機器翻譯\)。 <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>適用於 [設定 Windows 和 ConfigMgr] 的變數

請搭配此步驟使用下列工作順序變數：  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>適用於 [設定 Windows 和 ConfigMgr] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps) \(英文\)
- [New-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps) \(英文\)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps) \(英文\)
- [Set-CMTSStepSetupWindowsAndConfigMgr](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr?view=sccm-ps) \(英文\)

### <a name="properties-for-setup-windows-and-configmgr"></a>適用於 [設定 Windows 和 ConfigMgr] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="client-package"></a>用戶端封裝

選取 [瀏覽]  ，然後選擇要與此步驟搭配使用的 Configuration Manager 用戶端安裝套件。  

#### <a name="use-pre-production-client-package-when-available"></a>使用進入生產階段前用戶端封裝 (可用時)

如果有生產階段前用戶端套件可用，而且電腦是試驗集合的成員，工作順序就會使用此套件，而不是生產環境用戶端套件。 進入生產階段前用戶端是要在生產環境中測試的較新版本。 選取 [瀏覽]  ，然後選擇要與此步驟搭配使用的生產階段前用戶端安裝套件。  

#### <a name="installation-properties"></a>安裝內容

工作順序步驟會自動指定站台指派和預設設定。 請使用此欄位來指定安裝用戶端時，所要使用的任何其他安裝內容。 若要輸入多個安裝內容，請以空格分隔。  

請指定要在用戶端安裝期間使用的命令列選項。 例如，輸入 `/skipprereq: silverlight.exe` 可通知 CCMSetup.exe 不要安裝 Microsoft Silverlight 先決條件。 如需 CCMSetup.exe 可用命令列選項的詳細資訊，請參閱[關於用戶端安裝內容](../../core/clients/deploy/about-client-installation-properties.md)。  

### <a name="options-for-setup-windows-and-configmgr"></a>適用於 [設定 Windows 和 ConfigMgr] 的選項

> [!NOTE]  
> 請勿啟用 [選項]  索引標籤上的 [發生錯誤時仍繼續]  。如果在此步驟期間發生錯誤，不論您是否啟用此設定，工作順序都會失敗。  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> 升級作業系統

您可以使用此步驟，將較舊版本的 Windows 升級至較新版本的 Windows 10。  

此工作順序步驟只會在完整 OS 中執行。 它不會在 Windows PE 中執行。  

若要在工作順序編輯器中新增此步驟，請選取 [新增]  、選取 [映像]  ，然後選取 [升級作業系統]  。

> [!TIP]
> 從 Windows 10 1709 版開始，媒體包含多個版本。 當您設定工作順序以使用作業系統升級套件或作業系統映像時，請務必選取[支援的版本](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)。  
>
> 在使用者安裝工作順序之前，請使用內容預先快取來下載適用的 OS 升級套件。 如需詳細資訊，請參閱[設定預先快取內容](../deploy-use/configure-precache-content.md)。

### <a name="variables-for-upgrade-os"></a>適用於 [升級 OS] 的變數

請搭配此步驟使用下列工作順序變數：  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>適用於 [升級 OS] 的 Cmdlet

使用下列 PowerShell Cmdlet 來管理此步驟：<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem?view=sccm-ps) \(英文\)
- [New-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem?view=sccm-ps) \(英文\)
- [Remove-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem?view=sccm-ps) \(英文\)
- [Set-CMTSStepUpgradeOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem?view=sccm-ps) \(英文\)

### <a name="properties-for-upgrade-os"></a>適用於 [升級 OS] 的屬性

在這個步驟的 [內容]  索引標籤上，設定本節中所描述的設定。  

#### <a name="upgrade-package"></a>升級封裝

選取此選項以指定要用於升級的 Windows 10 OS 升級套件。  

#### <a name="source-path"></a>來源路徑

指定 Windows 安裝程式所使用之 Windows 10 媒體的本機或網路路徑。 此設定會與 Windows 安裝程式命令列選項 `/InstallFrom` 對應。

您也可以指定變數，例如 `%MyContentPath%` 或 `%DPC01%`。 當您使用變數來代表來源路徑時，請在此工作順序中早一點設定好其值。 例如，使用[下載套件內容](#BKMK_DownloadPackageContent)步驟來指定代表 OS 升級套件位置的變數。 然後，使用該變數來代表此步驟中的來源路徑。  

#### <a name="edition"></a>版本

指定要用來進行升級的 OS 媒體內版本。  

#### <a name="product-key"></a>產品金鑰

指定要套用至升級程序的產品金鑰。  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>在升級期間將下列驅動程式內容提供給 Windows 安裝程式

在升級程序期間，將驅動程式新增至目的地電腦。 這些驅動程式必須與 Windows 10 相容。 此設定會與 Windows 安裝程式命令列選項 `/InstallDriver` 對應。 如需詳細資訊，請參閱 [Windows 安裝程式命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers) \(部分機器翻譯\)。

指定下列其中一個選項：  

- **驅動程式套件**：選取 [瀏覽]  ，然後從清單中選擇現有的驅動程式套件。

- **分段內容**：選取此選項以指定驅動程式內容的位置。 您可以指定本機資料夾、網路路徑或工作順序變數。 當您使用變數來代表來源路徑時，請在此工作順序中早一點設定好其值。 例如，藉由使用[下載套件內容](task-sequence-steps.md#BKMK_DownloadPackageContent)步驟。  

> [!TIP]
> 如果您想要有適用於多種硬體類型的動態內容：
>
> - 使用此步驟的多個執行個體，並設定適用於硬體類型和個別驅動程式內容的條件。
>
> - 使用[下載套件內容](task-sequence-steps.md#BKMK_DownloadPackageContent)步驟的多個執行個體。 將內容放置於通用位置，然後使用 [分段內容]  選項。 此方法的優點是工作順序會具有單一 [升級 OS]  步驟。

#### <a name="time-out-minutes"></a>逾時 (分鐘)

指定 Configuration Manager 讓此步驟失敗前的分鐘數。 如果 Windows 安裝程式會停止處理但並不終止，此選項便相當有用。  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>執行 Windows 安裝程式相容性掃描而不啟動升級

執行 Windows 安裝程式相容性掃描而不啟動升級程序。 此設定會與 Windows 安裝程式命令列選項 `/Compat ScanOnly` 對應。 請使用此選項來部署整個 OS 升級套件。

<!--SCCMDocs-pr issue 2812-->
當啟用此選項時，此步驟並不會讓 Configuration Manager 用戶端進入佈建模式。 Windows 安裝程式會在背景中以無訊息模式執行，而用戶端則會繼續如常運作。 如需詳細資訊，請參閱[佈建模式](provisioning-mode.md)。

安裝程式會傳回結束代碼作為掃描的結果。 下表提供一些較常見的結束代碼：  

|結束碼|詳細資料|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|沒有相容性問題 (「成功」)。|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|可採取動作的相容性問題。|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|無法使用所選取的移轉選項。 例如，從 Enterprise 升級為 Professional。|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|不適用於 Windows 10。|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|可用磁碟空間不足。|  

如需有關此參數的詳細資訊，請參閱 [Windows 安裝程式命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat) \(英文\)。  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>忽略任何可解除的相容性訊息

指定安裝程式完成安裝，並忽略任何可解除的相容性訊息。 此設定會與 Windows 安裝程式命令列選項 `/Compat IgnoreWarning` 對應。  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>使用 Windows Update 動態更新 Windows 安裝程式

讓安裝程式執行動態更新作業，例如搜尋、下載和安裝更新。 此設定會與 Windows 安裝程式命令列選項 `/DynamicUpdate` 對應。 此設定與 Configuration Manager 軟體更新不相容。 如果您使用獨立式 Windows Server Update Services (WSUS) 或 Windows Update for Business 來管理更新，請啟用此選項。  

#### <a name="override-policy-and-use-default-microsoft-update"></a>覆寫原則並使用預設的 Microsoft Update

暫時即時覆寫本機原則以執行「動態更新」作業。 電腦會從 Windows Update 取得更新。
