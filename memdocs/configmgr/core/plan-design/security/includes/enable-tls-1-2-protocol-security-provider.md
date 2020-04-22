---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704076"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1.2 會預設為啟用。 因此，不需要對這些機碼進行任何變更，即可加以啟用。 當已遵循這些文章中的其餘指引，且已確認該環境只有在啟用 TLS 1.2 時才能正常運作之後，即可在 `Protocols` 下方進行變更以停用 TLS 1.0 與 TLS 1.1。

驗證 `\SecurityProviders\SCHANNEL\Protocols` 登錄子機碼設定，如 [.NET Framework 的傳輸層安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)中所示。

