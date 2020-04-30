---
title: 針對 BitLocker 進行疑難排解
titleSuffix: Configuration Manager
description: 了解如何對 Configuration Manager 中的 BitLocker 管理問題進行疑難排解
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708606"
---
# <a name="troubleshoot-bitlocker"></a>針對 BitLocker 進行疑難排解

適用於：  Configuration Manager (最新分支)

您可以利用本文提供的資訊，對 Configuration Manager 中的 BitLocker 管理問題進行疑難排解。

## <a name="server-error-in-self-service"></a>自助服務中的伺服器錯誤

當您第一次嘗試開啟自助入口網站 (`https://webserver.contoso.com/SelfService`) 時，您會看到下列錯誤訊息：

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

若要修正此問題，請確定您已在 Web 伺服器上安裝 **Microsoft ASP.NET MVC 4.0** 的[必要條件](../../plan-design/bitlocker-management.md#prerequisites)。

## <a name="see-also"></a>請參閱

如需關於使用 BitLocker 事件記錄檔的詳細資訊，請參閱 [BitLocker 事件記錄檔](about-event-logs.md)。

如需事件記錄檔項目的已知錯誤和可能原因的清單，請參閱下列文章：

- [用戶端事件記錄檔](client-event-logs.md)
- [伺服器事件記錄檔](server-event-logs.md)

若要了解為什麼用戶端會報告不符合 BitLocker 管理原則的規範，請參閱[不符合規範代碼](non-compliance-codes.md)。
