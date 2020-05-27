---
title: 端點分析預覽
titleSuffix: Configuration Manager
description: 端點分析預覽的指示。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c7a99931db27b6a55c9e0722cc12c1d7a9cc9e80
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764232"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a> 端點分析預覽

> [!Note]  
> 這項資訊與預覽功能相關，可能會在正式發行之前進行大幅修改。 Microsoft 對於此處提供的資訊不做任何明示或暗示保證。 
>
> 如需端點分析變更的詳細資訊，請參閱[端點分析的新功能](whats-new-endpoint-analytics.md)。 
>
>如果您想要加入端點分析的私人預覽，請在[此表單中](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u)輸入詳細資料。 隨著預覽開放擴展，將會提供租用戶發行小眾測試版。


## <a name="endpoint-analytics-overview"></a>端點分析概觀

一般使用者可能會遇到長時間開機時間或其他中斷的情況。 這些中斷的原因可能是下列各項的組合：

- 舊版硬體
- 未針對終端使用者體驗最佳化的軟體設定
- 設定變更和更新所造成的問題

這些問題與其他終端使用者體驗問題仍然存在，因為 IT 對終端使用者體驗的了解不多。 一般而言，對這些問題的唯一了解來自慢速且成本低廉的支援通道，該通道通常無法提供有關需要最佳化之內容的明確資訊。 承擔這些問題成本的不僅僅是 IT 支援。 資訊工作者花費在處理問題上的時間也很昂貴。 降低使用者生產力的效能、可靠性與支援問題，也可能會對組織的盈虧造成很大的影響。

**端點分析**旨在改善使用者生產力，並透過提供使用者體驗的見解來降低 IT 支援成本。 見解可讓 IT 利用主動式支援來最佳化終端使用者體驗，並透過評估設定變更對使用者的影響來偵測使用者體驗的迴歸。

此初始版本著重於三點：

- [**建議的軟體**](#bkmk_uea_rs)：提供最佳使用者體驗的建議
- [**主動式補救指令碼處理**](#bkmk_uea_prs)：修正終端使用者發現問題前的常見支援問題
- [**啟動效能**](#bkmk_uea_bp)：協助 IT 快速地將使用者從開機狀態轉換為具備生產力，而不需要冗長的開機和登入延遲

此版本僅僅是開端。 初始版本發行之後，我們將迅速針對其他重要使用者體驗推出新的見解。 如需端點分析變更的詳細資訊，請參閱[端點分析的新功能](whats-new-endpoint-analytics.md)。

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a> 開始使用

若要開始使用端點分析，請確認先決條件，然後開始收集資料。 

### <a name="technical-prerequisites"></a>技術性必要條件

在此預覽版中，您可以透過 Configuration Manager 或 Microsoft Intune 來註冊裝置。 

若要透過 Intune 註冊裝置，此預覽版需要：
- 執行 Windows 10 的 Intune 已註冊裝置
- 啟動效能見解僅適用於執行 1903 版或更新版 Windows 10 企業版 (目前不支援家用版與專業版) 的裝置，且裝置必須加入 Azure AD 或混合式 Azure AD。 目前不支援加入工作場所網路的機器。
- 從裝置到 Microsoft 公用雲端的網路連線。 如需詳細資訊，請參閱[端點](#bkmk_uea_endpoints)。
- 必須具備 [Intune 服務管理員角色](https://docs.microsoft.com/intune/fundamentals/role-based-access-control)才能[開始收集資料](#bkmk_uea_start)。
   - 一旦按一下 [開始]，即表示您同意並確認您的客戶資料可能會儲存在您於佈建 Microsoft Intune 租用戶時所選取之位置以外的位置。
   - 在按一下 [開始收集資料] 後，其他唯讀角色就可以檢視資料。

若要透過 Configuration Manager 註冊裝置，此預覽版需要：
- Configuration Manager 2002 版或更新版本
- 升級至 2002 版或更新版本的用戶端
- 已在北美洲或歐洲的 Azure 租用戶位置啟用了 [Microsoft 端點管理員租用戶附加](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) \(部分機器翻譯\) (我們很快就會擴展到其他區域)

無論是透過 Intune 或 Configuration Manager 註冊裝置，[**主動式補救指令碼**](#bkmk_uea_prs)都具有下列需求：
- 裝置必須加入 Azure AD 或混合式 Azure AD，並符合下列其中一個條件：
- 由 Intune 管理的 Windows 10 企業版、專業版或教育版裝置
- 執行 Windows 10 企業版 1607 版或更新版本的[共同管理](../../comanage/overview.md)裝置，且[用戶端應用程式工作負載](../../comanage/workloads.md#client-apps)指向 Intune。
- 執行 Windows 10 企業版 1903 版或更新版本的[共同管理](../../comanage/overview.md)裝置，且[用戶端應用程式工作負載](../../comanage/workloads.md#client-apps)指向 Configuration Manager。

### <a name="licensing-prerequisites"></a>授權必要條件

端點分析包含在下列方案中： 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) 或更高版本
- [Microsoft 365 企業版 E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) 或更高版本。

主動式補救也要求受控裝置必須具備下列其中一項授權：
- Windows 10 企業版 E3 或 E5 (隨附於 Microsoft 365 F3、E3 或 E5 中)
- Windows 10 教育版 A3 或 A5 (隨附於 Microsoft 365 A3 或 A5)
- Windows 虛擬桌面存取 E3 或 E5

### <a name="permissions"></a>權限

#### <a name="endpoint-analytics-permissions"></a>端點分析權限

以下是用於端點分析的權限：
- [裝置設定] 類別底下的 [讀取]。
- [組織] 類別底下的 [讀取]。 <!--temporary for pp-->
- [端點分析] 類別底下適用於使用者角色的權限。

唯讀使用者只需要 [裝置設定] 和 [端點分析] 類別底下的 [讀取] 權限。 Intune 管理員通常需要所有權限。

#### <a name="proactive-remediations-permissions"></a>主動式補救權限

針對主動式補救，使用者需要 [裝置設定] 類別底下適用於其角色的權限。  如果使用者只使用主動式補救，則不需要 [端點分析] 目錄中的權限。

第一次使用主動式補救之前，需要透過 [Intune 服務管理員](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions)確認授權需求。

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a> 開始收集資料
- 如果您只要註冊 Intune 受控裝置，請跳到[在端點分析入口網站中上線](#bkmk_uea_onboard)一節。

- 如果您要註冊由 Configuration Manager 管理的裝置，就必須執行下列步驟：
   - [在 Configuration Manager 中啟用端點分析資料收集](#bkmk_uea_cm_enroll)
   - [在 Configuration Manager 中啟用資料上傳](#bkmk_uea_cm_upload)
   - [在端點分析入口網站中上線](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a> 註冊由 Configuration Manager 管理的裝置
<!--6051638, 5924760-->
在您註冊 Configuration Manager 裝置之前，請先確認包括啟用 [Microsoft Endpoint Manager 租用戶附加](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) \(部分機器翻譯\) 在內的[必要條件](#bkmk_uea_prereq)。 

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a> 在 Configuration Manager 中啟用端點分析資料收集

1. 在 Configuration Manager 主控台中，移至 [管理] > [用戶端設定] > [預設用戶端設定]。
1. 以滑鼠右鍵按一下並選取 [屬性]，然後選取 [電腦代理程式] 設定。
1. 將 [啟用端點分析資料收集] 設定為 [是]。
   > [!Important] 
   > 如果您已將現有的自訂用戶端代理程式設定部署到您的裝置，則必須更新該自訂設定中的 [啟用端點分析資料收集] 選項，然後將其重新部署到您的電腦，以使其生效。

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a> 在 Configuration Manager 中啟用資料上傳

1. 在 Configuration Manager 主控台中，移至 [管理] > [雲端服務] > [共同管理]。
1. 選取 [CoMgmtSettingsProd]，然後按一下 [屬性]。
1. 在 [設定上傳] 索引標籤上，選取 [為上傳至 Microsoft Endpoint Manager 的裝置啟用端點分析] 選項

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="為上傳至 Microsoft Endpoint Manager 的裝置啟用端點分析" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a> 在端點分析入口網站中上線
Configuration Manager 與 Intune 受控裝置都需要從端點分析入口網站中上線。

1. 移至 `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. 按一下 [啟動] 。 這會自動指派組態設定檔，以用來收集所有合格裝置的開機效能資料。 您可以在稍後[變更指派的裝置](#bkmk_uea_profile)。 最多可能需要 24 小時的時間，才能在您的 Intune 已註冊裝置重新開機後，從其中填入啟動效能資料。
   - 如需常見問題的詳細資訊，請參閱[針對啟動效能裝置註冊進行疑難排解](#bkmk_uea_enrollment_tshooter)。

## <a name="overview-page"></a>概觀頁面

準備好您的資料之後，您會在 [概觀] 頁面上看到一些資訊，如下所述：

- [使用者體驗分數] 是 [建議的軟體] 與 [啟動效能分數] 的 50/50 加權平均值。 我們將隨著時間擴充一組子分數。

- 您可以透過設定基準來比較目前的分數與其他分數。
  - 如[基準](#bkmk_uea_baselines)一節中所述，「商業中位數」有一個內建基準，以查看您與一般企業之間的比較。 您可以根據目前的計量來建立新的基準，以便追蹤進度或檢視一段時間內的迴歸。
   - 基準標記會針對您的整體分數與子分數顯示。 如果任何分數下降超過所選基準的可設定閾值，分數就會以紅色顯示，而且會將最高分數標示為需要注意。
  - [資料不足] 的狀態表示您沒有足夠的裝置報告來提供有意義的分數。 我們目前至少需要五部裝置。

- [篩選條件] 可讓您檢視部分裝置或使用者的分數。 不過，此預覽版中不會啟用篩選功能。

- [見解與建議] 是優先順序清單，可改善您的分數。 當您瀏覽至 [最佳做法] 或 [建議的軟體] 時，此清單會篩選到子節點的內容。

[![端點分析概觀頁面](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a> 建議的軟體

> [!Important]  
> 端點分析會計算所有 Intune 受控裝置的**軟體採用**分數，不論這些裝置是否已在端點分析中註冊。

已知特定軟體可改善終端使用者體驗，與較低層級的健康情況計量無關。 例如，Windows 10 的淨推薦分數比 Windows 7 高得多。 **軟體採用**分數是介於 0 到 100 之間的數字，代表已部署各種建議軟體之裝置的百分比加權平均值。 Windows 的目前加權高於其他計量，因為使用者與其進行互動的頻率更高。 計量如下所述： 

[![端點分析建議的軟體頁面](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10 提供比舊版 Windows 更好的使用者體驗。 如需詳細資訊，請參閱 [TEI 白皮書](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf)。

此計量會測量 Windows 10 與舊版 Windows 之間的裝置百分比。

從舊版 Windows 移動裝置的建議補救動作是使用[電腦分析](../../desktop-analytics/overview.md)來建立部署計畫。

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a> Autopilot

Microsoft Autopilot 透過減少全新體驗 (OOBE) 中的畫面數目並提供預設值，提供比原始體驗更簡單的 Windows 10 電腦初始佈建體驗，以確保員工裝置可根據出廠預設值或在重設時正確佈建。

此計量會測量已註冊 Autopilot 的 Windows 10 裝置百分比。

建議的補救動作是使用 [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot) 在 Autopilot 中註冊現有的裝置。

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) 為使用者提供許多增進生產力的優點，包括應用程式與服務的全裝置單一登入、Windows Hello 登入、自助式 BitLocker 修復，以及公司資料漫遊。

此計量會測量在 Azure AD 中註冊的裝置百分比。

您的 Microsoft Intune 受控裝置已在 Azure AD 中註冊。 Configuration Manager 所管理之裝置的建議補救動作是[在 Azure AD 中加以註冊](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)或[加以共同管理](../../comanage/overview.md)。 共同管理裝置也會改善您的雲端管理分數。

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a> 雲端管理

Microsoft Intune 為使用者提供數項生產力優勢，包括即使公司資源不在公司網路中也能夠進行存取，以及消除群組原則的需求及其效能額外負荷，進而提供較佳的終端使用者體驗。 此計量會測量在 Microsoft Intune 中註冊的電腦百分比。 了解 [Microsoft 為我們的員工啟用此功能](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune) (英文) 的方式。

由 Configuration Manager 所管理但尚未在 Intune 中註冊之裝置的建議補救動作是[加以共同管理](../../comanage/overview.md)。

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a> 無商業中位數

**商業中位數**的內建基準目前沒有以上各節所列之子分數的計量。

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a> 啟動效能

> [!NOTE]
> 如果您未看見所有裝置的啟動效能資料，請參閱[排解啟動效能裝置註冊的疑難](#bkmk_uea_enrollment_tshooter)。

啟動效能分數協助 IT 快速地將使用者從開機狀態轉換為具備生產力，而不需要冗長的開機和登入延遲。 [啟動分數] 是介於 0 到 100 之間的數字。 此分數是 [開機分數] 與 [登入] 分數的加權平均值，其計算方式如下：

- **開機分數**：以從開啟電源到登入的時間為基礎。 我們會查看每部裝置的上次開機時間 (不包括更新階段)，然後將其從 0 (不佳) 到 100 (絕佳) 進行評分。 這些分數是用來提供整體租用戶開機分數的平均值。
- **登入分數**：以從輸入認證到使用者可以存取回應式桌面的時間為準 (表示桌面已轉譯，而且 CPU 使用量至少已連續 2 秒皆降低到 50% 以下)。 我們會查看每部裝置的上次登入時間 (不包括首次登入或功能更新後立即登入的時間)，然後將其從 0 (不佳) 到 100 (絕佳) 進行評分。 這些分數是用來提供整體租用戶開機分數的平均值。

[![端點分析啟動效能頁面](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>深入資訊

[啟動效能] 頁面也會提供 [見解與建議] 的優先順序清單，如下列各節所述：

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a> 硬碟機

[啟動效能] 提供開機磁碟機為硬碟的裝置數目見解。 硬碟通常會導致開機時間比固態硬碟長三到四倍。 我們也會報告您透過使用固態硬碟將獲得之預期的啟動效能改善。

按一下以查看具有硬碟機的裝置清單。 建議的動作是將這些裝置升級為固態硬碟。

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a> 群組原則

啟動效能提供因群組原則造成開機延遲以及登入時間延遲的裝置數目見解。 按一下會帶您前往 [裝置] 檢視。 此檢視會依群組原則時間排序，因此您可以查看受影響的裝置，以進行進一步的疑難排解。

如果您按一下特定裝置，您可以看到其開機與登入歷程記錄。 歷程記錄可協助您判斷問題是否為迴歸問題，以及可能發生的時間。

雖然有許多文章說明如何將群組原則效能最佳化，但您仍可選擇移轉到雲端管理。 移轉到雲端管理可讓您使用 [Intune 安全性基準](https://docs.microsoft.com/intune/protect/security-baselines)與即將發行的原則分析工具。

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a> 開機與登入時間緩慢

[啟動效能] 提供開機或登入時間緩慢的裝置數目見解。 開機分數或登入分數為 "0" 表示速度緩慢。 按一下會帶您前往 [裝置] 檢視。 裝置會分別依照核心開機時間或核心登入時間排序，因此您可以查看受影響的裝置，以進行進一步的疑難排解。

如果您按一下特定裝置，您可以看到其開機與登入歷程記錄。 歷程記錄可協助您判斷問題是否為迴歸問題，以及可能發生的時間。

### <a name="reporting-tabs"></a>報表索引標籤

[啟動效能] 頁面具有可為見解提供支援的 [報表] 索引標籤，包括：
1. [型號效能]。 此索引標籤可讓您依裝置型號查看開機與登入效能，有助於您識別效能問題是否僅限於特定型號。
1. [裝置效能]。 此索引標籤提供所有裝置的開機與登入計量。 您可以依特定計量 (例如 GP 登入時間) 排序，以查看哪些裝置的該計量分數最差，以協助進行疑難排解。 您也可以依名稱搜尋裝置。 如果您按一下裝置，便可以看到其開機與登入歷程，有助於您識別是否有最近的迴歸
1. [啟動處理序]。 啟動處理序可能會增加使用者必須等候桌面回應的時間，而對使用者體驗造成負面影響。 此索引標籤 (若有顯示；因為我們仍在開發這項功能，所以我們只會對某些人員發行小眾測試版) 會顯示哪些處理序正在影響登入「回應式桌面的時間」階段；這會將桌面轉譯後的 CPU 維持在 50% 以上。 此表格只會在租用戶中列出影響最少 10 部裝置的處理序。  

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a> 主動式補救

主動式補救是指令碼套件，可以在使用者意識到問題之前，在使用者裝置上偵測並修正常見的支援問題。 這些補救有助於減少支援通話。 您可以建立自己的指令碼套件，或部署我們已撰寫並在環境中使用的其中一個指令碼套件，以減少支援票證。

每個指令碼套件都是由偵測指令碼、補救指令碼與中繼資料所組成的。 透過 Intune，您將能夠部署這些指令碼套件，並查看其有效性相關報告。 我們正在積極開發新的指令碼套件，並希望了解您使用這些套件的體驗。 如果對指令碼套件有任何意見反應，請與端點分析預覽連絡人聯繫。

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a> 取得偵測與補救指令碼

1. 從此文章底部的 [PowerShell 指令碼](#bkmk_uea_ps_scripts)一節複製指令碼。
    - 名稱開頭為 `det` 的指令檔是偵測指令碼。 補救指令碼以 `rem` 開頭。
    - 如需指令碼的說明，請參閱[指令碼描述](#bkmk_uea_scripts)。
1. 使用所提供的名稱來儲存每個指令碼。 名稱也會出現在每個指令碼頂端的註解中。
    - 您可以使用不同的指令碼名稱，但它不符合[指令碼描述](#bkmk_uea_scripts)一節中所列的名稱。


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a> 部署及監視指令碼
**Microsoft Intune 管理延伸模組**服務會從 Intune 取得指令碼並加以執行。 這些指令碼會每隔 24 小時重新執行一次。 若要部署和監視指令碼，請遵循下列指示進行：

1. 移至主控台中的 [主動式補救] 節點。
1. 按一下 [建立指令碼套件] 按鈕以建立指令碼套件。
     [![端點分析主動式補救頁面。選取 [建立] 連結。](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. 在 [基本] 步驟中，為指令碼套件提供**名稱**與 (選擇性) **描述**。 [發行者] 欄位可以編輯，但預設為您的租用戶名稱。 [版本] 無法編輯。 
1. 在 [設定] 步驟中，將文字從您下載的指令碼中複製到 [偵測指令碼] 與 [補救指令碼] 欄位。 
   - 您需要在相同的套件中有對應的偵測與補救指令碼。 例如，`Detect_stale_Group_Policies.ps1` 偵測指令碼會對應 `Remediate_stale_GroupPolicies.ps1` 補救指令碼。
       [![端點分析主動式補救指令碼設定頁面。](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. 使用下列建議設定完成 [設定] 頁面上的選項：
   - **使用登入認證執行此指令碼**：這取決於指令碼。 如需詳細資訊，請參閱[指令碼描述](#bkmk_uea_scripts)。
   - **強制執行指令碼簽章檢查**：否
   - **在 64 位元的 PowerShell 中執行指令碼**：否
1. 按一下 [下一步]，然後指派所需的任何 [範圍標籤]。
1. 在 [指派] 步驟中，選取您要部署指令碼套件的裝置群組。
1. 完成部署的 [檢閱 + 建立] 步驟。
1. 在 [報告] > [端點分析 - 主動式補救] 下，可看到偵測與補救狀態的概觀。
       [![端點分析主動式補救報表，概觀頁面。](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. 按一下 [裝置狀態] 以取得部署中每部裝置的狀態詳細資料。
       [![端點分析主動式補救裝置狀態。](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a> 端點分析設定

在 [設定] 頁面中，您可以選取 [一般] 或 [基準]。 以下將針對每個設定進行說明：

### <a name="general"></a><a name="bkmk_uea_gen"></a> 一般

[設定] 中的 [一般] 頁面可讓您查看是否已啟用 Intune 啟動效能資料收集。 當您按一下 [開始] 以啟用使用者體驗分析時，預設會自動為所有裝置啟用此功能。 您可以選擇移至 Intune 資料收集原則節點，以變更收集開機和登入記錄的裝置集合。


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a> Intune 資料收集原則

若要將此設定指派給裝置的子集，請[建立設定檔](/intune/configuration/device-profile-create#create-the-profile)，並提供下列資訊： 

  - **名稱**：輸入設定檔的描述性名稱，例如 **Intune 資料收集原則**
   
  - **描述**：輸入設定檔的描述。 這是選擇性設定，但建議執行。
    
  - **平台**：選取 [Windows 10 及更新版本]
   
  - **設定檔類型**：選取 [Windows 健全狀況監視]
   
  - 進行這些 [設定]：
   
       - [健全狀況監視]：選取 [啟用] 以從 Windows 10 裝置收集事件資訊
    
    - **範圍**：選取 [開機效能] 

  - 使用[範圍標籤](/intune/configuration/device-profile-create#scope-tags)和[適用性規則](/intune/configuration/device-profile-create#applicability-rules)，將設定檔篩選到符合特定準則的特定 IT 群組或群組裝置。

> [!NOTE]
> 有一個預留位置，用於提供設定 Configuration Manager 資料連接器的指示。 不過，此功能尚未在此初始個人預覽版中實作。

  [![端點分析一般設定頁面](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a> 基準管理

您可以透過設定基準，將目前的分數和子分數與其他分數進行比較。

1. **商業中位數**的內建基準可讓您將您的分數與一般企業進行比較。
1. 您可以根據目前的計量來建立新的基準，以便追蹤進度或檢視一段時間內的迴歸。 按一下 [建立新的] 按鈕，並提供新的基準名稱。 我們建議使用包含日期的名稱，以便在報告頁面的下拉式清單中可以更輕鬆地選取。
1. 每個租用戶的限制為 100 個基準。 您可以刪除不再需要的舊基準。
1. 如果您目前的計量低於報告中的目前基準，則將會標示為紅色並顯示為已迴歸。 因為計量每天波動是完全正常的，因此您可以設定一個迴歸閾值，預設為 10%。 使用此閾值時，系統只會在計量的迴歸超過 10% 時才將其標示為已迴歸。

   [![端點分析基準設定頁面](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a> 疑難排解

可使用下列各節來協助針對可能會遇到的問題進行疑難排解。

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a> 針對啟動效能裝置註冊進行疑難排解

如果 [概觀] 頁面顯示的啟動效能分數為零，並附帶顯示其正在等候資料的橫幅，或啟動效能的 [裝置效能] 索引標籤所顯示裝置數目比預期少，則可採取一些步驟來針對問題進行疑難排解。

首先，以下簡短概述啟動效能資料的收集限制：
1. 裝置必須為 Windows 10 1903 版或更新版本。
2. 裝置必須加入 Azure AD。 目前不支援加入工作場所網路的裝置，但會主動調查將此功能新增至 Windows 的可行性。
3. 裝置必須是 Windows 10 企業版。 目前不支援 Windows 10 家用版與專業版，但會主動調查將此功能新增至 Windows 的可行性。

請注意，這些限制不會套用到來自即將推出之 Configuration Manager 連接器的資料；無論版本或目錄設定為何，該連接器都可從任何 Configuration Manager 用戶端電腦收集資料。

其次，以下是要進行疑難排解的快速檢查清單：
1. 請確定 Windows 健全狀況監控設定檔是以您想要其效能資料的所有裝置為目標。 您可從端點分析 [設定] 頁面中找到此設定檔的連結，也可以像任何其他 Intune 設定檔一樣巡覽到此設定檔。 查看 [指派] 索引標籤，確定該設定檔已指派給預期的裝置集合。 
1. 查看哪些裝置已成功設定資料收集。 您也可以在設定檔的 [概觀] 頁面中看到這項資訊。  
   - 其中有一個已知問題，客戶可能會看到設定檔指派錯誤：受影響的裝置會顯示錯誤碼 `-2016281112 (Remediation failed)`。 我們正積極調查此問題。
1. 已成功設定資料收集的裝置必須在啟用資料收集之後重新開機，最多必須等到 24 小時之後，裝置才會顯示在 [裝置效能] 索引標籤中。
1. 如果裝置已成功設定資料收集，隨後已重新開機，但 24 小時之後仍未看到該裝置，則可能是裝置無法連接到收集端點。 如果公司使用 Proxy 伺服器，但尚未在 Proxy 中啟用端點，則可能會發生此問題。 如需詳細資訊，請參閱[針對端點進行疑難排解](#bkmk_uea_endpoints)。


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a> 端點

若要將裝置註冊到端點分析，則其必須將必要的功能資料傳送給 Microsoft。 若您的環境使用 Proxy 伺服器，請使用此資訊協助設定 Proxy。

若要啟用功能資料共用，請設定您的 Proxy 伺服器，以允許下列端點：

> [!Important]  
> 針對隱私權與資料完整性，Windows 會在與必要的功能資料共用端點通訊時檢查 Microsoft SSL 憑證 (憑證關聯)。 無法進行 SSL 攔截和檢查。 若要使用端點分析，請從 SSL 檢查中排除這些端點。<!-- BUG 4647542 -->

| 端點  | 函式  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | 用於將[所需的功能資料](#bkmk_uea_datacollection)傳送至 Intune 資料收集端點。 |
| `https://graph.windows.net` | 用來在將階層附加到端點分析 (於 Configuration Manager 伺服器角色上)  時，自動擷取設定。 如需詳細資訊，請參閱[為站台系統伺服器設定 Proxy](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://*.manage.microsoft.com` | 用來將裝置集合和裝置與端點分析同步 (僅限於 Configuration Manager 伺服器角色)。 如需詳細資訊，請參閱[為站台系統伺服器設定 Proxy](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |


### <a name="proxy-server-authentication"></a>Proxy 伺服器驗證

如果組織使用 Proxy 伺服器驗證來存取網際網路，請確定其不會因為驗證而封鎖資料。 如果您的 Proxy 不允許裝置傳送這項資料，裝置就不會顯示在電腦分析中。

#### <a name="bypass-recommended"></a>略過 (建議)

設定您的 Proxy 伺服器，使其不會向目標為資料共用端點的流量要求 Proxy 驗證。 此選項是最全面的解決方案。 適用於所有 Windows 10 版本。  

#### <a name="user-proxy-authentication"></a>使用者 Proxy 驗證

設定裝置，以使用登入使用者的內容進行 Proxy 驗證。 此方法需要下列設定：

- 裝置具有受支援 Windows 版本的最新品質更新

- 在 Windows 設定的 [網路與網際網路] 群組中的 [Proxy 設定] 內，設定使用者層級 Proxy (WinINET Proxy)。 您也可以使用舊版的 [網際網路選項] 控制台。

- 確認使用者具備連線到資料共用端點的 Proxy 權限。 此選項需要裝置具備擁有 Proxy 權限的主控台使用者，因此您無法搭配無周邊裝置使用此方法。

> [!IMPORTANT]
> 使用者 Proxy 驗證方法與使用 Microsoft Defender 進階威脅防護不相容。 此行為是因為此驗證依賴將 **DisableEnterpriseAuthProxy** 登錄機碼設為 `0`，但 Microsoft Defender ATP 需要將其設為 `1`。 如需詳細資訊，請參閱[在 Microsoft Defender ATP 中設定電腦 Proxy 及網際網路連線能力設定](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)。

#### <a name="device-proxy-authentication"></a>裝置 Proxy 驗證

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

- 設定 Proxy 伺服器，以允許 Active Directory 中的電腦帳戶存取資料端點。 此設定需要 Proxy 伺服器支援 Windows 整合式驗證。  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a> 常見問題集

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>如果我將 Intune 租用戶移至不同的租用戶位置，我的端點分析資料是否會移轉？

如果您將 Intune 租用戶移轉至不同的位置，則在移轉時，您的端點分析解決方案中的所有資料都會遺失。 由於端點會持續向端點分析回報，因此，假設裝置保持正確註冊，則移轉後發生的所有事件都會自動上傳到新的租用戶位置，而且報告會開始重新匯入。 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>為什麼指令碼結束並傳回 1 的代碼？

指令碼結束並傳回 1 的代碼，以通知 Intune 應該進行補救。 在此情況下，結束偵測指令碼並傳回 1，表示需要進行補救。 許多只在 CM 中執行的指令碼套件可能會顯示為符合規範，但會結束並傳回 1 的代碼。 在這些指令碼中，結束並傳回 1 的代碼並不會有任何意義，但您可能會想要驗證裝置是否可以正確補救。

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>為什麼更新過時的群組原則指令碼會傳回錯誤 0x87D00321？

0x87D00321 是指令碼執行逾時錯誤。 此錯誤通常會發生在遠端連線的電腦上。 可能的緩和措施是僅部署到具有內部網路連線能力的動態電腦集合。

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a> 指令碼描述

此表格顯示指令碼名稱、描述、偵測、補救與可設定的項目。 名稱開頭為 `Detect` 的指令檔是偵測指令碼。 補救指令碼以 `Remediate` 開頭。 您可以從此文章的下一節複製這些指令碼。

|指令碼名稱|說明|
|---|---|
|**更新過時的群組原則** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| 偵測上次群組原則重新整理是否超過 `7 days`。  </br>變更偵測指令碼中 `$numDays` 的值，以自訂 7 天的閾值。 </br></br>執行 `gpupdate /target:computer /force` 與 `gpupdate /target:user /force` 來補救  </br> </br>可協助減少透過群組原則傳遞憑證與設定時與網路連線相關的支援通話。 </br> </br> **使用登入認證執行指令碼**：是|
|**重新啟動 Office 隨選即用服務** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| 偵測隨選即用服務是否設定為自動啟動，以及服務是否已停止。 </br> </br> 將服務設定為自動啟動，並啟動服務 (如果其已停止) 來補救。 </br></br> 協助修正 Win32 Microsoft 365 Apps 企業版因隨選即用服務已停止而無法啟動的問題。 </br> </br> **使用登入認證執行指令碼**：否|
|**檢查網路憑證** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|在電腦或使用者的個人存放區中偵測由 CA 簽發且已過期或即將過期的憑證。 </br> 變更偵測指令碼中 `$strMatch` 的值來指定 CA。 為 `$expiringDays` 指定 0 以尋找已過期的憑證，或指定其他天數來尋找即將過期的憑證。  </br></br>向使用者提出快顯通知以進行補救。 </br> 使用您想要讓使用者看到的訊息標題和文字來指定 `$Title` 與 `$msgText` 值。 </br> </br> 通知使用者可能需要更新的已過期憑證。 </br> </br> **使用登入認證執行指令碼**：否|
|**清除過時的憑證** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| 在目前使用者的個人存放區中偵測由 CA 簽發且已過期的憑證。 </br> 變更偵測指令碼中 `$certCN` 的值來指定 CA。 </br> </br> 從目前使用者的個人存放區中刪除由 CA 簽發且已過期的憑證來補救。 </br> 變更補救指令碼中 `$certCN` 的值來指定 CA。 </br> </br> 從目前使用者的個人存放區中尋找並刪除由 CA 簽發且已過期的憑證。 </br> </br> **使用登入認證執行指令碼**：是|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a> PowerShell 指令碼

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a> 端點分析資料隱私權

### <a name="data-flow"></a>資料流程

下圖顯示必要的功能資料如何從個別裝置透過我們的資料服務、暫時性儲存體流向您的租用戶。 資料會透過我們的現有企業管線流動，而不需依賴 Windows 診斷資料。

[![使用者體驗資料流程圖](media/dataflow.png)](media/dataflow.png#lightbox)

1. 為已註冊的裝置設定 **Intune 資料收集**原則。 根據預設，當**啟動**端點分析時，系統會將此原則指派給「所有裝置」。 但是，您可以隨時[將指派變更](#bkmk_uea_set)為裝置的子集，或不指派給任何裝置。

2. 裝置會傳送必要的功能資料。

    - 針對已指派原則的 Intune 裝置，資料會從 Intune 管理延伸模組進行傳送。 如需詳細資訊，請參閱[需求](#bkmk_uea_prereq)。
    - 針對 Configuration Manager 受控裝置，資料也可以透過 ConfigMgr 連接器流向 Microsoft 端點管理。 ConfigMgr 連接器已連接雲端。 它只需要 Intune 租用戶的連線，而不是開啟共同管理。

> [!Note]  
> 在開機期間，會產生計算裝置啟動分數所需的資料。 視電源設定和使用者行為而定，在正確指派原則給裝置後，可能需要數星期的時間才會在管理主控台上顯示啟動分數。  

3. Microsoft 端點管理服務會處理每部裝置的資料，並使用 MS Graph API 在管理主控台中發佈個別裝置和組織彙總的結果。

端對端的平均延遲大約是 12 小時，且會受到執行每日處理所花費的時間影響。 資料流程的所有其他部分全都近乎即時。

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>資料收集

目前，端點分析的基本功能會針對落入[識別](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data)與[匿名化](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data)類別的開機效能記錄，收集與其建立關聯的資訊。 隨著我們持續新增額外的功能，收集的資料將視需要而有所不同。 目前正在收集的主要資料點：

#### <a name="identified-data"></a>識別資料

- 硬體清查資訊
  - **make:** 裝置製造商
  - **model:** 裝置型號
  - **deviceClass:** 裝置分類。 例如，桌上型電腦、伺服器或行動裝置。
  - **Country:** 裝置區域設定
- 應用程式清查，如
  - **name:** Windows
  - **ver:** 目前作業系統的版本。
  
#### <a name="pseudonymized-data"></a>匿名化資料

- 診斷、效能及使用方式資料繫結至使用者及/或裝置
  - **logOnId**
  - **bootId:** 系統開機識別碼
  - **coreBootTimeInMilliseconds:** 核心開機的時間
  - **totalBootTimeInMilliseconds:** 總開機時間
  - **updateTimeInMilliseconds:** 完成 OS 更新的時間
  - **gpLogonDurationInMilliseconds**:處理群組原則的時間
  - **desktopShownDurationInMilliseconds:** 桌上型電腦 (explorer.exe) 的載入時間
  - **desktopUsableDurationInMilliseconds:** 到可使用桌上型電腦 (explorer.exe) 的時間
  - **topProcesses:** 資料開機時載入的處理緒清單，包含名稱、CPU 使用量狀態和應用程式詳細資料 (名稱、發行者、版本)。 例如 *{\"ProcessName\":\"svchost\"、\"CpuUsage\":43、\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\"、\"ProductName\":\"Microsoft&reg; Windows&reg; 作業系統\"、\"發行者\":\"Microsoft Corporation\"、\"ProductVersion\":\"10.0.18362.1\"}*
- 裝置資料未繫結至裝置或使用者 (如果此資料繫結至裝置或使用者，Intune 會將它識別為資料)
  - **ID：** Windows Update 使用的唯一裝置識別碼
  - **localId:** 裝置的本機定義唯一識別碼。 這不是人員可讀取的裝置名稱。 最有可能會等於儲存在 HKLM\Software\Microsoft\SQMClient\MachineId 的值。
  - **aaddeviceid:** Azure Active Directory 裝置識別碼
  - **orgId:** 代表 Microsoft O365 租用戶的唯一 GUID
  
> [!Important]  
> 我們的資料處理原則如 [Microsoft Intune 隱私權聲明](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement) \(英文\) 所述。 我們只會使用客戶資料來提供您已註冊的服務。 如上線程序的程序中所述，我們會匿名並彙總所有已註冊組織的分數，以將基準保持在最新狀態。


### <a name="resources"></a>資源

如需相關隱私權層面的詳細資訊，請參閱下列文章：

- [Microsoft Intune 隱私權聲明](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement) \(英文\)
- [Windows 10 與隱私權合規性](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licensing terms and documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) (授權條款與文件)  
- [Microsoft Azure 資料中心的安全性和隱私權](https://azure.microsoft.com/global-infrastructure/)  
- [對受信任雲端充滿信心](https://azure.microsoft.com/overview/trusted-cloud/)  
- [信任中心](https://www.microsoft.com/trustcenter)  
