---
title: 安裝 Exchange Connector
titleSuffix: Configuration Manager
description: 安裝並設定適用于 Configuration Manager 的 Exchange connector，以透過 ActiveSync 管理行動裝置。
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d854e4b70a59a364b8611947feea89d4678e7e6
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724842"
---
# <a name="install-and-configure-the-exchange-connector"></a>安裝和設定 Exchange connector

適用於：  Configuration Manager (最新分支)

使用此程式來安裝及設定 Exchange Server 連接器，以管理行動裝置。 在 Exchange 組織中，Configuration Manager 僅支援一個連接器。

安裝適用于 Configuration Manager 的 Exchange Server 連接器之前，請確定您擁有必要的許可權和版本。 如需詳細資訊，請參閱[使用 Exchange 和 Configuration Manager 的裝置管理](manage-mobile-devices-with-exchange-activesync.md#prerequisites)。

## <a name="exchange-connection-account"></a>Exchange 線上帳戶

決定用於連接至 Exchange Client Access Server 以管理行動裝置的帳戶。 此帳戶可以是站台伺服器的電腦帳戶，也可以是 Windows 使用者帳戶。

然後，在 Exchange 角色群組中設定此帳戶，以執行下列 Exchange Server Cmdlet：

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-User**  

- **Set-ActiveSyncOrganizationSettings**  

下列 Exchange Server 管理角色包括這些 Cmdlet：

- 收件者管理
- 僅限視圖的組織管理
- 伺服器管理

如需詳細資訊，請參閱 Exchange Server 2013 檔中的[瞭解管理角色群組](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help)。

> [!TIP]  
> 如果您嘗試在沒有必要 Cmdlet 的情況下安裝或使用 Exchange Server 連接器，您將會在網站伺服器電腦的 Easdisc.log 檔案中看到下列錯誤： `Invoking cmdlet <cmdlet> failed`。

## <a name="install-the-connector"></a>安裝連接器

1. 在 Configuration Manager 主控台中，移至 [系統**管理**] 工作區 **，展開 [** 階層設定]，然後選取 [ **Exchange Server 連接器**]。

1. 在功能區 [**首頁**] 索引標籤的 [**建立**] 群組中，選取 [**新增 Exchange Server**]。

1. 在 [新增 Exchange Server wizard] 的 [**一般**] 頁面上，選取其中一個 Exchange server 環境：

    - 內部**部署 Exchange server**：為每個 Active Directory 網站指定單一伺服器或用戶端存取伺服器陣列。

        如果伺服器或陣列離線，Configuration Manager 會嘗試探索要使用的 Client Access Server。 如果失敗，Configuration Manager 將會退而使用信箱伺服器建立與 Client Access Server 的連線。 當它重新嘗試連接時，它會將下列警告記錄在網站伺服器電腦上的 Easdisc.log 檔案中： `Failed to open runspace for site <site_name>`。

    - **託管的 Exchange server**：指定 exchange Online 環境的伺服器位址。

    然後選取要執行 Exchange Server 連接器的主要網站。

1. 在 [**帳戶**] 頁面上，指定要連接到 Exchange 伺服器的帳戶。 如需詳細資訊，請參閱[Exchange 線上帳戶](#exchange-connection-account)。

1. 在 [**探索**] 頁面上，設定同步處理排程和尋找裝置的規則。

1. 在 [**設定**] 頁面上，設定下列群組中的行動裝置設定：

    - **一般**
    - **密碼**
    - **電子郵件管理**
    - **安全性**
    - **應用程式**

    如需詳細資訊，請參閱[Exchange connector 設定](manage-mobile-devices-with-exchange-activesync.md#policies)。

    如果您也使用 Configuration Manager[內部部署 MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)註冊行動裝置，請啟用 [**允許外部行動裝置管理**] 選項。 此設定可讓這些行動裝置在 Configuration Manager 註冊後，繼續接收 Exchange 的電子郵件。

1. 完成精靈。

## <a name="verify-and-monitor"></a>驗證和監視

使用狀態訊息和記錄檔，確認 Exchange Server 連接器的安裝：

- 確認月臺元件管理員已成功安裝 Exchange Server 連接器。 從**SMS_EXCHANGE_CONNECTOR**元件尋找訊息狀態識別碼**1015** 。

    如果指定的用戶端存取伺服器離線，安裝可能會失敗。 如果 Configuration Manager 無法成功安裝連接器，Configuration Manager 每60分鐘重試一次安裝。 它會繼續重試，直到安裝成功或您移除 Exchange Server 連接器為止。

- 在網站伺服器電腦上，檢查下列專案的**sitecomp.log** ： `Component SMS_EXCHANGE_CONNECTOR flagged for installation`。 然後，它會以下列文字記錄成功的安裝`STATMSG: ID=1015`：。

完成安裝之後，請監視連接器找到及管理的行動裝置。 查看行動裝置的集合，並使用行動裝置的報告。

> [!NOTE]  
> Configuration Manager 會為所找到的行動裝置產生名稱。 其使用的格式為 [*使用者名稱*_*裝置類型*]。 例如， **jdoe_WindowsPhone**。 如果使用者的多個行動裝置均為相同的裝置類型，Configuration Manager 會在主控台和報告中顯示同一個名稱代表這些行動裝置。  

## <a name="see-also"></a>請參閱

- [設定用戶端和網站系統使用的埠](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Proxy 伺服器支援](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [行動裝置的安全性建議](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [使用 Exchange Server 連接器管理之行動裝置的隱私權資訊](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)
