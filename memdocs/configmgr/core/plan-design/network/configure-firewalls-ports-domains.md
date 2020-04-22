---
title: 網路基礎結構
titleSuffix: Configuration Manager
description: 設定防火牆、連接埠和網域，以準備進行 Configuration Manager 通訊。
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703086"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>適用於 Configuration Manager 的網路基礎結構考量

適用於：  Configuration Manager (最新分支)

若要準備您的網路以支援 Configuration Manager，您可能需要設定一些基礎結構元件。 例如，開啟防火牆連接埠以傳遞 Configuration Manager 所使用的通訊。  

## <a name="ports-and-protocols"></a>連接埠與通訊協定

不同的 Configuration Manager 功能會使用不同的網路連接埠。 有些連接埠為必要項，而有些連接埠可讓您自訂。

大多數的 Configuration Manager 通訊都會使用一般連接埠，例如，針對 HTTP 使用連接埠 80 或針對 HTTPS 使用 443。 有些站台系統角色支援使用自訂網站及自訂連接埠。 如需詳細資訊，請參閱[站台系統伺服器的網站](websites-for-site-system-servers.md)。

部署 Configuration Manager 之前，請先找出您打算使用的連接埠，然後視需要設定防火牆。

安裝 Configuration Manager 之後，如果您需要變更連接埠，別忘了更新裝置與網路上的防火牆。 此外，還要變更 Configuration Manager 中的連接埠設定。

如需詳細資訊，請參閱下列文章：

- [如何設定用戶端通訊連接埠](../../clients/deploy/configure-client-communication-ports.md)
- [Configuration Manager 中使用的連接埠](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>網際網路存取需求

某些 Configuration Manager 功能依賴網際網路連線能力來取得完整功能。 如果您的組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，請務必允許必要的端點。

如需詳細資訊，請參閱[網際網路存取需求](internet-endpoints.md)。


## <a name="proxy-servers"></a>Proxy 伺服器

您可以為不同的站台系統伺服器及用戶端指定不同的 Proxy 伺服器。 當您安裝站台系統角色或用戶端，或稍後視需要加以變更時，您就要進行這些設定。

如需詳細資訊，請參閱 [Proxy 伺服器支援](proxy-server-support.md)。
