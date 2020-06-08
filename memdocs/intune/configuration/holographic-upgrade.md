---
title: 在 Microsoft Intune 中升級至 Windows Holographic for Business - Azure | Microsoft Docs
description: 在 Microsoft Intune 中使用裝置組態設定檔，升級至 Windows 10 Holographic for Business。
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d561d2682cf90d5d7075640c260d8f21c8b891b1
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556110"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>將執行 Windows Holographic 的裝置升級至 Windows Holographic for Business

Microsoft Intune 包含許多設定，可協助管理和保護您的裝置。 本文列出並描述可將 Windows 全像攝影版裝置升級至 Windows Holographic for Business 的設定。

作為行動裝置管理 (MDM) 解決方案的一部分，請使用這些設定來升級您的 Windows 全像攝影版裝置。 至於 Microsoft HoloLens，您可購買 Commercial Suite，以取得升級所需的授權。 如需詳細資訊，請參閱[解除鎖定 Windows Holographic for Business 功能](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise)。

身為 Intune 系統管理員，您可以建立這些設定並將其指派給您的裝置。

如需此功能的詳細資訊，請參閱[升級 Windows 10 版本或啟用 S 模式](edition-upgrade-configure-windows-10.md)。

## <a name="before-you-begin"></a>開始之前

[建立 Windows 10 版本升級和模式切換裝置組態設定檔](edition-upgrade-configure-windows-10.md#create-the-profile)。

當您建立 Windows 10 版本升級和模式切換裝置組態設定檔時，設定會比本文所列的更多。 Windows Holographic for Business 裝置支援本文中的設定。

## <a name="edition-upgrade"></a>版本升級

- **要升級的目標版本**：選取 [Windows 10 Holographic for Business]。
- **授權檔案**：瀏覽至提供給您的 XML 授權檔案並加以選取。

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="在 Intune 中，輸入包含 Holographic for Business 授權資訊的 XML 檔案名稱。":::

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以針對 [Windows 10 及更新版本](edition-upgrade-windows-settings.md)裝置建立版本升級設定檔。
