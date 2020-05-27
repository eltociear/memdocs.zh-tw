---
title: 在 Microsoft Intune 中使用原則以限制裝置功能 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中，新增裝置設定檔，以限制 Android 裝置系統管理員、Android Enterprise、macOS、iOS、iPadOS、Windows Phone 與 Windows 10 裝置上的功能。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 951293ff723ff0243d4068656497cbe0bca27ef9
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989174"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>在 Microsoft Intune 中設定裝置限制設定

Intune 包含裝置限制原則，可協助系統管理員控制 Android、iOS/iPadOS、macOS 及 Windows 裝置。 這些限制可讓您控制廣泛的設定及功能，以保護您組織的資源。 例如，系統管理員可以：

- 允許或封鎖裝置相機。
- 控制針對 Google Play、App Store、檢視文件，以及遊戲的存取。
- 封鎖內建應用程式，或建立允許或禁止的應用程式清單。
- 允許或防止將檔案備份至雲端和儲存體帳戶。
- 設定密碼長度下限，以及封鎖簡單密碼。

這些功能可於 Intune 中取得，並可由系統管理員設定。 Intune 會使用「組態設定檔」來依據貴組織的需求建立和自訂這些設定。 在設定檔中新增這些功能之後，您接著便可以將設定檔推送或部署到您組織中的裝置。

本文會示範如何建立裝置限制設定檔。 您也可以查看適用於不同平台的所有可用設定。

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
        - **Windows 8.1 及更新版本**
        - **Windows Phone 8.1**

    - **設定檔**：選取 [裝置限制]。

        若想要建立像是 Surface Hub 等 Windows 10 團隊版裝置的裝置限制設定檔，選擇 [裝置限制 (Windows 10 團隊版)]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱為 **iOS/iPadOS：Block camera on devices**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。

7. 在 [組態設定] 中，您可進行的設定會根據您選擇的平台而不同。 選擇您平台來進行詳細設定：

    - [Android 裝置系統管理員](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 和更新版本](device-restrictions-windows-10.md)
    - [Windows 10 團隊版](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. 選取 [下一步]。
9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="next-steps"></a>後續步驟

建立設定檔之後即可加以指派。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
