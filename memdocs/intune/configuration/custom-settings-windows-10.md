---
title: 在 Microsoft Intune 中新增 Windows 10 裝置的自訂設定 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中新增或建立自訂設定檔，將 OMA-URI 設定用於執行 Windows 10 的裝置。 使用自訂設定檔新增自訂設定。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96074f4bea22b7468b1f210d631f0912eeafe7b5
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428998"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>在 Intune 中使用 Windows 10 裝置的自訂設定

本文會列出並描述您可在 Windows 10 和以上版本之裝置控制的所有不同自訂設定。 這些設定是行動裝置管理 (MDM) 解決方案的一部分，可用來設定非 Intune 內建的設定。

如需自訂設定檔詳細資訊，請參閱[使用自訂設定來建立設定檔](custom-settings-configure.md)。

這些設定會新增至 Intune 裝置組態設定檔，然後指派或部署到您的 Windows 10 裝置。

本功能適用於：

- Windows 10 和更新版本

Windows 10 自訂設定檔會使用開放行動聯盟的統一資源識別項 (OMA-URI) 設定來進行各種功能設定。 行動裝置製造商通常會使用這些設定來控制裝置上的功能。

Windows 10 讓許多設定服務提供者 (CSP) 設定可供使用，例如[原則設定服務提供者 (原則 CSP)](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers)。

如果您正在尋找特定的設定，請記住 [Windows 10 裝置限制設定檔](device-restrictions-windows-10.md)包含許多內建設定。 因此，您可能不需要輸入自訂值。

## <a name="before-you-begin"></a>開始之前

[建立 Windows 10 自訂設定檔](custom-settings-configure.md#create-the-profile)。

## <a name="oma-uri-settings"></a>OMA-URI 設定

**新增**：輸入下列設定：

- **名稱**：輸入 OMA-URI 設定的唯一名稱，協助您在設定清單中識別該設定。
- **描述**：輸入描述來概述設定和其他重要的詳細資料。
- **OMA-URI** (區分大小寫)：輸入您要用作設定的 OMA-URI。
- **資料類型**：選取您要用於這個 OMA-URI 設定的資料類型。 選項包括：

  - Base64 (檔案)
  - 布林值
  - 字串 (XML 檔案)
  - 日期和時間
  - 字串
  - 浮點數
  - 整數

- **值**：輸入要與您輸入之 OMA-URI 相關聯的資料值。 該值取決於您選取的資料類型。 例如，如果您選取 [日期和時間]，請從日期選擇器選取值。

新增一些設定之後，您可以選取 [匯出]。 [匯出] 會以逗號分隔值 (.csv) 檔案格式，為您新增的所有值建立一份清單。

## <a name="find-the-policies-you-can-configure"></a>尋找可設定的原則

在 [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (設定服務提供者參考) 中，可以找到 Windows 10 所支援所有設定服務提供者 (CSP) 的完整清單。

並非所有設定都與所有的 Windows 10 版本相容。 [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (設定服務提供者參考) 告訴您每個 CSP 所支援的版本。

此外，Intune 不支援所有在 [Configuration service provider reference](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) (設定服務提供者參考) 中列出的設定。 若要了解 Intune 是否支援您想要的設定，請開啟該設定的文章。 每個設定頁面都會顯示它所支援的作業。 若要使用 Intune，該設定必須支援 [新增]、[取代] 及 [取得] 作業。 若 **Get** 作業傳回的值與 **Add** 或 **Replace** 作業所提供值不相符，則 Intune 會報告合規性錯誤。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

[深入了解 Intune 中的自訂設定檔](custom-settings-configure.md)。
