---
title: 在新電腦上安裝 Windows
titleSuffix: Configuration Manager
description: 使用 Configuration Manager，以透過 PXE、OEM 或獨立媒體，在新電腦 (裸機) 上安裝作業系統。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a70269839b4a550fbef4dc5cab1b7ff3d426d87
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690666"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>使用 Configuration Manager 在新電腦 (裸機) 上安裝新版的 Windows

適用於：  Configuration Manager (最新分支)

此主題提供在 Configuration Manager 中安裝新電腦作業系統的一般步驟。 這個案例中有多種不同的部署方法可供選擇，例如 PXE、OEM 或獨立媒體。 如果您不確定此作業系統部署案例是否適合您，請參閱[使用 System Center Configuration Manager 部署企業作業系統的案例](scenarios-to-deploy-enterprise-operating-systems.md)。  

請使用下列章節的內容，以新版的 Windows 重新整理現有的電腦。  

##  <a name="plan"></a><a name="BKMK_Plan"></a> 方案  

-   **規劃並實作基礎結構需求**  

     必須要備妥數個基礎結構需求，才能部署作業系統，例如 Windows ADK、Windows 部署服務 (WDS)、支援的硬碟設定等。如需詳細資訊，請參閱[作業系統部署的基礎結構需求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。

##  <a name="configure"></a><a name="BKMK_Configure"></a> 設定  

1.  **準備開機映像**  

     開機映像會啟動 Windows PE 環境中的電腦 (內含有限元件和服務的最低作業系統)，接著在電腦上安裝完整的 Windows 作業系統。   部署作業系統時，您必須選取要使用的開機映像，將此映像發佈到發佈點。 請使用下列資訊準備開機映像：  

    -   如需深入了解開機映像，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

    -   如需如何自訂開機映像的詳細資訊，請參閱[自訂開機映像](../get-started/customize-boot-images.md)。  

    -   將開機映像發佈到發佈點。 如需詳細資訊，請參閱 [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

2.  **準備作業系統映像**  

     作業系統映像包含在目的地電腦安裝作業系統的必要檔案。 請使用下列資訊準備作業系統映像：  

    -   若要深入了解如何建立作業系統映像，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。

    -   將作業系統映像發佈至發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

    > [!NOTE]
    > 新的 Windows 安裝也可以透過 OS 升級套件從安裝來源檔案執行，但必須改為使用 OS 映像，例如 **install.wim**。
    >
    > 仍支援透過 OS 升級套件部署新的 Windows 安裝，但驅動程式必須與此方法相容。 從 OS 升級套件安裝 Windows 時，會安裝驅動程式，但驅動程式仍在 Windows PE 中，而不是像在 Windows PE 中只是插入。 某些驅動程式不相容，因此無法安裝在 Windows PE 中。 在 Windows PE 中，若驅動程式不相容而無法安裝，請改為使用 OS 映像。  

3.  **建立工作順序以透過網路部署作業系統**  

     使用網路上自動化作業系統安裝的工作順序。 請使用[建立工作順序以安裝作業系統](create-a-task-sequence-to-install-an-operating-system.md)中的步驟，建立工作順序以部署作業系統。 根據所選部署方法之不同，工作順序可能有其他考量。  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一來部署作業系統：  

    -   [使用 PXE 透過網路部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [使用多點傳送透過網路來部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [建立 OEM 原廠或本機 Depot 的映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [使用獨立媒體，而不使用網路來部署 Windows](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [透過網路使用可開機媒體部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>監視  

-   **監視工作順序部署**  

     若要監視工作順序部署以安裝作業系統，請參閱[監視作業系統部署](monitor-operating-system-deployments.md)。  
