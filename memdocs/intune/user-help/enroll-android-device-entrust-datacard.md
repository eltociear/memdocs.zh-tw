---
title: 使用 Microsoft Intune 應用程式和 Entrust Datacard 來註冊 Android 裝置
description: 註冊 Android 裝置，以及使用 Entrust Datacard 設定衍生的認證驗證。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: f59d3c0d06e9b12acab3292ba0c977b181e7c07e
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531786"
---
# <a name="set-up-android-device-with-company-portal-and-entrust-datacard"></a>使用公司入口網站和 Entrust Datacard 設定 Android 裝置

使用 Microsoft Intune 應用程式註冊您的裝置，以安全地使用行動裝置存取您組織的電子郵件、檔案和應用程式。 您的裝置註冊之後，它就變成「受控」。 您的組織可以透過 Intune 等行動裝置管理 (MDM) 提供者將原則和應用程式指派給裝置。

在註冊期間，您也會在裝置上安裝衍生的認證。 組織可能會要求在存取資源或簽署和加密電子郵件時，使用衍生認證作為驗證方法。

如果使用智慧卡來執行下列動作，則可能需要設定衍生認證：

* 登入學校或公司應用程式、Wi-Fi 和虛擬私人網路 (VPN)
* 使用 S/MIME 憑證簽署和加密學校或公司電子郵件

在本文中，您將：

* 使用 Intune 應用程式來註冊行動 Android 裝置
* 藉由安裝組織的衍生認證提供者 [Entrust Datacard](https://www.entrustdatacard.com/) 所衍生的認證，來設定您的智慧卡

## <a name="what-are-derived-credentials"></a>什麼是衍生認證？

衍生認證是從您的智慧卡認證衍生而來，並安裝在您裝置上的憑證。 它會授與公司資源的遠端存取權，同時防止未經授權的使用者存取機密資訊。

衍生認證可用來：

* 驗證登入學校或公司應用程式、Wi-Fi 和 VPN 的學生和員工
* 使用 S/MIME 憑證簽署和加密學校或公司電子郵件

衍生認證是適用於衍生個人識別驗證 (PIV) 認證的國家標準暨技術研究院 (NIST) 指導方針實作，是特殊發行集 (SP) 800-157 的一部分。

## <a name="prerequisites"></a>先決條件

 若要完成註冊，則必須具備：

* 學校或公司提供的智慧卡
* 可使用智慧卡登入的電腦或 Kiosk 存取權
* 可執行 Android 7.0 或更新版本之全新或重設成原廠設定的裝置
* 安裝有 Microsoft Intune 應用程式的裝置

## <a name="enroll-device"></a>註冊裝置  

1. 開啟新裝置或恢復出廠預設值之裝置的電源。  
2. 在 [歡迎使用] 畫面上選取您的語言。 若您收到指示，要求您使用 QR 代碼或 NFC 註冊，請遵循以下符合該方法的步驟。  
     * NFC：針對程式設計師裝置輕觸您支援 NFC 的裝置，來連線到您組織的網路。 遵循畫面上的提示。 當您到達 Chrome 的服務條款畫面時，請繼續前往步驟 5。  

     * QR 代碼：完成 [QR 代碼註冊](#qr-code-enrollment)中的步驟。  

     若您收到指示，要求您使用另一種方法，請繼續前往步驟 3。    

3. 連線到 Wi-Fi 並點選 [下一步]。 遵循符合您註冊方法的步驟。 

    * 權杖：當您到達 Google 登入畫面時，請完成[權杖註冊](#token-enrollment)中的步驟。  
    * Google Zero Touch：在您連線到 Wi-Fi 後，您的組織將能辨識您的裝置。 繼續前往步驟 4 並遵循畫面上的提示，直到安裝完成。    
 
       ![Google 條款畫面的範例影像 (若您使用 Google Zero Touch 的話)，其中已醒目提示 [接受並繼續] 按鈕。](./media/google-zero-touch-intune-app-01.png)   
   
4. 檢閱 Google 的條款。 然後點選 [接受並繼續]。  

      ![Google 條款畫面的範例影像，其中已醒目提示 [接受並繼續] 按鈕。](./media/fully-managed-intune-app-04.png)   

5. 檢閱 Chrome 的服務條款。 然後點選 [接受並繼續]。  

   ![Google 服務條款畫面的範例影像，其中已醒目提示 [接受並繼續] 按鈕。](./media/fully-managed-intune-app-06.png)   

6. 在登入畫面中，依序點選 [登入選項] 及 [從另一部裝置登入]。 

7. 記下螢幕上的代碼。  

8. 切換至可以使用您智慧卡的裝置，然後前往您畫面上顯示的網址。 

9. 輸入先前記下的代碼。

   > [!div class="mx-imgBorder"]
   > ![公司入口網站之 [輸入代碼] 提示的螢幕擷取畫面。](./media/enter-code-intercede.png)

10. 插入智慧卡以進行登入。  

11. 在登入畫面中，選取您的公司或學校帳戶。 切換回您的行動裝置。 

12. 取決於您組織的需求，您可能會收到提示，要求您更新設定 (例如畫面鎖定或加密)。 若您看到這些提示，請點選 [設定] 並遵循畫面上的說明。  

       ![設定您公司電話畫面的範例影像，其中已醒目提示 [設定] 按鈕。](./media/fully-managed-intune-app-10.png)   

13. 若要在您的裝置上安裝公司應用程式，請點選 [安裝]。 安裝完成後，請點選 [下一步]。  

       ![設定您公司電話畫面的範例影像，其中已醒目提示 [安裝] 按鈕。](./media/fully-managed-intune-app-11.png)    

14. 點選 [開始]，以開啟 Microsoft Intune 應用程式。 

    ![設定您公司電話畫面的範例影像，其中已醒目提示 [啟動] 按鈕。](./media/fully-managed-intune-app-17.png)   
 
15. 返回您行動裝置上的 Intune 應用程式，然後遵循螢幕上的指示，直到完成註冊為止。 

    ![設定存取 [註冊裝置] 畫面的範例影像，其中醒目提示 [完成] 按鈕。](./media/fully-managed-intune-app-19.png)   

16. 繼續閱讀本文中的[設定您的智慧卡](enroll-android-device-entrust-datacard.md#set-up-smart-card)一節，以完成您裝置的設定。  

### <a name="qr-code-enrollment"></a>QR 代碼註冊  
在本節中，您將會掃描您公司提供的 QR 代碼。  當您完成時，我們會將您重新導向回裝置註冊步驟。     
  
1. 在 [歡迎] 畫面上，點選畫面五次來啟動 QR 代碼安裝。  

   ![裝置安裝 [歡迎] 畫面的範例影像，其中已醒目提示點選畫面的說明。](./media/qr-code-intune-app-01.png)  

2. 請遵循任何畫面上的說明，來連線到 Wi-Fi。  
3. 若您的裝置沒有 QR 代碼掃描器，則安裝畫面會顯示安裝掃描器的進度。 等待安裝完成。  
4. 出現提示時，請掃描組織給您的註冊設定檔 QR 代碼。  
5. 返回[註冊裝置](#enroll-device)的步驟 4 來繼續安裝。  

### <a name="token-enrollment"></a>權杖註冊  
在本節中，您將會輸入您公司提供的權杖。 當您完成時，我們會將您重新導向回裝置註冊步驟。  

1. 在 Google 登入畫面的 [電子郵件或電話] 方塊中，鍵入 **afw#setup**。 然後點選 [下一步]。 

   ![Google 登入畫面的範例影像，其中顯示已在欄位中鍵入 "afw#setup"。](./media/token-intune-app-01.png)   

2. 針對 [Android 裝置原則] 應用程式選擇 [安裝]。 繼續安裝。 取決於您的裝置，您可能需要檢閱及接受其他條款。    

3. 在 [註冊此裝置] 畫面上，選取 [下一步]。  

4. 選取 [輸入代碼]。  

5. 在 [掃描或輸入代碼] 畫面上，鍵入組織給您的代碼。  然後按一下 [下一步] 。  

   ![[掃描或輸入代碼] 畫面的範例影像，其中已醒目提示 [下一步] 按鈕。](./media/token-intune-app-04.png)  

6. 返回[註冊裝置](#enroll-device)的步驟 4 來繼續安裝。

## <a name="set-up-smart-card"></a>設定智慧卡  

1. 註冊完成之後，Intune 應用程式會通知您設定智慧卡。 點選通知。 如果沒有收到通知，請檢查電子郵件。

   > [!div class="mx-imgBorder"]
   > ![裝置主畫面之公司入口網站推播通知的範例螢幕擷取畫面。](./media/action-required-in-app-android.png)

2. 在**設定智慧卡**畫面上：

   1. 點選組織其設定指示的連結。 如果組織未提供其他指示，則會將您送往這篇文章。

   2. 點選 [開始]。 

   > [!div class="mx-imgBorder"]
   > ![公司入口網站之設定行動智慧卡存取畫面的範例螢幕擷取畫面。](./media/smart-card-open-entrust-android.png)

3. 切換至啟用智慧卡的裝置，然後開啟 IdentityGuard。

4. 尋找 [智慧認證登入] 區域，然後選取 [登入] 按鈕。

5. 當收到提示要求選取憑證時，請挑選智慧卡認證。 然後選取 [確定]。

6. 輸入智慧卡 PIN。

7. 系統會要求從動作清單中選擇。 選取可讓您註冊衍生行動智慧認證的項目。 連結或按鈕可能會顯示**我想要註冊衍生行動智慧卡認證**。

8. 選取已成功下載及安裝的啟用智慧認證應用程式。 然後繼續前往下個畫面。

9. 輸入衍生智慧卡認證的相關資訊：

    1. 針對 [身分識別名稱]，輸入任何名稱，例如 *Entrust Derived Cred*。  
    2. 在下拉式功能表中，選取 [Entrust IdentityGuard 行動智慧認證]。

    3. 繼續前往下個畫面。 您將會看到一個 QR 代碼，其下方包含數字密碼。

10. 返回您的 Android 裝置。 在 Intune 應用程式 > [取得 QR 代碼] 畫面上，點選 [下一步]。

    > [!div class="mx-imgBorder"]
    > ![公司入口網站之取得 QR 代碼畫面的範例螢幕擷取畫面。](./media/get-qr-code-entrust-android.png)

11. 如有提示允許 Intune 應用程式使用您的相機時，請點選 [允許]。

12. 掃描支援智慧卡裝置上的 QR 代碼影像。

13. 在 [需要密碼] 畫面上，輸入出現在 QR 代碼底下的密碼。

    > [!div class="mx-imgBorder"]
    > ![公司入口網站 [需要密碼] 畫面的範例螢幕擷取畫面。](./media/password-required-entrust-android.png)  

14. Intune 應用程式會開始下載，並安裝存取公司或學校資源所需的憑證。 此程序需要一些時間，視您的網際網路連線而定。 在這段期間內，請勿關閉應用程式。

    > [!div class="mx-imgBorder"]
    > ![公司入口網站之「下載及安裝憑證」畫面的範例螢幕擷取畫面](./media/install-certificates-entrust-android.png)

15. 處理完所有憑證之後，請等待 Intune 應用程式完成您的裝置設定。 當出現**設定完成** 畫面時，表示設定已完成。

    > [!div class="mx-imgBorder"]
    > ![設定完成的範例螢幕擷取畫面](./media/all-set-android.png)

## <a name="next-steps"></a>後續步驟

註冊完成之後，您將能夠存取公司資源，例如電子郵件、Wi-Fi，以及組織提供的任何應用程式。 如需如何在 Intune 應用程式中取得、搜尋、安裝及解除安裝應用程式的詳細資訊，請參閱：

* [在裝置上使用受管理的應用程式](use-managed-apps-on-your-device-android.md)  
* [從公司入口網站網站管理應用程式](manage-apps-cpweb.md)  

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。