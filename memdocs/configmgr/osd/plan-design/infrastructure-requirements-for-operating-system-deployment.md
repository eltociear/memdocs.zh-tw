---
title: OSD 基礎結構需求
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中 OS 部署的外部和產品相依性及需求
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34c803cb2b43a2c69cee4c16f5029474e318eb2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709336"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Configuration Manager 中 OS 部署的基礎結構需求

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的 OS 部署除了產品內的相依性之外，也有外部相依性。 使用本文來協助您針對 OS 部署做好基礎架構準備。  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Configuration Manager 外部的相依性  

本節提供有關在 Configuration Manager 中部署作業系統所需之外部工具、安裝套件及 OS 版本的資訊。  

### <a name="windows-adk-for-windows-10"></a>Windows ADK for Windows 10  

Windows 評定及部署套件 (ADK) 是一組工具和文件，可支援 Windows 作業系統的設定和部署。 Configuration Manager 會使用 Windows ADK 來自動執行動作，例如安裝 Windows、擷取映像，以及移轉使用者設定檔和資料。  

如需詳細資訊，請參閱下列文章：  

- [給 IT 專業人員，適用於 Windows 10 的 Windows ADK 案例](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [下載適用於 Windows 10 的 Windows ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > 請務必下載 **Windows 10 版 Windows ADK** 和**適用於 ADK 的 Windows PE 附加元件**。

- [Windows 10 的支援](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>站台系統
Windows ADK 是下列站台系統伺服器的必要條件：

- 階層中頂層站台的站台伺服器  

- 階層中每個主要站台的站台伺服器  

- SMS 提供者的每個執行個體  


> [!NOTE]  
> 先在每部站台伺服器上手動安裝 Windows ADK，才能安裝 Configuration Manager 站台。  

#### <a name="windows-adk-features"></a>Windows ADK 功能
安裝下列 Windows ADK 功能：  

-   使用者狀態移轉工具 (USMT)  

    > [!Note]  
    > SMS 提供者上不需要 USMT。

-   Windows 部署工具  

-   Windows 預先安裝環境 (Windows PE)  

    > [!Important]  
    > 從 Windows 10 1809 版開始，Windows PE 是個別的安裝程式。 否則，沒有任何功能差異。<!--SCCMDocs-pr issue 2908-->  

如需可搭配不同 Configuration Manager 版本使用的 Windows 10 ADK 版本清單，請參閱[對 Windows 10 的支援](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)。


### <a name="user-state-migration-tool-usmt"></a>使用者狀態移轉工具 (USMT)  

Configuration Manager 會使用包含 USMT 10 來源檔案的 USMT 套件，在您部署 OS 的過程中擷取和還原使用者狀態。 頂層站台上的 Configuration Manager 安裝程式會自動建立 USMT 套件。 USMT 10 可從 Windows 7、Windows 8、Windows 8.1 及 Windows 10 擷取使用者狀態。  

如需詳細資訊，請參閱下列文章：  

- [USMT 10 的常見移轉案例](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [管理使用者狀態](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE 用於開機映像，以啟動電腦。 它是一個可提供有限服務的 Windows 作業系統，其使用時機是在 Windows 的預先安裝與部署期間。 下列清單包含適用於 Configuration Manager 最新分支的 Windows ADK 版本清單：  

#### <a name="windows-adk-version"></a>Windows ADK 版本  
適用於 Windows 10 的 Windows ADK。 如需詳細資訊，請參閱[對 Windows 10 的支援](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)。

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>可從 Configuration Manager 主控台自訂之開機映像的 Windows PE 版本  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>無法從 Configuration Manager 主控台自訂之開機映像的支援 Windows PE 版本  
Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

<sup>1</sup> 只有當開機映像是以 Windows PE 3.1 為基礎時，您才能將開機映像新增至 Configuration Manager。 請安裝適用於 Windows 7 SP1 的 Windows AIK 補充元件，以便使用適用於 Windows 7 SP1 的 Windows AIK 補充元件 (以 Windows PE 3.1 為基礎) 來升級適用於 Windows 7 的 Windows AIK (以 Windows PE 3 為基礎)。 請從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=5188)下載適用於 Windows 7 SP1 的 Windows AIK 補充元件。  

例如，當您有 Configuration Manager 時，便可從 Configuration Manager 主控台，使用適用於 Windows 10 的 Windows ADK (以 Windows PE 10 為基礎) 來自訂開機映像。 不過，若支援以 Windows PE 5 為基礎的開機映像，您必須從不同的電腦自訂開機映像，並使用與 Windows ADK for Windows 8 一起安裝的 DISM 版本。 接著，請將開機映像新增至 Configuration Manager 主控台。 如需自訂開機映像 (新增選用元件和驅動程式)、啟用開機映像的命令支援、將開機映像新增至 Configuration Manager 主控台，以及使用開機映像更新發佈點之步驟的詳細資訊，請參閱[自訂開機映像](../get-started/customize-boot-images.md)。 如需開機映像的詳細資訊，請參閱 [管理開機映像](../get-started/manage-boot-images.md)。  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS 是軟體更新點所需的服務，必須有軟體更新點，才能在部署 OS 的期間安裝軟體更新。 如需詳細資訊，請參閱[安裝及設定軟體更新點](../../sum/get-started/install-a-software-update-point.md)。


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>站台系統伺服器上的網際網路資訊服務 (IIS)  

發佈點、狀態移轉點及管理點都需要 IIS。 如需詳細資訊，請參閱 [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  


### <a name="windows-deployment-services-wds"></a>Windows 部署服務 (WDS)  

在 1802 版和先前版本中，PXE 部署需要 WDS。 從 1806 版開始，您可以在發佈點上啟用 PXE，而不需要 WDS。 如需詳細資訊，請參閱本文中的 [Windows 部署服務](#BKMK_WDS)。 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>動態主機設定通訊協定 (DHCP)  

DHCP 是 PXE 部署所需。 您必須具備作用中主機與正常運作 DHCP 伺服器，才能使用 PXE 部署作業系統。 如需 PXE 部署的詳細資訊，請參閱[透過網路來使用 PXE 部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>支援的作業系統和硬碟設定  

在您部署作業系統時，如需 Configuration Manager 所支援之 OS 版本和硬碟設定的詳細資訊，請參閱[支援的作業系統](#BKMK_SupportedOS)和[支援的磁碟設定](#BKMK_SupportedDiskConfig)。  


### <a name="windows-device-drivers"></a>Windows 裝置驅動程式  

當您在目的地電腦上安裝 OS 時，可能會使用 Windows 裝置驅動程式。 當您執行開機映像中的 Windows PE 時，也會使用這些驅動程式。 如需詳細資訊，請參閱[管理驅動程式](../get-started/manage-drivers.md)。  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Configuration Manager 相依性  

本節提供有關 Configuration Manager OS 部署必要條件的資訊。  


### <a name="os-image"></a>作業系統映像  

Configuration Manager 中的 OS 映像會以 Windows Imaging (WIM) 檔案格式儲存。 它們代表參考檔案與資料夾的壓縮集合。 必須要有這些映像，才能在電腦上成功安裝及設定 OS。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  


### <a name="driver-catalog"></a>驅動程式類別目錄  

若要部署裝置驅動程式，請匯入裝置驅動程式、啟用它，並且在 Configuration Manager 用戶端可以存取的發佈點上提供該驅動程式。 如需驅動程式類別目錄的詳細資訊，請參閱[管理驅動程式](../get-started/manage-drivers.md)。  


### <a name="management-point"></a>管理點  

管理點會在用戶端與 Configuration Manager 站台之間傳送資訊。 用戶端會使用管理點來執行工作順序以完成 OS 部署。 如需工作順序的詳細資訊，請參閱[自動化工作的規劃考量](planning-considerations-for-automating-tasks.md)。  


### <a name="distribution-point"></a>發佈點  

在大多數部署中，都會使用發佈點來儲存用來部署 OS 的資料，例如映像和驅動程式套件。 工作順序通常會從發佈點擷取資料來部署 OS。 如需安裝發佈點及管理內容之方式的詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  


### <a name="pxe-enabled-distribution-point"></a>啟用 PXE 的發佈點  

若要部署起始 PXE 的部署，請設定發佈點以接收來自用戶端的 PXE 要求。 如需詳細資訊，請參閱[設定發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。


### <a name="multicast-enabled-distribution-point"></a>啟用多點傳送的發佈點  

若要使用多點傳送將 OS 部署最佳化，請將發佈點設定成支援多點傳送。 如需詳細資訊，請參閱[設定發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)。   


### <a name="state-migration-point"></a>狀態移轉點  

當您擷取和還原並存與重新整理部署所需的使用者狀態資料時，請設定狀態移轉點，才能在另一部電腦上還原使用者狀態資料。  

如需如何設定狀態移轉點的詳細資訊，請參閱 [狀態移轉點](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

如需如何擷取和還原使用者狀態的詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  


### <a name="reporting-services-point"></a>Reporting Services 點  

若要使用 Configuration Manager 報表來進行 OS 部署，請安裝及設定報告點。 如需詳細資訊，請參閱[報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  


### <a name="security-permissions-for-os-deployments"></a>OS 部署的安全性權限  

[作業系統部署管理員]  安全性角色是內建的角色，您無法變更。 不過，您可以複製角色、進行變更，然後將變更儲存為新的自訂安全性角色。 以下是一些直接套用至 OS 部署的權限：  

- **開機映像套件**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

- **裝置驅動程式**：建立、刪除、修改、修改資料夾、修改報告、移動物件、讀取、執行報告  

- **驅動程式套件**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

- **作業系統映像**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

- **作業系統升級套件**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

- **工作排序套件**：建立、建立工作順序媒體、刪除、修改、修改資料夾、修改報告、移動物件、讀取、執行報告、設定安全性範圍  

如需詳細資訊，請參閱 [建立自訂安全性角色](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)。  


### <a name="security-scopes-for-os-deployments"></a>OS 部署的安全性範圍  

請使用安全性範圍來為系統管理使用者提供權限，以便讓他們能夠存取 OS 部署中所使用的可保護物件，例如 OS 和開機映像、驅動程式套件及工作順序套件。 如需詳細資訊，請參閱 [安全性範圍](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)。  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Windows 部署服務  

在 1802 版和先前版本中，Windows 部署服務 (WDS) 必須與您設定支援 PXE 或多點傳送的部署點安裝在同一部伺服器上。 WDS 已包含在伺服器 OS 中。 對於 PXE 部署而言，WDS 是執行 PXE 開機的服務。 安裝並啟用 PXE 的發佈點時，Configuration Manager 會將提供者安裝到使用 WDS PXE 開機功能的 WDS 中。  

從 1806 版開始，您可以在發佈點上啟用 PXE，而不需要 WDS。 如需詳細資訊，請參閱[安裝和設定發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)中的**啟用 PXE 回應程式而不需 Windows 部署服務**。


> [!NOTE]  
>  如果伺服器需要重新啟動，則 WDS 安裝可能會失敗。 


### <a name="wds-requirements"></a>WDS 需求  

-   系統管理員必須是本機 Administrators 群組的成員，才能在伺服器上安裝 WDS。  

-   WDS 伺服器必須是 Active Directory 網域成員，或是 Active Directory 網域的網域控制站。 所有 Windows 網域和樹系設定皆支援 WDS。  

-   如果遠端伺服器上安裝了提供者，則請在站台伺服器和遠端提供者上安裝 WDS。  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> 當您在同一部伺服器上有 WDS 和 DHCP 時的考量  

如果您規劃在執行 DHCP 的伺服器上共同裝載發佈點，請考慮以下設定問題：  

-   您必須擁有一部具作用中範圍之正在運作的 DHCP 伺服器 WDS 會使用 PXE，這需要 DHCP 伺服器。  

-   必須要有 DNS 伺服器，才能執行 WDS。  

-   在 WDS 伺服器上必須開啟下列 UDP 連接埠：  

    -   連接埠 67 (DHCP)  

    -   連接埠 69 (TFTP)  

    -   連接埠 4011 (PXE)  

    > [!NOTE]  
    >  如果伺服器上需要 DHCP 授權，就必須在伺服器上開啟 DHCP 用戶端連接埠 68。  

-   DHCP 和 WDS 都需要使用連接埠號碼 67。 如果您共同裝載 WDS 和 DHCP，則可以將 DHCP 或為 PXE 設定的發佈點移到個別的伺服器。 或者，您也可使用下列程序，將 WDS 伺服器設定為在不同的連接埠上接聽。  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>將 WDS 伺服器設定為在不同的連接埠上接聽  

1.  修改下列登錄機碼：  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  將登錄值 [UseDHCPPorts]  設定為 **0**。  

3.  若要讓新設定生效，可在伺服器執行下列命令：  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> 在 1810 版和更早的版本中，如果也在執行 DHCP 伺服器的伺服器上沒有 WDS，就不支援使用 PXE 回應程式。
>
> 從 1902 版開始，當您在發佈點上啟用 PXE 回應程式而不需要 Windows 部署服務時，它現在可位於與 DHCP 服務相同的伺服器上。 如需詳細資訊，請參閱[將至少一個發佈點設定為接受 PXE 要求](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure)。


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> 支援的作業系統  

在[支援的用戶端和裝置作業系統](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)中，列為支援之用戶端的所有 Windows 作業系統都可支援 OS 部署。  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> 支援的磁碟設定  

下表顯示支援 Configuration Manager OS 部署之參照電腦和目的地電腦上的硬碟設定組合：  

|參照電腦硬碟設定|目的地電腦硬碟設定|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁碟|基本磁碟|  
|動態磁碟上的簡單磁碟區|動態磁碟上的簡單磁碟區|  

Configuration Manager 僅支援從已設定簡單磁碟區的電腦擷取 OS 映像。 不支援下列硬碟設定：  

-   合併磁碟區  

-   等量磁碟區 (RAID 0)  

-   鏡像磁碟區 (RAID 1)  

-   同位檢查磁碟區 (RAID 5)  

下表顯示不支援 Configuration Manager OS 部署之參照和目的地電腦上的其他硬碟設定。  

|參照電腦硬碟設定|目的地電腦硬碟設定|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁碟|動態磁碟|  



## <a name="next-steps"></a>後續步驟

- [針對 OS 部署做好站台系統角色準備](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [針對 OS 部署做好準備](../get-started/prepare-for-operating-system-deployment.md)
