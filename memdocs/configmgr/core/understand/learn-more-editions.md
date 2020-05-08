---
title: 授權與分支
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 可用安裝選項的授權需求
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906056"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Configuration Manager 的授權和分支

適用於：*Configuration Manager (最新分支) 和 System Center Configuration Manager (長期維護分支)*

請使用此文章深入了解 Configuration Manager 的安裝選項授權需求。 這些安裝選項包括下列分支：

- 最新分支
- 長期維護分支 (LTSB)
- 最新分支的評估安裝
- Technical Preview 分支

## <a name="licensing-overview"></a>授權概觀

如果客戶具有 Configuration Manager 授權的作用中軟體保證 (SA) 或自 2016 年 10 月 1 日起的對等訂閱權限，即有權使用 2016 年 10 月發行的 Configuration Manager 1606 版。 如果客戶具有自 2016 年 10 月 1 日起的 Configuration Manager 權限，則在安裝時會發現最新分支和長期維護分支 (LTSB) 這兩個授權選項。

如需您透過 Microsoft 大量授權方案購買之產品的完整條款及條件，請參閱[授權條款與文件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1) \(英文\)。


## <a name="licensed-branches"></a>授權的分支

此文章參考了「軟體保證」合約或對等訂閱權限。 此 Microsoft 授權合約授與安裝及使用 Configuration Manager 的權限。

### <a name="current-branch"></a>最新分支

最新分支要求您必須有有效的「軟體保證」合約或 Configuration Manager 的對等權限。 如需詳細資訊，請參閱[軟體保證和最新分支](#software-assurance-and-the-current-branch)。

此分支支援在想要從 Microsoft 接收定期品質和功能更新的生產環境中使用。 它提供對所有功能和增強功能的存取權。

從 1710 版開始，每個更新版本自其正式運作發行日起都會提供為期 18 個月的支援。 如需詳細資訊，請參閱 [Configuration Manager 最新分支版本的支援](../servers/manage/current-branch-versions-supported.md)。

### <a name="long-term-servicing-branch-ltsb"></a>長期維護分支 (LTSB)

LTSB 要求您必須有 2016 年 10 月 1 日之後與 Microsoft 簽訂的最新軟體保證合約。 如需詳細資訊，請參閱[軟體保證和 LTSB](#software-assurance-and-the-ltsb)。

此分支支援在生產環境中使用。 適用於軟體保證 (SA) 或對等 Configuration Manager 訂閱權限已於 2016 年 10 月 1 日之後到期的客戶。 相較於最新分支，此分支有所限制。

此分支可獲得 Configuration Manager 的重大安全性更新，但無法使用任何新功能。

### <a name="evaluation-installation-of-the-current-branch"></a>最新分支的評估安裝

評估版本不需要與 Microsoft 簽訂「軟體保證」合約。 [評估安裝](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)一律是指最新分支，而且您可以使用它們 180 天。

您可以將評估安裝升級為最新分支的完整安裝。 您無法將評估安裝升級為長期維護分支。

### <a name="technical-preview-branch"></a>Technical Preview 分支

[Technical Preview 分支](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)已可供使用。 此分支是 Configuration Manager 的受限組建，可讓您試用新的功能。 您可以使用不同媒體來安裝 Technical Preview 而不是授權版本。 如需詳細資訊，請參閱 [Technical Preview](../get-started/technical-preview.md)。


## <a name="software-assurance-agreements"></a>軟體保證合約

您可以安裝並使用的分支是由 2016 年 10 月 1 日起，您所擁有的 Configuration Manager 授權軟體保證狀態或對等訂閱權限決定。

### <a name="software-assurance-and-the-current-branch"></a>軟體保證和最新分支

下列項目可提供 Configuration Manager 最新分支的使用權限：

- **System Center：** 如果使用者有 System Center 的標準或資料中心授權，即可安裝並使用 Configuration Manager 的最新分支選項。

- **System Center Configuration Manager：** 如果客戶有 Configuration Manager 授權的有效 SA 或對等訂閱權限，即可安裝並使用 Configuration Manager 的最新分支選項。

如果您有自 2016 年 10 月 1 日起的 Configuration Manager 授權有效 SA 或對等訂閱權限：

- 您可以安裝並使用最新分支。
- 如果您可接受 SA 或訂閱失效，則必須解除安裝最新分支。

### <a name="software-assurance-and-the-ltsb"></a>軟體保證和 LTSB

如果您有自 2016 年 10 月 1 日起的 Configuration Manager 授權有效 SA 或對等訂閱權限：

- 您可以安裝並使用 LTSB。 如果客戶有 Configuration Manager 的永久權限，或可接受 SA 或訂閱失效，則可在失效當下安裝 Configuration Manager LTSB 版。

LTSB 是以最新分支 1606 版為基礎，並具有下列限制：

- 不支援將最新分支轉換為 LTSB。 如果您目前有最新分支站台，則必須將 LTSB 安裝為新的站台。  

- LTSB 並非完全支援最新分支的所有功能。 如需詳細資訊，請參閱[長期維護分支簡介](introduction-to-the-ltsb.md)。 這些限制包括有限的功能集、有限升級選項，以及個別的產品支援生命週期。  

### <a name="software-assurance-expiration-date"></a>軟體保證到期日

從 Configuration Manager 的 1606 版 2016 年 10 月版基準媒體開始，您可以指定軟體保證合約的到期日。 [軟體保證到期日]  選用值，以方便提醒。 當您執行 Configuration Manager 安裝程式，或稍後從 Configuration Manager 主控台內執行時新增此值。

> [!NOTE]
> Microsoft 不會驗證您指定的到期日，也不會將這個日期用於授權驗證。 請將它作為到期日的提醒。 當 Configuration Manager 定期檢查線上提供的新軟體更新時，此值非常有用。 您的軟體保證授權狀態應該是最新的，以便您有資格使用其他更新。

#### <a name="to-specify-the-software-assurance-expiration-date"></a>指定軟體保證到期日

- 當您從 Configuration Manager 媒體執行安裝程式時，可以在 [安裝精靈] 的 [產品金鑰]  頁面上指定值。

- 在 Configuration Manager 主控台的 [階層設定]  中，請在 [授權]  索引標籤上指定值。


## <a name="licensing-resources"></a>授權資源

若要深入了解產品授權詳細資料，請使用下列資源。

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft 大量授權服務中心 (VLSC)

- [VLSC 的概觀](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Microsoft 大量授權產品條款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- 大量授權客戶可以從[大量授權服務中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx)取得其授權摘要。 移至 [授權]  功能表，然後選取 [授權摘要]  。

### <a name="vlsc-videos"></a>VLSC 影片

- 如需 VLSC 運作方式的訓練影片，請前往 [Microsoft 大量授權服務中心訓練和資源](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources)，然後選取 [示範影片]  。

- [查詢有效軟體保證合約的位置](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) \(從影片 43 秒開始\)  

- [如何取得 VLSC 的權限](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4)。 您可以將 VLSC 讀取和寫入權限委派給組織中的其他人。
