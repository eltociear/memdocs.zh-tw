---
title: 快速入門：建立 iOS/iPadOS 裝置的電子郵件裝置設定檔
titleSuffix: Microsoft Intune
description: 了解如何使用 Microsoft Intune 建立電子郵件裝置設定檔，讓 iOS/iPadOS 裝置可以安全地連線至公司電子郵件。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bc170c5260dc099d0a2b4109ed119572e0dbaff
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086862"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>快速入門：建立 iOS/iPadOS 的電子郵件裝置設定檔

在本快速入門中，您會看到如何建立 iOS/iPadOS 裝置的電子郵件裝置設定檔。 此設定檔指定 iOS/iPadOS 裝置上內建電子郵件應用程式所需的設定來連線至公司電子郵件。 電子郵件裝置設定檔可協助將各個裝置的設定標準化，並讓終端使用者不需要任何設定，就能從其個人裝置存取公司電子郵件。 若要進一步保護您的電子郵件，您可以使用電子郵件設定檔來判斷裝置是否符合規範，然後將條件式存取設定為僅允許符合規範的裝置存取電子郵件。 如需電子郵件設定檔的詳細資訊，請參閱[如何在 Microsoft Intune 中設定電子郵件設定](email-settings-configure.md)

如果沒有 Intune 訂用帳戶，請[註冊免費試用帳戶](../fundamentals/free-trial-sign-up.md)。

## <a name="sign-in-to-intune"></a>登入 Intune

請以全域管理員或 Intune 服務管理員身分登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。 如果您已建立 Intune 試用版訂閱，則用來建立訂閱的帳戶是全域管理員。

## <a name="create-an-iosipados-email-profile"></a>建立 iOS/iPadOS 電子郵件設定檔

1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取並移至 [裝置]   > [組態設定檔]   > [建立設定檔]  。
   ![在 Intune 中建立 iOS/iPadOS 的電子郵件設定檔](./media/quickstart-email-profile/ios-create-profile.png)

3. 輸入下列內容：
   - **平台**：選取 [iOS/iPadOS] 
   - **設定檔**：選取 [電子郵件] 
  
4. 選取 [建立]  。

5. 在 [基本資訊]  中，輸入下列內容：
   - **名稱**：為新的設定檔輸入描述性名稱。 在此範例中，輸入 **iOS require work email**。
   - **描述**：輸入**要求 iOS/iPadOS 裝置使用工作電子郵件**


        ![建立用於 Intune 中 iOS/iPadOS 裝置的電子郵件設定檔](./media/quickstart-email-profile/ios-email-profile-name.png)

6. 選取 [下一步]  。

7. 在 [組態設定]  中，輸入下列設定 (保留其他設定的預設值)：
   - **電子郵件伺服器**：在本快速入門中，輸入 **outlook.office365.com**。 此設定指定 iOS/iPadOS 郵件應用程式將用來連線至電子郵件之電子郵件伺服器的 Exchange 位置 (URL)。
   - **帳戶名稱**：輸入**公司電子郵件**。
   - **AAD 中的使用者名稱屬性**：此名稱是 Intune 從 Azure Active Directory (Azure AD) 中取得的屬性。 Intune 會使用此名稱動態產生此設定檔的使用者名稱。 在本快速入門中，假設我們想要使用**使用者主體名稱**作為設定檔的使用者名稱 (例如 user1@contoso.com)。
   - **AAD 中的電子郵件地址屬性**：此設定是 Azure AD 中將用來登入 Exchange 的電子郵件地址。 在本快速入門中，選取 [使用者主體名稱]  。
   - **驗證方法**：在本快速入門中，選取 [使用者名稱和密碼]  。 (如果已經設定 Intune 的憑證，則也可以選擇 [憑證]  。)

8. 選取 [下一步]  。

9. 在 [範圍標籤]  (選擇性) 中，選取 [下一步]  。 我們將不會針對此設定檔使用範圍標籤。

10. 在 [指派]  中，使用 [指派給]  下拉式清單選取 [所有使用者和所有裝置]  。  然後，選取 [下一步]  。

11. 在 [檢閱 + 建立]  中，檢閱您的設定。 當您選取 [建立]  時，系統會儲存您的變更，然後指派設定檔。 

## <a name="clean-up-resources"></a>清除資源

如果不想要使用為其他教學課程或測試建立的設定檔，則可以立即將其刪除。

1. 在 Intune 中，選取 [裝置]   > [裝置設定]  。
2. 選取您所建立的測試設定檔：**iOS/iPadOS require work email**，然後選取 [刪除]  。 

## <a name="next-steps"></a>後續步驟

在本快速入門中，您已建立 iOS/iPadOS 裝置的電子郵件設定檔。 現在，您可以使用此設定檔來判斷 iOS/iPadOS 裝置是否符合規範，方法是建立將任何不符合該設定檔之 iOS/iPadOS 裝置標記為不符合規範的合規性政策。 如需進一步保護，您可以建立條件式存取原則，以封鎖不符合規範的 iOS/iPadOS 裝置存取電子郵件。 如需裝置合規性原則的詳細資訊，請參閱[開始使用 Intune 中的裝置合規性原則](../protect/device-compliance-get-started.md)。

> [!div class="nextstepaction"]
> [教學課程：保護受控裝置上的 Exchange Online 電子郵件](../protect/tutorial-protect-email-on-enrolled-devices.md)
