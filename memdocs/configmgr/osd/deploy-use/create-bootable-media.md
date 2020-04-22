---
title: 建立可開機媒體
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的可開機媒體安裝新版的 Windows 或取代電腦。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c570fc2844093b190e388727dd3799bcbcdb92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694896"
---
# <a name="create-bootable-media"></a>建立可開機媒體

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的可開機媒體包含開機映像、選擇性的啟動前置命令和相關聯檔案，以及 Configuration Manager 檔案。 針對下列 OS 部署案例，使用預先設置的媒體：  

- [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

- [取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)  


## <a name="usage"></a>使用方式

以可開機媒體開機時，會發生下列流程：

1. 來源電腦啟動
1. 它會連線到網路
1. 它會從網站擷取下列內容：
    - 指定的工作順序
    - 作業系統映像
    - 任何其他必要的內容

由於工作順序不在媒體上，因此不需要重新建立媒體即可變更工作順序或內容。

可開機媒體上的套件並未加密。 若要確定套件內容免受未經授權的使用者的侵害，請採取適當的安全性措施。 例如，為媒體加上密碼。

## <a name="prerequisites"></a>先決條件

使用 [建立工作順序媒體精靈] 建立可開機媒體之前，請先確定符合所有條件。

### <a name="boot-image"></a>開機映像

請針對您將在工作順序中用來部署 OS 的開機映像，考慮下列相關要點：

- 開機映像的架構必須適用於目的電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。
- 確定開機映像包含佈建目的電腦所需的網路及儲存體驅動程式。

### <a name="create-a-task-sequence-to-deploy-an-os"></a>建立部署 OS 的工作順序

作為可開機媒體的一部分，請指定工作順序以部署 OS。 如需詳細資訊，請參閱[建立工作順序以安裝 OS](create-a-task-sequence-to-install-an-operating-system.md)。

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>發佈與工作順序相關聯的所有內容

將工作順序所需的所有內容都發佈到至少一個發佈點。 此內容包括開機映像，以及其他相關聯的啟動前置檔案。 精靈會在建立可開機媒體時從發佈點收集內容。

您的使用者帳戶至少需要該發佈點上內容庫的 [讀取]  存取。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

### <a name="prepare-the-removable-usb-drive"></a>準備卸除式 USB 磁碟機

如果您使用的是卸除式 USB 磁碟機，請將它連接到執行 [建立工作順序媒體精靈] 的電腦。 該 USB 磁碟機必須可由 Windows 偵測為卸除式裝置。 精靈會在建立媒體時直接寫入 USB 磁碟機。

### <a name="create-an-output-folder"></a>建立輸出資料夾

在您執行 [建立工作順序媒體精靈] 來針對 CD 或 DVD 組建立媒體之前，請先為精靈所建立的輸出檔案建立資料夾。 精靈針對 CD 或 DVD 組所建立的媒體會以 .ISO 檔案的形式直接寫入該資料夾中。


## <a name="process"></a>程序

 > [!NOTE]  
 > 針對 PKI 環境，由於根 CA 是在主要站台上指定的，因此請確定可開機的媒體是在主要站台上建立的。 CAS 站台沒有根 CA 資訊，因此無法正確建立可開機的媒體。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序媒體]  。 這個動作會啟動 [建立工作順序媒體精靈]。  

3. 在 [選取媒體類型]  頁面，指定下列選項：  

    - 選取 [可開機媒體]  。  

    - 如果您只想要允許部署 OS，而不需要使用者輸入，可以選擇性地選取 [允許自動部署作業系統]  。  

        > [!IMPORTANT]  
        > 當您選取此選項時，系統就不會提示使用者提供網路設定資訊或選擇性的工作順序。 如果媒體已設定密碼保護，系統仍然會提示使用者輸入密碼。  

4. 在 [媒體管理]  頁面上，指定下列其中一個選項：  

    - **動態媒體**：允許管理點根據用戶端在網站界限中的位置，將媒體重新導向至其他管理點。  

    - **以站台為基礎的媒體**：媒體僅會連絡指定的管理點。  

5. 在 [媒體類型]  頁面上，指定媒體為 [卸除式 USB 磁碟機]  或 [CD/DVD 組]  。 然後，設定下列選項：  

    > [!IMPORTANT]  
    > 媒體會使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 之檔案的 USB 磁碟機上建立媒體。  

    - 如果您選取 [卸除式 USB 磁碟機]  ，請選取要在其中儲存內容的磁碟機。  

        - **格式化卸除式 USB 磁碟機 (FAT32) 並使其為可開機**：根據預設，讓 Configuration Manager 準備 USB 磁碟機。 許多較新的 UEFI 裝置需要可開機的 FAT32 磁碟分割。 不過，這個格式也會限制檔案大小和磁碟機的整體容量。 如果您已經格式化並設定卸除式磁碟機，請停用此選項。

    - 如果您選取 [CD/DVD 組]  ，請指定媒體的容量 ([媒體大小]  )，以及輸出檔案的名稱和路徑 ([媒體檔案]  )。 精靈會將輸出檔案寫入此位置。 例如：`\\servername\folder\outputfile.iso`  

        如果媒體容量太小而無法儲存整個內容，便會建立多個檔案。 然後，您需要將內容儲存在多個 CD 或 DVD 上。 當它需要多個媒體檔案時，Configuration Manager 會在其所建立的每個輸出檔案名稱上加入序號。  

        > [!IMPORTANT]  
        > 如果您選取現有的 .iso 映像，[工作順序媒體精靈] 會在您繼續進行精靈的下一頁時從磁碟機或共用刪除映像。 即使您取消精靈，還是會刪除現有映像。  

    - **複寫用快取資料夾**<!--1359388-->:媒體建立程序可能會需要大量的暫存磁碟機空間。 根據預設，這個位置類似於下列路徑：`%UserProfile%\AppData\Local\Temp`。 從 1902 版開始，為了提升這些暫存檔存放位置的彈性，您可以將此值變更為另一個磁碟機和路徑。  

    - **媒體標籤**<!--1359388-->:從 1902 版開始，可以將標籤新增至工作順序媒體。 此標籤可協助您在建立媒體之後更輕鬆識別媒體。 預設值為 `Configuration Manager`。 此文字欄位會出現在下列位置：  

        - 如果您掛接 ISO 檔案，Windows 就會顯示此標籤作為掛接的磁碟機名稱  

        - 如果您格式化 USB 磁碟機，它會使用標籤的前 11 個字元作為其名稱  

        - Configuration Manager 會將稱為 `MediaLabel.txt` 的文字檔案寫入媒體的根目錄。 根據預設，此檔案包含一行文字：`label=Configuration Manager`。 如果您自訂媒體標籤，則這一行文字會使用您的自訂標籤，而不是預設值。  

    - **將 autorun.inf 檔案加入媒體**<!-- 4090666 -->:從 1906 版開始，Configuration Manager 預設不會新增 autorun.inf 檔案。 此檔案通常會遭到反惡意程式碼軟體產品的封鎖。 如需 Windows 自動執行功能的詳細資訊，請參閱 [Creating an AutoRun-enabled CD-ROM Application](https://docs.microsoft.com/windows/desktop/shell/autoplay) (建立已啟用自動執行的 CD-ROM 應用程式)。 如果您的案例仍有此需要，請選取此選項來包含該檔案。  

6. 在 [安全性]  頁面上，指定下列選項：  

    - **啟用未知電腦支援**：允許媒體將 OS 部署至未受 Configuration Manager 管理的電腦。 Configuration Manager 資料庫中不會有這些電腦的記錄。 如需詳細資訊，請參閱[準備未知電腦部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

    - **使用密碼保護媒體**：輸入強式密碼來協助防範他人未經授權存取媒體。 當您指定密碼時，使用者必須提供該密碼才能使用可開機媒體。  

        > [!IMPORTANT]  
        > 基於安全性最佳作法，一律指派密碼保護可開機媒體。  

    - 針對 HTTP 通訊，請選取 [建立自我簽署的媒體憑證]  。 然後指定憑證的開始日期和到期日期。  
    
      > [!NOTE]  
      > 如果選取此選項，則此精靈的 [開機映像]  頁面上就不會有可供選取的 HTTPS 管理點。

    - 針對 HTTPS 通訊，請選取 [匯入 PKI 憑證]  。 然後指定要匯入的憑證及其密碼。  

        如需開機映像使用之此用戶端憑證的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    - **使用者裝置親和性**：若要在 Configuration Manager 中支援使用者為中心的管理，請指定要如何讓媒體為使用者與目的地電腦建立關聯。 如需 OS 部署如何支援使用者裝置親和性的詳細資訊，請參閱[將使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

        - **允許自動核准使用者裝置親和性**：媒體會自動將使用者和目的地電腦產生關聯。 此功能是以部署 OS 之工作順序的動作為基礎。 在此案例中，工作順序會在將 OS 部署至目的地電腦時，為指定的使用者和目的地電腦建立關聯。  

        - **允許使用者親和性等待系統管理員核准**：媒體會在授與核准之後將使用者和目的地電腦產生關聯。 此功能是以部署 OS 之工作順序的範圍為基礎。 在此案例中，工作順序會為指定的使用者與目的電腦建立關聯性，但是會先等候系統管理使用者核准才部署 OS。  

        - **不允許使用者裝置親和性**：媒體不會將使用者和目的地電腦產生關聯。 在此案例中，工作順序在部署 OS 時，不會為使用者與目的電腦建立關聯性。  

7. 在 [開機映像]  頁面上，指定下列選項：  

    > [!IMPORTANT]  
    > 您發佈之開機映像的架構必須適用於目的電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。  

    - **開機映像**：選取用於啟動目的地電腦的開機映像。  

    - **發佈點**：選取具有開機映像的發佈點。 精靈會從發佈點擷取開機映像，並將其寫入至媒體。  

        > [!NOTE]  
        > 您的使用者帳戶至少需要該發佈點上內容庫的 [讀取]  權限。  

    - **管理點**：僅針對 [以站台為基礎的媒體]  ，從主要站台選取管理點。  

    - **相關聯的管理點**：僅針對 [動態媒體]  ，選取要使用的主要站台管理點，以及初始通訊的優先順序。  
    
        > [!NOTE]  
        > 只有在此精靈的 [安全性]  頁面中指定 PKI 憑證時，才會顯示已啟用 HTTPS 的管理點。  

8. 在 [自訂]  頁面上，指定下列選項：  

    - 加入工作順序會使用的任何變數。  

    - **啟用啟動前置命令**：指定您要在工作順序執行前執行的啟動前置命令。 啟動前置命令是在工作順序執行之前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 如需詳細資訊，請參閱[工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        > 在建立媒體時，工作順序會將套件識別碼和啟動前置命令列 (包括任何工作順序變數的值) 寫入執行 Configuration Manager 主控台之電腦的 **CreateTSMedia.log** 檔案中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

        如果啟動前置命令需要任何內容，請選取 [包含啟動前置命令的檔案]  的選項。  

9. 完成精靈。  


## <a name="alternate-method"></a>替代方法

當磁碟機未連線到執行 Configuration Manager 主控台的電腦時，可以在卸除式 USB 磁碟機上建立可開機媒體。

1. [建立工作順序開機媒體](#process)。 在 [媒體類型]  頁面上，選取 [CD/DVD 組]  。 精靈會將輸出檔案寫入您指定的位置。 例如：`\\servername\folder\outputfile.iso`。  

2. 準備卸除式 USB 磁碟機。 磁碟機必須格式化、清空且可開機。

3. 從共用位置掛接 ISO，並將檔案從 ISO 傳送到 USB 磁碟機。


## <a name="next-steps"></a>後續步驟

[透過網路使用可開機媒體部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  
