---
title: 針對 OSD 做好站台系統角色準備
titleSuffix: Configuration Manager
description: 先設定站台系統角色，然後於 Configuration Manager 中部署作業系統
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1beec2f5ef7b6da9f1f093300ec6c2b239e7396e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708796"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>使用 Configuration Manager 準備 OS 部署的站台系統角色

適用於：  Configuration Manager (最新分支)

若要在 Configuration Manager 中部署作業系統，請先準備下列需要特定設定和考量的站台系統角色。



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> 發佈點  

發佈點站台系統角色裝載了可供用戶端下載的來源檔案。 本內容適用於應用程式、軟體更新、OS 映像、開機映像，以及驅動程式套件。 使用頻寬、節流及排程選項控制內容發佈。  

您的發佈點數量必須足以支援在電腦上進行作業系統部署。 此外，規劃這些發佈點在階層中的位置也十分重要。 如需詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。 本文針對 OS 部署特定的發佈點，包含一些額外的規劃考量。  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> 發佈點的額外規劃考量  

下列項目是針對發佈點的額外規劃考量：  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>如何防止不需要的 OS 部署？  
Configuration Manager 不會區分站台伺服器與集合中的其他目的地電腦。 如果您將必要的工作順序部署至包含站台伺服器的集合，其執行工作順序的方式會與集合中任何其他電腦執行工作順序的方式相同。 請確定您的 OS 部署使用包含所預期用戶端的集合。  

請管理高風險工作順序部署的行為。 高風險部署會自動安裝於用戶端上，而且可能會造成不需要的結果。 例如，具有必要用途且會部署作業系統的工作順序。 若要降低不需要的高風險部署所帶來的風險，請設定部署驗證設定。 如需詳細資訊，請參閱 [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) (高風險部署的管理設定)。  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>一次可以有多少部電腦從單一發佈點接收 OS 映像？  
若要預估所需的發佈點數目，請考慮下列變數：  
- 發佈點的處理速度
- 發佈點的磁碟速度
- 網路上的可用頻寬
- 映像套件的大小   
  
例如，如果不考慮任何其他伺服器資源因素，在每秒 100 MB 的乙太網路上，一小時內最多可以有 11 部電腦處理一個 4-GB 的映像套件。  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

如果您必須在特定的時間範圍內將 OS 部署至特定數量的電腦，請將映像發佈至適量數量的發佈點。  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>是否可以將 OS 部署至發佈點？  
您可以將 OS 部署至發佈點，但必須從不同的發佈點接收 OS 映像。  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> 設定發佈點接受 PXE 要求  

若要將作業系統部署至發出 PXE 開機要求的 Configuration Manager 用戶端，請設定一或多個發佈點來接受 PXE 要求。 在您設定發佈點之後，該發佈點會回應 PXE 開機要求，並判斷要採取的適當部署動作。 如需詳細資訊，請參閱[安裝或修改發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> 自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊和視窗大小  

您可以針對支援 PXE 的發佈點自訂 RamDisk TFTP 區塊和視窗大小。 如果您已自訂網路，大型區塊或視窗大小可能會導致開機映像下載因發生逾時錯誤而失敗。 藉由自訂 RamDisk TFTP 區塊和視窗大小，可讓您在使用 PXE 來滿足特定網路需求時，將 TFTP 流量最佳化。 若要判斷哪一個設定最有效率，請在您的環境中測試自訂設定。  

-   **TFTP 區塊大小**：區塊大小是伺服器傳送給檔案下載用戶端的資料封包大小。 區塊大小越大，伺服器傳送的封包就越少，因此伺服器與用戶端之間的來回延遲也較少。 不過，大型區塊大小會導致封包分散，而大多數 PXE 用戶端實作並不支援分散的封包。  

-   **TFTP 視窗大小**：TFTP 針對每個傳送的資料區塊都會要求一個認可 (ACK) 封包。 伺服器在收到上一個區塊的 ACK 封包之前，不會傳送順序中的下一個區塊。 TFTP 視窗化可讓您定義填滿視窗所需的資料區塊數量。 伺服器會以背對背的方式傳送資料區塊，直到填滿視窗為止，然後用戶端會傳送 ACK 封包。 如果您增加此視窗大小，便可降低用戶端與伺服器之間的來回延遲數，並縮短下載開機映像所需的整體時間。  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>修改 RamDisk TFTP 視窗大小  
若要自訂 RamDisk TFTP 視窗大小，請新增下列有關支援 PXE 之發佈點的登錄機碼：  

- **位置**：`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **名稱**：RamDiskTFTPWindowSize  
- **類型**：REG_DWORD  
- **值**：(自訂視窗大小)  
    - 預設值為 **1** (一個資料區塊填滿視窗)。  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>修改 RamDisk TFTP 區塊大小  
若要自訂 RamDisk TFTP 視窗大小，請新增下列有關支援 PXE 之發佈點的登錄機碼：  

- **位置**：`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **名稱**：RamDiskTFTPBlockSize  
- **類型**：REG_DWORD  
- **值**：(自訂區塊大小)  
    - 預設值為 **4096**。  

> [!Note]  
> Windows 部署服務和 Configuration Manager PXE 回應程式服務支援這些 TFTP 設定。  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> 設定發佈點支援多點傳送  

多點傳送是一種網路最佳化方法。 當多個用戶端可能同時下載同一個 OS 映像時，請在發佈點上使用這種方法。 當您使用多點傳送時，多部電腦可以同時下載該 OS 映像，因為會由發佈點進行多點傳送。 如果沒有多點傳送，發佈點就會透過個別的連線，將資料複本傳送給各個用戶端。 如需詳細資訊，請參閱[使用多點傳送透過網路來部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

部署 OS 之前，請先將發佈點設定成支援多點傳送。 如需詳細資訊，請參閱[安裝及設定發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)。



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> 狀態移轉點  

狀態移轉點會儲存 USMT 在一部電腦上擷取到的使用者狀態資料，然後再還原至另一部電腦。 不過，當您擷取同一部電腦上的 OS 部署使用者設定時 (例如目的地電腦上您重新整理 Windows 的部署)，可以選擇要使用永久連結將資料儲存在同一部電腦上，或是使用狀態移轉點。 進行部分電腦部署時，若要建立狀態存放區，Configuration Manager 會自動在狀態存放區和目的地電腦之間建立關聯。 為狀態移轉點進行規劃時，請考量下列因素：    


### <a name="user-state-size"></a>使用者狀態的大小  

使用者狀態的大小會直接影響狀態移轉點的磁碟儲存體及移轉時的網路效能。 請考慮使用者狀態的大小以及要移轉的電腦數量。 另外也請一併考慮要從電腦移轉哪些設定。 例如，如果已經將 [我的文件]  資料夾備份到伺服器上，則您在部署映像時可能就不需要移轉該資料夾。 避免不必要的移轉可以讓使用者狀態維持較小的整體大小，也能降低使用者狀態大小對網路效能及狀態移轉點上磁碟儲存體造成的影響。  


### <a name="user-state-migration-tool"></a>使用者狀態移轉工具  

若要在部署作業系統期間擷取及還原使用者狀態，請使用指向 USMT 來源檔案的使用者狀態移轉工具 (USMT) 套件。 Configuration Manager 會在 Configuration Manager 主控台的 [軟體程式庫]   > [應用程式管理]   > [套件]  中自動建立這個套件。 Configuration Manager 會使用 USMT 10 從一個 OS 擷取使用者狀態，然後再還原至另一個 OS。 適用於 Windows 10 的 Windows 評定及部署套件 (Windows ADK) 包含 USMT 10。

如需不同 USMT 10 移轉案例的描述，請參閱 Windows 文件中的[常見移轉案例](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)。  


### <a name="retention-policy"></a>保留原則  

當您設定狀態移轉點時，請指定它所儲存之使用者狀態資料的保存時間長度。 存放在移轉點之使用者狀態的保存時間長度取決於以下兩項考慮因素：  

-   所存放的資料對於磁碟儲存體的影響。  

-   可能必須保存該資料，預防日後出現必須再次移轉該資料的需求。  
  
  
狀態移轉會發生在兩個階段中：擷取資料及還原資料。 擷取資料時會收集使用者狀態資料，並將其儲存在狀態移轉點中。 還原資料時，則會從狀態移轉點擷取使用者狀態資料、寫入目的地電腦中，然後再由 [釋放狀態存放區]  工作順序分階段釋放所存放的資料。 保留計時器會在釋放資料後啟動。 如果選取立即刪除所移轉資料的選項，就會在釋出使用者狀態資料後立即將其刪除。 如果選取在特定期限內保留資料的選項，則會在釋放狀態資料起經過一段特定時間後將其刪除。 您所設定的保留期間越長，所需的磁碟空間就可能越大。  


### <a name="select-drive-to-store-user-state-migration-data"></a>選取儲存使用者狀態移轉資料的磁碟機  

設定狀態移轉點時，請在伺服器上指定用於存放使用者狀態移轉資料的磁碟機。 您需從固定的磁碟機清單中選取磁碟機。 不過，其中部分磁碟機可能代表不可寫入磁碟機，例如光碟機或非網路共用磁碟機。 有些磁碟機代號可能無法與電腦上的任何磁碟機對應。 設定狀態移轉點時，請指定一個可寫入的共用磁碟機。  


### <a name="configure-a-state-migration-point"></a>設定狀態移轉點  

使用下列方法，將狀態移轉點設定為儲存使用者狀態資料：  

-   使用 [建立站台系統伺服器精靈]  ，為狀態管理點建立新的站台系統伺服器。  

-   使用 [新增站台系統角色精靈]  ，將狀態移轉點新增至現有伺服器。  

當您使用這些精靈時，系統會提示您為狀態移轉點提供下列資訊：  

-   用於儲存使用者狀態資料的資料夾。  

-   狀態移轉點上可儲存資料的用戶端數目上限。  

-   狀態移轉點用於儲存使用者狀態資料的最小可用空間。  

-   角色的刪除原則。 請指定是要在於電腦上還原使用者狀態資料後立刻刪除該資料，還是要在於電腦上還原使用者資料後的特定天數後再刪除該資料。  

-   狀態移轉點是否只回應還原使用者狀態資料的要求。 當您啟用此選項時，將無法使用狀態移轉點來儲存使用者狀態資料。  

如需安裝站台系統角色的步驟，請參閱[新增站台系統角色](../../core/servers/deploy/configure/add-site-system-roles.md)。  
