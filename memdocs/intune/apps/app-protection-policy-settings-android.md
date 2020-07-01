---
title: Android 應用程式防護原則設定
titleSuffix: Microsoft Intune
description: 本主題說明 Android 裝置的應用程式防護原則設定。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9e9ef9f5-1215-4df1-b690-6b21a5a631f8
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec80e0cde433f21474a53acf66dbef5ddca206bc
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502641"
---
# <a name="android-app-protection-policy-settings-in-microsoft-intune"></a>Microsoft Intune 的 Android 應用程式保護原則設定
本文描述 Android 裝置的應用程式防護原則設定。 您可以在 Azure 入口網站的 [設定] 窗格上，為應用程式防護原則[設定](app-protection-policies.md)所述的原則設定。
原則設定分為三類：資料保護設定、存取需求和條件式啟動。 在本文中「受原則管理的應用程式」一詞是指設有應用程式保護原則的應用程式。

> [!IMPORTANT]
> Android 裝置上需要有 Intune 公司入口網站，才能接收應用程式保護原則。 如需詳細資訊，請參閱 [Intune 公司入口網站存取應用程式需求](../fundamentals/end-user-mam-apps-android.md)。
>
> Intune Managed Browser 已淘汰。 請改用 [Microsoft Edge](../apps/manage-microsoft-edge.md) 作為受保護的 Intune 瀏覽器。 

## <a name="data-protection"></a>資料保護 
### <a name="data-transfer"></a>資料轉送
| 設定 | 如何使用 | 預設值 |
|------|------|------|
| **將組織資料備份至 Android 備份服務** | 選取 [封鎖]，防止此應用程式將公司或學校資料備份至 [Android 備份服務](https://developer.android.com/google/backup/index.html)。<br><br> 選取 [允許]，允許此應用程式備份公司或學校資料。| **允許** |
| **將組織資料傳送至其他應用程式** | 指定可以接收這個應用程式資料的應用程式： <ul><li> **受原則管理的應用程式**：只允許傳送至其他受原則管理的應用程式。</li> <li>**所有應用程式**：允許傳送到任何應用程式。 </li> <li>**無**：不允許將資料傳送到任何應用程式 (包括其他受原則管理的應用程式)。</li></ul> <p>Intune 可預設應用程式和服務的豁免清單，允許資料傳送。 此外，如果您需要允許資料傳送至不支援 Intune 應用程式的應用程式，您可以建立您自己的豁免清單。 如需詳細資訊，請參閱[資料轉送豁免](app-protection-policy-settings-android.md#data-transfer-exemptions)。<p>此原則也適用於 Android 應用程式連結。  一般 Web 連結則是由 [在 Intune Managed Browser 中開啟應用程式連結] 原則設定所管理。<p><div class="NOTE"><p>注意</p><p>Intune 目前不支援 Android Instant Apps 功能。 Intune 會封鎖與此應用程式之間的任何資料連接。 如需詳細資訊，請參閱 Android 開發人員文件中的 [Android Instant Apps](https://developer.android.com/topic/instant-apps/index.html) \(英文\)。</p><p>如果 [將組織資料傳送至其他應用程式] 已設定為 [所有應用程式]，則文字資料仍可透過 OS 共用傳送至剪貼簿。</p></div> | **所有應用程式** | 
|<ul><ui>**選取要豁免的應用程式** | 當您針對上一個選項選取 [受原則管理的應用程式] 時，可以使用這個選項。 | |
|<ul><ui>**儲存組織資料的複本** | 選擇 [封鎖]，在這個應用程式中停用 [另存新檔] 選項。 如果您想要允許使用 [另存新檔]，請選擇 [允許]。 **注意︰** *Microsoft Excel、OneNote、PowerPoint 和 Word 支援此設定。協力廠商和 LOB 應用程式也可能支援此設定。*| **允許** |  
|<ul><ui><ul><ui>**允許使用者儲存複本到指定的服務位置** |使用者可以儲存到幾個選取的服務 (商務用 OneDrive、SharePoint 和本機存放區)。 將會封鎖所有其他服務。  | **0 (已選取)** |
|<ul><ui>**將電信資料傳送至** | 一般來說，當使用者在應用程式中選取超連結電話號碼時，撥號程式應用程式將使用預先填入的電話號碼開啟，而且準備撥號。 當此類型的內容從受原則管理的應用程式起始時，請針對此設定選擇如何處理這類傳送：<ul><li>**無，不在應用程式之間傳送此資料**：當偵測到電話號碼時，不傳送通訊資料。</li><li>**特定的撥號程式應用程式**：當偵測到電話號碼時，允許特定的撥號程式應用程式起始連絡人。</li><li>**任一受原則管理的撥號程式應用程式**：當偵測到電話號碼時，允許任一受原則管理的撥號程式應用程式起始連絡人。</li><li>**任一撥號程式應用程式**：當偵測到電話號碼時，允許使用任一撥號程式應用程式起始連絡人。</li></ul>| **任一撥號程式應用程式** |  
|<ul><ui><ul><ui>**撥號程式應用程式套件識別碼** | 當您選取特定的撥號程式時，必須提供[應用程式套件識別碼](../apps/app-configuration-vpn-ae.md#get-the-app-package-id)。 | **空白** |
|<ul><ui><ul><ui>**撥號程式應用程式名稱** | 當您選取特定的撥號程式時，必須提供撥號程式應用程式的名稱。 | **空白** |
| **接收來自其他應用程式的資料** | 指定可將資料傳送至這個應用程式的應用程式： <ul><li>**受原則管理的應用程式**：只允許從其他受原則管理的應用程式傳送。</li><li>**所有應用程式**：允許從任何應用程式傳送資料。</li><li>**無**：不允許從任何應用程式 (包括其他受原則管理的應用程式) 傳送資料。 </li></ul> <p>有一些 Intune 可以允許從中進行資料傳輸的豁免應用程式和服務。 如需應用程式和服務的完整清單，請參閱[資料傳輸豁免](app-protection-policy-settings-android.md#data-transfer-exemptions)。 | **所有應用程式** |
| **限制其他應用程式之間的剪下、複製和貼上** | 指定何時剪下、複製和貼上動作可與這個應用程式搭配使用。 從下列選項進行選擇： <ul><li>**封鎖**：不允許在這個應用程式與任何其他應用程式之間進行剪下、複製和貼上動作。</li><li>**受原則管理的應用程式**：允許在這個應用程式與其他受原則管理的應用程式之間進行剪下、複製和貼上動作。</li><li>**具有貼上的受原則管理的應用程式**：允許在這個應用程式與其他受原則管理的應用程式之間進行剪下或複製。 允許將資料從任何應用程式貼入這個應用程式。</li><li>**任何應用程式**：不限制與這個應用程式之間的剪下、複製和貼上。 | **任何應用程式** |
| <ul><ui>**任何應用程式的剪下和複製字元限制** | 指定可以從組織資料和帳戶剪下或複製的字元數。  如此可允許共用指定的字元數，除非遭到 [限制利用其他應用程式剪下、複製及貼上] 設定封鎖。<p>預設值 = 0<p>**注意**：需要 Intune 公司入口網站 5.0.4364.0 版或更新版本。  | **0** |
| **螢幕擷取和 Google 助理** | 選取 [封鎖]，在使用這個應用程式時封鎖裝置的螢幕擷取和 **Google 助理** 功能。 選擇 [允許]，也會在搭配使用這個應用程式與工作或學校帳戶時模糊應用程式切換器預覽影像。| **封鎖** |
| **核准的鍵盤**  | 選取 [需要]，然後指定此原則核准的鍵盤清單。 <p>未使用核准鍵盤的使用者會收到提示，必須下載並安裝核准的鍵盤，才能使用受保護的應用程式。 此設定需要應用程式具有 Intune SDK for Android 版本 6.2.0 或更高版本。 | **不需要** |
| <ul><ui>**選取要核准的鍵盤** | 當針對上一個選項選取 [需要] 時，可以使用這個選項。 選擇 [選取] 以管理可與受此原則保護的應用程式搭配使用的鍵盤和輸入方法清單。 您可以將其他鍵盤新增至清單，並移除任何預設選項。 您必須至少有一個核准的鍵盤，才能儲存設定。 若要新增鍵盤，請指定： <ul><li>**名稱**：識別鍵盤並向使用者顯示的易記名稱。 </li><li>**套件識別碼**：Google Play 商店中的應用程式套件識別碼。 例如，如果應用程式在 Play 商店中的 URL 為 `https://play.google.com/store/details?id=com.contoskeyboard.android.prod`，則套件識別碼為 `com.contosokeyboard.android.prod`。 此套件識別碼會以簡單的連結形式呈現給使用者，以從 Google Play 下載鍵盤。 <p><div class="NOTE"><p>注意</p><p>已指派多項應用程式防護原則的使用者，只能使用所有原則皆通用的核准鍵盤。</p> | |

### <a name="encryption"></a>加密
| 設定 | 如何使用 | 預設值 |
|------|------|------|
| **加密組織資料** | 選擇 [需要]，在這個應用程式中啟用公司或學校資料的加密。 Intune 可搭配使用 OpenSSL 256 位元 AES 加密配置與 Android 金鑰儲存區系統，安全地加密應用程式資料。 資料會在檔案 I/O 工作期間，以同步方式加密。 將一律加密裝置儲存空間上的內容。 新檔案將會以 256 位元的金鑰進行加密。 現有的 128 位元加密檔案將會針對 256 位元金鑰進行移轉嘗試，但該程序不一定會成功。 以 128 位元金鑰加密的檔案將會維持可讀取性。 <br><br> 此加密方法已通過 FIPS 140-2 驗證；如需詳細資訊，請參閱 [OpenSSL FIPS Library and Android Guide](https://wiki.openssl.org/images/7/76/OpenSSL_FIPS_Library_and_Android_Guide.pdf) (OpenSSL FIPS Library 和 Android Guide)。     |  **需要**|  
| <ul><ui>**加密已註冊之裝置上的組織資料** | 選取 [需要] 以強制在所有裝置上使用 Intune 應用程式層加密來加密組織資料。 選取 [不需要] 以不強制在已註冊的裝置上使用 Intune 應用程式層加密來加密組織資料。| **需要** |


### <a name="functionality"></a>功能
| 設定 | 如何使用 | 預設值 |
|------|------|------|
| **與原生連絡人應用程式同步應用程式** | 選擇 [封鎖]，防止應用程式將資料儲存至裝置上的原生「連絡人」應用程式。 如果您選擇 [允許]，則應用程式可以將資料儲存至裝置上的原生「連絡人」應用程式。 <br><br>當您執行選擇性抹除以移除應用程式中的工作或學校資料時，會移除直接從應用程式同步到原生「連絡人」應用程式的連絡人。 無法清除從原生通訊錄同步處理到其他外部來源的任何連絡人。 目前這僅適用於 Microsoft Outlook 應用程式。 | **允許** |
| **列印組織資料** | 選擇 [封鎖]，防止應用程式列印公司或學校資料。 如果您將此設定保留為 [允許] (預設值)，則使用者將能夠匯出及列印所有組織資料。 | **允許** |
|**限制與其他應用程式的 Web 傳輸** | 指定如何從原則受控的應用程式開啟 Web 內容 (HTTP/HTTPS 連結)。 從下列選項進行選擇： <ul><li>**任何應用程式**：允許任何應用程式中的 Web 連結。</li><li>**Intune Managed Browser**：只允許在 Intune Managed Browser 中開啟 Web 內容。 此瀏覽器為受原則管理的瀏覽器。</li><li>**Microsoft Edge**：只允許在 Microsoft Edge 中開啟 Web 內容。 此瀏覽器為受原則管理的瀏覽器。</li><li>**非受控瀏覽器**：只允許在 [非受控瀏覽器通訊協定] 設定中定義的非受控瀏覽器中開啟 Web 內容。 Web 內容在目標瀏覽器中將會是非受控。<br>**注意**：需要 Intune 公司入口網站 5.0.4415.0 版或更新版本。</li><br><br>**原則受控的瀏覽器**<br>在 Android 上，如果未安裝 Intune Managed Browser 或 Microsoft Edge，您的終端使用者可以從支援 HTTP/HTTPS 連結的其他原則受控應用程式中進行選擇。<p>如果受控瀏覽器為必要但尚未安裝，則會提示終端使用者安裝 Microsoft Edge。<p>如果原則受控的瀏覽器為必要，則 Android 應用程式連結是由 [允許應用程式將資料傳送至其他應用程式] 原則設定所管理。<p>**Intune 裝置註冊**<br>如果您使用 Intune 管理裝置，請參閱[透過 Microsoft Intune 使用受管理的瀏覽器原則管理網際網路存取](manage-microsoft-edge.md)。<p>**原則受控的 Microsoft Edge**<br>適用於行動裝置 (iOS/iPadOS 和 Android) 的 Microsoft Edge 瀏覽器支援 Intune 應用程式保護原則。 使用其公司 Azure AD 帳戶登入 Microsoft Edge 瀏覽器應用程式的使用者，將會受到 Intune 的保護。 Microsoft Edge 瀏覽器可整合應用程式 SDK，並支援其所有的資料保護原則，但會防止：<br><ul><li>**另存新檔**：Microsoft Edge 瀏覽器不允許使用者將直接的應用程式內連線新增至雲端儲存體提供者 (例如 OneDrive)。</li><li>**連絡人同步**：Microsoft Edge 瀏覽器不會儲存至原生連絡人清單。</li></ul>**注意︰** *應用程式 SDK 無法判斷目標應用程式是否為瀏覽器。在 Android 裝置上，允許支援 HTTP/HTTPS 意圖的其他 Managed Browser 應用程式。* | **未設定** |
|<ul><ui>**非受控瀏覽器** | 輸入單一瀏覽器的應用程式識別碼。 來自原則受控應用程式的 Web 內容 (http/https 連結) 將會在指定的瀏覽器中開啟。  Web 內容在目標瀏覽器中將會是非受控。 | **空白** |
|<ul><ui>**非受控瀏覽器名稱** | 輸入與 [非受控瀏覽器識別碼] 關聯之瀏覽器的應用程式名稱。 若未安裝指定的瀏覽器，將會向使用者顯示此名稱。  | **空白** |
| **組織資料通知** | 透過組織帳戶的 OS 通知，以指定要共用多少組織資料。 此原則設定會影響本機裝置和任何連線的裝置，例如穿戴式裝置和智慧型喇叭。 應用程式可能會提供其他控制項來自訂通知行為，或選擇不接受所有值。 從下列項目進行選取： <ul><li>**封鎖**：不要共用通知。</li><ul><li>如果應用程式不支援，則會允許通知。</li></ul><li>**封鎖組織資料**：不要在通知中共用組織資料。 例如，「您有新郵件」、「您有一個會議」</li><UL><li>如果應用程式不支援，則會封鎖通知。</li></ul><li>**允許**：共用通知中的組織資料</li></ul> <p>**注意**：*此設定需要應用程式支援。適用於 Android 4.0.95 或更新版本的 Outlook 支援此設定。* | **允許**   |

## <a name="data-transfer-exemptions"></a>資料傳輸豁免

Intune 應用程式保護原則可以允許豁免某些應用程式和平台服務傳送和接收資料傳輸。 例如，Android 上所有 Intune 受控應用程式都必須能夠將資料傳輸至 Google 文字轉換語音並從中傳輸資料，因此可以大聲讀出您行動裝置螢幕中的文字。 這份清單可能隨時變更，並反映視為對安全產能有所幫助的服務和應用程式。

### <a name="full-exemptions"></a>完整豁免

  這些應用程式和服務完全可以接收和傳送 Intune 管理應用程式的資料傳輸。

  |應用程式/服務名稱 | 說明 |
  | ------ | ---- |
  | com.android.phone | 原生 Phone 應用程式
  | com.android.vending | Google Play 商店 |
  | com.android.documentsui | Android 文件選擇器|
  | com.google.android.webview | [WebView](https://developer.android.com/reference/android/webkit/WebView.html)，這是許多應用程式 (包括 Outlook) 的必要項目。 |
  | com.android.webview |[WebView](https://developer.android.com/reference/android/webkit/WebView.html)，這是許多應用程式 (包括 Outlook) 的必要項目。|
  | com.google.android.tts | Google 文字轉換語音 |
  | com.android.providers.settings | Android 系統設定 |
  | com.android.settings | Android 系統設定 |
  | com.azure.authenticator | Azure Authenticator 應用程式，這是許多情況下成功驗證的必要項目。 |
  | com.microsoft.windowsintune.companyportal | Intune 公司入口網站|

### <a name="conditional-exemptions"></a>條件式豁免
  只有在特定情況下，這些應用程式和服務才能接收和傳送 Intune 管理應用程式的資料傳輸。

  |應用程式/服務名稱 | 說明 | 豁免條件|
  | ------ | ---- | --- |
  | com.android.chrome | Google Chrome 瀏覽器 | Chrome 用於 Android 7.0+ 上的一些 WebView 元件，而且絕不會隱藏，可供檢視。 不過，一律會限制接收或傳送至應用程式的資料流程。  |
  | com.skype.raider | Skype | Skype 應用程式只允許能夠使用通話的特定動作。 |
  | com.android.providers.media | Android 媒體內容提供者 | 只允許進行鈴聲選取動作的媒體內容提供者。 |
  | com.google.android.gms; com.google.android.gsf | Google Play Services 套件 | 這些套件允許用於 Google Cloud Messaging 動作 (例如推送通知)。 |
  | com.google.android.apps.maps | Google 地圖 | 允許瀏覽地址 |

如需詳細資訊，請參閱[應用程式的資料傳輸原則例外狀況](app-protection-policies-exception.md)。

## <a name="access-requirements"></a>存取需求

| 設定 | 如何使用 |  
|------|------| 
| **PIN 以進行存取** | 選取 [需要]，要求 PIN 來使用此應用程式。 使用者第一次在工作或學校內容中執行應用程式時，系統會提示他們設定這個 PIN。 <br><br> 預設值 = **需要**<br><br> 您可以使用PIN 以進行存取區段底下可用的設定，設定 PIN 強度。
| <ul><ui>**PIN 類型** | 先設定數值或密碼類型的 PIN 需求，再存取已套用應用程式保護原則的應用程式。 數值需求只有數字，密碼則至少要以 1 個字母**或**至少要以 1 個特殊字元定義。 <br><br> 預設值 = **數值**<br><br> **注意︰** 允許的特殊字元包括 Android 英文鍵盤上的特殊字元和符號。 |
| <ul><ui> **簡單的 PIN** | 選取 [允許]，允許使用者使用簡單的 PIN 序列 (例如 *1234*、*1111*、*abcd* 或 *aaaa*)。 選取 [封鎖]，防止其使用簡單的序列。 系統會在 3 字元滑動視窗中檢查簡單序列。 如果設定了 [區塊]，系統就不接受終端使用者將 PIN 設定為 1235 或 1112，但允許 1122。 <br><br>預設值 = **允許** <br><br>**注意︰** 如果已設定密碼類型 PIN，而且 [簡單的 PIN] 已設定為 [允許]，則使用者的 PIN 中需要至少有一個字母**或**至少一個特殊字元。 如果已設定密碼類型 PIN，且 [簡單的 PIN] 已設定為 [封鎖]，則使用者的 PIN 中需要至少一個數字**和**一個字母**以及**至少一個特殊字元。 </li> |
| <ul><ui> **選取 PIN 長度下限** | 指定 PIN 序列的最小位數。 <br><br>預設值 = **4** | 
| <ul><ui> **指紋而非 PIN 以進行存取 (Android 6.0+)** | 選取 [允許]，允許使用者使用[指紋驗證](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication)而非 PIN 以進行應用程式存取。 <br><br>預設值 = **允許** <br><br>**注意︰** 此功能支援 Android 裝置上的生物特徵辨識通用控制項。 「不支援」OEM 特定的生物特徵辨識設定，例如 Samsung Pass。 <br><br>在 Android 上，您可以讓使用者使用 [Android 指紋驗證](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication)而非 PIN 來證明其身分識別。 使用者嘗試使用自己的公司或學校帳戶來使用這個應用程式時，系統會提示他們提供自己的指紋識別，而不是輸入 PIN。 <br><br> 已註冊 Android 工作設定檔的裝置必須註冊個別指紋，才能強制執行**指紋而非 PIN 以進行存取**原則。 此原則僅針對 Android 工作設定檔中安裝的原則管理應用程式生效。 藉著在公司入口網站中註冊而建立 Android 工作設定檔之後，個別指紋必須在裝置上註冊。 如需使用 Android 工作設定檔的工作設定檔指紋詳細資訊，請參閱[鎖定您的工作資料夾](https://support.google.com/work/android/answer/7029958)。 |
| <ul><ui>**逾時後以 PIN 覆寫指紋**| 若要使用此設定，請選取 [需要]，然後設定非使用狀態逾時。 <br><br>預設值 = **需要** |
| <ul><ui><ul><ui> **逾時 (非使用狀態分鐘數)**| 指定密碼或數字 (依設定) PIN 將會覆寫使用指紋的時間 (分鐘)。 此逾時值應該大於在 [重新檢查存取需求前的剩餘時間 (分鐘)] 下指定的值。<br><br>預設值 = **30** |
| <ul><ui>**在數天後重設 PIN** | 選取 [是]，要求使用者在設定的一段時間 (以天為單位) 後變更其應用程式 PIN。  <br><br>當設定為 [是] 時，您可以接著設定需要重設 PIN 前的經過天數。 <br><br> 預設值 = 否  |  
| <ul><ui><ul><ui> **天數** | 設定需要重設 PIN 前的經過天數。 <br><br> 預設值 = **90**  |
| <ul><ui>**選取要維護的先前 PIN 值數目** | 此設定會指定 Intune 將維護的先前 PIN 數目。 所有新的 PIN 都必須不同於 Intune 所維護的 PIN。 <br><br> 預設值 = **0** | 
| <ul><ui>**設定裝置 PIN 時的應用程式 PIN** | 選取 [不需要]，在設定公司入口網站的已註冊裝置上偵測到裝置鎖定時，停用應用程式 PIN。 <br><br> 預設值 = **需要**。 | 
| **公司或學校帳戶認證以進行存取** | 選擇 [需要]，要求使用者使用其公司或學校帳戶登入以進行應用程式存取，而不是輸入 PIN。 當設定為 [需要] 且已開啟 PIN 或生物特徵辨識提示時，會顯示公司認證以及 PIN 或生物特徵辨識提示。 <br><br>預設值 = **不需要** |
| **重新檢查存取需求前的經過時間 (非使用中狀態分鐘數)** | 進行下列設定： <ul><li>**逾時**︰這是重新檢查存取需求 (稍早定義於原則中) 前經過的分鐘數。 例如，若管理員在原則中開啟 PIN 及「封鎖已 Root 破解的裝置」，則當使用者開啟 Intune 受控應用程式時，就必須輸入 PIN 並在未 Root 破解的裝置上使用應用程式。 當使用這項設定時，使用者在等於設定值的時段內都不需要在任何 Intune 受控應用程式上輸入 PIN 或接受另一次 Root 偵測檢查。  <br><br>此原則設定格式支援正整數。 <br><br> 預設值 = **30 分鐘** <br><br> **注意︰** 在 Android 上，PIN 會在所有 Intune 受控應用程式間共用。 當裝置上的應用程式離開前景時，PIN 計時器就會重設。 在此設定中所定義的逾時持續時間內，使用者不需要在任何共用 PIN 的 Intune 受控應用程式上輸入 PIN。 <br><br></li> |

> [!NOTE]  
> 若要深入了解在同一應用程式和使用者集合的 [存取] 區段中設定的多個 Intune 應用程式保護設定如何在 Android 上運作，請參閱 [Intune MAM 常見問題集](mam-faq.md)與[在 Intune 中使用應用程式防護原則的存取動作選擇性地抹除資料](app-protection-policies-access-actions.md)。


## <a name="conditional-launch"></a>條件式啟動
設定條件式啟動設定，以設定您存取保護原則的登入安全性需求。 

根據預設，有數個設定會提供預先設定的值和動作。 您可以刪除某些設定，例如「最低 OS 版本」。 您也可以從 [選取一個] 下拉式清單中選取其他設定。 

| 設定 | 如何使用 |  
|---------|------------| 
| **PIN 嘗試次數上限** | 指定在執行已設定動作之前，使用者必須成功輸入 PIN 的嘗試次數。 此原則設定格式支援正整數。 「動作」包括： <br><ul><li>**重設 PIN** - 使用者必須重設其 PIN。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。  </li></ul> </li></ul> 預設值 = **5** |
| **離線寬限期** | MAM 應用程式可以離線執行的分鐘數。 指定經過多少時間 (分鐘) 之後即會重新檢查應用程式存取需求。 「動作」包括： <br><ul><li>**封鎖存取 (分鐘)** ：MAM 應用程式可以離線執行的分鐘數。 指定經過多少時間 (分鐘) 之後即會重新檢查應用程式存取需求。 在這段期間過後，應用程式必須進行 Azure Active Directory (Azure AD) 的使用者驗證，如此應用程式才能繼續執行。 <br><br>此原則設定格式支援正整數。 <br><br>預設值 = **720** 分鐘 (12 小時) </li></ul> <ul><li>**抹除資料 (天)** - 在離線執行達到此天數 (由系統管理員定義) 之後，應用程式需要使用者連線到網路並重新驗證。 如果使用者成功驗證，就可以繼續存取其資料，而且會重設離線間隔。  如果使用者無法驗證，應用程式會執行使用者帳戶和資料的選擇性抹除。 如需詳細資訊，請參閱[如何只抹除 Intune 管理之應用程式中的公司資料](apps-selective-wipe.md)。</li></ul> 此原則設定格式支援正整數。 <br><br>  預設值 = **90 天** </li></ul> <br><br>  此項目可以出現多次，每個執行個體支援不同的動作。 |   
| **已越獄或 Root 破解的裝置** |這項設定沒有可設定的值。 「動作」包括： <br><ul><li>**封鎖存取** - 防止在已越獄或 Root 破解的裝置上執行此應用程式。 使用者仍然可以繼續使用這個應用程式來執行個人工作，但必須使用不同裝置來存取這個應用程式中的工作或學校資料。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。  </li></ul> |
| **最低 OS 版本** | 指定要求使用此應用程式的最低 Android 作業系統。 「動作」包括： <br><ul><li>**警告** - 如果裝置上的 Android 版本不符合需求，使用者將會看見通知。 此通知可以關閉。  </li></ul> <ul><li>**封鎖存取** - 如果裝置上的 Android 版本不符合需求，將會禁止使用者存取。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。  </li></ul> </li></ul>此原則設定格式支援 major.minor、major.minor.build、major.minor.build.revision。 |
| **最低應用程式版本** | 指定作業系統最小值。 「動作」包括： <br><ul><li>**警告** - 如果裝置上的應用程式版本不符合需求，使用者會看見通知。 此通知可以關閉。</li></ul> <ul><li>**封鎖存取** - 如果裝置上的應用程式版本不符合需求，會封鎖使用者進行存取。 </li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。 </li></ul> </li></ul> 因為應用程式之間通常會有不同的版本控制配置，所以請建立包含一個針對單一應用程式之最低應用程式版本的原則 (例如，「Outlook 版本原則」)。<br><br> 此項目可以出現多次，每個執行個體支援不同的動作。<br><br> 此原則設定格式支援 major.minor、major.minor.build、major.minor.build.revision。<br><br> 此外，您可以設定終端使用者可從**何處**取得企業營運 (LOB) 應用程式的更新版本。 終端使用者將可在 [應用程式最小版本] 條件式啟動對話方塊中看見此功能，其將提示終端使用者更新為 LOB 應用程式的最小版本。 在 Android 上，此功能會使用公司入口網站。 若要設定終端使用者應該更新 LOB 應用程式的位置，應用程式需要使用金鑰 `com.microsoft.intune.myappstore` 傳送給它的受控[應用程式設定原則](app-configuration-policies-managed-app.md)。 傳送的值將定義終端使用者要從哪個存放區下載應用程式。 如果透過公司入口網站部署應用程式，則值必須為 `CompanyPortal`。 針對任何其他存放區，您必須輸入完整的 URL。 |
| **最低修補程式版本** | 要求裝置具有由 Google 發行的最低 Android 安全性修補程式。  <br><ul><li>**警告** - 如果裝置上的 Android 版本不符合需求，使用者將會看見通知。 此通知可以關閉。  </li></ul> <ul><li>**封鎖存取** - 如果裝置上的 Android 版本不符合需求，將會禁止使用者存取。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。  </li></ul></li></ul> 此原則設定支援 *YYYY-MM-DD* 的日期格式。 |
| **裝置製造商** | 指定以分號分隔的製造商清單。 這些值不會區分大小寫。 「動作」包括： <br><ul><li>**允許指定 (封鎖非指定)** - 僅有符合指定製造商的裝置可以使用應用程式。 會封鎖所有其他裝置。 </li></ul> <ul><li>**允許指定 (抹除非指定)** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。 </li></ul> 如需使用此設定的詳細資訊，請參閱[條件式啟動動作](app-protection-policies-access-actions.md#android-policy-settings)。 |
| **SafetyNet 裝置證明** | 應用程式保護原則支援 Google Play Protect 的部分 API。 特別的是，此設定會在終端使用者裝置上設定 Google 的 SafetyNet 證明。 指定 [基本完整性] 或是 [基本完整性和經認證的裝置]。 [基本完整性] 會告訴您有關裝置的一般完整性。 Root 破解的裝置、模擬器、虛擬裝置，以及具有竄改跡象的裝置都無法通過基本完整性。 [基本完整性和經認證的裝置] 會告訴您有關裝置與 Google 服務的相容性。 只有經過 Google 認證且未修改的裝置可以通過這項檢查。 「動作」包括： <br><ul><li>**警告** - 如果裝置不符合根據所設定值的 Google SafetyNet 證明掃描，使用者會看到通知。 此通知可以關閉。 </li></ul><ul><li>**封鎖存取** - 如果裝置不符合根據所設定值的 Google SafetyNet 證明掃描，使用者會遭到封鎖存取。 </li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。 </li></ul> </li></ul> 如需此設定相關的常見問題集，請參閱[關於 MAM 和應用程式防護的常見問題集](mam-faq.md#app-experience-on-android)。 |
| **需要對應用程式進行威脅掃描** | 應用程式保護原則支援 Google Play Protect 的部分 API。 此設定尤其可確保 Google 的驗證應用程式掃描已針對終端使用者裝置開啟。 如果設定，終端使用者將會遭到封鎖存取，直到他們在其 Android 裝置上開啟 Google 的應用程式掃描為止。 「動作」包括： <br><ul><li>**警告** - 如果裝置上的 Google 驗證應用程式掃描未開啟，使用者會看到通知。 此通知可以關閉。 </li></ul><ul><li>**封鎖存取** - 如果裝置上的 Google 驗證應用程式掃描未開啟，使用者會遭到封鎖存取。 </li></ul></li></ul> Google 驗證應用程式掃描結果會顯示在主控台中的 [可能有害的應用程式] 報表。 |
| **最低公司入口網站版本** | 透過使用 [最低公司入口網站版本]，您可以指定在終端使用者裝置上強制要求公司入口網站的特定最小定義版本。 此條件式啟動設定可讓您將值設定為 [封鎖存取]、[抹除資料]，與 [警告]，作為未符合每個值時的可能動作。 此值的可能格式遵循模式 [主要].[次要]、[主要].[次要].[組建] 或 [主要].[次要].[組建].[修訂]。 由於某些使用者可能不想立即強制更新應用程式，[警告] 選項可能是此設定的理想選項。 Google Play 商店可以只傳送應用程式更新的差異位元組，但這可能仍然是大量資料，如果更新時使用者使用的是行動數據，他們可能不會想要使用這些資料。 強制更新並因此下載更新的應用程式，可能會在更新時產生未預期的行動數據費用。 如需詳細資訊，請參閱 [Android 原則設定](app-protection-policies-access-actions.md#android-policy-settings)。 |
| **允許的裝置威脅等級上限** | 應用程式保護原則可以利用 Intune-MTD 連接器。 指定使用此應用程式可接受的最大威脅等級。 威脅取決於您在終端使用者裝置上選擇的 Mobile Threat Defense (MTD) 廠商應用程式。 指定 [安全]、[低]、[中] 或 [高]。 [安全] 要求裝置上沒有威脅，而且是最嚴格的可設定值，而 [高] 基本上需要作用中的 Intune 對 MTD 連線。 「動作」包括： <br><ul><li>[封鎖存取] - 如果終端使用者裝置上由您選擇的 Mobile Threat Defense (MTD) 廠商應用程式所決定的威脅等級不符合此需求，將會封鎖使用者進行存取。</li></ul> <ul><li>**抹除資料** - 與應用程式建立關聯的使用者帳戶會從裝置抹除。</li></ul>如需使用此設定的詳細資訊，請參閱[在 Intune 中針對尚未註冊的裝置啟用 Mobile Threat Defense 連接器](../protect/mtd-enable-unenrolled-devices.md)。 |
