---
title: 內容庫清理工具
titleSuffix: Configuration Manager
description: 使用內容庫清理工具，將不再和 Configuration Manager 部署建立關聯的孤立內容移除。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703626"
---
# <a name="content-library-cleanup-tool"></a>內容庫清理工具

適用於：  Configuration Manager (最新分支)

使用內容庫清理命令列工具，以移除發佈點上不再與套件或應用程式建立關聯的內容。 這種類型的內容稱為「孤立內容」  。 此工具會取代針對過去 Configuration Manager 產品所發行的類似舊版工具。  

此工具只會影響您在執行此工具時所指定發佈點上的內容。 此工具無法移除站台伺服器上的內容庫內容。

在站台伺服器上的 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中尋找 **ContentLibraryCleanup.exe**。



## <a name="requirements"></a>需求  

- 一次只能針對一個發佈點執行此工具。  

- 在裝載發佈點的電腦上直接執行此工具來清除，或從另一部伺服器遠端執行此工具。  

- 執行此工具的使用者帳戶必須與 Configuration Manager 中的**系統高權限管理員**安全性角色具有相同權限。  



## <a name="modes-of-operation"></a>作業模式

在下列兩種模式中執行工具：[假設](#what-if-mode)和[刪除](#delete-mode)。

> [!Tip]  
> 從「假設」  模式開始。 若您對結果感到滿意，則以「刪除」  模式執行此工具。  


### <a name="what-if-mode"></a>假設模式   

如果您未指定 `/delete` 參數，此工具會以假設模式執行。 此模式可識別要從發佈點刪除的內容。

- 以此模式執行時，此工具不會刪除任何資料。  

- 此工具會將所要刪除內容的相關資訊寫入記錄檔。 系統不會提示您確認每個可能的刪除動作。  


### <a name="delete-mode"></a>刪除模式   

當您搭配 `/delete` 參數執行此工具時，此工具會以刪除模式執行。

- 以此模式執行時，您可以從發佈點的內容庫刪除指定發佈點上所發現的孤立內容。  

- 在刪除每個檔案之前，請確認此工具應將其刪除。 選取 [Y]  表示是、選取 [N]  表示否，或選取 [全部皆是]  略過接下來的提示並刪除所有的孤立內容。  


### <a name="log-file"></a>記錄檔

以任一種模式執行此工具時，它會自動建立記錄檔。 它會使用下列資訊為記錄檔命名： 
- 用以執行此工具的模式  
- 發佈點的名稱  
- 作業的日期與時間  

當此工具完成時，它會自動在 Windows 中開啟記錄檔。 

根據預設，此工具會將記錄檔寫入執行此工具之使用者帳戶的暫存資料夾。 這個位置是在您執行此工具的電腦上，但該電腦不一定是此工具的目標。 請使用 `/log` 參數，將記錄檔重新導向至另一個位置，包括網路共用。



## <a name="run-the-tool"></a>執行工具

執行工具： 

1. 以系統管理員身分開啟命令提示字元。 將目錄切換到包含 **ContentLibraryCleanup.exe** 的資料夾。  

2. 輸入命令列，其中包含必要的[命令列參數](#bkmk_params)，以及您要使用的任何選擇性參數。



## <a name="command-line-parameters"></a><a name="bkmk_params"></a> 命令列參數  

以任意順序使用這些命令列參數。   

### <a name="required-parameters"></a>必要參數

|參數|詳細資料|
|---------|-------|
| `/dp <distribution point FQDN>`  | 指定要清除之發佈點的完整網域名稱 (FQDN)。 |
| `/ps <primary site FQDN>` | 只有在從次要站台的發佈點清除內容時才為「必要」  。 此工具會連線到父主要站台，以針對 SMS 提供者執行查詢。 這些查詢可讓此工具判定哪些內容應該要在發佈點上。 然後，它可以識別要移除的孤立內容。 因為無法直接從次要站台取得必要的詳細資料，所以必須為位於次要站台的發佈點建立父主要站台的連線。|
| `/sc <primary site code>`  | 只有在從次要站台的發佈點清除內容時才為「必要」  。 請指定父主要站台的站台碼。 |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>範例：掃描並記錄要刪除哪些內容 (假設)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>範例：掃描並記錄位在次要站台之 DP 的內容
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>選擇性參數

|參數|詳細資料|
|---------|-------|
|`/delete`| 當您準好要從發佈點刪除內容時，請使用此參數。 它會在刪除內容之前提示您。 </br></br> 未使用這個參數時，此工具會記錄與所要刪除內容相關的結果。 若沒有這個參數，它實際上並不會從發佈點刪除任何內容。 |
| `/q` | 此參數會以抑制所有提示的無訊息模式執行工具。 這些提示包含它刪除內容的時間。 它也不會自動開啟記錄檔。 |
| `/ps <primary site FQDN>` | 只有在從主要站台的發佈點清除內容時才為選擇性。 請指定發佈點所屬之主要站台的 FQDN。 |
| `/sc <primary site code>` | 只有在從主要站台的發佈點清除內容時才為選擇性。 請指定發佈點所屬之主要站台的站台碼。 |
| `/log <log file directory>` | 指定工具要寫入記錄檔的位置。 此位置可以是本機磁碟機或網路共用。</br></br> 未使用這個參數時，此工具會將記錄檔置於執行此工具之電腦上使用者的暫存目錄中。|

#### <a name="example-delete-content"></a>範例：刪除內容 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>範例：刪除內容而不提示
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>範例：記錄到本機磁碟機
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>範例：記錄到網路共用
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>已知問題

當任何套件或部署失敗，或正在進行中時，此工具可能會傳回下列錯誤：`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

此問題沒有任何因應措施。 正在進行部署或無法部署內容時，此工具無法可靠地識別孤立的檔案。 在您解決該問題之前，此工具不允許您清除內容。
