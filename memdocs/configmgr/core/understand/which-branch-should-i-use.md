---
title: 應該使用哪個分支
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 可用分支之間的差異。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 542069b82ea4c68a48ccc47b79007fd2fa25322a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906018"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>我應該使用哪個 Configuration Manager 分支？

適用於：*Configuration Manager (最新分支和 Technical Preview 分支) 和 System Center Configuration Manager (長期維護分支)*

Configuration Manager 有三個可用分支：

- 最新分支
- 長期維護分支
- Technical Preview 分支

請使用本文以協助您選擇正確的分支。

> [!TIP]  
> 同一個階層中的所有站台必須執行相同的分支。 不支援在不同站台具有不同分支的階層。

## <a name="current-branch"></a>最新分支

這個分支是生產環境中使用的授權分支。 使用這個分支可取得最新特色和功能。 如果您有下列其中一個授權，則可以使用這個分支：  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- 對等訂閱權限  

如需軟體保證和授權選項的詳細資訊，請參閱 [Configuration Manager 的授權和分支](learn-more-editions.md)，以及 [Configuration Manager 分支和授權常見問題集](product-and-licensing-faq.md)。

Microsoft 計劃每年發行幾次 Configuration Manager 最新分支的更新。 每個更新版本自其正式運作 (GA) 發行日起提供為期 18 個月的支援。 在整個支援期間均提供技術支援。 不過，我們的支援結構是動態的，並根據最新分支版本的可用性分成兩個不同服務階段。 如需詳細資訊，請參閱 [Configuration Manager 最新分支版本的支援](../servers/manage/current-branch-versions-supported.md)。 較新版本的更新會提供為主控台內更新。

若要將最新分支安裝為新站台，請使用[基準媒體](../servers/manage/updates.md#bkmk_Baselines)。 您也可以使用基準媒體從 System Center 2012 Configuration Manager Service Pack 2 或 System Center 2012 R2 Configuration Manager Service Pack 1 升級。 您組織授權 Configuration Manager 的方式會決定對此媒體的存取權。

您也可以使用基準媒體來安裝新站台，它會是最新分支評估版。 評估版並不需要授權。 您可以使用評估版 180 天。 它支援升級為最新分支授權版。 若只要安裝評估版，請從 [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) 加以取得。

> [!NOTE]
> 使用基準媒體安裝新 Configuration Manager 階層的站台。 如果先前已安裝基準版本，請使用主控台內更新將站台更新為新的版本。  
>
> 使用主控台內更新所更新的站台，會產生和使用基準媒體安裝的新站台一樣的站台。
>
> 如需詳細資訊，請參閱 [Configuration Manager 的更新](../servers/manage/updates.md)。  

### <a name="features-of-the-current-branch"></a>最新分支的功能

- 收到啟用新功能的[主控台內更新](../servers/manage/install-in-console-updates.md)。
- 收到提供現有功能安全性及品質修正程式的主控台內更新。
- 必要時支援頻外更新。 如需詳細資訊，請參閱[使用更新註冊工具](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)或[使用 Hotfix 安裝程式](../servers/manage/use-the-hotfix-installer-to-install-updates.md)。
- 與雲端式服務整合。
- 支援與其他 Configuration Manager 安裝彼此間互相[移轉資料](../migration/migrate-data-between-hierarchies.md)。
- 支援從舊版 Configuration Manager 升級。
- 支援安裝為評估版，未來可從此版升級為完整授權版安裝。

Microsoft 建議您一旦發行最新版，即立刻更新至此新版。 您有 18 個月的時間可以更新為較新版本。 您也可以略過更新逕行安裝最新的可用版本。 因為每個版本都會累積，如果您略過更新而安裝最新版本，仍然可以從舊版存取所有功能和改善。

如需詳細資訊，請參閱[最新分支版本支援](../servers/manage/current-branch-versions-supported.md)。

### <a name="current-branch-update-options"></a>最新分支更新選項

- 利用使用中的軟體保證，您可以安裝最新分支版本的主控台內更新。  
- 沒有任何選項可將最新分支轉換成 Technical Preview 分支。 Technical Preview 分支是不需要授權的個別安裝。
- 沒有任何選項可將最新分支轉換成長期維護分支 (LTSB)。 您必須解除安裝最新分支，再將 LTSB 安裝為新安裝。

## <a name="long-term-servicing-branch"></a>長期維護分支

這個分支是 Configuration Manager 客戶實際執行時使用的授權分支，這些客戶使用最新分支，且其 Configuration Manager 軟體保證 (SA) 或對等訂閱權限在 2016 年 10 月 1 日後才到期。 如需軟體保證和授權選項的詳細資訊，請參閱 [Configuration Manager 的授權和分支](learn-more-editions.md)，以及 [Configuration Manager 分支和授權常見問題集](product-and-licensing-faq.md)。

LTSB 是以 1606 版為基礎。 這個分支不會收到提供新功能或更新現有功能的主控台內更新。 但會提供重要的安全性修正程式。 若要安裝 LTSB，您必須使用 System Center 2016 隨附的 1606 版[基準媒體](../servers/manage/updates.md#bkmk_Baselines)。 較新的基準版本不支援安裝 LTSB。

若要將 LTSB 安裝為新站台，或從支援的 System Center 2012 Configuration Manager 站台升級 LTSB，請使用 System Center 2016 隨附的 1606 版[基準媒體](../servers/manage/updates.md#bkmk_Baselines)。 您可以使用基準媒體來安裝執行 1606 版最新分支的新站台，或執行長期維護分支的新站台。

> [!TIP]  
> 若要了解 System Center 2016，請參閱 [System Center 2016](https://docs.microsoft.com/system-center/index) 文件。 這份文件也會告訴您如何取得 System Center 2016，但需要 microsoft 軟體授權合約或類似的權限。  
>  
> 若要在大量授權服務中心 (VLSC) 中尋找 Configuration Manager 1606 版，請前往 [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) 的 [下載和金鑰]  索引標籤，並搜尋 `System Center 2016`，然後選取 **System Center 2016 Datacenter** 或 **System Center 2016 Standard**。  
>  
> 您也可以從 [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview) 下載 System Center 2016 評估版。  

### <a name="features-of-the-ltsb"></a>LTSB 的功能

- 收到提供重要安全性修正程式的主控台內更新。
- 當 Configuration Manager 的 SA 合約或對等權限過期時，提供安裝選項。
- 當您有 Configuration Manager 的目前 SA 合約或對等權限時，支援升級 (轉換) 至最新分支。

### <a name="ltsb-limitations"></a>LTSB 限制

LTSB 是以最新分支 1606 版為基礎，並具有下列限制：

- LTSB 在正式運作後 (2016 年 10 月) 會提供 10 年的重大安全性更新支援，過後此分支的支援即到期。 如需技術支援週期的詳細資訊，請參閱 [Microsoft 週期原則](https://support.microsoft.com/lifecycle)。
- 支援一組有限的伺服器和用戶端作業系統及相關技術 (如 SQL Server 版本) 清單。 如需詳細資訊，請參閱[支援的長期維護分支設定](supported-configurations-for-ltsb.md)。
- 不會收到新功能的更新
- 不支援下列功能：
  - 共同管理和電腦分析等雲端連結功能
  - 內部部署 MDM
  - Windows 10 服務儀表板、服務方案或 Windows 10 半年通道
  - Windows 10 LTSB 和 Windows Server 的未來版本
  - Asset Intelligence
  - 任何發行前版本功能

### <a name="ltsb-update-options"></a>LTSB 更新選項

- 您可以將 LTSB 安裝轉換成最新分支安裝。 支援在 LTSB 支援到期前後轉換為最新分支。

  若要轉換，您必須擁有使用中的 Microsoft 軟體保證協議。 如需詳細資訊，請參閱下列文章：

  - [將長期維護分支升級至最新分支](convert-to-current-branch.md)
  - [Configuration Manager 的授權和分支](learn-more-editions.md)
  - [基準和更新版本](../servers/manage/updates.md#bkmk_Baselines)

- 沒有任何選項可將 LTSB 轉換成 Technical Preview 分支。 Technical Preview 分支是不需要授權的個別安裝。

- 您無法將最新分支的評估版升級為 LTSB 安裝。

## <a name="technical-preview-branch"></a>Technical Preview 分支

Technical Preview 分支適用於實驗室環境。 了解並試用開發中的 Configuration Manager 最新功能。 它在生產環境中不受支援，也不需要有軟體保證授權合約。

若要安裝執行 Technical Preview 分支的新站台，請使用最新版 [Technical Preview 分支的基準媒體](../get-started/technical-preview.md#bkmk_install)。 安裝 Technical Preview 分支之後，每個月都有新版的主控台內更新。

### <a name="features-of-the-technical-preview-branch"></a>Technical Preview 分支的功能

- 以最新分支的最新基準版本為基礎
- 收到將安裝更新為最新版 Technical Preview 分支的主控台內更新
- Microsoft 希望您能對隨附的開發中新功能提供意見反應
- 收到僅適用於 Technical Preview 分支的更新

### <a name="technical-preview-limitations"></a>Technical Preview 限制

- [支援是有限的](../get-started/technical-preview.md#bkmk_reqs)，包括只有一部主要站台及最多 10 個用戶端。  
- 您無法將其升級或移轉到最新分支或 LTSB 安裝。
- 不支援下列行為：
  - 使用移轉將資料匯入或匯出至另一個 Configuration Manager 安裝
  - 從舊版 Configuration Manager 升級
  - 安裝成評估版

Technical Preview 分支首度推出的功能，通常會在之後的更新中新增至最新分支。 每個新的 Technical Preview 分支版本都包含舊版 Technical Preview 分支的功能，即使這些功能已新增至最新分支。

如需詳細資訊，請參閱 [Configuration Manager Technical Preview](../get-started/technical-preview.md)。

### <a name="technical-preview-update-options"></a>Technical Preview 更新選項

- 您可以安裝新版 Technical Preview 分支的任何主控台內更新。

- 沒有任何選項可將 Technical Preview 分支轉換成最新分支或 LTSB。

## <a name="identify-your-version-and-branch"></a>識別您的版本和分支

### <a name="version"></a>版本

若要檢查站台的版本，請在主控台中，移至主控台左上角的 [關於 Configuration Manager]  。 此對話方塊會顯示 [站台版本]  。 如需站台版本清單，請參閱[基準和更新版本](../servers/manage/updates.md#bkmk_Baselines)。

### <a name="branch"></a>分支

若要確認站台的分支，請移至主控台的 [系統管理]   > [站台設定]   > [站台]  ，並開啟 [階層設定]  。 如果其中具有可以轉換為最新分支的作用中選項，即表示站台執行 LTSB 版本。 當站台執行最新分支時，主控台會停用此選項。

如需 Configuration Manager 不同版本的詳細資訊，請參閱[基準和更新版本](../servers/manage/updates.md#bkmk_Baselines)。
