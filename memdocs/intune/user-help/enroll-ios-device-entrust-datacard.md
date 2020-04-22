---
title: 使用 Intune 公司入口網站和 Entrust Datacard 註冊 iOS 或 iPadOS 裝置
description: 註冊 iOS 或 iPadOS 裝置，以及使用 Entrust Datacard 設定衍生的認證驗證。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1e1f1c04bed91de3ac193ea3b6a07bde4e8658ba
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81638240"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>使用公司入口網站和 Entrust Datacard 設定 iOS 或 iPadOS 裝置

使用 Intune 公司入口網站應用程式註冊您的裝置，以安全地使用行動裝置存取您組織的電子郵件、檔案和應用程式。 您的裝置註冊之後，它就變成「受控」  。 您的組織可以透過 Intune 等行動裝置管理 (MDM) 提供者將原則和應用程式指派給裝置。  

在註冊期間，您也會在裝置上安裝衍生的認證。 組織可能會要求在存取資源或簽署和加密電子郵件時，使用衍生認證作為驗證方法。 

如果使用智慧卡來執行下列動作，則可能需要設定衍生認證：  

* 登入學校或公司應用程式、Wi-Fi 和虛擬私人網路 (VPN)
* 使用 S/MIME 憑證簽署和加密學校或公司電子郵件  

在本文中，您將：  

   * 使用 Intune 公司入口網站註冊 iOS 或 iPadOS 行動裝置。  
   * 從組織的衍生認證提供者 [Entrust Datacard](https://www.entrustdatacard.com/) 取得衍生認證。  

### <a name="what-are-derived-credentials"></a>什麼是衍生認證？  
衍生認證是衍生自智慧卡認證並安裝在裝置上的憑證。 它會授與公司資源的遠端存取權，同時防止未經授權的使用者存取機密資訊。  

衍生認證可用來： 
* 驗證登入學校或公司應用程式、Wi-Fi 和 VPN 的學生和員工
* 使用 S/MIME 憑證簽署和加密學校或公司電子郵件

衍生認證是適用於衍生個人識別驗證 (PIV) 認證的國家標準暨技術研究院 (NIST) 指導方針實作，是特殊發行集 (SP) 800-157 的一部分。  

## <a name="prerequisites"></a>必要條件

 若要完成註冊，則必須具備：

* 學校或公司提供的智慧卡
* 可使用智慧卡登入的電腦或 Kiosk 存取權
* 您的行動裝置
* iOS 和 iPadOS 版 Intune 公司入口網站應用程式，並已安裝在裝置上  


## <a name="enroll-device"></a>註冊裝置  
1. 在行動裝置上開啟 iOS/iPadOS 版公司入口網站應用程式，並使用公司帳戶登入。  

2. 記下螢幕上的代碼。  

    ![公司入口網站應用程式以及畫面上的訊息和驗證碼範例影像。](./media/copy-code-intercede.png)   

3. 切換至啟用智慧卡的裝置，然後前往 https://microsoft.com/devicelogin 。 
4. 輸入先前記下的驗證碼。  

    ![公司入口網站 [輸入代碼] 提示的範例螢幕擷取畫面。](./media/enter-code-intercede.png)   

5. 插入智慧卡以進行登入。   
6. 返回行動裝置上的公司入口網站應用程式，並遵循螢幕上的指示來註冊裝置。  
7. 註冊完成之後，公司入口網站會通知設定智慧卡。 點選通知。 如果沒有收到通知，請檢查電子郵件。   

    ![裝置主畫面上公司入口網站推播通知的範例螢幕擷取畫面。](./media/action-required-in-app-intercede.png)  

8. 在 [設定行動智慧卡存取]  畫面上：   
    a. 點選組織的設定指示連結。 如果組織未提供其他指示，則會將您送往這篇文章。  
    b. 點選 [開始]  。  

    ![公司入口網站 [設定行動智慧卡存取] 畫面的範例螢幕擷取畫面。](./media/smart-card-info-intercede.png)

9. 切換至啟用智慧卡的裝置，然後開啟 IdentityGuard。 
10. 尋找 [智慧認證登入] 區域，然後選取 [登入] 按鈕。  
11. 當收到提示要求選取憑證時，請挑選智慧卡認證。 然後選取 [確定]  。 
12. 輸入智慧卡 PIN。  
13. 系統會要求從動作清單中選擇。 選取可讓您註冊衍生行動智慧認證的項目。 連結或按鈕可能會顯示**我想要註冊衍生行動智慧卡認證**。  
14. 選取已成功下載及安裝的啟用智慧認證應用程式。 然後繼續前往下個畫面。   
15. 輸入衍生智慧卡認證的相關資訊。  
    a. 針對 [身分識別名稱]，輸入任何名稱，例如 *Entrust Derived Cred*。  
    b. 在下拉式功能表中，選取 [Entrust IdentityGudard 行動智慧認證]  。  
    c. 繼續前往下個畫面。 您將會看到一個 QR 代碼，其下方包含數字密碼。  

16. 返回行動裝置。 在 [公司入口網站] > [取得 QR 代碼]  畫面上，點選 [繼續]  。 

    ![公司入口網站 [取得 QR 代碼] 畫面的範例螢幕擷取畫面。](./media/get-qr-code-intercede.png)  
17. 點選 [使用相機]   > [確定]  。  

    ![公司入口網站提示的範例螢幕擷取畫面，其中要求權限以允許存取相機。](./media/allow-cp-camera-access-intercede.png)  
18. 掃描支援智慧卡裝置上的 QR 代碼影像。  
19. 輸入出現在 QR 代碼底下的數字密碼。  

    ![公司入口網站 [需要密碼] 畫面的範例螢幕擷取畫面，輸入密碼欄位。](./media/enter-password-derived-credentials.png)   

20. 等候公司入口網站完成裝置設定。  


## <a name="next-steps"></a>後續步驟  
註冊完成之後，您將能夠存取公司資源，例如電子郵件、Wi-Fi，以及組織提供的任何應用程式。 如需如何在公司入口網站中取得、搜尋、安裝和解除安裝應用程式的詳細資訊，請參閱：

* [從公司入口網站網站管理應用程式](manage-apps-cpweb.md)  
* [在裝置上使用受管理的應用程式](use-managed-apps-on-your-device-ios.md)  

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
