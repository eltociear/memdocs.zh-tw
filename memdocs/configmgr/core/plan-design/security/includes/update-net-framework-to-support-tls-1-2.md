---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704086"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>判斷 .NET 版本

首先，判斷已安裝的 .NET 版本。 如需詳細資訊，請參閱[如何判斷您安裝的 Microsoft .NET Framework 版本和其 Service Pack 等級](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)。

### <a name="install-net-updates"></a>安裝 .NET 更新

安裝 .NET 更新，可讓您啟用強式加密。 .NET Framework 的部分版本可能需要進行更新，才能啟用強式加密。 使用下列指引：

- .NET Framework 4.6.2 與更新版本支援 TLS 1.1 和 TLS 1.2。 確認登錄設定，但不需要進行其他變更。

- 更新 NET Framework 4.6 與更早版本以支援 TLS 1.1 與 TLS 1.2。 如需詳細資訊，請參閱 [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)。

- 如果您在 Windows 8.1 或 Windows Server 2012 上使用 .NET Framework 4.5.1 或 4.5.2，也可以從[下載中心](https://www.microsoft.com/download/details.aspx?id=42883)取得相關的更新與詳細資料。


### <a name="configure-for-strong-cryptography"></a>設定強式加密

設定 .NET Framework 以支援強式加密。 將 `SchUseStrongCrypto` 登錄設定設為 `DWORD:00000001`。 此值會停用 RC4 串流加密且需要重新啟動。 如需詳細資訊，請參閱 [Microsoft 資訊安全諮詢 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358) \(英文\)。

請務必在任何透過網路與啓用了 TLS 1.2 的系統進行通訊的電腦上，設定下列登錄機碼。 例如，站台伺服器及站台伺服器本身未安裝 Configuration Manager 用戶端、遠端站台系統角色。

針對在 32 位元 OS 上所執行 32 位元應用程式或在 64 位元 OS 上所執行 64 位元應用程式，更新下列子機碼值：

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

針對在 64 位元 OS 上執行的 32 位元應用程式，更新下列子機碼值：

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto` 設定允許 .NET 使用 TLS 1.1 和 TLS 1.2。 `SystemDefaultTlsVersions` 設定允許 .NET 使用 OS 設定。 如需詳細資訊，請參閱 [.NET Framework 的傳輸層安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls)。
