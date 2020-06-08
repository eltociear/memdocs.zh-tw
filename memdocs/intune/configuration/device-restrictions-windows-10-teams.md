---
title: Microsoft Intune 中的 Surface Hub Windows 10 團隊版裝置限制 - Azure | Microsoft Docs
titleSuffix: ''
description: 使用 Intune 來新增或設定執行 Windows 10 團隊版的 Surface Hub 裝置設定。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429679"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>使用 Intune 來允許或限制 Surface Hub 裝置功能的 Windows 10 團隊版設定

本文將說明所有的 Microsoft Intune 裝置限制設定，讓您可以為執行 Windows 10 團隊版的裝置進行設定，包括 Surface Hub 裝置。

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](device-restrictions-configure.md#create-the-profile)。

## <a name="apps-and-experience"></a>應用程式及體驗

這些設定使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **有人在房間時喚醒螢幕**：[封鎖] 會禁止在感應器偵測到房間內有人時自動喚醒螢幕。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **歡迎畫面上顯示的會議資訊**：選擇歡迎畫面會議磚上所顯示的資訊。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **僅限召集人和時間**
  - **召集人、時間和主旨 (私人會議會隱藏主旨)**
- **歡迎畫面背景影像 URL**：在 Windows 10 團隊版裝置上的**歡迎**畫面上，輸入您想要作為自訂背景的 .png 影像 URL。 影像必須是 PNG 格式，並且 URL 的開頭必須是 `https://`。
- **自動啟動 Connect**：[封鎖] 會禁止 Connect 應用程式在投影開始時自動開啟。 如果受到封鎖，使用者可以從中樞的設定手動啟動 Connect 應用程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **登入建議**：[封鎖] 會停用從已排程的會議中將受邀者自動填入登入對話方塊。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **我的會議與檔案**：[封鎖] 會停用 [開始] 功能表中的 [我的會議和檔案] 功能。 這項功能會顯示登入使用者的會議與 Office 365 檔案。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights**：[啟用] 會使用 Azure Operational Insights 來收集、儲存及分析來自 Windows 10 團隊版裝置的記錄資料。 Azure Operational Insights 是 Microsoft Operations Manager 套件的一部分。 輸入 [工作區識別碼] 和 [工作區金鑰] 以連線至 Azure Operational insights。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 不會收集此資料。

## <a name="maintenance"></a>維護

這些設定使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **更新的維護時段**：**啟用**可在安裝更新時建立維護時段。 輸入維護時段**開始時間**和**持續時間 (小時)** (1-5 小時)。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="session"></a>工作階段

這些設定使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **音量**：輸入新工作階段的預設音量值 (0-100)。 保留空白時，Intune 不會變更或更新此設定。 根據預設，OS 會將音量設為 45。
- **畫面逾時**：輸入關閉中樞畫面之前的分鐘數。
- **工作階段逾時**：輸入工作階段逾時之前的分鐘數。
- **睡眠逾時**：輸入中樞在進入睡眠模式之前的分鐘數。
- **工作階段繼續**：[封鎖] 會禁止使用者在工作階段逾時的時候繼續工作階段。當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="wireless-projection"></a>無線投影

這些設定使用 [SurfaceHub CSP](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp)。

- **無線投影的 PIN**：**需要**會強制使用者輸入 PIN，才能使用裝置上的無線投影功能。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **Miracast 無線投影**：[封鎖] 會禁止使用已啟用 Miracast 的裝置來投影。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **Miracast 無線投影通道**：選取要建立連線的 Miracast 通道。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱[如何設定裝置限制設定](device-restrictions-configure.md)。

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
