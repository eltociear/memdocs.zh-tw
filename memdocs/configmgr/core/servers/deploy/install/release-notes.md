---
title: 版本資訊
titleSuffix: Configuration Manager
description: 了解產品中尚未修正或 Microsoft 支援知識庫文章尚未涵蓋的緊急問題。
ms.date: 05/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 131b6104d5724c8a4eeb0bb68c4afd9a5319abb7
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823957"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager 的版本資訊

適用於：Configuration Manager (最新分支)

針對 Configuration Manager，產品版本資訊僅限於緊急問題。 這些是在產品中尚未修正，或在 Microsoft 知識庫文章中尚未詳述的問題。  

功能特定的文件包括會影響核心案例的已知問題相關資訊。  

本文包含 Configuration Manager 最新分支的版本資訊。 如需 Technical Preview 分支的資訊，請參閱 [Technical Preview](../../../get-started/technical-preview.md)  

如需不同版本所引進之新功能的相關資訊，請參閱下列文章：

- [2002 版的新功能](../../../plan-design/changes/whats-new-in-version-2002.md)
- [1910 版的新功能](../../../plan-design/changes/whats-new-in-version-1910.md)
- [1906 版的新功能](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [1902 版的新功能](../../../plan-design/changes/whats-new-in-version-1902.md)

如需電腦分析中新功能的詳細資訊，請參閱[電腦分析中的新功能](../../../../desktop-analytics/whats-new.md)。

> [!Tip]  
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>設定和升級  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>所有用戶端的用戶端自動升級會立即進行

<!-- 6040412 -->

*適用於 1910 版*

如果您的站台使用 [自動用戶端升級](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)，則當您將此站台更新至 1910 版時，所有用戶端都會在站台成功更新之後立即升級。 唯一隨機設定是用戶端收到此原則的時間，預設為每小時一次。 對於具有許多用戶端的大型站台而言，此行為可能會耗用大量的網路流量和壓力發佈點。

如需受影響版本的詳細資訊，請參閱 [Configuration Manager 最新分支的用戶端更新，1910 版](https://support.microsoft.com/help/4538166) \(英文\)。

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>被動模式中的站台伺服器不更新 configuration.mof

<!-- 5787848 -->

*適用於 1910 版*

如果您的站台包含[被動模式的站台伺服器](../configure/site-server-high-availability.md)，則更新站台時，可能會遺失清查自訂。 當容錯移轉站台伺服器時，站台目前不會同步處理 configuration.mof。

若要解決此問題，請手動備份並還原網站的 configuration.mof。

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>在 Server 2019 上設定網域功能等級的先決條件警告

<!-- 4904376 -->

*適用於 1906 版*

在包含執行 Windows Server 2019 的網域控制站的環境中安裝 1906 版更新時，網域功能等級的先決條件檢查會傳回下列警告：

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

若要解決此問題，請忽略警告。

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>Azure AD 使用者探索和集合群組同步處理在站台擴充之後無法運作

<!-- 4797313 -->
*適用於 1906 版*

設定下列其中一項功能之後：

- Azure Active Directory 使用者群組探索
- 將集合成員資格結果同步至 Azure Active Directory 群組

如果您之後將獨立主要站台擴充至包含管理中心網站的階層，您會在 SMS_AZUREAD_DISCOVERY_AGENT 中看到下列錯誤：

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

若要解決此問題，請更新 Azure AD 中與應用程式註冊建立關聯的金鑰。 如需詳細資訊，請參閱[更新秘密金鑰](../configure/azure-services-wizard.md#bkmk_renew)。

## <a name="role-based-administration"></a>角色式管理

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>某些資料夾的安全性範圍不會從 CAS 複寫到主要站台
<!--6306759-->
*適用於 1910 版*

升級至 1910 版之後，使用者集合和裝置集合中的[資料夾安全性範圍](../configure/configure-role-based-administration.md#bkmk_config-folder)不會從 CAS 複寫到主要站台。

## <a name="application-management"></a>應用程式管理

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>部署 Microsoft Edge 77 版及更新版本時，無法取得 PowerShell 錯誤的憑證
<!--5769384-->
適用於：*Configuration Manager 1910 版*

如果您是在語言為瑞典文、匈牙利文或日文的 OS 上執行 Configuration Manager 主控台，則在部署 Microsoft Edge 77 和更新版本時，將會收到下列錯誤：

`Unable to get certificate for Powershell`

發生此錯誤是因為瑞典文、匈牙利文或日文語言的 `AdminConsole\bin` 目錄下不存在 `scripts` 資料夾。 這些 OS 語言中的指令碼資料夾已當地語系化。

若要解決此問題，請在 `AdminConsole\bin` 目錄中建立稱為 `scripts` 的資料夾。 將檔案從當地語系化資料夾複製到新建立的 `scripts` 資料夾。 檔案複製完成後，請部署 Microsoft Edge 77 和更新版本。

## <a name="os-deployment"></a>OS 部署

### <a name="task-sequences-cant-run-over-cmg"></a>無法透過 CMG 執行工作順序

適用於：*Configuration Manager 版本2002*

在兩種情況下，您無法在透過雲端管理閘道 (CMG) 進行通訊的裝置上執行工作順序：

- 您為站台設定增強式 HTTP，且管理點為 HTTP。<!-- 6358851 -->

    若要解決此問題，請設定 HTTPS 的管理點。

- 您已安裝並註冊具有大量註冊權杖的用戶端以進行驗證。<!-- 6377921 -->

    若要解決此問題，請使用下列其中一種驗證方法：

  - 在內部網路上預先註冊裝置
  - 使用用戶端驗證憑證設定裝置
  - 將裝置加入至 Azure AD

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>在被動站台伺服器升級後，預設開機映像套件仍會使用之前作用中伺服器的套件來源

<!--3453224, SCCMDocs-pr issue 3097-->
適用於：*Configuration Manager 1810 版*

如果您有處於被動模式的站台伺服器 (伺服器 B)，當您將它升級為作用中時，預設開機映像的內容位置會繼續參考先前作用中的伺服器 (伺服器 A)。 如果伺服器 A 發生硬體故障，您就無法更新或變更預設開機映像。

此問題沒有任何因應措施。

## <a name="software-updates"></a>軟體更新

### <a name="security-roles-are-missing-for-phased-deployments"></a>階段式部署缺少安全性角色

<!--3479337, SCCMDocs-pr issue 3095-->
適用於：*Configuration Manager 1810、1902 版*

**作業系統部署管理員**內建安全性角色具有[階段式部署](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)權限。 下列角色缺少這些這些權限：  

- **應用程式系統管理員**  
- **應用程式部署管理員**  
- **軟體更新管理員**  

[應用程式作者] 角色可能有一些階段式部署權限，但應該無法建立部署。

具有這些角色其中之一的使用者可以啟動 [建立階段式部署精靈]，並可查看應用程式或軟體更新的階段式部署。 他們無法完成精靈或對現有的部署進行任何變更。

若要解決此問題，請建立自訂安全性角色。 複製現有的安全性角色，並在 [階段式部署] 物件類別上新增下列權限：

- 建立  
- 刪除  
- 修改  
- 讀取  

如需詳細資訊，請參閱[建立自訂安全性角色](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)

## <a name="desktop-analytics"></a>電腦分析

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a> Windows 7 的延伸安全性更新導致其顯示為**無法註冊**

<!-- 7283186 -->
適用於：_Configuration Manager 1902、1906、1910 與 2002 版_

Windows 7 2020 年 4 月延伸安全性更新 (ESU) 已將所需的最低 diagtrack.dll 版本從 10586 變更為 10240。 此變更會導致 Windows 7 裝置在 Desktop Analytics [連接健康狀態] 儀表板中顯示為**無法註冊**。 當您向下切入裝置檢視以檢視此狀態時，[DiagTrack 服務設定] 屬性會顯示下列狀態：`Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

此問題不需要任何因應措施。 請勿解除安裝四月份 ESU。 若已正確設定，則 Windows 7 裝置仍會將診斷資料回報給電腦分析服務，而且仍會顯示在入口網站中。

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>如果您針對分散式檢視使用硬體清查，則無法上架至電腦分析

<!-- 4950335 -->
適用於：*含更新彙總套件的 Configuration Manager 1902 版，以及 1906 版*

如果您有階層，並在任何站台複寫連結上，針對[分散式檢視](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews)啟用**硬體清查**站台資料，則在 Configuration Manager 中設定電腦分析連線之後，您會在 M365UploadWorker.log 中看到下列錯誤：

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

若要解決此問題，請針對每個站台複寫連結上的分散式檢視，停用**硬體清查**站台資料。

### <a name="console-unexpectedly-closes-when-removing-collections"></a>主控台會在移除集合時無預警關閉

<!-- 4749443 -->
適用於：含更新彙總套件的 Configuration Manager 1902 版

當您將站台連線至[電腦分析](../../../../desktop-analytics/connect-configmgr.md)之後，您可以**選取要與電腦分析同步處理的特定集合**。 如果您移除集合並套用變更，立即新增集合就會導致未處理的例外狀況。 主控台無預警關閉。

若要解決此問題，當移除集合時，請選取 [確定] 以關閉 [屬性] 視窗。 接著，再次開啟 [屬性]，以便在 [電腦分析連線] 索引標籤上新增集合。

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>[試驗狀態] 磚顯示有些裝置為「未定義」

<!-- 4547783 -->
適用於：*含更新彙總套件的 Configuration Manager 1902 版*

當您使用 Configuration Manager 主控台監視試驗部署狀態時，在該部署計劃的 Windows 目標版本上處於最新狀態的試驗裝置，會在 [試驗狀態] 磚中顯示為**未定義**。  

這些**未定義的**裝置對於該部署計劃的作業系統目標版本而言，處於**最新**狀態。 不需要進行其他動作。

## <a name="cloud-services"></a>雲端服務

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>適用於美國政府雲端的 Azure 服務顯示為公用雲端

<!-- 6036748 -->

*適用於 1910 版*

如果您建立與 Azure 服務的連線，並將 **Azure 環境**設定為政府雲端，則連線的屬性會將環境顯示為 Azure 公用雲端。 此問題只是主控台中的顯示問題，服務確實位於政府雲端。 若要確認設定，請在站台資料庫上執行下列 SQL 查詢：

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

若是政府雲端，針對特定租用戶執行此查詢的結果會是 `2`。

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>無法從已為 TLS 1.2 啟用的雲端管理閘道下載內容

<!-- 5771680 -->

*適用於 1906、1910 版早期更新通道*

如果將雲端管理閘道 (CMG) 啟用為 [作為雲端發佈點來運作並處理來自 Azure 儲存體的內容] 和 [強制執行 TLS 1.2]，您可能會看到內容下載失敗。

下列錯誤會顯示在用戶端的 DataTransferService.log 中：

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

下列錯誤會顯示在伺服器的 CMGContentService.log 中：

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

若要解決這個問題：

- 將網站更新為 2019 年 12 月 20 日發行的全球可用 1910 版。 (如果您先前已更新為 1910 早期更新通道，則必須在此組建可用時，更新為此組建)。

- 或者，也可以使用傳統的[雲端發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)。 該角色不會強制執行 TLS 1.2，而會與需要 TLS 1.2 的用戶端相容。

## <a name="protection"></a>保護

### <a name="bitlocker-management-appears-in-version-1906"></a>BitLocker 管理出現在 1906 版中

*適用於 1906 版*

<!-- 5984688 -->

在 2019 年 11 月 21 日之後，如果您從 1902 版或更早版本更新至 1906 版，BitLocker 管理功能將會開啟且可供使用。 此功能從 1910 版開始為選用功能。 1906 版不支援此功能。 如果您嘗試在 1906 版中使用此功能，可能會遇到非預期的結果。 如果您不使用此功能，則不受影響。

若要使用 [BitLocker 管理功能](../../../../protect/plan-design/bitlocker-management.md)，請更新至 1910 版。

<!--
## Backup and recovery

## Client deployment and upgrade
-->
