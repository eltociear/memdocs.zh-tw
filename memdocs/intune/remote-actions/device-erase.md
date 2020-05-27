---
title: 清除 macOS 裝置
titleSuffix: Microsoft Intune
description: 了解如何從 macOS 裝置清除包括作業系統在內的所有資料。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50575b1a4b19a6fbebb3fd904a471e19b070860e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989955"
---
# <a name="erase-all-data-from-a-macos-device"></a>清除 macOS 裝置的所有資料

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

您可以從 macOS 裝置清除包括作業系統在內的所有資料。 也會從 Intune 管理移除裝置。 使用者不會收到任何警告。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選擇 [裝置]   > [所有裝置]  > 選擇所要清除的裝置。
2. 按一下 [更多]   > [清除]  > 提供 6 位數的 [復原 PIN]  數值。 這是您必須提供給使用者的 pin，以便他們可以在自己的裝置上重新安裝作業系統。 請務必記下此 pin，因為清除動作完成後就看不到它。
![螢幕擷取畫面](./media/device-erase/providepin.png)
3. 按一下 [確定]  清除裝置。
