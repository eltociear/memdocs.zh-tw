---
title: 為受控的 Android Enterprise 裝置新增應用程式設定原則
titleSuffix: Microsoft Intune
description: 在 Microsoft Intune 中使用應用程式設定原則，以提供使用者執行受控 Google Play 應用程式時的設定。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d0b6f3fe-2bd4-4518-a6fe-b9fd115ed5e0
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f49d1e419eb7199d2a7cf20f03959689a5f5fa44
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342487"
---
# <a name="add-app-configuration-policies-for-managed-android-enterprise-devices"></a>為受控的 Android Enterprise 裝置新增應用程式設定原則

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune 中的應用程式設定原則能為受控 Android Enterprise 裝置上的受控 Google Play 應用程式提供設定。 應用程式開發人員會公開受 Android 管理的應用程式組態設定。 Intune 會使用這些公開設定來讓管理員設定應用程式的功能。 應用程式設定原則會指派給您的使用者群組。 每當應用程式檢查是否有原則設定時 (通常是應用程式第一次執行時)，便會使用這些原則設定。

> [!NOTE]  
> 並非每個應用程式都支援應用程式設定。 請連絡應用程式開發人員，以了解他們的應用程式是否支援應用程式設定原則。

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選擇 [應用程式]   > [應用程式設定原則]   > [新增]   > [受控裝置]  。 請注意，您可以在 [受控裝置]  和 [受管理的應用程式]  之間選擇。 如需詳細資訊，請參閱[支援應用程式設定的應用程式](app-configuration-policies-overview.md#apps-that-support-app-configuration)。
3. 在 [基本]  頁面上，設定下列詳細資料：
    - **名稱** - 在 Azure 入口網站中顯示的設定檔名稱。
    - **描述** - 在 Azure 入口網站中顯示的設定檔描述。
    - [裝置註冊類型]  - 此設定會設定為 [受控裝置]  。
4. 選取 [Android Enterprise]  作為 [平台]  。
5. 按一下 [目標應用程式]  旁邊的 [選取應用程式]  。 [相關聯的應用程式]  窗格隨即顯示。 
6. 在 [相關聯的應用程式]  窗格上，選擇要與設定原則相關聯的受控應用程式，然後按一下 [確定]  。
7. 按一下 [下一步]  以顯示 [設定]  頁面。
8. 按一下 [新增]  以顯示 [新增權限]  窗格。
9. 按一下您覆寫的權限。 所授與權限將會覆寫所選應用程式的 [預設應用程式權限] 原則。
10. 針對每個權限設定 [權限狀態]  。 您可以選擇 [提示]  、[自動授與]  或 [自動拒絕]  。 如需權限的詳細資訊，請參閱[使用 Intune，透過 Android Enterprise 設定將裝置標示為相容或不相容](../protect/compliance-policy-create-android-for-work.md)。
11. 在下拉式方塊中，選取 [組態設定格式]  。 選取下列其中一種方法來新增設定資訊：
    - **使用設定設計工具**
    - **輸入 JSON 資料**<br><br>
    如需使用設定設計工具的詳細資料，請參閱[使用設定設計工具](#use-the-configuration-designer)。 如需輸入 XML 資料的詳細資料，請參閱[輸入 JSON 資料](#enter-json-data)。
12. 按一下 [下一步]  以顯示 [指派]  頁面。
13. 在 [指派給]  旁邊的下拉式方塊中，選取 [選取的群組]  、[所有使用者]  、[所有裝置]  ，或 [所有使用者和所有裝置]  來指派應用程式設定原則。

    ![[原則指派] [包含] 索引標籤的螢幕擷取畫面](./media/app-configuration-policies-use-ios/app-config-policy01.png)

14. 在下拉式方塊中，選取 [所有使用者]  。

    ![[原則指派 - 所有使用者] 下拉式選項的螢幕擷取畫面](./media/app-configuration-policies-use-ios/app-config-policy02.png)

15. 按一下 [選取要排除的群組]  以顯示相關的窗格。

    ![[原則指派 - 選取要排除的群組] 窗格的螢幕擷取畫面](./media/app-configuration-policies-use-ios/app-config-policy03.png)

16. 選擇您要排除的群組，然後按一下 [選取]  。

    >[!NOTE]
    >新增群組時，如已包含任何其他群組用於指定的指派類型，就會預先選取且無法針對其他包含指派類型進行變更。 因此，已使用的該群組，不能用為排除的群組。

17. 按一下 [下一步]  以顯示 [檢閱 + 建立]  頁面。
18. 按一下 [建立]  以將應用程式設定原則新增至 Intune。

## <a name="use-the-configuration-designer"></a>使用設定設計工具

當應用程式已設計為支援組態設定時，您可以針對受控 Google Play 應用程式使用設定設計工具。 設定會套用至已在 Intune 中註冊的裝置。 設計工具可讓您針對應用程式公開的設定，設定特定的設定值。

1. 選取 [新增]  。 選擇您要為應用程式輸入的組態設定清單。

    如果您使用 GMail 或 Nine Work 作為電子郵件應用程式，請參閱[用來設定電子郵件的 Android Enterprise 裝置設定](../configuration/email-settings-android-enterprise.md)以取得這些設定的詳細資訊。

2. 對於設定中的每個金鑰和值，請設定：

    - **值類型**：設定值的資料類型。 針對「字串」值類型，您可以視需要選擇變數或憑證設定檔作為值類型。
    - **設定值**：設定的值。 如果您為 [值類型]  選取變數或憑證，請從變數或憑證設定檔清單中進行選擇。 如果您選擇憑證，則會在執行階段填入部署至裝置之憑證的憑證別名。

### <a name="supported-variables-for-configuration-values"></a>支援的設定值變數

如果您選擇變數作為值類型，將可以選擇下列選項：

| 選項 | 範例 |
|----|----|
| AAD 裝置識別碼 | dc0dc142-11d8-4b12-bfea-cae2a8514c82 |
| 帳戶識別碼 | fc0dc142-71d8-4b12-bbea-bae2a8514c81 |
| Intune 裝置識別碼 | b9841cd9-9843-405f-be28-b2265c59ef97 |
| Domain | contoso.com |
| 郵件 | john@contoso.com |
| 部分 UPN | john |
| 使用者識別碼 | 3ec2c00f-b125-4519-acf0-302ac3761822 |
| 使用者名稱 | John Doe |
| 使用者主體名稱 | john@contoso.com |

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>在多重身分識別應用程式中只允許設定的組織帳戶 

針對 Android 裝置，請使用下列索引鍵/值組：

| **Key** | com.microsoft.intune.mam.AllowedAccountUPNs |
|---|---|
| **值** | <ul><li>一或多個以 <code>;</code> 分隔的 UPN。</li><li>只有允許的帳戶才是這個索引鍵所定義受控使用者帳戶。</li><li> 若為 Intune 註冊的裝置，<code>{{userprincipalname}}</code> 權杖可用來代表註冊的使用者帳戶。</li></ul> |

   > [!NOTE]
   > 只允許搭配多身分識別使用已設定的組織帳戶時，您必須使用 Android 版 Outlook 2.2.222 與更新版本、Android 版 Word、Excel、PowerPoint 16.0.9327.1000 與更新版本，或 Android 版 OneDrive 5.28 與更新版本。<p></p>
   > 身為 Microsoft Intune 管理員，您可以控制要新增至受控裝置上 Microsoft Office 應用程式的使用者帳戶。 您可以僅允許組織使用者帳戶進行存取，並封鎖已註冊裝置上的個人帳戶。 支援的應用程式會處理應用程式設定和移除，並封鎖未經核准的帳戶。<p></p>

## <a name="enter-json-data"></a>輸入 JSON 資料

應用程式 (例如套件組合類型的應用程式) 上的某些組態設定無法使用設定設計工具來設定。 請使用 JSON 編輯器來設定那些值。 安裝應用程式時，會自動將設定值提供給應用程式。

1. 對於 [組態設定格式]  ，請選取 [進入 JSON 編輯器]  。
2. 您可以在編輯器中定義組態設定的 JSON 值。 您可以選擇 [下載 JSON 範本]  來下載之後可以設定的範例檔案。
3. 選擇 [確定]  ，然後選擇 [新增]  。

原則隨即建立，並顯示在清單中。

當指派的應用程式在裝置上執行時，會依照您在應用程式設定原則中的設定執行。

## <a name="preconfigure-the-permissions-grant-state-for-apps"></a>預先設定應用程式的權限授與狀態

您也可以預先設定應用程式權限以存取 Android 裝置功能。 根據預設，需要裝置權限 (例如存取位置或裝置相機) 的 Android 應用程式會提示使用者接受或拒絕授與權限。

以使用裝置麥克風的應用程式為例。 系統會提示使用者授與應用程式使用麥克風的權限。

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，選取 [應用程式]   > [應用程式設定原則]   >  [新增]   > [受控裝置]  。
2. 新增下列屬性：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，良好的原則名稱是**適用於整家公司的 Android Enterprise 提示權限應用程式原則**。
    - **描述**。 輸入設定檔的描述。 這是選擇性設定，但建議執行。
    - **裝置註冊類型**：此設定已設定為 [受控裝置]  。
    - **平台**：選取 [Android]  。

3. 選取 [相關聯的應用程式]  。 選擇您想要定義設定原則的應用程式。 從 Android 工作設定檔應用程式清單中，選取您已經使用 Intune 核准並同步處理的應用程式。
4. 選取 [權限]   > [新增]  。 從清單中，選取可用的應用程式權限 > [確定]  。
5. 為每個權限選取要使用此原則授與的選項：
    - **提示**。 提示使用者接受或拒絕。
    - **自動授與**。 自動核准且不通知使用者。
    - **自動拒絕**。 自動拒絕且不通知使用者。
6. 若要指派應用程式設定原則，請選取應用程式設定原則 > [指派]   > [選取群組]  。 選擇要指派的使用者群組 > [選取]  。
7. 選擇 [儲存]  來指派原則。

## <a name="additional-information"></a>其他資訊

- [將受控 Google Play 應用程式指派給 Android Enterprise 裝置](apps-add-android-for-work.md#assigning-a-managed-google-play-app-to-android-enterprise-work-profile-devices)
- [部署 iOS/iPadOS 與 Android 版 Outlook 應用程式組態設定](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune) \(部分機器翻譯\)

## <a name="next-steps"></a>後續步驟

繼續[指派](apps-deploy.md)及[監視](apps-monitor.md)應用程式。
