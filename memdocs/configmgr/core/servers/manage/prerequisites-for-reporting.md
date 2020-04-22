---
title: 報告的必要條件
titleSuffix: Configuration Manager
description: 了解影響您在 Configuration Manager 中使用報告的各種相依性。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e08833a5ef560a0f958fe68b4ade0d4717dffc73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703516"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Configuration Manager 中的報告必要條件

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的報告具有下列相依性：

- SQL Server Reporting Services
- Reporting Services 點
- Power BI 報表伺服器 (選擇性，從 2002 版開始)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

您必須先安裝和設定 SQL Server Reporting Services，才能在 Configuration Manager 中使用報告。

如需規劃和部署 Reporting Services 的詳細資訊，請參閱[安裝 SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services)。

在 64 位元 SQL Server 安裝的預設執行個體或具名執行個體上安裝 Reporting Services 資料庫。 將 SQL Server 執行個體與站台系統伺服器共置，或在遠端電腦上進行設定。

Configuration Manager 支援與站台資料庫相同的 SQL Server 版本來進行報告。 如需詳細資訊，請參閱[支援的 SQL Server 版本](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)。

## <a name="reporting-services-point"></a>Reporting Services 點

必須先設定 Reporting Services 點站台系統角色，才能在 Configuration Manager 中使用報告。

如需詳細資訊，請參閱 [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint) (站台和站台系統必要條件)。

## <a name="power-bi-report-server"></a>Power BI 報表伺服器

從 2002 版開始，可將報告與 Power BI 報表伺服器整合。 如需包含先決條件的詳細資訊，請參閱[與 Power BI 報表伺服器整合](powerbi-report-server.md)。

## <a name="next-steps"></a>後續步驟

[設定報告](configuring-reporting.md)
