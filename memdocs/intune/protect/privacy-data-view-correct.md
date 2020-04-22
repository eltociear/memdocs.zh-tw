---
title: 檢視及更正個人資料
titleSuffix: Microsoft Intune
description: 了解如何檢視及更正個人資料。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6cddd94400874c508a31b11b22fa4417798e2da
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084783"
---
# <a name="view-and-correct-personal-data"></a>檢視及更正個人資料

Intune 系統管理員可以根據其存取權限檢視某些個人資料，但只有終端使用者可以變更裝置的個人資料。

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>檢視個人資料

系統管理員可以看到 Intune UI 各種刀鋒視窗中的終端使用者個人資訊。 下列文章說明系統管理員有與沒有存取權的資訊：
- 在 Intune 中[查看裝置詳細資料](../remote-actions/device-inventory.md)說明如何檢閱終端使用者裝置的詳細資料。
- [監視應用程式資訊和指派](../apps/apps-monitor.md)說明如何查看終端使用者裝置上所安裝之應用程式的詳細資料。
- [當我註冊裝置時，我的公司可以看到哪些資訊？](https://docs.microsoft.com/mem/intune/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune)一文為終端使用者提供公司可以與無法看到的資料清單。 最好清楚告訴使用者要收集的資料種類，以及要收集的原因。 本文可以是該透明度的第一個步驟。

### <a name="who-can-view-the-data"></a>誰可以檢視資料？

Microsoft 會使用嚴格的控制來管理對客戶資料的存取、僅授與完成重要工作所需的最低層級存取權，以及在不再需要時撤銷存取權。 

您可以使用以角色為基礎的系統管理控制 (RBAC) 來保護和控制終端使用者的個人資料存取權。 如需詳細資訊，請參閱 [RBAC 搭配 Microsoft Intune](../fundamentals/role-based-access-control.md)。

您可以閱讀 Online Services 條款和 [Microsoft Online Services 隱私權聲明](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409)，進一步了解 Microsoft 資料做法。 

## <a name="correct-end-user-personal-data"></a>更正終端使用者的個人資料

系統管理員無法更新裝置或應用程式的特定資訊。 如果使用者要更正任何個人資料 (例如裝置名稱)，他們必須在其裝置上直接這樣做。 這類變更會在下次連線至 Intune 時同步。


## <a name="next-steps"></a>後續步驟

了解如何在 Intune 中[稽核、匯出或刪除](privacy-data-audit-export-delete.md)個人資料。
