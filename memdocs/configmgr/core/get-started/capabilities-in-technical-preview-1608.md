---
title: Technical Preview 1608 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1608 版中可用的功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074175"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Configuration Manager Technical Preview 1608 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1608 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>準備 ConfigMgr 用戶端以進行擷取之工作順序步驟的改進  
「準備 ConfigMgr 用戶端」步驟現在會完全移除 Configuration Manager 用戶端，而不是只移除金鑰資訊。 當工作順序部署擷取的作業系統映像時，每次都會安裝新的 Configuration Manager 用戶端。  


## <a name="improvements-to-software-center"></a>軟體中心的增強功能
* 軟體中心的 [應用程式]  、[更新]  及 [作業系統]  索引標籤現在會顯示最近新增的軟體。 瀏覽窗格中的數字顯示每個索引標籤中新軟體的數量。
* 使用者現在可以要求應用程式的核准，然後檢視軟體中心內 [應用程式詳細資料]  檢視中的要求歷程記錄。 [應用程式詳細資料]  中的 [要求]  按鈕不會再重新導向至 Web 應用程式類別目錄。

## <a name="improvements-to-asset-intelligence"></a>Asset Intelligence 的改進
我們為已清查的軟體內容新增了欄位，可讓您設定與其他軟體的父系及子系關聯。 在 [已清查的軟體] 清單中，您可以檢視任何軟體的父系，同時可隱藏所有子系軟體。

### <a name="configure-a-parent-to-child-relationship"></a>設定父系與子系關聯
  1. 若要設定父系軟體，請在 [已清查的軟體] 節點中，以滑鼠右鍵按一下 [已清查的軟體]  清單中的軟體項目，然後選擇 [內容]  。
  2. 在開啟的對話方塊中，選取您要設定為初始選擇之父系軟體的軟體。

### <a name="filter-the-software-display"></a>篩選軟體顯示
定義父系與子系關聯之後，您可以篩選檢視，只顯示父系軟體或未定義關聯性的軟體。 這會隱藏設定為另一個已清查軟體子系的所有軟體。 操作方法：
   1. 在搜尋列中，選擇 [新增準則] 
   2. 選取 [父系軟體]  ，然後將準則值變更為 [是空的]  ，再按一下 [搜尋]  。

此顯示畫面現在只會顯示父系軟體項目，或未定義關聯性的軟體。 只是另一個標題子系的軟體則不會顯示。

## <a name="remote-control-keyboard-translation"></a>遠端控制鍵盤轉譯
在過去，Configuration Manager 會將按鍵位置從檢視者的位置傳輸到共用者的位置。 如果檢視者和共用者的鍵盤設定不同，就會發生問題。 例如，具有英文鍵盤的檢視者會輸入"A"，但共用者的法文鍵盤會提供 "Q"。 我們將變更此預設行為，讓字元本身從檢視者的鍵盤傳輸到共用者，以確保檢視者預期輸入的內容會抵達共用者端。

如果檢視者想要根據共用者的鍵盤配置自行輸入，則可以關閉此行為。 若要變更此行為，請在 [Configuration Manager 遠端控制]  中，選擇 [動作]  ，然後選擇 [啟用鍵盤轉譯]  以轉移按鍵位置。

> [!NOTE]
>
> ~!#@$% 等特殊按鍵不會正確轉譯。
