---
title: 使用 Intune 管理 iOS 及 Android 版 Outlook
description: 使用 iOS 與 Android 版 Outlook 的 Intune 應用程式保護與設定原則，確保一律可使用保護措施來存取小組共同作業體驗。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3db207e4c1c75706c1f54762bf74c1757d342ac1
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973038"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>透過使用 iOS 及 Android 版 Outlook 與 Microsoft Intune 的搭配組合，管理訊息共同作業存取

iOS 及 Android 版 Outlook 的設計是將電子郵件、行事曆、連絡人與其他檔案結合在一起，讓組織中的使用者，能從其行動裝置執行更多動作。

當您訂閱 Enterprise Mobility + Security 套件 (包括 Microsoft Intune 與 Azure Active Directory Premium 功能，例如條件式存取) 時，可以使用 Office 365 資料最豐富且最廣泛的保護功能。 建議您至少部署允許從行動裝置連線到 iOS 及 Android 版 Outlook 的條件式存取原則，以及可確保共同作業體驗受到保護的 Intune 應用程式防護原則。

## <a name="apply-conditional-access"></a>套用條件式存取
組織可以使用 Azure AD 條件式存取原則，確保使用者只能使用 iOS 及 Android 版 Outlook 存取公司或學校內容。 若要這樣做，您將需要以所有潛在使用者為目標的條件式存取原則。 如需有關如何建立此原則的詳細資料，請參閱[需要應用程式保護原則，以使用條件式存取來存取雲端應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access) \(部分機器翻譯\)。

1. 遵循「步驟1：為 Office 365 設定 Azure AD 條件式存取原則」([案例 1：Office 365 應用程式需要具有應用程式防護原則的已核准應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies)，其允許 iOS 及 Android 版 Outlook，但封鎖 OAuth 支援 Exchange ActiveSync 用戶端連線至 Exchange Online。)

   > [!NOTE]
   > 此原則可確保行動使用者可以使用適用的應用程式，存取所有 Office 端點。

2. 遵循「步驟2：使用 ActiveSync (EAS) 為 Exchange Online 設定 Azure AD 條件式存取原則」([案例 1：Office 365 應用程式需要具有應用程式防護原則的已核准應用程式](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies)，其阻止 Exchange ActiveSync 用戶端運用基本驗證連線至 Exchange Online。)

   上述原則會運用授與控制項[需要應用程式防護原則](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference)，確保在授與存取權之前，會將 Intune 應用程式防護原則套用至 iOS 及 Android 版 Outlook 中相關聯的帳戶。 若未將使用者指派給 Intune 應用程式防護原則、未獲授權使用 Intune，或應用程式未包含在 Intune 應用程式防護原則中，則原則會阻止使用者取得存取權杖，以及取得訊息資料的存取權。

3. 最後，遵循[如何：使用條件式存取封鎖 Azure AD 的舊版驗證](https://docs.microsoft.com/azure/active-directory/conditional-access/block-legacy-authentication)，以封鎖 iOS 及 Android 裝置上其他 Exchange 通訊協定的舊版驗證；此原則應僅以 Office 365 Exchange Online 雲端應用程式與 iOS 及 Android 裝置平台為目標。 這可確保使用 Exchange Web 服務、IMAP4，或具有基本驗證之 POP3 通訊協定的行動應用程式，無法連線到 Exchange Online。

## <a name="create-intune-app-protection-policies"></a>建立 Intune 應用程式保護原則

應用程式保護原則 (APP) 定義允許哪些應用程式，以及其可以對組織資料採取的動作。 APP 中可用的選擇可讓組織針對其特定需求量身訂作保護方案。 針對一些組織，實作完整案例需要哪種原則設定可能不是那麼明顯。 為了協助組織排定行動用戶端端點強化的優先順序，Microsoft 引進了適用於 iOS 與 Android 行動裝置應用程式管理的 APP 資料保護架構分類法。

應用程式資料保護架構會組織成三個不同的設定層級，每個層級都以前一層為基礎而建置：

- **企業基本資料保護** (層級 1) 可確保應用程式使用 PIN 來保護並加密，並執行選擇性抹除作業。 針對 Android 裝置，此層級會驗證 Android 裝置證明。 這是一種入門級設定，可在 Exchange Online 信箱原則中提供類似的資料保護控制，並將 IT 與使用者人口引進 APP。
- **企業增強的資料保護** (層級 2) 引進 APP 資料洩露防護機制與最低 OS 需求。 此設定適用於大部分存取公司或學校資料的行動使用者。
- **企業高資料保護** (層級 3) 引進進階資料保護機制、增強的 PIN 設定，以及 APP 行動威脅防禦。 對於存取高風險資料的使用者而言，這是理想的設定。

若要查看必須保護之每個設定層級與最低應用程式的特定建議，請參閱[使用應用程式保護原則的資料保護架構](app-protection-framework.md)。

無論裝置是否已在聯合式端點管理 (UEM) 解決方案中註冊，都必須使用[如何建立及指派應用程式保護原則](app-protection-policies.md)中的步驟，為 iOS 與 Android 應用程式建立 Intune 應用程式保護原則。 這些原則至少必須符合下列條件：

1. 其包含所有 Microsoft 365 行動裝置應用程式，例如 Edge、Outlook、OneDrive、Office 或 Teams ，因為這可確保使用者能夠以安全的管道，存取及操作任何 Microsoft 應用程式中的公司或學校資料。

2. 其會指派給所有使用者。 這可確保所有使用者都受到保護，不論其使用 iOS 或 Android 版 Outlook。

3. 判斷哪一個架構層級符合您的需求。 大部分的組織都應該實作 **Enterprise 增強的資料保護** (層級 2) 中所定義的設定，因為這樣可啟用資料保護與存取需求控制。

如需有關可用設定的詳細資訊，請參閱 [Android 應用程式保護原則設定](app-protection-policy-settings-android.md)與 [iOS 應用程式保護原則設定](app-protection-policy-settings-ios.md)。

> [!IMPORTANT]
> 若要針對未在 Intune 中註冊之 Android 裝置上的應用程式套用 Intune 應用程式保護原則，使用者也必須安裝 Intune 公司入口網站。 如需詳細資訊，請參閱[當 Android 應用程式交由應用程式保護原則管理時的行為](../fundamentals/end-user-mam-apps-android.md)。

## <a name="utilize-app-configuration"></a>利用應用程式設定

iOS 及 Android 版 Outlook 支援像 Microsoft Endpoint Manager 這樣，允許整合端點管理系統管理員可自訂應用程式行為的應用程式設定。

應用程式設定可以透過已註冊裝置上的行動裝置管理 (MDM) OS 通道 (適用於 iOS 的[受控應用程式設定](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) \(英文\) 或適用於 Android 的 [ Android in the Enterprise](https://developer.android.com/work/managed-configurations) \(英文\) 通道) 或透過 Intune 應用程式保護原則 (APP) 通道來傳遞。 iOS 及 Android 版 Outlook 支援下列設定案例：

- 只允許公司或學校帳戶
- 一般應用程式組態設定
- S/MIME 設定
- 資料保護設定

如需 iOS 與 Android 版 Outlook 所支援應用程式組態設定的特定程序步驟和詳細文件，請參閱 [Deploying Outlook for iOS and Android app configuration settings](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune) (部署 iOS 與 Android 版 Outlook 應用程式組態設定)。

## <a name="next-steps"></a>後續步驟

- [什麼是應用程式保護原則？](app-protection-policy.md) 
- [Microsoft Intune 的應用程式設定原則](app-configuration-policies-overview.md)