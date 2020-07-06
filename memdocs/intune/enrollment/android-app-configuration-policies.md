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
ms.openlocfilehash: 6ecd15ea98ff9fa5ff0ff6ff570e644a8dcf5003
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502946"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Android Enterprise 安全性設定架構應用程式設定原則

作為 [Android Enterprise 安全性設定架構](android-configuration-framework.md)的一部分，您必須適當地針對 Android Enterprise 裝置設定應用程式設定原則。

Android Enterprise 工作設定檔裝置是設計來將工作與個人資料彼此隔離。 Android Enterprise 完全受控裝置是設計來僅搭配公司或學校資料使用。 因此，部署到這些裝置上的 Microsoft 應用程式必須設定為不允許個人帳戶。

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>在 Android Enterprise 裝置上不允許針對 Microsoft 應用程式使用個人帳戶

1. 將應用程式新增到受控的 Google Play。 如需詳細資訊，請參閱[使用 Intune 將受控 Google Play 應用程式新增至 Android Enterprise 裝置](../apps/apps-add-android-for-work.md)。
2. 如[為受控的 Android Enterprise 裝置新增應用程式設定原則]()中所述，為每個受控的 Google Play 應用程式建立原則。
3. 在每個原則中建立下列單一機碼：

    | 機碼 | 值 |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | 一或多個；分隔的 UPN。<br>只有允許的帳戶才是這個索引鍵所定義受控使用者帳戶。<br>針對已註冊到 Intune 的裝置，可以使用 {{userprincipalname}} 語彙基元來代表註冊的使用者帳戶。 |


## <a name="next-steps"></a>後續步驟
套用 [Android Enterprise 工作設定檔安全性設定](android-work-profile-security-settings.md)或 [Android Enterprise 完全受控安全性設定](android-fully-managed-security-settings.md)。