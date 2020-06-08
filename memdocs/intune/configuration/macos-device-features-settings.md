---
title: Microsoft Intune 中的 macOS 裝置功能設定 - Azure | Microsoft Docs
description: 請在 Microsoft Intune 中查看針對 AirPrint 設定 macOS 裝置的設定，並自訂 [登入] 視窗以顯示或隱藏電源按鈕。 請參閱取得適用於您網路中 AirPrint 伺服器的 IP 位址、路徑及連接埠設定步驟。 在裝置組態設定檔中使用這些設定，可設定 macOS 裝置功能。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d4bc2de9e16cfcf9322cf343badafe3c9a35c70
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428908"
---
# <a name="macos-device-feature-settings-in-intune"></a>Intune 中的 macOS 裝置功能設定

Intune 包含的內建設定可在 macOS 裝置上自訂功能。 例如，系統管理員可以新增 AirPrint 印表機、選擇使用者登入的方式、設定電源控制、使用單一登入驗證等。

使用這些功能來控制 macOS 裝置，作為行動裝置管理 (MDM) 解決方案的一部分。

本文會列出這些設定，並說明每個設定的用途。 同時也會列出使用終端機應用程式 (模擬器) 來取得 AirPrint 印表機之 IP 位址、路徑和連接埠的步驟。 如需裝置功能的詳細資訊，請移至[新增 iOS/iPadOS 或 macOS 裝置功能設定](device-features-configure.md)。

> [!NOTE]
> 使用者介面可能與本文中的註冊類型不同。 本文中的資訊正確。 即將推出的版本中將會更新使用者介面。

## <a name="before-you-begin"></a>開始之前

[建立 macOS 裝置功能設定檔](device-features-configure.md)。

> [!NOTE]
> 這些設定適用於不同的註冊類型，而其中有部分設定適用於所有註冊選項。 如需不同註冊類型的詳細資訊，請參閱 [macOS 註冊](../enrollment/macos-enroll.md)。

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>設定適用於：所有註冊類型

- **AirPrint 目的地**：**新增**一或多個使用者可從其裝置進行列印的 AirPrint 印表機。 另請輸入：
  - **連接埠** (iOS 11.0+、iPadOS 13.0+)：輸入 AirPrint 目的地的接聽連接埠。 如果將此屬性留白，AirPrint 就會使用預設連接埠。
  - **IP 位址**：輸入印表機的 IPv4 或 IPv6 位址。 例如，輸入 `10.0.0.1`。 如果您使用主機名稱來識別印表機，可以透過在終端機應用程式中偵測該印表機來取得 IP 位址。 (本文中的) [取得 IP 位址與路徑](#get-the-ip-address-and-path) (英文) 有更多詳細資料。
  - **路徑**：輸入印表機的資源路徑。 您網路上印表機的路徑通常是 `ipp/print`。 (本文中的) [取得 IP 位址與路徑](#get-the-ip-address-and-path) (英文) 有更多詳細資料。
  - **TLS** (iOS 11.0+、iPadOS 13.0+)：選項包括：
    - [否] (預設)：連線到 AirPrint 印表機時，不會強制執行傳輸層安全性 (TLS)。
    - **是**：使用傳輸層安全性 (TLS) 保護 AirPrint 連線。

- **匯入**包含 AirPrint 印表機且以逗號分隔的清單檔 (.csv)。 此外，當您於 Intune 中新增 AirPrint 印表機之後，也可以**匯出**此清單。

### <a name="get-the-ip-address-and-path"></a>取得 IP 位址和路徑

若要新增 AirPrinter 伺服器，您需要有印表機的 IP 位址、資源路徑及連接埠。 下列步驟說明如何取得此資訊。

1. 在連線到與 AirPrint 印表機相同區域網路 (子網路) 的 Mac 上，開啟 [終端機] (從 **/Applications/Utilities**)。
2. 在 [終端機] 應用程式中，輸入 `ippfind`，然後選取 Enter 鍵。

    記下印表機資訊。 例如，可能會傳回類似 `ipp://myprinter.local.:631/ipp/port1` 的內容。 第一個部分是印表機的名稱。 最後一個部分 (`ipp/port1`) 是資源路徑。

3. 在 [終端機] 中，輸入 `ping myprinter.local`，然後選取 Enter 鍵。

   記下 IP 位址。 例如，可能會傳回類似 `PING myprinter.local (10.50.25.21)` 的內容。

4. 使用 IP 位址和資源路徑值。 在此範例中，IP 位址是 `10.50.25.21`，而資源路徑則是 `/ipp/port1`。

## <a name="associated-domains"></a>相關網域

在 Intune 中，您可以︰

- 新增許多應用程式對網域關聯。
- 將許多網域與相同的應用程式關聯。

本功能適用於：

- macOS 10.15 與更新版本

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>設定適用於：使用者核准的裝置註冊，以及自動化的裝置註冊

- **相關網域**：**新增**網域與應用程式之間的關聯。 此功能共用 Contoso 應用程式與 Contoso 網站之間的登入認證。 另請輸入：

  - **應用程式識別碼**：輸入應用程式的應用程式識別碼，該應用程式要與網站建立關聯。 應用程式識別碼包含小組識別碼與套件組合識別碼：`TeamID.BundleID`。

    小組識別碼是由 Apple 為您的應用程式開發人員產生之 10 個字元的英數 (字母與數字) 字串，例如 `ABCDE12345`。 [尋找您的小組識別碼](https://help.apple.com/developer-account/#/dev55c3c710c)  (會開啟 Apple 的網站) 提供詳細資訊。

    套件組合識別碼能唯一識別應用程式，且其格式通常是反向網域名稱標記法。 例如，Finder 的套件組合識別碼為 `com.apple.finder`。 若要尋找套件組合識別碼，請在終端機中使用 AppleScript：

    `osascript -e 'id of app "ExampleApp"'`

  - **網域**：輸入要與應用程式建立關聯的網站網域。 網域包含服務類型與完整主機名稱，例如 `webcredentials:www.contoso.com`。

    您可以在網域開頭的前方輸入 `*.` (星號萬用字元與句號) 來表示相關聯網域的所有子網域。 句號為必要。 與萬用字元網域相比，確切的網域具有較高的優先順序。 因此，來自父網域的模式「只會在」於完整子網域中找不到相符項目時進行比對。

    服務類型可以是：

    - **authsrv**：單一登入應用程式擴充功能
    - **applink**：通用連結
    - **webcredentials**：自動填滿密碼

> [!TIP]
> 若要進行疑難排解，請在您的 macOS 裝置上開啟 [系統偏好設定] > [描述檔]。 確認您所建立的設定檔已位於裝置設定檔清單。 如果已加以列出，請確定設定檔中具有 [相關網域設定]，而且其包含正確的應用程式識別碼與網域。

## <a name="login-items"></a>登入項目

### <a name="settings-apply-to-all-enrollment-types"></a>設定適用於：所有註冊類型

- **新增登入時要啟動的檔案、資料夾與自訂應用程式**：[新增] 使用者登入裝置時所要開啟的檔案、資料夾、自訂應用程式或系統應用程式路徑。 另請輸入：

  - **項目的路徑**：輸入檔案、資料夾或應用程式的路徑。 系統應用程式，或針對您組織所建置或自訂的應用程式，通常會位於 `Applications` 資料夾中，並具有類似 `/Applications/AppName.app` 的路徑。

    您可以新增許多檔案、資料夾與應用程式。 例如，輸入：  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    新增任何應用程式、資料夾或檔案時，請務必輸入正確的路徑。 並非所有項目都位於 `Applications` 資料夾。 如果使用者將項目從某個位置移至另一個位置，則路徑會變更。 這個已移動的項目並不會在使用者登入時開啟。

  - **隱藏**：選擇顯示或隱藏該應用程式。 選項包括：
    - **未設定**：這是預設值。 Intune 不會變更或更新此設定。 根據預設，OS 會顯示在使用者與群組登入項目清單中，取消核取隱藏選項的項目。
    - **是**：隱藏使用者與群組登入項目清單中的應用程式。

## <a name="login-window"></a>登入視窗

### <a name="settings-apply-to-all-enrollment-types"></a>設定適用於：所有註冊類型

- **在選單列中顯示其他資訊**：選取功能表列上的時間區域時，[是] 可顯示主機名稱與 macOS 版本。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會在功能表列上顯示這項資訊。
- **橫幅**：輸入要在裝置登入畫面中顯示的訊息。 例如，輸入您的組織資訊、歡迎訊息、失物招領資訊等。
- **需要使用者名稱與密碼文字欄位**：選擇使用者登入裝置的方式。 [是] 需要使用者輸入使用者名稱與密碼。 當設定為 [未設定] 時，Intune 則不會變更或更新此設定。 根據預設，OS 需要使用者從清單中選取其使用者名稱，然後輸入其密碼。

  另請輸入：

  - **隱藏本機使用者**：[是] 不會在使用者清單中，顯示包含標準與系統管理員帳戶的本機使用者帳戶。 只會顯示網路和系統使用者帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會在使用者清單中顯示本機使用者帳戶。
  - **隱藏行動帳戶**：[是] 不會在使用者清單中顯示行動帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會在使用者清單中顯示行動帳戶。 有些行動帳戶可能會顯示為網路使用者。
  - **顯示網路使用者**：選取 [是]，即會在使用者清單中列出網路使用者。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會在使用者清單中顯示網路使用者帳戶。
  - **隱藏電腦的系統管理員**：[是] 不會在使用者清單中顯示系統管理員使用者帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會在使用者清單中顯示系統管理員使用者帳戶。
  - **顯示其他使用者**：選取 [是]，即會在使用者清單中列出 [其他] 使用者。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會在使用者清單中顯示其他使用者帳戶。

- **隱藏 [關機] 按鈕**：[是] 不會在登入畫面上顯示 [關機] 按鈕。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會顯示關機按鈕。
- **隱藏 [重新啟動] 按鈕**：[是] 不會在登入畫面上顯示 [重新啟動] 按鈕。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會顯示重新啟動按鈕。
- **隱藏 [睡眠] 按鈕**：[是] 不會在登入畫面上顯示 [睡眠] 按鈕。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會顯示睡眠按鈕。
- **讓使用者無法從 [主控台] 登入**：[是] 會隱藏用於登入的 macOS 命令列。 若是一般使用者，請將此設定設為 [是]。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓進階使用者使用 macOS 命令列登入。 為了進入主控台模式，使用者要在 [使用者名稱] 欄位中輸入 `>console`，然後必須在主控台視窗中進行驗證。
- **登入時停用 [關機]** ：[是] 可避免使用者在登入之後，選取 [關機] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者在裝置上選取 [關機] 功能表項目。
- **登入時停用 [重新啟動]** ：[是] 可避免使用者在登入之後，選取 [重新啟動] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者在裝置上選取 [重新啟動] 功能表項目。
- **登入時停用 [關閉電源]** ：[是] 可避免使用者在登入之後，選取 [關閉電源] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者在裝置上選取 [關機] 功能表項目。
- **登入時停用 [登出]** (macOS 10.13 及更新版本)：[是] 可避免使用者在登入之後，選取 [登出] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者在裝置上選取 [登出] 功能表項目。
- **登入時停用 [鎖定畫面]** (macOS 10.13 及更新版本)：[是] 可避免使用者在登入之後，選取 [鎖定畫面] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者在裝置上選取 [鎖定畫面] 功能表項目。

## <a name="single-sign-on-app-extension"></a>單一登入應用程式擴充功能

本功能適用於：

- macOS 10.15 與更新版本

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>設定適用於：使用者核准的裝置註冊，以及自動化的裝置註冊

- **SSO 應用程式延伸模組類型**：選擇認證 SSO 應用程式延伸模組的類型。 選項包括：

  - **未設定**：不使用應用程式延伸模組。 若要停用應用程式延伸模組，請將 SSO 應用程式延伸模組類型切換成 [未設定]。
  - **重新導向**：使用一般且可自訂的重新導向應用程式延伸模組，以搭配新式驗證流程使用 SSO。 請確定您知道組織應用程式延伸模組的延伸模組與小組識別碼。
  - **認證**：使用一般且可自訂的認證應用程式延伸模組，以搭配查問與回應驗證流程使用 SSO。 請確定您知道組織 SSO 應用程式延伸模組的延伸模組識別碼與小組識別碼。  
  - **Kerberos**：使用 Apple 的內建 Kerberos 延伸模組，其隨附於 macOS Catalina 10.15 與更新版本中。 此選項為 [認證] 應用程式延伸模組的 Kerberos 特定版本。

  > [!TIP]
  > 使用 [重新導向] 與 [認證] 類型時，您會新增自己的設定值來透過延伸模組傳遞。 如果您是使用 [認證]，請考慮使用由 Apple 在 [Kerberos] 類型中所提供的內建組態設定。

- **延伸模組識別碼** (重新導向與認證)：輸入能識別 SSO 應用程式延伸模組的套件組合識別碼，例如 `com.apple.ssoexample`。
- **小組識別碼** (重新導向與認證)：輸入 SSO 應用程式延伸模組的小組識別碼。 小組識別碼是由 Apple 產生之 10 個字元的英數 (數字與字母) 字串，例如 `ABCDE12345`。 

  [尋找小組識別碼](https://help.apple.com/developer-account/#/dev55c3c710c) (會開啟 Apple 的網站) 會提供詳細資訊。

- **領域** (認證與 Kerberos)：輸入驗證領域的名稱。 領域名稱應為大寫，例如 `CONTOSO.COM`。 您的領域名稱通常會與您的 DNS 網域名稱相同，但全部都是大寫。

- **網域** (認證與 Kerberos)：輸入可以透過 SSO 驗證的網站網域或主機名稱。 例如，如果您的網站是 `mysite.contoso.com`，則 `mysite` 是主機名稱，而 `contoso.com` 則是網域名稱。 當使用者連線到上述其中一個網站時，應用程式延伸模組會處理驗證挑戰。 此驗證可讓使用者使用 Face ID、Touch ID 或 Apple PIN 碼/密碼來登入。

  - 您單一登入應用程式延伸模組 Intune 設定檔中的所有網域都不能重複。 您不能在任何單一登入應用程式延伸模組設定檔中重複使用網域，即使您是使用不同類型的 SSO 應用程式延伸模組也一樣。
  - 這些網域不會區分大小寫。

- **URL** (僅限重新導向)：輸入識別提供者的 URL 前置詞，重新導向應用程式延伸模組會代為使用 SSO。 當使用者被重新導向到這些 URL 時，SSO 應用程式延伸模組即會介入並提示進行 SSO。

  - 您的 Intune 單一登入應用程式延伸模組設定檔中的所有 URL 都不能重複。 您不能在任何 SSO 應用程式延伸模組設定檔中重複使用網域，即使您是使用不同類型的 SSO 應用程式延伸模組也一樣。
  - URL 的開頭必須是 http:// 或 https://。

- **其他設定** (重新導向與認證)：輸入要傳遞到 SSO 應用程式延伸模組的其他延伸模組專用資料：
  - **索引鍵**：輸入所要新增項目的名稱，例如 `user name`。
  - **類型**：輸入資料的類型。 選項包括：

    - 字串
    - 布林值：在 [設定值] 中，輸入 `True` 或 `False`。
    - 整數：在 [設定值] 中，輸入數字。

  - **值**：輸入資料。
  
  - **新增**：選取以新增設定金鑰。

- **鑰匙串使用方式** (僅限 Kerberos)：選擇 [封鎖] 來防止將密碼儲存並保存在鑰匙串中。 如果選擇封鎖，則系統不會提示使用者儲存其密碼，且需要在 Kerberos 票證到期時重新輸入該密碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許將密碼儲存並保存在 Keychain 中。 當票證到期時，系統不會提示使用者重新輸入其密碼。
- **Face ID、Touch ID 或密碼** (僅限 Kerberos)：[必要]，強制使用者在需要認證以更新 Kerberos 票證時，輸入 Face ID、Touch ID 或裝置密碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會要求使用者使用生物識別技術或裝置密碼來重新整理 Kerberos 票證。 如果封鎖 [鑰匙串使用方式]，則不會套用此設定。
- **預設領域** (僅限 Kerberos)：選擇 [啟用] 以將所輸入的 [領域] 值設定為預設領域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會設定預設領域。

  > [!TIP]
  > - 如果您要在組織中設定多個 Kerberos SSO 應用程式延伸模組，就必須 [啟用] 此設定。
  > - 如果您會使用多個領域，請 [啟用] 此設定。 其會將您輸入的 [領域] 值設定為預設領域。
  > - 如果您只有單一領域，請將其保留為 [未設定] \(預設\)。

- **自動探索** (僅限 Kerberos)：設為 [封鎖] 時，Kerberos 延伸模組不會自動使用 LDAP 及 DNS 來判斷其 Active Directory 網站名稱。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許延伸模組自動找出 Active Directory 網站名稱。
- **密碼變更** (僅限 Kerberos)：[封鎖] 會防止使用者變更其用來登入所輸入網域的密碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許變更密碼。  
- **密碼同步** (僅限 Kerberos)：選擇 [啟用]，以將使用者的本機密碼同步到 Azure AD。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會停用密碼同步至 Azure AD。 請使用此設定作為 SSO 的替代方案或備案。 如果使用者是使用 Apple 行動帳戶來登入，此設定無法運作。
- **Windows Server Active Directory 密碼複雜度** (僅限 Kerberos)：選擇 [需要]，以強制使用者密碼符合 Active Directory 的密碼複雜性需求。 如需詳細資訊，請參閱[密碼必須符合複雜性需求](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements) (機器翻譯)。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會要求使用者符合 Active Directory 的密碼需求。
- **最小密碼長度** (僅限 Kerberos)：輸入組成使用者密碼的最少字元數。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會強制使用者施行密碼長度下限。
- **密碼重複使用限制** (僅限 Kerberos)：輸入可以在網域上重新使用先前密碼之前，必須使用的新密碼數目 (從 1 到 24)。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會強制施行密碼重複使用限制。
- **密碼最短存留期** (僅限 Kerberos)：輸入密碼必須在網域上使用的最少天數，然後使用者才可以變更密碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會強制施行密碼變更前的密碼最短存留期。
- **密碼到期通知** (僅限 Kerberos)：輸入系統會在密碼到期的幾天之前通知使用者其密碼即將到期。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會使用 `15` 天。
- **密碼到期** (僅限 Kerberos)：輸入必須變更裝置密碼前的天數。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 永遠不會讓密碼過期。
- **密碼變更 URL** (僅限 Kerberos)：輸入使用者啟動 Kerberos 密碼變更時開啟的 URL。
- **主體名稱** (僅限 Kerberos)：輸入 Kerberos 主體的使用者名稱。 您不需要包含領域名稱。 例如，在 `user@contoso.com` 中，`user` 是主體名稱，而 `contoso.com` 則是領域名稱。

  > [!TIP]
  > - 您也可以在主體名稱中使用變數，方法是輸入大括弧 `{{ }}`。 例如，若要顯示使用者名稱，請輸入 `Username: {{username}}`。 
  > - 不過，請小心使用變數替代，因為變數不會在 UI 中驗證，而且會區分大小寫。 請務必輸入正確的資訊。
  
- **Active Directory 網站代碼** (僅限 Kerberos)：輸入 Kerberos 延伸模組應使用的 Active Directory 網站名稱。 您可能不需要變更此值，因為 Kerberos 延伸模組可能會自動尋找 Active Directory 站台碼。
- **快取名稱** (僅限 Kerberos)：輸入 Kerberos 快取的一般安全性服務 (GSS) 名稱。 您通常不會需要設定此值。  
- **密碼需求訊息** (僅限 Kerberos)：輸入要向使用者顯示的組織密碼需求文字版本。 如果您不要求 Active Directory 的密碼複雜性需求，或未輸入密碼長度下限，便會顯示此訊息。  
- **應用程式套件組合識別碼** (僅限 Kerberos)：[新增] 應在裝置上使用單一登入的應用程式套件組合識別碼。 這些應用程式會被授權可存取 Kerberos 票證授權票證和驗證票證。 應用程式也會向已獲授權存取的服務驗證使用者。
- **網域領域對應** (僅限 Kerberos)：[新增] 應對應至領域的網域 DNS 尾碼。 在主機 DNS 名稱不符合領域名稱的情況下使用此設定。 您通常不會需要建立此自訂網域對領域對應。
- **PKINIT 憑證** (僅限 Kerberos)：[選取] 可用於 Kerberos 驗證的初始驗證公開金鑰加密 (PKINIT) 憑證。 您可以從自己已在 Intune 中新增的 [PKCS](../protect/certficates-pfx-configure.md) 或 [SCEP](../protect/certificates-scep-configure.md) 憑證中選擇。 如需憑證的詳細資訊，請參閱[在 Microsoft Intune 中使用憑證進行驗證](../protect/certificates-configure.md)。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

您也可以在 [iOS/iPadOS](ios-device-features-settings.md) 上設定裝置功能。
