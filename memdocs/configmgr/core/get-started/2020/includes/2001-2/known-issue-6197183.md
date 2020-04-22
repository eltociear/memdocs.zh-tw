---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692096"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> 無法建立或編輯部分集合

<!--6197183-->
您無法在此版本的 Technical Preview 分支中建立新的集合。 您也無法編輯現有使用者集合的屬性。

若要解決此問題，請使用 Configuration Manager PowerShell Cmdlet 來建立新的集合，並編輯現有的使用者集合。 一些可用來管理集合的 Cmdlet 包括：

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps) \(英文\)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps) \(英文\)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links) \(英文\)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps) \(英文\)
