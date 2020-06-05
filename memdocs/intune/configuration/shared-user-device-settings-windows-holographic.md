---
title: Windows Holographic Business 共用裝置設定 - Microsoft Intune - Azure | Microsoft Docs
description: 在 Microsoft Intune 中新增和使用 Windows Holographic for Business 來設定多位使用者共用或使用的裝置。 查看 [帳戶管理] 設定及他們在裝置上進行的所有設定清單，包括 Microsoft HoloLens。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49d1b8f407814fd368a7ff45bb94bc4c5ef7fd9d
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556280"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>使用 Intune 管理共用裝置的 Windows Holographic for Business 設定

Windows Holographic for Business 裝置 (例如 Microsoft HoloLens) 可供多位使用者使用。 擁有多位使用者的裝置稱為共用裝置，且是行動裝置管理 (MDM) 解決方案的一部分。

使用 Microsoft Intune，使用者可以透過來賓帳戶來登入這些共用裝置。 當他們使用裝置時，只能存取您允許的功能。

本文列出並描述您可以在 Windows Holographic for Business 裝置組態設定檔中使用的設定。 在 Intune 中建立設定檔之後，您可以接著將設定檔部署或指派給您組織中的裝置群組。 您也可以將此設定檔指派給具有混合裝置類型和 OS 版本的裝置群組。

如需這項 Intune 功能的詳細資訊，請參閱[控制共用電腦或多重使用者裝置上的存取權、帳戶和電源功能](shared-user-device-settings.md)。 如需 Windows CSP 的詳細資訊，請參閱 [AccountManagement CSP](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)。

## <a name="before-your-begin"></a>開始之前

[建立 Windows 10 共用的多重使用者裝置組態設定檔](shared-user-device-settings.md)。

當您建立 Windows 10 共用的使用者裝置組態設定檔時，設定會比本文所列的更多。 Windows Holographic for Business 裝置支援本文中的設定。

## <a name="shared-multi-user-device-settings"></a>共用的多重使用者裝置設定

> [!NOTE]
> 執行 Windows Holographic for Business 的裝置 (包括 Microsoft HoloLens) 只支援 [帳戶管理] 設定。 如果您設定 Intune 中所顯示的任何其他設定 (包括 [共用電腦模式])，則不會對這些裝置造成任何影響。

- **帳戶管理**：選擇是否自動刪除帳戶。 選項包括：
  - **未設定** (預設值)：自動刪除來賓建立的本機帳戶，以及 AD 和 Azure AD 中的帳戶。 當使用者登出裝置或系統維護執行時，就會刪除這些帳戶。

    另請輸入：

    - **帳戶刪除**：選擇何時刪除帳戶：
      - **達到儲存體空間閾值時**
      - **達到儲存體空間閾值及非使用中的閾值時**
      - **登出後立刻刪除**

    另請輸入：

    - **開始刪除閾值 (%)** ：輸入磁碟空間百分比 (0-100)。 當總磁碟/儲存空間低於您輸入的值時，則會刪除快取的帳戶。 它會繼續刪除帳戶以回收磁碟空間。 非使用中時間最長的帳戶會最先遭到刪除。
    - **停止刪除閾值 (%)** ：輸入磁碟空間百分比 (0-100)。 當總磁碟/儲存空間達到您輸入的值時，則會停止刪除。

  - **停用**：來賓建立的本機、AD 和 Azure AD 帳戶會保留在裝置上，不予刪除。

## <a name="next-steps"></a>後續步驟

- [指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
- 如需共用的使用者裝置設定，請參閱 [Windows 10 和更新版本](shared-user-device-settings-windows.md)。
