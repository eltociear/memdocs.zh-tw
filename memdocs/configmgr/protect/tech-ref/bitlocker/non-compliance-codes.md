---
title: 不符合規範代碼
titleSuffix: Configuration Manager
description: 不符合 BitLocker 原則規範的 Configuration Manager 用戶端可能代碼技術參考
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705956"
---
# <a name="non-compliance-codes"></a>不符合規範代碼

適用於：  Configuration Manager (最新分支)

<!--3601034-->

用戶端上的 WMI 會提供下列不符合規範代碼。 其也會說明特定裝置遭回報為不符合規範的原因。

有各種方法可以檢視 WMI。 例如，使用下列 PowerShell 命令：

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> 如果裝置符合規範，則此命令不會傳回任何資料。
>
> 您也可以檢查這個類別的 `Compliant` 屬性 (如果裝置符合規範，則為 `1`)。

|不符合規範代碼|不符合規範的原因|
|--- |--- |
|0|加密強度不是 AES 256。|
|1|BitLocker 原則要求此磁碟區必須加密，但其並未加密。|
|2|BitLocker 原則要求此磁碟區*不得*加密，但其已加密。|
|3|BitLocker 原則要求此磁碟區使用 TPM 保護裝置，但其並未使用。|
|4|BitLocker 原則要求此磁碟區使用 TPM+PIN 保護裝置，但其並未使用。|
|5|BitLocker 原則不允許非 TPM 機器回報為符合規範。|
|6|磁碟區有 TPM 保護裝置，但沒看到 TPM。|
|7|BitLocker 原則要求此磁碟區使用密碼保護裝置，但其並未擁有。|
|8|BitLocker 原則要求此磁碟區*不得*使用密碼保護裝置，但其已使用。|
|9|BitLocker 原則要求此磁碟區使用自動解除鎖定保護裝置，但其並未擁有。|
|10|BitLocker 原則要求此磁碟區*不得*使用自動解除鎖定保護裝置，但其已使用。|
|11|BitLocker 偵測到原則衝突，此衝突使其無法將此磁碟區回報為符合規範。|
|12|需要有系統磁碟區才能加密 OS 磁碟區，但其並不存在。|
|13|已暫停磁碟區的保護。|
|14|除非 OS 磁碟區已加密，否則自動解除鎖定保護裝置並不安全。|
|15|原則所需的加密強度下限為 XTS-AES-128 位元，實際的加密強度較弱。|
|16|原則所需的加密強度下限為 XTS-AES-256 位元，實際的加密強度較弱。|
