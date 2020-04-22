---
title: 設定網路喚醒
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中選取 [網路喚醒]。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 512d942d79d11178f010c4f0adb41a25ee432743
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694116"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>如何在 Configuration Manager 中設定網路喚醒

適用於：  Configuration Manager (最新分支)

當您想要將電腦從睡眠狀態喚醒時，針對 Configuration Manager 指定網路喚醒設定。

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a> 從 1810 版開始的網路喚醒
<!--3607710-->
從 Configuration Manager 1810 開始，將會有新的方法可以將睡眠中的電腦喚醒。 您可以從 Configuration Manager 主控台喚醒用戶端，即使該用戶端和站台伺服器沒有位於同一個子網路也一樣。 如果您需要執行維護作業或查詢裝置，不會受到睡眠的遠端用戶端所限。 站台伺服器會使用用戶端通知通道來識別在相同遠端子網路上甦醒的其他用戶端，並使用那些用戶端來傳送網路喚醒要求 (Magic 封包)。 使用用戶端通知通道可協助避免 MAC 翻動，其可能會造成路由器將連接埠關閉。 新版本的網路喚醒可與[舊版](#bkmk_wol-previous)同時啟用。

### <a name="limitations"></a>限制

- 目標子網路中至少有一個用戶端必須為喚醒狀態。
- 此功能不支援下列網路技術：
   - IPv6
   - 802.1x 網路驗證
    >[!NOTE]
    > 視硬體及其設定而定，802.1x 網路驗證可能可以搭配額外設定順利運作。
- 電腦只會在您透過 [喚醒]  用戶端通知來通知它們時才會甦醒。
    - 針對要在期限抵達時喚醒的功能，請使用舊版的網路喚醒。
    -  如果未啟用舊版功能，針對搭配 [使用網路喚醒來喚醒用戶端進行必要的部署]  或 [傳送喚醒封包]  設定所建立的部署將不會發生用戶端喚醒。  

> [!IMPORTANT]
> 建議一次只在有限數量的裝置 (100) 上使用網路喚醒功能。
>
> 當使用網路喚醒功能從 Configuration Manager 管理主控台喚醒電腦時，喚醒要求會放入其他即時動作功能所共用的內部佇列中。 這些其他功能的範例包括執行指令碼、CMPivot，以及其他快速通道用戶端通知。 視站台系統的效能而定，喚醒動作可能需要相當長的時間，且會延遲其他即時動作。 建議一次不要喚醒超過 100 部的電腦。 若要知道是否在此區域中累積可能會造成延遲的待辦事項，可以查看 ...\inboxes\objmgr.box 目錄，以確認是否有大量副檔名為 .OPA 的檔案。


### <a name="security-role-permissions"></a>安全性角色權限

- [集合] 類別底下的 [通知資源] 

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>從 1810 版開始設定用戶端以使用網路喚醒

以前您必須在網路介面卡的內容中手動啟用用戶端網路喚醒。 Configuration Manager 1810 包含名為 [允許網路喚醒]  的新用戶端設定。 請設定並部署此設定，而非修改網路介面卡的屬性。

1. 在 [系統管理]  底下，移至 [用戶端設定]  。
1. 選取您想要編輯的用戶端設定，或建立新的自訂用戶端設定來進行部署。 如需詳細資訊，請參閱[如何設定用戶端設定](configure-client-settings.md)。
1. 在 [電源管理]  用戶端設定底下，針對 [允許網路喚醒]  設定選取 [啟用]  。 如需此設定的詳細資訊，請參閱[關於用戶端設定](about-client-settings.md#power-management)。

4. 從 Configuration Manager 1902 開始，新版本的網路喚醒將會接受您針對 [網路喚醒連接埠號碼 (UDP)]  [ 用戶端設定](about-client-settings.md#power-management)指定的自訂 UDP 連接埠。 此設定會由新版和舊版的網路喚醒所共用。
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>從 1810 開始使用用戶端通知來喚醒用戶端
 
您現在可以喚醒單一用戶端或集合中任何睡眠中的用戶端。 針對集合中已經甦醒的裝置，系統將不會對它們採取任何動作。 系統只會將網路喚醒要求傳送給睡眠中的用戶端。 如需如何通知用戶端以將其喚醒的詳細資訊，請參閱[用戶端通知](../manage/client-notification.md)。

- **喚醒單一用戶端：** 以滑鼠右鍵按一下用戶端，移至 [用戶端通知]  ，然後選取 [喚醒]  。

   ![主控台中的喚醒用戶端通知](media/wol-wake-up-client-notification.png)

- **喚醒集合中所有睡眠中的用戶端：** 以滑鼠右鍵按一下裝置集合，移至 [用戶端通知]  ，然後選取 [喚醒]  。
   - 此動作不能在內建集合上執行。
   - 當您的集合中同時有睡眠中和已甦醒的用戶端時，系統只會將網路喚醒要求傳送給睡眠中的用戶端。
   - 從 Configuration Manager 2002 開始，可以從連線到管理中心網站、獨立站台或子主要站台的主控台使用此動作。
   - 在 1910 版和更早版本中，只有當 Configuration Manager 主控台連線至獨立或子主要站台時，此動作才會作用。 連線至管理中心網站時，無法使用此動作。

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>在僅啟用新版的網路喚醒時應預期的情況

當您僅啟用新版本的網路喚醒時，系統只會啟用 [喚醒]  用戶端通知。 系統不會在接收到部署期限 (例如工作順序、軟體散發或軟體更新安裝) 時，向用戶端傳送通知。 當睡眠中的電腦恢復上線時，在它與管理點簽入之後，便會被反映在主控台中。

從 Configuration Manager 1902 版開始，您可以指定網路喚醒連接埠。 此設定會由新版和舊版的網路喚醒所共用。

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>在同時啟用新版和舊版的網路喚醒時應預期的情況

當您同時啟用兩個版本的網路喚醒時，您可以使用 [喚醒]  用戶端通知，同時在期限抵達時喚醒。 用戶端通知的運作方式，與傳統網路喚醒會有點不同。 如需用戶端通知運作方式的簡短說明，請參閱[從 1810 版開始的網路喚醒](#bkmk_wol-1810)小節。 新的用戶端設定 [允許網路喚醒]  將會變更 NIC 屬性以允許網路喚醒。 您已不再需要針對新增至環境中的新電腦手動變更它。 網路喚醒的所有其他功能皆未變更。

從 1902 版開始，[喚醒]  用戶端通知會接受您現有的 [網路喚醒連接埠號碼 (UDP)]  設定。


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a> 適用於 1806 版及更早版本的網路喚醒

如果您想要讓電腦結束睡眠狀態以安裝必要的軟體，例如軟體更新、應用程式、工作順序及程式，請指定 Configuration Manager [網路喚醒] 設定。

您可以使用喚醒 Proxy 用戶端設定補充 [網路喚醒]。 不過，若要使用喚醒 Proxy，您必須先啟用站台的 [喚醒網路]，並指定 [僅使用喚醒封包]  及 [單點傳播]  選項做為 [網路喚醒] 傳輸方法。 此喚醒解決方案也支援臨機操作連線，例如遠端桌面連線。

請先利用程序設定 [網路喚醒] 的主要站台。 然後，使用第二項程序設定喚醒 Proxy 用戶端設定。 第二項程序會設定了喚醒 Proxy 設定的預設用戶端設定，以便套用至階層中的所有電腦。 如果您只想要將這些設定套用至選取的電腦，請建立自訂裝置設定，並將它指派至包含您要設定喚醒 Proxy 之電腦的集合。 如需如何建立自訂用戶端設定的詳細資訊，請參閱[如何設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md)。

接收喚醒 proxy 用戶端設定的電腦，可能會暫停其網路連線 1-3 秒。 這是因為用戶端必須重設網路介面卡，以啟用它的喚醒 Proxy 驅動程式。

> [!WARNING]
> 為避免非預期的網路服務中斷，請先在隔離且具代表性的網路基礎結構上評估喚醒 Proxy。 然後使用自訂用戶端設定，將測試擴充到數個子網路上所選取的電腦群組。 如需喚醒 Proxy 如何運作的詳細資訊，請參閱[規劃如何喚醒用戶端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>針對 1806 版及更早版本設定站台的網路喚醒

 若要使用網路喚醒，您必須針對階層中的每個站台設定它。

1. 在 Configuration Manager 主控台中，移至 [管理] > [站台設定] > [站台]  。
2. 按一下主要站台進行設定，然後按一下 [內容]  。
3. 按一下 [網路喚醒]  索引標籤，設定此站台所需要的選項。 若要支援喚醒 Proxy，請確定您選取了 [僅使用喚醒封包]  及 [單點傳播]  。 如需詳細資訊，請參閱[規劃如何喚醒用戶端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。
4. 按一下 [確定]  為階層中的所有主要站台重複此程序。

![在站台屬性中啟用網路喚醒](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>設定喚醒 proxy 用戶端設定

1. 在 Configuration Manager 主控台中，瀏覽至 [管理] > [用戶端設定]  。
2. 按一下 [預設用戶端設定]  ，然後按一下 [內容]  。
3. 選取 [電源管理]  ，然後針對 [啟用喚醒 Proxy]  選擇 [是]  。
4. 檢閱並設定其他喚醒 Proxy 設定 (如有需要)。 如需這些設定的詳細資訊，請參閱[電源管理設定](../../../core/clients/deploy/about-client-settings.md#power-management)。
5. 按一下 [確定]  以關閉對話方塊，然後按一下 [確定]  以關閉 [預設用戶端設定] 對話方塊。

您可以使用下列 [網路喚醒] 報告監控喚醒 Proxy 的安裝及設定：

- 喚醒 Proxy 的部署狀態摘要
- 喚醒 Proxy 的部署狀態詳細資料

> [!TIP]
> 若要測試喚醒 Proxy 是否可運作，請測試與睡眠中電腦的連線。 例如，連線至該電腦上的共用資料夾，或嘗試使用遠端桌面連線至電腦。 如果您使用 Direct Access，可嘗試對目前位於網際網路上的睡眠中電腦進行相同的測試，以檢查 IPv6 首碼是否正常運作。
