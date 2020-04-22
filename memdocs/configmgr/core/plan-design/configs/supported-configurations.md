---
title: 支援的設定
titleSuffix: Configuration Manager
description: 識別重要設定和需求，讓您可以規劃、部署和維護作用中的 Configuration Manager 部署。
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09618acc1c0950c3eaae79cca59fcf71dc7ef61e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688516"
---
# <a name="supported-configurations-for-configuration-manager"></a>支援的 Configuration Manager 設定

適用於：  Configuration Manager (最新分支)

Configuration Manager 是內部部署解決方案，利用伺服器、用戶端、網路設定和其他產品 (例如 Microsoft Intune、SQL Server 和 Azure)。

本主題和下列主題中的資訊是為了協助您識別重要設定、需求和限制，讓您可以規劃、部署和維護作用中 Configuration Manager 部署。  這項資訊是 Configuration Manager 站台、階層和受管理裝置的基礎結構所特有。

Configuration Manager 功能需要更特定設定時，功能特定文件會包含該資訊，而且該資訊補充更一般的設定詳細資料。  

 Configuration Manager 支援下列主題所述的產品和技術。 不過，本內容所含的內容並不代表任何超出產品個別支援週期之產品的支援延伸。 已不再支援搭配 Configuration Manager 使用超過其支援生命週期的產品，包括[延長安全性更新 (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates)計畫所涵蓋的任何產品。 如需 Microsoft 支援週期的詳細資訊，請造訪 [Microsoft 支援週期](https://go.microsoft.com/fwlink/p/?LinkId=208270) 網站。 如需有關 Configuration Manager 中延長安全性更新的詳細資訊，請參閱[Configuration Manager 針對用戶端和裝置支援的 OS 版本](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU)。

> [!NOTE]  
>  如需 Microsoft 支援週期原則的相關資訊，請前往 Microsoft 支援週期原則常見問題集網站，位於 [Microsoft 支援週期原則常見問題集](https://go.microsoft.com/fwlink/p/?LinkId=31976)。  

 此外，除非已在 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/) (企業行動力和安全性部落格) 上公告下列主題中未列出的產品和產品版本，否則 Configuration Manager 不予支援。  有些時候，此部落格上的內容會早於本文件內容的更新。


-  [大小和縮放比例](../../../core/plan-design/configs/size-and-scale-numbers.md)  
了解不同 Configuration Manager 階層設計中支援的站台數目、每個站台的站台系統角色以及用戶端或裝置。

-  [站台和站台系統必要條件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
了解 Windows Server 上支援不同站台類型和站台系統角色所需的設定。

-  [支援的站台系統伺服器作業系統](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
了解您可以用作站台伺服器或站台系統伺服器的作業系統。

-  [用戶端和裝置的支援作業系統](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
了解您可以使用 Configuration Manager 管理的作業系統，包括 Windows、Windows Embedded、Linux 和 UNIX、Mac，以及行動裝置。

-  [支援的主控台作業系統](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
了解哪些作業系統可以裝載 Configuration Manager 主控台，以提供用來管理部署的存取點。  

-  [SQL Server 版本支援](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
了解可裝載站台資料庫和報表資料庫的 SQL Server 版本，以及您可以使用的必要設定和選擇性設定。

-  [高可用性選項](../../servers/deploy/configure/high-availability-options.md)  
了解可在設計環境以協助維護 Configuration Manager 部署的高階可用服務時實作的選項。

-  [建議的硬體](../../../core/plan-design/configs/recommended-hardware.md)  
了解可協助您識別用來裝載 Configuration Manager 站台和主要服務之正確硬體和設定的指導方針。

-  [Active Directory 網域支援](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
了解 Configuration Manager 所需要和支援的支援 Active Directory 網域設定。

-  [Windows 功能和網路支援](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
了解支援的 Windows 技術 (例如 BranchCache 和重複資料刪除)，以及與 Configuration Manager 搭配使用時的限制。

-  [虛擬化環境支援](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
深入了解如何使用支援的虛擬機器技術。
