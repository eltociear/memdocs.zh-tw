---
title: 使用 Microsoft Intune 建立 macOS 系統與核心延伸模組 - Azure | Microsoft Docs
titleSuffix: ''
description: 新增或建立會設定系統延伸模組或是核心延伸模組的 macOS 裝置設定檔，以允許使用者覆寫、新增小組識別碼，以及在 Microsoft Intune 中新增套件組合與小組識別碼。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990295"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>在 Intune 中新增 macOS 系統與核心延伸模組

> [!NOTE]
> 系統延伸模組即將取代 macOS 核心延伸模組。 如需詳細資訊，請參閱[支援提示：在 Intune 中使用系統延伸模組，不要使用 macOS Catalina 10.15 的核心延伸模組](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413)。

在 macOS 裝置上，您可新增核心延伸模組與系統延伸模組。 核心延伸模組和系統延伸模組都可供使用者安裝應用程式延伸模組，以擴充作業系統的原生功能。 核心延伸模組會在核心層級執行其程式碼。 系統延伸模組會在嚴格控制的使用者空間中執行。

若要新增一律允許在您的裝置上載入的延伸模組，請使用 Microsoft Intune。 Intune 會使用「組態設定檔」來依據貴組織的需求建立和自訂這些設定。 在設定檔中新增這些功能之後，接著請將該設定檔推送或部署至您組織中的 macOS 裝置。

本文將說明系統延伸模組與核心延伸模組。 同時也將說明如何使用 Intune 中的延伸模組，建立裝置組態設定檔。

## <a name="system-extensions"></a>系統延伸模組

系統延伸模組在使用者空間中執行，不會存取核心。 目標是提高安全性、提供更佳的終端使用者控制，以及限制住核心層級的攻擊數。 這些延伸模組可以是：

- 驅動程式延伸模組，包括 USB 的驅動程式、網路介面卡 (NIC)、序列控制器，以及人性化介面裝置 (HID)
- 網路延伸模組，包括內容篩選器、DNS Proxy 與 VPN 用戶端
- 端點安全性延伸模組，包含端點偵測、端點回應與防毒

系統延伸模組包含在應用程式套件組合中，且從應用程式安裝。

如需有關系統延伸模組的詳細資訊，請參閱[系統延伸模組](https://developer.apple.com/documentation/systemextensions) (英文) (開啟 Apple 的網站)。

## <a name="kernel-extensions"></a>核心延伸模組

核心延伸模組會在核心層級新增功能。 這些功能可存取一般程式無法存取的作業系統部分。 貴組織可能會有應用程式、裝置功能等等中未提供的特定需求或需求。

例如，您的病毒掃描程式會掃描您的裝置是否有惡意內容。 您可以在 Intune 中將此病毒掃描程式的核心延伸模組新增為允許的核心延伸模組。 然後，將延伸模組「指派」至您的 macOS 裝置。

有了這項功能，系統管理員可以讓使用者覆寫核心延伸模組、新增小組識別碼，以及在 Intune 中新增特定核心延伸模組。

如需有關核心延伸模組的詳細資訊，請參閱[核心延伸模組](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (英文) (開啟 Apple 的網站)。

## <a name="prerequisites"></a>先決條件

- 本功能適用於：

  - macOS 10.13.2 及更新版本 (核心延伸模組)
  - macOS 10.15 及更新版本 (系統延伸模組)

  從 macOS 10.15 到 10.15.4，核心延伸模組與系統延伸模組可並存執行。

- 若要使用這項功能，裝置必須：

  - 使用 Apple 的裝置註冊計劃 (DEP) 在 Intune 中註冊。 [自動註冊 macOS 裝置](../enrollment/device-enrollment-program-enroll-macos.md)有詳細資訊。

    或

  - 已在 Intune 中使用「使用者核准的註冊」進行註冊 (Apple 的條款)。 [針對 macOS High Sierra 中核心延伸模組的變更做準備](https://support.apple.com/en-us/HT208019) (開啟 Apple 的網站) 有詳細資訊。

## <a name="what-you-need-to-know"></a>您必須知道的事項

- 可新增未簽署的舊版核心延伸模組與系統延伸模組。
- 請務必輸入該延伸模組正確的小組識別碼與套件組合識別碼。 Intune 不會驗證您輸入的值。 如果您輸入錯誤的資訊，此延伸模組將無法在裝置上使用。 小組識別碼的長度剛好是 10 個英數字元。

> [!NOTE]
> Apple 已發行所有軟體簽署和公證的相關資訊。 在 macOS 10.14.5 和更新版本上，透過 Intune 部署的核心延伸模組不需要符合 Apple 的公證原則。
>
> 如需此公證原則及任何更新或變更的詳細資訊，請參閱下列資源：
>
> - [散發前公證應用程式](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (開啟 Apple 的網站) 
> - [針對 macOS High Sierra 中核心延伸模組的變更做準備](https://support.apple.com/en-us/HT208019) (開啟 Apple 的網站)

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選取 [macOS]
    - **設定檔**：選取 [延伸模組]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱是 **macOS：在裝置上為核心延伸模組新增防毒掃描**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。

7. 在 [組態設定] 中進行設定：

    - [macOS](kernel-extensions-settings-macos.md)

8. 選取 [下一步]。
9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="next-steps"></a>後續步驟

建立設定檔之後即可加以指派。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
