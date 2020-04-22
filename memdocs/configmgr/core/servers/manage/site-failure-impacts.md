---
title: 站台失敗影響
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站台中各種失敗的影響。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708566"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Configuration Manager 中的站台失敗影響

適用於：  Configuration Manager (最新分支)

站台伺服器和任何其他站台系統都可能會失敗，因而導致遺失它們定期提供的服務。 如果您在相同的電腦上安裝多個站台系統，而且該電腦失敗，將無法再使用這些站台系統定期提供的所有服務。

規劃程序有部分應該包含了解對您提供給組織之服務的影響。 站台中的每個站台系統都提供不同的功能；因此，根據失敗站台系統的角色，站台上的失敗影響也會不同。 

使用[高可用性選項](../deploy/configure/high-availability-options.md)協助降低任何單一系統的失敗。 也會規劃和練習[備份和復原](backup-and-recovery.md)策略，以減少無法使用服務的時間長度。

下列各節描述所指定站台系統無法運作時的影響：


### <a name="site-server"></a>網站伺服器

- 無法管理站台。 您無法將主控台連線至站台。  

- 管理點會收集用戶端資訊，並在站台伺服器重新上線之前予以快取。  

- 使用者可以執行現有部署，而用戶端可以從發佈點下載內容。  


### <a name="site-database"></a>網站資料庫

- 無法管理站台。  

- 如果 Configuration Manager 用戶端已具有含新原則的原則指派，而且如果管理點已快取原則本文，則用戶端可以提出原則本文要求，並接收原則本文回覆。 不過，站台無法服務任何新的原則指派要求。  

- 只有在用戶端已收到原則並且已將相關聯的來源檔案快取至用戶端本機時，用戶端才能執行部署。  


### <a name="management-point"></a>管理點

- 雖然您可以建立新的部署，但是用戶端在管理點上線之前不會收到新的部署。  

- 用戶端仍然會收集清查、軟體計量和狀態資訊。 在管理點可用之前，它們會在本機儲存此資料。  

- 只有在用戶端已收到原則並且已將相關聯的來源檔案快取至用戶端本機時，用戶端才能執行部署。  


### <a name="distribution-point"></a>發佈點

- 只有已在本機下載相關聯的來源檔案或來源檔案可在對等來源上使用時，Configuration Manager 用戶端才能執行部署。

