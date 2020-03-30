---
title: 使用 Intune 管理適用於 iOS 和 Android 的 Microsoft Edge
titleSuffix: ''
description: 使用 Microsoft Edge 的 Intune 應用程式保護原則，以確保一律使用就地保護公司網站的存取。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
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
ms.openlocfilehash: 9c04423f79855f4c28121dad11fa21ccb05216de
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084163"
---
# <a name="manage-web-access-by-using-microsoft-edge-with-microsoft-intune"></a>透過搭配 Microsoft Intune 使用 Microsoft Edge 來管理 Web 存取

搭配 Microsoft Edge 使用 Intune 應用程式保護原則，可協助確保一律會使用就地保護措施來存取公司網站。 提供以下依據 Intune 原則啟用的 Microsoft Edge 企業功能：

- **雙重識別。** 使用者可以新增工作帳戶與個人帳戶以進行瀏覽。 系統會完整區隔兩個身分識別，類似於 Office 365 和 Outlook 中的架構與體驗。 Intune 系統管理員可以在公司帳戶內，針對受保護的瀏覽體驗設定所需原則。
- **Intune 應用程式保護原則整合。** 因為 Microsoft Edge 已與 Intune SDK 整合，所以您可以透過應用程式保護原則來防止資料遺失。 這些功能包括控制剪下、複製與貼上、防止螢幕擷取，以及確保使用者選取的連結只在其他受管理用程式中開啟。
- **Azure 應用程式 Proxy 整合。** 您可以控制針對軟體即服務 (SaaS) 應用程式和 Web 應用程式的存取。 這能協助確保瀏覽器型應用程式都只會在安全的 Microsoft Edge 瀏覽器中執行，無論使用者是從公司網路連線或從網際網路連線。
- **應用程式設定。** 您可以利用應用程式組態設定來加強組織的安全性狀態，並為使用者設定容易使用的功能。 例如，您可以定義書籤、首頁捷徑、允許或封鎖的網站，以及 Azure Active Directory (Azure AD) 應用程式 Proxy。

適用於 Microsoft Edge 的 Microsoft Intune 防護原則可協助保護組織資料和資源。 使用這些原則來搭配 Microsoft Edge 能確保公司資源無論是在原生安裝的應用程式內，或透過網頁瀏覽器存取時，都會受到保護。

## <a name="getting-started"></a>開始使用

您和您的終端使用者可以從公用應用程式存放區下載 Microsoft Edge，以便用於您的組織中。 瀏覽器原則的作業系統需求為下列其中之一：
- Android 4 及更新版本
- iOS 8.0 和更新版本

## <a name="application-protection-policies-for-microsoft-edge"></a>Microsoft Edge 的應用程式保護原則

因為 Microsoft Edge 已與 Intune SDK 整合，所以您可以將應用程式保護原則套用至它們上方。

您可以套用這些設定至：
- 向 Intune 註冊的裝置。
- 向其他行動裝置管理產品註冊的裝置。
- 非受控裝置。

如果 Microsoft Edge 未以 Intune 原則設定目標，使用者便無法使用它來存取來自其他受 Intune 管理的應用程式 (例如 Office 應用程式) 的資料。 

   >[!NOTE]
   > 套用另存新檔原則以防止影像下載時，會停用 Microsoft Edge 的長按動作。

## <a name="conditional-access-for-microsoft-edge"></a>Microsoft Edge 的條件式存取

您可以利用 Azure AD 條件式存取將使用者重新導向，讓他們只能透過 Microsoft Edge 來存取公司內容。 這會將行動瀏覽器針對已連線至 Azure AD 之 Web 應用程式的存取方式，限制為被原則保護的 Microsoft Edge。 這會封鎖來自任何其他未被保護之瀏覽器的存取，例如 Safari 或 Chrome。 您可以將條件式存取套用至 Azure 資源，例如 Exchange Online 和 SharePoint Online、Microsoft 365 系統管理中心，甚至是已透過 [Azure AD 應用程式 Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) \(部分機器翻譯\) 對外部使用者公開的內部部署網站。

> [!NOTE]
> 需要在受保護的瀏覽器中開啟時，iOS 裝置上新的 Web 剪輯 (釘選的 Web 應用程式) 將會在 Microsoft Edge (而不是 Intune Managed Browser) 中開啟。 針對較舊的 iOS Web 剪輯，您必須為這些 Web 剪輯重定目標，以確保其會在 Microsoft Edge (而非 Managed Browser) 中開啟。

若要限制已連線至 Azure AD 的 Web 應用程式在 iOS 和 Android 上只能使用 Microsoft Edge：
1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 在 Intune 節點下，選取 [條件式存取]   > [新原則]  。
3. 選取窗格之 [存取控制]  區段中的 [授與]  。
4. 選取 [需要經過核准的用戶端應用程式]  。
5. 選擇 [授與]  窗格上的 [選取]  。 此原則必須指派給您只想要讓 Intune Managed Browser 應用程式存取的雲端應用程式。

    ![條件式存取原則 - [授與] 的螢幕擷取畫面](./media/manage-microsoft-edge/manage-microsoft-edge-01.png)

6. 在 [指派] 區段中，選取 [條件]   > [應用程式]  。 [應用程式]  窗格隨即出現。
7. 在 [設定]  下，選取 [是]  來將原則套用至特定用戶端應用程式。
8. 確認已選取 **Browser** 作為用戶端應用程式。

    ![條件式存取原則 - [選取用戶端應用程式] 的螢幕擷取畫面](./media/manage-microsoft-edge/manage-microsoft-edge-02.png)

    > [!NOTE]
    > 如果您想要限制哪些原生應用程式 (非瀏覽器應用程式) 可以存取這些雲端應用程式，則也可以選取 [行動裝置 App 及桌面用戶端]  。

9. 在 [指派]  區段中，選取 [使用者和群組]  ，然後選擇您要指派此原則的使用者或群組。

10. 在 [指派]  區段中，選取 [雲端應用程式]  選擇要使用此原則保護的應用程式。

設定上述原則之後，系統會強制使用者使用 Microsoft Edge 來存取您使用此原則保護、已連線至 Azure AD 的 Web 應用程式。 在此情況下，如果使用者嘗試使用非受控瀏覽器，便會收到他們必須改為使用 Microsoft Edge 的訊息。

> [!TIP]
> 條件式存取是 Azure AD 技術。 從 Intune 存取之條件式存取節點與從 Azure AD 存取的節點相同。

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>在被原則保護的瀏覽器中針對已連線至 Azure AD 的 Web 應用程式使用單一登入

iOS 和 Android 上的 Microsoft Edge 可以針對所有已連線至 Azure AD 的 Web 應用程式 (SaaS 和內部部署) 利用單一登入 (SSO)。 SSO 可讓使用者透過 Microsoft Edge 存取已連線至 Azure AD 的 Web 應用程式，而不必重新輸入其認證。

SSO 要求裝置必須註冊 iOS 裝置的 Microsoft Authenticator 應用程式或 Android 上 Intune 公司入口網站應用程式。 當使用者具備上述其中一項時，系統會在他們在被原則保護的瀏覽器中移至已連線至 Azure AD 的 Web 應用程式時通知他們註冊其裝置。 (這只會在其裝置尚未註冊時發生。)使用 Intune 所管理的使用者帳戶註冊裝置之後，該帳戶便會針對已連線至 Azure AD 的 Web 應用程式啟用 SSO。

> [!NOTE]
> 裝置註冊是使用 Azure AD 服務的簡單簽入。 它不需要完整裝置註冊，且不會在該裝置上授與 IT 人員額外的權限。

## <a name="create-a-protected-browser-app-configuration"></a>建立受保護的瀏覽器應用程式設定

針對 Microsoft Edge 建立應用程式設定：

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   > [應用程式設定原則]   > [新增]  。
3. 在 [新增設定原則]  窗格上，輸入應用程式組態設定的 [名稱]  和選擇性 [描述]  。
4. 針對 [裝置註冊]  類型請選擇 [受管理的應用程式]  。
5. 選擇 [選取必要的應用程式]  。 然後在 [目標應用程式]  窗格上，選擇適用於 iOS/iPadOS、Adroid 或兩者的 **Managed Browser** 或 **Edge**。
6. 選取 [確定]  以返回 [新增設定原則]  窗格。
7. 選取 [組態設定]  。 在 [設定]  窗格上，您可以定義機碼和值組來為 Microsoft Edge 提供設定。 請使用本文稍後的各個章節，來了解您可以定義的不同金鑰和值組。

    > [!NOTE]
    > Microsoft Edge 使用與 Managed Browser 相同的金鑰和值組。 在 Android 上，必須使用應用程式保護原則將 Microsoft Edge 鎖定為目標，應用程式設定原則才會生效。

8. 完成之後，請選取 [確定]  。
9. 在 [新增設定原則]  窗格上，選擇 [新增]  。<br>
    會隨即建立新設定，然後顯示在 [應用程式設定]  窗格上。

## <a name="assign-the-configuration-settings-you-created"></a>指派您建立的組態設定 

您可以將設定指派給 Azure AD 中的使用者群組。 如果該使用者已經安裝目標受保護的瀏覽器應用程式，則此應用程式是由您指定的設定管理。

1. 在 Intune 行動應用程式管理儀表板的 [應用程式]  窗格上，選取 [應用程式設定原則]  。
2. 從應用程式設定清單，選取您要指派的設定。
3. 在下一個窗格上，選取 [指派]  。
4. 在 [指派]  窗格上，選取您要指派應用程式設定的 Azure AD 群組，然後選取 [確定]  。

## <a name="direct-users-to-microsoft-edge-instead-of-the-intune-managed-browser"></a>將使用者導向 Microsoft Edge，而不是 Intune Managed Browser 

Intune Managed Browser 和 Microsoft Edge 都可以用來作為被原則保護的瀏覽器。 為了確保您的使用者會被引導為使用正確的瀏覽器應用程式，請用下列組態設定來設定所有由 Intune 所管理之應用程式 (例如 Outlook、OneDrive 與 SharePoint) 的目標：

|    機碼    |    值    |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.useEdge`    |    值 `true` 將會引導您的使用者下載並使用 Microsoft Edge。<br>值 `false` 將會允許您的使用者使用 Intune Managed Browser。    |

如果**未**設定此應用程式設定值，則下列邏輯會定義哪一個瀏覽器將用來開啟公司連結。

在 Android 上：
- 如果使用者已在其裝置中下載 Intune Managed Browser 和 Microsoft Edge，則會開啟 Intune Managed Browser。 
- 如果裝置上僅下載 Microsoft Edge 且已經透過 Intune 原則設定為目標應用程式，則會開啟 Microsoft Edge。
- 如果裝置上只有 Managed Browser 且已經透過 Intune 原則設定為目標應用程式，則會啟動 Managed Browser。

在 iOS/iPadOS 上，針對已整合 Intune SDK for iOS v. 9.0.9+ 的應用程式：
- 如果裝置上同時有 Managed Browser 和 Microsoft Edge，則會啟動 Intune Managed Browser。  
- 如果裝置上只有 Microsoft Edge 且已經透過 Intune 原則設定為目標應用程式，則會啟動 Microsoft Edge。
- 如果裝置上只有 Managed Browser 且已經透過 Intune 原則設定為目標應用程式，則會啟動 Managed Browser。

## <a name="configure-application-proxy-settings-for-microsoft-edge"></a>針對 Microsoft Edge 設定應用程式 Proxy 設定

Microsoft Edge 及 [Azure AD 應用程式 Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) \(部分機器翻譯\) 可以一起使用，來讓使用者在他們的行動裝置上存取內部網路網站。 

以下是一些 Azure AD 應用程式 Proxy 能夠提供的案例範例： 

- 使用者正在使用受 Intune 保護的 Outlook 行動應用程式。 然後他們按一下電子郵件中的內部網路網站連結，Microsoft Edge 則辨識此內部網路網站已透過應用程式 Proxy 向使用者公開。 使用者會透過應用程式 Proxy 自動進行路由傳送，在到達內部網路網站之前，使用任何適用的多重要素驗證和條件式存取來進行驗證。 使用者現在能夠存取內部網路網站 (甚至是在其行動裝置上)，且 Outlook 中的連結會如預期運作。
- 使用者在其 iOS 或 Android 裝置上開啟 Microsoft Edge。 如果 Microsoft Edge 是被 Intune 保護，且已啟用應用程式 Proxy，則使用者可以使用他們慣用的內部 URL 來移至內部網路網站。 Microsoft Edge 會辨識此內部網路網站是透過應用程式 Proxy 向使用者公開。 系統會自動透過應用程式 Proxy 路由使用者，以在抵達內部網路網站之前進行驗證。 

### <a name="before-you-start"></a>在您開始使用 Intune 之前

- 透過 Azure AD 應用程式 Proxy 設定內部應用程式。
  - 若要設定應用程式 Proxy 並發佈應用程式，請參閱[安裝程式文件](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy)。
- Microsoft Edge 應用程式必須已指派 [Intune 應用程式保護原則](app-protection-policy.md)。

> [!NOTE]
> 更新的應用程式 Proxy 重新導向資料，最多可能需要 24 小時才會在 Managed Browser 和 Microsoft Edge 中生效。

#### <a name="step-1-enable-automatic-redirection-to-microsoft-edge-from-outlook"></a>步驟 1：從 Outlook 啟用針對 Microsoft Edge 的自動重新導向
搭配能啟用 [使用原則受控瀏覽器共用 Web 內容]  設定的應用程式保護原則來設定 Outlook。

![應用程式保護原則 - [使用原則受控瀏覽器共用 Web 內容] 的螢幕擷取畫面](./media/manage-microsoft-edge/manage-microsoft-edge-03.png)

#### <a name="step-2-set-the-app-configuration-setting-to-enable-app-proxy"></a>步驟 2：設定應用程式組態設定，以啟用應用程式 Proxy
使用下列金鑰/值組將 Microsoft Edge 設定為目標，以針對 Microsoft Edge 啟用應用程式 Proxy：

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    true    |

如需如何前後使用 Microsoft Edge 與 Azure AD 應用程式 Proxy 來緊密 (且被保護) 地存取內部部署 Web 應用程式的詳細資訊，請參閱[建議搭配使用：Intune 和 Azure Active Directory 合作以改善使用者存取](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254) \(英文\)。 此部落格文章參考 Intune Managed Browser，但內容也適用於 Microsoft Edge。

## <a name="configure-a-homepage-shortcut-for-microsoft-edge"></a>設定適用於 Microsoft Edge 的首頁捷徑

此設定允許您設定適用於 Microsoft Edge 的首頁捷徑。 當使用者在 Microsoft Edge 中開啟新索引標籤時，您設定的首頁捷徑會成為搜尋列下方第一個圖示。 使用者在其受控內容中無法編輯或刪除這個捷徑。 首頁捷徑會顯示您組織的名稱，以區分該捷徑。 

使用下列金鑰/值組來設定首頁捷徑：

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    指定有效的 URL。 基於安全性考量，會封鎖不正確的 URL。<br>**範例：**  <`https://www.bing.com`>     |

## <a name="configure-multiple-top-site-shortcuts-for-new-tab-pages-in-microsoft-edge"></a>為 Microsoft Edge 中的新索引標籤頁面設定多個熱門網站捷徑 
如同設定首頁捷徑，您也可以在 Microsoft Edge 中的新索引標籤頁面上設定多個熱門網站捷徑。 使用者在受控內容中無法編輯或刪除這些捷徑。 注意：您最多可以設定 8 個捷徑 (包含首頁捷徑)。 如果您設定了首頁捷徑，則該捷徑將會覆寫先前設定的第一個網站。 

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    指定一組值 URL。 每個熱門網站捷徑都會包含一個標題與 URL。 請使用 `|` 字元來分隔標題和 URL。 例如： <br> `GitHub | https://github.com/||LinkedIn|https://www.linkedin.com`    |

## <a name="configure-your-organizations-logo-and-brand-color-for-new-tab-pages-in-microsoft-edge"></a>針對 Microsoft Edge 中的新索引標籤頁面設定您組織的標誌與品牌色彩

這些設定可讓您自訂 Microsoft Edge 的新索引標籤頁面，以顯示您組織的標誌與品牌色彩作為頁面背景。

若要上傳您組織的標誌與色彩，請先完成下列步驟：
- 在 Azure 入口網站中，巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) -> [租用戶系統管理]   -> [自訂]   -> [公司身分識別商標]  。
- 若要設定品牌的標誌，請在 [顯示] 下選擇 [僅限公司標誌]。 建議使用透明背景標誌。 
- 若要設定您的品牌背景色彩，請在 [顯示] 下選擇 [佈景主題色彩]。 Microsoft Edge 會在新索引標籤頁面上套用較淺的色彩著色，以確保頁面具有高可讀性。 

接下來，使用下列機碼/值組，將您的組織商標提取到 Microsoft Edge：

|    機碼    |    值    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    True    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    True    |

## <a name="display-relevant-industry-news-on-new-tab-pages"></a>在新索引標籤頁面上顯示相關的產業新聞

您可以在 Microsoft Edge 行動版中設定新索引標籤頁面體驗，以顯示與您組織相關的產業新聞。 當您啟用這項功能時，Microsoft Edge 行動版會使用您組織的網域名稱，從網路彙總您的組織、組織產業和競爭者的相關新聞，讓您的使用者可以從 Microsoft Edge 的集中式新索引標籤頁面中找到所有相關外部新聞。 產業新聞預設為關閉，您可以為您的組織選擇加入。 

|    機碼    |    值    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **True** 將會在 Microsoft Edge 行動版的新索引標籤頁上顯示產業新聞。<p>**False** (預設) 將會隱藏新索引標籤頁面中的產業新聞。    |

## <a name="configure-managed-bookmarks-for-microsoft-edge"></a>設定 Microsoft Edge 的受控書籤

為了方便存取，您可以設定使用者在使用 Microsoft Edge 時可用的書籤。 

以下是一些詳細資料：

- 使用者在使用 Microsoft Edge 的[企業模式](https://docs.microsoft.com/intune/apps/app-configuration-managed-browser#how-to-configure-bookmarks-for-a-protected-browser)時，才會看到這些書籤。 
- 使用者無法刪除或修改這些書籤。
- 這些書籤會顯示在清單頂端。 使用者所建立的書籤都會顯示在這些書籤下方。
- 如果您已啟用應用程式 Proxy 重新導向，即可使用應用程式 Proxy Web 應用程式的內部或外部 URL 來新增這些應用程式 Proxy Web 應用程式。
- 確定您在清單中輸入 UTL 時，已在所有 URL 中加上 **http://** 或 **https://** 的前置詞。

您可以使用下列金鑰/值組來設定受控書籤：

|    機碼    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    此設定值是書籤清單。 每個書籤都是由書籤標題和書籤 URL 所組成。 請使用 `|` 字元來分隔標題和 URL。      範例：<br>`Microsoft Bing|https://www.bing.com`<br>若要設定多個書籤，請以雙引號字元 `||` 分隔每組配對。<p>範例：<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

## <a name="display-myapps-within-microsoft-edge-bookmarks"></a>在 Microsoft Edge 書籤內顯示 MyApps

根據預設，您的使用者將會看見在 Microsoft Edge 書籤的資料夾內針對他們所設定的 MyApps 網站。 該資料夾將會以您組織的名稱來標示。

|    機碼    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **True** 會在 Microsoft Edge 書籤中顯示 MyApps。<p>**False** 會在 Microsoft Edge 中隱藏 MyApps。    |
    
## <a name="use-https-protocol-as-default"></a>使用 HTTPS 通訊協定作為預設

如果使用者未指定通訊協定，您可以將 Microsoft Edge 行動版設定為預設使用 HTTPS 通訊協定。 一般而言，此為最佳做法。 使用下列機碼/值組，啟用 HTTPS 作為預設通訊協定：

|    機碼    |    值    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.defaultHTTPS`     |     **True** 會將預設通訊協定設定為使用 HTTPS     |


## <a name="specify-allowed-or-blocked-sites-list-for-microsoft-edge"></a>針對 Microsoft Edge 指定允許或封鎖的網站清單
您可以使用應用程式設定來定義當使用者使用他們的工作設定檔時，可以存取哪些網站。 如果您使用允許清單，則使用者將只能存取您明確列出的網站。 如果您使用封鎖清單，則使用者將能夠存取所有網站 (除了您明確封鎖的網站以外)。 您只應該強制允許或封鎖清單，而不應該同時使用兩者。 如果您同時強制兩者，系統只會採用允許清單。  

請使用下列金鑰/值組來針對 Microsoft Edge 設定允許或封鎖的網站清單。 

|    機碼    |    值    |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    從下列選項進行選擇：<p>1.指定允許的 URL (僅允許這些 URL；不能存取其他站台)：<br>`com.microsoft.intune.mam.managedbrowser.AllowListURLs`<p>2.指定封鎖的 URL (可以存取所有其他網站)：<br>`com.microsoft.intune.mam.managedbrowser.BlockListURLs`    |    金鑰的相對應值為 URL 清單。 您可以以單一值的方式，輸入想要允許或封鎖的所有 URL，並使用垂直線 `|` 字元分隔。<br>**範例：**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`  |

無論定義的允許清單或封鎖清單設定為何，一律允許下列網站：
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

### <a name="url-formats-for-allowed-and-blocked-site-list"></a>適用於允許和封鎖網站清單的 URL 格式 
您可以使用各種不同 URL 格式來建置您的允許/封鎖網站清單。 下表會詳細說明這些允許的模式。 在開始之前有一些注意事項： 
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

## <a name="transition-users-to-their-personal-context-when-trying-to-access-a-blocked-site"></a>嘗試存取已封鎖的網站時，將使用者轉換成其個人內容

由於 Microsoft Edge 中已內建雙重身分識別模型，您可以為使用者啟用 Intune Managed Browser 無法達成且更有彈性的體驗。 當使用者在 Microsoft Edge 中造訪被封鎖的網站時，您可以提示他們在其個人內容 (而非工作內容) 中開啟該連結。 這可讓他們持續被保護，同時也能確保企業資源的安全。 例如，如果使用者在 Outlook 中收到某篇新聞文章的連結，他們可以在其個人內容或 InPrivate 索引標籤中開啟該連結。其工作內容並不允許新聞網站。 根據預設，會允許這些轉換。

使用下列金鑰/值組來設定是否允許這些軟轉換：

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock`    |    **True** (預設值) 會允許 Microsoft Edge 將使用者轉換至其個人內容以開啟封鎖的網站。<p>**Block** 會防止 Microsoft Edge 轉換使用者。 使用者只會看見說明其所嘗試存取網站已封鎖的訊息。    |

## <a name="open-restricted-links-directly-in-inprivate-tab-pages"></a>直接在 InPrivate 索引標籤頁面中開啟受限制的連結

您可以設定受限制的連結是否應直接在 InPrivate 瀏覽中開啟，以提供使用者更順暢的瀏覽體驗。 這可讓使用者免於必須轉換到其個人內容以瀏覽網站的步驟。 InPrivate 瀏覽會被視為非受控，因此使用者在使用 InPrivate 瀏覽模式時將無法存取。  附註：若要讓此設定生效，您也必須將上述設定 `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock` 設定為 **True**。

|    機碼    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked`    |    **True** 會直接在 InPrivate 索引標籤中自動開啟網站，而不會提示使用者切換至其個人帳戶。 <p> **False** (預設值) 會封鎖 Microsoft Edge 中的網站，並要求使用者切換至其個人帳戶方可檢視。    |


## <a name="disable-microsoft-edge-features-to-customize-the-end-user-experience-for-your-organizations-needs"></a>停用 Microsoft Edge 功能，並根據組織需求自訂終端使用者體驗

### <a name="disable-prompts-to-share-usage-data-for-personalization"></a>停用共用個人化使用方式資料的提示 

根據預設，Microsoft Edge 會提示使用者提供使用狀況資料收集，以將其瀏覽體驗個人化。 您可以防止此提示顯示給終端使用者，藉此停用共用這筆資料。 

|    機碼    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableShareUsageData`    |     **True** 會停用此提示，使其無法向使用者顯示。    |

### <a name="disable-prompts-to-share-browsing-history"></a>停用共用瀏覽歷程記錄的提示 

根據預設，Microsoft Edge 會提示使用者提供瀏覽歷程記錄資料收集，以將其瀏覽體驗個人化。 您可以防止此提示顯示給終端使用者，藉此停用共用這筆資料。

|    機碼    |    值    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     `com.microsoft.intune.man.managedbrowser.disableShareBrowsingHistory`    |     **True** 會停用此提示，使其無法向使用者顯示。     |

### <a name="disable-prompts-that-offer-to-save-passwords"></a>停用儲存密碼的提示

根據預設，iOS 上的 Microsoft Edge 提供將您的使用者密碼儲存至鑰匙圈的選項。 如果要為您的組織停用此提示，請設定下列設定：

|    機碼    |    值    |
|-----------------------|-----------------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **password** 會停用儲存終端使用者密碼的提示。    |

### <a name="disable-users-from-adding-extensions-to-microsoft-edge"></a>讓使用者無法將擴充功能新增至 Microsoft Edge 

您可以在 Microsoft Edge 中停用擴充功能架構，以防止使用者安裝任何擴充功能應用程式。 若要執行此動作，請進行下列設定：

|    機碼    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableExtensionFramework`    |    **True** 將會停用擴充功能架構    |

### <a name="disable-inprivate-browsing-and-microsoft-accounts-to-restrict-browsing-to-work-only-contexts"></a>停用 InPrivate 瀏覽與 Microsoft 帳戶，將瀏覽限制為僅限工作的內容

如果組織在高度管制的產業中營運，或使用個別應用程式 VPN 以允許使用者透過 Microsoft Edge 存取工作資源，則您可選擇在 Microsoft Edge 內停用 InPrivate 瀏覽，其會被視為非工作內容。 

|    機碼    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.disableFeatures`    |    **inprivate** 會停用 InPrivate 瀏覽。   |

### <a name="restrict-microsoft-edge-use-to-allowed-accounts-only"></a>將 Microsoft Edge 限制為僅限允許的帳戶使用

除了封鎖 InPrivate 與 MSA 瀏覽之外，您也可以在使用者透過 AAD 帳戶登入時，只允許其使用 Microsoft Edge。 這項功能僅適用於已註冊 MDM 的使用者。 您可以在此處深入了解如何進行這項設定：

>[!NOTE]
> `com.microsoft.intune.mam.managedbrowser.disableFeatures` 可以用來同時停用多個功能。 例如，若要停用 InPrivate 和密碼，請使用 `inprivate| password`。

## <a name="configure-microsoft-edge-as-a-kiosk-app-on-android-devices"></a>在 Android 裝置上將 Microsoft Edge 設定為 Kiosk 應用程式

### <a name="enable-microsoft-edge-as-a-kiosk-app"></a>啟用 Microsoft Edge 作為 Kiosk 應用程式
若要啟用 Microsoft Edge 作為 Kiosk 應用程式，請先進行此父代設定：

|    機碼    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.enableKioskMode`    |    **True** 會針對 Microsoft Edge 啟用 Kiosk 設定    |

### <a name="show-address-bar-in-kiosk-mode"></a>在 Kiosk 模式中顯示網址列
若要在 Microsoft Edge 處於 Kiosk 模式時顯示網址列，請進行下列設定：

|    機碼    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode`    |    **True** 會顯示網址列。 <br> **False** (預設值) 將會隱藏網址列。    |

### <a name="show-bottom-action-bar-in-kiosk-mode"></a>在 Kiosk 模式中顯示底部動作列
|    機碼    |    值    |
|-----------|-------------|
|    `com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode`    |    **True** 會在 Microsoft Edge 中顯示底部動作列。 <br> **False** (預設值) 會隱藏底部列。    |


## <a name="use-microsoft-edge-to-access-managed-app-logs"></a>使用 Microsoft Edge 來存取受控應用程式記錄


在其 iOS 或 Android 裝置上安裝 Microsoft Edge 的使用者，可以檢視所有由 Microsoft 發行之應用程式的管理狀態。 使用者可以使用下列步驟，傳送記錄來對其受控的 iOS 或 Android 應用程式進行疑難排解：

1. 在您的裝置上開啟 Microsoft Edge。
2. 網址方塊中的類型 `about:intunehelp`。
3. Microsoft Edge 會啟動疑難排解模式。

如需儲存在應用程式記錄中的設定清單，請參閱[在 Managed Browser 中檢閱應用程式保護記錄](app-protection-policy-settings-log.md)。

若要了解如何在 Android 裝置上檢視記錄檔，請參閱[透過電子郵件將記錄檔傳送給 IT 系統管理員](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)。

## <a name="security-and-privacy-for-microsoft-edge"></a>Microsoft Edge 的安全性和隱私權

以下是 Microsoft Edge 的其他安全性和隱私權考量：

- Microsoft Edge 不會使用使用者在其裝置上針對原生瀏覽器 https://docs.microsoft.com/en-us/intune/apps/app-configuration-policies-use-android#allow-only-configured-organization-accounts-in-multi-identity-apps 所做的設定，因為 Microsoft Edge 無法存取這些設定。
- 您可以在與 Microsoft Edge 相關聯的應用程式保護原則中設定 [需要簡單的 PIN 碼才能存取]  或 [需要公司認證才能存取]  選項。 如果使用者選取驗證頁面上的說明連結，他們便可以瀏覽任何網際網路網站，無論那些網站是否被加入原則中的已封鎖清單。
- Microsoft Edge 可以在直接存取網站時，只封鎖網站的存取。 它不會在使用者使用中繼服務 (例如翻譯服務) 來存取網站時封鎖存取。
- 若要允許驗證並存取 Intune 文件，請從允許或封鎖清單設定中排除 * **.microsoft.com**。 它一律會被允許。
- 使用者可以關閉資料收集。 Microsoft 會自動收集有關 Managed Browser 效能和使用的匿名資料，以改善 Microsoft 產品和服務。 使用者可以在裝置上使用 **[使用方式資料]** 設定以關閉資料收集。 您無法控制這項資料的收集。 在 iOS 裝置上，使用者將無法開啟具有過期或未受信任憑證的網站。

## <a name="restrict-microsoft-edge-use-to-a-work-or-school-account"></a>將 Microsoft Edge 限制為使用公司或學校帳戶

尊重我們最大規模且高度管制之客戶的資料安全性和合規性政策，是 Microsoft 365 價值的關鍵要件。 有些公司需要在公司環境內擷取所有通訊資訊，以及確保裝置僅可用於公司通訊。 為了支援這些需求，可將已註冊裝置上適用於 iOS 和 Android 的 Edge 設定為只允許在適用於 iOS 和 Android 的 Edge 中佈建單一公司帳戶。

您可以在這裡深入了解如何設定組織允許的帳戶模式設定：

- [Android 設定](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS 設定](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

## <a name="next-steps"></a>後續步驟

- [什麼是應用程式保護原則？](app-protection-policy.md) 
