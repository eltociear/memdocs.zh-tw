---
title: 監視 Linux/UNIX 用戶端
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中監視 Linux 和 UNIX 伺服器上的用戶端。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696766"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>如何在 Configuration Manager 中監視 Linux 和 UNIX 伺服器上的用戶端

適用於：  Configuration Manager (最新分支)

> [!Important]  
> 從 1902 版開始，Configuration Manager 不支援 Linux 或 UNIX 用戶端。 
> 
> 請考慮以 Microsoft Azure 管理來管理 Linux 伺服器。 Azure 解決方案具有廣泛的 Linux 支援，在大部分情況下都超越 Configuration Manager 的功能性，包括 Linux 的完整修補程式管理。

您可以在 Configuration Manager 主控台檢視來自 Linux 和 UNIX 伺服器的資訊，所使用的方法與用來檢視 Windows 型用戶端資訊的方法相同。  

 您可以檢視的這些資訊包括：  

- 來自用戶端的狀態詳細資料，位於 Configuration Manager 主控台儀表板  

- 預設 Configuration Manager 報告中的用戶端詳細資料  

- 資源總管中的清查詳細資料  

  下列小節說明如何透過資源總管和報告取得這些詳細資訊。  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a> 使用資源總管來檢視 Linux 和 UNIX 伺服器的清查  

 Configuration Manager 用戶端將硬體清查提交給 Configuration Manager 站台之後，您可以使用資源總管檢視這項資訊。 Linux 和 UNIX 的 Configuration Manager 用戶端不會將新的清查類別或檢視新增至資源總管。 Linux 和 UNIX 清查資料對應至現有的 WMI 類別。 您可以使用資源總管，在 Windows 架構的分類中檢視 Linux 和 UNIX 伺服器的清查詳細資料。  

 例如，您可以收集 Linux 和 UNIX 伺服器上找到的所有原生安裝程式清單。 原生安裝程式的範例包括在 Linux 或 **.pkgs** Solaris 中的 **.rpms** 。 Linux 或 UNIX 用戶端已提交清查之後，您可以在 Configuration Manager 主控台的資源總管中檢視所有原生安裝的 Linux 或 UNIX 程式清單。  

 如需如何使用資源總管的相關資訊，請參閱[如何使用資源總管檢視硬體清查](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> 如何使用報告檢視 Linux 和 UNIX 伺服器的資訊  
 Configuration Manager 的報告包含 Linux 和 UNIX 伺服器的資訊，以及 Windows 電腦的資訊。 不需其他組態，也能將 Linux 和 UNIX 資料整合在報表中。  

 例如，如果您執行名為 [計算作業系統版本] 的報表時，它會顯示不同的作業系統和執行每個作業系統的用戶端數目清單。 報告根據執行不同作業系統的不同 Configuration Manager 用戶端所傳送的硬體清查資訊而定。  

 此外，也可以建立 Linux 和 UNIX 伺服器資料特定的自訂報表。 硬體清查類別 **作業系統** 的 **標題** 屬性，是實用的屬性，可讓您識別在報表查詢中的特定作業系統。  

 如需 Configuration Manager 中報表的資訊，請參閱[報告簡介](../../servers/manage/introduction-to-reporting.md)。  
