---
title: 管理網際網路上的用戶端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用雲端管理閘道和以網際網路為基礎的用戶端管理來管理用戶端。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690026"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>使用 Configuration Manager 管理網際網路上的用戶端

適用於：  Configuration Manager (最新分支)

一般來說，在 Configuration Manager 中，大部分受管理的電腦和伺服器實際上是與執行管理功能的站台系統伺服器位於相同的內部網路。 不過，您可以管理內部網路之外的用戶端 (如果它們連線到網際網路)。 這項功能並不需要用戶端透過 VPN 連線，才能連線到站台系統伺服器。

Configuration Manager 提供下列兩種方式來管理連接網際網路的用戶端：

-   雲端管理閘道

-   以網際網路為基礎的用戶端管理


## <a name="cloud-management-gateway"></a>雲端管理閘道

雲端管理閘道提供網際網路用戶端的管理。 它使用 Microsoft Azure 雲端服務，並結合新的站台系統角色與該服務通訊。 以網際網路為基礎的用戶端則使用雲端服務與內部部署 Configuration Manager 通訊。

#### <a name="advantages"></a>優點  

-   不需要任何額外的內部部署基礎結構投資。  

-   不會將內部部署基礎結構公開至網際網路。  

-   執行服務的雲端虛擬機器完全受 Azure 的管理，而且不需要維護。  

-   可在 Configuration Manager 主控台中輕鬆進行設定。  

#### <a name="disadvantages"></a>缺點  

-   雲端訂閱成本。  

-   會透過雲端服務傳送管理資料。  

如需詳細資訊，請參閱[規劃雲端管理閘道](cmg/plan-cloud-management-gateway.md)。  



## <a name="internet-based-client-management"></a>以網際網路為基礎的用戶端管理

這個方法需仰賴連結網際網路的站台系統伺服器 (用戶端與其進行通訊) 以進行管理。 您必須針對用戶端和站台系統伺服器進行相關設定，才能執行以網際網路為基礎的管理。

#### <a name="advantages"></a>優點  

-   無任何雲端服務相依性。  

-   無任何雲端訂閱的額外相關成本。  

-   可完整控制提供服務的伺服器和角色。  

#### <a name="disadvantages"></a>缺點  

-   需要額外的基礎結構投資。  

-   額外基礎結構會造成其他負荷和營運成本。  

-   基礎結構必須公開到網際網路。  

如需詳細資訊，請參閱[規劃以網際網路為基礎的用戶端管理](plan-internet-based-client-management.md)。  
