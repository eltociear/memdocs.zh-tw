---
title: 使用的帳戶
titleSuffix: Configuration Manager
description: 識別及管理 Configuration Manager 中使用的 Windows 群組、帳戶和 SQL 物件。
ms.date: 05/08/2020
ms.prod: configuration-manager
ms.technology: Configuration Manager-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bd1284b96e1739126b8d6ee19f20699d47e5880
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83267976"
---
# <a name="accounts-used-in-configuration-manager"></a>Configuration Manager 中使用的帳戶

適用於：Configuration Manager (最新分支)

利用下列資訊可識別 Configuration Manager 中使用的 Windows 群組、帳戶和 SQL 物件、其使用方式，以及任何需求。  

- [Configuration Manager 建立及使用的 Windows 群組](#bkmk_groups)  
  - [Configuration Manager_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [Configuration Manager_DViewAccess](#configmgr_dviewaccess)  
  - [Configuration Manager 遠端控制使用者](#configmgr_rcusers)  
  - [SMS Admins](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_&lt;站台碼\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;站台碼\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;站台碼\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_&lt;站台碼\>](#bkmk_filerepl)  

- [Configuration Manager 使用的帳戶](#bkmk_accounts)
  - [Active Directory 群組探索帳戶](#active-directory-group-discovery-account)  
  - [Active Directory 系統探索帳戶](#active-directory-system-discovery-account)  
  - [Active Directory 使用者探索帳戶](#active-directory-user-discovery-account)  
  - [Active Directory 樹系帳戶](#active-directory-forest-account)  
  - [憑證登錄點帳戶](#certificate-registration-point-account)  
  - [擷取 OS 映像帳戶](#capture-os-image-account)  
  - [用戶端推入安裝帳戶](#client-push-installation-account)  
  - [註冊點連線帳戶](#enrollment-point-connection-account)  
  - [Exchange Server 連線帳戶](#exchange-server-connection-account)  
  - [管理點連線帳戶](#management-point-connection-account)  
  - [多點傳送連線帳戶](#multicast-connection-account)  
  - [網路存取帳戶](#network-access-account)  
  - [套件存取帳戶](#package-access-account)  
  - [Reporting Services 點帳戶](#reporting-services-point-account)  
  - [遠端工具允許的檢視者帳戶](#remote-tools-permitted-viewer-accounts)  
  - [站台安裝帳戶](#site-installation-account)
  - [站台系統安裝帳戶](#site-system-installation-account)  
  - [站台系統 Proxy 伺服器帳戶](#site-system-proxy-server-account)  
  - [SMTP 伺服器連線帳戶](#smtp-server-connection-account)  
  - [軟體更新點連線帳戶](#software-update-point-connection-account)  
  - [來源站台帳戶](#source-site-account)  
  - [來源站台資料庫帳戶](#source-site-database-account)  
  - [工作順序網域加入帳戶](#task-sequence-domain-join-account)  
  - [工作順序網路資料夾連線帳戶](#task-sequence-network-folder-connection-account)  
  - [工作順序執行身分帳戶](#task-sequence-run-as-account)  

- [Configuration Manager 在 SQL 中使用的使用者物件](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Configuration Manager 在 SQL 中使用的資料庫角色](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Configuration Manager 建立及使用的 Windows 群組  

Configuration Manager 會自動建立，而且在許多情況下，會自動維護下列 Windows 群組：  

> [!NOTE]  
> 當 Configuration Manager 在屬於網域成員的電腦上建立群組時，群組會是本機安全性群組。 如果電腦是網域控制站，群組會是網域本機群組。 此類型的群組會在網域中所有網域控制站之間共用。  


### <a name="configuration-manager_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> Configuration Manager_CollectedFilesAccess

Configuration Manager 會使用此群組來授與軟體清查所收集之檔案的檢視權限。  

如需詳細資訊，請參閱[軟體清查簡介](../../clients/manage/inventory/introduction-to-software-inventory.md)。

#### <a name="type-and-location"></a>類型和位置
此群組為主要網站伺服器上建立的本機安全性群組。

當您解除安裝站台時，此群組不會自動移除。 請在解除安裝站台之後手動將它刪除。

#### <a name="membership"></a>成員資格
Configuration Manager 會自動管理群組成員資格。 成員資格包括系統管理使用者，會授與對指派的安全性角色中 [集合]  安全物件的 [檢視收集到的檔案]  權限。

#### <a name="permissions"></a>權限
根據預設，此群組具有站台伺服器上下列資料夾的 [讀取] 權限：`C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configuration-manager_dviewaccess"></a><a name="configmgr_dviewaccess"></a>Configuration Manager_DViewAccess  

此群組是 Configuration Manager 在子主要站台的站台資料庫伺服器或資料庫複本伺服器上建立的本機安全性群組。 當您使用分散式檢視在階層中的站台之間進行資料庫複寫時，站台會建立此群組。 它包含管理中心網站的站台伺服器和 SQL Server 電腦帳戶。

如需詳細資訊，請參閱[站台間的資料傳輸](data-transfers-between-sites.md)。


### <a name="configuration-manager-remote-control-users"></a><a name="configmgr_rcusers"></a> Configuration Manager 遠端控制使用者  

Configuration Manager 遠端工具使用此群組來儲存您在 [允許的檢視者] 清單中設定的帳戶和群組。 站台會將此清單指派給每個用戶端。  

如需詳細資訊，請參閱[遠端控制簡介](../../clients/manage/remote-control/introduction-to-remote-control.md)。

#### <a name="type-and-location"></a>類型和位置
此群組是用戶端收到啟用遠端工具的原則時，在 Configuration Manager 用戶端上建立的本機安全性群組。

停用用戶端的遠端工具後，此群組不會自動移除。 請在停用遠端工具之後手動將它刪除。

#### <a name="membership"></a>成員資格
根據預設，此群組中沒有成員。 當您將使用者新增至 [允許的檢視者] 清單時，使用者會自動新增至此群組。

使用 [允許的檢視者] 清單來管理此群組的成員資格，而不要直接將使用者或群組新增至此群組。

除了作為允許的檢視者之外，系統管理使用者還必須具備**集合**物件的**遠端控制**權限。 使用 [遠端工具操作員] 安全性角色來指派此權限。  

#### <a name="permissions"></a>權限
根據預設，此群組沒有存取電腦上任何位置的權限。 它只能用來保存 [允許的檢視者] 清單。  


### <a name="sms-admins"></a>SMS Admins  

Configuration Manager 使用此群組來授與透過 WMI 存取 SMS 提供者的權限。 檢視及變更 Configuration Manager 主控台中的物件都需要存取 SMS 提供者。  

> [!NOTE]  
> 系統管理使用者之以角色為基礎的系統管理設定可決定他們在使用 Configuration Manager 主控台時可檢視和管理的物件。  

如需詳細資訊，請參閱[規劃 SMS 提供者](plan-for-the-sms-provider.md)。

#### <a name="type-and-location"></a>類型和位置
此群組是每部擁有 SMS 提供者電腦上建立的本機安全性群組。 

當您解除安裝站台時，此群組不會自動移除。 請在解除安裝站台之後手動將它刪除。

#### <a name="membership"></a>成員資格
Configuration Manager 會自動管理群組成員資格。 根據預設，階層中的每位系統管理使用者及站台伺服器電腦帳戶，都是站台中每部 SMS 提供者電腦的 **SMS Admins** 群組成員。

#### <a name="permissions"></a>權限
您可以在 [WMI 控制] MMC 嵌入式管理單元中，檢視 SMS Admins 群組的權限。 預設會將 `Root\SMS` WMI 命名空間的 [啟用帳戶] 和 [遠端啟用] 權限授與此群組。 已驗證的使用者具有 **Execute Methods**、**Provider Write** 及 **Enable Account**。

當您使用遠端 Configuration Manager 主控台時，請同時設定站台伺服器電腦和 SMS 提供者的 [遠端啟用] DCOM 權限。 將這些權限授與 **SMS Admins** 群組。 此動作會簡化系統管理，而不是直接將這些權限授與使用者或群組。 如需詳細資訊，請參閱[設定遠端 Configuration Manager 主控台的 DCOM 權限](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole)。 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;站台碼\>  
 
站台伺服器的遠端管理點使用此群組來連線到站台資料庫。 此群組提供網站伺服器和網站資料庫上 [收件匣] 資料夾的管理點存取。  

#### <a name="type-and-location"></a>類型和位置
此群組是每部擁有 SMS 提供者電腦上建立的本機安全性群組。

當您解除安裝站台時，此群組不會自動移除。 請在解除安裝站台之後手動將它刪除。

#### <a name="membership"></a>成員資格
Configuration Manager 會自動管理群組成員資格。 根據預設，成員資格包括擁有網站管理點之遠端電腦的電腦帳戶。

#### <a name="permissions"></a>權限
根據預設，此群組具有站台伺服器上下列資料夾的 [讀取]、[讀取與執行] 及 [列出資料夾內容] 權限：`C:\Program Files\Microsoft Configuration Manager\inboxes`。 對於管理點寫入用戶端資料之 [收件匣] 下方的子資料夾，此群組具有額外的 [寫入] 權限。


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;站台碼\>  
 
遠端 SMS 提供者電腦使用此群組來連線到站台伺服器。  

#### <a name="type-and-location"></a>類型和位置
此群組為網站伺服器上建立的本機安全性群組。

當您解除安裝站台時，此群組不會自動移除。 請在解除安裝站台之後手動將它刪除。

#### <a name="membership"></a>成員資格
Configuration Manager 會自動管理群組成員資格。 根據預設，成員資格包括電腦帳戶或網域使用者帳戶。 它會使用此帳戶從每個遠端 SMS 提供者連線到站台伺服器。

#### <a name="permissions"></a>權限
根據預設，此群組具有站台伺服器上下列資料夾的 [讀取]、[讀取與執行] 及 [列出資料夾內容] 權限：`C:\Program Files\Microsoft Configuration Manager\inboxes`。 此群組具有 [收件匣] 下方子資料夾的額外 [寫入] 和 [修改] 權限。 SMS 提供者需要存取這些資料夾。

此群組也具有站台伺服器上下列子資料夾的 [讀取] 權限：`C:\Program Files\Microsoft Configuration Manager\OSD\Bin`。 

它也具有 `C:\Program Files\Microsoft Configuration Manager\OSD\boot` 下方子資料夾的下列權限：
- **讀取**  
- **讀取與執行**  
- **列出資料夾內容**  
- **寫入**  
- **修改**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;站台碼\>  

Configuration Manager 遠端站台系統電腦上的檔案發送管理員元件使用此群組來連線到站台伺服器。  

#### <a name="type-and-location"></a>類型和位置
此群組為網站伺服器上建立的本機安全性群組。

當您解除安裝站台時，此群組不會自動移除。 請在解除安裝站台之後手動將它刪除。

#### <a name="membership"></a>成員資格
Configuration Manager 會自動管理群組成員資格。 根據預設，成員資格包括電腦帳戶或網域使用者帳戶。 它會使用此帳戶從執行檔案發送管理員的每個遠端站台系統連線到站台伺服器。

#### <a name="permissions"></a>權限
根據預設，此群組具有站台伺服器上下列資料夾及其子資料夾的 [讀取]、[讀取與執行] 及 [列出資料夾內容] 權限：`C:\Program Files\Microsoft Configuration Manager\inboxes`。 

此群組具有站台伺服器上下列資料夾的額外 [寫入] 和 [修改] 權限：`C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`。


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;站台碼\>  
Configuration Manager 會使用此群組在階層中的站台間啟用以檔案為基礎之複寫。 對於直接將檔案傳送到這個站台的每個遠端站台，這個群組具有設定為 [檔案複寫帳戶] 的帳戶。  

#### <a name="type-and-location"></a>類型和位置
此群組為網站伺服器上建立的本機安全性群組。

#### <a name="membership"></a>成員資格
當您安裝新站台作為另一個站台的子站台時，Configuration Manager 會自動將新站台伺服器的電腦帳戶新增至父站台伺服器上的這個群組。 Configuration Manager 還會將父站台上的電腦帳戶新增至新站台伺服器上的群組。 如果您指定另一個帳戶進行檔案為基礎的傳輸，請將該帳戶新增至目的地網站伺服器上的此群組。

當您解除安裝站台時，此群組不會自動移除。 請在解除安裝站台之後手動將它刪除。

#### <a name="permissions"></a>權限
根據預設，此群組具有下列資料夾的 [完全控制]：`C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`。



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Configuration Manager 使用的帳戶  

您可以為 Configuration Manager 設定下列帳戶。  

> [!TIP]
> 請勿針對您在 Configuration Manager 主控台中指定之帳戶的密碼使用百分比字元 (`%`)。 該帳戶將無法進行驗證。<!-- SCCMDocs#1032 -->

### <a name="active-directory-group-discovery-account"></a>Active Directory 群組探索帳戶  

站台使用 **Active Directory 群組探索帳戶**從您在 Active Directory 網域服務中指定的位置探索下列物件：
- 本機、全域和萬用安全性群組
- 這些群組內的成員資格
- 通訊群組內的成員資格
  - 通訊群組不會當作群組資源來探索

此帳戶可以是執行探索之網站伺服器的電腦帳戶，或是 Windows 使用者帳戶。 該帳戶必須具有您為探索所指定 Active Directory 位置的**讀取**權限。  

如需詳細資訊，請參閱 [Active Directory 群組探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup)。


### <a name="active-directory-system-discovery-account"></a>Active Directory 系統探索帳戶  

站台使用 **Active Directory 系統探索帳戶**，從您在 Active Directory 網域服務中指定的位置來探索電腦。  

此帳戶可以是執行探索之網站伺服器的電腦帳戶，或是 Windows 使用者帳戶。 該帳戶必須具有您為探索所指定 Active Directory 位置的**讀取**權限。  

如需詳細資訊，請參閱 [Active Directory 系統探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)。


### <a name="active-directory-user-discovery-account"></a>Active Directory 使用者探索帳戶  
 
站台使用 **Active Directory 使用者探索帳戶**，從您在 Active Directory 網域服務中指定的位置來探索使用者帳戶。  

此帳戶可以是執行探索之網站伺服器的電腦帳戶，或是 Windows 使用者帳戶。 該帳戶必須具有您為探索所指定 Active Directory 位置的**讀取**權限。  

如需詳細資訊，請參閱 [Active Directory 使用者探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)。 


### <a name="active-directory-forest-account"></a>Active Directory 樹系帳戶  

站台使用 **Active Directory 樹系帳戶**，從 Active Directory 樹系探索網路基礎結構。 管理中心網站和主要網站也會使用它將站台資料發佈至樹系的 Active Directory Domain Services。  

> [!NOTE]  
> 次要網站一律使用次要網站伺服器電腦帳戶發佈至 Active Directory。  

若要探索並發佈至不受信任的樹系，Active Directory 樹系帳戶必須是通用帳戶。 如果您未使用站台伺服器的電腦帳戶，則只能選取通用帳戶。  

此帳戶必須具有您要探索網路基礎結構所在之每個 Active Directory 樹系的 [讀取]  權限。  

此帳戶必須具有您要發佈站台資料所在的每個 Active Directory 樹系中，[系統管理] 容器及其所有子物件的 [完全控制] 權限。 如需詳細資訊，請參閱[準備 Active Directory 以發佈站台](../network/extend-the-active-directory-schema.md)。  

如需詳細資訊，請參閱 [Active Directory 樹系探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)。


### <a name="certificate-registration-point-account"></a>憑證登錄點帳戶  

憑證登錄點使用**憑證登錄點帳戶**來連線到 Configuration Manager 資料庫。 根據預設，它會使用其電腦帳戶，但您可以設定改為使用者帳戶。 當憑證登錄點位於站台伺服器的不受信任網域時，您必須指定使用者帳戶。 此帳戶僅需要網站資料庫的**讀取**權限，因為寫入操作會由狀況訊息系統處理。  

如需詳細資訊，請參閱[憑證設定檔簡介](../../../protect/deploy-use/introduction-to-certificate-profiles.md)。


### <a name="capture-os-image-account"></a>擷取 OS 映像帳戶  

當您擷取 OS 映像時，Configuration Manager 使用**擷取 OS 映像帳戶**存取您用來儲存所擷取映像的資料夾。 如果您將 [擷取 OS 映像] 步驟新增至工作順序，就需要此帳戶。  

對於您儲存所擷取映像的網路共用，此帳戶必須具有 [讀取] 和 [寫入] 權限。  

如果您在 Windows 中變更此帳戶的密碼，請以新密碼更新工作順序。 在用戶端接著下載用戶端原則時，Configuration Manager 用戶端會收到新的密碼。  

如果您需要使用此帳戶，請建立一個網域使用者帳戶。 授與它最低權限以存取必要的網路資源，並將它用於所有擷取工作順序。  

> [!IMPORTANT]  
> 請勿將互動式登入權限指派給此帳戶。  
>   
> 請勿對此帳戶使用網路存取帳戶。  

如需詳細資訊，請參閱[建立工作順序以擷取 OS](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)。


### <a name="client-push-installation-account"></a>用戶端推入安裝帳戶  

當您使用用戶端推入安裝方法來部署用戶端時，站台使用**用戶端推入安裝帳戶**來連線到電腦，並安裝 Configuration Manager 用戶端軟體。 如果您未指定此帳戶，站台伺服器會嘗試使用其電腦帳戶。  

此帳戶必須是目標用戶端電腦上本機**系統管理員**群組的成員。 此帳戶不需要 [網域系統管理員] 權限。  

您可以指定多個用戶端推入安裝帳戶。 Configuration Manager 會嘗試輪流使用每個帳戶，直到其中一個成功為止。  

> [!TIP]  
> 如果您有大型 Active Directory 環境並需要變更此帳戶，請使用下列程序以更有效率地協調此帳戶更新： 
> 1. 以不同的名稱建立新的帳戶   
> 2. 將新帳戶新增至 Configuration Manager 中的用戶端推入安裝帳戶清單  
> 3. 提供 Active Directory 網域服務足夠的時間複寫新帳戶  
> 4. 然後從 Configuration Manager 和 Active Directory 網域服務移除舊帳戶  

> [!IMPORTANT]  
> 請勿將本機登入權限授與此帳戶。  

如需詳細資訊，請參閱[用戶端推入安裝](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)。


### <a name="enrollment-point-connection-account"></a>註冊點連線帳戶  

註冊點使用**註冊點連線帳戶**來連線到 Configuration Manager 站台資料庫。 根據預設，它會使用其電腦帳戶，但您可以設定改為使用者帳戶。 當註冊點位於站台伺服器的不受信任網域時，您必須指定使用者帳戶。 此帳戶需要網站資料庫的**讀取**和**寫入**權限。  

如需詳細資訊，請參閱[為內部部署 MDM 安裝站台系統角色](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)。


### <a name="exchange-server-connection-account"></a>Exchange Server 連線帳戶  

站台伺服器使用 **Exchange Server 連線帳戶**來連線到指定的 Exchange Server。 它會使用此連線來尋找及管理連線到 Exchange Server 的行動裝置。 此帳戶需要提供給 Exchange Server 電腦必要權限的 Exchange PowerShell Cmdlet。 如需 Cmdlet 的詳細資訊，請參閱[安裝和設定 Exchange Connector](../../../mdm/deploy-use/install-configure-exchange-connector.md)。  


### <a name="management-point-connection-account"></a>管理點連線帳戶  

管理點使用**管理點連線帳戶**來連線到 Configuration Manager 站台資料庫。 它會使用此連線為用戶端傳送及擷取資訊。 根據預設，管理點會使用其電腦帳戶，但您可以設定改為使用者帳戶。 當管理點位於站台伺服器的不受信任網域時，您必須指定使用者帳戶。  

在執行 Microsoft SQL Server 的電腦上建立低權限的本機帳戶。  

> [!IMPORTANT]  
> 請勿將互動式登入權限授與此帳戶。  


### <a name="multicast-connection-account"></a>多點傳送連線帳戶  

啟用多點傳送的發佈點使用**多點傳送連線帳戶**來讀取站台資料庫的資訊。 根據預設，伺服器會使用其電腦帳戶，但您可以設定改為使用者帳戶。 當站台資料庫位於不受信任的樹系時，您必須指定使用者帳戶。 例如，如果您的資料中心在站台伺服器和站台資料庫以外樹系中擁有周邊網路，請使用此帳戶來讀取站台資料庫的多點傳送資訊。  

如果您需要此帳戶，請在執行 Microsoft SQL Server 的電腦上建立低權限的本機帳戶。  

> [!IMPORTANT]  
> 請勿將互動式登入權限授與此帳戶。  

如需詳細資訊，請參閱[使用多點傳送透過網路來部署 Windows](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。


### <a name="network-access-account"></a>網路存取帳戶  

用戶端電腦在無法使用其本機電腦帳戶來存取發佈點上的內容時，就會使用**網路存取帳戶**。 它最常套用至不受信任網域的工作群組用戶端和電腦。 當安裝 OS 的電腦尚未有網域上的電腦帳戶時，此帳戶也會在 OS 部署期間使用。  

> [!Important]  
> 網路存取帳戶絕不能作為執行程式、安裝軟體更新或執行工作順序的資訊安全內容。 它只能用來存取網路上的資源。  

Configuration Manager 用戶端會先嘗試使用其電腦帳戶來下載內容。 如果失敗，則會接著嘗試網路存取帳戶。  

如果您針對 HTTPS 或[增強 HTTP](enhanced-http.md) 設定站台，工作群組或已加入 Azure AD 的用戶端就能安全地從發佈點存取內容，而不需要網路存取帳戶。 此行為包括從開機媒體、PXE、或軟體中心執行工作順序的 OS 部署案例。<!--1358228,1358278--> 如需詳細資訊，請參閱[用戶端到管理點的通訊](communications-between-endpoints.md#bkmk_client2mp)。<!-- SCCMDocs#1345 -->

> [!Note]  
> 如果您啟用 [增強 HTTP] 以不要求網路存取帳戶，發佈點必須執行 Windows Server 2012 或更新版本。 <!--SCCMDocs-pr issue #2696-->
>  
> 請將用戶端升級為至少 1806 版，再啟用這項功能。 如果您只允許 [增強 HTTP] 連線，舊版用戶端就無法使用此方法進行驗證，因此無法從發佈點下載用戶端升級套件。 <!--vso2841213-->   

#### <a name="permissions"></a>權限

請授與此帳戶用戶端存取軟體所需之內容的最低適當權限。 此帳戶必須在發佈點上具有 [從網路存取這台電腦]  權限。 每個站台最多可設定 10 個網路存取帳戶。  

請在提供必要的資源存取權限的任何網域中建立此帳戶。 網路存取帳戶一律必須包含網域名稱。 此帳戶不支援傳遞安全性。 如果您在多個網域中擁有發佈點，請在受信任網域中建立此帳戶。  

> [!TIP]  
> 為避免帳戶鎖定，請勿變更現有網路存取帳戶的密碼。 您可改為建立新帳戶，並且在 Configuration Manager 中設定新帳戶。 經過一段時間所有用戶端都已收到新帳戶的詳細資料後，從網路共用資料夾移除舊帳戶，並刪除該帳戶。  

> [!IMPORTANT]  
> 請勿將互動式登入權限授與此帳戶。  
>   
> 請勿授與此帳戶將電腦加入網域的權限。 如果您必須在工作順序期間將電腦加入網域，請使用[工作順序網域加入帳戶](#task-sequence-domain-join-account)。  

#### <a name="configure-the-network-access-account"></a>設定網路存取帳戶  

1.  在 Configuration Manager 主控台中，移至 [系統管理] 工作區，展開 [站台設定]，然後選取 [站台] 節點。 然後選取站台。  

2.  在功能區的 [設定] 群組中，選取 [設定站台元件]，然後選擇 [軟體發佈]。  

3.  選擇 [網路存取帳戶] 索引標籤。設定一或多個帳戶，然後選擇 [確定]。  


### <a name="package-access-account"></a>套件存取帳戶  

**套件存取帳戶**可讓您設定 NTFS 權限，指定可以存取發佈點上套件內容的使用者和使用者群組。 根據預設，Configuration Manager 只會將存取權授與一般的**使用者**與**系統管理員**存取帳戶。 您可以使用其他 Windows 帳戶或群組，控制用戶端電腦的存取。 行動裝置一律會匿名擷取套件內容，因此不會使用套件存取帳戶。  

根據預設，當 Configuration Manager 將內容檔案複製到發佈點時，會將**讀取**權限授與本機**使用者**群組，並將**完全控制**授與本機 **Administrator** 群組。 實際需要的權限則依套件而定。 如果有用戶端位於工作群組或不受信任的樹系中，這些用戶端會使用網路存取帳戶來存取套件內容。 請使用預設套件存取帳戶來確保網路存取帳戶有權限存取套件。  

使用網域中可存取發佈點的帳戶。 如果您在建立套件後建立或修改帳戶，則必須重新發佈套件。 更新套件並不會變更套件上的 NTFS 權限。  

您不需要將網路存取帳戶新增為套件存取帳戶，因為**使用者**群組的成員資格會自動新增該帳戶。 將套件存取帳戶限制為只有網路存取帳戶不會阻止用戶端存取套件。  

#### <a name="manage-package-access-accounts"></a>管理套件存取帳戶  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫]。  

2.  在 [軟體程式庫] 工作區中，決定您想要管理其存取帳戶的內容類型，然後遵循提供的步驟進行：  

    - **應用程式**：展開 [應用程式管理]，選擇 [應用程式]，然後選取要管理其存取帳戶的應用程式。  

    - **套件**：展開 [應用程式管理]，選擇 [套件]，然後選取要管理其存取帳戶的套件。  

    - **軟體更新部署套件**：展開 [軟體更新]，選擇 [部署套件]，然後選取要管理其存取帳戶的部署套件。  

    - **驅動程式套件**：展開 [作業系統]，選擇 [驅動程式套件]，然後選取要管理其存取帳戶的驅動程式套件。  

    - **OS 映像**：展開 [作業系統]，選擇 [作業系統映像]，然後選取要管理其存取帳戶的作業系統映像。  

    - **OS 升級套件**：展開 [作業系統]，選擇 [作業系統升級套件]，然後選取要管理其存取帳戶的 OS 升級套件。  

    - **開機映像**：展開 [作業系統]，選擇 [開機映像]，然後選取要管理其存取帳戶的開機映像。  

3.  在選取的物件上按一下滑鼠右鍵，然後選擇 [管理存取帳戶]。  

4.  在 [新增帳戶]  對話方塊中，指定將被授與存取內容權限的帳戶，然後指定與帳戶關聯的存取權限。  

    > [!NOTE]  
    > 當您新增帳戶的使用者名稱，且 Configuration Manager 同時找到使用該名稱的本機使用者帳戶與網域使用者帳戶時，Configuration Manager 會為網域使用者帳戶設定存取權限。  


### <a name="reporting-services-point-account"></a>Reporting Services 點帳戶  
 
SQL Server Reporting Services 使用 **Reporting Services 點帳戶**，從站台資料庫擷取 Configuration Manager 報告的資料。 您指定的 Windows 使用者帳戶和密碼皆經過加密，並且儲存在 SQL Server Reporting Services 資料庫中。  

> [!NOTE]  
> 您所指定帳戶在裝載 SQL Reporting Services 資料庫的電腦上，必須具有 [本機登入] 權限。

> [!NOTE]  
> 當帳戶新增到 Configuration Manager 資料庫上的 smsschm_users SQL Database 角色之後，會自動獲授所有必要權限。

如需詳細資訊，請參閱[報告簡介](../../servers/manage/introduction-to-reporting.md)。


### <a name="remote-tools-permitted-viewer-accounts"></a>遠端工具允許的檢視者帳戶  

指定進行遠端控制的 [獲准檢視器]  是一份使用者清單，這些使用者均獲准使用用戶端上的遠端工具功能。  

如需詳細資訊，請參閱[遠端控制簡介](../../clients/manage/remote-control/introduction-to-remote-control.md)。


### <a name="site-installation-account"></a>站台安裝帳戶
<!--SCCMDocs issue #572-->
使用網域使用者帳戶來登入伺服器，以執行 Configuration Manager 安裝程式並安裝新站台。

此帳戶需要下列權限：  

- 下列伺服器上的**系統管理員**：
    - 站台伺服器  
    - 裝載站台資料庫的每部伺服器  
    - 適用於該站台的每個 SMS 提供者執行個體  

- 在裝載站台資料庫之 SQL Server 執行個體上的 **Sysadmin**  

Configuration Manager 安裝程式會自動將此帳戶新增至 [SMS Admins](#sms-admins) 群組。

安裝後，此帳戶會是唯一具有 Configuration Manager 主控台權限的使用者。 如果您需要移除此帳戶，請務必先將其權限新增至其他使用者。

展開獨立站台以包含管理中心網站時，此帳戶需要獨立主要站台的**系統高權限管理員**或**基礎結構系統管理員**角色型系統管理權限。


### <a name="site-system-installation-account"></a>站台系統安裝帳戶  

站台伺服器使用**站台系統安裝帳戶**來安裝、重新安裝、解除安裝和設定站台系統。 如果設定站台系統要求站台伺服器起始與此站台系統之間的連線，則安裝站台系統和任何角色後，Configuration Manager 也會使用此帳戶從站台系統系統提取資料。 每個站台系統可以有不同的安裝帳戶，但您只能設定一個安裝帳戶來管理該站台系統上的所有角色。  

此帳戶需要目標站台系統的本機系統管理權限。 此外，此帳戶必須在安全性原則中具有目標站台系統的 [從網路存取這部電腦] 權限。  

> [!TIP]  
> 如果您有許多網域控制站，且會跨網域使用這些帳戶，請在設定站台系統之前，檢查 Active Directory 是否已複寫這些帳戶。  
>   
> 在每個受控的站台系統指定本機帳戶時，這種設定比使用網域帳戶更安全。 它能夠有效降低攻擊者入侵帳戶時所造成的損失。 儘管如此，網域帳戶還是較容易管理。 請考慮安全性與系統管理效益之間的取捨。  


### <a name="site-system-proxy-server-account"></a>站台系統 Proxy 伺服器帳戶
<!--SCCMDocs issue #648-->
下列站台系統角色使用**站台系統 Proxy 伺服器帳戶**，透過要求驗證存取的 Proxy 伺服器或防火牆來存取網際網路：

- Asset Intelligence 同步處理點
- Exchange Server 連接器
- 服務連接點
- 軟體更新點

> [!IMPORTANT]  
> 為所需的 Proxy 伺服器或防火牆指定具備最低可能權限的帳戶。  

如需詳細資訊，請參閱 [Proxy 伺服器支援](../network/proxy-server-support.md)。


### <a name="smtp-server-connection-account"></a>SMTP 伺服器連線帳戶  

當 SMTP 伺服器需要驗證存取時，站台伺服器使用 **SMTP 伺服器連線帳戶**來傳送電子郵件警示。  

> [!IMPORTANT]  
> 指定具備最低可能權限的帳戶來寄送電子郵件。  

如需詳細資訊，請參閱[使用警示和狀態系統](../../servers/manage/use-alerts-and-the-status-system.md)。


### <a name="software-update-point-connection-account"></a>軟體更新點連線帳戶  

站台伺服器使用**軟體更新點連線帳戶**進行下列兩種軟體更新服務：  

- Windows Server Update Services (WSUS) 會設定產品定義、分類及上游設定之類的設定值。  

- WSUS Synchronization Manager，會要求與上游 WSUS 伺服器或 Microsoft Update 同步處理。  

[站台系統安裝帳戶](#site-system-installation-account)可以安裝軟體更新元件，但無法在軟體更新點上執行軟體更新專屬功能。 如果因為軟體更新點位於不受信任的樹系中而無法以站台伺服器電腦帳戶使用此功能，則除了站台系統安裝帳戶外，還必須指定這個帳戶。  

此帳戶必須是您安裝 WSUS 之電腦上的本機系統管理員。 它也必須是本機 **WSUS 系統管理員**群組的成員。  

如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。


### <a name="source-site-account"></a>來源站台帳戶  

移轉程序使用**來源站台帳戶**來存取來源站台的 SMS 提供者。 此帳戶需要 [讀取]  權限以讀取來源網站中的網站物件，才能收集移轉作業所需的資料。  

如果您有 Configuration Manager 2007 發佈點或具有共置發佈點的次要站台，當您將其升級為 Configuration Manager (最新分支) 發佈點時，此帳戶也必須具有 [站台] 類別的 [刪除] 權限。 此權限可在升級期間成功從 Configuration Manager 2007 站台移除發佈點。  

> [!NOTE]  
> 來源站台帳戶與[來源站台資料庫帳戶](#source-site-database-account)均識別為**移轉管理員**，其位於 Configuration Manager 主控台 [管理] 工作區的 [帳戶] 節點中。  

如需詳細資訊，請參閱[在階層間移轉資料](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies)。


### <a name="source-site-database-account"></a>來源站台資料庫帳戶  

移轉程序使用**來源站台資料庫帳戶**存取來源站台的 SQL Server 資料庫。 若要從來源站台的 SQL Server 資料庫收集資料，來源站台資料庫帳戶必須具有來源站台 SQL Server 資料庫的 [讀取] 和 [執行] 權限。  

如果使用 Configuration Manager (最新分支) 電腦帳戶，請確定此帳戶的下列條件皆成立：  
  
- 在與 Configuration Manager 2007 站台相同的網域中為 **Distributed COM Users** 安全性群組的成員  
- 其為 **SMS Admins** 安全性群組的成員  
- 它具有所有 Configuration Manager 2007 物件的 [讀取] 權限  

> [!NOTE]  
> 來源站台帳戶與[來源站台資料庫帳戶](#source-site-database-account)均識別為**移轉管理員**，其位於 Configuration Manager 主控台 [管理] 工作區的 [帳戶] 節點中。  

如需詳細資訊，請參閱[在階層間移轉資料](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies)。


### <a name="task-sequence-domain-join-account"></a>工作順序網域加入帳戶 

Windows 安裝程式使用**工作順序網域加入帳戶**，將新製作映像的電腦加入網域。 您需要此帳戶，才能進行[加入網域或工作群組](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)工作順序步驟，並選取 [加入網域] 選項。 您也可以透過[套用網路設定](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings)步驟設定此帳戶，但並非必要條件。  

此帳戶需要目標網域的 [網域加入] 權限。  

> [!TIP]  
> 建立一個具備最低權限的網域使用者帳戶以加入網域，並將它用於所有工作順序。  

> [!IMPORTANT]  
> 請勿將互動式登入權限指派給此帳戶。  
>   
> 請勿對此帳戶使用網路存取帳戶。  


### <a name="task-sequence-network-folder-connection-account"></a>工作順序網路資料夾連線帳戶  

工作順序引擎會使用**工作順序網路資料夾連線帳戶**來連線到網路上的共用資料夾。 您需要此帳戶，才能進行[連線至網路資料夾](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)工作順序步驟。  

此帳戶須有指定之共用資料夾的存取權限。 它必須是網域使用者帳戶。  

> [!TIP]  
> 建立一個具備最低權限的網域使用者帳戶以存取必要的網路資源，並將它用於所有工作順序。  

> [!IMPORTANT]  
> 請勿將互動式登入權限指派給此帳戶。  
>   
> 請勿對此帳戶使用網路存取帳戶。  


### <a name="task-sequence-run-as-account"></a>工作順序執行身分帳戶  

工作順序引擎使用**工作順序執行身分帳戶**，透過本機系統帳戶以外的認證來執行命令列或 PowerShell 指令碼。 您需要此帳戶，才能進行[執行命令列](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)及[執行 PowerShell 指令碼](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)工作順序步驟，並選取 [以下列帳戶的身分執行此步驟] 選項。  

設定具有所需最低權限的帳戶，以便執行您在工作順序中指定的命令列。 此帳戶需要互動式登入權限。 它通常需要能夠安裝軟體及存取網路資源。 針對執行 PowerShell 指令碼工作，此帳戶需要本機系統管理員權限。 

> [!IMPORTANT]  
> 請勿對此帳戶使用網路存取帳戶。  
>   
> 永不使帳戶成為網域系統管理員。  
>   
> 永不設定此帳戶的漫遊設定檔。 當工作順序執行時，它會下載帳戶的漫遊設定檔。 這會導致在本機電腦上存取該設定檔變成很容易的事。  
>   
> 限制帳戶的範圍。 例如，為每一個工作順序建立不同的工作順序執行身分帳戶。 之後如果一個帳戶遭到洩露，則只有該帳戶可存取的用戶端電腦會遭到洩露。  
>   
> 如果命令列需要電腦的系統管理存取權限，請考慮在所有執行該工作順序的電腦上建立單獨作為此帳戶的本機系統管理員帳戶。 一旦您不再需要此帳戶，請將它刪除。  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Configuration Manager 在 SQL 中使用的使用者物件 
<!--SCCMDocs issue #1160-->
Configuration Manager 會自動建立和維護 SQL 中的下列使用者物件。  這些物件位在 Configuration Manager 資料庫內的 [安全性]/[使用者] 下。  

> [!IMPORTANT]  
>  修改或移除這些物件，可能會在 Configuration Manager 環境中造成重大問題。  我們建議您不要對這些物件進行任何變更。


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

此物件是用來在唯讀內容下執行查詢。  數個預存程序會利用此物件。


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

此物件是用來提供動態 SQL 陳述式的權限。


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

此物件是用來執行 SQL Reporting 執行。  下列預存程序與此函式搭配使用：spSRExecQuery。


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Configuration Manager 在 SQL 中使用的資料庫角色
<!--SCCMDocs issue #1160-->
Configuration Manager 會自動建立和維護 SQL 中的下列角色物件。 這些角色提供對特定預存程序、資料表、檢視與函式的存取權，來執行每個角色所需的動作，以便從 Configuration Manager 資料庫擷取資料或將資料插入到其中。 這些物件位在 Configuration Manager 資料庫內的 [安全性]/[使用者]/[資料庫角色] 下。

> [!IMPORTANT]  
> 修改或移除這些物件，可能會在 Configuration Manager 環境中造成重大問題。 請勿變更這些物件。 下列清單僅供參考。

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Asset Intelligence 大量授權匯入。 Configuration Manager 會根據 RBA 存取權將此權限授與使用者帳戶，以便能夠匯入與 Asset Intelligence 搭配使用的大量授權。  此帳戶可由系統高權限管理員或資產管理員角色新增。

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Asset Intelligence 更新同步處理。 Configuration Manager 會將存取權授與裝載 Asset Intelligence 同步處理點帳戶的電腦帳戶，以取得 Asset Intelligence Proxy 資料並檢視擱置中的待上傳 AI 資料。

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

頻外管理。 此角色是由 Configuration Manager AMT 角色使用以擷取支援 Intel AMT 之裝置上的資料。

> [!NOTE]  
> 此角色在較新版本的 Configuration Manager 中已過時。

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

支援簡單憑證註冊通訊協定 (SCEP) 的憑證登錄點。 Configuration Manager 會將權限授與支援憑證登錄點 (以提供 SCEP 支援) 的站台系統電腦帳戶，以進行憑證簽署及更新。

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

憑證登錄點 PFX 支援。 Configuration Manager 會將權限授與支援針對 PFX 支援所設定之憑證登錄點的站台系統電腦帳戶，以進行簽署及更新。

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

裝置管理點。 Configuration Manager 會將此權限授與具有 [允許行動裝置和 Mac 電腦使用此管理點] 選項之管理點的電腦帳戶，以便能夠支援已向 MDM 註冊的裝置。

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

服務連接點。 Configuration Manager 會將此權限授與裝載服務連接點的電腦帳戶，以擷取並提供遙測資料、管理雲端服務及擷取服務更新。

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

分散式檢視。 當在複寫連結屬性中選取 SQL Server 分散式檢視選項時，Configuration Manager 會將此權限授與 CAS 上主要站台伺服器的電腦帳戶。

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

資料倉儲。 Configuration Manager 會將此權限授與裝載資料倉儲角色的電腦帳戶。

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 註冊點。 Configuration Manager 會將此權限授與裝載註冊點的電腦帳戶，以允許透過 MDM 進行裝置註冊。

### <a name="smsdbrole_extract"></a>smsdbrole_extract

提供對所有延伸結構描述檢視的存取權。

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

階層管理員服務。 Configuration Manager 會將權限授與此帳戶，以管理階層中站台之間的容錯移轉狀態訊息與 SQL Server Broker 交易。

> [!NOTE]  
> smdbrole_WebPortal 角色預設是此角色的成員。

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

多點傳送服務。 Configuration Manager 會將此權限授與支援多點傳送之發佈點的電腦帳戶。

### <a name="smsdbrole_mp"></a>smsdbrole_MP

管理點。 Configuration Manager 會將此權限授與裝載管理點角色的電腦帳戶，以支援 Configuration Manager 用戶端。

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

管理點 Microsoft BitLocker 系統管理與監視。 Configuration Manager 會將此權限授與裝載管理點的電腦帳戶，該管理點可管理環境適用的 MBAM。

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

管理點應用程式要求。 Configuration Manager 會將此權限授與裝載管理點的電腦帳戶，以支援使用者型應用程式要求。

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

SMS 提供者。 Configuration Manager 會將此權限授與裝載 SMS 提供者角色的電腦帳戶。  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

站台伺服器。 Configuration Manager 會將此權限授與裝載主要或 CAS 站台的電腦帳戶。

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

軟體更新點。 Configuration Manager 會將此權限授與裝載軟體更新點的電腦帳戶，以處理第三方更新。

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

應用程式類別目錄網站點。 Configuration Manager 會將此權限授與裝載應用程式類別目錄 Web 服務點的電腦帳戶，以提供使用者型應用程式部署。

### <a name="smsschm_users"></a>smsschm_users

使用者報告存取權。 Configuration Manager 會將存取權授與用於 Reporting Services 點的帳戶，以允許存取 SMS 報告檢視來顯示 Configuration Manager 報告資料。  會進一步使用 RBA 來限制資料。

## <a name="elevated-permissions"></a>提升的權限

<!-- SCCMDocs#405 -->

Configuration Manager 要求某些帳戶需具備提升的權限，才能執行進行中的作業。 例如，請參閱[安裝主要站台的必要條件](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri)。 下列清單摘要說明這些權限與需要這些權限的原因。

- 主要站台伺服器與管理中心網站伺服器的電腦帳戶需要：

  - 所有站台伺服器上的本機系統管理員權限。 此權限可用來管理、安裝及移除系統服務。 當您新增或移除角色時，站台伺服器也會更新站台系統上的本機群組。

  - 可存取站台資料庫之 SQL 執行個體的系統管理員權限。 此權限可設定及管理站台的 SQL。 Configuration Manager 會與 SQL 緊密整合，而不只是資料庫。

- 具有系統高權限管理員角色的使用者帳戶需要：

  - 站台伺服器上的本機系統管理員權限。 此權限可檢視、編輯、移除及安裝系統服務、登錄機碼與值，以及 WMI 物件。

  - 可存取站台資料庫之 SQL 執行個體的系統管理員權限。 此權限可在安裝或復原期間安裝及更新資料庫。 SQL 維護和作業也需要用到此權限。 例如，重建索引及更新統計資料。

    > [!NOTE]
    > 有些組織可能選擇移除系統管理員存取權，並且只在需要時才授與。 這種行為有時稱為「Just-In-Time (JIT) 存取」。 在此情況下，具有系統高權限管理員角色的使用者仍然有權在 Configuration Manager 資料庫上讀取、更新及執行預存程序。 這些權限讓這類使用者能夠對大部分問題進行疑難排解，而不需完整的系統管理員存取權。
