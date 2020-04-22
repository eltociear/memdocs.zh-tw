---
title: 在 Microsoft Intune 裝置中使用大量裝置動作。
titleSuffix: ''
description: 使用大量遠端裝置動作。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f33198e71fd4250ee93207e571bc535abd1c95f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325375"
---
# <a name="use-bulk-device-actions"></a>使用大量裝置動作

您可以使用大量動作來進行下列遠端動作：
- [Autopilot 重設](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [自訂通知](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [刪除](devices-wipe.md#delete-devices-from-the-intune-portal)
- [重新命名](device-rename.md)
- [重新啟動](device-restart.md)
- [同步](device-sync.md)
- [抹除](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>使用大量裝置動作

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選擇 [裝置]   > [所有裝置]   > [大量裝置動作]  。
![大量裝置動作](./media/bulk-device-actions/bulk-device-actions.png)
3. 在 [大量裝置動作]  頁面上，選取 [OS]  和 [裝置動作]  。 有些裝置動作會有其他選項或需要填入的欄位。 選擇 **[下一步]** 。
4. 在 [裝置]  頁面上，選取 1 到 100 個裝置 > [下一步]  。
5. 在 [檢閱 + 建立]  頁面上，選取 [建立]  。

## <a name="next-steps"></a>後續步驟
[裝置管理概觀](device-management.md)。
