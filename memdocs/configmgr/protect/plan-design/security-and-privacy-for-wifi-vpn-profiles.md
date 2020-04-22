---
title: Wi-Fi 和 VPN 設定檔的安全性和隱私權
titleSuffix: Configuration Manager
description: 了解管理 Configuration Manager 中裝置 Wi-Fi 和 VPN 設定檔的安全性管理建議。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705976"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 中的 Wi-Fi 和 VPN 設定檔安全性和隱私權

適用於：  Configuration Manager (最新分支)

## <a name="security-recommendations"></a>安全性建議

當您管理裝置的 Wi-Fi 和 VPN 設定檔時，請使用下列安全性最佳做法。

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>選擇 Wi-Fi 和 VPN 基礎結構以及用戶端作業系統能夠支援的最安全選項

Wi-Fi 和 VPN 設定檔提供便利的方法，集中散發及管理裝置已支援的 Wi-Fi 和 VPN 設定。 Configuration Manager 不會新增 Wi-Fi 或 VPN 功能。 識別、實作並遵循裝置和基礎結構的任何安全性建議。

## <a name="privacy-information"></a>隱私權資訊

您可以使用 Wi-Fi 和 VPN 設定檔來設定用戶端裝置，以連線到 Wi-Fi 和 VPN 伺服器。 然後使用 Configuration Manager 評估這些裝置在套用設定檔之後是否符合規範。 管理點會將相容性資訊傳到站台伺服器，且該資訊會存放在站台資料庫中。 當裝置將資訊傳送至管理點時，資訊已加密，但不會以加密格式儲存在站台資料庫內。 資料庫會保留資訊，直到站台維護工作 [刪除過時設定管理資料]  將它刪除為止。 預設的刪除間隔時間為 90 天，但此設定可以變更。 相容性資訊不會傳送給 Microsoft。

根據預設，裝置不會評估 Wi-Fi 和 VPN 設定檔。 此外，您必須設定設定檔，然後將其部署至使用者。  

設定 Wi-Fi 或 VPN 設定檔之前，請考慮您的隱私權需求。  
