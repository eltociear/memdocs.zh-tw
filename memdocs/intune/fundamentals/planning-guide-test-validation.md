---
title: Intune 測試與驗證
titleSuffix: Microsoft Intune
description: 如何在您的環境中測試及驗證 Intune 僅雲端解決方案。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 3/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4f82ee0c-4bd6-4623-9b10-9249d316ccf5
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: aeca72af3eadf55174f1ad97c1e294f48f131801
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79357229"
---
# <a name="intune-testing-and-validation"></a>Intune 測試與驗證

在測試 Microsoft Intune 的實作時，請考慮功能驗證及使用案例驗證。 功能驗證包含測試每個元件和設定，以判斷是否正確運作。 使用案例驗證包含測試以驗證涉及一系列工作的案例會如預期般運作。 

建議您在測試階段納入 IT 支援和技術服務人員，以便建立支援文件，讓 IT 支援和技術服務人員熟悉支援產品。 如果元件或案例無法根據使用案例運作，請務必記錄必要的變更，並包含進行變更的原因。

## <a name="before-you-begin"></a>開始之前

建議您記錄下列各項：

- **測試準則：** 找出測量的測試基準。

- **設計元件：** 至少必須存在於一項測試準則中。

如果設計元件不存在於至少符合需求或案例的一項測試準則中，請考慮設計元件是否為必要。 此外，請確定擁有下列項目︰

- **帳戶：** 有 EMS 和 Office 365 授權可測試所有使用案例的測試帳戶。

- **裝置：** 可以抹除或重設為原廠預設值的測試裝置。

- **整合元件：** 如有需要，應該安裝並設定所有的整合元件 (憑證連接器及 Intune Exchange 內部部署連接器)。

您可能需要設計變更，以備處理無法預見的問題。 此外，所有的設計變更都應該詳細記錄每項變更的原因。 下例示範可能的變更︰

<blockquote>您知道自己不符合網路裝置註冊服務 (NDES) 的需求，也了解可以使用根 CA 設定 VPN 和 Wi-Fi 設定檔，在不實作 NDES 的情況下滿足相同需求。</blockquote>

在測試和驗證過程中，您可能會遇到需要技術指導或特定疑難排解的困難或問題。 建議您透過 Microsoft 支援管道尋求協助。

- [如何取得 Microsoft Intune 的管理支援](get-support.md)

- [Microsoft Intune 的連絡電話協助支援](get-support.md)

## <a name="functional-validation-testing"></a>功能驗證測試

功能驗證包含測試每個元件和設定，以判斷是否正確運作。 下表有驗證測試範例。

![第 9 節表 1](./media/planning-guide-test-validation/section-9-image-1-table.PNG)

## <a name="use-case-validation-testing"></a>使用案例驗證測試

執行使用案例驗證測試，以確認案例都完整且運作正常。 使用案例有兩種類型：IT 管理員和使用者。

### <a name="it-admin"></a>IT 管理員

執行 IT 管理員驗證測試，以驗證對裝置或使用者功能執行的管理動作正確無誤。 下例是 IT 管理員的端對端驗證案例。

![第 9 節表 2](./media/planning-guide-test-validation/section-9-image-2-table.PNG)

### <a name="end-user"></a>終端使用者

執行使用者驗證測試，以確認所有使用者通訊中的使用者體驗都能如預期正確呈現。 請務必確認使用者體驗正確無誤。 如果無法確認，它可能會導致採用率較低以及較大量的技術服務人員呼叫。

![第 9 節表 3](./media/planning-guide-test-validation/section-9-image-3-table.PNG)

## <a name="next-steps"></a>後續步驟

現在您已測試並驗證您的 Intune 功能和使用案例，因此可以[推出 Intune 產品](planning-guide-rollout-plan.md)。

如需更多規劃範本和資訊，請參閱[其他資源](planning-guide-resources.md)。
