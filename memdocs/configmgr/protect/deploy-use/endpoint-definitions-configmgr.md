---
title: Endpoint Protection 惡意程式碼定義
titleSuffix: Configuration Manager
description: 了解如何將 Configuration Manager 軟體更新設定為傳遞定義更新至用戶端電腦。
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126070"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>使用 Configuration Manager 傳遞定義更新

適用於：  Configuration Manager (最新分支)

您可將 Configuration Manager 軟體更新設定為自動傳遞定義更新至用戶端電腦。 開始建立自動部署規則之前，請務必先設定 Configuration Manager 軟體更新。 如需詳細資訊，請參閱[軟體更新簡介](../../sum/understand/software-updates-introduction.md)。

> [!NOTE]
> 此程序特定於 Endpoint Protection。 如需自動部署規則的詳細資訊，請參閱[自動部署軟體更新](../../sum/deploy-use/automatically-deploy-software-updates.md)。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [軟體更新]  ，然後選取 [自動部署規則]  。

1. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [建立自動部署規則]  。

1. 在 [建立自動部署規則精靈]  的 [一般]  頁面上，指定下列資訊：

    - **名稱**：輸入自動部署規則的唯一名稱。

    - **集合**：選取要在其中部署定義更新的裝置集合。

        > [!NOTE]
        > 您無法將定義更新部署至使用者集合。

1. 選取 [新增至現有的軟體更新群組]  。

1. 選取 [在執行此規則後啟用部署]  。

1. 在精靈的 [部署設定]  頁面上，針對 [詳細等級]  ，選取 [僅錯誤訊息]  。

    > [!NOTE]
    > 當選取 [僅錯誤訊息]  時，會減少定義部署所傳送的狀態訊息數目。 這項設定有助於減少 Configuration Manager 伺服器上的 CPU 處理。

1. 在 [軟體更新]  頁面上：

    1. 選取 [更新分類]  屬性篩選。 在 [搜尋條件]  清單中，選取 [<要尋找的項目\>]  。

        在 [搜尋準則]  視窗中，選取 [定義更新]  ，然後選取 [確定]  。

    1. 選取 [產品]  屬性篩選。 在 [搜尋條件]  清單中，選取 [<要尋找的項目\>]  。

        在 [搜尋準則]  視窗中，針對 Windows 8.1 及較舊版本選取 [System Center Endpoint Protection]  ，或針對 Windows 10 及更新版本選取 [Windows Defender]  ，然後選取 [確定]  。

    > [!NOTE]
    > 或者，您可以篩選出被取代的更新。 選取 [已取代]  屬性篩選。 在 [搜尋條件]  清單中，選取 [<要尋找的項目\>]  。 在 [搜尋準則]  視窗中，選取 [否]  ，然後選取 [確定]  。

1. 在精靈的 [評估排程]  頁面上，選取 [每次軟體更新點同步處理後均執行規則]  。

1. 在精靈的 [部署排程]  頁面上，設定下列設定：

    - **時間依據**：如果想要所有用戶端同時安裝最新的定義，請選取 [UTC]  。 實際的安裝時間會有所不同，但會在兩小時內完成。

    - **軟體可用時間**：指定此規則所建立的部署可用時間。 指定的時間必須至少為自動部署規則執行之後一小時。 此設定有助於確保內容有足夠的時間複寫至發佈點。 某些定義更新可能也包含反惡意程式碼引擎更新，因此可能需要更長時間才能連線到發佈點。

    - **安裝期限**：選取 [盡快]  。

        > [!NOTE]
        > 軟體更新期限會有所不同，但會在兩小時期間完成。 此行為會防止所有用戶端同時要求更新。

1. 在精靈的 [使用者體驗]  頁面上，針對 [使用者通知]  ，選取 [在軟體中心和所有通知中隱藏]  。 使用此設定時，會以無訊息模式安裝定義更新。

1. 在精靈的 [部署套件]  頁面上選取現有部署套件，或建立新的套件。

    > [!NOTE]
    > 請考慮將定義更新放在不包含其他軟體更新的套件中。 這項策略可保持較小的定義更新封裝大小，以更快速地複寫至發佈點。

1. 如果您建立新的部署套件，請在精靈的 [發佈點]  頁面上選取一或多個發佈點。 網站會將此套件的內容複寫至這些發佈點。

1. 在 [下載位置]  頁面上，選取 [從網際網路下載軟體更新]  。

1. 在 [語言選擇]  頁面上，針對要下載的更新選取其每個語言版本。

1. 在 [下載設定]  頁面上，選取所需的軟體更新下載行為。

1. 完成精靈。

驗證 Configuration Manager 主控台的 [自動部署規則]  節點會顯示新規則。

> [!div class="nextstepaction"]
> [建立及部署反惡意程式碼原則](endpoint-antimalware-policies.md)
