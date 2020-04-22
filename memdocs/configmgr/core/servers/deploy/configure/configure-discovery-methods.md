---
title: 設定探索
titleSuffix: Configuration Manager
description: 設定探索方法以從您的網路、Active Directory 及 Azure Active Directory 尋找要管理的裝置。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3bd03cb15ae1633d8ddfc8c2f26a741d2679b083
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704746"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>設定 Configuration Manager 的探索方法

適用於：  Configuration Manager (最新分支)

設定探索方法以從您的網路、Active Directory 及 Azure Active Directory (Azure AD) 尋找要管理的裝置。 請先啟用再設定搜尋環境時所要使用的每個方法。 您也可以使用與啟用方法時所用的相同程序來停用方法。 此程序的唯一例外是「活動訊號探索」和「伺服器探索」︰  

- **活動訊號探索**預設在您安裝 Configuration Manager 主要站台時便已啟用。 它會設定為依基本排程執行。 請將「活動訊號探索」保持啟用。 它可確保裝置的探索資料記錄 (DDR) 是最新的。 如需活動訊號探索的詳細資訊，請參閱[活動訊號相關訊息](about-discovery-methods.md#bkmk_aboutHeartbeat)。  

- **伺服器探索**是一個自動探索方法。 它會尋找您用來作為站台系統的電腦。 不過您無法設定或停用。  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Active Directory 樹系探索  

若要完成 Active Directory 樹系探索的設定，請在下列 Configuration Manager 主控台位置進行設定：  

- 在 [探索方法]  節點中：

  - 啟用此探索方法。  

  - 設定輪詢排程。  

  - 選取探索是否要為 Active Directory 站台和它發現的子網路自動建立界限。  

- 在 [Active Directory 樹系]  節點中：

  - 新增您想要探索的樹系。  

  - 針對 Active Directory 站台和該樹系中的子網路啟用探索。  

  - 配置讓 Configuration Manager 站台將其站台資訊發佈至樹系的設定。  

  - 指派帳戶以當做每個樹系的 Active Directory 樹系帳戶。  

利用下列程序啟用 Active Directory 樹系探索，以及設定個別樹系搭配 Active Directory 樹系探索使用。  

### <a name="configure-active-directory-forest-discovery"></a>設定 Active Directory 樹系探索  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [探索方法]  節點。  

2. 為您要設定探索的站台選取 [Active Directory 樹系探索] 方法。  

3. 在功能區的 [常用]  索引標籤上，選取 [內容]  。  

4. 在 [內容] 的 [一般]  索引標籤上，進行下列設定：  

    - 啟用探索方法。

    - 指定選項以建立所探索位置的站台界限。  

    - 指定探索執行的排程。  

5. 選取 [確定]  儲存設定。  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>設定 Active Directory 樹系探索的樹系  

1. 在 [系統管理]  工作區中，展開 [階層設定]  ，然後選取 [Active Directory 樹系]  節點。 如果 Active Directory 樹系探索之前已執行，您會在結果窗格中看見每個探索到的樹系。 當此探索方法執行時，它會探索本機樹系和任何信任的樹系。 請手動新增未受信任的樹系。  

    - 若要設定先前探索到的樹系，請在結果窗格中選取樹系。 在功能區中，選取 [內容]  以開啟樹系內容。

    - 若要設定未列出的新樹系，在功能區 [常用]  索引標籤的 [建立]  群組中，選取 [新增樹系]  。 這個動作會開啟 [新增樹系]  對話方塊。

2. 在 [一般]  索引標籤上，完成您要探索之樹系的設定，然後指定 [Active Directory 樹系帳戶]  。 如需此帳戶的詳細資訊，請參閱[帳戶](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account)。  

    > [!NOTE]  
    > Active Directory 樹系探索需要通用帳戶，才能探索及發佈至不受信任的樹系。 如果您未使用站台伺服器的電腦帳戶，就只能選取通用帳戶。  

3. 如果您打算讓站台將站台資料發佈至此樹系，可在 [發佈]  索引標籤上完成發佈至此樹系的設定。  

    > [!NOTE]  
    > 如果您讓站台發佈至樹系，請針對 Configuration Manager 延伸該樹系的 Active Directory 架構。 Active Directory 樹系帳戶必須具有該樹系中系統容器的完全控制權限。  

4. 選取 [確定]  儲存設定。  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> 電腦、使用者或群組的 Active Directory 探索  

若要設定電腦、使用者或群組的探索，請從下列常用步驟開始：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [探索方法]  節點。  

2. 為您要設定探索的站台選取方法。  

3. 在功能區的 [常用]  索引標籤上，選取 [內容]  。  

4. 在 [內容] 的 [一般]  索引標籤上，選取核取方塊來啟用探索。 您也可以在現在設定探索，稍後再返回啟用探索。  

接著，使用以下各節中的資訊來設定特定的探索方法：  

- [Active Directory 群組探索](#bkmk_config-adgd)  

- [Active Directory 系統探索](#bkmk_config-adgd)  

- [Active Directory 使用者探索](#bkmk_config-adud)  

> [!NOTE]  
> 本節中的資訊不適用於「Active Directory 樹系探索」。  

雖然每一種探索方法各自獨立，但是有一些類似的選項。 如需這些設定選項的詳細資訊，請參閱[群組、系統和使用者探索的共用選項](about-discovery-methods.md#bkmk_shared)。  

> [!WARNING]  
> 每一種探索方法的 Active Directory 輪詢可能產生相當大的網路流量。 請考慮將每一種探索方法排定在此網路流量不會對網路之業務使用造成負面影響的時段執行。  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a> 設定 Active Directory 群組探索  

1. 在 [Active Directory 群組探索內容] 視窗的 [一般]  索引標籤上，選取 [新增]  來設定探索範圍。 選取 [群組]  或 [位置]  。 然後在 [新增群組]  或 [新增 Active Directory 位置]  對話方塊中完成下列設定：  

    1. 為此探索範圍指定 [名稱]  。  

    2. 指定要搜尋的 [Active Directory 網域]  或 [位置]  ：  

        - 如果您選擇 [群組]  ，請指定一或多個要探索的 Active Directory 群組。  

        - 如果您選擇 [位置]  ，請指定 Active Directory 容器作為要探索的位置。 您也可以針對此位置啟用 Active Directory 子容器的遞迴搜尋。  

    3. 指定站台用來搜尋此探索範圍的 **Active Directory 群組探索帳戶**。 如需詳細資訊，請參閱[帳戶](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account)。  

    4. 選取 [確定]  來儲存探索範圍設定。  

2. 針對您要定義的每個額外探索範圍重複執行上述步驟。  

3. 在 [輪詢排程]  索引標籤上，設定完整探索輪詢排程和差異探索。

4. 在 [選項]  索引標籤上進行設定，以從探索中篩選掉或排除過時的電腦記錄。 此外，也請設定發佈群組的成員資格探索。  

    > [!NOTE]  
    > 根據預設，Active Directory 群組探索只會探索安全性群組的成員資格。  

5. 選取 [確定]  儲存設定。  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a> 設定 Active Directory 系統探索  

1. 在 [Active Directory 系統探索內容] 視窗的 [一般]  索引標籤上，選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif) 來指定新的 Active Directory 容器。 在 [Active Directory 容器]  對話方塊方塊中，完成下列設定︰  

    1. 輸入或瀏覽到適用於**路徑**的位置。 這個值是連至容器或組織單位 (OU) 的有效 LDAP 路徑。 站台會查詢這個資源路徑。 例如， `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. 指定可變更搜尋行為的選項：  

        - **在 Active Directory 群組內探索物件**：站台也會查看此路徑中的群組成員資格。  

        - **以遞迴方式搜尋 Active Directory 子容器**：如果您啟用此選項，站台就會搜尋上述路徑內的任何其他容器或 OU。 如果您停用此選項，站台就只會搜尋特定路徑中的資源。  

          從 1806 版開始，請選取要從此遞迴搜尋中排除的子容器。 此選項有助於減少探索到的物件數目。 選取 [新增]  來選擇上述路徑下方的容器。 在 [選取新的容器] 對話方塊中，選取要排除的子容器。 選取 [確定]  來關閉 [選取新容器] 對話方塊。<!--1358143-->

          > [!Tip]  
          > [Active Directory 系統探索內容] 視窗中的 Active Directory 容器清單會包含 [已設定排除]  欄。 當您選取要排除的容器時，此值為 [是]  。  

    3. 針對每個位置指定要做為 [Active Directory 探索帳戶]  使用的帳戶。 如需詳細資訊，請參閱[帳戶](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account)。  

        > [!TIP]  
        > 您可以針對每個指定的位置，設定一組探索選項和一個唯一的「Active Directory 探索帳戶」。  

    4. 選取 [確定]  以儲存 Active Directory 容器設定。  

2. 在 [輪詢排程]  索引標籤上，設定完整探索輪詢排程和差異探索。  

3. 在 [Active Directory 屬性]  索引標籤上，針對您要探索的電腦設定其他 Active Directory 屬性。 這個索引標籤會列出預設的物件屬性。  

    > [!Tip]  
    > 例如，您的組織要使用 Active Directory 中電腦帳戶上的 **Description** 屬性。 選取 [自訂]  ，然後新增 `Description` 作為自訂屬性。 此探索方法執行之後，這個屬性會顯示在裝置中 Configuration Manager 主控台的 [內容] 索引標籤上。<!--513948-->  

4. 在 [選項]  索引標籤上進行設定，以從探索中篩選掉或排除過時的電腦記錄。  

5. 選取 [確定]  儲存設定。  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a> 設定 Active Directory 使用者探索  

1. 在 [Active Directory 使用者探索內容] 視窗的 [一般]  索引標籤上，選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif) 來指定新的 Active Directory 容器。 在 [Active Directory 容器]  對話方塊方塊中，完成下列設定︰  

    1. 指定要搜尋的一個或多個位置。  

    2. 針對每個位置指定變更搜尋行為的選項。  

    3. 針對每個位置指定要做為 [Active Directory 探索帳戶]  使用的帳戶。 如需詳細資訊，請參閱[帳戶](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account)。  

        > [!NOTE]  
        > 您可以針對每個指定的位置，設定一組唯一的探索選項和一個唯一的「Active Directory 探索帳戶」。  

    4. 選取 [確定]  以儲存 Active Directory 容器設定。  

2. 在 [輪詢排程]  索引標籤上，設定完整探索輪詢排程和差異探索。  

3. 在 [Active Directory 屬性]  索引標籤上，針對您要探索的電腦設定其他 Active Directory 屬性。 這個索引標籤會列出預設的物件屬性。  

4. 選取 [確定]  儲存設定。  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a> Azure AD 使用者探索

「Azure AD 使用者探索」的啟用或設定方式與其他探索方法不同。 請在讓 Configuration Manager 站台在 Azure AD 中上線時設定它。

如需詳細資訊，請參閱 [Azure AD 使用者探索](about-discovery-methods.md#azureaddisc)。

### <a name="prerequisites"></a>先決條件

若要啟用並設定此探索方法，請[設定 Azure 服務](azure-services-wizard.md)來進行**雲端管理**。

如果您使用 Configuration Manager *建立* Azure 應用程式，它會以所需的權限設定應用程式。

如果您先在 Azure 中建立應用程式，然後將其*匯入*至 Configuration Manager 中，則您必須手動設定應用程式。 此設定包括授與伺服器應用程式讀取目錄資料的權限。

1. 以具有*全域管理員*權限的使用者身分，開啟 [Azure 入口網站](https://portal.azure.com)。 移至 [Azure Active Directory]  ，然後選取 [應用程式註冊]  。 視需要切換至 [所有應用程式]  。

1. 選取目標應用程式。

1. 在 [管理]  功能表中，選取 [API 權限]  。  

    1. 在 [API 權限]  面板上，選取 [新增權限]  。  

    2. 在 [要求 API 權限]  面板中，切換至 [我的組織使用的 API]  。  

    3. 搜尋並選取 **Microsoft Graph** API。  

        > [!Tip]
        > 在 1810 版和更舊版本中，請使用 **Azure Active Directory Graph** API。

    4. 選取 [應用程式權限]  群組。 展開 [目錄]  ，然後選取 **Directory.Read.All**。  

    5. 選取 [新增權限]  。  

1. 在 [API 權限]  面板的 [授與同意]  區段中，選取 [授與系統管理員同意...]  。選取 [是]  。  

### <a name="configure-azure-ad-user-discovery"></a>設定 Azure AD 使用者探索

設定**雲端管理** Azure 服務時：

- 在精靈的 [探索]  頁面上，選取 [啟用 Azure Active Directory 使用者探索]  的選項。
- 選取 [設定]  。
- 在 [Azure AD 使用者探索設定] 對話方塊中，設定進行探索的排程。 您也可以啟用差異探索，這將只檢查 Azure AD 中是否有新的或已變更的帳戶。

> [!Note]  
> 如果使用者是同盟或同步處理身分識別，您就必須使用 Configuration Manager [Active Directory 使用者探索](about-discovery-methods.md#bkmk_aboutUser)以及 Azure AD 使用者探索。 如需混合式身分識別的詳細資訊，請參閱[定義混合式身分識別採用策略](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)。<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Azure AD 使用者群組探索

<!--3611956-->
> [!Tip]  
> 此功能最初是在 1906 版中引進作為[發行前版本功能](../../manage/pre-release-features.md)。 從 2002 版開始，其不再是發行前版本功能。  

您可以從 Azure AD 中探索使用者群組和這些群組的成員。 當網站在先前未探索到的 Azure AD 群組中找到使用者時，它會將他們新增為 Configuration Manager 中的新使用者資源。 當群組是安全性群組時，會建立使用者群組資源記錄。

### <a name="prerequisites"></a>先決條件

- 雲端管理 [Azure 服務](azure-services-wizard.md)
- 讀取和搜尋 Azure AD 群組的權限

### <a name="limitations"></a>限制

Azure AD 使用者群組探索的差異探索目前已停用。

### <a name="log-files"></a>記錄檔

請使用 SMS_AZUREAD_DISCOVERY_AGENT.log 來進行疑難排解。 此記錄檔也會與 Azure AD 使用者探索共用。 如需詳細資訊，請參閱[記錄檔](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs)。

### <a name="enable-azure-ad-user-group-discovery"></a>啟用 Azure AD 使用者群組探索

若要在現有的**雲端管理** Azure 服務上啟用探索：

1. 移至 [管理]  工作區、展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。
1. 選取其中一項 Azure 服務，然後選取功能區中的 [內容]  。
1. 在 [探索]  索引標籤上，核取 [啟用 Azure Active Directory 群組探索]  的方塊，然後選取 [設定]  。
1. 選取 [探索範圍]  索引標籤下方的 [新增]  。
    - 您可以在其他索引標籤中修改 [輪詢排程]  。
1. 選取一或多個使用者群組。 您可以依名稱 [搜尋]  ，然後選擇是否要查看 [僅限安全性群組]  。
    - 當您第一次選取 [搜尋]  時，系統會提示您登入至 Azure。
1. 當您完成選取群組時，請選取 [確定]  。
1. 完成執行探索時，您可以在 [使用者]  節點中瀏覽您的 Azure AD 使用者群組。

若要在設定新的**雲端管理** Azure 服務時啟用探索：

- 在精靈的 [探索]  頁面上，選取 [啟用 Azure Active Directory 群組探索]  的選項。
- 選取 [設定]  。
- 在 [Azure AD 群組探索設定] 對話方塊中，設定您的探索範圍以及進行探索的排程。


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> 活動訊號探索

Configuration Manager 會在您安裝主要站台時啟用活動訊號探索方法。 如果您想要使用每七天的預設排程，則不需設定其他項目。 否則，您只需設定用戶端將活動訊號探索資料記錄傳送至管理點的排程。  

> [!NOTE]  
> 如果您在相同站台上啟用用戶端推入安裝和**清除安裝旗標**的站台維護工作，請將活動訊號探索的排程設定為低於**清除安裝旗標**站台維護工作的**用戶端重新探索期間**。 如需站台維護工作的詳細資訊，請參閱[維護工作](../../manage/maintenance-tasks.md)。  

### <a name="configure-the-heartbeat-discovery-schedule"></a>設定活動訊號探索排程  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [探索方法]  節點。  

2. 針對您要設定活動訊號探索的站台，選取**活動訊號探索**方法。  

3. 在功能區的 [常用]  索引標籤上，選取 [內容]  。  

4. 設定用戶端提交活動訊號探索資料記錄的頻率。 然後選取 [確定]  來儲存設定。  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> 網路探索  

設定網路探索之前，請先了解下列主題：  

- 可用的網路探索層級  

- 可用的網路探索選項  

- 限制網路上的網路探索  

如需詳細資訊，請參閱[關於網路探索](about-discovery-methods.md#bkmk_aboutNetwork)。  

下面各節提供有關一般網路探索設定的資訊。 您可以設定同一次探索執行期間使用的其中一項或多項設定。 如果您使用多個設定，請針對可能影響探索結果的互動進行規劃。  

例如，您探索使用特定 SNMP 群體名稱的所有簡易網路管理通訊協定 (SNMP) 裝置。 您會針對同一次探索執行來停用特定子網路上的探索。 執行探索時，「網路探索」不會在您已停用的子網路上探索具有所指定群體名稱的 SNMP 裝置。  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> 判斷您的網路拓撲  

您可以使用拓撲專屬探索對應您的網路。 這類探索不會探索潛在的用戶端。 拓撲專屬網路探索依賴 SNMP。  

對應網路拓撲時，在 [網路探索內容]  對話方塊的 [SNMP]  索引標籤上，設定 [躍點數上限]  。 只需幾個躍點，就有助於控制探索執行時所使用的網路頻寬。 進一步探索網路時，增加躍點數以深入了解您的網路拓撲。  

了解您的網路拓撲之後，設定網路探索的其他內容。 這些內容有助於探索潛在用戶端及其作業系統。 此外，也請設定網路探索來限制其可搜尋的網路區段。  

如需詳細資訊，請參閱[如何判斷您的網路拓撲](#bkmk_proc-top)

### <a name="network-discovery-search-options"></a>網路探索搜尋選項

Configuration Manager 支援使用下列方法來搜尋網路：

- [使用子網路限制搜尋](#BKMK_LimitBySubnet)
- [搜尋特定網域](#BKMK_SearchByDomain)
- [使用 SNMP 群體名稱限制搜尋](#BKMK_LimitBySNMPname)
- [搜尋特定的 DHCP 伺服器](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> 使用子網路限制搜尋  

您可以將網路探索設定為在探索執行期間搜尋特定子網路。 根據預設，網路探索會搜尋執行探索的伺服器子網路。 您設定與啟用的其他任何子網路都只能套用至 SNMP 和 DHCP 搜尋選項。 當「網路探索」搜尋網域時，並不會受到子網路的設定限制。  

如果您在 [網路探索內容]  對話方塊的 [子網路]  索引標籤上指定一或多個子網路，則只會搜尋您標記為**啟用**的子網路。  

當您停用子網路時，站台便會從探索中將它排除，而且適用下列情況：  

- 以 SNMP 為主的查詢無法在子網路上執行。  

- DHCP 伺服器不會使用位於子網路的資源清單來回覆。  

- 網域為主的查詢可以探索位於子網路的資源。  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> 搜尋特定網域  

您可以將網路探索設定為在探索執行期間，搜尋特定網域或一組網域。 根據預設，網路探索會搜尋執行探索的本機伺服器網域。  

如果您在 [網路探索內容]  對話方塊的 [網域]  索引標籤上指定一或多個網域，則只會搜尋您標記為**啟用**的網域。  

當您停用網域時，站台便會從探索中將它排除，而且適用下列情況：  

- 網路探索不會查詢該網域中的網域控制站。  

- SNMP 為主的查詢仍可在網域中的子網路上執行。  

- DHCP 伺服器仍可用位於網域中的資源清單來回覆。  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> 使用 SNMP 群體名稱限制搜尋  

您可以將網路探索設定為在探索執行期間，搜尋特定 SNMP 群體或一組群體。 根據預設，此方法會設定**公開**群體名稱。  

網路探索會使用群體名稱來存取等於 SNMP 裝置的路由器。 路由器會提供網路探索有關其他路由器，以及連結至第一個路由器的子網路的資訊。  

> [!NOTE]  
> SNMP 群體名稱和密碼類似。 「網路探索」只能從您已為其指定群體名稱的 SNMP 裝置取得資訊。 各個 SNMP 裝置皆可擁有自己的群體名稱，但是通常數個裝置會共用相同的群體名稱。 此外，多數的 SNMP 裝置皆有預設的 [公用]  群體名稱。 不過，有些組織會從其裝置刪除 [公用]  群體名稱，以當作安全預防措施。  

如果您在 [網路探索內容]  對話方塊的 [SNMP]  索引標籤上包含多個 SNMP 群體，它就會按照這些群體的顯示順序進行搜尋。 請確定最常使用的名稱會位於清單最上方。 此設定有助於將站台在嘗試使用不同名稱連絡裝置時所產生的網路流量降至最低。

> [!NOTE]  
> 除了使用 SNMP 群體名稱之外，您還可以指定特定 SNMP 裝置的 IP 位址或可解析名稱。 您可以在 [網路探索內容]  對話方塊的 [SNMP 裝置]  索引標籤上執行此動作。  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> 搜尋特定的 DHCP 伺服器  

您可以將網路探索設定為使用特定 DHCP 伺服器或多個伺服器，在探索執行期間探索 DHCP 用戶端。  

網路探索會搜尋您在 [網路探索內容]  對話方塊中的 [DHCP]  索引標籤上指定的各個 DHCP 伺服器。 如果正在執行探索的伺服器會向 DHCP 伺服器租用它的 IP 位址，您可以設定探索來搜尋該 DHCP 伺服器。 使用 [包含設定站台伺服器使用的 DHCP 伺服器]  選項來啟用此行為。  

> [!NOTE]  
> 若要成功設定網路探索中的 DHCP 伺服器，您的環境必須支援 IPv4。 在原生 IPv6 環境中，您無法將「網路探索」設定為使用 DHCP 伺服器。  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> 如何設定網路探索  

使用以下程序，先只探索您的網路拓撲，然後使用一個或多個可用的網路探索選項，將網路探索設定為探索潛在用戶端。  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a> 如何判斷您的網路拓撲  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [探索方法]  節點。  

2. 針對您要探索網路資源的站台選取**網路探索**方法。  

3. 在功能區的 [常用]  索引標籤上，選取 [內容]  。  

    - 在 [一般]  索引標籤上，選取 [啟用網路探索]  的選項。 接著，從 [探索類型]  選項中選取 [拓樸]  。  

    - 在 [子網路]  索引標籤上，選取 [搜尋本機子網路]  選項。  

      > [!TIP]  
      > 如果您知道組成網路的特定子網路，請取消選取 [搜尋本機子網路]  核取方塊。 接著，選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif) 來新增您想要搜尋的特定子網路。 針對大型網路，一次只搜尋一或兩個子網路，以便將網路頻寬的使用量降至最低。  

    - 在 [網域]  索引標籤上，選取 [搜尋本機網域]  的選項。  

    - 在 [SNMP]  索引標籤上，從 [躍點數上限]  下拉式清單中選取選項。 這個選項會指定網路探索在對應您的拓撲時需要多少個路由器躍點。  

      > [!TIP]  
      > 當您首次對應網路拓撲時，只要設定幾個路由器躍點就能將網路頻寬的使用量減到最少。  

4. 在 [排程]  索引標籤上，選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif) 以設定執行探索的排程。  

    > [!NOTE]  
    > 您不能對個別的「網路探索」排程指派不同的探索設定。 每次執行網路探索時，皆會使用目前的探索設定。  

5. 選取 [確定]  以接受設定。 網路探索會在排定的時間執行。  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a> 如何設定網路探索  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [階層設定]  ，然後選取 [探索方法]  節點。  

2. 針對您要探索網路資源的站台選取**網路探索**方法。  

3. 在功能區的 [常用]  索引標籤上，選取 [內容]  。  

4. 在 [一般]  索引標籤上，選取 [啟用網路探索]  的選項。  

    - 從 [探索類型]  選項中，選取您想要執行的探索類型。  

    - 啟用 [低速網路]  選項，讓 Configuration Manager 可用來自動調整低頻寬網路。  

5. 若要設定探索來搜尋子網路，請切換至 [子網路]  索引標籤。接著，設定下列一或多個選項：  

    - 若要在執行探索的本機電腦子網路上執行探索，請啟用 [搜尋本機子網路]  的選項。  

    - 若要搜尋特定子網路，請確認子網路列在 [要搜尋的子網路]  中，且 [搜尋]  值為 [已啟用]  ：  

      1. 如果未列出子網路，請選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif)。 在 [新增子網路指派]  對話方塊中，輸入**子網路**與**遮罩**資訊，然後選取 [確定]  。 預設為啟用新的子網路以進行搜尋。  

      2. 若要變更所列子網路的**搜尋**值，請在清單中選取它。 接著，選取 [切換]  圖示，以便在 [停用]  和 [啟用]  之間切換值。  

6. 若要設定探索來搜尋網域，請切換至 [網域]  索引標籤。接著，設定下列一或多個選項：  

    - 若要在執行探索的電腦網域上執行探索，請啟用 [搜尋本機網域]  的選項。  

    - 若要搜尋特定網域，請確認網域列在 [網域]  中，且 [搜尋]  值為 [已啟用]  ：  

      1. 如果未列出網域，請選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif)。 在 [網域內容]  對話方塊中輸入**網域**資訊，然後選取 [確定]  。 預設為啟用新的網域以進行搜尋。  

      2. 若要變更所列網域的**搜尋**值，請在清單中選取它。 接著，選取 [切換]  圖示，以便在 [停用]  和 [啟用]  之間切換值。  

7. 若要設定探索來搜尋 SNMP 裝置的特定 SNMP 群體名稱，請切換至 [SNMP]  索引標籤。接著，設定下列一或多個選項：  

    - 若要將 SNMP 群體名稱新增至 **SNMP 群體名稱**清單，請選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif)。 在 [新增 SNMP 群體名稱]  對話方塊中，指定 SNMP 群體的**名稱**，然後選取 [確定]  。  

    - 若要移除 SNMP 群體名稱，請選取該群體名稱，然後選取 [刪除]  圖示 ![刪除圖示](media/Disc_delete_Icon.gif)。  

    - 若要調整 SNMP 群體名稱的搜尋順序，從清單中選取群體名稱。 接著，選取 [將項目向上移]  圖示![上移圖示](media/Disc_moveUp_Icon.gif) 或 [將項目向下移]  圖示 ![下移圖示](media/Disc_moveDown_Icon.gif)。 執行探索時，會以由上向下的順序搜尋群體名稱。 

    - 若要設定 SNMP 搜尋所使用的路由器躍點數上限，從 [躍點數上限]  下拉式清單選取躍點數。  

8. 若要設定 SNMP 裝置，請切換至 [SNMP 裝置]  索引標籤。如果未列出裝置，請選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif)。 在 [新增 SNMP 裝置]  對話方塊中，指定 SNMP 裝置的 IP 位址或裝置名稱，然後選取 [確定]  。  

    > [!NOTE]  
    > 如果指定裝置名稱，Configuration Manager 必須能夠將 NetBIOS 名稱解析為 IP 位址。  

9. 若要設定探索來查詢特定的 DHCP 伺服器，請切換至 [DHCP]  索引標籤。接著，設定下列一或多個選項：  

    - 若要查詢正在執行探索之電腦上的 DHCP 伺服器，請啟用 [永遠使用站台伺服器的 DHCP 伺服器]  的選項。  

      > [!NOTE]  
      > 若要使用此選項，伺服器必須向 DHCP 伺服器租用其 IP 位址，且不能使用靜態 IP 位址。  

    - 若要查詢特定的 DHCP 伺服器，請選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif)。 在 [新增 DHCP 伺服器]  對話方塊中，指定 DHCP 伺服器的 IP 位址或伺服器名稱，然後選取 [確定]  。  

      > [!NOTE]  
      > 如果指定伺服器名稱，Configuration Manager 必須能夠將 NetBIOS 名稱解析為 IP 位址。  

10. 若要設定探索執行時間，請切換至 [排程]  索引標籤。然後選取 [新增]  圖示 ![新增圖示](media/Disc_new_Icon.gif) 來設定執行網路探索的排程。 您可以設定多個週期性排程和多個非週期性排程。  

    > [!NOTE]  
    > 如果 [排程]  索引標籤同時顯示多個排程，則網路探索會針對所有排程，按照排程上指示的設定時間執行。 此行為也適用於週期性排程。  

11. 選取 [確定]  以儲存設定。  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> 如何確認網路探索是否已完成  

完成「網路探索」所需的時間可能因下列一或多個因素而有所不同：  

- 網路的大小  

- 網路的拓撲  

- 設定為尋找網路中路由器的躍點數目上限  

- 執行的探索類型  

網路探索不會在其完成時，建立訊息來警示您。 使用下列程序來確認探索已完成：  

1. 在 Configuration Manager 主控台中，按一下 [監視]  工作區。 展開 [系統狀態]  ，然後選取 [狀態訊息查詢]  節點。  

2. 選取 [所有狀態訊息]  查詢。  

3. 在功能區 [常用]  索引標籤的 [狀態訊息查詢]  群組中，選取 [顯示訊息]  。  

4. 在 [所有狀態訊息] 視窗中，從 [選取日期和時間]  下拉式清單中選取值，其中包含探索是在多久以前開始。 接著，選取 [確定]  以開啟 **Configuration Manager 狀態訊息檢視器**。  

    > [!TIP]  
    > 您也可以使用 [指定日期和時間]  選項以選取您執行探索的特定日期和時間。 如果您在特定日期執行網路探索，並且只想要擷取該日期的訊息時，此選項就很有用。  

5. 若要驗證網路探索是否完成，請搜尋包含下列詳細資料的狀態訊息：  

    - 訊息識別碼：**502**  

    - 元件：**SMS_NETWORK_DISCOVERY**  

    - 描述:**此元件已停止**  

    如果未出現此狀態訊息，表示「網路探索」尚未完成。  

6. 若要在網路探索開始時進行驗證，請搜尋包含下列詳細資料的狀態訊息：  

    - 訊息識別碼：**500**  

    - 元件：**SMS_NETWORK_DISCOVERY**  

    - 描述:**此元件已啟動**  

    這項資訊會確認網路探索已啟動。 如果沒有此資訊，請重新排定「網路探索」。  
