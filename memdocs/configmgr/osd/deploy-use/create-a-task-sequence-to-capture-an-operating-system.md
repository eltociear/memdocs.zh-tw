---
title: 建立工作順序以擷取 OS
titleSuffix: Configuration Manager
description: 建置和擷取工作順序會建立參照電腦，其可包含特定的驅動程式和軟體更新與 OS。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707386"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>建立工作順序以擷取 OS

適用於：  Configuration Manager (最新分支)

使用工作順序將 OS 部署到 Configuration Manager 中的電腦時，電腦會安裝在工作順序中指定的 OS 映像。 您可以自訂 OS 映像，使其包含特定驅動程式、應用程式和軟體更新。 請先使用建置和擷取工作順序來建立參照電腦。 然後從該參照電腦擷取 OS 映像。 如果已經有用於擷取的參照電腦，請建立自訂工作順序以擷取 OS。

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a> 關於建置和擷取工作順序

建置和擷取工作順序：

- 分割並格式化參照電腦
- 安裝 OS
- 安裝 Configuration Manager 用戶端
- 安裝應用程式
- 套用軟體更新
- 從參照電腦擷取 OS

在部署建置和擷取工作順序之前，在發佈點上必須先有與工作順序建立關聯的套件，例如應用程式。

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a> 需求

建立工作順序以安裝 OS 之前，下列元件必須先準備就緒：  

### <a name="required"></a>必要

- [開機映像](../get-started/manage-boot-images.md)

- [OS 映像](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>必要 (如果有用到)

- [驅動程式套件](../get-started/manage-drivers.md)，其包含必要的 Windows 驅動程式，以支援參照電腦上的硬體。 如需管理驅動程式的工作順序步驟詳細資訊，請參閱[使用工作順序來安裝裝置驅動程式](../get-started/manage-drivers.md#BKMK_TSDrivers)。

- [軟體更新](../../sum/get-started/synchronize-software-updates.md)

- [應用程式](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> 建立組建和擷取工作順序

請使用下列程序，以使用工作順序建置參照電腦和擷取 OS。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

1. 在功能區 [首頁]  索引標籤的 [建立]  群組中，選取 [建立工作順序]  來啟動 [建立工作順序精靈]。  

1. 在 [建立新的工作順序]  頁面上，選取 [建立並擷取參照作業系統映像]  。  

1. 在 [工作順序資訊]  頁面上指定下列設定：  

    - **工作順序名稱**：指定識別工作順序的名稱。  

    - **描述**：為工作順序指定選擇性描述。 例如，描述工作順序所建立的 OS。

    - **開機映像**：指定要與此工作順序搭配使用的開機映像。  

        > [!IMPORTANT]  
        > 開機映像的架構必須與目的地電腦的硬體架構相容。  

1. 在 [安裝 Windows]  頁面上指定下列設定：  

    - **映像套件**：指定 OS 映像套件，其中包含安裝 OS 所需的檔案。  

    - **映像索引**：指定要安裝在映像中的 OS 索引。 如果 OS 映像包含多個版本，則選取想要安裝的版本。  

    - **產品金鑰**：視需要指定所要安裝 Windows OS 的產品金鑰。 您可以指定編碼的大量授權金鑰和標準產品金鑰。 如果使用未編碼的產品金鑰，則會以每五個字元為一組，之間以虛線 (`-`) 來分隔。 例如：`XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **伺服器授權模式**：若有必要，請指定伺服器授權為 [按照基座]  、[按照伺服器]  ，或者不指定授權。 如果伺服器授權為 [按照伺服器]  ，請同時指定伺服器連線數目上限。  

    - 指定要如何為已部署的 OS 設定系統管理員帳戶：  

        - **隨機產生本機系統管理員密碼，並在所有支援的平台上停用帳戶**：為本機系統管理員帳戶建立隨機密碼。 Windows 設定完成時，請停用帳戶。

        - **啟用帳戶並指定本機系統管理員密碼**：在部署此 OS 的所有電腦上，使用相同的本機系統管理員帳戶密碼。

1. 在 [設定此網路]  頁面指定下列設定：

    - **加入工作群組**：指定是否在部署 OS 時，將目的地電腦新增至工作群組。  

    - **加入網域**：指定是否在部署 OS 時，將目的地電腦新增至網域。 在 [網域]  中，指定網域名稱。  

        > [!IMPORTANT]  
        > 您可以進行瀏覽以尋找本機樹系中的網域。 指定遠端樹系的網域名稱。

        您也可以指定組織單位 (OU)。 這是選用設定，會指定要建立電腦帳戶所在 OU 的 LDAP X.500 辨別名稱 (如果帳戶尚未存在)。  

    - **帳戶**：指定具有加入指定網域權限之帳戶的使用者名稱和密碼。 例如：`domain\user` 或 `%variable%`。  

        > [!IMPORTANT]  
        > 如果計畫在部署期間移轉網域設定或工作群組設定，請務必在這裡輸入適當的網域認證。  

1. 在 [安裝 Configuration Manager]  頁面上，指定 Configuration Manager 用戶端套件。 此套件包含安裝 Configuration Manager 用戶端所需的來源檔案。 此外，也請指定安裝用戶端所需的任何其他屬性。  

    如需詳細資訊，請參閱[關於用戶端安裝內容](../../core/clients/deploy/about-client-installation-properties.md)。

1. 在 [包含更新]  頁面上，指定要安裝必要的軟體更新、所有軟體更新，或不安裝軟體更新。 如果您指定安裝軟體更新，Configuration Manager 只會將目標軟體更新安裝至目的地電腦為其成員的集合。  

1. 在 [安裝應用程式]  頁面上，指定要安裝在目的地電腦上的應用程式。 如果您指定多個應用程式，也可以指定工作順序在特定應用程式安裝失敗時繼續執行。  

    > [!NOTE]
    > [系統準備]  頁面會顯示在精靈的下一個畫面中，但已不再使用。 選取 [下一步]  以繼續進行操作。

1. 在 [映像內容]  頁面上，指定下列 OS 映像的設定：

    - **建立者**：指定使用者名稱以註記為 OS 映像的建立者。  

    - **版本**：指定與 OS 映像建立關聯的版本號碼。 此屬性不一定要是 OS 版本，因為網站會分開儲存該值。

    - **描述**：指定 OS 映像的描述。  

1. 在 [擷取映像]  頁面上指定下列設定：

    - **路徑**：指定 Configuration Manager 應儲存輸出映像檔 (.wim) 的共用網路資料夾。 此檔案內含的 OS 映像，取決於在此精靈中指定的設定。 如果指定內含現有 .WIM 檔案的資料夾，就會覆寫該檔案。  

    - **帳戶**：指定具有儲存映像之網路共用權限的 Windows 帳戶。  

1. 完成精靈。  

若要將其他步驟新增至工作順序，請加以選取，然後選擇 [編輯]  。 如需如何編輯工作順序的詳細資訊，請參閱[使用工作順序編輯器](../understand/task-sequence-editor.md)。  

請使用下列方法之一將工作順序部署至參照電腦：  

- 如果參照電腦已經是 Configuration Manager 用戶端，請將建置和擷取工作順序部署至包含參照電腦的集合。 如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md)。

- 如果參照電腦不是 Configuration Manager 用戶端，或如果您想要在參照電腦上手動執行工作順序，請使用 [建立工作順序媒體精靈]  以建立可開機媒體。 如需詳細資訊，請參閱[建立可開機媒體](create-bootable-media.md)。  

擷取映像後，就可以將其部署到其他電腦。 如需如何部署已擷取 OS 映像的詳細資訊，請參閱[建立工作順序以安裝作業系統](create-a-task-sequence-to-install-an-operating-system.md)。  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a> 從現有的參照電腦擷取

如果已經有要擷取的參照電腦，請建立僅會從參照電腦擷取 OS 的工作順序。 使用 [擷取作業系統映像]  工作順序步驟，從參照電腦擷取一或多個映像，並將其存放在指定網路共用上的映像檔 (.wim) 中。 使用開機映像在 Windows PE 中啟動參照電腦。 工作順序會將參照電腦上的每個硬碟，擷取為 .wim 檔案內的個別映像。 如果參照的電腦中有多個磁碟機，則所產生的 .wim 檔案將包含每個磁碟區的個別映像。 此工作順序只會擷取格式化成 NTFS 或 FAT32 的磁碟區。 會略過其他格式的磁碟區或 USB 磁碟區。  

請使用下列程序，從現有的參照電腦擷取 OS 映像：

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

1. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序]  。 這個動作會啟動 [建立工作順序精靈]。  

1. 在 [建立新的工作順序]  頁面上，選取 [建立新的自訂工作順序]  。  

1. 在 [工作順序資訊]  頁面上，指定工作順序的名稱。 (選擇性) 為工作順序新增描述。  

1. 指定工作順序的開機映像。 Configuration Manager 會使用此開機映像，以 Windows PE 啟動參照電腦。 如需詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

1. 完成精靈。  

1. 在 [工作順序]  節點中，選取新的工作順序。 接著，在功能區的 [首頁]  索引標籤的 [工作順序]  群組中選取 [編輯]  。 此動作會開啟工作順序編輯器。  

1. 如果參照電腦上已安裝 Configuration Manager 用戶端：

    前往 [新增]  功能表，選取 [映像]  ，然後選擇 [準備 ConfigMgr 用戶端以進行擷取](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)。 此步驟會將參照電腦上的 Configuration Manager 用戶端一般化。

    > [!Note]  
    > 工作順序不支援解除安裝 Configuration Manager 用戶端。

1. 前往 [新增]  功能表，選取 [映像]  ，然後選擇 [準備 Windows 以進行擷取](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture)。 此步驟會執行 Sysprep，然後讓電腦在重新開機時進入為工作順序指定的 Windows PE 開機映像。 若要順利完成此動作，請勿將參照電腦加入網域。

1. 前往 [新增]  功能表，選取 [映像]  ，然後選擇 [擷取作業系統映像](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)。 此步驟將只從 Windows PE 執行，以擷取參照電腦上的硬碟。 進行以下設定：

    - **名稱**與**描述**：(選擇性) 您可以變更工作順序步驟的名稱，並提供描述。  

    - **目的地**：指定儲存輸出 .WIM 檔案的共用網路資料夾。 此檔案內含的 OS 映像，取決於利用此精靈所指定的設定。 如果指定內含現有 .WIM 檔案的資料夾，就會覆寫該檔案。  

    - **描述**、**版本**和**建立者**：(選擇性) 提供要擷取之映像的詳細資料。  

    - **擷取作業系統映像帳戶**：指定具有您指定之網路共用權限的 Windows 帳戶。 選取 [設定]  以指定該 Windows 帳戶的名稱。  

選取 [確定]  以儲存變更並關閉工作順序編輯器。  

請使用下列方法之一將工作順序部署至參照電腦：  

- 如果參照電腦已經是 Configuration Manager 用戶端，請將擷取工作順序部署至包含參照電腦的集合。 如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md)。

- 如果參照電腦不是 Configuration Manager 用戶端，或如果想要在參照電腦上手動執行工作順序，則請使用 [建立工作順序媒體精靈]  以建立擷取媒體。 如需詳細資訊，請參閱[建立擷取媒體](create-capture-media.md)。  

擷取映像後，就可以將其部署到其他電腦。 如需如何部署已擷取 OS 映像的詳細資訊，請參閱[建立工作順序以安裝作業系統](create-a-task-sequence-to-install-an-operating-system.md)。

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a> 範例工作順序

當在建立用於建置和擷取 OS 映像的工作順序時，請使用下表作為指南。 資料表會協助您決定工作順序步驟的一般順序，以及如何將這些步驟組織並結構化到邏輯群組。 您建立的工作順序可能會與此範例不同。 該工作順序可能會包含較多或較少的步驟和群組。

> [!NOTE]  
> 請一律使用 [建立工作順序精靈] 來建立此類型的工作順序。
>
> 此精靈新增至工作順序的步驟名稱會與手動新增相同步驟時所看到名稱略有不同。

### <a name="group-build-the-reference-machine"></a>群組：建置參照機器

這個群組包含建置參照電腦時所需的動作。

|工作順序步驟|說明|  
|-------------------------------|---------------|  
|**在 Windows PE 中重新啟動**|將目的地電腦重新開機至指派給工作順序的開機映像。 此步驟中會顯示訊息給使用者，指出電腦將會重新啟動以便繼續進行安裝。<br /><br />此步驟使用唯讀 `_SMSTSInWinPE` 工作順序變數。 如果相關聯的值等於 `false`，則工作順序步驟會繼續。|
|**分割磁碟 0 – BIOS**|在 BIOS 模式中分割並格式化目的地電腦上的硬碟。 預設的磁碟編號為 `0`。<br /><br />此步驟使用數個唯讀工作順序變數。 例如，此步驟只會在 Configuration Manager 用戶端的快取不存在時執行，而如果電腦設定為 UEFI，則不會執行。|
|**分割磁碟 0 - UEFI**|在 UEFI 模式中分割並格式化目的地電腦上的硬碟。 預設的磁碟編號為 `0`。<br /><br />此步驟使用數個唯讀工作順序變數。 例如，此步驟只會在 Configuration Manager 用戶端的快取不存在時執行，且只有在電腦設定為 UEFI 時才會執行。|
|**套用作業系統**|在目的地電腦上安裝指定的 OS 映像。 此步驟會先刪除該磁碟區上 (除了 Configuration Manager 特定控制檔案之外) 的任何檔案。 然後，它會將 WIM 檔案中包含的所有磁碟區映像套用至目標電腦上相對應的循序磁碟區。|
|**套用 Windows 設定**|設定目的地電腦的 Windows 設定。|
|**套用網路設定**|指定目的地電腦的網路或工作群組設定資訊。|
|**套用裝置驅動程式**|在部署 OS 時一併比對並安裝驅動程式。 如需詳細資訊，請參閱[自動套用驅動程式](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)。<br /><br />此步驟使用唯讀 `_SMSTSMediaType` 工作順序變數。 如果相關聯的值不等於 `FullMedia`，則不會執行此步驟。|
|**安裝 Windows 和 Configuration Manager**|安裝 Configuration Manager 用戶端軟體。 Configuration Manager 會安裝並註冊 Configuration Manager 用戶端 GUID。 包含任何必要的**安裝屬性**。|
|**安裝更新**|指定如何在目的地電腦上安裝軟體更新。 直到此步驟執行之後，才會評估目的地電腦是否有適用的軟體更新。 此時，評估會類似於任何其他由 Configuration Manager 管理的用戶端。 如需詳細資訊，請參閱[安裝軟體更新](../understand/install-software-updates.md)。<br /><br />此步驟使用唯讀 `_SMSTSMediaType` 工作順序變數。 如果相關聯的值不等於 `FullMedia`，則不會執行此步驟。|
|**安裝應用程式**|指定要在參照電腦上安裝的任何應用程式。|

### <a name="group-capture-the-reference-machine"></a>群組：擷取參考機器

這個群組包含必要的步驟來準備和擷取參照電腦。

|工作順序步驟|說明|  
|-------------------------------|---------------|  
|**準備 Configuration Manager 用戶端**|將參照電腦上的 Configuration Manager 用戶端一般化。|
|**準備 OS**|執行 Sysprep 以將 Windows 一般化。 然後 Sysprep 會讓電腦在重新開機時進入為工作順序指定的 Windows PE 開機映像。|
|**擷取參照機器**|將映像擷取至指定的網路共用和 .WIM 檔案。|

> [!IMPORTANT]
> 從參照電腦擷取映像後，請勿從參照電腦擷取另一個 OS 映像。 登錄項目會在初始設定期間建立。 您每一次擷取 OS 映像，都會建立新的參照電腦。 如果打算使用相同參照電腦來建立未來的 OS 映像，請先解除安裝並重新安裝 Configuration Manager 用戶端。

## <a name="next-steps"></a>後續步驟

[部署企業作業系統的方法](methods-to-deploy-enterprise-operating-systems.md)
