---
title: '將更新新增至更新群組 '
titleSuffix: Configuration Manager
description: 將軟體更新手動或自動新增至您環境中的軟體更新群組。
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c38ed629e606d3f891a6473866d0e8eda40eade1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708586"
---
# <a name="add-software-updates-to-an-update-group"></a>將軟體更新新增至更新群組  

適用於：  Configuration Manager (最新分支)

 軟體更新群組提供您在環境中組織軟體更新的有效方法。 您可以手動將軟體更新新增至軟體更新群組，或使用 ADR 自動將軟體更新新增至軟體更新群組。 您也可以手動部署軟體更新群組，或使用 ADR 自動部署群組。 部署軟體更新群組之後，您可以將新的軟體更新新增至群組，然後 Configuration Manager 就會自動部署它們。 利用下列程序，將軟體更新新增至新的或現有軟體更新群組。  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>將軟體更新新增至新的軟體更新群組  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。  

2.  在 [軟體程式庫] 工作區中，展開 [軟體更新]  ，然後按一下 [所有軟體更新]  。  

3.  選取要新增到新軟體群組的軟體更新。  

4.  在 [首頁]  索引標籤的 [更新]  群組中，按一下 [建立軟體更新群組]  。  

5.  指定軟體更新群組的名稱，並選擇是否要提供描述。 使用能為您提供足夠資訊的名稱和描述，來判斷哪一種類型的軟體更新應在軟體更新群組中。 若要進行，請按一下 [建立]  。  

6.  按一下 [軟體更新群組]  以顯示新的軟體更新群組。  

7.  選取軟體更新群組，然後在 [首頁]  索引標籤的 [更新]  群組中按一下 [顯示成員]  ，顯示此群組包括的軟體更新的清單。  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>將軟體更新新增至現有軟體更新群組  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫]  。  

2.  在 [軟體程式庫] 工作區中，展開 [軟體更新]  ，然後按一下 [所有軟體更新]  。  

3.  選取您要新增到新軟體群組的軟體更新。  

    > [!NOTE]  
    >  在上 [所有軟體更新]  節點上，Configuration Manager 會顯示所有更新，除了**升級**分類和 **Office 365 用戶端**產品分類。  

4.  在 [首頁]  索引標籤的 [更新]  群組中，按一下 [編輯成員資格]  。  

5.  選取您要新增軟體更新的軟體更新群組。  

6.  按一下 [軟體更新群組]  節點，以顯示軟體更新群組。  

7.  選取軟體更新群組，然後在 [首頁]  索引標籤的 [更新]  群組中按一下 [顯示成員]  ，顯示軟體更新群組包括的軟體更新的清單。  
