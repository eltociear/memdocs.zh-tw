---
title: 建立擷取媒體
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用擷取媒體來從參照電腦擷取 OS 映像。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbbec355356a74d61f263fe2b16d44c0cd15ba80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690766"
---
# <a name="create-capture-media"></a>建立擷取媒體

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的擷取媒體可讓您從參照電腦擷取 OS 映像。 擷取媒體包含能啟動參照電腦的開機映像，以及能擷取 OS 映像的工作順序。 針對該案例使用擷取媒體來[建立工作順序以擷取 OS](create-a-task-sequence-to-capture-an-operating-system.md)。  


## <a name="prerequisites"></a>先決條件

在使用 [建立工作順序媒體精靈] 建立擷取媒體之前，請先確定符合所有這些條件。

### <a name="boot-image"></a>開機映像

請針對您將在工作順序中用來部署 OS 的開機映像，考慮下列相關要點：

- 開機映像的架構必須適用於目的電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。
- 確定開機映像包含佈建目的電腦所需的網路及儲存體驅動程式。

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>發佈與工作順序相關聯的所有內容

將工作順序所需的所有內容都發佈到至少一個發佈點。 此內容包括開機映像、OS 映像，以及其他相關聯的檔案。 精靈會在建立擷取媒體時從發佈點收集內容。

您的使用者帳戶至少需要該發佈點上內容庫的 [讀取]  存取權限。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

### <a name="prepare-the-removable-usb-drive"></a>準備卸除式 USB 磁碟機

如果您使用的是卸除式 USB 磁碟機，請將它連接到執行 [建立工作順序媒體精靈] 的電腦。 該 USB 磁碟機必須可由 Windows 偵測為卸除式裝置。 精靈會在建立媒體時直接寫入 USB 磁碟機。

### <a name="create-an-output-folder"></a>建立輸出資料夾

在您執行 [建立工作順序媒體精靈] 來針對 CD 或 DVD 組建立媒體之前，請先為精靈所建立的輸出檔案建立資料夾。 精靈針對 CD 或 DVD 組所建立的媒體會以 .ISO 檔案的形式直接寫入該資料夾中。


## <a name="process"></a>程序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立工作順序媒體]  。 這個動作會啟動 [建立工作順序媒體精靈]。  

3. 在 [選取媒體類型]  頁面上，選取 [擷取媒體]  。  

4. 在 [媒體類型]  頁面上，指定媒體為 [卸除式 USB 磁碟機]  或 [CD/DVD 組]  。 然後，設定下列選項：  

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

5. 在 [開機映像]  頁面上，指定下列選項：  

    > [!IMPORTANT]  
    > 您發佈之開機映像的架構必須適用於目的電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。  

    - **開機映像**：選取用於啟動目的地電腦的開機映像。  

    - **發佈點**：選取具有開機映像的發佈點。 精靈會從發佈點擷取開機映像，並將其寫入至媒體。  

        > [!NOTE]  
        > 您的使用者帳戶至少需要該發佈點上內容庫的 [讀取]  權限。  

6. 完成精靈。  


## <a name="next-steps"></a>後續步驟

[建立工作順序以擷取 OS](create-a-task-sequence-to-capture-an-operating-system.md)
