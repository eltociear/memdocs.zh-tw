---
title: 使用裝置註冊管理員帳戶註冊裝置
titleSuffix: Microsoft Intune
description: 使用裝置註冊管理員帳戶，在 Intune 中註冊裝置。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 27ec9e4c407dd8ef1a94e9c443f62ea5456866dc
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808146"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>使用裝置註冊管理員帳戶在 Intune 中註冊裝置

您可以使用裝置註冊管理員 (DEM) 帳戶，向單一 Azure Active Directory 帳戶註冊多達 1,000 部行動裝置。 DEM 是 Intune 權限，可套用至 AAD 使用者帳戶，並讓使用者註冊多達 1,000 部裝置。 如果裝置在交給裝置使用者之前就已註冊並備妥，則 DEM 帳戶會很有用。 根據設計，Microsoft Intune 中有最多 150 個裝置註冊管理員 (DEM) 帳戶的限制。

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>以 DEM 帳戶註冊裝置的限制

DEM 使用者帳戶及以 DEM 使用者帳戶註冊的裝置具有下列限制：

- DEM 帳戶使用者必須獲指派 Intune 授權。
- 無法從公司入口網站進行抹除。 您可以從 Azure 入口網站中的 Intune，對 DEM 使用者帳戶註冊的裝置進行抹除。
- 只有本機裝置會出現在公司入口網站應用程式或網站中。
- DEM 使用者帳戶無法將 Apple 大量採購方案 (VPP) 應用程式與 Apple VPP 使用者授權搭配使用，因為應用程式管理需要個別使用者的 Apple ID。
- 透過 Apple 的自動裝置註冊 (ADE) 註冊裝置時，無法使用 DEM 帳戶。
- 裝置如果具有 Apple VPP 裝置授權，即可以安裝 VPP 應用程式。
- 裝置已針對條件式存取封鎖，但 indows 10 1803+ 除外
- 使用 DEM 帳戶註冊的每部裝置都必須獲得正確授權，才能由 Intune 進行管理。 授權可能是 Intune 使用者授權或 Intune 裝置授權。
- 若要使用 DEM 帳戶[註冊 Android Enterprise 工作設定檔裝置](android-work-profile-enroll.md)，每個帳戶只能註冊 10 部裝置。
- [不支援使用 DEM 帳戶註冊 Android Enterprise 完全受控裝置](android-fully-managed-enroll.md)。

## <a name="add-a-device-enrollment-manager"></a>新增裝置註冊管理員

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，選擇 [裝置]   > [註冊裝置]   > [裝置註冊管理員]  。

2. 選取 [新增]  。

3. 在 [新增使用者]  刀鋒視窗中，輸入 DEM 使用者的使用者主體名稱，然後選取 [新增]  。 DEM 隨即會新增至 DEM 使用者清單。

## <a name="permissions-for-dem"></a>DEM 的權限

需要具備全域管理員或 Intune 服務管理員 Azure AD 角色以
- 將 DEM 權限指派給 Azure AD 使用者帳戶
- 查看所有 DEM 使用者

若未針對使用者指派全域管理員或 Intune 服務管理員角色，但他們具備已針對所指派裝置註冊管理員角色啟用的讀取權限，則只能看到他們所建立的 DEM 使用者。


## <a name="remove-device-enrollment-manager-permissions"></a>移除裝置註冊管理員權限

移除裝置註冊管理員並不會影響已註冊的裝置。

**移除裝置註冊管理員**

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，選擇 [裝置]   > [註冊裝置]   > [裝置註冊管理員]  。
2. 在 [裝置註冊管理員]  刀鋒視窗上，依序選取 DEM 使用者和 [刪除]  。

