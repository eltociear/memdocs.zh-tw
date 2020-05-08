---
title: 在 Microsoft Intune 中監視裝置合規性原則 - Azure | Microsoft Docs
description: 使用裝置相容性儀表板來監視整體裝置相容性、檢視報表，以及逐條原則與逐項設定地檢視裝置相容性。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f85a8ffc81aa91bce09d6a76eeb5a52335d8b23
ms.sourcegitcommit: dda5e6f00f79737348e850d971f15fc3093d6431
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82745193"
---
# <a name="monitor-intune-device-compliance-policies"></a>監視 Intune 裝置合規性政策

更新狀態報告可協助您檢閱裝置合規性，並針對組織內的合規性相關問題進行疑難排解。 您可以使用這些報告來檢視下列相關資訊：

- 裝置的整體合規性狀態
- 個別設定的合規性狀態
- 個別政策的合規性狀態
- 深入細探個別裝置，檢視影響裝置的特定設定和政策

## <a name="open-the-compliance-dashboard"></a>開啟合規性儀表板

開啟 [Intune 裝置合規性儀表板]  ：

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [概觀]   > [合規性狀態]  索引標籤。

> [!IMPORTANT]
> 裝置必須在 Intune 註冊才能接收裝置合規性政策。

## <a name="dashboard-overview"></a>儀表板概觀

當儀表板開啟時，您可以取得所有更新狀態報告的概觀。 在這些報告中，您可以查看並檢查：

- 整體裝置合規性
- 每一政策的裝置合規性
- 每一設定的裝置合規性
- 威脅代理程式狀態
- 裝置保護狀態

![儀表板影像顯示裝置合規性儀表板和不同的報告](./media/compliance-policy-monitor/idc-1.png)

當您鑽研此報告時，您也可能會看到套用至特定裝置的任何特定合規性政策和設定，包括每個設定的合規性狀態。

### <a name="device-compliance-status"></a>裝置合規性狀態

[裝置合規性狀態]  圖表會顯示所有 Intune 已註冊裝置的合規性狀態。 裝置合規性狀態會保留在兩個不同的資料庫中：Intune 和 Azure Active Directory。

> [!IMPORTANT]
> Intune 會遵循裝置簽入排程，以符合裝置上的所有合規性評估。 [深入了解裝置簽入排程](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)。

不同裝置合規性政策狀態的說明如下：

- **符合規範**：裝置已成功套用一或多個裝置合規性政策設定。

- **在寬限期內︰** 裝置是以一或多個裝置合規性政策設定為目標。 但使用者尚未套用政策。 這表示裝置不符合規範，但仍在管理員定義的寬限期內。

  - 深入了解[對不符合規範之裝置所要採取的動作](actions-for-noncompliance.md)。

- **未評估**：新註冊之裝置的初始狀態。 此狀態的其他可能原因包括：

  - 裝置未獲指派合規性政策，且沒有可檢查合規性之觸發程序
  - 裝置自上次更新合規性政策後就未曾簽入
  - 裝置未與特定使用者建立關聯，例如：
    - 透過不具使用者親和性的 Apple 裝置註冊計劃 (DEP) 所購買 iOS/iPadOS 裝置
    - Android kiosk 或 Android Enterprise 專用裝置
  - 裝置使用裝置註冊管理員 (DEM) 帳戶註冊

- **不符合規範︰** 裝置無法套用一或多個裝置合規性政策設定。 或者，使用者尚未符合政策規範。

- **裝置未同步處理︰** 裝置無法報告其裝置合規性政策狀態，原因為下列其中之一：

  - **不明**：裝置已離線或因為其他原因無法與 Intune 或 Azure AD 通訊。

  - **錯誤**：裝置無法與 Intune 和 Azure AD 通訊，並收到錯誤訊息和原因。

> [!IMPORTANT]
> 已在 Intune 註冊但未鎖定任何裝置相容性原則目標的裝置，會納入此報表中的 [相容]  值區之下。

#### <a name="drill-down-for-more-details"></a>深入細探以取得更多詳細資料

在 [裝置合規性狀態]  圖表中，選取一個狀態。 例如，選取 [不符合規範]  狀態：

![選擇 [不符合規範] 狀態](./media/compliance-policy-monitor/select-not-compliant-status.png)

該動作會開啟 [裝置合規性]  視窗，並在 [裝置狀態]  圖表中顯示裝置。 此圖表會顯示處於該狀態的裝置詳細資料，包括作業系統平台、上次簽入日期等。
![儀表板影像顯示該特定狀態之裝置的更多詳細資料](./media/compliance-policy-monitor/drill-down-details.png)

如果您想要查看特定使用者擁有的所有裝置，您也可以輸入使用者的電子郵件來篩選圖表報告。

> [!TIP]
> 若沒有使用者登入裝置，則具備目標裝置合規性政策的裝置就會將合規性報告傳送回 Intune，顯示**系統帳戶**作為使用者主體名稱。 發生這種情況的原因是裝置合規性政策已瞄準使用者群組或裝置群組，但在評估合規性政策時沒有任何使用者登入裝置。
>
> 此外，若有多名使用者登入相同的裝置，且在巧合情況下裝置瞄準了範圍涵蓋所有目前登入裝置使用者的合規性政策，則合規性報告可能會顯示相同的裝置多次，因為每一名登入裝置的使用者都必須評估裝置合規性政策並將其報告回 Intune。

#### <a name="filter-and-columns"></a>篩選和資料行

![選取 [篩選] 和 [資料行] 以變更圖表中的結果](./media/compliance-policy-monitor/filter-columns.png)

當選取 [篩選]  按鈕時，[篩選] 快顯視窗隨即開啟並顯示更多選項，包括 [合規性]  狀態、[破解]  的裝置等。 **套用**篩選以更新結果。

使用 [資料行]  屬性在圖表輸出中新增或移除資料行。 例如，[使用者主體名稱]  可能顯示裝置上註冊的電子郵件地址。 **套用**資料行以更新結果。

#### <a name="device-details"></a>裝置詳細資訊

在 [裝置詳細資料]  圖表內，選取特定裝置，然後選取 [裝置合規性]  ：

![選擇特定裝置，然後選擇 [裝置合規性] 以查看套用的合規性政策](./media/compliance-policy-monitor/see-policies-applied-specific-device.png)

Intune 會顯示該裝置上所套用裝置合規性原則設定的詳細資料。 當您選取特定政策時，它會顯示該政策中的所有設定。

### <a name="devices-without-compliance"></a>沒有合規性的裝置

在 [合規性狀態]  頁面上的 [原則合規性]  圖表旁，您可以選取 [沒有合規性原則的裝置]  磚，以針對未指派任何合規性原則的裝置檢視其相關資訊：

![查看沒有任何合規性政策的裝置](./media/compliance-policy-monitor/devices-without-policies.png)

當您選取磚時，它會顯示沒有合規性政策的所有裝置。 它也會顯示裝置的使用者、政策部署狀態和裝置型號。

#### <a name="what-you-need-to-know"></a>您必須知道的事項

- 使用 [將未指派合規性政策的裝置標記為]  安全性設定，請務必識別沒有合規性政策的裝置。 接著，您可以將至少一個合規性原則指派給這些裝置。

  您可以在 Intune 入口網站中設定安全性設定。 請移至 [裝置]   > [合規性原則]   > [合規性原則設定]  。 接著，將 [將未指派合規性政策的裝置標記為]  設定為 [符合規範]  或 [不符合規範]  。

  深入了解 [Intune 服務中的安全性增強功能](https://blogs.technet.microsoft.com/intunesupport/2018/02/09/updated-upcoming-security-enhancements-in-the-intune-service/) \(英文\)。

- 使用者如果已獲指派任何類型的合規性政策，便不會出現在此報告中，不論是使用哪一種裝置平台。 例如，如果您已將 Windows 合規性政策指派給具有 Android 裝置的使用者，該裝置便不會出現在此報告中。 不過，Intune 會將該 Android 裝置視為不符合規範。 為了避免發生問題，建議您針對每個裝置平台建立原則，然後將它們部署至所有使用者。

### <a name="per-policy-device-compliance"></a>每一政策的裝置合規性

[原則合規性]  圖表會顯示原則，以及符合規範與不符合規範的裝置數目。

![查看政策清單，以及該政策中符合規範的裝置數目與不符合規範的裝置數目比較](./media/compliance-policy-monitor/idc-8.png)

### <a name="setting-compliance"></a>設定合規性

[設定合規性]  圖表會顯示所有合規性原則中的所有裝置合規性原則設定、套用原則設定的平台，以及不符合規範的裝置數目。

![查看不同政策中的所有設定清單](./media/compliance-policy-monitor/idc-10.png)

## <a name="view-compliance-reports"></a>檢視合規性報告

除了使用圖表上的 [合規性狀態]  ，您也可以移至 [報告]   > [裝置合規性]  。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [監視]  ，然後在 [合規性]  下方選取您想要檢視的報告。 一些可用的合規性報告包括：

   - 裝置相容性
   - 不符合規範的裝置
   - 沒有合規性政策的裝置
   - 設定合規性
   - 原則合規性
   - Windows 健康情況證明報表
   - 威脅代理程式狀態

如需報告的詳細資訊，請參閱 [Intune 報告](../fundamentals/reports.md)

## <a name="view-status-of-device-policies"></a>檢視裝置原則狀態

您可以依平台檢查原則的不同狀態。 例如，您有一個 macOS 合規性原則。 您希望查看受此原則影響的裝置，並了解是否存在衝突或失敗。

這項功能包含在裝置狀態報告中：

1. 選取 [裝置]   > [合規性原則]   > [原則]  。 會顯示原則清單，包括平台 (如果已指派原則) 以及更多詳細資料。
2. 選取一個原則 > [概觀]  ： 在此檢視中，原則指派會包含下列狀態：

    - **成功**：已套用原則
    - **錯誤**：原則無法套用。 訊息通常會顯示一個用來連結至說明的錯誤碼。
    - **衝突**：兩個設定會套用至相同的裝置，且 Intune 無法解決衝突。 系統管理員應該檢閱。
    - **Pending**：裝置尚未使用 Intune 簽入以接收政策。
    - **不適用**：裝置無法接收原則。 例如，該原則更新了 iOS 11.1 的特定設定，但該裝置使用的是 iOS 10。

3. 若要在使用此原則的裝置上查看詳細資料，請選取其中一個狀態。 例如，選取 [成功]  。 在下一個視窗中會列出特定裝置詳細資料，包括裝置名稱與部署狀態。

## <a name="how-intune-resolves-policy-conflicts"></a>Intune 如何解決原則衝突

將多項 Intune 原則套用至一部裝置時，可能會發生原則衝突。 如果原則設定重疊，Intune 會使用下列規則解決任何衝突︰

- 若衝突的設定來自 Intune 設定原則與合規性原則，合規性原則中的設定仍優先於設定原則中的設定。 即使設定原則中的設定更為安全亦然。

- 若您已部署多項合規性原則，Intune 會使用其中最安全的原則。

## <a name="next-steps"></a>後續步驟

[合規性政策概觀](device-compliance-get-started.md)
