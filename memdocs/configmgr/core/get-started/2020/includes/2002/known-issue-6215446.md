---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 54e00688c1375f9ec54ada86d2b2c4b9347d5405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691846"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> 無法刪除集合

<!--6245446-->
您無法在此版本的技術預覽分支中刪除集合。

此問題的因應措施為使用下列 Configuration Manager PowerShell Cmdlet 來刪除集合：

- [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps) \(英文\)
