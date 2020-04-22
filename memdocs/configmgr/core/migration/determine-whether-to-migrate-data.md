---
title: 選擇要移轉的項目
titleSuffix: Configuration Manager
description: 了解您可以遷移哪些資料，以及無法遷移哪些資料至 Configuration Manager 最新分支。
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701766"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>判斷是否要將資料遷移至 Configuration Manager 最新分支

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 最新分支中，移轉提供一項程序，可將支援的 Configuration Manager 版本所建立的資料和設定，傳輸到新階層。  您可以使用該程序：  

-   將多個階層合併為一個階層。  

-   將資料和設定從實驗室部署移至生產部署。

-   從舊版 Configuration Manager (例如無法升級到 Configuration Manager 最新分支的 Configuration Manager 2007) 或從 System Center 2012 Configuration Manager (支援升級到 Configuration Manager 最新分支) 移動資料和設定。  

除了發佈點站台系統角色和裝載發佈點的電腦以外，各階層間無法共用基礎結構 (包括站台、站台系統角色或裝載站台系統角色的電腦)、移轉和傳送。  

 雖然您無法移轉伺服器基礎結構，但可在階層間移轉 Configuration Manager 用戶端。 用戶端移轉包括將用戶端使用的資料從來源階層移轉至目的地階層，然後再安裝或重新指派用戶端軟體，使用戶端回報至新階層。

在您將用戶端安裝至新階層並且在用戶端提交其資料後，其獨有的 Configuration Manager 識別碼可協助 Configuration Manager 將您先前移轉的資料與各個用戶端電腦建立關聯。  

 移轉所提供的功能有助於保有您在設定和部署期間所做的投資，同時可讓您先充分利用產品中的核心變更 (System Center 2012 Configuration Manager 中首次出現且在 Configuration Manager 仍然使用的產品)。 這些變更包括使用較少站台及資源的精簡型 Configuration Manager 階層，以及使用在 64 位元硬體上執行的原生 64 位元程式碼來改善處理。  

 如需移轉支援的 Configuration Manager 版本資訊，請參閱[移轉的必要條件](../../core/migration/prerequisites-for-migration.md)。  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a>可遷移到 Configuration Manager 最新分支的資料

移轉程序可以在支援的 Configuration Manager 階層之間移轉大部分物件。 從支援的 Configuration Manager 2007 版本移轉的某些物件執行個體，必須進行修改才能符合 Systerm Center 2012 Configuration Manager 架構及物件格式。

這些修改不會影響來源站台資料庫中的資料。 從支援的 System Center 2012 Configuration Manager 或 Configuration Manager 最新分支版本遷移的物件不需要進行修改。  

以下是可根據來源階層中的 Configuration Manager 版本進行移轉的物件。 有些物件 (例如查詢) 並不會移轉。 如果您想要繼續使用這些不會移轉的物件，就必須在新階層中重新建立這些物件。 其他物件 (包括某些用戶端資料) 會在您於該階層中管理用戶端時，於新階層中自動重新建立這些物件。  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>您可以從 System Center 2012 Configuration Manager 或 Configuration Manager 最新分支遷移的物件

-   System Center 2012 Configuration Manager 及更新版本的應用程式  

-   System Center 2012 Configuration Manager 及更新版本的 App-V 虛擬環境  

-   Asset Intelligence 自訂  

-   界限  

-   集合：若要從支援的 System Center 2012 Configuration Manager 或 Configuration Manager 最新分支版本遷移集合，請使用物件移轉作業。  

-   相容性設定：  

    -   設定基準  

    -   設定項目  

-   部署  

-   作業系統部署：  

    -   開機映像  

    -   驅動程式套件  

    -   驅動程式  

    -   映像  

    -   套件  

    -   工作順序  

-   搜尋結果：已儲存搜尋條件  

-   軟體更新：  

    -   部署  

    -   部署套件  

    -   範本  

    -   軟體更新清單  

-   軟體發佈套件  

-   軟體計量規則  

-   虛擬應用程式套件  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>您可以從 Configuration Manager 2007 SP2 移轉的物件

-   公告  

-   System Center 2012 Configuration Manager 及更新版本的應用程式  

-   System Center 2012 Configuration Manager 及更新版本的 App-V 虛擬環境  

-   Asset Intelligence 自訂  

-   界限  

-   集合：您可以使用集合移轉作業，從支援的 Configuration Manager 2007 版本移轉集合。  

-   相容性設定 (在 Configuration Manager 2007 中稱為 Desired Configuration Management)：  

    -   設定基準  

    -   設定項目  

-   作業系統部署：  

    -   開機映像  

    -   驅動程式套件  

    -   驅動程式  

    -   映像  

    -   套件  

    -   工作順序  

-   搜尋結果：搜尋資料夾  

-   軟體更新：  

    -   部署  

    -   部署套件  

    -   範本  

    -   軟體更新清單  

-   軟體發佈套件  

-   軟體計量規則  

-   虛擬應用程式套件  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a>不可遷移到 Configuration Manager 最新分支的資料

您無法移轉下列類型的物件：  

-   AMT 用戶端佈建資訊  

-   用戶端上的檔案，包含：  

    -   用戶端清查和歷程記錄資料  

    -   用戶端快取中的檔案  

-   查詢  

-   Configuration Manager 2007 安全性權限及執行個體  

-   來自 SQL Server Reporting Services 的 Configuration Manager 2007 報表  

-   Configuration Manager 2007 Web 報表  

-   System Center 2012 Configuration Manager 和 Configuration Manager 最新分支報告  

-   System Center 2012 Configuration Manager 和 Configuration Manager 最新分支角色型系統管理：  

    -   安全性角色  

    -   安全性範圍  
