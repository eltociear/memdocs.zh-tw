---
title: 使用 Microsoft Intune 開啟 iOS/iPadOS 受監管模式
titleSuffix: ''
description: 了解如何使用 Intune 開啟 iOS/iPadOS 受監管模式。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/15/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8190814-07f0-42d8-9b3a-87c67dd2b7ed
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da03bb3fdf1f0d67639f7719215d756b7d598d7c
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325078"
---
# <a name="turn-on-iosipados-supervised-mode"></a>開啟 iOS/iPadOS 受監管模式


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple iOS/iPadOS 受監管模式讓管理員在管理 Apple 裝置時擁有更多選項，適合用於大規模部署的屬公司擁有裝置。 舉例來說，您可以限制 AirDrop 或防止使用者變更裝置名稱。 如需需要受監管模式的設定清單，請參閱 [Intune 中的 iOS 裝置限制設定](../configuration/device-restrictions-ios.md)。

Intune 在 Apple [裝置註冊計劃 (DEP)](../enrollment/device-enrollment-program-enroll-ios.md) 中提供受監管模式的支援。

如需需要監督的 Apple 控制權清單，請參閱 Apple 的 [Payload settings reference](http://help.apple.com/configurator/mac/2.4/#/cad5370d089) (承載設定參考)。

## <a name="turn-on-supervised-mode-during-enrollment"></a>在註冊期間開啟受監管模式

在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，您可在[於 DEP 中建立 Apple 註冊設定檔](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile)時為裝置開啟受監督模式。 在 [裝置管理設定]  下，選取 [受監督]  方塊。

## <a name="turn-on-supervised-mode-after-enrollment"></a>在註冊之後開啟受監管模式

註冊之後，開啟受監管模式的唯一方式是將 iOS/iPadOS 裝置連接到 Mac，然後[使用 Apple Configurator](../enrollment/apple-configurator-enroll-ios.md) (這會重設裝置)。 您無法在註冊之後，於 Intune 中設定裝置的受監管模式。

## <a name="identify-a-supervised-device"></a>識別受監管的裝置

若要判斷裝置是否受監管，請檢查鎖定畫面或 [關於]  頁面：
- 裝置的鎖定畫面上會顯示**此 iPhone 是由「公司名稱」管理。**
- 裝置的 [關於]  頁面上會顯示**此 iPhone 已被監管。「公司名稱」可以監控您的 Internet 流量並定位此裝置。**

## <a name="next-steps"></a>後續步驟

如需其他裝置管理選項，請參閱[什麼是 Microsoft Intune 裝置管理？](device-management.md)
