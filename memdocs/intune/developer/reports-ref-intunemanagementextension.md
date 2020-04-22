---
title: IntuneManagementExtension 實體
titleSuffix: Microsoft Intune
description: Intune 資料倉儲 API 中實體集合的 IntuneManagementExtension 實體類別參考主題。
keywords: Intune 資料倉儲
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8152eb12779376e1885d0a2b2898cd602aa825d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79359764"
---
# <a name="reference-for-intune-management-extensions"></a>Intune 管理延伸模組的參考

**intuneManagementExtensions** 類別包含的行動裝置實體，可追蹤下列資訊：

- IntuneManagementExtension 的版本
- IntuneManagementExtension 的安裝狀態

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

**intuneManagementExtensionVersion** 實體會列出 intuneManagementExtensions 使用的所有版本。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| extensionVersionKey |intuneManagementExtensions 版本的唯一識別碼。 | 1 |
| extensionVersion |4 位數的版本號碼。 |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

**intuneManagementExtensionHealthState** 會列出 intuneManagementExtensions 的所有可能健康情況狀態。

| 屬性  | Description | 範例 |
|---------|------------|--------|
| extensionStateKey |健全狀況狀態的唯一識別碼。 | 2 |
| extensionState |IntuneManagementExtension 的健全狀況狀態。 | Healthy |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

**intuneManagementExtension** 會列出每部 Windows 10 裝置每日的 IntuneManagementExtensions 健康情況。
保留最近 60 天的資料。 


|      屬性       |                         Description                         | 範例 |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               日期的唯一識別碼。                |   123   |
|      tenantKey      |              租用戶的唯一識別碼。               |   456   |
|      deviceKey      |              裝置的唯一識別碼。               |   789   |
| extensionVersionKey | intuneManagementExtension 版本的唯一識別碼。 |    1    |
|  extensionStateKey  |             健全狀況狀態的唯一識別碼。              |    2    |

