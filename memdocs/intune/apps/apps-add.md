---
title: 將應用程式新增至 Microsoft Intune
titleSuffix: ''
description: 了解如何為 Microsoft Intune 新增應用程式，以便您可以指派應用程式給使用者和裝置。 Intune 支援各種不同的應用程式類型。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1ded457-0ecf-4f9c-a2d2-857d57f8d30a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 73173d599c3d19bb39090b34e0c5f6ffec5753fe
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083856"
---
# <a name="add-apps-to-microsoft-intune"></a>將應用程式新增至 Microsoft Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

您必須先將應用程式新增至 Microsoft Intune，才可以設定、指派、保護或監視這些應用程式。

您公司中的應用程式與裝置使用者 (也就是您公司的員工) 可能會有數種不同的應用程式需求。 將應用程式新增至 Intune 並向員工開放使用前，您必須確認該應用程式有用，進而評定並了解幾項應用程式基本概念。 有各種應用程式類型可供 Intune 使用。 您必須判斷您公司使用者需要的應用程式需求，例如公司員工需要的平台和功能。 您必須決定是否要使用 Intune 來管理裝置 (包含應用程式)，或僅管理應用程式而不管理裝置。 您也必須判斷公司員工需要的應用程式和功能，以及有需要的人。 本文中的資訊可協助您開始。

## <a name="app-types-in-microsoft-intune"></a>Microsoft Intune 中的應用程式類型

Intune 支援各種不同的應用程式類型。 每種應用程式類型的可用選項都不相同。 Intune 可讓您新增及指派下列應用程式類型：

| 應用程式類型 | 安裝 | 更新 |
|---|---|---|
| 來自市集的應用程式 (市集應用程式) | Intune 會將應用程式安裝在裝置上。  | 應用程式會自動更新。 |
| 內部撰寫的應用程式 (企業營運) | Intune 會將應用程式安裝在裝置上 (您負責提供安裝檔案)。 | 您必須更新應用程式。 |
| 內建的應用程式 (內建應用程式) | Intune 會將應用程式安裝在裝置上。  | 應用程式會自動更新。 |
| Web 上的應用程式 (Web 連結) | Intune 會在裝置主畫面上建立 Web 應用程式的捷徑。 | 應用程式會自動更新。 |

### <a name="specific-app-type-details"></a>特定應用程式類型詳細資料
 
下表列出特定應用程式類型，以及如何在 Intune 的 [新增應用程式]  窗格中新增它們：

| **應用程式特定類型** | **一般類型** | **應用程式特定程序** |
| --- | --- | --- |
| Android 市集應用程式  | 市集應用程式  | [應用程式類型]  選取 [Android]  ，並輸入應用程式的 Google Play 商店 URL。 |
| Android Enterprise 應用程式  | 市集應用程式  | [應用程式類型]  選取 [Android]  ，然後輸入應用程式的受控 Google Play 商店 URL。 <sup>1</sup> |
| iOS/iPadOS store apps  | 市集應用程式  | [應用程式類型]  選取 [iOS]  ，搜尋應用程式，然後在 Intune 中選取該應用程式。 |
| Windows Phone 8.1 市集應用程式  | 市集應用程式  | [應用程式類型]  選取 [Windows Phone 8.1]  ，並輸入應用程式的 Microsoft Store URL。 |
| Microsoft Store 應用程式  | 市集應用程式  | [應用程式類型]  選取 [Windows]  ，並輸入應用程式的 Microsoft Store URL。 |
| 受控的 Google Play 應用程式 | 市集應用程式  | [應用程式類型]  選取 [受控的 Google Play]  、搜尋應用程式，然後在 Intune 中選取該應用程式。 |
| 適用於 Windows 10 的 Office 365 應用程式  | 市集應用程式 (Office 365) | [應用程式類型]  選取 [Office 365 套件]  下的 [Windows 10]  ，然後選取想要安裝的 Office 365 應用程式。  |
| 適用於 macOS 的 Office 365 應用程式 | 市集應用程式 (Office 365) | [應用程式類型]  選取 [Office 365 套件]  下的 [macOS]  ，然後選取 Office 365 應用程式套件。 |
| 適用於 Windows 10 的 Microsoft Edge 77 版和更新版本 | 市集應用程式 | [應用程式類型]  選取 [Microsoft Edge 77 版和更新版本]  下的 [Windows 10]  。 |
| 適用於 macOS 的 Microsoft Edge 77 版和更新版本 | 市集應用程式 | [應用程式類型]  選取 [Microsoft Edge 77 版和更新版本]  下的 [macOS]  。 |
| Android 企業營運 (LOB) 應用程式 | LOB 應用程式 | [應用程式類型]  選取 [企業營運]  應用程式，選取 [應用程式套件檔案]  ，然後輸入副檔名為 **.apk** 的 Android 安裝檔。  |
| iOS/iPadOS LOB apps | LOB 應用程式 | 針對 [應用程式類型]  選取 [企業營運]  應用程式，選取 [應用程式套件檔案]  ，然後輸入副檔名為 **.ipa** 的 iOS/iPadOS 安裝檔。  |
| Windows Phone LOB 應用程式 | LOB 應用程式 | [應用程式類型]  選取 [企業營運]  應用程式，選取 [應用程式套件檔案]  ，然後輸入副檔名為 **.xap** 的 Windows Phone 安裝檔。  |
| Windows LOB 應用程式 | LOB 應用程式 | [應用程式類型] 選取 [企業營運]  應用程式，選取 [應用程式套件檔案]  ，然後輸入副檔名為 **.msi**、 **.appx**、 **.appxbundle**、 **.msix** 和 **.msixbundle** 的 Windows 安裝檔案。 |
| 內建 iOS/iPadOS 應用程式  | 內建應用程式 | [應用程式類型]  選取 [內建應用程式]  ，然後在提供的應用程式清單中選取內建應用程式。  |
| 內建 Android 應用程式  | 內建應用程式 | [應用程式類型]  選取 [內建應用程式]  ，然後在提供的應用程式清單中選取內建應用程式。  |
| Web 應用程式  | Web 應用程式  | [應用程式類型]  選取 [Web 連結]  ，然後輸入指向 Web 應用程式的有效 URL。  |
| Android Enterprise 系統應用程式  | 市集應用程式  | 選取 [Android Enterprise 系統應用程式]  作為 [應用程式類型]  ，然後輸入應用程式名稱、發行者和套件檔案。  |
| Windows 應用程式 (Win32)  | LOB 應用程式  | [應用程式類型]  選取 [Windows 應用程式 (Win32)]  ，選取 [應用程式套件檔案]  ，然後選取副檔名為 **.intunewin** 的安裝檔。  |
| macOS LOB 應用程式 | LOB 應用程式  | 選取 [企業營運]  作為 [應用程式類型]  、選取 [應用程式套件檔案]  ，然後選取副檔名為 **.intunemac** 的安裝檔。  |


<sup>1</sup> 如需 Android Enterprise 和 Android 工作設定檔的詳細資訊，請參閱下面的[了解授權的應用程式](apps-add.md#understanding-licensed-apps)。

您可以依序選取 [應用程式]   > [所有應用程式]   > [新增]  ，在 Microsoft Intune 中新增應用程式。 [選取應用程式類型]  窗格隨即顯示，並可讓您選取 [應用程式類型]  。 

>[!TIP]
> LOB 應用程式是您從應用程式安裝檔新增的應用程式。 例如，若要安裝 iOS LOB/iPadOS 應用程式，您必須在 [選取應用程式類型]  窗格中選取 [企業營運應用程式]  作為 [應用程式類型]  。 然後，選取應用程式套件檔案 (副檔名為 .ipa)。 這些類型的應用程式通常都是內部撰寫的。

## <a name="assess-app-requirements"></a>評估應用程式需求
身為 IT 管理員，您必須判斷您的群組必須使用哪些應用程式，還必須判斷每個群組和子群組所需要的功能。 您必須針對每個應用程式判斷所需的平台、需要該應用程式的使用者群組、要套用至那些群組的設定原則，以及要套用的保護原則。  

此外，您還必須決定要將重心放在行動裝置管理 (MDM)，還是只放在行動應用程式管理 (MAM) 上。 

在下列情況下，使用 Intune 搭配 MDM 來管理裝置將很有用：
- 使用者需要 Wi-Fi 或 VPN 公司連線設定檔，才能具有生產力。
- 使用者需要將一組應用程式推送到他們的裝置。
- 您的組織需要遵守的法規或其他原則會要求特定 MDM 控制項 (例如安全性或加密)。

在下列情況下，使用 Intune 搭配 MAM 在不管理裝置之下管理應用程式將很有用：
- 您想要讓使用者使用他們自己的裝置 (BYOD)。
- 您想要提供單次快顯訊息，讓使用者知道 MAM 保護已就位，而不是一直發送裝置層級的通知。
- 您想要遵守對個人裝置要求較少管理功能的原則。 例如，您想要針對應用程式管理公司資料，而不是管理整部裝置的公司資料。

如需詳細資訊，請[比較 MDM 和 MAM](../fundamentals/byod-technology-decisions.md)。

### <a name="determine-who-will-use-the-app"></a>決定誰會使用應用程式

當您在判斷員工需要哪些應用程式時，請考慮不同的使用者群組和他們所使用的各種應用程式。 了解這些群組，即使在您新增應用程式後也很實用。 新增應用程式後，您會指派可使用該應用程式的使用者群組。 

首先，您必須根據應用程式所包含資料的敏感度，決定有哪些群組可以存取該應用程式。 您可能需要包含或排除組織內特定的角色類型。 例如，銷售群組可能只需要特定的 LOB 應用程式，而著重在工程、財務、人力資源或法律的使用者可能不需要使用 LOB 應用程式。 此外，您的銷售群組可能需要額外的資料保護，以及從行動裝置存取內部的公司服務的能力。 您必須決定這個群組如何使用應用程式連線到資源。 應用程式所存取的資料要存在於雲端還是內部部署之中？ 以及，使用者使用應用程式時，會以何種方式連線到資源？ 

Intune 也支援存取需要安全存取內部部署資料的用戶端應用程式，例如企業營運應用程式伺服器。 這種存取通常是使用 [Intune 受控憑證](../protect/certificates-configure.md)來提供，並搭配使用位於周邊的標準 VPN 閘道或 Proxy，例如 Azure Active Directory 應用程式 Proxy。 Intune 的 [App Wrapping Tool 與 App SDK](../developer/apps-prepare-mobile-application-management.md) 可協助將存取的資料限制在企業營運應用程式內，讓它無法將公司資料傳遞至取用者應用程式或服務。

使用 [Intune 部署規劃、設計和實作指南](../fundamentals/planning-guide.md)來協助判斷如何識別哪些組織群組與每個應用程式使用案例和子使用案例相關。 如需將應用程式指派給群組的詳細資訊，請參閱[使用 Microsoft Intune 將應用程式指派給群組](apps-deploy.md)。

### <a name="determine-the-type-of-app-for-your-solution"></a>決定解決方案的應用程式類型

您可以選擇下列應用程式類型：
- **來自市集的應用程式**：已上傳至 Microsoft Store、iOS/iPadOS 市集或 Android 市集的應用程式即為市集應用程式。 市集應用程式的提供者會維護應用程式並提供更新。 您可以在市集清單中選取應用程式，並使用 Intune 將它新增為使用者可用的應用程式。
- **內部撰寫的應用程式 (企業營運)** ：於公司內部建立的應用程式即為企業營運 (LOB) 應用程式。 已為其中一個 Intune 支援的平台 (例如 Windows、iOS/iPadOS、macOS 或 Android) 建立此類型應用程式的功能。 您的組織會建立更新，並以個別檔案提供給您。 您會使用 Intune 來新增及部署應用程式更新，藉此將其提供給使用者。
- **網路上的應用程式**：Web 應用程式是用戶端伺服器應用程式。 伺服器提供了 Web 應用程式，其中包括 UI、內容和功能。 此外，現代的 Web 裝載平台通常會提供安全性、負載平衡和其他優勢。 此類型的應用程式會在網路上進行個別維護。 您會使用 Intune 指向此應用程式類型。 您也會指派有哪些使用者群組可以存取該應用程式。 請注意，Android 不支援 Web 應用程式。

在決定您的組織需要哪些應用程式時，請考慮這些應用程式會如何與雲端服務整合、會存取哪些資料、是否可供 BYOD 使用者使用，以及是否需要存取網際網路。

如需組織所需應用程式類型的詳細資訊，請參閱[建立設計](../fundamentals/planning-guide-design.md#feature-requirements)＜功能需求＞一節中的＜應用程式＞小節。

### <a name="understanding-app-management-and-protection-policies"></a>了解應用程式管理和保護原則
Intune 讓您修改部署的應用程式功能，幫助這些應用程式符合公司的規範及安全性原則。 這項控制能讓您決定保護公司資料的方式。 Intune 受控應用程式使用一組豐富的行動應用程式保護原則，例如：

- 限制複製和貼上及另存新檔功能。
- 設定網頁連結以在 Intune Managed Browser 應用程式內開啟。
- 啟用使用多重身分識別和應用程式層級的條件式存取。

Intune 受控應用程式也可以在無需註冊之下啟用應用程式保護，這可讓您選擇在不管理使用者裝置的情況下套用資料外洩防護原則。 此外，您可以使用 Intune App SDK 和 App Wrapping Tool，將行動應用程式管理併入您的行動和企業營運應用程式。 如需這些工具的詳細資訊，請參閱 [Intune App SDK 概觀](../developer/app-sdk.md)。

### <a name="understanding-licensed-apps"></a>了解授權應用程式
除了了解 Web 應用程式、市集應用程式和 LOB 應用程式之外，您也應了解大量採購方案應用程式和授權應用程式的目的地，例如： 
- **Apple 商務用大量採購計劃 (iOS)** ：iOS/iPadOS App Store 可讓您針對要在公司內執行的應用程式購買多個授權。 購買多個複本有助於您在公司中有效率地管理應用程式。 如需詳細資訊，請參閱[管理 iOS/iPadOS 大量採購的應用程式](vpp-apps-ios.md)。
- **Android 工作設定檔**：將應用程式指派給 Android 工作設定檔裝置的方式，與您將應用程式指派給標準 Android 裝置的方式不同。 您針對 Android 工作設定檔安裝的所有應用程式都是來自受控的 Google Play 商店。 您可以使用 Intune 來瀏覽所需的應用程式，並核准它們。 然後，該應用程式會出現在 Azure 入口網站的 [授權的應用程式]  節點中，接著您可以管理其指派對象，如同管理其他應用程式一般。
- **商務用 Microsoft Store (Windows 10)** ：商務用 Microsoft Store 可讓您為組織個別或大量尋找及購買應用程式。 透過將市集連線至 Microsoft Intune，就可以在 Azure 入口網站中管理大量採購的應用程式。 如需詳細資訊，請參閱[從商務用 Microsoft Store 管理應用程式](windows-store-for-business.md)。

    > [!NOTE]
    > Windows 應用程式的副檔名包含 **.msi**、 **.appx**、 **.appxbundle**、 **.msix** 和 **.msixbundle**。  

## <a name="before-you-add-apps"></a>在您新增應用程式之前
在您開始新增和指派應用程式之前，請考慮下列事項：

- 當您新增及指派來自市集的應用程式時，您的使用者必須擁有該市集的帳戶，才能安裝應用程式。
- 您指派的某些應用程式或項目，可能相依於內建的 iOS/iPadOS 應用程式。 例如，如果您指派 iOS/iPadOS 市集中的書籍，則裝置上必須有 iBooks 應用程式。 如果您已經移除了 iBooks 內建應用程式，您將無法使用 Intune 來恢復該應用程式。

> [!IMPORTANT]
> 若您在部署並安裝應用程式之後透過 Intune Azure 入口網站變更應用程式名稱，將無法再使用命令定位應用程式。

## <a name="cloud-storage-space"></a>雲端儲存空間
使用軟體安裝程式安裝類型所建立的所有應用程式 (例如企業營運應用程式)，都會封裝並上傳至 Intune 雲端儲存空間。 Intune 的試用版訂閱內容包含 2 GB 的雲端式儲存空間，可用來儲存受控的應用程式和更新。 完整的訂閱不會限制儲存空間的總量。

雲端儲存空間需求如下：

- 所有應用程式安裝檔案必須位於相同的資料夾。
- 您上傳的任何檔案其大小上限都是 8 GB。

  > [!NOTE]
  > Windows 企業營運 (LOB) 應用程式，包括 Win32、Windows 通用 AppX、Windows 通用 AppX 套件組合、Windows 通用 MSI X 和 Windows 通用 MSI X 套件組合，其大小上限為每應用程式 8 GB。 包括 iOS/iPadOS LOB 應用程式在內的所有其他 LOB 應用程式，其大小上限為每應用程式 2 GB。

## <a name="create-and-edit-categories-for-apps"></a>建立及編輯應用程式的類別

應用程式類別可協助您排序應用程式，以利使用者在公司入口網站中執行搜尋。 您可以指派一或多個類別給應用程式，例如 [開發人員應用程式]  或 [通訊應用程式]  。

當您將應用程式新增到 Intune 時，可以自由選取所需的類別。 使用平台特定的主題來新增應用程式及指派類別。 若要建立及編輯您自己的類別，請使用下列程序︰

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
3. 選取 [應用程式]   > [應用程式類別]  。  
    [應用程式類別]  窗格會顯示目前類別的清單。 
5. 請執行下列其中一個動作：
    - 若要新增類別，請在 [建立類別]  窗格中，選取 [新增]  ，然後輸入類別的名稱。  
    名稱只能以一種語言輸入，而且 Intune 不會加以翻譯。
    - 若要編輯類別，請選取類別旁的省略符號 ( **...** )，然後選取 [釘選至儀表板]  或 [刪除]  。
6. 選取 [建立]  。

## <a name="apps-that-are-added-automatically-by-intune"></a>Intune 自動新增的應用程式

原本，Intune 包含許多您可以快速指派的內建應用程式。 根據 Intune 客戶的意見反應，我們移除了此清單，而且也不再顯示內建應用程式。 不過，如果您已指派任何內建應用程式，那些應用程式仍會顯示在應用程式清單中。 若有需要，您可以繼續指派這些應用程式。

> [!NOTE]
> 對於安裝所需的非企業營運應用程式，假設未偵測到應用程式且應用程式的安裝狀態不是「安裝擱置中」  ，則 Intune 將嘗試在裝置簽入時傳送安裝命令來安裝應用程式。

## <a name="installing-updating-or-removing-required-apps"></a>安裝、更新或移除必要的應用程式

Intune 會在 24 小時內自動重新安裝、更新或移除必要的應用程式，而不是等候 7 天的重新評估週期。

Intune 會根據下列條件，自動重新安裝、更新或移除必要的應用程式：
- 如果使用者解除安裝的應用程式是您要求必須在裝置上安裝的應用程式，則 Intune 會在過了此排程之後自動重新安裝應用程式。
- 如果必要的應用程式安裝失敗，或因任何原因導致裝置上沒有該應用程式，則 Intune 會在過了此排程之後評估合規性，並重新安裝應用程式。  
- 系統管理員可將應用程式設為可供使用者群組使用的目標，使用者即可透過裝置上的公司入口網站來安裝應用程式。 之後，系統管理員可將應用程式從 v1 更新為 v2。 如果裝置上仍有任何舊版的應用程式，Intune 會在過了此排程之後更新應用程式。
- 如果系統管理員部署解除安裝的意圖，但裝置上的應用程式無法解除安裝，則 Intune 會在過了此排程之後評估合規性，並解除安裝應用程式。   

## <a name="app-installation-errors"></a>應用程式安裝錯誤

如需有關 Intune 應用程式安裝錯誤的詳細資料，請參閱[應用程式安裝錯誤](troubleshoot-app-install.md)。

## <a name="next-steps"></a>後續步驟

若要了解如何將不同平台的應用程式新增至 Intune，請參閱：

- [Android 市集應用程式](store-apps-android.md)
- [Android LOB 應用程式](lob-apps-android.md)
- [iOS 市集應用程式](store-apps-ios.md)
- [iOS LOB 應用程式](lob-apps-ios.md)
- [macOS LOB 應用程式](lob-apps-macos.md)
- [Web 應用程式 (適用於所有平台)](web-app.md)
- [Windows Phone 8.1 市集應用程式](store-apps-windows-phone-8-1.md)
- [Windows Phone LOB 應用程式](lob-apps-windows-phone.md)
- [Microsoft Store 應用程式](store-apps-windows.md)
- [Windows LOB 應用程式](lob-apps-windows.md)
- [適用於 Windows 10 的 Office 365 應用程式](apps-add-office365.md)
- [適用於 macOS 的 Office 365 應用程式](apps-add-office365-macos.md)
- [受控的 Google Play 應用程式](apps-add-android-for-work.md)
- [適用於 Windows 10 的 Microsoft Edge](apps-windows-edge.md)
- [適用於 macOS 的 Microsoft Edge](apps-edge-macos.md)
- [內建應用程式](apps-add-built-in.md)
- [Android Enterprise 系統應用程式](apps-ae-system.md)
- [Win32 應用程式](apps-win32-app-management.md)
