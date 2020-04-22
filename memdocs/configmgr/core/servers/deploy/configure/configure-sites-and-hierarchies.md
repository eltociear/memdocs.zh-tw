---
title: 設定站台和階層
titleSuffix: Configuration Manager
description: 請參閱這份檢查清單，確保考慮到對站台和階層皆有影響的最常見設定。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704676"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>為 Configuration Manager 設定站台和階層

適用於：  Configuration Manager (最新分支)

安裝第一個 Configuration Manager 站台，或將其他站台新增至您的階層之後，使用此檢查清單可確保您考慮到會影響站台與階層的最常見設定。  

下列設定注意事項適用於大部分的部署：  

- 但有些選項是彼此相依的，例如 Active Directory 樹系探索、界限以及界限群組。  

- 其中有一些設定有預設值，無須任何設定變更即可使用 (至少開始)。  

- 其他設定 (例如界限群組與發佈點群組) 則必須先設定之後才能使用。  

| 動作 | 詳細資料 |  
|------------|-------------|  
| 設定以角色為基礎的系統管理 | 分隔系統管理的指派，以控制哪些系統管理使用者可以在 Configuration Manager 環境中檢視及管理不同的物件與資料。<br /><br /> 階層中的所有站台，會共用以角色為基礎之系統管理的組態。   <br/><br/>如需詳細資訊，請參閱[設定以角色為基礎的系統管理](configure-role-based-administration.md)。 |  
| 將站台資料發佈至 Active Directory Domain Services | 讓用戶端輕鬆找到服務，並有效率地使用站台資源。<br /><br /> 先[擴充 Active Directory 架構](../../../plan-design/network/extend-the-active-directory-schema.md)。 接著個別設定每個站台來[發佈站台資料](publish-site-data.md) |  
| 設定服務連接點 | 規劃在階層的頂層站台安裝及設定服務連接點。 如需詳細資訊，請參閱 [About the service connection point](about-the-service-connection-point.md) (關於服務連接點)。 |  
| 新增站台系統角色 | 為各個站台安裝一個或多個額外的站台系統角色。 如需詳細資訊，請參閱[安裝站台系統角色](add-site-system-roles.md)。 |  
| 設定界限與界限群組 | 指定界限以在您的內部網路上定義網路位置，其中可包含您要管理的裝置。 然後設定界限群組，讓位於那些網路位置的用戶端可以找到 Configuration Manager 資源。 如需詳細資訊，請參閱[定義站台界限與界限群組](define-site-boundaries-and-boundary-groups.md)。 |  
| 設定發佈點群組 | 設定發佈點的邏輯群組，讓管理部署更容易。 如需詳細資訊，請參閱[管理發佈點群組](install-and-configure-distribution-points.md#bkmk_manage)。 |  
| 執行探索工作 | 執行探索以在網路上尋找資源，包括網路基礎結構、裝置與使用者。<br /><br /> 如需詳細資訊，請參閱[執行探索](run-discovery.md)。 |  
| 為系統管理員新增備援和容量 | 安裝其他 SMS 提供者與 Configuration Manager 主控台，為管理基礎結構的系統管理員擴充容量：<br /><br /> **安裝其他 SMS 提供者**可為站台的主控台和 API 連線提供備援。 如需詳細資訊，請參閱[管理 SMS 提供者](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。<br /><br /> **安裝其他 Configuration Manager 主控台**可為額外的系統管理使用者提供存取。 如需詳細資訊，請參閱[安裝 Configuration Manager 主控台](../install/install-consoles.md)。 |  
| 設定站台元件 | 在每個站台設定站台元件，以修改站台系統角色與站台狀態報告的行為。 如需詳細資訊，請參閱[站台元件](site-components.md)。 |  
| 建立自訂集合 | 請使用站台探索到的裝置與使用者相關資訊，建立物件的自訂集合，以簡化日後的管理工作。 如需詳細資訊，請參閱[如何建立集合](../../../clients/manage/collections/create-collections.md)。 |  
| 設定管理高風險部署的設定 | 在系統管理者建立高風險的部署時，會對其發出警告的站台上指定這些設定。 如需詳細資訊，請參閱 [Settings to manage high-risk deployments](../../manage/settings-to-manage-high-risk-deployments.md) (高風險部署的管理設定)。 |  
| 為管理點設定資料庫複本 | 設定資料庫複本，以減少管理點在服務來自用戶端的要求時，加諸站台資料庫伺服器的處理器負載。 如需詳細資訊，請參閱[管理點的資料庫複本](database-replicas-for-management-points.md)。 |  
| 設定 SQL Server Always On 可用性群組 | 將可用性群組設定為在主要站台及管理中心網站裝載站台資料庫的高可用性和災害復原方案。 如需詳細資訊，請參閱[適用於高可用性站台資料庫的 SQL Server AlwaysOn](sql-server-alwayson-for-a-highly-available-site-database.md)。 |  
| 修改站台間的複寫 | 請參閱[站台間的資料轉送](../../../plan-design/hierarchy/data-transfers-between-sites.md)以了解下列主題：<br /><br /> 設定次要站台之間的[檔案式複寫](../../../plan-design/hierarchy/file-based-replication.md)<br /><br /> 設定[資料庫複寫連結](../../../plan-design/hierarchy/database-replication.md)<br /><br /> 設定[分散式檢視](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| 以被動模式設定站台伺服器 | 從 1806 版開始，針對每個主要站台和管理中心網站以被動模式設定站台伺服器。 這項功能提供高可用性站台伺服器。 如需詳細資訊，請參閱[站台伺服器高可用性](site-server-high-availability.md)。 |  
