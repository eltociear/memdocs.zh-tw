---
title: Microsoft Intune 中的 iOS/iPadOS 裝置功能設定 - Azure | Microsoft Docs
description: 查看 Microsoft Intune 中，設定 iOS 與 iPadOS 裝置的 AirPrint、主畫面配置、應用程式通知、共用裝置、單一登入與網路內容篩選器設定的所有設定。 在裝置組態設定檔中使用這些設定，以設定 iOS/iPadOS 裝置來在貴組織中使用這些 Apple 功能。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 351c6ade59d98ce620b939c5ff6238e650390a5f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361077"
---
# <a name="ios-and-ipados-device-settings-to-use-common-iosipados-features-in-intune"></a>要在 Intune 中使用常見 iOS/iPadOS 功能用的 iOS 與 iPadOS 裝置設定

Intune 包含一些內建設定，可讓 iOS/iPadOS 使用者在其裝置上使用不同的 Apple 功能。 例如，系統管理員可以控制 iOS/iPadOS 使用者如何使用 AirPrint 印表機、將應用程式與資料夾新增至 Dock 與主畫面上的頁面、顯示應用程式通知、在鎖定畫面上顯示資產標籤詳細資料、使用單一登入驗證，以及使用憑證來對使用者進行驗證。

使用這些功能來控制 iOS/iPadOS 裝置，作為行動裝置管理 (MDM) 解決方案的一部分。

本文會列出這些設定，並說明每個設定的用途。 如需這些功能的詳細資訊，請移至[新增 iOS/iPadOS 或 macOS 裝置功能設定](device-features-configure.md)。

## <a name="before-you-begin"></a>開始之前

[建立 iOS/iPadOS 裝置組態設定檔](device-features-configure.md)。

> [!NOTE]
> 這些設定適用於不同的註冊類型，而其中有部分設定適用於所有註冊選項。 如需不同註冊類型的詳細資訊，請參閱 [iOS/iPadOS 註冊](../enrollment/ios-enroll.md)。

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>設定適用於：所有註冊類型

> [!NOTE]
> 請務必將所有印表機新增到相同的設定檔。 Apple 會防止多個 AirPrint 設定檔以相同裝置為目標。

- **IP 位址**：輸入印表機的 IPv4 或 IPv6 位址。 如果您是使用主機名稱來識別印表機，則可以透過在終端機偵測該印表機來取得 IP 位址。 本文中的取得 IP 位址和路徑會提供更多詳細資料。
- **路徑**：您網路上印表機的路徑通常是 `ipp/print`。 本文中的取得 IP 位址和路徑會提供更多詳細資料。
- **連接埠**：輸入 AirPrint 目的地的接聽連接埠。 如果將此屬性留白，AirPrint 就會使用預設連接埠。 可以在 iOS 11.0+ 與 iPadOS 13.0+ 上使用。
- **TLS**：選擇 [啟用]  以保護 AirPrint 與傳輸層安全性 (TLS) 的連線。 可以在 iOS 11.0+ 與 iPadOS 13.0+ 上使用。

若要新增 AirPrint 伺服器，您可以：

- [新增]  可新增 AirPrint 伺服器至清單中。 可以新增許多 AirPrint 伺服器。
- **匯入**含有此資訊的逗點分隔檔 (.csv)。 或者，[匯出]  以建立您所新增之 AirPrint 伺服器的清單。

### <a name="get-server-ip-address-resource-path-and-port"></a>取得伺服器 IP 位址、資源路徑與連接埠

若要新增 AirPrinter 伺服器，您需要印表機的 IP 位址、資源路徑及連接埠。 下列步驟說明如何取得此資訊。

1. 在連線到與 AirPrint 印表機相同區域網路 (子網路) 的 Mac 上，開啟 [終端機]  (從 **/Applications/Utilities**)。
2. 在 [終端機] 中，輸入 `ippfind`，然後選取 Enter 鍵。

    請記下印表機資訊。 例如，可能會傳回類似 `ipp://myprinter.local.:631/ipp/port1` 的內容。 第一個部分是印表機的名稱。 最後一個部分 (`ipp/port1`) 是資源路徑。

3. 在 [終端機] 中，輸入 `ping myprinter.local`，然後選取 Enter 鍵。

   記下 IP 位址。 例如，可能會傳回類似 `PING myprinter.local (10.50.25.21)` 的內容。

4. 使用 IP 位址和資源路徑值。 在此範例中，IP 位址是 `10.50.25.21`，而資源路徑則是 `/ipp/port1`。

## <a name="home-screen-layout"></a>主畫面配置

本功能適用於：

- iOS 9.3 或更新版本
- iPadOS 13.0 和更新版本

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>設定適用於：自動裝置註冊 (受監督)

### <a name="dock"></a>Dock

使用 [Dock]  設定將最多六個項目或資料夾新增到 iOS/iPadOS 畫面的 Dock。 許多裝置支援的項目數較少。 例如，iPhone 裝置最多支援 4 個項目。 在此情況下，裝置上只會顯示您新增的前四個項目。

您最多可以為裝置 Dock 新增**六個**項目 (應用程式和資料夾合併)。

- **新增**：新增應用程式或資料夾到裝置上的 Dock。
- **類型**：新增 [應用程式]  或 [資料夾]  ：

  - **應用程式**：選擇此選項以將應用程式新增至畫面上的 Dock。 輸入：

    - **應用程式名稱**：輸入應用程式的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 而「不會」  顯示在 iOS/iPadOS 裝置上。
    - **應用程式套件組合識別碼**：輸入應用程式的套件組合識別碼。 請參閱[內建 iOS/iPadOS 應用程式的套件組合識別碼](bundle-ids-built-in-ios-apps.md)，以取得一些範例。

  - **資料夾**：選擇此選項以將資料夾新增至畫面上的 Dock。

    新增到資料夾中頁面的應用程式會以和清單相同的順序，由左至右排列。 如果您新增的應用程式超過一個頁面所能容納的數目，應用程式就會被移到另一個頁面。

    - **資料夾名稱**：資料夾的名稱。 這是在使用者裝置上對使用者顯示的名稱。
    - **頁面清單**：**新增**頁面，然後輸入下列屬性：

      - **頁面名稱**：輸入頁面的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 而「不會」  顯示在 iOS/iPadOS 裝置上。
      - **應用程式名稱**：輸入應用程式的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 而「不會」  顯示在 iOS/iPadOS 裝置上。
      - **應用程式套件組合識別碼**：輸入應用程式的套件組合識別碼。 請參閱[內建 iOS/iPadOS 應用程式的套件組合識別碼](bundle-ids-built-in-ios-apps.md)，以取得一些範例。

      您最多可以為裝置 Dock 新增 **20** 個頁面。

> [!NOTE]
> 當使用 [固定] 設定新增圖示時，在主畫面與頁面上的圖示會鎖定，且無法移動。 這可能是由 iOS/iPadOS 與 Apple 的 MDM 原則所設計。

#### <a name="example"></a>範例

在以下範例中，Dock 畫面只會顯示 [Safari]、[郵件] 和 [股市] 應用程式。 其中已選取 [郵件] 應用程式來顯示其屬性：

![範例 iOS/iPadOS Dock 設定](./media/ios-device-features-settings/FfFiUcP.png)

當您將該原則指派給 iPhone 時，Dock 看起來會如下圖所示：

![iPhone 上的 iOS/iPadOS Dock 配置範例](./media/ios-device-features-settings/bAgCe8F.png)

### <a name="pages"></a>Pages

新增您想要在主畫面上顯示的頁面，以及要在每個頁面顯示的應用程式。 新增到頁面的應用程式會以和清單相同的順序，由左至右排列。 如果您新增的應用程式超過一個頁面所能容納的數目，應用程式就會被移到另一個頁面。

> [!TIP]
> 若要將任何主畫面或頁面清單中的項目重新排序，您可以拖放那些項目。

您最多可以在裝置上新增 **40** 個頁面。

- **頁面清單**：**新增**頁面，然後輸入下列屬性：

  - **頁面名稱**：輸入頁面的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考，而「不會」  顯示在 iOS/iPadOS 裝置上。

  您最多可以在裝置上新增 **60** 個項目 (應用程式和資料夾合併)。

  - **新增**：新增應用程式或資料夾到裝置上的頁面。

    - **類型**：新增 [應用程式]  或 [資料夾]  ：

      - **應用程式**：選擇此選項以將應用程式新增至畫面上的頁面。 另請輸入：

        - **應用程式名稱**：輸入應用程式的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 而「不會」  顯示在 iOS/iPadOS 裝置上。
        - **應用程式套件組合識別碼**：輸入應用程式的套件組合識別碼。 請參閱[內建 iOS/iPadOS 應用程式的套件組合識別碼](bundle-ids-built-in-ios-apps.md)，以取得一些範例。

      - **資料夾**：選擇此選項以將資料夾新增至畫面上的 Dock。

        新增到資料夾中頁面的應用程式會以和清單相同的順序，由左至右排列。 如果您新增的應用程式超過一個頁面所能容納的數目，應用程式就會被移到另一個頁面。

        - **資料夾名稱**：輸入資料夾的名稱。 這是在裝置上對使用者顯示的名稱。
        - **新增**：將頁面新增到資料夾。 一併輸入下列屬性：

          - **頁面名稱**：輸入頁面的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 而「不會」  顯示在 iOS/iPadOS 裝置上。
          - **應用程式名稱**：輸入應用程式的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 而「不會」  顯示在 iOS/iPadOS 裝置上。
          - **應用程式套件組合識別碼**：輸入應用程式的套件組合識別碼。 請參閱[內建 iOS/iPadOS 應用程式的套件組合識別碼](bundle-ids-built-in-ios-apps.md)，以取得一些範例。

#### <a name="example"></a>範例

在以下範例中，將會新增名為 **Contoso** 的新頁面。 此頁面會顯示 [尋找朋友] 和 [設定] 應用程式。 其中已選取 [設定] 應用程式來顯示其屬性：

![Intune 中的 iOS/iPadOS 主畫面設定範例](./media/ios-device-features-settings/Jc2OxyX.png)

當您將該原則指派給 iPhone 時，頁面看起來會如下圖所示：

![Intune 中已修改主畫面的 iOS/iPadOS 裝置](./media/ios-device-features-settings/Bd37PHa.png)

## <a name="app-notifications"></a>應用程式通知

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>設定適用於：自動裝置註冊 (受監督)

- **新增**：為應用程式新增通知：

    ![在 Intune 中的 iOS/iPadOS 設定檔中新增應用程式通知](./media/ios-device-features-settings/ios-macos-app-notifications.png)

  - **應用程式套件組合識別碼**：輸入您要新增之應用程式的 [應用程式套件組合識別碼]  。 請參閱[內建 iOS/iPadOS 應用程式的套件組合識別碼](bundle-ids-built-in-ios-apps.md)，以取得一些範例。
  - **應用程式名稱**：輸入您要新增之應用程式的名稱。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 它「不會」  顯示在裝置上。
  - **發行者**：輸入您要新增之應用程式的發行者。 此名稱用於供您在 Microsoft 端點管理員系統管理中心中參考， 它「不會」  顯示在裝置上。
  - **通知**：[啟用]  或 [停用]  應用程式對裝置傳送通知的功能。
    - **在通知中心顯示**：[啟用]  會允許應用程式在裝置的「通知中心」內顯示通知。 [停用]  會防止應用程式在裝置的「通知中心」內顯示通知。
    - **在鎖定畫面顯示**：選取 [啟用]  以在裝置鎖定畫面上查看來自應用程式的通知。 [停用]  會防止應用程式在鎖定畫面上顯示通知。
    - **警示類型**：當裝置解除鎖定時，請選擇通知的顯示方式。 選項包括：
      - **無**：不顯示任何通知。
      - **橫幅**：短暫顯示含有通知的橫幅。
      - **強制回應**：裝置會顯示通知，而使用者必須手動關閉通知，才能繼續使用裝置。
    - **應用程式圖示上的徽章**：選取 [啟用]  以將徽章新增至應用程式圖示。 徽章意謂著應用程式已傳送通知。
    - **音效**：選取 [啟用]  以在傳遞通知時播放音效。

## <a name="lock-screen-message"></a>鎖定畫面訊息

本功能適用於：

- iOS 9.3 和更新版本
- iPadOS 13.0 和更新版本

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>設定適用於：自動裝置註冊 (受監督)

- **資產標籤資訊**：輸入裝置資產標籤的相關資訊。 例如，輸入 `Owned by Contoso Corp` 或 `Serial Number: {{serialnumber}}`。

  您輸入的文字會顯示在裝置的登入視窗與鎖定畫面上。

- **鎖定畫面註腳**：輸入當裝置遺失或遭竊時，可能有助於取回裝置的備註。 您可以輸入任何所需的文字。 例如，輸入類似 `If found, call Contoso at ...` 的內容。

  裝置權杖也可用來在這些欄位中新增裝置特定資訊。 例如，若要顯示序號，請輸入 `Serial Number: {{serialnumber}}`。 在鎖定畫面上，此文字顯示類似於 `Serial Number 123456789ABC`。 輸入變數時，請務必使用大括弧 `{{ }}`。 [應用程式設定權杖](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list)包含可以使用的變數清單。 您也可以使用 `deviceName` 或任何其他的裝置特定值。

  > [!NOTE]
  > 變數不會在 UI 中驗證，而且會區分大小寫。 因此，您可能會看到儲存之設定檔含有不正確的輸入。 例如，如果輸入 `{{DeviceID}}` 而非 `{{deviceid}}`，則會顯示常值字串而非裝置的唯一識別碼。 請務必輸入正確的資訊。

## <a name="single-sign-on"></a>單一登入

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>設定適用於：裝置註冊、自動裝置註冊 (受監督)

- **AAD 中的使用者名稱屬性**：Intune 會針對 Azure AD 中的每個使用者尋找這個屬性。 Intune 接著會先填入個別欄位 (例如 UPN)，然後才產生會安裝在裝置上的 XML。 選項包括：

  - **使用者主體名稱**：系統會以下列方式剖析 UPN：

    ![Intune 中的 iOS/iPadOS 使用者名稱 SSO 屬性](./media/ios-device-features-settings/User-name-attribute.png)

    您也可以使用在 [領域]  文字方塊中輸入的文字覆寫領域。

    例如，Contoso 有數個區域，包括歐洲、亞洲及北美洲。 Contoso 想要讓其亞洲使用者使用 SSO，而應用程式將會要求 `username@asia.contoso.com` 格式的 UPN。 當您選取 [使用者主體名稱]  時，系統會從 Azure AD 取得每個使用者的領域，亦即 `contoso.com`。 因此，針對在亞洲的使用者，請選取 [使用者主體名稱]  ，然後輸入 `asia.contoso.com`。 使用者的 UPN 會變成 `username@asia.contoso.com`，而不是 `username@contoso.com`。

  - **Intune 裝置識別碼**：Intune 會自動選取 Intune 裝置識別碼。

    根據預設，應用程式只需要使用裝置識別碼。 但如果您的應用程式會使用領域和裝置識別碼，您可以在 [領域] 文字方塊中輸入領域。

    > [!NOTE]
    > 如果使用裝置識別碼，則領域預設為留白。

  - **Azure AD 裝置識別碼**

- **領域**：輸入 URL 的網域部分。 例如，輸入 `contoso.com`。
- **將會使用單一登入的 URL 首碼**：[新增]  貴組織中需要使用者單一登入驗證的任何 URL。

  例如，當使用者連線到這些網站的任一個時，iOS/iPadOS 裝置會使用單一登入認證。 使用者不需要輸入任何其他認證。 如果已啟用多重要素驗證，使用者就必須輸入第二道驗證。

  > [!NOTE]
  > 這些 URL 必須是格式正確的 FQDN。 Apple 要求這些必須採用 `http://<yourURL.domain>` 格式。

  URL 的比對模式開頭必須是 `http://` 或 `https://`。 系統會執行簡單的字串比對，因此 `http://www.contoso.com/` URL 首碼不會與 `http://www.contoso.com:80/` 相符。 使用 iOS 10.0+ 與 iPadOS 13.0+ 或更新版本時，可以使用單一萬用字元 \* 來輸入所有符合的值。 例如，`http://*.contoso.com/` 同時會符合 `http://store.contoso.com/` 和 `http://www.contoso.com`。

  `http://.com` 和 `https://.com` 模式分別會符合所有 HTTP 和 HTTPS URL。

- **將使用單一登入的應用程式**：[新增]  使用者裝置上可使用單一登入的應用程式。

  `AppIdentifierMatches` 陣列必須包含符合應用程式套件組合識別碼的字串。 這些字串可以是完全相符的項目 (例如 `com.contoso.myapp`)，或是您也可以使用 \* 萬用字元來輸入套件組合識別碼的首碼相符項目。 此萬用字元必須出現在字串結尾處的句號字元 (.) 之後，且只能出現一次 (例如 `com.contoso.*`)。 包含萬用字元時，套件組合識別碼開頭為首碼的任何應用程式都會被授與帳戶存取權。

  使用 [應用程式名稱]  輸入使用者易記的名稱來協助您識別套件組合識別碼。

- **認證更新憑證**：如果使用憑證 (而不是密碼) 來進行驗證，請選取現有的 SCEP 或 PFX 憑證作為驗證憑證。 一般而言，此憑證會與部署至使用者以用於其他設定檔 (例如 VPN、Wi-Fi 或電子郵件) 的憑證相同。

## <a name="web-content-filter"></a>Web 內容篩選

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>設定適用於：自動裝置註冊 (受監督)

- **篩選類型**：選擇以允許特定網站。 選項包括：

  - **設定 URL**：使用 Apple 的內建網路篩選器，以尋找成人詞彙，包含不雅及成人內容語言。 此功能會在每個網頁載入時對它進行評估，然後識別並封鎖不合適的內容。 您也可以新增不想要讓篩選器檢查的 URL。 或是封鎖特定 URL，不論 Apple 的篩選器設定為何。

    - **允許的 URL**：[新增]  您想要允許的 URL。 這些 URL 會略過 Apple 的網路篩選器。

        > [!NOTE]
        > 您輸入的 URL 是您不想要讓 Apple 網路篩選器評估的 URL。 這些 URL 不是允許網站的清單。 若要建立允許網站的清單，請將 [篩選器類型]  設定為 [僅限特定網站]  。

    - **封鎖的 URL**：[新增]  您想要防止開啟的 URL，不論 Apple 網路篩選器設定為何。

  - **僅限特定網站** (僅適用於 Safari 網頁瀏覽器)：這些 URL 會被新增至 Safari 瀏覽器的書籤。 使用者**只能**瀏覽這些網站；他們無法開啟任何其他網站。 只有在您知道使用者可以存取的確切 URL 清單時，才使用此選項。

    - **URL**：輸入您要允許的網站 URL。 例如，輸入 `https://www.contoso.com`。
    - **書籤路徑**：Apple 已變更此設定。 所有書籤都會進入 [允許的網站]  資料夾。 書籤不會進入您輸入的書籤路徑。
    - **標題**：輸入書籤的描述性標題。

    如果您未輸入任何 URL，則使用者除了 `microsoft.com`、`microsoft.net` 及 `apple.com` 之外，將無法存取任何網站。 這些 URL 是 Intune 自動允許的 URL。

## <a name="single-sign-on-app-extension"></a>單一登入應用程式擴充功能

本功能適用於：

- iOS 13.0 與更新版本
- iPadOS 13.0 和更新版本

### <a name="settings-apply-to-all-enrollment-types"></a>設定適用於：所有註冊類型

- **SSO 應用程式延伸模組類型**：選擇 SSO 應用程式延伸模組的類型。 選項包括：

  - **未設定**：不使用應用程式延伸模組。 若要停用應用程式延伸模組，您可以將 SSO 應用程式延伸模組類型切換為 [未設定]  。
  - **重新導向**：使用一般且可自訂的重新導向應用程式延伸模組，搭配新式驗證流程執行 SSO。 請確定您知道組織應用程式延伸模組的延伸模組識別碼。
  - **認證**：使用一般且可自訂的認證應用程式延伸模組，搭配查問與回應驗證流程執行 SSO。 請確定您知道組織應用程式延伸模組的延伸模組識別碼。
  - **Kerberos**：使用 Apple 的內建 Kerberos 延伸模組，其包含在 iOS 13.0+ 與 iPadOS 13.0+ 中。 此選項為 [認證]  應用程式延伸模組的 Kerberos 特定版本。

  > [!TIP]
  > 使用 [重新導向]  與 [認證]  類型時，您會新增自己的設定值來透過延伸模組傳遞。 如果您使用的是**認證**，請考慮使用 Apple 在 **Kerberos** 類型中提供的內建組態設定。

- **延伸模組識別碼** (重新導向與認證)：輸入能識別 SSO 應用程式延伸模組的套件組合識別碼，例如 `com.apple.extensiblesso`。

- **小組識別碼** (重新導向與認證)：輸入 SSO 應用程式延伸模組的小組識別碼。 小組識別碼是由 Apple 產生之 10 個字元的英數 (數字與字母) 字串，例如 `ABCDE12345`。 小組識別碼不是必要的。

  [尋找小組識別碼](https://help.apple.com/developer-account/#/dev55c3c710c) (會開啟 Apple 的網站) 會提供詳細資訊。

- **領域** (認證與 Kerberos)：輸入驗證領域的名稱。 領域名稱應為大寫，例如 `CONTOSO.COM`。 您的領域名稱通常會與您的 DNS 網域名稱相同，但全部都是大寫。

- **網域** (認證與 Kerberos)：輸入可以透過 SSO 驗證的網站網域或主機名稱。 例如，如果您的網站是 `mysite.contoso.com`，則 `mysite` 是主機名稱，而 `contoso.com` 則是網域名稱。 當使用者連線到上述其中一個網站時，應用程式延伸模組會處理驗證挑戰。 此驗證可讓使用者使用 Face ID、Touch ID 或 Apple PIN 碼/密碼來登入。

  - 您單一登入應用程式延伸模組 Intune 設定檔中的所有網域都不能重複。 您不能在任何單一登入應用程式延伸模組設定檔中重複使用網域，即使您是使用不同類型的 SSO 應用程式延伸模組也一樣。
  - 這些網域不會區分大小寫。

- **URL** (僅限重新導向)：輸入重新導向應用程式延伸模組會代為執行 SSO 的識別提供者其 URL 前置詞。 當系統將使用者重新導向到這些 URL 時，SSO 應用程式延伸模組將會介入並提示進行 SSO。

  - 您的 Intune 單一登入應用程式延伸模組設定檔中的所有 URL 都不能重複。 您不能在任何 SSO 應用程式延伸模組設定檔中重複使用網域，即使您是使用不同類型的 SSO 應用程式延伸模組也一樣。
  - URL 的開頭必須是 http:// 或 https://。

- **其他設定** (重新導向與認證)：輸入要傳遞到 SSO 應用程式延伸模組的其他延伸模組專用資料：
  - **索引鍵**：輸入所要新增項目的名稱，例如 `user name`。
  - **類型**：輸入資料的類型。 選項包括：

    - 字串
    - 布林值：在 [設定值]  中，輸入 `True` 或 `False`。
    - 整數：在 [設定值]  中，輸入數字。
    
  - **值**：輸入資料。

  - **新增**：選取以新增設定金鑰。

- **鑰匙串使用方式** (僅限 Kerberos)：選擇 [封鎖]  來防止將密碼儲存並保存在鑰匙串中。 如果選擇封鎖，則系統不會提示使用者儲存密碼，且需要在 Kerberos 票證到期時重新輸入密碼。 [未設定]  \(預設\) 允許將密碼儲存並保存在鑰匙串中。 當票證到期時，系統不會提示使用者重新輸入密碼。
- **Face ID、Touch ID 或密碼** (僅限 Kerberos)：[必要]  ，強制使用者在需要認證以更新 Kerberos 票證時，輸入 Face ID、Touch ID 或裝置密碼。 [未設定]  (預設)，不會要求使用者使用生物特徵辨識技術或密碼來更新 Kerberos 票證。 如果封鎖 [鑰匙串使用方式]  ，則不會套用此設定。
- **預設領域** (僅限 Kerberos)：選擇 [啟用]  以將所輸入的 [領域]  值設定為預設領域。 [未設定]  \(預設\) 不會設定預設領域。

  > [!TIP]
  > - 如果您要在組織中設定多個 Kerberos SSO 應用程式延伸模組，就必須 [啟用]  此設定。
  > - 如果您會使用多個領域，請 [啟用]  此設定。 其會將您輸入的 [領域]  值設定為預設領域。
  > - 如果您只有單一領域，請將其保留為 [未設定]  \(預設\)。

- **主體名稱** (僅限 Kerberos)：輸入 Kerberos 主體的使用者名稱。 您不需要包含領域名稱。 例如，在 `user@contoso.com` 中，`user` 是主體名稱，而 `contoso.com` 則是領域名稱。

  > [!TIP]
  > - 您也可以在主體名稱中使用變數，方法是輸入大括弧 `{{ }}`。 例如，若要顯示使用者名稱，請輸入 `Username: {{username}}`。 
  > - 不過，請小心使用變數替代，因為變數不會在 UI 中驗證，而且會區分大小寫。 請務必輸入正確的資訊。

- **Active Directory 網站代碼** (僅限 Kerberos)：輸入 Kerberos 延伸模組應使用的 Active Directory 網站名稱。 您可能不需要變更此值，因為 Kerberos 延伸模組可能會自動尋找 Active Directory 站台碼。
- **快取名稱** (僅限 Kerberos)：輸入 Kerberos 快取的一般安全性服務 (GSS) 名稱。 您通常不會需要設定此值。
- **應用程式套件組合識別碼** (僅限 Kerberos)：[新增]  應在裝置上使用單一登入的應用程式套件組合識別碼。 系統會將 Kerberos 票證授權票證 (驗證票證) 的存取權授與這些應用程式，使應用程式能夠將使用者驗證至其具有存取權的服務。
- **網域領域對應** (僅限 Kerberos)：[新增]  應對應至領域的網域 DNS 尾碼。 在主機 DNS 名稱不符合領域名稱的情況下使用此設定。 您通常不會需要建立此自訂網域對領域對應。
- **PKINIT 憑證** (僅限 Kerberos)：[選取]  可用於 Kerberos 驗證的初始驗證公開金鑰加密 (PKINIT) 憑證。 您可以從自己已在 Intune 中新增的 [PKCS](../protect/certficates-pfx-configure.md) 或 [SCEP](../protect/certificates-scep-configure.md) 憑證中選擇。 如需憑證的詳細資訊，請參閱[在 Microsoft Intune 中使用憑證進行驗證](../protect/certificates-configure.md)。

## <a name="wallpaper"></a>桌布

若將沒有影像之設定檔指派給已有影像的裝置，您可能會遇到非預期的行為。 例如，您建立一個沒有影像的設定檔。 然後將此設定檔指派給已有影像的裝置。 在此案例中，影像可能會變更為裝置預設，或原始影像可能會保留在裝置上。 此行為受到 Apple MDM 平台的控制和限制。

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>設定適用於：自動裝置註冊 (受監督)

- **底色圖案顯示位置**：選擇裝置上要顯示影像的位置。 選項包括：
  - **未設定**：未將自訂影像新增至裝置。 裝置會使用作業系統預設值。
  - **鎖定畫面**：將影像新增至鎖定畫面。
  - **主畫面**：將影像新增至主畫面。
  - **鎖定畫面與主畫面**：在鎖定畫面與主畫面上使用相同的影像。
- **底色圖案影像**：上傳您想要使用的現有 .png、.jpg 或 .jpeg 影像。 請確定檔案大小小於 750 KB。 您也可以**移除**已新增的影像。

> [!TIP]
> 若要在鎖定畫面與主畫面上顯示不同的影像，請使用鎖定畫面影像來建立設定檔。 然後使用主畫面影像建立另一個設定檔。 將兩個設定檔都指派給您的 iOS/iPadOS 使用者或裝置群組。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以針對 [macOS](macos-device-features-settings.md) 裝置建立裝置功能設定檔。
