---
title: Microsoft Intune 中的 macOS 延伸模組設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 在 macOS 裝置上新增、設定或建立設定，以使用系統延伸模組及核心延伸模組。 此外，允許使用者覆寫核准的延伸模組、允許來自某個小組識別碼的所有延伸模組，或允許 Microsoft Intune 中的特定延伸模組或應用程式。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
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
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429521"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>在 Intune 中設定及使用核心與系統延伸模組的 macOS 裝置設定

> [!NOTE]
> 系統延伸模組即將取代 macOS 核心延伸模組。 如需詳細資訊，請參閱[支援提示：在 Intune 中使用系統延伸模組，不要使用 macOS Catalina 10.15 的核心延伸模組](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413)。

本文列出並描述您可以在 macOS 裝置上控制的各種核心與系統延伸模組設定。 您可在行動裝置管理 (MDM) 解決方案中使用這些設定，以在裝置上新增和管理延伸模組。

若要深入了解 Intune 的延伸模組及任何必要條件，請參閱[新增 macOS 延伸模組](kernel-extensions-overview-macos.md)。

這些設定會新增至 Intune 裝置組態設定檔，然後指派或部署到您的 macOS 裝置。

## <a name="before-you-begin"></a>開始之前

[建立 macOS 延伸模組組態設定檔](kernel-extensions-overview-macos.md)。

> [!NOTE]
> 這些設定適用於不同註冊類型。 如需不同註冊類型的詳細資訊，請參閱 [macOS 註冊](../enrollment/macos-enroll.md)。

## <a name="kernel-extensions"></a>核心延伸模組

本功能適用於：

- macOS 10.13.2 和更新版本
- 需有使用者核准的裝置註冊 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>設定適用於：使用者核准的裝置註冊、自動裝置註冊

- **允許使用者覆寫**：[是] 可讓使用者核准組態設定檔未包含的核心延伸模組。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可防止使用者允許未包含在組態設定檔中的延伸模組。 換句話說，只允許包含在組態設定檔中的延伸模組。

  如需這項功能的詳細資訊，請參閱 [User-Approved Kernel Extension Loading](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (使用者核准的核心延伸模組載入)。

- **允許的小組識別碼**：使用此設定可允許一或多個小組識別碼。 任何以所輸入小組識別碼簽署的核心延伸模組都會被允許並受到信任。 換句話說，使用此選項可允許相同小組識別碼內的所有核心延伸模組，這可能是特定的開發人員或合作夥伴。

  按一下 [新增]，設定要載入之已簽署且有效的核心延伸模組小組識別碼。 您可以新增多個小組識別碼。 小組識別碼必須是英數字元 (字母和數字) 且包含 10 個字元。 例如，輸入 `ABCDE12345`。

  新增小組識別碼之後，您也可以將它刪除。

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (尋找小組識別碼) (會開啟 Apple 的網站) 會提供詳細資訊。

- **允許的核心延伸模組**：使用此設定可允許特定的核心延伸模組。 只有所輸入的核心延伸模組會被允許或受到信任。

  按一下 [新增]，設定要載入之核心延伸模組的套件組合識別碼和小組識別碼。 針對未簽署的舊版核心延伸模組，請使用空白的小組識別碼。 您可以新增多個核心延伸模組。 小組識別碼必須是英數字元 (字母和數字) 且包含 10 個字元。 例如，針對 [套件組合識別碼] 輸入 `com.contoso.appname.macos`，並針對 [小組識別碼] 輸入 `ABCDE12345`。

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

## <a name="system-extensions"></a>系統延伸模組

本功能適用於：

- macOS 10.15 與更新版本
- 需有使用者核准的裝置註冊

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>設定適用於：使用者核准的裝置註冊、自動裝置註冊

- **禁止使用者覆寫**：[是] 會禁止使用者核准不在允許清單中的系統延伸模組。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許使用者核准組態設定檔未包含的未知延伸模組， 亦即允許組態設定檔未包含的延伸模組。

- **允許的小組識別碼**：使用此設定可允許一或多個小組識別碼。 只要系統延伸模組以您輸入的小組識別碼簽署，就一律允許並信任。 換句話說，使用此選項即允許特定開發人員或合作夥伴同一小組識別碼內的所有系統延伸模組。

  按一下 [新增]，設定要載入之有效且已簽署的系統延伸模組**小組識別碼**。 您可以新增多個小組識別碼。 小組識別碼必須是英數字元 (字母和數字) 且包含 10 個字元。 例如，輸入 `ABCDE12345`。

  新增小組識別碼之後，您也可以將它刪除。

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (尋找小組識別碼) (會開啟 Apple 的網站) 會提供詳細資訊。

- **允許的系統延伸模組**：使用此設定可一律允許特定的系統延伸模組。 只會允許或信任您輸入的系統延伸模組。

  按一下 [新增]，設定要載入之系統延伸模組的**套件組合識別碼**和**小組識別碼**。 若為未簽署的舊版系統延伸模組，請使用空白的小組識別碼。 您可以新增多個系統延伸模組。 小組識別碼必須是英數字元 (字母和數字) 且包含 10 個字元。 例如，針對 [套件組合識別碼] 輸入 `com.contoso.appname.macos`，並針對 [小組識別碼] 輸入 `ABCDE12345`。

- **允許的系統延伸模組類型**：輸入小組識別碼，及該小組識別碼允許的系統延伸模組類型：
  - **小組識別碼**：輸入要允許特定延伸類型的另一個系統延伸模組小組識別碼。 或者，輸入您在 [允許的系統延伸模組] 中新增的小組識別碼。
  - **允許的系統延伸模組類型**：選取各個小組識別碼要允許的系統延伸模組類型。 選項包括：
    - 全選
    - 驅動程式延伸模組
    - 網路延伸模組
    - 端點安全性延伸模組

    如需這些延伸模組類型的詳細資訊，請參閱[系統延伸模組](https://developer.apple.com/system-extensions/) (點選會開啟 Apple 的網站)。

    您可以新增**允許的系統延伸模組**清單中的小組識別碼，並允許特定的延伸模組類型。 如果延伸模組的類型不被允許，則延伸模組可能不會執行。

    若要允許某個小組識別碼的所有延伸模組類型，請將小組識別碼新增至**允許的系統延伸模組**清單。 請不要將小組識別碼新增至**允許的系統延伸模組類型**清單。 換句話說，如果小組識別碼在**允許的系統延伸模組**清單中，而不在**允許的系統延伸模組類型**清單中，就會允許該小組識別碼的所有延伸模組類型。

> [!NOTE]
> 若在**允許的系統延伸模組**和**允許的小組識別碼**中新增相同的小組識別碼，會引發錯誤並導致設定檔失敗。 請不要在這兩項設定中新增完全相同的小組識別碼。 

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
