---
title: 規劃站台資料庫
titleSuffix: Configuration Manager
description: 當您在規劃 Configuration Manager 階層時，請考慮站台資料庫及站台資料庫伺服器角色。
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a32f0a59a0b3ce3ad864fecf61fe7281b8ebbdd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704416"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>規劃 Configuration Manager 的站台資料庫

適用於：  Configuration Manager (最新分支)

站台資料庫伺服器是用來執行支援版本之 Microsoft SQL Server 的電腦。 SQL Server 則是用來儲存 Configuration Manager 站台的資訊。 Configuration Manager 階層中的每個網站都包含網站資料庫，以及獲指派網站資料庫伺服器角色的伺服器。  

-   針對管理中心網站和主要網站，您可以在網站伺服器上安裝 SQL Server，或者在網站伺服器以外的電腦上安裝 SQL Server。  

-   針對次要站台，您可以使用 SQL Server Express 安裝，而不是完整的 SQL Server 安裝。 不過，資料庫伺服器必須在次要站台伺服器上執行。  

-  針對 SQL 可用性群組用途，資料庫復原模式必須設定為 [完整]  

-  針對非 SQL 可用性群組用途，資料庫復原模式必須設定為 [簡易]  

如需 SQL 復原模式的進一步資訊，請參閱[復原模式 (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server)。

下列的 SQL Server 組態可以用來裝載站台資料庫：  

-   SQL Server 預設執行個體  

-   在執行 SQL Server 之單一電腦上的具名執行個體  

-   在 SQL Server 叢集執行個體上的具名執行個體  

-   SQL Server AlwaysOn 可用性群組 (自 Configuration Manager 1602 版開始)


若要裝載站台資料庫，SQL Server 必須符合 [Configuration Manager 的 SQL Server 版本支援](../../../core/plan-design/configs/support-for-sql-server-versions.md)中所述的需求。  



## <a name="remote-database-server-location-considerations"></a>遠端資料庫伺服器位置考量  

如果您使用遠端資料庫伺服器電腦，請確保中介網路連線為高可用性、高頻寬的網路連線。 站台伺服器與部分站台系統角色必須持續與裝載站台資料庫的遠端伺服器保持通訊，

-   而進行資料庫伺服器通訊所需的頻寬量，則因許多不同的站台和用戶端設定組合而異。 因此，實際需要的頻寬無法精準預測。  

-   每台執行 SMS 提供者的電腦，以及連線至網站資料庫的電腦，都會增加網路頻寬的需求。  

-   執行 SQL Server 的電腦所在網域，必須具有站台伺服器和所有執行 SMS 提供者的電腦之間的雙向信任。  

-   網站資料庫與網站伺服器共置時，您無法使用網站資料庫伺服器的叢集 SQL 伺服器。  


一般來說，站台系統伺服器僅支援來自單一 Configuration Manager 站台的站台系統角色。 不過，您可以使用不同 SQL Server 執行個體 (位於執行 SQL Server 的叢集或非叢集伺服器中) 來裝載來自不同 Configuration Manager 站台的資料庫。 若要支援來自不同網站的資料庫，您必須設定每個 SQL Server 執行個體使用通訊用的唯一連接埠。  
