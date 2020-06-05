---
title: 包含檔案
description: 包含檔案
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347237"
---
## <a name="apple-device-network-information"></a>Apple 裝置網路資訊

|**使用對象**|**主機名稱 (IP 位址/子網路)**|**通訊協定**|**連接埠**|
|------------|-----------|------------|-----------|
|擷取並顯示來自 Apple 伺服器的內容|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|與 APNS 伺服器通訊|#-courier.push.apple.com<br>'#' 是從 0 至 50 的隨機數字。|TCP|5223 和 443|
|各種功能，包括存取網際網路、iTunes store、macOS App Store、iCloud、傳訊等。|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 或 443|

如需詳細資訊，請參閱：

- [Apple 軟體產品使用的 TCP 和 UDP 埠](https://support.apple.com/HT202944)
- [關於 macOS、iOS/iPadOS 和 iTunes 伺服器主機連線與 iTunes 背景處理序](https://support.apple.com/HT201999)
- [如果 macOS 和 iOS/iPadOS 用戶端無法取得 Apple 推播通知](https://support.apple.com/HT203609)