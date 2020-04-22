---
title: VPN 設定檔
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 VPN 設定檔，將 VPN 設定部署至組織中的使用者。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706246"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Configuration Manager 中的 VPN 設定檔

適用於：  Configuration Manager (最新分支)

<!--1283610-->
若要將 VPN 設定部署至組織中的使用者，請在 Configuration Manager 中使用 VPN 設定檔。 透過部署這些設定，即可最小化連線到公司網路上資源所需的使用者工作。  

例如，您想要使用連線到內部網路檔案共用所需的設定來設定所有 Windows 10 裝置。 使用連線到內部網路所需的設定建立 VPN 設定檔。 然後將此設定檔部署到所有具有執行 Windows 10 之裝置的使用者。 這些使用者會在可用的網路清單中看到此 VPN 連線，而且很輕鬆就能完成連線。

建立 VPN 設定檔時，您可以加入多種安全性設定。 這些設定包括使用 Configuration Manager 憑證設定檔佈建的伺服器驗證和用戶端驗證憑證。 如需詳細資訊，請參閱[憑證設定檔](introduction-to-certificate-profiles.md)。

> [!Note]
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

## <a name="supported-platforms"></a>支援的平台

下表說明針對不同裝置平台可以設定的 VPN 設定檔。

|連線類型|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|是|否|是|是|
|**F5 Edge Client**|是|否|是|是|
|**Dell SonicWALL Mobile Connect**|是|否|是|是|
|**Check Point Mobile VPN**|是|否|是|是|
|**Microsoft SSL (SSTP)**|是|是|是|否|
|**Microsoft Automatic**|是|是|是|否|
|**IKEv2**|是|是|是|否|
|**PPTP**|是|是|是|否|
|**L2TP**|是|是|是|否|

## <a name="next-step"></a>後續步驟

> [!div class="nextstepaction"]
> [如何建立 VPN 設定檔](create-vpn-profiles.md)

## <a name="see-also"></a>請參閱

- [VPN 設定檔的必要條件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [VPN 設定檔的安全性和隱私權](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
