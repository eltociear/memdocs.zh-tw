---
title: 管理 Windows 10 快速更新
titleSuffix: Configuration Manager
description: Configuration Manager 支援 Windows 10 的快速安裝檔案，可在用戶端上提供更小的下載並縮短安裝時間。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4093eafe9f8a337ce322165a529f630a759b365f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701376"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>管理適用於 Windows 10 更新的快速安裝檔案

Configuration Manager 支援適用於 Windows 10 更新的快速安裝檔案。 將用戶端設定為僅下載本月 Windows 10 累積品質更新與上個月更新之間的變動部分。 如果沒有快速安裝檔案，Configuration Manager 用戶端就會每月下載完整的 Windows 10 累積更新 (其中包括先前月份的所有更新)。 使用快速安裝檔案可在用戶端提供較小的下載項目及更快速的安裝時間。

若要了解如何使用 Configuration Manager 來管理更新內容，以便讓 Windows 10 保持最新狀態，請參閱[將 Windows 10 更新傳遞最佳化](optimize-windows-10-update-delivery.md)。  


> [!IMPORTANT]  
> Windows 10 1607 版及更新過的 Windows Update 代理程式提供了此作業系統用戶端支援。 這個更新會隨附在 2017 年 4 月 11 日發行的更新之中。 如需這些更新的詳細資訊，請參閱[支援文章 4015217](https://support.microsoft.com/kb/4015217)。 未來的更新會運用快速功能以提供較小的下載項目。 Windows 10 的舊版本以及不含此更新的 Windows 10 1607 版皆不支援快速安裝檔案。  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>讓站台可以下載 Windows 10 更新的快速安裝檔案
若要開始同步 Windows 10 快速安裝檔案的中繼資料，請在軟體更新點內容中加以啟用。  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取管理中心網站或獨立主要站台。  

3. 在功能區中，依序按一下 [設定站台元件]  和 [軟體更新點]  。 切換至 [更新檔案]  索引標籤，然後選取 [下載所有核准更新的完整檔案和 Windows 10 的快速安裝檔案]  。

> [!NOTE]    
> 您無法將軟體更新點元件設定為僅  下載快速更新。  除了完整檔案之外，這個站台還會下載快速安裝檔案。 這樣會增加內容庫中儲存的內容量，也會增加發佈至發佈點和發佈點上儲存的內容量。

> [!Tip]  
> 若要確定各個檔案實際使用的磁碟空間，請檢查檔案的**磁碟大小**屬性。 「磁碟大小」屬性應該比「大小值」小得的多。 如需詳細資訊，請參閱 [Windows 10 更新傳遞最佳化常見問答集](optimize-windows-10-update-delivery.md#bkmk_faq)。  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>讓用戶端可以下載並安裝快速安裝檔案
若要啟用用戶端的快速安裝檔案支援，請在用戶端設定的**軟體更新**群組中啟用快速安裝檔案。 這個設定會建立新的 HTTP 接聽程式，以在指定的連接埠上接聽下載快速安裝檔案的要求。

> [!NOTE]    
> 這是用戶端的本機連接埠，可用來接聽來自傳遞最佳化或背景智慧型傳送服務 (BITS) 的要求，以便從發佈點下載快速內容。 您不需要在防火牆上開啟此連接埠，因為所有流量都在本機電腦上。  

在您部署用戶端設定以在用戶端上啟用這項功能之後，該功能會嘗試下載目前月份的 Windows 10 累積更新與上個月更新之間的差異。 用戶端必須要執行能支援快速安裝檔案的 Windows 10 版本。  

1. 在軟體更新點元件內容 (上一個程序) 中啟用快速安裝檔案的支援。  

2. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，然後選取 [用戶端設定]  。  

3. 選取適當的用戶端設定，然後按一下功能區中的 [內容]  。  

4. 選取 [軟體中心]  群組。 將 [啟用用戶端上的快速更新安裝]  設定成 [是]  。 將 [下載快速更新所需內容時會用到的連接埠]  設定成用戶端 HTTP 接聽程式會用到的連接埠。
    - 在 1902 版中，**用以下載 Express Update 內容的連接埠**已變更為**用戶端用以接收差異內容要求的連接埠**。

## <a name="next-steps"></a>後續步驟

[部署軟體更新](deploy-software-updates.md)