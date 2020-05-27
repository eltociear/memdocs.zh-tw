---
title: 使用 Intune 公司入口網站和 DISA Purebred 註冊 iOS 或 iPadOS 裝置
description: 了解如何註冊 iOS 或 iPadOS 裝置，並設定 DISA Purebred 的衍生認證驗證。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
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
ms.openlocfilehash: 50330bbdc61eeeada022c44f4d1f2f68b31f19a4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881545"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>使用公司入口網站和 DISA Purebred 設定 iOS 或 iPadOS 裝置  

使用 Intune 公司入口網站應用程式註冊您的裝置，以安全地使用行動裝置存取您組織的電子郵件、檔案和應用程式。 您的裝置註冊之後，它就變成「受控」  。 您的組織可以透過 Intune 等行動裝置管理 (MDM) 提供者將原則和應用程式指派給裝置。  

在註冊期間，您也會在裝置上安裝衍生的認證。 組織可能會要求在存取資源或簽署和加密電子郵件時，使用衍生認證作為驗證方法。 

如果使用智慧卡來執行下列動作，則可能需要設定衍生認證：

* 登入學校或公司應用程式、Wi-Fi 和虛擬私人網路 (VPN)
* 使用 S/MIME 憑證簽署和加密學校或公司電子郵件  

在本文中，您將：  

   * 使用 Intune 公司入口網站註冊 iOS 或 iPadOS 行動裝置。  
   * 從組織的衍生認證提供者 DISA Purebred (https:\//cyber.mil/pki-pke/purebred/) 取得衍生認證。  

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
* 您的行動裝置
* iOS 和 iPadOS 版 Intune 公司入口網站應用程式，並已安裝在裝置上   

您也必須在設定期間連絡 Purebred 專員或代表。      

## <a name="enroll-device"></a>註冊裝置  
1. 在行動裝置上開啟 iOS/iPadOS 版公司入口網站應用程式，並使用公司帳戶登入。  

2. 記下螢幕上的代碼。  

    ![公司入口網站應用程式以及螢幕上訊息和代碼的範例影像。](./media/copy-code-intercede.png)  
3. 切換至啟用智慧卡的裝置，然後前往 https://microsoft.com/devicelogin 。 
4. 輸入先前記下的代碼。  

    ![公司入口網站 [輸入代碼] 提示的範例螢幕擷取畫面。](./media/enter-code-intercede.png)   

5. 插入智慧卡以進行登入。  
6. 返回行動裝置上的公司入口網站應用程式，並遵循螢幕上的指示來註冊裝置。  
7. 註冊完成之後，公司入口網站會通知設定智慧卡。 點選通知。 如果沒有收到通知，請檢查電子郵件。   

    ![裝置主畫面上公司入口網站推播通知的範例螢幕擷取畫面。](./media/action-required-in-app-intercede.png)  
8. 在 [設定行動智慧卡存取]  畫面上：  
    a. 點選組織的設定指示連結。 如果組織未提供其他指示，則會將您送往這篇文章。  
    b. 按一下 [開啟]  以開啟 Purebred 應用程式。  

    ![公司入口網站 [設定行動智慧卡存取] 畫面的範例螢幕擷取畫面。](./media/smart-card-open-disa-purebred.png)  
9. 當系統提示您允許公司入口網站開啟 Purebred Registration 應用程式時，請選取 [開啟]  。   

    ![公司入口網站提示的範例螢幕擷取畫面，其中提示開啟 DISA Purebred 應用程式。](./media/open-app-prompt-disa-purbred.png)  
10. 當應用程式運作時，請與組織的 Purebred 專員合作，以設定及下載 Purebred 註冊前組態設定檔。   
11. 移至 [設定] 應用程式 > [一般]   > [設定檔與裝置管理]   > [安裝設定檔]  ，然後點選 [安裝]  。  
12. 輸入您的裝置密碼。  
13. 安裝設定檔。 可能必須點選 [安裝]  多次，才能開始進行安裝。 
14. 返回 Purebred Registration 應用程式。 遵循 Purebred 專員的指示繼續進行。  
 
15. 下載組態設定檔之後，請移至 [設定] 應用程式 > [一般]   > [設定檔與裝置管理]   > [安裝設定檔]  ，然後點選 [安裝]  。   
16.  輸入您的裝置密碼。
17. 安裝設定檔。 可能必須點選 [安裝]  多次，才能開始進行安裝。 
18. 安裝完成之後，請返回公司入口網站應用程式。  
19.  在 [設定行動智慧卡存取]  畫面上，點選 [繼續]  。  

20. 從 [匯入憑證]  畫面，您將會擷取並匯入從 DISA Purebred 取得的衍生認證。  

    a. 點選 [繼續]  。   

    ![公司入口網站設定 [匯入憑證] 畫面的範例螢幕擷取畫面。](./media/import-certificate-disa-purebred.png)  
    b. 移至 iCloud 磁碟機 [瀏覽]   > [位置]  ，然後點選 [其他位置]  。  

    ![iCloud 磁碟機 [瀏覽] 功能表的範例螢幕擷取畫面，其中醒目提示 [其他位置] 選項。](./media/icloud-drive-more-locations.png)  
    c. 點選開關以啟用 [Purebred Key Chain]  。  

    ![iCloud 磁碟機 [瀏覽] 檢視的範例螢幕擷取畫面，其中醒目提示已啟用 [Purebred Key Chain] 開關。](./media/icloud-drive-enable-purebred-keychain.png)   

    d. 點選 [Purebred Credential Package] \(Purebred 認證套件\)  。  

    ![iOS 畫面的範例螢幕擷取畫面，其中包含可供選取的 [Purebred Credential Package] \(Purebred 認證套件\) 選項。](./media/purebred-credential-package.png)  
    f. 憑證清單隨即出現。 選取其中一個，然後點選 [匯入金鑰]  。  

    ![可供選取的憑證清單範例螢幕擷取畫面，其中已選取一個。](./media/import-purebred-keychain.png) 
21. 返回公司入口網站應用程式，並等候公司入口網站完成裝置設定。   

## <a name="next-steps"></a>後續步驟  
註冊完成之後，您將能夠存取公司資源，例如電子郵件、Wi-Fi，以及組織提供的任何應用程式。 如需如何在公司入口網站中取得、搜尋、安裝和解除安裝應用程式的詳細資訊，請參閱：

* [從公司入口網站網站管理應用程式](manage-apps-cpweb.md)  
* [在裝置上使用受管理的應用程式](use-managed-apps-on-your-device-ios.md)  

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。
