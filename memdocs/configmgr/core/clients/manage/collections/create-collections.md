---
title: 建立集合
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中建立集合，更輕鬆地管理使用者和裝置群組。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3f178b41fbb305ef938063bd9b9743daa6b5c69
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695336"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>如何在 Configuration Manager 中建立集合

適用於：  Configuration Manager (最新分支)

集合是使用者或裝置的群組。 請使用集合來執行像是管理應用程式、部署合規性設定，或安裝軟體更新等工作。 您也可以使用集合來管理用戶端設定群組，或搭配角色型系統管理來指定系統管理使用者可以存取的資源。 Configuration Manager 包含數個內建集合。 如需詳細資訊，請參閱[集合簡介](introduction-to-collections.md)。  

> [!NOTE]  
> 集合可包含使用者或裝置，但不能同時包含兩者。  


此文章中的資訊可協助您在 Configuration Manager 中建立集合。 您也可以匯入在目前這個 Configuration Manager 站台或是在其他站台建立的集合。 如需有關如何匯出與匯入集合的詳細資訊，請參閱[如何管理集合](manage-collections.md)。  


## <a name="collection-rules"></a>集合規則

您可以使用不同類型的規則在 Configuration Manager 中設定集合的成員。  


### <a name="direct-rule"></a>直接規則

您可以使用直接規則來選擇要新增到集合的使用者或電腦。 除非從 Configuration Manager 中移除資源，否則這個成員資格不會變更。 Configuration Manager 必須已探索到資源或您必須匯入資源，才可以將它們新增至直接規則集合。 直接規則集合比查詢規則集合具有更高的系統管理負荷，因為需要手動變更。


### <a name="query-rule"></a>查詢規則

依據 Configuration Manager 排程執行的查詢，來動態更新集合的成員資格。 例如，您可以在 Active Directory 網域服務中，建立屬於人力資源組織單位成員的使用者集合。 當人力資源組織單位加入或移除新使用者時，此集合會自動更新。

如需可用來建立集合的查詢範例，請參閱[如何建立查詢](../../../servers/manage/create-queries.md)。


### <a name="device-category-rule"></a>裝置類別規則

透過將裝置類別與裝置集合相關聯，可以更輕鬆地管理裝置。 

如需詳細資訊，請參閱[自動將裝置分類為集合](automatically-categorize-devices-into-collections.md)。<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>包含集合規則

在 Configuration Manager 集合中包含另一個集合的成員。 如果包含的集合有所變更，則目前集合的成員資格會依排程由 Configuration Manager 更新。

您可將多個包含集合規則新增至某個集合。


### <a name="exclude-collection-rule"></a>排除集合規則

排除集合規則可讓您將某一個集合的成員從另一個 Configuration Manager 集合中排除。 如果排除的集合有所變更，則目前集合的成員資格會依排程由 Configuration Manager 更新。

您可將多個排除集合規則新增至某個集合。 如果一個集合同時具有包含集合規則和排除集合規則，就會發生衝突，此時排除集合規則的優先順序會較高。

#### <a name="example"></a>範例
您可以建立一個集合，其中具有一個包含集合規則和一個排除集合規則。 包含集合規則是針對 Dell 桌上型電腦的集合。 排除集合規則是針對 RAM 容量低於 4 GB 的電腦集合。 新的集合會包含至少擁有 4 GB RAM 的 Dell 桌上型電腦。



## <a name="create-a-collection"></a><a name="bkmk_create"></a> 建立集合  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。  

    - 若要建立裝置集合  ，請選取 [裝置集合]  節點。 然後在功能區 [首頁]  索引標籤上的 [建立]  群組中，選取 [建立裝置集合]  。  

    - 若要建立使用者集合  ，請選取 [使用者集合]  節點。 然後在功能區 [首頁]  索引標籤上的 [建立]  群組中，選取 [建立使用者集合]  。  

2. 在精靈的 [一般]  頁面，提供 [名稱]  和 [註解]  。 在 [限制集合]  區段中選取 [瀏覽]  ，以選取限制集合。 您所建立的集合將只會包含來自限制集合的成員。  

4. 在 [成員資格規則]  頁面的 [新增規則]  清單中，選取您要用於此集合的成員資格規則類型。 您可以為每個集合設定多個規則。 每個規則的設定各不相同。 如需有關如何設定每個規則的詳細資訊，請參閱此文章的以下各節：  
    - [直接規則](#bkmk-direct)
    - [查詢規則](#bkmk-query)
    - [裝置類別規則](#bkmk-category)
    - [包含集合規則](#bkmk-include)
    - [排除集合規則](#bkmk-exclude)

5. 此外，在 [成員資格規則]  頁面上，檢閱下列設定。

    - **針對此集合使用累加式更新**：選取此選項可定期掃描，並僅更新上一次集合評估中的新資源或變更的資源。 此流程獨立於完整的集合評估之外。 根據預設，累加式更新的時間間隔為每 5 分鐘發生一次。  

        > [!IMPORTANT]  
        >  具有使用下列類別之查詢規則的集合不支援累加式更新：  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (僅限使用者的集合)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (僅限使用者的集合)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **排程此集合的完整更新**：排程集合成員資格的定期完整評估。  

        從 1810 版開始，集合評估行為的下列變更可改善站台效能：<!--3607726-->  

        - 之前當您在以查詢為基礎的集合上設定排程時，網站會繼續評估查詢是否啟用了 [排程此集合的完整更新]  集合設定。 若要完全停用排程，必須將排程變更為 [無]  。

            現在網站會在您停用此設定時清除排程。 若要指定集合評估排程，請啟用 [排程此集合的完整更新]  選項。  

            當您更新網站時，網站會針對已指定排程的任何現有集合啟用 [排程此集合的完整更新]  選項。 雖然您可能並沒有啟用此設定的意圖，但它是排程中，在您更新站台前的實際行為。 若要停止網站評估集合排程，請停用此選項。  

        - 您無法停用內建集合 (例如 [所有系統]  ) 評估，但現在可以設定排程。 此行為可讓您在符合需求時自訂此動作。 

            > [!TIP]  
            > 在內建集合上，請只變更自訂排程的 [時間]  。 請勿變更 [定期模式]  。 未來反覆項目可能會強制執行特定的定期模式。  

6. 完成精靈以建立新的集合。 新集合會顯示在 [資產與相容性]  工作區的 [裝置集合]  節點中。  

> [!NOTE]  
> 若要查看集合成員，您必須重新整理或重新載入 Configuration Manager 主控台。 直到第一次排定的更新後，它們才會出現在集合中。 您也可以手動為集合選取 [更新成員資格]  。 可能需要幾分鐘的時間才能完成集合更新。  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a> 設定直接規則  

1. 在 [建立直接成員資格規則精靈]  的 [搜尋資源]  頁面上，指定下列資訊。  

    - **資源類別**：選取您要搜尋並新增至集合的資源類型。 例如：
        - **系統資源**：搜尋從用戶端電腦傳回的清查資料。
        - **未知的電腦**：從未知的電腦傳回的值中選取。
        - **使用者資源**：搜尋 Configuration Manager 收集的使用者資訊。
        - **使用者群組資源**：搜尋 Configuration Manager 收集的使用者群組資訊。

    - **屬性名稱**：選取您要搜尋與所選資源類別建立關聯的屬性。 例如：  

        - 如果您想要依 NetBIOS 名稱選取電腦，請選取 [資源類別]  清單中的 [系統資源]  和 [屬性名稱]  清單中的 [NetBIOS 名稱]  。  

        - 如果您想要依組織單位 (OU) 名稱選取使用者，請選取 [資源類別]  清單中的 [使用者資源]  和 [屬性名稱]  清單中的 [使用者 OU 名稱]  。  

    - **排除標記為已過時的資源**：如果用戶端電腦已標記為過時，請不要在搜尋結果中包含此值。  

    - **排除未安裝 Configuration Manager 用戶端的資源**：這些資源將不會顯示在搜尋結果中。  

    - **值**：輸入值以搜尋所選屬性名稱。 使用百分比字元 (%) 作為萬用字元。 例如：  
        - 若要搜尋 NetBIOS 名稱開頭是 "M" 的電腦，請在此欄位中輸入 **M%** 。  
        - 若要在 Contoso OU 中搜尋使用者，請在此欄位中輸入 **Contoso**。

2. 在 [選取資源]  頁面上，從 [資源]  清單中選取您想要新增至集合中的資源，然後選取 [下一步]  。  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a> 設定查詢規則  

在 [查詢規則內容]  對話方塊中，指定下列資訊。  

- **名稱**：指定查詢的唯一名稱。  

- **匯入查詢陳述式**：開啟 [瀏覽查詢]  對話方塊。 選取 [Configuration Manager 查詢](../../../servers/manage/create-queries.md) 以作為集合查詢規則。   

- **資源類別**：選取您要搜尋並新增至集合的資源類型。 從 [系統資源]  選取一個值以搜尋用戶端電腦傳回的清查資料，或選擇 [未知電腦]  以從未知電腦所傳回的值進行選取。  

- **編輯查詢陳述式**：開啟 [查詢陳述式內容]  對話方塊，您可以在其中撰寫查詢以作為集合的規則。 如需查詢的詳細資訊，請參閱[查詢簡介](../../../servers/manage/introduction-to-queries.md)。  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a> 裝置類別規則

[選取裝置類別]  視窗中提供下列動作。

- **建立**：指定名稱以建立新的類別。
- **重新命名**：重新命名選取的類別。
- **刪除**：選取一或多個類別，然後使用此動作將其從清單中移除。

如需詳細資訊，請參閱[自動將裝置分類為集合](automatically-categorize-devices-into-collections.md)。<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a> 設定包含集合規則  

在 [選取集合]  對話方塊中，選取您想要在新集合中包含的集合，然後選取 [確定]  。  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a> 設定排除集合規則  

在 [選取集合]  對話方塊中，選取您想要在新集合中包含的集合，然後選取 [確定]  。  



## <a name="import-a-collection"></a><a name="bkmk_import"></a> 匯入集合  

從站台匯出集合時，Configuration Manager 會將它另存為受控物件格式 (MOF) 檔案。 使用此程序將該檔案匯入至您的站台資料庫。 若要成此程序，您需要集合類別上的**建立**權限。

> [!IMPORTANT]  
> - 請確定檔案僅包含集合資料、來自受信任的來源，而且未遭到竄改。  
> 
> - 請確定檔案是從與您執行相同版本 Configuration Manager 的站台匯出。  

如需有關匯出集合的詳細資訊，請參閱[如何管理集合](manage-collections.md)。


1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。 選取 [使用者集合]  或是 [裝置集合]  節點。  

2. 在功能區 [首頁]  索引標籤的 [建立]  群組中，選取 [匯入集合]  。  

3. 在 [匯入集合精靈]  的 [一般]  頁面上，選取 [下一步]  。  

4. 在 [MOF 檔案名稱]  頁面上，選取 [瀏覽]  。 瀏覽至包含您要匯入之集合資訊的 MOF 檔案。  

5. 完成精靈以匯入集合。 新集合會顯示在 [資產與相容性]  工作區的 [使用者集合]  或 [裝置集合]  節點中。 若要查看新匯入集合的集合成員，請重新整理或重新載入 Configuration Manager 主控台。  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a> 將集合成員資格結果同步至 Azure Active Directory 群組

<!--3607475-->
> [!Tip]  
> 此功能最初是在 1906 版中引進作為[發行前版本功能](../../../servers/manage/pre-release-features.md)。 從 2002 版開始，其不再是發行前版本功能。  

您可以啟用將集合成員資格同步至 Azure Active Directory (Azure AD) 群組。 此同步可讓您根據集合成員資格結果建立 Azure AD 群組成員資格，藉以在雲端中使用現有的內部部署群組規則。 您可以同步裝置集合。 只有含 Azure Active Directory 記錄的裝置會反映於 Azure AD 群組中。 同時支援混合式已加入 Azure AD 和已加入 Azure Active Directory 的裝置。

Azure AD 同步處理會每五分鐘進行一次。 這是一個從 Configuration Manager 到 Azure AD 的單向流程。 在 Azure AD 中進行的變更不會反映在 Configuration Manager 集合中，但也不會由 Configuration Manager 覆寫。 例如，若 Configuration Manager 集合有兩部裝置，而 Azure AD 群組有三部不同裝置，則在同步處理後，Azure AD 群組將會有五部裝置。


### <a name="prerequisites"></a>先決條件

- [雲端管理](../../../servers/deploy/configure/azure-services-wizard.md)
- [Azure Active Directory 使用者探索](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>在 Azure AD 中建立群組並設定擁有者

1. 移至 [https://portal.azure.com](https://portal.azure.com)。
1. 巡覽至 [Azure Active Directory]   > [群組]   > [所有群組]  。
1. 按一下 [新增群組]  ，然後輸入**群組名稱**，並選擇是否輸入**群組描述** (選擇性)。
1. 請確定 [成員資格類型]  是 [已指派]  。
1. 選取 [擁有者]  ，然後在 Configuration Manager 中新增將建立同步關聯性的身分識別。
1. 按一下 [建立]  以完成建立 Azure AD 群組。

### <a name="enable-collection-synchronization-for-the-azure-service"></a>針對 Azure 服務啟用集合同步

1. 在 Configuration Manager 主控台中，移至 [管理]   > [概觀]   > [雲端服務]   > [Azure 服務]  。
1. 以滑鼠右鍵按一下您建立群組所在的 Azure AD 租用戶，然後選取 [屬性]  。
1. 在 [集合同步處理]  索引標籤中，核取 [啟用 Azure Active Directory 群組同步]  的方塊。
1. 按一下 [確定]  以儲存設定。

### <a name="enable-the-collection-to-synchronize"></a>啟用要同步的集合

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]   > [概觀]   > [裝置集合]  。
1. 以滑鼠右鍵按一下要同步的集合，然後按一下 [屬性]  。 
1. 在 [AAD 群組同步]  索引標籤中，按一下 [新增]  。
1. 從下拉式功能表中，選取您建立 Azure AD 群組所在的**租用戶**。
1. 在 [名稱開始是]  欄位中輸入您的搜尋準則，然後按一下 [搜尋]  。
  - 如果系統提示您登入，請使用您指定為 Azure AD 群組擁有者的身分識別。
1. 選取目標群組、按一下 [確定]  以新增群組，然後再按一下 [確定]  以結束集合的屬性。
1. 您必須等候大約 5 到 7 分鐘，才能在 Azure 入口網站中驗證群組成員資格。
   - 若要起始完整同步，以滑鼠右鍵按一下集合，然後選取 [同步處理成員資格]  。


### <a name="verify-the-azure-ad-group-membership"></a>驗證 Azure AD 群組成員資格

1. 移至 [https://portal.azure.com](https://portal.azure.com)。
1. 巡覽至 [Azure Active Directory]   > [群組]   > [所有群組]  。
1. 尋找您所建立的群組，然後選取 [成員]  。 
1. 確認成員會在 Configuration Manager 集合中反映那些項目。
   - 只有具備 Azure AD 身分識別的裝置才會顯示於群組中。


![將集合同步至 Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a> 使用 PowerShell

您可以使用 PowerShell 建立和匯入集合。 如需詳細資訊，請參閱：

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection) \(英文\)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection) \(英文\)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection) \(英文\)

## <a name="next-steps"></a>後續步驟

[管理集合](manage-collections.md)
