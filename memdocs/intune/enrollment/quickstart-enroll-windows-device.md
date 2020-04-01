---
title: 快速入門 - 在 Microsoft Intune 中註冊您的 Windows 10 Desktop 裝置
description: 快速入門 - 使用公司入口網站在 Microsoft Intune 中註冊您的 Windows 10 Desktop 裝置。
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f70c8487d9cb30b2a7cced63e6e019541f73704
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327062"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>快速入門：註冊您的 Windows 10 裝置

在此快速入門中，您會先扮演 Intune 使用者角色並在 Microsoft Intune 中註冊您的 Windows 10 裝置。 然後，您會返回 Intune 並確認已註冊裝置。

在 Microsoft Intune 中註冊裝置，可讓 Windows 10 裝置存取組織的安全資料，包括電子郵件、檔案和其他資源。 這適用於 Windows 10 Desktop 和 Windows 10 Mobile 裝置。 註冊您的裝置能夠協助保護您和您的組織，並且協助區隔您的工作資料與個人資料。

> [!TIP]
> 了解當您[在 Intune 中註冊裝置](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md)時會發生什麼事，以及那對[裝置上的資訊](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md)有何意義。

如果沒有 Intune 訂用帳戶，請[註冊免費試用帳戶](../fundamentals/free-trial-sign-up.md)。

## <a name="prerequisites"></a>先決條件

- Microsoft Intune 訂用帳戶 - [註冊免費試用帳戶](../fundamentals/free-trial-sign-up.md)
- 若要完成此快速入門，您必須完成[在 Intune 中設定自動註冊](quickstart-setup-auto-enrollment.md)的步驟。

## <a name="confirm-your-windows-10-desktop-version"></a>確認您的 Windows 10 Desktop 版本

註冊 Windows 10 Desktop 之前，您必須確認已安裝的 Windows 版本。

1. 以滑鼠右鍵按一下 Windows **開始**圖示，然後選取 [設定]  以顯示 [Windows 設定] 選項。

   ![[Windows 設定] - [系統] 的螢幕擷取畫面](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. 選取 [系統]   > [關於]  。 

   ![您系統設定的螢幕擷取畫面](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > 您也可以在**搜尋列**中鍵入「關於您的電腦」一詞，然後選取 [關於您的電腦]  。

3. 在 [設定]  視窗中，您會看到電腦的**Windows 規格**清單。 在此清單中，找出 [版本]  。

4. 確認 Windows 10 的 [版本]  為 **1607 或更新版本**。

    > [!IMPORTANT]
    > 此快速入門中所顯示的步驟適用 Windows 10 **1607 版或更新版本**如果您的版本是 **1511 或較舊版本**，請繼續進行[這些步驟](../user-help/enroll-windows-10-device.md)。  

## <a name="enroll-windows-10-desktop"></a>註冊 Windows 10 Desktop

1. 返回 [Windows 設定]，然後選取 [帳戶]  。

   ![您系統設定 - [帳戶] 的螢幕擷取畫面](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. 選取 [存取公司或學校資源]   > [連線]  。

    ![選取 [存取公司或學校帳戶]](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. 使用您的工作或學校帳戶登入 Intune，然後選取 [下一步]  。 如果遵循 [建立使用者並指派授權](../fundamentals/quickstart-create-user.md) 快速入門，就可以使用已建立的使用者帳戶登入。

    > [!NOTE]
    > 如果您要設定 ".onmicrosoft.com"，使用者帳戶將會以 **.onmicrosoft.com** 作為帳戶地址的一部分。 

   ![輸入您的工作或學校帳戶](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    您會看到一則訊息，指出公司或學校正在登錄裝置。

4. 當您看到 [已全部完成]  時 的畫面時，請選取 [完成]。  大功告成。

5. 您現在會在 Windows Desktop 的 [存取公司或學校資源]  設定中看到新增的帳戶。

   ![新增帳戶的螢幕擷取畫面](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    如果已遵循前述步驟，但仍無法存取自己的工作或學校電子郵件帳戶和檔案，請遵循[針對當看見 [存取公司或學校資源] 時需遵循的步驟進行疑難排解](../user-help/troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-access-work-or-school)中步驟。

## <a name="confirm-your-device-enrollment-in-intune"></a>確認在 Intune 中註冊您的裝置

1. 請以全域管理員或 Intune 服務管理員身分登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置]   > [所有裝置]  以檢視在 Intune 中註冊的裝置。
3. 確認您已在 Intune 中註冊其他裝置。

   ![Intune 已註冊裝置的螢幕擷取畫面](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>清除資源

若要解除註冊您的 Windows 裝置，請參閱[從管理移除您的 Windows 裝置](../user-help/unenroll-your-device-from-intune-windows.md)。

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已了解如何在 Intune 中註冊 Windows 10 裝置。 您可以了解跨所有平台註冊裝置的其他方式。 如需透過 Intune 使用裝置的詳細資訊，請參閱[使用受控裝置完成工作](../user-help/use-managed-devices-to-get-work-done.md)。

若要繼續參閱此 Intune 快速入門系列，請前往下一個快速入門。

> [!div class="nextstepaction"]
> [快速入門：為 Android 裝置設定必要的密碼長度](../protect/quickstart-set-password-length-android.md)
