---
title: Microsoft Intune 中的 iOS/iPadOS 應用程式佈建設定檔
titleSuffix: ''
description: Intune 提供您一些工具，可讓您主動將新的佈建設定檔指派給具有即將到期應用程式的裝置。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: bbc3ba4a-df48-4aeb-988b-69a177764e3a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3cf008c708ce42611a842ff7f8720d48d57ac91
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79341616"
---
# <a name="use-ios-app-provisioning-profiles-to-prevent-your-apps-from-expiring"></a>使用 iOS 應用程式佈建設定檔以避免應用程式過期

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

## <a name="introduction"></a>簡介

指派至 iPhone 與 iPad 的 Apple iOS/iPadOS 企業營運應用程式，是使用所內含佈建設定檔與透過憑證簽署的程式碼來建置。 當該應用程式執行時，iOS/iPadOS 會確認該 iOS/iPadOS 應用程式的完整性，並強制執行由佈建設定檔定義的原則。 發生下列驗證︰

- **安裝檔案完整性** - iOS/iPadOS 會將應用程式詳細資料與企業簽署憑證的公開金鑰加以比較。 如果不同，應用程式內容可能已變更，且不允許執行該應用程式。
- **功能強制** - iOS/iPadOS 嘗試從來自應用程式安裝檔 (.ipa) 中的企業佈建設定檔 (而非個別開發人員佈建設定檔) 強制執行應用程式功能。


您用來簽署應用程式的企業簽署憑證通常會持續三年。 不過佈建設定檔將會在一年後到期。 當憑證仍然有效時，Intune 會提供工具，您可主動將新的佈建設定檔指派至有應用程式即將到期的裝置。
憑證過期後，您必須使用新的憑證再次簽署應用程式，並使用新憑證的金鑰內嵌新的佈建設定檔。

身為系統管理員，您可以包含及排除安全性群組以指派 iOS/iPadOS 應用程式佈建設定。 例如，您可以將 iOS/iPadOS 應用程式佈建設定指派給「所有使用者」，但排除執行群組。

## <a name="how-to-create-an-ios-mobile-app-provisioning-profile"></a>如何建立 iOS 行動應用程式佈建設定檔

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   > [iOS 應用程式佈建設定檔]   > [建立設定檔]  。
3. 在 [基本]  頁面上，新增下列值：
    - **名稱** - 提供此行動佈建設定檔的名稱。
    - [描述]  - 提供原則的描述 (選擇性)。
    - **上傳設定檔** - 選擇 [開啟]  圖示，然後選擇您從 [Apple 開發人員網站](https://developer.apple.com/) \(英文\) 下載的 Apple 行動組態設定檔檔案 (副檔名為 `.mobileprovision`)。

   [到期日]  將會填入您在上面新增的 Apple 行動組態設定檔檔案中的值。<br>

   <img alt="Create profile - Basics" src="/media/app-provisioning-profile-ios/app-provisioning-profile-ios-01.png">

4. 按一下 [下一步:  範圍標籤]。<br>
   在 [範圍標籤]  頁面上，您可以選擇性地設定範圍標籤，以決定誰可以在 Intune 中查看 iOS/iPadOS 應用程式佈建設定檔。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用角色型存取控制和範圍標籤](../fundamentals/scope-tags.md)。
5. 按一下 [下一步:  指派]。<br>
   [指派]  頁面可讓您將設定檔指派給使用者和裝置。 請務必注意不論裝置是否由 Intune 管理，您都可以將設定檔指派給該裝置。
6. 按一下 [下一步:  檢閱 + 建立]，以檢閱您針對設定檔輸入的值。
7. 完成後，請按一下 [建立]  ，在 Intune 中建立 iOS/iPadOS 應用程式佈建設定檔。 

## <a name="next-steps"></a>後續步驟

將設定檔指派給所需的 iOS/iPadOS 裝置。 如需詳細資訊，請使用[如何指派裝置設定檔](../configuration/device-profile-assign.md)中的步驟。
