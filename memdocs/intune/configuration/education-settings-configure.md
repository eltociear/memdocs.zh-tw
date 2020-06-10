---
title: 在 Microsoft Intune 中新增或設定教育設定 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中，於 Windows 10 和更新版本之裝置上的裝置組態設定檔中使用 [進行測驗] 應用程式。 使用 [教育] 設定建立組態設定檔，然後輸入測驗應用程式 URL、選擇使用者登入方式、在測驗期間監視畫面，以及在測驗期間允許或防止文字建議。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52eae65e6735ad655c2e8db53e34383ccc5e3b30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988397"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>在 Microsoft Intune 中，於 Windows 10 裝置上使用 [進行測驗] 應用程式

Intune 中的教育設定檔是專為學生在裝置上進行測驗或考試而設計的。 此功能包括 [進行測驗] 應用程式，以及新增測驗 URL，選擇使用者登入測驗之方式的設定等。 此功能支援下列平台：

- Windows 10 及更新版本

當使用者登入時，[進行測驗] 應用程式會自動開啟您所輸入的測驗。 在測驗過程中，裝置上無法執行任何其他應用程式。 [在 Windows 10 中進行測驗](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) \(部分機器翻譯\) 提供了有關 [進行測驗] 應用程式的更多詳細資料。

本文列出在 Microsoft Intune 中建立裝置組態設定檔的步驟。 它還包括用於閱讀和了解 Windows 10 裝置可用的教育設定的資訊。

## <a name="create-a-device-profile"></a>建立裝置設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選取 [Windows 10 及更新版本]。
    - **設定檔**：選取 [安全性評定 (教育)]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：為新的設定檔輸入描述性名稱。
    - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。
7. 在 [組態設定] 中，輸入您要設定的設定：

    - [Windows 10 及以上版本](education-settings-windows.md)

8. 選取 [下一步]。

9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或使用者群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

當每個裝置下次簽入時，就會套用原則。

## <a name="next-steps"></a>後續步驟

查看 [Windows 10 教育設定](education-settings-windows.md)的清單及其描述。

[指派設定檔](device-profile-assign.md)後，[監視其狀態](device-profile-monitor.md)。
