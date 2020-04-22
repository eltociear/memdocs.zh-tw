---
title: 軟體更新所使用的圖示
titleSuffix: Configuration Manager
description: Configuration Manager 主控台包含圖示，指出已同步處理的更新或軟體更新群組的狀態。
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3843dd4ab4fe5a9aecaae8e6f207c3d037fc1950
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700046"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>針對 Configuration Manager 中的軟體更新所使用的圖示

適用於：  Configuration Manager (最新分支)

同步處理的軟體更新會顯示在 Configuration Manager 主控台中，而且每個軟體更新的第一個資料行都會包含指出特定狀態的圖示。 軟體更新群組也會以圖示代表，以提供群組中所含軟體更新的狀態資訊。 本節提供軟體更新圖示和每個圖示所代表意義的相關資訊。  

## <a name="icons-for-software-updates"></a>軟體更新的圖示  
 同步處理的軟體更新會以下列其中一個圖示代表。  

### <a name="normal-icon"></a>一般圖示  
 ![圖示](../media/Normal.jpg "一般圖示") 具有綠色箭號的圖示代表一般軟體更新。  

 **描述：**  

 一般軟體更新已進行同步處理，且可用於軟體部署。  

 **操作考量：**  

 沒有任何操作考量。  

### <a name="expired-icon"></a>已過期圖示  
 ![圖示](../media/Expired.jpg "已過期圖示") 具有黑色 X 的圖示代表已過期的軟體更新。 當軟體更新顯示在 Configuration Manager 主控台時，您也可以檢視軟體更新的 [已過期]  資料行，來識別已過期的軟體更新。  

 **描述：**  

 已過期的軟體更新之前可以部署至用戶端電腦，但是軟體更新一旦過期，就無法再建立軟體更新的新部署。 已從作用中部署移除過期軟體更新，因此無法再供用戶端使用。  

 **操作考量：**  

 沒有任何操作考量。

### <a name="superseded-icon"></a>已取代圖示  
 ![圖示](../media/Superseded.jpg "已取代圖示") 具有黃色星星的圖示代表已取代的軟體更新。 當軟體更新顯示在 Configuration Manager 主控台時，您也可以檢視軟體更新的 [已取代]  資料行，來識別已取代的軟體更新。  

 **描述：**  

 已取代的軟體更新已取代為軟體更新的較新版本。 通常，取代其他軟體更新的軟體更新會執行下列一或多個動作：  

- 增強、改進或新增至由一個或多個先前發行之軟體更新所提供的修正程式。  

- 提升其軟體更新檔案封裝的效率，如果已核准安裝軟體更新，則用戶端會進行安裝。 例如，已取代的軟體更新可能包含不再與修正程式相關或與新軟體更新現在所支援作業系統相關檔案，因此不會將這些檔案包含在將取代的軟體更新檔案套件中。  

- 更新新版的產品，或者，換句話說，不再適用於舊版本或產品組態。 如果已進行修改來擴充語言支援，則軟體更新也可以取代其他軟體更新。 例如，Microsoft Office 的新版修訂版產品更新可能會移除對舊版作業系統的支援，但在初始軟體更新版本中新增對新語言的其他支援。  

  在 [軟體更新點元件] 內容的 [取代規則] 索引標籤上，您可以指定如何管理已取代的軟體更新。 如需詳細資訊，請參閱 [取代規則](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)。  

  **操作考量：**  

  如果可能的話，請將取代軟體更新部署至用戶端電腦，而不是已取代的軟體更新。 您可以顯示軟體更新清單，這份軟體更新清單會取代軟體更新內容之 [取代資訊]  索引標籤上的軟體更新。  

### <a name="invalid-icon"></a>無效圖示  
 ![圖示](../media/Invalid.jpg "無效圖示") 具有紅色 X 的圖示代表無效軟體更新。  

 **描述：**  

 無效軟體更新位於使用中部署內，但基於某個原因而無法使用內容 (軟體更新檔案)。 下列是可能發生這個狀態的情況：  

- 您已成功部署軟體更新，但是軟體更新檔案已從部署封裝中移除，因此無法再使用。  

- 您在站台建立軟體更新部署，且部署物件已成功複寫到子站台，但部署套件未成功地複寫到子站台。  

  **操作考量：**  

  遺失軟體更新的內容時，除非可以在發佈點上再次使用內容，否則用戶端無法安裝軟體更新。 使用 [重新發佈]  動作，可以將內容重新發佈至發佈點。 遺失在父站台建立之部署中的軟體更新內容時，必須將軟體更新複寫或重新發佈至子站台。 如需內容重新發佈的詳細資訊，請參閱[管理您已發佈的內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)。  

### <a name="metadata-only-icon"></a>僅中繼資料圖示
 ![圖示](../media/MetadataOnly.png "僅中繼資料圖示") 具有藍色箭號的圖示代表僅中繼資料軟體更新。

 **描述：**  

 Configuration Manager 主控台中提供僅中繼資料軟體更新，其可用於產生報告。 您無法部署或下載僅限中繼資料軟體更新，因為軟體更新檔案未與軟體更新中繼資料建立關聯。  

 **操作考量：**  

 僅限中繼資料軟體更新可用於產生報告，但不適用於軟體更新部署。  

## <a name="icons-for-software-update-groups"></a>軟體更新群組圖示  
 軟體更新群組會以下列其中一個圖示代表。  

### <a name="normal-icon"></a>一般圖示  
 ![圖示](../media/Normal.jpg "一般圖示") 具有綠色箭號的圖示，代表只包含一般軟體更新的軟體更新群組。  

 **操作考量：**  

 沒有任何操作考量。  

### <a name="expired-icon"></a>已過期圖示  
 ![圖示](../media/Expired.jpg "已過期圖示") 具有黑色 X 的圖示，代表包含一或多個已過期軟體更新的軟體更新群組。  

 **操作考量：**  

 如果可能，請移除或取代軟體更新群組中已過期的軟體更新。  

### <a name="superseded-icon"></a>已取代圖示  
 ![圖示](../media/Superseded.jpg "已取代圖示") 具有黃色星星的圖示，代表包含一或多個已取代軟體更新的軟體更新群組。  

 **操作考量：**  

 如果可能的話，請將軟體更新群組中的已取代軟體更新取代為取代軟體更新。  

### <a name="invalid-icon"></a>無效圖示  
 ![圖示](../media/Invalid.jpg "無效圖示") 具有紅色 X 的圖示，代表包含一或多個無效軟體更新的軟體更新群組。  

 **操作考量：**  

 遺失軟體更新的內容時，除非可以在發佈點上再次使用內容，否則用戶端無法安裝軟體更新。 使用 [重新發佈]  動作，可以將內容重新發佈至發佈點。 在父站台建立之部署的軟體更新中遺失內容時，需要將軟體更新複寫或重新發佈至子站台。 如需內容重新發佈的詳細資訊，請參閱[管理您已發佈的內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)。  


## <a name="next-steps"></a>後續步驟 

[規劃軟體更新](../plan-design/plan-for-software-updates.md)