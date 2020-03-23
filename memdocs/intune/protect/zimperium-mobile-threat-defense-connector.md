---
title: 搭配 Intune 使用的 Zimperium MTD 連接器
titleSuffix: Intune on Azure
description: 深入了解整合 Intune 與 Zimperium Mobile Threat Defense 來控制行動裝置對公司資源的存取。
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
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed623abeb602e599866af7b7249756edd87d5a29
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349195"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>搭配 Intune 使用的 Zimperium Mobile Threat Defense 連接器

您可以根據由 Zimperium (與 Microsoft Intune 整合的 Mobile Threat Defense (MTD) 解決方案) 所進行的風險評量，使用條件式存取來控制行動裝置對公司資源的存取。 風險是根據從執行 Zimperium 應用程式之裝置所收集的遙測來評定的。

您可以根據透過適用於註冊裝置的 Intune 裝置相容性原則所啟用的 Zimperium 風險評定來設定條件式存取原則，然後使用這些原則，以根據所偵測到威脅來允許或封鎖不相容的裝置存取公司資源。 針對未註冊的裝置，您可以使用應用程式保護原則，根據偵測到的威脅來強制執行封鎖或選擇性抹除。

## <a name="supported-platforms"></a>支援的平台

- **Android 4.1 和更新版本**

- **iOS 8 和更新版本**

## <a name="prerequisites"></a>先決條件

- Azure Active Directory Premium

- Microsoft Intune 訂閱

- Zimperium Mobile Threat Defense 訂用帳戶

  - 如需詳細資訊，請參閱 [Zimperium 網站](https://www.zimperium.com/zips-mobile-ips) \(英文\)。

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Intune 和 Zimperium 如何協助您保護您的公司資源？

適用於 Android 及 iOS/iPadOS 的 Zimperium 應用程式可擷取檔案系統、網路堆疊、裝置和應用程式遙測 (如果可用)，然後將遙測資料傳送至 Zimperium 雲端服務，以評定裝置的行動威脅風險。

- **支援已註冊的裝置** - Intune 裝置相容性原則包含行動防禦 (MTD) 規則，可使用 Zimperium 的風險評定資訊。 啟用 MTD 規則時，Intune 會評估裝置是否符合所啟用的原則。 如果發現裝置不相容，則會封鎖使用者對 Exchange Online 和 SharePoint Online 這類公司資源的存取。 使用者也會從安裝在其裝置內的 Zimperium 應用程式收到指導方針，以解決問題並重新取得公司資源的存取權。 支援搭配已註冊的裝置使用 Zimperium：
  - [將 MTD 應用程式新增至裝置](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [建立支援 MTD 的裝置相容性原則](../protect/mtd-device-compliance-policy-create.md)
  - [在 Intune 中啟用 MTD 連接器](../protect/mtd-connector-enable.md)

- **支援未註冊的裝置** - 當使用 Intune 應用程式保護原則時，Intune 可以在未註冊的裝置上使用 Zimperium 應用程式中風險評定資料。 系統管理員可以使用此組合來協助保護[受 Microsoft Intune 保護應用程式](../apps/apps-supported-intune-apps.md)中的公司資料，也可以針對未註冊裝置上的公司資料發出封鎖或選擇性抹除。 支援搭配未註冊的裝置使用 Zimperium：
  - [將 MTD 應用程式新增至未註冊的裝置](../protect/mtd-add-apps-unenrolled-devices.md)
  - [建立行動威脅防禦應用程式保護原則](../protect/mtd-app-protection-policy.md)
  - [在 Intune 中針對未註冊的裝置啟用 MTD 連接器](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>範例案例

下方有一些案例可供您在將 Zimperium 與 Intune 整合時參考：

### <a name="control-access-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制存取權

在裝置上偵測到惡意應用程式 (例如惡意程式碼) 時，您可以封鎖裝置，直到解決威脅為止︰

- 連線到公司電子郵件

- 使用 OneDrive for Work 應用程式來同步處理公司檔案

- 存取公司應用程式

*於偵測到惡意應用程式時進行封鎖：*

> [!div class="mx-imgBorder"]
> ![偵測到惡意應用程式的概念影像](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*修復後允許存取：*

> [!div class="mx-imgBorder"]
> ![補救後授與存取權的概念影像](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>依據對網路的威脅性來控制存取

偵測網路中的「攔截式攻擊」  等威脅，並根據裝置風險保護對 Wi-Fi 網路的存取。

*封鎖透過 Wi-Fi 的網路存取︰*

> [!div class="mx-imgBorder"]
> ![封鎖透過 Wi-Fi 的網路存取](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*修復後允許存取：*

> [!div class="mx-imgBorder"]
> ![補救後授與存取權](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>依據對網路的威脅來控制對 SharePoint Online 的存取

偵測網路中的「攔截式攻擊」  等威脅，並根據裝置風險防止對公司檔案進行同步處理。

*偵測到網路威脅時封鎖 SharePoint Online：*

> [!div class="mx-imgBorder"]
> ![偵測到網路威脅時封鎖 SharePoint Online](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*修復後允許存取：*

> [!div class="mx-imgBorder"]
> ![Sharepoint 的補救後授與存取權範例](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制未註冊裝置存取權

當 Zimperium 行動威脅防禦解決方案將裝置視為受感染時：

> [!div class="mx-imgBorder"]
> ![應用程式保護原則因偵測到惡意程式碼而封鎖](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

補救後授與存取權：

> [!div class="mx-imgBorder"]
> ![應用程式保護原則的補救後授與存取權](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>後續步驟

- [將 Zimperium 與 Intune 整合](zimperium-mtd-connector-integration.md)

- [設定 Zimperium 應用程式](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [建立 Zimperium 裝置合規性政策](mtd-device-compliance-policy-create.md)

- [啟用 Zimperium MTD 連接器](mtd-connector-enable.md)

- [建立 MTD 應用程式保護原則](../protect/mtd-app-protection-policy.md)
