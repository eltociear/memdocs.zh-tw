---
title: 搭配 Intune 使用的 Better Mobile Threat Defense 連接器
titleSuffix: Intune on Azure
description: 設定搭配 Intune 使用的 Better Mobile Threat Defense 連接器。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: beb1f8c287e952726c0ba929b49496c16599fe08
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990431"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>搭配 Intune 使用的 Better Mobile Threat Defense 連接器

您可以根據由 Better Mobile (與 Microsoft Intune 整合的 Mobile Threat Defense (MTD) 解決方案) 所進行的風險評量，使用條件式存取來控制行動裝置對公司資源的存取。 風險是根據從執行 Better Mobile 應用程式之裝置所收集的遙測來評定的。

您可以根據透過適用於註冊裝置的 Intune 裝置相容性原則所啟用 Better Mobile 風險評定以設定條件式存取原則，然後使用這些原則，根據所偵測到威脅來允許或封鎖不相容的裝置存取公司資源。 針對未註冊的裝置，您可以使用應用程式保護原則，根據偵測到的威脅來強制執行封鎖或選擇性抹除。

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Intune 和 Better Mobile 如何協助保護您的公司資源？

已在行動裝置上安裝並執行 Better Mobile 應用程式。 這個應用程式可擷取檔案系統、網路堆疊，以及裝置和應用程式遙測 (如果可用)，然後將資料傳送到 Better Mobile 雲端服務，以評估裝置的行動威脅風險。

- **支援已註冊的裝置** - Intune 裝置合規性政策包含行動威脅防禦 (MTD) 規則，可使用來自 Better Mobile 的風險評定資訊。 啟用 MTD 規則時，Intune 會評估裝置是否符合所啟用的政策。 如果發現裝置不相容，則會封鎖使用者對 Exchange Online 和 SharePoint Online 這類公司資源的存取。 使用者也會從安裝在其裝置內的 Better Mobile 應用程式收到指導方針，以解決問題並重新取得公司資源的存取權。 支援搭配已註冊的裝置使用 Better Mobile：
  - [將 MTD 應用程式新增至裝置](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [建立支援 MTD 的裝置合規性政策](../protect/mtd-device-compliance-policy-create.md)
  - [在 Intune 中啟用 MTD 連接器](../protect/mtd-connector-enable.md)

- **支援未註冊的裝置** - 當使用 Intune 應用程式保護政策時，Intune 可以在未註冊裝置上使用 Better Mobile 應用程式中的風險評定資料。 系統管理員可以使用此組合來協助保護[受 Microsoft Intune 保護應用程式](../apps/apps-supported-intune-apps.md)中的公司資料，也可以針對未註冊裝置上的公司資料發出封鎖或選擇性抹除。 支援搭配未註冊的裝置使用 Better Mobile：
  - [將 MTD 應用程式新增至未註冊的裝置](../protect/mtd-add-apps-unenrolled-devices.md)
  - [建立行動威脅防禦應用程式保護原則](../protect/mtd-app-protection-policy.md)
  - [在 Intune 中針對未註冊的裝置啟用 MTD 連接器](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>支援的平台

- **Android 4.1 和更新版本**

- **iOS 8.0 及更新版本**

## <a name="prerequisites"></a>先決條件

- Azure Active Directory Premium

- Microsoft Intune 訂閱

- Better Mobile Threat Defense 訂用帳戶

  - 如需詳細資訊，請參閱 [Better Mobile 網站](https://www.better.mobi/)。

## <a name="sample-scenarios"></a>範例案例

以下是一些常見案例。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制存取權

在裝置上偵測到惡意應用程式 (例如惡意程式碼) 時，您可在解決威脅之前封鎖裝置執行下列動作：

- 連線到公司電子郵件

- 使用 OneDrive for Work 應用程式來同步處理公司檔案

- 存取公司應用程式

於偵測到惡意應用程式時進行封鎖：

![顯示偵測到惡意應用程式的影像](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

補救後授與存取權：

![偵測到惡意應用程式後授與存取](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>依據對網路的威脅性來控制存取

偵測到**攔截式攻擊**等網路威脅，並根據裝置風險保護 Wi-Fi 網路的存取。

封鎖透過 Wi-Fi 的網路存取：

![封鎖透過 Wi-Fi 的網路存取](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

補救後授與存取權：

![顯示修復後授與存取權的影像](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>依據對網路的威脅來控制對 SharePoint Online 的存取

偵測到**攔截式攻擊**等網路威脅，並根據裝置風險防止同步處理公司檔案。

偵測到網路威脅時封鎖 SharePoint Online：

![偵測到網路威脅時封鎖 SharePoint Online](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

補救後授與存取權：

![Sharepoint 的補救後授與存取範例](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制未註冊裝置其存取權

當 BETTER 行動威脅防禦解決方案將裝置視為受感染時：![應用程式保護原則因偵測到惡意程式碼而封鎖](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

補救後授與存取權：

![應用程式保護原則的補救後授與存取權](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>後續步驟

- [整合 Better Mobile 與 Intune](better-mobile-mtd-connector-integration.md)

- [設定 Better Mobile 應用程式](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [建立 Better Mobile 裝置合規性原則](mtd-device-compliance-policy-create.md)

- [啟用 Better Mobile MTD 連接器](mtd-connector-enable.md)

- [建立 MTD 應用程式保護原則](mtd-app-protection-policy.md) 
