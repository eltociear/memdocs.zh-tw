---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697846"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> 工作順序無法供 PXE 或媒體使用

<!--5578298-->
如果您為 PXE 或媒體 (USB 或 DVD) 部署工作順序，用戶端不會收到原則。 下列訊息位於 **smsts.log** 中：

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>因應措施

從軟體中心開始工作順序。
