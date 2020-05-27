---
title: 在 Microsoft Intune 中將喜好設定檔案設定新增至 macOS 裝置 - Azure | Microsoft Docs
titleSuffix: ''
description: 新增 XML 或 plist 檔案，其中包含應用程式的索引鍵資訊。 使用喜好設定檔案裝置組態設定檔來變更屬性清單檔中的索引鍵資訊，並將其指派給 macOS 裝置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
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
ms.openlocfilehash: ebf65ecc6dbe5059adbd6fec70833bf2fcab9de7
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988663"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>使用 Microsoft Intune 將屬性清單檔新增至 macOS 裝置

使用 Microsoft Intune，可以新增 macOS 裝置的屬性清單檔 (.plist)，或 macOS 裝置上應用程式的屬性清單檔。

本功能適用於：

- macOS 10.7 和更新版本

屬性清單檔包含 macOS 應用程式的資訊。 如需詳細資訊，請參閱 [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (屬性清單檔的資訊) (Apple 的網站) 和 [Custom payload settings](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1) (自訂承載設定)。

本文列出並描述可新增到 macOS 裝置的不同屬性清單檔。 請使用屬於行動裝置管理 (MDM) 解決方案的這些設定，新增應用程式的配套識別碼 (`com.company.application`)，並新增應用程式的 .plist 檔。

這些設定會新增至 Intune 裝置組態設定檔，然後指派或部署到您的 macOS 裝置。

## <a name="what-you-need-to-know"></a>您必須知道的事項

- 這些設定未經過驗證。 請務必先測試變更，再將設定檔指派給裝置。
- 如果不確定如何輸入應用程式金鑰，請在應用程式內變更設定。 然後，使用 [Xcode](https://developer.apple.com/xcode/) 檢查應用程式的喜好設定檔案，以查看設定的進行方式。 Apple 建議在匯入檔案之前，先使用 Xcode 移除無法管理的設定。
- 只有部分應用程式能使用受控喜好設定，而這些應用程式可能不允許管理所有設定。
- 請務必上傳以裝置通道設定為目標的屬性清單檔，而不是以使用者通道設定為目標的屬性清單檔。 以整個裝置為目標的屬性清單檔。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選取 [macOS]
    - **設定檔**：選取 [喜好設定檔案]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱是 **macOS：新增喜好設定檔案，以在裝置上設定 Microsoft Defender ATP**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。

7. 在 [組態設定] 中進行設定：

    - **喜好設定網域名稱**：輸入套件組合識別碼，例如 `com.company.application`。 例如，輸入 `com.Contoso.applicationName`、`com.Microsoft.Edge` 或 `com.microsoft.wdav`。

      屬性清單檔通常用於網頁瀏覽器 (Microsoft Edge)、[Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (機器翻譯) 和自訂應用程式。 當建立喜好設定網域時，也會建立套件組合識別碼。

    - **屬性清單檔**：選取與應用程式建立關聯的屬性清單檔。 請確定它是 `.plist` 或 `.xml` 檔案。 例如，上傳 `YourApp-Manifest.plist` 或 `YourApp-Manifest.xml` 檔案。

      會顯示屬性清單檔中的索引鍵資訊。 如果需要變更索引鍵資訊，請在另一個編輯器中開啟清單檔，然後在 Intune 中重新上傳該檔案。

    請確定檔案格式正確。 檔案應該只有索引鍵值組，且不應包裝在 `<dict>`、`<plist>`或 `<xml>` 標籤中。 例如，屬性清單檔應該類似下列檔案：

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. 選取 [下一步]。
9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

如需 Microsoft Edge 喜好設定檔案的詳細資訊，請參閱[使用 .plist 針對 macOS 設定 Microsoft Edge 原則設定](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac)。
