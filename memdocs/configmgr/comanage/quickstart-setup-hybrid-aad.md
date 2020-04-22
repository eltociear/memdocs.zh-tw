---
title: 設定混合式 Azure AD
titleSuffix: Configuration Manager
description: 如果您的環境目前有已加入網域的 Windows 10 裝置，請先設定混合式 Azure AD，然後再啟用共同管理
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e2f7bbb51c72fa3d0f2a36e8a5419552d468b4c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691216"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>設定混合式 Azure AD 以進行共同管理

如果您的Windows 10 裝置已加入至內部部署 Active Directory，請先將這些裝置加入至 Azure Active Directory (Azure AD)，然後才能在 Configuration Manager 中啟用共同管理。 此流程稱為「混合式 Azure AD 加入」。 

在下列影片中，資深專案經理 Sandeep Deo 與產品行銷經理 Adam Harbour 正在討論和示範如何在 Azure AD 中設定裝置：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

混合式 Azure AD 加入流程會向 Azure AD 自動註冊已加入內部部署網域的裝置。 如需有關此程序的詳細資訊，請參閱下列文章：
- [Azure Active Directory 中的裝置管理簡介](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [如何規劃混合式 Azure AD 加入](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) \(機器翻譯\)

混合式 Azure AD 加入是可用來進行共同管理的重要基礎之一。 此程序對某些客戶來說可能具有挑戰性，例如：
- 您的組織使用協力廠商身分識別解決方案 
- 設定 Active Directory 同盟服務 (ADFS) 的複雜度

解決這些挑戰，可能需要一些指導方針。 此文章有助於降低任何延遲。


## <a name="how-to-do-it"></a>如何進行

建立您想要保護的身分識別時，裝置類似於使用者。 如果隨時隨地都要保護裝置的身分識別，您需要將該裝置的身分識別帶入 Azure AD。

根據您使用的網域類型而定，有兩種主要方式可執行此動作。 針對下列網域類型設定混合式 Azure AD 加入：  
- [同盟網域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [受控網域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

上述兩種方法會提供最佳體驗。 如需詳細資訊 (包括完全手動的程序)，請參閱下列文章：
- [手動設定已加入混合式 Azure AD 的裝置](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) \(機器翻譯\)  
- [適用於混合式 Azure AD 的 ADFS 傳遞驗證](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview) \(機器翻譯\)，其中包含 Azure AD 探索  

如需疑難排解指導方針，請參閱 [Windows 10 混合式 Azure AD 加入的疑難排解指南](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current) \(機器翻譯\)。



## <a name="case-study"></a>案例研究

有一家大型歐洲軟體公司，其網路中的使用者已超過 100,000 位，而該公司採取了細微且分階段的方法來啟用混合式 Azure AD 加入。

在規劃階段，由於混合式 Azure AD 加入為支援共同管理的重要元素，因此，Configuration Manager 系統管理員會與身分識別小組合作。 此軟體公司有許多 ADFS 規則，其中有些很複雜。 為了解決此挑戰，身分識別小組先檢閱了現有的 ADFS 規則，然後再啟用混合式 Azure AD 加入。 IT 小組也選擇將 Azure AD Connect 升級至最新版。 Azure AD Connect 現在提供自動化程序流程來啟用混合式 Azure AD 加入。

在其進入生產階段前的環境中成功部署和測試之後，此客戶會針對整個生產資產啟用混合式 Azure AD 加入。 他們會在一週內共同管理每部 Windows 10 裝置。



## <a name="contact-fasttrack"></a>連絡 FastTrack

如果您在設定 Azure AD 的程序中任何時刻需要協助，請移至 [Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登入並要求提供協助。 

如需詳細資訊，請參閱[從 FastTrack 取得協助](quickstart-fasttrack.md)。 

