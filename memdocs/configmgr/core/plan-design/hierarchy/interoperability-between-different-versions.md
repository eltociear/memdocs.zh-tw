---
title: 版本之間的互通性
titleSuffix: Configuration Manager
description: 了解如何避免在相同網路中的多個 Configuration Manager 階層之間產生衝突。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693516"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Configuration Manager 不同版本之間的互通性

適用於：  Configuration Manager (最新分支)

您可在相同網路上安裝及操作多個獨立的 Configuration Manager 階層。 不過，由於不同的 Configuration Manager 階層無法在移轉程序外互通，因此每個階層的設定都需要避免彼此之間發生衝突。 此外，您可以建立特定設定，幫助所管理的資源與正確階層的站台系統互動。  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a> 最新分支與舊版之間的互通性  

不同版本的站台不能共存於同一個 Configuration Manager 階層。 唯一的例外狀況是在下列升級案例的程序期間：

- 從 System Center 2012 Configuration Manager 至 Configuration Manager 最新分支
- 使用主控台內的更新從某一個 Configuration Manager 最新分支版本到較新版本

您可以部署與現有 System Center 2012 Configuration Manager 站台或階層並存的 Configuration Manager 最新分支站台和階層。 請規劃好以避免任一版本的用戶端嘗試加入至另一個版本的站台。

例如，如果兩個或更多個 Configuration Manager 階層有包含相同網路位置的[重疊界限](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries)，請將每個新的用戶端指派給特定站台，而不是使用自動站台指派。 如需詳細資訊，請參閱[如何將用戶端指派至站台](../../clients/deploy/assign-clients-to-a-site.md)。  

此外，若電腦已裝載 Configuration Manager 最新分支的站台系統角色，您將無法在其中安裝 System Center 2012 Configuration Manager 的用戶端。 您也無法在裝載 2012 Configuration Manager 站台系統角色的電腦上，安裝 Configuration Manager 最新分支用戶端。  

不支援下列用戶端和連線：  

- 任何 System Center 2012 Configuration Manager 或更早的電腦用戶端版本  

- 任何 System Center 2012 Configuration Manager 或更早的裝置管理用戶端  

- Windows CE Platform Builder 裝置管理用戶端 (任何版本)  

- System Center Mobile Device Manager VPN 連線  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> 用戶端站台指派考量  

Configuration Manager 用戶端只能指派給單一主要站台。 當下列所有條件均成立時，您便無法預測用戶端的實際站台指派：

- 您使用自動站台指派，在用戶端安裝期間將用戶端指派給站台
- 有多個界限群組包含相同界限
- 界限群組具有不同的指派站台

如果界限跨多個 Configuration Manager 站台和階層重疊，可能就不會將用戶端指派給您預期的站台，也可能根本不會指派給任何站台。  

Configuration Manager 最新分支用戶端會先檢查站台的版本，然後才完成站台指派。 如果站台界限重疊，您就無法將用戶端指派給舊版的站台。 不過，可能會不正確地將舊版 System Center 2012 Configuration Manager 用戶端指派給新版的 Configuration Manager 最新分支站台。  

為避免在兩個階層的界限重疊時不小心將用戶端指派給錯誤的站台，請設定用戶端安裝參數以將用戶端指派給特定的站台。  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> 混合版本階層中的 Configuration Manager 限制  

當您升級 Configuration Manager 最新分支階層時，有時不同的站台將具有不同版本。 例如，您先升級管理中心網站。 由於站台維護期間的緣故，您只能延至較晚的時間和日期來升級主要站台。  

當單一階層中的不同站台執行不同版本時，部分功能就無法使用。 此行為會影響您在 Configuration Manager 主控台中管理 Configuration Manager 物件的方式，以及對用戶端提供的功能。 通常，無法在執行較舊 Service Pack 版本的站台或用戶端上存取較新版 Configuration Manager 的功能。  

### <a name="network-access-account"></a>網路存取帳戶

您會將管理中心網站升級至 Configuration Manager 最新分支。 您可從連線到此更新站台的 Configuration Manager 主控台，檢視網路存取帳戶詳細資料。 它不會顯示來自仍執行 System Center 2012 Configuration Manager 之站台的帳戶詳細資料。

當您將主要站台升級至與管理中心網站相同的版本之後，主控台中就會顯示帳戶詳細資料。

當您在 Configuration Manager 的版本之間進行更新時，會套用相同的行為。

### <a name="boot-images-for-os-deployment"></a>OS 部署的開機映像

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>從 System Center 2012 Configuration Manager 升級至 Configuration Manager 最新分支時

當階層的頂層站台升級至 Configuration Manager 最新分支時，其會自動更新預設開機映像，以使用 Windows 評定及部署套件 (ADK) 版本 10。 只有在部署至 Configuration Manager 最新分支站台上的用戶端時，才使用這些開機映像。 如需詳細資訊，請參閱[規劃 OS 部署互通性](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)。

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>在 Configuration Manager 最新分支版本之間進行升級時

只要 Configuration Manager 的新版本未更新使用中的 Windows ADK 版本，就不會影響開機映像。

### <a name="new-task-sequence-steps"></a>新的工作順序步驟

如果您建立的工作順序使用了舊版未提供但已在某個 Configuration Manager 版本引進的步驟，可能就會遇到下列問題：

- 當您嘗試從執行舊版 Configuration Manager 的站台編輯工作順序時，即會發生錯誤。

- 工作順序無法在執行舊版 Configuration Manager 用戶端的電腦上執行。

### <a name="client-to-down-level-management-point-communications"></a>用戶端對舊版管理點通訊

如果 Configuration Manager 用戶端是透過比用戶端更舊版本的站台來與管理點進行通訊 ，則只能使用舊版 Configuration Manager 支援的功能。 例如，如果您最近升級了 Configuration Manager 最新分支站台，並從該站台將內容部署至用戶端，假設此用戶端與尚未升級為該版本的管理點進行通訊，該用戶端就無法使用最新版本的新功能。

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>將套件和工作順序部署至舊版用戶端

<!-- SCCMDocs-pr issue #3493 -->

從 1902 版開始，您無法將套件或工作順序部署至用戶端版本 5.7730 或更早版本。 若要解決此限制，請將用戶端升級至較新版本。

## <a name="software-updates"></a>軟體更新

### <a name="orchestration-groups"></a>協調流程群組

在 2002 版中引進的協調流程群組無法用於混合版本的階層中。 <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Configuration Manager 主控台的互通性  

本節包含在混用不同 Configuration Manager 版本的環境中使用 Configuration Manager 主控台的相關資訊。  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>使用 System Center 2012 Configuration Manager 和 Configuration Manager 最新分支的環境

若要管理 Configuration Manager 站台，主控台和主控台連接的站台兩者必須執行相同版本的 Configuration Manager。 例如，您無法使用 System Center 2012 Configuration Manager 主控台來管理 Configuration Manager 最新分支站台，反之亦然。

此外，在同一部電腦上不能同時安裝 System Center 2012 Configuration Manager 主控台和 Configuration Manager 最新分支主控台。

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>安裝多個 Configuration Manager 版本的環境

Configuration Manager 最新分支只支援在電腦上安裝單一 Configuration Manager 主控台。 若要使用不同 Configuration Manager 版本專用的主控台，請在不同的電腦上安裝不同的主控台。

將階層中的站台更新為新版本時，您可以將主控台連線至執行新版本的站台，並檢視該階層中其他站台的資訊。 不過，我們不建議您使用這種設定。 主控台版本與 Configuration Manager 站台版本之間的差異可能會導致資料問題。 而且最新產品版本中所提供的某些功能將無法在主控台中使用。

使用版本與站台版本不符的主控台時，無法管理站台。 這樣做可能會造成資料遺失，也可能讓您的站台面臨風險。 例如，使用 1610 版的主控台無法管理執行 1606 版的站台。
