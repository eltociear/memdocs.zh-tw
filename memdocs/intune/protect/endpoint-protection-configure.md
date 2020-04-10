---
title: 在 Microsoft Intune 中設定 Endpoint Protection 設定 - Azure | Microsoft Docs
description: 您可以在於 Microsoft Intune 中建立 macOS 或 Windows 10 裝置設定檔時，建立 Endpoint Protection 設定。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 6b5d0f88222c8d48da4f91ff3cf8d4628ccb179d
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551583"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>在 Intune 中新增 Endpoint Protection 設定

透過 Intune，您可以使用裝置組態設定檔，來管理裝置上的一般端點保護安全性功能，包括：

- 防火牆
- BitLocker
- 允許和封鎖應用程式
- Microsoft Defender 及加密

例如，您可以建立一個只允許 macOS 使用者從 Mac App Store 安裝應用程式的 Endpoint Protection 設定檔。 或者，在於 Windows 10 裝置上執行應用程式時，啟用 Windows SmartScreen。

建立設定檔之前，請檢閱下列文章，這些文章將詳細說明 Intune 可基於每個支援平台來管理的端點保護設定：

- [macOS 設定](endpoint-protection-macos.md)
- [Windows 10 設定](endpoint-protection-windows-10.md)

> [!NOTE]
> Intune 使用者介面 (UI) 正在更新為全螢幕體驗，而且可能需要數週的時間。 在您的租用戶收到此更新之前，當您建立或編輯此文章中所述的設定時，您的工作流程將略有不同。

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>建立包含 Endpoint Protection 設定的裝置設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。

3. 輸入下列內容：

    - **平台**：選擇您的裝置平台。 選項包括：

        - **macOS**
        - **Windows 10 及以上版本**

    - **設定檔**：選取 [Endpoint Protection]  。

4. 選取 [建立]  。
5. 在 [基本資訊]  中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱是 **macOS：Endpoint Protection 設定檔，為所有 macOS 裝置設定防火牆**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]  。

7. 在 [組態設定]  中，您可進行的設定會根據您選擇的平台而不同。 選擇您平台來進行詳細設定：

   - [macOS 設定](endpoint-protection-macos.md)
   - [Windows 10 設定](endpoint-protection-windows-10.md)

8. 選取 [下一步]  。
9. 在 [範圍標籤]  (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]  。

10. 在 [指派]  中，選取將接收您設定檔的使用者或群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](../configuration/device-profile-assign.md)。

    選取 [下一步]  。

11. 在 [檢閱 + 建立]  中，檢閱您的設定。 當您選取 [建立]  時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>新增適用於 Windows 10 裝置的自訂防火牆規則

當在包含 Windows 10 Endpoint Protection 規則的設定檔中設定 Microsoft Defender 防火牆時，即可設定防火牆的自訂規則。 自訂規則可讓您擴充 Windows 10 支援的一組預先定義防火牆規則。

當您規劃使用自訂防火牆規則的設定檔時，請考量下列資訊，這可能會影響您在設定檔中選擇將防火牆規則分組的方式：

- 每個設定檔最多支援 150 個防火牆規則。 需使用超過 150 個規則時，請建立額外的設定檔，每個都限制為 150 個規則。

- 針對每個設定檔，若有任何一個規則無法套用，則該設定檔中的所有規則都會失敗，且不會將任何規則套用至裝置。

- 當某規則無法套用時，設定檔中的所有規則都會回報為失敗。 Intune 無法識別哪一個個別規則失敗。  

Intune 可以管理的防火牆規則詳述於 Windows [防火牆設定服務提供者](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP)。 若要檢閱 Intune 所支援 Windows 10 裝置的自訂防火牆設定清單，請參閱[自訂防火牆規則](endpoint-protection-windows-10.md#firewall-rules)。

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>將自訂防火牆規則新增至 Endpoint Protection 設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。

3. 針對「平台」  選取 [Windows10 及更新版本]  ，然後針對「設定檔」  選取 [Endpoint Protection]  。

    選取 [建立]  。

4. 輸入設定檔的**名稱** > [下一步]  。
5. 在 [組態設定]  中，選取 [Microsoft Defender 防火牆]  。 針對「防火牆規則」  ，請選取 [新增]  以開啟 [建立規則]  頁面。

6. 指定防火牆規則的設定，然後選取 [確定]  以儲存。 若要在文件中檢閱可用的自訂防火牆規則選項，請參閱[自訂防火牆規則](endpoint-protection-windows-10.md#firewall-rules)。

    1. 規則會顯示在規則清單的 [Microsoft Defender 防火牆]  頁面中。
    2. 若要修改規則，請從清單中選取規則以開啟 [編輯規則] 頁面  。
    3. 若要從設定檔刪除規則，請選取規則的省略符號 [...]  ，然後選取 [刪除]  。
    4. 若要變更規則顯示的順序，請選取規則清單頂端的「向上和向下箭號」  圖示。

7. 選取 [下一步]  直到看見 [檢閱 + 建立]  。 當選取 [建立]  時，系統會儲存變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

## <a name="next-steps"></a>後續步驟

雖然設定檔已建立，但它可能還不會執行任何動作。 接下來，[指派設定檔](../configuration/device-profile-assign.md)並[監視其狀態](../configuration/device-profile-monitor.md)。
