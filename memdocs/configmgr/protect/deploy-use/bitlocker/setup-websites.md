---
title: 設定 BitLocker 入口網站
titleSuffix: Configuration Manager
description: 安裝自助入口網站，以及管理與監視網站的 BitLocker 管理元件
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53fc4f694579fb8c53a4aea1054cf49dff21e1d2
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715674"
---
# <a name="set-up-bitlocker-portals"></a>設定 BitLocker 入口網站

適用於：Configuration Manager (最新分支)

<!--3601034-->

若要在 Configuration Manager 中使用下列 BitLocker 管理元件，您必須先加以安裝：

- 使用者自助入口網站
- 管理與監視網站 (服務台入口網站)

您可以在已安裝 IIS 的現有站台伺服器或站台系統伺服器上安裝入口網站，或使用獨立的 Web 伺服器來加以裝載。

> [!NOTE]
> 只安裝具有主要站台資料庫的自助入口網站，以及管理與監視網站。 在階層中，為每個主要站台安裝這些網站。

開始之前，請先確認這些元件的[先決條件](../../plan-design/bitlocker-management.md#prerequisites)。

## <a name="script-usage"></a>指令碼使用方式

此程序使用 PowerShell 指令碼 MBAMWebSiteInstaller.ps1 在網頁伺服器上安裝這些元件。 它接受下列參數︰

- `-SqlServerName <ServerName>` (必要)：主要站台資料庫伺服器的完整網域名稱。

- `-SqlInstanceName <InstanceName>`：主要站台資料庫的 SQL Server 執行個體名稱。 若 SQL 使用預設執行個體，請不要包括此參數。

- `-SqlDatabaseName <DatabaseName>` (必要)：主要站台資料庫的名稱，例如 `CM_ABC`。

- `-ReportWebServiceUrl <ReportWebServiceUrl>`：主要站台之 Reporting Services 點的 Web 服務 URL。 它是 [Reporting Services 組態管理員] 中的 [Web 服務 URL] 值。

    > [!NOTE]
    > 此參數的目的是要安裝連結至管理與監視網站的**復原稽核報告**。 根據預設，Configuration Manager 包含其他 BitLocker 管理報告。

- `-HelpdeskUsersGroupName <DomainUserGroup>`：例如 `contoso\BitLocker help desk users`。 其成員對於管理和監視網站中 [管理 TPM] 和 [磁碟機修復] 區域具有存取權的網域使用者群組。 當使用這些選項時，此角色需要填寫所有欄位，包括使用者的網域與帳戶名稱。

- `-HelpdeskAdminsGroupName <DomainUserGroup>`：例如 `contoso\BitLocker help desk admins`。 成員可存取管理及監視網站之所有復原區域的網域使用者群組。 協助使用者修復其驅動程式時，此角色只需要輸入修復金鑰。

- `-MbamReportUsersGroupName <DomainUserGroup>`：例如 `contoso\BitLocker report users`。 成員具有管理及監視網站之**報表**區域唯讀存取權的網域使用者群組。

    > [!NOTE]
    > 安裝程式指令碼不會建立您在 **-HelpdeskUsersGroupName**、 **-HelpdeskAdminsGroupName** 與 **-MbamReportUsersGroupName** 參數中指定的網域使用者群組。 執行指令碼之前，請務必先建立這些群組。
    >
    > 當您指定 **-HelpdeskUsersGroupName**、 **-HelpdeskAdminsGroupName** 與 **-MbamReportUsersGroupName** 參數時，請務必同時指定網域名稱與群組名稱。 請使用 `"domain\user_group"` 格式。 不要排除網域名稱。 如果網域或群組名稱包含空格或特殊字元，請將參數括在引號中 (`"`)。

- `-SiteInstall Both`：指定要安裝的元件。 有效選項包括：
  - `Both`：安裝兩個元件
  - `HelpDesk`：只安裝管理和監視網站
  - `SSP`：只安裝自助入口網站

- `-IISWebSite`：指令碼在其中安裝 MBAM Web 應用程式的網站。 根據預設，它會使用 IIS 預設網站。 請先建立自訂網站，再使用此參數。

- `-InstallDirectory`：指令碼在其中安裝 Web 應用程式檔案的路徑。 此路徑預設為 `C:\inetpub`。 請先建立自訂目錄，再使用此參數。

- `-Uninstall`：在先前已安裝的 Web 伺服器上，解除安裝 BitLocker Management 服務台/自助 Web 入口網站。


## <a name="run-the-script"></a>執行指令碼

在目標 Web 伺服器上，執行下列動作：

> [!NOTE]
> 視您的網站設計而定，您可能需要執行指令碼多次。 例如，請在管理點上執行指令碼，以安裝管理與監視網站。 然後在獨立的 Web 伺服器上再次加以執行，以安裝自助入口網站。

1. 將下列檔案從站台伺服器上 Configuration Manager 安裝資料夾中的 `SMSSETUP\BIN\X64` 複製到目標伺服器上的本機資料夾：

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. 以系統管理身分執行 PowerShell，然後執行如下列命令列的指令碼：

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    例如，

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > 此範例命令列會使用所有可能的參數來顯示其使用方式。 根據您環境中的需求調整您的使用方式。

安裝之後，透過下列 URL 存取入口網站：

- 自助入口網站：`https://webserver.contoso.com/SelfService`
- 管理和監視網站：`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft 建議建議您使用 HTTPS，但不要求您這樣做。 如需詳細資訊，請參閱 [How to set up SSL on IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis) (如何在 IIS 上設定 SSL)。

## <a name="verify"></a>確認

使用下列記錄來進行監視及進行疑難排解：

- **Microsoft-Windows-MBAM-Web** 下的 Windows 事件記錄檔。 如需詳細資訊，請參閱[關於 BitLocker 事件記錄檔](../../tech-ref/bitlocker/about-event-logs.md)與[伺服器事件記錄檔](../../tech-ref/bitlocker/server-event-logs.md)。

- 每個元件的追蹤記錄檔都位於下列預設位置：

  - 自助入口網站：`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - 管理和監視網站：`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

如需詳細的疑難排解資訊，請參閱[針對 BitLocker 進行疑難排解](../../tech-ref/bitlocker/troubleshoot.md)。

## <a name="next-steps"></a>後續步驟

[自訂自助入口網站](customize-self-service-portal.md)

如需使用您所安裝之元件的詳細資訊，請參閱下列文章：

- [BitLocker 管理和監視網站](helpdesk-portal.md)
- [BitLocker 自助入口網站](self-service-portal.md)
