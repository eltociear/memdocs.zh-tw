---
title: 加密復原資料
titleSuffix: Configuration Manager
description: 在網路和 Configuration Manager 資料庫中，加密 BitLocker 修復金鑰、修復套件和 TPM 密碼雜湊。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709346"
---
# <a name="encrypt-recovery-data"></a>加密復原資料

適用於：  Configuration Manager (最新分支)

<!--3601034-->

當建立 BitLocker 管理原則時，Configuration Manager 會將復原服務部署到管理點。 在 BitLocker 管理原則的 [用戶端管理]  頁面上，當您 [設定 BitLocker 管理服務]  時，用戶端會將金鑰修復資訊備份至網站資料庫。 這項資訊包含 BitLocker 修復金鑰、復原套件和 TPM 密碼雜湊。 當使用者被鎖在受保護的裝置外時，您可以使用這項資訊來協助使用者復原裝置的存取權。

基於這項資訊的敏感性特質，您必須在下列情況下加以保護：

- Configuration Manager 需要用戶端與復原服務之間的 HTTPS 連線，才能加密網路中傳輸的資料。 有兩個選項：

  - 針對在管理點上裝載復原服務的 IIS 網站啟用 HTTPS，而不是整個管理點角色。 此選項僅適用於 Configuration Manager 2002 版。<!-- 5925660 -->

  - 設定 HTTPS 的管理點。 在管理點的屬性上，[用戶端連線]  設定必須是 [HTTPS]  。 此選項適用於 Configuration Manager 1910 或 2002 版。

    > [!NOTE]
    > 目前不支援增強 HTTP。

- 將此資料儲存在站台資料庫時，也請考慮將其加密。 您可使用 SQL Server 儲存格層級加密來搭配自有憑證。

    如果您不想要建立 BitLocker 管理加密憑證，請選擇使用純文字來儲存修復資料。 當您建立 BitLocker 管理原則時，啟用 [允許以純文字格式儲存復原資訊]  選項。

    > [!NOTE]
    > 另一層安全性是加密整個網站資料庫。 如果您對資料庫啟用加密，Configuration Manager 就不會有任何功能上的問題。
    >
    > 請謹慎使用加密，特別是在大規模環境中。 視您加密的資料表和 SQL 版本而定，您可能會發現效能降低近 25%。 更新您的備份和復原計畫，以便成功復原加密的資料。

## <a name="certificate-requirements"></a>憑證需求

### <a name="https-server-authentication-certificate"></a>HTTPS 伺服器驗證憑證

<!--5925660-->

在 Configuration Manager 最新分支 1910 版中，若要整合 BitLocker 復原服務，則必須針對管理點啟用 HTTPS。 需要有 HTTPS 連線，才能從 Configuration Manager 用戶端，將網路上的修復金鑰加密至管理點。 對許多客戶而言，設定管理點和所有 HTTPS 用戶端可能會很困難。

從 2002 版開始，HTTPS 需求適用於裝載復原服務的 IIS 網站，而不是整個管理點角色。 這項變更放寬了憑證需求，但仍然會加密傳輸中的修復金鑰。

現在，管理點的 [用戶端連線]  屬性可以是 **HTTP** 或 **HTTPS**。 如果管理點已設定為 **HTTP**，若要支援 BitLocker 復原服務，請：

1. 取得伺服器驗證憑證。 將憑證繫結至管理點上裝載 BitLocker 復原服務的 IIS 網站。

2. 將用戶端設定為信任伺服器驗證憑證。 有兩種方式可完成此信任：

    - 使用來自公用且全球受信任的憑證提供者的憑證。 例如 (但不限於)，DigiCert、Thawte 或 VeriSign。 Windows 用戶端包含來自這些提供者的受信任的根憑證授權單位 (CA)。 使用這些提供者之一發出的伺服器驗證憑證，用戶端應該會自動信任該憑證。

    - 使用 CA 根據組織公開金鑰基礎結構 (PKI) 所發出的憑證。 大部分 PKI 實作會將信任的根 CA 新增到 Windows 用戶端。 例如，使用搭配群組原則的 Active Directory 憑證服務。 如果從用戶端未自動信任的 CA 發出伺服器驗證憑證，則請將 CA 受信任的根憑證新增至用戶端。

> [!TIP]
> 唯一需要與復原服務通訊的用戶端，是您打算使用 BitLocker 管理原則作為目標且包含**用戶端管理**規則的用戶端。

在用戶端上，請使用 **BitLockerManagementHandler.log** 來針對此連線進行疑難排解。 針對復原服務的連線，該記錄檔會顯示用戶端正在使用的 URL。 請找出開頭為 `Checking for Recovery Service at` 的項目。

> [!NOTE]
> 如果您的網站有多個管理點，請在受 BitLocker 管理的用戶端可能通訊的網站上，啟用所有管理點上的 HTTPS。 如果 HTTPS 管理點無法使用，用戶端可能會容錯移轉 至 HTTP 管理點，繼而無法委付其修復金鑰。
>
> 這項建議適用於這兩個選項：啟用 HTTPS 的管理點或啟用在管理點上裝載復原服務的 IIS 網站。

### <a name="sql-encryption-certificate"></a>SQL 加密憑證

使用此憑證來啟用 BitLocker 修復資料的 SQL Server 儲存格層級加密。 您可以使用自己的程序來建立和部署 BitLocker 管理加密憑證，只要此憑證符合下列需求：

- BitLocker 管理加密憑證的名稱必須是 `BitLockerManagement_CERT`。

- 使用資料庫主要金鑰加密此憑證。

- 下列 SQL 使用者需要此憑證的**控制**權限：
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- 在階層中的每個網站資料庫上部署相同憑證。

- 在您環境中使用最新版本的 SQL Server 來建立憑證。 例如：
  - 使用 SQL Server 2016 或更新版本建立的憑證與 SQL Server 2014 或更舊版本相容。
  - 使用 SQL Server 2014 或更舊版本建立的憑證與 SQL Server 2016 或更新版本不相容。

## <a name="example-scripts"></a>範例指令碼

這些 SQL 指令碼是在 Configuration Manager 站台資料庫中建立及部署 BitLocker 管理加密憑證的範例。

### <a name="create-certificate"></a>建立憑證

這個範例指令碼會執行下列動作：

- 建立憑證
- 設定權限
- 建立資料庫主要金鑰

在生產環境中使用此指令碼之前，請變更下列值：

- 站台資料庫名稱 (`CM_ABC`)
- 建立主要金鑰所用的密碼 (`MyMasterKeyPassword`)
- 憑證到期日 (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>備份憑證

此範例指令碼會備份憑證。 將憑證儲存到檔案後，即可將此憑證[還原](#restore-certificate)到階層中的其他網站資料庫。

在生產環境中使用此指令碼之前，請變更下列值：

- 站台資料庫名稱 (`CM_ABC`)
- 檔案路徑和名稱 (`C:\BitLockerManagement_CERT_KEY`)
- 匯出金鑰密碼 (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> 將所匯出憑證檔案和相關聯密碼儲存在安全的位置。

### <a name="restore-certificate"></a>還原憑證

這個範例指令碼會從檔案還原憑證。 使用此程序將您建立的憑證部署到另一個站台資料庫。

在生產環境中使用此指令碼之前，請變更下列值：

- 站台資料庫名稱 (`CM_ABC`)
- 主要金鑰密碼 (`MyMasterKeyPassword`)
- 檔案路徑和名稱 (`C:\BitLockerManagement_CERT_KEY`)
- 匯出金鑰密碼 (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>驗證憑證

使用此 SQL 指令碼驗證 SQL 已成功建立具有必要權限的憑證。

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

如果憑證有效，指令碼會傳回 `1` 值。

## <a name="see-also"></a>請參閱

如需這些 SQL 命令的詳細資訊，請參閱下列文章：

- [SQL Server 和資料庫加密金鑰](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [CREATE CERTIFICATE](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [BACKUP CERTIFICATE](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [CREATE MASTER KEY](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [BACKUP MASTER KEY](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [ 憑證權限](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
