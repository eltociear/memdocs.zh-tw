---
title: 啟用傳輸層安全性 (TLS) 1.2 時的常見問題
titleSuffix: Configuration Manager
description: 描述啟用傳輸層安全性 (TLS) 1.2 時的常見問題
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c07b0af1b3063619ac5f71965d96f611aefafd9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704066"
---
# <a name="common-issues-when-enabling-tls-12"></a>啟用 TLS 1.2 時的常見問題

下文提供的建議是針對當在 Configuration Manager 中啟用 TLS 1.2 支援時所發生常見問題。

## <a name="unsupported-platforms"></a>不支援的平台

Configuration Manager 支援下列用戶端平台，但在 TLS 1.2 的環境中不支援：

- Windows CE
- Apple OS X
- 使用內部部署 MDM 所管理的 Windows 10 裝置

## <a name="reports-dont-show-in-the-console"></a>報表沒有顯示在主控台中

如果 Configuration Manager 主控台中未顯示報表，請務必更新正在執行主控台的電腦。 [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，並啟用強式加密。

## <a name="fips-security-policy-enabled"></a>已啟用 FIPS 安全性原則

如果為用戶端或伺服器啟用 FIPS 安全性原則設定，則安全通道 (Schannel) 交涉可能會導致它們使用 TLS 1.0。 即使您在登錄中停用通訊協定，也會發生此行為。

若要調查，請啟用安全通道事件記錄，然後檢閱系統記錄中的 Schannel 事件。 如需詳細資訊，請參閱[如何在 Schannel.dll 中限制特定密碼編譯演算法與通訊協定的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc) \(機器翻譯\)。

## <a name="sql-server-communication-failure"></a>SQL Server 通訊失敗

如果 SQL Server 通訊失敗並傳回 **SslSecurityError** 錯誤，請確認下列設定：

- [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，並在每部機器上啟用強式加密
- 在主機伺服器上[更新 SQL Server](enable-tls-1-2-server.md#bkmk_sql)
- 在與 SQL 通訊的所有系統上[更新 SQL 用戶端元件](enable-tls-1-2-server.md#bkmk_sql-client)。 例如，站台伺服器、SMS 提供者和站台角色伺服器。

## <a name="configuration-manager-client-communication-failures"></a>Configuration Manager 用戶端通訊失敗

如果 Configuration Manager 用戶端無法與站台角色通訊，請確認是否已[更新 Windows](enable-tls-1-2-client.md#bkmk_winhttp) 以使用 WinHTTP 支援 TLS 1.2 進行主從式通訊。 常見的站台角色包含發佈點、管理點和狀態移轉點。

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Reporting Services 點失敗並傳回預期的錯誤

如果 Reporting Services 點未設定報告，請檢查 **SRSRP.log** 以取得下列錯誤項目：

`The underlying connection was closed:`
`An expected error occurred on a receive.`

若要解決此問題，請遵循下列步驟：

1. [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，並在所有相關的電腦上啟用強式加密。

1. 安裝任何更新後，請重新啟動 SMS_Executive 服務。

## <a name="application-catalog-doesnt-initialize"></a>應用程式類別目錄不會初始化

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)。

如果應用程式類別目錄不會初始化，請檢查 **ServicePortalWebSite.svclog** 檔案以取得下列錯誤項目：

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

若要解決此問題，請遵循下列步驟：

1. [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，並在所有相關的電腦上啟用強式加密。

1. 在應用程式類別目錄伺服器的 `%WinDir%\System32\InetSrv` 資料夾中，使用下列內容來建立 **W2SP.exe.config** 檔案：

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > 如果應用程式是使用 .NET Framework 4.6.3 建置的，則此檔案是已建立的預設檔案。

1. 針對應用程式類別目錄角色使用 HTTPS 傳輸安全性。

    > [!Important]
    > 當您針對應用程式類別目錄角色使用 HTTP 訊息安全性時，即會將 WCF 硬式編碼為只使用 SSL 3.0 與 TLS 1.0。 這可防止使用 TLS 1.2。

1. 如果您進行了任何變更，請重新啟動電腦。

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>軟體中心或瀏覽器不會與應用程式類別目錄進行通訊

> [!Important]  
> 1910 版會終止對應用程式類別目錄角色的支援。 如需詳細資訊，請參閱[已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)。

要使軟體中心與已啟用 TLS 1.2 之站台中的使用者可用應用程式搭配使用，最佳方法就是移除應用程式類別目錄角色。 然後讓軟體中心直接與管理點通訊。 如需詳細資訊，請參閱[移除應用程式類別目錄](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)。

如果您需要解決應用程式類別目錄和軟體中心之間的通訊失敗，請確認下列條件：

- [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，並在每部電腦上啟用強式加密。

- 在您進行變更之後，重新啟動所有受影響的電腦。

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>服務連接點上傳失敗

如果服務連接點無法將資料上傳至 SCCMConnectedService，請[更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，並在每部電腦上啟用強式加密。 在您進行變更之後，請記得重新啟動電腦。

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager 主控台會顯示 [Intune 上線] 對話方塊

如果當主控台嘗試連線到 Intune 入口網站時出現 Intune 上線對話方塊，請[更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，並在每部電腦上啟用強式加密。 在您進行變更之後，請記得重新啟動電腦。

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager 主控台會顯示無法登入 Azure

當您嘗試在 Azure Active Directory (Azure AD) 中建立應用程式時，如果 Azure 服務上線對話方塊在您選取 [登入]  之後立即失敗，請[更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，並啟用強式加密。 在您進行變更之後，請記得重新啟動電腦。

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager 雲端服務與 TLS 1.2

雲端管理閘道和雲端發佈點所使用的 Azure 虛擬機器支援 TLS 1.2。 支援的用戶端版本會自動使用 TLS 1.2。

**SMSAdminui.log** 可能包含類似於下列範例的錯誤：

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

在系統事件記錄檔中，可以使用以下描述記錄 SChannel EventID 36874：`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>其他資源

- [.NET Framework 的傳輸層安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244：Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) \(機器翻譯\)
- [密碼編譯控制技術參考](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>後續步驟

- [在用戶端啟用 TLS 1.2](enable-tls-1-2-client.md)
- [在站台伺服器與遠端站台系統啟用 TLS 1.2](enable-tls-1-2-server.md)

