---
title: 已淘汰的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 不再支援的功能。
ms.date: 05/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 40eda7184d7be5010bf51e3ac0d30d6d9442203c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905069"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>已移除且淘汰的 Configuration Manager 功能

適用於：  Configuration Manager (最新分支)

本文列出已從 Configuration Manager 支援淘汰或移除的功能。 未來更新中將會移除已淘汰的功能。 這些未來變更可能會影響 Configuration Manager 的使用。  

這項資訊會隨著未來版本而有所變更。 它可能不會包含每項已淘汰的 Configuration Manager 功能。

## <a name="deprecated-features"></a>已淘汰的功能

下列是已淘汰的功能。 您現在仍然可以使用，但 Microsoft 打算在未來結束支援。

|功能|首次宣布的淘汰項目|移除的&nbsp;支援|
|-----------|---|--------------|
| [桌面分析] 選項，可**檢視裝置註冊與安全性更新的最近資料**。<!-- 7080949 --> 如需詳細資訊，請參閱[資料延遲](../../../../desktop-analytics/troubleshooting.md#data-latency)。|2020 年 5 月|2020 年 7 月|
|從 Azure 共用內容的實作已經變更。 使用內容啟用雲端管理閘道。 未來您將無法建立傳統雲端發佈點。|2019 年 2 月|TBD<sup>[備註 1](#bkmk_note1)</sup>|
|Azure 的傳統服務部署，用於雲端管理閘道和雲端發佈點。 如需詳細資訊，請參閱[規劃 CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)。|2018 年 11 月|TBD<sup>[備註 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> 附註 1：TBD 移除的支援

即將決定 (TBD) 的特定時間範圍。 Microsoft 建議您變更為新的處理序或功能，但您可以在不久的將來繼續使用已淘汰處理序或功能。

## <a name="unsupported-and-removed-features"></a>不受支援和移除的功能

不再支援下列功能。 在某些情況下，它們已不再存在於產品中。

|功能|首次宣布的淘汰項目|移除的&nbsp;支援|  
|-----------|---|--------------|  
| Windows Analytics 與更新整備小幫手整合。 如需詳細資訊，請參閱 [KB 4521815：Windows Analytics 於 2020 年 1 月 31 日淘汰](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。 | 2019 年 10 月 14 日 | 2020 年 1 月 31 日 |
| 用於條件式存取合規性政策的裝置健康情況證明評定 <!--1235616 aka 3608202--> 如需詳細資訊，請參閱[混合式 MDM 有哪些改變？](../../../../mdm/understand/what-happened-to-hybrid.md)。| 2019 年 7 月 3 日 | 1910 版 |
| Configuration Manager 公司入口網站應用程式 | 2019 年 5 月 21 日 | 1910 版 |
| 應用程式類別目錄，包括兩個網站系統角色：應用程式類別目錄網站點與 Web 服務點。 如需詳細資訊，請參閱[移除應用程式類別目錄](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)。 | 2019 年 5 月 21 日 | 1910 版 |
|搭配 Configuration Manager 中 Windows Hello 企業版設定的憑證式驗證<br>如需詳細資訊，請參閱 [Windows Hello 企業版設定](../../../../protect/deploy-use/windows-hello-for-business-settings.md)。|2017 年 12 月|1910 版|
|System Center Endpoint Protection for Mac<br>如需詳細資訊，請參閱[支援終止部落格文章](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257)。|2018 年 10 月|2018 年 12 月 31 日|
|內部部署條件式存取<br>如需詳細資訊，請參閱[混合式 MDM 有哪些改變？](../../../../mdm/understand/what-happened-to-hybrid.md)。|2019 年 1 月 30 日|2019 年 9 月 1 日|
|混合式行動裝置管理 (MDM)<br>如需詳細資訊，請參閱[混合式 MDM 有哪些改變？](../../../../mdm/understand/what-happened-to-hybrid.md)。<br><br>從 1902 Intune 服務版本開始，預計在 2019 年 2 月底，新客戶將無法建立新的混合式連線。<!--Intune feature 2683117-->|2018 年 8 月 14 日|2019 年 9 月 1 日|
|安全性內容自動化通訊協定 (SCAP) 延伸模組。 <!--3607889--><br>先前的認證版本仍可在 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=48741)取得。|2018 年 9 月|1810 版|
|不再支援應用程式類別目錄網站點的 **Silverlight 使用者體驗**。 使用者應該使用新的軟體中心。 如需詳細資訊，請參閱[設定軟體中心](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)。<!--1358309-->|2017 年 8 月 11 日| 1806 版|
|舊版軟體中心。<br><br>如需新軟體中心的詳細資訊，請參閱[規劃和設定應用程式管理](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex)。|2016 年 12 月 13 日|1802 版|
|使用 Configuration Manager 管理虛擬硬碟 (VHD)。 <br><br>此取代包括移除建立新 VHD 或是使用工作序列管理 VHD 的選項，以及從 Configuration Manager 主控台移除虛擬硬碟節點。 <br><br>不會刪除現有的 VHD，但也無法再從 Configuration Manager 主控台中存取它。  |2017 年 1 月 6 日 |1710 版|
|工作順序： <br /> - 將磁碟轉換成動態磁碟 <br /> - 安裝部署工具 |2016 年 11 月 18 日|1710 版|
|升級評估工具<br><br>「升級評估工具」同時依賴 Configuration Manager 與應用程式相容性工具組 (ACT) 6.x。 ACT 的最終版本隨附於 Windows 10 v1511 ADK。 由於 ACT 已不會有任何進一步的更新，因此會中止升級評估工具的支援。 取代注意事項已於 2016 年 9 月 12 日新增至 [UAT 下載頁面](https://www.microsoft.com/software-download/windows10)。 | 2016 年 9 月 12 日  | 2017 年 7 月 11 日 |
|具有網路負載平衡 (NLB) 叢集的軟體更新點 | 2016 年 2 月 27 日 | 版本 1702 |
|工作順序： <br /> - OSDPreserveDriveLetter  <br /><br /> 在作業系統部署期間，Windows 安裝程式現在預設會決定要使用的最佳磁碟機代號 (通常是 C:)。 如果您想要指定使用不同的磁碟機，您可以在「套用作業系統」工作順序步驟中變更位置。 移至 [請選取要套用此作業系統的位置]  設定。 選取 [特定邏輯磁碟機代號]  並選擇您想要使用的磁碟機。 |2016 年 6 月 20日 |1606 版 |
|網路存取保護 (NAP) - 自 System Center 2012 Configuration Manager 起提供|2015 年 7 月 10 日|版本 1511|  
|頻外管理 - 自 System Center 2012 Configuration Manager 起提供|2015 年 10 月 16 日|版本 1511|

### <a name="features-removed-in-version-1511"></a>版本 1511 中移除的功能

下列各節包含從版本 1511 移除之功能的其他詳細資料：

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> 超出訊號範圍管理  

Configuration Manager 已從 Configuration Manager 主控台內移除 AMT 型電腦的原生支援。  

- 當您使用 [Configuration Manager 的 Intel SCS 附加元件](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)時，AMT 型電腦仍會完全受控。 附加元件可讓您存取管理 AMT 的最新功能，同時移除 Configuration Manager 併入那些變更之前所引入的限制。  

- 這項變更不會影響 System Center 2012 Configuration Manager 中的頻外管理。  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> 網路存取保護

Configuration Manager 已移除對網路存取保護的支援。 此功能在 Windows Server 2012 R2 中已淘汰，且已從 Windows 10 移除。  

如需了解網路存取保護的替代方案，請參閱 [網路原則與存取服務概觀](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)) 中的 *淘汰的功能*一節。

## <a name="see-also"></a>請參閱

- [已移除和已取代](removed-and-deprecated.md)
- [Microsoft 支援週期](https://support.microsoft.com/lifecycle)
- [System Center Configuration Manager 最新分支版本支援](../../../servers/manage/current-branch-versions-supported.md)
