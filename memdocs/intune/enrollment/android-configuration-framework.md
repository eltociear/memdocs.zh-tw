---
title: Android Enterprise 安全性設定架構
titleSuffix: Microsoft Intune
description: 了解針對 Android Enterprise 裝置基本和高安全性的限制和所建議的設定。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502934"
---
# <a name="android-enterprise-security-configuration-framework"></a>Android Enterprise 安全性設定架構

Android Enterprise 安全性設定架構是適用於裝置合規性和設定原則設定的一系列建議。 這些建議可協助您將組織的行動裝置安全性保護打造為符合自己的特定需求。

具備安全性意識的組織會尋找能確實保護行動裝置上公司資料的方式。 其中一個用來保護該資料的方式是使用裝置註冊。 裝置註冊能協助組織：
- 部署合規性原則 (例如 PIN 強度、越獄/Root 驗證等等)。
- 部署設定原則 (例如 WIFI、憑證、VPN)。
- 管理應用程式生命週期。

為了協助您設定完整的安全性案例，Microsoft 已針對 [Windows 10 中的安全性設定](https://aka.ms/secconframework) \(英文\) 引進新的分類法。 Intune 針對其 Android Enterprise 安全性設定架構也使用類似的分類法。 其包含針對基本、增強及高安全性所建議的裝置合規性和裝置限制設定。 此分類法已在下列文章中說明：

1. [Android Enterprise 架構部署方法](framework-deployment-methodology.md)：部署安全性設定架構的建議方法。
2. [Android 裝置註冊限制](device-enrollment-restrictions.md)：適用於 Android Enterprise 裝置的預先註冊裝置限制。
3. [為 Android Enterprise 裝置設定應用程式設定原則](android-app-configuration-policies.md)：將裝置上的應用程式設定為不允許個人帳戶。
4. [Android Enterprise 工作設定檔安全性設定](android-work-profile-security-settings.md)：適用於工作設定檔裝置上基本和高安全性的特定組態設定。
5. [Android Enterprise 完全受控安全性設定](android-fully-managed-security-settings.md)：適用於完全受控裝置上基本、增強及高安全性的特定組態設定。

## <a name="android-enterprise-enrollment-modes"></a>Android Enterprise 註冊模式

在 Android 5.0 中，Google 已引進 Android Enterprise，其包含兩種註冊模式。 Android Enterprise 安全性設定架構能為這兩種模式提供建議。
- [完全受控裝置 (裝置擁有者)](android-fully-managed-enroll.md)：適用於與單一使用者相關聯、由公司擁有的裝置。 這種裝置專門用於工作，而非個人用途。
- [工作設定檔 (設定檔擁有者)](android-work-profile-enroll.md)：通常適用於 IT 想要在其中清楚分隔工作和個人資料的個人擁有裝置。 由 IT 所控制的原則，可確保工作資料無法傳送到個人設定檔中。


## <a name="next-steps"></a>後續步驟

[Android Enterprise 架構部署方法](framework-deployment-methodology.md)