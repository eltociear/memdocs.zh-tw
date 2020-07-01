---
title: 在 Microsoft Intune 中使用端點安全性原則管理磁碟加密 | Microsoft Docs
description: 使用 Microsoft 端點管理員中的端點安全性磁碟加密原則，為您管理的裝置設定及部署原則。
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
ms.openlocfilehash: a8eeb8263e337fa7427818c05f183fdea3c9dbea
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353627"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Intune 中端點安全性的磁碟加密原則

端點安全性磁碟加密設定檔只會聚焦在與裝置內建加密方法相關的設定，例如 FileVault 或 BitLocker。 這樣聚焦可讓安全性系統管理員輕鬆管理磁碟加密設定，而無須瀏覽大量不相關的設定。

雖然您可以使用裝置設定的 *Endpoint Protection* 設定檔來進行相同的裝置設定，但裝置組態設定檔會包含其他設定類別。 由於其他這些設定與磁碟加密無關，因此可能會使僅針對磁碟加密進行的設定工作變得複雜。

磁碟加密原則的端點安全性原則位於 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) [端點安全性] 節點中的 [管理] 下方。

## <a name="prerequisites-for-disk-encryption-policy"></a>磁碟加密原則的必要條件

- **macOS** - macOS 10.13 或更新版本
- **Windows** - Windows 10 或更新版本

## <a name="disk-encryption-profiles"></a>磁碟加密設定檔

**macOS 設定檔**：

- **FileVault** - FileVault 為 macOS 裝置提供內建的完整磁碟加密。

  管理 macOS 的 [FileVault 設定](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault)。

  若要建立 FileVault 設定檔，請參閱[使用 macOS 的 FileVault 磁碟加密](../protect/encrypt-devices-filevault.md) (機器翻譯)。

**Windows 10 設定檔**：

- **BitLocker** - BitLocker 磁碟機加密是一項整合在作業系統中的資料保護功能，可以應付資料竊取威脅，或面臨遺失、遭竊或電腦不當除役的風險

  管理 Windows 10 的 [BitLocker 設定](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)。

  若要建立 BitLocker 設定檔，請參閱[在 Intune 中管理 Windows 10 的 BitLocker 原則](../protect/encrypt-devices.md)。

## <a name="manage-device-encryption"></a>管理裝置加密

在您部署原則以加密裝置磁碟後，請參閱下列文章以取得管理加密的資訊：

- [管理 BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [管理 FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [監視裝置加密](../protect/encryption-monitor.md)

## <a name="next-steps"></a>後續步驟

- [建立 FileVault 設定檔](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [建立 BitLocker 設定檔](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
