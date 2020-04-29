---
title: 針對應用程式部署進行疑難排解的技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 中應用程式部署進行疑難排解的技術參考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688866"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Configuration Manager 中應用程式部署的技術參考

適用於：  Configuration Manager (最新分支)

在本文中，您將了解應用程式的部署如何運作。

## <a name="before-you-begin"></a>開始之前

當部署了疑難排解應用程式之後，有多個項目可讓您用於檢閱用戶端記錄。 這些項目包括：

- 應用程式的 CI 識別碼
- 應用程式的唯一識別碼
- 部署類型的唯一識別碼
- 應用程式部署的唯一識別碼 (也稱為指派的唯一識別碼)
- 應用程式部署目的
- 內容的唯一識別碼
- 集合識別碼與名稱
- 集合類型

若要簡化疑難排解，可以對 Configuration Manager 資料庫，執行類似如下的 SQL 查詢，以取得上列資訊。

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> 執行此查詢時，**必須**使用在應用程式屬性之一般資訊索引標籤中所列的應用程式名稱，而不是使用在應用程式屬性之 [軟體中心] 索引標籤內所列之當地語系化的應用程式名稱。

## <a name="next-steps"></a>後續步驟

- [應用程式部署原則](deployment-policy-technical-reference.md)
