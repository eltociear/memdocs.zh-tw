---
title: Intune 端點安全性帳戶保護原則設定 | Microsoft Docs
description: Microsoft Intune 中的端點安全性帳戶保護原則設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431991"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Intune 中端點安全性的帳戶保護原則設定

檢視您可在設定檔中，在[端點安全性原則](../protect/endpoint-security-policy.md)為 Intune 端點安全性節點「帳戶保護」原則進行的設定。

支援的平台和設定檔：

- **Windows 10 及更新版本**：
  - 設定檔：**帳戶保護** (預覽)


## <a name="account-protection-profile"></a>帳戶保護設定檔

### <a name="account-protection"></a>帳戶防護

- **封鎖 Windows Hello 企業版**

  Windows Hello 企業版是一種能取代密碼、智慧卡及虛擬智慧卡來登入 Windows 的方法。
  - **未設定** (預設) - 裝置會佈建 Windows Hello 企業版。
  - **停用** - 裝置會佈建 Windows Hello 企業版。
  - **啟用** - 裝置不會為任何使用者佈建 Windows Hello 企業版
  
- **允許使用安全性金鑰登入**

  允許使用 Windows Hello 安全性金鑰作為租用戶所有電腦的登入認證。
  - [未設定] (預設)
  - **是**

- **開啟 Credential Guard**  
  [CSP：[]DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard 會使用 Windows Hypervisor 來提供保護。 Credential Guard 需要硬體支援以進行安全開機和 DMA 保護。 這項設定只能成功用於符合硬體需求的裝置。
  - **未設定** (預設) - 停用 Credential Guard，這是 Windows 的預設。
  - **啟用且具備 UEFI 鎖定** - 啟用 Credential Guard 並禁止從遠端關閉，因為 UEFI 保存的設定必須手動清除。
  - **啟用但不具備 UEFI 鎖定** - 啟用 Credential Guard，且允許在不實際存取電腦的情況下將其關閉。

## <a name="next-steps"></a>後續步驟

[適用於帳戶保護的端點安全性原則](../protect/endpoint-security-account-protection-policy.md)
