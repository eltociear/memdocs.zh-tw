---
title: 使用 Microsoft Intune 建立 macOS 核心延伸模組裝置設定檔 - Azure |Microsoft Docs
titleSuffix: ''
description: 新增或建立 macOS 裝置設定檔，然後將核心延伸模組設定為允許使用者覆寫、新增小組識別碼，以及 Microsoft Intune 中的組合和小組識別碼。
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
ms.openlocfilehash: 8f9212d275b17db6a40e3133b5363cd13c9d13d6
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551436"
---
# <a name="add-macos-kernel-extensions-in-intune"></a>在 Intune 中新增 macOS 核心延伸模組

> [!NOTE]
> 系統延伸模組即將取代 macOS 核心延伸模組。 如需詳細資訊，請參閱[支援提示：在 Intune 中使用系統延伸模組，不要使用 macOS Catalina 10.15 的核心延伸模組](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413)。

在 macOS 裝置上，您可以在核心層級新增功能。 這些功能可存取一般程式無法存取的作業系統部分。 貴組織可能會有應用程式、裝置功能等等中未提供的特定需求或需求。 

若要新增一律允許在您的裝置上載入的核心延伸模組，請在 Microsoft Intune 中新增「核心延伸模組」(KEXT)，然後將這些延伸模組部署到您的裝置。

例如，您的病毒掃描程式會掃描您的裝置是否有惡意內容。 您可以在 Intune 中將此病毒掃描程式的核心延伸模組新增為允許的核心延伸模組。 然後，將延伸模組「指派」至您的 macOS 裝置。

有了這項功能，系統管理員可以讓使用者覆寫核心延伸模組、新增小組識別碼，以及在 Intune 中新增特定核心延伸模組。

本功能適用於：

- macOS 10.13.2 與更新版本

若要使用這項功能，裝置必須：

- 使用 Apple 的裝置註冊計劃 (DEP) 在 Intune 中註冊。 [自動註冊 macOS 裝置](../enrollment/device-enrollment-program-enroll-macos.md)有詳細資訊。

  或

- 已在 Intune 中使用「使用者核准的註冊」進行註冊 (Apple 的條款)。 [針對 macOS High Sierra 中核心延伸模組的變更做準備](https://support.apple.com/en-us/HT208019) (開啟 Apple 的網站) 有詳細資訊。

Intune 會使用「組態設定檔」來依據貴組織的需求建立和自訂這些設定。 在設定檔中新增這些功能之後，您接著可以將設定推送貨部署到您組織中的 macOS 裝置。

本文說明如何使用 Intune 中的核心延伸模組來建立裝置組態設定檔。

> [!TIP]
> 如需有關核心延伸模組的詳細資訊，請參閱[核心延伸模組概觀](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (開啟 Apple 的網站)。

## <a name="what-you-need-to-know"></a>您必須知道的事項

- 可新增未簽署的舊版核心延伸模組。
- 請務必輸入核心延伸模組的正確小組識別碼和套件組合識別碼。 Intune 不會驗證您輸入的值。 如果您輸入錯誤的資訊，此延伸模組將無法在裝置上使用。 小組識別碼的長度剛好是 10 個英數字元。 

> [!NOTE]
> Apple 已發行所有軟體簽署和公證的相關資訊。 在 macOS 10.14.5 和更新版本上，透過 Intune 部署的核心延伸模組不需要符合 Apple 的公證原則。
>
> 如需此公證原則及任何更新或變更的詳細資訊，請參閱下列資源：
>
> - [散發前公證應用程式](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (開啟 Apple 的網站) 
> - [針對 macOS High Sierra 中核心延伸模組的變更做準備](https://support.apple.com/en-us/HT208019) (開啟 Apple 的網站)

> [!NOTE]
> Intune 使用者介面 (UI) 正在更新為全螢幕體驗，而且可能需要數週的時間。 在您的租用戶收到此更新之前，當您建立或編輯此文章中所述的設定時，您的工作流程將略有不同。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。
3. 輸入下列內容：

    - **平台**：選取 [macOS] 
    - **設定檔**：選取 [延伸模組]  。

4. 選取 [建立]  。
5. 在 [基本資訊]  中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱是 **macOS：將核心延伸模組新增至裝置**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]  。

7. 在 [組態設定]  中進行設定：

    - [macOS](kernel-extensions-settings-macos.md)

8. 選取 [下一步]  。
9. 在 [範圍標籤]  (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]  。

10. 在 [指派]  中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]  。

11. 在 [檢閱 + 建立]  中，檢閱您的設定。 當您選取 [建立]  時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="next-steps"></a>後續步驟

建立設定檔之後即可加以指派。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
