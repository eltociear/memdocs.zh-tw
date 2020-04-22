---
title: 建立預先設置的媒體
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用預先設置的媒體，以簡化數個案例中的 Windows 部署。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d5219b518d46ccca174c7aa3fef62fe3334def35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690716"
---
# <a name="create-prestaged-media"></a>建立預先設置的媒體

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的預先設置媒體是 Windows 映像 (WIM) 檔案。 其可由廠商安裝於裸機電腦上，或是安裝在未連線至 Configuration Manager 生產環境的設置中心。 預先設置的媒體包含用於啟動目的電腦的開機映像，以及套用至目的電腦的 OS 映像。 您也可以指定在預先設置的媒體中加入應用程式、套件及驅動程式套件。 媒體中不包含部署 OS 的工作順序。 將電腦交給使用者之前，即需將預先設置的媒體套用至新電腦的硬碟中。

針對下列 OS 部署案例，請使用預先設置的媒體：  

- [建立 OEM 原廠或本機 Depot 的映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

- [部署 Windows to Go](deploy-windows-to-go.md)  


## <a name="usage"></a>使用方式

當電腦在您套用預先設置媒體後首次啟動時，它將會在 Windows PE 中啟動。 它會連線至管理點以尋找能完成 OS 部署程序的工作順序。 當您部署使用預先設置媒體的工作順序時，用戶端會先檢查本機工作順序快取中是否存在有效內容。 如果找不到內容或內容已被修改，用戶端便會從發佈點或同儕節點下載該內容。  


## <a name="prerequisites"></a>先決條件

使用 [建立工作順序媒體精靈] 建立預先設置的媒體之前，請先確定已符合所有條件。

### <a name="boot-image"></a>開機映像

請針對您將在工作順序中用來部署 OS 的開機映像，考慮下列相關要點：

- 開機映像的架構必須適用於目的電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。
- 確定開機映像包含佈建目的電腦所需的網路及儲存體驅動程式。

### <a name="create-a-task-sequence-to-deploy-an-os"></a>建立部署 OS 的工作順序

作為預先設置媒體的一部分，請指定工作順序以部署 OS。 如需詳細資訊，請參閱[建立工作順序以安裝 OS](create-a-task-sequence-to-install-an-operating-system.md)。

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>發佈與工作順序相關聯的所有內容

將工作順序所需的所有內容都發佈到至少一個發佈點。 此內容包括開機映像、OS 映像，以及其他相關聯的檔案。 精靈會在建立預先設置媒體時從發佈點收集內容。

您的使用者帳戶至少需要該發佈點上內容庫的 [讀取]  存取。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

### <a name="hard-drive-on-the-destination-computer"></a>目的電腦上的硬碟機

必須先對目的電腦的硬碟進行格式化，再將預先設置的媒體套用到其上方。 如果在套用媒體時硬碟尚未進行格式化，部署 OS 的工作順序將會在嘗試啟動目的電腦時失敗。

> [!NOTE]  
> [建立工作順序媒體精靈] 會在媒體上設定下列工作順序變數條件： **_SMSTSMediaType = OEMMedia**。 您可以在工作順序中使用這個相同的條件。  


## <a name="process"></a>程序

 > [!NOTE]  
 > 針對 PKI 環境，由於根 CA 是在主要站台上指定的，因此請確定預先設置的媒體是在主要站台上建立的。 CAS 站台沒有根 CA 資訊，因此無法正確建立預先設置的媒體。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序媒體]  。 這個動作會啟動 [建立工作順序媒體精靈]。  

3. 在 [選取媒體類型]  頁面上，指定下列選項：  

    - 選取 [預先設置的媒體]  。  

    - 如果您只想要允許部署 OS，而不需要使用者輸入，可以選擇性地選取 [允許自動部署作業系統]  。  

        > [!IMPORTANT]  
        > 當您選取此選項時，系統就不會提示使用者提供網路設定資訊或選擇性的工作順序。 如果媒體已設定密碼保護，系統仍然會提示使用者輸入密碼。  

4. 在 [媒體管理]  頁面上，指定下列其中一個選項：  

    - **動態媒體**：允許管理點根據用戶端在網站界限中的位置，將媒體重新導向至其他管理點。  

    - **以站台為基礎的媒體**：媒體僅會連絡指定的管理點。  

5. 在 [媒體內容]  頁面上，指定下列資訊：  

    - **建立者**：指定媒體的建立者。  

    - **版本**：指定媒體的版本號碼。  

    - **註解**：指定媒體用途的唯一描述。  

    - **媒體檔案**：指定輸出檔案的名稱和路徑。 精靈會將輸出檔案寫入此位置。 例如：`\\servername\folder\outputfile.wim`  

    - **複寫用快取資料夾**<!--1359388-->:媒體建立程序可能會需要大量的暫存磁碟機空間。 根據預設，這個位置類似於下列路徑：`%UserProfile%\AppData\Local\Temp`。 從 1902 版開始，為了提升這些暫存檔存放位置的彈性，您可以將此值變更為另一個磁碟機和路徑。  

6. 在 [安全性]  頁面上，指定下列選項：  

    - **啟用未知電腦支援**：允許媒體將 OS 部署至未受 Configuration Manager 管理的電腦。 Configuration Manager 資料庫中不會有這些電腦的記錄。 如需詳細資訊，請參閱[準備未知電腦部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

    - **使用密碼保護媒體**：輸入強式密碼來協助防範他人未經授權存取媒體。 當您指定密碼時，使用者必須提供密碼才能使用預先設置的媒體。  

        > [!IMPORTANT]  
        > 為安全起見，請一律指定密碼，協助保護預先設置媒體。  
 
    - 針對 HTTP 通訊，請選取 [建立自我簽署媒體憑證]  。 然後指定憑證的開始日期和到期日期。  
    
        > [!NOTE] 
        > 如果選取此選項，則此精靈的 [開機映像]  頁面上就不會有可供選取的 HTTPS 管理點。

    - 針對 HTTPS 通訊，請選取 [匯入 PKI 憑證]  。 然後指定要匯入的憑證及其密碼。  

        如需開機映像使用之此用戶端憑證的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    - **使用者裝置親和性**：若要在 Configuration Manager 中支援使用者為中心的管理，請指定要如何讓媒體為使用者與目的地電腦建立關聯。 如需 OS 部署如何支援使用者裝置親和性的詳細資訊，請參閱[將使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

        - **允許自動核准使用者裝置親和性**：媒體會自動將使用者和目的地電腦產生關聯。 此功能是以部署 OS 之工作順序的動作為基礎。 在此案例中，工作順序會在將 OS 部署至目的地電腦時，為指定的使用者和目的地電腦建立關聯。  

        - **允許使用者親和性等待系統管理員核准**：媒體會在授與核准之後將使用者和目的地電腦產生關聯。 此功能是以部署 OS 之工作順序的範圍為基礎。 在此案例中，工作順序會為指定的使用者與目的電腦建立關聯性，但是會先等候系統管理使用者核准才部署 OS。  

        - **不允許使用者裝置親和性**：媒體不會將使用者和目的地電腦產生關聯。 在此案例中，工作順序在部署 OS 時，不會為使用者與目的電腦建立關聯性。  

7. 在 [工作順序]  頁面上，選取會在目的電腦上執行的工作順序。 確認由工作順序參考的內容清單。  

    - **偵測相關聯的應用程式相依性，並將其新增至此媒體**：同時也會針對應用程式相依性將內容新增至媒體。  

        > [!TIP]  
        > 如果您沒有看見預期的應用程式相依性，請取消選取此選項，然後再重新選取它以重新整理清單。  

8. 在 [開機映像]  頁面上，指定下列選項：  

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

9. 在 [影像]  頁面上，指定下列選項：  

    - **映像套件**：指定要使用的 OS 映像。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  

    - **映像索引**：如果套件包含多個 OS 映像，請指定要部署之映像的索引。  

    - **發佈點**：指定具有 OS 映像套件的發佈點。 精靈會從發佈點擷取 OS 映像，並將其寫入至媒體。  

10. 在 [選取應用程式]  頁面上，選取其他應用程式以加入預先設置的媒體檔案。  

11. 在 [選取套件]  頁面上，選取其他套件以加入預先設置的媒體檔案。  

12. 在 [選取驅動程式套件]  頁面上，選取其他驅動程式套件以加入預先設置的媒體檔案。  

13. 在 [發佈點]  頁面上，選取要用來取得內容的一或多個發佈點。  

    Configuration Manager 只會顯示擁有內容的發佈點。 先將所有與工作順序建立關聯的內容發佈到至少一個發佈點，才能繼續。 發佈內容之後，重新整理發佈點清單。 移除您已在這個頁面上選取的任何發佈點、移至上一頁，然後回到 [發佈點]  頁面。 或者，重新啟動精靈。 如需詳細資訊，請參閱[發佈工作順序所參考的內容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)和[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

14. 在 [自訂]  頁面上，指定下列選項：  

    - 加入工作順序會使用的任何變數。  

    - **啟用啟動前置命令**：指定您要在工作順序執行前執行的啟動前置命令。 啟動前置命令是在工作順序執行之前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 如需詳細資訊，請參閱[工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        > 在建立媒體時，工作順序會將套件識別碼和啟動前置命令列 (包括任何工作順序變數的值) 寫入執行 Configuration Manager 主控台之電腦的 **CreateTSMedia.log** 檔案中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

        如果啟動前置命令需要任何內容，請選取 [包含啟動前置命令的檔案]  的選項。  

15. 完成精靈。  


## <a name="next-steps"></a>後續步驟

[建立 OEM 原廠或本機 Depot 的映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
