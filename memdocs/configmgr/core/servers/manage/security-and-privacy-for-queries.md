---
title: 查詢的安全性和隱私權
titleSuffix: Configuration Manager
description: 當您查詢站台資料庫中的資訊時，請了解安全性和隱私權的最佳做法。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695696"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Configuration Manager 中的查詢安全性與隱私權

適用於：  Configuration Manager (最新分支)

Configuration Manager 的查詢可讓您依據指定的準則，從站台資料庫擷取資訊。 Configuration Manager 會在標準作業期間收集站台資料庫資訊。 例如，使用已從探索或清查過程中收集的資訊，您可以設定查詢來識別符合指定的準則的裝置。  

 如需查詢的詳細資訊，請參閱[查詢簡介](../../../core/servers/manage/introduction-to-queries.md)。 如需使用查詢擷取收集資料之 Configuration Manager 作業的安全性最佳做法和隱私權資訊，請參閱 [Configuration Manager 的安全性和隱私權](../../../core/plan-design/security/security-and-privacy.md)。  

## <a name="security-best-practices-for-queries"></a>查詢的安全性最佳做法

 為查詢使用此安全性最佳做法。  

|安全性最佳做法|更多資訊|  
|----------------------------|----------------------|  
|當您要匯出或匯入儲存在網路位置的查詢時，請保護該位置和網路通道。|限制誰可以存取網路資料夾。<br /><br /> 使用在網路位置和站台伺服器之間的伺服器訊息區 (SMB) 簽署或網際網路通訊協定安全性 (IPsec)，在匯入前防止攻擊者竄改查詢資料。|  

## <a name="next-steps"></a>後續步驟
  
[Configuration Manager 的安全性和隱私權](../../../core/plan-design/security/security-and-privacy.md)
