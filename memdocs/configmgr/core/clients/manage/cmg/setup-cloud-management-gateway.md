---
title: 設定雲端管理閘道
titleSuffix: Configuration Manager
description: 使用此逐步程序來設定雲端管理閘道 (CMG)。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 783323c3e9218b34b1f2b7f3c7d9bb13eea44e2e
ms.sourcegitcommit: ed2c18e210db177eb0d5e10d74207006561b7b5d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83383715"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>設定 Configuration Manager 的雲端管理閘道

適用於：Configuration Manager (最新分支)

此程序包括設定雲端管理閘道 (CMG) 所需的步驟。

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../../servers/manage/install-in-console-updates.md#bkmk_options)。


## <a name="before-you-begin"></a>開始之前

請先閱讀[規劃雲端管理閘道](plan-cloud-management-gateway.md)文章。 使用該文章可決定您的 CMG 設計。

使用下列檢查清單，確定您有建立 CMG 的必要資訊和必要條件：  

- 要使用的 Azure 環境。 例如，Azure 公用雲端或 Azure 美國政府雲端。  

- 依您的設計而定，您需要一個或多個供 CMG 使用的憑證。 如需詳細資訊，請參閱[雲端管理閘道的憑證](certificates-for-cloud-management-gateway.md)。  

- 您需要下列需求才能進行 CMG 的 [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) 部署：  

    - 與 [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) 整合以進行**雲端管理**。 不需要 Azure AD 使用者探索。  

    - **Microsoft.ClassicCompute** & **Microsoft.Storage** 資源提供者必須在 Azure 訂用帳戶內註冊。 如需詳細資訊，請參閱 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services)。

    - 訂用帳戶系統管理員必須登入。  

- 服務的全域唯一名稱。 此名稱來自 [CMG 伺服器驗證憑證](certificates-for-cloud-management-gateway.md#bkmk_serverauth)。  

- 如果將 CMG 作為雲端發佈點啟用，則所選擇的相同全域唯一 CMG 服務名稱也必須當成全域唯一的儲存體帳戶名稱來提供。 此名稱來自 [CMG 伺服器驗證憑證](certificates-for-cloud-management-gateway.md#bkmk_serverauth)。

- 此 CMG 部署的 Azure 區域。  

- 調整規模和備援所需的 VM 執行個體數目。  

- 如果您仍然需要在 Configuration Manager 1810 版或更早版本中使用 Azure 傳統服務部署，則需要下列需求：  

    > [!Important]  
    > 從 1810 版開始，Configuration Manager 已淘汰 Azure 的傳統服務部署。 針對雲端管理閘道，使用 Azure Resource Manager 部署。 如需詳細資訊，請參閱[規劃 CMG](plan-cloud-management-gateway.md#azure-resource-manager)。  
    >
    > 從 Configuration Manager 1902 版開始，對於雲端管理閘道的新執行個體，Azure Resource Manager 是唯一的部署機制。<!-- 3605704 -->

    - Azure 訂用帳戶識別碼  

    - Azure 管理憑證  


## <a name="set-up-a-cmg"></a>設定 CMG

在頂層站台上執行此程序。 此站台可以是獨立的主要站台，也可以是管理中心網站。

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，展開 [雲端服務]，然後選取 [雲端管理閘道]。  

2. 在功能區中選取 [建立雲端管理閘道]。  

3. 在精靈的 [一般] 頁面上，選取 [登入]。 使用 Azure 訂用帳戶管理員帳戶進行驗證。 精靈會使用 Azure AD 整合先決條件期間所儲存的資訊，自動填入其餘欄位。 如果您擁有多個訂用帳戶，請選取需要使用的訂用帳戶的**訂用帳戶識別碼**。

    > [!Note]  
    > 從 1810 版開始，Configuration Manager 已淘汰 Azure 的傳統服務部署。 在 1902 版和更早版本中，選取 [Azure Resource Manager 部署] 作為 CMG 部署方法。
    >
    > 如果您需要使用傳統服務部署，請在此頁面上選取該選項。 首先，輸入您的 Azure **訂用帳戶識別碼**。 然後選取 [瀏覽] 並選擇 Azure 管理憑證的 .PFX 檔案。

4. 指定此 CMG 的 **Azure 環境**。 下拉式清單中的選項可能會根據部署方法而不同。  

5. 選取 [下一步]。 等待站台測試 Azure 的連線。  

6. 在精靈的 [設定] 頁面中，先選取 [瀏覽] 並選擇 CMG 伺服器驗證憑證的 .PFX 檔案。 此憑證的名稱會填入所需的 [服務 FQDN] 和[服務名稱] 欄位。  

   > [!NOTE]  
   > CMG 伺服器驗證憑證支援萬用字元。 如果您使用萬用字元憑證，請將 [服務 FQDN] 欄位中的星號 (`*`) 取代為 CMG 所需的主機名稱。<!--491233-->  

7. 選取 [區域] 下拉式清單以選擇此 CMG 的 Azure 區域。  

8. 選取**資源群組**選項。
   1. 如果您選擇 [使用現有的]，請從下拉式清單中選取現有的資源群組。 選取的資源群組，必須已經存在您於步驟 7 選取的區域內。 如果您選取現有的資源群組，但其所處區域與先前選取的區域不同，CMG 就無法佈建。
   2. 如果您選擇 [新建]，請輸入新的資源群組名稱。

9. 在 [VM 執行個體] 欄位中，輸入此服務的 VM 數目。 預設值是 1，但您可以擴大為每個 CMG 16 個 VM。  

10. 選取 [憑證] 以新增用戶端受信任的根憑證。 在信任鏈結中新增所有憑證。  

    > [!Note]  
    > 從 1806 版開始，當您建立 CMG 時，不再需要於 [設定] 頁面上提供受信任的根憑證。 使用 Azure Active Directory (Azure AD) 進行用戶端驗證時，不需要此憑證，但以前在精靈中需要此憑證。 如果您要使用 PKI 用戶端驗證憑證，則仍然必須將受信任的根憑證新增至 CMG。<!--SCCMDocs-pr issue #2872-->  
    >
    > 在 1902 版和更早版本中，您只能指定兩個信任的根 CA，以及四個中繼 (從屬) CA。<!-- SCCMDocs-pr#4022 -->

11. 根據預設，精靈會啟用 [驗證用戶端憑證撤銷] 選項。 憑證撤銷清單 (CRL) 必須公開發佈，供此驗證運作。 如需詳細資訊，請參閱[發佈憑證撤銷清單](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl)。  

12. 從 1906 版開始，您可以**強制使用 TLS 1.2**。 此設定僅適用於 Azure 雲端服務 VM。 它不適用於任何內部部署 Configuration Manager 站台伺服器或用戶端。 如需 TLS 1.2 的詳細資訊，請參閱[如何啟用 TLS 1.2](../../../plan-design/security/enable-tls-1-2.md)。<!-- SCCMDocs-pr#4021 -->

13. 從 1806 版開始，精靈預設會啟用下列選項：**允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容**。 現在，CMG 也可以將內容提供給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。  

14. 選取 [下一步]。  

15. 若要使用 14 天閾值監視 CMG 流量，請選擇核取方塊，以開啟閾值警示。 然後，指定臨界值，以及引發不同警示等級的百分比。 完成時，請選擇 [下一步]。  

16. 檢閱設定，然後選擇 [下一步]。 Configuration Manager 隨即開始設定服務。 在您關閉精靈之後，需要 5 到 15 分鐘，才能在 Azure 中完整地佈建服務。 檢查新 CMG 的 [狀態] 欄，以判斷服務何時就緒。  

    > [!Note]  
    > 若要對 CMG 部署進行疑難排解，請使用 **CloudMgr.log** 和 **CMGSetup.log**。 如需詳細資訊，請參閱[記錄檔](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。


## <a name="configure-primary-site-for-client-certificate-authentication"></a>設定主要站台以進行用戶端憑證驗證

如果您使用[用戶端驗證憑證](certificates-for-cloud-management-gateway.md#bkmk_clientauth)讓用戶端向 CMG 進行驗證，請遵循此程序來設定每個主要站台。  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，展開 [站台設定]，然後選取 [站台]。  

2. 選取您以網際網路為基礎的用戶端要指派到的主要站台，然後選擇 [內容]。  

3. 切換至主要站台屬性工作表的 [用戶端電腦通訊] 索引標籤，核取 [使用可用的 PKI 用戶端憑證 (用戶端驗證)]。  

    > [!Note]
    > 從 1906 版開始，此索引標籤稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

4. 如果您不要發佈 CRL，請取消選取 [由用戶端檢查站台系統的憑證撤銷清單 (CRL)] 的選項。  


## <a name="add-the-cmg-connection-point"></a>新增 CMG 連接點

CMG 連接點是與 CMG 通訊的站台系統角色。 若要新增 CMG 連接點，請遵循一般指示[安裝站台系統角色](../../../servers/deploy/configure/install-site-system-roles.md)。 在「新增站台系統角色精靈」的 [系統角色選取] 頁面中，選取 [雲端管理閘道連接點]。 然後選取這部伺服器連線的**雲端管理閘道名稱**。 精靈會顯示所選 CMG 的區域。

> [!Important]
> 在某些情況下，CMG 連接點必須有[用戶端驗證憑證](certificates-for-cloud-management-gateway.md#bkmk_clientauth)。

若要對 CMG 服務健康情況進行疑難排解，請使用 **CMGService.log** 和 **SMS_Cloud_ProxyConnector.log**。 如需詳細資訊，請參閱[記錄檔](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。


## <a name="configure-client-facing-roles-for-cmg-traffic"></a>設定 CMG 流量的用戶端對向角色

設定管理點和軟體更新點站台系統接受 CMG 流量。 針對為以網際網路為基礎用戶端提供服務的所有管理點和軟體更新點，在主要站台上執行此程序。  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，並展開 [站台設定]，然後選取 [伺服器和站台系統角色] 節點。 在功能區的 [首頁] 索引標籤上，選取 [檢視] 群組中的 [具有角色的伺服器]。 然後從清單中選取 [管理點]。  

2. 選取您想要針對 CMG 流量設定的站台系統伺服器。 在詳細資料窗格中選取 [管理點] 角色，然後在功能區中選取 [內容]。  

3. 在 [用戶端連線] 下的 [管理點] 內容工作表中，核取 [允許 Configuration Manager 雲端管理閘道流量] 旁的方塊。

    根據您的 CMG 設計和 Configuration Manager 版本，您可能需要啟用 [HTTPS] 選項。 如需詳細資訊，請參閱[啟用 HTTPS 的管理點](certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

4. 選取 [確定] 以關閉管理點內容視窗。  

視需要針對其他管理點以及任何軟體更新點重複這些步驟。


## <a name="configure-boundary-groups"></a>設定界限群組

<!--3640932-->
從 1902 版開始，您可以將 CMG 關聯至界限群組。 此設定可讓用戶端根據界限群組關聯性來預設或回復為 CMG 以進行用戶端通訊。

如需界限群組的詳細資訊，請參閱[設定界限群組](../../../servers/deploy/configure/boundary-groups.md)。

當您[建立或設定界限群組](../../../servers/deploy/configure/boundary-group-procedures.md)時，請在 [參考] 索引標籤上，新增雲端管理閘道。 此動作會將 CMG 與此界限群組建立關聯。


## <a name="configure-clients-for-cmg"></a>設定 CMG 的用戶端

CMG 和站台系統角色執行之後，用戶端就會在下一個位置要求自動收到 CMG 服務的位置。 用戶端必須位於內部網路，才能接收 CMG 服務的位置，除非您[安裝 Windows 10 用戶端並使用 Azure AD 指派 Windows 10 用戶端進行驗證](../../deploy/deploy-clients-cmg-azure.md)。 位置要求的輪詢週期為每 24 小時。 如果您不想等候標準排程的位置要求，您可以在電腦上重新啟動 SMS Agent Host 服務 (ccmexec.exe) 來強制執行要求。  

> [!Note]
> 根據預設，所有用戶端都會接收 CMG 原則。 請使用[允許用戶端使用雲端管理閘道](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway)用戶端設定來控制此行為。

Configuration Manager 用戶端會自動判斷它是位於內部網路還是網際網路。 如果用戶端可以連絡網域控制站或內部部署管理點，則會將其連線類型設定為 [目前為內部網路]。 否則會切換成 [目前為網際網路]，並使用 CMG 服務的位置與站台通訊。

>[!NOTE]
> 您可以強制用戶端一律使用 CMG，無論用戶端是在內部網路還是網際網路上。 此設定對測試用途很有用，也對您想要強制一律使用 CMG 的用戶端很有用。 在用戶端上設定下列登錄機碼：
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> 您也可以在用戶端安裝期間使用 [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) 屬性指定此設定。
>
> 此設定一律將會套用，即使用戶端漫遊到界限群組設定將利用本機資源的位置也一樣。


若要確認用戶端具有指定 CMG 的原則，請在用戶端電腦上以系統管理員身分開啟 Windows PowerShell 命令提示字元，然後執行下列命令：`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

此命令會顯示用戶端知道的任何以網際網路為基礎的管理點。 雖然 CMG 在技術上並不是以網際網路為基礎的管理點，但從用戶端觀點來看就是如此。

> [!Note]  
> 若要對 CMG 用戶端流量進行疑難排解，請使用 **CMGHttpHandler.log**、**CMGService.log** 和 **SMS_Cloud_ProxyConnector.log**。 如需詳細資訊，請參閱[記錄檔](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway)。

### <a name="install-off-premises-clients-using-a-cmg"></a>使用 CMG 安裝外部部署用戶端

若要在目前未連線到內部網路的系統上安裝用戶端代理程式，就必須符合下列其中一個條件。 在所有情況下，都需要目標系統上的本機系統管理員帳戶。

1. Configuration Manager 站台已正確設定為使用 PKI 憑證進行用戶端驗證。 此外，每個用戶端系統都具有先前核發給該系統之有效、唯一且受信任的用戶端驗證憑證。

2. 這些系統已加入 Azure AD 網域或已加入混合式 Azure AD 網域。

3. 此站台正在執行 Configuration Manager 2002 版或更新版本。

針對選項 1 與 2，在呼叫 **ccmsetup.exe** 時，使用 **/mp** 參數來指定 CMG 的 URL。 如需詳細資訊，請參閱[關於用戶端安裝參數和內容](../../deploy/about-client-installation-properties.md#mp)。

針對選項 3，從 Configuration Manager 2002 版開始，您可以使用大量註冊權杖，在未連線到內部網路的系統上安裝用戶端代理程式。 如需此方法的詳細資訊，請參閱[建立大量註冊權杖](../../deploy/deploy-clients-cmg-token.md#create-a-bulk-registration-token)。

### <a name="configure-off-premises-clients-for-cmg"></a>設定 CMG 的外部部署用戶端

符合下列條件時，您就能將系統連線到最近設定的 CMG：  

- 系統已經安裝 Configuration Manager 用戶端代理程式。

- 系統尚未連線且無法連線到您的內部網路。

- 系統符合下列其中一個條件：

 - 每個系統都具有先前核發給該系統之有效、唯一且受信任的用戶端驗證憑證。
 
 - 已加入 Azure AD 網域
 
 - 已加入混合式 Azure AD 網域。

- 您不希望或無法完全重新安裝現有的用戶端代理程式。

- 您有一種方法可以變更電腦登錄值，並使用本機系統管理員帳戶重新啟動 **SMS Agent Host** 服務。

若要在這些系統上強制連線，請在 **HKLM\Software\Microsoft\CCM** 底下建立 **CMGFQDNs** 登錄值 (類型為 REG_SZ)。 將此值設定為 CMG 的 URL (例如 `https://contoso-cmg.contoso.com`)。 設定之後，重新啟動用戶端系統上的 **SMS Agent Host** 服務。

如果 Configuration Manager 用戶端並未在登錄中設定目前的 CMG 或網際網路面向管理點，其會自動檢查 **CMGFQDNs** 登錄值。 當 **SMS Agent Host** 服務啟動時，或偵測到網路變更時，此檢查每隔 25 小時就會進行一次。 當用戶端連線到站台並了解 CMG 時，其會自動更新此值。

## <a name="modify-a-cmg"></a>修改 CMG

建立 CMG 之後，您可以修改其部分設定。 在設定管理員主控台中選取 CMG，然後選取 [內容]。 在下列索引標籤上進行設定：  

#### <a name="general"></a>一般

- **Azure 管理憑證**：變更 CMG 的 Azure 管理憑證。 在憑證到期前更新憑證時，此選項很有用。  

#### <a name="settings"></a>設定

- **憑證檔案**：變更 CMG 的伺服器驗證憑證。 在憑證到期前更新憑證時，此選項很有用。  

- **VM 執行個體**：變更服務在 Azure 中使用的虛擬機器數目。 此設定可讓您根據使用量或成本考量，將服務動態相應增加或相應減少。  

- **憑證**：新增或移除受信任的根或中繼 CA 憑證。 加入新的 CA 或淘汰過期的憑證時，此選項很有用。  

- **驗證用戶端憑證撤銷**：如果您在建立 CMG 時原本未啟用此設定，就可以在發佈 CRL 之後加以啟用。 如需詳細資訊，請參閱[發佈憑證撤銷清單](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl)。  

- **允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容**：從 1806 版開始，預設會啟用此新選項。 現在，CMG 也可以將內容提供給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。<!--1358651-->  

#### <a name="alerts"></a>警示

建立 CMG 之後，您可以隨時重新設定警示。


### <a name="redeploy-the-service"></a>請重新部署服務

更重要的變更 (例如下列設定)，需要重新部署服務：

- Azure Resource Manager 的傳統部署方法
- 訂用帳戶
- 服務名稱
- 私用到公用 PKI
- 區域

永遠至少保留一個作用中的 CMG，讓以網際網路為基礎的用戶端能接收更新的原則。 以網際網路為基礎之用戶端無法與已移除的 CMG 通訊。 用戶端要在漫遊回內部網路時，才會知道有新的 CMG。 為了刪除第一個 CMG 執行個體而建立第二個時，也會建立另一個 CMG 連接點。

用戶端預設每 24 小時會重新整理原則，因此請在建立新的 CMG 之後，在刪除舊的憑證之前，至少等待一天。 如果用戶端關閉或沒有網際網路連線，您就必須等待更久的時間。

如果您目前在傳統部署方法上有 CMG，就必須部署新的 CMG 才能使用 Azure Resource Manager 部署方法。<!--509753--> 有兩個選項：  

- 如果您想要重複使用相同的服務名稱：  

    1. 首先刪除傳統 CMG，考慮到指導方針，一定至少要有一個作用中的 CMG 供以網際網路為基礎的用戶端使用。  

    2. 使用資源管理員部署建立新的 CMG。 重複使用相同的伺服器驗證憑證。  

    3. 重新設定 CMG 連線點以使用新的 CMG 執行個體。  

- 如果您想要使用新的服務名稱：  

    1. 使用資源管理員部署建立新的 CMG。 使用新的伺服器驗證憑證。  

    2. 建立新的 CMG 連接點並與新的 CMG 連結。  

    3. 至少等待一天，讓以網際網路為基礎的用戶端接收與新的 CMG 相關的原則。  

    4. 刪除傳統 CMG。  

> [!Tip]  
> 若要判斷 CMG 目前的部署模型：<!--SCCMDocs issue #611-->  
>
> 1. 在設定管理員主控台中，移至 [系統管理] 工作區，展開 [雲端服務]，然後選取 [雲端管理閘道] 節點。  
> 2. 選取 CMG 執行個體。  
> 3. 在視窗底部的詳細資料窗格中，尋找 [部署模型] 屬性。 若是 Resource Manager 部署，此屬性會是 [Azure Resource Manager]。 具有 Azure 管理憑證的舊版部署模型會顯示為 **Azure Service Manager**。
>
> 您也可以將 [部署模型] 屬性當作資料行新增至清單檢視。  

### <a name="modifications-in-the-azure-portal"></a>Azure 入口網站中的修改

從 Configuration Manager 主控台只修改 CMG。 不支援在 Azure 中直接修改服務，或作為基礎的 VM。 可能會遺失任何變更而不顯示通知。 如同任何 PaaS，服務可以隨時重建 VM。 可能會因為後端硬體維護，或為了將更新套用至 VM OS，而發生這些重建。

### <a name="delete-the-service"></a>刪除服務

如果您需要刪除 CMG，也請從 Configuration Manager 主控台進行。 在 Azure 中手動移除任何元件會導致系統不一致。 此狀態會保留被遺棄的資訊，而且可能會發生非預期的行為。


## <a name="next-steps"></a>後續步驟

- [監視雲端管理閘道的用戶端](monitor-clients-cloud-management-gateway.md)
- [雲端管理閘道的相關常見問題集](cloud-management-gateway-faq.md)
