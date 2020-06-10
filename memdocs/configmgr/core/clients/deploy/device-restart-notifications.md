---
title: 裝置重新啟動通知
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中，重新啟動各種用戶端設定的通知行為。
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b326c4dd8112a72555239f2c3eda078ebf47bf82
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347214"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager 中的裝置重新啟動通知

適用於：Configuration Manager (最新分支)

使用者針對擱置裝置重新啟動所收到的通知，可能會根據[電腦重新啟動用戶端設定](#client-settings)與您所使用的 Configuration Manager 版本而有所不同。 此文章可協助您針對擱置裝置重新啟動通知設定使用者體驗。

## <a name="deployment-types-for-restart-notifications"></a>適用於重新啟動通知的部署類型

[電腦啟動用戶端設定](#client-settings)會針對需要下列重新啟動類型的所有必要部署變更使用者體驗：

- [應用程式](../../../apps/deploy-use/deploy-applications.md)
- [工作順序](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [軟體更新](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>重新啟動通知類型

當裝置需要重新啟動時，用戶端會向終端使用者顯示即將重新啟動的通知。 使用者會收到四種一般通知。

### <a name="toast-notification"></a>快顯通知

Windows 快顯通知會通知使用者裝置需要重新啟動。 快顯通知中的資訊可能會根據您正在執行的 Configuration Manager 版本而有所不同。 這種類型的通知是 Windows 作業系統的原生通知。 您也可以使用這種類型的通知來查看協力廠商軟體。

![擱置重新啟動的快顯通知](media/3555947-restart-toast.png)

### <a name="software-center-notification-with-snooze"></a>具有延遲的軟體中心通知

[軟體中心] 會顯示具有 [延遲] 選項與強制裝置重新啟動之前的剩餘時間的通知。 根據您的 Configuration Manager 版本而定，訊息可能有所不同。

![具有延遲按鈕的擱置重新啟動軟體中心通知](media/3976435-snooze-restart-countdown.png)

### <a name="software-center-final-countdown-notification"></a>軟體中心最後倒數計時通知

[軟體中心] 會顯示使用者無法關閉或延遲的這個最後倒數計時通知。

![軟體中心最後倒數計時通知](media/3976435-final-restart-countdown.png)

從 1906 版開始，在擱置的重新啟動少於 24 小時之前，使用者將不會在重新啟動通知中看到進度列。

### <a name="software-center-notification-before-deadline"></a>期限之前的 [軟體中心] 通知

如果使用者在期限之前主動安裝必要軟體 (且該軟體要求必須重新啟動)，則其會看到不同的通知。 當使用者體驗設定允許通知，而您並未針對部署使用快顯通知時，就會發生下列通知。 如需進行這些設定的詳細資訊，請參閱[部署**使用者體驗**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)和[必要部署的使用者通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)。

![主動安裝的軟體通知](media/3976435-proactive-user-restart-notification.png)

#### <a name="available-apps"></a>可用的應用程式

當您未使用快顯通知時，標示為**可用**的軟體對話方塊會與主動安裝的軟體類似。 如果是**可用**的軟體，通知沒有重新啟動的期限，使用者可以選擇自己的延遲間隔。 如需詳細資訊，請參閱[核准設定](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)。

![標示為「可用」的軟體在通知中沒有重新啟動的期限。](media/3555947-deployment-marked-available-restart.png)

## <a name="client-settings"></a>用戶端設計

若要控制用戶端重新啟動行為，請在 [電腦重新啟動] 群組中設定下列裝置用戶端設定。 如需詳細資訊，請參閱[如何設定用戶端設定](configure-client-settings.md)。

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>指定在裝置重新開機前一段期限後經過的時間 (分鐘)

此設定的持續時間必須比套用至電腦的最短維護時段還要短。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../manage/collections/use-maintenance-windows.md)。

預設值為 90 分鐘。 從 1906 版開始，最大值從 1440 分鐘 (24 小時) 增加到 20160 分鐘 (兩週)。

> [!NOTE]
> 此設定先前的標題為**向使用者顯示暫時的通知，指出使用者登出或電腦重新啟動之前的間隔 (分鐘)** 。

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>指定在裝置重新開機前，使用者顯示最後倒計時通知的時間長度 (分鐘)

此設定的持續時間必須比套用至電腦的最短維護時段還要短。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../manage/collections/use-maintenance-windows.md)。

預設值為 15 分鐘。

> [!NOTE]
> 此設定先前的標題為**顯示使用者無法關閉的對話方塊，其中顯示使用者登出或電腦重新啟動之前的倒數計時間隔 (分鐘)** 。

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>指定在重新啟動裝置前，在期限之後向使用者顯示提醒通知的頻率 (分鐘)
<!--3976435-->
_從 1906 版開始_

此頻率的持續時間值應小於**指定在裝置重新開機前一段期限後經過的時間 (分鐘)** 減去**指定在裝置重新開機前，使用者顯示最後倒計時通知的時間長度 (分鐘)** 的值。 否則，提醒通知將無法使用。

預設值為 240 分鐘。

> [!NOTE]
> 此設定先前的標題為**指定電腦重新啟動倒數通知的延遲持續時間 (分鐘)** 。

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗
<!--3555947-->
從 1902 版開始，將此設定設為 [是] 會將使用者體驗變更為更具提示效果。 此設定適用於所有應用程式、工作順序及軟體更新的部署。 如需詳細資訊，請參閱[針對軟體中心進行規劃](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)。

> [!IMPORTANT]
> 在 Configuration Manager 1902 中，在某些情況下，對話方塊將不會取代快顯通知。 若要解決此問題，請安裝 [Configuration Manager 1902 的更新彙總套件](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>裝置重新啟動通知 (1906 版)
<!--3976435-->
某些客戶偏好頻繁的重新啟動通知，並僅允許使用者延遲較短的時間。 其他客戶則允許使用者將重新啟動延遲一段較長的時間，而且不希望太頻繁地通知使用者有擱置的重新啟動。 從 Configuration Manager 1906 版開始，您可以進一步控制重新啟動通知的時間與頻率。

### <a name="install-required-software-at-or-after-the-deadline"></a>在期限或之後安裝必要軟體

在期限到期或之後安裝必要軟體時，視您選取的用戶端設定而定，您的使用者將會看到通知。

如果已將 [部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗] 設定設為：

- **否**：Windows 會顯示快顯通知，直到部署達到最後的倒數通知為止。

- **是**：[軟體中心] 會顯示通知：

  - 如果重新啟動超過 24 小時，則會顯示估計的重新啟動時間。 此通知的時機會以下列設定為基礎：**指定在裝置重新開機前一段期限後經過的時間 (分鐘)** 。

    ![重新啟動時間超過 24 小時](media/3976435-notification-greater-than-24-hours.png)

  - 如果重新啟動少於 24 小時，則會顯示進度列。 此通知的時機會以下列設定為基礎：**指定在裝置重新開機前一段期限後經過的時間 (分鐘)** 。

    ![重新啟動時間少於 24 小時](media/3976435-notification-less-than-24-hours.png)

如果使用者選取 [延遲]，則會在延遲期間過後顯示另一個暫時通知。 此行為假設其尚未達到最後倒數計時。 下一個通知的時機會以下列設定為基礎：**指定在重新開機裝置前，在期限之後向使用者顯示提醒通知的頻率 (分鐘)** 。 如果使用者選取 [延遲]，而您的延遲間隔為一小時，則 [軟體中心] 會在 60 分鐘後再次通知使用者。 此行為假設其尚未達到最後倒數計時。

當達到最後倒數時，[軟體中心] 會向使用者顯示無法關閉的通知。 進度列為紅色，而且使用者無法加以 [延遲]。

![1906 版中的軟體中心最後倒數計時通知](media/3976435-1906-final-restart-countdown.png)

### <a name="proactively-install-required-software-before-the-deadline"></a>在期限前主動安裝必要軟體

如果使用者主動安裝需要在期限前重新啟動的必要軟體，則會看到不同的通知。 如需進行這些設定的詳細資訊，請參閱[部署**使用者體驗**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)和[必要部署的使用者通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)。

當使用者體驗設定允許通知，而您並未針對部署使用快顯通知時，就會發生下列通知：

![主動安裝的軟體通知](media/3976435-proactive-user-restart-notification.png)

當部署達到期限後，[軟體中心] 會遵循此行為，[在期限或之後安裝必要軟體](#install-required-software-at-or-after-the-deadline)。

## <a name="example-configurations"></a>範例設定

下列範例說明如何設定用戶端設定，以達到特定的行為。

### <a name="reminders-are-off"></a>提醒已關閉

| 設定 | 值 |
|---------|---------|
|指定在裝置重新開機前一段期限後經過的時間 (分鐘)|180|
|指定在裝置重新開機前，使用者顯示最後倒計時通知的時間長度 (分鐘)|60|
|指定在重新開機裝置前，在期限之後向使用者顯示提醒通知的頻率 (分鐘)|240|
|部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗|否|

裝置會在部署期限後三小時 (**180** 分鐘) 重新啟動。 重新啟動之前一小時 (**60** 分鐘)，使用者會看到無法關閉或延遲的倒數計時。 第一個提醒通知會設定為在期限之後的四小時 (**240** 分鐘) 開始，這是在重新啟動之後。 因此，使用者看不到任何提醒。

### <a name="low-reminder-frequency"></a>低提醒頻率

| 設定 | 值 |
|---------|---------|
|指定在裝置重新開機前一段期限後經過的時間 (分鐘)|7200|
|指定在裝置重新開機前，使用者顯示最後倒計時通知的時間長度 (分鐘)|120|
|指定在重新開機裝置前，在期限之後向使用者顯示提醒通知的頻率 (分鐘)|900|
|部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗|是|

裝置會在部署期限後的五天 (**7200** 分鐘) 重新啟動。 重新啟動之前兩小時 (**120** 分鐘)，使用者會看到無法關閉或延遲的倒數計時。 此設定允許顯示提醒 118 小時 (`(7200 - 120) / 60`)。 期限後 15 小時 (**900** 分鐘)，[軟體中心] 會顯示第一個提醒。 每 15 小時 (**900 分鐘**) 會顯示最多 6 個額外提醒。 使用者會將提醒視為畫面上的視窗，而不是在幾秒內消失的通知。

### <a name="high-reminder-frequency"></a>高提醒頻率

| 設定 | 值 |
|---------|---------|
|指定在裝置重新開機前一段期限後經過的時間 (分鐘)|2880|
|指定在裝置重新開機前，使用者顯示最後倒計時通知的時間長度 (分鐘)|60|
|指定在重新開機裝置前，在期限之後向使用者顯示提醒通知的頻率 (分鐘)|30|
|部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗|是|

裝置會在部署期限後兩天 (**2880** 分鐘) 重新啟動。 重新啟動之前一小時 (**60** 分鐘)，使用者會看到無法關閉或延遲的倒數計時。 此設定允許顯示提醒 47 小時 (`(2880 - 60) / 60`)。 期限後 **30** 分鐘，[軟體中心] 會顯示第一個提醒。 每 **30 分鐘**會顯示最多 92 個額外提醒。 使用者會將提醒視為畫面上的視窗，而不是在幾秒內消失的通知。

## <a name="device-restart-notifications-version-1902"></a>裝置重新啟動通知 (1902 版)

<!--3555947-->
有時使用者會看不到有關重新啟動或必要部署的 Windows 快顯通知。 然後他們就會看不到可將提醒延遲的體驗。 此行為可能導致在用戶端達到期限時，使用者無法獲得良好的體驗。

從 1902 版開始，需要進行軟體變更或需要重新啟動部署時，您可以選擇使用更具提示效果的對話視窗。

在用戶端設定的[電腦重新啟動](#client-settings)群組中，啟用下列選項：[部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗]。  

設定此用戶端設定會針對需要從快顯通知中重新啟動的所有必要部署變更使用者體驗：

![[需要重新啟動] 的快顯通知](media/3555947-restart-toast-initial.png)  

到更具提示效果的對話視窗：

![[重新啟動您的電腦] 的對話視窗](media/3976435-proactive-user-restart-notification.png)

如果使用者未在安裝後重新啟動其裝置，則將收到通知作為提醒。 這個暫時的提醒將根據用戶端設定來向使用者顯示：**向使用者顯示暫時的通知，指出使用者登出或電腦重新啟動之前的間隔 (分鐘)** 。 此設定是使用者在強制重新啟動之前，必須重新啟動電腦的整體時間。

- 當您使用快顯通知時的暫時通知：

  ![擱置重新啟動的快顯通知](media/3555947-restart-toast.png)

- 當您使用軟體中心對話方塊視窗，而不是快顯時的暫時通知：

  ![具有延遲按鈕的擱置重新啟動軟體中心通知](media/3555947-1902-hide-notification.png)

如果使用者未在暫時通知之後重新啟動，系統將會為他們提供無法關閉的最後倒數計時通知。 最後通知出現的時機會根據用戶端設定而定：**顯示使用者無法關閉的對話方塊，其中顯示使用者登出或電腦重新啟動之前的倒數計時間隔 (分鐘)** 。 例如，如果設定為 60，則會在重新啟動的前一小時，強制向使用者顯示最後通知：

![軟體中心最後倒數計時通知](media/3555947-1902-final-countdown.png)

下列設定的持續時間必須比套用至電腦的最短[維護時段](../manage/collections/use-maintenance-windows.md)還要短：

- **向使用者顯示短暫的通知，指出使用者登出或電腦重新啟動之前的間隔 (分鐘)**
- **顯示使用者無法關閉的對話方塊，其中顯示使用者登出或電腦重新啟動之前的倒數計時間隔 (分鐘)**

> [!IMPORTANT]
> 在 Configuration Manager 1902 中，在某些情況下，對話方塊將不會取代快顯通知。 若要解決此問題，請安裝 [Configuration Manager 1902 的更新彙總套件](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->

## <a name="log-files"></a>記錄檔

若要進行裝置重新啟動的疑難排解，請使用用戶端上的 **RebootCoordinator.log** 與 **SCNotify.log** 檔案。 根據特定的部署類型，您可能也必須使用其他用戶端[記錄檔](../../plan-design/hierarchy/log-files.md)。

## <a name="next-steps"></a>後續步驟

- [如何設定用戶端設定](configure-client-settings.md)
- [應用程式部署**的使用者體驗**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [必要應用程式部署的使用者通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
