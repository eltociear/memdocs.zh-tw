---
title: 在電腦分析中註冊裝置
titleSuffix: Configuration Manager
description: 了解如何在電腦分析中註冊裝置。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: acb8900a57408152133637ead3b8a0cf4732b4a7
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268720"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>如何在電腦分析中註冊裝置

當您[連線 Configuration Manager](connect-configmgr.md) 至電腦分析時，您可以進行設定以將裝置註冊至電腦分析。 您可隨時變更這些設定。 此外，請確保裝置是最新的。

## <a name="update-devices"></a>更新裝置

電腦分析使用兩個主要的 Windows 元件：

- **相容性元件**：相容性元件 (**Appraiser**) 會對 Windows 裝置執行診斷，從而評估其與最新版 Windows 10 的相容性狀態。

- **已連線的使用者體驗與遙測服務**：啟用 Windows 診斷資料之後，已連線的使用者體驗與遙測服務 (**DiagTrack**) 將會收集系統、應用程式與驅動程式的資料。 接著 Microsoft 會分析此資料，並透過電腦分析與您共用。

安裝這些元件的最新版本，以獲取電腦分析的最佳體驗。

下表列出各項元件在支援之 OS 版本上的更新：

| OS 版本 | Appraiser | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | 包含<sup>[附註 1](#bkmk_note1)</sup> | [最新的累積更新](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | 包含 | [最新的累積更新](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | 包含 | [最新的累積更新](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | 包含 | [最新的累積更新](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | 包含 | [最新的累積更新](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978)<sup>[附註 2](#bkmk_note2)</sup> | [最新的每月彙總](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664)<sup>[附註 3](#bkmk_note3)</sup> | [最新的每月彙總](https://support.microsoft.com/help/4009469) |

> [!TIP]
> 使用 Configuration Manager 安裝這些更新。 如需詳細資訊，請參閱 [Deploy software updates](../sum/deploy-use/deploy-software-updates.md) (部署軟體更新)。
>
> 在第一次安裝相容性更新之後，請將裝置重新開機。

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a> 附註 1：Windows 10

雖然 Windows 10 預設會包含這些元件，但 Windows 10 裝置仍需要最新的累積更新，才能獲取電腦分析的完整功能。 例如，評估裝置與最新 OS 版本的相容性，以及獲取部署與註冊狀態幾近即時的資訊。

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a> 附註 2：Windows 8.1

Microsoft 會定期增加對此元件的更新，但相關聯的知識庫編號不會變更。 請確保您一律擁有最新版本的更新。

此元件會對參與 Windows 客戶經驗改進計畫的 Windows 8.1 系統執行診斷。 這些診斷有助於判斷當升級至 Windows 10 時，是否會有相容性問題。

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a> 附註 3：Windows 7

若您的組織未將「每月品質彙總」更新套用到 Windows 7 裝置，而只套用了「僅限安全性」更新，您將會在[取代 KB 2952664 更新的清單](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c)中看到一些「僅限安全性」更新。 您可以安裝這些較新的更新，而不要安裝 KB 2952664。

> [!NOTE]
> 對於 Windows 8.1，Microsoft 只在「每月品質彙總」更新修訂了 KB 2976978。

## <a name="device-enrollment"></a>裝置註冊

電腦分析服務沒有可安裝的代理程式。 您需要在要監視的裝置上進行設定，以註冊裝置。 這些設定可以控制裝置應將其資料傳送至哪一個電腦分析執行個體，以及其他設定選項。

> [!Note]  
> 如果您先前已使用 Windows Analytics，請將相同的工作區用於電腦分析。 如果先前已經將裝置註冊至 Windows Analytics，則亦須將該裝置重新註冊至電腦分析。
>
> 每個 Azure AD 租用者只擁能有一個電腦分析工作區。 裝置只能將診斷資料傳送至一個工作區。  

Configuration Manager 提供整合式體驗，可讓您管理這些設定並將其部署至用戶端。 請使用 Configuration Manager 以獲得最佳體驗。

當連線 Configuration Manager 至電腦分析時，您可以進行設定以註冊裝置。 如需詳細資訊，請參閱[如何將 Configuration Manager 連線至電腦分析](connect-configmgr.md#bkmk_connect)。

若要變更這些設定，請使用下列程序：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。 選取與電腦分析的連線，然後選擇功能區中的 [屬性]  。

2. 在 [診斷資料]  頁面上，視需要對下列設定進行變更：  

    - **商業識別碼**：此值應該會自動填入組織識別碼。 如果沒有，請先確定 Proxy 伺服器已設定為允許所有必要的[端點](enable-data-sharing.md#endpoints)並繼續。 您也可以從[電腦分析入口網站](monitor-connection-health.md#bkmk_ViewCommercialID)，手動擷取您的商業識別碼。

    - **Windows 10 診斷資料層級**：如需詳細資訊，請參閱[診斷資料層級](enable-data-sharing.md#diagnostic-data-levels)。  

    - **允許診斷資料中的裝置名稱**：如需詳細資訊，請參閱[裝置名稱](#device-name)。  

    當對此頁面進行變更時，[可用的功能]  頁面會顯示電腦分析功能的預覽，以及選取的診斷資料設定。  

3. 在 [電腦分析連線]  頁面上，視需要對下列設定進行變更：

    - **顯示名稱**：電腦分析入口網站會使用此名稱來顯示此 Configuration Manager 連線。  

    - **目標集合**：此集合包含 Configuration Manager 使用商業識別碼與診斷資料設定來進行設定的所有裝置。 這是一組由 Configuration Manager 連線至電腦分析服務的完整裝置。  

    - **目標集合中的裝置使用使用者已驗證 Proxy 進行輸出通訊**：根據預設，此值為 [否]  。 視環境需要，請將其設定為 **Yes**。 如需詳細資訊，請參閱 [Proxy 伺服器驗證](enable-data-sharing.md#proxy-server-authentication)。

    - **選取特定集合並與電腦分析同步處理**：選取 [新增]  以包含**目標集合**階層中的其他集合。 這些集合可以在電腦分析入口網站中使用，並與部署計劃組成群組。 請確保此新增包含試驗與試驗排除集合。  <!-- 4097528 -->

        > [!IMPORTANT]
        > 這些集合會隨著成員資格的變更，持續同步。 例如，部署計劃使用含有 Windows 7 成員資格規則的集合。 當這些裝置升級至 Windows 10 時，Configuration Manager 會評定集合成員資格，而這些裝置將會從集合與部署計劃中移出。

### <a name="windows-settings"></a>Windows 設定

當 Configuration Manager 將裝置註冊到電腦分析之後，將會設定 Windows 原則，以設定裝置供電腦分析之用。 在大多數情況下，只會使用 Configuration Manager 來進行這些設定。 請不要將這些設定也套用到網域群組原則物件。

如需詳細資訊，請參閱[電腦分析的群組原則設定](group-policy-settings.md)。

### <a name="device-name"></a>裝置名稱

從 Windows 10 1803 版開始，已不再根據預設收集裝置名稱。 您需要另外加入，以使用診斷資料來收集裝置名稱。 如果沒有裝置名稱，則在評定升級為新版的 Windows 時，您會更難以識別需要注意的裝置。

若未傳送裝置名稱，其電腦分析中會顯示為「未知」：

![顯示「不明」名稱的電腦分析裝置清單](media/unknown-device-name.png)

在 Configuration Manager 設定中，有一個選項可供電腦分析設定此選項：[允許診斷資料中的裝置名稱]  。 此 Configuration Manager 設定控制 [Windows 原則設定](group-policy-settings.md) **AllowDeviceNameInTelemetry**。

### <a name="conflict-resolution"></a>衝突解決

一般而言，請使用 Configuration Manager 集合來針對處理電腦分析設定與註冊。 使用直接成員資格或查詢，以包含或排除集合中的裝置。 如需詳細資訊，請參閱[如何建立集合](../core/clients/manage/collections/create-collections.md)。

Configuration Manager 只有在值不存在時，才會進行 Windows 設定。 如果需要為唯一的一組裝置進行不同設定，則可使用[群組原則](group-policy-settings.md)。 群組原則所針對的設定會優先於 Configuration Manager 設定。

當設定診斷資料層級時，您可以設定裝置的界限。 根據預設，在 Windows 10 1803 版和更新版本中，使用者可以選擇設定較低的層級。 您可以使用 [Configure telemetry opt-in setting user interface] \(設定遙測加入設定使用者介面\)此群組原則設定來控制此行為  。 如需詳細資訊，請參閱[電腦分析的群組原則設定](group-policy-settings.md)。

### <a name="proxy-settings"></a>Proxy 設定

若您組織使用 Proxy 伺服器驗證來存取網際網路，請務必正確設定該驗證或您的裝置。 如需詳細資訊，請參閱 [Proxy 伺服器驗證](enable-data-sharing.md#proxy-server-authentication)。

## <a name="next-steps"></a>後續步驟

前往下一篇文章，以在電腦分析中建立部署計劃。
> [!div class="nextstepaction"]
> [建立部署計劃](create-deployment-plans.md)
