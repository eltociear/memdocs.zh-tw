---
title: 使用 Microsoft Intune 來管理裝置 - Azure | Micrososft Docs
description: 檢閱您使用 Microsoft Intune 來管理的裝置，包括將裝置清單匯出成 CSV 格式、檢視已加入 Azure Active Directory 的裝置、檢閱裝置上的動作變更記錄、使用「TeamViewer 連接器」以允許 IT 系統管理員從遠端對 Android 裝置進行疑難排解，以及檢視您可在裝置上執行的所有動作。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d2412418-d91a-4767-a3d6-bc88bb29caa2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98451e7ffd6aef9e5fb298af96b91074f39c383e
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325276"
---
# <a name="what-is-microsoft-intune-device-management"></a>什麼是 Microsoft Intune 裝置管理？

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

身為 IT 系統管理員，您必須確保受控裝置為使用者提供執行其工作所需的資源，同時保護該資料遠離風險。

**裝置**工作負載可供深入了解所管理的裝置，並讓您在這些裝置上啟動遠端工作。

## <a name="get-to-your-devices"></a>移至您的裝置

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
3. 選取 [裝置]  。 此檢視會顯示有關個別裝置的詳細資訊，以及它們各有哪些功能，包括：

   - [概觀]  會顯示已註冊裝置的視覺化快照集、有多少裝置使用不同的平台等。
   - [所有裝置]  會顯示您所管理的已註冊裝置清單。

     使用 [匯出]  功能來建立所有裝置的 .zip 清單，增量單位為 10,000 (Internet Explorer) 或 30,000 (Microsoft Edge、Chrome)。

     選取任一裝置來[檢視該裝置的其他詳細資料](device-inventory.md)，例如硬體詳細資料、已安裝的應用程式、原則等。

   - [Azure AD 裝置]  會顯示已向 Azure Active Directory (Azure AD) 註冊或已加入 Azure AD 的裝置清單。 深入了解 [Azure AD 裝置管理](https://docs.microsoft.com/azure/active-directory/device-management-introduction)。
   - [裝置動作]  包含在不同裝置上所執行遠端動作的歷程記錄，包括動作、其狀態、啟動動作的人員及時間。

     ![監視裝置動作的螢幕擷取畫面](./media/device-management/monitor-device-actions.png)

   - [稽核記錄]  是在 Intune 中產生變更之活動的記錄。 [稽核記錄](../fundamentals/monitor-audit-logs.md) 可提供更多詳細資料。
   - [TeamViewer 連接器]  是一項服務，可讓 Intune 所管理 Android 裝置的使用者從其 IT 系統管理員處取得遠端協助。 深入了解 [TeamViewer](teamviewer-support.md)。
   - [說明及支援]  提供有關疑難排解提示、要求支援或檢查 Intune 的捷徑。

## <a name="available-device-actions"></a>可執行的裝置動作
可用的動作取決於裝置平台和裝置設定。

- [檢視裝置清查](device-inventory.md)
- 執行遠端裝置動作：
  - [Autopilot 重設](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
  - [BitLocker 金鑰輪替](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) (僅限 Windows)
  - [刪除](devices-wipe.md#delete-devices-from-the-intune-portal)
  - [停用啟用鎖定](device-activation-lock-disable.md) (僅限 iOS)
  - [全新開始](device-fresh-start.md) (僅限 Windows)
  - [完整掃描](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (僅限 Windows 10)
  - [尋找裝置](device-locate.md) (僅限 iOS)
  - [遺失模式](device-lost-mode.md) (僅限 iOS)
  - [快速掃描](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (僅限 Windows 10)
  - [Android 遠端控制](teamviewer-support.md)
  - [遠端鎖定](device-remote-lock.md)
  - [重新命名裝置](device-rename.md)
  - [重設密碼](device-passcode-reset.md)
  - [重新啟動](device-restart.md) (僅限 Windows)
  - [淘汰](devices-wipe.md#retire)
  - [更新 Windows Defender 安全情報](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus)
  - [重設 Windows 10 的 PIN 碼](device-windows-pin-reset.md)
  - [抹除](devices-wipe.md#wipe)
  - [傳送自訂通知](custom-notifications.md#send-a-custom-notification-to-a-single-device) (Android、iOS/iPadOS)
  - [同步裝置](device-sync.md)
- [大量裝置動作](bulk-device-actions.md)

## <a name="next-steps"></a>後續步驟

- 在 [所有裝置]  中，選取裝置以檢視有關該特定裝置的更多詳細資料。
- 選擇 [裝置動作]  查看您管理的裝置上所執行動作的狀態。
