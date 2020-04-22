---
title: 產品生命週期儀表板
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用產品生命週期儀表板來檢視 Microsoft 生命週期原則。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695166"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>使用 Configuration Manager 管理 Microsoft 生命週期原則

適用於：  Configuration Manager (最新分支)

從 1806 版開始，您可以使用 Configuration Manager 產品生命週期儀表板來檢視 Microsoft 生命週期原則。 該儀表板會針對安裝於使用 Configuration Manager 管理之裝置上的 Microsoft 產品，顯示 Microsoft 生命週期原則的狀態。 它也會提供有關環境中的 Microsoft 產品、支援狀態，以及支援終止日期的資訊。 使用儀表板來了解每項產品的支援可用性。 這項資訊可以在您所使用的 Microsoft 產品達到其目前的終止支援之前，協助您規劃更新該產品的時機。  

如需詳細資訊，請參閱 [Microsoft 生命週期原則](https://support.microsoft.com/lifecycle)。

從 1810 版開始，儀表板會包含 System Center 2012 Configuration Manager 和更新版本的資訊。<!--1358702-->  



## <a name="prerequisites"></a>先決條件 

 若要查看產品生命週期儀表板中的資料，需要下列元件：  

- 執行 Configuration Manager 主控台的電腦上必須安裝 Internet Explorer 9 或更新版本。  

- 必須安裝並設定服務連接點角色。 若要取得此儀表板上資料的更新，服務連接點必須保持上線，或是在離線的情況下定期同步。 如需詳細資訊，請參閱 [About the service connection point](../../../servers/deploy/configure/about-the-service-connection-point.md) (關於服務連接點)。

- 需要 Reporting Services 點以取得儀表板中的超連結功能。 SQL Server Reporting Services (SSRS) 報表的儀表板連結。 如需詳細資訊，請參閱[報告簡介](../../../servers/manage/introduction-to-reporting.md)。  

- 必須設定並同步 Asset Intelligence 同步處理點。 儀表板會使用 Asset Intelligence 類別目錄作為產品標題的中繼資料。 中繼資料會與您階層中的清查資料進行比較。 如需詳細資訊，請參閱[設定 Configuration Manager 中的 Asset Intelligence](configuring-asset-intelligence.md)。  
  - 如果您是第一次設定 Asset Intelligence 服務點，請務必[啟用 Asset Intelligence 硬體清查類別](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)。 生命週期儀表板取決於這些 Asset Intelligence 硬體清查類別。 儀表板在用戶端掃描並傳回硬體清查之前不會顯示資料。  
  - 若要在此儀表板中檢視延長安全性更新 (ESU) 的相關資訊，請啟用硬體清查類別 [軟體授權產品 - Asset Intelligence (SoftwareLicensingProduct)]  。 如需詳細資訊，請參閱[啟用 Asset Intelligence 硬體清查類別](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)。 <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>使用產品生命週期儀表板

根據站台從受控裝置所收集的清查資料，儀表板會顯示所有目前產品的相關資訊。 不過，針對作業系統和 SQL Server 所顯示的資訊僅限於下列版本：

- Windows Server 2008 及更新版本
- Windows XP 及更新版本
- SQL Server 2008 及更新版本

若要存取 Configuration Manager 主控台中的生命週期儀表板，請移至 [資產與合規性]  工作區，展開 [Asset Intelligence]  ，然後選取 [產品生命週期]  節點。

> [!NOTE]  
> 儀表板中的資料會以 Configuration Manager 主控台所連線的站台為依據。 如果主控台連線到您的頂層站台，您就會看到整個階層的資料。 連線到子主要站台時，只會顯示該站台的資料。

### <a name="product-lifecycle-dashboard"></a>產品生命週期儀表板

![主控台中的產品生命週期儀表板螢幕擷取畫面](media/product-lifecycle-dashboard.png)

從**產品類別目錄**清單選取下列選項之一來變更檢視：  
- **全部**：同時檢視所有產品  
- **Windows 用戶端**：檢視 Windows 用戶端 OS 版本  
- **Windows 伺服器**：檢視 Windows 伺服器 OS 版本  
- **資料庫**：檢視 SQL Server 版本  
- **Configuration Manager**：從 1810 版開始，檢視 Configuration Manager 版本 
- **Microsoft Office**：從 1902 版開始，檢視從 Office 2003 至 Office 2016 之已安裝版本的資訊 <!--3556026-->

儀表板具有以下磚：  

- **前五個生命週期已結束的產品**：此圖格是產品的彙總資料檢視，這些產品可在您的環境中找到且生命週期已結束。 圖表會顯示與作業系統和 SQL Server 產品的支援生命週期相較之下已過期的已安裝軟體。  

- **前五個即將結束生命週期的產品**：此圖格是產品的彙總資料檢視，這些產品可在您的環境中找到且即將在接下來 18 個月內結束生命週期。 圖表會顯示與作業系統和 SQL Server 產品的支援生命週期相較之下，到期時間在 18 個月內的已安裝軟體。  

- **已安裝產品的生命週期資料**：此圖格可讓您大概了解產品從支援狀態轉換為過期狀態的時機。 圖表提供已安裝產品的用戶端數目和支援可用性狀態的細目，以及可深入了解應採取之後續步驟的連結。 圖表中包含下列資訊：     
    - 剩餘的支援時間
    - 環境中的數目 
    - 主要支援結束日期
    - 延伸支援結束日期
    - 後續步驟  

> [!IMPORTANT]  
> 此儀表板中所顯示的資訊為供您方便使用，並應僅供貴公司內部使用。 您不應完全依賴此資訊來確認合規性。 請務必確認提供給您之資訊的準確性，並瀏覽 [Microsoft 生命週期原則](https://support.microsoft.com/lifecycle)以確認支援資訊的可用性。  



## <a name="reporting"></a>報告

還會提供其他報表。 在 Configuration Manager 主控台中，移至 [監視]  工作區，然後依序展開 [報告]  和 [報表]  。 下列新報表已新增至 [Asset Intelligence]  類別：  

- **生命週期 01A - 使用特定軟體產品的電腦**：檢視被偵測到具有指定產品的電腦清單。  

- **生命週期 02A - 組織中產品過期的電腦清單**：檢視具有過期產品的電腦。 您可以依產品名稱來篩選此報表。

- **生命週期 03A - 在組織中找到的過期產品清單**：檢視您環境中生命週期日期已過期的產品詳細資料。  

- **生命週期 04A - 一般產品生命週期概觀**：檢視產品生命週期的清單。 您可以依產品名稱和到期日來篩選此清單。  

- **生命週期 05A - 產品生命週期儀表板**：自 1810 版開始，此報表包含類似主控台中儀表板的資訊。 選取類別以檢視您環境中的產品計數，以及剩餘的支援天數。  

如需詳細資訊，請參閱[報表清單](../../../servers/manage/list-of-reports.md#asset-intelligence)。<!--SCCMDocs issue 997-->  
