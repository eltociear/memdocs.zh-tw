---
title: 集合安全性和隱私權
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 中集合的安全性與隱私權最佳做法。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695526"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Configuration Manager 中集合的安全性與隱私權

適用於：  Configuration Manager (最新分支)

本主題包含 Configuration Manager 中集合的安全性最佳做法和隱私權資訊。  

 沒有專門針對 Configuration Manager 集合的隱私權資訊。 集合是資源的容器，例如使用者和裝置。 集合成員資格通常依賴 Configuration Manager 在標準作業期間所收集的資訊。 例如，透過使用從探索或清查收集到的資源資訊，集合可以設定成包含符合指定準則的裝置。 集合也可以用戶端管理作業目前的狀態資訊為基礎，例如部署軟體和檢查相容性。 除了這些以查詢為基礎的集合，系統管理員的使用者也可以新增資源至集合。  

 如需集合的詳細資訊，請參閱[集合簡介](../../../../core/clients/manage/collections/introduction-to-collections.md)。 如需可用於設定集合成員資格之 Configuration Manager 作業的安全性最佳作法詳細資訊和隱私權資訊，請參閱 [Configuration Manager 的安全性最佳做法和隱私權資訊](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md)。  

## <a name="security-best-practices-for-collections"></a>集合的安全性最佳做法  
 請使用下列集合安全性最佳做法。  

|安全性最佳做法|更多資訊|  
|----------------------------|----------------------|  
|當您使用儲存在網路位置的受管理物件格式 (MOF) 檔案匯出或匯入集合時，請保護位置和網路通道。|限制存取網路資料夾的人員。<br /><br /> 使用在網路位置和站台伺服器之間的伺服器訊息區 (SMB) 簽署或網際網路通訊協定安全性 (IPsec)，防止攻擊者竄改匯出的集合資料。 在網路上使用 IPsec 為資料加密，以防止洩露資訊。|  

### <a name="security-issues-for-collections"></a>集合的安全性問題  
 集合有下列安全性問題：  

-   如果您使用集合變數，本機系統管理員可以讀取潛在的敏感資訊。  

     當您部署作業系統時，可以使用集合變數。  
