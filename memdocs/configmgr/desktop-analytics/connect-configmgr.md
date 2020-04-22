---
title: 連線 Configuration Manager
titleSuffix: Configuration Manager
description: 將 Configuration Manager 與電腦分析連線的操作指南。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0835892788f86e9c246ed98d46658025fbc4180d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708316"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>如何將 Configuration Manager 與電腦分析連線

電腦分析與 Configuration Manager 緊密整合。 首先，請先確認站台已更新至最新狀態，以支援最新功能。 然後，請在 Configuration Manager 中建立電腦分析連線。 最後，請監視連線的健全狀況。

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a> 更新站台

首先，請確認 Configuration Manager 正在執行的版本至少是 1902。 如需詳細資訊，請參閱[安裝主控台內的更新](../core/servers/manage/install-in-console-updates.md)。

您也需要安裝 1902 版更新彙總套件 (4500571) 來支援與電腦分析的整合。 如需此更新的詳細資訊，請參閱 [Configuration Manager 目前分支的更新彙總套件 (1902 版)](https://support.microsoft.com/help/4500571)。

1. 使用 1902 版的更新彙總套件來更新站台。 如需詳細資訊，請參閱[安裝主控台內的更新](../core/servers/manage/install-in-console-updates.md)。

2. 更新用戶端。 如果要簡化此程序，請考慮使用自動用戶端升級。 如需詳細資訊，請參閱[升級用戶端](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a> 連線至服務

> [!TIP]
> 請先建立步驟 8 中所述的目標集合後再啟動精靈，因為一旦啟動後，即無法在精靈外部選取。

使用此程序來將 Configuration Manager 連線到電腦分析，並設定裝置設定。 此程序是將階層附加至雲端服務的一次性程序。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。 選取功能區中的 [設定 Azure 服務]  。

    > [!TIP]
    > 從 [電腦分析服務]  節點直接連線到服務。 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，然後選取 [電腦分析服務]  節點。 在 [初次使用電腦分析嗎?]  方塊中，選取第二個連結以前往「將 Configuration Manager 連線至電腦分析服務」  。

2. 在 [Azure 服務精靈] 的 [Azure 服務]  頁面上，進行下列設定：

    - 為 Configuration Manager 中的物件指定 [名稱]  。

    - 指定選用 [描述]  以協助您識別服務。

    - 從可用的服務清單中選取 [電腦分析]  。

   選取 [下一步]  。

3. 在 [應用程式]  頁面上，選取適當的 **Azure 環境**。 然後針對 Web 應用程式選取 [瀏覽]  。

4. 若有想要針對此服務重複使用的現有應用程式，請從清單中選擇，然後選取 [確定]  。

5. 在大多數的案例中，您可以使用此精靈為電腦分析連線建立應用程式。 選取 [建立]  。<!-- 3572123 -->

    > [!TIP]
    > 若無法從精靈建立應用程式，則可在 Azure AD 中手動建立應用程式，然後匯入至 Configuration Manager。 如需詳細資訊，請參閱[對 Configuration Manager 建立及匯入應用程式](troubleshooting.md#create-and-import-app-for-configuration-manager)。

6. 在 [建立伺服器應用程式]  視窗中進行下列設定：

    - **應用程式名稱**：Azure AD 中應用程式的易記名稱。

    - **首頁 URL**：Configuration Manager 不使用此值，但卻是 Azure AD 的必要值。 根據預設，此值為 `https://ConfigMgrService`。

    - **App 識別碼 URI**：這在 Azure AD 租用戶中必須是唯一的值。 其位於 Configuration Manager 用戶端用來要求存取服務的存取權杖中。 根據預設，此值為 `https://ConfigMgrService`。

    - **祕密金鑰有效期間**：從下拉式清單中選擇 [1 年]  或 [2 年]  。 預設值為一年。

    選取 [登入]  。 向 Azure 成功驗證身分後，頁面會顯示 [Azure AD 租用戶名稱]  以供參考。

    > [!NOTE]
    > 以**全域管理員**身分完成此步驟。 Configuration Manager 不會儲存這些認證。 此角色在 Configuration Manager 中不需要權限，而且不需要為執行 Azure 服務精靈的相同帳戶。

    選取 [確定]  以在 Azure AD 中建立 Web 應用程式，然後關閉 [建立伺服器應用程式] 對話方塊。 在 [伺服器應用程式] 對話方塊上，選取 [確定]  。 然後在 [Azure 服務精靈] 的 [應用程式] 頁面上，選取 [下一步]  。

7. 在 [診斷資料]  頁面上，進行下列設定：

    - **商業識別碼**：此值應該會自動填入組織識別碼。 如果沒有，請先確定 Proxy 伺服器已設定為允許所有必要的[端點](enable-data-sharing.md#endpoints)並繼續。 或者，從[電腦分析入口網站](monitor-connection-health.md#bkmk_ViewCommercialID)手動取得商業識別碼。

    - **Windows 10 診斷資料層級**：至少選取 [基本]  。 請參閱[診斷資料層級](enable-data-sharing.md#diagnostic-data-levels)
  
    - **允許診斷資料中的裝置名稱**：選取 [啟用] 

        > [!NOTE]
        > 從 Windows 10 版本 1803 開始，根據預設，裝置名稱不會傳送至 Microsoft。 如未傳送裝置名稱，則其會在電腦分析中顯示為「不明」。 這種行為可能會讓您難以識別及評定裝置。

   選取 [下一步]  。 [可用的功能]  頁面會顯示可用電腦分析功能，其中包含上一頁中的診斷資料設定。 選取 [下一步]  以繼續，或 [上一步]  來進行變更。

    ![[Azure 服務精靈] 中的範例可用功能頁面](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. 在 [集合]  頁面上，進行下列設定：

    - **顯示名稱**：電腦分析入口網站會使用此名稱來顯示此 Configuration Manager 連線。 使用其來區別不同的階層，以及識別來自不同階層的集合。 使用詞彙輕鬆地區分您環境中的多個階層，例如：「測試實驗室」  或「生產」  。

    - **目標集合**：此集合包含 Configuration Manager 使用商業識別碼與診斷資料設定來進行設定的所有裝置。 這是一組由 Configuration Manager 連線至電腦分析服務的完整裝置。

    - **目標集合中的裝置使用使用者已驗證 Proxy 進行輸出通訊**：根據預設，此值為 [否]  。 視環境需要，請將其設定為 [是]  。

    - **選取要與電腦分析同步的特定集合**：選取 [新增]  以包含**目標集合**階層中的其他集合。 這些集合可以在電腦分析入口網站中使用，並與部署計劃組成群組。 請務必包含試驗與試驗排除集合。  <!-- 4097528 -->

        > [!TIP]
        > [選取集合] 視窗只會顯示受**目標集合**限制的集合。
        >
        > 在下列範例中，請選取 CollectionA 作為目標集合。 接著在新增其他集合時，您會看到 CollectionA、CollectionB 及 CollectionC。 您無法新增 CollectionD。
        >
        > - CollectionA：受**所有系統**集合限制
        >     - CollectionB：受 CollectionA 限制
        >         - CollectionC：受 CollectionB 限制
        > - CollectionD：受**所有系統**集合限制
        >
        > 若要管理電腦分析入口網站中可用來分組部署計劃的集合，請在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。 選取與**電腦分析** Azure 服務建立關聯的項目，然後在電腦分析的 [集合]  頁面中更新設定。

        > [!IMPORTANT]
        > 這些集合會隨著成員資格的變更，持續同步。 例如，您的目標集合使用具有 Windows 7 成員資格規則的集合。 當這些裝置升級至 Windows 10，且 Configuration Manager 評估集合成員資格時，這些裝置會從集合與電腦分析中移出。

9. 完成精靈。

Configuration Manager 會建立設定原則來設定目標集合中的裝置。 此原則包括可讓裝置將資料傳送至 Microsoft 的診斷資料設定。 根據預設，用戶端會每小時更新原則一次。 收到新的設定之後，可能需要數小時的時間，資料才可供電腦分析使用。

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a> 監視連線健全狀況

監視裝置的設定以進行電腦分析。 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [電腦分析服務]  節點，然後選取 [連線健全狀況]  儀表板。

如需詳細資訊，請參閱[監視連線健全狀況](monitor-connection-health.md)。

Configuration Manager 會在建立連線的 60 分鐘內同步集合。 在電腦分析入口網站中，前往 [通用試驗]  ，然後查看 Configuration Manager 裝置集合。

> [!NOTE]
> 電腦分析的 Configuration Manager 連線會依賴服務連接點。 對此站台系統角色所做的任何變更，可能會影響與雲端服務的同步處理。 如需詳細資訊，請參閱 [About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move) (關於服務連接點)。

## <a name="next-steps"></a>後續步驟

前往下一篇文章，以向電腦分析註冊裝置。
> [!div class="nextstepaction"]
> [註冊裝置](enroll-devices.md)
