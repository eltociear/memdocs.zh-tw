---
title: 檢視診斷資料
titleSuffix: Configuration Manager
description: 檢視診斷和使用方式資料，確認 Configuration Manager 階層不包含任何機密資訊。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692736"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>如何檢視 Configuration Manager 的診斷及使用方式資料

適用於：  Configuration Manager (最新分支)

您可以檢視 Configuration Manager 階層的診斷和使用方式資料，以確認它沒有包含任何敏感性或可識別資訊。 站台會摘要其診斷資料並儲存在站台資料庫的 **TEL_TelemetryResults** 資料表中。 它會格式化資料，以便以程式設計方式來有效率地使用。

本文中資訊可讓您檢視傳送至 Microsoft 的確切資料。 它不適用於其他用途，例如資料分析。  

## <a name="view-data-in-database"></a>檢視資料庫中的資料

下列 SQL 命令可用來檢視這份資料表的內容，並顯示已傳送的確切資料：  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>匯出資料

當服務連接點處於離線模式時，請使用服務連接工具將目前的資料匯出為逗點分隔值 (CSV) 檔案。 請使用 **-Export** 參數在服務連接點上執行服務連接工具。

如需詳細資訊，請參閱[使用服務連線工具](../../servers/manage/use-the-service-connection-tool.md)。

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a> 單程雜湊

一些資料是由隨機英數字元字串所組成。 Configuration Manager 使用 SHA-256 演算法來建立單程雜湊。 此程序可確保 Microsoft 不會收集潛在的敏感性資料。 雜湊資料仍會用於相互關聯和比較用途。

例如，擷取每個資料表名稱的單程雜湊，而不是收集站台資料庫的資料表名稱。 此行為可確保不顯示任何自訂的資料表名稱。 然後，Microsoft 會執行預設 SQL 資料表名稱的相同單程雜湊程序。 比較這兩項查詢的結果，可判斷您資料庫架構與產品預設值的偏差。 然後，此資訊可用來改善需要變更 SQL 結構描述的更新。  

檢視未經處理的資料時，每個資料列都會出現一個通用的雜湊值。 此雜湊是階層識別碼。 它用來建立資料與相同階層的相互關聯，但不識別客戶或來源。

### <a name="how-the-one-way-hash-works"></a>單程雜湊的運作方式

1. 在 SQL Management Studio 中針對 Configuration Manager 資料庫執行下列 SQL 查詢來取得階層識別碼︰

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. 使用下列 Windows PowerShell 指令碼來執行階層識別碼的單程雜湊。  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. 比較指令碼輸出與原始資料中的 GUID。 此程序會示範資料的遮蔽方式。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [診斷使用方式資料的層級](levels-overview.md)
