---
title: 使用 Samsung 的 Knox Mobile Enrollment 自動註冊 Android 裝置
titleSuffix: Microsoft Intune
description: 了解如何使用 Samsung KME 來註冊 Android 裝置
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: ''
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 30df0f9e-6e9e-4d75-a722-3819e33d480d
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d7ec41361571647cc417dc34ad29522d50477eb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339562"
---
# <a name="automatically-enroll-android-devices-by-using-samsungs-knox-mobile-enrollment"></a>使用 Samsung Knox Mobile Enrollment 自動註冊 Android 裝置

本主題能協助您使用 Samsung Knox Mobile Enrollment (KME) 來設定 Intune 以註冊支援的 Android 裝置。 透過搭配 Samsung KME 使用 Intune，您可以在使用者首次開啟其公司所擁有的 Android 裝置，並連線至 WiFi 或行動電話通訊網路時，對這些裝置進行大量註冊。 此外，在使用 Knox 部署應用程式時，將可以使用藍牙或 NFC 註冊裝置。

若要搭配 Samsung KME 進行 Intune 註冊，您必須依下列順序使用 Intune 和 Samsung Knox 入口網站：

1. 在 Knox 入口網站中：
    1. [建立 MDM 設定檔](#create-mdm-profile)
    2. [新增裝置](#add-devices)
    3. [將 MDM 設定檔指派至裝置](#assign-an-mdm-profile-to-devices)
2. 在 Knox 入口網站中，[設定使用者登入](#configure-how-end-users-sign-in)。
3. [散發裝置](#distribute-devices)。


從參與 Knox 部署計畫的授權經銷商處購買裝置時，包含這些裝置的裝置識別碼 (序號與 IMEI) 清單將會自動新增至 Knox 入口網站。


## <a name="prerequisites"></a>先決條件

若要使用 KME 註冊至 Intune，您必須先遵循下列步驟，在 Samsung Knox 入口網站上註冊您的公司：
1. [確認可在您的國家/地區取得 KME](https://www.samsungknox.com/en/solutions/it-solutions/knox-configure/available-countries) \(英文\)：在超過 55 個國家/地區都能取得 KME。 請確定您的部署國家/地區受到支援。

2. [支援的裝置](https://www.samsungknox.com/en/knox-platform/supported-devices/2.4+) \(英文\)：KME 適用於所有 Samsung 裝置，其中 Android 註冊最低要求為 Knox 2.4，Android Enterprise 註冊最低要求為 Knox 2.8。

3. [網路需求](https://docs.samsungknox.com/KME-Getting-Started/Content/firewall_exceptions.htm) \(英文\)：確定您的網路上已允許必要的防火牆和網路存取規則。

4. [註冊 Samsung 帳戶](https://www2.samsungknox.com/en/user/register) \(英文\)：需要 Samsung 帳戶以註冊並啟用 KME，並於單一位置管理所有的 Knox 企業權利。

5. 註冊檢閱：在您的設定檔已完成並提交之後，Samsung 會審核您的申請並立即核准它，或將該申請置於待審核的狀態以進行後續追蹤。 在 Samsung 核准您的帳戶之後，您便可以繼續進行後續步驟。

## <a name="create-mdm-profile"></a>建立 MDM 設定檔

成功註冊您的公司之後，您便可以在 Knox 入口網站中使用下列資訊建立適用於 Microsoft Intune 的 MDM 設定檔。 您可以在 Knox 入口網站中為 Android 和 Android Enterprise 建立 MDM 設定檔。
- 若要建立 Android MDM 設定檔，請在 Knox 入口網站中選取 [Device Admin] \(裝置系統管理員\)  作為設定檔類型。 
- 若要建立 Android 企業 MDM 設定檔，請在 Knox 入口網站中選取 [Device Owner] \(裝置擁有者\)  作為設定檔類型。  

### <a name="for-android"></a>適用於 Android

| MDM 設定檔欄位| 必要？ | 值 | 
|-------------------|-----------|-------| 
|設定檔名稱       | 是       |輸入您選擇的設定檔名稱。 |
|說明        | 否        |輸入描述設定檔的文字。 |
|MDM Information (MDM 資訊)     | 是        |選擇 [Server URI not required for my MDM] \(我的 MDM 不需要伺服器 URI\)  。| 
|MDM Agent APK \(MDM 代理程式 APK\)      | 是       |https://aka.ms/intune_kme_deviceowner| 
|Custom JSON \(自訂 JSON\)        | 是*        |{"com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN":"輸入 Intune 註冊權杖字串"}。 瞭解如何為[專用裝置](android-kiosk-enroll.md)和[完全受控裝置](android-fully-managed-enroll.md)建立註冊權杖。 |
|Skip Setup wizard \(略過設定精靈\)  | 否        |針對使用者選擇此選項以略過標準裝置設定提示。|
|Allow End User to Cancel Enrollment \(允許使用者取消註冊\) | 否 | 選擇此選項以允許使用者取消 KME。|
| Privacy Policy, EULAs and Terms of Service (隱私權原則、EULA 和服務條款) | 否 | 將此留白。 |
| Support contact details (支援連絡人詳細資料) | 是 | 選擇 [Edit] \(編輯\) 以更新連絡人詳細資料 |
|Associate a Knox license with this profile \(將 Knox 授權與此設定檔相關聯\) | 否 | 將此選項保持未選取。 使用 KME 註冊 Intune 並不需要 Knox 授權。|

\* 在 Knox 入口網站中完成設定檔建立時，不需要此欄位。 不過，Intune 必須填入此欄位，才能讓設定檔在 Intune 中成功註冊裝置。

### <a name="for-android-enterprise"></a>針對 Android Enterprise

如需逐步指導方針，請參閱 [Samsung 的建立設定檔](https://docs.samsungknox.com/KME-Getting-Started/Content/create-profiles.htm) \(英文\) 的指示。

| MDM 設定檔欄位| 必要？ | 值 |
|-------------------|-----------|-------|
|設定檔名稱       | 是       |輸入您選擇的設定檔名稱。|
|說明        | 否        |輸入描述設定檔的文字。|
|Pick your MDM (挑選您的 MDM) | 是 | 選擇 [Microsoft Intune]。 |
|MDM Agent APK \(MDM 代理程式 APK\)      | 是       |https://aka.ms/intune_kme|
|MDM Server URI \(MDM 伺服器 URI\)     | 否        |將此留白。|
|Custom JSON Data (自訂 JSON 資料)        | 否        |將此留白。|
|Dual DAR (雙重 DAR) | 否 | 將此留白。|
|QR code for enrollment (用於註冊的 QR 代碼) | 否 | 您可以新增 QR 代碼以加速註冊。|
|System applications (系統應用程式) | 是 | 選擇 [Leave all system apps enabled] \(保留所有系統應用程式為啟用\)  選項以確保所有應用程式可啟用，並可供設定檔使用。 如果未選擇此選項，則裝置的應用程式系統匣僅會顯示一組有限的系統應用程式。 例如電子郵件應用程式等應用程式仍會保持隱藏。 |
|Privacy Policy, EULAs and Terms of Service (隱私權原則、EULA 和服務條款) | 否 | 將此留白。|
|公司名稱 | 是 | 此名稱會在裝置註冊期間顯示。 |

## <a name="add-devices"></a>新增裝置

若要將 MDM 設定檔指派至裝置，必須使用下列其中一個方法將支援的 Samsung Knox 裝置新增至 Knox 入口網站：
- **使用 Samsung 核准的轉銷商：** 如果您是從其中一個 Samsung 核准的轉銷商購買裝置，請使用此方法。 轉銷商可以在獲得核准時為您自動上傳裝置。 [請造訪 Samsung Knox 註冊使用者指南以了解如何新增轉銷商](https://docs.samsungknox.com/KME-Getting-Started/Content/Register_resellers.htm) \(英文\)。

- **使用 Knox 部署應用程式 (KDA)：** 如果您有現有裝置是需要使用 KME 來註冊的，請使用此方法。 透過此方法，您可以使用藍牙或 NFC 來將裝置新增至 Knox 入口網站。 [請造訪 Samsung Knox 註冊使用者指南以了解使用 KDA 的方法](https://docs.samsungknox.com/KME-Getting-Started/Content/add-device-info.htm) \(英文\)。

## <a name="assign-an-mdm-profile-to-devices"></a>將 MDM 設定檔指派給裝置
您必須先將 MDM 設定檔指派給 Knox 入口網站中的已新增裝置，才能註冊那些裝置。 [請造訪 Samsung Knox 註冊使用者指南以了解裝置設定](https://docs.samsungknox.com/KME-Getting-Started/Content/configure-devices.htm) \(英文\)。

## <a name="configure-how-end-users-sign-in"></a>設定使用者登入的方式

針對使用適用於 Android 之 KME 註冊至 Intune 的裝置，您可以透過下列方法設定使用者登入的方式：

- **沒有使用者名稱關聯：** 在 Knox 入口網站中的 [Device details]  \(裝置詳細資訊\) 底下，將所新增裝置的 [User ID]  \(使用者識別碼\) 和 [Password]  \(密碼\) 欄位保留空白。 此選項會要求使用者在註冊至 Intune 時，必須輸入使用者名稱與密碼。

- **有使用者名稱關聯：** 在 Knox 入口網站的 [Device details]  \(裝置詳細資料\) 底下，為已新增的裝置提供 [User ID]  \(使用者識別碼\) (例如已指派使用者的使用者名稱，或是[裝置註冊管理員](device-enrollment-manager-enroll.md)帳戶)。 此選項會在使用者註冊至 Intune 時預先填入使用者名稱，並要求使用者輸入密碼。

> [!NOTE]
>
>使用者關聯只適用於 Android 裝置管理員註冊。 在使用者關聯已定義的情況下，只有已關聯的使用者可以使用 KME 註冊裝置。 就算是對裝置進行原廠重設也是如此。 在 Knox 入口網站中沒有定義任何使用者關聯的情況下，任何具備有效 Intune 授權的使用者都可以使用 KME 來註冊裝置。
>針對 Android Enterprise 完全受控裝置，即使已定義使用者關聯，也不會將它傳遞至裝置或將裝置繫結至使用者。
>

## <a name="distribute-devices"></a>散發裝置

在建立及指派 MDM 設定檔，關聯使用者名稱，並在 Intune 中將裝置識別為公司所擁有的裝置之後，您便可以將裝置散發給使用者。

是否仍需要協助？ 請參閱完整的 [KME 使用者指南](https://docs.samsungknox.com/KME-Getting-Started/Content/get-started.htm) \(英文\)。

## <a name="frequently-asked-questions"></a>常見問題集

- 裝置擁有者支援：   - 裝置擁有者支援  Intune 支援使用 KME 入口網站註冊專用且完全受控的裝置。 其他 Android Enterprise 裝置擁有者模式將在 Intune 中可用時受支援。

- **不支援工作設定檔：** KME 是一種企業裝置註冊方法，在 Android 工作設定檔中註冊的裝置可確保工作和個人資料在個人裝置上是分開的。 因此，在 Intune 中不支援使用 KME 將裝置註冊至工作設定檔。

- **重設成出廠預設值以註冊 Android Enterprise：** 如果要重新安排已經設定的裝置，需要在向 Android Enterprise 註冊時，重設成出廠預設值。

- **使用 Google Play 帳戶更新：** Google Play 帳戶並非將裝置註冊至 Microsoft Intune 的必要項目。 但針對 Android 裝置管理員註冊，未來針對 Intune 公司入口網站應用程式的更新，可能會要求裝置具備 Google Play 帳戶。 註冊 Google 裝置擁有者時，不需要 Google Play 帳戶。

- **忽略「密碼」欄位：** 若 Knox 入口網站 [裝置詳細資料]  中的 [密碼]  欄位已填入，則在 Android 註冊期間，Intune 公司入口網站應用程式會將其忽略。 使用者必須在裝置上輸入密碼以完成裝置註冊。


## <a name="getting-support"></a>取得支援
深入了解[如何取得 Samsung KME 的支援](https://docs.samsungknox.com/KME-Getting-Started/Content/to-get-kme-support.htm) \(英文\)。


