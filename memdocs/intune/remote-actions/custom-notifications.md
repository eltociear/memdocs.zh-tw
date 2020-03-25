---
title: 使用 Microsoft Intune 將自訂通知傳送給使用者
titleSuffix: Microsoft Intune
description: 使用 Intune 來建立自訂推播通知，並將其傳送給 iOS/iPadOS 和 Android 裝置的使用者
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b79c7a9cdc740984e1ace90b37bdea8dbdc70de
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220246"
---
# <a name="send-custom-notifications-in-intune"></a>在 Intune 中傳送自訂通知

使用 Microsoft Intune 將自訂通知傳送給受控 iOS/iPadOS 和 Android 裝置的使用者。 這些訊息會在使用者裝置上顯示為來自公司入口網站應用程式與來自 Microsoft Intune 應用程式的標準推播通知，與裝置上其他應用程式通知的出現方式一樣。 macOS 和 Windows 裝置均不支援 Intune 自訂通知。

自訂通知訊息包含簡短的標題和訊息本文，長度為 500 個字元或更少。 這些訊息可以針對任何一般通訊目的來自訂。

### <a name="what-the-notification-looks-like-on-an-iosipados-device"></a>通知在 iOS/iPadOS 裝置上的外觀

如果您已在 iOS/iPadOS 裝置上開啟公司入口網站應用程式，則通知類似下列螢幕擷取畫面：

> [!div class="mx-imgBorder"]
> ![公司入口網站 iOS/iPadOS 測試通知](./media/custom-notifications/105046-1.png)

如果裝置已鎖定，則通知類似下列螢幕擷取畫面：

> [!div class="mx-imgBorder"]
> ![鎖定的裝置 iOS/iPadOS 測試通知](./media/custom-notifications/105046-2.png)

### <a name="what-the-notification-looks-like-on-an-android-device"></a>通知在 Android 裝置上的外觀

如果您已在 Android 裝置上開啟公司入口網站應用程式，則通知類似下列螢幕擷取畫面：

> [!div class="mx-imgBorder"]
> ![Android 測試通知](./media/custom-notifications/105046-3.png)

## <a name="common-scenarios-for-sending-custom-notifications"></a>傳送自訂通知的常見案例  

- 通知所有員工排程的變更，例如，因為惡劣氣候而放假。
- 將通知傳送至單一裝置的使用者，以傳達緊急要求，例如，重新啟動裝置以完成更新的安裝。

## <a name="considerations-for-using-custom-notifications"></a>使用自訂通知的考量

**裝置設定**

- 裝置必須先安裝公司入口網站應用程式或 Microsoft Intune 應用程式，使用者才能接收自訂通知。 他們也必須設定權限以允許公司入口網站應用程式或 Microsoft Intune 應用程式傳送推播通知。 視需要，公司入口網站應用程式和 Microsoft Intune 應用程式可能會提示使用者允許通知。
- 在 Android 上，Google Play Services 是必要的相依性。
- 裝置必須已註冊 MDM。

**權限**：

- 若要將通知傳送至群組，您的帳戶在 Intune 中必須具有下列 RBAC 權限：[組織]   > [更新]  。
- 若要將通知傳送至裝置，您的帳戶在 Intune 中必須具有下列 RBAC 權限：[遠端工作]   > [傳送自訂通知]  。

**建立通知**：
 
- 若要建立訊息，請使用已指派 Intune 角色的帳戶，其中包含如先前「權限」  區段中所述的正確權限。 若要將權限指派給使用者，請參閱[角色指派](../fundamentals/role-based-access-control.md#role-assignments)。
- 自訂通知限制為 50 個字元的標題，以及 500 個字元的訊息。  
- Intune 不會儲存先前所傳送自訂通知中的文字。 若要重新傳送訊息，您必須重新建立該訊息。  
- 每小時最多只能將 25 則訊息傳送至群組。 這是租用戶層級的限制。 將通知傳送至個人時，不適用這項限制。
- 將訊息傳送至個別裝置時，每小時最多只能傳送 10 則訊息給同一個裝置。
- 您可以將通知傳送給群組中的使用者。 將通知傳送至群組時，每則通知最多可直接針對 25 個群組傳送。 巢狀群組不計入於此總計中。 將通知傳送至群組時，訊息只會以群組中的使用者為目標，並傳送至該使用者已註冊的每部 iOS/iPadOS 或 Android 裝置。 以通知為目標時，將會忽略群組中的裝置。
- 您可以將通知傳送至單一裝置。 您不需要使用群組，而是選取裝置，然後使用遠端[裝置動作](device-management.md#available-device-actions)來傳送自訂通知。

**傳遞**：

- Intune 會將訊息傳送給使用者的公司入口網站應用程式或 Microsoft Intune 應用程式，其之後會建立推播通知。 使用者不需要登入應用程式，通知也會推播到裝置上，但該裝置必須已由目標使用者註冊。
- Intune、公司入口網站應用程式和 Microsoft Intune 應用程式無法保證能傳遞自訂通知。 自訂通知可能會延遲數小時顯示；如有此類延遲，則不應用於緊急訊息。
- Intune 中的自訂通知訊息會以標準推播通知形式顯示於裝置上。 如果公司入口網站應用程式在 iOS/iPadOS 裝置上開啟時收到通知，則會在應用程式中顯示該通知，而不會顯示為系統推播通知。  
- 取決於裝置設定，自訂通知可以在 iOS/iPadOS 和 Android 裝置的鎖定畫面上顯示。  
- 在 Android 裝置上，其他應用程式可能會存取您自訂通知中的資料。 請勿將其用於敏感通訊。  
- 最近取消註冊的裝置使用者，或已從群組中移除的使用者，可能仍會收到稍後傳送至該群組的自訂通知。  同樣地，如果您在將自訂通知傳送至群組之後將使用者新增至該群組，則最近新增的使用者可能會收到先前傳送的通知訊息。  

## <a name="send-a-custom-notification-to-groups"></a>將自訂通知傳送至群組

1. 使用具有建立及傳送通知權限的帳戶登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後移至 [租用戶管理]   > [自訂通知]  。  

2. 在 [基本] 索引標籤上指定下列各項，然後選取 [下一步]  以繼續。  
   - **標題** - 為此通知指定標題。 標題長度限制為 50 個字元。  
   - **本文** - 指定訊息。 訊息長度限制為 500 個字元。

   ![建立自訂通知](./media/custom-notifications/custom-notifications.png)  

3. 在 [指派]  索引標籤上，選取您要傳送此自訂通知的群組，然後選取 [下一步] 以繼續。 將通知傳送至群組時，只會以該群組中的使用者為目標；通知會傳送至該使用者已註冊的所有 iOS/iPadOS 和 Android 裝置。

4. 檢閱在 [檢閱 + 建立]  索引標籤上的資訊，並在準備好傳送通知時選取 [建立]  。  

Intune 會立即處理您建立的訊息。 只有 Intune 通知會確認訊息已傳送，該通知會確認已傳送自訂通知。  

![確認通知已傳送](./media/custom-notifications/notification-sent.png)  

Intune 不會追蹤您傳送的自訂通知，裝置也不會在裝置的通知中心之外記錄接收。 如果使用者要求公司入口網站或 Intune 應用程式內的支援，則通知可以包含於暫存診斷記錄中。

## <a name="send-a-custom-notification-to-a-single-device"></a>將自訂通知傳送至單一裝置

1. 使用有權建立及傳送通知的帳戶登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後移至 [裝置]   > [所有裝置]  。

2. 按兩下您想要傳送通知的受控裝置名稱，以開啟裝置的 [概觀]  頁面。

3. 在裝置的 [概觀]  頁面上，選取 [傳送自訂通知]  裝置動作以開啟 [傳送自訂通知]  窗格。 如果無法使用此選項，請選取頁面右上方的 [...]  (省略符號) 選項，然後選取 [傳送自訂通知]  。

4. 在 [傳送自訂通知]  窗格中，指定下列訊息詳細資料：  

   - **標題** - 為此通知指定標題。 標題長度限制為 50 個字元。  
   - **本文** - 指定訊息。 訊息長度限制為 500 個字元。  

5. 選取 [傳送]  以將自訂通知傳送至裝置。 不同於您傳送至群組的通知，您不會先設定指派或檢閱訊息，然後再傳送它。  

Intune 會立即處理訊息。 已傳送訊息的唯一確認是您將在主控台中收到的 Intune 通知，其會顯示您所傳送的訊息文字。  

## <a name="receive-a-custom-notification"></a>接收自訂通知

使用者可在裝置上看到 Intune 傳送的自訂通知訊息，作為來自公司入口網站應用程式或 Microsoft Intune 應用程式的標準推播通知。 這些通知類似於使用者從裝置上其他應用程式接收的推播通知。  

在 iOS/iPadOS 裝置上，如果收到通知時公司入口網站應用程式是開啟的，則通知會在應用程式中顯示，而不是顯示為推播通知。  

通知會持續顯示，直到使用者將其關閉為止。  

## <a name="next-steps"></a>後續步驟

[管理裝置](device-management.md)
