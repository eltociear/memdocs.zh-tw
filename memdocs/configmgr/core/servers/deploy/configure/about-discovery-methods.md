---
title: 探索方法
titleSuffix: Configuration Manager
description: 了解在您的網路上、從 Active Directory 或 Azure Active Directory 尋找裝置時，可用的探索方法。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 68e622d45de6575ec0f652f33934654cd1481dc2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704996"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>關於 Configuration Manager 的探索方法

適用於：  Configuration Manager (最新分支)

Configuration Manager 探索方法可在您的網路上尋找各種不同裝置、從 Active Directory 尋找裝置和使用者，或從 Azure Active Directory (Azure AD) 尋找使用者。 若要有效利用探索方法，您應該了解其可用的設定和限制。  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a> Active Directory 樹系探索  
 **可設定：** 是  

 **預設啟用：** 否  

 可用來執行這個方法的**帳戶**︰  

-   **Active Directory 樹系探索帳戶** (使用者定義)  

-   站台伺服器的**電腦帳戶**  

與其他 Active Directory 探索方法不同，Active Directory 樹系探索不會探索您可管理的資源。 取而代之的是，此方法會探索 Active Directory 中設定的網路位置。 它可以將這些位置轉換成可在您整個階層中使用的界限。  

這個方法執行時會搜尋本機 Active Directory 樹系、每個信任的樹系，以及每個您在 Configuration Manager 主控台 **Active Directory 樹系**節點設定的其他樹系。  

使用 Active Directory 樹系探索，以：  

-   探索 Active Directory 站台和子網路，然後根據這些網路位置建立 Configuration Manager 界限。  

-   識別已指派給 Active Directory 站台的超網路。 將每個超網路轉換成 IP 位址範圍界限。  

-   當允許發佈至某個樹系時，發佈至該樹系中的 Active Directory Domain Services (AD DS)。 指定的「Active Directory 樹系帳戶」必須具有該樹系的權限。  

您可以在 Configuration Manager 主控台中管理「Active Directory 樹系探索」。 移至 [系統管理]  工作區，然後展開 [階層設定]  。   

-   **探索方法**：讓「Active Directory 樹系探索」在階層的頂層站台上執行。 您也可以指定簡單的排程來執行探索。 請將它設定為自動從其探索的 IP 子網路和 Active Directory 站台建立界限。 Active Directory 樹系探索無法在子主要站台或次要站台上執行。  

-   **Active Directory 樹系**：設定要探索的額外樹系、指定每個「Active Directory 樹系帳戶」，並設定發佈至每個樹系。 監視探索程序。 將 IP 子網路和 Active Directory 站台新增為 Configuration Manager 界限及界限群組的成員。  

若要設定將階層中每個站台發佈至 Active Directory 樹系，請將您的 Configuration Manager 主控台連線至階層的頂層站台。 Active Directory 站台 [內容]  對話方塊中的 [發佈]  索引標籤只能顯示目前的站台及其子站台。 針對樹系啟用發佈且已針對 Configuration Manager 延伸該樹系的架構時，就會為獲允許發佈至該 Active Directory 樹系的每個站台發佈下列資訊：  

-    **SMS-Site-&lt;站台碼>**

-   **SMS-MP-&lt;站台碼>-&lt;站台系統伺服器名稱>**  

-   **SMS-SLP-&lt;站台碼>-&lt;站台系統伺服器名稱>**  

-   **SMS-&lt;站台碼>-&lt;Active Directory 站台名稱或子網路>**  

> [!NOTE]  
>  次要網站一律使用次要網站伺服器電腦帳戶發佈至 Active Directory。 如果您要由次要站台發佈至 Active Directory，請確定次要站台伺服器電腦具備發佈至 Active Directory 的權限。 次要站台無法將資料發佈至不信任的樹系。  

> [!CAUTION]  
>  取消選取選項以將站台發佈至 Active Directory 樹系時，該站台先前發佈的所有資訊，包括可用的站台系統角色，都會 Active Directory 中移除。  

Active Directory 樹系探索動作會記錄在下列記錄中：  

-   所有動作 (但不包括與發佈相關的動作) 都會記錄在站台伺服器上 **&lt;安裝路徑>\Logs** 資料夾的 **ADForestDisc.Log** 檔案中。  

-   Active Directory 樹系探索的發佈活動會記錄在站台伺服器 **&lt;安裝路徑>\Logs** 資料夾的 **hman.log** 和 **sitecomp.log** 檔案中。  

如需有關如何設定此探索方法的詳細資訊，請參閱[設定探索方法](configure-discovery-methods.md#BKMK_ConfigADForestDisc)。  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a> Active Directory 群組探索  
**可設定：** 是  

**預設啟用：** 否  

可用來執行這個方法的**帳戶**︰  

-   **Active Directory 群組探索帳戶** (使用者定義)  

-   站台伺服器的**電腦帳戶**  

> [!TIP]  
>  除了本節中的資訊，請參閱 [Common features of Active Directory Group, System, and User Discovery](#bkmk_shared) (Active Directory 群組、系統和使用者探索的通用功能)。  

使用此方法搜尋 Active Directory Domain Services，以識別︰  

-   本機、全域和萬用安全性群組。  

-   群組的成員資格。  

-   群組成員電腦與使用者的有限資訊，即使另一個探索方法先前未探索到這些電腦與使用者亦然。  

此探索方法的目的在於識別群組以及群組成員的群組關係。 根據預設，僅會探索安全性群組。 如果您也想找到發佈群組的成員資格，就必須在 [Active Directory 群組探索內容]  對話方塊的 [選項]  索引標籤上選取 [探索發佈群組的成員資格]  選項方塊。  

「Active Directory 群組探索」不支援可使用「Active Directory 系統探索」或「Active Directory 使用者探索」來識別的延伸 Active Directory 屬性。 由於此探索方法未最佳化以探索電腦和使用者資源，因此請考慮在執行「Active Directory 系統探索」和「Active Directory 使用者探索」之後，再執行此探索方法。 之所以這麼建議，是因為此方法會為群組建立完整的探索資料記錄 (DDR)，但針對作為群組成員的電腦和使用者，則只會建立有限的 DDR。  

您可以設定下列探索範圍以控制此方法搜尋資訊的方式：  

-   **位置**：請使用位置來搜尋一個或多個 Active Directory 容器。 此範圍選項支援以遞迴方式搜尋指定的 Active Directory 容器。 此程序會搜尋您指定容器下的每個子容器。 它會繼續執行，直到找不到任何其他子容器為止。  

-   **群組**：請使用群組來搜尋一個或多個特定 Active Directory 群組。 您可以將 [Active Directory 網域]  設定為使用預設網域和樹系，或縮小個別網域控制站的搜尋範圍。 此外，您還可以指定一個或多個要搜尋的群組。 如果您未指定至少一個群組，則會搜尋在指定的 [Active Directory 網域]  位置中找到的所有群組。  

> [!CAUTION]  
>  當您設定探索範圍時，請僅選擇您必須探索的群組。 之所以這麼建議，是因為「Active Directory 群組探索」會嘗試探索該探索範圍中每個群組的每個成員。 大型群組的探索會需要使用大量的頻寬和 Active Directory 資源。  

> [!NOTE]  
>  您必須先視您想要探索的對象而定，執行「Active Directory 系統探索」或「Active Directory 使用者探索」，才能建立以延伸之 Active Directory 屬性為基礎的集合，並確保電腦和使用者的探索結果正確。  

Active Directory 群組探索動作會記錄在站台伺服器 **&lt;裝路徑\>\LOGS** 資料夾的 **adsgdis.log** 檔案中。  

如需有關如何設定此探索方法的詳細資訊，請參閱[設定探索方法](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral)。  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a> Active Directory 系統探索  
**可設定：** 是  

**預設啟用：** 否  

可用來執行這個方法的**帳戶**︰  

-   **Active Directory 系統探索帳戶** (使用者定義)  

-   站台伺服器的**電腦帳戶**  

> [!TIP]  
>  除了本節中的資訊，請參閱 [Common features of Active Directory Group, System, and User Discovery](#bkmk_shared) (Active Directory 群組、系統和使用者探索的通用功能)。  

使用此探索方法來搜尋指定的 Active Directory Domain Services 位置，以尋找可用來建立集合與查詢的電腦資源。 您也可以使用用戶端推入安裝，將 Configuration Manager 用戶端安裝在探索到的裝置上。  

此方法預設會探索電腦的相關基本資訊，包括下列屬性：  

-   電腦名稱  

-   作業系統和版本  

-   Active Directory 容器名稱  

-   IP 位址  

-   Active Directory 站台  

-   上次登入時間戳記  

若要成功建立電腦的 DDR，Active Directory 系統探索必須能夠識別電腦帳戶，然後成功將電腦名稱解析為 IP 位址。  

在 [Active Directory 系統探索內容]  對話方塊中的 [Active Directory 屬性]  索引標籤上，您可以檢視它所探索的預設物件屬性完整清單。 您也可以設定方法以探索額外 (擴充) 的屬性。  

Active Directory 系統探索動作會記錄在站台伺服器 **&lt;裝路徑\>\LOGS** 資料夾的 **adsysdis.log** 檔案中。  

如需有關如何設定此探索方法的詳細資訊，請參閱[設定探索方法](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral)。  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a> Active Directory 使用者探索  
**可設定：** 是  

**預設啟用：** 否  

可用來執行這個方法的**帳戶**︰  

-   **Active Directory 使用者探索帳戶** (使用者定義)  

-   站台伺服器的**電腦帳戶**  

> [!TIP]  
>  除了本節中的資訊，請參閱 [Common features of Active Directory Group, System, and User Discovery](#bkmk_shared) (Active Directory 群組、系統和使用者探索的通用功能)。  

使用此探索方法來搜尋 Active Directory Domain Services，以識別使用者帳戶和相關屬性。 此方法預設會探索使用者帳戶的相關基本資訊，包括下列屬性：  

-   使用者名稱  

-   唯一的使用者名稱 (包括網域名稱)  

-   Domain  

-   Active Directory 容器名稱  

在 [Active Directory 使用者探索內容]  對話方塊中的 [Active Directory 屬性]  索引標籤上，您可以檢視它所探索的預設物件屬性完整清單。 您也可以設定方法以探索額外 (擴充) 的屬性。

Active Directory 使用者探索動作會記錄在站台伺服器 **&lt;安裝路徑\>\LOGS** 資料夾的 **adusrdis.log** 檔案中。  

如需有關如何設定此探索方法的詳細資訊，請參閱[設定探索方法](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral)。  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a> Azure Active Directory 使用者探索

您可以使用「Azure Active Directory (Azure AD) 使用者探索」來搜尋 Azure AD 訂用帳戶是否有具有新式雲端身分識別的使用者。 Azure AD 使用者探索可以尋找下列屬性：

- objectId
- displayName
- mail
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName
- AAD tenantID
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistinguishedName

此方法支援從 Azure AD 以完整或差異方式同步處理使用者屬性。 此資訊接著可搭配您透過其他探索方法所收集到的探索資料使用。

Azure AD 使用者探索的動作會記錄在位於階層頂層站台伺服器上的 **SMS_AZUREAD_DISCOVERY_AGENT.log** 檔案中。

若要設定 Azure AD 使用者探索，請參閱[設定 Azure 服務](azure-services-wizard.md)以進行雲端管理。 如需有關如何設定此探索方法的相關資訊，請參閱[設定 Azure AD 使用者探索](configure-discovery-methods.md#azureaadisc)。

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Azure Active Directory 使用者群組探索
<!--3611956-->
*(在 1906 版中當作[發行前版本功能](../../manage/pre-release-features.md)推出)*

您可以從 Azure Active Directory (Azure AD) 中探索使用者群組和這些群組的成員。 Azure AD 使用者群組探索可以尋找下列屬性：

- objectId
- displayName
- mailNickname
- onPremisesSecurityIdentifier
- AAD tenantID

Azure AD 使用者群組探索的動作會記錄在位於階層頂層站台伺服器上的 **SMS_AZUREAD_DISCOVERY_AGENT.log** 檔案中。 如需有關如何設定此探索方法的資訊，請參閱[設定 Azure AD 使用者群組探索](configure-discovery-methods.md#bkmk_azuregroupdisco)。

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a> 活動訊號探索  
**可設定：** 是  

**預設啟用：** 是  

可用來執行這個方法的**帳戶**︰  

-   站台伺服器的**電腦帳戶**  

活動訊號探索與其他 Configuration Manager 探索方法不同。 依預設會啟用此項，並在每個電腦用戶端 (而不是站台伺服器) 上執行，以建立 DDR。 若為行動裝置用戶端，則會由行動裝置用戶端正在使用的管理點來建立此 DDR。 為協助維護 Configuration Manager 用戶端的資料庫記錄，請勿停用活動訊號探索。 除了維護資料庫記錄之外，此方法還可強制將電腦探索為新的資源記錄。 此外，它也可以重新填入已從資料庫刪除的電腦資料庫記錄。  

「活動訊號探索」會依據針對階層中所有用戶端設定的排程執行。 「活動訊號探索」的預設排程是設定為每 7 天一次。 如果您變更活動訊號探索間隔，請確定其執行頻率比站台維護工作 [刪除過時探索資料]  的執行頻率高。 此工作會從站台資料庫刪除非作用中的用戶端記錄。 您只能針對主要站台設定 [刪除過時探索資料]  工作。 

您也可以在特定用戶端上手動叫用「活動訊號探索」。 請執行用戶端 Configuration Manager 控制台之 [動作]  索引標籤上的 [探索資料收集週期]  。  

當活動訊號探索執行時，會建立具有用戶端目前資訊的 DDR。 然後用戶端會將這個小檔案 (大小約 1 KB) 複製到管理點，以便主要站台加以處理。 此檔案具有下列資訊：  

-   網路位置  

-   NetBIOS 名稱  

-   用戶端代理程式版本  

-   操作狀態詳細資料  

活動訊號探索是唯一提供用戶端安裝狀態詳細資訊的探索方法。 其執行作業的方法是更新系統資源用戶端屬性，設定等於 [是]  的值。  

> [!NOTE]  
>  即使停用活動訊號探索，仍會建立 DDR，並針對作用中行動裝置用戶端提交。 此行為可確保 [刪除過時探索資料]  工作不會影響作用中的行動裝置。 當 [刪除過時探索資料]  工作刪除行動裝置的資料庫記錄時，也會撤銷裝置憑證。 此動作會讓行動裝置無法連線至管理點。  

活動訊號探索動作會記錄在以下位置：  

-   若為電腦用戶端，則會將活動訊號探索動作記錄在用戶端 *%Windir%\CCM\Logs* 資料夾的 **InventoryAgent.log** 檔案中。  

-   若為行動裝置用戶端，活動訊號探索動作則會記錄在行動裝置用戶端所使用管理點 *%Program Files%\CCM\Logs* 資料夾中的 **DMPRP.log** 檔案內。  

如需有關如何設定此探索方法的詳細資訊，請參閱[設定探索方法](configure-discovery-methods.md#BKMK_ConfigHBDisc)。  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a> 網路探索  
**可設定：** 是  

**預設啟用：** 否  

可用來執行這個方法的**帳戶**︰  

-   站台伺服器的**電腦帳戶**  

使用此方法探索網路拓撲，以及探索具有 IP 位址的網路裝置。 「網路探索」會藉由查詢下列實體，搜尋您的網路是否有已啟用 IP 的資源： 
- 執行 Microsoft 之 DHCP 實作的伺服器
- 網路路由器中的「位址解析通訊協定」(ARP) 快取
- 具備 SNMP 功能的裝置
- Active Directory 網域  

使用網路探索之前，必須先指定執行探索的*層級*。 您也要設定可啟用網路探索來查詢網路區段或裝置的一個或多個探索機制。 您也可以設定能協助控制網路上探索動作的設定。 最後，您要定義網路探索執行的一或多個排程。  

為了讓這個方法成功探索資源，網路探索必須找出資源的 IP 位址和子網路遮罩。 找出物件子網路遮罩的方法如下：  

-   **路由器 ARP 快取：** 網路探索會查詢路由器的 ARP 快取，以尋找子網路資訊。 通常，路由器 ARP 快取中資料的存留時間都很短。 因此，當網路探索查詢 ARP 快取時，ARP 快取可能已不再具有所要求物件的資訊。  

-   **DHCP：** 網路探索會查詢您指定要探索裝置的各個 DHCP 伺服器，以了解 DHCP 伺服器提供的使用期。 網路探索僅支援執行 Microsoft DHCP 實作的 DHCP 伺服器。  

-   **SNMP 裝置：** 網路探索可以直接查詢 SNMP 裝置。 若要讓網路探索查詢裝置，該裝置必須安裝本機 SNMP 代理程式。 此外，請將「網路探索」設定為使用 SNMP 代理程式正在使用的群體名稱。  

當探索辨識出可 IP 定址的物件，並可判斷物件子網路遮罩時，便會建立該物件的 DDR。 由於會有不同類型的裝置連線到網路，因此「網路探索」會探索出不支援 Configuration Manager 用戶端的資源。 例如，可以探索出但並不受管理的裝置，包括印表機和路由器。  

網路探索可以傳回數種屬性，作為其建立之探索記錄的一部分。 這些屬性包括：  

-   NetBIOS 名稱  

-   IP 位址  

-   資源網域  

-   系統角色  

-   SNMP 社群名稱  

-   MAC 位址  

網路探索活動會記錄在執行探索的站台伺服器 *&lt;安裝路徑\>\Logs* 的 **Netdisc.log** 檔案中。  

 如需有關如何設定此探索方法的詳細資訊，請參閱[設定探索方法](configure-discovery-methods.md#BKMK_ConfigNetworkDisc)。  

> [!NOTE]  
>  複雜網路和低頻寬的連線會導致網路探索執行速度緩慢，並產生明顯的網路流量。 最佳作法是只在其他探索方法無法找出您必須探索的資源時，才執行網路探索。 例如，若您必須探索工作群組電腦，就請使用網路探索。 其他探索方法不會探索工作群組電腦。  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a> 網路探索的層級  
設定網路探索時，要從三個探索層級中指定一個：  

|探索的層級|詳細資料|  
|------------------------|-------------|  
|拓撲|此層級會探索路由器和子網路，但不會識別出物件的子網路遮罩。|  
|拓撲和用戶端|除了拓撲外，此層級也會探索潛在用戶端 (如電腦) 和資源 (如印表機和路由器)。 此探索層級會嘗試識別出所找到物件的子網路遮罩。|  
|拓撲、用戶端和用戶端作業系統|除了拓撲與潛在用戶端外，此層級也會嘗試探索電腦作業系統名稱和版本。 此層級會使用 Windows 瀏覽器和 Windows 網路功能呼叫。|  

 隨著層級遞增，網路探索也會隨之增加其活動和網路頻寬使用量。 請考量在您啟用網路探索所有面向前可能會產生的網路流量。  

 例如，第一次使用網路探索時，您可能只會以拓撲層級來開始，以識別您的網路基礎結構。 接著，請重新設定「網路探索」，以探索物件及其裝置作業系統。 您也可以進行設定，將網路探索限制在特定網路區段範圍內。 這樣一來，您就可以在所需的網路位置中探索物件，而避免不必要的網路流量。 此程序也可讓您從邊緣路由器或網路外部探索物件。  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a> 網路探索選項  
若要讓「網路探索」能夠搜尋可 IP 定址的裝置，請設定這其中的一或多個選項。  

> [!NOTE]  
>  網路探索會在執行探索之站台伺服器的電腦帳戶內容中執行。 如果電腦帳戶沒有不信任網域的權限，網域與 DHCP 伺服器設定就無法探索資源。  

#### <a name="dhcp"></a>DHCP  

指定要網路探索進行查詢的每個 DHCP 伺服器。 (網路探索僅支援執行 Microsoft DHCP 實作的 DHCP 伺服器)。  

-   網路探索會使用遠端程序呼叫 DHCP 伺服器的資料庫，來擷取資訊。  

-   網路探索可以同時查詢 32 位元和 64 位元 DHCP 伺服器，以找出每個伺服器上註冊的裝置清單。  

-   若要讓網路探索成功查詢 DHCP 伺服器，執行探索之伺服器的電腦帳戶必須是 DHCP 伺服器上 DHCP 使用者群組的成員。 例如，當下列其中一個陳述為真時，便會有此層級的存取權：  

    -   指定的 DHCP 伺服器是執行探索之伺服器的 DHCP 伺服器。  

    -   執行探索的電腦與 DHCP 伺服器位於同一網域。  

    -   在執行探索的電腦與 DHCP 伺服器間存在雙向信任。  

    -   站台伺服器是 DHCP 使用者群組的成員。  

-   網路探索列舉 DHCP 伺服器時，不會每次都找到靜態 IP 位址。 網路探索不會找到 DHCP 伺服器上在 IP 位址排除範圍內的 IP 位址， 也不會探索已保留供手動指派的 IP 位址。  

#### <a name="domains"></a>網域  

指定要網路探索進行查詢的每個網域。  

-   執行探索的站台伺服器電腦帳戶必須具備權限，才能讀取每個指定網域中的網域控制站。  

-   若要從本機網域探索電腦，您必須至少在一部電腦上啟用「電腦瀏覽器」服務。 此電腦所在的子網路必須與執行「網路探索」的站台伺服器相同。  

-   網路探索可以在您瀏覽網路時探索出可從站台伺服器上檢視的所有電腦。  

-   「網路探索」會擷取 IP 位址。 接著，它會使用「網際網路控制訊息通訊協定」(ICMP) 回應要求，針對所找到的每個裝置執行 Ping。 **ping** 命令可協助判斷目前作用中的電腦。  

#### <a name="snmp-devices"></a>SNMP 裝置  

指定要網路探索進行查詢的每個 SNMP 裝置。  

-   網路探索會從回應該查詢的 SNMP 裝置擷取 ipNetToMediaTable 值。 此值會傳回用戶端電腦或其他資源 (如印表機、路由器或其他可 IP 定址的裝置) 的 IP 位址陣列。  

-   若要查詢某個裝置，您必須指定該裝置的 IP 位址或 NetBIOS 名稱。  

-   將「網路探索」設定為使用裝置的群體名稱，否則裝置會拒絕以 SNMP 為基礎的查詢。  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a> 限制網路探索  
當「網路探索」查詢位於網路邊緣的 SNMP 裝置時，可以識別出位於您直接網路外之子網路和 SNMP 裝置的相關資訊。 您可經由設定可與探索通訊的 SNMP 裝置，以及指定要查詢的網路區段，使用下列資訊來限制網路探索。  

#### <a name="subnets"></a>子網路  

設定網路探索在使用 SNMP 和 DHCP 選項時查詢的子網路。 這兩個選項只會搜尋已啟用的子網路。  

例如，DHCP 要求可以從整個網路的某個位置傳回裝置。 如果您想要只探索特定子網路上的裝置，請在 [網路探索內容]  對話方塊的 [子網路]  索引標籤上指定和啟用該特定子網路。 當您指定和啟用子網路時，會將未來的 DHCP 和 SNMP 探索工作限制在這些子網路。  

> [!NOTE]  
>  子網路設定不會限制 [網域]  探索選項所探索的物件。  

#### <a name="snmp-community-names"></a>SNMP 群體名稱  

若要讓「網路探索」能夠順利查詢 SNMP 裝置，請為「網路探索」設定裝置的群體名稱。 如果網路探索不是使用 SNMP 裝置的群體名稱進行設定，裝置會拒絕查詢。  

#### <a name="maximum-hops"></a>躍點數上限  

當您設定路由器躍點數上限時，會限制網路探索可使用 SNMP 查詢的網路區段和路由器數目。  

您所設定的躍點數目，會限制網路探索可查詢之其他裝置和網路區段數目。  

例如，含 **0** (零) 路由器躍點的僅拓撲探索，會探索原始伺服器所在的子網路。 這包含該子網路上的任何路由器。  

下圖顯示僅拓撲網路探索查詢在伺服器 1 上，指定了 0 路由器躍點的情況下執行時，找到的項目：子網路 D 和路由器 1。  

 ![以零個路由器跳躍點進行探索的影像](media/Disc-0.gif)  

 下圖顯示拓撲和用戶端網路探索查詢在伺服器 1 上，指定了 0 路由器躍點的情況下執行時，找到的項目：子網路 D 和路由器 1，以及子網路 D 上所有潛在用戶端。  

 ![以一個路由器跳躍點進行探索的影像](media/Disc-1.gif)  

 若要得知其他路由器躍點是如何增加探索的網路資源量，請考慮下列網路：  

 ![以兩個路由器跳躍點進行探索的影像](media/Disc-2.gif)  

 從伺服器 1 使用一個路由器躍點執行拓撲專屬「網路探索」時會探索到下列實體：  

-   路由器 1 和子網路 10.1.10.0 (用零個躍點找到)  

-   子網路 10.1.20.0 和 10.1.30.0、子網路 A 和路由器 2 (在第一個躍點上找到)  

> [!WARNING]  
>  每次增加路由器躍點數目，都會大幅提高可探索的資源數目，以及增加網路探索所使用的網路頻寬。  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a> 伺服器探索  
**可設定：** 否  

除了使用者可設定的探索方法外，Configuration Manager 會使用一種名為**伺服器探索** (SMS_WINNT_SERVER_DISCOVERY_AGENT) 的處理序。 這個探索方法會為站台系統的電腦 (例如設定為管理點的電腦) 建立資源記錄。  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a> Active Directory 群組探索、系統探索及使用者探索的通用功能  
本節提供下列探索方法之通用功能的資訊︰  

-   Active Directory 群組探索  

-   Active Directory 系統探索  

-   Active Directory 使用者探索  

> [!NOTE]  
>  本節中的資訊不適用於 Active Directory 樹系探索。  

這三種探索方法在設定及操作方面相當類似。 這些方法可以探索電腦、使用者，以及儲存在 Active Directory Domain Services 中與資源群組成員資格相關的資訊。 此探索程序會由探索代理程式管理。 此代理程式會在已設定執行探索之每個站台的站台伺服器上執行。 您可以設定每一種探索方法來搜尋一個或多個 Active Directory 位置，作為本機樹系或遠端樹系中的位置執行個體。  

當探索搜尋不受信任的樹系以尋找資源時，探索代理程式必須能成功解析下列情況：  

-   若要使用 Active Directory 系統探索來探索電腦資源，探索代理程式必須能解析資源的 FQDN。 如果它無法解析 FQDN，就會嘗試依其 NetBIOS 名稱來解析資源。  

-   若要使用 Active Directory 使用者探索或 Active Directory 群組探索來探索使用者或群組資源，探索代理程式必須能解析您為 Active Directory 位置指定的網域控制站名稱 FQDN。  

您可以針對指定的每個位置，設定個別的搜尋選項，例如啟用遞迴式搜尋來搜尋 Active Directory 子容器位置。 您也可以設定唯一的帳戶以便在搜尋該位置時使用。 此帳戶可提供彈性，亦即在一個站台上設定探索方法，即可跨多個樹系搜尋多個 Active Directory 位置。 您不需要設定一個對所有位置都具有權限的單一帳戶。  

當您在特定站台上執行這三種探索方法時，該站台上的 Configuration Manager 站台伺服器會連絡指定 Active Directory 樹系中最近的網域控制站，以找出 Active Directory 資源。 網域和樹系可以處於任何支援的 Active Directory 模式中。 您指派給每個位置執行個體的帳戶都必須擁有指定 Active Directory 位置的**讀取**權限。

探索會在指定的位置上搜尋物件，然後嘗試收集與這些物件相關的資訊。 當能夠識別足夠的資源相關資訊時便建立 DDR。 必要的資訊會依使用的探索方法而有所不同。  

如果您要設定在不同 Configuration Manager 站台上執行相同的探索方法，以善用本機 Active Directory 伺服器查詢，您可以使用一組唯一的探索選項來設定每個站台。 由於探索資料會在階層中的每個站台間共用，因此請避免重複這些設定以便一次就有效率地探索每個資源。

針對較小的環境，請考慮只在您階層內的一個站台上執行每個探索方法。 此設定可降低系統管理額外負荷，也可降低多個探索動作重新探索相同資源的可能性。 當您將執行探索的站台數目降到最低時，就會減少探索所使用的整體網路頻寬。 您也可以減少站台伺服器所建立及必須處理的整體 DDR 數目。  

許多的探索方法設定都一目了然。 請利用以下各節取得與探索選項相關的詳細資訊，在設定這些選項之前您可能會需要額外的資訊。  

搭配多個 Active Directory 探索方法可使用下列選項︰  

-   [差異探索](#bkmk_delta)  

-   [依網域登入來篩選過時的電腦記錄](#bkmk_stalelogon)  

-   [依電腦密碼篩選過時的記錄](#bkmk_stalepassword)  

-   [搜尋自訂的 Active Directory 屬性](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a> 差異探索  
可用於：  

-   Active Directory 群組探索  

-   Active Directory 系統探索  

-   Active Directory 使用者探索  

差異探索並非獨立的探索方法，而是適用探索方法的可用選項。 差異探索會搜尋特定的 Active Directory 屬性，自適用的探索方法上次完整探索週期後是否有所變更。 屬性變更會提交至 Configuration Manager 資料庫以更新資源的探索記錄。  

差異探索的執行週期預設為 5 分鐘。 此排程比一般完整探索週期排程更為頻繁。 如此頻繁的週期是可行的，因為差異探索使用的站台伺服器和網路資源比完整探索週期少。 使用差異探索時，您可以降低該探索方法的完整探索週期頻率。  

以下是差異探索最常偵測到的變更：  

-   將新的電腦或使用者新增到 Active Directory  

-   基本的電腦和使用者資訊的變更  

-   新增到群組的新電腦或使用者  

-   從群組移除的電腦或使用者  

-   系統群組物件的變更  

儘管差異探索可以偵測到新的資源與群組成員資格的變更，但當資源已從 Active Directory 刪除時，就無法偵測。 差異探索所建立與完整探索週期所建立之 DDR 的處理方式類似。  

您可以在每種探索方法的內容中的 [輪詢排程]  索引標籤上設定差異探索。  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a> 依網域登入來篩選過時的電腦記錄  
可用於：  

-   Active Directory 群組探索  

-   Active Directory 系統探索  

您可以設定讓探索排除具有過時電腦記錄的電腦。 此排除動作會根據電腦的上次網域登入時間。 當啟用此選項時，Active Directory 系統探索會評估其識別的每部電腦。 Active Directory 群組探索則會評估所探索的群組成員的每一部電腦。  

若要使用此選項：  

-   必須設定電腦更新 Active Directory 網域服務的 **lastLogonTimeStamp** 屬性。  

-   Active Directory 網域功能層級必須設定為 Windows Server 2003 或更新版本。  

當您設定要在這項設定中使用的上次登入時間時，請考量網域控制站之間的複寫間隔。  

您可以在 [Active Directory 探索內容]  及 [Active Directory 群組探索內容]  對話方塊的 [選項]  索引標籤上設定篩選。 選擇 [僅探索在指定時間登入網域的電腦]  。  

> [!WARNING]  
>  當您設定此篩選及 [Filter stale records by computer password] \(依電腦密碼篩選過時的記錄\)  時，電腦只要符合其中一項篩選的準則，探索就會將其排除。  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a> 依電腦密碼篩選過時的記錄  
可用於：  

-   Active Directory 群組探索  

-   Active Directory 系統探索  

您可以設定讓探索排除具有過時電腦記錄的電腦。 此排除動作會根據電腦上次更新電腦帳戶密碼的時間。 當啟用此選項時，Active Directory 系統探索會評估其識別的每部電腦。 Active Directory 群組探索則會評估所探索的群組成員的每一部電腦。  

若要使用此選項：  

-   必須設定電腦更新 Active Directory 網域服務的 **pwdLastSet** 屬性。  

當您在設定此選項時，請考量此屬性的更新間隔。 此外，也請考量網域控制站間的複寫間隔。  

您可以在 [Active Directory 探索內容]  及 [Active Directory 群組探索內容]  對話方塊的 [選項]  索引標籤上設定篩選。 選擇 [僅探索在指定時間更新其電腦帳戶密碼的電腦]  。  

> [!WARNING]  
>  當您設定此篩選及 [Filter stale records by domain logon] \(依網域登入來篩選過時的記錄\)  時，電腦只要符合其中一項篩選的準則，探索就會將其排除。  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a> 搜尋自訂的 Active Directory 屬性  
 可用於：  

-   Active Directory 系統探索  

-   Active Directory 使用者探索  

每種探索方法都支援可探索的唯一 Active Directory 屬性清單。  

您可以在 [Active Directory 系統探索內容]  和 [Active Directory 使用者探索內容]  對話方塊中的 [Active Directory 屬性]  索引標籤上，檢視及設定自訂屬性的清單。  
