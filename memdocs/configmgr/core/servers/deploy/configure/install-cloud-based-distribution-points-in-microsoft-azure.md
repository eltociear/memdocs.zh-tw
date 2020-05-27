---
title: 安裝雲端發佈點
titleSuffix: Configuration Manager
description: 使用這些步驟在 Configuration Manager 中設定雲端發佈點。
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35379aed71544a25a98ec4dfa421be70c1bae851
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427696"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>安裝 Configuration Manager 的雲端發佈點

適用於：Configuration Manager (最新分支)

> [!Important]  
> 從 Azure 共用內容的實作已經變更。 藉由啟用 [允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容] 選項，來使用啟用內容的雲端管理閘道。 如需詳細資訊，請參閱[修改 CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)。
>
> 未來您將無法建立傳統雲端發佈點。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。

本文詳述在 Microsoft Azure 中安裝 Configuration Manager 雲端發佈點的步驟。 它包含下列各節：

- [開始之前](#bkmk_before)
- [設定](#bkmk_setup)
- [設定 DNS](#bkmk_dns)
- [設定站台伺服器 Proxy](#bkmk_proxy)
- [發佈內容和設定用戶端](#bkmk_client)
- [管理和監視](#bkmk_monitor)
- [修改](#bkmk_modify)
- [進階疑難排解](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a> 開始之前

請先閱讀[使用雲端發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)一文。 該文協助您規劃及設計雲端發佈點。

使用下列檢查清單，確定您有建立雲端發佈點的必要資訊和必要條件：  

- 站台伺服器可連線到 Azure。 如果您的網路使用 Proxy，請[設定站台系統角色](#bkmk_proxy)。  

- 要使用的 **Azure 環境**。 例如，Azure 公用雲端或 Azure 美國政府雲端。  

- 從 1806 版開始，「建議」使用 **Azure Resource Manager 部署**。 其需求如下：<!--1322209-->  

    - 與 [Azure Active Directory](azure-services-wizard.md) 整合以進行**雲端管理**。 不需要 Azure AD 使用者探索。  

    - Azure **訂用帳戶識別碼**。  

    - Azure **資源群組**。  

    - **訂用帳戶系統管理員帳戶**必須在執行精靈期間保持登入。  

- 匯出為 .PFX 檔案的**伺服器驗證憑證**。  

- 雲端發佈點的全域唯一**服務名稱**。  

    > [!TIP]  
    > 要求使用此服務名稱的伺服器驗證憑證之前，請確認想要的 Azure 網域名稱是唯一的。 例如，*WallaceFalls.CloudApp.Net*。
    >
    > 1. 登入 [Azure 入口網站](https://portal.azure.com)。
    > 1. 選取 [所有資源]，然後選取 [新增]。
    > 1. 搜尋**雲端服務**。 選取 [建立]。
    > 1. 在 [DNS 名稱] 欄位中輸入您想要的前置詞，例如 *WallaceFalls*。 介面將會反映網域名稱可用或已由另一個服務使用。
    >
    > 請勿在入口網站中建立服務，只要使用此程序檢查名稱可用性。

- 此部署的 Azure **區域**。  

- 如果您仍然需要在 Configuration Manager 1810 版或更早版本中使用 Azure **傳統服務部署**，則需要下列需求：  

    > [!Important]  
    > 從 1810 版開始，Configuration Manager 已淘汰 Azure 的傳統服務部署。 開始針對雲端發佈點使用 Azure Resource Manager 部署。 如需詳細資訊，請參閱 [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager)。  
    >
    > 從 Configuration Manager 1902 版開始，對於雲端發佈點的新執行個體，Azure Resource Manager 是唯一的部署機制。<!-- 3605704 -->

    - Azure **訂用帳戶識別碼**。  

    - 匯出為 .CER 及 .PFX 檔案的 Azure **管理憑證**。 Azure 訂用帳戶系統管理員必須將 .CER 管理憑證新增至 [Azure 入口網站](https://portal.azure.com)中的訂用帳戶。  

### <a name="branchcache"></a>BranchCache

若要讓雲端發佈點使用 Windows BranchCache，請在網站伺服器上安裝 BranchCache 功能。<!-- SCCMDocs-pr#4054 -->

- 如果網站伺服器具有內部部署發佈點網站系統角色，請在該角色的屬性中設定選項，以**啟用並設定 BranchCache**。 如需詳細資訊，請參閱[設定發佈點](install-and-configure-distribution-points.md#bkmk_config-general)。

- 如果網站伺服器沒有發佈點角色，請在 Windows 中安裝 BranchCache 功能。 如需詳細資訊，請參閱[安裝 BranchCache 功能](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature)。

如果您已將內容發佈到雲端發佈點，然後決定要啟用 BranchCache，請先安裝此功能。 接著將內容重新發佈到雲端發佈點。

> [!NOTE]  
> 在 Configuration Manager 1810 版和更早版本中，如果您有多個雲端發佈點，則需要手動設定 BranchCache 金鑰複雜密碼。 如需詳細資訊，請參閱 [Microsoft 支援服務 KB 4458143](https://support.microsoft.com/help/4458143)。

## <a name="set-up"></a><a name="bkmk_setup"></a> 設定  

視您的[設計](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology)而定，在裝載此雲端發佈點的站台上執行此程序。  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區中，展開 [雲端服務]，然後選取 [雲端發佈點]。 在功能區中，選取 [建立雲端發佈點]。  

2. 在 [建立雲端發佈點精靈] 的 [一般] 頁面上，設定下列設定：  

    1. 先指定 **Azure 環境**。  

    2. 從 1806 版開始，「建議」選取 [Azure Resource Manager 部署] 作為部署方法。 選取 [登入]，使用 Azure 訂用帳戶系統管理員帳戶進行驗證。 精靈會使用 Azure AD 整合先決條件期間所儲存的資訊，自動填入其餘欄位。 如果您擁有多個訂用帳戶，請選取需要使用的訂用帳戶的**訂用帳戶識別碼**。  

    > [!Note]  
    > 從 1810 版開始，Configuration Manager 已淘汰 Azure 的傳統服務部署。
    >
    > 如果您需要使用傳統服務部署，請在此頁面上選取該選項。 首先，輸入您的 Azure **訂用帳戶識別碼**。 然後選取 [瀏覽] 並選取 Azure 管理憑證的 .PFX 檔案。  

3. 選取 [下一步]。 等待站台測試 Azure 的連線。  

4. 在 [設定] 頁面上指定下列設定，然後選取 [下一步]：  

    - **區域**：選取您要建立雲端發佈點所在的 Azure 區域。  

    - **資源群組** (僅限 Azure Resource Manager 部署方法)  

        - **使用現有的**：從下拉式清單中選取現有的資源群組。  

        - **新建**：輸入要在您 Azure 訂用帳戶中建立的新資源群組名稱。  

    - **主要站台**：選取要將內容發佈至此發佈點的主要站台。

    - **憑證檔案**：選取 [瀏覽]，然後選取此雲端發佈點之伺服器驗證憑證的 .PFX 檔案。 此憑證的通用名稱會填入所需的 [服務 FQDN] 和 [服務名稱] 欄位。  

        > [!NOTE]  
        > 雲端發佈點伺服器驗證憑證支援萬用字元。 如果您使用萬用字元憑證，請將 [服務 FQDN] 欄位中的星號 (`*`) 取代為服務所需的主機名稱。  

5. 在 [警示] 頁面上，設定儲存配額、傳輸配額，以及您想讓 Configuration Manager 產生警示的這些配額百分比。 然後選取 [下一步]。  

6. 完成精靈。  

### <a name="monitor-installation"></a>監視安裝  

站台會為雲端發佈點開始建立新的託管服務。 關閉精靈之後，在 Configuration Manager 主控台中監視雲端發佈點的安裝進度。 另外監視主要站台伺服器上的 **CloudMgr.log** 檔案。 如有必要，在 Azure 入口網站中監視雲端服務的佈建。  

> [!NOTE]  
> 在 Azure 中佈建新的發佈點可能需要長達 30 分鐘的時間。 **CloudMgr.log** 檔案會重複下列訊息，直到儲存體帳戶佈建完成：  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> 佈建儲存體帳戶之後，會建立並設定服務。  

### <a name="verify-installation"></a>確認安裝

使用下列方法確認雲端發佈點安裝已完成：  

- 在 Configuration Manager 主控台中，移至 [系統管理] 工作區。 展開 [雲端服務]，然後選取 [雲端發佈點] 節點。 在清單中尋找新的雲端發佈點。 [狀態] 資料行應為 [就緒]。  

- 在 Configuration Manager 主控台中，按一下 [監視] 工作區。 展開 [系統狀態]，然後選取 [元件狀態] 節點。 顯示 **SMS_CLOUD_SERVICES_MANAGER** 元件的所有訊息，然後尋找狀態訊息識別碼 **9409**。  

- 如有必要，請前往 Azure 入口網站。 雲端發佈點的 [部署] 顯示狀態為 [就緒]。  


## <a name="configure-dns"></a><a name="bkmk_dns"></a> 設定 DNS  

用戶端必須能夠將雲端發佈點的名稱解析成 Azure 所管理的 IP 位址，才能使用雲端發佈點。 管理點會為其提供雲端發佈點的 [服務 FQDN]。 雲端發佈點在 Azure 中是以 [服務名稱] 表示。 您可以在雲端發佈點內容的 [設定] 索引標籤上，查看這些值。

> [!Note]  
> 主控台中的 [雲端發佈點] 節點包含名為 [服務名稱] 的資料行，但實際上會顯示 [服務 FQDN] 值。 若要查看這兩個值，請開啟雲端發佈點的 [內容]，然後切換至 [設定] 索引標籤。  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

伺服器驗證憑證通用名稱應該包含您的網域名稱。 當您購買來自公用提供者的憑證時，需要此名稱。 這是您從 PKI 發行此憑證時的建議做法。 例如 `WallaceFalls.contoso.com`。 當您在 [建立雲端發佈點精靈] 中指定此憑證時，通用名稱會填入 [服務 FQDN] 內容 (`WallaceFalls.contoso.com`)。 [服務名稱] 會接受相同的主機名稱 (`WallaceFalls`)，並將它附加至 Azure 網域名稱 (`cloudapp.net`)。 在此案例中，用戶端需要將您網域的 [服務 FQDN] (`WallaceFalls.contoso.com`) 解析成 Azure [服務名稱] (`WallaceFalls.cloudapp.net`)。 建立對應至這些名稱的 CNAME 別名。

### <a name="create-cname-alias"></a>建立 CNAME 別名

在貴組織的公用網際網路對向 DNS 中建立正式名稱記錄 (CNAME)。 此記錄會為用戶端接收之雲端發佈點的 [服務 FQDN] 內容，建立對應至 Azure [服務名稱] 的別名。 例如，建立新的 CNAME 記錄，將 `WallaceFalls.contoso.com` 對應至 `WallaceFalls.cloudapp.net`。  

### <a name="client-name-resolution-process"></a>用戶端名稱解析程序

下列程序說明用戶端如何解析雲端發佈點的名稱：  

1. 用戶端在內容來源清單中取得雲端發佈點的 [服務 FQDN]。 例如 `WallaceFalls.contoso.com`。  

2. 它查詢 DNS，這會使用 CNAME 別名將 [服務 FQDN] 解析成 Azure [服務名稱]。 例如 `WallaceFalls.cloudapp.net`。  

3. 它再次查詢 DNS，這會將 Azure 服務名稱解析成 Azure 公用 IP 位址。  

4. 用戶端使用此 IP 位址開始與雲端發佈點通訊。  

5. 雲端發佈點提供伺服器驗證憑證給用戶端。 用戶端使用憑證的信任鏈結進行驗證。  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a> 設定站台伺服器 Proxy  

管理雲端發佈點的主要站台伺服器必須與 Azure 通訊。 如果貴組織使用 Proxy 伺服器控制網際網路存取，請設定主要站台伺服器使用此 Proxy。  

如需詳細資訊，請參閱 [Proxy 伺服器支援](../../../plan-design/network/proxy-server-support.md)。  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a> 發佈內容和設定用戶端

將內容發佈至雲端發佈點，其方式與任何其他內部部署發佈點相同。 除非管理點包含用戶端要求的內容，否則不會在內容位置清單中包含雲端發佈點。 如需詳細資訊，請參閱[發佈和管理內容](deploy-and-manage-content.md)。

管理雲端發佈點，其方式與任何其他內部部署發佈點相同。 這些動作包括將它指派給發佈點群組，以及管理內容套件。 如需詳細資訊，請參閱[安裝及設定發佈點](install-and-configure-distribution-points.md)。

預設用戶端設定會自動啟用用戶端以使用雲端發佈點。 您可以使用下列用戶端設定，控制對您階層中所有雲端發佈點的存取：  

- 在 [用戶端設定] 群組中，修改 [允許存取雲端發佈點] 設定。  

    - 此設定預設會設定為 [是]。  

    - 請為使用者和裝置修改及部署此設定。  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a> 管理和監視  

監視您發佈至雲端發佈點的內容，其方式與任何其他內部部署發佈點相同。 如需詳細資訊，請參閱[監視內容](monitor-content-you-have-distributed.md)。

當在主控台中檢視雲端發佈點清單時，您可在清單中新增其他欄。 例如，[資料輸出] 欄會顯示過去 30 天內用戶端從服務下載的資料數量。<!-- SCCMDocs#755 -->

### <a name="alerts"></a><a name="bkmk_alerts"></a> 警示  

Configuration Manager 會定期檢查 Azure 服務。 如果該服務並未啟用，或出現訂閱或憑證問題，Configuration Manager 會產生警示。

設定要儲存在雲端發佈點上的資料量閾值，以及用戶端從發佈點下載之資料量的閾值。 使用這些閾值的警示可協助您決定何時停止或刪除雲端服務、調整您儲存在雲端發佈點中的內容，或是修改可以使用該服務的用戶端。

- **存放裝置警示閾值**：存放裝置警示閾值可設定您要儲存在雲端架構發佈點的資料或內容量上限 (GB)。 此閾值預設為 2,000 GB。 當剩餘可用空間達到您指定的層級時，Configuration Manager 會產生警告和重大警示。 根據預設，在達到 50% 和 90% 閾值時，就會發生這些警示。  

- **每月傳輸警示閾值**：每月傳輸警示閾值可協助您監視 30 天內從發佈點傳輸至用戶端的內容量。 此閾值預設為 10,000 GB。 當傳輸量達到您定義的值時，站台會產生警告和重大警示。 根據預設，在達到 50% 和 90% 閾值時，就會發生這些警示。  

    > [!IMPORTANT]  
    > Configuration Manager 會監視資料傳輸，但不會在資料傳輸量超出指定的傳輸警示閾值時停止傳輸資料。  

在安裝期間指定每個雲端發佈點的閾值，或使用雲端發佈點內容的 [警示] 索引標籤。  

> [!NOTE]  
> 雲端發佈點的警示因 Azure 的使用量統計資料而有所不同，最長可能要 24 小時後才能使用。 如需 Azure 儲存體分析的詳細資訊，請參閱 [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics) (儲存體分析)。  

每小時的週期中，監視雲端發佈點的主要站台會從 Azure 下載交易資料。 它會將此交易資料儲存在站台伺服器上的 `CloudDP-<ServiceName>.log` 檔案。 Configuration Manager 接著會根據每個雲端發佈點的儲存和傳輸配額來評估此資訊。 資料傳輸達到或超過指定的警告警示或重大警示容量時，Configuration Manager 便會產生相應的警示。  

> [!WARNING]  
> 由於站台每小時都會從 Azure 下載一次資料傳輸相關資訊，因此在 Configuration Manager 存取資料並產生警示之前，使用量可能就已超出警告或重大閾值。  


## <a name="modify"></a><a name="bkmk_modify"></a> 修改

在 Configuration Manager 主控台的 [系統管理] 工作區中，於 [雲端服務] 的 [雲端發佈點] 節點中，檢視發佈點的高階資訊。 選取發佈點，然後選取 [內容] 以檢視更多詳細資料。  

當您編輯雲端發佈點的內容時，下列索引標籤包含可供編輯的設定：  

#### <a name="settings"></a>設定

- **描述**  

- **憑證檔案**：伺服器驗證憑證到期之前，使用相同的通用名稱發行新憑證。 然後在這裡新增憑證讓服務開始使用。 如果憑證到期，用戶端將不會信任並使用該服務。  

#### <a name="alerts"></a>警示

調整儲存和每月傳輸警示的資料閾值。  

#### <a name="content"></a>Content

管理內容，其方式與內部部署發佈點相同。  

### <a name="redeploy-the-service"></a>請重新部署服務

更重要的變更 (例如下列設定)，需要重新部署服務：

- Azure Resource Manager 的傳統部署方法
- 訂用帳戶
- 服務名稱
- 私用到公用 PKI
- Azure 區域

從 1806 版開始，如果您在傳統部署方法有現有的雲端發佈點，您必須部署新的雲端發佈點才能使用 Azure Resource Manager 部署方法。 有兩個選項：

- 如果您想要重複使用相同的服務名稱：  

    1. 先刪除傳統雲端發佈點。 如果沒有其他雲端發佈點，則用戶端可能無法取得內容。  

    2. 使用 Resource Manager 部署建立新的雲端發佈點。 重複使用相同的伺服器驗證憑證。  

    3. 將必要的軟體套件內容發佈至新的雲端發佈點。  

- 如果您想要使用新的服務名稱：  

    1. 使用 Resource Manager 部署建立新的雲端發佈點。 使用新的伺服器驗證憑證。  

    2. 將必要的軟體套件內容發佈至新的雲端發佈點。  

    3. 刪除傳統雲端發佈點。

> [!Tip]  
> 判斷雲端發佈點目前的部署模型：<!--SCCMDocs issue #611-->  
>
> 1. 在設定管理員主控台中，移至 [系統管理] 工作區，展開 [雲端服務]，然後選取 [雲端發佈點] 節點。  
> 2. 將 [部署模型] 屬性當作資料行新增至清單檢視。 若是 Resource Manager 部署，此屬性會是 [Azure Resource Manager]。  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>依需求停止或啟動雲端服務

您可以在 Configuration Manager 主控台中，隨時停止雲端發佈點。 此動作可立即防止用戶端透過該服務下載其他內容。 從 Configuration Manager 主控台重新啟動雲端服務，即可還原用戶端的存取權。 例如，在達到閾值時停止雲端服務。  

當您停止雲端發佈點時，雲端服務不會刪除儲存體帳戶的內容。 它也不會防止站台伺服器將其他內容傳輸至雲端發佈點。 管理點仍會將雲端發佈點傳回用戶端作為有效的內容來源。

使用下列程序可停止雲端發佈點：  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區。 展開 [雲端服務]，然後選取 [雲端發佈點] 節點。  

2. 選取雲端發佈點。 若要停止在 Azure 中執行的雲端服務，請選取功能區中的 [停止服務]。  

3. 選取 [啟動服務] 以重新啟動雲端發佈點。  

### <a name="delete-a-cloud-distribution-point"></a>刪除雲端發佈點

若要解除安裝雲端發佈點，請在 Configuration Manager 主控台中選取發佈點，然後選取 [刪除]。  

當您從階層中刪除雲端發佈點時，Configuration Manager 會從 Azure 中的雲端服務移除內容。

在 Azure 中手動移除任何元件會導致系統不一致。 此狀態會保留被遺棄的資訊，而且可能會發生非預期的行為。


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a> 進階疑難排解

如果您需要從 Azure VM 收集診斷記錄，以協助針對您的雲端發佈點問題進行疑難排解，請使用下列 PowerShell 範例來啟用訂用帳戶的服務診斷延伸模組：<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

下列範例是上述 PowerShell 指令碼中 **public_config** 變數所參考的範例 **diagnostics.wadcfgx** 檔案。 如需詳細資訊，請參閱 [Azure 診斷延伸模組的設定結構描述](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema)。  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
