---
title: 保護資料和站台的基礎結構
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 保護組織的資源，避免暴露或遭受惡意攻擊。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708596"
---
# <a name="protect-data-and-site-infrastructure"></a>保護資料和站台的基礎結構

適用於：  Configuration Manager (最新分支)

您希望使用者能安全存取您組織的資源。 保護您的基礎結構和資料免受暴露或惡意攻擊。 使用 Configuration Manager 啟用存取，並協助保護您組織的資源。  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) 可讓您管理用戶端電腦的下列 Microsoft Defender 原則：

  - Microsoft Defender 反惡意程式碼
  - Microsoft Defender 防火牆
  - Microsoft Defender 進階威脅防護
  - Microsoft Defender 惡意探索防護
  - Microsoft Defender 應用程式防護
  - Microsoft Defender 應用程式控制

  > [!TIP]
  > 若要使用 Microsoft Endpoint Manager 雲端服務管理共同受控 Windows 10 裝置上的端點保護，請將 [**Endpoint Protection** 工作負載](../../comanage/workloads.md#endpoint-protection)切換至 Intune。 如需詳細資訊，請參閱 [Microsoft Intune Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)。

- 使用 BitLocker 磁碟機加密 (BDE) 保護儲存在內部部署 Windows 用戶端上的資料。 Configuration Manager 提供完整的 BitLocker 生命週期管理，其可取代使用 Microsoft BitLocker Administration and Monitoring (MBAM)。 如需詳細資訊，請參閱[規劃 BitLocker 管理](../plan-design/bitlocker-management.md)。

- 在 Windows 10 裝置上使用 Windows Hello 企業版啟用替代的登入方法，而不是傳統密碼。 如需詳細資訊，請參閱 [Windows Hello 企業版設定](../deploy-use/windows-hello-for-business-settings.md)。

- 使用 VPN 設定檔啟用 VPN 連線，以降低使用者連線到資源的困難度。 如需詳細資訊，請參閱 [VPN 設定檔](../deploy-use/vpn-profiles.md)。  

- Wi-Fi 設定檔提供一組工具和資源，協助您管理組織裝置上的無線網路設定。 部署這些設定之後，使用者就可更為輕鬆地連線至無線網路。 如需詳細資訊，請參閱 [Wi-fi 設定檔](../deploy-use/create-wifi-profiles.md)。  

- 以使用者連線資源所需的憑證來佈建裝置。 如需詳細資訊，請參閱[憑證設定檔](../deploy-use/introduction-to-certificate-profiles.md)。  
