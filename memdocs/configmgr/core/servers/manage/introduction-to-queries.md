---
title: 查詢簡介
titleSuffix: Configuration Manager
description: 建立並執行查詢，以找出 Configuration Manager 階層中符合查詢準則的物件。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694566"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Configuration Manager 中的查詢簡介

適用於：  Configuration Manager (最新分支)

您可以建立並執行查詢，以找出 Configuration Manager 階層中符合查詢準則的物件。 這些物件包含像電腦或使用者群組等特定類型的項目。 查詢可以傳回大部分類型的 Configuration Manager 物件，其中包括網站、集合、應用程式以及清查資料。  

## <a name="query-creation-overview"></a>查詢建立概觀

 建立查詢時，您必須指定至少兩個參數：要搜尋的位置與您想要搜尋的項目。 例如，若要尋找 Configuration Manager 站台中所有電腦的可用硬碟空間量，您可以建立查詢以搜尋 [邏輯磁碟]  屬性類別和 [可用空間 (MB)]  屬性，以取得可用硬碟空間。  

 建立初始查詢之後，您可以指定其他的查詢準則。 例如，您可以指定查詢結果僅包含指派給指定站台的電腦。 您也可以變更結果的顯示方式，依您所需的順序來檢視結果。 例如，您可以指定依可用硬碟空間量的遞增或遞減順序來排序結果。  

 當您建立查詢時，Configuration Manager 會將它們儲存並顯示在 [監視]  工作區的 [查詢]  節點中。 您可以從這個位置建立新的查詢，以及執行、更新及管理現有的查詢。  

 您也可以將查詢匯入 Configuration Manager 集合中的查詢規則。 如需詳細資訊，請參閱[如何建立集合](../../../core/clients/manage/collections/create-collections.md)。  

## <a name="next-steps"></a>後續步驟

 [如何建立查詢](../../../core/servers/manage/create-queries.md)
