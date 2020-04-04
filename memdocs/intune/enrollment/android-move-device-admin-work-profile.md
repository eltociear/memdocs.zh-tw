---
title: 將 Android 裝置從裝置系統管理員移至工作設定檔管理
titleSuffix: Microsoft Intune
description: 在 Intune 中，將 Android 裝置從裝置系統管理員移至工作設定檔管理。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c8c521dc0899b3429de85e95116a6277d724771
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327283"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>將 Android 裝置從裝置系統管理員移至工作設定檔管理

您可以使用合規性設定，協助使用者將其 Android 裝置從裝置系統管理員移至工作設定檔管理，以**禁止使用裝置系統管理員管理的裝置**。 如果裝置會透過裝置系統管理員來管理，則此設定可讓您將裝置設定為不符合規範。 

當使用者看到裝置因為此原因而不符合規範時，可以點選 [解決]  。 系統會將使用者帶往檢查清單，並引導其完成下列動作：
1. 從裝置系統管理員管理取消註冊
2. 在工作設定檔管理中註冊
3. 解決任何合規性問題。 

## <a name="prerequisites"></a>先決條件

- 使用者必須擁有 [Android 裝置系統管理員註冊的裝置](android-enroll-device-administrator.md)，其中具備 Android 公司入口網站 5.0.4720.0 版或更新版本。
- 透過[將 Intune 租用戶帳戶連線到 Android Enterprise 帳戶](connect-intune-android-enterprise.md)，以設定 Android 公司設定檔管理。
- 針對要移至 Android 工作設定檔的使用者群組，[設定 Android Enterprise 工作設定檔註冊](android-work-profile-enroll.md)。
- 考慮增加您的使用者裝置限制。 從裝置系統管理員管理取消註冊裝置時，可能不會立即移除裝置記錄。 若要在這段期間提供緩衝，您可能需要增加裝置限制容量，讓使用者可以在工作設定檔管理中註冊。
  - 針對每位使用者的裝置數目上限，[設定 Azure Active Directory 裝置設定](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) \(部分機器翻譯\)。
  - 藉由設定裝置限制來調整 [Intune 裝置限制](enrollment-restrictions-set.md#create-a-device-limit-restriction)。 

## <a name="create-device-compliance-policy"></a>建立裝置合規性原則

1. 在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [裝置]   > [合規性政策]   > [原則]   > [建立原則]  。

    ![建立原則](./media/android-move-device-admin-work-profile/create-policy.png)

2. 在 [建立原則]  頁面上，將 [平台]  設定為 [Android 裝置系統管理員]   > [建立]  。
3. 在 [基本]  頁面上，輸入**名稱**和**描述** > [下一步]  。

    ![基本頁面](./media/android-move-device-admin-work-profile/basics.png)
    
4. 在 [合規性設定]  頁面的 [裝置健康情況]  區段中，將 [禁止使用裝置系統管理員管理的裝置]  設定為 [是]   > [下一步]  。

    ![封鎖裝置](./media/android-move-device-admin-work-profile/block-devices.png)

5. 在 [位置]  頁面上，視需要新增位置 > [下一步]  。
6. 在 [因不符合規範而採取的動作]  上，您可以設定 [傳送電子郵件給使用者]  動作。

    ![傳送電子郵件](./media/android-move-device-admin-work-profile/send-email.png)


    在電子郵件中，您可以在給使用者的訊息中包含下列 URL。 此 URL 將啟動 Android 公司入口網站，並移至 [更新裝置設定]  頁面。 此頁面會啟動其流程以移至工作設定檔管理。
    - [https://portal.manage.microsoft.com/UpdateSettings.aspx](https://portal.manage.microsoft.com/UpdateSettings.aspx)。
    - 若為美國政府，您可以改用此連結：[https://portal.manage.microsoft.us/UpdateSettings.aspx](https://portal.manage.microsoft.us/UpdateSettings.aspx)。
  
    > [!NOTE]
    > - 當然，您可以在與使用者通訊的連結中，使用使用者易記的超文字。 但是，不要使用 URL 短網址，因為若該方式變更，連結可能無法正常作用。
    > - 如果 Android 公司入口網站已開啟且在背景中，則當使用者點選連結時，可能會改為前往其已開啟的最後一個頁面。
    > - 使用者必須在 Android 裝置上點選連結。 如果改為貼入瀏覽器，就不會啟動 Android 公司入口網站。 

    選擇 [下一步]  。

7. 在 [範圍標籤]  頁面上，選取您想要包含的任意範圍標籤。
8. 在 [指派]  頁面上，將原則指派給含有已使用裝置系統管理員管理註冊之裝置的群組 > [下一步]  。
9. 在 [檢閱 + 建立]  頁面上，確認您的所有設定，然後選取 [建立]  。

## <a name="troubleshooting"></a>疑難排解

[移至新裝置管理設定的終端使用者流程](../user-help/move-to-new-device-management-setup.md) \(英文\) 會引導使用者從裝置系統管理員管理取消註冊，然後開始設定工作設定檔管理。 使用者必須擁有 [Android 裝置系統管理員註冊的裝置](android-enroll-device-administrator.md)，其中具備 Android 公司入口網站 5.0.4720.0 版或更新版本。

### <a name="user-sees-an-error-after-tapping-resolve"></a>使用者在點擊 [解決] 之後看到錯誤
如果使用者在點擊 [解決]  按鈕之後看到錯誤，可能是因為下列其中一個原因：
- 工作設定檔註冊未正確設定 (可能是 Android Enterprise 帳戶未連線，或已將註冊限制設定為禁止工作設定檔註冊)。
- 裝置正在執行不支援工作設定檔註冊的 Android 4.4 或更舊版本。 
- 裝置製造商不支援此裝置型號的工作設定檔註冊。

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>[解決] 按鈕未出現在使用者的裝置上
如果使用者在按照上述裝置合規性政策設定目標之後，於裝置系統管理員管理中註冊，則 [解決]  按鈕將不會出現在使用者的裝置上。

若要讓 [解決]  按鈕出現，使用者必須將安裝延後，並從通知中重新啟動流程。

若要避免這種情況，請使用註冊限制來禁止在裝置系統管理員管理中註冊。

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>使用者在點擊 [更新裝置設定] 頁面的 URL 之後看到錯誤
使用者在瀏覽器上點擊 Android 公司入口網站之 [更新裝置設定]  頁面的 URL 後，可能會看到錯誤。 此錯誤可能是因下列其中一個原因所致：
- 裝置不是 Android。
- Android 裝置不具公司入口網站應用程式。
- Android 公司入口網站版本早於 5.0.4720.0。
- Android 裝置使用 Android 6 或更早版本。 

## <a name="next-steps"></a>後續步驟
[查看終端使用者流程](../user-help/move-to-new-device-management-setup.md)
[使用 Intune 管理 Android 工作設定檔裝置](android-enterprise-overview.md)
