---
title: 適用於 Intune 之 Microsoft Defender 防毒軟體的 macOS 防毒軟體原則設定 | Microsoft Docs
description: 查看適用於 macOS 的 Microsoft Defender 防毒軟體設定檔中的設定清單。 此設定檔是 Microsoft Intune 中適用於 macOS 之端點安全性防毒軟體原則的一部分。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: 325460e4d487ade7337fc99b8a77fd3182d6cc17
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83430115"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Microsoft Intune 中適用於 Mac 的 Microsoft Defender ATP 設定

檢視您可以在 Microsoft Intune 中，為適用於 Mac 的 Microsoft Defender ATP 設定的*防毒軟體*設定檔設定。 如需這些設定的詳細資訊，請參閱 Windows 文件中的 [Mac 版 Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) \(部分機器翻譯\)。

了解如何在 Intune 中使用[端點安全性原則](../protect/endpoint-security-policy.md)。

**Microsoft Defender ATP**

- **即時保護**  
  要求 macOS 裝置上的 Defender 使用即時監視功能。 即時監視會找出惡意程式碼，並使其無法在您的裝置上安裝或執行。 您可以短時間關閉此設定，然後再自動重新開啟。

  - **未設定** (*預設*) - 此設定會還原為系統預設值
  - **已啟用** - 強制使用即時監視。 裝置使用者無法變更此設定。
  - **已停用** - 停用此設定。 裝置使用者無法變更此設定。

- **雲端提供的保護**  
  根據預設，Defender 會將所發現之任何問題的相關資訊傳送給 Microsoft。 Microsoft 會分析該資訊，以深入了解影響您與其他客戶的問題，並提供改善的解決方案。 當 [自動提交範例] 設定為開啟時，保護效果最佳。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **已啟用** - 開啟雲端提供的保護。 裝置使用者無法變更此設定。
  - **已停用** - 停用此設定。 裝置使用者無法變更此設定。

- **自動提交範例**  
  傳送樣本檔案給 Microsoft，以協助保護裝置使用者與您的組織免受潛在威脅的影響。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **已啟用** - 開啟雲端提供的保護。  裝置使用者無法變更此設定。
  - **已停用** - 停用此設定。 裝置使用者無法變更此設定。

- **診斷資料收集**

  設定如何與 Microsoft 共用診斷與使用狀況資料。

  - **未設定** (*預設*) - 此設定會還原為系統預設值。
  - **必要**
  - **選擇性**

- **要排除不予掃描的資料夾**  
  選取 [新增]，然後指定要在掃描期間忽略的資料夾。

- **已排除不予掃描的檔案**  
  選取 [新增]，然後指定要在掃描期間忽略的檔案。

- **要排除不予掃描的檔案類型**  
  選取 [新增]，然後指定要在掃描期間忽略的副檔名。

- **要排除不予掃描的處理序**  
  選取 [新增]，然後指定要在掃描期間忽略的處理序。
