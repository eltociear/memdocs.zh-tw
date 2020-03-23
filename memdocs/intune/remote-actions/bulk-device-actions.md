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
ms.openlocfilehash: 8c50f5495aa593dc8904fe6a9120ecd29de693ee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349143"
---
# <a name="use-bulk-device-actions"></a>使用大量裝置動作

您可以使用大量動作來進行下列遠端動作：
- [Autopilot 重設](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (機器翻譯)
- [自訂通知](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [刪除](devices-wipe.md#delete-devices-from-the-intune-portal)
- [重新命名](device-rename.md)
- [重新啟動](device-restart.md)
- [同步](device-sync.md)
- [抹除](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>使用大量裝置動作

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選擇 [裝置]   > [所有裝置]   > [大量裝置動作]  。
![大量裝置動作](./media/bulk-device-actions/bulk-device-actions.png)
3. 在 [大量裝置動作]  頁面上，選取 [OS]  和 [裝置動作]  。 有些裝置動作會有其他選項或需要填入的欄位。 選擇 [下一步]  。
4. 在 [裝置]  頁面上，選取 1 到 100 個裝置 > [下一步]  。
5. 在 [檢閱 + 建立]  頁面上，選取 [建立]  。

## <a name="next-steps"></a>後續步驟
[裝置管理概觀](device-management.md)。
