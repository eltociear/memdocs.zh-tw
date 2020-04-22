---
title: 監視用戶端
titleSuffix: Configuration Manager
description: 取得如何在 Configuration Manager 中監視用戶端的詳細指導方針
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1f31ac96f29fc302e601b8da071b1486f4e7df90
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696746"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>如何在 Configuration Manager 中監視用戶端

適用於：  Configuration Manager (最新分支)

在您站台中的 Windows 裝置上安裝 Configuration Manager 用戶端之後，即可在 Configuration Manager 主控台中監視其健康情況與活動。  


## <a name="about-client-status"></a><a name="bkmk_about"></a> 關於用戶端狀態

Configuration Manager 提供下列類型的資訊作為用戶端狀態：  

- **用戶端線上狀態**：如果裝置已連線到受指派的管理點，則該站台就會將裝置視為**線上**。 為了表示用戶端在線上，它會傳送類似 Ping 的訊息給管理點。 如果管理點未在 5 分鐘內收到訊息，則該站台就會將該用戶端視為**離線**。  

- **用戶端活動**：如果用戶端在過去七天內與 Configuration Manager 通訊，則該站台就會將用戶端視為**作用中**。 如果用戶端在七天內未完成下列動作，則該站台就會將用戶端視為**非使用中**：  

    - 要求原則更新  
    - 傳送活動訊號訊息  
    - 傳送硬體清查  

- **用戶端檢查**：Configuration Manager 用戶端在裝置上執行之定期評估的狀態。 此評估會檢查裝置，而且可以修復它所發現的一些問題。 如需詳細資訊，請參閱[用戶端健康情況檢查](#BKMK_ClientHealth)。  

     在執行 Windows 7 的裝置上，用戶端檢查會作為排定的工作執行。 在更新版本的 OS 上，用戶端檢查會在 Windows 維護期間自動執行。  

     您可以設定不在特定裝置上執行補救，例如攸關業務的伺服器。 如果還有其他要評估的項目，請使用 Configuration Manager 合規性設定來監視其他設定。 如需合規性設定的詳細資訊，請參閱[規劃和設定合規性設定](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

- **已解除任務**：該站台已標示要刪除的裝置記錄。 當相同裝置的新註冊分配給階層中相同或不同的主要站台時，可能會發生此行為。 該站台會在下次執行站台維護工作 (**刪除過時探索資料**) 時刪除這些裝置。<!-- SCCMDocs issue #1418 -->  

- **已淘汰**：該站台已發現具有相同硬體識別碼的新裝置記錄，因此它會將舊記錄標示為已過時。 報告不會多次計算相同裝置的過時記錄。 您仍然可以讓原則以過時的裝置為目標。 如果站台在 90 天無活動狀態後沒有取得過時記錄的活動訊號，則會在執行站台維護工作 (**刪除過時用戶端探索資料**) 時移除過時的裝置。


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a> 監視個別用戶端

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 選取 [裝置]  節點，或在 [裝置集合]  下選擇一個集合。  

    每一列列開頭的圖示都會指出裝置的線上狀態︰  

    |||  
    |-|-|  
    |![用戶端的線上狀態圖示](../../../core/clients/manage/media/online-status-icon.png)|裝置在線上|  
    |![用戶端的離線狀態圖示](../../../core/clients/manage/media/offline-status-icon.png)|裝置已離線|  
    |![用戶端的未知狀態圖示](../../../core/clients/manage/media/unknown-status-icon.png)|線上狀態未知|  
    |![未安裝用戶端](../../../core/clients/manage/media/client-not-installed.png)|用戶端未安裝在裝置上|  

2. 如需更詳細的線上狀態，請將用戶端線上狀態資訊新增至裝置檢視中。 以滑鼠右鍵按一下欄標頭，然後選取您想要新增的線上狀態欄位：

    - **裝置上線狀態**：指出用戶端目前在線上或離線。 (此狀態與圖示所提供的相同)。  

    - **前次上線時間**：指出用戶端線上狀態變更為線上的時間  

    - **前次離線時間**：指出狀態變更為離線的時間  

3. 在清單窗格中選取個別用戶端，以在詳細資料窗格中查看更多狀態。 此資訊包括用戶端活動與用戶端檢查狀態。  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a> 用戶端健全狀況儀表板

<!--3599209-->
您可以部署軟體更新及其他應用程式，以協助保護您的環境，但這些部署只能連到狀況良好的用戶端。 狀況不良的 Configuration Manager 會對整體合規性造成不良的影響。 判斷用戶端的健全狀況可能會十分有挑戰性，而這會依其分母而定：應共有多少裝置在您的管理範圍中？ 例如，若您從 Active Directory 探索所有的系統，即使其中某些記錄屬於已停用的電腦，這程序仍會增加您的分母。

從 1902 版開始，您可以檢視環境中含有 Configuration Manager 用戶端健康情況相關資訊的儀表板。 檢視您的用戶端健全狀況、案例健全狀況，以及常見錯誤。 透過數個屬性來篩選檢視，即可查看 OS 及用戶端版本的任何潛在問題。

在 Configuration Manager 主控台中，按一下 [監視]  工作區。 展開 [用戶端狀態]  ，然後選取 [用戶端健全狀況儀表板]  節點。

![用戶端健康情況儀表板螢幕擷取畫面](media/3599209-client-health-dashboard.png)

> [!Tip]  
> 沒有任何要 ccmeval 的變更。  

用戶端健全狀況儀表板預設會顯示線上用戶端，以及過去三年作用中的用戶端。 因此，您在此儀表板中看到的數目，可能與其他用戶端健全狀況歷程記錄來源中的數目不同。 例如，[用戶端狀態]  底下的其他節點，或是用戶端狀態類別中的報告。

### <a name="filters"></a>篩選

在儀表板的頂端，有可以調整顯示於儀表板上資料的一組篩選。

- **集合**：根據預設，會顯示裝置的儀表板位於 [所有系統]  集合中。 從清單選取裝置集合，即可將檢視範圍縮小到特定集合中裝置的子集。  

- **上線/離線**：根據預設，儀表板只會顯示上線的用戶端。 此狀態來自用戶端通知通道，該通道每五分鐘就會更新用戶端的狀態。 如需詳細資訊，請參閱[關於用戶端狀態](monitor-clients.md#bkmk_about)。  

- [使用 \# 天]  ：根據預設，儀表板會顯示過去三天使用過的用戶端。  

- **僅限失敗**：將檢視範圍縮小到只有回報用戶端健全狀況失敗的裝置。  

    > [!Tip]  
    > 搭配用戶端版本及 OS 版本磚使用此篩選。 如需詳細資訊，請參閱[版本磚](#version-tiles)。

### <a name="client-health-percentage"></a>用戶端健全狀況百分比

此磚可顯示您階層中的整體用戶端健全狀況。

狀況良好的 Configuration Manager 用戶端具有以下屬性：

- Online  
- 正在傳送資料  
- 通過全部用戶端健全狀況評估檢查  

如需詳細資訊，請參閱[關於用戶端狀態](monitor-clients.md#bkmk_about)。

狀況良好的用戶端成功與站台通訊。 其會根據用戶端設定中的已定義排程回報所有資料。

選取此圖表的區段，即可向下切入至裝置清單檢視。

### <a name="version-tiles"></a>版本磚

有兩個可以依 Configuration Manager 用戶端版本及 OS 版本，顯示用戶端健全狀況的磚。 當您對 [僅限失敗]  等篩選進行變更時，這些磚非常實用。 其可協助特別提示特定版本上是否有任何問題持續出現。 使用此資訊協助您做出升級決策。

選取這些圖表的區段，即可向下切入至裝置清單檢視。

### <a name="scenario-health"></a>案例健全狀況

此橫條圖會顯示以下核心案例的整體健全狀況：

- 用戶端原則
- 活動訊號探索
- 硬體清查
- 軟體清查
- 狀態訊息

使用選取器調整圖表中特定案例的焦點。

永遠顯示以下兩個橫條：

- **已合併 (全部)** ：全部案例的組合 (和)  
- **已合併 (任何)** ：至少一個情節 (或)

> [!Tip]  
> 案例健全狀況並非從您用戶端設定的組態測量得出。 這些值會根據每個裝置的原則結果組而有所不同。 使用以下步驟來調整案例健全狀況的評估期：
>
> - 前往 Configuration Manager 主控台中的 [監視]  工作區，然後選取 [用戶端狀態]  節點。  
> - 在功能區中選取 [用戶端狀態設定]  。  
>
> 根據預設，若用戶端沒有在 **7 天**內傳送案例特定資料，則對於該案例，Configuration Manager 會認為用戶端狀況不良。

### <a name="top-10-client-health-failures"></a>前 10 個用戶端健全狀況失敗

此圖表會列出環境中最常見的失敗。 這些錯誤來自 Windows 或 Configuration Manager。

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> 監視所有用戶端的狀態

1. 前往 Configuration Manager 主控台中的 [監視]  工作區，然後選取 [用戶端狀態]  節點。 檢閱整個站台的用戶端活動與用戶端檢查的整體統計資料。 選擇不同的集合來變更資訊的範圍。  

2. 若要深入了解回報的統計資料，請選擇回報資訊的名稱。 例如，**已通過用戶端檢查的作用中用戶端或沒有結果**。 然後檢閱有關個別用戶端的資訊。  

3. 選取 [用戶端活動]  以查看顯示您 Configuration Manager 站台中用戶端活動的圖表。  

4. 選取 [用戶端檢查]  km以查看顯示您 Configuration Manager 站台中用戶端檢查狀態的圖表。  

    設定警示，以在用戶端檢查結果或用戶端活動低於指定百分比時通知您。 當指定百分比之用戶端上的補救失敗時，該站台也可以警示您。 如需詳細資訊，請參閱[如何設定用戶端狀態](../deploy/configure-client-status.md)。  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a> 用戶端健康情況檢查

用戶端檢查會執行下列檢查和補救：  

|用戶端檢查|補救動作|更多資訊|  
|------------------|------------------------|----------------------|  
|確認最近有執行用戶端檢查|執行用戶端檢查|確認過去三天內是否至少執行一次用戶端檢查。|  
|確認已安裝用戶端必要條件|安裝用戶端必要條件|確認是否已安裝用戶端必要條件。 閱讀用戶端安裝資料夾中的檔案 ccmsetup.xml，以探索必要條件。|  
|WMI 存放庫完整性測試|重新安裝 Configuration Manager 用戶端|確認 Configuration Manager 用戶端項目是否存在於 WMI 中。|  
|確認用戶端服務正在執行|啟動用戶端 (SMS Agent Host) 服務|沒有其他資訊|  
|WMI 事件接收測試。|重新啟動用戶端服務|確認是否遺失 Configuration Manager 相關 WMI 事件接收測試|  
|確認 Windows Management Instrumentation (WMI) 服務已存在|沒有補救措施|沒有其他資訊|  
|確認已正確安裝用戶端|重新安裝用戶端|沒有其他資訊|  
|確認反惡意程式碼服務啟動類型為自動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認反惡意程式碼端服務正在執行|啟動反惡意程式碼服務|沒有其他資訊|  
|確認 Windows Update 服務啟動類型為自動或手動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認用戶端服務 (SMS Agent Host) 啟動類型為自動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認 Windows Management Instrumentation (WMI) 服務正在執行。|啟動 Windows Management Instrumentation 服務|沒有其他資訊|  
|確認 Microsoft SQL CE 資料庫是否狀況良好|重新安裝 Configuration Manager 用戶端|沒有其他資訊|  
|Microsoft Policy Platform WMI 完整性測試|修復 Microsoft Policy Platform|沒有其他資訊|  
|確認 Microsoft Policy Platform 服務存在|修復 Microsoft Policy Platform|沒有其他資訊|  
|確認 Microsoft Policy Platform 服務啟動類型為手動。|將服務啟動類型重設為手動|沒有其他資訊|  
|確認背景智慧型傳送服務已存在|沒有補救措施|沒有其他資訊|  
|確認背景智慧型傳送服務啟動類型為自動或手動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認網路檢查服務啟動類型為手動|將服務啟動類型重設為手動 (如果已安裝)|沒有其他資訊|  
|確認 Windows Management Instrumentation (WMI) 服務啟動類型為自動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認 Windows Update 服務在 Windows 8 裝置上的啟動類型為自動或手動|將服務啟動類型重設為手動|沒有其他資訊|  
|確認用戶端 (SMS Agent Host) 服務是否存在。|沒有補救措施|沒有其他資訊|  
|確認 Configuration Manager 遠端控制服務啟動類型為自動或手動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認 Configuration Manager 遠端控制服務正在執行|啟動遠端控制服務|沒有其他資訊|  
|確認喚醒 Proxy 服務 (ConfigMgr Wake-up Proxy) 正在執行|啟動 ConfigMgr Wakeup Proxy 服務|此用戶端檢查只有在所支援用戶端作業系統上的 [電源管理]  ：[啟用喚醒 Proxy]  用戶端設定已設為 [是]  時才能進行。|  
|確認喚醒 Proxy 服務 (ConfigMgr Wake-up Proxy) 啟動類型為自動|將 ConfigMgr Wakeup Proxy 服務啟動類型重設為自動|此用戶端檢查只有在所支援用戶端作業系統上的 [電源管理]  ：[啟用喚醒 Proxy]  用戶端設定已設為 [是]  時才能進行。|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>用戶端部署記錄檔

如需用戶端部署與管理作業所使用之記錄檔的相關詳細資訊，請參閱[記錄檔](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)。
