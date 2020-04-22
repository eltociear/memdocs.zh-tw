---
title: 規劃用戶端移轉
titleSuffix: Configuration Manager
description: 了解將用戶端從來源階層移轉至 Configuration Manager 最新分支目的地階層的工作。
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704556"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>規劃 Configuration Manager 中的用戶端移轉策略

適用於：  Configuration Manager (最新分支)

若要將用戶端從來源階層遷移至 Configuration Manager 最新分支目的地階層，您必須執行兩項工作。 您必須移轉與用戶端相關聯的物件，而且必須將用戶端從來源階層重新安裝或重新指派至目的地階層。 先移轉物件，如此在移轉用戶端時，就可以使用物件。 與用戶端相關聯的物件是使用移轉作業進行移轉。 若要深入了解如何遷移與用戶端相關聯的物件，請參閱[規劃移轉作業策略](../../core/migration/planning-a-migration-job-strategy.md)。  

 使用以下各節內容有助於規劃將用戶端移轉至目的地階層。  

-   [規劃將用戶端移轉至目的地階層](#Planning_for_Client_Agent_Migration)  

-   [規劃處理移轉期間保留在用戶端上的資料](#Planning_for_Client_Data_Migration)  

-   [規劃移轉期間的清查和合規性資料](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> 規劃將用戶端移轉至目的地階層  
 從來源階層移轉用戶端時，用戶端電腦上的用戶端軟體會升級，以符合來源階層的產品版本。  

-   **Configuration Manager 2007 來源階層：** 當您從執行 Configuration Manager 受支援版本的來源階層移轉用戶端時，用戶端軟體會升級為目的地階層的用戶端版本。  

-   **System Center 2012 Configuration Manager 或更新版本的來源階層：** 當移轉相同產品版本階層之間的用戶端時，用戶端軟體不會變更或升級。 而是從來源階層重新指派至目的地階層中的站台。  

    > [!NOTE]  
    >  若某階層產品版本無法移轉到您的目的地階層，請將來源階層中的所有站台和用戶端全升級到相容的產品版本。 在來源階層升級到受支援的產品版本後，就可以在階層之間移轉。 如需詳細資訊，請參閱[移轉必要條件](../../core/migration/prerequisites-for-migration.md)的[支援移轉的 Configuration Manager 版本](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions)。  

請利用下列資訊幫助您規劃用戶端移轉：  

-   若要從來源站台將用戶端升級或重新指派至目的地站台，請使用支援在目的地階層中部署用戶端的任何用戶端部署方法。 一般用戶端部署方法包括用戶端推入安裝、軟體發佈、群組原則，以及軟體更新為基礎的用戶端安裝。 如需詳細資訊，請參閱[用戶端安裝方法](../../core/clients/deploy/plan/client-installation-methods.md)。  

-   請確定執行來源階層之用戶端軟體的裝置符合最低硬體需求，並且執行目的地階層中 Configuration Manager 版本支援的作業系統。  

-   在移轉用戶端之前，請先執行移轉作業來移轉用戶端將在目的地階層中使用的資訊。  

-   升級後保留部署執行歷程記錄的用戶端。 這可以避免部署在目的地階層中不必要地重複執行。  

    -   若是 Configuration Manager 2007 用戶端，會保留公告執行歷程記錄。  

    -   針對 System Center 2012 Configuration Manager 或 Configuration Manager 最新分支的用戶端，保留部署執行歷程記錄。  

-   您可以依照您選擇的任何順序，從來源階層中的站台移轉用戶端。 不過，請考慮分階段移轉有限的用戶端數目，不要一次移轉大量的用戶端。 分段移轉可在每個新升級的用戶端將其初始完整清查和相容性資料提交至其指派的站台時，減少網路頻寬需求和伺服器處理。  

-   當您移轉 Configuration Manager 2007 用戶端時，現有的用戶端軟體會從用戶端電腦上解除安裝，然後安裝新的用戶端軟體。  

-   Configuration Manager 無法移轉安裝了 App-V 用戶端的 Configuration Manager 2007 用戶端，除非 App-V 用戶端版本是 4.6 SP1 或更新版本。  

在 Configuration Manager 主控台之 [管理]  工作區的 [移轉]  節點，您可以監視用戶端移轉進度。  

將用戶端移轉至目的地階層之後，您就無法再使用來源階層管理該裝置，而應該考慮從來源階層中移除用戶端。 雖然這不是移轉階層時的需求，但是有助於避免在來源階層報告中識別移轉的用戶端，或是在移轉期間發生兩個階層之間的資源計數不正確。 例如，如果移轉的用戶端留在來源站台資料庫中，您可能會執行軟體更新報告，而誤將該電腦識別為未受管理的資源，而實際上是受到目的地階層管理。  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a> 規劃處理移轉期間保留在用戶端上的資料  
您將用戶端從其來源階層移轉至目的地階層時，有些資料會保留在裝置上，而有些資料在移轉後就不會存在裝置上。  

下列資訊會保留在用戶端裝置上：  

-   唯一識別碼 (GUID)，會將用戶端與 Configuration Manager 資料庫中的相關資訊產生關聯。  

-   公告或部署歷程記錄，可避免用戶端在目的地階層中不必要地重複執行公告或部署。  

下列資訊不會保留在用戶端裝置上：  

-   用戶端快取中的檔案。 如果用戶端需要這些檔案才能安裝軟體，用戶端會再次從目的地階層下載這些檔案。  

-   來源階層中尚未執行的任何公告或部署的相關資訊。 如果您要讓用戶端在移轉後執行公告或部署，則必須將它們重新部署到目的地階層中的用戶端。  

-   清查的相關資訊。 用戶端會在移轉且已產生新的用戶端資料後，將此資訊重新傳送至目的地階層中其指定的站台。  

-   相容性資料。 用戶端會在移轉且已產生新的用戶端資料後，將此資訊重新傳送至目的地階層中其指定的站台。  

用戶端移轉時，儲存在 Configuration Manager 用戶端登錄和檔案路徑中的資訊不會保留。 移轉後，重新套用這些設定。 以下是一般設定：  

-   電源配置  

-   記錄設定  

-   本機原則設定  

此外，您可能需要重新安裝部分應用程式。  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> 規劃移轉期間的清查和相容性資料  
您將用戶端移轉至目的地階層時，用戶端清查和相容性資料並不會儲存。 此資訊會在用戶端初次將其資訊傳送至其指定的站台時，於目的地階層中重新建立。 若要幫助減少產生的網路頻寬需求和伺服器處理，請考慮分階段移轉小量用戶端，而不要一次移轉大量用戶端。  

 此外，您無法從來源階層移轉硬體清查的自訂。 您必須在移轉之外另行將這些自訂導入目的地階層中。 如需如何擴充硬體清查的資訊，請參閱[如何設定硬體清查](../../core/clients/manage/inventory/configure-hardware-inventory.md)。  
