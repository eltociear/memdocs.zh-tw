---
title: 搭配 Intune 使用的 Pradeo Mobile Threat Defense 連接器
titleSuffix: Intune on Azure
description: 深入了解如何將 Intune 與 Pradeo Mobile Threat Defense 連接器整合，以控制行動裝置對您公司資源的存取權。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a23155c31586992c82781998bb664bf2ce6a0889
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339172"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>搭配 Intune 使用的 Pradeo Mobile Threat Defense 連接器

您可以根據由 Pradeo (與 Microsoft Intune 整合的 Mobile Threat Defense (MTD) 解決方案) 所進行的風險評量，使用條件式存取來控制行動裝置對公司資源的存取。 風險是根據從執行 Pradeo 應用程式之裝置所收集的遙測來評定的。

您可以根據透過 Intune 裝置合規性政策所啟用的 Pradeo 風險評量，來設定條件式存取原則，而您可以根據偵測到的威脅，使用它們來允許或封鎖不符合規範的裝置存取公司資源。

> [!NOTE]
> 此 Mobile Threat Defense 廠商不支援尚未註冊的裝置。

## <a name="supported-platforms"></a>支援的平台

- **Android 4.0.3 及更新版本**

- **iOS 7 及更新版本**

## <a name="prerequisites"></a>必要條件

- Azure Active Directory Premium

- Microsoft Intune 訂閱

- 適用於 Mobile Threat Defense 的 Pradeo Security 訂閱

  - 如需詳細資訊，請參閱 [Pradeo 網站](https://www.pradeo.com/en-US/mobile-threat-protection)。

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Intune 和 Pradeo 如何協助保護您的公司資源？

適用於 Android 及 iOS/iPadOS 的 Pradeo 應用程式可擷取檔案系統、網路堆疊、裝置和應用程式遙測 (如果可用)，然後將遙測資料傳送至 Pradeo 雲端服務，以評定裝置的行動威脅風險。

Intune 裝置合規性原則包含以 Pradeo 風險評定為基礎的 Pradeo Mobile Threat Defense 規則。 啟用此規則時，Intune 會評估裝置是否符合您啟用的原則。 如果發現裝置不相容，則會封鎖使用者對 Exchange Online 和 SharePoint Online 這類公司資源的存取。 使用者也會從安裝在其裝置內的 Pradeo 應用程式收到指導方針，以解決問題並重新取得公司資源的存取權。

## <a name="sample-scenarios"></a>範例案例

以下是一些常見案例。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制存取權

在裝置上偵測到惡意應用程式 (例如惡意程式碼) 時，您可在解決威脅之前封鎖裝置執行下列動作：

- 連線到公司電子郵件

- 使用 OneDrive for Work 應用程式來同步處理公司檔案

- 存取公司應用程式

*於偵測到惡意應用程式時進行封鎖：*

![偵測到惡意應用程式的概念影像](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*修復後允許存取：*

![偵測到惡意應用程式後授與存取](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>依據對網路的威脅性來控制存取

偵測到**攔截式攻擊**等網路威脅，並根據裝置風險保護 Wi-Fi 網路的存取。

*封鎖透過 Wi-Fi 的網路存取︰*

![封鎖透過 Wi-Fi 的網路存取](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*修復後允許存取：*

![修復後授與存取權的概念影像](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>根據網路威脅來控制 SharePoint Online 的存取權

偵測到**攔截式攻擊**等網路威脅，並根據裝置風險防止同步處理公司檔案。

*偵測到網路威脅時封鎖 SharePoint Online：*

![偵測到網路威脅時封鎖 SharePoint Online](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*修復後允許存取：*

![修復後授與存取權的概念影像 (SharePoint 範例)](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>後續步驟

- [整合 Pradeo 與 Intune](pradeo-mtd-connector-integration.md)

- [設定 Pradeo 應用程式](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [建立 Pradeo 裝置合規性原則](mtd-device-compliance-policy-create.md)

- [啟用 Pradeo MTD 連接器](mtd-connector-enable.md)
