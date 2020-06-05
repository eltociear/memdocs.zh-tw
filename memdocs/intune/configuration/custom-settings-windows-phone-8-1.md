---
title: 在 Microsoft Intune 中將自訂設定新增至 Windows Phone 8.1 裝置 - Azure | Microsoft Docs
titleSuffix: ''
description: 在 Microsoft Intune 中新增或建立自訂設定檔，將 OMA-URI 設定用於執行 Windows Phone 8.1 的裝置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce8433ee87c0f5e4b397003b78c0ceb751eb46b7
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556263"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>在 Intune 中使用 Windows Phone 8.1 裝置的自訂設定

透過 Microsoft Intune，您可以使用「自訂設定檔」新增或建立 Windows Phone 8.1 裝置的自訂設定。 自訂設定檔是 Intune 中的功能。 其設計目的是為了新增 Intune 中未內建的裝置設定和功能。

Windows Phone 8.1 自訂設定檔會使用開放行動聯盟的統一資源識別項 (OMA-URI) 設定來進行各種功能設定。 行動裝置製造商通常會使用這些設定來控制裝置上的功能。 [Windows Phone 8.1 MDM 通訊協定文件](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10))會列出這些設定。

本文示範如何建立 Windows Phone 8.1 裝置的自訂設定檔。 

## <a name="before-you-begin"></a>開始之前

[建立 Windows Phone 8.1 自訂設定檔](custom-settings-configure.md)。

## <a name="custom-oma-uri-settings"></a>自訂 OMA-URI 設定

- **OMA-URI 設定**：按一下 [新增] 進行下列設定：

  - **名稱**：輸入 OMA-URI 設定的唯一名稱，協助您在設定清單中識別該設定。
  - **描述**：輸入描述來概述設定及其他可協助您找到設定檔的相關資訊。
  - **OMA-URI** (區分大小寫)：輸入您要用作設定的 OMA-URI。
  - **資料類型**：選取您要用於這個 OMA-URI 設定的資料類型。 選項包括：

    - 字串
    - 字串 (XML 檔案)
    - 日期和時間
    - 整數
    - 浮點數
    - 布林值
    - Base64 (檔案)

  - **值**：輸入要與您輸入之 OMA-URI 相關聯的資料值。 該值取決於您選取的資料類型。 例如，如果您選取 [日期和時間]，請從日期選擇器選取值。

  新增一些設定之後，您可以選取 [匯出]。 [匯出] 會以逗號分隔值 (.csv) 檔案格式，為您新增的所有值建立一份清單。

## <a name="example"></a>範例

在下列範例中，當在電訊廠商的涵蓋範圍外行動時，將無法變更 Windows 8.1 電話裝置的行動電話通訊網路。

- **名稱**：允許行動數據漫遊
- **描述**：允許或禁止行動數據漫遊
- **OMA-URI** (區分大小寫)：./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **資料類型**：整數
- **值**：0

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

[在 Windows 10 裝置上建立自訂設定檔](custom-settings-windows-10.md)。
