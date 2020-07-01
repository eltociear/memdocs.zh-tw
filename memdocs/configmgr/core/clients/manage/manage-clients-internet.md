---
title: 管理網際網路上的用戶端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用雲端管理閘道和以網際網路為基礎的用戶端管理來管理用戶端。
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715589"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>使用 Configuration Manager 管理網際網路上的用戶端

適用於：Configuration Manager (最新分支)

一般來說，在 Configuration Manager 中，大部分受管理的電腦和伺服器實際上是與執行管理功能的站台系統伺服器位於相同的內部網路。 不過，您可以管理內部網路之外的用戶端 (如果它們連線到網際網路)。 這項功能並不需要用戶端透過 VPN 連線，才能連線到站台系統伺服器。

Configuration Manager 提供下列兩種方式來管理連接網際網路的用戶端：

- 雲端管理閘道

- 以網際網路為基礎的用戶端管理

> [!NOTE]
> 您可以為單一網站結合這兩個服務。 如果裝置從網站取得 IBCM 和 CMG 的原則，其會在兩者之間隨機分配以進行通訊。 控制通訊的唯一可用機制是用戶端驗證。 例如，如果已加入 Azure AD 的用戶端不信任網際網路型管理點的伺服器驗證憑證，則只能使用 CMG。 如果加入網域的用戶端不信任 CMG 的伺服器驗證憑證，其只能使用網際網路型管理點。<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>雲端管理閘道

雲端管理閘道提供網際網路用戶端的管理。 其使用 Microsoft Azure 雲端服務與會與該服務通訊之內部部署站台系統角色的組合。 以網際網路為基礎的用戶端則使用雲端服務與內部部署 Configuration Manager 通訊。

### <a name="cmg-advantages"></a>CMG 的優點

- 不需要任何額外的內部部署基礎結構投資。  

- 不會將內部部署基礎結構公開至網際網路。  

- 執行服務的雲端虛擬機器完全受 Azure 的管理，而且不需要維護。  

- 可在 Configuration Manager 主控台中輕鬆進行設定。  

### <a name="cmg-disadvantages"></a>CMG 的缺點  

- 雲端訂閱成本。  

- 會透過雲端服務傳送管理資料。  

如需詳細資訊，請參閱[規劃雲端管理閘道](cmg/plan-cloud-management-gateway.md)。  

## <a name="internet-based-client-management"></a>以網際網路為基礎的用戶端管理

此方法需仰賴網際網路面向站台系統伺服器 (用戶端與其直接進行通訊) 以進行管理。 您必須針對用戶端與站台系統伺服器進行相關設定，才能執行以網際網路為基礎的用戶端管理 (IBCM)。

### <a name="ibcm-advantages"></a>IBCM 的優點

- 無任何雲端服務相依性。  

- 無任何雲端訂閱的額外相關成本。  

- 可完整控制提供服務的伺服器和角色。  

### <a name="ibcm-disadvantages"></a>IBCM 的缺點

- 需要額外的基礎結構投資。  

- 額外基礎結構會造成其他負荷和營運成本。  

- 基礎結構必須公開到網際網路。  

如需詳細資訊，請參閱[規劃以網際網路為基礎的用戶端管理](plan-internet-based-client-management.md)。  
