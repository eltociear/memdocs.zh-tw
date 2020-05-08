---
title: 啟用資料共用
titleSuffix: Configuration Manager
description: 與電腦分析共用診斷資料的參考指南。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f8dd7c4c561ca22c679ee8ae03764ebb20b87664
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906091"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>啟用電腦分析的資料共用

若要向電腦分析註冊裝置，裝置便需要傳送診斷資料給 Microsoft。 若您的環境使用 Proxy 伺服器，請使用此資訊協助設定 Proxy。

## <a name="diagnostic-data-levels"></a>診斷資料層級

![電腦分析診斷資料層級圖表](media/diagnostic-data-levels.png)

當您將電腦分析與 Configuration Manager 整合時，您也會使用 Configuration Manager 管理裝置上的診斷資料層級。 如需最佳體驗，請使用 Configuration Manager。

> [!Important]  
> 在大多數情況下，只會使用 Configuration Manager 來進行這些設定。 請不要將這些設定也套用到網域群組原則物件。 如需詳細資訊，請參閱[衝突解決](enroll-devices.md#conflict-resolution)。

電腦分析的基本功能會在 [基本]  [診斷資料層級](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)上運作。 若您沒有在 Configuration Manager 中設定 [增強 (受限)]  層級，您將無法取得電腦分析的下列功能：

- 應用程式使用量
- [其他應用程式見解](compat-assessment.md#additional-insights)
- 部署狀態資料
- 健康情況監視資料

Microsoft 建議您搭配電腦分析啟用 [增強 (受限)]  診斷資料層級，以利最大化您的獲益。

> [!Tip]
> Configuration Manager 中的 [增強 (受限)]  設定，與執行 Windows 10 版本 1709 及更新版本裝置上可用的**將增強診斷資料限制在 Windows Analytics 所需要的最低程度**原則是相同的設定。
>
> 執行 Windows 10 版本 1703 及更早版本、Windows 8.1 或 Windows 7 的裝置沒有此原則設定。 當您在 Configuration Manager 中設定 [增強 (受限)]  設定時，這些裝置會回復為 [基本]  層級。
>
> 執行 Windows 10 版本 1709 的裝置則包含此原則設定。 但是，當您在 Configuration Manager 中設定 [增強 (受限)]  設定時，這些裝置也會回復為 [基本]  層級。

如需使用 [增強 (受限)]  與 Microsoft 共用的診斷資料詳細資訊，請參閱 [Windows 10 增強診斷資料事件與欄位](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)。

> [!Important]
> Microsoft 堅決致力於提供可讓您掌控隱私權的工具和資源。 因此，雖然電腦分析支援 Windows 8.1 裝置，Microsoft 不會從位於歐洲國家/地區 (EEA 與瑞士) 的 Windows 8.1 裝置收集 Windows 診斷資料。

如需詳細資訊，請參閱[電腦分析隱私權](privacy.md)。

下列文章也是進一步了解 Windows 診斷資料層級的良好資源：

- [適用於 IT 決策者的 Windows 10 和 GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [在組織中設定 Windows 診斷資料](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> 設為限制增強診斷資料的用戶端也會在初次的完整掃描時，傳送約 2 MB 的資料到 Microsoft 雲端。 每天的每日差異介於 250 至 400 KB。
>
> 每日差異掃描會在裝置當地時間的上午 3:00 進行。 有些事件會在一整天中的第一個可用時間內進行傳送。 您無法設定這些時間。
>
> 如需詳細資訊，請參閱[在組織中設定 Windows 診斷資料](https://aka.ms/enterprisetelemetry)。  

## <a name="endpoints"></a>端點

若要啟用資料共用，請設定 Proxy 伺服器，以允許下列網際網路端點。

> [!Important]  
> 針對隱私權和資料完整性，Windows 會在與診斷資料端點通訊時，檢查 Microsoft SSL 憑證 (憑證關聯)。 無法進行 SSL 攔截和檢查。 若要使用電腦分析，請從 SSL 檢查中排除這些端點。<!-- BUG 4647542 -->

從 2002 版開始，如果 Configuration Manager 站台無法連線至雲端服務的必要端點，就會引發重大狀態訊息識別碼 11488。 當無法連線至服務時，SMS_SERVICE_CONNECTOR 元件狀態會變更為重大。 在 Configuration Manager 主控台的 [元件狀態](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) 節點中，查看詳細狀態。<!-- 5566763 -->

> [!NOTE]
> 如需 Microsoft IP 位址範圍的詳細資訊，請參閱 [Microsoft 公用 IP 空間](https://www.microsoft.com/download/details.aspx?id=53602) \(英文\)。 這些位址會定期更新。 服務沒有任何細微性，您可以使用這些範圍中的任何 IP 位址。

### <a name="server-connectivity-endpoints"></a>伺服器連線端點

服務連接點必須與下列端點進行通訊：

| 端點  | 函式  |
|-----------|-----------|
| `https://aka.ms` | 用來找出服務 |
| `https://graph.windows.net` | 用來在將您的階層附加到電腦分析 (於 Configuration Manager 伺服器角色上) 時，自動擷取如 CommercialId 等設定。 如需詳細資訊，請參閱[為站台系統伺服器設定 Proxy](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://*.manage.microsoft.com` | 用來與電腦分析同步裝置集合成員資格、部署計劃和裝置整備程度狀態 (僅限在 Configuration Manager 伺服器角色上)。 如需詳細資訊，請參閱[為站台系統伺服器設定 Proxy](../core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>使用者體驗和診斷元件端點

用戶端裝置必須與下列端點進行通訊：

| 端點  | 函式  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | 已連線的使用者體驗和診斷元件端點。 由執行 Windows 10 版本 1809 或更新版本，或是安裝了 2018-09 累積更新的版本 1803 或更新版本裝置使用。 |
| `https://v10.events.data.microsoft.com` | 已連線的使用者體驗和診斷元件端點。 由執行「並未」  安裝 2018-09 累積更新的 Windows 10 版本 1803 裝置使用。 |
| `https://v10.vortex-win.data.microsoft.com` | 已連線的使用者體驗和診斷元件端點。 由執行 Windows 10 版本 1709 或更早版本的裝置使用。 |
| `https://vortex-win.data.microsoft.com` | 已連線的使用者體驗和診斷元件端點。 由執行 Windows 7 和 Windows 8.1 的裝置使用 |

### <a name="client-connectivity-endpoints"></a>用戶端連線端點

用戶端裝置必須與下列端點進行通訊：

| 索引 | 端點  | 函式  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | 啟用相容性更新，傳送資料至 Microsoft。 |
| 2 | `http://adl.windows.com` | 允許相容性更新從 Microsoft 接收最新的相容性資料。 |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1803 或更早版本中監視部署健康情況。 |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中提供裝置健康情況報告。 |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中監視部署健康情況。 |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中監視部署健康情況。 |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中監視部署健康情況。 |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中監視部署健康情況。 |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中監視部署健康情況。 |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows 錯誤報告 (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting)。 需要用來在 Windows 10 版本 1809 或更新版本中監視部署健康情況。 |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [線上當機分析 (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis)。 需要用來在 Windows 10 版本 1809 或更新版本中提供裝置健康情況報告。 |
| 12 | `https://oca.telemetry.microsoft.com`  | [線上當機分析 (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis)。 需要用來在 Windows 10 版本 1803 或更早版本中監視部署健康情況。 |
| 13 | `https://login.live.com` | 需要用來為電腦分析提供更可靠的裝置身分識別。 <br> <br>若要停用終端使用者 Microsoft 帳戶存取，請使用原則設定，而非封鎖此端點。 如需詳細資訊，請參閱[企業中的 Microsoft 帳戶](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。 |
| 14 | `https://v20.events.data.microsoft.com` | 已連線的使用者體驗和診斷元件端點。 |

## <a name="proxy-server-authentication"></a>Proxy 伺服器驗證

如果您的組織使用 Proxy 伺服器驗證來存取網際網路，請確定其不會因為驗證而封鎖診斷資料。 如果您的 Proxy 不允許裝置傳送這項資料，裝置就不會顯示在電腦分析中。

### <a name="bypass-recommended"></a>略過 (建議)

設定您的 Proxy 伺服器，使其不會向前往診斷資料端點的流量要求 Proxy 驗證。 此選項是最全面的解決方案。 適用於所有 Windows 10 版本。  

### <a name="user-proxy-authentication"></a>使用者 Proxy 驗證

設定裝置，以使用登入使用者的內容進行 Proxy 驗證。 此方法需要下列設定：

- 裝置具有受支援 Windows 版本的最新品質更新

- 在 Windows 設定的 [網路與網際網路] 群組中的 [Proxy 設定]  內，設定使用者層級 Proxy (WinINET Proxy)。 您也可以使用舊版的 [網際網路選項] 控制台。

- 請確認使用者具備觸達診斷資料端點的 Proxy 權限。 此選項需要裝置具備擁有 Proxy 權限的主控台使用者，因此您無法搭配無周邊裝置使用此方法。

> [!IMPORTANT]
> 使用者 Proxy 驗證方法與使用 Microsoft Defender 進階威脅防護不相容。 此行為是因為此驗證依賴將 **DisableEnterpriseAuthProxy** 登錄機碼設為 `0`，但 Microsoft Defender ATP 需要將其設為 `1`。 如需詳細資訊，請參閱[在 Microsoft Defender ATP 中設定電腦 Proxy 及網際網路連線能力設定](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)。

### <a name="device-proxy-authentication"></a>裝置 Proxy 驗證

此方法支援下列案例：

- 無周邊裝置，沒有使用者登入，或裝置的使用者無法存取網際網路

- 未使用 Windows 整合式驗證的已驗證 Proxy

- 如果您也使用 Microsoft Defender 進階威脅防護

這個方法是最複雜的，因為其需要下列設定：

- 確認裝置可在本機系統內容中，透過 WinHTTP 觸達 Proxy 伺服器。 使用下列任一選項設定此行為：

  - 命令列 `netsh winhttp set proxy`

  - Web Proxy 自動探索 (WPAD) 通訊協定

  - 透明 Proxy

  - 請使用下列群組原則設定來設定全裝置的 WinINET Proxy：**讓 Proxy 設定依每部電腦來設定 (而不是依每位使用者)** (ProxySettingsPerUser = `1`)

  - 路由連線，或是使用網路位址轉譯 (NAT) 的連線

- 設定 Proxy 伺服器，允許 Active Directory 中的電腦帳戶存取診斷資料端點。 此設定需要 Proxy 伺服器支援 Windows 整合式驗證。  
