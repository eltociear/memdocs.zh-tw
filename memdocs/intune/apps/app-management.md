---
title: 什麼是 Microsoft Intune 應用程式管理？
titleSuffix: ''
description: 了解各平台適用於 Microsoft Intune 的用戶端應用程式管理功能。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: baffa150b416b778e41a59fdf4e5a1b686cdae7b
ms.sourcegitcommit: 4381afb515c06f078149bd52528d1f24b63a2df9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82538146"
---
# <a name="what-is-microsoft-intune-app-management"></a>什麼是 Microsoft Intune 應用程式管理？


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

身為 IT 系統管理員，您可以使用 Microsoft Intune 來管理公司員工使用的用戶端應用程式。 而這項功能還可以用於管理裝置與保護資料。 系統管理員最優先的事項之一，是確保終端使用者能夠存取工作所需的應用程式。 這個目標不易達成，因為：
- 裝置平台及應用程式類型有千百種。
- 您可能需要同時管理公司裝置和使用者個人裝置上的應用程式。
- 您必須確保網路和資料的安全。

此外，您也可能需要指派及管理未向 Intune 註冊之裝置上的應用程式。

## <a name="mobile-application-management-mam-basics"></a>行動應用程式管理 (MAM) 基本概念

[Intune 行動應用程式管理](app-lifecycle.md)指的是 Intune 管理功能套件，可讓您針對您的使用者發行、推送、設定、保護、監視與更新行動應用程式。

MAM 可讓您管理和保護應用程式內的組織資料。 透過**沒有註冊的 MAM** (MAM-WE)，幾乎可在任何[裝置](app-management.md#app-management-capabilities-by-platform) (包括**攜帶您自己的裝置** (BYOD) 案例中的個人裝置) 上管理包含敏感性資料的公司或學校相關應用程式。 許多生產力應用程式 (例如 Microsoft Office 應用程式) 可以由 Intune MAM 管理。 請參閱可供公開使用的 [Microsoft Intune 受保護應用程式](apps-supported-intune-apps.md)官方清單。

Intune MAM 支援兩個組態︰
- **Intune MDM + MAM**：IT 系統管理員只能管理已在 Intune 行動裝置管理 (MDM) 註冊之裝置上使用 MAM 與應用程式保護原則的應用程式。 若要使用 MDM + MAM 管理應用程式，客戶應該在 Azure 入口網站中使用 Intune 主控台，網址為 [https://portal.azure.com](https://portal.azure.com )。
- **不需註冊裝置的 MAM**：不需註冊裝置的 MAM (或 MAM-WE) 允許 IT 系統管理員管理未在 Intune MDM 註冊之裝置上使用 MAM 與應用程式保護原則的應用程式。 這表示應用程式可由向協力廠商 EMM 提供者註冊之裝置上的 Intune 來管理。 若要使用 MAM-WE 管理應用程式，客戶應該在 Azure 入口網站中使用 Intune 主控台，網址為 [https://portal.azure.com](https://portal.azure.com )。 此外，向協力廠商企業行動管理 (EMM) 提供者註冊的裝置，或是完全不註冊 MDM 的裝置，也可使用 Intune 來管理應用程式。 如需有關 BYOD 與 Microsoft EMS 的詳細資訊，請參閱[使用 Microsoft Enterprise Mobility + Security (EMS) 啟用 BYOD 的技術決策](../fundamentals/byod-technology-decisions.md)。

## <a name="app-management-capabilities-by-platform"></a>各種平台的應用程式管理功能

Intune 提供各種功能，可協助您在所要的裝置上取得所需的應用程式並執行。 下表提供應用程式管理功能的摘要。

|  | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 | Windows Phone 8.1 |
|-------------------------------------------------------------------------------------|---------|-----|-------|------------|-------------------|
| 新增應用程式並指派給裝置與使用者 | 是 | 是 | 是 | 是 | 是 |
| 指派應用程式給未向 Intune 註冊的裝置 | 是 | 是 | 否 | 否 | 否 |
| 使用應用程式設定原則控制應用程式的啟動行為 | 是 | 是 | 否 | 否 | 否 |
| 使用行動裝置應用程式佈建原則更新過期的應用程式 | 否 | 是 | 否 | 否 | 否 |
| 使用應用程式保護原則保護應用程式中的公司資料 | 是 | 是 | 否 | 否 <sup>1</sup> | 否 |
| 只移除已安裝應用程式中的公司資料 (應用程式選擇性抹除) | 是 | 是 | 否 | 是 | 是 |
| 監視應用程式指派 | 是 | 是 | 是 | 是 | 是 |
| 指派及追蹤從應用程式市集中大量採購的應用程式 | 否 | 否 | 否 | 是 | 否 |
| 在裝置上強制安裝應用程式 (必要) <sup>2</sup> | 是 | 是 | 是 | 是 | 是 |
| 可從公司入口網站挑選裝置可安裝的選項 (可用安裝) | 是 <sup>3</sup> | 是 | 是 | 是 | 是 |
| 安裝 Web 應用程式的捷徑 (Web 連結) | 是 <sup>4</sup> | 是 | 是 | 是 | 是 |
| 內部 (企業營運) 應用程式 | 是 | 是 | 是 | 是 | 否 |
| 市集應用程式 | 是 | 是 | 否 | 是 | 是 |
| 更新應用程式 | 是 | 是 | 否 | 是 | 是 |

<sup>1</sup>您可以考慮使用 [Windows 資訊保護](../protect/windows-information-protection-configure.md)來保護 Windows 10 裝置上的應用程式。<br>
<sup>2</sup> 僅適用於 Intune 管理的裝置。<br>
<sup>3</sup> Intune 支援 Android Enterprise 裝置上受控 Google Play 商店中的可用應用程式。<br>
<sup>4</sup> Intune 不提供在標準 Android Enterprise 裝置上將應用程式的捷徑安裝為網頁連結。 不過，會針對[多應用程式專用的 Android Enterprise 裝置](../configuration/device-restrictions-android-for-work.md#dedicated-devices)提供網頁連結支援。 


## <a name="get-started"></a>開始使用

您可以按照以下步驟，在 [應用程式]  工作負載中找到與應用程式最密切相關的資訊：

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
3. 選取 [應用程式]  。

    ![[應用程式] 工作負載窗格](./media/app-management/apps-workload.png)

應用程式工作負載提供連結來存取常用的應用程式資訊和功能。 

應用程式工作負載導覽功能表頂端提供常用的應用程式詳細資料：
- **概觀**：選取此選項可檢視租用戶名稱、MDM 授權單位、租用戶位置、帳戶狀態、應用程式安裝狀態，以及應用程式防護原則狀態。
- **所有應用程式**：選取此選項可顯示所有可用的應用程式清單。 您可以從此頁面新增其他應用程式。 此外，您也可以查看每個應用程式的狀態，以及是否已指派每個應用程式。 如需詳細資訊，請參閱[新增應用程式](apps-add.md)和[指派應用程式](apps-deploy.md)。
- **監視應用程式**
    - **應用程式授權**：檢視、指派及監視從應用程式市集大量採購的應用程式。 如需詳細資訊，請參閱 [iOS 大量採購方案 (VPP) 應用程式](vpp-apps-ios.md)和[商務用 Microsoft Store 大量採購應用程式](windows-store-for-business.md)。
    - **探索到的應用程式**：檢視 Intune 所指派或安裝在裝置上的應用程式。 如需詳細資訊，請參閱 [Intune 探索到的應用程式](app-discovered-apps.md)。
    - **應用程式安裝狀態**：檢視您所建立應用程式指派的狀態。 如需詳細資訊，請參閱[使用 Microsoft Intune 監視應用程式資訊和指派](apps-monitor.md#device-and-user-status-graphs)。
    - **應用程式保護狀態**：檢視您所選取使用者的應用程式保護原則狀態。
- **依平台**：選取這些平台，依平台檢視可用的應用程式。
    - Windows
    - iOS
    - macOS
    - Android
- **原則**：
    - **應用程式保護原則**：選取此選項，將各項設定與應用程式產生關聯並協助保護它所使用的公司資料。 例如，您可以限制某應用程式與其他應用程式的通訊能力，或者您可以要求使用者輸入 PIN 碼才能存取公司應用程式。 如需詳細資訊，請參閱[應用程式防護原則](app-protection-policies.md)。
    - **應用程式設定原則**：選取此選項來提供使用者執行應用程式時可能需要的設定。 如需詳細資訊，請參閱[應用程式設定原則](app-configuration-policies-use-ios.md)、[iOS 應用程式設定原則](app-configuration-policies-use-ios.md)和 [Android 應用程式設定原則](app-configuration-policies-overview.md)。
    - **iOS 應用程式佈建設定檔**：iOS 應用程式包含佈建設定檔和由憑證所簽署的程式碼。 憑證過期之後便無法再次執行應用程式。 Intune 為您提供了可以主動將新的佈建設定檔原則指派給有應用程式即將到期的裝置。 如需詳細資訊，請參閱 [iOS 應用程式佈建設定檔](app-provisioning-profile-ios.md)。
    - **S 模式補充原則**：選取此選項可授權其他應用程式在受控 S 模式裝置上執行。 如需詳細資訊，請參閱 [S 模式補充原則](apps-win32-s-mode.md)。
    - **原則集合**：選取此選項可建立應用程式、原則及所建立其他管理物件的可指派集合。 如需詳細資訊，請參閱[原則集合](../fundamentals/policy-sets.md)。
- **其他**：   
    - **應用程式選擇性抹除**：選取此選項，從選取的使用者裝置只移除公司資料。 如需詳細資訊，請參閱[應用程式選擇性抹除](apps-selective-wipe.md)。
    - **應用程式類別**：新增、釘選及刪除應用程式類別名稱。
    - **電子書**：針對您想要在公司內使用的應用程式或書籍，某些應用程式市集可讓您購買多個授權。 如需詳細資訊，請參閱[使用 Microsoft Intune 管理大量採購的應用程式與書籍](vpp-apps.md)。
- **說明及支援**：進行疑難排解、要求支援，或者檢視 Intune 狀態。 如需詳細資訊，請參閱[針對問題進行疑難排解](../fundamentals/help-desk-operators.md)。

### <a name="try-the-interactive-guide"></a>試試互動式指南
[使用 Microsoft 端點管理員管理和保護行動和傳統型應用程式](https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager) (英文) 互動式指南會帶您逐步使用 Microsoft Endpoint Manager 系統管理中心，以示範如何在 Intune 中管理註冊的裝置、實施政策合規性，以及保護組織的資料。</br></br>

> [!VIDEO https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager]

## <a name="additional-information"></a>其他資訊
主控台內的下列項目提供應用程式相關功能：
- **商務用 Microsoft Store**：設定對商務用 Microsoft Store 的整合。 執行此動作之後，可以將採購的應用程式同步到 Intune 並加以指派，以及追蹤授權使用狀況。 如需詳細資訊，請參閱[商務用 Microsoft Store 大量採購應用程式](windows-store-for-business.md)。
- **Windows 企業憑證**：套用或檢視程式碼簽署憑證的狀態，此憑證可用來將企業營運應用程式發佈到您的受控 Windows 裝置。
- **Windows Symantec 憑證**：套用或檢視 Symantec 程式碼簽署憑證的狀態，將 XAP 和 WP8.x appx 檔案發佈至 Windows 10 行動裝置版裝置時需要此憑證。
- **Windows 側載金鑰**：新增 Windows 側載金鑰，以用來將應用程式直接安裝到裝置，而非發行應用程式並從 Windows 市集下載。 如需詳細資訊，請參閱[側載 Windows 應用程式](app-sideload-windows.md)。
- **Apple VPP 權杖**：套用並檢視您的 iOS/iPadOS 大量採購方案 (VPP) 授權。 如需詳細資訊，請參閱 [iOS/iPadOS 大量採購應用程式](vpp-apps-ios.md)。
- **受控的 Google Play**：受控 Google Play 是 Google 的企業應用程式商店，也是適用於 Android Enterprise 之應用程式的唯一來源。 如需詳細資訊，請參閱[使用 Intune 將受控 Google Play 應用程式新增至 Android Enterprise 裝置](apps-add-android-for-work.md)。
- **自訂**：自訂公司入口網站以顯示您公司的品牌。 如需詳細資訊，請參閱[公司入口網站設定](company-portal-app.md)。

如需應用程式的詳細資訊，請參閱[將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

## <a name="next-steps"></a>後續步驟

- [將應用程式新增至 Microsoft Intune](apps-add.md)
