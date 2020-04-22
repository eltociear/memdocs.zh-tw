---
title: 1902 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 最新分支 1902 版所引進之變更和新功能的詳細資料。
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4972f6e8689ad44dbd1a19adcde104cd5f59038c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702396"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Configuration Manager 最新分支 1902 版的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 最新分支 1902 更新可以透過主控台內更新的方式取得。 在執行 1802、1806 或 1810 版的站台上套用此更新。 <!-- baseline only statement:-->在安裝新站台時，也可以基準版本的形式取得。 此文章摘要說明 Configuration Manager 1902 版的變更和新功能。  

請一律檢閱適用於安裝此更新的最新檢查清單。 如需詳細資訊，請參閱[安裝更新 1902 的檢查清單](../../servers/manage/checklist-for-installing-update-1902.md)。 更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist)。

若要充分利用 Configuration Manager 的新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> 已淘汰的功能和作業系統

在[已移除與已淘汰的項目](deprecated/removed-and-deprecated.md)中實作支援變更之前，請先了解這些變更。

- 從 Azure 共用內容的實作已經變更。 藉由啟用 [允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容]  選項，來使用啟用內容的雲端管理閘道。 未來您將無法建立傳統雲端發佈點。

1902 版已捨棄對下列產品的支援：  

- Linux 和 UNIX 作為用戶端。 淘汰隨 [1802 版](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support)宣布。 請考慮以 Microsoft Azure 管理來管理 Linux 伺服器。 Azure 解決方案具有廣泛的 Linux 支援，在大部分情況下都超越 Configuration Manager 的功能性，包括 Linux 的完整修補程式管理。


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> 站台基礎結構

### <a name="client-health-dashboard"></a>用戶端健全狀況儀表板

<!--3599209-->
您可以部署軟體更新及其他應用程式，以協助保護您的環境，但這些部署只能連到狀況良好的用戶端。 狀況不良的 Configuration Manager 會對整體合規性造成不良的影響。 判斷用戶端的健全狀況可能會十分有挑戰性，而這會依其分母而定：應共有多少裝置在您的管理範圍中？ 例如，若您從 Active Directory 探索所有的系統，即使其中某些記錄屬於已停用的電腦，這程序仍會增加您的分母。

您現可檢視環境中含有 Configuration Manager 用戶端健全狀況相關資訊的儀表板。 檢視您的用戶端健全狀況、案例健全狀況，以及常見錯誤。 透過數個屬性來篩選檢視，即可查看 OS 及用戶端版本的任何潛在問題。

在 Configuration Manager 主控台中，按一下 [監視]  工作區。 展開 [用戶端狀態]  ，然後選取 [用戶端健全狀況儀表板]  節點。

![用戶端健全狀況儀表板的螢幕擷取畫面](media/3599209-client-health-dashboard.png)

如需詳細資訊，請參閱[如何監視用戶端](../../clients/manage/monitor-clients.md#bkmk_health)。

### <a name="new-management-insight-rules"></a>新的管理見解規則

管理見解功能有下列新規則：

- 提供有關管理集合建議的多個規則。 使用這些見解可簡化管理並改善效能。 檢閱 [集合]  群組中的這些規則。<!--3555752-->  

- [管理簡單]  群組中的 [將用戶端更新為支援的 Windows 10 版本]  規則。 此規則會報告執行不再受支援之 Windows 10 版本的用戶端。 它也包含服務即將結束 (三個月) 的 Windows 10 版本。<!--3897268-->  

如需詳細資訊，請參閱[管理見解](../../servers/manage/management-insights.md)。

### <a name="improvement-to-enhanced-http"></a>對增強 HTTP 的改善

<!--3798957-->

您現在可以為每個主要站台或為管理中心網站啟用增強 HTTP。

在管理中心網站的屬性上，選取 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  選項。 此設定只會套用至管理中心網站中的站台系統角色。 它不是階層的全域設定。

如需詳細資訊，請參閱[增強式 HTTP](../hierarchy/enhanced-http.md)。

### <a name="improvement-to-setup-prerequisites"></a>安裝程式先決條件的改善

當您安裝或更新至 1902 版時，Configuration Manager 安裝程式現在包含下列先決條件檢查：

- **遠端 SQL Server 上的暫止系統重新啟動**：此先決條件檢查類似 [系統重新啟動擱置中]  規則，但它檢查的是遠端 SQL Server。 如需詳細資訊，請參閱[先決條件檢查清單](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server)。 <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> 雲端連結管理

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>雲端服務超過閾值時予以停止

<!--3735092-->
Configuration Manager 現可在總資料傳輸超過限制時，停止雲端管理閘道 (CMG) 服務。 CMG 一律具有警示，可在使用量達到警告或重大層級時，觸發通知。 為了協助減少因使用量突然增加而導致的任何非預期 Azure 成本，這個新選項會關閉雲端服務。

如需詳細資訊，請參閱[當 CMG 超過閾值時予以停止](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop)。

### <a name="use-azure-resource-manager-for-cloud-services"></a>將 Azure Resource Manager 用於雲端服務

<!--3605704-->
從 1810 版開始，Azure 已淘汰傳統服務部署，無法在 Configuration Manager 中使用。 該版本是支援建立這些 Azure 部署的最後版本。

現有的部署可繼續運作。 從這個最新分支版本開始，對於雲端管理閘道和雲端發佈點的新執行個體，Azure Resource Manager 是唯一的部署機制。

如需詳細資訊，請參閱[適用於雲端管理閘道的 Azure Resource Manager](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)。

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>將雲端管理閘道新增至界限群組

<!--3640932-->
您現在可以將雲端管理閘道 (CMG) 與界限群組建立關聯。 此設定可讓用戶端根據界限群組關聯性來預設或回復為 CMG 以進行用戶端通訊。 此行為在分公司和 VPN 案例中特別有用。 您可以將用戶端流量從昂貴且緩慢的 WAN 連結導向成改用 Microsoft Azure 較快的網際網路連線。

如需詳細資訊，請參閱 [CMG 階層設計](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design)和[設定 CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups)。


## <a name="real-time-management"></a><a name="bkmk_real"></a> 即時管理

### <a name="run-cmpivot-from-the-central-administration-site"></a>從管理中心網站執行 CMPivot

<!--3610960-->
Configuration Manager 現在支援從管理中心網站的階層中執行 CMPivot。 主要站台仍會處理與用戶端的通訊。 從管理中心網站執行 CMPivot 時，它會通過高速的訊息訂閱通道與主要站台進行通訊。 此通訊不依賴站台之間的標準 SQL 複寫。

如需詳細資訊，請參閱[即時資料的 CMPivot](../../servers/manage/cmpivot.md#bkmk_cmpivot1902)。

### <a name="edit-or-copy-powershell-scripts"></a>編輯或複製 PowerShell 指令碼

<!--3705507-->
您現已可**編輯**或**複製**與「執行指令碼」功能搭配使用的現有 PowerShell 指令碼。 現在您可以直接編輯指令碼，而不必重新建立需要變更的指令碼。 這兩個動作都使用您建立新指令碼時所使用的相同精靈體驗。 當您編輯或複製指令碼時，Configuration Manager 不會保存核准狀態。

如需詳細資訊，請參閱[執行指令碼](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit)。


## <a name="content-management"></a><a name="bkmk_content"></a> 內容管理

### <a name="distribution-point-maintenance-mode"></a>發佈點維護模式

<!--3555754-->

您現在可於維護模式中設定發佈點。 當您要安裝軟體更新，或對伺服器進行硬體變更時，請啟用維護模式。

發佈點處於維護模式時，它具有下列行為：

- 站台未散發任何內容給它。  

- 管理點不會將此發佈點的位置傳回給用戶端。

- 當您更新站台時，維護模式中的發佈點仍會更新。

- 發佈點屬性為唯讀。 例如，您無法變更憑證或新增界限群組。  

- 任何排程工作 (例如內容驗證) 仍然會按照相同的排程執行。

如需此功能的詳細資訊，請參閱[維護模式](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint)。

如需如何使用 Configuration Manager SDK 來將此程序自動化的詳細資訊，請參閱 [SMS_DistributionPointInfo 類別中的 SetDPMaintenanceMode 方法](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md)。


## <a name="client-management"></a><a name="bkmk_client"></a> 用戶端管理

### <a name="client-provisioning-mode-timeout"></a>用戶端佈建模式逾時

<!--3197824-->
工作順序會在將用戶端置於佈建模式時，設定時間戳記。 處於佈建模式的用戶端會在時間戳記以來的持續時間內每隔 60 分檢查一次。 如果它處於佈建模式的時間已超過 48 小時，用戶端會自動結束佈建模式，並重新啟動其程序。

如需詳細資訊，請參閱[佈建模式](../../../osd/understand/provisioning-mode.md)。

### <a name="view-first-screen-only-during-remote-control"></a>在遠端控制期間只檢視第一個畫面

<!--3231732-->
連線至具有兩個或更多個監視器的用戶端時，可能難以在 Configuration Manager 遠端控制檢視器中檢視所有這些監視器。 遠端工具操作員現已可選擇查看 [所有畫面]  或只查看 [第一個畫面]  。

如需詳細資訊，請參閱[如何從遠端管理 Windows 用戶端電腦](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)。

### <a name="specify-a-custom-port-for-peer-wakeup"></a>為對等喚醒指定自訂連接埠

<!--3605925-->
您現可指定用於喚醒 Proxy 的自訂連接埠號碼。 在用戶端設定中，在 [電源管理]  群組中，設定 [網路喚醒連接埠號碼 (UDP)]  的設定。  

如需詳細資訊，請參閱[如何設定網路喚醒](../../clients/deploy/configure-wake-on-lan.md)。


## <a name="application-management"></a><a name="bkmk_app"></a> 應用程式管理

### <a name="improvements-to-application-approvals-via-email"></a>對透過電子郵件進行應用程式核准的改善

<!--3594063-->
此版本提供接收應用程式要求電子郵件通知的功能改善。 使用者一律能夠從軟體中心將註解新增至要求。 此註解會在 Configuration Manager 主控台的應用程式要求中顯示。 現在，註解也會顯示於電子郵件中。 將此註解包含在電子郵件中，有助於核准者針對核准或拒絕要求，做出更佳的決策。

如需詳細資訊，請參閱[電子郵件通知](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)。

### <a name="improvements-to-package-conversion-manager"></a>改善套件轉換管理員

<!-- SCCMDocs-pr issue #3357 -->
此版本包含[套件轉換管理員](../../../apps/pcm/package-conversion-manager.md)的下列改善：

- 根據預設，已排程的套件分析會每 7 天執行一次
- 用來分析及轉換套件的 PowerShell Cmdlet
- 一般 Bug 修正和改善


## <a name="os-deployment"></a><a name="bkmk_osd"></a> 作業系統部署

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>就地升級工作順序期間的進度狀態

<!--3747129-->
您現在在 Windows 10 就地升級工作順序期間可以看到更詳細的進度列。 這個列會顯示 Windows 安裝程式的進度，否則安裝程式在工作順序期間會以無訊息方式進行。 使用者現在可以看到一些基礎的進度。 針對擔心升級程序因缺乏進度指示而被暫停的情況，這會有所幫助。  

![Windows 升級進度的相關範例工作順序進度](media/3747129-installation-progress.png)

此功能可與任何支援的 Windows 10 版本搭配使用，且只能搭配就地升級工作順序。

### <a name="improvements-to-task-sequence-media-creation"></a>工作順序媒體建立的改善

<!--3556027, fka 1359388-->
此版本包含幾個改善，可協助您建立及管理工作順序媒體更順手。 如需詳細資訊，請參閱下列適用於特定媒體類型的文章：

- [建立獨立媒體](../../../osd/deploy-use/create-stand-alone-media.md)
- [建立預先設置的媒體](../../../osd/deploy-use/create-prestaged-media.md)
- [建立可開機媒體](../../../osd/deploy-use/create-bootable-media.md)
- [建立擷取媒體](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>指定暫存位置

現在，當您建立工作順序媒體時，可以自訂站台使用的資料暫存位置。 此程序可能需要大量的暫存磁碟機空間。 這項變更可讓您擁有更大的彈性，以選擇要儲存這些暫存檔的位置。

在 [建立工作順序媒體精靈]  中，指定**複寫用快取資料夾**的位置。 根據預設，這個位置類似於下列路徑：`%UserProfile%\AppData\Local\Temp`。

#### <a name="add-a-label-to-the-media"></a>將標籤新增至媒體

您現在可以將標籤新增至工作順序媒體。 此標籤可協助您在建立媒體之後更輕鬆識別媒體。 在 [建立工作順序媒體精靈]  中，指定**媒體標籤**。

### <a name="import-a-single-index-of-an-os-image"></a>匯入 OS 映像的單一索引

<!--3719699-->
當您將 Windows 映像 (WIM) 檔匯入至 Configuration Manager 中時，現在可指定自動匯入單一索引，而不是檔案中的所有映像索引。 這個選項提供下列優點：

- 較小的映像檔  
- 更快速的離線服務  
- 最佳化映像服務，適用於離線服務後的較小映像檔

當您匯入 OS 映像時，選取 [從指定的 WIM 檔案擷取特定映像索引]  選項。 然後從清單中選取映像索引。  

如需詳細資訊，請參閱[新增 OS 映像](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)。

### <a name="optimized-image-servicing"></a>最佳化的映像服務

<!--3555951-->
當您將軟體更新套用至 OS 映像時，有一個新選項可藉由移除任何已取代的更新，將輸出最佳化。 離線服務的最佳化只適用於具有單一索引的映像。

當您建立排程以更新 OS 映像時，選取 [在更新映像後，移除已取代的更新]  選項。

如需詳細資訊，請參閱[將軟體更新套用至映像](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase)。

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>執行 PowerShell 指令碼工作順序步驟的改善

<!--3556028, fka 1359389-->
[執行 PowerShell 指令碼]  工作順序步驟現在包含下列改善：  

- 您現在可以在此步驟中直接輸入 Windows PowerShell 程式碼。 這項變更可讓您在工作順序期間執行 PowerShell 命令，而不需要先使用指令碼來建立和發佈套件。

- 當您選擇 [輸入 PowerShell 指令碼]  選項時，請選取 [編輯指令碼]  。 新的 PowerShell 指令碼視窗會提供下列動作：  

    - 直接編輯指令碼  

    - 從檔案開啟現有的指令碼  

    - 瀏覽至 Configuration Manager 中現有的已核准指令碼

- 將指令碼輸出儲存至自訂工作順序變數中  

- 若要在工作順序記錄中包含指令碼參數，請將工作順序變數 **OSDLogPowerShellParameters** 設定為 **TRUE**。 根據預設，參數並不在記錄中。  

- 提供類似[執行命令列](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)步驟之功能的其他改善。 例如，指定替代使用者認證，或指定逾時。

> [!Important]  
> 若要利用此 Configuration Manager 新功能，請在更新站台之後，也將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。

如需詳細資訊，請參閱[執行 PowerShell 指令碼](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)。

### <a name="other-improvements-to-os-deployment"></a>其他 OS 部署改善

<!--3633146,3641475,3654172,3734270-->
此版本包含 OS 部署的下列改善：

- 工作順序上有新的 [檢視]  預設動作。 <!--3633146-->  

- 工作順序錯誤對話視窗現在會顯示詳細資訊。 它會顯示失敗工作順序步驟的名稱。 <!--3641475-->  

- 當您將 **OSDDoNotLogCommand** 工作順序變數設為 true 時，現在也會從記錄檔的 [執行命令列] 步驟中隱藏命令列。 它之前只會遮罩 smsts.log 中 [安裝套件] 步驟的程式名稱。<!--3654172-->  

- 當您在發佈點上啟用 PXE 回應程式而不需要 Windows 部署服務時，它現在可位於與 DHCP 服務相同的伺服器上。 <!--3734270--> 如需詳細資訊，請參閱[將至少一個發佈點設定為接受 PXE 要求](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure)。


## <a name="software-center"></a><a name="bkmk_userxp"></a> 軟體中心

### <a name="replace-toast-notifications-with-dialog-window"></a>以對話視窗取代快顯通知

<!--3555947-->
有時使用者會看不到有關重新啟動或必要部署的 Windows 快顯通知。 然後他們就會看不到可將提醒延遲的體驗。 此行為可能導致在用戶端達到期限時，使用者無法獲得良好的體驗。

現在，當需要重新啟動部署或進行軟體變更時，您可以選擇使用更具提示效果的對話視窗。

如需詳細資訊，請參閱[針對軟體中心進行規劃](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)

### <a name="configure-user-device-affinity-in-software-center"></a>在軟體中心內設定使用者裝置親和性

<!--3485366-->
藉著從 1806 版開始的[軟體中心基礎結構改善](whats-new-in-version-1806.md#software-center-infrastructure-improvements)，大部分的情況下已不再需要應用程式類別目錄站台伺服器角色。 有些客戶仍依賴應用程式類別目錄，以讓使用者能夠設定主要裝置的使用者裝置親和性。

現在使用者可以在軟體中心內設定其主要裝置。 這個動作可讓他們成為 Configuration Manager 中的裝置主要使用者。

如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

### <a name="configure-default-views-in-software-center"></a>在軟體中心內設定預設檢視

<!--3612112-->
這一版 Configuration Manager 會進一步反覆說明如何自訂「軟體中心」：

- 設定應用程式的預設版面配置 (設定為圖格或清單)  

    - 如果使用者變更此設定，「軟體中心」未來將會保存使用者的喜好設定  

- 設定預設應用程式篩選 (全部或僅限所需的應用程式)  

    - 「軟體中心」一律會使用您的預設設定。 使用者可以變更此篩選，但「軟體中心」不會保存其喜好設定。

在用戶端設定的 [軟體中心]  群組中指定這些設定。

如需詳細資訊，請參閱[關於用戶端設定](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults)。


## <a name="software-updates"></a><a name="bkmk_sum"></a> 軟體更新

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>指定 Windows 10 服務中，功能更新的優先順序

<!--3734525-->
調整用戶端透過 [Windows 10 服務](../../../osd/deploy-use/manage-windows-as-a-service.md)安裝功能更新的優先順序。 根據預設，用戶端現在會以較高的處理優先順序來安裝功能更新。

用戶端設定來設定此選項。 在 [軟體更新]  群組中，進行下列設定：[指定功能更新的執行緒優先順序]  。

如需詳細資訊，請參閱[關於用戶端設定](../../clients/deploy/about-client-settings.md#software-updates)。


## <a name="office-management"></a><a name="bkmk_o365"></a> Office 管理

### <a name="redirect-windows-known-folders-to-onedrive"></a>將 Windows 已知資料夾重新導向至 OneDrive

<!--3556021-->
使用 Configuration Manager 將 Windows 已知資料夾移至「商務用 OneDrive」。 這些資料夾包括 [桌面]、[文件] 及 [圖片]。 若要簡化您的 Windows 10 升級，請在部署工作順序之前，先將這些設定部署至 Windows 7 用戶端。

如需有關這項「商務用 OneDrive」功能的詳細資訊，請參閱[將 Windows 已知資料夾重新導向及移至 OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders) \(機器翻譯\)。

首先，[尋找您的 Office 365 租用戶識別碼](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id) \(機器翻譯\)。 部署 OneDrive 同步處理用戶端 18.111.0603.0004 版或更新版本。 如需詳細資訊，請參閱[使用 Configuration Manager 部署 OneDrive 應用程式](https://docs.microsoft.com/onedrive/deploy-on-windows)。  

若要部署商務用 OneDrive 設定檔，請在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 展開 [合規性設定]  ，然後選取 [商務用 OneDrive 設定檔]  節點。  

如需詳細資訊，請參閱[商務用 OneDrive 設定檔](../../../compliance/deploy-use/onedrive-profile.md)一文中的＜將 Windows 已知資料夾重新導向至 OneDrive＞一節。

### <a name="integration-for-office-365-proplus-readiness"></a>與 Office 365 ProPlus 整備的整合

<!--3735402-->
使用 Configuration Manager 來識別具有高信賴度準備升級到 Office 365 ProPlus 的裝置。 該整合提供任有關您環境中使用之 Office 增益集與巨集之潛在相容性問題的見解。 接著，使用 Configuration Manager 將 Office 部署到已就緒的裝置。

現有的 Office 365 用戶端管理儀表板現在包括新的 [Office 365 ProPlus 更新整備小幫手]  圖格。

如需詳細資訊，請參閱 [Office 365 用戶端管理儀表板](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)

### <a name="additional-languages-for-office-365-updates"></a>Office 365 更新的額外語言

<!--3555955-->
Configuration Manager 現在支援 Office 365 用戶端更新的所有支援語言。 更新工作流程會從 **Office 365 用戶端更新**的諸多語言分成 **Windows Update** 的 38 種語言。

如需詳細資訊，請參閱[管理 Office 365 更新](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang)

### <a name="office-products-on-lifecycle-dashboard"></a>生命週期儀表板上的 Office 產品

<!--3556026-->
產品生命週期儀表板現在會包含已安裝的 Office 2003 到 Office 2016 版本資訊。 在站台執行生命週期摘要工作 (每隔 24 小時執行一次) 之後，資料就會出現。

如需詳細資訊，請參閱[使用產品生命週期儀表板](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)。


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> 階段式部署

### <a name="dedicated-monitoring-for-phased-deployments"></a>階段式部署的專用監視

<!--3555949-->
階段式部署現在有自己的專用監視節點。 此節點可讓您更輕鬆地識別您所建立的階段式部署，然後瀏覽至階段式部署監視檢視。 前往 Configuration Manager 主控台中的 [監視]  工作區，然後選取 [階段式部署]  節點。 它會顯示階段式部署的清單。

如需詳細資訊，請參閱[階段式部署監視檢視](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor)。

### <a name="improvement-to-phased-deployment-success-criteria"></a>階段式部署成功準則的改善

<!--3555946-->
指定額外準則，以在階段式部署中成功完成階段。 此準則現在也可以是成功部署的裝置數目，而不是只有百分比。 當集合的大小可變時，此選項很有用，而且而且您在移至下一個階段之前有特定是木的裝置可顯示成功。

建立工作順序、軟體更新或應用程式的階段式部署。 然後在精靈的 [設定] 頁面上，選取下列選項作為第一個階段的成功準則：**成功部署的裝置數**。

如需詳細資訊，請參閱[建立階段式部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)。


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager 主控台

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Configuration Manager 主控台的改善

<!--3594151-->
根據在 Midwest Management Summit (MMS) Desert Edition 2018 的客戶意見反應，此版本包含對 Configuration Manager 主控台的下列改進：

- 將應用程式偵測方法的瀏覽登錄視窗最大化
- 從應用程式部署移至集合
- 從監視狀態移除內容
- 檢視在 [監視]  工作區的 [部署]  節點中，會依整數值排序
- 移動大量結果的警告

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md#tips)。

### <a name="configuration-manager-console-notifications"></a>Configuration Manager 主控台通知

<!--3556016, fka 1318035-->
為了讓您能更清楚掌握情況，以採取適當的動作，Configuration Manager 主控台現在會通知您下列事件：

- Configuration Manager 本身有可用的更新
- 當環境中發生生命週期和維護事件

這個通知列位於功能區下方的主控台視窗頂端。 它會取代先前提供 Configuration Manager 更新的體驗。 這些主控台內通知仍會顯示重大資訊，但不會影響您在主控台中的工作。 您無法關閉重大通知。 主控台會在標題列的新通知區域中顯示所有通知。

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md)。

### <a name="confirmation-of-console-feedback"></a>確認主控台的意見反應

<!--3556010-->
當您在 Configuration Manager 主控台中傳送[意見反應](../../understand/find-help.md#product-feedback)時，它現在會顯示確認訊息。 此訊息包含**意見反應識別碼**，您可以將其提供給 Microsoft 作為追蹤識別碼。

如需詳細資訊，請參閱[產品意見反應](../../understand/find-help.md#bkmk_feedbackid)。

### <a name="view-recently-connected-consoles"></a>檢視最近連線的主控台

<!--3699367-->
您現可檢視 Configuration Manager 主控台的最近連線。 此檢視包含使用中的連線，以及最近連線的主控台。 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [安全性]  ，然後選取 [主控台連線]  節點。

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md#bkmk_viewconnected)。

### <a name="in-console-documentation-dashboard"></a>主控台內的文件儀表板

<!--3556019, fka 1357546-->
新 [社群]  工作區中有新的 [文件]  節點。 此節點包含 Configuration Manager 文件和支援文章的最新資訊。

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md#bkmk_doc-dashboard)。

### <a name="search-device-views-using-mac-address"></a>使用 MAC 位址搜尋裝置檢視

<!--3600878-->
您現在可在 Configuration Manager 主控台的裝置檢視中搜尋 MAC 位址。 在針對 PXE 型部署進行疑難排解時，這個屬性對於 OS 部署管理員來說非常有用。 當您檢視裝置的清單時，請將 [MAC 位址]  資料行新增至檢視。 使用 [搜尋] 欄位即可新增 [MAC 位址]  搜尋準則。

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md#tips)。

### <a name="use-net-47-for-improved-console-accessibility"></a>使用 .NET 4.7 以取得改善的主控台協助工具

<!-- SCCMDocs-pr issue #3228 -->
若要改善 Configuration Manager 主控台的協助工具功能，請在執行主控台的電腦上，將 .NET 更新至 4.7 版或更新版本。

如需詳細資訊，請參閱 [Configuration Manager 的協助工具功能](../../understand/accessibility-features.md)。

### <a name="changes-to-console-setup-process"></a>主控台安裝程式程序的變更

<!-- 3612513 -->
安裝 Configuration Manager 主控台時需要新元件。 如果您建立用於在其他電腦上安裝主控台的套件，請確定該套件包含下列檔案：

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

當您安裝或更新站台伺服器時，它會將這些安裝檔案與站台的支援語言套件複製到 **Tools\ConsoleSetup** 子資料夾。 如需詳細資訊，請參閱[安裝 Configuration Manager 主控台](../../servers/deploy/install/install-consoles.md)。


## <a name="other-updates"></a>其他更新

除了新功能之外，此版本也包含錯誤修正等其他變更。 如需詳細資訊，請參閱 [Configuration Manager 最新分支 1902 版中變更的摘要](https://support.microsoft.com/help/4498910) \(機器翻譯\)。

如需適用於 Configuration Manager 之 Windows PowerShell Cmdlet 變更的詳細資訊，請參閱 [PowerShell 1902 版版本資訊](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps) \(機器翻譯\)。

自 2019 年 6 月 17 日起，可在主控台中取得下列更新彙總套件 (4500571)：[適用於 Configuration Manager 目前分支 1902 版的更新彙總套件](https://support.microsoft.com/help/4500571) \(機器翻譯\)。

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>後續步驟

當您準備安裝此版本時，請參閱[安裝 Configuration Manager 的更新](../../servers/manage/updates.md)和[安裝更新 1902 的檢查清單](../../servers/manage/checklist-for-installing-update-1902.md)。

> [!TIP]  
> 若要安裝新的站台，請使用 Configuration Manager 的基準版本。  
>
> 深入了解：    
> - [安裝新的站台](../../servers/deploy/install/installing-sites.md)  
> - [基準和更新版本](../../servers/manage/updates.md#bkmk_Baselines)  

如需已知的重大問題，請參閱[版本資訊](../../servers/deploy/install/release-notes.md)。

更新站台之後，也請檢閱[更新後的檢查清單](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist)。
