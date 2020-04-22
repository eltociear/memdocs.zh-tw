---
title: 第三方 MDM 共存
titleSuffix: Configuration Manager
description: 了解搭配 Configuration Manager 使用第三方 MDM 服務
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f22ba6f29e0c85e19ab66d1b052085db5303cc2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690306"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>搭配 Configuration Manager 的第三方 MDM 共存

當您同時使用 Configuration Manager 和 Microsoft Intune 來管理 Windows 10 裝置時，此功能被稱為[共同管理](overview.md)。 當您使用 Configuration Manager 來管理裝置，並註冊至第三方 MDM 服務時，此功能被稱為「共存」  。 當您針對單一裝置具備兩個管理授權單位，且沒有在兩者之間取得適當協調的情況下，可能會帶來許多挑戰性。 在使用共同管理的情況下，Configuration Manager 和 Intune 會平衡[工作負載](workloads.md)，以確保不會發生衝突。 在使用第三方服務的情況下，由於此互動並不存在，使得共存具備有限的管理能力。

Configuration Manager 用戶端可以與執行 Windows 10 1709 版或更新版本且已加入 Azure Active Directory 之裝置上的第三方 MDM 服務共存。 裝置可以是下列任一類型：

- 僅限[已加入 Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)。 (此類型有時稱為「已加入雲端網域」)  

- [已加入混合式網域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) \(部分機器翻譯\)，其中裝置已加入您的內部部署 Active Directory，並已向 Azure Active Directory 註冊。  

> [!Note]  
> 它並不支援[個人擁有的裝置](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) \(英文\)。  

當 Configuration Manager 用戶端偵測到同時有第三方 MDM 服務在管理該裝置時，它便會自動停用 Configuration Manager 中的部分工作負載。 此行為可讓 MDM 服務接管這些功能。 它也會避免用戶端上的設定發生衝突，其可能會嚴重影響到裝置和使用者體驗。 在此情況下，Configuration Manager 中的下列工作負載會被停用：

- 適用於 VPN、Wi-Fi、電子郵件及憑證設定的資源存取原則
- 應用程式管理，包括舊版套件
- 軟體更新掃描和安裝
- Endpoint Protection，此為反惡意程式碼保護功能的 Windows Defender 套件
- 適用於條件式存取的合規性原則
- 裝置設定
- Office 隨選即用管理

Configuration Manager 用戶端會繼續執行下列唯讀作業，來避免與第三方管理授權單位發生衝突：

- 硬體與軟體清查
- Asset Intelligence
- 軟體計量
- 電源管理報告

如需搭配 Configuration Manager 和 Intune 進行共同管理之優點的詳細資訊，請參閱[共同管理優點](overview.md#benefits)。
