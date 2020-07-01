---
title: 網際網路存取需求
titleSuffix: Configuration Manager
description: 了解允許用於 Configuration Manager 功能之完整功能的網際網路端點。
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb965ec6547ff1c06586464780b6db224b943000
ms.sourcegitcommit: 9a8a9cc7dcb6ca333b87e89e6b325f40864e4ad8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2020
ms.locfileid: "84740758"
---
# <a name="internet-access-requirements"></a>網際網路存取需求

某些 Configuration Manager 功能依賴網際網路連線能力來取得完整功能。 如果您的組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，請務必允許這些端點。

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a> 服務連接點

這些設定會套用到裝載服務連接點的電腦，以及所有位於該電腦與網際網路之間的防火牆。 它們都必須允許透過連出連接埠 **TCP 443** (適用於 HTTPS) 和連出連接埠 **TCP 80** (適用於 HTTP) 來與下列網際網路位置通訊。

服務連接點支援使用 Web Proxy (不論有無驗證) 來使用這些位置。 如需詳細資訊，請參閱 [Proxy 伺服器支援](proxy-server-support.md)。

如需服務連接點的詳細資訊，請參閱[關於服務連接點](../../servers/deploy/configure/about-the-service-connection-point.md)。

其他 Configuration Manager 功能可能需要來自服務連接點的其他端點。 如需詳細資訊，請參閱本文的其他小節。

> [!TIP]  
> 服務連接點會在連線到 `go.microsoft.com` 或 `manage.microsoft.com` 時使用 Microsoft Intune 服務。 已知在服務連線點上，如果 Baltimore CyberTrust 根憑證未安裝、過期或損毀，Intune 連接器會發生連線問題。 如需詳細資訊，請參閱 [KB 3187516：服務連接點不會下載更新](https://support.microsoft.com/help/3187516) \(機器翻譯\)。  

從 2002 版開始，如果 Configuration Manager 站台無法連線至雲端服務的必要端點，則會引發重大狀態訊息識別碼 11488。 當無法連線至服務時，SMS_SERVICE_CONNECTOR 元件狀態會變更為重大。 在 Configuration Manager 主控台的 [元件狀態](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) 節點中，查看詳細狀態。<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a> 更新及服務

如需此功能的詳細資訊，請參閱 [Configuration Manager 的更新與服務](../../servers/manage/updates.md)。

> [!Tip]  
> 針對[管理見解](../../servers/manage/management-insights.md)規則 (**將網站連線到 Microsoft 雲端以進行 Configuration Manager 更新**) 啟用這些端點。

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Windows 10 服務

如需此功能的詳細資訊，請參閱[管理 Windows 即服務](../../../osd/deploy-use/manage-windows-as-a-service.md)。

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure 服務

如需此功能的詳細資訊，請參閱[設定要與 Configuration Manager 搭配使用的 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)。

- `management.azure.com` (Azure 公用雲端)
- `management.usgovcloudapi.net` (Azure 美國政府雲端)

## <a name="co-management"></a>共同管理

如果您向 Microsoft intune 註冊 Windows 10 裝置以進行共同管理，請確定那些裝置可以存取 Intune 所需的端點。 如需詳細資訊，請參閱 [Microsoft Intune 的網路端點](https://docs.microsoft.com/intune/intune-endpoints)。

## <a name="microsoft-store-for-business"></a>商務用 Microsoft Store

如果您要與[商務用 Microsoft Store](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) 整合 Configuration Manager，請確定服務連接點和目標裝置皆可以存取雲端服務。 如需詳細資訊，請參閱[商務用 Microsoft Store Proxy 設定](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration) \(部分機器翻譯\)。

## <a name="delivery-optimization"></a>傳遞最佳化

如果使用傳遞最佳化，用戶端即必須與其雲端服務通訊：`*.do.dsp.mp.microsoft.com`

支援 Microsoft 網內快取的發佈點也需要這些端點。

如需詳細資訊，請參閱下列文章：

- [傳遞最佳化常見問題](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Configuration Manager 的內容管理基本概念](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Configuration Manager 中的 Microsoft 連線快取](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a> 雲端服務

<!-- SCCMDocs-pr #3402 -->

本節涵蓋下列功能：

- 雲端管理閘道 (CMG)
- 雲端發佈點 (CDP)
- Azure Active Directory (Azure AD) 整合
- 以 Azure AD 為基礎的探索

如需 CMG 的詳細資訊，請參閱[進行 CMG 規劃](../../clients/manage/cmg/plan-cloud-management-gateway.md)。

下列各節依角色列出端點。 某些端點會依 `<name>` 參考服務，這是 CMG 或 CDP 的雲端服務名稱。 例如，如果您的 CMG 為 `GraniteFalls.CloudApp.Net`，則實際儲存體端點為 `GraniteFalls.blob.core.windows.net`。<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>服務連接點

針對 CMG/CDP 服務部署，服務連接點需要下列項目的存取權：

- 每個環境的特定 Azure 端點都會因設定而有所不同。 Configuration Manager 會將這些端點儲存於站台資料庫中。 在 SQL Server 中查詢 **AzureEnvironments** 資料表以取得 Azure 端點清單。

- [Azure 服務](#azure-services)

- 若為 Azure AD 使用者探索：

  - 1902 版和更新版本：Microsoft Graph 端點 `https://graph.microsoft.com/`

  - 1810 版和更早版本：Azure AD Graph 端點 `https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG 連接點

CMG 連接點需要下列服務端點的存取權：

- 雲端服務名稱 (針對 CMG 或 CDP)：
  - `<name>.cloudapp.net` (Azure 公用雲端)
  - `<name>.usgovcloudapp.net` (Azure 美國政府雲端)

- 服務管理端點：`https://management.core.windows.net/`  

- 儲存體端點 (針對啟用內容的 CMG 或 CDP)：
  - `<name>.blob.core.windows.net` (Azure 公用雲端)
  - `<name>.blob.core.usgovcloudapi.net` (Azure 美國政府雲端)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

CMG 連接點站台系統支援使用 Web Proxy。 如需針對 Proxy 設定此角色的詳細資訊，請參閱 [Proxy 伺服器支援](proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 CMG 連接點只需連線到 CMG 服務端點。 它不需要存取其他 Azure 端點。

### <a name="configuration-manager-client"></a>Configuration Manager 用戶端

- 雲端服務名稱 (針對 CMG 或 CDP)：
  - `<name>.cloudapp.net` (Azure 公用雲端)
  - `<name>.usgovcloudapp.net` (Azure 美國政府雲端)

- 儲存體端點 (針對啟用內容的 CMG 或 CDP)：
  - `<name>.blob.core.windows.net` (Azure 公用雲端)
  - `<name>.blob.core.usgovcloudapi.net` (Azure 美國政府雲端)

- Azure AD 端點 (針對 Azure AD 權杖擷取)：
  - `login.microsoftonline.com` (Azure 公用雲端)
  - `login.microsoftonline.us` (Azure 美國政府雲端)

### <a name="configuration-manager-console"></a>Configuration Manager 主控台

- Azure AD 端點 (針對 Azure AD 權杖擷取)：

  - Azure 公用雲端
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure 美國政府雲端
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a> 軟體更新

允許主動式軟體更新點存取下列端點，如此一來，WSUS 和自動更新就能與 Microsoft Update 雲端服務進行通訊：  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

如需軟體更新的詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。

### <a name="intranet-firewall"></a>內部網路防火牆

在下列案例中，您可能需要將端點新增至兩個站台系統之間的防火牆：

- 如果子站台具有軟體更新點
- 如果站台有以網際網路為基礎的遠端主動式軟體更新點

#### <a name="software-update-point-on-the-child-site"></a>子站台上的軟體更新點

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>管理 Office 365

> [!NOTE]
> 從 2020 年 4 月 21 日開始，「Office 365 專業增強版」會重新命名為「Microsoft 365 Apps 企業版」。 如需詳細資訊，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) \(部分機器翻譯\)。 在主控台正在進行更新時，您在 Configuration Manager 主控台與輔助文件中可能仍會看到提及舊名稱。

如果您使用 Configuration Manager 來部署和更新 Microsoft 365 Apps 企業版，請允許下列端點：

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` - 用來同步 Microsoft 365 Apps 企業版用戶端更新的軟體更新點

- `config.office.com` - 用來建立 Microsoft 365 Apps 企業版部署的自訂設定

## <a name="configuration-manager-console"></a>Configuration Manager 主控台

具有 Configuration Manager 主控台的電腦需要存取下列網際網路端點以取得特定功能：

### <a name="in-console-feedback"></a>主控台內意見反應

- `http://petrol.office.microsoft.com`

如需此功能的詳細資訊，請參閱[產品意見反應](../../understand/find-help.md#product-feedback)。

### <a name="community-workspace"></a>社群工作區

#### <a name="documentation-node"></a>文件節點

如需此主控台節點的詳細資訊，請參閱[使用 Configuration Manager 主控台](../../servers/manage/admin-console.md)。

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>社群中樞

如需此功能的詳細資訊，請參閱[社群中樞](../../servers/manage/community-hub.md)。

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>[監視] 工作區、[站台階層] 節點

如果您使用 [地理檢視]，請允許存取下列端點：

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>電腦分析

如需適用於電腦分析雲端服務所需端點的詳細資訊，請參閱[啟用資料共用](../../../desktop-analytics/enable-data-sharing.md#endpoints)。

## <a name="microsoft-public-ip-addresses"></a>Microsoft 公用 IP 位址

如需 Microsoft IP 位址範圍的詳細資訊，請參閱 [Microsoft 公用 IP 空間](https://www.microsoft.com/download/details.aspx?id=53602) \(英文\)。 這些位址會定期更新。 服務沒有任何細微性，您可以使用這些範圍中的任何 IP 位址。

## <a name="see-also"></a>請參閱

- [Configuration Manager 中使用的連接埠](../hierarchy/ports.md)

- [Configuration Manager 中的 Proxy 伺服器支援](proxy-server-support.md)
