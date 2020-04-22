---
title: 使用 Intune 設定適用於 Android Enterprise 的 Microsoft Launcher
titleSuffix: ''
description: 搭配 Microsoft Launcher 使用 Intune 設定原則。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0711b407b185b3a9621ff80a371bd3aaa5032ead
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407742"
---
# <a name="configure-microsoft-launcher"></a>設定 Microsoft Launcher

Microsoft Launcher 是 Android 應用程式，讓使用者能夠將他們的電話個人化、保持在最上面的位置，並從其電話傳輸到電腦。 

在 Android Enterprise 完全受控裝置上，Launcher 讓企業 IT 系統管理員能夠藉由選取背景圖案、應用程式和圖示位置來自訂受控裝置的主畫面。 這會在不同的 OEM 裝置和系統版本間，將所有受控 Android 裝置的外觀與風格標準化。 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>如何設定 Microsoft Launcher 應用程式 

Microsoft Launcher 應用程式[新增至 Intune](../apps/apps-add.md) 後，請巡覽至 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [應用程式]   > [應用程式設定原則]  。 為執行 **Android** 的**受控裝置**新增設定原則，然後選擇 [Microsoft Launcher]  作為相關聯的應用程式。 按一下 [組態設定]  以設定其他可用的 Managed Home Screen 設定。 

## <a name="choosing-a-configuration-settings-format"></a>選擇組態設定格式 

有兩種方法可以用來定義 Microsoft Launcher 的組態設定： 

- **設定設計工具**易於使用的 UI 可讓您將功能切換為開啟或關閉及設定值，藉此進行設定。 在此方法中，有數個值類型為 BundleArray 的設定索引鍵已停用。 這些只能設定索引碼藉由輸入 JSON 資料來設定。 

- **JSON 資料**可讓您使用 JSON 指令碼定義所有可用的設定索引碼。 

若您使用**設定設計工具**來新增屬性，即可從 [組態設定格式]  下拉式清單中選取 [輸入 JSON 資料]  ，來將這些屬性自動轉換成 JSON，如下所示。

   ![組態設定格式 - 使用設定設計工具](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > 透過設定設計工具設定屬性之後，JSON 資料也會更新為只反映這些屬性。 若要將其他設定金鑰新增至 JSON 資料，請使用 [JSON 指令碼範例](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example)，為每個設定金鑰複製必要的程式碼。 

## <a name="using-configuration-designer"></a>使用設定設計工具

設定設計工具可讓您選取預先填入的設定及其相關值。

   ![組態設定格式 - 輸入 JSON 資料](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

下表列出 Microsoft Launcher 可用的設定索引鍵、值類型、預設值及描述。 描述提供取決於所選值的預期裝置行為。 在設定設計工具中無法使用的設定索引碼，不會在表中列出。

|    設定機碼    |    值類型    |    預設值    |    說明     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    註冊類型    |    字串     |    預設值    |    允許您設定應套用此原則的註冊類型。 目前，**Default** 值會參考 **CorporateOwnedBuisnessOnly**。 現在沒有任何其他支援的註冊類型。        JSON 金鑰名稱：management_mode_key        |
|    已允許使用者變更主畫面應用程式順序    |    布林值    |    True    |    讓您能夠指定終端使用者是否可以變更 [主畫面應用程式順序]  設定。<ul><li>如果設定為 **True**，就只會針對初始部署強制執行原則中定義的應用程式順序。 之後，將不會強制執行原則來採用使用者可能進行的任何變更。</li><li>如果設定為 **False**，則會在每次同步處理時強制執行應用程式順序。</li></ul><br>**注意︰** 主畫面應用程式順序只能透過 JSON 編輯器來設定。<br><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    設定格線大小    |    字串    |    自動    |    讓您可為要放置於主畫面的應用程式設定格線大小。 您可以利用下列格式來設定應用程式的列數與欄數，以定義格線大小：`columns;rows`。 如果您定義了格線大小，主畫面上一列中將顯示的應用程式最大數目即為您設定的列數，而主畫面上一欄中將顯示的應用程式最大數目則為您設定的欄數。<br><br>        JSON 金鑰名稱：<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    設定裝置背景圖案    |    字串    |    Null    |    讓您可輸入想要設為背景圖案的影像 URL，來設定自選的背景圖案。<br><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    已允許使用者變更設定裝置背景圖案    |    Bool    |    True    |    讓您能夠指定終端使用者是否可以變更 [設定裝置背景圖案] 設定。<ul><li>如果設定為 **True**，就只會針對初始部署強制執行原則中定義的背景圖案。 之後，將不會強制執行原則來採用使用者可能進行的任何變更。</li><li>如果設定為 **False**，則會在每次同步處理時強制執行背景圖案。</li></ul><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    摘要啟用    |    布林值    |    True    |    讓您能夠在使用者於主畫面上向右撥動時，在裝置上啟用啟動器摘要。<ul><li>如果設定為 **True**，將會啟用摘要。</li><li>如果設定為 **False**，將會停用摘要。</li></ul><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Feed.Enabled`    |
|    已允許使用者變更摘要啟用    |    布林值    |    True    |     讓您能夠指定終端使用者是否可以變更 [摘要啟用]  設定。<ul><li>如果設定為 **True**，就只會針對初始部署強制執行摘要。 之後，將不會強制執行原則來採用使用者可能進行的任何變更。</li><li>如果設定為 **False**，則會在每次同步處理時強制執行摘要。</li></ul><br>JSON 金鑰名稱：`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    搜尋列位置   |    字串    |    下層    |  可供在主畫面上指定**搜尋列的位置**。 <ul><li>如果設定為 [底端]  ，搜尋列就會位於主畫面底部。</li><li>如果設定為 [頂端]  ，搜尋列就會位於主畫面頂端。</li><li>如果設定為 [隱藏]  ，搜尋列就會從主畫面中移除。</li></ul><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    允許使用者變更搜尋列位置   |    Bool    |    True    |  可供指定終端使用者是否可以變更 [搜尋列位置]  設定。 <ul><li>如果設定為 [True]  ，就只會強制執行初始部署的搜尋列位置。 之後，將不會強制執行原則來採用使用者可能進行的任何變更。</li><li>如果設定為 [False]  ，則會在每次同步處理時強制執行搜尋列位置。</li></ul><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`    |
|    Dock 模式  |    字串    |    顯示    | 可供在使用者於主畫面上向右撥動時，在裝置上啟用 Dock。<ul><li>如果設定為 [顯示]  ，就會啟用 Dock。</li><li>如果設定為 [隱藏]  ，主畫面就會隱藏 Dock，但使用者可在需要時顯示。</li><li>如果設定為 [停用]  ，就會停用 Dock。</li></ul><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Dock.Mode`    |
|   允許使用者變更 Dock 模式   |    字串    |    True    |  可供指定終端使用者是否可以變更 Dock 模式設定。<ul><li>如果設定為 [True]  ，就只會強制執行初始部署的 Dock 模式設定。 之後，將不會強制執行原則來採用使用者可能進行的任何變更。</li><li>如果設定為 [False]  ，則會在每次同步處理時強制執行 Dock 模式設定。</li></ul><br>JSON 金鑰名稱：<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>輸入 JSON 資料

輸入 JSON 資料可設定 Microsoft Launcher 的所有可用設定，以及**設定設計工具**中已停用的設定，如下所示。

   ![設定設計工具 - JSON 資料](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

除了設定設計工具表格 (上表) 中列出的可變更設定清單之外，下表還提供只能透過 JSON 資料設定的設定索引鍵。

|    設定機碼    |    值類型    |    預設值    |    說明     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    設定允許列出的應用程式<br>JSON 金鑰：`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | 請參閱：[設定允許列出的應用程式](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    讓您能夠從裝置上已安裝的應用程式中，定義一組可在主畫面上顯示的應用程式。 您可以針對想要顯示的應用程式輸入其應用程式套件名稱來定義應用程式，例如，輸入 `com.android.settings` 會使設定可在主畫面上存取。 您允許列於此區段的應用程式應已安裝於裝置上，才能在主畫面上顯示。<p>內容：<ul><li>**套件：** 應用程式套件名稱</li><li>**類別：** 應用程式活動，專屬於特定應用程式頁面。 如果此值是空的，即會使用預設的應用程式頁面。</li></ul>      |
|    主畫面應用程式順序<br>JSON 金鑰：`com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    請參閱：[主畫面應用程式順序](configure-microsoft-launcher.md#home-screen-app-order)      |    讓您能夠在主畫面上指定應用程式順序。<p>內容：<br><ul><li>**型別：** 如要指定應用程式的位置，僅支援 `application` 類型。 如要指定網頁連結的位置，則類型為 `weblink`。</li><li>**位置：** 這會指定主畫面上的應用程式圖示插槽。 這會從左上方的位置 1 開始，從左至右，從上往下。</li><li>**套件：** 這是指定應用程式順序所用的應用程式套件。</li><li>**類別：** 這是某應用程式頁面特定的應用程式活動。 如果此值是空的，將使用預設的應用程式頁面。 這個屬性供應用程式使用。</li><li>**標籤：** 這是某應用程式頁面特定的應用程式活動。 如果此值是空的，將使用預設的應用程式頁面。 此屬性用於應用程式。</li><li>**連結：** 終端使用者按一下網頁連結圖示後要啟動的 URL。 此屬性用於網頁連結。</li></ul>    |
|    設定釘選的網頁連結<br>JSON 金鑰：`com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    請參閱：[設定釘選的網頁連結](configure-microsoft-launcher.md#set-pinned-web-link)      |    此鍵可供將網站釘選到主畫面為快速啟動圖示。 如此即可確保終端使用者能夠快速輕鬆地存取重要的網站。 您可在「主畫面應用程式順序」設定中修改每個網頁連結圖示的位置。<p>內容：<br><ul><li>**• 標籤：** 顯示在 MS 啟動器主畫面上的網頁連結標題。</li><li>**連結：** 終端使用者按一下網頁連結圖示後要啟動的 URL。</li></ul>    |


### <a name="set-allow-listed-applications"></a>設定允許列出的應用程式

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>主畫面應用程式順序

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>設定釘選的網頁連結

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Microsoft 啟動器設定範例

以下是包含所有可用設定索引碼的範例 JSON 指令碼：

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>後續步驟

- 如需 Android Enterprise 完全受控裝置的詳細資訊，請參閱[設定 Android Enterprise 完全受控裝置的 Intune 註冊](../enrollment/android-fully-managed-enroll.md)。
