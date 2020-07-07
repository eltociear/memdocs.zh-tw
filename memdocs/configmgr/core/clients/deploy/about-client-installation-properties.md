---
title: 用戶端安裝參數和屬性
titleSuffix: Configuration Manager
description: 了解用來安裝 Configuration Manager用戶端的 ccmsetup 命令列參數和屬性。
ms.date: 06/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 388a051f899369aa6a7754f94b0a7727f943f0ec
ms.sourcegitcommit: efe89408a3948b79b38893174cb19268ee37c8f3
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854400"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>關於 Configuration Manager 中的用戶端安裝參數和屬性

適用於：Configuration Manager (最新分支)

使用 CCMSetup.exe 命令來安裝設定管理員用戶端。 如果在命令列上提供用戶端安裝「參數」，則這些參數會修改安裝行為。 如果在命令列上提供用戶端安裝「屬性」，則這些屬性會修改所安裝用戶端代理程式的初始組態。

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> 關於 CCMSetup.exe

CCMSetup.exe 命令會下載所需的檔案，以從管理點或來源位置安裝用戶端。 這些檔案可能包含下列項目：  

- 安裝用戶端軟體的 Windows Installer 套件 client.msi

- 用戶端先決條件

- Configuration Manager 用戶端的更新和修正程式

> [!NOTE]
> 您無法直接安裝 client.msi。  

CCMSetup.exe 提供命令列「參數」來自訂安裝。 參數前面會加上斜線 (`/`)，且依慣例會採用小寫。 您可在必要時指定參數值，方法是使用冒號 (`:`)，後面緊接著值。 如需詳細資訊，請參閱 [CCMSetup.exe 命令列參數](#ccmsetupexe-command-line-parameters)。

您也可以在 CCMSetup.exe 命令列提供「屬性」來修改 client.msi 的行為。依慣例，屬性會採用大寫。 指定屬性值的方式是使用等號 (`=`)，後面緊接著值。 如需詳細資訊，請參閱 [Client.msi 屬性](#clientMsiProps)。

> [!IMPORTANT]  
> 請先指定 CCMSetup 參數，再指定 client.msi 的屬性。  

CCMSetup.exe 及其支援檔案位於站台伺服器上 Configuration Manager 安裝資料夾的 **Client** 資料夾中。 Configuration Manager 會將此資料夾與站台共用下的網路共用。 例如 `\\SiteServer\SMS_ABC\Client`。

在命令列提示字元，CCMSetup.exe 命令會使用下列格式：  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

例如：  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

此範例會執行下列動作：  

- 指定名為 SMSMP01 的管理點要求發佈點清單，以下載用戶端安裝檔案。  

- 指定如果電腦上已存在用戶端版本，則應停止安裝程序。  

- 指示 client.msi 將用戶端指派為網站碼 S01。  

- 指示 client.msi 使用名為 SMSFP01 的後援狀態點。  

> [!TIP]  
> 如果參數具有空白字元，請使用引號將其括住。  

如果擴充 Configuration Manager 的 Active Directory 架構，則站台會在 Active Directory Domain Services 中發佈許多用戶端安裝屬性。 設定管理員用戶端會自動讀取這些屬性。 如需詳細資訊，請參閱[關於發佈至 Active Directory 網域服務的用戶端安裝屬性](about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="ccmsetupexe-command-line-parameters"></a>CCMSetup.exe 命令列參數

### <a name=""></a><a name="bkmk_help"></a> /?

顯示 ccmsetup.exe 的可用命令列參數。  

範例：`ccmsetup.exe /?`

### <a name="source"></a>/source

指定檔案的下載位置。 使用本機或 UNC 路徑。 裝置會利用伺服器訊息區 (SMB) 通訊協定下載檔案。 若要使用 **/source**，則進行用戶端安裝的 Windows 使用者帳戶需要該位置的**讀取**權限。

如需 ccmsetup 如何下載內容的詳細資訊，請參閱[界限群組 - 用戶端安裝](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)。 如果您同時使用 **/mp** 與 **/source** 參數，該文章也會包含 ccmsetup 行為的詳細資料。

> [!TIP]  
> 您可以在命令列中多次使用 **/source** 參數來指定替代的下載位置。  

範例：`ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

指定電腦要連線的來源管理點。 電腦會使用此管理點來尋找安裝檔案的最接近發佈點。 如果沒有發佈點或電腦在 4 小時後仍無法從發佈點下載檔案，它們便會從指定的管理點下載檔案。  

如需 ccmsetup 如何下載內容的詳細資訊，請參閱[界限群組 - 用戶端安裝](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)。 如果您同時使用 **/mp** 與 **/source** 參數，該文章也會包含 ccmsetup 行為的詳細資料。

> [!IMPORTANT]  
> 此參數會指定可供電腦尋找下載來源的初始管理點，且可以是任何站台中的任何管理點。 不會將用戶端「指派」給指定的管理點。

電腦會根據用戶端連線的網站系統角色設定，透過 HTTP 或 HTTPS 連線下載檔案。 如有設定，您也可以使用 BITS 節流進行下載。 如果將所有發佈點和管理點設為僅供 HTTPS 用戶端連線，請確認用戶端電腦具備有效的用戶端憑證。  

您可以使用 **/mp** 命令列參數來指定多個管理點。 如果電腦無法連線到第一個管理點，則會嘗試指定清單中的下一個管理點。 當您指定多個管理點時，請使用分號分隔這些值。

如果用戶端使用 HTTPS 連線到管理點，請指定 FQDN，而不是電腦名稱。 此值必須符合管理點 PKI 憑證的**主體名稱**或**主體別名**。 雖然 Configuration Manager 支援在內部網路上使用憑證中的電腦名稱來進行連線，但建議使用 FQDN。

使用電腦名稱的範例：`ccmsetup.exe /mp:SMSMP01`  

使用 FQDN 的範例：`ccmsetup.exe /mp:smsmp01.contoso.com`  

此參數也可以指定雲端管理閘道 (CMG) 的 URL。 使用這個 URL 在以網際網路為基礎的裝置上安裝用戶端。 若要取得此參數的值，請使用下列步驟：

- 建立 CMG。 如需詳細資訊，請參閱[設定 CMG](../manage/cmg/setup-cloud-management-gateway.md)。
- 在使用中用戶端上，以系統管理員身分開啟 Windows PowerShell 命令提示字元。
- 執行下列命令：

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- 附加 `https://` 首碼以與 **/mp** 參數搭配使用。

當您使用雲端管理閘道 URL 時的範例：`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> 為 **/mp** 參數指定雲端管理閘道的 URL 時，其開頭必須是 `https://`。

### <a name="regtoken"></a>/regtoken

<!--5686290-->

從 2002 版開始，您可使用此參數來提供大量註冊權杖。 網際網路型裝置會在透過雲端管理閘道 (CMG) 的註冊程序中使用此權杖。 如需詳細資訊，請參閱 [CMG 的權杖型驗證](deploy-clients-cmg-token.md)。

當使用此參數時，亦需一併加入下列參數和屬性：

- [ **/mp**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

下列範例命令列包含其他必要的安裝程式參數和屬性：

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

如果 CCMSetup.exe 無法下載安裝檔案，請使用此參數來指定重試間隔 (分鐘)。 CCMSetup 會持續重試，直到達到 [ **/downloadtimeout**](#downloadtimeout) 參數所指定的限制為止。

範例：`ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

此參數可防止 CCMSetup 以預設的服務形式執行。 當 CCMSetup 以服務形式執行時，它會在電腦的本機系統帳戶內容中執行。 此帳戶可能沒有足夠權限可以存取安裝必要的網路資源。 若使用 **/noservice**，CCMSetup.exe 會在您用於啟動安裝的使用者帳戶內容中執行。

範例：`ccmsetup.exe /noservice`  

### <a name="service"></a>/service

指定 CCMSetup 應以使用本機系統帳戶的服務形式執行。  

> [!TIP]
> 如果搭配 **/service** 參數使用指令碼來執行 CCMSetup.exe，CCMSetup.exe 就會在服務啟動後結束。 而可能無法正確回報安裝詳細資料給指令碼。

範例：`ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

使用此參數來解除安裝 Configuration Manager 用戶端。 如需詳細資訊，請參閱[解除安裝用戶端](../manage/manage-clients.md#BKMK_UninstalClient)。

範例：`ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

如果已安裝任何版本的用戶端，此參數會指定應該停止用戶端安裝。  

範例：`ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

如有必要，請使用此參數來強制電腦重新啟動以完成安裝。 如果未指定此參數，CCMSetup 就會在需要重新啟動時結束。 然後在下一次手動重新啟動之後繼續。

範例：`CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

當裝置透過 HTTP 連線下載用戶端安裝檔案時，請使用此參數來指定下載優先順序。 請指定下列其中一個可能的值：

- `FOREGROUND`

- `HIGH`

- `NORMAL` (預設)

- `LOW`

範例：`ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

如果 CCMSetup 無法下載用戶端安裝檔案，則此參數會指定逾時上限 (分鐘)。 超過此逾時值，CCMSetup 就會停止嘗試下載安裝檔案。 預設值為 **1440** 分鐘 (一天)。

使用 [ **/retry**](#retry) 參數來指定重試嘗試之間的間隔。

範例：`ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

為用戶端指定此參數，以使用 PKI 用戶端驗證憑證。 如果未包含此參數，或如果用戶端找不到有效的憑證，則會使用具有自我簽署憑證的 HTTP 連線。

範例：`CCMSetup.exe /UsePKICert`  

> [!NOTE]
> 在某些情況下，您不需要指定此參數，但仍可以使用用戶端憑證。 例如，以用戶端推入和軟體更新為基礎的用戶端安裝。 當手動安裝用戶端並搭配啟用 HTTPS 的管理點使用 **/mp** 參數時，請使用此參數。
>
> 此外，當安裝用戶端來進行僅限網際網路的通訊時，請指定此參數。 請將 **CCMALWAYSINF=1** 屬性與以網際網路為基礎的管理點屬性 (**CCMHOSTNAME**) 及站台碼屬性 (**SMSSITECODE**) 搭配使用。 如需以網際網路為基礎的用戶端管理的詳細資訊，請參閱[從網際網路或未受信任之樹系的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

### <a name="nocrlcheck"></a>/NoCRLCheck

指定用戶端在使用 PKI 憑證進行 HTTPS 通訊時，不應該檢查憑證撤銷清單 (CRL)。 若未指定此參數，則用戶端會先檢查 CRL，再建立 HTTPS 連線。 如需有關用戶端 CRL 檢查的詳細資訊，請參閱 [PKI 憑證撤銷的規劃](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。

範例：`CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

此參數會指定列出用戶端安裝屬性的文字檔。

- 如果 CCMSetup 以服務形式執行，請將此檔案放在 CCMSetup 系統資料夾 `%Windir%\Ccmsetup` 中。

- 如果指定 [ **/noservice**](#noservice) 參數，請將此檔案放在與 CCMSetup.exe 相同的資料夾中。

範例：`CCMSetup.exe /config:"configuration file name.txt"`

為了提供正確檔案格式，請使用站台伺服器上 Configuration Manager 安裝目錄其 `\bin\<platform>` 資料夾中的 **mobileclienttemplate.tcf** 檔案。 此檔案具有各區段及其使用方式的相關註解。 在 `[Client Install]` 區段中的 `Install=INSTALL=ALL` 文字後方指定用戶端安裝屬性。

`[Client Install]` 區段項目的範例：`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

此參數會指定 CCMSetup.exe 不安裝指定的必要條件。 您可輸入多個值。 使用分號字元 (`;`) 分隔每一個值。

範例：

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

如需用戶端先決條件的詳細資訊，請參閱 [Windows 用戶端先決條件](prerequisites-for-deploying-clients-to-windows-computers.md)。

### <a name="forceinstall"></a>/forceinstall

指定 CCMSetup.exe 解除安裝任何現有的用戶端，並安裝新的用戶端。  

### <a name="excludefeatures"></a>/ExcludeFeatures

此參數會指定 CCMSetup.exe 不安裝指定的功能。

範例：`CCMSetup.exe /ExcludeFeatures:ClientUI` 不會在用戶端上安裝軟體中心。  

> [!NOTE]  
> `ClientUI` 是 **/ExcludeFeatures** 參數唯一支援的值。

### <a name="alwaysexcludeupgrade"></a>/AlwaysExcludeUpgrade

此參數會指定用戶端是否會在您啟用 [[自動用戶端升級](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)] 時自動升級。

支援的值：

- `TRUE`：用戶端不會自動升級
- `FALSE`：用戶端會自動升級 (預設值)

例如：  

`CCMSetup.exe /AlwaysExcludeUpgrade:TRUE`

如需詳細資訊，請參閱[延伸互通性用戶端](../../understand/interoperability-client.md)。

> [!NOTE]  
> 使用 **/AlwaysExcludeUpgrade** 參數時，自動升級仍會執行。 不過，當系統執行 CCMSetup 以執行升級時，其會注意到已設定 **/AlwaysExcludeUpgrade** 參數，並會在 **ccmsetup.log** 中記錄下列這一行：
>
> `Client is stamped with /alwaysexcludeupgrade. Stop proceeding.`
>
> CCMSetup 將會立即結束，且不會執行升級。

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> CCMSetup.exe 傳回碼

CCMSetup.exe 命令會提供下列傳回碼。 若要進行疑難排解，請檢閱用戶端上的 `%WinDir%\ccmsetup\ccmsetup.log`，以取得傳回碼的內容和其他詳細資料。

|傳回碼|意義|  
|-----------|-------|  
|0|成功|  
|6|錯誤|  
|7|需要重新開機|  
|8|安裝程式已在執行中|  
|9|必要條件評估失敗|  
|10|安裝程式資訊清單雜湊驗證失敗|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a> Ccmsetup.msi 屬性

下列屬性可以修改 ccmsetup.msi 的安裝行為。

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

使用此 ccmsetup.*msi* 屬性將其他命令列參數和屬性傳遞給 ccmsetup.*exe*。 請以引號 (`"`) 括住其他參數和屬性。 當使用 [Intune MDM 安裝方法](plan/client-installation-methods.md#microsoft-intune-mdm-installation)來啟動載入 Configuration Manager 用戶端時，請使用此屬性。

範例：`ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune 會將命令列限制為 1024 個字元。

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a> Client.msi 屬性

下列屬性可以修改 ccmsetup.exe 所安裝 client.msi 的安裝行為。 如果使用[用戶端推入安裝方法](plan/client-installation-methods.md#client-push-installation)，請在 Configuration Manager 主控台其 [用戶端推入安裝內容] 的 [用戶端] 索引標籤中指定這些屬性。

### <a name="aadclientappid"></a>AADCLIENTAPPID

指定 Azure Active Directory (Azure AD) 用戶端應用程式識別碼。 當為雲端管理[設定 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)時，可建立或匯入用戶端應用程式。 Azure 系統管理員可以從 Azure 入口網站取得此屬性的值。 如需詳細資訊，請參閱[取得應用程式識別碼](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。 針對 **AADCLIENTAPPID** 屬性，此應用程式識別碼適用於 [原生] 應用程式類型。

範例：`ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

指定 Azure AD 伺服器應用程式識別碼。 當為雲端管理[設定 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)時，可建立或匯入伺服器應用程式。 當建立伺服器應用程式時，在 [建立伺服器應用程式] 視窗中，此屬性是 [App 識別碼 URI]。

Azure 系統管理員可以從 Azure 入口網站取得此屬性的值。 在 **Azure Active Directory** 中，於 [應用程式註冊] 下尋找伺服器應用程式。 尋找應用程式類型 [Web 應用程式/API]。 開啟應用程式，選取 [設定]，然後選取 [屬性]。 針對此 **AADRESOURCEURI** 用戶端安裝屬性，使用 [App 識別碼 URI] 值。

範例：`ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

指定 Azure AD 租用戶識別碼。 當為雲端管理[設定 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)時，Configuration Manager 會連結至此租用戶。 若要取得這個屬性的值，請使用下列步驟：

- 在已加入相同 Azure AD 租用戶的 Windows 10 裝置上，開啟命令提示字元。
- 執行下列命令：`dsregcmd.exe /status`
- 在 [裝置狀態] 區段中，尋找 **TenantId** 值。 例如， `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Azure 系統管理員也可以在 Azure 入口網站取得此值。 如需詳細資訊，請參閱[取得租用戶識別碼](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。

範例：`ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

指定一個或多個 Windows 使用者帳戶或群組，授與用戶端設定和原則的存取權限。 此屬性適用於在用戶端電腦上沒有本機系統管理認證的情況。 指定以分號 (`;`) 分隔的帳戶清單。

範例：`CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

如有必要，請允許電腦以無訊息方式在用戶端安裝後重新啟動。

> [!IMPORTANT]  
> 當使用此屬性時，電腦會重新啟動，而不顯示警告。 即使使用者已登入 Windows，也會發生這種行為。

範例：`CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

若要指定用戶端一律是以網際網路為基礎，且永遠不會連線到內部網路，請將此屬性值設定為 `1`。 用戶端的連線類型會顯示 [永遠為網際網路] 。  

搭配 [**CCMHOSTNAME**](#ccmhostname) 使用此屬性來指定以網際網路為基礎管理點的 FQDN。 您也可以將其與 CCMSetup 參數 [ **/UsePKICert**](#usepkicert) 及站台碼 ([**SMSSITECODE**](#smssitecode)) 搭配使用。

如需以網際網路為基礎的用戶端管理的詳細資訊，請參閱[從網際網路或未受信任之樹系的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。

範例：`CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

使用此屬性來指定憑證簽發者清單。 此清單包含 Configuration Manager 站台所信任受信任的根憑證授權單 (CA) 相關憑證資訊。  

根 CA 憑證中的主體屬性會區分大小寫。 請以逗號 (`,`) 或分號 (`;`) 分隔屬性。 並使用分隔線 (`|`) 來指定多個根 CA 憑證。

範例：`CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> 請使用站台的 **mobileclient.tcf** 檔案中 **CertificateIssuers** 屬性值。 此檔案位於站台伺服器上 Configuration Manager 安裝目錄的 `\bin\<platform>` 子資料夾中。

如需憑證簽發者清單，以及憑證選取程序期間，用戶端如何使用清單的詳細資訊，請參閱[規劃 PKI 用戶端憑證選擇](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)。

### <a name="ccmcertsel"></a>CCMCERTSEL

如果用戶端有一個以上適用於 HTTPS 通訊的憑證，則此屬性會指定準則，讓其能夠選取有效的用戶端驗證憑證。

使用下列關鍵字來搜尋憑證主體名稱或主體別名：

- **主旨**：尋找完全相符的項目
- **SubjectStr**：尋找部分符合的項目

範例：

- `CCMCERTSEL="Subject:computer1.contoso.com"`：搜尋與 [主體名稱] 或 [主體別名] 中電腦名稱 `computer1.contoso.com` 完全相符的憑證。

- `CCMCERTSEL="SubjectStr:contoso.com"`：搜尋 [主體名稱] 或 [主體別名] 中含 `contoso.com` 的憑證。

使用 **SubjectAttr** 關鍵字來搜尋 [主體名稱] 或 [主體別名] 中的物件識別碼 (OID) 或辨別名稱屬性。

範例：

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`：搜尋以物件識別碼表示並命名為 `Computers` 的組織單位屬性。

- `CCMCERTSEL="SubjectAttr:OU = Computers"`：搜尋以辨別名稱表示並命名為 `Computers` 的組織單位屬性。

> [!IMPORTANT]
> 如果使用 [主體名稱]，則 **Subject** 關鍵字區分大小寫，而 **SubjectStr** 關鍵字不區分大小寫。
>
> 如果使用 [主體別名]，則 **Subject** 和 **SubjectStr** 關鍵字皆不區分大小寫。

如需可用於憑證選擇的完整屬性清單，請參閱 [PKI 憑證選擇準則支援的屬性值](#BKMK_attributevalues)。

如果有一個以上的憑證符合搜尋，且將 [**CCMFIRSTCERT**](#ccmfirstcert) 設定為 `1`，則用戶端安裝程式會選取有效期最長的憑證。

### <a name="ccmcertstore"></a>CCMCERTSTORE

如果用戶端安裝程式在電腦的預設 [個人] 憑證存放區中找不到有效的憑證，請使用此屬性來指定替代憑證存放區名稱。

範例：`CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

此屬性會在用戶端安裝時啟用偵錯記錄。 此屬性可讓用戶端記錄用於疑難排解的低階資訊。 請避免在生產站台中使用此屬性。 可能發生過多記錄，讓您難以在記錄檔中尋找相關資訊。 請同時啟用 [**CCMENABLELOGGING**](#ccmenablelogging)。

支援的值：

- `0`：關閉偵錯記錄 (預設)
- `1`：開啟偵錯記錄

範例：`CCMSetup.exe CCMDEBUGLOGGING=1`  

如需詳細資訊，請參閱[關於記錄檔](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Configuration Manager 預設會啟用記錄。

支援的值：

- `TRUE`：開啟記錄 (預設)
- `FALSE`：關閉記錄

範例：`CCMSetup.exe CCMENABLELOGGING=TRUE`  

如需詳細資訊，請參閱[關於記錄檔](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

用戶端健全狀況評估工具 (ccmeval.exe) 執行的頻率 (分鐘)。 請指定介於 `1` 到 `1440` 之間的整數值。 根據預設，ccmeval 會一天 (1440 分鐘) 執行一次。

範例：`CCMSetup.exe CCMEVALINTERVAL=1440`

如需用戶端健全狀況評估的詳細資訊，請參閱[監視用戶端](../manage/monitor-clients.md#bkmk_health)。

### <a name="ccmevalhour"></a>CCMEVALHOUR

用戶端健全狀況評估工具 (ccmeval.exe) 執行當天的時數。 請指定介於 `0` (午夜) 到 `23` (下午 11:00) 之間的整數值。 根據預設，ccmeval 會在午夜執行。

如需用戶端健全狀況評估的詳細資訊，請參閱[監視用戶端](../manage/monitor-clients.md#bkmk_health)。

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

如果將此屬性設定為 `1`，則用戶端會選取有效期最長的 PKI 憑證。

範例：`CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

如果是透過網際網路管理用戶端，則此屬性會指定以網際網路為基礎之管理點的 FQDN。  

請勿指定將此選項搭配 **SMSSITECODE=AUTO** 的安裝屬性。 請將以網際網路為基礎用戶端直接指派給同樣基礎的站台。

範例：`CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

此屬性可以指定雲端管理閘道 (CMG) 的位址。 若要取得這個屬性的值，請使用下列步驟：

- 建立 CMG。 如需詳細資訊，請參閱[設定 CMG](../manage/cmg/setup-cloud-management-gateway.md)。
- 在使用中用戶端上，以系統管理員身分開啟 Windows PowerShell 命令提示字元。
- 執行下列命令：

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- 原封不動使用傳回值與 **CCMHOSTNAME** 屬性。

例如：`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> 當針對 **CCMHOSTNAME** 屬性指定 CMG 的位址時，請勿附加 `https://` 之類的首碼。 請只將此首碼與 CMG 的 **/mp** URL 搭配使用。

### <a name="ccmhttpport"></a>CCMHTTPPORT

指定用戶端在透過 HTTP 與站台系統伺服器通訊時所要使用的連接埠。 根據預設，此值為 `80`。

範例：`CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

指定用戶端在透過 HTTPS 與站台系統伺服器通訊時所要使用的連接埠。 根據預設，此值為 `443`。

範例：`CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

使用此屬性來設定安裝 Configuration Manager 用戶端檔案的資料夾。 預設會使用 `%WinDir%\CCM`。

> [!TIP]
> 無論將用戶端檔案安裝在何處，一律會在 `%WinDir%\System32` 資料夾中安裝 **ccmcore.dll** 檔案。 在 64 位元 OS 上，則會在 `%WinDir%\SysWOW64` 資料夾中安裝 ccmcore.dll 的複本。 這個檔案支援 32 位元應用程式，該應用程式會使用來自 Configuration Manager SDK 的 32 位元版本用戶端 API。

範例：`CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

使用此屬性來指定要寫入 Configuration Manager 記錄檔的詳細資料層級。

支援的值：

- `0`：詳細資訊
- `1`：預設值
- `2`：警告和錯誤
- `3`：僅錯誤

範例：`CCMSetup.exe CCMLOGLEVEL=0`

如需詳細資訊，請參閱[關於記錄檔](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

當 Configuration Manager 記錄檔達到大小上限時，用戶端會將它重新命名以當作備份，並建立新的記錄檔。 此屬性可指定要保留多少個舊版的記錄檔。 預設值為 `1`。 如果將此值設定為 `0`，則用戶端不會保留任何記錄檔歷程記錄。

範例：`CCMSetup.exe CCMLOGMAXHISTORY=5`

如需詳細資訊，請參閱[關於記錄檔](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

此屬性會指定記錄檔大小上限 (位元組)。 當記錄檔成長到指定大小時，用戶端會將其重新命名為歷程記錄檔案，並建立新的記錄檔。 預設大小為 250,000 個位元組，而大小下限為 10,000 個位元組。

範例：`CCMSetup.exe CCMLOGMAXSIZE=300000` (300,000 個位元組)

### <a name="disablesiteopt"></a>DISABLESITEOPT

將此屬性設定為 `TRUE`，以禁止系統管理員在 Configuration Manager 控制台中變更指派的站台。

範例：**CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

如果設為 TRUE，這個屬性會停用系統管理使用者在 **Configuration Manager** 控制台中變更用戶端快取資料夾設定的能力。  

範例：`CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

指定用戶端的 DNS 網域以尋找在 DNS 中發佈的管理點。 當用戶端找到管理點時，會告知用戶端有關階層中的其他管理點。 此行為表示用戶端從 DNS 找到的管理點可以是階層中任何管理點。

> [!NOTE]
> 如果用戶端位於與已發佈管理點相同的網域，您就不必指定此屬性。 若是這種情況，會自動使用用戶端網域來搜尋管理點的 DNS。

如需發佈為設定管理員用戶端服務位置方法之 DNS 的詳細資訊，請參閱[服務位置以及用戶端如何判斷其指派的管理點](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)。

> [!NOTE]  
> 根據預設，Configuration Manager 不會啟用 DNS 發佈。

範例：`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

指定後援狀態點，這些狀態點會接收及處理 Configuration Manager 用戶端所傳送的狀態訊息。

如需詳細資訊，請參閱[判斷是否需要後援狀態點](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)。

範例：`CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

如果將此屬性設定為 `TRUE`，則用戶端安裝程式不會檢查 Microsoft Application Virtualization (App-V) 版本是否符合最低需求。

> [!IMPORTANT]  
> 如果安裝 Configuration Manager 用戶端而未安裝 App-V，則無法[部署虛擬應用程式](../../../apps/get-started/deploying-app-v-virtual-applications.md)。

範例：`CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

當啟用此屬性時，用戶端會報告狀態，但不會針對所找到的問題進行補救。

範例：`CCMSetup.exe NOTIFYONLY=TRUE`

如需詳細資訊，請參閱[如何設定用戶端狀態](configure-client-status.md)。

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

從 2002 版開始，您可使用此屬性在用戶端成功向站台註冊後，於其上啟動工作順序。

> [!NOTE]
> 若工作順序會安裝軟體更新或應用程式，用戶端就需要有效的用戶端驗證憑證。 單一權杖驗證無法使用。 如需詳細資訊，請參閱[版本資訊 - OS 部署](../../servers/deploy/install/release-notes.md#os-deployment)。<!--7527072-->
      
例如，您使用 Windows Autopilot 佈建新的 Windows 10 裝置、將該裝置自動註冊到 Microsoft Intune，然後安裝 Configuration Manager 用戶端以進行共同管理。 如果指定這個新選項，新佈建的用戶端就會執行工作順序。 這個處理序可讓您更靈活地安裝應用程式和軟體更新，或進行設定。


請使用下列程序：

1. [建立非 OS 部署工作順序](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)來安裝應用程式、安裝軟體更新，以及進行設定。

1. [部署此工作順序](../../../osd/deploy-use/deploy-a-task-sequence.md)到 [所有佈建裝置] 這個新的內建集合。 請記下工作順序部署識別碼，例如 `PRI20001`。

1. 在裝置上[安裝 Configuration Manager 用戶端](deploy-clients-to-windows-computers.md#BKMK_Manual)，並包含下列屬性：`PROVISIONTS=PRI20001`。 請將此屬性的值設定為工作順序部署識別碼。

    - 如果您是在共同管理註冊期間從 Intune 安裝用戶端，請參閱[如何準備網際網路型裝置以進行共同管理](../../../comanage/how-to-prepare-Win10.md)。

      > [!NOTE]
      > 這個方法可能有其他必要條件。 例如，將站台註冊到 Azure Active Directory，或建立已啟用內容的雲端管理閘道。

在用戶端安裝並正確地向站台註冊之後，就會啟動參考的工作順序。 如果用戶端註冊失敗，則不會啟動工作順序。



### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

如果用戶端具有錯誤的 Configuration Manager 受信任根金鑰，則無法連絡受信任管理點以接收新的受信任根金鑰。 請使用此屬性來移除舊的受信任根金鑰。 在您將用戶端從某個站台階層移至另一個站台階層時，就可能會發生這種情況。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

範例：`CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

與 [SMSSITECODE=AUTO](#smssitecode) 搭配使用時，可啟用用戶端升級的自動站台重新指派。

範例：`CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

指定用戶端電腦上用戶端快取資料夾的位置。 根據預設，此快取位置為 `%WinDir%\ccmcache`。

範例：`CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

搭配 [**SMSCACHEFLAGS**](#smscacheflags) 屬性使用此屬性來控制用戶端快取資料夾的位置。 例如，若要在最大的可用用戶端磁碟機上安裝用戶端快取資料夾：`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

使用此屬性為用戶端快取資料夾指定進一步的安裝詳細資料。 您可個別使用 **SMSCACHEFLAGS** 屬性，或以分號 (`;`) 分隔來合併使用。

如果未包含此屬性：

- 用戶端會根據 [**SMSCACHE**](#smscachedir) 屬性來安裝快取資料夾
- 不會壓縮資料夾
- 用戶端會使用 [**SMSCACHESIZE**](#smscachesize) 屬性作為快取的大小限制 (MB)

當升級現有的用戶端時，用戶端安裝程式會忽略這個屬性。

#### <a name="values-for-the-smscacheflags-property"></a>SMSCACHEFLAGS 屬性的值

- **PERCENTDISKSPACE**:以「總」磁碟空間的百分比來設定快取大小。 如果指定此屬性，請同時將 [**SMSCACHESIZE**](#smscachesize) 設定為百分比值。

- **PERCENTFREEDISKSPACE**：以「可用」磁碟空間的百分比來設定快取大小。 如果指定此屬性，請同時將 [**SMSCACHESIZE**](#smscachesize) 設定為百分比值。 例如，磁碟的可用空間為 10 MB，且指定 `SMSCACHESIZE=50`。 用戶端安裝程式會將快取大小設定為 5 MB。 此屬性無法搭配 **PERCENTDISKSPACE** 屬性使用。

- **MAXDRIVE**：在最大的可用磁碟上安裝快取。 如果使用 [**SMSCACHEDIR**](#smscachedir) 屬性指定路徑，則用戶端安裝程式會忽略這個值。

- **MAXDRIVESPACE**：在具有最多可用空間的磁碟機上安裝快取。 如果使用 [**SMSCACHEDIR**](#smscachedir) 屬性指定路徑，則用戶端安裝程式會忽略這個值。

- **NTFSONLY**：只在 NTFS 格式的磁碟機上安裝快取。 如果使用 [**SMSCACHEDIR**](#smscachedir) 屬性指定路徑，則用戶端安裝程式會忽略這個值。

- **COMPRESS**：以壓縮格式儲存快取。

- **FAILIFNOSPACE**：如果空間不足，無法安裝快取，請移除 Configuration Manager 用戶端。

範例：`CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> 用戶端設定可用於指定用戶端快取資料夾大小。 加入這些用戶端設定實際上會取代使用 SMSCACHESIZE 作為 client.msi 內容來指定用戶端快取大小。 如需詳細資訊，請參閱[快取大小的用戶端設定](about-client-settings.md#client-cache-settings)。  

當升級現有的用戶端時，用戶端安裝程式會忽略這項設定。 當用戶端下載軟體更新時，也會忽略快取大小。

範例：`CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> 如果重新安裝用戶端，則無法使用 **SMSCACHESIZE** 或 **SMSCACHEFLAGS** 將快取大小設定為比先前設定更小的值。 先前的大小是最小值。

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

使用此屬性來指定用戶端安裝程式檢查組態設定的位置和順序。 這是包含一或多個字元的字串，每一個字元都定義了特定的組態來源：

- `R`：檢查登錄中的組態設定。

  如需詳細資訊，請參閱[佈建用戶端安裝內容](deploy-clients-to-windows-computers.md#BKMK_Provision)。

- `P`：從命令列檢查安裝屬性中的組態設定。

- `M`：當升級舊版用戶端時，檢查現有的設定。

- `U`：將安裝的用戶端升級至較新版本，並使用指派的站台碼。

根據預設，用戶端安裝程式會使用 `PU`。 其會先檢查安裝屬性 (`P`)，再檢查現有的設定 (`U`)。  

範例：`CCMSetup.exe SMSCONFIGSOURCE=RP`

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

指定用戶端是否可以使用 Windows 網際網路名稱服務 (WINS) 尋找接受 HTTP 連線的管理點。 用戶端在 Active Directory 網域服務或 DNS 中找不到管理點時，會使用此方法。

此內容不會影響用戶端是否使用 WINS 進行名稱解析。

您可以為此內容設定兩個不同的模式：

- **NOWINS**：這個值是此屬性最安全的設定。 可防止用戶端在 WINS 中尋找管理點。 當您使用此設定時，用戶端必須使用替代方法來找出內部網路的管理點。 例如，Active Directory Domain Services 或 DNS 發行。

- **WINSSECURE** (預設)：在此模式中，使用 HTTP 通訊的用戶端可以使用 WINS 來尋找管理點。 不過，用戶端必須擁有受信任根金鑰的複本，才能順利與管理點連線。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

範例：`CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

指定 Configuration Manager 用戶端要使用的初始管理點。  

> [!IMPORTANT]  
> 如果管理點只接受透過 HTTPS 的用戶端連線，請在管理點名稱前面加上 `https://`。

範例：

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

如果用戶端無法從 Active Directory Domain Services 取得 Configuration Manager 受信任的根金鑰，請使用此屬性來指定金鑰。 此屬性適用於使用 HTTP 和 HTTPS 通訊的用戶端。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

範例：`CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> 從站台伺服器上的 mobileclient.tcf 檔案中，取得站台的受信任根金鑰值。 如需詳細資訊，請參閱[使用檔案以受信任的根金鑰預先佈建用戶端](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file)。

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

使用此屬性來重新安裝 Configuration Manager 受信任的根金鑰。 這會指定包含受信任根金鑰的檔案完整路徑和名稱。 此內容適用於使用 HTTP 和 HTTPS 用戶端通訊的用戶端。 如需詳細資訊，請參閱[規劃受信任的根金鑰](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

範例：`CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

指定站台伺服器上所匯出自我簽署憑證的完整路徑和名稱。 站台伺服器會將此憑證儲存在 **SMS** 憑證存放區中。 其主體名稱為**站台伺服器**，易記名稱為**站台伺服器簽署憑證**。

範例：`CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

此屬性會指定要指派用戶端的目標 Configuration Manager 站台。 這個值可以是三個字元的站台碼或單字 `AUTO`。 如果指定 `AUTO`，或未指定此屬性，則用戶端會嘗試從 Active Directory Domain Services 或從指定的管理點判斷其站台指派。 若要針對用戶端升級啟用 `AUTO`，請同時設定 [SITEREASSIGN=TRUE](#sitereassign)。

> [!NOTE]  
> 如果同時還使用 [**CCMHOSTNAME**](#ccmhostname) 屬性來指定以網際網路為基礎的管理點，請勿搭配 **SMSSITECODE** 使用 `AUTO`。 請藉由指定站台碼，以直接將用戶端指派給其站台。

範例：`CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> 憑證選擇準則的屬性值

Configuration Manager 支援下列 PKI 憑證選擇準則屬性值：

|OID 屬性|辨別名稱屬性|屬性定義|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|網域元件|  
|1.2.840.113549.1.9.1|E 或 E-mail|電子郵件地址|  
|2.5.4.3|CN|一般名稱|  
|2.5.4.4|SN|主體名稱|  
|2.5.4.5|SERIALNUMBER|序號|  
|2.5.4.6|C|國碼 (地區碼)|  
|2.5.4.7|L|位置|  
|2.5.4.8|S 或 ST|省份名稱|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|組織名稱|  
|2.5.4.11|OU|組織單位|  
|2.5.4.12|T 或 Title|標題|  
|2.5.4.42|G 或 GN 或 GivenName|指定的名稱|  
|2.5.4.43|I 或 Initials|縮寫|  
|2.5.29.17|(沒有值)|主體替代名稱|  
