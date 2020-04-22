---
title: Policy Spy
titleSuffix: Configuration Manager
description: 在 Configuration Manager 用戶端上使用 Policy Spy 檢視原則系統並進行疑難排解。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707546"
---
# <a name="policy-spy"></a>Policy Spy

適用於：  Configuration Manager (最新分支)

Policy Spy 是 [Configuration Manager 工具](tools.md)其中之一。 它是在 Configuration Manager 用戶端上檢視原則系統並進行疑難排解的工具。 執行 **PolicySpy.exe** 開啟使用者介面。 如需命令列使用方式的相關資訊，請參閱[命令列語法](#bkmk_policyspy-syntax)。

> [!Important]  
> 以系統管理員身分執行 Policy Spy。 如果不**以系統管理員身分執行**，您會在 [Client Info] \(用戶端資訊\) 中看到下列錯誤：  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a> 命令列語法

Policy Spy 主要是透過其使用者介面使用。 它提供有限的命令列選項，以支援自動化和批次處理。

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>選項：`/export`
此選項以無訊息方式匯出本機或遠端電腦的原則。 `<ExportFilename>` 是工具儲存 XML 匯出原則的檔案名稱。 如果您指定 `<computername>` 選項，Policy Spy 會匯出該電腦的原則，而不是本機電腦的原則。

> [!Note]  
> 此命令列選項不提供指定使用者認證的方法。 若要使用替代認證以存取遠端電腦，請使用 **runas** 命令以所需之安全性認證開啟新的命令提示字元。  


## <a name="usage"></a>使用方式

### <a name="tools-menu"></a>[工具] 功能表

[工具]  功能表提供下列動作：  

- **開啟遠端**：連線到遠端電腦上的 Configuration Manager 用戶端原則。 使用 [連線] 對話方塊擷取遠端電腦的名稱和選用的使用者認證。 如果連線失敗，會在 [Client Info] \(用戶端資訊\) 窗格中顯示錯誤資訊。 如果連線再次失敗，請嘗試選取 [編輯]  功能表的 [重新整理]  或按 F5 連線。  

- **開啟檔案**：開啟 [匯出原則]  選項所建立的原則匯出檔案 (XML)。 此工具會顯示和即時原則如出一轍的匯出原則。 它會停用某些僅適用於您連線到實際用戶端時的功能。  

- **要求電腦指派**：在目標電腦上觸發電腦原則指派的要求。 檢視匯出的原則時，會停用這項功能。  

- **評估電腦原則**：在目標電腦上觸發電腦原則評估。 檢視匯出的原則時，會停用這項功能。  

- **要求使用者指派**：針對目前登入使用者觸發使用者原則指派的要求。 只有在本機電腦上檢視原則時，才能使用此功能。  

- **評估使用者原則**：針對目前登入的使用者觸發使用者原則評估。 只有在本機電腦上檢視原則時，才能使用此功能。  

- **重設原則**：移除所有非預設的原則，並重設站台的原則 Cookie。 然後，觸發機器原則指派的要求。 檢視匯出的原則時，會停用這項功能。  

- **匯出原則**：將目標電腦的原則匯出為 XML 檔案。 在任何使用 Policy Spy 的電腦上檢視此檔案。 若要開啟匯出檔案，請選取 [工具]  功能表的 [開啟檔案]  。 檢視匯出的原則時，會停用這項功能。  


### <a name="edit-menu"></a>[編輯] 功能表

[編輯]  功能表提供下列動作：  

- **刪除**：刪除 [結果] 窗格中選取的執行個體。 僅原則執行個體支援此動作。 如果您嘗試刪除原則執行個體以外的所有項目，此工具會顯示錯誤訊息。 檢視匯出的原則時，會停用這項功能。  

- **重新整理**：重新整理所有的結果，以檢視最新的資訊。 所有在重新整理之前展開的樹狀節點，之後全都會自動展開。 如果 Policy Spy 尚未成功連線到目標電腦的原則，它會嘗試重新連線。 檢視匯出的原則時，會停用這項功能。  

- **清除事件**：清除 [事件] 索引標籤中的所有項目。  



## <a name="results-pane"></a>[結果] 窗格

[結果] 窗格會顯示目標電腦上原則系統的不同檢視。 按一下下列四個索引標籤的其中一個，即可存取這些檢視： 
- [[實際]](#bkmk_policyspy-actual)
- [[已要求]](#bkmk_policyspy-requested)
- [預設值](#bkmk_policyspy-default)
- [[事件]](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a> [實際]

此索引標籤會顯示用戶端目前的原則。 目前的原則會決定用戶端的行為及其用戶端代理程式的行為，例如軟體發佈和清查。 此索引標籤顯示結果的樹狀格式，是以電腦命名空間為根節點，再加上每個使用者特定的命名空間。 展開命名空間節點以顯示類別清單。 展開類別以顯示其執行個體清單。 類別清單只包含有執行個體的類別。


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a> [已要求]

此索引標籤會顯示用戶端自其指派站台擷取的原則指派。 此索引標籤顯示結果的樹狀格式，是以機器命名空間為根節點，再加上每個使用者特定的命名空間。 展開命名空間節點會顯示下列節點：  

- **設定**：顯示衍生自 CCM_Policy_Config 的設定類別清單，其中包含原則物件、指派和其他項目。  

- **設定**：顯示原則所產生的所有使用中設定。 [設定] 會顯示在 [組態] 節點下。 

> [!Note]   
> 多個執行個體可以同名存在，因為用戶端尚未將這些設定合併為最終的結果組。 Policy Spy 使用 RealKey 屬性來顯示這個節點下的執行個體，而不是它們真實的原則金鑰。 將這些執行個體相互關聯至 [實際] 索引標籤顯示的結果組。  


### <a name="default"></a><a name="bkmk_policyspy-default"></a> [預設值]

此索引標籤會顯示和 [已要求]  索引標籤相同的資訊。它也會包含 DefaultMachine 和 DefaultUser 命名空間的內容。


### <a name="events"></a><a name="bkmk_policyspy-events"></a> [事件]

此索引標籤會在原則代理程式事件發生時顯示事件。 此檢視會建立衍生自 CCM_PolicyAgent_Event 之所有事件的 WMI 事件訂閱。 檢視最多顯示 200 個事件。 必要時，它會從清單最上層移除最舊的事件。 如果您選取清單中的最後一個項目，清單就會在新增新的事件時自動向下捲動。 否則，檢視會維持在目前的位置，而您則必須向下捲動或按 End 鍵，才能檢視新的事件。 此檢視在檢視匯出的原則時一律為空。



## <a name="client-info-pane"></a>[Client Info] \(用戶端資訊\) 窗格
[Client Info] \(用戶端資訊\) 窗格會顯示目標電腦的屬性清單。 如有，它會顯示下列屬性：  
- Name
- 識別碼
- 版本
- 網站
- 指派的 MP
- 常駐 MP
- Proxy MP
- Proxy 狀態



## <a name="details-pane"></a>[詳細資料] 窗格
[詳細資料] 窗格會顯示目前選取範圍的詳細資訊。 如果沒有作用中的選取範圍，它會顯示 Policy Spy 本身包括版本的相關資訊。 否則，它會以受控物件格式 (MOF) 表示法顯示所選項目。

Policy Spy 會使用它自己的 MOF 產生常式，建立比 WMI 產生之純文字 MOF 更好用的 HTML 顯示。 此行為允許 Policy Spy 新增下列功能，讓 MOF 更易於閱讀：  

- 語法醒目提示  

- 縮排的物件和陣列  

- 屬性可分為系統、繼承和本機群組。 預設摺疊系統和繼承群組。 您可以立即查看執行個體實際使用哪些屬性。  

- 將 MOF 或純文字 MOF 複製到剪貼簿。 這項功能透過直接呼叫 MofComp 工具，將 MOF 貼入其他應用程式，十分好用。  

若為衍生自 CCM_Policy_Policy 的原則物件執行個體，[詳細資料] 窗格會顯示出現之 MOF 下的原則本文。 如果用戶端尚未下載原則本文，Policy Spy 會顯示超連結。 按一下連結，直接從用戶端的管理點下載原則本文。 如果此工具成功下載原則本文，它會以回覆內容取代超連結。 否則，Policy Spy 會更新顯示，指出要求失敗。

