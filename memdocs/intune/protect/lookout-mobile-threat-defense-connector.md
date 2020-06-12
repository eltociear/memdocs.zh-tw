---
title: 整合 Lookout Mobile Endpoint 與 Microsoft Intune
titleSuffix: Microsoft Intune
description: 深入了解整合 Intune 與 Lookout Mobile Threat Defense (MTD) 來控制行動裝置對公司資源的存取。
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1083e195cee20c3df9572db94395d462f9531a39
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330945"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Lookout Mobile Endpoint Security 連接器與 Intune

您可以根據由 Lookout (一個與 Microsoft Intune 整合的 Mobile Threat Defense 解決方案) 所進行的風險評估，來控制行動裝置對公司資源的存取。 風險評估是根據 Lookout 服務收集自裝置的遙測，包括︰
- 作業系統漏洞
- 安裝的惡意應用程式
- 惡意網路設定檔

您可以根據透過適用於註冊裝置的 Intune 相容性原則所啟用的 Lookout 風險評定來設定條件式存取原則，然後使用這些原則，以根據所偵測到威脅來允許或封鎖不相容的裝置存取公司資源。 針對未註冊的裝置，您可以使用應用程式保護原則，根據偵測到的威脅來強制執行封鎖或選擇性抹除。

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Intune 和 Lookout Mobile Endpoint Security 如何協助保護公司資源？

已在行動裝置上安裝和執行 Lookout 行動應用程式 (**Lookout for Work**)。 這個應用程式可擷取檔案系統、網路堆疊，以及裝置和應用程式遙測 (如果可用)，然後將其傳送至 Lookout 雲端服務，以評估裝置威脅的裝置風險。 您可以在 Lookout 主控台中變更威脅的風險層級分類，以符合您的需求。

- **支援已註冊的裝置** - Intune 裝置相容性原則包含行動威脅防護 (MTD) 規則，可使用 Lookout for Work 的風險評定資訊。 啟用 MTD 規則時，Intune 會評估裝置是否符合所啟用的原則。 如果發現裝置不相容，則會封鎖使用者對 Exchange Online 和 SharePoint Online 這類公司資源的存取。 使用者也會從安裝在其裝置內的 Lookout for Work 應用程式收到指導方針，以解決問題並重新取得公司資源的存取權。 若要支援搭配使用 Lookout for Work 與已註冊的裝置，請：
  - [將 MTD 應用程式新增至裝置](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [建立支援 MTD 的裝置合規性政策](../protect/mtd-device-compliance-policy-create.md)
  - [在 Intune 中啟用 MTD 連接器](../protect/mtd-connector-enable.md)

- **支援未註冊的裝置** - 當使用 Intune 應用程式保護原則時，Intune 可以在未註冊裝置上使用 Lookout for Work 應用程式中的風險評定資料。 系統管理員可以使用此組合來協助保護[受 Microsoft Intune 保護的應用程式](../apps/apps-supported-intune-apps.md)中的公司資料，也可以針對未註冊裝置上的公司資料發出封鎖或選擇性抹除。 若要支援搭配使用 Lookout for Work 與未註冊的裝置，請：
  - [將 MTD 應用程式新增至未註冊的裝置](../protect/mtd-add-apps-unenrolled-devices.md)
  - [建立行動威脅防禦應用程式保護原則](../protect/mtd-app-protection-policy.md)
  - [在 Intune 中針對未註冊的裝置啟用 MTD 連接器](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>支援的平台

在 Intune 中註冊時，Lookout 支援下列平台︰

- **Android 4.1 和更新版本**  
- **iOS 8 和更新版本**  

如需平台和語言支援的其他資訊，請前往 [Lookout 網站](https://personal.support.lookout.com/hc/articles/114094140253)。  

## <a name="prerequisites"></a>先決條件

- Lookout Mobile Endpoint Security 企業訂閱  
- Microsoft Intune 訂閱
- Azure Active Directory Premium
- Enterprise Mobility + Security (EMS) E3 或 E5，並具備指派給使用者的授權。  

如需詳細資訊，請參閱 [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="sample-scenarios"></a>範例案例

以下是搭配 Intune 使用 Mobile Endpoint Security 時的常見案例。

### <a name="control-access-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制存取權

在裝置上偵測到惡意應用程式 (例如惡意程式碼) 時，您可以在解決威脅之後封鎖裝置執行下列作業︰

- 連線到公司電子郵件
- 使用 OneDrive for Work 應用程式來同步處理公司檔案
- 存取公司應用程式

*於偵測到惡意應用程式時進行封鎖：*

> [!div class="mx-imgBorder"]
> ![因惡意應用程式而封鎖存取的原則概念影像](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*修復後允許存取：*

> [!div class="mx-imgBorder"]
> ![顯示補救後授與裝置存取權的概念影像](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>依據對網路的威脅性來控制存取

偵測到攔截式攻擊等網路威脅，並根據裝置風險保護 Wi-Fi 網路的存取。

*封鎖透過 Wi-Fi 的網路存取：*

> [!div class="mx-imgBorder"]
> ![顯示依據網路威脅來封鎖 WiFi 存取的影像](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*修復後允許存取：*

> [!div class="mx-imgBorder"]
> ![補救後允許存取的條件式存取概念影像](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>依據對網路的威脅來控制對 SharePoint Online 的存取

偵測您的網路威脅 (例如攔截式攻擊)，並依據裝置風險來防止同步處理公司的檔案。

*偵測到網路威脅時封鎖 SharePoint Online：*

> [!div class="mx-imgBorder"]
> ![封鎖存取 SharePoint Online 的概念影像](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*修復後允許存取：*

> [!div class="mx-imgBorder"]
> ![補救網路威脅後允許存取的概念影像](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>根據惡意應用程式的威脅來控制未註冊裝置存取權

當 Lookout 行動威脅防禦解決方案將裝置視為受感染時：
> [!div class="mx-imgBorder"]
> ![應用程式保護原則因偵測到惡意程式碼而封鎖](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

補救後授與存取權：

> [!div class="mx-imgBorder"]
> ![應用程式保護原則的補救後授與存取權](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>後續步驟

您必須執行下列主要步驟來實作這個解決方案：

- [設定 Lookout 整合](lookout-mtd-connector-integration.md)
- [在 Intune 中啟用 Mobile Endpoint Security](mtd-connector-enable.md)
- [新增並指派 Lookout for Work 應用程式](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [設定 Lookout 裝置合規性原則](mtd-device-compliance-policy-create.md)
- [建立 MTD 應用程式保護原則](mtd-app-protection-policy.md)
