---
title: 管理設定資料
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中建立設定項目和基準之後，您可以使用其他命令來執行各種動作。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: de8168d7d699998117eff8821929c654815f1a49
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692396"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>在 Configuration Manager 中管理設定資料

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中建立設定項目和設定基準之後，即可取得有利於執行不同動作的進一步命令。  

## <a name="manage-configuration-items"></a>管理設定項目  

-   在 [資產與相容性]  工作區中，展開 [相容性設定]   > [設定項目]  ，先選取要管理的設定項目，再選取管理工作。  

|管理工作|詳細資料|  
|---------------------|-------------|  
|**建立子設定項目**|開啟 [建立子設定項目精靈]  ，以在其中從選取的設定項目中建立子設定項目。<br /><br /> 您無法從行動裝置組態項目中建立子組態項目。<br /><br /> 如需詳細資訊，請參閱[建立子設定項目](../../compliance/deploy-use/create-child-configuration-items.md)。|  
|**修訂歷程記錄**|開啟 [設定項目修訂歷程記錄]  對話方塊，以在其中檢視和管理所選取設定項目的舊修訂版本。|  
|**檢視 XML 定義**|在新的視窗中，顯示所選取組態項目的 XML 定義檔。 當您想要手動撰寫組態資料時此資訊很有用。|  
|**匯出**|匯出封包 (.cab) 檔案格式的組態項目，但前提為於該站台上建立。 接著可以將它匯入相同或不同的 Configuration Manager 站台。 組態資料會轉換成 DCM 摘要。|  
|**複製**|使用您指定的名稱，建立一份所選取組態項目的複本。 新的組態項目不會保留任何原始組態項目的關聯性。 這表示重複的組態項目不會繼續從原始的設定項目繼承的組態資訊。|  
|**刪除**|開啟 [刪除設定項目]  對話方塊，以在其中檢閱這個設定項目的任何參考。<br /><br /> 您必須先移除組態項目的所有參考，才能刪除組態項目。|  

## <a name="manage-configuration-baselines"></a>管理設定基準  

-   在 [資產與相容性]  工作區中，展開 [相容性設定]   > [設定基準]  ，先選取要管理的設定基準，再選取管理工作。  


|管理工作|詳細資料|  
|---------------------|-------------|  
|**顯示成員**|顯示組態基準所參考的所有組態項目。|  
|**排程摘要**|設定排程，這是 Configuration Manager 主控台的 [設定基準]  節點顯示資料所依據的排程，這些資料是使用站台資料庫的最新資訊加以更新。|  
|**執行摘要**|摘要會使用站台資料庫的最新資訊來重新整理 [組態基準]  節點中的資料。 這個動作可能需要幾分鐘的時間才能完成。 您可能需要先按一下 [重新整理]  ，才能在主控台中看到最新資料。|  
|**檢視 XML 定義**|在新的視窗中，顯示所選取組態基準的 XML 定義檔。 當您想要手動撰寫組態資料時此資訊很有用。|  
|**啟用**|啟用合規性監視的組態基準。|  
|**停用**|停用組態基準，讓它不再評估用戶端電腦上的相容性。 也會停用參考此設定基準的組態基準。|  
|**匯出**|匯出封包 (.cab) 檔案格式的組態基準，但前提為它是在該站台建立。 接著可以將它匯入相同或不同的 Configuration Manager 站台。 組態資料會轉換成 DCM 摘要。<br /><br /> 如需如何匯入設定資料的資訊，請參閱[匯入設定資料](../../compliance/deploy-use/import-configuration-data.md)。|  
|**複製**|使用您指定的名稱，建立一份所選取組態基準的複本。 新的組態基準不保留原始的設定基準任何關聯性。|  
|**刪除**|開啟 [刪除組態基準]  對話方塊，以在其中檢閱這個組態基準的任何參考。<br /><br /> 您必須先移除組態基準的所有參考，才能刪除組態基準。|  
|**部署**|開啟 [部署組態基準]  對話方塊，以在其中將一個或多個組態基準部署至階層中的裝置。<br /><br /> 如需詳細資訊，請參閱[部署設定基準](../../compliance/deploy-use/deploy-configuration-baselines.md)。|  
