---
title: 管理發佈點
titleSuffix: Configuration Manager
description: 使用發佈點來裝載您部署至裝置與使用者的內容。
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1d93dd446a65fda0b259bb10e0c944780d41059
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347086"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>在 Configuration Manager 中安裝及設定發佈點

適用於：Configuration Manager (最新分支)

安裝 Configuration Manager 發佈點，來裝載部署至裝置與使用者的內容檔案。 建立發佈點群組，以簡化發佈點的管理方式與將內容發佈至發佈點的方式。  

您可以使用安裝精靈來「安裝新的發佈點」。 如需詳細資訊，請參閱[安裝發佈點](#bkmk_install)。 若要「管理現有發佈點的內容」，請編輯發佈點的內容。 如需詳細資訊，請參閱[設定發佈點](#bkmk_configs)。

使用任一方法可設定大部分發佈點設定。 有一些設定唯有當您在安裝或編輯時才能使用，無法同時適用於這兩種情況：  

- 只有在安裝發佈點時才可用的設定：  

    - **允許 Configuration Manager 在發佈點電腦上安裝 IIS**

    - **設定發佈點的磁碟機空間設定**  

- 只有在編輯發佈點內容時才可用的設定：  

    - **管理發佈點群組關聯性**  

    - **檢視部署至發佈點的內容**  

    - **替傳輸到發佈點的資料設定速率限制**  

    - **替傳輸到發佈點的資料設定排程**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a> 安裝發佈點  

選擇站台伺服器作為發佈點，才能讓用戶端電腦使用內容。 先將發佈點指派給至少一個[界限群組](boundary-groups.md#distribution-points)，內部部署用戶端電腦才能使用該發佈點作為內容來源位置。 將發佈點角色新增至新的站台系統伺服器，或將它新增至現有的站台系統伺服器。

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a> 先決條件

當您安裝新的發佈點時，可以使用安裝精靈，逐步引導您完成可用的設定。 開始之前，請考量下列必要條件：  

- 您必須擁有下列安全性權限，才能建立及設定發佈點。  

    - [發佈點] 物件的 [讀取]  權限  

    - [發佈點] 物件的 [複製到發佈點]  權限  

    - [網站] 物件的 [修改]  權限  

    - [網站] 物件的 [管理作業系統部署的憑證]  權限  

- 在裝載發佈點的 Windows 伺服器上安裝 Internet Information Services (IIS)。 或者，在您安裝站台系統角色時，Configuration Manager 可為您安裝並設定 IIS。  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a> 安裝發佈點的程序  

您可以使用此程序來新增發佈點。 若要變更現有發佈點的設定，請參閱[設定發佈點](#bkmk_configs)一節。  

請從[安裝站台系統角色](install-site-system-roles.md)的一般程序開始。 在 [建立站台系統伺服器精靈] 的 [系統角色選取] 頁面上，選取 [發佈點] 角色。 此動作會將下列頁面新增至精靈：  

- [發佈點](#bkmk_config-general)
- [通訊](#bkmk_config-comm)
- [磁碟機設定](#bkmk_config-drive)
- [提取發佈點](#bkmk_config-pull)
- [PXE 設定](#bkmk_config-pxe)
- [多點傳送](#bkmk_config-multicast)
- [內容驗證](#bkmk_config-valid)
- [界限群組](#bkmk_config-boundary)

> [!Important]  
> 只有在安裝發佈點時才可以使用下列設定：  
>
> - **允許 Configuration Manager 在發佈點電腦上安裝 IIS**  
>
> - **設定發佈點的磁碟機空間設定**  

如需發佈點角色特定精靈頁面的詳細資訊，請參閱[設定發佈點](#bkmk_configs)一節。 例如，如果您想要安裝發佈點作為[提取發佈點](#bkmk_config-pull)，請選擇 [啟用此發佈點以便從其他發佈點提取內容] 選項。 然後進行提取發佈點所需的額外設定。  

在您完成 [建立站台系統伺服器精靈] 之後，站台會將發佈點角色新增至站台系統伺服器。  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a> 管理發佈點群組  

發佈點群組提供內容發佈的發佈點邏輯群組。 使用這些群組，從跨越多個站台的發佈點中心位置來管理與監視內容。 請謹記下列重點：

- 從階層內的任何站台將一或多個發佈點新增至發佈點群組。  

- 將發佈點新增至一個以上的發佈點群組。  

- 在您將內容發佈至發佈點群組時，Configuration Manager 會將內容發佈至所有屬於群組成員的發佈點。  

- 若您在初始內容發佈之後，將發佈點新增至群組，Configuration Manager 會自動將內容發佈至該新發佈點成員。  

- 建立集合與發佈點群組的關聯。 發佈內容到集合時，Configuration Manager 會判斷與集合建立關聯的群組。 然後，它會將內容發佈至所有屬於這些群組成員的發佈點。  

    > [!NOTE]  
    > 將內容發佈至集合後，若您再將該集合與新的發佈點群組建立關聯性，則必須將內容重新發佈至該集合，才能將該內容發佈至新的發佈點群組。  

下列各節列出為管理發佈點群組所採取之下列動作的程序：  

- [建立和設定新的發佈點群組](#bkmk_dpgroup-create)
- [修改現有的發佈點群組](#bkmk_dpgroup-modify)
- [將選取的發佈點新增至現有的發佈點群組](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a> 建立和設定新的發佈點群組程序  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，然後選取 [發佈點群組] 節點。  

2. 在功能區中，選取 [建立群組]。  

3. 在 [建立新的發佈點群組] 視窗中，輸入群組的**名稱**，並選擇性地輸入**描述**。  

4. 在 [成員] 索引標籤上，選取 [新增]。  

5. 在 [新增發佈點] 視窗中，選取要新增作為群組成員的一或多個發佈點。 然後選擇 [確定]。  

6. 如有必要，請切換至 [建立新的發佈點群組] 視窗的 [集合] 索引標籤，然後選取 [新增]。  

7. 在 [選取集合] 視窗中，選取要與發佈點群組建立關聯的集合，然後選擇 [確定]。  

8. 在 [建立新的發佈點群組] 視窗中，選擇 [確定] 以建立群組。  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>從現有的發佈點建立新的群組

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，然後選取 [發佈點] 節點。 選取要新增至新發佈點群組的一或多個發佈點。  

2. 在功能區中，選取 [新增選取的項目]，然後選取 [將選取的項目新增至新的發佈點群組]。  

此程序會在 [建立新的發佈點群組] 視窗的 [成員] 索引標籤中，自動填入選取的伺服器。

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a> 修改現有的發佈點群組程序  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，然後選取 [發佈點群組] 節點。  

2. 選取要修改的現有發佈點群組。 在功能區中，選取 [內容]。  

3. 若要將新集合與此群組建立關聯，請切換至 [集合] 索引標籤，然後選擇 [新增]。 選取集合，然後選擇 [確定]。  

4. 若要將新發佈點新增至此群組，請切換至 [成員] 索引標籤，然後選擇 [新增]。 選取發佈點，然後選擇 [確定]。  

5. 按一下 [確定]，儲存對發佈點群組的變更。  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a> 將選取的發佈點新增至現有的發佈點群組程序  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，然後選取 [發佈點] 節點。 選取要新增至現有群組的一或多個發佈點。  

2. 在功能區中，選取 [新增選取的項目]，然後選取 [將選取的項目新增至現有的發佈點群組]。  

3. 在 [可用的發佈點群組] 中，選取要新增選取的發佈點作為其成員的群組。 然後選擇 [確定]。  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a> 重新指派發佈點

<!-- 1306937 -->

許多客戶擁有大型的 Configuration Manager 基礎結構，並會減少主要或次要站台，以簡化其環境。 他們仍然需要保留分公司位置的發佈點，以提供內容給受控的用戶端。 這些發佈點通常包含數 TB 以上的內容。 此內容在散發到這些遠端伺服器時會耗用大量時間和網路頻寬。

這項功能可讓您將發佈點重新指派給其他主要站台，而不需要重新發佈內容。 此動作會更新站台系統指派，同時保存伺服器上的所有內容。 如果您需要重新指派多個發佈點，請先在單一發佈點上執行此動作。 然後逐一處理其他伺服器。

> [!IMPORTANT]  
> 目標伺服器只能裝載發佈點角色。 如果站台系統伺服器裝載其他 Configuration Manager 伺服器角色 (例如狀態移轉點)，就無法重新指派發佈點。 您無法重新指派雲端發佈點。

重新指派發佈點之前，請在目標發佈點伺服器上先將本機目的地站台伺服器的電腦帳戶加入至本機系統管理員群組。

遵循下列步驟，重新指派發佈點：

1. 在 Configuration Manager 主控台中，連線至管理中心網站。  

2. 移至 [系統管理] 工作區，然後選取 [發佈點] 節點。  

3. 以滑鼠右鍵按一下目標發佈點，然後選取 [重新指派發佈點]。  

4. 選取您要重新指派這個發佈點的目標站台伺服器和站台碼。  

監視重新指派的方法與您加入新的角色時一樣。 最簡單的方法是在數分鐘後重新整理主控台檢視。 將站台碼欄加入至檢視。 此值會在 Configuration Manager 重新指派伺服器時變更。 如果您在重新整理主控台檢視之前，嘗試在目標伺服器上執行其他動作，就會發生「找不到物件」錯誤。 請確認程序完成後，重新整理主控台檢視，然後才在伺服器上開始任何其他動作。

重新指派發佈點之後，請重新整理伺服器憑證。 新的站台伺服器必須將使用其公開金鑰的憑證重新加密，並儲存在站台資料庫中。 如需詳細資訊，請在發佈點屬性的 [一般](#bkmk_config-general) 索引標籤上，參閱 [針對發佈點建立自我簽署的憑證，或匯入公開金鑰基礎結構 (PKI) 用戶端憑證]定。

- 對於 PKI 憑證，則不需要建立新的憑證。 匯入相同的 .PFX，並輸入密碼。  

- 對於自我簽署憑證，請調整要更新憑證的到期日或時間。  

- 如果您不重新整理憑證，發佈點仍會提供內容，但下列功能會失敗：  

    - 內容驗證訊息 (distmgr.log 顯示它無法解密憑證)  

    - 用戶端的 PXE 支援  

### <a name="tips"></a>提示

- 從管理中心網站執行此動作。 這種做法有助於複寫至主要站台。  

- 請不要將內容發佈至目標伺服器，然後嘗試加以重新指派。 進行重新指派程序時，發佈正在進行中的工作可能會失敗，但會按一般的方式重試。  

- 如果該伺服器也是 Configuration Manager 用戶端，也請務必將用戶端重新指派給新的主要站台。 此步驟對於使用用戶端元件下載內容的提取發佈點特別重要。  

- 此程序會移除舊站台預設界限群組中的發佈點。 如有必要，您必須手動將它新增至新站台的預設界限群組。 所有其他界限群組指派會維持不變。  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a> 維護模式

<!--3555754-->

從 1902 版開始，您可於維護模式中設定發佈點。 當您要安裝軟體更新，或對伺服器進行硬體變更時，請啟用維護模式。

發佈點處於維護模式時，它具有下列行為：

- 站台未散發任何內容給它。  

- 管理點不會將此發佈點的位置傳回給用戶端。

- 當您更新站台時，維護模式中的發佈點仍會更新。

- 發佈點屬性為唯讀。 例如，您無法變更憑證或新增界限群組。  

- 任何排程工作 (例如內容驗證) 仍然會按照相同的排程執行。

在多個發佈點上啟用維護模式時請小心。 此動作可能會對其他發佈點造成效能影響。 視您的界限群組設定而定，用戶端可能已增加下載時間，或無法下載內容。

任何發佈點的維護模式都不可為長期狀態。 針對任何持續時間很長的動作，請考慮先移除發佈點角色。

> [!NOTE]
> 當發佈點處於維護模式時，請勿執行下列動作：<!-- SCCMDocs-pr #4699 -->
>
> - 移除角色
> - 重新指派發佈點

### <a name="enable-maintenance-mode"></a>啟用維護模式

若要將發佈點置於維護模式，您的使用者帳戶需要擁有**站台**類別上的**修改**使用權限。 例如，**基礎結構系統管理員**和**系統高權限管理員**內建角色具有這個使用權限。<!-- SCCMDocs-pr issue #3407 -->

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區。  

2. 選取 [發佈點] 節點。  

3. 選取目標發佈點，然後從功能區選擇 [啟用維護模式]。  

若要檢視發佈點的目前狀態，請將 [維護模式] 資料行新增至主控台中的 [發佈點] 節點。

如需如何使用 Configuration Manager SDK 來將此程序自動化的詳細資訊，請參閱 [SMS_DistributionPointInfo 類別中的 SetDPMaintenanceMode 方法](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md)。


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a> 設定發佈點  

個別發佈點會支援各種不同的設定。 不過，並非所有的發佈點類型都支援所有的組態。 例如，雲端發佈點不支援啟用 PXE 或多點傳送的部署。 如需特定限制的詳細資訊，請參閱下列文章：  

- [使用雲端發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [使用提取發佈點](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

下列各節描述在[安裝新的發佈點](#bkmk_install-procedure)或[編輯現有的發佈點](#bkmk_change-procedure)時的發佈點設定：  

- [一般設定](#bkmk_config-general)
- [通訊](#bkmk_config-comm)
- [磁碟機設定](#bkmk_config-drive)
- [防火牆設定](#bkmk_firewall)
- [提取發佈點](#bkmk_config-pull)
- [PXE 設定](#bkmk_config-pxe)
- [多點傳送](#bkmk_config-multicast)
- [內容驗證](#bkmk_config-valid)
- [界限群組](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a> 變更發佈點程序

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，然後選取 [發佈點] 節點。  

2. 選取要設定的發佈點。 在功能區中，選擇 [內容]。  

3. 在編輯發佈點的內容時，請使用下列各節中的資訊。  

4. 進行所需的變更之後，選取 [確定] 以儲存您的設定並關閉發佈點屬性。  

### <a name="general"></a><a name="bkmk_config-general"></a> 一般  

> [!Note]  
> 在 1902 版和更舊版本中，此頁面有適用於 HTTP/HTTPS 和憑證的其他設定。 從 1906 版開始，這些設定現在會在 [通訊](#bkmk_config-comm) 頁面上。

下列設定位於 [建立站台系統伺服器精靈] 的 [發佈點] 頁面上，以及發佈點內容視窗的的 [一般] 索引標籤上：  

- **描述**：此發佈點角色的選擇性描述。  

- **在 Configuration Manager 需要時安裝並設定 IIS**：如果伺服器尚未安裝 IIS，Configuration Manager 會進行安裝與設定。 Configuration Manager 在所有發佈點上都需要 IIS。 如果您未選擇此設定，且未在伺服器上安裝 IIS，請先安裝 IIS，Configuration Manager 才能順利安裝發佈點。  

    > [!NOTE]  
    > 只有 [建立站台系統伺服器精靈] 的 [發佈點] 頁面上才有此選項。 只有在[安裝新的發佈點](#bkmk_install-procedure)時才可用。  

- **啟用並設定此發佈點的 BranchCache**：選擇此設定可讓 Configuration Manager 設定發佈點伺服器上的 Windows BranchCache。 如需詳細資訊，請參閱 [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。  

- **調整要用來使用未使用網路頻寬的下載速度 (Windows LEDBAT)**<!--1358112-->:從 1806 版開始，啟用發佈點以使用網路壅塞控制。 如需詳細資訊，請參閱 [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat)。 LEDBAT 支援的最低需求：<!-- SCCMDocs issue 883 -->  

    - Configuration Manager 1806 版 (一般版本)  

        - Windows Server 1709 版或更新版本  

    - Configuration Manager 1806 版含更新彙總 (4462978) 或更新版本  

        - Windows Server 1709 版或更新版本
        - 具有下列更新的 Windows Server 2016：
           - 累積更新 KB4132216 (2018 年 6 月 21 日發行) 或更新版本的累積更新。
           - 服務堆疊更新 KB4284833 (2018 年 5 月 18 日發行) 或更新版本的服務堆疊更新。

    - Configuration Manager 1810 版或更新版本：

        - Windows Server 1709 版或更新版本
        - 具有下列更新的 Windows Server 2016：
           - 累積更新 KB4132216 (2018 年 6 月 21 日發行) 或更新版本的累積更新。
           - 服務堆疊更新 KB4284833 (2018 年 5 月 18 日發行) 或更新版本的服務堆疊更新。
        - Windows Server 2019  

- **啟用此發佈點供預先設置的內容使用**：此設定可讓您在發佈軟體之前將內容新增至伺服器。 因為內容檔已經存在於內容庫中，所以當您發佈軟體時，就不會透過網路傳輸。 如需詳細資訊，請參閱[預先設置的內容](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)。  

- **允許將此發佈點用作 Microsoft 連線快取伺服器**：從 1906 版開始，您可以在發佈點上安裝 Microsoft 連線快取伺服器。 藉由快取此內部部署內容，您的用戶端就可以受益於傳遞最佳化功能，但您可以協助保護 WAN 連結。 如需詳細資訊，包括其他設定的描述，請參閱 [Configuration Manager 中的 Microsoft 連線快取](../../../plan-design/hierarchy/microsoft-connected-cache.md)。


### <a name="communication"></a><a name="bkmk_config-comm"></a> 通訊

> [!Note]  
> 從 1906 版開始，下列設定會在 [通訊] 索引標籤上。在 1902 版和更舊版本中，這些設定在 [一般](#bkmk_config-general) 索引標籤上。

下列設定位於 [建立站台系統伺服器精靈] 的 [通訊] 頁面上，以及發佈點內容視窗上：  

- **設定用戶端裝置與發佈點通訊的方式**：使用 **HTTP** 或 **HTTPS** 有其各自的優點和缺點。 如需詳細資訊，請參閱[內容管理的安全性最佳做法](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)。  

- **允許用戶端以匿名方式連線**：此設定指定發佈點是否允許從 Configuration Manager 用戶端匿名連線至內容庫。  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **建立自我簽署憑證或匯入 PKI 用戶端憑證**：Configuration Manager 針對下列目的使用此憑證：  

    - 在發佈點傳送狀態訊息前，向管理點驗證發佈點。  

    - 當您在 [PXE 設定] 頁面上 [為用戶端啟用 PXE 支援] 時，發佈點會將它傳送至 PXE 開機的電腦。 然後，這些電腦可以在 OS 部署程序期間使用它來連線到管理點。  

    當您設定站台中的所有管理點供 HTTP 使用時，請選取 [建立自我簽署憑證] 選項。 當您設定管理點供 HTTPS 使用時，請從 PKI 使用 [匯入憑證] 選項。  

    若要匯入憑證，請瀏覽至有效的公開金鑰加密標準 (PKCS #12) 檔案。 此 PFX 或 CER 檔案的 PKI 憑證具有下列 Configuration Manager 需求：  

    - 預期用途包含用戶端驗證  

    - 讓私密金鑰能夠匯出  

    > [!TIP]  
    > 對於憑證主體或主體別名 (SAN) 並無特定需求。 如有必要，請針對多個發佈點使用同一個憑證。  

    如需憑證需求的詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。  

    如需此憑證的部署範例，請參閱[為發佈點部署用戶端憑證](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)。  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a> 磁碟機設定  

> [!NOTE]  
> 這些選項只有在安裝新的發佈點時才可用。  

指定發佈點的磁碟機設定。 為內容庫設定最多兩部磁碟機，以及為套件共用設定兩部磁碟機。 當前兩部磁碟機達到設定的磁碟機空間保留時，Configuration Manager 可以使用其他磁碟機。 [磁碟機設定]  頁面可設定磁碟機的優先順序，以及保留在每部磁碟機上的可用磁碟空間數量。  

- **磁碟機空間保留 (MB)** ：此值可在 Configuration Manager 選擇不同磁碟機並繼續對該磁碟機進行複製程序前，判斷磁碟機上的可用空間量。 內容檔案可以跨越多個磁碟機。  

- **內容位置**：指定此發佈點上內容庫和套件共用的位置。 根據預設，所有內容位置都會設定為 [自動]。 Configuration Manager 會將內容複製到主要內容位置，直到可用空間量達到 [磁碟機空間保留 (MB)] 指定的值為止。 當您選取 [自動] 時，Configuration Manager 會將主要內容位置設定為在安裝時擁有最多磁碟空間的磁碟機。 它會將次要位置設定為擁有次多可用磁碟空間的磁碟機。 當主要和次要位置都達到磁碟機空間保留的設定時，Configuration Manager 會選取其他具備最多可用磁碟空間的磁碟機，繼續進行複製程序。  

> [!Tip]  
> 為避免 Configuration Manager 在特定磁碟機上進行安裝，請建立名為 **no_sms_on_drive.sms** 的空檔案，並將它複製到磁碟機的根資料夾，再安裝發佈點。  

如需詳細資訊，請參閱[內容庫](../../../plan-design/hierarchy/the-content-library.md)。

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a>防火牆設定

Windows 防火牆中必須設定以下輸入規則，才能使用發佈點：

- Windows Management Instrumentation (DCOM-In)
- Windows Management Instrumentation (WMI-In)

如果缺少這些規則，用戶端就會在嘗試下載內容時於 DataTransferService.log 收到錯誤 0x801901F4。

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a> 提取發佈點  

當您 [啟用此發佈點以便從其他發佈點提取內容]  時，它會成為提取發佈點。 您可以變更發佈點如何取得您發佈至其上之內容的行為。 如需詳細資訊，請參閱[使用提取發佈點](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)。

針對每個您設定的提取發佈點，請指定可從中取得內容的一或多個來源發佈點：  

- 選擇 [新增]，然後選取一或多個可用的發佈點作為來源。  

- 使用箭號按鈕調整優先順序。 當提取發佈點嘗試傳輸內容時，優先順序是它連絡來源發佈點的順序。 它會先連絡具有最低值的發佈點。  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a> PXE  

指定是否要在發佈點上啟用 PXE。 使用 PXE 在用戶端上啟動 OS 部署。 如需如何在 Configuration Manager 中使用 PXE 的詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。

當您啟用 PXE 時，Configuration Manager 會視需要在伺服器上安裝 Windows 部署服務 (WDS)。 WDS 是一項執行 PXE 開機以安裝作業系統的服務。 在您完成精靈以建立發佈點後，Configuration Manager 會在 WDS 中安裝一個使用 PXE 開機功能的提供者。

從 1806 版開始，您可以在發佈點上啟用 PXE，而不需要 WDS。

選取 [為用戶端啟用 PXE 支援]  選項，然後設定下列設定：  

> [!Note]  
> 選取 [檢閱 PXE 所需的連接埠] 對話方塊中的 [是]，以確認您想要啟用 PXE。 Configuration Manager 自動在 Windows 防火牆上設定預設連接埠。 如果您使用不同的防火牆，請手動設定連接埠。  
>
> 如果您在同一部伺服器上安裝 WDS 和 DHCP，請設定 WDS 接聽不同的連接埠。 根據預設，DHCP 會接聽相同的連接埠。 如需詳細資訊，請參閱[當您在同一部伺服器上有 WDS 和 DHCP 時的考量](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP)。  

- **允許此發佈點回應傳入的 PXE 要求**：指定是否啟用 WDS，以回應 PXE 服務要求。 使用此設定來啟用和停用服務，而不需移除發佈點上的 PXE 功能。  

- **啟用未知電腦支援**：指定是否要針對 Configuration Manager 未管理的電腦啟用支援。 如需詳細資訊，請參閱[準備未知電腦部署](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md)。  

- **在不使用 Windows 部署服務的情況下啟用 PXE 回應程式**：從 1806 版開始，這個選項會啟用發佈點上的 PXE 回應程式，而不需要 WDS。 此 PXE 回應程式支援 IPv6 網路。 如果您在已經支援 PXE 的發佈點上啟用這個選項，Configuration Manager 就會暫止 WDS 服務。 如果您停用此選項，但仍 [為用戶端啟用 PXE 支援]，則發佈點會再次啟用 WDS。<!--1357580-->  

    > [!Note]  
    > 在 1810 版和更早的版本中，如果也在執行 DHCP 伺服器的伺服器上沒有 WDS，就不支援使用 PXE 回應程式。
    >
    > 從 1902 版開始，當您在發佈點上啟用 PXE 回應程式而不需要 Windows 部署服務時，它現在可位於與 DHCP 服務相同的伺服器上。 <!--3734270-->  

- **電腦使用 PXE 時需要密碼**：若要為您的 PXE 部署提供其他安全性，請指定強式密碼。  

- **使用者裝置親和性**：指定您希望發佈點如何為 PXE 部署的使用者與目的地電腦建立關聯。 選擇下列其中一個選項：  

  - **允許自動核准使用者裝置親和性**：選擇此設定以自動為使用者與目的地電腦建立關聯，不需要等待核准。  

  - **允許使用者親和性等待系統管理員核准**：選擇此設定以等待系統管理使用者核准後，使用者才能與目的地電腦建立關聯。  

  - **不允許使用者裝置親和性**：選擇此設定以指定使用者不可與目的地電腦建立關聯。 這是預設設定。  

    如需使用者裝置親和性的詳細資訊，請參閱[使用使用者裝置親和性連結使用者和裝置](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

- **網路介面**：指定發佈點從所有網路介面或從特定網路介面回應 PXE 要求。 如果發佈點回應特定網路介面，則提供每個網路介面的 MAC 位址。  

    > [!Note]  
    > 變更網路介面時，請重新啟動 WDS 服務以確保正確地儲存設定。 從 1806 版開始，當使用 PXE 回應程式服務時，請重新啟動 **ConfigMgr PXE 回應程式服務** (SccmPxe)。<!--SCCMDocs issue 642-->  

- **指定 PXE 伺服器回應延遲 (秒)** ：當您使用多部 PXE 伺服器時，請指定支援 PXE 的發佈點等待回應電腦要求的時間。 根據預設，Configuration Manager 支援 PXE 的發佈點會立即回應。  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a> 多點傳送  

指定是否要在發佈點上啟用多點傳送。 多點傳送部署會藉由同時傳送資料至多個 Configuration Manager 用戶端，以保留網路頻寬。 如果沒有多點傳送，伺服器就會透過個別的連線，將資料複本傳送給各個用戶端。 如需如何使用多點傳送部署 OS 的詳細資訊，請參閱[使用多點傳送透過網路來部署 Windows](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。

當您啟用多點傳送時，Configuration Manager 會視需要在伺服器上安裝 Windows 部署服務 (WDS)。  

選取 [啟用多點傳送來同時傳送資料到多個用戶端] 選項，然後設定下列設定：  

- **多點傳送連線帳戶**：指定當您針對多點傳送設定 Configuration Manager 資料庫連線時所要使用的帳戶。 如需詳細資訊，請參閱[多點傳送連線帳戶](../../../plan-design/hierarchy/accounts.md#multicast-connection-account)。  

- **多點傳送位址設定**：指定用於將資料傳送至目的地電腦的 IP 位址。 根據預設，它可從啟用發佈多點傳送位址的 DHCP 伺服器取得 IP 位址。 根據網路環境不同，您可以指定介於 239.0.0.0 到 239.255.255.255 之間的 IP 位址範圍。  

    > [!IMPORTANT]  
    > 要求 OS 映像的目的地電腦必須可以存取您設定的這些 IP 位址。 確認路由器和防火牆允許目的地電腦和發佈點之間的多點傳送流量。  

- **多點傳送的 UDP 連接埠範圍**：指定 UDP 連接埠的範圍，其可用於傳送資料至目的地電腦。  

    > [!IMPORTANT]  
    > 要求 OS 映像的目的地電腦必須可以存取 UDP 連接埠。 確認路由器和防火牆允許目的地電腦和網站伺服器之間的多點傳送流量。  

- **用戶端上限**：指定可以從此發佈點下載 OS 映像的目的地電腦數目上限。  

- **啟用排程多點傳送**：指定 Configuration Manager 如何控制於何時開始將作業系統部署至目的地電腦。 設定下列選項：  

    - **工作階段啟動延遲 (分鐘)** ：指定 Configuration Manager 在回應第一個部署要求前等待的分鐘數。  

    - **工作階段大小上限 (用戶端)** ：指定必須接收到多少要求，Configuration Manager 才會開始部署作業系統。  

> [!IMPORTANT]  
> 從 1806 版開始，若要在發佈點內容的 [多點傳送] 索引標籤上啟用和設定多點傳送，發佈點必須使用 Windows 部署服務。  
>
> - 如果您 [為用戶端啟用 PXE 支援] 並 [啟用多點傳送來同時傳送資料到多個用戶端]，則您無法 [在不使用 Windows 部署服務的情況下啟用 PXE 回應程式]。  
>
> - 如果您 [為用戶端啟用 PXE 支援] 並 [在不使用 Windows 部署服務的情況下啟用 PXE 回應程式]，則您無法 [啟用多點傳送來同時傳送資料到多個用戶端]  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a> 群組關聯性  

> [!NOTE]  
> 這些選項只有在編輯先前安裝之發佈點的內容時才可用。  

管理成員包含此發佈點的發佈點群組。  

若要新增此發佈點做為現有發佈點群組的成員，請選擇 [新增]。 在 [新增至發佈點群組] 視窗中，選取現有的群組，然後選擇 [確定]。  

若要從發佈點群組移除此發佈點，請在清單中選取群組，然後選擇 [移除]。 將發佈點從發佈點群組中移除並不會從該發佈點中移除任何內容。

### <a name="content"></a><a name="bkmk_config-content"></a> 內容  

> [!NOTE]  
> 這些選項只有在編輯先前安裝之發佈點的內容時才可用。  

管理您發佈至發佈點的內容。 從部署套件清單中選取，並執行下列動作：  

- **驗證**：開始驗證軟體之內容檔案完整性的程序。 若要檢視內容驗證程序的結果，請在 [監視] 工作區中展開 [發佈狀態]，然後選擇 [內容狀態] 節點。 如需詳細資訊，請參閱[驗證內容](deploy-and-manage-content.md#validate-content)。  

- **重新發佈**：將所選軟體的所有內容檔案複製到發佈點，且覆寫現有檔案。 通常您會使用此動作修復內容檔案。 如需詳細資訊，請參閱[重新發佈內容](deploy-and-manage-content.md#redistribute-content)。  

- **移除**：從發佈點移除軟體的內容檔案。 如需詳細資訊，請參閱[移除內容](deploy-and-manage-content.md#remove-content)。  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a> 內容驗證  

設定排程以驗證發佈點上內容檔案的完整性。 當您依照排程啟用內容驗證時，Configuration Manager 會於排程的時間啟動程序。 它會根據本機 SMS_PackagesInContLib SCCMDP 類別來驗證所有內容。 您也可以設定內容驗證優先順序。 根據預設，優先順序會設為 [最低] 。 增加優先順序可能會增加驗證程序期間伺服器上的處理器和磁碟使用量，但應該更快完成。

若要檢視內容驗證程序的結果，請在 [監視] 工作區中展開 [發佈狀態]，然後選擇 [內容狀態] 節點。 它會顯示每個軟體類型的內容，例如應用程式、軟體更新套件和開機映像。  

> [!WARNING]  
> 雖然您是使用電腦的本機時間來指定內容驗證排程，但 Configuration Manager 主控台會使用 UTC 來顯示排程。  

如需詳細資訊，請參閱[驗證內容](deploy-and-manage-content.md#validate-content)。

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a> Boundary groups  

管理您指派此發佈點的目標界限群組。 將發佈點新增到至少一個界限群組。 部署內容期間，用戶端必須存在於與發佈點關聯的界限群組之中，才能使用該界限群組作為內容的來源位置。

設定界限群組「關聯性」，其定義用戶端可以後援以尋找內容的時機和界限群組。 如需詳細資訊，請參閱[界限群組](boundary-groups.md)。

選擇 [新增]，然後從清單中選取現有的界限群組。

若要為此發佈點建立新的界限群組，請選擇 [建立]。 如需如何建立及設定界限群組的詳細資訊，請參閱[界限群組的程序](boundary-group-procedures.md)。

您可以在編輯先前安裝之發佈點的內容時，管理 [Enable for on-demand distribution] \(啟用依需求散發\) 選項。 此選項可讓 Configuration Manager 在用戶端要求時，自動將內容發佈至此伺服器。 如需詳細資訊，請參閱[依需求散發內容](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)。

### <a name="schedule"></a><a name="bkmk_config-sched"></a> 排程  

> [!NOTE]  
> 這些選項只有在編輯先前安裝之發佈點的內容時才可用。
>
> 只有當編輯在站台伺服器之遠端發佈點的內容時，才能使用此索引標籤。  

設定排程以限制 Configuration Manager 可將資料傳輸至發佈點的時間。 請依優先順序限制資料，或是關閉所選取時段的連線。

若要限制資料，請在方格中選取時段，然後選擇下列其中一個 [可用性] 設定：  

- **對所有優先順序開放**：Configuration Manager 可不受限制地傳送資料至發佈點。 這是所有時段的預設設定。  

- **允許中高優先順序**：Configuration Manager 僅將中優先順序和高優先順序的資料傳送至發佈點。  

- **僅允許高優先順序**：Configuration Manager 僅將高優先順序的資料傳送至發佈點。  

- **已關閉**：Configuration Manager 不會傳送任何資料至發佈點。  

在軟體內容的 [發佈設定] 索引標籤上，設定軟體的 [發佈優先順序]。

> [!IMPORTANT]  
> 排程是以傳送端網站的時區為依據，而不是發佈點。  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a> 速率限制  

> [!NOTE]  
> 這些選項只有在編輯先前安裝之發佈點的內容時才可用。  
>
> 只有當編輯在站台伺服器之遠端發佈點的內容時，才能使用此索引標籤。  

設定速率限制以控制 Configuration Manager 用來將內容傳輸至發佈點時的網路頻寬。 選擇下列選項：  

- **傳送至此目的地時無限制**：Configuration Manager 可不受速率限制地傳送內容至發佈點。 這是預設設定。  

- **脈衝模式**：此選項指定站台伺服器傳送至發佈點的資料區塊大小。 您也可以指定傳送每個資料區塊之間的時間延遲。 如果您必須經由非常低頻寬的網路連線傳送資料至發佈點，請使用此選項。 例如，您可以限制每五秒傳送 1 KB 的資料，無論於特定時間的連結速度或其使用情形為何。  

- **限制為指定的每小時最大傳送速率**：指定此設定會讓站台僅使用您設定的時間百分比傳送資料至發佈點。 使用此選項時，Configuration Manager 不會識別網路的可用頻寬。 而是會細分可傳送資料的時間。 伺服器會傳送資料一小段時間，下一段時間則不傳送資料。 例如，如果您將 [限制可用的頻寬] 設定為 [50%]，Configuration Manager 會傳輸資料一段時間，下一段同等時間則不傳送資料。 不會管理實際資料量大小 (或資料區塊大小)。 只會管理傳送資料的時間長度。  
