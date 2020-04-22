---
title: 管理集合
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中執行常見的集合管理工作。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fc8347ae766cbd16075ef4170efa2f8042371f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695306"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>如何管理 Configuration Manager 中的集合

適用於：  Configuration Manager (最新分支)

使用本文中的概觀資訊來協助您執行 Configuration Manager 中集合的管理工作。  

> [!NOTE]  
>  如需有關如何建立 Configuration Manager 集合的資訊，請參閱[如何在 Configuration Manager 中建立集合](create-collections.md)。



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a> 如何管理裝置集合  

在 [資產與相容性]  工作區中，選取 [裝置集合]  ，並選取要管理的集合，然後選取管理工作。  


#### <a name="show-members"></a>顯示成員
在 [裝置]  節點下，顯示臨時節點中為所選取集合成員的所有資源。


#### <a name="add-selected-items"></a>加入選取的項目
提供下列選項： 

- **將選取的項目新增至現有裝置集合**：開啟 [選取集合]  對話方塊。 請選取您想要新增所選集合成員的集合。 使用 [包含集合]  成員資格規則，將選取的集合包含在這個集合。  

- **將選取的項目新增至新裝置集合**：開啟 [建立裝置集合精靈]  ，您可以在其中建立新的集合。 使用 [包含集合]  成員資格規則，將選取的集合包含在這個集合。  


如需詳細資訊，請參閱[如何建立集合](create-collections.md)。


#### <a name="install-client"></a>安裝用戶端
開啟 [安裝用戶端精靈]  。 此精靈會使用用戶端推入安裝，在所選取集合內的所有電腦上安裝 Configuration Manager 用戶端。 如需詳細資訊，請參閱[用戶端推入安裝](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。


#### <a name="run-script"></a>執行指令碼
開啟 [執行指令碼] 精靈  ，以在集合內的所有用戶端上執行 PowerShell 指令碼。 如需詳細資訊，請參閱[建立及執行 PowerShell 指令碼](../../../../apps/deploy-use/create-deploy-scripts.md)。


#### <a name="manage-affinity-requests"></a>管理同質要求
開啟 [管理使用者裝置親和性要求]  對話方塊。 請核准或拒絕擱置中的要求，以針對所選集合中的裝置建立使用者裝置親和性。 如需詳細資訊，請參閱[透過使用者裝置親和性來連結使用者和裝置](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)


#### <a name="clear-required-pxe-deployments"></a>清除所需的 PXE 部署
清除所選取集合之所有成員中的任何必要 PXE 開機部署。 如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。


#### <a name="update-membership"></a>更新成員資格
評估所選取之集合的成員資格。 對於具有許多成員的集合，這個更新可能需要一些時間才能完成。 使用 [重新整理]  動作，會在更新完成之後，使用新的集合成員來更新顯示。


#### <a name="add-resources"></a>新增資源
開啟 [將資源新增至集合]  對話方塊。 請搜尋要新增至所選集合的新資源。 在更新期間，所選取集合的圖示會顯示沙漏符號。


#### <a name="client-notification"></a>用戶端通知
如需詳細資訊，請參閱[用戶端通知](../client-notification.md)。


#### <a name="endpoint-protection"></a>Endpoint Protection
如需詳細資訊，請參閱[用戶端通知](../client-notification.md)。


#### <a name="export"></a>匯出
開啟 [匯出集合精靈]  以協助您將此集合匯出至「受控物件格式」(MOF) 檔案。 然後便可在另一個 Configuration Manager 站台封存或匯入此檔案。 當您匯出集合時，並不會匯出所參考的集合。 所參考的集合是由所選集合利用 **Include** 或 **Exclude** 規則來參考的。


#### <a name="copy"></a>複製
建立所選取之集合的複本。 新的集合會使用選取的集合作為限制集合。


#### <a name="refresh"></a>重新整理
重新整理檢視。


#### <a name="delete"></a>刪除
刪除選取的集合。 您也可以從站台資料庫中刪除集合中的所有資源。 

您無法刪除 Configuration Manager 內建的集合。 如需內建集合的清單，請參閱[集合簡介](introduction-to-collections.md#built-in-collections)。


#### <a name="simulate-deployment"></a>模擬部署
開啟 [模擬應用程式部署精靈]  。 此精靈可讓您無須安裝或解除安裝應用程式，即可測試應用程式部署的結果。 如需詳細資訊，請參閱[如何模擬應用程式部署](../../../../apps/deploy-use/simulate-application-deployments.md)。


#### <a name="deploy"></a>部署
顯示下列選項：  

- **應用程式**：開啟 [部署軟體精靈]  。 請選取並設定對所選集合的應用程式部署。 如需詳細資訊，請參閱[如何部署應用程式](../../../../apps/deploy-use/deploy-applications.md)。  

- **程式**：開啟 [部署軟體精靈]  。 請選取並設定對所選集合的套件和程式部署。 如需詳細資訊，請參閱[套件和程式](../../../../apps/deploy-use/packages-and-programs.md)。  

- **設定基準**：開啟 [部署設定基準]  對話方塊。 請設定將一或多個設定基準部署至選取的集合。 如需詳細資訊，請參閱[如何部署設定基準](../../../../compliance/deploy-use/deploy-configuration-baselines.md)。  

- **工作順序**：開啟 [部署軟體精靈]  。 請選取並設定對所選集合的工作順序部署。 如需詳細資訊，請參閱[管理工作順序，將工作自動化](../../../../osd/deploy-use/deploy-a-task-sequence.md)。  

- **軟體更新**：開啟 [部署軟體更新精靈]  。 請設定將軟體更新部署至所選集合中的資源。 如需詳細資訊，請參閱[管理軟體更新](../../../../sum/understand/software-updates-introduction.md)。  


#### <a name="clear-server-group-deployment-locks"></a>清除伺服器群組部署鎖定
手動釋出集合的所有伺服器群組部署鎖定。 如需詳細資訊，請參閱[提供伺服器群組](../../../../sum/deploy-use/service-a-server-group.md)。


#### <a name="move"></a>移動
將所選集合移至 [裝置集合]  節點中的另一個資料夾。 


#### <a name="properties"></a>屬性
如需詳細資訊，請參閱[集合內容](#BKMK_CollProp)。  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a> 如何管理使用者集合  

在 [資產與相容性]  工作區中，選取 [使用者集合]  ，並選取要管理的集合，然後選取管理工作。  

> [!Note]  
> 以下是使用者集合上的可用動作，但行為與搭配裝置集合使用時相同。 唯一的不同在於它們是套用至使用者集合和集合內的使用者。 如需詳細資訊，請參閱[如何管理裝置集合](#bkmk_device)底下的相對應動作。  

- **顯示成員**  
- **新增選取的項目**  
    - **將選取的項目新增至現有的使用者集合**  
    - **將選取的項目新增至新使用者集合**  
- **管理親和性要求**  
- **更新成員資格**  
- **新增資源**  
- **匯出**  
- **複製**  
- **重新整理**  
- **刪除**  
- **模擬部署**  
- **部署**  
    - **應用程式**  
    - **程式**  
    - **設定基準**
- **移動**  
- <bpt id="p1">**</bpt>Properties<ept id="p1">**</ept>


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> 集合內容  

當您開啟集合的 [內容]  對話方塊時，請檢視並設定下列選項：  

#### <a name="general"></a>一般
檢視及設定有關所選集合的一般資訊，包括集合名稱和限制集合。

#### <a name="membership-rules"></a>成員資格規則
設定定義此集合之成員資格的成員資格規則。 如需詳細資訊，請參閱[如何建立集合](create-collections.md)。  

#### <a name="power-management"></a>電源管理
設定您已指派給所選集合內電腦的電源管理計劃。 如需詳細資訊，請參閱[電源管理簡介](../power/introduction-to-power-management.md)。  

#### <a name="deployments"></a>部署
顯示您已部署至所選集合成員的任何軟體。  

#### <a name="maintenance-windows"></a>維護期間
檢視及設定套用至所選集合成員的維護期間。 如需詳細資訊，請參閱[如何使用維護期間](use-maintenance-windows.md)。

#### <a name="collection-variables"></a>集合變數
設定套用至此集合且可供工作順序使用的變數。 如需詳細資訊，請參閱[如何設定工作順序變數](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set)。  

#### <a name="distribution-point-groups"></a>發佈點群組
將一或多個發佈點群組與所選集合的成員建立關聯。 如需詳細資訊，請參閱[管理內容與內容基礎結構](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md)。

#### <a name="aad-group-sync"></a>AAD 群組同步
將集合成員資格結果同步至 Azure Active Directory 群組。 從 1906 版開始，此同步是[發行前版本功能](../../../servers/manage/pre-release-features.md)。 如需詳細資訊，請參閱[建立集合](create-collections.md#bkmk_aadcollsync)。

#### <a name="security"></a>安全性
顯示具有所選取集合與相關聯角色和安全性範圍權限的系統管理使用者。 如需詳細資訊，請參閱[以角色為基礎的系統管理基本概念](../../../understand/fundamentals-of-role-based-administration.md)。  

#### <a name="alerts"></a>警示 
設定何時為用戶端狀態和 Endpoint Protection 產生警示。 如需詳細資訊，請參閱[如何設定用戶端狀態](../../deploy/configure-client-status.md)和[如何監視 Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md)。  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> 使用 PowerShell

PowerShell 可用來管理集合。  如需詳細資訊，請參閱：

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection) \(英文\)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection) \(英文\)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection) \(英文\)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection) \(英文\)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection) \(英文\)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection) \(英文\)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection) \(英文\)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember) \(英文\)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting) \(英文\)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate) \(英文\)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule) \(英文\)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement) \(英文\)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule) \(英文\)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule) \(英文\)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule) \(英文\)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule) \(英文\)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule) \(英文\)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser) \(英文\)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule) \(英文\)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule) \(英文\)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule) \(英文\)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup) \(英文\)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule) \(英文\)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule) \(英文\)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser) \(英文\)
