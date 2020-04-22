---
title: 電源管理的建議
titleSuffix: Configuration Manager
description: 了解 Microsoft 對 Configuration Manager 電源管理的建議。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696626"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>了解 Configuration Manager 電源管理的建議

適用於：  Configuration Manager (最新分支)

了解下列對 Configuration Manager 電源管理的建議。  

## <a name="monitor-at-a-representative-time"></a>代表性時間的監視

電源管理的監視階段可向您提供組織中電腦的下列資訊：

- 耗電量
- 活動
- 電源管理功能
- 環境衝擊

選擇監視裝置的代表性時間。 例如，國定假日期間之監視不能提供電腦耗電量的實際報告。

## <a name="create-a-control-collection"></a>建立控制項集合

建立兩個電腦集合，協助您監視將電源計劃套用至電腦的效果。 第一個集合應該包含您想要套用電源設定的大部分電腦。 「控制項集合」  應該包含其餘的電腦。 將必要的電源管理計劃套用至第一個集合。 然後執行報告，比較兩個集合受到的衝擊。  

## <a name="run-reports-before-you-apply-a-plan"></a>先執行報表再套用計劃

請先執行 [電源設定]  報告，再將電源管理計劃套用至電腦集合。 使用此報告有利於了解已對集合中電腦設定的電源管理設定。 如果您將新的電源管理設定套用至電腦卻未先檢查現有設定，這可能會增加耗電量。  

## <a name="exclude-servers"></a>排除伺服器

不支援執行 Windows Server 的電腦電源管理。 將伺服器新增至集合，但將它排除在電源管理外。  

> [!NOTE]
> 雖然 Configuration Manager 不支援 Windows Server 的電源管理，但仍會收集電源使用量資料以供分析和報告。

## <a name="exclude-other-computers"></a>排除其他電腦

如有不想使用電源管理來管理的電腦，請將這些電腦新增至排除集合。  

您可能想要將下列類型的電腦排除在電源管理之外：

- 必須保持開啟的電腦。  

- 使用者需要遠端連線的電腦。  

- 無法使用電源管理的電腦。  

- 具有發佈點站台系統角色的電腦。  

- 公用電腦，例如 kiosk 電腦、資訊顯示器，或其電腦與監視器必須一直開啟的監視主控台。  

如需詳細資訊，請參閱[設定電源管理](configuring-power-management.md)。  

## <a name="apply-power-plans-to-a-test-collection"></a>將電源計劃套用至測試集合

一律測試對測試電腦集合套用電源管理計劃的效果，再將電源計劃套用至較大的電腦集合。  

當您將電腦排除在電源管理外時，所有的電源設定都會還原成其原始值。 您無法將個別的電源設定還原為其原始值。  

## <a name="apply-power-plan-settings-individually"></a>個別套用電源計劃設定

先監視套用每種電源設定的效果，再套用下一種。 此程序可確保每種設定都能達到所需效果。 如需電源計劃設定的詳細資訊，請參閱[可用的電源管理計劃設定](create-and-apply-power-plans.md#BKMK_Plans)。  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>定期監視電腦是否有多個電源計劃

電源管理包括一份報告，其會顯示套用多項電源計劃的電腦：**具有多項電源計劃的電腦**。

如果電腦是多個集合的成員，且每個集合都套用不同的電源計劃，則會套用下列行為：  

- **電源計劃**：如果您在電腦上套用多個電源設定的值，則電腦會使用限制最鬆散的值。  

- **喚醒時間**：如果您在桌上型電腦套用多個喚醒時間，則電腦會使用最接近午夜的時間。  

如需詳細資訊，請參閱[具有多項電源計劃的電腦](monitor-and-plan-for-power-management.md#BKMK_Multiple)。  

## <a name="save-or-export-power-management-information"></a>儲存或匯出電源管理資訊

當您在監視和合規性階段執行報告時，請儲存或匯出結果。 為免 Configuration Manager 稍後會移除資料，請保留資料以供稍後比較。  

Configuration Manager 會將下列電源管理資訊保留在網站資料庫中：

- 每日報告所使用的電源管理資訊：31 天

- 每月報告所使用的電源管理資訊：13 個月
