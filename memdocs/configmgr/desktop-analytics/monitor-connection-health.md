---
title: 監視連線健康情況
titleSuffix: Configuration Manager
description: 有關如何在 Configuration Manager 中監視電腦分析連線健全狀況和裝置狀態的詳細資料。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 37555c6b60b0d2c18096c2778e9a077baeb9143f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695596"
---
# <a name="monitor-connection-health"></a>監視連線健康情況

使用 Configuration Manager 中的 [連線健全狀況]  儀表板，依裝置健全狀況向下切入到各類別。 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [電腦分析服務]  節點，然後選取 [連線健全狀況]  儀表板。  

[![Configuration Manager 連線健全狀況儀表板的螢幕擷取畫面](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

當您第一次設定電腦分析時，這些圖表可能不會顯示完整資料。 使用中裝置可能需要 2 到 3 天才會將診斷資料傳送到電腦分析服務，服務接著會處理資料，然後與 Configuration Manager 站台同步。<!-- 4098037 -->

## <a name="connection-details"></a>連線詳細資料

這個圖格會顯示下列從 Configuration Manager 至電腦分析連線的基本資訊：

- **租用戶名稱**：[Azure 服務]  節點中電腦分析連線的名稱

- **目標集合**：您在將 Configuration Manager 連線到電腦分析時指定的相同「目標集合」  。 此集合包含 Configuration Manager 使用商業識別碼與診斷資料設定來進行設定的所有裝置。 這是由 Configuration Manager 連線到電腦分析服務的完整裝置集。

- **目標裝置**：目標集合中的所有裝置，減去下列裝置類型：

  - 已解除
  - 已淘汰
  - 非使用中
  - 非受控
  - 執行 Windows 10 長期維護通道 (LTSC) 版本的裝置
  - 執行 Windows Server 的裝置

    如需這些裝置狀態的詳細資訊，請參閱[關於用戶端狀態](../core/clients/manage/monitor-clients.md#bkmk_about)。

    > [!Note]  
    > Configuration Manager 會將目標集合中所有裝置減去已解除和已淘汰的用戶端後，上傳至電腦分析。

- **符合 DA 資格的裝置數**：目標裝置減去不符合電腦分析資格裝置後的數量。 例如，目標集合中執行 Windows Server 或 Windows 10 長期維護通道 (LTSC) 的裝置。

## <a name="last-sync-details"></a>上次同步詳細資料

這個圖格會顯示 Configuration Manager 與電腦分析雲端服務同步的時間，以及其同步的裝置數量。

- **同步裝置數**：Configuration Manager 傳送到電腦分析的合格裝置數。 服務會在目前可見的快照集中包含這些裝置。

- **上次服務同步**：與電腦分析入口網站中的**上次更新**時間相同。

- **下次服務同步**：您可以預期電腦分析中出現下一次每日快照集的時間。

> [!Note]  
> 當您第一次向電腦分析註冊裝置時，資料可能需要數天才會上傳並進行處理。 在此期間，[上次同步詳細資料]  圖格可能會顯示空白。
> 此外，這個圖格中的任何值都不會在您要求隨選快照集時自動更新。 如需詳細資訊，請參閱[資料延遲](troubleshooting.md#data-latency)。

若您認為某些裝置並未在電腦分析中顯示，請確認電腦分析支援那些裝置。 如需詳細資訊，請參閱[必要條件](overview.md#prerequisites)。

## <a name="connection-health"></a>連線健全狀況

**連線健全狀況**圖表會顯示處於下列健全狀況狀態中的裝置數：  

- [已正確註冊](#properly-enrolled)：裝置會出現電腦分析中，並附帶完整的清查
- [無法註冊](#unable-to-enroll)：發生執行問題，導致無法註冊裝置
- [設定警示](#configuration-alert)：裝置不會出現在電腦分析中，或會在附帶不完整清查的情況下出現。 Configuration Manager 也識別出裝置註冊發生問題。
- [正在等待註冊](#awaiting-enrollment)：Configuration Manager 已設定裝置，但其尚未出現在電腦分析中
- [狀態暫止](#status-pending)：Configuration Manager 仍在設定此裝置，或沒有足夠的裝置資料來判斷其狀態
- [遺失資料](#missing-data)：Configuration Manager 已設定裝置，但電腦分析只有部分資料

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

此圖表中的總裝置數應和 [連線詳細資料] 圖格中的 [符合 DA 資格的裝置數]  值相同。

請選取圖表中切片來向下切入該狀態的裝置清單。 如需詳細資訊，請參閱[裝置清單](#device-list)。

選取圖例中的類別名稱來從圖表中移除或新增。 這項動作有助於縮放圖表，讓您可以看見較小區段的相對大小。

### <a name="properly-enrolled"></a>已正確註冊

裝置具有下列屬性：

- Configuration Manager 用戶端 1902 版或更新版本  
- 沒有任何設定錯誤  
- 電腦分析在過去 28 天內從此裝置接收了完整的診斷資料  
- 電腦分析也具有裝置設定及已安裝應用程式的完整清查  

### <a name="unable-to-enroll"></a>無法註冊

Configuration Manager 偵測到一或多個執行問題，這些問題導致裝置無法註冊。 如需詳細資訊，請參閱 [Configuration Manager 中的電腦分析裝置屬性](#bkmk_config-issues)清單。  

例如，Configuration Manager 用戶端並非至少是版本 1902 (5.0.8790)。 請將用戶端更新到最新版本。 請考慮為 Configuration Manager 站台啟用自動用戶端升級。 如需詳細資訊，請參閱[升級用戶端](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。  

從 2002 版開始，可更輕鬆地識別下列兩個領域中用戶端 Proxy 設定的問題：

- **端點連線能力檢查**：如果用戶端無法連線到必要的端點，即會在儀表板中看到設定警示。 向下切入至無法註冊的用戶端，以查看用戶端因 Proxy 設定問題而無法連線的端點。 如需詳細資訊，請參閱[端點連線能力檢查](#endpoint-connectivity-checks)。<!-- 4963230 -->

- **連線能力狀態**：如果用戶端使用 Proxy 伺服器來存取電腦分析，則 Configuration Manager 會顯示來自用戶端的 Proxy 驗證問題。 向下切入以查看因 Proxy 驗證問題而無法註冊的用戶端。 如需詳細資訊，請參閱[連線能力狀態](#connectivity-status)。<!-- 4963383 -->

### <a name="configuration-alert"></a>設定警示

裝置不會出現在電腦分析中，或會在附帶不完整清查的情況下出現。 Configuration Manager 也識別出裝置註冊發生問題。 如需詳細資訊，請參閱 [Configuration Manager 中的電腦分析裝置屬性](#bkmk_config-issues)清單。

例如，裝置沒有對服務的連線能力。 如需詳細資訊，請參閱 [Windows 診斷端點連線能力](#windows-diagnostic-endpoint-connectivity)。

### <a name="awaiting-enrollment"></a>正在等待註冊

電腦分析沒有此裝置的診斷資料。 此問題可能是因為您最近將裝置新增到目標集合，而其尚未傳送資料所致。 這也可能表示裝置並未正常地與服務通訊，且最新的診斷資料已超過 28 天。

請確認裝置可以和服務通訊。 如需詳細資訊，請參閱[端點](enable-data-sharing.md#endpoints)。  

### <a name="status-pending"></a>狀態暫止

Configuration Manager 仍在設定此裝置，或沒有足夠的裝置資料來判斷其狀態。

### <a name="missing-data"></a>遺失資料

Configuration Manager 已成功設定裝置，但電腦分析無法建立相容性評定。 其沒有裝置設定 (普查) 或已安裝應用程式 (清查) 的完整資料集。

此問題通常會在裝置重試時自動修正。 若問題持續發生，請確認裝置可以和服務通訊。 如需詳細資訊，請參閱[端點](enable-data-sharing.md#endpoints)。  

## <a name="device-list"></a>裝置清單

若要根據狀態查看裝置的特定清單，請從 [連線健全狀況]  儀表板開始。 選取 [連線健全狀況]  圖格的其中一個區段，然後向下切入至此狀態的裝置清單。 根據預設，此自訂裝置檢視會顯示下列電腦分析欄：

- 商業識別碼設定
- 最低相容性更新
- Windows 診斷資料加入
- Windows 商業資料加入
- Windows 診斷端點連線能力
- 連線能力狀態 (從 2002 版開始)
- 端點連線能力檢查 (從 2002 版開始)

這些欄會對應至裝置與電腦分析通訊的關鍵[先決條件](overview.md#prerequisites)。

[![無法註冊裝置清單的螢幕擷取畫面](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

選取其中一部裝置以在詳細資料窗格中查看可用屬性的完整清單。 您也可以將這些屬性中的任何屬性作為欄新增至裝置清單。

## <a name="device-properties"></a><a name="bkmk_config-issues"></a> 裝置屬性

下列電腦分析裝置屬性可以作為 Configuration Manager 裝置清單中的欄使用：

- [端點連線能力檢查](#endpoint-connectivity-checks) (從 2002 版開始)
- [連線能力狀態](#connectivity-status) (從 2002 版開始)
- [評鑑程式設定](#appraiser-configuration)  
- [最低相容性更新](#minimum-compatibility-update)  
- [評鑑程式版本](#appraiser-version)  
- [上次成功的評鑑程式完整執行](#last-successful-full-run-of-appraiser)  
- [評鑑程式資料集合](#appraiser-data-collection)  
- [上次成功的普查完整執行](#last-successful-full-run-of-census)  
- [普查資料集合](#census-data-collection)  
- [Windows 診斷端點連線能力](#windows-diagnostic-endpoint-connectivity)  
- [檢查終端使用者診斷資料](#check-end-user-diagnostic-data)  
- [檢查使用者 Proxy](#check-user-proxy)  
- [商業識別碼設定](#commercial-id-configuration)  
- [Windows 商業資料加入](#windows-commercial-data-opt-in)  
- [檢查診斷資料中的裝置名稱](#check-device-name-in-diagnostic-data)  
- [DiagTrack 服務設定](#diagtrack-service-configuration)  
- [DiagTrack 版本](#diagtrack-version)  
- [SQM 識別碼擷取](#sqm-id-retrieval)  
- [唯一裝置識別碼擷取](#unique-device-identifier-retrieval)  
- [Windows 診斷資料加入](#windows-diagnostic-data-opt-in)  

[連線健全狀況] 儀表板之 [最常出現註冊封鎖程式和設定警示]  圖格會顯示裝置最常報告為問題的屬性。

### <a name="endpoint-connectivity-checks"></a>端點連線能力檢查

從 2002 版開始，<!-- 4963230 --> 若要偵測 Proxy 驗證問題，用戶端會針對所需的端點執行連線能力檢查。 如果用戶端無法連線到所需的端點，則這項屬性會顯示已編號的端點清單，列出因為 Proxy 設定問題導致無法連線的端點。 請將此清單與[必要端點](enable-data-sharing.md#endpoints)的發佈清單進行比較。

### <a name="connectivity-status"></a>連線能力狀態

從 2002 版開始，<!-- 4963383 --> 如果用戶端使用 Proxy 伺服器來存取電腦分析，則這項屬性會顯示 Proxy 驗證問題。 其中包含下列與 Proxy 驗證相關的詳細資料：

- 狀態碼
- 傳回碼

您會在記錄檔中看到下列類似的錯誤：

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

其中 `%s` 是必要端點的 URL。

您可能也會看到非決定性的錯誤訊息，在裝置發生註冊問題之前不需要特別在意。 例如：

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

如需設定 Proxy 伺服器以搭配使用電腦分析的詳細資訊，請參閱 [Proxy 伺服器驗證](enable-data-sharing.md#proxy-server-authentication)。

### <a name="appraiser-configuration"></a>評鑑程式設定

<!--20,21-->
評鑑程式對應至[相容性更新](enroll-devices.md#update-devices)的 Windows 元件。 其會針對與最新版本 Windows 的相容性來評定裝置上應用程式和驅動程式。

若此檢查成功，則表示評鑑程式元件已在裝置上正確設定。

否則，可能會顯示下列其中一個錯誤：

- 無法設定裝置應用程式相容性資料集合 (SetRequestAllAppraiserVersions)。 請檢查記錄以取得例外狀況詳細資料  

- 無法設定裝置應用程式相容性資料集合 (SetRequestAllAppraiserVersions)。 請檢查記錄以取得例外狀況詳細資料  

- 無法將 RequestAllAppraiserVersions 寫入登錄機碼 `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`。 請檢查權限  

請檢查此登錄機碼上的權限。 確認本機系統帳戶可以針對要設定的 Configuration Manager 用戶端存取此機碼。  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

### <a name="minimum-compatibility-update"></a>最低相容性更新

<!--18,19,32-->
裝置上並未安裝相容性更新 (appraiser.dll)，或已過期。 其比電腦分析的最低需求 (10.0.17763) 舊。

請安裝最新的相容性更新。 如需詳細資訊，請參閱[相容性更新](enroll-devices.md#update-devices)。

### <a name="appraiser-version"></a>評鑑程式版本

此屬性會顯示裝置上評鑑程式元件的目前版本。 該屬性會顯示 `%windir%\System32\appraiser.dll` 上的檔案版本 (不帶小數點)。 例如，檔案版本 10.0.17763 會顯示為 10017763。

### <a name="last-successful-full-run-of-appraiser"></a>上次成功的評鑑程式完整執行

此屬性會顯示裝置上次成功執行評鑑程式的日期和時間。

### <a name="appraiser-data-collection"></a>評鑑程式資料集合

<!--Appraiser run status-->
<!--22,33-->
此屬性會顯示 Windows 執行評鑑程式元件的最新結果。

若沒有成功，其可能會顯示下列其中一個錯誤：

- 無法收集應用程式相容性資料 (RunAppraiser)。 請檢查記錄以取得詳細資料  

- 應用程式相容性資料收集 (CompatTelRunner.exe) 已結束，錯誤碼為  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。

請檢查下列檔案：`%windir%\System32\CompatTelRunner.exe`。 若其不存在，請重新安裝必要的[相容性更新](enroll-devices.md#update-devices)。 請確認沒有其他系統元件正在移除此檔案，例如群組原則或反惡意程式碼服務。

若用戶端上的 M365AHandler.log 檔案包含下列其中一個錯誤：

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

為了協助補救這些錯誤，請在受影響的用戶端上，從提升權限的 Windows PowerShell 主控台中執行下列命令：

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>上次成功的普查完整執行

此屬性會顯示裝置上次成功執行普查的日期和時間。

### <a name="census-data-collection"></a>普查資料集合

<!-- Census run status -->
<!--51,52-->
普查是 Windows 元件，負責清查裝置。 此清查資料會用來了解裝置及其設定。

此屬性會顯示 Windows 執行普查元件的最新結果。

若沒有成功，其可能會顯示下列其中一個錯誤：

- 無法收集裝置及其設定的相關資料 (RunCensus)。 請檢查記錄以取得例外狀況詳細資料  

- 找不到裝置和設定資料收集工具 (devicecensus.exe)  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。

請檢查下列檔案：`%windir%\System32\DeviceCensus.exe`。 若其不存在，請重新安裝必要的[相容性更新](enroll-devices.md#update-devices)。 請確認沒有其他系統元件正在移除此檔案，例如群組原則或反惡意程式碼服務。

### <a name="windows-diagnostic-endpoint-connectivity"></a>Windows 診斷端點連線能力

<!--12,15-->
若此檢查成功，則裝置便可以連線到已連線使用者體驗與遙測端點 (Vortex)。

否則，可能會顯示下列其中一個錯誤：  

- 無法連線至已連線使用者體驗與遙測端點 (Vortex)。 請檢查網路/Proxy 設定  

- 無法檢查與已連線使用者體驗與遙測端點的連線能力 (CheckVortexConnectivity)。 請檢查記錄以取得例外狀況詳細資料  

裝置會根據 OS 版本，使用向下列端點發出的 GET 要求來驗證連線能力：

| OS 版本 | 端點 |
|------------|----------|
| - Windows 10，1809 版或更新版本<br/>- Windows 10，包含 2018-09 或更新累積更新的 1803 版 | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10，「不」  包含 2018-09 或更新累積更新的 1803 版 | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10，1709 版或更早版本 | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 或 Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

請確認裝置可以和服務通訊。 這項檢查會驗證一部分，但不會驗證所有的必要端點。 如需詳細資訊，請參閱[端點](enable-data-sharing.md#endpoints)。  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

### <a name="check-end-user-diagnostic-data"></a>檢查終端使用者診斷資料

<!--1004-->
若此檢查成功，則表示使用者在裝置上選取了較低的 Windows 診斷資料。 這也可能是由發生衝突的群組原則物件所造成。 如需詳細資訊，請參閱 [Windows 設定](enroll-devices.md#windows-settings)。

取決於商務需求，您可以透過群組原則來停用使用者選擇。 使用設定來**設定遙測加入設定使用者介面**。 如需詳細資訊，請參閱[在組織中設定 Windows 診斷資料](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。

### <a name="check-user-proxy"></a>檢查使用者 Proxy

<!--30,35-->
Windows 7 預設會啟用 DisableEnterpriseAuthProxy 設定。 針對 Windows 8.1 電腦，Configuration Manager 會將 DisableEnterpriseAuthProxy 設定設為 0 (而非停用)。

此屬性可能會顯示下列錯誤：

- 已啟用驗證 Proxy。 請在 `HKLM\Software\Policies\Microsoft\Windows\DataCollection` 中將 DisableEnterpriseAuthProxy 設為 0

- 無法檢查驗證 Proxy 狀態。 請檢查記錄以取得例外狀況詳細資料

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

請檢查此登錄機碼上的權限。 確認本機系統帳戶可以針對要設定的 Configuration Manager 用戶端存取此機碼。 這也可能是由發生衝突的群組原則物件所造成。 如需詳細資訊，請參閱 [Windows 設定](enroll-devices.md#windows-settings)。  

### <a name="commercial-id-configuration"></a>商業識別碼設定

<!--9, 11, 53-->
Microsoft 會使用唯一的商業識別碼，將裝置的資訊對應到電腦分析工作區。 當將 Configuration Manager 與電腦分析整合時，其會自動向服務查詢此識別碼。 Configuration Manager 應會自動將此識別碼套用到您瞄準電腦分析設定的目標用戶端。

若此檢查成功，則表示已成功使用商業識別碼正確設定裝置。

否則，可能會顯示下列其中一個錯誤：

- 無法將 CommercialId 寫入登錄機碼 `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`。 請檢查權限  

- 無法更新登錄機碼 `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` 中的 CommercialId。 請檢查記錄以取得例外狀況詳細資料  

- 請在 `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` 提供正確的 CommercialId 值  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

請檢查此登錄機碼上的權限。 確認本機系統帳戶可以針對要設定的 Configuration Manager 用戶端存取此機碼。 這也可能是由發生衝突的群組原則物件所造成。 如需詳細資訊，請參閱 [Windows 設定](enroll-devices.md#windows-settings)。  

裝置有不同的識別碼。 群組原則會使用此登錄機碼。 其會優先於 Configuration Manager 提供的識別碼。  

<a name="bkmk_ViewCommercialID"></a> 若要在電腦分析入口網站中檢視商業識別碼，請使用下列程序：

1. 前往電腦分析入口網站，然後在全域設定群組中選取 [已連線的服務]  。  

2. 在 [已連線的服務]  窗格中，根據預設會選取 [已註冊的裝置]  窗格。 在 [註冊裝置] 窗格中，[資訊] 區段會顯示商業識別碼金鑰。  

[![電腦分析入口網站中商業識別碼的螢幕擷取畫面](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> 請只在無法使用目前的金鑰時，才**取得新的識別碼金鑰**。 若重新產生商業識別碼，請[使用新的識別碼重新註冊裝置](enroll-devices.md#device-enrollment)。這項流程可能會導致在轉換期間遺失診斷資料。  

### <a name="windows-commercial-data-opt-in"></a>Windows 商業資料加入

<!--64-->
此屬性僅適用於執行 Windows 7 或 Windows 8.1 的裝置。 其會執行與 [Windows 診斷資料加入](#windows-diagnostic-data-opt-in)相似的測試 (CommercialDataOptIn 值除外)。

### <a name="check-device-name-in-diagnostic-data"></a>檢查診斷資料中的裝置名稱

<!--56,58-->
若此檢查成功，則表示裝置已正確設定為共用裝置名稱。

否則，可能會顯示下列其中一個錯誤：

- 無法檢查要作為 Windows 診斷資料一部分傳送至 Microsoft 的裝置名稱。 請檢查記錄以取得例外狀況詳細資料  

- 無法將 AllowDeviceNameInTelemetry 寫入登錄機碼 `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`。 請檢查權限  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

請檢查此登錄機碼上的權限。 確認本機系統帳戶可以針對要設定的 Configuration Manager 用戶端存取此機碼。 這也可能是由發生衝突的群組原則物件所造成。 如需詳細資訊，請參閱 [Windows 設定](enroll-devices.md#windows-settings)。  

請確認另一項原則機制 (例如群組原則) 並未停用此設定。

### <a name="diagtrack-service-configuration"></a>DiagTrack 服務設定

<!--44,45,50-->
若此檢查成功，則表示 DiagTrack 元件已在裝置上正確設定。 電腦分析的最低版本需求是 10010586 (10.0.10586)。

否則，可能會顯示下列其中一個錯誤：

- 已連線使用者體驗與遙測 (diagtrack.dll) 元件已過期。 請檢查需求  

- 找不到已連線使用者體驗與遙測 (diagtrack.dll) 元件。 請檢查需求  

- 啟用並啟動已連線的使用者體驗與遙測服務來將資料傳送給 Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

安裝最新的更新。 如需詳細資訊，請參閱[裝置更新](enroll-devices.md#update-devices)。

請確認裝置上的**已連線使用者體驗與遙測**服務正在執行。

### <a name="diagtrack-version"></a>DiagTrack 版本

此屬性會顯示裝置上已連線使用者體驗與遙測元件的目前版本。 該屬性會顯示 `%windir%\System32\diagtrack.dll` 上的檔案版本 (不帶小數點)。 例如，檔案版本 10.0.10586 會顯示為 10010586。

### <a name="sqm-id-retrieval"></a>SQM 識別碼擷取

<!--38-->
此屬性主要適用於 Windows 7 裝置。 其也可以由更新的 OS 版本作為裝置後援識別碼使用。

若並未成功，其可能會顯示下列錯誤：

- 無法擷取舊版裝置遙測識別碼 (SQM 識別碼)

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

請確認您環境中沒有重複的識別碼。 例如，使用尚未一般化的 OS 映像部署裝置。

### <a name="unique-device-identifier-retrieval"></a>唯一裝置識別碼擷取

<!--54-->
電腦分析會使用 Microsoft 帳戶服務，以取得更可靠的裝置身分識別。

請確認 **Microsoft 帳戶登入小幫手**服務並未停用。 啟動類型應為**手動 (觸發程序啟動)** 。

若要停用終端使用者 Microsoft 帳戶存取，請使用原則設定，而非封鎖此端點。 如需詳細資訊，請參閱[企業中的 Microsoft 帳戶](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。

### <a name="windows-diagnostic-data-opt-in"></a>Windows 診斷資料加入

<!--8,40,55,62-->
此屬性會檢查 Windows 已正確設為允許診斷資料。 其會檢查下列登錄機碼中的 AllowTelemetry 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

請檢查這些登錄機碼上的權限。 確認本機系統帳戶可以針對要設定的 Configuration Manager 用戶端存取這些機碼。 這也可能是由發生衝突的群組原則物件所造成。 如需詳細資訊，請參閱 [Windows 設定](enroll-devices.md#windows-settings)。  

如需詳細資訊，請檢閱用戶端上的 M365AHandler.log。  

## <a name="see-also"></a>請參閱

[針對電腦分析進行疑難排解](troubleshooting.md) \(部分機器翻譯\)
