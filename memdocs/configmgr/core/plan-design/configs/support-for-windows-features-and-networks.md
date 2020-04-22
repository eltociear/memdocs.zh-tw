---
title: Windows 功能支援
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 所支援的 Windows 和網路功能。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e8e65571a3902661176ca3840690c159faef416
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688586"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Configuration Manager 對 Windows 功能和網路的支援

適用於：  Configuration Manager (最新分支)

本文識別適用於一般 Windows 和網路功能的 Configuration Manager 支援。  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  

在發佈點上啟用 Windows BranchCache 時，請將它與 Configuration Manager 搭配使用，並將用戶端設為以分散式快取模式使用它。

您可以在應用程式的部署類型上、套件的部署上、以及針對工作順序指定 BranchCache 設定。 從 1802 版開始，預設會啟用 BranchCache。

當符合 BranchCache 需求時，此功能可讓位於遠端位置的用戶端從具有目前內容快取的本機用戶端取得內容。  

例如，當第一個啟用 BranchCache 的用戶端從設定為 BranchCache 伺服器的發佈點要求內容時，用戶端會下載並快取內容。 此內容接著會提供給相同子網路上要求此相同內容的用戶端使用。

這些用戶端也會快取內容。 相同子網路上的其他用戶端就不需從發佈點下載內容。 該內容會分散在多個用戶端上以供未來傳輸。  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>支援 BranchCache 與 Configuration Manager 的需求

#### <a name="configure-distribution-points"></a>設定發佈點

請將 **Windows BranchCache** 功能新增至設定為發佈點的站台系統伺服器。

- 在設定為支援 BranchCache 的伺服器上，其發佈點不需要額外的設定。
- 您無法將 Windows BranchCache 新增至雲端式發佈點。 雲端式發佈點支援由已針對 Windows BranchCache 設定的用戶端下載內容。  

#### <a name="configure-clients"></a>設定用戶端

- 可支援 BranchCache 的用戶端必須針對 BranchCache 分散式快取模式進行設定。  
- 必須啟用 BITS 用戶端設定的 OS 設定，才能支援 BranchCache。  

如需相關資訊，請參閱 Windows 文件中的[設定 BranchCache 的用戶端](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache)。

Configuration Manager 支援的所有 Windows 版本，預設都支援 BranchCache。

如需詳細資訊，請參閱 Windows Server 文件中[適用於 Windows 的 BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) \(機器翻譯\)。  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> 工作群組中的電腦  

Configuration Manager 會針對工作群組中的用戶端提供支援。  

- Configuration Manager 支援將用戶端從工作群組移到網域，或從網域移到工作群組。 如需詳細資訊，請參閱[如何在工作群組電腦上安裝 Configuration Manager 用戶端](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)。  

> [!NOTE]
> 雖然工作群組中的用戶端受到支援，但所有站台系統都必須是受支援 Active Directory 網域的成員。  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a> 重複資料刪除

Configuration Manager 支援在 Windows Server 2012 或更新版本上，搭配發佈點使用重複資料刪除。

> [!IMPORTANT]  
> 裝載套件來源檔案的磁碟區不能標示進行重複資料刪除。 這項限制是因為重複資料刪除會使用重新分析點。 Configuration Manager 不支援使用內容來源位置而將檔案儲存在重新分析點上。  

如需詳細資訊，請參閱下列文章：

- Configuration Manager 小組部落格上的 [Configuration Manager 發佈點與 Windows Server 2012 重複資料刪除](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) \(英文\)

- Windows Server 文件中的[重複資料刪除概觀](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) \(部分機器翻譯\)

## <a name="directaccess"></a><a name="bkmk_DA"></a> DirectAccess  

Configuration Manager 支援 DirectAccess 功能，以進行用戶端與站台伺服器系統之間的通訊。  

- 滿足 DirectAccess 的所有需求時，它可讓網際網路上的 Configuration Manager 用戶端與其指派的站台通訊，就彷彿它們位於內部網路上。  

- 對於伺服器起始的動作 (例如，遠端控制和用戶端推入安裝)，起始的電腦必須執行 IPv6。 所有中介網路裝置上都必須支援此通訊協定。  

Configuration Manager 不支援透過 DirectAccess 執行下列功能：  

- OS 部署

- Configuration Manager 站台之間的通訊  

- 站台內 Configuration Manager 站台系統伺服器之間的通訊  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a> 雙重開機電腦  

Configuration Manager 無法在單一電腦上管理多個 OS。 如果要管理的電腦上有多個 OS，請調整站台的探索與用戶端安裝方法，以確保 Configuration Manager 用戶端只會安裝在必須管理的 OS 上。  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a> IPv6  

Configuration Manager 除了網際網路通訊協定第 4 版 (IPv4) 之外，也支援網際網路通訊協定第 6 版 (IPv6)，但下列例外狀況除外：  

|函式| IPv6 支援的例外狀況|  
|--------------|-------------------------------|  
|雲端架構的發佈點|需要 IPv4 才能支援 Microsoft Azure 與雲端式發佈點。|  
|雲端管理閘道|需要 IPv4 才能支援 Microsoft Azure 與雲端管理閘道。|  
|由 Microsoft Intune 與 Microsoft 服務連接器註冊的行動裝置|需要 IPv4 才能支援由 Microsoft Intune 與 Microsoft 服務連接器註冊的行動裝置。|  
|網路探索|當您設定 DHCP 伺服器以搜尋網路探索時需要 IPv4。|  
|OS 部署|在 1802 版和先前版本中，需要 IPv4 才能支援 OS 部署。  </br> </br> 從 1806 版開始，在不使用 Windows 部署服務的情況下，於發佈點上啟用 PXE 回應程式。 這個新的 PXE 回應程式服務支援 IPv6。 OS 部署功能的其他層面　(例如，在工作順序期間擷取或設定靜態 IP 位址) 會繼續要求 IPv4。 |  
|喚醒 proxy 通訊|支援用戶端喚醒 proxy 封包時需要 IPv4。|  
|Windows CE|支援 Windows CE 裝置上的 Configuration Manager 用戶端時需要 IPv4。|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a> 網路位址轉譯  

除非站台支援位於網際網路上的用戶端，且用戶端偵測到它已連線到網際網路，否則 Configuration Manager 不支援網路位址轉譯 (NAT)。 如需以網際網路為基礎之用戶端管理的詳細資訊，請參閱[以網際網路為基礎的用戶端管理規劃](../../clients/manage/plan-internet-based-client-management.md)。  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a> 專門儲存體技術  

Configuration Manager 可以與硬體搭配運作，但硬體必須是安裝 Configuration Manager 元件之 OS 版本的 Windows 硬體相容性清單上已通過認證的硬體。

站台伺服器角色需要 NTFS，讓 Configuration Manager 能夠設定目錄和檔案權限。 Configuration Manager 假設它具有邏輯磁碟機的完整擁有權。 在不同電腦上執行的站台系統無法共用任何儲存體技術上的邏輯磁碟分割。 不過，每一部電腦可以在共用存放裝置的相同實體磁碟分割上，使用不同的邏輯磁碟分割。  

### <a name="support-considerations"></a>支援考量

- **存放區域網路**：當所支援 Windows 伺服器直接連接到 SAN 裝載的磁碟區時，支援存放區域網路 (SAN)。  

- **儲存單一版本**：Configuration Manager 不支援在具有儲存單一版本 (SIS) 功能的磁碟區上設定發佈點套件和簽章資料夾。  

     此外，在已啟用 SIS 的磁碟區上也不支援 Configuration Manager 用戶端的快取。  

- **卸除式磁碟機**：Configuration Manager 不支援在卸除式磁碟機上安裝 Configuration Manager 站台系統或用戶端。  
