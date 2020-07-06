---
title: 使用 Intune 管理 iOS 及 Android 版 Office
titleSuffix: ''
description: 使用 iOS 及 Android 版 Office 的 Intune 應用程式防護與設定原則，確保一律可使用保護措施來存取共同作業體驗。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d23eaeee839122bad46cd9619a790b9ca6332a6
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383252"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>使用 iOS 及 Android 版 Office 搭配 Microsoft Intune 來管理共同作業體驗

iOS 及 Android 版 Office 傳遞了數個重要的權益，包括：

- 合併 Word、Excel 與 PowerPoint，讓您下載或切換更少的應用程式，以簡化體驗。 所需要的手機儲存空間不但比安裝個別應用程式少，同時還保留了人們已知及所用的現有行動應用程式的所有功能。
- 整合 Office Lens 技術以解除鎖定相機功能，例如將影像轉換成可編輯的 Word 與 Excel 文件、掃描 PDF，以及使用自動數位增強來擷取白板等功能，更方便閱讀內容。
- 新增人們使用手機工作時經常執行的工作，像是快速建立筆記、簽署 PDF、掃描 QR 代碼，以及在裝置之間傳輸檔案等等。

當您訂閱 Enterprise Mobility + Security 套件 (包括 Microsoft Intune 與 Azure Active Directory Premium 功能，例如條件式存取) 時，可以使用 Office 365 資料最豐富且最廣泛的保護功能。 建議您至少部署允許從行動裝置連線到 iOS 及 Android 版 Office 的條件式存取原則，以及可確保共同作業體驗受到保護的 Intune 應用程式防護原則。

## <a name="apply-conditional-access"></a>套用條件式存取
組織可以使用 Azure AD 條件式存取原則，確保使用者只能使用 iOS 及 Android 版 Office 存取公司或學校內容。 若要這樣做，您將需要以所有潛在使用者為目標的條件式存取原則。 如需有關如何建立此原則的詳細資料，請參閱[需要應用程式保護原則，以使用條件式存取來存取雲端應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access) \(部分機器翻譯\)。

1. 遵循「步驟1：為 Office 365 設定 Azure AD 條件式存取原則」([案例 1：Office 365 應用程式需要具有應用程式防護原則的已核准應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies)，允許 iOS 及 Android 版 Office，但禁止協力廠商 OAuth 支援行動裝置用戶端連線至 Office 365 端點。)

   >[!NOTE]
   > 此原則可確保行動使用者使用適合的應用程式，存取所有 Office 端點。

## <a name="create-intune-app-protection-policies"></a>建立 Intune 應用程式保護原則

應用程式保護原則 (APP) 定義允許哪些應用程式，以及其可以對組織資料採取的動作。 APP 中可用的選擇可讓組織針對其特定需求量身訂作保護方案。 針對一些組織，實作完整案例需要哪種原則設定可能不是那麼明顯。 為了協助組織排定行動用戶端端點強化的優先順序，Microsoft 引進了適用於 iOS 與 Android 行動裝置應用程式管理的 APP 資料保護架構分類法。

應用程式資料保護架構會組織成三個不同的設定層級，每個層級都以前一層為基礎而建置：

- **企業基本資料保護** (層級 1) 可確保應用程式使用 PIN 來保護並加密，並執行選擇性抹除作業。 針對 Android 裝置，此層級會驗證 Android 裝置證明。 這是一種入門級設定，可在 Exchange Online 信箱原則中提供類似的資料保護控制，並將 IT 與使用者人口引進 APP。
- **企業增強的資料保護** (層級 2) 引進 APP 資料洩露防護機制與最低 OS 需求。 此設定適用於大部分存取公司或學校資料的行動使用者。
- **企業高資料保護** (層級 3) 引進進階資料保護機制、增強的 PIN 設定，以及 APP 行動威脅防禦。 對於存取高風險資料的使用者而言，這是理想的設定。

若要查看必須保護之每個設定層級與最低應用程式的特定建議，請參閱[使用應用程式保護原則的資料保護架構](app-protection-framework.md)。

無論裝置是否已在聯合式端點管理 (UEM) 解決方案中註冊，都必須使用[如何建立及指派應用程式保護原則](app-protection-policies.md)中的步驟，為 iOS 與 Android 應用程式建立 Intune 應用程式保護原則。 這些原則至少必須符合下列條件：

1. 包括所有 Microsoft 365 行動應用程式，例如 Edge、Outlook、OneDrive、Office 或 Teams，因為這可確保使用者能夠以安全的方式存取及操作任何 Microsoft 應用程式中的公司或學校資料。

2. 其會指派給所有使用者。 這可確保所有使用者都受到保護，不論其是否使用 iOS 及 Android 版 Office。

3. 判斷哪一個架構層級符合您的需求。 大部分的組織都應該實作 **Enterprise 增強的資料保護** (層級 2) 中所定義的設定，因為這樣可啟用資料保護與存取需求控制。

如需有關可用設定的詳細資訊，請參閱 [Android 應用程式保護原則設定](app-protection-policy-settings-android.md)與 [iOS 應用程式保護原則設定](app-protection-policy-settings-ios.md)。

> [!IMPORTANT]
> 若要針對未在 Intune 中註冊之 Android 裝置上的應用程式套用 Intune 應用程式保護原則，使用者也必須安裝 Intune 公司入口網站。 如需詳細資訊，請參閱[當 Android 應用程式交由應用程式保護原則管理時的行為](../fundamentals/end-user-mam-apps-android.md)。

## <a name="utilize-app-configuration"></a>利用應用程式設定

iOS 及 Android 版 Office 支援允許 Microsoft Endpoint Manager 等聯合式端點管理系統管理員可自訂應用程式行為的應用程式設定。

應用程式設定可以透過已註冊裝置上的行動裝置管理 (MDM) OS 通道 (適用於 iOS 的[受控應用程式設定](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) \(英文\) 或適用於 Android 的 [ Android in the Enterprise](https://developer.android.com/work/managed-configurations) \(英文\) 通道) 或透過 Intune 應用程式保護原則 (APP) 通道來傳遞。 iOS 及 Android 版 Office 支援下列設定案例：

- 只允許公司或學校帳戶
- 資料保護設定

> [!IMPORTANT]
> 針對要求在 Android 註冊裝置的設定案例，裝置必須在 Android Enterprise 中註冊，而且 Android 版 Office 必須經由受控 Google Play 商店部署。 如需詳細資訊，請參閱[設定 Android Enterprise 工作設定檔裝置的註冊](../enrollment/android-work-profile-enroll.md)與[為受控的 Android Enterprise 裝置新增應用程式設定原則](app-configuration-policies-use-android.md)。

每個設定案例都會強調其特定需求。 例如，設定案例是否要求進行裝置註冊，因此可與任何 UEM 提供者搭配運作，或要求 Intune 應用程式保護原則。

> [!NOTE]
> 使用 Microsoft 端點管理員時，透過 MDM OS 通道傳遞的應用程式設定稱為**受控裝置** 應用程式組態原則 (ACP)；透過應用程式保護原則通道提供的應用程式設定稱為**受控應用程式**應用程式組態原則。

## <a name="only-allow-work-or-school-accounts"></a>只允許公司或學校帳戶

尊重我們最大規模且高度管制之客戶的資料安全性和合規性政策，是 Microsoft 365 價值的關鍵要件。 有些公司需要在公司環境內擷取所有通訊資訊，以及確保裝置僅可用於公司通訊。 為了支援這些需求，您可將已註冊裝置上的 Android 版 Office 設定為只允許在應用程式內佈建單一公司帳戶。

您可以在這裡深入了解如何設定組織允許的帳戶模式設定：

- [Android 設定](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

此設定案例僅適用於已註冊的裝置。 不過，支援任何 UEM 提供者。 如果您不是使用 Microsoft 端點管理員，則需要參閱您的 UEM 文件，以了解如何部署這些設定金鑰。

> [!NOTE]
> 此時，只有 Android 版 Office 才能支援組織允許的帳戶模式。

## <a name="data-protection-app-configuration-scenarios"></a>資料保護應用程式設定案例

當您將 Intune 應用程式防護原則套用到已登入應用程式的公司或學校帳戶，使用 Microsoft Endpoint Manager 管理應用程式時，iOS 及 Android 版 Office 會支援下列資料防護設定的應用程式設定原則：

- 透過傳輸檔案動作管理檔案傳輸
- 透過附近裝置分享動作管理檔案傳輸

無論裝置註冊狀態為何，這些設定都可以部署到應用程式。

### <a name="manage-file-transfers"></a>管理檔案傳輸

根據預設，iOS 及 Android 版 Office 可讓使用者使用各種機制來共用內容：

- 如果檔案是裝載於 OneDrive 或 SharePoint 中，使用者可以直接在檔案內起始共用要求。
- 使用者可以使用 [傳輸檔案] 動作來將檔案傳輸到桌面系統。
- 使用者可以使用 [鄰近分享] 動作來將檔案共用到鄰近的行動裝置。

[傳輸檔案] 和 [鄰近分享] 動作只能用於媒體、本機檔案，以及未受應用程式保護原則保護的檔案。 

|    機碼    |    值    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.ShareNearby.IsAllowed.IntuneMAMOnly    |    **True** (預設) 會啟用公司或學校帳戶的附近裝置分享功能<br>**False** 會停用公司或學校帳戶的附近裝置分享功能    |
|    com.microsoft.office.TransferFiles.IsAllowed.IntuneMAMOnly    |    **True** (預設) 會啟用公司或學校帳戶的傳輸檔案功能<br>**False** 會停用公司或學校帳戶的傳輸檔案功能    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>使用 Microsoft 端點管理員部署應用程式設定案例

若您使用 Microsoft Endpoint Manager 作為您的行動應用程式管理提供者，請參閱[在不註冊裝置的情況下新增受控應用程式的應用程式設定原則](app-configuration-policies-managed-app.md)，了解如何為資料防護應用程式設定案例建立受控應用程式的應用程式設定原則。 設定建立之後，您可以將其原則指派給使用者的群組。

## <a name="next-steps"></a>後續步驟

- [什麼是應用程式保護原則？](app-protection-policy.md) 
- [Microsoft Intune 的應用程式設定原則](app-configuration-policies-overview.md)