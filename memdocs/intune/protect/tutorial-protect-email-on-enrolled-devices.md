---
title: 教學課程：保護受控裝置上的 Exchange Online 電子郵件
titleSuffix: Microsoft Intune
description: 了解如何使用 iOS Intune 合規性政策和 Azure AD 條件式存取來要求受控裝置和 Outlook 應用程式，以保護 Exchange Online。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/21/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9921fb9e22b17a47c588dfcbfbf502e00ef2aadd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349871"
---
# <a name="tutorial-protect-exchange-online-email-on-managed-devices"></a>教學課程：保護受控裝置上的 Exchange Online 電子郵件

了解如何搭配條件式存取使用裝置合規性政策，以確保 iOS 裝置只能在受到 Intune 管理並使用核准的電子郵件應用程式時，才能存取 Exchange Online 電子郵件。

您將在本教學課程中了解如何：

> [!div class="checklist"]
> * 建立 Intune iOS 裝置合規性政策來設定裝置必須符合才能視為合規的條件。
> * 建立 Azure Active Directory (Azure AD) 條件式存取原則，要求 iOS 裝置在 Intune 中註冊、符合 Intune 原則，並使用核准的 Outlook 行動應用程式來存取 Exchange Online 電子郵件。

如果您沒有 Intune 訂用帳戶，請[註冊免費試用帳戶](../fundamentals/free-trial-sign-up.md)。

## <a name="prerequisites"></a>先決條件

您將需要在本教學課程中，使用以下訂用帳戶測試租用戶：

- Azure Active Directory Premium ([免費試用](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))

- 包含 Exchange ([免費試用](https://go.microsoft.com/fwlink/p/?LinkID=510938)) 的 Office 365 商務版訂用帳戶

在開始之前，請先依照下列內容中的步驟，建立適用於 iOS 裝置的測試裝置設定檔：[Quickstart:建立 iOS/iPadOS 的電子郵件裝置設定檔](../configuration/quickstart-email-profile.md)。

## <a name="sign-in-to-intune"></a>登入 Intune

以[全域管理員](../fundamentals/users-add.md#types-of-administrators)或 Intune [服務管理員](../fundamentals/users-add.md#types-of-administrators)身分登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。 如果您已建立 Intune 試用版訂閱，則用來建立訂閱的帳戶是全域管理員。

## <a name="create-the-ios-device-compliance-policy"></a>建立 iOS 裝置合規性政策

建立 Intune 裝置合規性政策來設定裝置必須符合才能視為合規的條件。 我們將會在本教學課程中，為 iOS 裝置建立裝置合規性政策。 合規性政策是平台特定的，因此您想要評估每個裝置平台都需要有個別的合規性政策。

1. 在 Intune 中，選取 [裝置]   > [合規性原則]   > [建立原則]  。

2. 針對 [名稱]  ，請輸入 **iOS 合規性原則測試**。

3. 針對 [描述]  ，請輸入 **iOS 合規性原則測試**。

4. 針對 [平台]  ，選取 [iOS/iPadOS]  。

5. 選取 [設定]   > [電子郵件]  。

   1. 在 [需要行動裝置具有受管理的電子郵件設定檔]  旁邊選取 [必要]  。

   2. 選取 [確定]  。

   ![設定電子郵件合規性政策以要求受管理的電子郵件設定檔](./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-email.png)

6. 選取 [裝置健全狀況]  。 在 [破解的裝置]  旁邊選取 [封鎖]  ，然後選取 [確定]  。

7. 選取 [系統安全性]  並進入 [密碼]  設定。 針對本教學課程，請選取下列建議設定：

   - 針對 [需要密碼才可解除鎖定行動裝置]  選取 [必要]  。

   - 針對 [簡單密碼]  ，選取 [封鎖]  。

   - 針對 [最小密碼長度]  ，輸入 **4**。

     > [!TIP]
     > 灰色且為斜體的預設值僅為建議。 您必須取代建議的值以設定某個設定。

   - 針對 [必要的密碼類型]  ，選擇 [英數字元]  。

   - 針對 [在螢幕鎖定最少幾分鐘後必須輸入密碼]  ，選擇 [立即]  。

   - 針對 [密碼到期 (天數)]  ，輸入 **41**。

   - 針對 [避免重複使用以前用過的密碼次數]  ，輸入 **5**。
 
   ![設定電子郵件合規性政策的密碼設定](./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-system-security.png)

8. 選取 [確定]  ，然後再選取一次 [建立]  。

9. 選取 [建立]  。

## <a name="create-the-conditional-access-policy"></a>建立條件式存取原則

現在我們將先建立條件式存取原則來要求所有裝置平台在 Intune 中註冊，並遵守我們的 Intune 合規性政策，然後它們才能存取 Exchange Online。 我們也將要求使用 Outlook 應用程式存取電子郵件。 條件式存取原則可以在 Azure AD 入口網站或 Intune 入口網站中設定。 因為我們已經在 Intune 入口網站中，所以我們將在這裡建立原則。

1. 在 Intune 中，選取 [端點安全性]   > [條件式存取]   > [新增原則]  。

2. 針對 [名稱]  ，請輸入 **Office 365 電子郵件測試原則**。

3. 在 [指派]  底下，選取 [使用者和群組]  。 在 [包含]  索引標籤中，選取 [所有使用者]  ，然後選取 [完成]  。

4. 在 [指派]  底下，選取 [雲端應用程式或動作]  。 因為我們想要保護 Office 365 Exchange Online 電子郵件，所以我們將依照下列步驟選取它：

   1. 在 [包含]  索引標籤上，選擇 [選取應用程式]  。

   2. 選擇 [選取]  。 

   3. 在應用程式清單中，選取 [Office 365 Exchange Online]  ，然後選擇 [選取]  。 

   4. 選取 [完成]  。
  
   ![選取 Office 365 Exchange Online 應用程式](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-apps.png)

5. 在 [指派]  底下，選取 [條件]   > [裝置平台]  。

   1. 在 [設定]  底下，選取 [是]  。

   2. 在 [包含]  索引標籤中，選取 [任何裝置]  ，然後選取 [完成]  。 

   3. 再次選取 [完成]  。

   ![包含任何裝置](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-device-platforms.png)

6. 在 [指派]  底下，選取 [條件]   > [用戶端應用程式]  。

   1. 在 [設定]  底下，選取 [是]  。

   2. 針對本教學課程，選取 [行動裝置 App 及桌面用戶端]  與 [新式驗證用戶端]  (指像 iOS 版 Outlook 和 Android 版 Outlook 這樣的 App)。 清除所有其他核取方塊。

   3. 選取 [完成]  ，然後再次選取 [完成]  。

   ![選取應用程式和用戶端](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-client-apps.png)

7. 在 [存取控制]  底下，選取 [授與]  。

   1. 在 [授與]  窗格中，選取 [授與存取權]  。

   2. 選取 [裝置需要標記為合規]  。

   3. 選取 [需要經過核准的用戶端應用程式]  。

   4. 在 [針對多個控制項]  底下，選取 [需要所有選取的控制項]  。 此設定可確保選取的兩項需求會在裝置嘗試存取電子郵件時強制執行。

   5. 選擇 [選取]  。

   ![選取控制項](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-grant-access.png)

8. 在 [啟用原則]  底下，選取 [開啟]  。

   ![啟用原則](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-enable-policy.png)

9. 選取 [建立]  。

## <a name="try-it-out"></a>試試看

透過使用已建立的原則，所有嘗試登入 Office 365 電子郵件的 iOS/iPadOS 裝置都必須在 Intune 中註冊，並使用 iOS/iPadOS 版 Outlook 行動應用程式。 若要在 iOS 裝置上測試此案例，請嘗試使用您測試租用戶中使用者的認證登入 Exchange Online。 系統將會提示您註冊裝置並安裝 Outlook 行動應用程式。

1. 若要在 iPhone 上測試，請前往 [設定]   > [密碼與帳戶]   > [新增帳戶]   > [Exchange]  。

2. 輸入您測試租用戶中使用者的電子郵件地址，然後按 [下一步]  。

3. 按 [登入]  。

4. 輸入測試使用者的密碼，然後按 [登入]  。

5. 此時會顯示訊息，說明您的裝置必須受到管理才能存取資源，並提供註冊選項。

## <a name="clean-up-resources"></a>清除資源

當不再需要測試原則時，您可以將它們移除。
1. 請以全域管理員或 Intune 服務管理員身分登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 選取 [裝置]   > [合規性政策]  。

3. 在 [原則名稱]  清單中，選取測試原則的操作功能表 ( **...** )，然後選取 [刪除]  。 選取 [確定]  來確認。

4. 選取 [端點安全性]   > [條件式存取]  。

5. 在 [原則名稱]  清單中，選取測試原則的操作功能表 ( **...** )，然後選取 [刪除]  。 選取 [是]  確認。

## <a name="next-steps"></a>後續步驟

您已經在本教學課程中，建立要求 iOS 裝置在 Intune 中註冊，並使用 Outlook 應用程式存取 Exchange Online 電子郵件的原則。 若要了解如何搭配條件式存取使用 Intune 來保護其他應用程式和服務 (包括 Office 365 Exchange Online 的 Exchange ActiveSync 用戶端)，請參閱[設定條件式存取](conditional-access.md)。
