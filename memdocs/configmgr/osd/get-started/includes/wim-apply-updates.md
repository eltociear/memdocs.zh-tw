---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708876"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a> 將軟體更新套用至映像

> [!Note]  
> 本節同時適用於**作業系統映像**和**作業系統升級套件**。 它使用一般術語「映像」來指稱 Windows 映像檔 (WIM)。 這兩個物件都有一個 WIM，其包含 Windows 安裝檔案。 軟體更新適用於這兩個物件中的這些檔案。 此程序的行為在這兩個物件之間是相同的。  

每個月都有適用於映像的新軟體更新。 您需要有下列必要條件才可以套用軟體更新：

- 軟體更新基礎結構  
- 已成功同步軟體更新  
- 軟體更新已下載至站台伺服器的內容庫  

如需詳細資訊，請參閱 [Deploy software updates](../../../sum/deploy-use/deploy-software-updates.md) (部署軟體更新)。  

依指定排程將適用的軟體更新套用至映像。 這項程序有時稱為「離線服務」  。 在此排程中，Configuration Manager 會將選取的軟體更新套用至映像， 然後將更新的映像重新發佈至發佈點。

> [!Important]  
> 雖然您可以選取以版本為基礎的映像所適用任何軟體更新，但 DISM 只能套用映像的特定類型更新。 **OfflineServicingMgr.log** 檔案會顯示下列項目：`Not applying this update binary, it is not supported`。<!-- SCCMDocs issue 1324 -->

站台資料庫儲存有關映像的資訊，包括在匯入期間套用的軟體更新。 最初新增時所套用至映像的軟體更新也會儲存在站台資料庫中。 當您啟動精靈套用軟體更新時，它會擷取站台尚未套用至映像的適用軟體更新清單。 Configuration Manager 會將您從內容庫選取的軟體更新複製到站台伺服器。 然後將軟體更新套用到映像。  

### <a name="servicing-process"></a>服務處理程序

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [作業系統映像]  或 [作業系統升級套件]  。  

2. 選取要套用軟體更新的物件。  

3. 在功能區中，選取 [排程更新]  啟動精靈。  

4. 在 [選擇更新]  頁面上，選取要套用至映像的軟體更新。 更新清單可能需要一些時間才會出現在精靈中。 使用 [篩選]  搜尋中繼資料中的字串。 使用 [系統架構]  下拉式清單篩選 **X86**、**X64** 或**全部**。 您可以在清單中選取一個、多個或所有更新。 當您完成選取更新後，請選取 [下一步]  。  

5. 在 [設定排程]  頁面上指定下列設定，然後按 [下一步]  。  

    1. **排程**：指定站台何時將軟體更新套用至映像的排程。  

    2. **發生錯誤時繼續**：選取此選項，即使發生錯誤仍會繼續作業，將軟體更新套用至映像。  

    3. **使用映像更新發佈點**：選取此選項，在站台套用軟體更新之後，更新發佈點上的映像。  

6. 完成排程更新精靈。  

> [!NOTE]  
> 為了降低承載大小，所提供的作業系統升級套件和作業系統映像會移除舊版。  

### <a name="servicing-operations"></a>服務作業

在 Configuration Manager 主控台的 [作業系統映像]  或是 [作業系統升級套件]  節點，將下列資料行新增至檢視：

- **排程更新日期**：這個屬性會顯示您已定義的下一個排程。  
- **排程更新狀態**：這個屬性會顯示狀態。 例如，**成功**或**處理中**。  

選取特定的映像物件，然後切換至 [詳細資料] 窗格中的 [更新狀態]  索引標籤。 此索引標籤會顯示映像中的更新清單。

選取特定的映像物件，然後選取功能區中的 [屬性]  。 [已安裝的更新]  索引標籤會顯示映像中的更新清單。 [服務]  索引標籤是目前服務排程和已排程套用更新的唯讀檢視。

當狀態為**處理中**時，您可以選取功能區的 [取消已排程的更新]  。 此動作會取消使用中的服務程序。

若要對此程序進行疑難排解，請檢視站台伺服器上的 **OfflineServicingMgr.log** 和 **dism.log** 檔案。 如需詳細資訊，請參閱[記錄檔](../../../core/plan-design/hierarchy/log-files.md)。

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a> 針對離線 OS 映像服務指定磁碟機

<!--1358924-->

從 1810 版開始，指定 Configuration Manager 要在作業系統映像離線服務期間使用的磁碟機。 此程序的暫存檔會耗用大量磁碟空間。 此選項可讓您彈性選取要使用的磁碟機。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 在功能區中，按一下 [設定站台元件]  ，然後選取 [作業系統部署]  。  

2. 在 [離線服務]  索引標籤上，指定**供映像離線服務使用之本機磁碟機**的選項。  

此設定預設為 [自動]  。 使用此值，Configuration Manager 會選取其安裝所在的磁碟機。

如果站台伺服器沒有您選取的磁碟機，Configuration Manager 的行為就像您選取了 [自動]  一樣。

在離線服務期間，Configuration Manager 會將暫存檔儲存在資料夾 `<drive>:\ConfigMgr_OfflineImageServicing` 中。 它也會在此資料夾中裝載作業系統映像。

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a> 最佳化的映像服務

<!--3555951-->

從 1902 版開始，當您將軟體更新套用至 OS 映像時，有一個新選項可藉由移除任何已取代的更新來將輸出最佳化。 離線服務的最佳化只適用於具有單一索引的映像。

當您為站台進行排程以將軟體更新套用至 OS 映像時，它會使用 Windows 部署映像服務與管理 (DISM) 命令列工具。 在服務程序期間，這項變更引入了下列兩個額外的步驟：  

- 它會使用參數 `/Cleanup-Image /StartComponentCleanup /ResetBase` 針對裝載的離線映像執行 DISM。 如果此命令失敗，則目前服務程序就會失敗。 它不會認可映像的任何變更。  

- Configuration Manager 認可映像的變更，並將它從檔案系統取消掛接之後，即會將映像匯出為另一個檔案。 此步驟會使用 DISM 參數 `/Export-Image`。 它會從映像移除不必要的檔案，以減少大小。  

Microsoft 建議您定期將更新套用至離線映像。 您不必在每次提供映像服務時使用此選項。 當您每個月執行此程序時，這個新選項可透過一段時間的使用，為您提供最大的好處。 如需詳細資訊，請參閱[安裝軟體更新步驟的建議](../../understand/install-software-updates.md#recommendations)。

雖然此選項有助於減少服務映像的整體大小，但完成此程序確實需要更長的時間。 使用精靈可在方便的時間為服務進行排程。 這也需要在站台伺服器上有額外的儲存體。 您可以自訂站台來使用替代位置。 如需詳細資訊，請參閱[指定提供離線 OS 映像服務的磁碟機](#bkmk_servicing-drive)。

#### <a name="process-to-optimize-image-servicing"></a>將映像服務最佳化的程序

1. 啟動[服務程序](#servicing-process)。  

2. 在 [設定排程]  頁面上，選取 [在更新映像後，移除已取代的更新]  選項。 此選項不會自動啟用。 如果映像具有多個索引，您便無法使用此選項。  

3. 若要為映像服務進行排程，請完成此精靈。  

請使用 **OfflineServicing.log** 來驗證和監視程序。
