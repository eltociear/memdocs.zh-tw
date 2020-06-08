---
title: 使用 Microsoft Intune 的端點安全性原則管理攻擊帳戶防護設定 | Microsoft Docs
description: 設定及部署使用 Microsoft 端點管理員端點安全性帳戶防護原則設定所管理的裝置原則。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 6fb5702b7c809c7810004a53d084f19fa94dea9e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431848"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Intune 中端點安全性的帳戶防護原則

使用 Intune 端點安全性原則來保護帳戶，以保護使用者的身分識別和帳戶。 帳戶防護原則著重於 Windows Hello 和 Credential Guard 的設定，這是 Windows 身分識別與存取管理的一部分。

- *Windows Hello 企業版*使用電腦和行動裝置上的強式雙重要素驗證來取代密碼。
- *Credential Guard* 可協助保護您在裝置上使用的認證和祕密。

若要深入了解，請參閱 Windows 身分識別與存取管理文件中的[身分識別與存取管理](https://docs.microsoft.com/windows/security/identity-protection/)。

在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的 [端點安全性] 節點中，在 [管理] 下尋找帳戶防護的端點安全性原則。

檢視[帳戶防護設定檔的設定](../protect/endpoint-security-asr-profile-settings.md)。

## <a name="prerequisites-for-account-protection-profiles"></a>帳戶防護設定檔的必要條件

- Windows 10 或更新版本

## <a name="account-protection-profiles"></a>帳戶防護設定檔

*帳戶防護設定檔已開放預覽*。

**Windows 10 設定檔**：

- **帳戶防護** *(預覽)* - 帳戶防護原則的設定可協助您保護使用者認證。

## <a name="next-steps"></a>後續步驟

[設定端點安全性原則](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
