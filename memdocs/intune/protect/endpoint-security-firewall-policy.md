---
title: 使用 Microsoft Intune 的端點安全性原則管理防火牆設定 | Microsoft Docs
description: 設定及部署您使用 Microsoft 端點管理員之端點安全性防火牆原則管理的裝置原則。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
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
ms.openlocfilehash: aa518036aa99d5de003fbc56f99748267f3cc87b
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776866"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Intune 端點安全性的防火牆原則

使用 Intune 的端點安全性防火牆原則，為執行 macOS 和 Windows 10 的裝置設定裝置內建防火牆。

雖然您可以使用裝置設定的 Endpoint Protection 設定檔來設定相同的防火牆設定，但裝置組態設定檔會包含其他的設定類別。 這些其他設定與防火牆無關，而且會讓僅針對環境設定防火牆的工作變複雜。

在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的 [端點安全性] 節點中，在 [管理] 下尋找防火牆的端點安全性原則。

檢視[防火牆設定檔的設定](../protect/endpoint-security-Firewall-profile-settings.md)。

## <a name="prerequisites-for-firewall-profiles"></a>電子郵件設定檔的必要條件

- Windows 10 或以上版本
- 所有受支援的 macOS 版本

## <a name="firewall-profiles"></a>防火牆設定檔

**macOS 設定檔**：

- **macOS 防火牆** – 啟用和設定 macOS 的內建防火牆設定。

**Windows 10 設定檔**：

- **Microsoft Defender 防火牆** – 使用進階安全性設定 Windows Defender 防火牆設定。 Windows Defender 防火牆為裝置提供主機型的雙向網路流量篩選，會封鎖未經授權的網路流量流入或流出本機裝置。

- **Microsoft Defender 防火牆規則 (預覽)**  - 定義精確的防火牆規則，包括特定的連接埠、通訊協定、應用程式與網路，以及允許或封鎖網路流量。 此設定檔的每個執行個體最多支援 150 項自訂規則。

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>防火牆規則合併和原則衝突

規劃僅使用一項原則將各種防火牆原則套用至裝置。 使用單一原則執行個體和原則類型，有助於避免兩項原則分別將不同的設定套用至相同的設定，造成衝突。 當使用不同的值管理同一設定的兩個原則執行個體或原則類型之間發生衝突時，此設定就不會傳送至裝置。

- 這種形態的原則衝突會發生在 **Microsoft Defender 防火牆**設定檔，其會與其他 Microsoft Defender 防火牆設定檔，或由裝置設定等不同原則類型傳遞的防火牆設定發生衝突。

  「Microsoft Defender 防火牆設定檔」與「Microsoft Defender 防火牆規則」設定檔不會發生衝突。

當您使用 **Microsoft Defender 防火牆規則**設定檔時，您可以將多個規則設定檔套用至相同的裝置。 不過，當使用不同設定的同一裝置存在不同的規則時，兩套規則都會傳送至裝置，並在裝置上發生衝突。

- 例如，如果一項規則封鎖 *Teams.exe* 不得通過防火牆，而第二項規則卻允許 *Teams.exe*，這兩項規則都會傳遞至用戶端。 此結果和透過防火牆設定其他原則而產生的衝突不同。

當來自多個規則設定檔的規則彼此不相衝突時，裝置會合併每個設定檔中的規則，在裝置上建立合併的防火牆規則設定。 這個行為讓您部署的規則數目，比每個個別設定檔支援裝置的150 還要多。

- 例如，您有兩個 Microsoft Defender 防火牆規則設定檔。 第一個設定檔允許 *Teams.exe* 通過防火牆。 第二個設定檔允許 *Outlook.exe* 通過防火牆。 當裝置收到這兩個設定檔後，裝置會設定成允許兩個應用程式通過防火牆。

## <a name="next-steps"></a>後續步驟

[設定端點安全性原則](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
