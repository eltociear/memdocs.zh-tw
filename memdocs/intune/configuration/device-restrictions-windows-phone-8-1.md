---
title: Windows Phone 8.1 的 Microsoft Intune 裝置限制設定
titleSuffix: ''
description: 了解執行 Windows Phone 8.1 的裝置上可用以控制裝置設定與功能的 Intune 設定。
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24fd2085839df35a486fcfa4cf817944b0d19944
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556246"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Microsoft Intune Windows Phone 8.1 裝置限制設定

本文將說明所有的 Microsoft Intune 裝置限制設定，讓您可以為執行 Windows Phone 8.1 的裝置進行設定。

## <a name="before-you-begin"></a>開始之前

[建立 Windows Phone 8.1 裝置的限制設定檔](device-restrictions-configure.md)。

## <a name="general"></a>一般

- **相機**：[封鎖] 會防止存取裝置相機。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  Intune 只管理裝置相機的存取權。 無權存取圖片或影片。

- **複製並貼上**：[封鎖] 會防止在裝置上的應用程式之間使用複製並貼上。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **抽取式存放裝置**：[封鎖] 會防止在裝置上使用外部存放裝置，例如 SD 記憶卡。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **地理位置**：[封鎖] 會防止在裝置上開啟位置服務。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **Microsoft 帳戶**：[封鎖] 會防止使用者建立 Microsoft 帳戶與裝置的關聯。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **螢幕擷取**：[封鎖] 會防止在裝置上取得螢幕擷取畫面。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **診斷資料提交**：[封鎖] 會禁止裝置將診斷與使用狀況遙測資料傳送給 Microsoft。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **自訂電子郵件帳戶同步**：[封鎖] 會防止裝置連線到非 Microsoft 電子郵件帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="password"></a>密碼

- **密碼**：[需要] 會強制使用者必須輸入密碼，才能存取裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 僅適用於本機帳戶。 網域帳戶密碼仍然由 Active Directory (AD) 和 Azure AD 設定。
  - **必要的密碼類型**：選擇密碼的類型。 選項包括：
    - **裝置預設**：密碼可以包含數字和字母。
    - **英數字元**：密碼必須混合數字和字母。
    - **數字**：密碼只能是數字。
  - **密碼長度下限**：輸入所需的字元數下限，從 4 到 16。 例如，輸入 `6` 表示密碼長度至少需要六個字元。
  - **簡單密碼**：[封鎖] 會防止使用者建立簡單密碼，例如 `1234` 或 `1111`。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **登入失敗幾次後即抹除裝置**：輸入抹除裝置前允許的密碼錯誤次數。
  - **停止活動最多幾分鐘後鎖定螢幕**：輸入裝置必須閒置多久，螢幕才會自動鎖定。 例如，輸入 `5` 會在閒置 5 分鐘後鎖定裝置。 當設定為 [未設定] 或保留空白時，Intune 不會變更或更新此設定。
  - **密碼到期 (天數)** ：輸入裝置密碼的有效期限，從 1 到 255 天。 例如，輸入 `90`，密碼會在 90 天後到期。 當此值為空白時，Intune 則不會變更或更新此設定。
  - **避免重複使用以前用過的密碼**：輸入不得重複使用的舊密碼，從 1 到 24。 列如，輸入 `5` 讓使用者無法將新密碼設定為其目前密碼或之前使用過的四個密碼之一。 當此值為空白時，Intune 不會變更或更新此設定。
- **加密**：[需要] 會要求裝置必須加密，包括檔案。 並非所有裝置都支援加密。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 若要設定此設定並正確報告合規性，也請設定：
  - **需要密碼**：設定為 [需要]。
  - **必要的密碼類型**：至少設定為 [數值]。
  - **密碼長度下限**：至少設定為 `4`。

## <a name="app-store"></a>App Store

- **App Store**：[封鎖] 會防止使用者存取 App Store。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="restricted-apps"></a>受限應用程式

您可以在受限制應用程式清單中，設定下列清單之一︰

- **封鎖的應用程式**：列出不允許使用者安裝和執行的應用程式 (不由 Intune 管理)。
- **允許的應用程式**：列出允許使用者安裝的應用程式。 自動允許 Intune 所管理的應用程式。

若要設定清單，請按一下 [新增]，然後在應用程式市集中，指定您所選的名稱 (也可指定選用的應用程式發行者) 以及應用程式的 URL。

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>如何在市集中指定應用程式的 URL

若要在允許和封鎖的應用程式清單中指定應用程式 URL，請使用下列格式：

從 [[Windows Phone 市集]](https://www.microsoft.com/store/apps/windows-phone) 頁面中，搜尋您想要使用的應用程式。

開啟應用程式的頁面，然後將 URL 複製到剪貼簿。 您現在可以使用這個 URL 作為允許或封鎖應用程式清單中的 URL。

範例：在市集中搜尋 Skype 應用程式。 您使用的 URL 是 `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`。

### <a name="additional-options"></a>其他選項

您也可以按一下 [匯入] 填入格式如一下的 csv 檔案清單：<*應用程式 URL*>，<*應用程式名稱*>，<*應用程式發行者*>，或按一下 [匯出]，建立 csv 檔案，其中包含格式相同的受限應用程式清單內容。

## <a name="browser"></a>瀏覽器

- **網頁瀏覽器**：[封鎖] 會關閉裝置上的內建網頁瀏覽器。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="cellular-and-connectivity"></a>行動數據與連線

- **Wi-Fi**：[封鎖] 會停用裝置上的 Wi-Fi 功能。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **Wi-Fi 網際網路共用功能**：[封鎖] 會防止在裝置上使用 Wi-Fi 網際網路共用功能。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **自動連線至 Wi-Fi 熱點**：可讓裝置自動連線到免費 Wi-Fi 熱點並自動接受任何使用條款。
- **Wi-Fi 熱點報告**：[封鎖] 會防止裝置傳送 Wi-Fi 熱點連線資訊。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **NFC**：[封鎖] 會在支援近距離無線通訊 (NFC) 的裝置上停用使用此作業。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **藍牙**：[封鎖] 防止使用者啟用藍牙。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="next-steps"></a>後續步驟

如需裝置限制設定檔的一般概觀，請參閱[在 Microsoft Intune 中設定裝置限制設定](device-restrictions-configure.md)。
