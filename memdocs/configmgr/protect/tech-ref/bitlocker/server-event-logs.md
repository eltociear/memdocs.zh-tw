---
title: 伺服器事件記錄檔
titleSuffix: Configuration Manager
description: Windows 事件記錄檔中可能之 BitLocker (MBAM) 伺服器項目的技術參考
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d49a24b6fea08f12d1fe70c1e0b7415adf98719
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074804"
---
# <a name="server-event-logs"></a>伺服器事件記錄檔

適用於：  Configuration Manager (最新分支)

<!--3601034-->

使用「Windows 事件檢視器」來檢視 Configuration Manager 中下列 BitLocker 管理伺服器元件的事件記錄檔：

- 管理點上的復原服務
- 自助入口網站
- 管理和監視網站

在裝載一或多個這些元件的伺服器上，開啟 [事件檢視器]。 接著移至 [應用程式及服務記錄檔]  、[Microsoft]  、[Windows]  ，然後展開 [MBAM-Web]  。 預設有 [系統管理](#admin) 和 [可操作](#operational) 事件記錄檔。

下列各節包含 BitLocker 管理伺服器元件可能發生之事件識別碼的訊息和疑難排解資訊。

## <a name="admin"></a>系統管理員

### <a name="1-webappspnerror"></a>1：WebAppSpnError

應用程式：{SiteName}{VirtualDirectory} 遺漏下列服務主體名稱 (SPN):{ListOfSpns}。請在下列帳戶上註冊所需的 SPN：{ExecutionAccount}。

若要讓整合式「Windows 驗證」成功，必須備妥必要的 SPN。 此訊息表示未正確設定應用程式所需的 SPN。 此事件中包含的詳細資料應該會提供更多資訊。

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100：AdminServiceRecoveryDbError

可能的錯誤訊息：

- GetMachineUsers：從資料庫取得使用者資訊時發生錯誤。
- GetRecoveryKey：從資料庫取得修復金鑰時發生錯誤。
- GetRecoveryKey：從資料庫取得使用者資訊時發生錯誤。
- GetRecoveryKeyIds：從資料庫取得修復金鑰識別碼時發生錯誤。
- GetTpmHashForUser：從復原資料庫取得 TPM 雜湊資料時發生錯誤。
- GetTpmHashForUser：從復原資料庫取得 TPM 雜湊資料時發生錯誤。
- QueryDriveRecoveryData：從資料庫取得磁碟機復原資料時發生錯誤。
- QueryRecoveryKeyIdsForUser：從資料庫取得修復金鑰識別碼時發生錯誤。
- QueryVolumeUsers：從資料庫取得使用者資訊時發生錯誤。

每當與復原資料庫進行通訊時，只要發生例外狀況，就會記錄此訊息。 請仔細閱讀追蹤中所包含的資訊，以取得例外狀況的相關具體詳細資料。

### <a name="101-adminservicecompliancedberror"></a>101：AdminServiceComplianceDbError

可能的錯誤訊息：

- GetRecoveryKey：將稽核事件記錄至合規性資料庫時發生錯誤。
- GetRecoveryKeyIds：將稽核事件記錄至合規性資料庫時發生錯誤。
- GetTpmHashForUser：將稽核事件記錄至合規性資料庫時發生錯誤。
- QueryRecoveryKeyIdsForUser：將稽核事件記錄至合規性資料庫時發生錯誤。
- QueryDriveRecoveryData：將稽核事件記錄至合規性資料庫時發生錯誤。

每當與合規性資料庫進行通訊時，只要發生例外狀況，就會記錄此訊息。 請仔細閱讀追蹤中所包含的資訊，以取得例外狀況的相關具體詳細資料。

### <a name="102-agentservicerecoverydberror"></a>102：AgentServiceRecoveryDbError

此訊息表示服務嘗試與復原資料庫進行通訊時發生例外狀況。 請仔細閱讀事件中所包含的訊息，以取得例外狀況的相關具體資訊。

請確認 MBAM 應用程式集區帳戶具有連線到復原資料庫所需的權限。

### <a name="103-agentserviceerror"></a>103：AgentServiceError

可能的錯誤訊息：

- 無法偵測用戶端電腦帳戶或資料移轉使用者帳戶。

    每當對 `PostKeyRecoveryInfo`、`IsRecoveryKeyResetRequired`、`CommitRecoveryKeyRest` 或 `GetTpmHash` Web 方法進行呼叫時，它都會擷取呼叫端內容以取得呼叫端認證。 如果呼叫端內容為 Null 或空白，服務就會記錄此訊息。

- 呼叫端身分識別的帳戶驗證失敗。

    如果 Web 方法預期呼叫端是電腦帳戶，但卻不是，就會記錄此訊息。 如果 Web 方法預期呼叫端是使用者帳戶，但卻不是使用者帳戶或資料移轉群組帳戶的成員，也可能造成此問題。

### <a name="104-statusservicecompliancedbconfigerror"></a>104：StatusServiceComplianceDbConfigError

登錄中的合規性資料庫連接字串空白。

每當合規性資料庫連接字串無效，就會記錄此訊息。 請確認在登錄機碼 `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` 的值。

### <a name="105-statusservicecompliancedberror"></a>105：StatusServiceComplianceDbError

此錯誤表示網站或 Web 服務無法連線到合規性資料庫。 請確認 IIS 應用程式集區帳戶可以連線到資料庫。

### <a name="106-helpdeskerror"></a>106：HelpdeskError

已知的錯誤和可能的原因：

- 對 URL 的要求導致內部錯誤。

    在管理和監視網站 (服務台) 的應用程式中發生未處理的例外狀況。 請檢閱 [系統管理]  事件記錄檔中的記錄項目，以找出具體的例外狀況。

- 取得執行內容資訊時發生錯誤。 無法確認「服務主體名稱」(SPN) 註冊。

    在初始服務台網站載入作業期間，它會檢查 SPN。 若要確認 SPN，它需要與服務台網站對應的帳戶資訊、IIS Sitename 及 ApplicationVirtualPath。 當這些屬性中有一或多個屬性無效或遺失時，就會記錄此錯誤訊息。

- 確認「服務主體名稱」(SPN) 註冊時發生錯誤。

    此訊息表示在確認 SPN 時，系統擲回安全性例外狀況。 請參考事件詳細資料中所包含的例外狀況。

### <a name="107-selfserviceportalerror"></a>107：SelfServicePortalError

已知的錯誤和可能的原因：

- 取得使用者的修復金鑰時發生錯誤

    表示在提出要求以擷取修復金鑰時，系統擲回未預期的例外狀況。 請參考事件詳細資料中的例外狀況訊息。 如果已在服務台應用程式上啟用追蹤，請參考追蹤資料以取得詳細的例外狀況訊息。

- 取得執行內容資訊時發生錯誤。 無法確認「服務主體名稱」(SPN) 註冊

    在初始載入作業期間，自助入口網站會擷取自助網站的帳戶資訊、IIS Sitename 及 ApplicationVirtualPath 來確認 SPN。 當這些屬性中有一或多個屬性無效時，就會記錄此錯誤訊息。

- 確認「服務主體名稱」(SPN) 註冊時發生錯誤。 EventDetails：{ExceptionMessage}

    此訊息表示在確認 SPN 時，系統擲回安全性例外狀況。 請參考事件詳細資料中所包含的例外狀況。

### <a name="108-domaincontrollererror"></a>108：DomainControllerError

已知的錯誤和可能的原因：

- 解析網域名稱 {DomainName} 時發生錯誤，發生記憶體配置失敗。

    為了解析網域名稱，它會呼叫 `DsGetDcName` Windows API。 當此 API 傳回 `ERROR_NOT_ENOUGH_MEMORY` (表示記憶體配置失敗) 時，就會記錄此訊息。

- 無法叫用 DsGetDcName 方法

    此訊息表示 `DsGetDcName` API 在主機上無法使用。

### <a name="109-webapprecoverydberror"></a>109：WebAppRecoveryDbError

已知的錯誤和可能的原因：

- 讀取復原資料庫的組態時發生錯誤。 未設定復原資料庫的連接字串。

    此訊息表示 `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` 的復原資料庫連接字串資訊無效。 請確認指定的登錄機碼值。

如果您看到下列任何訊息，請確認來自 IIS 伺服器的應用程式集區認證是否可以連線到復原資料庫：

- DoesUserHaveMatchingRecoveryKey：取得使用者的修復金鑰識別碼時發生錯誤。
- QueryDriveRecoveryData：取得磁碟機復原資料時發生錯誤。
- QueryRecoveryKeyIdsForUser：取得使用者的修復金鑰識別碼時發生錯誤。
- 從復原資料庫取得 TPM 密碼雜湊時發生錯誤。

### <a name="110-webappcompliancedberror"></a>110：WebAppComplianceDbError

已知的錯誤和可能的原因：

- 讀取合規性資料庫的組態時發生錯誤。 未設定合規性資料庫的連接字串。

    此訊息表示 `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` 的合規性資料庫連接字串資訊無效。 請確認此登錄機碼的值。

如果您看到下列任何訊息，請確認來自 IIS 伺服器的應用程式集區認證是否可以連線到合規性資料庫：

- GetRecoveryKeyForCurrentUser：將稽核事件記錄至合規性資料庫時發生錯誤。
- QueryRecoveryKeyIdsForUser：將稽核事件記錄至合規性資料庫時發生錯誤。
- QueryRecoveryKeyIdsForUser：將稽核事件記錄至合規性資料庫時發生錯誤。

### <a name="111-webappdberror"></a>111：WebAppDbError

這些錯誤表示下列兩種情況其中之一

- MBAM 網站/Web 服務無法連線到合規性資料庫或復原資料庫
- MBAM 網站/Web 服務執行帳戶 (應用程式集區帳戶) 無法在合規性資料庫或復原資料庫上執行 `GetVersion` 預存程序

事件中所包含的訊息會提供有關例外狀況的更多詳細資料。

請確認應用程式集區帳戶可以連線到合規性資料庫或復原資料庫。 確認它具有執行 `GetVersion` 預存程序的權限。

### <a name="112-webapperror"></a>112：WebAppError

確認「服務主體名稱」(SPN) 註冊時發生錯誤。

為了確認 SPN，它會查詢 Active Directory 以擷取 SPN 對應執行帳戶清單。 它也會查詢 `ApplicationHost.config` 以取得網站繫結。 此錯誤訊息表示它無法與 Active Directory 進行通訊，或無法載入 `ApplicationHost.config` 檔案。

請確認應用程式集區帳戶具有查詢 Active Directory 或 `ApplicationHost.config` 檔案的權限。 亦請確認 `ApplicationHost.config` 檔案中的網站繫結項目。

## <a name="operational"></a>作業

### <a name="4-performancecountererror"></a>4：PerformanceCounterError

擷取效能計數器時發生錯誤。

此追蹤訊息包含實際的例外狀況訊息，以下列出其中部分訊息：

- ArgumentNullException：如果所要求效能計數器的類別、計數器或執行個體無效，就會擲回此例外狀況。
- System.InvalidOperationException：categoryName 是空字串 ("")。 counterName 是空字串 ("")。
- 要求的讀取/寫入權限設定對此計數器而言無效。
- 指定的類別不存在 (如果 readOnly 為 true)。
- 指定的類別不是 .NET Framework 的自訂類別 (如果 readOnly 為 false)。
- 指定的類別已標示為多重執行個體，且要求使用執行個體名稱來建立效能計數器。
- instanceName 的長度超過 127 個字元。
- categoryName 與 counterName 已當地語系化成不同語言。
- System.ComponentModel.Win32Exception：存取系統 API 時發生錯誤。
- System.UnauthorizedAccessException:在沒有系統管理權限情況下執行的程式碼嘗試讀取效能計數器。

事件中的訊息會提供有關例外狀況的更多詳細資料。

針對 `System.UnauthorizedAccessException`，請確認應用程式集區帳戶能夠存取效能計數器 API。

### <a name="200-helpdeskinformation"></a>200：HelpDeskInformation

管理網站應用程式已順利找到並連線到支援的復原/合規性資料庫版本。

表示從服務台網站順利連線到復原或合規性資料庫。

### <a name="201-selfserviceportalinformation"></a>201：SelfServicePortalInformation

自助入口網站應用程式已順利找到並連線到支援的復原/合規性資料庫版本。

表示從自助入口網站順利連線到復原或合規性資料庫。

### <a name="202-webappinformation"></a>202：WebAppInformation

應用程式已正確註冊其 SPN。

表示服務台網站所需的 SPN 已針對執行帳戶正確註冊。

## <a name="see-also"></a>請參閱

如需有關使用這些記錄檔的詳細資訊，請參閱 [BitLocker 事件記錄檔](about-event-logs.md)。

如需詳細的疑難排解資訊，請參閱[針對 BitLocker 進行疑難排解](troubleshoot.md)。

如需有關安裝這些網站的詳細資訊，請參閱[設定 BitLocker 報表和入口網站](../../deploy-use/bitlocker/setup-websites.md)。
