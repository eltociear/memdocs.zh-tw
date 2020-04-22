---
title: 部署軟體更新
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 主控台中手動或自動部署軟體更新。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 8104bbab04e2c8741bfbbc9c6fb61039033941c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696136"
---
# <a name="deploy-software-updates"></a>部署軟體更新  

適用於：  Configuration Manager (最新分支)

軟體更新部署階段是部署軟體更新的程序。 無論您部署軟體更新的方式為何，站台都會：
- 將更新新增至軟體更新群組
- 將更新內容發佈至發佈點
- 將更新群組部署至用戶端  

在您建立部署之後，站台會將相關聯的軟體更新原則傳送至目標用戶端。 用戶端會從內容來源將軟體更新內容檔案下載到其本機快取。 網際網路上的用戶端一律會從 Microsoft Update 雲端服務下載內容。 接著，這些軟體更新便可供用戶端安裝。   

> [!Tip]  
>  若發佈點不可用，內部網路上的用戶端可以從 Microsoft Update 下載軟體更新。  

> [!NOTE]  
>  軟體更新和其他部署類型不同，全都會下載至用戶端快取。 無論用戶端上快取大小上限的設定為何。 如需用戶端快取設定的詳細資訊，請參閱[設定 Configuration Manager 用戶端的用戶端快取](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。  

如果您設定必要的軟體更新部署，就會在排程期限自動安裝軟體更新。 或者，用戶端電腦上的使用者可以在期限前排程或起始軟體更新安裝。 在嘗試安裝後，用戶端電腦會將狀態訊息傳回網站伺服器，回報軟體更新安裝是否成功。 如需軟體更新部署的詳細資訊，請參閱 [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows)。  

軟體更新的部署共有三種主要案例： 
- [手動部署](#BKMK_ManualDeployment)  
- [自動部署](#bkmk_auto)  
- [階段式部署](#bkmk_phased)  

通常，您一開始會手動部署軟體更新以建立用戶端的基準，然後使用自動部署或階段式部署來管理用戶端上的軟體更新。  

> [!Note]  
> 使用階段式部署時，您無法使用自動部署規則。



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> 手動部署軟體更新
在 Configuration Manager 主控台中選取軟體更新，並手動開始部署程序。 您通常會使用這種部署方法來：  

- 在建立管理每月部署的自動部署規則之前，以所需的軟體更新將用戶端更新為最新狀態  

- 部署頻外軟體更新  


以下清單提供手動部署軟體更新的一般工作流程：  

1. 篩選使用特定需求的軟體更新。 例如，提供可擷取超過 50 個用戶端所需之所有安全性或重要軟體更新的準則。  

2. 建立含有軟體更新的軟體更新群組。  

3. 在軟體更新群組中下載軟體更新的內容。  

4. 手動部署軟體更新群組。  

如需詳細資訊和詳細步驟，請參閱[手動部署軟體更新](manually-deploy-software-updates.md)。

> [!Tip]  
> 在手動部署 Office 365 用戶端更新時，請在 [軟體程式庫]  工作區之 [Office 365 用戶端管理]  下方的 [Office 365 更新]  節點中尋找它們。  



## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> 自動部署軟體更新

使用自動部署規則 (ADR) 來設定自動軟體更新部署。 這種部署方式是每月軟體更新 (一般稱為「週二修補程式日」) 和管理定義更新的常見方式。 您可以定義 ADR 的準則以自動化部署程序。 以下清單提供自動部署軟體更新的一般工作流程：  

1.  建立指定部署設定的 ADR。  

2.  站台會將軟體更新新增至軟體更新群組。  

3.  站台會將軟體更新群組部署至目標集合中的用戶端。  

首先，判斷您的自動軟體更新部署策略。 例如，建立 ADR，以便一開始以測試用戶端集合為目標。 在您確認測試群組已成功安裝軟體更新之後，將新的部署新增至規則。 您也可以將現有部署中的目標集合變更為包含更多用戶端的集合。 決定要使用的策略時，請考量下列行為：  

- 您能夠修改 ADR 所建立之軟體更新物件的內容。   

- 當您將軟體更新新增至目標集合時，ADR 會自動將它們部署到用戶端。  

- 當您或 ADR 將新的軟體更新新增至軟體更新群組時，站台會自動將它們部署到目標集合中的用戶端。  

- 隨時啟用或停用 ADR 的部署。  


建立 ADR 之後，請將其他部署新增至規則中。 此動作可協助您管理將不同更新部署到不同集合的複雜性。 每個新部署都會有完整的功能和部署監視體驗。  

您新增的每個新部署：  

- 使用 ADR 第一次執行時所建立的相同更新群組和套件  
- 能夠以不同集合為目標  
- 支援獨特的部署內容，包括：  
  -   啟用時間  
  -   期限  
  -   使用者經驗  
  -   分隔每個部署的警示  


如需詳細資訊和詳細步驟，請參閱[自動部署軟體更新](automatically-deploy-software-updates.md)



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> 分階段進行部署軟體更新

<!--1358146-->
從 1810 版開始，您可以建立軟體更新的階段式部署。 階段式部署可讓您根據可自訂的準則與群組，以組織協調且循序的軟體推出。

如需詳細資訊，請參閱[建立階段式部署](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)。

