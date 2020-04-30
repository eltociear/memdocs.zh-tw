---
title: 重新整理現有電腦的 OS
titleSuffix: Configuration Manager
description: 您可以在 Configuration Manager 中使用多種方法來磁碟分割現有電腦和加以格式化，並在電腦上安裝新的 OS。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9582d6840e1f750d53504da4e8e7f6bf54f44965
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708406"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>使用新的 Windows 版本重新整理現有的電腦

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager 來分割和格式化現有的電腦，然後安裝新的 OS。 此程序有時稱為*重新安裝映像*或*抹除和載入*。 這個案例中有多種不同的部署方法可供選擇，例如 PXE、可開機媒體或軟體中心。 您也可以使用狀態移轉點來儲存設定，然後將其還原至新的 OS。

若要選擇正確的 OS 部署案例，請參閱[部署企業作業系統的案例](scenarios-to-deploy-enterprise-operating-systems.md)。  

## <a name="plan"></a><a name="BKMK_Plan"></a> 方案  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>規劃並實作基礎結構需求

您必須符合幾項基礎結構需求，才能部署 OS。 其中一些需求包括 Windows ADK、使用者狀態移轉工具 (USMT) 和 Windows 部署服務 (WDS)。 如需詳細資訊，請參閱 [OS 部署的基礎結構需求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

### <a name="install-a-state-migration-point"></a>安裝狀態移轉點

如果您想要從現有的電腦擷取設定，然後將設定還原至新的 OS，請考慮使用狀態移轉點。 如需詳細資訊，請參閱[狀態移轉點](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

## <a name="configure"></a><a name="BKMK_Configure"></a> 設定  

### <a name="prepare-a-boot-image"></a>準備開機映像

開機映像會在 Windows PE 環境中啟動電腦。 Windows PE 是最小的 OS，具有有限的元件和服務。 在 Windows PE 中，Configuration Manager 隨後可在電腦上安裝完整的 Windows OS。

如需詳細資訊，請參閱下列文章：

- [管理開機映像](../get-started/manage-boot-images.md)

- [自訂開機映像](../get-started/customize-boot-images.md)

- [發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>準備 OS 映像

OS 映像包含必須在目的電腦上安裝 OS 所需的檔案。

如需詳細資訊，請參閱下列文章：

- [管理 OS 映像](../get-started/manage-operating-system-images.md)

- [發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>建立部署 OS 的工作順序

使用工作順序自動執行 OS 的安裝。 根據所選部署方法之不同，工作順序可能有其他考量。

如需詳細資訊，請參閱下列文章：

- [建立工作順序以安裝 OS](create-a-task-sequence-to-install-an-operating-system.md)

- [管理使用者狀態](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> 部署

- 使用下列其中一個部署方法來部署 OS：  

  - [使用 PXE 透過網路部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

  - [使用多點傳送透過網路來部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

  - [建立 OEM 原廠或本機 Depot 的映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [使用獨立媒體，而不使用網路來部署 Windows](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [透過網路使用可開機媒體部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [使用軟體中心透過網路部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>監視  

如需詳細資訊，請參閱[監視 OS 部署](monitor-operating-system-deployments.md)。  

> [!Note]
> 當您重新安裝 UEFI 裝置的映像時，Windows 開機管理程式會在開機載入器中建立新的項目。 當您重複重新安裝裝置的映像時 (例如，在測試環境或學生實驗室中)，此行為最為明顯。 這通常不會影響到裝置的效能或使用方式。 如果清單變得太大，某些特定的硬體裝置可能會發生功能問題。 例如，無法經由外接式 USB 磁碟機開機，或無法從清單中選取目前的開機項目。 請使用 Windows **bcdedit** 命令清除未使用的開機項目。 如需詳細資訊，請參閱 [BCDEdit /deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue)。<!-- 2841926 -->
