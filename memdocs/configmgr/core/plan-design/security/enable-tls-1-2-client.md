---
title: 如何在用戶端啟用傳輸層安全性 (TLS) 1.2
titleSuffix: Configuration Manager
description: 如何針對 Configuration Manager 用戶端啟用 TLS 1.2 的相關資訊。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704106"
---
# <a name="how-to-enable-tls-12-on-clients"></a>如何在用戶端啟用 TLS 1.2

適用於：*Configuration Manager (最新分支)*

針為 Configuration Manager 環境啟用 TLS 1.2 時，請先確認用戶端能夠處理且已正確設定為使用 TLS 1.2，然後才啟用 TLS 1.2，並在站台伺服器和遠端站台系統上停用較舊的通訊協定。 在用戶端啟用 TLS 1.2 有三個工作：

- 更新 Windows 和 WinHTTP
- 確定已在作業系統層級啟用 TLS 1.2 作為安全通道的通訊協定
- 更新並設定 .NET Framework 以支援 TLS 1.2

如需特定 Configuration Manager 功能和案例的相依性詳細資訊，請參閱[關於啟用 TLS 1.2](enable-tls-1-2.md)。

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> 更新 Windows 和 WinHTTP

Windows 8.1、Windows Server 2012 R2、Windows 10、Windows Server 2016 與 Window 更新版本原生支援 TLS 1.2，以透過 WinHTTP 進行主從式通訊。 

舊版 Windows (例如 Windows 7 或 Windows Server 2012) 預設不會啟用 TLS 1.1 或 1.2 以使用 WinHTTP 進行安全通訊。 針對這些舊版 Windows，請安裝[更新 3140245](https://support.microsoft.com/help/3140245) 以啟用以下的登錄值，可設定此值以將 TLS 1.1 和 TLS 1.2 新增至 WinHTTP 的預設安全通訊協定清單。 安裝修補程式之後，請建立下列登錄值：

> [!IMPORTANT]
> 在執行舊版 Windows 的所有用戶端上啟用這些設定，「然後」  啟用 TLS 1.2 並停用 Configuration Manager 伺服器上的舊版通訊協定。 否則，您可能會在無意中孤立它們。

確認 `DefaultSecureProtocols` 登錄設定的值，例如：

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

如果您變更此值，請重新啟動電腦。

上述範例顯示了 WinHTTP `DefaultSecureProtocols` 設定的 `0xAA0` 值。 [KB 3140245：Update to enable TLS 1.1 and TLS 1.2 as default secure protocols in WinHTTP in Windows](https://support.microsoft.com/help/3140245) (更新以在 Windows 中的 WinHTTP 中啟用 TLS 1.1 和 TLS 1.2 作為預設安全通訊協定) 中列出了每個通訊協定的十六進位值。 根據預設，在 Windows 中此值是 `0x0A0`，以針對 WinHTTP 啟用 SSL 3.0 和 TLS 1.0。 上述範例會保留這些預設值，並為 WinHTTP 啟用 TLS 1.1 和 TLS 1.2。 此設定可確保變更不會中斷任何其他可能仍仰賴 SSL 3.0 或 TLS 1.0 的應用程式。 您可以使用 `0xA00` 的值，僅啟用 TLS 1.1 與 TLS 1.2。 Configuration Manager 支援 Windows 在兩部裝置之間進行交涉的最安全通的訊協定。

 如果您想要完全停用 SSL 3.0 與 TLS 1.0，請使用 Windows 中的 SChannel 停用通訊協定設定。 如需詳細資訊，請參閱[如何在 Schannel.dll 中限制特定密碼編譯演算法與通訊協定的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc) \(機器翻譯\)。

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> 確定已在作業系統層級啟用 TLS 1.2 作為安全通道的通訊協定

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> 更新並設定 .NET Framework 以支援 TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>後續步驟

- [在站台伺服器與遠端站台系統啟用 TLS 1.2](enable-tls-1-2-server.md)
- [啟用 TLS 1.2 時的常見問題](enable-tls-1-2-troubleshoot.md)

