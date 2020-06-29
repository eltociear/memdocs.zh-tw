---
title: Microsoft Intune App SDK for Android 開發人員測試指南
description: Microsoft Intune App SDK for Android 測試指南可協助您測試 Intune 管理的 Android 應用程式。
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd4ece62215d48f3481923e099feecc992d7aa6d
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093361"
---
# <a name="microsoft-intune-app-sdk-for-android-developers-testing-guide"></a>Microsoft Intune App SDK for Android 開發人員測試指南

Microsoft Intune App SDK for Android 測試指南旨在協助您測試 Intune 管理的 Android 應用程式。

## <a name="demo-tenant-setup"></a>示範租用戶設定
若您的公司還沒有租用戶，您可以建立包含或不包含預先產生資料的示範租用戶。 您必須註冊成為 [Microsoft 合作夥伴](https://partner.microsoft.com/en-us/business-opportunities/why-microsoft)，才能存取 Microsoft CDX。 建立新帳戶：
1. 瀏覽至 [Microsoft CDX 租用戶建立網站](https://cdx.transform.microsoft.com/my-tenants/create-tenant)並建立 Microsoft 365 企業版租用戶。
2. [設定 Intune](../fundamentals/setup-steps.md) 以啟用行動裝置管理 (MDM)。
3. [建立使用者](../fundamentals/users-add.md)。
4. [建立群組](../fundamentals/groups-add.md)。
5. 根據測試需要[指派授權](../fundamentals/licenses-assign.md)。


## <a name="azure-portal-policy-configuration"></a>Azure 入口網站原則設定
在 [Azure 入口網站的 Intune 刀鋒視窗](../apps/app-protection-policies.md)中[建立及指派應用程式保護原則](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview)。 您也可以在 Intune 刀鋒視窗中建立及指派[應用程式設定原則](../apps/app-configuration-policies-overview.md)。

> [!NOTE]
> 若您的應用程式未列於 Azure 入口網站中，您可以選取 [更多應用程式] 選項並在文字方塊中提供套件名稱，使用原則將該應用程式設為目標。

## <a name="test-cases"></a>測試案例

下列測試案例提供設定和確認步驟。 使用這些測試來驗證最近整合的 Android 應用程式。

### <a name="required-pin-and-corporate-credentials"></a>必要的 PIN 和公司認證

您可以要求 PIN 以存取公司資源。 此外，您可以要求使用者進行公司驗證，才能使用受控應用程式。 以下說明做法：

1. 將 [需要 PIN 碼才可存取] 與 [需要公司認證以進行存取] 設定為 [是]。 如需詳細資訊，請參閱 [Microsoft Intune 的 Android 應用程式保護原則設定](../apps/app-protection-policy-settings-android.md#access-requirements)。
2. 確認下列條件：
    - 應用程式啟動應顯示輸入 PIN 的提示，和/或使用者在公司入口網站註冊期間所使用的生產環境。
    - 無法顯示有效登入提示的原因可能是 Android 資訊清單設定不正確，特別是 Azure Active Directory 驗證程式庫 (ADAL) 整合 (SkipBroker、ClientID 和授權單位) 的值。
    - 若未顯示任何提示字元，可能是因整合的 `MAMActivity` 值不正確。 如需 `MAMActivity` 的詳細資訊，請參閱 [Microsoft Intune App SDK for Android 開發人員指南](app-sdk-android.md)。

> [!NOTE] 
> 如果前面的測試無法運作，則接下來的測試可能也會失敗。 檢閱 [SDK](app-sdk-android.md#sdk-integration) 與 [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal) 整合。

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>限制傳送和接收其他應用程式的資料
您可以控制公司管理應用程式之間的資料傳輸，如下所示：

1. 將 [允許應用程式將資料傳送到其他應用程式] 設定為 [受原則管理的應用程式]。
2. 將 [允許應用程式接收其他應用程式的資料] 設定為 [所有應用程式]。 

使用方式和內容提供者會受到這些原則影響。
3. 確認下列條件：
    - 可以正常從非受控應用程式開啟您的應用程式。
    - 允許在應用程式與受控應用程式之間共用內容。
    - 禁止從應用程式共用到非受控應用程式 (例如 Chrome)。


#### <a name="restrict-receiving-data-from-other-apps"></a>限制接收來自其他應用程式的資料

1. 將 [將組織資料傳送到其他應用程式] 設定為 [所有應用程式]。
2. 將 [接收其他應用程式的資料] 設定為 [受原則管理的應用程式]。 
3. 確認下列條件：
    - 從您的應用程式函式中正確傳送至非受控應用程式。
    - 允許在應用程式與受控應用程式之間共用內容。
    - 禁止從非受控應用程式 (例如 Chrome) 共用到應用程式。

若您的應用程式需要[整合的「開啟自」控制項](app-sdk-android.md#opening-data-from-a-local-or-cloud-storage-location)，您可以控制**開啟自**功能，如下所示：

1. 將 [接收其他應用程式的資料] 設定為 [受原則管理的應用程式]。 
2. 將 [將資料開啟為組織文件] 設定為 [封鎖]。 
3. 確認下列條件：
    - 開啟僅限於適當的受控位置。

### <a name="restrict-cut-copy-and-paste"></a>限制剪下、複製及貼上
您可以將系統剪貼簿限制於受控應用程式，如下所示：

1. 將 [限制與其他應用程式的剪下、複製和貼上] 設為 [原則管理的貼上]。
2. 確認下列條件：
    - 將文字複製從您的應用程式複製到非受控應用程式 (例如 Messages) 會被封鎖。

### <a name="prevent-save"></a>禁止儲存
若您的應用程式需要[整合的另存新檔控制項](app-sdk-android.md#example-data-transfer-between-apps-and-device-or-cloud-storage-locations)，您可以控制**另存新檔**功能，如下所示：

1. 將 [不可進行另存新檔] 設為 [是]。
2. 確認下列條件：
    - 儲存僅限於適當的受管理位置。

### <a name="file-encryption"></a>檔案加密
您可以加密裝置上的資料，如下所示：

1. 將 [應用程式資料加密] 設為 [是]。
2. 確認下列條件：
    - 一般的應用程式行為不會受到影響。

### <a name="prevent-android-backups"></a>禁止 Android 備份
您可以控制應用程式備份，如下所示：

1. 如果您已設定 [整合式備份限制](app-sdk-android.md#protecting-backup-data)，請將 [禁止 Android 備份] 設定為 [是]。
2. 確認下列條件：
    - 備份受到限制。

### <a name="wipe"></a>抹除
您可以從遠端抹除包含公司電子郵件與文件的受管理應用程式。 當個人資料不再受到管理時，會將其解密。 以下說明做法：

1. 從 Azure 入口網站[發出抹除](../apps/apps-selective-wipe.md)。
2. 如果您的應用程式沒有註冊任何抹除處理常式，請確認下列條件：
    - 可完整抹除應用程式。
3. 如果您的應用程式已註冊 `WIPE_USER_DATA` 或 `WIPE_USER_AUXILARY_DATA`，請確認下列條件：
    - 受管理的內容已從應用程式移除。 如需詳細資訊，請參閱 [Microsoft Intune App SDK for Android 開發人員指南 - 選擇性抹除](app-sdk-android.md#selective-wipe)。

### <a name="multi-identity-support"></a>多重身分識別支援
整合[多重身分識別支援](app-sdk-android.md#multi-identity-optional)是高風險的變更，必須先經過徹底測試。 最常見的問題是因為使用中的身分識別設定不正確 (`Context` 與威脅層級)，或是追蹤檔案身分識別不正確 (`MAMFileProtectionManager`)。

請至少確認：

- **另存新檔**原則是否正常運作於受控識別。
- 複製並貼上的限制正確實施 (從受控到個人)。
- 僅加密屬於受控識別的資料，不修改個人檔案。
- 在取消註冊期間的選擇性抹除只會移除受控識別資料。
- 從非受控的帳戶變更為受控帳戶時，系統會提示使用者進行條件式啟動 (僅限第一次)。

### <a name="app-configuration-optional"></a>應用程式設定 (選用)
您可以設定受控應用程式的行為。 如果您的應用程式會取用任何應用程式組態設定，您應該測試應用程式是否可正確處理您 (系統管理員) 能夠設定的所有值。 您可以在 Intune 中建立並指派[應用程式設定原則](../apps/app-configuration-policies-overview.md)。


