---
title: 針對連線快取進行疑難排解
titleSuffix: Configuration Manager
description: Microsoft 連線快取的技術詳細資料，可協助您針對問題進行疑難排解。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5be6158a2ed7d79af2bee72c81a462e4d83b68e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700866"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>在 Configuration Manager 中針對 Microsoft 連線快取進行疑難排解

本文提供 Configuration Manager 中 Microsoft 連線快取的相關技術詳細資料。 可用來協助您針對環境中可能發生的問題進行疑難排解。 如需其運作方式及使用方式的詳細資訊，請參閱 [Configuration Manager 中的 Microsoft 連線快取](../../../plan-design/hierarchy/microsoft-connected-cache.md)。

> [!NOTE]
> 從 1910 版開始，這項功能現在稱為 **Microsoft 連線快取**。 先前稱為傳遞最佳化網路內快取 (DOINC)。

## <a name="verify"></a>確認

當您正確安裝「傳遞最佳化」快取伺服器，且正確設定用戶端時，它們會從發佈點上安裝的快取伺服器 (而不是網際網路) 下載。

請[在用戶端上](#bkmk_verify-client)或[在伺服器上](#bkmk_verify-server)確認此行為。

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a> 在用戶端上驗證

1. 在執行 Windows 10 1809 版或更新版本的用戶端上，下載雲端管理的內容。 如需連線快取所支援內容類型的詳細資訊，請參閱[驗證連線快取](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify)。

2. 開啟 PowerShell 並執行下列命令：`Get-DeliveryOptimizationStatus`

例如：

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

請注意，`BytesFromCacheServer` 屬性不是零。

如果未正確設定用戶端，或未正確安裝快取伺服器，則傳遞最佳化用戶端會回復為原始的雲端來源。 然後，BytesFromCacheServer 屬性會是零。

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a> 在伺服器上驗證

首先，驗證已正確設定登錄屬性：`HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`。 例如，磁碟機快取位置是 `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`，其中 `PrimaryDrivesInput` 可以是多個磁碟機 (例如 `C,D,E`)。

接下來，使用下列方法，以必要標頭模擬伺服器的用戶端下載要求。

1. 以系統管理員的身分開啟 64 位元 PowerShell 視窗。
2. 執行下列命令，並以伺服器的名稱或 IP 位址取代 `<DoincServer>`：

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

輸出看起來類似下列範例：

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

下列屬性表示成功：

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>記錄檔

- ARR 安裝記錄檔：`%temp%\arr_setup.log`

- DO 快取伺服器安裝記錄檔：發佈點上的 `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log`，以及站台伺服器上的 `DistMgr.log`

- IIS 作業記錄檔：預設為 `%SystemDrive%\inetpub\logs\LogFiles`

- DO 快取伺服器作業記錄檔：`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > 在其他用途中，此記錄檔可協助您識別 Microsoft 雲端的連線問題。

## <a name="setup-error-codes"></a>安裝錯誤碼

下表列出 Configuration Manager 在發佈點上安裝連線快取元件時可能發生的可能錯誤碼：

| 錯誤碼 | 錯誤描述 |
|------------|-------------------|
| 0x00000000 | 成功 |
| 0x00000BC2 | 成功，需要重新開機 |
| 0x00000643 | 一般安裝失敗 |
| 0x00D00001 | 只有在已安裝 Internet Information Services (IIS) 時，才能執行連線快取安裝程式 |
| 0x00D00002 | 只有在伺服器上有「預設的網站」時，才能執行連線快取安裝程式 |
| 0x00D00003 | 如果已安裝應用程式要求路由 (ARR)，則無法安裝連線快取 |
| 0x00D00004 | 只有在 Install.ps1 指令碼已安裝應用程式要求路由 (ARR) 時，才能執行連線快取安裝程式 |
| 0x00D00005 | 連線快取安裝程式需要以系統管理員身分執行 PowerShell 工作階段 |
| 0x00D00006 | 連線快取安裝程式只能從 64 位元 PowerShell 環境執行 |
| 0x00D00007 | 連線快取安裝程式只能在 Windows Server 上執行 |
| 0x00D00008 | 失敗：所指定快取磁碟機數目必須符合指定的快取磁碟機大小百分比數目 |
| 0x00D00009 | 失敗：必須提供有效的快取節點識別碼 |
| 0x00D0000A | 失敗：必須提供有效的快取磁碟機集合 |
| 0x00D0000B | 失敗：必須提供有效的快取磁碟機大小百分比集合 |
| 0x00D0000C | 失敗：必須提供有效的快取磁碟機大小百分比集合或快取磁碟機大小 (GB) |
| 0x00D0000D | 失敗：無法同時提供有效的快取磁碟機大小百分比集合與快取磁碟機大小 (GB) |
| 0x00D0000E | 失敗：所指定快取磁碟機數目必須符合指定的快取磁碟機大小 (GB) 數目 |
| 0x00D0000F | 失敗：無法將 applicationhost.config 檔案從 $AppHostConfig 備份至 $AppHostConfigDestinationName |
| 0x00D00010 | 失敗：無法將預設的網站 web.config 檔案從 $WebsiteConfigFilePath 備份至 $WebConfigDestinationName |
| 0x00D00011 | 失敗：SetupARRWebFarm.ps1 中發生例外狀況 |
| 0x00D00012 | 失敗：SetupARRWebFarmRewriteRules.ps1 中發生例外狀況 |
| 0x00D00013 | 失敗：SetupARRWebFarmProperties.ps1 中發生例外狀況 |
| 0x00D00014 | 失敗：SetupAllowableServerVariables.ps1 中發生例外狀況 |
| 0x00D00015 | 失敗：SetupFirewallRules.ps1 中發生例外狀況 |
| 0x00D00016 | 失敗：SetupAppPoolProperties.ps1 中發生例外狀況 |
| 0x00D00017 | 失敗：SetupARROutboundRules.ps1 中發生例外狀況 |
| 0x00D00018 | 失敗：SetupARRDiskCache.ps1 中發生例外狀況 |
| 0x00D00019 | 失敗：SetupARRProperties.ps1 中發生例外狀況 |
| 0x00D0001A | 失敗：SetupARRHealthProbes.ps1 中發生例外狀況 |
| 0x00D0001B | 失敗：VerifyIISSItesStarted.ps1 中發生例外狀況 |
| 0x00D0001C | 失敗：SetDrivesToHealthy.ps1 中發生例外狀況 |
| 0x00D0001D | 失敗：VerifyCacheNodeSetup.ps1 中發生例外狀況 |
| 0x00D0001E | 如果預設網站不在連接埠 80 上，您就無法安裝連線快取 |
| 0x00D0001F | 失敗：快取磁碟機配置 (百分比) 不能超過 100 |
| 0x00D00020 | 失敗：快取磁碟機配置 (GB) 不能超過磁碟機的可用空間 |
| 0x00D00021 | 失敗：快取磁碟機配置 (百分比) 必須大於 0 |
| 0x00D00022 | 失敗：快取磁碟機配置 (GB) 必須大於 0 |
| 0x00D00023 | 失敗：RegisterScheduledTask_CacheNodeKeepAlive 中發生例外狀況 |
| 0x00D00024 | 失敗：RegisterScheduledTask_Maintenance 中發生例外狀況 |
| 0x00D00025 | 失敗：設定下列 HTTPS 伺服器陣列的重寫規則時發生例外狀況：$FarmName |
| 0x00D00026 | 失敗：設定下列 HTTP 伺服器陣列的重寫規則時發生例外狀況：$FarmName |
| 0x00D00027 | 您無法安裝連線快取，因為無法安裝相依軟體「應用程式要求路由 (ARR)」。 請參閱位於 %temp%\arr_setup.log 的記錄檔 |

## <a name="iis-configurations"></a>IIS 設定

DO 快取伺服器安裝會對發佈點上的 IIS 設定進行幾項修改。

### <a name="application-request-routing"></a>應用程式要求路由

DO 快取伺服器會安裝及設定 IIS [應用程式要求路由 (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing)。 為避免可能發生的衝突，發佈點無法安裝此元件。

### <a name="allowed-server-variables"></a>允許的伺服器變數

在您安裝 DO 快取伺服器之後，預設的網站會有下列「本機」  伺服器變數：

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### <a name="rewrite-rules"></a>重寫規則

DO 快取伺服器會新增下列重寫規則：

#### <a name="inbound-rewrite-rules"></a>輸入重寫規則

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>輸出重寫規則

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>管理伺服器資源

每部 DO 快取伺服器所需磁碟空間可能會根據您組織的更新需求而有所不同。 100 GB 應該有足夠的空間來快取下列內容：

- 功能更新
- 兩到三個月的品質和 Office 更新
- Microsoft Intune 應用程式和 Windows 收件匣應用程式

DO 快取伺服器不應耗用太多的系統記憶體或處理器時間。 當您安裝 DO 快取伺服器之後，如果您發現大量的處理序或記憶體資源耗用量，請分析 IIS 和 ARR 記錄檔。

如果 IIS 和 ARR 記錄檔在伺服器上佔用太多空間，您可以使用數種方法來管理記錄檔。 如需詳細資訊，請參閱 [Managing IIS Log File Storage](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview) (管理 IIS 記錄檔儲存體)。

## <a name="see-also"></a>請參閱

[Configuration Manager 中的 Microsoft 連線快取](../../../plan-design/hierarchy/microsoft-connected-cache.md)
