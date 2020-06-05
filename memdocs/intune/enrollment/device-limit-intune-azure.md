---
title: 了解 Intune 與 Azure 的裝置限制
titleSuffix: ''
description: 了解 Intune 裝置限制和 Azure AD 裝置限制之間的差異。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8610b619a4ac05f37b893060b3b3a2bcb1dae528
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864849"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>了解 Intune 與 Azure AD 的裝置限制

您可以透過兩種方式來設定裝置限制：
- Intune 註冊
- 加入 Azure Active Directory (AD) 或註冊 Azure AD

本文說明系統會在何時根據您的設定套用這些限制。

## <a name="intune-device-limit-restrictions"></a>Intune 裝置限制

Intune 裝置限定可設定使用者能夠控制的裝置數目上限 (設定上限為 15)。 若要設定此 [裝置限制]，請前往 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [裝置] > [註冊限制]。 如需詳細資訊，請參閱[建立裝置限制的限制](enrollment-restrictions-set.md#create-a-device-limit-restriction)

## <a name="azure-device-limit-restriction"></a>Azure 裝置限制的限制

Azure 裝置限制可設定加入 Azure AD 或註冊 Azure AD 的裝置數目上限。 若要設定 [每位使用者的裝置數目上限]，請前往 Azure 入口網站 > [Azure Active Directory] > [裝置]。 如需詳細資訊，請參閱[進行裝置設定](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal) (機器翻譯)

## <a name="settings-applied-based-on-user-affinity"></a>根據使用者親和性套用的設定

如果您已設定 Intune 和 Azure 這兩種裝置限制，下表是會根據使用者親和性設定套用的內容。

| 裝置平台 | 使用者親和性 | 適用於 Azure | 適用於 Intune |
| ----- | ----- | ----- | ----- | ----- |
| Android Enterprise 工作設定檔 | 是 | 是 | 是|
| Android Enterprise 專用裝置 | 否 | 否 | 否 |
| Android Enterprise 完全受控 | 是 | 是 | 是 |
| Android 裝置管理員 | 是 | 是 | 是 |
| Android 裝置系統管理員 DEM | 否 | | 否 | 
| iOS/macOS BYOD | 是 | 是 | 是 |
| iOS/macOS 的自動裝置註冊 (ADE) | 是 | 是 | 是 |
| iOS/macOS ADE | 否 | 是 | 否 |
| Windows BYOD | 是 | 是 | 是 |
| 僅限 Windows MD | | 是 | 是 |
| 已加入 Windows Azure AD| 是 | 是 | 否 |
| Windows Autopilot | 是 | 是 | 否 |
| Windows 已加入混合式 Azure AD | 否 | 否 | 是 |
| Windows 共同管理 | 否 | 是 | 否 |
| Windows DEM | 否 | 是 | 否 |
| Windows 大量註冊 | 否 | 是 | 否 |


## <a name="android-and-ios-devices"></a>Android 和 iOS 裝置

### <a name="ios-or-android-devices-example-1"></a>iOS 或 Android 裝置範例 1

- Azure 的 [每位使用者的裝置數目上限] 設定為 3。
- Intune 的 [裝置限制] 設定為 5。
 
**結果：** 數目上限以每位使用者為單位。 好比說，如果您註冊三台 Intune 裝置，則第四台裝置的 Azure 註冊將會失敗，因為設定會限制裝置的註冊數目。

### <a name="ios-or-android-devices-example-2"></a>iOS 或 Android 裝置範例 2

- Azure 的 [每位使用者的裝置數目上限] 設定為 20。
- Intune 的 [裝置限制] 設定為 2。

**結果：** 您可以成功註冊兩台裝置。 其他裝置都無法再進行 Intune 註冊。 不具使用者親和性的 ADE 雖然未與使用者建立關聯，但仍受限於 Azure 裝置註冊限制。

## <a name="windows-devices"></a>Windows 裝置

Intune 裝置限制不適用於下列 Windows 註冊類型：
- 共同受控註冊
- 群組原則物件 (GPO) 註冊
- 加入 Azure AD 的註冊
- 大量加入 Azure AD 的註冊
- Autopilot 註冊
- 裝置註冊管理員註冊

系統會將這些註冊類型視為共用裝置案例，因此您無法對其強制執行裝置限制。 您可以在 Azure Active Directory 中，為這些註冊類型設定固定限制。

若是 Azure 中的裝置限制，[每位使用者的裝置數目上限] 設定會套用至已加入 Azure AD 或已註冊 Azure AD 的裝置。 此設定不會套用至已加入混合式 Azure AD 的裝置。

### <a name="windows-10-example-1"></a>Windows 10 範例 1

- Azure 的 [每位使用者的裝置數目上限] 設定為 5。
- Intune 的 [裝置限制] 設定為 3。
- 裝置已自動加入混合式 Azure AD 並註冊 (已設定 GPO)。

**結果：** 因為註冊透過 GPO 推送，所以不適用 Azure 裝置註冊限制，  也不適用 Intune 裝置限制。

### <a name="windows-10-example-2"></a>Windows 10 範例 2

- Azure 的 [每位使用者的裝置數目上限] 設定為 5。
- Intune 的 [裝置限制] 設定為 2。
- 裝置已使用 [設定] > [存取公司或學校資源] > [連線]，加入本機網域並註冊。

**結果：** 您只能在裝置封鎖之前註冊 (enroll) 兩台裝置， 但最多可以註冊 (register) 五台裝置。


## <a name="next-steps"></a>後續步驟

- [在 Azure 中建立裝置限制](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)。
- [在 Azure 中進行裝置設定](enrollment-restrictions-set.md#create-a-device-limit-restriction)。
- [深入了解註冊和加入網域](https://docs.microsoft.com/azure/active-directory/devices/overview#getting-devices-in-azure-ad)。
