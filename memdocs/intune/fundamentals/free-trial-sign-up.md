---
title: 快速入門 - 免費試用 Microsoft Intune
titleSuffix: ''
description: 在此快速入門中，您將建立免費試用訂用帳戶、了解支援的設定和網路需求，並選擇性地設定您的網域名稱。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/16/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 893981700ede9587a980faa0e4d6b0384c24e3d4
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80401493"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>快速入門：免費試用 Microsoft Intune

Microsoft Intune 透過管理裝置和應用程式來協助您保護員工的公司資料。 在此快速入門中，您將建立免費訂用帳戶，以在測試環境中試用 Intune。

Intune 從透過 Microsoft 端點管理員系統管理中心管理的安全雲端式服務，提供行動裝置管理 (MDM) 與行動應用程式管理 (MAM)。 使用 Intune，您可以確保正確設定、存取及更新員工的公司資源 (資料、裝置和應用程式)，以符合您公司的合規性原則和需求。

## <a name="prerequisites"></a>必要條件
設定 Microsoft Intune 之前，請先檢閱下列需求：

- [支援的作業系統與瀏覽器](supported-devices-browsers.md)
- [網路設定需求與頻寬](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>註冊 Microsoft Intune 免費試用

免費試用 Intune 30 天。 如果您已經有工作或學校帳戶，請**登入**該帳戶，並將 Intune 新增您的訂閱。 否則，您可以**註冊**新帳戶供您的組織使用 Intune。

> [!IMPORTANT]
> 註冊新帳戶後，無法合併現有的工作或學校帳戶。

1. 前往 [Microsoft Intune 試用](https://go.microsoft.com/fwlink/?linkid=2019088)頁面並填寫表單。

    ![Microsoft Intune 試用帳戶註冊網頁的螢幕擷取畫面](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    若您大部分的 IT 作業與使用者分屬於不同的地區設定，建議您在 [國家或地區]  下選取該地區設定。 Azure 會使用您的區域資訊來提供適當的服務。 此設定將無法變更。

2. 使用您的公司名稱後面接著 **.onmicrosoft.com** 來建立帳戶。 

    ![Intune 試用版帳戶新增認證程序的螢幕擷取畫面](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    如果您的組織本身有您想要使用，但不含 **.onmicrosoft.com** 的自訂網域，您可以在 Microsoft 365 系統管理中心進行變更，如本文稍後所述。

3. 在註冊程序結束時，檢視您的新帳戶資訊。

    ![帳戶資訊的影像](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>在 Microsoft 端點管理員中登入 Intune

如果您還沒有登入入口網站，請完成下列步驟：

1. 開啟新的瀏覽器視窗，然後在網址列中輸入 **https://endpoint.microsoft.com** 。 
2. 使用在上述步驟中取得的使用者識別碼來登入 ( *yourID@yourdomain* .onmicrosoft.com)。

    ![入口網站登入頁面的影像](./media/free-trial-sign-up/azure-portal-signin.png)

當您註冊試用版時，您也會收到電子郵件訊息，其中包含您在註冊程序期間提供的帳戶資訊和電子郵件地址。 本電子郵件可確認您的試用版是使用中的狀態。

> [!TIP]
> 使用 Microsoft 端點管理員時，在一般模式下使用瀏覽器可能會獲得更好的結果，而不是私密模式。

## <a name="confirm-the-mdm-authority-in-intune"></a>在 Intune 中確認 MDM 授權單位

根據預設，當您建立免費試用時，會設定 MDM 授權單位。 您可以透過使用下列步驟來確認是否已設定 MDM 授權單位：

1. 如果您尚未登入，請登入 Microsoft 端點管理員。
2. 按一下 [租用戶系統管理]  。
3. 檢視租用戶詳細資料。 **MDM 授權單位**應該已設定為 **Microsoft Intune**。

如果登入 Microsoft 端點管理員之後，您看到橙色橫幅指出您尚未設定 MDM 授權單位，您可以在此時啟動它。 行動裝置管理 (MDM) 授權單位設定會決定您管理裝置的方式。 在使用者可以註冊裝置以進行管理之前，必須先設定 MDM 授權單位。

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>若要將 MDM 授權單位設定為 Intune，請執行下列步驟：

1. 開啟新的瀏覽器視窗，然後在網址列中輸入 **https://portal.azure.com** 。 
2. 選擇 [所有服務]   > [Microsoft Intune]  。
3. 選取指出您尚未啟用裝置管理的橫幅，或如果您沒有立即看到橫幅，請選取 [裝置註冊]  。 如果您尚未啟用裝置管理，會顯示 [選擇 MDM 授權單位]  刀鋒視窗。

    > [!NOTE]
    > 如果您已設定 MDM 授權單位，您會在 [裝置註冊]  刀鋒視窗中看到 MDM 授權值。 只有在您尚未設定 MDM 授權單位時，才會顯示橙色橫幅。 

    ![選擇 MDM 授權單位刀鋒視窗的影像](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. 如果未設定 MDM 授權單位，請在 [選擇 MDM 授權單位]  下，將您的 MDM 授權單位設定為 [Intune MDM 授權單位]  。

如需 MDM 授權單位的詳細資訊，請參閱[設定行動裝置管理授權單位](mdm-authority-set.md)。

## <a name="configure-your-custom-domain-name-optional"></a>設定您的自訂網域名稱 (選擇性)

如上所述，如果您的組織本身有您想要使用，但不含 **.onmicrosoft.com** 的自訂網域，您可以在 Microsoft 365 系統管理中心進行變更。 您可以透過下列步驟，新增、驗證及設定您的自訂網域名稱。  

> [!IMPORTANT]
> 您無法重新命名或移除網域名稱中「初始的」  **onmicrosoft.com** 部分。 但是，您可以新增、驗證或移除 Intune 使用的「自訂」  網域名稱，以利企業識別。 如需詳細資訊，請參閱[設定自訂網域名稱](custom-domain-name-configure.md)。

1. 前往 [Microsoft 365 系統管理中心](https://admin.microsoft.com)並使用您的系統管理員帳戶登入。

2. 在瀏覽窗格中，選擇 [設定]   > [網域]   > [新增網域]  。

3. 鍵入您的自訂網域名稱。 然後，選取 [下一步]  。

   ![Microsoft 365 系統管理中心 - [新增網域] 的螢幕擷取畫面](./media/free-trial-sign-up/domain-custom-add.png)

4. 確認您是上一個步驟所輸入網域的擁有者。 
    
    選取 [透過電子郵件傳送驗證碼]  會傳送電子郵件給您網域中已註冊的連絡人。 收到電子郵件之後，請複製驗證碼，並在標示為 [在這裡輸入您的驗證碼]  的欄位中輸入。 如果驗證碼符合，則會將網域新增至您的租用戶。 顯示的電子郵件看起來可能很陌生。 有些註冊機構會隱藏實際電子郵件地址。 同時，電子郵件地址可能不同於註冊網域時所提供的電子郵件地址。

   ![Microsoft 365 系統管理中心 - [驗證網域] 的螢幕擷取畫面](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > 如需 TXT 記錄驗證詳細資料，請參閱[在任一 DNS 主機服務提供者建立 Office 365 的 DNS 記錄](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166)。

## <a name="admin-experiences"></a>管理體驗

您會最常使用的入口網站有兩個：
- Microsoft 端點管理員系統管理中心 ([https://endpoint.microsoft.com/](https://endpoint.microsoft.com/)) 可讓您探索 [Intune 的功能](what-is-intune.md)。 這是系統管理員使用 Intune 的地方。
- Microsoft 365 系統管理中心 ([https://admin.microsoft.com](https://admin.microsoft.com)) 是您可以新增及管理使用者的位置，前提是您未使用 Azure Active Directory 進行此工作。 您也可以管理您帳戶的其他事宜，包括計費及支援。

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已建立免費訂用帳戶，以在測試環境中試用 Intune。 如需設定 Intune 的詳細資訊，請參閱[設定 Intune](setup-steps.md)。

若要遵循此 Intune 快速入門系列，請繼續前往下一個快速入門。

> [!div class="nextstepaction"]
> [快速入門：建立使用者並為其指派授權](quickstart-create-user.md)
