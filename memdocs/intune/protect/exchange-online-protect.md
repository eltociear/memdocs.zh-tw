---
title: 沒有裝置管理功能的 Exchange
titleSuffix: Microsoft Intune
description: 使用 Microsoft Intune 讓員工存取其 Office 365 Exchange Online 電子郵件，而不必設定裝置管理系統。
keywords: Office 365 Exchange 電子郵件存取
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/31/2017
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.technology: ''
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8746a6dee0b35dec7886a596d0448874dfb04f16
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352016"
---
# <a name="protect-office-365-exchange-online-without-requiring-device-management"></a>保護 Office 365 Exchange Online 而不需要進行裝置管理

您可以讓員工存取其公司電子郵件，而沒有設定裝置管理系統的額外負荷。 您可以透過 Intune 存取 Office 365 Exchange Online。 若要完成必要步驟，請確認您擁有 Microsoft 365 或 Azure Active Directory (進階) 和 Intune 的授權。 員工需要擁有[支援的 iOS/iPadOS 或 Android 裝置](../fundamentals/supported-devices-browsers.md)。 

您可以決定設定裝置管理系統。 這類型應用程式保護的運作方式與裝置管理無關。 

## <a name="action-plan"></a>動作計劃

1. [深入了解條件式存取](conditional-access.md)。 
2. [了解以應用程式為基礎的條件式存取](app-based-conditional-access-intune.md)。
3. [為 Exchange Online 設定以應用程式為基礎的條件式存取原則](app-based-conditional-access-intune-create.md)。
4. [封鎖無法管理的應用程式](app-modern-authentication-block.md)，特別是未使用 Azure Active Directory Authentication Library (ADAL) 的應用程式。
5. (選擇性) [為 SharePoint Online 設定以應用程式為基礎的條件式存取原則](app-based-conditional-access-intune-create.md)。 這些原則會封鎖存取來自無法管理和保護之應用程式的公司資料。 原則也會透過 SharePoint 行動來限制存取權。 

## <a name="what-to-tell-employees-and-students"></a>員工和學生須知

* 要求您的員工和學生從 Apple App Store 下載並安裝 iOS/iPadOS 版 Microsoft Outlook 或 Microsoft SharePoint，或是從 Google Play Store 下載並安裝 Android 版 Microsoft Outlook 或 Microsoft SharePoint。 
* 如果您封鎖存取未使用新式驗證的應用程式，則請讓員工和學生知道這項限制。 

## <a name="next-steps"></a>後續步驟

您已使用以應用程式為基礎的條件式存取，來提高公司資料的安全性。 在接下來的步驟中，您可以深入了解提高公司資料保護的其他方式，包含： 

* 根據裝置合規性、裝置風險、位置和使用者屬性，設定 [Active Directory 和 Azure Active Directory 中的條件式存取](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)。  
* 設定應用程式保護原則，可協助您保護公司資料，防止有意或無意的資料外洩。 
* 利用 Azure 資訊保護，保護網路外部的公司資料。 

需要啟用這個案例或其他 EMS 或 Office 365 案例的協助嗎？ 如果您至少有 Microsoft 365、Enterprise Mobility + Security 或 Azure Active Directory Premium 的 150 個授權，請使用 [FastTrack 權益](https://docs.microsoft.com/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program)。 
