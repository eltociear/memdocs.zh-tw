---
title: 使用 Intune 管理 iOS 與 Android 版 Edge
titleSuffix: ''
description: 使用 iOS 與 Android 版 Edge 的 Intune 應用程式保護原則來確保一律使用適當的安全性措施保護公司網站的存取。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad0a886aba8e1966e47e9ea11c99cb97c35c4f5a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988384"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>透過搭配 Microsoft Intune 使用 iOS 與 Android 版 Edge 來管理 Web 存取

iOS 與 Android 版 Edge 是設計用來讓使用者瀏覽 Web 並支援多重身分識別。 使用者可以新增工作帳戶與個人帳戶以進行瀏覽。 這兩個身分識別之間有完整的分隔，就像其他 Microsoft 行動裝置應用程式中所提供的一樣。

iOS 12.0 與更新版本支援 iOS 版 Edge。 Android 5 與更新版本支援 Android 版 Edge。

> [!NOTE]
> iOS 與 Android 版 Edge 不會使用使用者在其裝置上針對原生瀏覽器所做的設定，因為 iOS 與 Android 版 Edge 無法存取這些設定。

當您訂閱 Enterprise Mobility + Security 套件 (包括 Microsoft Intune 與 Azure Active Directory Premium 功能，例如條件式存取) 時，可以使用 Office 365 資料最豐富且最廣泛的保護功能。 您至少會想要部署條件式存取原則，只允許從行動裝置連線到 iOS 與 Android 版 Edge，以及可確保瀏覽體驗受到保護的 Intune 應用程式保護原則。

> [!NOTE]
> 需要在受保護的瀏覽器中開啟時，新的 Web 剪輯 (釘選的 Web 應用程式) 將會在 iOS 與 Android 版 Edge (而不是 Intune Managed Browser) 中開啟。 針對較舊的 iOS Web 剪輯，您必須為這些 Web 剪輯重定目標，以確保其會在 iOS 與 Android 版 Edge (而非 Managed Browser) 中開啟。

## <a name="apply-conditional-access"></a>套用條件式存取
組織可以使用 Azure AD 條件式存取原則來確保使用者只能使用 iOS 與 Android 版 Edge 來存取公司或學校內容。 若要這樣做，您將需要以所有潛在使用者為目標的條件式存取原則。 如需有關如何建立此原則的詳細資料，請參閱[需要應用程式保護原則，以使用條件式存取來存取雲端應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access) \(部分機器翻譯\)。

1. 遵循[案例 2：瀏覽器應用程式需要具有應用程式保護原則的已核准應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies)，這允許 iOS 與 Android 版 Edge，但會封鎖其他行動裝置網頁瀏覽器，使其無法連線到 Office 365 端點。

   >[!NOTE]
   > 此原則可確保行動裝置使用者可以從 iOS 與 Android 版 Edge 存取所有 Office 365 端點。 此原則也會防止使用者使用 InPrivate 來存取 Office 365 端點。

使用條件式存取時，您也能以透過 [Azure AD 應用程式 Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) 公開給外部使用者的內部部署網站為目標。

## <a name="create-intune-app-protection-policies"></a>建立 Intune 應用程式保護原則

應用程式保護原則 (APP) 定義允許哪些應用程式，以及其可以對組織資料採取的動作。 APP 中可用的選擇可讓組織針對其特定需求量身訂作保護方案。 針對一些組織，實作完整案例需要哪種原則設定可能不是那麼明顯。 為了協助組織排定行動用戶端端點強化的優先順序，Microsoft 引進了適用於 iOS 與 Android 行動裝置應用程式管理的應用程式資料保護架構分類法。

應用程式資料保護架構會組織成三個不同的設定層級，每個層級都以前一層為基礎而建置：

- **企業基本資料保護** (層級1) 可確保應用程式使用 PIN 來保護並加密，並執行選擇性抹除作業。 針對 Android 裝置，此層級會驗證 Android 裝置證明。 這是一種入門級設定，可在 Exchange Online 信箱原則中提供類似的資料保護控制，並將 IT 與使用者人口引進 APP。
- **企業增強的資料保護** (層級2) 引進應用程式資料洩露防護機制與最低 OS 需求。 此設定適用於大部分存取公司或學校資料的行動使用者。
- **企業高資料保護** (層級3) 引進進階資料保護機制、增強的 PIN 設定，以及 APP 行動威脅防禦。 對於存取高風險資料的使用者而言，這是理想的設定。

若要查看必須保護之每個設定層級與最低應用程式的特定建議，請參閱[使用應用程式保護原則的資料保護架構](app-protection-framework.md)。

無論裝置是否已在聯合式端點管理 (UEM) 解決方案中註冊，都必須使用[如何建立及指派應用程式保護原則](app-protection-policies.md)中的步驟，為 iOS 與 Android 應用程式建立 Intune 應用程式保護原則。 這些原則至少必須符合下列條件：

1. 其包含所有 Microsoft 行動裝置應用程式，例如 Outlook、OneDrive、Office 或 Teams ，因為這可確保使用者能夠以安全的方式存取及操作任何 Microsoft 應用程式中的公司或學校資料。

2. 其會指派給所有使用者。 這可確保所有使用者都受到保護，不論他們是否使用 iOS 或 Android 版 Edge。

3. 判斷哪一個架構層級符合您的需求。 大部分的組織都應該實作 **Enterprise 增強的資料保護** (層級 2) 中所定義的設定，因為這樣可啟用資料保護與存取需求控制。

如需有關可用設定的詳細資訊，請參閱 [Android 應用程式保護原則設定](app-protection-policy-settings-android.md)與 [iOS 應用程式保護原則設定](app-protection-policy-settings-ios.md)。

> [!IMPORTANT]
> 若要針對未在 Intune 中註冊之 Android 裝置上的應用程式套用 Intune 應用程式保護原則，使用者也必須安裝 Intune 公司入口網站。 如需詳細資訊，請參閱[當 Android 應用程式交由應用程式保護原則管理時的行為](../fundamentals/end-user-mam-apps-android.md)。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>在被原則保護的瀏覽器中針對已連線至 Azure AD 的 Web 應用程式使用單一登入

iOS 與 Android 版 Edge 可以針對所有已連線至 Azure AD 的 Web 應用程式 (SaaS 與內部部署) 利用單一登入 (SSO)。 SSO 可讓使用者透過 iOS 與 Android 版 Edge 存取已連線至 Azure AD 的 Web 應用程式，而不必重新輸入其認證。

SSO 要求裝置必須註冊 iOS 裝置的 Microsoft Authenticator 應用程式或 Android 上 Intune 公司入口網站應用程式。 當使用者具備上述其中一項時，系統會在他們在受原則保護的瀏覽器中移至已連線至 Azure AD 的 Web 應用程式時通知他們註冊其裝置 (只有當其裝置尚未註冊時才會發出此通知)。 使用 Intune 所管理的使用者帳戶註冊裝置之後，該帳戶便會針對已連線至 Azure AD 的 Web 應用程式啟用 SSO。

> [!NOTE]
> 裝置註冊是使用 Azure AD 服務的簡單簽入。 它不需要完整裝置註冊，且不會在該裝置上授與 IT 人員額外的權限。

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>利用應用程式設定來管理瀏覽體驗

iOS 與 Android 版 Edge 支援允許聯合式端點管理 (如 Microsoft 端點管理員) 的應用程式設定，可讓系統管理員自訂應用程式的行為。

應用程式設定可以透過已註冊裝置上的行動裝置管理 (MDM) OS 通道 (適用於 iOS 的[受控應用程式設定](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) \(英文\) 或適用於 Android 的 [ Android in the Enterprise](https://developer.android.com/work/managed-configurations) \(英文\) 通道) 或透過 Intune 應用程式保護原則 (APP) 通道來傳遞。 iOS 與 Android 版 Edge 支援下列設定案例：

- 只允許公司或學校帳戶
- 一般應用程式組態設定
- 資料保護設定

> [!IMPORTANT]
> 針對要求在 Android 進行裝置註冊的設定案例，裝置必須在 Android Enterprise 中註冊，而且必須透過受控 Google Play 商店部署 Android 版 Edge。 如需詳細資訊，請參閱[設定 Android Enterprise 工作設定檔裝置的註冊](../enrollment/android-work-profile-enroll.md)與[為受控的 Android Enterprise 裝置新增應用程式設定原則](app-configuration-policies-use-android.md)。

每個設定案例都會強調其特定需求。 例如，設定案例是否要求進行裝置註冊，因此可與任何 UEM 提供者搭配運作，或要求 Intune 應用程式保護原則。

> [!NOTE]
> 使用 Microsoft 端點管理員時，透過 MDM OS 通道傳遞的應用程式設定稱為**受控裝置** 應用程式組態原則 (ACP)；透過應用程式保護原則通道提供的應用程式設定稱為**受控應用程式**應用程式組態原則。

## <a name="only-allow-work-or-school-accounts"></a>只允許公司或學校帳戶

尊重我們最大規模且高度管制之客戶的資料安全性和合規性政策，是 Microsoft 365 價值的關鍵要件。 有些公司需要在公司環境內擷取所有通訊資訊，以及確保裝置僅可用於公司通訊。 為了支援這些需求，可將已註冊裝置上的 iOS 與 Android 版 Edge 設定為只允許在應用程式內佈建單一公司帳戶。

您可以在這裡深入了解如何設定組織允許的帳戶模式設定：

- [Android 設定](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS 設定](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

此設定案例僅適用於已註冊的裝置。 不過，支援任何 UEM 提供者。 如果您不是使用 Microsoft 端點管理員，則需要參閱您的 UEM 文件，以了解如何部署這些設定金鑰。

## <a name="general-app-configuration-scenarios"></a>一般應用程式設定案例

iOS 與 Android 版 Edge 可讓系統管理員為數個應用程式內設定自訂預設設定。 目前只有當 iOS 與 Android 版 Edge 已將 Intune 應用程式保護原則套用至已登入應用程式的公司或學校帳戶時，才會提供此功能。

> [!IMPORTANT]
> Android 版 Edge 不支援受控 Google Play 中提供的 Chromium 設定。

Edge 支援下列組態設定：

- 新的索引標籤頁面體驗
- 書籤體驗
- 應用程式行為體驗
- Kiosk 模式體驗

無論裝置註冊狀態為何，這些設定都可以部署到應用程式。

### <a name="new-tab-page-experiences"></a>新的索引標籤頁面體驗

iOS 與 Android 版 Edge 為組織提供數個調整新索引標籤頁面體驗的選項。

#### <a name="organization-logo-and-brand-color"></a>組織標誌與品牌色彩

這些設定可讓您自訂 iOS 與 Android 版 Edge 的新索引標籤頁面，以顯示您組織的標誌與品牌色彩作為頁面背景。

若要上傳您組織的標誌與色彩，請先完成下列步驟：
1. 在 [Microsoft 端點管理員](https://endpoint.microsoft.com)中，瀏覽至 [租用戶系統管理] -> [自訂] -> [公司身分識別商標]。
2. 若要設定品牌的標誌，請在 [在標題中顯示] 旁，選擇 [僅組織標誌]。 建議使用透明背景標誌。
3. 若要設定您品牌的背景色彩，請選取 [佈景主題色彩]。 iOS 與 Android 版 Edge 會在新索引標籤頁面上套用較淺的色彩著色，以確保頁面具有高可讀性。

接下來，使用下列機碼/值組，將您的組織商標套用到 iOS 與 Android 版 Edge：

|    機碼    |    值    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **true** 會顯示組織的品牌標誌<br>**false** (預設值) 將不會公開標誌    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **true** 會顯示組織的品牌色彩<br>**false** (預設值) 將不會公開色彩    |

#### <a name="homepage-shortcut"></a>首頁捷徑

此設定可讓您設定 iOS 與 Android 版 Edge 的首頁捷徑。 當使用者在 iOS 與 Android 版 Edge 中開啟新索引標籤時，您設定的首頁捷徑會成為搜尋列下方第一個圖示。 使用者在其受控內容中無法編輯或刪除這個捷徑。 首頁捷徑會顯示您組織的名稱，以區分該捷徑。 

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    指定有效的 URL。 基於安全性考量，會封鎖不正確的 URL。<br>例如：`https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>多個熱門網站捷徑

如同設定首頁捷徑，您也可以在 iOS 與 Android 版 Edge 中的新索引標籤頁面上設定多個熱門網站捷徑。 使用者在受控內容中無法編輯或刪除這些捷徑。 注意：您最多可以設定 8 個捷徑 (包含首頁捷徑)。 如果您設定了首頁捷徑，則該捷徑將會覆寫先前設定的第一個網站。 

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    指定一組值 URL。 每個熱門網站捷徑都會包含一個標題與 URL。 請使用 `|` 字元來分隔標題和 URL。<br>例如：`GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>產業新聞

您可以在 iOS 與 Android 版 Edge 中設定新索引標籤頁面體驗，以顯示與您組織相關的產業新聞。 當您啟用此功能時，iOS 與 Android 版 Edge 會使用您組織的網域名稱，從網路彙總您的組織、組織產業與競爭者的相關新聞，讓您的使用者可以從 iOS 與 Android 版 Edge 的集中式新索引標籤頁面中找到所有相關外部新聞。 產業新聞預設為關閉。 

|    機碼    |    值    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **true** 會在新索引標籤頁面上顯示產業新聞<br>**False** (預設值) 將會在新索引標籤頁面上隱藏產業新聞    |

### <a name="bookmark-experiences"></a>書籤體驗

iOS 與 Android 版 Edge 為組織提供數個管理書籤的選項。

#### <a name="managed-bookmarks"></a>受控書籤

為了方便存取，您可以設定想讓使用者在使用 iOS 與 Android 版 Edge 時可用的書籤。

- 書籤只會出現在公司或學校帳戶中，而不會公開至個人帳戶。
- 使用者無法刪除或修改書籤。
- 書籤會顯示在清單頂端。 使用者所建立的書籤都會顯示在這些書籤下方。
- 如果您已啟用應用程式 Proxy 重新導向，即可使用應用程式 Proxy Web 應用程式的內部或外部 URL 來新增這些應用程式 Proxy Web 應用程式。
- 確定您在清單中輸入 UTL 時，已在所有 URL 中加上 **http://** 或 **https://** 的前置詞。
- 書籤會放在以 Azure Active Directory 中定義之組織名稱命名的資料夾中。

|    機碼    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    此設定值是書籤清單。 每個書籤都是由書籤標題和書籤 URL 所組成。 請使用 `|` 字元來分隔標題和 URL。<br> 例如：`Microsoft Bing|https://www.bing.com`<p>若要設定多個書籤，請以雙引號字元 `||` 分隔每組配對。<br>例如：<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>我的應用程式書籤

根據預設，使用者會在 iOS 與 Android 版 Edge 內的組織資料夾內設定 [我的應用程式書籤]。

|    機碼    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true** (預設值) 會在 iOS 與 Android 版 Edge 書籤內顯示 [我的應用程式]<br>**false** 會在 iOS 與 Android 版 Edge 隱藏 [我的應用程式]    |

### <a name="app-behavior-experiences"></a>應用程式行為體驗

iOS 與 Android 版 Edge 為組織提供數個管理應用程式行為的選項。

#### <a name="default-protocol-handler"></a>預設通訊協定處理常式

根據預設，當使用者未在 URL 中指定通訊協定時，iOS 與 Android 版 Edge 會使用 HTTPS 通訊協定處理常式。 一般而言，這是最佳做法，但您也可以加以停用。

|    機碼    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **true** (預設值) 預設通訊協定處理常式是 HTTPS<br>**false** 預設通訊協定處理常式是 HTTP     |

#### <a name="disable-data-sharing-for-personalization"></a>停用資料共用以進行個人化

根據預設，iOS 與 Android 版 Edge 會提示使用者同意使用狀況資料收集並共用瀏覽歷程記錄，以將其瀏覽體驗個人化。 組可以透過防止此提示顯示給終端使用者，以停用此資料共用。

|    機碼    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **true** 會停用此提示，使其無法向終端使用者顯示<br>**false** (預設值) 會提示使用者共用使用狀況資料    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **true** 會停用此提示，使其無法向終端使用者顯示<br>**false** (預設值) 會提示使用者共用瀏覽歷程記錄     |

#### <a name="disable-specific-features"></a>停用特定功能

iOS 與 Android 版 Edge 可讓組織停用預設啟用的特定功能。 若要停用這些功能，請進行下列設定：

|    機碼    |    值    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password** 會停用儲存終端使用者密碼的提示<br>**inprivate** 會停用 InPrivate 瀏覽<p>若要停用多項功能，請使用 `|` 來分隔值。 例如，`inprivate|password` 可同時停用 InPrivate 與密碼儲存。     |

> [!NOTE]
> Android 版 Edge 不支援停用密碼管理員。

#### <a name="disable-extensions"></a>停用延伸模組

您可以停用 Android 版 Edge 內的延伸模組架構，以防止使用者安裝任何應用程式延伸模組。 若要執行此動作，請進行下列設定：

|    機碼    |    值    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **true** 會停用延伸模組架構<br>**false** (預設值) 會啟用延伸模組架構    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Android 裝置上的 Kiosk 模式體驗

您可以使用下列設定，將 Android 版 Edge 啟用為 Kiosk 應用程式：

|    機碼    |    值    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **true** 會啟用 Android 版 Edge 的 Kiosk 模式<br>**false** (預設值) 會停用 Kiosk 模式    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **true** 會在 Kiosk 模式中顯示網址列<br> **false** (預設值) 會在 Kiosk 模式中隱藏網址列    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **true** 會在 Kiosk 模式中顯示底部動作列<br> **false** (預設值) 會在 Kiosk 模式中隱藏底部列    |

## <a name="data-protection-app-configuration-scenarios"></a>資料保護應用程式設定案例

當應用程式由 Microsoft 端點管理員管理且 Intune 應用程式保護原則已套用到已登入應用程式的公司或學校帳戶時，iOS 與 Android 版 Edge 支援下列資料保護設定的應用程式設定原則：

- 管理帳戶同步
- 管理受限制的網站
- 管理 Proxy 設定
- 管理 NTLM 單一登入網站

無論裝置註冊狀態為何，這些設定都可以部署到應用程式。

### <a name="manage-account-synchronization"></a>管理帳戶同步

根據預設，Microsoft Edge 同步可讓使用者在其登入的所有裝置上存取其瀏覽資料。 同步支援的資料包括：

- 我的最愛
- 密碼
- 地址等 (自動填入表單輸入)

同步功能是透過使用者同意啟用，而且使用者可以針對上面列出的每個資料類型開啟或關閉同步。 如需詳細資訊，請參閱 [Microsoft Edge 同步](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync)。

組織可以停用 iOS 與 Android 上的 Edge 同步。 

|機碼  |值  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**true** (預設值) 會允許 Edge 同步<br>**false** 會停用 Edge 同步          |

### <a name="manage-restricted-web-sites"></a>管理受限制的網站

組織可以定義使用者在 iOS 與 Android 版 Edge 中使用公司或學校帳戶時可以存取哪些網站。 如果您使用允許清單，使用者將只能存取明確列出的網站。 如果您使用封鎖的清單，使用者將能夠存取明確封鎖之網站以外的所有網站。 您只應該強制允許或封鎖清單，而不應該同時使用兩者。 如果您同時強制兩者，系統只會採用允許清單。

組織也會定義當使用者嘗試瀏覽至受限制的網站時會發生什麼事。 根據預設，會允許轉換。 如果組織允許，受限制的網站可以在個人帳戶內容、Azure AD 帳戶的 InPrivate 內容中開啟，或是否完全封鎖網站。 如需支援之各種案例的詳細資訊，請參閱 [Microsoft Edge 行動裝置版中的受限網站轉換](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333) \(英文\)。 透過允許轉換體驗，組織的使用者會保持受保護狀態，同時確保公司資源的安全。

> [!NOTE]
> iOS 與 Android 版 Edge 只有在直接存取網站時，才能封鎖對網站的存取。 它不會在使用者使用中繼服務 (例如翻譯服務) 來存取網站時封鎖存取。

請使用下列機碼/值組來為 iOS 與 Android 版 Edge 設定允許或封鎖的網站清單。 

|機碼  |值  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |金鑰的相對應值為 URL 清單。 您能以單一值的方式輸入要允許的所有 URL，並使用垂直線 `|` 字元分隔。<p>**範例：**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |金鑰的相對應值為 URL 清單。 您能以單一值的方式輸入要封鎖的所有 URL，並使用垂直線 `|` 字元分隔。<br>**範例：**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**true** (預設值) 允許 iOS 與 Android 版 Edge 轉換限制的網站。 當個人帳戶未停用時，系統會提示使用者切換到個人上下文以開啟限制的網站，或新增個人帳戶。 如果 com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked 設定為 true，使用者將能在 InPrivate 模式中開啟限制的網站。<p>**false** 會防止 iOS 與 Android 版 Edge 轉換使用者。 使用者只會看見說明其所嘗試存取網站已封鎖的訊息。         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**true** 會允許在 Azure AD 帳戶的 InPrivate 模式中開啟限制的網站。 如果該 Azure AD 帳戶是 iOS 與 Android 版 Edge 中設定的唯一帳戶，則會在 InPrivate 模式中自動開啟限制的網站。 如果使用者已設定個人帳戶，系統會提示使用者在開啟 InPrivate 或切換至個人帳戶之間進行選擇。<p> **false** (預設值) 會要求在使用者的個人帳戶中開啟限制的網站。 若個人帳戶已停用，則會封鎖網站。<p>為了讓此設定生效，com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock 必須設定為 true。          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | 輸入使用者會看到點心棒通知「連結已使用 InPrivate 模式開啟。 您的組織要求必須使用 InPrivate 模式來存取此內容。」的秒數。 根據預設，點心棒通知會顯示 7 秒。

無論定義的允許清單或封鎖清單設定為何，一律允許下列網站：
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>適用於允許和封鎖網站清單的 URL 格式 

您可以使用各種不同 URL 格式來建置您的允許/封鎖網站清單。 下表會詳細說明這些允許的模式。

- 確定您在清單中輸入 UTL 時，已在所有 URL 中加上 **http://** 或 **https://** 的前置詞。
- 您可以根據下列許可模式清單中的規則，來使用萬用字元符號 (\*)。
- 萬用字元只能比對主機名稱的整個元件 (以句點分隔) 或路徑的整個部分 (以正斜線分隔)。 例如，**不**支援 `http://*contoso.com`。
- 您可以在位址中指定連接埠號碼。 如不指定連接埠號碼，會使用下列值：
  - 針對 http 使用連接埠 80
  - 針對 https 使用連接埠 443
- **不**支援對連接埠號碼使用萬用字元。 例如，不支援 `http://www.contoso.com:*` 和 `http://www.contoso.com:*/`。 

    |    URL    |    詳細資料    |    相符項    |    不符合    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    比對單一頁面    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    比對單一頁面    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    比對所有以 `www.contoso.com` 開頭的 URL    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    比對 `contoso.com` 下的所有子網域    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    比對所有結尾為 `contoso.com/` 的子網域    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    比對單一資料夾    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    使用連接埠號碼來比對單一頁面    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    比對單一且安全的頁面    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    符合單一資料夾及所有子資料夾    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- 以下是一些您無法指定的輸入範例：
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP 位址
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>管理 Proxy 設定

iOS 與 Android 版 Edge 和 [Azure AD 應用程式 Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) \(部分機器翻譯\) 可以一起使用，來讓使用者在他們的行動裝置上存取內部網路網站。 例如： 

- 使用者正在使用受 Intune 保護的 Outlook 行動應用程式。 然後他們按一下電子郵件中的內部網路網站連結，iOS 與 Android 版 Edge 則辨識此內部網路網站已透過應用程式 Proxy 向使用者公開。 使用者會透過應用程式 Proxy 自動進行路由傳送，在到達內部網路網站之前，使用任何適用的多重要素驗證和條件式存取來進行驗證。 使用者現在能夠存取內部網路網站 (甚至是在其行動裝置上)，且 Outlook 中的連結會如預期運作。
- 使用者在其 iOS 或 Android 裝置上開啟 iOS 與 Android 版 Edge。 如果 iOS 與 Android 版 Edge 已受 Intune 保護，且已啟用應用程式 Proxy，則使用者可以使用他們慣用的內部 URL 來移至內部網路網站。 iOS 與 Android 版 Edge 會辨識此內部網路網站已透過應用程式 Proxy 向使用者公開。 系統會自動透過應用程式 Proxy 路由使用者，以在抵達內部網路網站之前進行驗證。 

在開始之前：

- 透過 Azure AD 應用程式 Proxy 設定內部應用程式。
  - 若要設定應用程式 Proxy 並發佈應用程式，請參閱[安裝程式文件](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)。
- iOS 與 Android 版 Edge 應用程式必須獲指派 [Intune 應用程式保護原則](app-protection-policy.md)。
- Microsoft 應用程式必須有**限制使用其他應用程式的 Web 內容傳輸**資料傳輸設定已設定為 **Microsoft Edge** 的應用程式保護原則。

> [!NOTE]
> 已更新的應用程式 Proxy 重新導向資料最多可能需要 24 小時才會在 iOS 與 Android 版 Edge 中生效。

使用下列機碼/值組將 iOS 與 Android 版 Edge 設定為目標，以啟用應用程式 Proxy：

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** 會啟用 Azure AD App Proxy 重新導向案例<br>**false** (預設值) 會防止 Azure AD App Proxy 案例    |

> [!NOTE]
> Android 版 Edge 不會使用此機碼。 相反地，只要已登入的 Azure AD 帳戶已套用應用程式保護原則，Android 版 Edge 就會自動使用 Azure AD 應用程式 Proxy 設定。

如需如何使用 iOS 與 Android 版 Edge 和 Azure AD 應用程式 Proxy 來緊密 (且以受保護方式) 地存取內部部署 Web 應用程式的詳細資訊，請參閱[建議搭配使用：Intune 和 Azure Active Directory 合作以改善使用者存取](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254) \(英文\)。 此部落格文章參考 Intune Managed Browser，但內容也適用於 iOS 與 Android 版 Edge。

### <a name="manage-ntlm-single-sign-on-sites"></a>管理 NTLM 單一登入網站

組織可能會要求使用者使用 NTLM 進行驗證，以存取內部網路網站。 根據預設，每次使用者存取需要 NTLM 驗證的網站時，系統都會提示他們輸入認證，因為 NTLM 認證快取已停用。 

組織可以針對特定網站啟用 NTLM 認證快取。 針對這些網站，使用者輸入認證並成功驗證之後，預設會快取認證 30 天。


|機碼  |值  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |金鑰的相對應值為 URL 清單。 您能以單一值的方式輸入要允許的所有 URL，並使用垂直線 `|` 字元分隔。<p>**範例：**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>如需所支援 URL 格式類型的詳細資訊，請參閱[允許和封鎖的網站清單的 URL 格式](#url-formats-for-allowed-and-blocked-site-list)。         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |快取認證的時數，預設值為 720 小時         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>使用 Microsoft 端點管理員部署應用程式設定案例

如果您使用 Microsoft 端點管理員作為您的行動裝置應用程式管理提供者，下列步驟可讓您建立受控應用程式設定原則。 建立組態之後，您可以將其設定指派給使用者群組。

1. 登入 [Microsoft 端點管理員](https://endpoint.microsoft.com)。

2. 選取 [應用程式]，然後選取 [應用程式設定原則]。

3. 在 [應用程式設定原則] 刀鋒視窗上，選擇 [新增]，然後選取 [受控應用程式]。

4. 在 [基本] 區段上，輸入應用程式組態設定的 [名稱] 與選擇性的 [描述]。

5. 針對 [公用應用程式]，選擇 [選取公用應用程式]，然後在 [目標應用程式] 刀鋒視窗上，透過同時選取 iOS 與 Android 平台應用程式以選擇 [iOS 與 Android 版 Edge]。 按一下 [選取] 以儲存選取的公用應用程式。

6. 按一下 [下一步] 以完成應用程式設定原則的基本設定。

7. 在 [設定] 區段上，展開 [Edge 組態設定]。

8. 如果您想要管理資料保護設定，請據以設定所需的設定：

    - 針對 [應用程式 Proxy 重新導向]，請從可用選項中選擇：**啟用**、**停用** (預設值)。

    - 針對 [首頁捷徑 URL]，指定包含 *http://* 或 *https://* 前置詞的有效 URL。 基於安全性考量，會封鎖不正確的 URL。

    - 針對 [受控書籤]，請指定標題與包含 *http://* 或 *https://* 前置詞的有效 URL。

    - 針對[ 允許的 URL]，指定有效的 URL (只允許這些 URL；無法存取其他站台)。 如需所支援 URL 格式類型的詳細資訊，請參閱[允許和封鎖的網站清單的 URL 格式](#url-formats-for-allowed-and-blocked-site-list)。

    - 針對 [封鎖的 URL]，指定有效的 URL (只會封鎖這些 URL)。 如需所支援 URL 格式類型的詳細資訊，請參閱[允許和封鎖的網站清單的 URL 格式](#url-formats-for-allowed-and-blocked-site-list)。

    - 針對 [將受限制網站重新導向至個人內容]，請從可用選項中選擇：**啟用** (預設值)、**停用**。

    > [!NOTE]
    > 當原則中同時定義了允許的 URL 與封鎖的 URL 時，只會接受允許的清單。

9. 若要新增上述原則中未公開的其他應用程式組態設定，請展開 [一般組態設定] 節點，並據以輸入機碼值組。

10. 當您完成設定之後，請選擇 [下一步]。

11. 在 [指派] 區段上，選擇 [選取要納入的群組]。 選取您要指派應用程式設定原則的 Azure AD 群組，然後選擇 [選取]。

12. 當您完成指派時，請選擇 [下一步]。

13. 在 [建立應用程式設定原則檢閱 + 建立] 刀鋒視窗上，檢閱配置的設定，然後選擇 [建立]。

新建立的設定原則會顯示在 [應用程式設定] 刀鋒視窗上。

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>使用 iOS 與 Android 版 Edge 來存取受控應用程式記錄檔

在其 iOS 或 Android 裝置上安裝 iOS 與 Android 版 Edge 的使用者，可以檢視所有由 Microsoft 發行之應用程式的管理狀態。 使用者可以使用下列步驟，傳送記錄來對其受控的 iOS 或 Android 應用程式進行疑難排解：

1. 在您的裝置上開啟 iOS 與 Android 版 Edge。
2. 網址方塊中的類型 `about:intunehelp`。
3. iOS 與 Android 版 Edge 會啟動疑難排解模式。

如需儲存在應用程式記錄中的設定清單，請參閱[在 Managed Browser 中檢閱應用程式保護記錄](app-protection-policy-settings-log.md)。

若要了解如何在 Android 裝置上檢視記錄檔，請參閱[透過電子郵件將記錄檔傳送給 IT 系統管理員](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)。

## <a name="next-steps"></a>後續步驟

- [什麼是應用程式保護原則？](app-protection-policy.md) 
