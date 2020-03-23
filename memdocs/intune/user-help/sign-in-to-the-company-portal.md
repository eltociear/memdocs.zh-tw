---
title: 如何登入公司入口網站應用程式 | Microsoft 文件
description: 了解如何在多種平台上登入「公司入口網站」應用程式。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 4088185da2c01cfa7fd343203f7452d2796c4466
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79335818"
---
# <a name="sign-in-to-company-portal"></a>登入公司入口網站  

有三種方式可登入公司入口網站應用程式：

* 使用您的工作電子郵件地址與密碼登入。  
* 使用憑證式驗證登入。  
* 從另一部裝置登入。    


## <a name="sign-in-with-your-email-address-and-password"></a>使用您的電子郵件地址與密碼登入
下列步驟顯示 iOS 版公司入口網站的螢幕擷取畫面。  

1. 在裝置上開啟應用程式，然後點選 [登入]  。  

   ![公司入口網站登入頁面的範例螢幕擷取畫面。](./media/intune-ios-cp-signin-1908.png)


2. 輸入您的 [工作或學校帳戶]  ，然後點選 [下一步]  。

   ![系統會在畫面上單獨提示使用者輸入電子郵件地址，而不是同時提示輸入電子郵件與密碼。](./media/cp_ios_aad_signin_after_1804_002.png)

3. 輸入您的密碼，然後點選 [登入]  。

   ![接受使用者的電子郵件地址後，系統會提示使用者輸入密碼。](./media/cp_ios_aad_signin_after_1804_003.png)

4. 應用程式會確認認證。 完成時，您就可以存取組織資源並安裝可用的應用程式。  

   ![執行驗證程序之後，公司入口網站應用程式會登入，並顯示載入列。](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>使用憑證式驗證登入
只有在組織允許憑證式驗證，且您有可供使用的憑證時，才會看到此登入選項。  

1. 在您的裝置上開啟「公司入口網站」應用程式。  

2. 輸入 [工作或學校帳戶]  。  

3. 點選 [以憑證登入]  連結。  

4. 點選 [繼續]  以使用憑證。  

## <a name="sign-in-from-another-device"></a>從另一部裝置登入

如果公司使用智慧卡來存取電腦，則您可能需要從另一部裝置登入來進行驗證。  

1. 在您的裝置上開啟「公司入口網站」應用程式。 請確定這是您將用來存取公司資源的裝置。       

1. 選取 [從另一部裝置登入]  。  

   ![公司入口網站登入頁面會提示使用者輸入電子郵件地址。  顯示 [下一步] 按鈕與 [從另一部裝置登入] 連結。 此外，也包含 [無法存取您的帳戶?] 連結 底部的連結會指向 Microsoft 隱私權與 Cookie 資訊。](./media/cp_ios_aad_signin_after_1804_005.png)

2. 您會收到用來登入公司入口網站的唯一一次性驗證碼。 請複製驗證碼。

   ![系統會提供指示和一個唯一密碼，說明應從工作電腦移至 https://microsoft.com/devicelogin 頁面，然後使用該驗證碼來進行登入。](./media/cp_ios_aad_signin_after_1804_006.png)

3. 在其他裝置上 (您用來驗證的裝置)，開啟瀏覽器並前往 [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)。 輸入或貼上驗證碼。  

   ![使用者工作電腦上的瀏覽器 (而非公司入口網站應用程式) 的影像。 顯示的 [裝置登入] 頁面提示使用者輸入在公司入口網站應用程式中收到的驗證碼。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. 選取 [繼續]  以允許公司入口網站登入公司裝置。   

   ![使用者已將唯一驗證碼輸入至欄位，且 [裝置登入] 網站已要求確認 Intune 公司入口網站是接收驗證以登入的正確應用程式。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. 驗證碼一旦驗證後，您便可以關閉此視窗。  

   ![確認頁面指出使用者現已在其裝置上登入公司入口網站應用程式，並且可以關閉此頁面。](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. 公司入口網站應用程式將您登入公司裝置。  

   ![經過驗證程序之後，公司入口網站應用程式會登入，並以載入列指出其進度。](./media/cp_ios_aad_signin_after_1804_007.png)

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  
