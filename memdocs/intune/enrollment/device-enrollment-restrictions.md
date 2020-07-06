---
title: 適用於 Android Enterprise 安全性設定架構的裝置註冊限制
titleSuffix: Microsoft Intune
description: 適用於 Android Enterprise 安全性設定架構的裝置註冊限制。
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
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502914"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Android Enterprise 裝置註冊限制

在針對 [Android Enterprise 安全性設定架構]()註冊裝置之前，組織必須設定適當的限制。 這些限制能確保使用者只可以註冊
- 核准的裝置。
- 指定數目的裝置。
- 具有指定平台的裝置。
- 具有指定作業系統的裝置。
- 來自指定製造商的裝置。

如需裝置註冊限制的詳細資訊，請參閱[設定註冊限制](enrollment-restrictions-set.md)。

## <a name="work-profile-basic-level-1-security-restrictions"></a>工作設定檔基本 (層級 1) 安全性限制

針對 Android Enterprise 工作設定檔基本安全性 (層級 1)，必須實作下列裝置限制：

| 類型 | 平台 | 版本 | 允許個人裝置 |
|--------|--------|--------|--------|
| Android 企業 | 允許 | Android 5.0 及更新版本。<p>Microsoft 建議將最低 Android 主要版本設定為符合 Microsoft 應用程式所支援的 Android 版本。 遵守 Android Enterprise 建議需求的 OEM 和裝置必須支援目前發行版本 + 一個字母升級。   目前，Android 建議知識工作者使用 Android 8.0 和更新版本。 如需詳細資訊，請參閱 [Android Enterprise Recommended 規格需求](https://www.android.com/enterprise/recommended/requirements/)。 | 是 |
| Android 裝置管理員| 封鎖 | 所有版本 | 是 |

## <a name="work-profile-high-level-3-security-restrictions"></a>工作設定檔高 (層級 3) 安全性限制
針對 Android Enterprise 工作設定檔高安全性 (層級 3)，應該要實作下列裝置限制：

| 類型 | 平台 | 版本 | 允許個人裝置 |
|--------|--------|--------|--------|
| Android 企業 | 允許 | Android 8.0 及更新版本 | 是 |
| Android 裝置管理員| 封鎖 | 所有版本 | 是 |

## <a name="fully-managed-security-restrictions"></a>完全受控安全性限制
透過檢閱 Android Enterprise 完全受控註冊，來確保組織支援 Android Enterprise 完全受控裝置註冊。 

## <a name="next-steps"></a>後續步驟

[設定應用程式設定原則](android-app-configuration-policies.md)
