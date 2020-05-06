---
title: 自訂自助入口網站
titleSuffix: Configuration Manager
description: 將自訂群組織特定資訊新增至 BitLocker 管理自助入口網站
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f4fdb0d6a41c2b40c9e35840dfc27261a42e68b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693496"
---
# <a name="customize-the-self-service-portal"></a>自訂自助入口網站

適用於：  Configuration Manager (最新分支)

<!--3601034-->

[安裝 BitLocker 自助入口網站](setup-websites.md)後，您可以為組織自訂該入口網站。 您可以新增自訂通知、組織名稱，以及其他組織特定資訊。

## <a name="branding"></a>商標

以您組織的名稱、技術支援 URL 和通知文字，為自助入口網站加上品牌。

1. 在裝載自助入口網站的 Web 伺服器上，以管理員身分登入。

1. 啟動 [Internet Information Services (IIS) 管理員]  (執行 **inetmgr.exe**)。

1. 展開 [網站]  ，展開 [預設的網站]  ，然後選取 **SelfService** 節點。 在詳細資料窗格的 **ASP.NET** 群組中，開啟 [應用程式設定]  。

    [![IIS 管理員中 SelfService 應用程式設定的 範例螢幕擷取畫面](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. 選取您要變更的項目，然後在 [動作]  窗格中選取 [編輯]  。 將 [值]  變更為您要使用的新名稱。

    > [!CAUTION]
    > 請勿變更 [名稱]  值。 例如，請勿變更 `CompanyName`，而應變更 `Contoso IT`。 如果您變更 [名稱]  值，自助入口網站將會停止運作。

變更會立即生效。

### <a name="supported-branding-values"></a>支援的商標值

針對您可以設定的值，請參閱下表：

|Name|說明|預設值|
|--- |--- |--- |
|公司名稱|自助入口網站在每個頁面頂端顯示為標題的組織名稱。|`Contoso IT`|
|DisplayNotice|顯示使用者必須確認的初始聲明。|`true`|
|HelpdeskText|在右窗格中位於 [針對所有其他相關問題] 下方的字串|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|HelpdeskText 字串的連結。|(空白)|
|NoticeTextPath|使用者必須確認的初始聲明文字。 根據預設，Web 伺服器上的完整檔案路徑為 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`。 請在純文字編輯器中編輯並儲存檔案。 此路徑值相對於 SelfService 應用程式。|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

如需預設自助入口網站的螢幕擷取畫面，請參閱 [BitLocker 自助入口網站](self-service-portal.md)。

> [!TIP]
> 如有必要，您可以將其中部分的字串當地語系化，以不同的語言顯示。 如需詳細資訊，請參閱[當地語系化](#bkmk_localize)。

## <a name="session-time-out"></a>工作階段逾時

若要讓使用者的工作階段在閒置一段指定的時間之後過期，您可以變更自助入口網站的工作階段逾時設定。

1. 在裝載自助入口網站的 Web 伺服器上，以管理員身分登入。

1. 啟動 [Internet Information Services (IIS) 管理員]  (執行 **inetmgr.exe**)。

1. 展開 [網站]  ，展開 [預設的網站]  ，然後選取 **SelfService** 節點。 在詳細資料窗格的 **ASP.NET** 群組中，開啟 [工作階段狀態]  。

1. 在 [Cookie 設定]  群組中，變更 [逾時 (以分鐘為單位)]  值。 這是使用者工作階段到期前的分鐘數。 預設值為 `5`。 若要停用此設定讓工作階段不會逾時，請將值設定為 `0`。

1. 在 [動作]  窗格中，選取 [套用]  。

## <a name="localize-helpdesk-text-and-url"></a><a name="bkmk_localize"></a> 當地語系化技術支援的文字和 URL

您可以設定自助入口網站 `HelpdeskText` 陳述式和 `HelpdeskUrl` 連結的當地語系化版本。 這個字串會通知使用者在使用入口網站時如何取得其他說明。 如果您設定當地語系化的文字，入口網站就會以該語言顯示網頁瀏覽器的當地語系化版本。 如果找不到當地語系化版本，則會顯示 `HelpdeskText` 和 `HelpdeskUrl` 設定中的預設值。

1. 在裝載自助入口網站的 Web 伺服器上，以管理員身分登入。

1. 啟動 [Internet Information Services (IIS) 管理員]  (執行 **inetmgr.exe**)。

1. 展開 [網站]  ，展開 [預設的網站]  ，然後選取 **SelfService** 節點。 在詳細資料窗格的 **ASP.NET** 群組中，開啟 [應用程式設定]  。

1. 在 [動作]  窗格中，選取 [新增]  。

1. 在 [新增應用程式設定]  視窗中，設定下列值：

    - **名稱**：輸入 `HelpdeskText_<language>`，其中 `<language>` 是文字的語言代碼。

      例如，若要以西班牙文 (西班牙) 建立當地語系化的 `HelpdeskText` 陳述式，則名稱為 `HelpdeskText_es-es`。

    - **值**：要在自助入口網站的右窗格中顯示於 [針對所有其他相關問題] 下的當地語系化字串

1. 選取 [確定]  以儲存新的設定。

1. 重複此程序，為符合相關 `HelpdeskText_<language>` 設定的 `HelpdeskUrl_<language>` 新增應用程式設定。

重複此程序，為您在組織中支援的所有語言新增設定配對。

## <a name="localize-the-notice-file"></a>將聲明檔案當地語系化

您可以針對使用者在自助入口網站中必須確認的初始聲明設定當地語系化版本。 根據預設，Web 伺服器上的完整檔案路徑為 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`。

若要顯示當地語系化的聲明文字，請建立當地語系化的 notice.txt 檔案。 然後，將其儲存在特定的語言資料夾底下。 例如：`Self Service Website\es-es\Notice.txt` 用於西班牙文 (西班牙)。

自助入口網站會根據下列規則顯示聲明文字：

- 如果遺漏預設的聲明檔案，入口網站會顯示遺漏預設檔案的訊息。

- 如果您在適當的語言資料夾中建立當地語系化的聲明檔案，則會顯示當地語系化的聲明文字。

- 如果 Web 伺服器找不到聲明檔案的當地語系化版本，則會顯示預設聲明。

- 如果使用者將瀏覽器設定為沒有當地語系化聲明的語言，則入口網站會顯示預設聲明。

### <a name="create-a-localized-notice-file"></a>建立當地語系化的聲明檔案

1. 在裝載自助入口網站的 Web 伺服器上，以管理員身分登入。

1. 在 `Self Service Website` 應用程式路徑中，為每個支援的語言建立一個 `<language>` 資料夾。 例如，`es-es` 用於西班牙文 (西班牙)。 根據預設，完整路徑為 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`。

    如需您可以使用的有效語言代碼清單，請參閱 [National Language Support (NLS) API Reference](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers) (國家語言支援 (NLS) API 參考)。

    > [!TIP]
    > 語言資料夾的名稱也可以是非語言相關的名稱。 例如，以 **es** 表示西班牙文，而非以 **es-es** 表示西班牙文 (西班牙) 或以 **es-ar** 表示西班牙文 (阿根廷)。 如果使用者將瀏覽器設定為 **es-es**，而該語言資料夾不存在，則 Web 伺服器會以遞迴方式檢查父地區設定資料夾 (**es**)。 (父地區設定定義於 .NET 中。)例如 `Self Service Website\es\Notice.txt`。 這個遞迴的回溯會模擬 .NET 資源載入規則。

1. 建立具有當地語系化文字的預設聲明檔案複本。 將其儲存在語言代碼的資料夾中。 例如，西班牙文 (西班牙) 的預設完整路徑為 `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`。

對您在組織中支援之所有語言的當地語系化聲明檔案重複此程序。

## <a name="next-steps"></a>後續步驟

現在您已安裝和自訂自助入口網站，請立即試用！ 如需詳細資訊，請參閱 [BitLocker 自助入口網站](self-service-portal.md)。
