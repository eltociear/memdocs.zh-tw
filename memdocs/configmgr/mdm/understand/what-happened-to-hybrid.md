---
title: 混合式 MDM 有哪些改變？
titleSuffix: Configuration Manager
description: 瞭解 Configuration Manager 中的混合式行動裝置管理（MDM）淘汰
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724652"
---
# <a name="what-happened-to-hybrid-mdm"></a>混合式 MDM 有哪些改變？

適用於：  Configuration Manager (最新分支)

> [!WARNING]
> Microsoft 已于2019年9月1日淘汰混合式 MDM 服務供應專案。 任何剩餘的混合式 MDM 裝置將不會收到原則、應用程式或安全性更新。

## <a name="remove-hybrid-mdm"></a>移除混合式 MDM

如果您的 Configuration Manager 站台具有 Microsoft Intune 訂閱，則必須予以移除。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [雲端服務]****，然後選取 [Microsoft Intune 訂閱]**** 節點。 請刪除您現有的「Intune 訂閱」。

1. 在 [**移除 Microsoft Intune 訂**用帳戶] 中，選取 [**從 Configuration Manager 移除 Microsoft Intune 訂用**帳戶] 選項，然後按 **[下一步]**。

1. 完成精靈。

## <a name="deprecation-announcement"></a>淘汰公告

下列注意事項是原始的淘汰公告：

> [!NOTE]  
> 自 2018 年 8 月 14 日起，混合式行動裝置管理是[已被取代的功能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。 從 1902 Intune 服務版本開始，預計在 2019 年 2 月底，新客戶將無法建立新的混合式連線。
> <!--Intune feature 2683117-->  
> 自一年多前推出 Azure 起，Intune 已新增數百個由客戶提出要求且市場頂尖的新服務功能。 它現在提供的功能比透過混合式行動裝置管理 (MDM) 所提供的還要多更多。 「Azure 上的 Intune」可為您的企業行動性需求，提供更具整合性的簡化系統管理體驗。
>
> 因此，與混合式 MDM 相比，大多數客戶都優先選擇「Azure 上的 Intune」。 隨著越來越多客戶移轉至雲端，使用混合式 MDM 的客戶數目也持續減少。 因此，在 2019 年 9 月 1 日，Microsoft 將淘汰混合式 MDM 服務供應項目。
>
> 這項變更並不會影響內部部署的 Configuration Manager 或 [Windows 10 裝置的共同管理](../../comanage/overview.md)。 如果您不確定是否使用混合式 MDM，請移至 Configuration Manager 主控台的 [系統**管理**] 工作區，展開 [**雲端服務**]，然後選取 [ **Microsoft Intune**訂用帳戶]。 如果您有已設定的 Microsoft Intune 訂閱，即表示您的租用戶已針對混合式 MDM 進行設定。
>
> **此變更對我造成什麼影響？**
>
> - Microsoft 到明年仍將支援您的混合式 MDM 使用。 此功能將繼續收到主要的 Bug 修正。 Microsoft 將在新的 OS 版本上支援現有的功能，例如 iOS 12 上的註冊。 將不提供任何混合式 MDM 新功能。  
>
> - 如果您在混合式 MDM 供應項目結束之前移轉至「Azure 上的 Intune」，則對使用者應該沒有任何影響。  
>
> - 到了 2019 年 9 月 1 日，所有剩餘的混合式 MDM 裝置將不再收到原則、應用程式或安全性更新。  
>
> - 授權將維持不變。 混合式 MDM 隨附「Azure 上的 Intune」授權。  
>
> - Configuration Manager 中的內部部署 MDM 功能不會被取代。 從 Configuration Manager 版本1810開始，您可以使用內部部署 MDM，而不需要 Intune 連線。 如需詳細資訊，請參閱[新的內部部署 MDM 部署已不再需要 Intune](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm)連線。
>
> - Configuration Manager 的內部部署條件式存取功能也會隨著混合式 MDM 而被取代。 如果您在 Configuration Manager 用戶端所管理的裝置上使用條件式存取，請先確定它們受到保護，再進行遷移。
>     1. 在 Azure 中設定條件式存取原則
>     2. 在 Intune 入口網站中設定相容性原則
>     3. 完成混合式遷移，並將 MDM 授權單位設定為 Intune
>     4. 啟用共同管理
>     5. 將相容性原則共同管理工作負載移至 Intune
>
>     如需詳細資訊，請參閱[搭配共同管理的條件式存取](../../comanage/quickstart-conditional-access.md)。
>
> **我需要為這項變更做什麼準備？**
>
> - 開始從 ConfigMgr 主控台進行將 MDM 移轉至 Azure 的規劃。 許多客戶 (包括 Microsoft IT) 都已經歷這個過程。 如需詳細資訊，請參閱這份 [Microsoft 案例研究](https://aka.ms/Intune_MSFT) \(英文\)。  
>
> - 請與您的記錄可查夥伴 FastTrack 連絡以取得協助。 [適用於 Microsoft 365 的 FastTrack](https://aka.ms/hybrid_fasttrack)可協助您從混合式 MDM 移轉至「Azure 上的 Intune」。
>
> 如需詳細資訊，請參閱[Intune 支援的 blog 文章](https://aka.ms/hybrid_notification)。

## <a name="next-steps"></a>後續步驟

如需管理 MDM 裝置所支援功能的詳細資訊，請參閱下列文章：

- [什麼是 Microsoft Intune？](https://docs.microsoft.com/intune/what-is-intune)
- [什麼是內部部署 MDM？](manage-mobile-devices-with-on-premises-infrastructure.md)
- [使用 Exchange 管理裝置](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
