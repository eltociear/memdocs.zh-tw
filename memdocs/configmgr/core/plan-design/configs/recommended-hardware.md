---
title: 建議的硬體
titleSuffix: Configuration Manager
description: 了解硬體建議，以協助您在基本部署之外調整 Configuration Manager 環境的規模。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428789"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Configuration Manager 的建議硬體

適用於：Configuration Manager (最新分支)

下列建議方針可協助您調整 Configuration Manager 環境，以支援較複雜的站台、站台系統與用戶端部署。 這些建議不完全適用於所有站台與階層設定。  

使用下方各區段中的資訊作為指南來協助規劃硬體。 針對使用 Configuration Manager 可用功能的用戶端與站台，請確定硬體符合其處理負載。

如需詳細資訊，請參閱 [Configuration Manager 的效能與調整指導方針白皮書](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e) (英文)。

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a> 站台系統

本區段提供建議的 Configuration Manager 站台系統硬體設定。 使用這些建議來支援最大數目的用戶端，並妥善利用 Configuration Manager 的大部分或所有功能。 如果環境未支援最大數目的用戶端，且未使用所有可用的功能，則該環境可能僅需要較少的資源。 一般而言，限制整體系統效能的主要因素如下所示：

1. 磁碟 I/O 效能

2. 可用的記憶體

3. CPU

為發揮最佳效能，所有資料磁碟和 1-Gbps 乙太網路都請使用 RAID 10 設定。

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a> 站台伺服器

|站台設定|CPU (核心)|記憶體 (GB)|SQL Server 的記憶體配置 (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|獨立主要站台伺服器，並在相同伺服器上具有資料庫站台角色<sup>[附註 1](#bkmk_note1)</sup>|16|96|80|  
|獨立主要站台伺服器，並具有遠端站台資料庫|8|16|-|  
|獨立主要站台的遠端資料庫伺服器|16|72|90|  
|管理中心站台伺服器，並在相同伺服器上具有資料庫站台角色<sup>[附註 1](#bkmk_note1)</sup>|20|128|80|  
|管理中心網站伺服器，並具有遠端站台資料庫|8|16|-|  
|管理中心網站的遠端資料庫伺服器|16|96|90|  
|子主要站台，並在相同伺服器上具有資料庫站台角色|16|96|80|  
|子主要站台伺服器，並具有遠端站台資料庫|8|16|-|  
|子主要站台的遠端資料庫伺服器|16|72|90|  
|次要網站伺服器|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a> 附註 1：共置 SQL

當在相同電腦上安裝站台伺服器與 SQL Server 時，此部署可支援站台和用戶端的[調整大小與級別數目](size-and-scale-numbers.md)上限。 這項設定可能會限制[高可用性選項](../../servers/deploy/configure/high-availability-options.md)，例如使用 SQL Server 叢集。 如果您擁有較大的環境，則在同一部電腦上支援這兩個角色的 I/O 需求較高，請考慮使用遠端 SQL Server。

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a> 遠端站台系統伺服器

下列方針適用於保有單一站台系統角色的電腦。 當在同一部電腦上安裝多個站台系統角色時規劃調整。

|網站系統角色|CPU (核心)|記憶體 (GB)|磁碟空間 (GB)|  
|----------------------|---------------|---------------|--------------------|  
|管理點|4|8|50|  
|發佈點|2|8|如作業系統和儲存部署的內容所需|  
|軟體更新點<sup>[附註 2](#bkmk_note2)</sup>|8|16|如作業系統和儲存部署的更新所需|  
|所有其他的網站系統角色|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a> 附註 2：WSUS 設定

裝載軟體更新點的電腦需要為 IIS 應用程式集區進行下列設定：  

- 將 **WsusPool 佇列長度**增加至 **2000**。  

- 將 **WsusPool 專用記憶體限制**增加為 4 倍，或設為 **0** (無限制)。  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a> 站台系統的磁碟空間

磁碟配置和設定會影響 Configuration Manager 的效能。 由於每個 Configuration Manager 環境各有不同，因此您實作的值可能與下列方針不盡相同。

為發揮最佳效能，請將每個物件分別置於獨立的專用 RAID 磁碟區中。 針對 Configuration Manager 及其資料庫檔案的所有資料磁碟區，使用 RAID 10 可發揮最佳效能。

|資料使用量|磁碟空間下限|25,000 個用戶端|50,000 個用戶端|100,000 個用戶端|150,000 個用戶端|700,000 個用戶端 (管理中心網站)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Configuration Manager 應用程式和記錄檔|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|網站資料庫 .mdf 檔|每 25,000 個用戶端需要 75 GB|75 GB|150 GB|300 GB|500 GB|2 TB|  
|網站資料庫 .ldf 檔|每 25,000 個用戶端需要 25 GB|25 GB|50 GB|100 GB|150 GB|100 GB|  
|暫存資料庫檔案 (.mdf 和.ldf)|視需要|視需要|視需要|視需要|視需要|視需要|  

如需 Windows 系統磁碟，請參閱已安裝作業系統版本的大小調整指引。

針對發佈點上的內容，其會根據部署而定。 此指引中並不包括站台伺服器或發佈點上內容庫中所需的磁碟空間。 如需詳細資訊，請參閱[內容庫](../../../core/plan-design/hierarchy/the-content-library.md)。

當規劃磁碟空間需求時，亦請考量下列其他方針：

- 每個用戶端需要大約 5-10 MB 的資料庫空間。 此大小取決於階層類型、設定和用戶端數目。 在較大的環境中，大小通常較小。 較小站台的每個用戶端則會有較大資料庫使用方式。<!-- SCCMDocs#1048 -->

- 針對主要站台暫存資料庫，請以站台資料庫 .mdf 檔案的 25% 到 30% 為準來規劃合併大小。 實際大小可能較小或更大。 這取決於站台伺服器的效能以及短期或長期傳入資料量。

  > [!NOTE]
  > 當在站台擁有 50,000 個以上的用戶端時，請規劃使用四個以上的暫存資料庫 .mdf 檔案。

- 管理中心網站的暫存資料庫大小通常遠低於主要站台。

- 如果您將 SQL Server Express 用於次要站台資料庫，則其會將資料庫大小限制為 10 GB。

## <a name="clients"></a><a name="bkmk_ScaleClient"></a> 用戶端

本節說明使用 Configuration Manager 用戶端軟體所管理之電腦的建議硬體設定。

### <a name="client-for-windows-computers"></a>Windows 電腦的用戶端

下列為您使用 Configuration Manager 管理 Windows 電腦的最低需求，包括內嵌版本：

- **處理器與記憶體：** 請參考作業系統的處理器和 RAM 需求。

- **磁碟空間：** 500 MB 可用磁碟空間，建議使用 5GB 作為 Configuration Manager 用戶端快取。 如果您使用自訂的設定來安裝 Configuration Manager 用戶端，則僅需要較少的磁碟空間。

  - 您可使用 client.msi 屬性 **SMSCACHESIZE** 來設定小於預設值 5120 MB 的快取大小。 大小下限為 1 MB。 下列範例會建立 2 MB 的快取：`CCMSetup.exe SMSCACHESIZE=2`

    如需詳細資訊，請參閱[關於用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。

    > [!TIP]
    > 使用最少的磁碟空間安裝用戶端適用於 Windows Embedded 裝置，它們通常磁碟大小比標準的 Windows 電腦小。

下列為針對 Configuration Manager 中選用功能的額外最低硬體需求：

- **作業系統部署：** 384 MB 以上的 RAM

- **軟體中心：** 500 MHz 以上的處理器

- **遠端控制：** 若要獲得最佳體驗，請使用 Pentium 4 超執行緒 3GHz (單核心) 或同級 CPU，搭配 1 GB 以上的 RAM。

### <a name="client-for-linux-and-unix"></a>Linux 和 UNIX 的用戶端

下列為使用 Configuration Manager 來管理 Linux 及 UNIX 伺服器的最低需求。

|需求|詳細資料|  
|-----------------|-------------|  
|處理器與記憶體|請參考電腦作業系統的處理器和 RAM 需求。|  
|磁碟空間|500 MB 可用磁碟空間，建議使用 5 GB 作為 Configuration Manager 用戶端快取。|  
|網路連線|Configuration Manager 用戶端電腦必須具有 Configuration Manager 站台系統的網路連線能力，才能啟用管理功能。|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a> Configuration Manager 主控台

下列為適用於執行 Configuration Manager 主控台的電腦最低硬體需求：

- Intel i3 或同級 CPU  

- 2 GB 的 RAM  

- 2 GB 的磁碟空間  

|DPI 設定|最低解析度|  
|-----------------|------------------------|  
|96 / 100%|1024 x 768|  
|120 /125%|1280 x 960|  
|144 / 150%|1600 x 1200|  
|196 / 200%|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a> 實驗室部署

針對 Configuration Manager 實驗室和測試部署，請使用下列最低硬體建議。 這些建議適用於所有站台類型，最多 100 個用戶端：  

|[角色]|CPU (核心)|記憶體 (GB)|磁碟空間 (GB)|  
|----------|---------------|-------------------|-----------------------|  
|站台和資料庫伺服器|2 - 4|8 - 12|100|  
|網站系統伺服器|1 - 4|2 - 4|50|  
|用戶端|1 - 2|1 - 3|30|  
