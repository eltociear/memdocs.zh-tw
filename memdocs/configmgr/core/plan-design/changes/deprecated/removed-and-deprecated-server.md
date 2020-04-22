---
title: 站台伺服器的已淘汰項目
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 不再支援的站台伺服器產品和作業系統。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702566"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Configuration Manager 站台伺服器的已移除與已淘汰項目

適用於：  Configuration Manager (最新分支)

本文描述已從 Configuration Manager 站台伺服器移除支援的產品與作業系統，或在後續更新中將會移除 (已淘汰) 的產品與作業系統。 它會提早通知可能會影響您使用 Configuration Manager 的未來變更。  

這項資訊可能會在未來變更。 它可能不會包含每個已淘汰的功能、產品或作業系統。  

## <a name="server-os"></a>伺服器 OS  

|作業系統|首次宣布的淘汰項目|移除的支援|
|-|-|-|
|Windows Server 2008 R2 包含 SP1|2015 年 7 月 10 日| 版本 1702|
|Windows Server 2008 SP2|2015 年 7 月 10 日|版本 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server 版本|首次宣布的淘汰項目|移除的支援|
|-|-|-|
|SQL Server 2008 R2|2015 年 7 月 10 日|版本 1702|
|SQL Server 2008|2015 年 7 月 10 日|版本 1511|

如果需要升級您的 SQL Server 版本，建議使用下列方法 (依複雜度由低到高排列)：

1. [就地升級 SQL Server](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (建議選項)。  

2. 在新電腦上安裝新的 SQL Server 版本。 接著，若要將您的站台伺服器指向新 SQL Server，請[使用 Configuration Manager 安裝程式的資料庫移動選項](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig)。  

3. 使用[備份及復原](../../../servers/manage/backup-and-recovery.md)。  

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱下列文章：

- [已移除和已取代](removed-and-deprecated.md)  

- [Microsoft 支援週期](https://support.microsoft.com/lifecycle)  

- [System Center Configuration Manager 最新分支版本支援](../../../servers/manage/current-branch-versions-supported.md)  
