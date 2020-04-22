---
title: Endpoint Protection 惡意程式碼定義
titleSuffix: Configuration Manager
description: 了解如何將 Configuration Manager 軟體更新設定為傳遞定義更新至用戶端電腦。
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 16dce8e11edbe41dda3dcbf0fd503374ce05bf83
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697256"
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>使用 Configuration Manager 軟體更新傳遞定義更新檔

適用於：  Configuration Manager (最新分支)


 您可以將 Configuration Manager 軟體更新設定為傳遞定義更新至用戶端電腦。 此程序是經由設定自動部署規則所完成。 開始建立自動部署規則之前，請確定您已設定 Configuration Manager 軟體更新。 如需詳細資訊，請參閱[軟體更新簡介](../../sum/understand/software-updates-introduction.md)。

> [!NOTE]
>  此程序僅供必須明確地為 Endpoint Protection 設定的項目所使用。 如需 [建立自動部署規則精靈] 的詳細資訊，請參閱[自動部署軟體更新](../../sum/deploy-use/automatically-deploy-software-updates.md)。

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>設定自動部署規則來傳遞定義更新

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。

2. 在 [軟體程式庫]  工作區中，展開 [軟體更新]  ，然後按一下 [自動部署規則]  。

3. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立自動部署規則]  。

4. 在 [建立自動部署規則精靈]  的 [一般]  頁面上，指定下列資訊：

   -   **名稱**：輸入自動部署規則的唯一名稱。

   -   **集合**：選取您要在其中部署定義更新的用戶端電腦集合。

       > [!NOTE]
       >  您無法將定義更新部署至使用者集合。

5. 按一下 [新增至現有的軟體更新群組]  。

6. 確定已選取 [在執行此規則後啟用部署]   核取方塊，然後按一下 [下一步]  。

7. 在精靈 [部署設定]  頁面上的 [詳細等級]  清單中，選取 [僅錯誤訊息]  ，然後按一下 [下一步]  。

   > [!NOTE]
   >  選取 [僅錯誤訊息]  會減少定義部署所傳回的狀態訊息數目。 這項設定有助於減少 Configuration Manager 伺服器上的 CPU 處理使用量。

8. 在 [內容篩選器]  清單中，選取 [更新分類]  核取方塊。

9. 在 [搜尋條件]  清單中，按一下 [<要尋找的項目\>]  。 然後，在 [搜尋條件]  對話方塊中的 [指定要搜尋的值]  清單中，選取 [定義更新]  。

10. 按一下 [確定]  以關閉 [搜尋條件]  對話方塊。

11. 在 [內容篩選器]  清單中，選取 [產品]  核取方塊。

12. 在 [搜尋條件]  清單中，按一下 [<要尋找的項目\>]  。 然後，在 [搜尋條件]  對話方塊中的 [指定要搜尋的值]  清單中，針對 Windows 8.1 及更早版本選取 [Forefront Endpoint Protection 2010]  ，或針對 Windows 10 及更新版本選取 [Windows Defender]  。

13. 按一下 [確定]  以關閉 [搜尋條件]  對話方塊，然後按一下 [下一步]  。

14. 或者，您可以篩選出被取代的更新。   操作方法：
    1.  在 [內容篩選器]  清單中，選取 [已取代]  核取方塊。
    2.  在 [搜尋條件]  清單中，按一下 [<要尋找的項目\>]  。 然後，在 [搜尋條件]  對話方塊中的 [指定要搜尋的值]  清單中，選取 [否]  。  <br><br>

15. 按一下 [確定]  以關閉 [搜尋條件]  對話方塊，然後按一下 [下一步]  。

16. 在精靈的 [評估排程]  頁面上，選取 [啟用規則以依排程執行]  ，然後設定用來下載定義更新的排程。 至少將規則設定為每次軟體更新點同步處理的兩個小時之後才執行。 按一下 [下一步]  。

17. 在精靈的 [部署排程]  頁面上，設定下列設定：

    -   **時間依據**：如果您想要階層中所有用戶端同時安裝最新的定義，則選取 [UTC]  。 實際的安裝時間會有所不同，但會在兩小時期間內完成。 這項設定是建議的最佳作法。

    -   **軟體可用時間**：指定此規則所建立的部署可用時間。 指定的時間必須至少為自動部署規則執行之後一小時。 這有助於確保內容有足夠的時間複寫至階層中的發佈點。 某些定義更新可能也包含反惡意程式碼引擎更新，因此可能需要更長時間才能連線到發佈點。

    -   **安裝期限**：選取 [盡快]  。

        > [!NOTE]
        >  軟體更新期限會有兩小時期間的差異，以防止所有的用戶端同時要求更新。

18. 按一下 [下一步]  。

19. 請在精靈 [使用者體驗]  頁面上的 [使用者通知]  清單中，選取 [在軟體中心和所有通知中隱藏]  。   這可確保以無訊息模式安裝定義更新。 按一下 [下一步]  。

20. 在精靈的 [警示]  頁面上，您不需要設定任何警示。 Configuration Manager 中的 Endpoint Protection 會產生任何可能需要的警示。 按一下 [下一步]  。

21. 在精靈的 [部署套件]  頁面上，選取現有部署套件或建立新的部署套件，以包含與規則相關聯的軟體更新檔案。

    > [!NOTE]
    >  請考慮將定義更新放在不包含其他軟體更新的套件中。 這項策略可保持較小的定義更新封裝大小，以更快速地複寫至發佈點。

22. 若要建立新套件，請在精靈的 [發佈點]  頁面上選取一或多個會將此套件的內容複製到其中的發佈點，然後按一下 [下一步]  。

23. 在精靈的 [下載位置]  頁面上，選取 [從網際網路下載軟體更新]  ，然後按一下 [下一步]  。

24. 在精靈的 [語言選擇]  頁面上，針對要下載的更新選取其每個語言版本，然後按一下 [下一步]  。

25. 在精靈的 [下載設定]  頁面上，選取所需的軟體更新下載行為，然後按一下 [下一步]  。

26. 在精靈的 [摘要]  頁面上，檢閱設定，然後按一下 [下一步]  。

26. 完成 [建立自動部署規則精靈]。

27. 確認新的規則會顯示在 Configuration Manager 主控台的 [自動部署規則]  節點中。


> [!div class="button"]
> [下一個步驟 >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [上一步 >](endpoint-configure-alerts.md)
