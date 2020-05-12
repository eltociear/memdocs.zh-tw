---
title: 自訂資料庫檔案位置
titleSuffix: Configuration Manager
description: 了解如何指定 SQL Server 資料庫檔案的自訂位置。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d3f01e54ba196ee9c27295d8f970a7dbe352f63f
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906184"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Configuration Manager 站台資料庫檔案的自訂位置

適用於：  Configuration Manager (最新分支)

 Configuration Manager 支援 SQL Server 資料庫檔案的自訂位置。  

> [!NOTE]  
>  當您使用 SQL Server 叢集時，無法使用指定非預設檔案位置的選項。  

 在新的主要站台或管理中心網站之**安裝期間**，您可以：  

-   **為站台資料庫指定非預設的檔案位置**：Configuration Manager 安裝程式隨後會使用這些位置來建立站台資料庫。  

-   **指定採用使用自訂檔案位置之預先建立的 SQL Server 資料庫**：Configuration Manager 安裝程式隨後會使用預先建立的資料庫及其預先設定的檔案位置。  

**安裝之後**，您可變更站台資料庫檔案的位置。 這必須停止站台及編輯 SQL Server 中的檔案位置：  

-   在 Configuration Manager 站台伺服器上，停止 **SMS_Executive** 服務。  

-   如需如何移動使用者資料庫的詳細資訊，請參閱[移動使用者資料庫](https://docs.microsoft.com/sql/relational-databases/databases/move-user-databases?view=sql-server-2014) \(部分機器翻譯\)。  

-   移動好資料庫檔案之後，請重新啟動 Configuration Manager 站台伺服器上的 **SMS_Executive** 服務。  
