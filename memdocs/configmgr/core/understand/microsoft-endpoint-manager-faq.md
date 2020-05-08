---
title: Microsoft Endpoint Configuration Manager 常見問題集
titleSuffix: Configuration Manager
description: Microsoft Endpoint Configuration Manager 的相關常見問題集
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f6c7321301e5705c4188012ba53b50f4c37b57
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906024"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Microsoft Endpoint Configuration Manager 常見問題集

適用於：*Configuration Manager (最新分支、Technical Preview 分支)*

從 1910 版開始，Configuration Manager 現在是 Microsoft 端點管理員的一部分。 本文提供常見問題的解答。

## <a name="summary"></a>[摘要]

首先，請觀看下列由 Microsoft 公司副總裁 Brad Anderson 針對 Microsoft 365 提供的兩分鐘影片：

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>常見問題集

### <a name="what-is-microsoft-endpoint-manager"></a>什麼是 Microsoft 端點管理員？

Microsoft Endpoint Manager 是一個整合的解決方案，可用於管理您的所有裝置。 Microsoft 將 Configuration Manager 和 Intune 整合成簡化的授權。 繼續運用現有的 Configuration Manager 投資，同時以自有步調來利用 Microsoft 雲端的強大功能。

下列 Microsoft 管理解決方案全都是 **Microsoft Endpoint Manager** 品牌的一部分：

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [電腦分析](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [裝置管理系統管理員主控台](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)中的其他功能

如需詳細資訊，請參閱 Brad Anderson (Microsoft 公司副總裁) 所張貼有關 Microsoft 365 的下列文章：

- [公告部落格文章](https://aka.ms/cmannounce)
- [願景文章](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Microsoft 端點管理員隨附的 Configuration Manager 有何變更？

在 1910 版中，除了名稱變更之外，Configuration Manager 的運作方式仍然相同。

最值得注意的是，[Configuration Manager 主控台](../servers/manage/admin-console.md#bkmk_open)和[軟體中心](software-center.md#bkmk_open) 等通用元件的 [開始] 功能表資料夾名稱已變更。

### <a name="how-do-we-refer-to-the-product-now"></a>現在如何參考此產品？

- 參考包含所有元件的整個解決方案時：**Microsoft 端點管理員**

- 參考內部部署元件時：
  - 第一次參考時，請使用完整的品牌名稱：**Microsoft Endpoint Configuration Manager**
  - 一般使用：**Configuration Manager**
  - 空間有限時使用：**ConfigMgr**，僅在一般使用名稱不適合的情況下使用

### <a name="are-there-any-licensing-changes"></a>是否有任何授權變更？

可以！ 如 Microsoft Ignite 2019 所宣告，如果有 Configuration Manager 的授權，則您現在也會獲得[共同管理](../../comanage/overview.md) Windows 電腦的 Intune 授權。 如需詳細資訊，請參閱[產品與授權常見問題集](product-and-licensing-faq.md#bkmk_mem)。

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>為什麼我在某些地方還是會看到 "System Center Configuration Manager"？

在所有產品、服務和支援資料 (例如文件) 之間進行變更需要一些時間。

也有一些基本元件可能永遠不會變更。 站台伺服器上的主要 Windows 服務仍然是 **SMS_Executive**。 支援此文件的 GitHub 存放庫會繼續是 **SCCMDocs**。

## <a name="next-steps"></a>後續步驟

了解 [Configuration Manager 累加版本的新功能](../plan-design/changes/whats-new-incremental-versions.md)。
