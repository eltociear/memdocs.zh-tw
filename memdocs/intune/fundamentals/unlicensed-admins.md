---
title: 註冊或登入 Microsoft Intune
description: 如何註冊 Microsoft Intune 訂用帳戶，或如何登入以開始使用訂用帳戶。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae30e03a03b4d690bdaa9e6a4c73da6ab15226f7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095751"
---
# <a name="unlicensed-admins"></a>未授權的系統管理員

您可以在沒有 Intune 授權的情況下，將 Intune/Microsoft Endpoint Manager 系統管理中心的存取權授與系統管理員。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > [租用戶管理] > [系統管理員授權]。
2. 選擇 [允許未經授權的系統管理員進行存取] > [是]。
    >[!WARNING]
    >按一下 [是] 之後，就無法復原此設定。

3. 從現在開始，登入 Microsoft Endpoint Manager 系統管理中心的使用者不需要 Intune 授權。 存取範圍由其獲指派的角色所定義。

Intune 對每個安全性群組最多支援 350 個未授權的系統管理員。 超過此限制的系統管理員將會遇到未預期的行為。




