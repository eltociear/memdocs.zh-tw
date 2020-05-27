---
title: 將 iOS 企業營運應用程式新增至 Microsoft Intune
titleSuffix: ''
description: 了解如何將 iOS 企業營運 (LOB) 應用程式新增至 Microsoft Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 099101e8-4b22-40ac-ba19-82ba5c71944c
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4aee16fc0dacce46e75735a161ae2c56d3bdb15
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990671"
---
# <a name="add-an-ios-line-of-business-app-to-microsoft-intune"></a>將 iOS 企業營運應用程式新增至 Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

使用本文中的資訊，協助您將 iOS 企業營運 (LOB) 應用程式新增至 Microsoft Intune。 企業營運 (LOB) 應用程式是您從 IPA 應用程式安裝檔案新增至 Intune 的應用程式。 這類應用程式通常是在內部撰寫的。 您必須先加入 iOS Developer Enterprise Program。 如需做法詳細資訊，請參閱 [Apple 的網站](https://developer.apple.com/programs/ios/enterprise/) \(英文\)。

> [!NOTE]
> iOS 裝置的使用者可以移除部分內建的 iOS 應用程式，例如股票和地圖。 您無法使用 Intune 來重新部署這些應用程式。 如果使用者刪除這些應用程式，則必須移至應用程式商店，並手動重新安裝。
>
> iOS LOB 應用程式對於每個應用程式設有 2 GB 的大小上限。

> [!NOTE]
> 組合識別碼 (例如，*com.contoso.app*) 必須為應用程式的唯一識別碼。 例如，若要在實際執行版本上安裝 LOB 應用程式的搶鮮版 (Beta)，以供測試之用，該搶鮮版 (Beta) 必須具有不同的唯一識別碼 (例如 *com.contoso.app-beta*)。 否則，該搶鮮版 (Beta) 會與實際執行版本重疊，並視其為升級。 重新命名 .ipa 檔案並不會影響此行為。

## <a name="select-the-app-type"></a>選取應用程式類型

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   > [所有應用程式]   > [新增]  。
3. 在 [選取應用程式類型]  窗格中，在 [其他]  應用程式類型底下，選取 [企業營運應用程式]  。
4. 按一下 [選取]  。 [新增應用程式]  步驟隨即顯示。

## <a name="step-1---app-information"></a>步驟 1 - 應用程式資訊

### <a name="select-the-app-package-file"></a>選取應用程式套件檔案

1. 在 [新增應用程式]  窗格中，按一下 [選取應用程式套件檔案]  。 
2. 在 [應用程式套件檔案]  窗格中，選取 [瀏覽] 按鈕。 然後選取副檔名為 **.ipa** 的 iOS 安裝檔案。
   應用程式詳細資料隨即顯示。
3. 當您完成時，請選取 [應用程式套件檔案]  窗格上的 [確定]  以新增應用程式。

### <a name="set-app-information"></a>設定應用程式資訊

1. 在 [應用程式資訊]  頁面中，新增應用程式的詳細資料。 窗格中某些值會隨著所選的應用程式自動填入。
    - **名稱**：輸入在公司入口網站中顯示的應用程式名稱。 確定您使用的所有應用程式名稱都是唯一的。 如果有重複的應用程式名稱，只有一個應用程式會出現在公司入口網站中。
    - **描述**：輸入應用程式的描述。 此描述會出現在公司入口網站上。
    - **發行者**：輸入應用程式發行者的名稱。
    - **最基本的作業系統**：從清單中，選擇能夠安裝應用程式的最基本作業系統版本。 若將應用程式指派給安裝舊版作業系統的裝置，就不會進行安裝。
    - **類別**：選取一或多個內建的應用程式類別，或選取您建立的類別。 類別可以讓使用者在瀏覽公司入口網站時，更輕鬆地找到應用程式。
    - **將此顯示為公司入口網站中的精選應用程式**：當使用者瀏覽應用程式時，在公司入口網站的主頁面上，以突顯的方式顯示應用程式。
    - **資訊 URL**：(選用) 輸入包含此應用程式相關資訊的網站 URL。 此 URL 會出現在公司入口網站上。
    - **隱私權 URL**：(選擇性) 輸入包含這個應用程式之隱私權資訊的網站 URL。 此 URL 會出現在公司入口網站上。
    - **開發人員**：(選擇性) 輸入應用程式開發人員的姓名。
    - **擁有者**：(選擇性) 輸入此應用程式之擁有者的名稱。 **人力資源部門**就是一個例子。
    - **附註**：輸入要與此應用程式建立關聯的任何附註。
    - **標誌**：上傳與應用程式相關聯的圖示。 這是使用者瀏覽公司入口網站時，會隨應用程式一起顯示的圖示。
2. 按一下 [下一步]  以顯示 [範圍標籤]  頁面。

## <a name="step-2---select-scope-tags-optional"></a>步驟 2 - 選取範圍標籤 (選擇性)
您可以使用範圍標籤來決定可在 Intune 中看見用戶端應用程式資訊的人員。 如需範圍標籤的完整詳細資料，請參閱[針對分散式 IT 使用角色型存取控制和範圍標籤](../fundamentals/scope-tags.md)。

1. 按一下 [選取範圍標籤]  以選擇性地為應用程式新增範圍標籤。 
2. 按一下 [下一步]  以顯示 [指派]  頁面。

## <a name="step-3---assignments"></a>步驟 3 - 指派

1. 為應用程式選取 [必要]  、[適用於已註冊的裝置]  、[無論註冊與否均可使用]  或 [解除安裝]  群組指派。 如需詳細資訊，請參閱[新增群組來組織使用者和裝置](../fundamentals/groups-add.md)與[使用 Microsoft Intune 將應用程式指派給群組](apps-deploy.md)。
2. 按一下 [下一步]  以顯示 [檢閱 + 建立]  頁面。

## <a name="step-4---review--create"></a>步驟 4 - 檢閱 + 建立

1. 檢閱您針對應用程式所輸入的值與設定。
2. 當您完成時，請按一下 [建立]  以將應用程式新增到 Intune。

    企業營運應用程式的 [概觀]  刀鋒視窗隨即顯示。

您所建立的應用程式現在會出現在應用程式清單中。 在清單中，您可以將應用程式指派給您選擇的群組。 如需協助，請參閱[如何將應用程式指派給群組](apps-deploy.md)。

> [!NOTE]
> iOS LOB 應用程式的佈建設定檔到期前有 30 天的通知時間。

## <a name="step-5-update-a-line-of-business-app"></a>步驟 5：更新企業營運應用程式

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

企業營運應用程式的更新將會自動安裝。

> [!NOTE]
> 若要讓 Intune 服務成功地將新的 IPA 檔案部署到裝置，您必須對 IPA 套件中 Info.plist 檔案內的 `CFBundleVersion` 字串進行遞增處理。

## <a name="next-steps"></a>後續步驟

- 您所建立的應用程式會出現在應用程式清單中。 您現在可以將它指派給您選擇的群組。 如需協助，請參閱[如何將應用程式指派給群組](apps-deploy.md)。

- 深入了解您可用來監視應用程式屬性和指派的方式。 請參閱[如何監視應用程式資訊和指派](apps-monitor.md)。

- 深入了解您應用程式在 Intune 中的內容。 請參閱[裝置和應用程式生命週期的概觀](../fundamentals/device-lifecycle.md)。
