---
title: 內容庫
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 用來減少整體發佈內容大小的內容庫。
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 567c03d231c145718f4f960bda7073ba4b904de2
ms.sourcegitcommit: d1c7548b4177d720065b822356f9a08d1e1657c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82880987"
---
# <a name="the-content-library-in-configuration-manager"></a>Configuration Manager 中的內容庫

適用於：  Configuration Manager (最新分支)

內容庫是 Configuration Manager 中內容的單一執行個體存放區。 站台使用它來減少您所發佈內容的合併主體整體大小。 內容庫會儲存軟體部署的所有內容檔案，例如：軟體更新、應用程式和 OS 部署。  

- 站台會在每部站台伺服器和每個發佈點上自動建立及維護一份內容庫複本。  

- 在 Configuration Manager 將內容檔案新增至站台伺服器，或將檔案複製到發佈點之前，它會先驗證內容庫中是否已存在每個內容檔案。  

- 若可使用內容檔案，Configuration Manager 並不會複製檔案。 相反地，它會建立現有內容檔案與應用程式或套件的關聯。  

在發佈點伺服器上，設定下列選項：

- 要建立內容庫的一個或多個磁碟機。  

- 每個所使用的磁碟機之優先順序。  

Configuration Manager 會將內容檔案複製到優先順序最高的磁碟機，直到該磁碟機的可用空間數少於您指定的下限為止。  

- 您可在發佈點安裝期間設定磁碟機設定。  

- 完成安裝之後，即無法在發佈點內容中設定磁碟機設定。  

如需如何設定發佈點之磁碟機設定的詳細資訊，請參閱[管理內容和內容基礎結構](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

> [!IMPORTANT]
> 若要在安裝後將內容庫移至發佈點上的不同位置，請使用 Configuration Manager 工具中的 [內容庫傳輸]  工具。 如需詳細資訊，請參閱[內容庫傳輸工具](../../support/content-library-transfer.md)。  


## <a name="about-the-content-library-on-the-central-administration-site"></a>關於管理中心網站上的內容庫

Configuration Manager 預設會在安裝管理中心網站時於站台上建立內容庫。 內容庫將存放於站台伺服器中有最多可用磁碟空間的磁碟機中。 由於您無法在管理中心網站上安裝發佈點，因此無法設定內容庫使用之磁碟機的優先順序。 類似於其他站台伺服器上的內容庫和發佈點上的內容庫，當包含內容庫的磁碟機可用磁碟空間不足，內容庫將自動跨越至下個可用的磁碟機。  

Configuration Manager 在下列案例中會使用管理中心網站上的內容庫︰  

- 在管理中心網站上建立內容  

- 移轉其他 Configuration Manager 站台的內容，並將管理中心網站指派為管理該內容的站台  

> [!NOTE]  
> 當您在主要站台建立內容，並將內容發佈至不同的主要站台或不同主要站台之下的次要站台時，管理中心網站會暫時將該內容儲存在管理中心網站上的排程器收件匣中，但不會將該內容新增至其內容庫。  

使用下列選項在管理中心網站上管理內容庫︰  

- 若要避免將內容庫安裝在特定磁碟機，請建立名為 **no_sms_on_drive.sms**的空白檔案。 在建立內容庫之前，將該檔案複製到磁碟機的根目錄。  

- 建立內容庫之後，請使用 Configuration Manager 工具中的 [內容庫傳輸]  工具來管理內容庫的位置。 如需詳細資訊，請參閱[內容庫傳輸工具](../../support/content-library-transfer.md)。  

> [!Note]  
> 雲端發佈點不會使用單一執行個體儲存體。 站台會先將套件加密再傳送至 Azure，而且每個套件都有唯一的加密金鑰。 即使兩個檔案相同，加密版本也不會完全一樣。  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a> 針對站台伺服器設定遠端內容庫

<!--1357525-->
從 1806 版開始，若要設定[站台伺服器高可用性](../../servers/deploy/configure/site-server-high-availability.md)，或釋出您管理中心或主要站台伺服器上的硬碟空間，請將內容庫重新定位到另一個儲存位置。 將內容庫移至站台伺服器上的另一個磁碟機、個別的伺服器，或是存放區域網路 (SAN) 上的容錯磁碟。 建議使用 SAN，因為它高度可用，並能提供彈性的存放空間，可隨內容需求的變化而放大或壓縮。 如需詳細資訊，請參閱[高可用性選項](../../servers/deploy/configure/site-server-high-availability.md)。

遠端內容庫是[站台伺服器高可用性](../../servers/deploy/configure/site-server-high-availability.md)的必要條件。

> [!Note]  
> 此動作只會移動站台伺服器上的內容庫。 它不會影響內容庫在發佈點上的位置。 

> [!Tip]  
> 另請規劃管理套件來源內容，這是內容庫的外部內容。 Configuration Manager 中的每個軟體物件在網路共用上都有套件來源。 請考慮將所有來源集中到單一共用，但確定此位置是多餘的且高度可用。
>
> 如果您將內容庫移至相同存放磁碟區作為您的封裝來源，則無法將此磁碟區標示為重複資料刪除。 雖然內容庫支援重複資料刪除，但套件來源磁碟區並不支援。 如需詳細資訊，請參閱[重複資料刪除](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup)。<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>先決條件  

- 針對您要移動內容庫的目標網路路徑，站台伺服器電腦帳戶需要擁有路徑的**完全控制**權限。 此權限適用於共用及檔案系統。 遠端系統上不會安裝任何元件。

- 站台伺服器不能有發佈點角色。 發佈點也會使用內容庫，且此角色不支援遠端內容庫。 移動內容庫之後，您即無法將發佈點角色新增至站台伺服器。  

> [!Important]  
> 請勿在多個站台之間重複使用共用網路位置。 例如，請勿針對管理中心網站和子主要站台使用相同的路徑。 此設定可能會損毀內容庫，而需要您加以重建。<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>管理內容庫的程序

1. 在網路共用中建立資料夾，作為內容庫的目標。 例如 `\\server\share\folder`。  

    > [!Warning]  
    > 請勿重複使用具有內容的現有資料夾。 例如，請勿使用與封裝來源相同的資料夾。 複製內容庫之前，設定管理員會從您指定的位置移除任何現有內容。  

2. 在 Configuration Manager 主控台中，切換至 [系統管理]  工作區。 展開 [站台設定]  ，選取 [站台]  節點，然後選取站台。 在詳細資料窗格底部的 [摘要]  索引標籤上，留意到 [內容庫]  會有一個新欄位。  

3. 選取功能區上的 [管理內容庫]  。  

4. 在 [管理內容庫] 視窗中，[目前的位置]  欄位顯示本機磁碟機和路徑。 針對 [新增位置]  輸入有效的網路路徑。 此路徑是站台移動內容庫的目標位置。 它必須包含共用上已存在的資料夾名稱，例如 `\\server\share\folder`。 選取 [確定]  。  

5. 請注意到詳細資料窗格之 [摘要] 索引標籤上 [內容庫] 欄位中的 [狀態]  值。 它會更新以顯示站台移動內容庫的進度。  

   - **進行中**時，[移動進度 (%)]  值會顯示完成百分比。  

        > [!Note]  
        > 如果您有一個大型的內容庫，您可能會在主控台中看到一段時間的 `0%` 進度。 例如，對於 1 TB的內容庫，它必須在顯示 `1%` 之前複製 10 GB。 檢閱 **distmgr.log**，其中顯示了複製的檔案和位元組數目。 從 1810 版開始，記錄檔也會顯示預估的剩餘時間。

   - 發生錯誤狀態時，狀態會顯示錯誤。 常見的錯誤包含**拒絕存取**或**磁碟已滿**。  

   - 完成時，它會顯示 [完成]  。  

     如需詳細資料，請參閱 **distmgr.log**。 如需詳細資訊，請參閱[站台伺服器與站台系統伺服器記錄檔](log-files.md#BKMK_SiteSiteServerLog)。  

如需此程序的詳細資訊，請參閱[流程圖 - 管理內容庫](manage-content-library-flowchart.md)。

站台實際將內容庫檔案「複製」  到遠端位置。 此程序不會刪除站台伺服器上原始位置的內容庫檔案。 若要釋放空間，系統管理員必須手動刪除這些原始檔案。

如果原始內容庫跨越兩個磁碟機，則它將合併到新目的地的單一資料夾中。

從 1810 版開始，在複製過程中，**Despooler** 和**發佈管理員**元件不會處理新的套件。 此動作可確保移動時不會將內容新增至內容庫中。 不論如何，請在系統維護期間排定這項變更。

如果您需要將內容庫移回站台伺服器，請重複此程序，但針對 [新增位置]  輸入本機磁碟機和路徑。 它必須包含磁碟機上已存在的資料夾名稱，例如 `D:\SCCMContentLib`。 如果原始內容仍然存在，此程序會快速將設定移至站台伺服器的本機位置。

> [!Tip]  
> 若要將內容移至站台伺服器上的另一個磁碟機，請使用**內容庫傳輸**工具。 如需詳細資訊，請參閱[內容庫傳輸工具](../../support/content-library-transfer.md)。  


## <a name="inside-the-content-library"></a>內容庫內部

> [!Warning]  
> 下一節僅供參考。 請勿改變、新增或移除內容庫中的任何檔案或資料夾。 這樣做可能會損毀套件、內容或整個內容庫。 如果您懷疑有任何資料遺失、損毀或無效，請使用 Configuration Manager 主控台中的驗證功能來偵測這類問題。 然後重新發佈受影響的內容以修正問題。

根據預設，內容庫會儲存在磁碟機根目錄中稱為 **SCCMContentLib** 的資料夾。 此資料夾預設會以 **SCCMContentLib$** 形式共用。 資料夾和共用具有限制的權限，可防止意外損壞。 所有變更都應該透過 Configuration Manager 主控台進行。 此資料夾包含下列物件：  

- 套件庫 (**PkgLib** 資料夾)：發佈點上存在哪些套件的相關資訊。  

- 資料庫 (**DataLib** 資料夾)：套件原始結構的相關資訊。  

- 檔案庫 (**FileLib** 資料夾)：套件中的原始檔案。 此資料夾通常會使用大量的儲存空間。  

![Configuration Manager 內容庫的圖表概觀](media/content-library-overview.png)

> [!Tip]  
> 使用 Configuration Manager 工具中的 [內容庫總管]  工具來瀏覽內容庫的內容。 您無法使用此工具來修改內容。 它提供呈現內容的見解，並允許進行驗證和重新發佈。 如需詳細資訊，請參閱[內容庫總管](../../support/content-library-explorer.md)。  

### <a name="package-library"></a>套件庫

套件庫資料夾 **PkgLib** 針對發佈至發佈點的每個套件各含一個檔案。 檔案名稱為套件識別碼，例如 `ABC00001.INI`。 在此檔案的 `[Packages]` 區段下，會列出屬於套件一部分的內容識別碼，以及版本等其他資訊。 例如，**ABC00001** 是版本 **1** 的舊版套件。 此檔案中的內容識別碼為 `ABC00001.1`。

### <a name="data-library"></a>資料庫

資料庫資料夾 **DataLib** 針對每個套件中的每個內容各含一個檔案和一個資料夾。 例如，此檔案和資料夾的名稱分別為 `ABC00001.1.INI` 和 `ABC00001.1`。 檔案包含驗證資訊。 資料夾會從原始套件重新建立資料夾結構。

資料庫中的檔案會取代為具有套件中原始檔案名稱的 INI 檔案。 例如 `MyFile.exe.INI`。 這些檔案包含原始檔案的相關資訊，例如大小、修改時間和雜湊。 使用雜湊的前四個字元來尋找檔案庫中的原始檔案。 例如，MyFile.exe.INI 中的雜湊為 **DEF98765**，前四個字元為 **DEF9**。

### <a name="file-library"></a>檔案庫

如果內容庫跨越多個磁碟機，套件檔案可能會在任何磁碟機上的檔案庫資料夾 **FileLib** 中。

使用資料庫中所找到雜湊的前四個字元來尋找特定檔案。 檔案庫資料夾中有許多資料夾，每個資料夾的名稱都是由四個字元所組成。 尋找符合雜湊前四個字元的資料夾。 找到此資料夾之後，它會包含一或多組檔案，每組各有三個檔案。 這些檔案會共用相同的名稱，但其中一個副檔名為 INI、另一個副檔名為 SIG，還有一個檔案不具副檔名。 原始檔案是不具副檔名的檔案，其名稱與資料庫中的雜湊相同。

例如，資料夾 **DEF9** 包含 `DEF98765.INI`、`DEF98765.SIG` 和 `DEF98765`。 `DEF98765` 是原始 `MyFile.exe`。 INI 檔案包含共用相同檔案的「使用者」或內容識別碼清單。 站台必須同時移除所有內容，才能移除檔案。

### <a name="drive-spanning"></a>跨越磁碟機

內容庫可以跨越多個磁碟機。 您可以在建立發佈點時選擇這些磁碟機。 根據預設，Configuration Manager 會自動選擇內容庫跨越的磁碟機。

當您選擇磁碟機時，請選取主要和次要磁碟機。 站台會將所有中繼資料儲存在主要磁碟機上。 它只會跨越檔案庫到次要磁碟機。 次要磁碟機的資料夾共用名稱包含磁碟機代號。 例如，如果 D: 和 E: 是內容庫的次要磁碟機，則共用名稱為 **SCCMContentLibD$** 和 **SCCMContentLibE$** 。

如果您選擇 [自動]  選項，Configuration Manager 會選取具備最多可用空間的磁碟機作為其主要磁碟機。 它會將所有中繼資料儲存在此磁碟機上。 站台只會跨越檔案庫到次要磁碟機。

您可以在設定期間指定保留空間量。 Configuration Manager 會在最佳可用的磁碟只剩下此保留空間量可用時，嘗試使用次要磁碟。 每次選取要使用的新磁碟機時，都會選取具備最多可用空間的磁碟機。

您無法指定發佈點應該使用特定組以外的所有磁碟機。 在磁碟機根目錄中建立稱為 `NO_SMS_ON_DRIVE.SMS` 的空白檔案，即可避免此行為。 請在 Configuration Manager 選取要使用的磁碟機之前放置此檔案。 如果 Configuration Manager 在磁碟機根目錄中偵測到此檔案，則不會將該磁碟機用作內容庫。


## <a name="troubleshooting"></a>疑難排解

下列祕訣可協助您針對內容庫問題進行疑難排解：  

- 檢閱站台伺服器上的記錄 (**distmgr.log** 和 **PkgXferMgr.log**) 以及發佈點上的記錄 (**smsdpprov.log**) 中的任何失敗指標。  

- 使用[內容庫總管](../../support/content-library-explorer.md)工具。  

- 檢查檔案是否遭到其他處理序鎖定，例如防毒軟體。 從自動防毒軟體掃描中排除所有磁碟機上的內容庫，以及每個磁碟機上的暫存預備目錄 **SMS_DP$** 。  

- 若要查看是否有任何雜湊不相符，請從 Configuration Manager 主控台驗證套件。  

- 重新發佈內容會是最後選擇。 此動作應該會解決大部分問題。  

如需詳細資訊，請參閱[了解及針對 Configuration Manager 中的內容發佈進行疑難排解](https://support.microsoft.com/help/4482728/understand-troubleshoot-content-distribution-in-configuration-manager) \(機器翻譯\)。
