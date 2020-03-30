---
title: Windows Phone 8.1 的 Microsoft Intune 電子郵件設定
titleSuffix: ''
description: 了解可用於設定執行 Windows Phone 8.1 之裝置上電子郵件連線的 Intune 設定。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 369e856b26ecbf8a7d6d7f8c0a87a9bfdf69e318
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086907"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>在執行 Windows Phone 8.1 之裝置上的 Microsoft Intune 電子郵件設定檔設定

本文展示您可為執行 Windows Phone 8.1 之裝置設定的電子郵件設定檔設定。

>[!IMPORTANT]
>Windows Phone 8.1 電子郵件設定檔也適用於Windows 10 裝置。

## <a name="before-you-begin"></a>開始之前

[建立 Windows Phone 8.1 電子郵件設定檔](email-settings-configure.md)。

## <a name="email-settings"></a>電子郵件設定

- **電子郵件伺服器**：輸入 Exchange Server 的主機名稱。 例如，輸入 `outlook.office365.com`。
- **帳戶名稱**：輸入電子郵件帳戶的顯示名稱。 此名稱會在其裝置上向使用者顯示。
- **AAD 中的使用者名稱屬性**：此名稱是 Intune 從 Azure Active Directory (AAD) 中取得的屬性。 Intune 會動態產生此設定檔所使用的使用者名稱。 選項包括：
  - **使用者主體名稱**：取得名稱，例如 `user1` 或 `user1@contoso.com`。
  - **主要 SMTP 位址**：取得電子郵件地址格式的名稱，例如 `user1@contoso.com`。
  - **sAM 帳戶名稱**：需要網域，例如 `domain\user1`。 另請輸入：
    - **使用者網域名稱來源**：選項包括：
      - **AAD** (Azure Active Directory)：輸入**取自 AAD 的使用者網域名稱屬性**。 選擇以取得使用者的 [完整網域名稱]  或 [NetBIOS 名稱]  屬性。
      - **自訂**：輸入**要使用的自訂網域名稱**。 輸入 Intune 用於網域名稱的值，例如 `contoso.com` 或 `contoso`。

- **AAD 中的電子郵件地址屬性**：Intune 會從 Azure Active Directory (AAD) 取得此屬性。 選擇使用者電子郵件地址的產生方式。 選項包括：
  - **使用者主體名稱**：使用完整主體名稱 (例如 `user1@contoso.com` 或 `user1`) 作為電子郵件地址。
  - **主要 SMTP 位址**：使用主要 SMTP 位址 (例如 `user1@contoso.com`) 來登入 Exchange。

## <a name="security-settings"></a>安全性設定

- **SSL**：[啟用]  會在傳送電子郵件、接收電子郵件以及與 Exchange 伺服器進行通訊時，使用安全通訊端層 (SSL) 通訊。 [停用]  不會要求使用 SSL。

## <a name="synchronization-settings"></a>同步處理設定

- **要同步處理的電子郵件數量**：選擇您要同步電子郵件的天數。 當設定為 [未設定]  (預設) 時，Intune 不會變更或更新此設定。 選取 [無限制]  來同步所有可用的電子郵件。
- **同步排程**：選取裝置用來同步處理 Exchange Server 資料的排程。 您也可以選取 [郵件送達時]  ，以便在資料抵達時立即進行同步。 或者，選取 [手動]  ，讓裝置使用者能夠開始同步。

## <a name="content-sync-settings"></a>內容同步設定

- **要同步處理的內容類型**：選取您想要與裝置同步的內容類型：
  - **連絡人**：[開啟]  會同步連絡人。 [關閉]  不會自動同步連絡人。 使用者可以手動同步。
  - **行事曆**：[開啟]  會同步行事曆。 [關閉]  不會自動同步連絡人。 使用者可以手動同步。
  - **工作**：[開啟]  會同步工作。 [關閉]  不會自動同步工作。 使用者可以手動同步。

## <a name="next-steps"></a>後續步驟

您也可以在 [Android](email-settings-android.md)、[Android Enterprise](email-settings-android-enterprise.md)、[iOS/iPadOS](email-settings-ios.md) 與 [Windows 10](email-settings-windows-10.md) 上設定電子郵件設定。

[在 Intune 中設定電子郵件設定](email-settings-configure.md)。
