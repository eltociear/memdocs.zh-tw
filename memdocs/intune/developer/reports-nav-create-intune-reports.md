---
title: 使用 Intune 資料倉儲
titleSuffix: Microsoft Intune
description: 使用 Intune 資料倉儲來建置報表，以深入了解您的企業行動環境。
keywords: Intune 資料倉儲
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 57019B11-DF9B-4D8A-95FE-254C75398DDE
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 459b957137ff4a34e811b0662747450e213f6c19
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988544"
---
# <a name="use-the-microsoft-intune-data-warehouse"></a>使用 Microsoft Intune 資料倉儲

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

使用 Intune 資料倉儲來建置報表，以深入了解您的企業行動環境。 例如，某些報表包含：
- Intune 中使用者註冊趨勢，以最佳化授權採購
- 應用程式和 OS 版本分解，以檢閱行動裝置的狀態
- 註冊和裝置合規性趨勢，以順暢地轉出原則更新

## <a name="data-warehouse-benefits"></a>資料倉儲的優點

資料倉儲可讓您存取 Azure 入口網站以外之行動環境的詳細資訊。 您可以使用 Intune 資料倉儲存取：

- 歷程 Intune 資料
- 以每日步調重新整理的資料
- 使用 OData 標準的資料模型

> [!Note]
> 如果您是使用共同管理的行動裝置管理 (MDM) 搭配 Microsoft Endpoint Configuration Manager 與 Microsoft Intune，您需要從 Configuration Manager 擷取資料。 Intune 資料倉儲只包含 Intune 資料。 您可以針對自訂報表使用 Configuration Manager Power BI 儀表板。 如需詳細資訊，請參閱[宣佈適用於 Configuration Manager 的 Power BI 解決方案範本](https://powerbi.microsoft.com/blog/sccm-solution-template) \(英文\) 和[適用於 Dynamics 365 的 Power BI 內容](https://docs.microsoft.com/dynamics365/unified-operations/dev-itpro/analytics/power-bi-home-page) \(英文\)。

> [!Important]  
> 您現在可以藉由設定查詢參數  `api-version=v1.0` 來使用 Intune 資料倉儲 v1.0 版。 資料倉儲中對集合所進行的更新為附加性質，因此不會破壞現有的案例。<br><br>
> 您可以使用搶鮮版 (Beta) 來試用最新資料倉儲功能。 若要使用搶鮮版 (Beta)，URL 必須包含查詢參數  `api-version=beta`。 搶鮮版 (Beta) 能在功能被正式推出為支援的服務之前預先提供它們。 Intune 新增功能時，搶鮮版 (Beta) 可能會變更行為和資料合約。 與搶鮮版 (Beta) 相依的任何自訂程式碼或報告工具都可能會中斷進行中更新。

## <a name="next-steps"></a>後續步驟

- 取得連結，並使用 Power BI 深入了解。 如需指示，請參閱[使用 Power BI 連線至 Intune 資料倉儲](reports-proc-get-a-link-powerbi.md)。
- 使用您的連結，以 Power BI 建立自訂報表。 如需指示，請參閱[利用 Power BI 的 OData 摘要建立報表](reports-proc-create-with-odata.md)。
- 取得 Intune 資料倉儲 API、資料模型以及實體間之關聯性的詳細資訊<!-- , and an example of creating a custom client to retrieve data,--> 請參閱 [Intune 資料倉儲 API](reports-nav-intune-data-warehouse.md)。
