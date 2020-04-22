---
title: 發行前版本功能
titleSuffix: Configuration Manager
description: 發行前版本功能為最新分支中用來在生產環境中進行早期測試的功能。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703536"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager 的發行前版本功能

適用於：  Configuration Manager (最新分支)

發行前版本功能為最新分支中用來在生產環境中進行早期測試的功能。 這些功能全部受到支援，但仍在開發中。 它們在移出發行前版本類別目錄之前可能會一直變更。

## <a name="give-consent"></a>同意  

使用發行前版本功能之前，請同意使用發行前版本功能。 同意是每個階層的一次性動作，無法取消。 直到您同意之前，您無法啟用更新中包含的發行前版本功能。 在您開啟發行前版本功能之後，即無法關閉它。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 按一下功能區的 [階層設定]  。  

3. 在 [階層設定內容] 的 [一般]  索引標籤上，啓用選項以 [Consent to use Pre-Release features] \(同意使用發行前版本功能\)  。 按一下 [確定]  。  

## <a name="enable-pre-release-features"></a>啟用發行前版本功能

當您安裝包含發行前版本功能的更新時，[更新與服務精靈] 中會顯示這些功能和包含在更新中的一般功能。

### <a name="if-you-have-given-consent"></a>如果您已同意

請在 [更新與服務精靈] 中，啟用發行前版本功能。 選取發行前版本功能 (如同選取任何其他功能)。

或者，稍後從 [管理]  工作區 [更新與服務]  下的 [功能]  節點中，啟用發行前版本功能。 選取一項功能，然後按一下功能區中的 [開啟]  。 在您同意前，此選項都不提供使用。

### <a name="if-you-havent-given-consent"></a>如果您尚未同意

您可以在 [更新與服務精靈] 中看到發行前版本功能，但無法啟用。 安裝更新之後，這些功能就會出現在 [功能]  節點中。 不過，在您同意前都無法啟用它們。

> [!IMPORTANT]  
> 在多網站階層中，您只能從系統管理中心網站啟用選擇性或發行前版本的功能。 此行為可避免整個階層中不會發生衝突。 <!--507197-->  
>
> 如果您已在獨立主要站台表示同意，然後藉由安裝新的管理中心網站來擴充階層，則必須於管理中心網站再授權一次。  

當您啟用發行前功能時，Configuration Manager 階層管理員 (HMAN) 必須在該功能提供使用前，先處理變更。 變更通常要立即處理。 完成時間最多需要 30 分鐘，視 HMAN 處理週期而定。 處理完變更之後，請先重新啟動主控台，再使用功能。

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a> 發行前版本功能清單

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| 功能          | 已新增為發行前版本 | 已新增為完整功能 |
|------------------|----------------------|-------------------------|
| [協調流程群組](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | 2002 版 | ![尚未提供此服務](media/red_x.png) |
| [工作順序部署類型](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | 2002 版 | ![尚未提供此服務](media/red_x.png) |
| [移除管理中心網站](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | 2002 版 | ![尚未提供此服務](media/red_x.png) |
| [工作順序偵錯工具](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | 1906 版 | ![尚未提供此服務](media/red_x.png) |
| [ 應用程式群組](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | 1906 版 | ![尚未提供此服務](media/red_x.png) |
| [Azure Active Directory 使用者群組探索](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| 1906 版 | 2002 版 |
| [將集合成員資格結果同步至 Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| 1906 版| 2002 版 |
| [CMPivot 獨立](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | 1906 版 | 2002 版 |
| [SMS 提供者管理服務](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | 1810 版 | 1906 版 |
| [增強的 HTTP 站台系統](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | 1806 版 | 1810 版 |
| [共同管理裝置的用戶端應用程式](../../../comanage/workloads.md#client-apps) <br/> (之前稱為「用於共同受控裝置的行動應用程式」  ) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | 1806 版 | 2002 版 |
| [套件轉換管理員](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | 1806 版 | 1810 版 |
| [分階段部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | 1802 版 | 1806 版 |
| [Windows Defender 應用程式控制管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | 版本 1702 | 1906 版 |
| [服務叢集感知集合 (伺服器群組)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | 1602 版 | ![尚未提供此服務](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> 如需您必須先啟用的非發行前版本功能的詳細資訊，請參閱[從更新啟用選擇性功能](install-in-console-updates.md#bkmk_options)。  
>
> 如需僅在技術預覽分支提供之功能的詳細資訊，請參閱[技術預覽](../../get-started/technical-preview.md)。  
