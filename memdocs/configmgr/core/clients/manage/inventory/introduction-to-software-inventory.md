---
title: 軟體清查
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 中的軟體清查簡介。
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695386"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Configuration Manager 中的軟體清查簡介

適用於：  Configuration Manager (最新分支)

軟體清查可用來收集用戶端裝置上檔案的相關資訊。 軟體清查也可以從用戶端裝置收集檔案，並將這些檔案儲存到站台伺服器。 當您在用戶端設定中選取 [在用戶端上啟用軟體清查]  設定時，會收集軟體清查。 您也可以在用戶端設定中排程作業。  

在啟用軟體清查且用戶端執行軟體清查週期之後，用戶端會將資訊傳送至用戶端站台中的一個管理點。 管理點接著會將清查資訊轉送至 Configuration Manager 站台伺服器，再由該伺服器將資訊儲存到站台資料庫。

 以下是檢視軟體清查資料的幾個方法︰  

- [建立查詢](../../../../core/servers/manage/create-queries.md)，以傳回具有所指定檔案的裝置。   

- 建立[查詢式集合](../../../../core/clients/manage/collections/introduction-to-collections.md)，以傳回具有所指定檔案的裝置。   

- [執行報告](../../../servers/manage/introduction-to-reporting.md)，以提供裝置上檔案的詳細資料。

- 使用[資源總管](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)，檢查從用戶端裝置清查及收集之檔案的詳細資訊。   

 當軟體清查在用戶端裝置上執行時，第一份報告是完整清查。 後續報告只會包含差異清查資訊。 站台伺服器會依差異資訊收到的順序來進行處理。 如果遺漏用戶端的差異資訊，站台伺服器會拒絕之後的差異資訊，並指示該用戶端執行完整清查。  

 Configuration Manager 可以探索雙重開機電腦，但只會傳回清查時在作用中的作業系統清查資訊。  
