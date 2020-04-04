---
title: Microsoft Intune 中的 macOS 核心延伸模組設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 在 macOS 裝置上新增、設定或建立設定，以使用核心延伸模組。 此外，允許使用者覆寫核准的延伸模組、允許來自某個小組識別碼的所有延伸模組，或允許 Microsoft Intune 中的特定延伸模組或應用程式。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359288"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>在 Intune 中設定和使用核心延伸模組的 macOS 裝置設定

此文章列出並描述您可以在 macOS 裝置上控制的各種不同核心擴充功能設定。 作為行動裝置管理 (MDM) 解決方案的一部分，請使用這些設定在裝置上新增和管理核心延伸模組。

若要深入了解 Intune 中的核心延伸模組，以及任何必要條件，請參閱[新增 macOS 核心延伸模組](kernel-extensions-overview-macos.md)。

這些設定會新增至 Intune 裝置組態設定檔，然後指派或部署到您的 macOS 裝置。

## <a name="before-you-begin"></a>開始之前

[建立裝置核心延伸模組組態設定檔](kernel-extensions-overview-macos.md)。

> [!NOTE]
> 這些設定適用於不同註冊類型。 如需不同註冊類型的詳細資訊，請參閱 [macOS 註冊](../enrollment/macos-enroll.md)。

## <a name="kernel-extensions"></a>核心延伸模組

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>設定適用於：使用者核准的自動裝置註冊

- **允許使用者覆寫**：[允許]  可讓使用者核准未包含在組態設定檔中的核心延伸模組。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可防止使用者允許未包含在組態設定檔中的延伸模組。 換句話說，只允許包含在組態設定檔中的延伸模組。

  如需這項功能的詳細資訊，請參閱 [User-Approved Kernel Extension Loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (使用者核准的核心延伸模組載入)。

- **允許的小組識別碼**：使用此設定可允許一或多個小組識別碼。 任何以所輸入小組識別碼簽署的核心延伸模組都會被允許並受到信任。 換句話說，使用此選項可允許相同小組識別碼內的所有核心延伸模組，這可能是特定的開發人員或合作夥伴。

  **新增**所要載入其有效且已簽署核心延伸模組的小組識別碼。 您可以新增多個小組識別碼。 小組識別碼必須是英數字元 (字母和數字) 且包含 10 個字元。 例如，輸入 `ABCDE12345`。

  新增小組識別碼之後，您也可以將它刪除。

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (尋找小組識別碼) (會開啟 Apple 的網站) 會提供詳細資訊。

- **允許的核心延伸模組**：使用此設定可允許特定的核心延伸模組。 只有所輸入的核心延伸模組會被允許或受到信任。

  **新增**所要載入其核心延伸模組的套件組合識別碼和小組識別碼。 針對未簽署的舊版核心延伸模組，請使用空白的小組識別碼。 您可以新增多個核心延伸模組。 小組識別碼必須是英數字元 (字母和數字) 且包含 10 個字元。 例如，針對 [套件組合識別碼]  輸入 `com.contoso.appname.macos`，並針對 [小組識別碼]  輸入 `ABCDE12345`。

  > [!TIP]
  > 若要在 macOS 裝置上取得核心延伸模組 (Kext) 的套件組合識別碼，您可以：
  >
  > 1. 在終端機中，執行 `kextstat | grep -v com.apple`，並記下輸入。 安裝所要的軟體或 Kext。 再次執行 `kextstat | grep -v com.apple`，並尋找變更。
  >
  >    在終端機中，`kextstat` 會列出 OS 上的所有核心延伸模組。 
  >
  > 2. 在裝置上，開啟 Kext 的資訊屬性清單檔案 (Info.plist)。 套件組合識別碼隨即顯示。 每個 Kext 都有 Info.plist 檔案儲存在其中。

> [!NOTE]
> 您不需要新增小組識別碼和核心延伸模組。 您可以對其中一個進行設定。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
