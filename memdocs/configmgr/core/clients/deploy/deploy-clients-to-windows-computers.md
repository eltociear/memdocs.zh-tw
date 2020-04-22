---
title: 將用戶端部署至 Windows
titleSuffix: Configuration Manager
description: 了解如何將設定管理員用戶端部署至 Windows 電腦。
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07c5488b0ea28f37f7f8a07b532c67fb64aad810
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694006"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>如何在 Configuration Manager 中將用戶端部署至 Windows 電腦

適用於：  Configuration Manager (最新分支)

本文詳細說明如何將 Configuration Manager 用戶端部署至 Windows 電腦。 如需規劃及準備用戶端部署的詳細資訊，請參閱這些文章：

- [用戶端安裝方法](plan/client-installation-methods.md)  
- [將用戶端部署至 Windows 電腦的先決條件](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Configuration Manager 用戶端的安全性和隱私權](plan/security-and-privacy-for-clients.md)  
- [用戶端部署的最佳作法](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> 用戶端推入安裝

用戶端入的使用方式主要有三種：  

- 當您為站台設定用戶端推入安裝時，用戶端安裝會在站台探索到的電腦上自動執行。 此方法是以站台設定的界限為範圍 (如果這些界限已設定為界限群組)。  

- 針對特定集合或集合中的資源執行 [用戶端推入安裝精靈]，以起始用戶端推入安裝。  

- 請使用 [用戶端推入安裝精靈] 安裝可用來[查詢](../../servers/manage/introduction-to-queries.md)結果的設定管理員用戶端。 只有在查詢所傳回的其中一個項目必須是來自 [系統資源]  類別的 **ResourceID** 屬性時，才能安裝成功。

如果站台伺服器無法連絡用戶端電腦或啟動安裝程序，則會每小時自動重試安裝。 伺服器會持續重試最多七天。  

若要協助追蹤用戶端安裝程序，請先安裝後援狀態點，再安裝用戶端。 當您安裝後援狀態點時，會在藉由用戶端推入安裝方法進行安裝時，自動指派給用戶端。 若要追蹤用戶端安裝程序，請檢視用戶端部署和指派報表。

用戶端記錄檔會提供更詳細的疑難排解資訊。 記錄檔不需要後援狀態點。 例如，站台伺服器上的 CCM.log 檔案會記錄站台伺服器連線到電腦時發生的任何問題。 用戶端上的 CCMSetup.log 檔案會記錄安裝程序。  

> [!IMPORTANT]  
> 只有在符合所有先決條件時，用戶端推入才會成功。 如需詳細資訊，請參閱[安裝方法相依性](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies)。

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>將站台設定為針對探索到的電腦自動使用用戶端推入

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取您要為其設定自動全站台用戶端推入安裝的站台。  

3. 在功能區的 [首頁]  索引標籤上，選取 [設定]  群組中的 [用戶端安裝設定]  ，然後選取 [用戶端推入安裝]  。  

4. 在 [用戶端推入安裝內容] 視窗的 [一般]  索引標籤上，選取 [啟用自動全站台用戶端推入安裝]  。

5. 從 1806 版開始，當您更新站台時，會針對用戶端推入啟用 Kerberos 檢查。 預設會啟用 [允許連線回復為NTLM]  選項，這與先前的行為一致。 如果站台無法使用 Kerberos 驗證用戶端，則會嘗試使用 NTLM 進行連線。 為增強安全性，建議的設定是停用此設定，其會要求沒有 NTLM 回復的 Kerberos。<!--1358204-->  

    > [!NOTE]  
    > 當站台使用用戶端推入安裝設定管理員用戶端時，站台伺服器會建立與用戶端的遠端連線。 從 1806 版開始，站台可以藉由在建立連線之前不允許回復為 NTLM 來要求 Kerberos 相互驗證。 此增強功能有助於保護伺服器和用戶端之間的通訊。  
    >
    > 根據安全性原則而定，您的環境可能已經偏好使用或需要 Kerberos，而不是較舊 NTLM 驗證。 如需這些驗證通訊協定的安全性考量詳細資訊，請參閱[用來限制 NTLM 的 Windows 安全性原則設定](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations) \(部分機器翻譯\)。  
    >
    > 若要使用此功能，用戶端必須位於信任的 Active Directory 樹系中。 Windows 中的 Kerberos 依賴 Active Directory 進行相互驗證。  

6. 選取 Configuration Manager 應在其中推入用戶端軟體的系統類型。 選取是否要在網域控制站上安裝用戶端。  

7. 在 [帳戶]  索引標籤上，指定一或多個帳戶，讓 Configuration Manager 在連線至目標電腦時使用。 選取 [建立]  圖示、輸入 [使用者名稱]  和 [密碼]  \(不超過 38 個字元\)、確認密碼，然後選取 [確定]  。 至少指定一個用戶端推入安裝帳戶。 此帳戶在要安裝用戶端的目標電腦上必須擁有本機系統管理員權限。 如果您未指定用戶端推入安裝帳戶，Configuration Manager 會嘗試使用站台系統電腦帳戶。 使用站台系統電腦帳戶時，跨網域用戶端推入會失敗。  

    > [!NOTE]  
    > 若要從次要站台使用用戶端推入，請在次要站台指定起始用戶端推入的帳戶。  
    >
    > 如需用戶端推入安裝帳戶的詳細資訊，請參閱下一個程序[使用用戶端推入安裝精靈](#use-the-client-push-installation-wizard)。  

8. 在 [安裝內容]  索引標籤上，指定所有必要的安裝內容。

    如果您已擴充 Configuration Manager 的 Active Directory 架構，站台會將指定的[用戶端安裝內容](about-client-installation-properties.md)發佈到 Active Directory Domain Services。 在不使用安裝內容的情況下執行 CCMSetup 時，它會從 Active Directory 讀取這些內容。  

    > [!NOTE]  
    > 如果您在次要站台上啟用用戶端推入安裝，請將 **SMSSITECODE** 內容設定為其父主要站台的 Configuration Manager 站台碼。 如果您已擴充 Configuration Manager 的 Active Directory 架構，若要自動尋找正確的站台指派，請將此內容設定為 **AUTO**。

### <a name="use-the-client-push-installation-wizard"></a>使用用戶端推入安裝精靈

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取您要為其設定自動全站台用戶端推入安裝的站台。  

3. 在功能區的 [首頁]  索引標籤上，選取 [設定]  群組中的 [用戶端安裝設定]  ，然後選取 [用戶端推入安裝]  。  

4. 在 [安裝內容]  索引標籤上，指定所有必要的安裝內容。  

    如果您已擴充 Configuration Manager 的 Active Directory 架構，站台會將指定的[用戶端安裝內容](about-client-installation-properties.md)發佈到 Active Directory Domain Services。 在不使用安裝內容的情況下執行 CCMSetup 時，它會從 Active Directory 讀取這些內容。

5. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區。  

6. 在 [裝置]  節點中，選取一或多部電腦。 或在 [裝置集合]  節點中，選取一個電腦集合。  

7. 在功能區的 [首頁]  索引標籤上，選擇下列其中一個選項：  

    - 若要將用戶端推入一或多部裝置，請在 [裝置]  群組中，選取 [安裝用戶端]  。  

    - 若要將用戶端推入一組裝置集合，請在 [集合]  群組中，選取 [安裝用戶端]  。  

8. 在 [安裝 Configuration Manager 用戶端精靈] 的 [開始之前]  頁面上檢閱資訊，然後選取 [下一步]  。  

9. 在 [安裝選項]  頁面上，選取適當的選項。  

10. 檢閱安裝設定，然後完成精靈。  

> [!NOTE]  
> 即使站台未設定為可進行用戶端推入，使用此精靈還是可以安裝用戶端。  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> 以軟體更新為基礎的安裝  

以軟體更新為基礎的用戶端安裝，會將用戶端發佈到軟體更新點，以當作軟體更新。 請使用此方法進行第一次安裝或升級。  

如果電腦已安裝設定管理員用戶端，則會從站台接收用戶端原則。 此原則包含要從中取得軟體更新的軟體更新點伺服器名稱和連接埠。

> [!IMPORTANT]  
> 針對以軟體更新為基礎的安裝，請使用相同的 Windows Server Update Services (WSUS) 伺服器進行用戶端安裝和軟體更新。 此伺服器在主要網站必須是主動式軟體更新點。 如需詳細資訊，請參閱[安裝軟體更新點](../../../sum/get-started/install-a-software-update-point.md)。

如果電腦未安裝設定管理員用戶端，請設定並指派群組原則物件。 群組原則可指定軟體更新點的伺服器名稱。  

您無法新增命令列內容至以軟體更新為基礎的用戶端安裝。 如果您已擴充 Configuration Manager 的 Active Directory 架構，用戶端安裝會自動查詢 Active Directory Domain Services，以取得安裝內容。  

如果您尚未擴充 Active Directory 架構，請使用群組原則來佈建用戶端安裝設定。 這些設定會自動套用到任何以軟體更新為基礎的用戶端安裝。 如需詳細資訊，請參閱[如何佈建用戶端安裝內容](#BKMK_Provision)一節和[如何將用戶端指派給站台](assign-clients-to-a-site.md)一文。  

使用下列程序，將不含 Configuration Manager 用戶端的電腦設定為使用軟體更新點。 也有將用戶端軟體發佈到軟體更新點的程序。  

> [!TIP]  
> 如果電腦在先前的軟體安裝之後處於擱置重新啟動狀態，則以軟體更新為基礎的用戶端安裝可能會導致電腦重新啟動。  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>設定群組原則物件以指定軟體更新點  

1. 使用 [群組原則管理主控台]  來開啟新的或現有的群組原則物件。  

2. 依序展開 [電腦設定]  、[系統管理範本]  和 [Windows 元件]  ，然後選取 [Windows Update]  。  

3. 開啟 [指定近端內部網路 Microsoft 更新服務的位置]  設定的內容，然後選取 [已啟用]  。  

4. **設定偵測更新的近端內部網路更新服務**：指定軟體更新點伺服器的名稱和連接埠。  

    - 如果您已將 Configuration Manager 站台系統設定為使用完整網域名稱 (FQDN)，請使用此格式。  

    - 如果 Configuration Manager 站台系統未設定為使用 FQDN，請使用短名稱格式。

    > [!TIP]  
    > 若要判斷連接埠號碼，請參閱[如何判斷 WSUS 使用的連接埠設定](../../../sum/plan-design/plan-for-software-updates.md)。

    FQDN 格式範例：`http://server1.contoso.com:8530`  

5. **設定近端內部網路統計伺服器**：此設定通常是使用相同的伺服器名稱設定的。

6. 將群組原則物件指派給您要安裝用戶端及接收軟體更新的電腦。  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>將設定管理員用戶端發佈到軟體更新點  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取您要為其設定以軟體更新為基礎之用戶端安裝的站台。  

3. 在功能區的 [首頁]  索引標籤上，選取 [設定]  群組中的 [用戶端安裝設定]  ，然後選取 [以軟體更新為基礎的用戶端安裝]  。  

4. 選取 [啟用以軟體更新為基礎的用戶端安裝]  。  

5. 如果站台的的用戶端版本比軟體更新點上的版本還要新，則會開啟 [偵測到較新版本的用戶端套件]  對話方塊。 選取 [是]  以發佈最新版本。  

    > [!NOTE]  
    > 如果您尚未將用戶端軟體發佈到軟體更新點，此方塊會是空白的。

設定管理員用戶端的軟體更新不會在有新版本時自動更新。 當您更新站台時，請重複此程序來更新用戶端。  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> 群組原則安裝

使用 Active Directory Domain Services 中的群組原則發佈或指派設定管理員用戶端。 用戶端會在電腦啟動時安裝。 當您使用群組原則時，用戶端會顯示在 [控制台] 中的 [新增或移除程式]  中，以供使用者安裝。 您可以從 DPM 安裝程式進行安裝。  

將 Windows Installer 套件 CCMSetup.msi 用於以群組原則為基礎的安裝。 此檔案可在站台伺服器的 `<ConfigMgr installation directory>\bin\i386` 資料夾中找到。 您無法將內容新增至此檔案以修改安裝行為。  

> [!IMPORTANT]  
> 您必須擁有系統管理員權限，才能存取用戶端安裝檔案。  

- 如果您已擴充 Configuration Manager 的 Active Directory 架構，而且已選取 [站台內容]  對話方塊中 [發行]  索引標籤上的網域，則用戶端電腦會自動搜尋 Active Directory Domain Services 的安裝內容。 如需詳細資訊，請參閱[關於發佈至 Active Directory Domain Services 的用戶端安裝內容](about-client-installation-properties-published-to-active-directory-domain-services.md)。  

- 如果您尚未擴充 Active Directory 架構，請參閱[如何佈建用戶端安裝內容](#BKMK_Provision)一節，了解將安裝內容儲存在電腦 Windows 登錄中的相關資訊。 當用戶端安裝時會使用這些安裝內容。  

如需詳細資訊，請參閱[如何使用群組原則從遠端安裝軟體](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server) \(英文\)。  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> 手動安裝

使用 CCMSetup.exe 在電腦上手動安裝用戶端軟體。 您可以在站台伺服器上 Configuration Manager 安裝資料夾的 [Client] 資料夾中找到此程式與其支援檔案。 站台會以下列形式對網路共用此資料夾：  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` 是主要站台伺服器名稱。 `<site code>` 是用戶端指派目標之主要站台的站台碼。 若要從用戶端上的命令列執行 CCMSetup.exe，請連線到此網路位置，然後執行命令。  

> [!IMPORTANT]  
> 您必須擁有系統管理員權限，才能存取用戶端安裝檔案。  

CCMSetup.exe 會將所有必要條件複製到用戶端電腦，並且呼叫 Windows Installer 套件 (Client.msi) 來安裝用戶端。 您無法直接執行 Client.msi。  

若要修改用戶端安裝的行為，請指定 CCMSetup.exe 與 Client.msi 的命令列選項。 請務必先指定以 `/` 為開頭的 CCMSetup 參數，再指定 Client.msi 內容。 例如：  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

此範例中會使用下列選項來安裝用戶端：  

|選項|說明|  
|--------------|-----------------|  
|`/mp:SMSMP01`|此 CCMSetup 參數會指定管理點 SMSMP01，以用於下載必要的用戶端安裝檔案。|  
|`/logon`|此 CCMSetup 參數會指定：當發現電腦上已有 Configuration Manager 用戶端時，應該停止安裝。|  
|`SMSSITECODE=AUTO`|此 Client.msi 內容會指定：用戶端會使用 Active Directory 網域服務，嘗試尋找要使用的 Configuration Manager 站台碼。|  
|`FSP=SMSFP01`|此 Client.msi 內容會指定：名為 SMSFP01 的後援狀態點，會用於接收從用戶端電腦傳送的狀態訊息。|  

如需詳細資訊，請參閱[關於用戶端安裝參數和內容](about-client-installation-properties.md)。  

> [!TIP]  
> 如需在現代 Windows 10 裝置上使用 Azure Active Directory (Azure AD) 身分識別安裝設定管理員用戶端的程序，請參閱[安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證](deploy-clients-cmg-azure.md)。 該程序適用於內部網路或網際網路上的用戶端。  

### <a name="manual-installation-examples"></a>手動安裝範例

這些範例適用於內部網路上已加入 Active Directory 的用戶端。 其使用下列值：  

- **MPSERVER**：裝載管理點的伺服器
- **FSPSERVER**：裝載後援狀態點的伺服器  
- **ABC**：站台碼  
- **contoso.com**：網域名稱  

假設您已經以內部網路 FQDN 設定好所有站台系統伺服器，而且已將站台資訊發佈至的 Active Directory。  

在用戶端電腦上開始執行下列步驟：  

1. 以本機系統管理員身分登入。  
2. 將磁碟機 Z: 對應至 `\\MPSERVER\SMS_ABC\Client`。  
3. 將命令提示字元切換至磁碟機 Z。  

然後執行下列其中一個命令：  

#### <a name="manual-example-1"></a>手動範例 1  

`CCMSetup.exe`  

此命令會安裝沒有其他參數或內容的用戶端。 用戶端會自動以發佈至 Active Directory Domain Services 的用戶端安裝內容設定，包括下列設定：  

- 站台碼：此設定需要在您已為用戶端指派設定的界限群組中包含用戶端網路位置。  
- 管理點。
- 後援狀態點。
- 只使用 HTTPS 通訊。  

如需詳細資訊，請參閱[關於發佈至 Active Directory Domain Services 的用戶端安裝內容](about-client-installation-properties-published-to-active-directory-domain-services.md)。  

#### <a name="manual-example-2"></a>手動範例 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
此命令會覆寫 Active Directory Domain Services 提供的自動設定。 它不需要您在為用戶端指派設定的界限群組中包含用戶端網路位置。 相反地，安裝會指定以下設定：

- 站台碼
- 內部網路管理點
- 以網際網路為基礎的管理點
- 接受來自網際網路的連線的後援狀態點
- 使用具有最長有效期限的用戶端公開金鑰基礎結構 (PKI) 憑證 (如果有的話)

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> 登入指令碼安裝

Configuration Manager 支援使用登入指令碼安裝設定管理員用戶端軟體。 使用登入指令碼中的程式檔案 CCMSetup.exe 觸發用戶端安裝。  

登入指令碼安裝所使用的方式，與手動用戶端安裝相同。 為 CCMSsetup.exe 指定 `/logon` 安裝參數。 如果電腦上已經有任何版本的用戶端，此參數可防止安裝用戶端。 此行為可防止每次執行登入指令碼時，都要重新安裝用戶端。  

如果您未透過 `/Source` 參數指定安裝來源，而且未透過 `/MP` 參數指定可從中取得安裝的管理點，CCMSetup.exe 會搜尋 Active Directory Domain Services 來找出管理點。 只有在您已擴充 Configuration Manager 的架構，也已將站台發佈至 Active Directory Domain Services 時，才會發生這種行為。 此外，用戶端可以使用 DNS 或 WINS 尋找管理點。  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> 套件和程式安裝

使用 Configuration Manager 來建立和部署套件與程式，以升級所選裝置的用戶端軟體。 Configuration Manager 提供套件定義檔，可在套件內容中填入一般常用值。 藉由指定其他命令列參數和內容，即可自訂用戶端安裝的行為。  

> [!NOTE]  
> 您無法使用這種方法升級 Configuration Manager 2007 用戶端。 請改用自動用戶端升級，這會自動建立並部署包含最新用戶端版本的套件。 如需詳細資訊，請參閱[升級用戶端](../manage/upgrade/upgrade-clients.md)。  
>
> 如需如何從舊版設定管理員用戶端移轉的詳細資訊，請參閱[規劃用戶端移轉策略](../../migration/planning-a-client-migration-strategy.md)。  

### <a name="create-a-package-and-program-for-the-client-software"></a>建立用戶端軟體的套件和程式  

依照下列程序，建立可部署至 Configuration Manager 用戶端電腦的 Configuration Manager 套件和程式，以升級用戶端軟體。  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [應用程式管理]  ，然後選取 [套件]  節點。  

2. 在功能區的 [首頁]  索引標籤上，選取 [建立]  群組中的 [從定義建立套件]  。  

3. 在精靈的 [套件定義]  頁面上，從 [發行者]  清單中選取 [Microsoft]  ，並從 [套件定義]  清單中選取 [Configuration Manager 用戶端升級]  。  

4. 在 [來源檔案]  頁面上，選取 [永遠從來源資料夾取得檔案]  。  

5. 在 [來源資料夾]  頁面上，選取 [網路路徑 (UNC 名稱)]  。 然後輸入包含用戶端安裝檔案的伺服器和共用的網路路徑。  

    > [!NOTE]  
    > Configuration Manager 部署執行所在的電腦必須能夠存取指定的網路資料夾。 否則，用戶端安裝會失敗。  

    若要變更任何用戶端安裝內容，請在 [Configuration Manager 代理程式無訊息升級內容]  程式對話方塊的 [一般]  索引標籤上，修改 CCMSetup.exe 命令列。 預設安裝內容是 `/noservice SMSSITECODE=AUTO`。  

6. 將套件發佈至所有您想要裝載用戶端升級套件的發佈點。 然後，將套件部署到包含您要升級之用戶端的裝置集合。  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Intune MDM 管理的 Windows 裝置

將 Configuration Manager 用戶端部署至使用 Microsoft Intune 註冊的裝置。

此程序適用於連線到內部網路的傳統用戶端。 它使用傳統的用戶端驗證方法。 為確保裝置在安裝用戶端後維持在受控狀態，它必須位於內部網路中及 Configuration Manager 站台界限內。  

如需在現代 Windows 10 裝置上使用 Azure AD 身分識別安裝設定管理員用戶端的程序，請參閱[安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證](deploy-clients-cmg-azure.md)。

在您安裝 Configuration Manager 用戶端之後，裝置並不會從 Intune 取消註冊。 它們可以使用設定管理員用戶端，同時保有 MDM 註冊。 如需詳細資訊，請參閱[共同管理概觀](../../../comanage/overview.md)。  

> [!Note]
> 您可以使用其他用戶端安裝方法來在受 Intune 管理的裝置上安裝 Configuration Manager 用戶端。 例如，如果受 Intune 管理的裝置位於內部網路上，並已加入 Active Directory 網域，您便可以使用群組原則來安裝 Configuration Manager 用戶端。<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>使用 Intune 來安裝 Configuration Manager 用戶端

1. 在 Intune 中，[新增 Windows 企業營運應用程式](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) (包含設定管理員用戶端安裝檔案 **CCMSetup.msi**)。 您可以在站台伺服器上 Configuration Manager 安裝目錄的 `\bin\i386` 資料夾中找到此檔案。  

2. 在 Intune 軟體發行者中，輸入命令列參數。 例如，對內部網路上的傳統用戶端使用此命令：  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > 如需使用 Azure AD 驗證搭配現代 Windows 10 用戶端的命令範例，請參閱[如何準備網路型裝置進行共同管理](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)。  

3. [指派應用程式](https://docs.microsoft.com/mem/intune/apps/apps-deploy)到已註冊的 Windows 電腦群組。  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> OS 映像安裝

在您用來建立 OS 映像的參照電腦上，預先安裝 Configuration Manager 用戶端。

> [!IMPORTANT]  
> 當您使用 Configuration Manager 工作順序部署作業系統映像時，[準備 ConfigMgr 用戶端](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)步驟會完全移除設定管理員用戶端。  

### <a name="prepare-the-client-computer-for-imaging"></a>準備進行映像處理的用戶端電腦  

1. 在參照電腦上手動安裝設定管理員用戶端軟體。 如需詳細資訊，請參閱[如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)。  

    > [!IMPORTANT]  
    > 請不要在 CCMSetup.exe 命令列內容中指定用戶端的 Configuration Manager 站台碼。  

2. 在命令提示字元中輸入 `net stop ccmexec`，以停止參照電腦上的 SMS Agent Host 服務 (CcmExec.exe)。  

3. 在參照電腦上，將 [Windows] 資料夾中的 SMSCFG.INI 檔案刪除。  

4. 移除參照電腦上儲存於本機電腦存放區中的任何憑證。 例如，如果您使用 PKI 憑證，請在為電腦進行映像處理之前，針對 [電腦]  和 [使用者]  移除 [個人]  存放區中的憑證。  

5. 如果用戶端安裝在不同於參照電腦階層的 Configuration Manager 階層中，請從參照電腦移除受信任的根金鑰。  

    > [!NOTE]  
    > 如果用戶端無法查詢 Active Directory Domain Services 以找出管理點，就會使用信任的根金鑰來判斷信任的管理點。 如果您將所有經過映像處理的用戶端部署在與主要電腦相同的階層中，請保留受信任的根金鑰。
    >
    > 如果您將用戶端部署在不同的階層中，請移除受信任的根金鑰。 並且以新的受信任的根金鑰佈建這些用戶端。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

6. 使用您的映像軟體來擷取參照電腦的映像。  

7. 將映像部署到目的地電腦。  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> 工作群組電腦

Configuration Manager 支援工作群組中電腦的用戶端安裝。 使用[如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)中指定的方法，在工作群組電腦上安裝用戶端。  

### <a name="prerequisites"></a>先決條件  

- 在每部工作群組電腦上手動安裝用戶端。 安裝期間，互動使用者必須具備本機系統管理員權限。  

- 若要存取 Configuration Manager 站台伺服器網域的資源，請針對該站台設定網路存取帳戶。 在軟體發佈站台元件中指定此帳戶。 如需詳細資訊，請參閱[站台元件](../../servers/deploy/configure/site-components.md)。  

### <a name="limitations"></a>限制  

- 工作群組用戶端無法從 Active Directory Domain Services 找到管理點。 相反地，它們會使用 DNS、WINS 或其他管理點。  

- 不支援全域漫遊。 工作群組用戶端無法向 Active Directory Domain Services 查詢站台資訊。  

- Active Directory 探索方法無法探索工作群組中的電腦。  

- 您無法將軟體部署至工作群組電腦的使用者。  

- 您無法使用用戶端推入安裝方法，在工作群組電腦上安裝用戶端。  

- 工作群組用戶端無法使用 Kerberos 進行驗證，它們可能需要手動核准。  

- 您無法將工作群組用戶端設定為發佈點。 Configuration Manager 要求發佈點電腦為網域的成員。  

### <a name="install-the-client-on-workgroup-computers"></a>在工作群組電腦上安裝用戶端  

請檢查先決條件，然後遵循[如何手動安裝設定管理員用戶端](#BKMK_Manual)一節中的指示。  

#### <a name="workgroup-example-1"></a>工作群組範例 1

此範例會執行下列動作：

- 針對內部網路用戶端管理安裝用戶端
- 指定站台碼
- 指定用於找出管理點的 DNS 尾碼  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>工作群組範例 2

此範例要求用戶端位於界限群組中設定的網路位置。 如果不符合此需求，自動站台指派將無法運作。 此命令包含伺服器 FSPSERVER 上的後援狀態點。 此內容可協助追蹤用戶端部署，並找出任何用戶端通訊問題。

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> 以網際網路為基礎的用戶端管理  

> [!NOTE]  
> 此節不適用於使用[雲端管理閘道](../manage/cmg/plan-cloud-management-gateway.md)的用戶端。 若要使用雲端管理閘道來安裝以網際網路為基礎的用戶端，請參閱[安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證](deploy-clients-cmg-azure.md)。  

對於有時位於內部網路、有時在網際網路上的用戶端，當 Configuration Manager 站台支援[以網際網路為基礎的用戶端管理](../manage/plan-internet-based-client-management.md)時，您在內部網路安裝用戶端時有兩個選項：  

- 安裝用戶端時，請使用手動安裝或用戶端推入來包含 Client.msi 內容 `CCMHOSTNAME=<internet FQDN of the internet-based management point>`。 當您使用此方法時，請直接將用戶端指派給站台。 您無法使用自動站台指派。 請參閱[如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)一節，該節提供此設定方法的範例。  

- 針對內部網路用戶端管理安裝用戶端，然後將以網際網路為基礎的用戶端管理點指派給用戶端。 請使用控制台中 [Configuration Manager]  頁面上的用戶端內容，或使用指令碼來變更管理點。 使用此方法時，您可以使用自動用戶端指派。 如需詳細資訊，請參閱[如何在安裝用戶端後，針對以網際網路為基礎的用戶端管理設定用戶端](#BKMK_ConfigureIBCM_MP)一節。  

若要安裝位於網際網路的用戶端，請選擇下列其中一個支援的方法：  

- 提供機制，讓這些用戶端使用 VPN 暫時連線至內部網路。 然後使用任何適當的用戶端安裝方法安裝用戶端。  

- 使用與 Configuration Manager 無關的安裝方法。 例如，將用戶端安裝來源檔封裝至抽取式媒體，然後將媒體寄送給使用者。 用戶端安裝來源檔位於 Configuration Manager 站台伺服器的 `<installation path>\Client` 資料夾中。 在媒體上，納入指令碼以手動複製用戶端資料夾。 從此資料夾安裝用戶端，方法是使用 CCMSetup.exe 以及所有適當的 CCMSetup 命令行內容。  

> [!NOTE]  
> Configuration Manager 不支援直接從以網際網路為基礎的管理點，或從以網際網路為基礎的軟體更新點來安裝用戶端。

在網際網路上受管理的用戶端必須與以網際網路為基礎的站台系統通訊。 請確定您在安裝用戶端之前，這些用戶端也具備公開金鑰基礎結構 (PKI) 憑證。 從 Configuration Manager 個別安裝這些憑證。 如需詳細資訊，請參閱 [PKI 憑證需求](../../plan-design/network/pki-certificate-requirements.md)。  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>指定 CCMSetup 命令列內容，在網際網路上安裝用戶端  

1. 請遵循[如何手動安裝 Configuration Manager 用戶端](#BKMK_Manual)一節中的指示。 一律包含下列選項：  

    - CCMSetup 命令列參數 `/source:<local path of the copied Client folder>`  

    - CCMSetup 命令列參數 `/UsePKICert`  

    - Client.msi 內容 `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Client.msi 內容 `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Client.msi 內容 `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > 如果站台有一個以上以網際網路為基礎的管理點，您要指定將哪一個管理點用於 `CCMHOSTNAME` 內容都沒問題。 Configuration Manager 用戶端連線至以網際網路為基礎的指定管理點時，它會向用戶端傳送站台中以網際網路為基礎的可用管理點清單。 用戶端會從清單中隨機選取一個。

2. 如果您不要讓用戶端檢查憑證撤銷清單 (CRL)，請指定 CCMSetup 命令列參數 `/NoCRLCheck`。  

3. 如果您使用的是以網際網路為基礎的後援狀態點，請指定 Client.msi 內容 `FSP=<internet FQDN of the internet-based fallback status point>`。  

4. 如果您要針對僅在網際網路上執行的用戶端管理安裝用戶端，請指定 Client.msi 內容 `CCMALWAYSINF=1`。  

5. 判斷您是否必須指定其他 CCMSetup 命令列參數。 例如，如果用戶端有多個有效的 PKI 憑證，您可能必須指定憑證選取準則。 如需可用內容的清單，請參閱[關於用戶端安裝參數和內容](about-client-installation-properties.md)。  

#### <a name="internet-based-example"></a>以網際網路為基礎的範例

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

此範例會以下列行為安裝用戶端：

- 使用 D 磁碟機上資料夾的原始程式檔。
- 使用用戶端 PKI 憑證。
- 選取具有最長有效期限的憑證。
- 僅在網際網路上執行的用戶端管理。
- 指派用戶端使用名為 SERVER1 這個以網際網路為基礎的管理點。
- 指派 contoso.com 網域中以網際網路為基礎的後援狀態點。
- 將用戶端指派至 ABC 站台。  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> 安裝用戶端後，針對以網際網路為基礎的用戶端管理設定用戶端  

若要在安裝用戶端後指派以網際網路為基礎的管理點，請使用以下其中一種程序。 第一個需要手動設定，且適用於少數用戶端。 第二個較適合設定多個用戶端。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>從 Configuration Manager 控制台安裝用戶端後，針對以網際網路為基礎的用戶端管理設定用戶端  

1. 在用戶端上開啟 **Configuration Manager** 控制台。  

2. 在 [網際網路]  索引標籤上，輸入以網際網路為基礎之管理點的完整網域名稱 (FQDN) 作為 [網際網路 FQDN]  。  

    > [!NOTE]  
    > [網際網路]  索引標籤僅在用戶端具備用戶端 PKI 憑證時才能使用。  

3. 如果用戶端使用 Proxy 伺服器存取網際網路，請輸入 Proxy 伺服器設定。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>安裝用戶端後，使用指令碼針對以網際網路為基礎的用戶端管理設定用戶端  

##### <a name="powershell"></a>PowerShell

1. 開啟 PowerShell 內嵌編輯器，例如 PowerShell ISE 或 Visual Studio Code。 您也可以使用文字編輯器，例如 [記事本]。

2. 複製下列程式碼並插入到編輯器中。 將 `'mp.contoso.com'` 取代為以網際網路為基礎的管理點的網際網路 FQDN。

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > 最後一行的目的是要驗證新的網際網路管理點值。
    >
    > 若要刪除以網際網路為基礎的指定管理點，請移除引號內的伺服器 FQDN 值。 這一行會變成 `$newInternetBasedManagementPointFQDN = ''`。

3. 以副檔名 .ps1 儲存檔案。  

4. 以用戶端電腦上較高的權限執行指令碼。 使用下列其中一種方法：  

    - 使用套件和程式，將檔案部署至現有 Configuration Manager 用戶端。  

    - 按兩下檔案總管中的指令碼檔案，在現有的設定管理員用戶端上本機執行檔案。  

您可能必須重新啟動用戶端，變更才會生效。  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> 佈建用戶端安裝內容

針對以群組原則和軟體更新為基礎的用戶端安裝佈建用戶端安裝內容。 使用 Windows 群組原則，以設定管理員用戶端安裝內容來佈建電腦。 這些內容會儲存在電腦的登錄中。 用戶端安裝時會讀取這些內容。 這通常不是必要程序，但部分用戶端安裝情況可能需要這個程序，例如：  

- 您使用群組原則設定或以軟體更新為基礎的用戶端安裝方法。 您尚未延伸 Configuration Manager 的 Active Directory 架構。  

- 您想在特定電腦上覆寫用戶端安裝內容。  

> [!NOTE]  
> 如果 CCMSetup.exe 命令列上已提供任何安裝內容，就不會使用佈建在電腦上的安裝內容。

Configuration Manager 安裝媒體上提供了名為 `ConfigMgrInstallation.adm` 的群組原則系統管理範本。 使用此範本以安裝內容來佈建用戶端電腦。

> [!TIP]
> 根據預設，`ConfigMgrInstallation.adm` 不支援大於 255 個字元的字串。 此設定可能會影響到新增多個參數，或是具有較長值的參數 (例如 CCMCERTISSUERS)。<!-- SCCMDocs#1648 -->
>
> 此問題的因應措施：
>
> 1. 在記事本中編輯 `ConfigMgrInstallation.adm`。
> 2. 針對 `VALUENAME SetupParameters` 屬性，將 `MAXLEN` 值變更為較大的整數。 例如 `MAXLEN 511`。

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>使用群組原則物件設定和指派用戶端安裝內容  

1. 使用如 Windows 群組原則物件編輯器的編輯器，將 ConfigMgrInstallation.adm 系統管理範本匯入至新的或現有的群組原則物件 (GPO)。 您可以在 Configuration Manager 安裝媒體上的 `TOOLS\ConfigMgrADMTemplates` 資料夾中找到此檔案。  

2. 開啟已匯入設定 [設定用戶端部署設定]  的屬性。  

3. 選取 [已啟用]  。  

4. 在 [CCMSetup]  方塊中，輸入必要的 CCMSetup 命令列屬性。 如需所有 CCMSetup 命令列內容及其用法範例的清單，請參閱[關於用戶端安裝參數和內容](about-client-installation-properties.md)。  

5. 將 GPO 指派給您要以設定管理員用戶端安裝內容來佈建的電腦。  
