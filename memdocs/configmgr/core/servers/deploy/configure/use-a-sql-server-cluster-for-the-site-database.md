---
title: SQL Server 叢集
titleSuffix: Configuration Manager
description: 使用 SQL Server 叢集來裝載 Configuration Manager 站台資料庫
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e731ef2d133c2187eb9eaa98c07afeed37645fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700846"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>針對站台資料庫使用 SQL Server 叢集

適用於：  Configuration Manager (最新分支)

您可以使用 SQL Server 容錯移轉叢集來裝載 Configuration Manager 站台資料庫。 叢集會提供容錯移轉支援，並改善站台資料庫的可靠性。 不過，它未提供額外的處理或負載平衡好處。 此外，SQL Server 容錯移轉叢集使用共用儲存體並引進單一失敗點。 因為站台伺服器必須先尋找作用中的 SQL Server 叢集節點，才能連線到站台資料庫，所以效能可能會因此而降低。  

> [!IMPORTANT]  
> 成功設定 SQL Server 叢集遵循 SQL Server 文件庫中所提供的文件和程序。  


安裝 Configuration Manager 之前，請準備 SQL Server 叢集，以支援 Configuration Manager。 如需詳細資訊，請參閱[準備叢集 SQL Server 執行個體](#bkmk_prepare)。

在 Configuration Manager 安裝期間，會在 Microsoft Windows Server 叢集的每個實體電腦節點上安裝 Windows 磁碟區陰影複製服務寫入器。 此服務支援**備份站台伺服器**維護工作。  

安裝站台之後，Configuration Manager 會每小時檢查叢集節點有無變更。 Configuration Manager 會自動管理發現任何會影響其元件安裝的變更。 例如，節點容錯移轉，或在 SQL Server 叢集加入新節點。  



## <a name="supported-options"></a>支援的選項

用作站台資料庫的 SQL Server 容錯移轉叢集支援下列選項︰

- 單一執行個體叢集  

- 多個執行個體組態  

- 多個作用中的節點  

- 具名執行個體或預設執行個體  



## <a name="prerequisites"></a>先決條件

請注意下列先決條件：  

- 站台資料庫相對於站台伺服器而言，必須是遠端的資料庫 (叢集不得包含站台系統伺服器)。  

    > [!Note]  
    > 從 1810 版開始，Configuration Manager 安裝程序不會再封鎖在具有容錯移轉叢集 Windows 角色的電腦上安裝站台伺服器角色。 先前您無法將站台資料庫共置在站台伺服器上。 透過此變更，您可以使用較少的伺服器建立高可用性的站台，方法是在被動模式中使用 SQL 叢集和站台伺服器。 如需詳細資訊，請參閱[高可用性選項](high-availability-options.md)。 <!--3607761, fka 1359132-->  

- 將站台伺服器的電腦帳戶新增至叢集中每部伺服器的本機 [Administrators]  群組。  

- 若要支援 Kerberos 驗證，請為每個 SQL Server 叢集節點的網路連線啟用 **TCP/IP** 網路通訊協定。 **具名管道**通訊協定並非必要，但可用於針對 Kerberos 驗證問題進行疑難排解。 網路通訊設定是在 [SQL Server 組態管理員]  的 [SQL Server 網路組態]  下設定。  

- 如果您使用公開金鑰基礎結構 (PKI)，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。 當您針對站台資料庫使用 SQL Server 叢集時，有特定的憑證需求。  



## <a name="limitations"></a>限制

請考慮下列限制：  


### <a name="installation-and-configuration"></a>安裝及設定

- 次要站台無法使用 SQL Server 叢集。  

- 當您指定 SQL Server 叢集時，無法使用用於為站台資庫指定非預設檔案位置的選項。  


### <a name="sms-provider"></a>SMS 提供者

您無法在 SQL Server 叢集上安裝 SMS 提供者的執行個體。 在以叢集 SQL Server 節點身分執行的電腦上也不支援它。  


### <a name="data-replication-options"></a>資料複寫選項

若使用**分散式檢視**，將無法使用 SQL Server 叢集來裝載站台資料庫。  


### <a name="backup-and-recovery"></a>備份與復原

Configuration Manager 不支援為使用具名執行個體的 SQL Server 叢集進行 Data Protection Manager (DPM) 備份。 它確實支援在使用預設 SQL Server 執行個體的 SQL Server 叢集上執行 DPM 備份。  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a> 準備叢集 SQL Server 執行個體  

以下是準備站台資料庫所需完成的主要工作︰

- 建立虛擬 SQL Server 叢集，以便在現有的 Windows Server 叢集環境裝載站台資料庫。 如需安裝和設定 SQL Server 叢集的特定步驟，請參閱 SQL Server 版本的相關文件。 如需詳細資訊，請參閱[建立新的 SQL Server 容錯移轉叢集](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017)。  

- 在 SQL Server 叢集中的每台電腦上，在您不希望 Configuration Manager 安裝站台元件之每個磁碟機的根資料夾中放置檔案。 將檔案命名為 `NO_SMS_ON_DRIVE.SMS`。 Configuration Manager 預設會在每個實體節點上安裝一些元件，以支援備份等作業。  

- 將站台伺服器的電腦帳戶新增至 Windows Server 叢集節點電腦的本機 [Administrators]  群組。  

- 在虛擬 SQL Server 執行個體中，將 **sysadmin** SQL Server 角色指派給要執行 Configuration Manager 安裝程式的使用者帳戶。  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>使用叢集 SQL Server 安裝新的站台  

若要安裝使用叢集站台資料庫的站台，除了下列幾個步驟之外，請遵循您安裝站台時的正常程序執行 Configuration Manager 安裝程式：  

- 在 [資料庫資訊]  頁面上，指定要裝載站台資料庫之虛擬 SQL Server 叢集執行個體的名稱。 此虛擬執行個體會取代執行 SQL Server 之電腦的名稱。  

    > [!IMPORTANT]  
    > 當您輸入虛擬 SQL Server 叢集執行個體的名稱時，請勿輸入 Windows Server 叢集所建立的虛擬 Windows Server 名稱。 若是使用虛擬 Windows Server 名稱，站台資料庫將會安裝在作用中 Windows Server 叢集節點的本機硬碟上。 若該節點失敗，將會造成容錯移轉失敗。  
