---
title: 內容擁有權工具
titleSuffix: Configuration Manager
description: 使用內容擁有權工具來變更 Configuration Manager 中孤立套件的擁有權。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707846"
---
# <a name="content-ownership-tool"></a>內容擁有權工具

適用於：  Configuration Manager (最新分支)

內容擁有權工具是其中一種 [Configuration Manager 工具](tools.md)。 它可變更 Configuration Manager 中孤立套件的擁有權。 孤立套件沒有擁有套件的站台伺服器。 站台伺服器仍然擁有套件時，若移除此站台伺服器，套件就會變成孤立套件。

在 Configuration Manager 階層中的任何站台伺服器上執行內容擁有權工具。 以擁有足夠套件權限的系統管理使用者身分登入。  

> [!Tip]  
> 使用 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中的 **ContentLibraryCleanup.exe** 移除  發佈點的孤立內容。 如需詳細資訊，請參閱[內容庫清理工具](../plan-design/hierarchy/content-library-cleanup-tool.md)。  



## <a name="features"></a>功能

- 顯示所有孤立套件  

- 顯示所有套件 (即使它們不是孤立套件)  

- 檢視站台的連線狀態  

- 依名稱、站台碼或套件類型篩選套件  

- 依任何顯示的資料行排序  

- 以單一動作變更一或多個套件的指派  

- 檢視擁有權移轉活動的進度  



## <a name="usage"></a>使用方式

執行 **ContentOwnershipTool.exe** 來啟動工具。 執行此工具不需要電腦的本機系統管理員權限。

沒有任何命令列參數。

> [!Important]   
> 此工具會變更孤立套件的擁有權。 套件本身不會從其儲存所在的發佈點移動。 變更此擁有權並不會在發佈點上更新套件。 它也不會導致用戶端重新評估套件部署的原則。 擁有權變更之後，請確定新的站台伺服器可以存取來源檔案。 它對每個套件的來源檔案至少應具有**讀取**權限。 



## <a name="see-also"></a>請參閱

- [內容管理的基本概念](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [內容庫](../plan-design/hierarchy/the-content-library.md)
