---
title: 在 Microsoft Intune - Azure 中使用自訂裝置設定 | Microsoft Docs
description: 使用 Microsoft Intune 新增或建立設定檔，以使用 Windows Phone、Windows 8.1、Windows 10 及更新版本、Android 裝置系統管理員、Android Enterprise、macOS 和 iOS/iPadOS 裝置的自訂設定。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ddbb82d3cd5c86ff32917013edd4f16b303678fe
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990087"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>在 Intune 中使用自訂設定建立設定檔

Microsoft Intune 包含許多內建設定，可控制裝置上的不同功能。 您也可以建立自訂設定檔，其建立方式類似內建設定檔。 當您想要使用未內建在 Intune 的裝置設定和功能時，自訂設定檔會很有用。 這些設定檔包含功能和設定，可讓您控制組織中的裝置。 例如，您可以建立自訂設定檔，為每部 iOS/iPadOS 裝置設定相同的功能。

為每個平台設定自訂設定的方式皆不同。 例如，若要控制 Android 與 Windows 裝置上的功能，您可輸入開放行動裝置聯盟統一資源識別項 (OMA-URI) 值。 若是 Apple 裝置，您可以使用 [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) 或 [Apple Profile Manager](https://support.apple.com/profile-manager) 匯入所建立的檔案。

如需組態設定檔的詳細資訊，請參閱[什麼是 Microsoft Intune 裝置設定檔？](device-profiles.md)。

此文章示範如何建立 Android 裝置系統管理員、Android Enterprise、iOS/iPadOS、macOS 和 Windows 的自訂設定檔。 您也可以查看適用於不同平台的所有可用設定。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選擇您的裝置平台。 選項包括：  

        - **Android 裝置系統管理員**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 及以上版本**
        - **Windows Phone 8.1**

    - **設定檔**：選取 [自訂]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，一個良好的原則名稱是 **Windows 10：自訂可啟用 AllowVPNOverCellular 自訂 OMA-URI 的設定檔**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。

7. 在 [組態設定] 中，您可進行的設定會根據您選擇的平台而不同。 選擇您平台來進行詳細設定：

    - [Android 裝置系統管理員](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. 選取 [下一步]。
9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="example"></a>範例

在下列範例中，已啟用 **Connectivity/AllowVPNOverCellular** 設定。 此設定可讓 Windows 10 裝置在行動電話通訊網路上時，開啟 VPN 連線。

> [!div class="mx-imgBorder"]
> ![包含 Intune 和端點管理員中 VPN 設定的自訂原則範例](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>後續步驟

雖然設定檔已建立，但它可能還不會執行任何動作。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
