---
title: 電源管理的安全性與隱私權
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 中電源管理的安全性和隱私權資訊。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696506"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Configuration Manager 中電源管理的安全性與隱私權

適用於：  Configuration Manager (最新分支)

本主題包含 Configuration Manager 中電源管理的安全性和隱私權資訊。  

## <a name="security-best-practices-for-power-management"></a>電源管理的安全性最佳做法  
 電源管理沒有任何安全性相關的最佳做法。  

## <a name="privacy-information-for-power-management"></a>電源管理的隱私權資訊  
 電源管理使用 Windows 來監視電源使用量和套用至電腦的電源設定上班時間和非商務小時期間內建的功能。 Configuration Manager 會從電腦收集電源使用量資訊，包含使用者何時使用電腦的相關資料。 雖然 Configuration Manager 監視集合的電源使用量不是每一部電腦的使用量，但是集合可以只包含一部電腦。 電源管理預設不啟用，而且必須由系統管理員設定。  

 電源使用量資訊存放在 Configuration Manager 資料庫中，且不會傳送給 Microsoft。 詳細資訊會在資料庫中保留 31 天，摘要資訊會保留 13 個月。 您可以設定刪除間隔。  

 在您設定電源管理之前，請先考慮隱私權需求。  
