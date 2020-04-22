---
title: 使用 Microsoft Intune 將內建應用程式新增到行動裝置
titleSuffix: ''
description: 了解如何使用 Intune 以更容易安裝內建應用程式行動裝置。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0ec8de66-5a0f-4c8d-afbf-c2becc7d6eec
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74db26a3d5f80a0192e996913177745c0b438ac6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80324922"
---
# <a name="add-built-in-apps-to-microsoft-intune"></a>將內建應用程式新增至 Microsoft Intune

「內建」  應用程式類型可讓您輕鬆將準備好的受控應用程式 (例如 Office 365 應用程式) 指派給 iOS/iPadOS 與 Android 裝置。 您可以指派此應用程式類型的特定應用程式，例如 Excel、OneDrive、Outlook、Skype 及其他。 新增應用程式之後，應用程式會顯示為*內建 iOS 應用程式*或*內建 Android 應用程式*。 使用內建應用程式類型，您可以選擇向裝置使用者發佈這些應用程式的哪一些。

在舊版的 Intune 主控台中，Intune 提供數種預設的受控 Office 365 應用程式，例如 Outlook 和 OneDrive。 這些受控應用程式的應用程式類型標記為*受控 iOS Store 應用程式*或*受控 Android 應用程式*。 我們不建議使用這些應用程式類型，請使用內建應用程式類型。 藉著使用程式類型，您能夠獲得編輯及刪除 Office 365 應用程式的額外彈性。

>[!NOTE]
>當所有指派都已刪除時，標記為*受控 iOS 市集*和*受控 Android 應用程式*的預設 Office 365 應用程式就會從應用程式清單中移除。

## <a name="add-a-built-in-app"></a>新增內建應用程式

若要將內建應用程式新增至 Microsoft Intune 的可用應用程式，請執行下列作業：
1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [應用程式]   > [所有應用程式]   > [新增]  。
3. 在 [選取應用程式類型]  窗格中，在可用的 [市集應用程式]  類型下，選取 [內建應用程式]  。
4. 按一下 [選取]  。 [新增應用程式]  步驟隨即顯示。
5. 在 [選取內建應用程式]  頁面中，按一下 [選取應用程式]  來選取您想要包含的應用程式。
6. 選取您想要包含的內建應用程式。 
7. 在您選取應用程式之後，請按一下 [選取內建應用程式]  窗格上的 [選取]  。
8. 按一下 [下一步]  以顯示 [範圍標籤]  頁面。
9. 按一下 [選取範圍標籤]  來選擇性地為應用程式新增範圍標籤。 如需詳細資訊，請參閱[針對分散式 IT 使用角色型存取控制 (RBAC) 和範圍標籤](../fundamentals/scope-tags.md)。
10. 按一下 [下一步]  以顯示 [指派]  頁面。
11. 為應用程式選取群組指派。 如需詳細資訊，請參閱[新增群組來組織使用者與裝置](../fundamentals/groups-add.md)。 
12. 按一下 [下一步]  以顯示 [檢閱 + 建立]  頁面。 檢閱您針對應用程式所輸入的值和設定。
13. 當您完成時，請按一下 [建立]  以將應用程式新增到 Intune。

    您所建立之應用程式的 [概觀]  刀鋒視窗隨即顯示。

## <a name="configure-app-information"></a>設定應用程式資訊

您可修改內建應用程式的相關資訊。 這項資訊可協助您在 Intune 中識別應用程式，並幫助使用者在公司入口網站中尋找應用程式。
1. 選取 [應用程式]   > [所有應用程式]  ，並選取您想要修改的內建應用程式。  
   即會顯示內建應用程式的窗格。
2. 選取 [屬性]  。
3. 選取 [應用程式資訊]  旁邊的 [編輯]  。
4. 在 [應用程式資訊]  窗格中，您可修改下列資訊：
    - **名稱**：輸入將顯示在公司入口網站中的內建應用程式名稱。 確定您使用的所有名稱都是唯一的。 如果有重複的應用程式名稱，使用者只會在公司入口網站中看到其中一個應用程式。
    - **描述**：輸入應用程式的描述。 
    - **發行者**：輸入應用程式發行者的名稱。
    - **類別**：(選擇性) 選取一或多個內建應用程式類別。 設定此選項可讓使用者在瀏覽公司入口網站時，更輕鬆地找到應用程式。
    - **將此顯示為公司入口網站中的精選應用程式**：當使用者瀏覽應用程式時，在公司入口網站的主頁面上，以突顯的方式顯示應用程式。
    - **資訊 URL**：(選用) 輸入包含此應用程式相關資訊的網站 URL。 使用者會在公司入口網站中看到這個 URL。
    - **隱私權 URL**：(選擇性) 輸入包含這個應用程式之隱私權資訊的網站 URL。 使用者會在公司入口網站中看到這個 URL。
    - **開發人員**：(選擇性) 輸入應用程式開發人員的姓名。
    - **擁有者**：(選擇性) 輸入此應用程式的擁有者名稱 (例如「人力資源部門」  )。
    - **附註**：輸入要與此應用程式建立關聯的任何附註。
    - **上傳圖示**：上傳當使用者瀏覽公司入口網站時，隨應用程式一起顯示的圖示。
5. 按一下 [檢閱並儲存]  以顯示 [檢閱 + 建立]  頁面。 檢閱您針對應用程式所輸入的值和設定。
13. 完成後，請按一下 [儲存]  來在 Intune 中更新應用程式。

    您所建立之應用程式的 [概觀]  刀鋒視窗隨即顯示。

## <a name="next-steps"></a>後續步驟

- 您現在可以將應用程式指派給您選擇的群組。 如需詳細資訊，請參閱[將應用程式指派給群組](apps-deploy.md)。
