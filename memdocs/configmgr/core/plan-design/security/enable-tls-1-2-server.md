---
title: 在站台伺服器與遠端站台系統啟用傳輸層安全性 (TLS) 1.2
titleSuffix: Configuration Manager
description: 如何針對 Configuration Manager 站台伺服器啟用 TLS 1.2 的相關資訊。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704096"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>如何在站台伺服器與遠端站台系統啟用 TLS 1.2

適用於：*Configuration Manager (最新分支)*

為 Configuration Manager 環境啟用 TLS 1.2 時，首先請[針對用戶端啟用 TLS 1.2](enable-tls-1-2-client.md)。 其次，在站台伺服器與遠端站台系統上啟用 TLS 1.2。 最後，測試用戶端對站台系統的通訊，然後才可能在伺服器端上停用舊版通訊協定。 若要在站台伺服器和遠端站台系統上啟用 TLS 1.2，需要執行下列工作：

- 確定已在作業系統層級啟用 TLS 1.2 作為安全通道的通訊協定
- 更新並設定 .NET Framework 以支援 TLS 1.2
- 更新 SQL Server 和用戶端元件
- 更新 Windows Server Update Services (WSUS)

如需特定 Configuration Manager 功能和案例的相依性詳細資訊，請參閱[關於啟用 TLS 1.2](enable-tls-1-2.md)。 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> 確定已在作業系統層級啟用 TLS 1.2 作為安全通道的通訊協定

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> 更新並設定 .NET Framework 以支援 TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> 更新 SQL Server 和用戶端元件

Microsoft SQL Server 2016 與更新版本支援 TLS 1.1 和 TLS 1.2。 舊版和相依程式庫可能需要更新。 如需詳細資訊，請參閱 [KB 3135244：Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) \(機器翻譯\)。

次要站台伺服器必須至少使用包含 Service Pack 2 的 SQL Server 2016 Express (13.2.50.26) 或更新版本。

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) 也說明 SQL Server 用戶端元件的需求。

請務必至少將 SQL Server Native Client 更新為版本 SQL 2012 SP4 (11.*.7001.0)。 從版本 1810 開始，此需求是[先決條件檢查 (警告)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

Configuration Manager 會在下列站台系統角色上使用 SQL Server Native Client：

- 網站資料庫伺服器
- 站台伺服器：管理中心網站、主要站台或次要站台
- 管理點
- 裝置管理點
- 狀態移轉點
- SMS 提供者
- 軟體更新點
- 啟用多點傳送的發佈點
- Asset Intelligence 更新服務點
- Reporting Services 點
- 應用程式類別目錄 Web 服務
- 註冊點
- Endpoint Protection 點
- 服務連接點
- 憑證登錄點
- 資料倉儲服務點


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> 更新 Windows Server Update Services (WSUS)

若要在舊版 WSUS 中支援 TLS 1.2，請在 WSUS 伺服器上安裝下列更新：

- 針對執行 Windows Server 2012 的 WSUS 伺服器，請安裝[更新 4022721](https://support.microsoft.com/help/4022721) 或較新的彙總套件更新。
- 針對執行 Windows Server 2012 R2 的 WSUS 伺服器，請安裝[更新 4022720](https://support.microsoft.com/help/4022720) 或較新的彙總套件更新。

從 Windows Server 2016 開始，WSUS 預設會支援 TLS 1.2。  只有在 Windows Server 2012 和 Windows Server 2012 R2 WSUS 伺服器上才需要 TLS 1.2 更新。

## <a name="next-steps"></a>後續步驟

- [啟用 TLS 1.2 時的常見問題](enable-tls-1-2-troubleshoot.md)
