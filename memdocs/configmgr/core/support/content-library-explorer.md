---
title: 內容庫總管
titleSuffix: Configuration Manager
description: 使用內容庫總管來檢視 Configuration Manager 發佈點上的內容庫，並針對其進行疑難排解。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92aa778dded970800a65cab9074a547e870bf88e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707856"
---
# <a name="content-library-explorer"></a>內容庫總管

適用於：  Configuration Manager (最新分支)

內容庫總管是其中一種 [Configuration Manager 工具](tools.md)。 您可以使用此工具執行下列活動：  

- 探索特定發佈點上的內容庫  

- 針對內容庫問題進行疑難排解  

- 複製內容庫中的套件、內容、資料夾和檔案  

- 將套件重新發佈至發佈點  

- 驗證遠端發佈點上的套件  



## <a name="requirements"></a>需求

- 使用具有系統管理權限的帳戶來執行此工具：  

    - 目標發佈點  

    - 站台伺服器上的 WMI 提供者  

    - Configuration Manager 提供者  

- 只有**系統高權限管理員**和**唯讀分析師**角色才有足夠的權限，可從此工具檢視所有資訊。  

    - 其他角色 (例如**應用程式系統管理員**) 可以檢視部分資訊。 如需詳細資訊，請參閱[已停用的套件](#bkmk_disabled-packages)。  

    - **唯讀分析師**無法從此工具重新發佈套件。  

- 只要可以連線至下列項目，即可從任何電腦執行此工具：  

    - 目標發佈點  

    - 主要站台伺服器  

    - Configuration Manager 提供者  

- 如果發佈點與站台伺服器共置，則仍然需要具有站台伺服器的系統管理存取權。  



## <a name="usage"></a>使用方式 

當您啟動 **ContentLibraryExplorer.exe** 時，請輸入目標發佈點的完整網域名稱 (FQDN)。 它接著會連線至發佈點。 如果發佈點是次要站台的一部分，則會提示您輸入主要站台伺服器的 FQDN，以及主要站台碼。

在左窗格中，檢視會發佈至此發佈點的套件。 展開套件，並探索其資料夾結構。 此結構符合您用來建立套件的資料夾結構。

當您選取資料夾時，會將資料夾內的任何檔案顯示在右窗格中。 此檢視包含下列資訊： 
- 檔案名稱
- 檔案大小
- 它所在的磁碟機
- 使用磁碟機上相同檔案的其他套件
- 上次在發佈點上變更檔案時

此工具也會連線至 Configuration Manager 提供者。 此連線是要判斷將哪些套件發佈至發佈點，以及它們是否實際上位於發佈點的內容庫中。 例如，擱置發佈的套件可能尚未存在於內容庫中。 這類套件在工具中會顯示為「擱置」，而且不會啟用此套件的動作。


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a> 已停用套件

有些套件會出現在發佈點上，但在 Configuration Manager 主控台中看不到。 這些套件會標上星號 (\*)。 可能未對這些套件執行任何動作。 其他套件也可能會標上星號，並已停用動作。 

已停用套件有三個主要原因：  

- 此套件是 Configuration Manager 用戶端升級。 此套件包含 "ccmsetup.exe"。  

- 您的使用者帳戶無法存取套件，原因可能是以角色為基礎的系統管理。 例如，**應用程式作者**角色在主控台中看不到驅動程式套件，因此會將發佈點上的任何驅動程式套件都標示為已停用。  

- 套件在發佈點上是孤立的。  


### <a name="validate-packages"></a>驗證套件

使用工具列上的 [套件]   > [驗證]  ，來驗證套件。 先在左窗格中選取套件節點，請不要選取內容或資料夾。 此工具會連線至此動作之發佈點上的 WMI 提供者。 此工具啟動時，會將遺漏一或多個內容的套件標示為無效。 驗證套件時會顯示遺漏的內容。 如果所有內容都存在，但資料損毀，則驗證會偵測到損毀。


### <a name="redistribute-packages"></a>重新發佈套件

使用工具列上的 [套件]   > [重新發佈]  ，來重新發佈套件。 先在左窗格中選取套件節點。 此動作需要重新發佈套件的權限。


### <a name="other-actions"></a>其他動作

使用 [編輯]   > [複製]  ，將套件、內容、資料夾和檔案從內容庫複製至指定的資料夾。 您無法複製內容庫本身。 選取多個檔案，但您無法選取多個資料夾。

使用 [編輯]   > [尋找套件]  ，來搜尋套件。 此動作會在套件名稱和套件識別碼中搜尋您的查詢。



## <a name="limitations"></a>限制

- 此工具無法以任何方式直接操縱內容庫。 內容庫的變更可能會導致故障。  

- 此工具可以重新發佈套件，但只能發佈至目標發佈點。  

- 當您將發佈點與站台伺服器共置時，會無法驗證套件資料。 請改為使用 Configuration Manager 主控台。 此工具仍然會檢查套件以確定所有內容都存在，但不一定完整。  

- 您無法使用此工具來刪除內容。



## <a name="see-also"></a>請參閱

- [內容管理的基本概念](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [內容庫](../plan-design/hierarchy/the-content-library.md)
