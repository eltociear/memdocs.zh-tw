---
title: 升級到 Windows 10
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager，將 OS 從 Windows 7 或更新版本升級到 Windows 10。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8bfb45ba835851c33d6017f7f0a884bd2c1e9421
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429328"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>使用 Configuration Manager 將 Windows 升級為最新版

適用於：  Configuration Manager (最新分支)

本文提供 Configuration Manager 中將電腦上的 OS 升級的步驟。 有不同的部署方法可供您選擇，例如獨立媒體或軟體中心。 就地升級案例具有下列功能：  

- 將 OS 升級至 Windows 10 或 Windows Server 2016 和更新版本

- 保留電腦上的應用程式、設定和使用者資料

- 沒有外部相依性，例如 Windows ADK

- 比傳統 OS 部署更快也更有彈性

> [!Note]  
> Windows 10 就地升級工作順序現在支援部署到透過[雲端管理閘道](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)管理的網際網路型用戶端。 此功能讓遠端使用者可以更輕鬆地升級到 Windows 10，而不需連線到內部網路。 如需詳細資訊，請參閱[透過 CMG 部署 Windows 10 就地升級](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)。 <!-- 1357149 -->


## <a name="supported-versions"></a>支援的版本

### <a name="upgrade-version"></a>升級版本

僅建立升級至下列 OS 版本的 OS 升級套件：

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>原始版本

裝置必須執行下列其中一個 OS 版本，以設定 OS 升級工作順序的目標：

#### <a name="windows-client"></a>Windows 用戶端

- Windows 7
- Windows 8.1
- 舊版的 Windows 10。 例如，您可以將 Windows 10 1809 版升級到 Windows 10 1903 版。  

如需詳細資訊，請參閱 [Windows 10 升級路徑](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths)。

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- 舊版的 Windows Server 2016
- 舊版的 Windows Server 2019

若要進一步了解 Windows Server 支援的升級路徑，請參閱 [Windows Server 2016 支援的升級路徑](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)和 [Windows Server 升級中心](https://aka.ms/upgradecenter)。


## <a name="plan"></a><a name="BKMK_Plan"></a> 方案  

### <a name="task-sequence-requirements-and-limitations"></a>工作順序需求和限制

檢閱升級 OS 之工作順序的下列需求和限制，以確定它符合您的需要：  

- 只新增與升級 OS 核心工作相關的工作順序步驟。 這些步驟主要包括安裝套件、應用程式或更新。 也請使用執行命令列、PowerShell 或設定動態變數的步驟。  

- 檢閱電腦上安裝的驅動程式和應用程式。 部署升級工作順序之前，請確定驅動程式與 Windows 10 相容。  

下列工作與就地升級不相容。 它們需要您使用傳統 OS 部署：  

- 變更電腦的網域成員資格或更新本機 Administrators 群組。  

- 實作電腦上的基本變更，例如：

  - 變更磁碟分割
  - 將系統架構從 x86 變更為 x64
  - 實作 UEFI (如需可能選項的詳細資訊，請參閱[在就地升級期間從 BIOS 轉換至 UEFI](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu))。
  - 修改基本 OS 語言  

- 您有自訂需求，包括使用自訂基底映像、使用協力廠商磁碟加密，或需要 WinPE 離線作業。  

### <a name="infrastructure-requirements"></a>基礎結構需求  

升級案例的唯一先決條件是讓發佈點可供使用。 發佈 OS 升級套件以及您在工作順序中包含的任何其他套件。 如需詳細資訊，請參閱[安裝或修改發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。


## <a name="configure"></a><a name="BKMK_Configure"></a> 設定  

### <a name="prepare-the-os-upgrade-package"></a>準備 OS 升級套件  

Windows 10 升級套件包含在目的地電腦上升級 OS 所需的來源檔案。 升級套件的版本、架構和語言必須與要升級的用戶端相同。 如需詳細資訊，請參閱[管理 OS 升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>建立工作順序以升級 OS  

使用[建立工作順序以升級 OS](create-a-task-sequence-to-upgrade-an-operating-system.md) 中的步驟，自動升級 OS。  

> [!NOTE]  
> 若要建立工作順序以將 OS 升級到 Windows 10，一般會使用[建立工作順序以升級 OS](create-a-task-sequence-to-upgrade-an-operating-system.md) 中的步驟。 該工作順序包含**升級 OS** 步驟，以及其他建議的步驟和群組，以處理整個升級流程。
>
> 您可以建立自訂工作順序，並新增[升級 OS](../understand/task-sequence-steps.md#BKMK_UpgradeOS) 步驟。 此步驟是將 OS 升級到 Windows 10 所需的唯一步驟。 如果您選擇這個方法，請在**升級 OS** 步驟之後，也加上[重新啟動電腦](../understand/task-sequence-steps.md#BKMK_RestartComputer)步驟，以完成升級。 請務必使用 [目前安裝的預設作業系統]  設定，將電腦重新啟動為已安裝的 OS，而不是 Windows PE。  


## <a name="deploy"></a><a name="BKMK_Deploy"></a> 部署  

若要部署 OS，請使用下列其中一個部署方法：  

- [使用軟體中心透過網路部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

- [使用獨立媒體，而不使用網路來部署 Windows](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > 當您使用獨立媒體時，工作順序必須內含開機映像。 此設定會使工作順序可在工作順序媒體精靈中使用。


## <a name="monitor"></a>監視  

若要監視工作順序部署以升級 OS，請參閱[監視 OS 部署](monitor-operating-system-deployments.md)。  
