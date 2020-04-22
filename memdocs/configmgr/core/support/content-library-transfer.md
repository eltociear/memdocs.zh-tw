---
title: 內容庫傳輸工具
titleSuffix: Configuration Manager
description: 使用內容庫傳輸工具，在 Configuration Manager 發佈點上將內容從某部磁碟機傳輸到另一部磁碟機。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703436"
---
# <a name="content-library-transfer-tool"></a>內容庫傳輸工具

適用於：  Configuration Manager (最新分支)

內容庫傳輸工具是其中一種 [Configuration Manager 工具](tools.md)。 它可將內容從某部磁碟機傳輸到另一部磁碟機。 此工具是設計來在發佈點站台系統上執行。 它支援與站台或遠端站台系統共存的發佈點。  

此工具適用於裝載內容庫的磁碟機已滿時的情況。 首先，請新增或識別擁有足夠空間的另一部硬碟來裝載內容庫。 接者使用 **ContentLibraryTransfer.exe**，將內容從舊的已滿硬碟傳輸至新的空磁碟機。
 
一旦完成傳輸，內容就可供用戶端電腦從新位置進行存取。



## <a name="usage"></a>使用方式 

以擁有系統管理權限的使用者身分在發佈點上執行 **ContentLibraryTransfer.exe**。 

#### <a name="syntax"></a>語法 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>範例
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>限制

- 在發佈點本機上執行此工具。 您無法從遠端電腦執行它。  

- 只有在用戶端未主動存取發佈點時才使用它。 如果您在用戶端存取內容時執行此工具，則目的地磁碟機上的內容庫可能有不完整的資料。 資料轉送可能會完全失敗，而導致內容庫無法使用。  

- 當您執行此工具時，請勿將內容發佈到發佈點。 如果您在內容寫入發佈點時執行此工具，則目的地磁碟機上的內容庫可能有不完整的資料。 資料轉送可能會完全失敗，而導致內容庫無法使用。



## <a name="see-also"></a>請參閱

- [內容管理的基本概念](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [內容庫](../plan-design/hierarchy/the-content-library.md)
