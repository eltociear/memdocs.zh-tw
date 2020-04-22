---
title: Client Spy
titleSuffix: Configuration Manager
description: 使用 Client Spy 針對 Configuration Manager 用戶端上的軟體發佈、清查和軟體計量進行疑難排解。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707906"
---
# <a name="client-spy"></a>Client Spy

適用於：  Configuration Manager (最新分支)

Client Spy 是 [Configuration Manager 工具](tools.md)中的其中一項。 它是用來針對 Configuration Manager 用戶端上的軟體發佈、清查和軟體計量進行疑難排解的工具。 

工具所擷取的大部分資訊與軟體部署有關：
- 所有目前的軟體部署 
- 軟體發佈歷程記錄
- 用戶端快取設定
- 快取項目
- 暫止的必要部署
- 可用的部署  

它也會顯示下列清查資訊
- 最新的清查週期日期
- 上次報告日期
- 軟體清查的主要和次要版本
- 檔案收集
- 硬體清查
- IDMIF 收集
- 探索資料記錄 (DDR) 

也會顯示軟體計量規則。 

> [!Note]   
> 為了改善效能，此工具只會在您選取每個索引標籤時收集它的資訊。 同樣地，當您按一下 [重新整理]  ，它只會重新整理目前所顯示索引標籤的資訊。



## <a name="usage"></a>使用方式


### <a name="tools-menu"></a>[工具] 功能表

[工具]  功能表提供下列動作：  

#### <a name="connect"></a>連線
從另一部電腦擷取資訊。  

- 根據預設，工具會顯示目前電腦的資訊。 

- 使用遠端電腦名稱、帳戶的使用者名稱和密碼進行連線。 工具會建立與遠端電腦之 IPC$ 共用的連線。 當工具結束時，或您連線至其他電腦時，它會刪除連線。  

- 它需要具有足夠認證可取得資訊的帳戶。  

- 如果您未指定使用者名稱和密碼，Client Spy 會使用目前登入使用者的資訊安全內容來進行連線嘗試。  

- 當您連線到遠端電腦時，顯示的所有索引標籤會顯示來自遠端電腦的資訊。

#### <a name="software-distribution"></a>軟體發佈
顯示 [[軟體發佈](#software-distribution)] 索引標籤，並隱藏其他索引標籤。 根據預設，Client Spy 會顯示 [軟體發佈] 索引標籤。

#### <a name="inventory"></a>清查
顯示 [清查] 索引標籤，並隱藏其他索引標籤。

#### <a name="software-metering"></a>軟體計量
顯示 [軟體計量] 索引標籤，並隱藏其他索引標籤。

#### <a name="save-current-tab-to-file"></a>將目前的索引標籤儲存至檔案
將目前顯示索引標籤中的資訊，儲存至您指定的文字檔案。 

#### <a name="save-all-tabs-to-file"></a>將所有索引標籤儲存至檔案
將所有索引標籤中的資訊，儲存至您指定的文字檔案。 它只會儲存您的帳戶可以看到的資訊。



## <a name="software-distribution-tab"></a>[軟體發佈] 索引標籤

在下列四個索引標籤上設定：
- [軟體發佈執行要求](#bkmk_exec-requests)
- [軟體發佈歷程記錄](#bkmk_history)
- [軟體發佈快取資訊](#bkmk_cache-info)
- [暫止執行的軟體發佈](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a> 軟體發佈執行要求

此索引標籤會顯示所有現有的部署，包括以裝置和使用者為目標的部署。

[軟體發佈執行要求] 索引標籤中的每個樹狀結構項目都包含下列四個屬性：
- 公告識別碼。 如果是可用的部署，這個值可能是空白。 
- 套件識別碼 
- 程式名稱 
- 使用者。 這可能是目標使用者 SID，或要求起始者的使用者 SID。 如果兩者都是系統要求，則顯示的使用者是 System。 

針對每個執行要求，它也會以子樹狀目錄結構顯示下列資訊：
- 程式名稱 
- 套件識別碼 
- 封裝名稱 
- 要求建立時間 
- 狀況 
- 執行狀態，如果狀態為 Running 
- 執行內容 (使用者或管理員) 
- 記錄狀態 (Success、Failure 或 NotRun) 
- LastRunTime (Never，如果程式尚未執行過) 
- RetryCount，如果狀態為 WaitingRetry 
- ContentAccess (重試計數，如果狀態為 WaitingRetry) 
- FailureCode，如果狀態為 WaitingRetry 
- FailureReason，如果狀態為 WaitingRetry 

如果要求需要內容，則狀態會是 WaitingContent。 [軟體發佈快取資訊] 索引標籤會顯示這項下載要求的詳細資料。

如果執行的要求是下載要求，它也會顯示下載的位元組數。

> [!Note]   
> 它會針對執行要求的各種狀態使用不同的圖示。


### <a name="software-distribution-history"></a><a name="bkmk_history"></a> 軟體發佈歷程記錄

此索引標籤包含所有先前執行程式的相關資訊。 此資訊儲存在登錄中。

這個樹狀結構的主要分支是不同的使用者歷程記錄，包括 System。 它會顯示包含套件清單的樹狀子目錄，程式已針對每個使用者從這個樹狀子目錄執行。 

每個套件樹狀子目錄的套件識別碼和套件名稱會顯示已執行的程式清單。 它會針對每一者顯示下列屬性： 
- 程式名稱
- 執行狀態
- 上次執行時間
- 失敗碼
- 失敗原因  

程式成功執行時，失敗碼和失敗原因是空白。


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a> 軟體發佈快取資訊

#### <a name="cache-config"></a>快取設定
包含 Configuration Manager 用戶端快取的相關資訊。 這項資訊包括快取位置、快取大小，以及它是否目前在使用中。 

#### <a name="cached-items"></a>快取項目
包含目前快取中所有項目的樹狀子目錄。 每個樹狀目錄項目包含每個項目的下列相關資訊： 
- 快取中的項目位置 (資料夾)
- 目前狀態
- 套件識別碼
- 套件名稱
- 套件版本
- 套件大小
- 目前參考計數
- 上次參考時間 (UTC)  

#### <a name="downloading-items"></a>正在下載項目
這些是用戶端目前正在下載的項目。 每個會顯示快取項目所顯示的相同資訊，以及下載的 KB 數。 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a> 暫止執行的軟體發佈

此索引標籤包含詳述過去和未來必要部署和可用部署清單的資訊。

每個樹狀目錄分支是針對具有可用部署的每個使用者帳戶，包括 System。

針對每個使用者，樹狀子目錄會包含下列三個項目：  

#### <a name="mandatory-advertisements-with-future-executions"></a>具有未來執行的必要公告
這些是仍有剩餘待執行程式的必要公告。 這些可以是週期性、單次，或多個排程公告。 每一者都會顯示公告識別碼、下次執行時間，以及執行公告的排程。 

#### <a name="optional-advertisements"></a>選擇性公告
顯示所有已發佈公告的清單。 它也會顯示每一個公告的詳細資料，例如公告識別碼、程式名稱和套件名稱。 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>沒有任何未來排程公告的過去強制公告
這是存在於用戶端且沒有排定未來待執行程式的公告清單。 會顯示公告識別碼、套件名稱和程式名稱。 會針對任何選擇性的公告顯示樹狀子目錄項目。

> [!Note]  
> 只有在經檢視的電腦上具有與已公告原則相關聯的套件，才提供套件名稱資訊。 不再有與可用原則相關聯的套件，會顯示「套件名稱無法再使用」的訊息。  



## <a name="inventory-tab"></a>清查索引標籤

只有一個索引標籤包含清查資訊。 主要的樹狀目錄包含下列五個項目：  

- **軟體清查**：包含上一個週期開始的日期、上次報告的日期，和上次報告的主要和次要版本。  

- **檔案收集**：包含上一個週期開始的日期、上次報告的日期，和上次報告的主要和次要版本。  

- **硬體清查**：包含上一個週期開始的日期、上次報告的日期，和上次報告的主要和次要版本。  

- **IDMIF 收集**：包含上一個週期開始的日期、上次報告的日期，和上次報告的主要和次要版本。  

- **DDR**：包含上一個週期開始的日期、上次報告的日期，和上次報告的主要和次要版本。 DDR 資訊也會顯示在樹狀子目錄中。



## <a name="software-metering-tab"></a>軟體計量索引標籤

這個索引標籤會以樹狀子目錄顯示資訊，並且包含所有軟體計量規則。 它會將每個規則顯示為一個節點，節點是以檔案名稱和規則識別碼來識別。 展開樹狀目錄中的每個節點，並檢視下列資訊：
- 總管檔案名稱 
- 原始檔案名稱
- 規則識別碼
- 檔案版本
- 語言


