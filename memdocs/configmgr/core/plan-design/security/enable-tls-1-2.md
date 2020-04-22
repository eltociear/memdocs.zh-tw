---
title: 啟用傳輸層安全性 (TLS) 1.2 概觀
titleSuffix: Configuration Manager
description: 如何針對 Configuration Manager 啟用 TLS 1.2 的概觀。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5d9d7cea7e5653b338a3eb4adb01d9fded99035e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704056"
---
# <a name="how-to-enable-tls-12"></a>如何啟用 TLS 1.2

適用於：*Configuration Manager (最新分支)*

傳輸層安全性 (TLS)，例如安全通訊端層 (SSL)，是一種加密通訊協定；其目的是要在透過網路傳輸時保護資料的安全。 這些文章描述確保 Configuration Manager 安全通訊使用 TLS 1.2 通訊協定所需的步驟。 這些文章也會描述對於常用元件的更新需求，以及常見問題的疑難排解。

## <a name="enabling-tls-12"></a>啟用 TLS 1.2

Configuration Manager 仰賴許多不同的元件進行安全通訊。 針對指定連線所使用通訊協定同時取決於用戶端與伺服器端的相關元件功能。 如果任何元件已過期或設定不正確，則通訊可能會使用較舊且較不安全的通訊協定。 若要正確啟用 Configuration Manager 以針對所有安全通訊支援 TLS 1.2，您必須針對所有必要的元件啟用 TLS 1.2。 必要的元件取決於您的環境，以及您所使用的 Configuration Manager 功能。

> [!IMPORTANT]
> 與用戶端一起啟動此程序，特別是舊版的 Windows。 在 Configuration Manager 伺服器上啟用 TLS 1.2 並停用較舊的通訊協定之前，請確定所有的用戶端都支援 TLS 1.2。 否則，用戶端無法與伺服器通訊，且可能被孤立。


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Configuration Manager 用戶端、站台伺服器和遠端站台系統的工作

若要針對 Configuration Manager 進行安全通訊所依賴元件啟用 TLS 1.2，您必須在用戶端和站台伺服器上執行多項工作。

### <a name="enable-tls-12-for-configuration-manager-clients"></a>針對 Configuration Manager 啟用 TLS 1.2

- [更新 Windows 和 Windows 8.0、Windows Server 2012 (非 R2) 及更早版本上的 WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)
- [確定已在作業系統層級啟用 TLS 1.2 作為安全通道的通訊協定](enable-tls-1-2-client.md#bkmk_protocol)
- [更新並設定 .NET Framework 以支援 TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>針對 Configuration Manager 站台伺服器和遠端站台系統啟用 TLS 1.2

- [確定已在作業系統層級啟用 TLS 1.2 作為安全通道的通訊協定](enable-tls-1-2-server.md#bkmk_protocol)
- [更新並設定 .NET Framework 以支援 TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [更新 SQL Server 和 SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [更新 Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>功能和案例相依性

下表說明特定 Configuration Manager 功能和案例的相依性。 若要確定接下來的步驟，請找到適用於您環境的項目。

|功能或案例|更新工作|
|--- |--- |
|站台伺服器 (中央、主要或次要)| - [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - 驗證強式加密設定|
|網站資料庫伺服器|[更新 SQL Server 與其用戶端元件](enable-tls-1-2-server.md#bkmk_sql)|
|次要站台伺服器|[更新 SQL Server 與其用戶端元件](enable-tls-1-2-server.md#bkmk_sql)至相容的 SQL Express 版本|
|網站系統角色| - [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net) 並驗證強式加密設定 <br/> - [更新 SQL Server 與其用戶端元件](enable-tls-1-2-server.md#bkmk_sql) (在需要它的角色上)，包括 [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Reporting Services 點|在站台伺服器、SQL Reporting Services 伺服器與任何包含主控台的電腦上- [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - 視需要重新啟動 SMS_Executive 服務|
|軟體更新點|[更新 WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|雲端管理閘道|[強制使用 TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager 主控台| - [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - 驗證強式加密設定|
|具備 HTTPS 站台系統角色的 Configuration Manager 用戶端|[更新 Windows 以使用 WinHTTP 支援 TLS 1.2 進行主從式通訊](enable-tls-1-2-client.md#bkmk_winhttp)|
|軟體中心| - [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - 驗證強式加密設定|
|Windows 7 用戶端| 在任何伺服器元件上啟用 TLS 1.2「之前」  ，請先[更新 Windows 以使用 WinHTTP 支援 TLS 1.2 進行主從式通訊](enable-tls-1-2-client.md#bkmk_winhttp)。 如果先在伺服器元件上啟用 TLS 1.2，會造成較早版本的用戶端被孤立。|

## <a name="frequently-asked-questions"></a>常見問題集

### <a name="why-use-tls-12-with-configuration-manager"></a>為何使用 TLS 1.2 搭配 Configuration Manager？

TLS 1.2 比先前的密碼編譯通訊協定 (例如 SSL 2.0、SSL 3.0、TLS 1.0 和 TLS 1.1) 更安全。 基本上，TLS 1.2 會讓資料在網路上傳輸時更安全。

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Configuration Manager 在何處使用 TLS 1.2 之類的加密通訊協定？

基本上 Configuration Manager 在五個區域使用 TLS 1.2 之類的加密通訊協定：

- 當角色設定為使用 HTTPS 時，與以 IIS 為基礎的站台伺服器角色進行用戶端通訊。 這些角色的範例包括發佈點、軟體更新點和管理點。
- 與 SQL 的管理點、SMS Executive 和 SMS 提供者通訊。 Configuration Manager 一律會加密 SQL 通訊。
- 將 WSUS 設定為使用 HTTPS 時的站台伺服器對 WSUS 通訊。
- SSRS 設定為使用 HTTPS 時，Configuration Manager 主控台對 SQL Reporting Services (SSRS) 的通訊。
- 與網際網路服務的任何連接。 範例包括雲端管理閘道 (CMG)、服務連接點同步，以及來自 Microsoft Update 的更新中繼資料同步。

### <a name="what-determines-which-encryption-protocol-is-used"></a>決定使用哪一種加密通訊協定的因素為何？

HTTPS 一律會在加密的交談中交涉用戶端和伺服器所支援最高通訊協定版本。 建立連接時，用戶端會以最高的可用通訊協定，將訊息傳送至伺服器。 如果伺服器支援相同版本，便會使用該版本來傳送訊息。 這個交涉過的版本便會用於連接。 如果伺服器不支援用戶端所提出版本，則伺服器訊息會指定能使用的最高版本。 如需 TLS 信號交換通訊協定的詳細資訊，請參閱 [Establishing a Secure Session by using TLS](https://docs.microsoft.com/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls) (使用 TLS 建立安全工作階段)。

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>決定用戶端和伺服器可以使用哪個通訊協定版本的因素為何？

一般來說，下列項目可以決定所使用通訊協定版本：

- 應用程式可以決定要交涉的特定通訊協定版本。
  - 最佳做法會決定避免在應用程式層級將特定通訊協定版本寫入程式碼，且遵循在元件和作業系統通訊協定層級所定義設定。
  - Configuration Manager 遵循這種最佳做法。
- 針對使用 .NET Framework 所撰寫應用程式，預設通訊協定版本取決於其編譯所在的架構版本。  
  - 4\.6.3 之前的 .NET 版本預設不會在交涉用通訊協定清單中包含 TLS 1.1 和 1.2。
- 使用 WinHTTP 進行 HTTPS 通訊的應用程式 (例如 Configuration Manager 用戶端) 會依賴作業系統版本、修補程式層級和設定來決定通訊協定版本支援。


## <a name="additional-resources"></a>其他資源

- [密碼編譯控制技術參考](cryptographic-controls-technical-reference.md)
- [.NET Framework 的傳輸層安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244：Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) \(機器翻譯\)

## <a name="next-steps"></a>後續步驟

- [在用戶端啟用 TLS 1.2](enable-tls-1-2-client.md)
- [在站台伺服器上啟用 TLS 1.2](enable-tls-1-2-server.md)
