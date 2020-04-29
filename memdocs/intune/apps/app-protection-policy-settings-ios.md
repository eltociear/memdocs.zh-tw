---
title: iOS/iPadOS 應用程式防護原則設定
titleSuffix: Microsoft Intune
description: 本主題描述 iOS/iPadOS 裝置的 iOS/iPadOS 應用程式保護原則 (APP) 設定。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f8b08f2-504c-4b38-bea2-b8a4ef0526b8
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eda210408adbb15d82d6bfc31bef2f225f53bc6f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80863072"
---
# <a name="ios-app-protection-policy-settings"></a>iOS 應用程式保護原則設定
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

本文描述 iOS/iPadOS 裝置的應用程式保護原則設定。 建立新原則時，您可以在 Azure 入口網站的 [設定]  窗格上，為應用程式保護原則[設定](app-protection-policies.md)所述的原則設定。

原則設定有三個類別：「資料重新配置」  、「存取需求」  和「條件式啟動」  。 在本文中「受原則管理的應用程式」一詞是指設有應用程式保護原則的應用程式。

> [!IMPORTANT]
> Intune Managed Browser 已退場。 請改用 [Microsoft Edge](../apps/manage-microsoft-edge.md) 作為受保護的 Intune 瀏覽器。 

## <a name="data-protection"></a>資料保護

### <a name="data-transfer"></a>資料轉送
| 設定 | 如何使用 | 預設值 |
|------|----------|-------|
| **將組織資料備份至 iTunes 和 iCloud 備份** | 選取 [封鎖]  ，防止此應用程式將公司或學校資料備份至 iTunes 和 iCloud。 選取 [允許]  ，允許此應用程式將公司或學校資料備份至 iTunes 和 iCloud。 | **允許**  |
| **將組織資料傳送至其他應用程式** | 指定可以接收這個應用程式資料的應用程式： <ul><li>**所有應用程式**：允許傳送到任何應用程式。 接收方應用程式將能夠讀取及編輯資料。</li><li>**無**：不允許將資料傳送到任何應用程式 (包括其他受原則管理的應用程式)。 如果使用者執行受控的開啟方式功能並傳輸文件，則資料將會加密且無法讀取。</li><li> **受原則管理的應用程式**：只允許傳送至其他受原則管理的應用程式。 <p><p>**注意︰** _使用者或許能夠透過「開啟方式」或「共用」擴充功能，來將內容傳輸至已取消註冊裝置上的非受控應用程式，或允許與非受控應用程式共用的已註冊裝置。傳輸的資料會由 Intune 加密，而非受控應用程式無法讀取該資料。_</li><li>**具有 OS 共用的原則受控應用程式**：僅允許將資料傳輸到其他原則受控的應用程式，以及將檔案傳輸至已註冊裝置上的其他 MDM 受控應用程式。 <p><p>**注意︰** _[具有 OS 共用的原則受控應用程式]  值僅適用於 MDM 註冊裝置。如果此設定會以取消註冊裝置上的使用者為目標，則適用**原則受控應用程式**值的行為。使用者將可透過「開啟方式」或「共用」擴充功能，來將未加密的內容傳輸至 iOS MDM allowOpenFromManagedtoUnmanaged 設定所允許的任何應用程式。如需此 iOS/iPadOS MDM 設定的詳細資訊，請參閱 https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf 。_<p><p></li><li>**具有開啟方式/共用的原則受控應用程式篩選**：僅允許傳輸到其他原則受控應用程式，並篩選 OS [開啟方式/共用] 對話方塊，以僅顯示原則受控應用程式。 若要設定 [開啟方式/共用]  對話方塊的篩選，則同時需要作為檔案/文件來源的應用程式，以及可開啟此檔案/文件來使用 Intune SDK for iOS 8.1.1 版或更新版本的應用程式。 <p><p>**注意︰** _如果應用程式支援 Intune 私有資料類型，使用者就能透過「開啟方式」或「共用」延伸模組來傳輸內容。傳輸的資料會由 Intune 加密，而非受控應用程式無法讀取該資料。_</li></ul><br>此外，設定為 [受原則管理的應用程式]  或 [無]  時，則會封鎖焦點搜尋 (允許在應用程式中搜尋資料) 和 Siri 捷徑等 iOS 9 功能。 <p><p>此原則也適用於 iOS/iPadOS 通用連結。 一般 Web 連結則是由 [在 Intune Managed Browser 中開啟應用程式連結]  原則設定所管理。 <p> Intune 可預設應用程式和服務的豁免清單，允許資料傳送。 此外，如果您需要允許資料傳送至不支援 Intune 應用程式的應用程式，您可以建立您自己的豁免清單。 請參閱[資料轉送豁免](#data-transfer-exemptions)以取得詳細資訊。 | **所有應用程式** |
| <ul><ui>**選取要豁免的應用程式** | 當您針對上一個選項選取 [受原則管理的應用程式]  時，可以使用這個選項。   |   |
| **接收來自其他應用程式的資料** | 指定可將資料傳送至這個應用程式的應用程式： <ul><li>**所有應用程式**：允許從任何應用程式傳送資料。</li><li>**無**：不允許從任何應用程式 (包括其他受原則管理的應用程式) 傳送資料。</li><li>**受原則管理的應用程式**：只允許從其他受原則管理的應用程式傳送。</li><li>**所有包含傳入組織資料的應用程式**：允許從任何應用程式傳送資料。 將沒有使用者身分識別的所有傳入資料視為組織中資料。 資料將使用由 `IntuneMAMUPN` 設定定義的 MDM 註冊使用者身分識別來進行標記。<p><p>**注意︰** _[所有包含傳入組織資料的應用程式]  值僅適用於 MDM 註冊裝置。如果此設定以未註冊裝置上的使用者為目標，則適用於**任意應用程式**值的行為。_</li></ul> 有一些 Intune 可以允許從中進行資料傳輸的豁免應用程式和服務。 如需應用程式和服務的完整清單，請參閱[資料傳輸豁免](#data-transfer-exemptions)。 在未註冊的 iOS/iPadOS 裝置上，啟用多重身分識別 MAM 的應用程式會忽略這項原則，並允許所有內送資料。<br><br> | **所有應用程式**    |
| **儲存組織資料的複本** | 選取 [封鎖]  ，在這個應用程式中停用 [另存新檔]  選項。 如果您想要允許使用 [另存新檔]  ，請選取 [允許]  。 <br><br>**注意︰** *Microsoft Excel、OneNote、Outlook、PowerPoint 和 Word 支援此設定。協力廠商和 LOB 應用程式也可以支援此設定。* <br><br> 當設定為 [封鎖]  時，您可以設定下列設定：[允許使用者儲存所選服務的複本]  。   | <br><br> **允許**   |
| <ul><ui>**允許使用者儲存複本到指定的服務位置** | 使用者可以儲存到幾個選取的服務 (商務用 OneDrive、SharePoint 和本機存放區)。 會封鎖所有其他服務。| **0 (已選取)**  |
| **限制其他應用程式之間的剪下、複製和貼上** | 指定何時剪下、複製和貼上動作可與這個應用程式搭配使用。 從下列項目進行選取： <ul><li>**封鎖**：不允許在這個應用程式與任何其他應用程式之間進行剪下、複製和貼上動作。</li><li>**受原則管理的應用程式**：允許在這個應用程式與其他受原則管理的應用程式之間進行剪下、複製和貼上動作。</li><li>**具有貼上的受原則管理的應用程式**：允許在這個應用程式與其他受原則管理的應用程式之間進行剪下或複製。 允許將資料從任何應用程式貼入這個應用程式。</li><li>**任何應用程式**：不限制與這個應用程式之間的剪下、複製和貼上。</ul> | **任何應用程式**   |
| <ul><ui>**任何應用程式的剪下和複製字元限制** | 指定可以從組織資料和帳戶剪下或複製的字元數。  如此可允許共用指定的字元數給任何應用程式，而不管 [限制利用其他應用程式剪下、複製及貼上]  設定。<p>預設值 = 0<p>**注意**：應用程式需要有 Intune SDK 9.0.14 版或更新版本。   | **0**   |
| **組織資料通知** | 透過組織帳戶的 OS 通知，以指定要共用多少組織資料。 此原則設定會影響本機裝置和任何連線的裝置，例如穿戴式裝置和智慧型喇叭。 應用程式可能會提供其他控制項來自訂通知行為，或選擇不接受所有值。 從下列項目進行選取： <ul><li>**封鎖**：不要共用通知。</li><ul><li>如果應用程式不支援，則會允許通知。</li></ul><li>**封鎖組織資料**：例如，不要在通知中共用組織資料。</li><UL><li>「您有新郵件」；「您有一個會議」。</li><li>如果應用程式不支援，則會封鎖通知。</li></ul><li>**允許**：在通知中共用組織資料。</li></ul> <p>**注意**：*此設定需要應用程式支援。目前，適用於 iOS 的 Outlook 版本 4.15.0 (或更新版本) 將支援此設定。* | **允許**   |
| **協力廠商鍵盤** | 選擇 [封鎖]  以防止在受控應用程式中使用協力廠商鍵盤。<p>啟用此設定時，使用者會收到一次性訊息，指出已封鎖使用協力廠商鍵盤。 當使用者第一次與需要使用鍵盤的組織資料互動時，就會顯示此訊息。 使用受控應用程式時，只能使用標準 iOS/iPadOS 鍵盤，其他鍵盤選項都會停用。 這項設定會影響多重身分識別應用程式的組織和個人帳戶。 此設定不會影響在非受控應用程式中使用協力廠商鍵盤。<p>**注意︰** 此功能需要應用程式使用 Intune SDK 版本 12.0.16 或更新版本。 若應用程式使用 8.0.14 到 (含) 12.0.15 的 SDK 版本，則不會正確地將此功能套用到多重身分識別應用程式。 如需詳細資訊，請參閱[已知問題：在 iOS/iPadOS 中未針對個人帳戶封鎖協力廠商鍵盤](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Updated-Known-issue-Third-party-keyboards-are-not-blocked-in-iOS/ba-p/339486) (英文)。 | **允許**  |

### <a name="encryption"></a>加密
| 設定 | 如何使用 | 預設值 |
|------|----------|-------|
| **加密組織資料** | 選擇 [需要]，在這個應用程式中啟用公司或學校資料的加密。  Intune 會強制 iOS/iPadOS 裝置加密以在裝置鎖定時保護應用程式資料。  應用程式可能會選擇性使用 Intune APP SDK 加密來加密應用程式資料。  Intune APP SDK 使用 iOS/iPadOS 密碼編譯方法來套用 256 位元 AES 加密到應用程式資料。 <br><br> 當您啟用這項設定時，使用者可能必須設定並使用 PIN 才能存取其裝置。 如果裝置没有 PIN，但必須加密，會出現下列訊息提示使用者設定 PIN：「您的組織要求您先啟用裝置 PIN，才能存取此應用程式」。 <br><br> 前往[正式 Apple 文件](https://support.apple.com/en-us/HT202739)，以查看哪些 iOS/iPadOS 加密模組已經過 FIPS 140-2 驗證。 | **需要**  |


### <a name="functionality"></a>功能
| 設定 | 如何使用 | 預設值 |
|------|----------|-------|
| **與原生連絡人應用程式同步應用程式** |  選取 [封鎖]  ，防止應用程式將資料儲存至裝置上的原生「連絡人」應用程式。 如果您選取 [允許]  ，則應用程式可以將資料儲存至裝置上的原生「連絡人」應用程式。 <br><br>當您執行選擇性抹除以移除應用程式中的工作或學校資料時，會移除直接從應用程式同步到原生「連絡人」應用程式的連絡人。 無法清除從原生通訊錄同步處理到其他外部來源的任何連絡人。 目前這僅適用於 Microsoft Outlook 應用程式。   | **允許**  |
| **列印組織資料** | 選取 [封鎖]  ，防止應用程式列印公司或學校資料。 如果您將此設定保留為 [允許]  (預設值)，則使用者將能夠匯出及列印所有組織資料。  | **允許**  |
| **限制與其他應用程式的 Web 傳輸** | 指定如何從原則受控的應用程式開啟 Web 內容 (HTTP/HTTPS 連結)。 從下列選項進行選擇： <ul><li>**任何應用程式**：允許任何應用程式中的 Web 連結。</li><li>**Intune Managed Browser**：只允許在 Intune Managed Browser 中開啟 Web 內容。 此瀏覽器為受原則管理的瀏覽器。</li><li>**Microsoft Edge**：只允許在 Microsoft Edge 中開啟 Web 內容。 此瀏覽器為受原則管理的瀏覽器。</li><li>**非受控瀏覽器**：只允許在 [非受控瀏覽器通訊協定]  設定中定義的非受控瀏覽器中開啟 Web 內容。 Web 內容在目標瀏覽器中將會是非受控。<br>**注意**：應用程式需要有 Intune SDK 11.0.9 版或更新版本。</li></ul> 如果您使用 Intune 管理裝置，請參閱[透過 Microsoft Intune 使用受控的瀏覽器原則管理網際網路存取](app-configuration-managed-browser.md)。<br><br>如果受控瀏覽器為必要但尚未安裝，則會提示終端使用者安裝 Microsoft Edge。<p>如果原則受控的瀏覽器為必要，則 iOS/iPadOS 通用連結是由 [允許應用程式將資料傳送至其他應用程式]  原則設定所管理。 <p>**Intune 裝置註冊**<br>如果您使用 Intune 來管理裝置，請參閱＜透過 Microsoft Intune 使用受控瀏覽器原則管理網際網路存取＞。 <p>**原則受控的 Microsoft Edge**<br>適用於行動裝置 (iOS/iPadOS 和 Android) 的 Microsoft Edge 瀏覽器支援 Intune 應用程式保護原則。 使用其公司 Azure AD 帳戶登入 Microsoft Edge 瀏覽器應用程式的使用者，將會受到 Intune 的保護。 Microsoft Edge 瀏覽器整合了 Intune SDK，並支援其所有的資料保護原則，但會防止：<br><ul><li>**另存新檔**：Microsoft Edge 瀏覽器不允許使用者將直接的應用程式內連線新增至雲端儲存體提供者 (例如 OneDrive)。</li><li>**連絡人同步**：Microsoft Edge 瀏覽器不會儲存至原生連絡人清單。</li></ul><br>**注意**：Intune SDK 無法判斷目標應用程式是否為瀏覽器。  在 iOS/iPadOS 裝置上，不允許任何其他受控瀏覽器應用程式。    | **未設定**  |
|<ul><ui>**非受控瀏覽器通訊協定** | 輸入*單一*非受控瀏覽器的通訊協定。 來自受原則管理之應用程式的 Web 內容 (http/https 連結) 將在任何支援此通訊協定的應用程式中開啟。 Web 內容在目標瀏覽器中將會是非受控。 <br><br>僅當您想要與未使用 Intune 應用程式防護原則啟用的特定瀏覽器共用受保護的內容時，才應該使用這個功能。 您必須與瀏覽器供應商聯繫，以判斷所需的瀏覽器所支援的通訊協定。<br><br>**注意**：只包含通訊協定前置詞。  如果您的瀏覽器需要 `mybrowser://www.microsoft.com` 格式的連結，請輸入 `mybrowser`。<br>連結將轉譯為：<br><ul><li>`http://www.microsoft.com` > `mybrowser://www.microsoft.com`</li><li>`https://www.microsoft.com` > `mybrowsers://www.microsoft.com`</li></ul> | **空白**  |

> [!NOTE]  
> 沒有資料保護設定可以控制 iOS/iPadOS 裝置上的 Apple 受控開啟方式功能。 若要使用管理 Apple「開啟於」，請參閱[使用 Microsoft Intune 管理 iOS/iPadOS 應用程式之間的資料傳輸](data-transfer-between-apps-manage-ios.md)。

## <a name="data-transfer-exemptions"></a>資料傳輸豁免

在特定情況下，有一些 Intune 應用程式保護原則可以允許豁免應用程式和平台服務傳送和接收資料傳輸。 這份清單可能隨時變更，並反映視為對安全產能有所幫助的服務和應用程式。

| 應用程式/服務名稱 | 說明 |
| ---- | --- |
|<code>tel; telprompt</code> | 原生 Phone 應用程式 |
| <code>skype</code> | Skype |
| <code>app-settings</code> | 裝置設定 |
| <code>itms; itmss; itms-apps; itms-appss; itms-services</code> | App Store |
| <code>calshow</code> | 原生行事曆 |


## <a name="access-requirements"></a>存取需求

| 設定 | 如何使用 | 預設值 |
|------|----------|-------|
| **PIN 以進行存取** | 選取 [需要]  ，要求 PIN 來使用此應用程式。 使用者第一次在工作或學校內容中執行應用程式時，系統會提示他們設定這個 PIN。 線上或離線工作時都會套用 PIN。    <br><br> 您可以使用 [PIN 以進行存取]  區段底下可用的設定，設定 PIN 強度。   | **需要** |
| <ul><ui> **PIN 類型** | 先設定數值或密碼類型的 PIN 需求，再存取已套用應用程式保護原則的應用程式。 數值需求只有數字，密碼則至少要以 1 個字母**或**至少要以 1 個特殊字元定義。  <br><br> **注意︰** *若要設定密碼類型，應用程式需要有 Intune SDK 7.1.12 版或更新版本。數值類型沒有 Intune SDK 版本限制。所允許特殊字元包括 iOS/iPadOS 英文鍵盤上的特殊字元和符號。*  | **數字**  |
| <ul><ui> **簡單的 PIN** | 選取 [允許]  ，允許使用者使用簡單的 PIN 序列 (例如 1234、1111、abcd 或 aaaa)。 選取 [封鎖]  ，防止其使用簡單的序列。 系統會在 3 字元滑動視窗中檢查簡單序列。 如果設定了 [區塊]  ，系統就不接受終端使用者將 PIN 設定為 1235 或 1112，但允許 1122。 <br><br>**注意**：*如果已設定密碼類型 PIN，而且 [允許簡單的 PIN] 設定為 [是]，則使用者的 PIN 需要至少 1 個字母**或**至少 1 個特殊字元。如果已設定密碼類型 PIN，而且 [允許簡單的 PIN] 設定為 [否]，則使用者的 PIN 需要至少 1 個數字 **和** 1 個字母 **以及** 至少 1 個特殊字元。*   |**允許**  |
| <ul><ui> **選取 PIN 長度下限** | 指定 PIN 序列的最小位數。  | **4**  |
| <ul><ui> **Touch ID 而非 PIN 以進行存取 (iOS 8+)** | 選取 [允許]  ，允許使用者使用 [Touch ID](https://support.apple.com/HT201371) 而非 PIN 以進行應用程式存取。    | **允許**  |
|<ul><ui><ul><ui>**逾時後以 PIN 覆寫 Touch ID**|  若要使用此設定，請選取 [需要]  ，然後設定非使用狀態逾時。  |**需要**  |
| <ul><ui><ul><ui><ul><ui> **逾時 (非使用狀態分鐘數)** |  指定密碼或數字 (依設定) PIN 將會覆寫使用指紋或臉部做為存取方法的時間 (分鐘)。 此逾時值應該大於在 [重新檢查存取需求前的剩餘時間 (分鐘)] 下指定的值。  |**30**  |
| <ul><ui><ul><ui>**以 Face ID 而非 PIN 存取 (iOS 11+)** | 選取 [允許]  ，允許使用者使用臉部辨識技術來驗證 iOS/iPadOS 裝置使用者。 如果允許，則必須使用 Face ID 來存取具備 Face ID 功能裝置上的應用程式。    | **允許**  |
| <ul><ui>**在數天後重設 PIN** | 選取 [是]  ，要求使用者在設定的一段時間 (以天為單位) 後變更其應用程式 PIN。  <br><br>當設定為 [是]  時，您可以接著設定需要重設 PIN 前的經過天數。 |**否**  |  
| <ul><ui><ul><ui> **天數** | 設定需要重設 PIN 前的經過天數。  |**90**  |
| <ul><ui>**設定裝置 PIN 時的應用程式 PIN** | 選取 [停用]  ，在設定公司入口網站的已註冊裝置上偵測到裝置鎖定時，停用應用程式 PIN。<br><br> **注意︰** *應用程式需要有 Intune SDK 7.0.1 版或更新版本。*  <br><br>在 iOS/iPadOS 裝置上，您可以讓使用者使用 [Touch ID](https://support.apple.com/HT201371) 或 [Face ID](https://support.apple.com/HT208109) 而非 PIN 來證明其身分識別。 Intune 使用 [LocalAuthentication](https://developer.apple.com/documentation/localauthentication/) API 來驗證使用 Touch ID 和 Face ID 的使用者。 若要深入了解 Touch ID 和 Face ID，請參閱 [iOS 安全性指南](https://www.apple.com/business/docs/iOS_Security_Guide.pdf)。  <br><br> 使用者嘗試透過其公司或學校帳戶使用此應用程式時，系統會提示他們提供自己的指紋識別或臉部識別，而不是輸入 PIN。 啟用此設定時，App 切換預覽影像會在使用工作或學校帳戶時變得很模糊。  |  **啟用** |  
| **公司或學校帳戶認證以進行存取** | 選取 [需要]  ，要求使用者使用其公司或學校帳戶登入以進行應用程式存取，而不是輸入 PIN。 如果您將此設定為 [需要]  且已開啟 PIN 或生物特徵辨識提示，則會顯示公司認證以及 PIN 或生物特徵辨識提示。  | **不需要** |
| **重新檢查存取需求前的經過時間 (非使用中狀態分鐘數)** | 設定必須經過的非使用中狀態分鐘數，之後應用程式會要求使用者再次指定存取需求。 <br><br> 例如，若管理員在原則中開啟 PIN 及「封鎖已 Root 破解的裝置」，則當使用者開啟 Intune 受控應用程式時，就必須輸入 PIN 並在未 Root 破解的裝置上使用應用程式。 如果使用這項設定，使用者在等於設定值的時段內都不需要在任何 Intune 受控應用程式上輸入 PIN 或接受另一次 Root 偵測檢查。  <br><br>**注意︰** *在 iOS/iPadOS 上，**相同發行者**的所有 Intune 受控應用程式都會共用 PIN。當裝置上的應用程式離開前景時，特定 PIN 的 PIN 計時器就會重設。在此設定中定義的逾時持續時間內，使用者不需要在任何共用 PIN 和 Intune 受控應用程式上輸入 PIN。此原則設定格式支援正整數。*     | **30** |

> [!NOTE]
> 若要深入了解在同一應用程式和使用者集合的 [存取] 區段中所設定多個 Intune 應用程式保護設定如何在 iOS/iPadOS 上運作，請參閱 [Intune MAM 常見問題集](mam-faq.md#app-experience-on-ios)與[在 Intune 中使用應用程式防護原則的存取動作選擇性地抹除資料](app-protection-policies-access-actions.md)。

## <a name="conditional-launch"></a>條件式啟動
設定條件式啟動設定，以設定您存取保護原則的登入安全性需求。 

根據預設，有數個設定會提供預先設定的值和動作。 您可以刪除其中某些設定，例如「最低 OS 版本」  。 您也可以從 [選取一個]  下拉式清單中選取其他設定。 

| 設定 | 如何使用 |  
|---------|------------| 
| **最低 OS 版本** | 指定使用此應用程式的最低 iOS/iPadOS 作業系統。 「動作」  包括： <br><ul><li>**警告** - 如果裝置上的 iOS/iPadOS 版本不符合需求，使用者將會看見通知。 此通知可以關閉。 </li></ul> <ul><li>**封鎖存取** - 如果裝置上的 iOS/iPadOS 版本不符合需求，將會禁止使用者存取。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。  </li></ul> </li></ul>此項目可以出現多次，每個執行個體支援不同的動作。<br><br> 此原則設定格式支援 major.minor、major.minor.build、major.minor.build.revision。 <br><br>**注意︰** *應用程式需要有 Intune SDK 7.0.1 版或更新版本。* |
| **PIN 嘗試次數上限** | 指定在執行已設定動作之前，使用者必須成功輸入 PIN 的嘗試次數。 此原則設定格式支援正整數。 「動作」  包括： <br><ul><li>**重設 PIN** - 使用者必須重設其 PIN。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。  </li></ul></li></ul> 預設值 = **5** |
| **離線寬限期** | MAM 應用程式可以離線執行的分鐘數。 指定經過多少時間 (分鐘) 之後即會重新檢查應用程式存取需求。 「動作」  包括： <br><ul><li>**封鎖存取 (分鐘)** ：MAM 應用程式可以離線執行的分鐘數。 指定經過多少時間 (分鐘) 之後即會重新檢查應用程式存取需求。 在設定的期間過後，該應用程式會封鎖對公司或學校資料的存取要求，直到有可用的網路連線為止。 此原則設定格式支援正整數。<br><br>預設值 = **720** 分鐘 (12 小時) </li></ul> <ul><li>**抹除資料 (天)** - 在離線執行達到此天數 (由系統管理員定義) 之後，應用程式需要使用者連線到網路並重新驗證。 如果使用者成功驗證，就可以繼續存取其資料，而且會重設離線間隔。  如果使用者無法驗證，應用程式會執行使用者帳戶和資料的選擇性抹除。  如需使用選擇性抹除會移除哪些資料的詳細資訊，請參閱[如何只抹除 Intune 管理之應用程式中的公司資料](apps-selective-wipe.md)。 此原則設定格式支援正整數。 <br><br> 預設值 = **90 天** </li></ul>  此項目可以出現多次，每個執行個體支援不同的動作。 |
| **已越獄或 Root 破解的裝置** | 這項設定沒有可設定的值。 「動作」  包括： <br><ul><li>**封鎖存取** - 防止在已越獄或 Root 破解的裝置上執行此應用程式。 使用者仍然可以繼續使用這個應用程式來執行個人工作，但必須使用不同裝置來存取這個應用程式中的工作或學校資料。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。 </li></ul> |
| **最低應用程式版本** | 指定作業系統最小值。 「動作」  包括： <br><ul><li>**警告** - 如果裝置上的應用程式版本不符合需求，使用者會看見通知。 此通知可以關閉。</li></ul> <ul><li>**封鎖存取** - 如果裝置上的應用程式版本不符合需求，會封鎖使用者進行存取。 </li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。 </li></ul> </li></ul>   因為應用程式之間通常會有不同的版本控制配置，所以請建立包含一個針對單一應用程式之最低應用程式版本的原則 (例如，「Outlook 版本原則」  )。<br><br> 此項目可以出現多次，每個執行個體支援不同的動作。<br><br> 此原則設定格式支援 major.minor、major.minor.build、major.minor.build.revision。<br><br> **注意︰** *應用程式需要有 Intune SDK 7.0.1 版或更新版本。*<br><br> 此外，您可以設定終端使用者可從**何處**取得企業營運 (LOB) 應用程式的更新版本。 終端使用者將可在 [應用程式最小版本]  條件式啟動對話方塊中看見此功能，其將提示終端使用者更新為 LOB 應用程式的最小版本。 在 iOS/iPadOS 上，此功能需要整合 (或使用包裝工具包裝) 應用程式與 Intune SDK for iOS。 10.0.7 版或更新版本。 若要設定終端使用者應該更新 LOB 應用程式的位置，應用程式需要使用金鑰 `com.microsoft.intune.myappstore` 傳送給它的受控[應用程式設定原則](app-configuration-policies-managed-app.md)。 傳送的值將定義終端使用者要從哪個存放區下載應用程式。 如果透過公司入口網站部署應用程式，則值必須為 `CompanyPortal`。 針對任何其他存放區，您必須輸入完整的 URL。 |
| **最低 SDK 版本** | 指定 Intune SDK 版本的最低值。 「動作」  包括： <br><ul><li>**封鎖存取** - 如果應用程式的 Intune 應用程式防護原則 SDK 版本不符合需求，則會封鎖使用者進行存取。 </li></ul><ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。 </li></ul></li></ul>若要深入了解 Intune 應用程式保護原則 SDK，請參閱 [Intune App SDK 概觀](../developer/app-sdk.md)。 因為應用程式之間通常會有不同的 Intune SDK 版本，所以請建立包含一個針對單一應用程式之最低 Intune SDK 版本的原則 (例如，「適用於 Outlook 的 Intune SDK 版本原則」  )。 <br><br> 此項目可以出現多次，每個執行個體支援不同的動作。|
| **裝置型號** | 指定以分號分隔的型號識別碼清單。 這些值不會區分大小寫。 「動作」  包括： <br><ul><li>**允許指定 (封鎖非指定)** - 僅有符合指定裝置型號的裝置可以使用應用程式。 會封鎖所有其他裝置型號。 </li></ul> <ul><li>**允許指定 (抹除非指定)** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。</li></ul> 如需使用此設定的詳細資訊，請參閱[條件式啟動動作](app-protection-policies-access-actions.md#ios-policy-settings)。 |
| **允許的裝置威脅等級上限** | 應用程式保護原則可以利用 Intune-MTD 連接器。 指定使用此應用程式可接受的最大威脅等級。 威脅取決於您在終端使用者裝置上選擇的 Mobile Threat Defense (MTD) 廠商應用程式。 指定 [安全]  、[低]  、[中]  或 [高]  。 [安全]  要求裝置上沒有威脅，而且是最嚴格的可設定值，而 [高]  基本上需要作用中的 Intune 對 MTD 連線。 「動作」  包括： <br><ul><li>[封鎖存取]  - 如果終端使用者裝置上由您選擇的 Mobile Threat Defense (MTD) 廠商應用程式所決定的威脅等級不符合此需求，將會封鎖使用者進行存取。</li></ul><ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。</li></ul>**注意︰** 應用程式需要有 Intune SDK 12.0.15 版或更新版本。  <br><br> 如需使用此設定的詳細資訊，請參閱[為已取消註冊的裝置啟用 MTD](../protect/mtd-enable-unenrolled-devices.md)。 |

### <a name="learn-more"></a>深入了解
- 深入了解 [LinkedIn information and features in your Microsoft apps](https://go.microsoft.com/fwlink/?linkid=850740) (Microsoft 應用程式中的 LinkedIn 資訊與功能)。
- 在 [Office 365 藍圖頁面](https://products.office.com/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc)上深入了解 LinkedIn 帳戶連線版本。 
- 深入了解 [Microsoft 應用程式和服務的 LinkedIn 帳戶連線](https://docs.microsoft.com/azure/active-directory/linkedin-integration)。
- 如需在使用者的 LinkedIn 與 Microsoft 工作或學校帳戶之間所共用資料的詳細資訊，請參閱[使用工作或學校帳戶在 Microsoft 應用程式中 LinkedIn](https://www.linkedin.com/help/linkedin/answer/84077)。
