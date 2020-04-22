---
title: 選擇裝置管理解決方案
titleSuffix: Configuration Manager
description: 了解 Microsoft 為管理電腦、伺服器與裝置所提供的解決方案。
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702266"
---
# <a name="choose-a-device-management-solution"></a>選擇裝置管理解決方案

Microsoft 提供不同的解決方案來管理電腦、伺服器與裝置。 這些解決方案可在內部部署、雲端式，或結合兩者的環境中使用。 選擇適合您組織業務需求的解決方案。 根據您需要管理的裝置平台以及您需要的管理功能做出決定。

## <a name="overview"></a>概觀

在不同情況下，可能有數個最適合您的 Microsoft 解決方案。 您不需要只選擇一個。

- 針對小型組織，Windows 系統管理中心之類的工具可能很適合。
- 大約 75% 的 IT 組織都是使用 Configuration Manager 來管理其裝置。
- Microsoft Azure 透過以伺服器管理為主要目標的 Azure Stack 從雲端或內部部署提供各種解決方案。
- Microsoft Intune 提供用戶端的雲端管理。
- 您可以將 Configuration Manager 和 Intune 與共同管理結合。

使用下表來協助比較這些管理技術：

|  | 僅雲端 | 雲端連結 | 內部部署 | 已中斷連線 |
|---------|---------|---------|---------|---------|
| **Hyper-V 主機** | 不適用 | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager |
| **Windows Server** | - Azure 管理<br/> - Configuration Manager | - Azure 管理<br/> - Configuration Manager | - Azure 管理<br/> - Configuration Manager | Configuration Manager |
| **Linux 伺服器** | Azure 管理 | Azure 管理 | Azure 管理 |  |
| **Windows 10** | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | - Intune<br/> - Configuration Manager | Configuration Manager |
| **Windows 7 或 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows 虛擬桌面** | Configuration Manager | 不適用 | 不適用 | 不適用 |

如需詳細資訊，請參閱下列文章：

- [什麼是 Azure Stack？](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [什麼是 Windows Admin Center？](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [什麼是 Virtual Machine Manager？](https://docs.microsoft.com/system-center/vmm/overview)
- [Azure 管理產品](https://docs.microsoft.com/azure/)
- [什麼是 Windows 虛擬桌面？](https://docs.microsoft.com/azure/virtual-desktop/overview)

如需 Configuration Manager 與 Intune 解決方案的詳細資訊，請繼續閱讀下一節。

## <a name="client-management"></a>用戶端管理

此節比較下列四個用戶端管理解決方案：

- [Configuration Manager 用戶端](#bkmk_sccm)
- [使用 Configuration Manager 的內部部署行動裝置管理 (MDM)](#bkmk_opmdm)
- [使用 Microsoft Intune 的共同管理](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

您可以單獨使用這些解決方案或將其互相搭配使用。 例如，使用用戶端型管理方式管理您組織中的電腦伺服器，也可以使用共同管理來管理以網際網路為基礎的筆記型電腦。 透過這種方式來合併使用方式，您就可以涵蓋所有裝置管理需求。  

也有兩個表格依下列因素比較管理解決方案：

- [依支援的平台比較](#bkmk_comp1)
- [依管理功能比較](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Configuration Manager 用戶端  

此選項需要在裝置上安裝 Configuration Manager 用戶端。 它會提供大部分的功能來管理您環境中的電腦、伺服器和其他裝置。

如需詳細資訊，請參閱[用戶端安裝方法](../clients/deploy/plan/client-installation-methods.md)。  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> 內部部署 MDM  

此選項會使用內建在 Windows 10 中的裝置管理功能。 雖然內部部署 MDM 沒有用戶端型管理的完整功能，但提供更簡單的管理方式。 它使用內部部署 Configuration Manager 資源管理裝置。  

如需詳細資訊，請參閱[使用內部部署基礎結構來管理行動裝置](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> 使用 Microsoft Intune 的共同管理

共同管理是將您現有的 Configuration Manager 部署附加至 Microsoft 365 雲端其中一種主要方式。 它可讓您使用 Configuration Manager 和 Microsoft Intune 同時管理多部 Windows 10 裝置。 共同管理可讓您透過加入新的功能，在雲端附加您在 Configuration Manager 方面現有的投資。

如需詳細資訊，請參閱[什麼是共同管理？](../../comanage/overview.md)。  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Microsoft Exchange  

此選項使用 Exchange Server 連接器將多部 Exchange 伺服器連接至 Configuration Manager。 其可集中管理能夠連線到 Exchange ActiveSync 的裝置。 您可以從 Configuration Manager 主控台設定 Exchange 行動裝置管理功能。 範例功能包括遠端裝置抹除，以及可控制多部 Exchange 伺服器的設定。

如需詳細資訊，請參閱[使用 Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> 依支援的平台比較解決方案  

|平台|Configuration Manager 用戶端|內部部署 MDM|使用 Exchange 的 Configuration Manager| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |是| 是 |
|iOS| | |是| 是 |
|Mac OS X|是| |是| 是 |
|Windows 10|是|是|是| 是 |
|Windows 10 Mobile| |是|是| 是 |
|Windows (舊版)|是| |是|  |
|Windows Server|是| |是|  |
|Windows Embedded|是| | |  |

如需支援平台的完整清單，請參閱下列文章：

- [Configuration Manager 針對用戶端和裝置支援的 OS 版本](configs/supported-operating-systems-for-clients-and-devices.md)
- [Intune 支援的設定](https://docs.microsoft.com/intune/supported-devices-browsers)

Microsoft 建議使用 Intune 管理 Android、iOS 和 Windows 10 行動裝置。 如需詳細資訊，請參閱[什麼是 Microsoft Intune？](https://docs.microsoft.com/intune/what-is-intune)。

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> 依管理功能比較解決方案  

|管理功能|Configuration Manager 用戶端|內部部署 MDM|使用 Exchange 的 Configuration Manager|  
|--------|----------------------------|---------------|-----------------------------------|  
|憑證型相互驗證|是|是| |
|用戶端安裝|是| | |
|透過網際網路支援|是| | |
|探索|是| |是|
|硬體清查|是|是|是|
|軟體清查|是| |是|
|設定|是|是|是|
|軟體部署|是|是| |
|軟體更新管理|是| | |
|OS 部署|是| | |
|封鎖 Configuration Manager|是|是| |
|隔離和封鎖 Exchange Server (及 Configuration Manager)| | |是|
|遠端抹除| |是|是|
