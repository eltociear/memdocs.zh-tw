---
title: 多語系支援
titleSuffix: Configuration Manager
description: 設定 Configuration Manager 以符合特定的國際需求。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704596"
---
# <a name="international-support-in-configuration-manager"></a>Configuration Manager 中的多語系支援

適用於：  Configuration Manager (最新分支)

下列各節提供的技術詳細資料可協助您設定 Configuration Manager，使其符合特定國際的需求。  

## <a name="gb18030-requirements"></a>GB18030 需求  
 Configuration Manager 符合 GB18030 中定義的標準，因此您可以在中國使用 Configuration Manager。 符合 GB18030 需求的 Configuration Manager 部署必須使用下列設定：  

-   使用 Configuration Manager 時，所用的每一台站台伺服器電腦和 SQL Server 電腦都必須使用中文作業系統。  

-   階層中的每個站台資料庫和每個 SQL Server 執行個體都必須使用相同的集合，而且必須為下列其中之一：  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  這些資料庫定序是 [Configuration Manager 的 SQL Server 版本支援](../../../core/plan-design/configs/support-for-sql-server-versions.md)中所述需求的例外狀況。  

-   您必須將名為 **GB18030.SMS** 的檔案置於階層中每台站台伺服器電腦系統磁碟區的根資料夾中。 此檔案不含任何資料，而且可以是根據此需求命名的空白文字檔。  
