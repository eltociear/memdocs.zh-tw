---
title: 如何使用資源總管
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用資源總管檢視硬體清查。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690096"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>如何在 Configuration Manager 中使用資源總管檢視硬體清查

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中使用資源總管檢視硬體清查的相關資訊。 站台會從您階層中的用戶端收集這項資訊。  

> [!Tip]  
>  在您要連線的用戶端上執行硬體清查週期之前，資源總管不會顯示任何資料。  



## <a name="overview"></a>概觀

資源總管包含與硬體清查相關的下列區段：  

- **硬體**：顯示從指定用戶端裝置收集來的最新硬體清查。  

    - [工作站狀態]  節點會顯示裝置上次硬體清查的時間和日期。  

- **硬體歷程記錄**：自上次硬體清查週期後所變更的清查項目歷程記錄。  

    - 您可以展開某個項目，查看 [目前]  節點以及一或多個具有過去日期的節點。 比較目前節點與其中一個歷程記錄節點中的資訊，即可查看已變更的項目。  

> [!NOTE]  
> 根據預設，Configuration Manager 會刪除 90 天未使用的硬體清查資料。 您可以在 [刪除過時清查歷程記錄]  站台維護工作中調整此天數。 如需詳細資訊，請參閱[維護工作](../../../servers/manage/maintenance-tasks.md)。  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a> 如何開啟 [資源總管]   

1.  在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [裝置]  節點。 您也可以在 [裝置集合]  節點中選取任何集合。  

2.  選取一個裝置。 在功能區的 [首頁]  索引標籤和 [裝置]  群組上，按一下 [開始]  ，然後選取 [資源總管]  。   

> [!Tip]  
> 在 [資源總管] 中，以滑鼠右鍵按一下右側結果窗格中的項目，以執行其他動作。 按一下 [內容]  以其他格式來檢視該項目。  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a> 使用大整數值
<!--1357880-->
在 Configuration Manager 1802 版和舊版中，硬體清查對大於 4,294,967,296 (2^32) 的整數具有限制。 硬碟大小 (位元組) 此類的屬性，可能會達到此限制。 管理點無法處理超過此限制的整數值，因此沒有值儲存在資料庫中。 

從 1806 版開始，此限制已增加至 18,446,744,073,709,551,616 (2^64)。 

如果屬性帶有一個不會變更的值，例如磁碟大小總計，在升級站台之後，您可能無法立即看到該值。 大部分的硬體清查是一種差異報表。 用戶端只會傳送能變更的值。 若要解決此問題，請加入另一個屬性至相同的類別。 這個動作會導致用戶端將類別中所有已變更的屬性，予以更新。 



## <a name="see-also"></a>請參閱

如需如何檢視執行 Linux 與 UNIX 之用戶端的硬體清查資訊，請參閱[如何監視 Linux 和 UNIX 伺服器的用戶端](../monitor-clients-for-linux-and-unix-servers.md)。  

[資源總管] 也會顯示軟體清查。 如需詳細資訊，請參閱[如何使用 [資源總管] 檢視軟體清查](use-resource-explorer-to-view-software-inventory.md)。
