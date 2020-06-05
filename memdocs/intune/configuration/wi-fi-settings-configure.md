---
title: 在 Microsoft Intune 中建立裝置的 Wi-Fi 設定檔 - Azure | Microsoft Docs
description: 請查看在 Microsoft Intune 中建立 Wi-Fi 裝置組態設定檔的步驟。 建立適用於 Android 裝置系統管理員、Android 企業、Android kiosk、iOS、iPadOS、macOS、Windows 10 及更新版本，以及 Windows Holographic for Business 的設定檔。 您可以使用這些設定檔建立 WiFi 連線以使用憑證、選擇 EAP 類型、選取驗證方法、啟用 Proxy，以及執行更多作業。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca2a5ddd3d2b4c0aa93c7c955d0d688944ee8f95
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985510"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>在 Microsoft Intune 中新增 Wi-Fi 設定並在您的裝置上使用

Wi-Fi 是許多行動裝置用來存取網路的無線網路。 Microsoft Intune 包含內建的 Wi-Fi 設定，可被部署到貴組織中的使用者和裝置。 這組設定稱為「設定檔」，其可被指派給不同的使用者和群組。 指派之後，您的使用者即可在無須自行設定的情況下存取貴組織的 Wi-Fi 網路。

例如，您安裝了名為 Contoso Wi-Fi 的新 Wi-Fi 網路。 然後您要將所有 iOS/iPadOS 裝置都設定為連線到此網路。 程序如下︰

1. 建立包含可連線到 Contoso Wi-Fi 無線網路之設定的 Wi-Fi 設定檔。
2. 將設定檔指派給包含所有 iOS/iPadOS 裝置使用者的群組。
3. 使用者即可在其裝置上的無線網路清單中找到新的 Contoso Wi-Fi 網路。 然後他們可以使用您選擇的驗證方法連線到網路。

本文列出建立 Wi-Fi 設定檔的步驟。 它也包含說明每個平台之不同設定的連結。

## <a name="supported-device-platforms"></a>支援的裝置平台

Wi-Fi 設定檔支援下列裝置平台：

- Android 5 及更新版本
- Android 企業與 kiosk
- iOS 11.0 與更新版本
- iPadOS 13.0 和更新版本
- macOS X 10.12 與更新版本
- Windows 10 及更新版本、Windows 10 行動裝置版，以及 Windows Holographic for Business

> [!NOTE]
> 對於執行 Windows 8.1 的裝置，可以匯入先前從其他裝置所匯出的 Wi-Fi 設定。

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

    - **設定檔**：選取 [Wi-Fi]。

      > [!TIP]
      >
      > - 針對以專用裝置 (kiosk) 形式執行的 **Android 企業**裝置，您可以選擇 [僅限裝置擁有者] > [Wi-Fi]。
      > - 您可為 **Windows 8.1 和更新版本**選擇 [Wi-Fi 匯入]。 此選項可讓您以先前從不同裝置所匯出的 XML 檔案方式匯入 Wi-Fi 設定。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：為設定檔輸入描述性名稱。 命名您的設定檔，以方便之後能輕鬆識別。 例如，良好的設定檔名稱為**整個公司的 WiFi 設定檔**。
    - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。
7. 在 [組態設定] 中，您可進行的設定會根據您選擇的平台而不同。 選取您的平台來進行詳細設定：

    - [Android 裝置系統管理員](wi-fi-settings-android.md)
    - [Android 企業](wi-fi-settings-android-enterprise.md)，包括專用裝置
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 和更新版本](wi-fi-settings-windows.md)
    - [Windows 8.1 和更新版本](wi-fi-settings-import-windows-8-1.md)，包含 Windows Holographic for Business

8. 選取 [下一步]。
9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

> [!TIP]
> 若您針對 Wi-Fi 設定檔使用以憑證為基礎的驗證，請部署 Wi-Fi 設定檔、憑證設定檔及信任的根設定檔至相同群組，以確保每部裝置都能識別您憑證授權單位的合法性。  如需詳細資訊，請參閱[如何使用 Microsoft Intune 設定憑證](../protect/certificates-configure.md)。


## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接者，請[指派此設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

[在 Intune 中針對 Wi-Fi 設定檔進行疑難排解](troubleshoot-wi-fi-profiles.md)。
