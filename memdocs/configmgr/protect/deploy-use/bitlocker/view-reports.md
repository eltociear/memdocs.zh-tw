---
title: 檢視 BitLocker 報告
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的 BitLocker 管理報告
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d10717f980922e1f6d1fca9224e288b4df709da2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699616"
---
# <a name="view-bitlocker-reports"></a>檢視 BitLocker 報告

適用於：  Configuration Manager (最新分支)

<!--3601034-->

在 Reporting Services 點上[安裝報告](setup-websites.md)之後，您可以檢視報告。 這些報告會顯示企業和個別裝置的 BitLocker 合規性。 其提供表格式資訊與圖表，並包含能以不同角度檢視資料的篩選器。

在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [報告]  ，然後選取 [報告]  節點。 下列報告位於 [BitLocker 管理]  類別中：

- [BitLocker 電腦合規性](#bkmk-compliancereport)

- [BitLocker Enterprise 合規性儀表板](#bkmk-dashboard)

- [BitLocker Enterprise 合規性詳細資料](#bkmk-compliancedetails)

- [BitLocker Enterprise 合規性摘要](#bkmk-compliancesummary)

- [修復稽核報告](#bkmk-audit)

您可以直接從 Reporting Services 點網站存取所有的這類報告。

> [!NOTE]
> 若要讓這些報告顯示完整的資料：
>
> - 建立 BitLocker 管理原則，並將其部署至裝置集合
> - 目標集合中的用戶端必須傳送硬體清查

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a> BitLocker 電腦合規性

請使用這種報告來收集電腦的特定資訊。 其中提供關於 OS 磁碟機和任何固定資料磁碟機的詳細加密資訊。 若要檢視每個磁碟機的詳細資料，請展開 [電腦名稱] 項目。 其亦指出套用到電腦上每種磁碟機類型的原則。

[![BitLocker 電腦符合性報告的 範例螢幕擷取畫面](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

您也可以使用這份報告來判斷遺失或遭竊的電腦最後已知的 BitLocker 加密狀態。 Configuration Manager 會根據您所部署的 BitLocker 原則來判斷裝置的合規性。 在嘗試判斷裝置的 BitLocker 加密狀態之前，請先確認您已為其部署的原則。

> [!NOTE]
> 此報告不會顯示卸除式資料磁碟區的加密狀態。

### <a name="computer-details"></a>電腦詳細資料

|資料行名稱|說明|
|----------------|----|
|電腦名稱|使用者指定的 DNS 電腦名稱。|
|網域名稱|電腦的完整網域名稱。|
|電腦類型|電腦的類型，有效的類型為**非可攜式**和**可攜式**。|
|作業系統|電腦的 OS 類型。|
|整體相容性|電腦的整體 BitLocker 合規性狀態。 有效的狀態是 [符合規範]  和 [不符合規範]  。 [每個磁碟機的合規性狀態](#bkmk_volume)可能會指出不同的合規性狀態。 不過，此欄位會根據指定的原則，顯示該合規性狀態。|
|作業系統合規性|電腦上 OS 的合規性狀態。 有效的狀態是 [符合規範]  和 [不符合規範]  。|
|固定資料磁碟機合規性|電腦上固定資料磁碟機的合規性狀態。 有效的狀態是 [符合規範]  和 [不符合規範]  。|
|上次更新日期|電腦上次連線到伺服器以報告合規性狀態的日期和時間。|
|豁免|指出使用者已豁免或未豁免 BitLocker 原則。|
|已豁免使用者|已豁免 BitLocker 原則的使用者。|
|豁免日期|獲得豁免的日期。|
|合規性狀態詳細資料|與根據所指定原則判斷電腦合規性狀態相關的錯誤和狀態訊息。|
|原則：加密強度|您在 BitLocker 管理原則中選取的密碼強度。|
|原則：作業系統磁碟機|指出 OS 磁碟機是否需要加密，並指出適當的保護裝置類型。|
|原則：固定資料磁碟機|指出固定資料磁碟機是否需要加密。|
|製造商|電腦製造商名稱 (與電腦 BIOS 顯示的名稱相同)。|
|型號|電腦製造商型號名稱 (與電腦 BIOS 顯示的名稱相同)。|
|裝置使用者|電腦上的已知使用者。|

### <a name="computer-volume"></a><a name="bkmk_volume"></a> 電腦磁碟區

|資料行名稱|說明|
|----------------|----|
|磁碟機代號|電腦上的磁碟機代號。|
|磁碟機類型|磁碟機的類型。 有效值是 [作業系統磁碟機]  和 [固定資料磁碟機]  。 這些項目是實體磁碟機，不是邏輯磁碟區。|
|加密強度|您在 BitLocker 管理原則中選取的密碼強度。|
|保護裝置類型|您在原則中選取用以加密磁碟機的保護裝置類型。 OS 磁碟機的有效保護裝置類型為 **TPM** 或 **TPM+PIN**。 固定資料磁碟機的有效保護裝置類型則為 [密碼]  。|
|保護裝置狀態|指出電腦是否已啟用原則中指定的保護裝置類型。 有效的狀態是 [開啟]  或 [關閉]  。|
|加密狀態|磁碟機的加密狀態。 有效的狀態為 [已加密]  、[未加密]  或 [正在加密]  。|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a> BitLocker Enterprise 合規性儀表板

此報告提供下列圖表，以顯示組織內部的 BitLocker 合規性狀態：

- 合規性狀態分佈

- 不符合規範 - 錯誤分佈

- 合規性狀態分佈 (依磁碟機類型)

[![BitLocker 企業符合性儀表板的 範例螢幕擷取畫面](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>合規性狀態分佈

這個圓形圖會顯示組織內電腦的合規性狀態。 其亦會顯示具有該合規性狀態的電腦佔所選集合中電腦總數的百分比。 另外也會顯示具有每種狀態的實際電腦數目。

此圓形圖會顯示下列合規性狀態：

- 符合標準

- 不相容

- 使用者豁免

- 暫時使用者豁免

- 原則未強制執行

- 不明。 這些電腦已回報狀態錯誤，或其屬於集合的一部分，但從未回報其合規性狀態。 如果電腦與組織中斷連線，則可能發生缺少合規性狀態的情況。

### <a name="non-compliant---errors-distribution"></a>不符合規範 - 錯誤分佈

此圓形圖會顯示您的組織中不符合 BitLocker 磁碟機加密原則的電腦類別。 此外也會顯示每個類別的電腦數目。 報告會從集合中不符合規範的電腦總數計算出每個類別的百分比。

- 使用者已延遲加密

- 找不到相容的 TPM

- 系統磁碟分割無法使用或不夠大

- TPM 可見但未初始化

- 原則衝突

- 等待 TPM 自動佈建

- 發生未知的錯誤

- 沒有資訊。 這些電腦未安裝 BitLocker 管理代理程式，或是已安裝但未啟用。 例如，服務無法運作。

### <a name="compliance-status-distribution-by-drive-type"></a>合規性狀態分佈 (依磁碟機類型)

這個橫條圖會依磁碟機類型顯示目前的 BitLocker 合規性狀態。 狀態包括 [符合規範]  和 [不符合規範]  。 顯示的橫條代表固定資料磁碟機和 OS 磁碟機。 報告中包含沒有固定資料磁碟機的電腦，且只會顯示 [作業系統磁碟機]  橫條中的值。 此圖表不包含已豁免 BitLocker 磁碟機加密原則的使用者或「沒有原則」類別。

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a> BitLocker Enterprise 合規性詳細資料

此報告會針對已部署 BitLocker 管理原則的電腦集合，顯示您整個組織的整體 BitLocker 合規性相關資訊。

[![BitLocker Enterprise 合規性詳細資料的範例螢幕擷取畫面](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|欄名|說明|
|--- |--- |
|受控電腦|已部署 BitLocker 管理原則的電腦數目。|
|% 符合規範|組織中符合規範的電腦百分比。|
|% 不符合規範|組織中不符合規範的電腦百分比。|
|% 不明的合規性|合規性狀態不明的電腦百分比。|
|% 豁免|已豁免 BitLocker 加密需求的電腦百分比。|
|% 非豁免|未豁免 BitLocker 加密需求的電腦百分比。|
|符合標準|組織中符合規範的電腦計數。|
|不符合規範|組織中不符合規範的電腦計數。|
|不明的合規性|合規性狀態不明的電腦計數。|
|豁免|已豁免 BitLocker 加密需求的電腦計數。|
|非豁免|未豁免 BitLocker 加密需求的電腦計數。|

### <a name="computer-details"></a>電腦詳細資料

|欄名|說明|
|--- |--- |
|電腦名稱|受控裝置的 DNS 電腦名稱。|
|網域名稱|電腦的完整網域名稱。|
|合規性狀態|電腦的整體合規性狀態。 有效的狀態是 [符合規範]  和 [不符合規範]  。|
|豁免|指出使用者已豁免或未豁免 BitLocker 原則。|
|裝置使用者|裝置的使用者。|
|合規性狀態詳細資料|與根據所指定原則判斷電腦合規性狀態相關的錯誤和狀態訊息。|
|上次連絡|電腦上次連線到伺服器以報告合規性狀態的日期和時間。|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a> BitLocker Enterprise 合規性摘要

使用此報告可顯示您整個組織的整體 BitLocker 合規性。 此外也會顯示已部署 BitLocker 管理原則之個別電腦的合規性。

[![BitLocker 企業符合性摘要的 範例螢幕擷取畫面](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|欄名|說明|
|--- |--- |
|受控電腦|使用 BitLocker 原則進行管理的電腦數目。|
|% 符合規範|組織中符合規範的電腦百分比。|
|% 不符合規範|組織中不符合規範的電腦百分比。|
|% 不明的合規性|合規性狀態不明的電腦百分比。|
|% 豁免|已豁免 BitLocker 加密需求的電腦百分比。|
|% 非豁免|未豁免 BitLocker 加密需求的電腦百分比。|
|符合標準|組織中符合規範的電腦計數。|
|不相容|組織中不符合規範的電腦計數。|
|不明的合規性|合規性狀態不明的電腦計數。|
|豁免|已豁免 BitLocker 加密需求的電腦計數。|
|非豁免|未豁免 BitLocker 加密需求的電腦計數。|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a> 修復稽核報告

> [!NOTE]
> 您也可以從 [BitLocker 管理和監視網站](helpdesk-portal.md#reports)取得此報告。
>
> 若要在 Configuration Manager 主控台中檢視此報告，請移至 [監視]  工作區。 在瀏覽窗格中，展開 [報告]  節點，展開 [報告]  ，然後展開 [BitLocker 管理]  資料夾。 選取報告的當地語系化版本的子資料夾，例如 **en-us**。

請使用這種報告來稽核要求存取 BitLocker 修復金鑰的使用者。 您可以根據下列準則進行篩選：

- 特定類型的使用者，例如技術支援使用者或終端使用者
- 如果要求失敗或成功
- 要求的特定金鑰類型：修復金鑰密碼、修復金鑰識別碼或 TPM 密碼雜湊
- 執行擷取的日期範圍

[![BitLocker 修復審核報告的 範例螢幕擷取畫面](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|資料行名稱|說明|
|----------------|----|
|要求日期和時間|終端使用者或技術支援使用者要求金鑰的日期和時間。|
|稽核要求來源|產生要求的來源網站。 有效的值為**自助入口網站**或**技術支援**。|
|要求結果|要求的狀態。 有效的值為**成功**或**失敗**。|
|技術支援使用者|要求金鑰的管理使用者。 如果技術支援管理員在未指定使用者名稱的情況下復原金鑰，則 [終端使用者]  欄位將會空白。 標準技術支援使用者必須指定使用者名稱 (會出現在此欄位中)。 透過自助入口網站進行復原時，此欄位和 [終端使用者]  欄位會顯示提出要求的使用者名稱。|
|終端使用者|要求金鑰擷取的使用者名稱。|
|電腦|已修復的電腦名稱。|
|金鑰類型|使用者要求的金鑰類型。 三種類型的金鑰為：<br/><br/>- **修復金鑰密碼**：用於以修復模式來修復電腦<br/>- **修復金鑰識別碼**：用於代表其他使用者以修復模式來修復電腦<br/>- **TPM 密碼雜湊**：用於修復 TPM 鎖定的電腦|
|原因描述|使用者要求指定金鑰類型的原因，視其在表單中選取的選項而定。|
