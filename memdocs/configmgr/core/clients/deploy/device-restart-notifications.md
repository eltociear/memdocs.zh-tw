---
title: 裝置重新啟動通知
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中，重新啟動各種用戶端設定的通知行為。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693956"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager 中的裝置重新啟動通知

適用於：  Configuration Manager (最新分支)

使用者針對擱置裝置重新啟動所收到的通知，可能會根據[電腦重新啟動用戶端設定](about-client-settings.md#computer-restart)和使用的 Configuration Manager 版本而有所不同。 本文可協助管理員判斷哪個使用者體驗適用於擱置裝置重新啟動通知。

>[!NOTE]
> - 本文著重於可在 Configuration Manager 1902 版和 1906 版中找到的用戶端設定。


## <a name="deployment-types-for-restart-notifications"></a>適用於重新啟動通知的部署類型

[電腦啟動用戶端設定](about-client-settings.md#computer-restart)會針對需要下列重新啟動類型的所有必要部署變更使用者體驗：

- [應用程式](../../../apps/deploy-use/deploy-applications.md)
- [工作順序](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [軟體更新](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>重新啟動通知類型

需要重新啟動時，終端使用者會收到即將重新啟動的通知。 使用者會收到四個一般通知：

**快顯通知**會告知您需要重新啟動。 快顯通知中的資訊可能會根據您正在執行的 Configuration Manager 版本而有所不同。 此類型的通知是 Windows OS 原生的，而您也可能也會使用此類型的通知來查看協力廠商軟體。

![擱置重新啟動的快顯通知](media/3555947-restart-toast.png)

含有延遲選項的軟體中心通知會顯示強制重新啟動之前的剩餘時間。 根據您的 Configuration Manager 版本而定，訊息可能有所不同。

![具有延遲按鈕的擱置重新啟動軟體中心通知](media/3976435-snooze-restart-countdown.png)

使用者無法關閉的軟體中心最後倒數計時通知。 延遲按鈕會呈現灰色。

![軟體中心最後倒數計時通知](media/3976435-final-restart-countdown.png)

如果使用者主動安裝需要在期限到期前重新啟動的必要軟體，則會看到不同的通知。 當使用者體驗設定允許通知，而您並未針對部署使用快顯通知時，就會發生下列通知。 如需進行這些設定的詳細資訊，請參閱[部署**使用者體驗**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)和[必要部署的使用者通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)。

![主動安裝的軟體通知](media/3976435-proactive-user-restart-notification.png)

- 當您未使用快顯通知時，標示為**可用**的軟體對話方塊會與主動安裝的軟體類似。

  - 如果是**可用**的軟體，通知沒有重新啟動的期限，使用者可以選擇自己的延遲間隔。 如需詳細資訊，請參閱[核准設定](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)。

    ![標示為「可用」的軟體在通知中沒有重新啟動的期限。](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>1902 版中的裝置重新啟動通知

<!--3555947-->
有時使用者會看不到有關重新啟動或必要部署的 Windows 快顯通知。 然後他們就會看不到可將提醒延遲的體驗。 此行為可能導致在用戶端達到期限時，使用者無法獲得良好的體驗。

從 1902 版開始，需要進行軟體變更或需要重新啟動部署時，您可以選擇使用更具提示效果的對話視窗。

在用戶端設定的[電腦重新啟動](about-client-settings.md#computer-restart)群組中，啟用下列選項：[部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗]  。  

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

## <a name="device-restart-notifications-starting-in-version-1906"></a>在 1906 版中啟動的裝置重新啟動通知
<!--3976435-->
某些管理員偏好使用經常性重新啟動通知，以及可讓重新啟動延遲的短暫時間範圍。 其他管理員則允許使用者將重新啟動延遲一段較長的時間，並希望使用者不要經常收到擱置重新啟動通知。 Configuration Manager 1906 版讓管理員能夠進一步控制重新啟動通知的時間和頻率。 1906 中引進了下列項目，讓管理員能夠擁有更大的控制權：

- 已將 [指定電腦重新啟動倒數通知的延遲持續時間 (分鐘)]  新增至[電腦重新啟動用戶端設定](about-client-settings.md#computer-restart)。
- **向使用者顯示短暫的通知，指出使用者登出或電腦重新啟動之前間隔 (分鐘)** 的最大值，已從 1440 分鐘 (24 小時) 增加到 20160 分鐘 (兩週)。
- 在擱置的重新啟動少於 24 小時之前，使用者將不會在重新啟動通知中看到進度列。

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>在期限到期或之後安裝必要軟體時的通知

在期限到期或之後安裝必要軟體時，視您選取的用戶端設定而定，您的使用者將會看到通知。

如果已將 [部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗]  設定設為：

- **否**：會在進入最後倒數計時通知之前使用快顯通知。
- **是**：會顯示軟體中心通知。
  - 如果重新啟動超過 24 小時，則會顯示估計的重新啟動時間。 此通知的時機會以下列設定為基礎：**向使用者顯示暫時的通知，指出使用者登出或電腦重新啟動之前的間隔 (分鐘)** 。

     ![重新啟動時間超過 24 小時](media/3976435-notification-greater-than-24-hours.png)

  - 如果重新啟動少於 24 小時，則會顯示進度列。 此通知的時機會以下列設定為基礎：**向使用者顯示短暫的通知，指出使用者登出或電腦重新啟動之前的間隔 (分鐘)**

     ![重新啟動時間少於 24 小時](media/3976435-notification-less-than-24-hours.png)

如果使用者選取 [延遲]  按鈕，則將在延遲一段時間後發生另一個暫時通知，但前提是他們尚未進入最後倒數計時。 下一個通知的時機會以下列設定為基礎：**指定電腦重新啟動倒數通知的延遲持續時間 (小時)** 。 如果使用者選取 [延遲]  ，而您的延遲間隔是一小時，則將在 60 分鐘後再次通知使用者，但前提是他們尚未進入最後倒數計時。

進入最後倒數計時之後，系統會為使用者提供無法關閉的通知。 進度列為紅色，而且使用者無法點擊 [延遲]  。

![1906 版中的軟體中心最後倒數計時通知](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>使用者在期限到期之前主動安裝

如果使用者主動安裝需要在期限到期前重新啟動的必要軟體，則會看到不同的通知。 如需進行這些設定的詳細資訊，請參閱[部署**使用者體驗**設定](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)和[必要部署的使用者通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)。 

當使用者體驗設定允許通知，而您並未針對部署使用快顯通知時，就會發生下列通知：

![主動安裝的軟體通知](media/3976435-proactive-user-restart-notification.png)

一旦到達軟體的期限之後，就會遵循[在期限到期或之後安裝必要軟體時的通知](#notifications-when-required-software-is-installed-at-or-after-the-deadline)行為。

## <a name="log-files"></a>記錄檔

使用 **RebootCoordinator** 和 **SCNotify.log** 進行裝置重新啟動的疑難排解。 您可能也必須根據所使用的部署類型，使用其他用戶端[記錄檔](../../plan-design/hierarchy/log-files.md)。

## <a name="next-steps"></a>後續步驟

- [應用程式管理簡介](../../../apps/understand/introduction-to-application-management.md)
- [作業系統部署簡介](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [軟體更新管理簡介](../../../sum/understand/software-updates-introduction.md)
