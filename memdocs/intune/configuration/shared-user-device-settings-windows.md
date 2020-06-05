---
title: Windows 10 共用裝置設定 - Microsoft Intune - Azure | Microsoft Docs
description: 在 Microsoft Intune 中新增和使用 Windows 10 來設定多位使用者共用或使用的裝置。 查看他們在裝置上進行的所有設定清單，包括 Microsoft Surface。 在裝置組態設定檔中控制來賓帳戶、管理帳戶和刪除非使用中的帳戶、允許或防止儲存至本機儲存體、設定電源和睡眠選項、選擇何時安裝更新，以及在教育環境中使用裝置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
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
ms.openlocfilehash: f013074ac67b7622b509d8b9781de3ab5f4041e0
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429497"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>使用 Intune 管理共用裝置的 Windows 10 及更新版本設定

Windows 10 及更新版本裝置 (例如 Microsoft Surface) 可供許多使用者使用。 擁有多位使用者的裝置稱為共用裝置，且是行動裝置管理 (MDM) 解決方案的一部分。

使用 Microsoft Intune，終端使用者可以透過來賓帳戶來登入這些共用裝置。 當他們使用裝置時，只能存取您允許的功能。 身為 Intune 系統管理員，您可以為共用的 Windows 10 裝置設定存取權、選擇何時刪除帳戶、控制電源管理設定，以及執行其他作業。

本文列出並描述您可以在 Windows 10 (及更新版本) 裝置組態設定檔中使用的設定。 在 Intune 中建立設定檔之後，您可以將設定檔部署或指派給您組織中的裝置群組。 您也可以將此設定檔指派給具有混合裝置類型和 OS 版本的裝置群組。

如需這項 Intune 功能的詳細資訊，請參閱[控制共用電腦或多重使用者裝置上的存取權、帳戶和電源功能](shared-user-device-settings.md)。 如需 Windows CSP 的詳細資訊，請參閱 [SharedPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp)。

## <a name="before-your-begin"></a>開始之前

[建立設定檔](shared-user-device-settings.md)。

## <a name="shared-multi-user-device-settings"></a>共用的多重使用者裝置設定

這些設定使用 [SharedPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp)。

- **共用電腦模式**：[啟用] 可開啟共用電腦模式。 在此模式中，一次只能有一位使用者登入裝置。 在第一位使用者登出之前，其他使用者無法登入。當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **來賓帳戶**：在登入畫面上選擇建立來賓選項。 來賓帳戶不需要任何使用者認證或驗證。 這項設定會在每次使用時建立新的本機帳戶。 選項包括：
  - **來賓**：在本機裝置上建立來賓帳戶。
  - **網域**：在 Azure Active Directory (AD) 中建立來賓帳戶。
  - **來賓和網域**：在本機裝置和 Azure Active Directory (AD) 中建立來賓帳戶。
- **帳戶管理**：選擇是否自動刪除帳戶。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **啟用**：系統會自動刪除來賓建立的帳戶，以及 AD 和 Azure AD 中的帳戶。 當使用者登出裝置或系統維護執行時，就會刪除這些帳戶。

    另請輸入：

    - **帳戶刪除**：選擇何時刪除帳戶：
      - **達到儲存體空間閾值時**
      - **達到儲存體空間閾值及非使用中的閾值時**
      - **登出後立刻刪除**

    另請輸入：

    - **開始刪除閾值 (%)** ：輸入磁碟空間百分比 (0-100)。 當總磁碟/儲存空間低於您輸入的值時，則會刪除快取的帳戶。 它會繼續刪除帳戶以回收磁碟空間。 非使用中時間最長的帳戶會最先遭到刪除。
    - **停止刪除閾值 (%)** ：輸入磁碟空間百分比 (0-100)。 當總磁碟/儲存空間達到您輸入的值時，則會停止刪除。
    - **非使用中帳戶閾值**：輸入連續幾天未登入即會刪除帳戶的天數 (0 到 60 天)。

  - **Disabled**：來賓建立的本機、AD 和 Azure AD 帳戶會保留在裝置上，不予刪除。

- **本機儲存體**：使用者可以使用本機存放區，儲存及檢視裝置硬碟上的檔案。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **啟用**：防止使用者在裝置的硬碟中儲存和檢視檔案。
  - **Disabled**：允許使用者利用檔案總管在本機查看和儲存檔案。

- **電源原則**：允許或防止使用者變更電源設定。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **啟用**：使用者無法關閉休眠功能、覆寫所有睡眠動作 (例如關閉筆記電腦螢幕)，亦無法變更電源設定。
  - **Disabled**：使用者可以讓裝置休眠、關閉筆記電腦螢幕讓裝置睡眠，亦可變更電源設定。

- **睡眠逾時 (秒)** ：輸入裝置進入睡眠模式前閒置的秒數 (0-18000)。 `0` 表示裝置永遠不會睡眠。 如果您未設定時間，裝置會在 3600 秒 (60 分鐘) 後進入睡眠狀態。

- **當電腦喚醒時登入**：選擇使用者是否必須在裝置離開睡眠模式後登入。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **啟用**：當裝置離開睡眠模式時，需要使用者使用密碼登入。
  - **Disabled**：使用者不需要輸入使用者名稱和密碼。

- **維護開始時間 (從午夜開始以分鐘計)** ：以分鐘 (0-1440) 為單位，輸入自動維護工作 (例如 Windows Update) 執行的時間。 預設開始時間是午夜或零 (`0`) 分鐘。 若要變更開始時間，請輸入從午夜開始以分鐘計的開始時間。 例如，如果您想要從上午 2 點開始進行維護，請輸入 `120`。 如果您想要從下午 8 點開始進行維護，請輸入 `1200`。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

- **教育原則**：選擇是否啟用教育環境的原則。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **啟用**：使用學校用裝置的建議設定，這些設定的限制較嚴格。
  - **Disabled**：不使用預設和建議的教育原則。

  如需教育原則功能的詳細資訊，請參閱 [Windows 10 configuration recommendations for education customers](https://docs.microsoft.com/education/windows/configure-windows-for-education) (適用於教育客戶的 Windows 10 設定建議)。

> [!TIP]
> [設定共用或來賓電腦](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (開啟其他 Docs 網站) 是關於此 Windows 10 功能的絕佳資源，它包括概念和可以在共用模式中設定的群組原則。

## <a name="next-steps"></a>後續步驟

- [指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
- 請參閱 [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) 的設定。
