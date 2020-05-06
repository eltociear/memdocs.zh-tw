---
title: 群組原則設定
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 和電腦分析在 Windows 中所使用的本機和群組原則設定
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0224d9faecb9ff17afc2af3a57ba222023b5a3d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701736"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>電腦分析的群組原則設定

適用於：  Configuration Manager (最新分支)

本文詳細說明 Configuration Manager 和電腦分析在 Windows 中使用的本機和群組原則設定。

當 Configuration Manager 在電腦分析中註冊裝置後，會設定 Windows 原則以設定裝置。 在大多數情況下，只會使用 Configuration Manager 來進行這些設定。

## <a name="windows-settings"></a>Windows 設定

Configuration Manager 會在下列其中一或兩個登錄機碼中設定 Windows 原則：

- 群組原則物件 (**GPO**)：`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **本機**原則喜好設定：`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| 原則 | 路徑 | 適用於 | 值 |
|--------|------|------------|-------|
| **CommercialId** | 本機 | 所有 Windows 版本 | 若要讓裝置顯示在電腦分析中，請使用組織商業識別碼來進行設定。 |
| **AllowTelemetry**  | GPO | Windows 10 | 針對 [基本]  」設定為 `1`、[增強]  設定為 `2`，或設定為 `3` 以取得**完整**診斷資料。 電腦分析至少需要基本診斷資料。 Microsoft 建議針對電腦分析使用「增強 (限制)」層級。 如需詳細資訊，請參閱[在組織中設定 Windows 診斷資料](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization)。 |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10 1803 版與更新版本 | 只有在 AllowTelemetry 設定為 `2` 時，才會套用此設定。 其會將要傳送給 Microsoft 的「增強」診斷資料事件限制為只有電腦分析所需的事件。 如需詳細資訊，請參閱[透過限制增強診斷資料原則所收集的 Windows 10 診斷資料事件與欄位](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)。 |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10 1803 版與更新版本 | 讓裝置能夠傳送裝置名稱。 根據預設，裝置名稱不會傳送至 Microsoft。 如未傳送裝置名稱，則其會在電腦分析中顯示為「不明」。 如需詳細資訊，請參閱[裝置名稱](enroll-devices.md#device-name)。 |
| **CommercialDataOptIn** | 本機 | Windows 8.1 和更舊版本 | 電腦分析需要的值為 `1`。 如需詳細資訊，請參閱 [Commercial Data Opt-in in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)) (Windows 7 中的商業資料加入)。 |
| **RequestAllAppraiserVersions** | 兩者 | Windows 8.1 和更舊版本 | 電腦分析要求值必須為 `1`，資料收集才能正常運作。 |
| **DisableEnterpriseAuthProxy** | GPO | 所有 Windows 版本 | 如果您的環境需要使用了 Windows 整合式驗證的使用者驗證 Proxy 來存取網際網路，則電腦分析需要 `0` 值才能讓資料收集正常運作。 如需詳細資訊，請參閱 [Proxy 伺服器驗證](enable-data-sharing.md#proxy-server-authentication)。 |

> [!IMPORTANT]
> 在大多數情況下，只會使用 Configuration Manager 來進行這些設定。 請不要將這些設定也套用到網域群組原則物件。 如需詳細資訊，請參閱[衝突解決](enroll-devices.md#conflict-resolution)。

### <a name="settings-from-upgrade-readiness"></a>來自更新整備小幫手的設定

Windows Analytics 也會透過更新整備小幫手指令碼來設定下列原則：

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

如果您在裝置上執行更新整備小幫手上線指令碼，則這些原則設定可能仍然存在。 請勿使用舊版指令碼。 在向電腦分析註冊裝置前，請先移除這些先前的原則設定。

## <a name="group-policy-settings"></a>群組原則設定

一般而言，請使用 Configuration Manager 集合來針對處理電腦分析設定與註冊。 使用直接成員資格或查詢，以包含或排除集合中的裝置。 如需詳細資訊，請參閱[如何建立集合](../core/clients/manage/collections/create-collections.md)。

Configuration Manager 會在目標集合上設定商業識別碼和診斷資料設定。 如果您需要針對不同的裝置群組來設定不同的診斷資料設定，請使用群組原則設定來覆寫 Configuration Manager 設定。 例如，您需要為某些裝置設定 [增強式 (有限)]  層級，並為其他裝置設定 [基本]  層級。 某些裝置可能會有不同的 [Proxy 伺服器驗證](enable-data-sharing.md#proxy-server-authentication)設定。

相關的群組原則設定位於下列路徑：[電腦設定]   > [系統管理範本]   > [Windows 元件]   > [資料收集與預覽組建]  。

群組原則設定只會修改下列機碼中的登錄設定：`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> 當您使用群組原則設定來啟用複雜案例時，請特別注意可能會造成設定衝突的原則設定。 只有在*值不存在時*，Configuration Manager 才會進行 [Windows 設定](#windows-settings)。 群組原則設定的優先順序高於 Configuration Manager 設定，因此某些群組原則設定可能會導致電腦分析發生問題。

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>可能與電腦分析的 Configuration Manager 設定發生衝突的群組原則設定

下表中的群組原則設定最有可能會與 Configuration Manager 在裝置上所設定，並向電腦分析註冊的 Windows 設定發生衝突：

| 顯示名稱 | 登錄值 | 對電腦分析中所註冊裝置的影響 |
|--------------|----------------|-------------------------------------------------|
| **設定商業識別碼** | CommercialId | 如果您將此原則設定為不同的值，其將會覆寫 Configuration Manager 所設定的商業識別碼。 如果識別碼不同，所設定的裝置可能不會出現在電腦分析中。 |
| **允許遙測** | AllowTelemetry | 如果您將此原則設定為不同的值，其將會覆寫您在 Configuration Manager 中為目標集合所設定的全域診斷資料層級。 |
| **將增強的診斷資料限制為 Windows Analytics 所需的最小值** | LimitEnhancedDiagnosticDataWindowsAnalytics | 此原則相依於先前的 AllowTelemetry 設定。 根據您在 Configuration Manager 或群組原則中所設定的層級而定，此原則可以將裝置上的診斷資料層級變更為 [增強]  或 [增強 (有限)]  。 只有當 AllowTelemetry 設定為 `2` (**增強**) 時，才會套用此原則。 |
| **允許在 Windows 診斷資料中傳送裝置名稱** | AllowDeviceNameInTelemetry | 如果您選擇在 Configuration Manager 中傳送裝置名稱，則可以藉由將此原則設定為 [停用] 來加以覆寫。 當您停用此設定時，裝置名稱會在電腦分析中顯示為「未知」。 如需詳細資訊，請參閱[裝置名稱](enroll-devices.md#device-name)。 |
| **為已連線的使用者體驗和遙測服務設定已驗證的 Proxy 使用方式** | DisableEnterpriseAuthProxy | 如果您將 Configuration Manager 裝置設定為使用使用者驗證 Proxy (`0`)，然後將此原則設定為 [停用已驗證的 Proxy 使用方式]  (`1`)，則裝置會傳送系統內容 (而非使用者內容) 中的診斷資料。 如果您未在系統內容中使用 Proxy 來設定裝置，或裝置無法向 Proxy 驗證，Windows 便無法將診斷資料傳送給電腦分析。 |

> [!NOTE]
> 舊版原則**設定已連線的使用者體驗和遙測** (TelemetryProxy) 可讓 Windows 將診斷資料轉送至專用 Proxy，而不是使用使用者 (WinINET) 或裝置 (WinHTTP) Proxy。 某些 Windows 元件不支援此原則。 如果您使用此原則，則可能會導致電腦分析發生資料品質問題。

#### <a name="behavior-of-disabled-settings"></a>已停用設定的行為

如果您將這些群組原則設定設為 [停用]  ，其會對系統行為產生不同的影響。

- 當您停用 **CommercialId** 原則時，Windows 會移除登錄值。 商業識別碼的 Configuration Manager 設定 (設定於本機原則登錄路徑中) 便會套用至裝置中。

- 針對 Configuration Manager 在與群組原則相同的登錄位置中設定的原則，當您在群組原則中停用設定時，Windows 會移除登錄值。 Configuration Manager 會在下一次的原則處理週期中再次進行設定，而 Windows 則會在下一次群組原則重新整理時將設定移除。 設定一直這樣變化可能會導致電腦分析出現您不想要的行為。

  - 如果您將這些群組原則設定設為 [未設定]  ，Windows 就只會移除該值一次，而不會繼續將其移除。 此設定可讓 Configuration Manager 如預期地套用其值。

### <a name="group-policy-settings-to-customize-the-user-experience"></a>用來自訂使用者體驗的群組原則設定

Configuration Manager 或電腦分析不需要這些群組原則設定。 您可以在群組原則中進行設定，以設定使用者在使用 Windows 診斷資料時的體驗。

| 顯示名稱 | 登錄值 | 對電腦分析中所註冊裝置的影響 |
|--------------|----------------|-------------------------------------------------|
| **設定遙測加入變更通知** | DisableTelemetryOptInChangeNotification | 從 Windows 10 1803 版開始，當診斷資料層級有所變更時，Windows 就會通知使用者。 使用此原則即可停用通知。 |
| **設定遙測加入設定使用者介面** | DisableTelemetryOptInSettingsUx | 當設定診斷資料層級時，您可以設定裝置的界限。 從 Windows 10 1803 版開始，使用者已可設定較低的層級。 使用此原則可防止使用者變更診斷層級。 如需詳細資訊，請參閱[在組織中設定 Windows 診斷資料](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。 |
| **停用刪除診斷資料** | DisableDeviceDelete | 從 Windows 10 1809 版開始，使用者可以從 [診斷和意見反應]  設定頁面中刪除診斷資料。 使用此原則可防止刪除 Microsoft 從裝置收集到的診斷資料。 |
| **停用診斷資料檢視器** | DisableDiagnosticDataViewer | 從 Windows 10 1809 版開始，使用者可以從 [診斷和意見反應]  設定頁面中啟用和開啟診斷資料檢視器。 使用此原則可在 Windows 設定中停用診斷資料檢視器，並防止其顯示 Microsoft 從裝置收集到的診斷資料。|
