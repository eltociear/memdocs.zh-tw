---
title: 虛擬化支援
titleSuffix: Configuration Manager
description: 在虛擬化環境中安裝 Configuration Manager 用戶端和站台系統角色的需求。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688546"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager 的虛擬化環境支援

適用於：  Configuration Manager (最新分支)

Configuration Manager 支援在支援的作業系統上安裝用戶端和站台系統角色，且這些作業系統是在本文的虛擬化環境中執行作為虛擬機器。 這項支援即使是在虛擬機器主機 (虛擬化環境) 不支援做為用戶端或站台伺服器的情況下都存在。  

例如，您使用 Microsoft Hyper-V Server 2012 裝載執行 Windows Server 2012 的虛擬機器。 您可以在執行 Windows Server 2012 的虛擬機器上安裝用戶端或站台系統角色。 您無法在執行 Microsoft Hyper-V Server 2012 的主機上安裝用戶端。  

## <a name="virtualization-environments"></a>虛擬化環境

- Windows Server 2019  
- Windows Server 2016 <sup>[附註 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[附註 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a> 附註 1：巢狀虛擬化

Configuration Manager 不支援[巢狀虛擬化](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)，這是 Windows Server 2016 的新功能。

### <a name="virtualization-environment-support"></a>虛擬化環境支援

每部虛擬電腦都必須有您用於實體 Configuration Manager 電腦的相同硬體和軟體需求。  

若要驗證您的虛擬化環境受到 Configuration Manager 支援，請使用伺服器虛擬化驗證方案。 它包含線上虛擬化方案支援原則精靈。 如需詳細資訊，請參閱 [Windows Server 虛擬化驗證方案](https://www.windowsservercatalog.com/svvp.aspx) \(英文\)。  

> [!NOTE]  
> Configuration Manager 不支援在 Mac 電腦上執行的虛擬電腦或虛擬伺服器客體作業系統。  

除非虛擬機器處於線上狀態，否則 Configuration Manager 無法管理虛擬機器。 無法更新離線虛擬機器映像，也無法在主機電腦上使用 Configuration Manager 用戶端收集清查。  

虛擬機器沒有特殊的考量。 例如，如果虛擬機器已停止並重新啟動，而未儲存已套用更新之虛擬機器的狀態，Configuration Manager 可能無法判斷更新是否要重新套用至虛擬機器映像。  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Microsoft Azure 虛擬機器  

Configuration Manager 可以在 Azure 虛擬機器上執行，就像在資料中心內部部署執行一樣。 在下列案例中，搭配使用 Configuration Manager 與 Azure 虛擬機器：  

- **案例 1**：在 Azure 虛擬機器上執行 Configuration Manager。 使用它來管理其他 Azure 虛擬機器上的用戶端。  

- **案例 2**：在 Azure 虛擬機器上執行 Configuration Manager。 使用它來管理在 Azure 之外執行的用戶端。  

- **案例 3**：在 Azure 虛擬機器上執行不同的 Configuration Manager 站台系統角色。 在正確地連線至 Azure 的內部部署資料中心執行其他角色。  

適用於在內部部署上安裝 Configuration Manager 的相同網路、支援的設定和硬體 Configuration Manager 需求，也適用於在 Azure 虛擬機器上安裝。  

如需詳細資訊，請參閱 [Azure 上的 Configuration Manager](../../understand/configuration-manager-on-azure.md)。

> [!IMPORTANT]  
> 此外，在 Azure 虛擬機器上執行的 Configuration Manager 站台和用戶端受限於與內部部署安裝相同的授權需求。  

## <a name="windows-virtual-desktop"></a>Windows 虛擬桌面

[Windows 虛擬桌面](https://docs.microsoft.com/azure/virtual-desktop/)是 Microsoft Azure 和 Microsoft 365 的預覽功能。 從 1906 版開始，請使用 Configuration Manager 來管理這些在 Azure 中執行 Windows 的虛擬裝置。 如需詳細資訊，請參閱[用戶端和裝置的支援作業系統](supported-operating-systems-for-clients-and-devices.md)。
