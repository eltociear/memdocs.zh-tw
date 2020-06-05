---
title: Microsoft Intune 中的共用或多重使用者裝置設定 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中新增和使用多位使用者共用或使用的 Windows 10 和 Windows Holographic for Business 裝置。 查看他們在裝置上進行的所有設定清單，包括 Microsoft HoloLens。 在裝置組態設定檔中控制來賓帳戶、管理帳戶和刪除非使用中的帳戶、允許或防止儲存至本機儲存體、設定電源和睡眠選項、選擇何時安裝更新，以及在教育環境中使用裝置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984003"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>使用 Intune 控制共用電腦或多重使用者裝置上的存取權、帳戶和電源功能

擁有多位使用者的裝置稱為共用裝置，且是行動裝置管理 (MDM) 解決方案常見的一部分。 使用 Microsoft Intune，您可以自訂執行下列平台的共用裝置：

- Windows 10 專業版和更新版本
- Windows 10 企業版和更新版本
- Windows Holographic for Business，例如 HoloLens

例如，學校擁有許多學生通常會使用的裝置。 使用此設定時，學校的 Intune 系統管理員可以開啟 [共用的電腦] 功能，一次只允許一位使用者。 學生無法在裝置上切換不同的登入帳戶。 當學生登出時，您也選擇移除所有使用者特定的設定。

終端使用者可以透過來賓帳戶來登入這些共用裝置。 使用者登入之後，就會快取認證。 當終端使用者使用裝置時，只能存取您允許的功能。 例如，您可以選擇裝置何時進入睡眠模式、使用者能否在本機查看和儲存檔案、啟用或停用電源管理設定，以及執行其他作業。 您也可以控制是否在使用者登出時刪除來賓帳戶，或在達到閾值時刪除非使用中的帳戶。

本文示範如何建立組態設定檔，並包含可用設定及其描述的連結。

在 Intune 中建立設定檔之後，您可以將設定檔部署或指派給您組織中的裝置群組。 您也可以將此設定檔指派給具有混合裝置類型和作業系統 (OS) 版本的裝置群組。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

   - **平台**：選取 [Windows 10 及更新版本]。
   - **設定檔**：選取 [共用的多重使用者裝置]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

   - **名稱**：為新的設定檔輸入描述性名稱。
   - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。
7. 在 [組態設定] 中，您可進行的設定會根據您選擇的平台而不同。 選擇您平台來進行詳細設定：

    - [Windows 10 及以上版本](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. 選取 [下一步]。

9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取接收設定檔的裝置群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

    > [!NOTE]
    > 請務必將此設定檔指派到您組織中的裝置群組。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

當每個裝置下次簽入時，就會套用原則。

## <a name="next-steps"></a>後續步驟

- 請參閱 [Windows 10 和更新版本](shared-user-device-settings-windows.md)以及 [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) 的所有設定。
- [指派設定檔](device-profile-assign.md)後，[監視其狀態](device-profile-monitor.md)。
