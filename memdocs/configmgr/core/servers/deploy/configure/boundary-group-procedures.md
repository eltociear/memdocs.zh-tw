---
title: 界限群組的程序
titleSuffix: Configuration Manager
description: 設定界限群組，以邏輯方式組織稱為界限的相關網路位置。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697386"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>如何設定 Configuration Manager 的界限群組

適用於：  Configuration Manager (最新分支)

本文包含如何設定界限群組的程序。 請務必在開始前先行了解界限群組的概念。 如需詳細資訊，請參閱[界限群組](boundary-groups.md)。



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a> 建立界限群組  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [界限群組]  節點。  

2.  在 [常用]  索引標籤的 [建立]  群組中，選取 [建立界限群組]  。  

3.  在 [建立界限群組]  對話方塊的 [一般]  索引標籤上，指定此界限群組的**名稱**。 選擇性地包含**描述**。  

4.  選取 [確定]  以儲存新界限群組，或繼續進行進行下一節來設定界限群組。  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a> 設定界限群組  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [界限群組]  節點。  

2.  選取您想要修改的界限群組，然後選取功能區中的 [內容]  。 這個動作會開啟界限群組的 [內容] 視窗。  

進行以下設定：  
- [新增或移除界限](#bkmk_add)  
- [設定站台指派和選取站台系統伺服器](#bkmk_references)  
- [設定後援行為](#bkmk_bg-fallback)  
- [設定界限群組選項](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a> 新增或移除界限

在界限群組的 [內容] 視窗中，使用 [一般]  索引標籤來修改屬於此界限群組成員的界限：  

- 若要新增界限，請選取 [新增]  。 在 [新增界限] 視窗中，選取一或多個界限的核取方塊，然後選取 [確定]  。  

- 若要移除界限，請選取清單中的界限，然後選取 [移除]  。  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a> 設定站台指派和選取站台系統伺服器

若要修改站台指派和相關聯的站台系統伺服器設定，請切換至界限群組 [內容] 視窗中的 [參考]  索引標籤。  

- 若要啟用此界限群組以供用戶端用來指派站台，請選取 [使用此界限群組進行站台指派]  。 然後從 [指派的站台]  下拉式清單中選擇站台。 如需詳細資訊，請參閱[站台指派](boundary-groups.md#site-assignment)。  

- 若要將可用的站台系統伺服器與此界限群組建立關聯，請選取 [新增]  。 [新增站台系統] 視窗只會列出具有已支援之站台系統角色的伺服器。 選取一或多部伺服器的核取方塊，然後選取 [確定]  。 它會將它們新增為此界限群組的相關聯站台系統伺服器。  

    > [!NOTE]  
    >  您可以從階層中的任何網站選取可用站台系統的任何組合。 選取的站台系統會在每個屬於此界限群組成員之界限內容中的 [站台系統]  索引標籤上列出。  

- 若要從此界限群組中移除伺服器，請選取該伺服器，然後選取 [移除]  。  

    > [!NOTE]  
    >  若要停止使用此界限群組做為相關聯的站台系統，請移除所有列為相關聯站台系統伺服器的伺服器。  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a> 設定後援行為

若要設定後援行為，請切換到界限群組 [內容] 視窗中的 [關聯性]  索引標籤。  

- 建立與另一個界限群組的關聯性：  

  - 選取 [新增]  。 在 [後援界限群組] 視窗中，選取要設定的界限群組。  

  - 針對下列站台系統角色設定後援時間：  
    - 發佈點  
    - 軟體更新點  
    - 管理點  

      > [!Note]  
      > 例如，您可以開啟「分公司」界限群組的 [內容] 視窗。 在 [後援界限群組] 視窗中，選取「主要辦公室」界限群組。 您會將發佈點後援時間設定為 `20`。 當您儲存此設定時，「分公司」界限群組中的用戶端將在 20 分鐘之後，在「主要辦公室」界限群組中搜尋發佈點的內容。  

  - 若要避免對特定界限群組進行後援，請選取該界限群組，然後針對站台系統角色的類型選取 [永不後援]  。 這個動作可以包含「預設的站台界限群組」  。  

- 若要修改現有關聯性的設定，請在清單中選取界限群組，然後選取 [變更]  。 這個動作只會開啟適用於此界限群組的 [後援界限群組] 視窗。  
 
- 若要移除關聯性，請選取清單中的界限群組，然後選取 [移除]  。  

如需詳細資訊，請參閱[後援](boundary-groups.md#fallback)。 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a> 設定界限群組選項
<!--1356193-->
從 1806 版開始，若要為此界限群組中的用戶端設定其他選項，請切換至 [選項]  索引標籤。如需詳細資訊，請參閱[適用於對等下載的界限群組選項](boundary-groups.md#bkmk_bgoptions)。

- **允許此界限群組中的對等下載**：這個選項預設為啟用。 管理點會為用戶端提供內容位置清單，其中包含對等來源。  

    - **對等下載期間，僅使用相同子網路中的對等**：此設定取決於上方的設定。 如果您啟用此選項，管理點只會包含於內容位置清單對等來源中，而這些來源位於與用戶端相同的子網路。  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a> 設定自動站台指派的後援站台  

如果用戶端不在具有指派站台的界限群組中，請在進行安裝時，將它們指派給此站台。

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2.  在功能區 [常用]  索引標籤的 [站台]  群組中，選取 [階層設定]  。  

3.  在 [一般]  索引標籤上，選取 [使用後援站台]  的核取方塊。 然後從 [後援站台]  下拉式清單中選取站台。  

4.  選取 [確定]  儲存設定。  

如需詳細資訊，請參閱[站台指派](boundary-groups.md#site-assignment)。


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a> 允許使用慣用的管理點  

如需詳細資訊，請參閱[慣用的管理點](boundary-groups.md#bkmk_preferred)。

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 在功能區 [常用]  索引標籤的 [站台]  群組中，選取 [階層設定]  。  

3. 在 [一般]  索引標籤上，選取 [用戶端偏好使用界限群組中指定的管理點]  。  

4. 選取 [確定]  儲存設定。  

