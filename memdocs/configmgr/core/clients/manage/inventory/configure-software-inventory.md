---
title: 設定軟體清查
titleSuffix: Configuration Manager
description: 設定軟體清查，並在 Configuration Manager 中排除軟體清查的資料夾。
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6fcf4736c30d8743d0d26b52aac60ef12b5c9cd
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906304"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>如何在 Configuration Manager 中設定軟體清查

適用於：  Configuration Manager (最新分支)

這個程序會設定軟體清查的預設用戶端設定，並套用至階層中的所有電腦。 如果您只想要將這些設定套用至部分電腦，請建立自訂裝置用戶端設定，並將它指派給集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱[如何設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)。   

## <a name="to-configure-software-inventory"></a>設定軟體清查  

1. 在 Configuration Manager 主控台中，選擇 [系統管理]   > [用戶端設定]  [預設用戶端設定]  。  

2. 在 [首頁]  索引標籤的 [內容]  群組中，選擇 [內容]  。  

3. 在 [預設設定]  對話方塊中，選擇 [軟體清查]  。  

4. 在 [裝置設定]  清單中，設定下列值：  

   -   **在用戶端上啟用軟體清查** - 從下拉式清單中選取 [True]  。  

   -   **排程軟體清查和檔案收集** - 設定用戶端收集軟體清查和檔案的間隔。   

5. 設定您需要的用戶端設定。 [關於用戶端設定](../../../../core/clients/deploy/about-client-settings.md)一文的[軟體清查](../../../../core/clients/deploy/about-client-settings.md#software-inventory)一節中包含用戶端設定清單。  

   用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則擷取，請參閱[如何管理用戶端](../../../../core/clients/manage/manage-clients.md)。  

   > [!TIP]
   >   inventoryprovider.log 中的錯誤碼 80041006 表示 WMI 提供者的記憶體不足。 亦即，已叫用提供者的記憶體配額限制，而且清查提供者無法繼續。
   > 在此情況下，清查代理程式所建立的報表具有 0 個項目，因此不會回報任何清查項目。 <br/>
   > 此錯誤的可能解決方案會是減少軟體清查收集的範圍。 在限制清查範圍之後發生錯誤的環境中，增加 [_ProviderHostQuotaConfiguration](https://docs.microsoft.com/windows/win32/wmisdk/--providerhostquotaconfiguration) 類別中所定義的 [MemoryPerHost](https://techcommunity.microsoft.com/t5/ask-the-performance-team/memory-and-handle-quotas-in-the-wmi-provider-service/ba-p/373319) 屬性可以提供解決方案。

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>排除資料夾不進行軟體清查  

1.  使用 Notepad.exe，建立名為 **Skpswi.dat**的空白檔案。  

2.  以滑鼠右鍵按一下 **Skpswi.dat** 檔案，然後按一下 [內容]  。 在 Skpswi.dat 檔案的檔案內容中，選取 [隱藏]  屬性。  

3.  將 **Skpswi.dat** 檔案放在您想要排除不進行軟體清查之每個用戶端硬碟機或資料夾結構的根目錄。  

> [!NOTE]  
>  除非從用戶端電腦的用戶端磁碟機中刪除這個檔案，否則軟體清查不會重新清查磁碟機。
