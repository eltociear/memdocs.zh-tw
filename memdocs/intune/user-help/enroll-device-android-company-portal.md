---
title: 使用 Intune 公司入口網站註冊 Android 裝置 | Microsoft Docs
description: 描述如何使用 Intune 公司入口網站註冊 Android 裝置
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
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 0f6efa6d026879a3231c21662e799bf8ba7ada09
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79337742"
---
# <a name="enroll-your-device-with-company-portal"></a>使用公司入口網站來註冊您的裝置  
註冊您個人或公司擁有的 Android 裝置，以安全地存取公司電子郵件、應用程式和資料。 公司入口網站支援執行 Android 4.4 及更新版本的 Android 裝置 (包括 Samsung Knox)。  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung Knox 是某種類型的安全性，可供特定 Samsung 裝置使用，以提供原生 Android 所提供項目之外的額外保護。 若要查看裝置是否為 Samsung Knox 裝置，請移至 [設定]   > [關於裝置]  。 若該處未列出 **Knox 版本**，表示您的裝置是原生 Android 裝置。

## <a name="enroll-device"></a>註冊裝置  
請務必[從 Google Play 安裝免費 Intune 公司入口網站應用程式](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)。 

在註冊期間，系統可能會要求您選擇最能描述您裝置使用方式的類別。 公司支援人員會使用您的答案來檢查您可以存取的應用程式。  

1. 開啟公司入口網站應用程式並使用您的公司或學校帳戶登入。  

2. 若您收到提示，要求您接受組織的條款及條件，請點選 [全部接受]  。  

   ![公司入口網站 [條款] 畫面的範例影像，其中醒目提示 [全部接受] 按鈕。](./media/accept-terms-1911.png)  


3. 檢閱您的組織可以看到與無法看到的內容。 然後點選 [繼續]  。


    ![公司入口網站 [我們重視您的隱私權] 畫面的的範例影像，其中 [繼續] 按鈕已反白顯示。](./media/android-privacy-screen-1911.png)  
4. 檢閱後續步驟的預期內容。 然後點選 [下一步]  。  

    ![公司入口網站 [下一步是什麼] 畫面的範例影像，其中醒目提示 [下一步] 按鈕。](./media/android-whats-next-1911.png)  


5. 視 Android 版本而定，系統可能會提示您允許存取裝置的特定部分。 這些提示是由 Google 所要求，且不是由 Microsoft 所控制。  

    針對下列權限，點選 [允許]  ：  
    * **允許公司入口網站進行和管理通話**：此權限可讓裝置與組織的裝置管理提供者 Intune 共用其國際行動設備識別碼 (IMEI)。 允許此權限並不會造成問題。 Microsoft 永遠不會進行或管理通話。  
    * **允許公司入口網站存取連絡人**：此權限可讓公司入口網站應用程式建立、使用和管理公司帳戶。  允許此權限並不會造成問題。 Microsoft 永遠不會存取連絡人。 

    如果您拒絕權限，則下次登入公司入口網站時，系統會再次提示您。 若要關閉這些訊息，請選取 [不再詢問]  。 若要管理應用程式權限，請移至 [設定] 應用程式 > [應用程式]   > [公司入口網站]   > [權限]   > [電話]  。  

6. 啟用裝置系統管理員應用程式。 

    公司入口網站需要裝置系統管理員權限，才能安全地管理裝置。 啟用應用程式可供組織找出可能的安全性問題 (例如嘗試解除鎖定裝置重複失敗)，並適當地回應。  

    ![啟用裝置系統管理員畫面的範例影像，其中醒目提示啟用按鈕。](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft 不會控制此畫面上的訊息。 我們了解其措辭可能顯得有點極端。 公司入口網站無法指定哪些限制和存取與組織相關。 如果對組織如何使用應用程式有任何問題，請連絡 IT 支援人員。 前往[公司入口網站網站](https://go.microsoft.com/fwlink/?linkid=2010980)來尋找您組織的連絡資訊。  


7. 裝置會開始註冊。 如果您使用 Samsung Knox 裝置，則系統會提示先檢閱並確認 ELM Agent 隱私權原則。   

    ![註冊期間出現的 Samsung Knox 隱私權原則畫面範例影像。](./media/and-enroll-7-knox-privacy-policy.png)  

8. 在 [公司存取設定]  畫面上，確認裝置已註冊。 然後點選 [繼續]  。  

    ![公司入口網站 [公司存取設定] 畫面的範例影像，其中顯示 [讓裝置成為受控] 已完成。](./media/update-settings-1911.png)  

9. 貴組織可能會要求您更新裝置設定。 點選 [解決]  以調整設定。 當您完成更新設定時，請點選 [繼續]  。  

   ![公司入口網站 [更新裝置設定] 的範例影像，其中醒目提示 [解決] 和 [繼續] 按鈕。](./media/resolve-settings-1911.png)  

10. 當安裝程式完成時，請按一下 [完成]  。    

    ![公司入口網站 [公司存取設定] 畫面的範例影像，其中顯示已完成的設定且 [完成] 按鈕已反白顯示。](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>後續步驟  

嘗試安裝學校或公司應用程式之前，請移至 [設定]   > [安全性]  ，然後開啟 [未知來源]  。 如果您不開啟此選項，您在嘗試安裝應用程式時將會看到下列訊息：「已封鎖安裝。 基於安全性理由，您的裝置設定成封鎖安裝從未知來源取得的應用程式。」 您可以點選訊息上的 [設定]  ，直接移至 [未知來源]  。  

> [!Note]
> 如果您的組織使用電信費用管理軟體，您需要完成幾個額外步驟，裝置才會完全註冊。 如需詳細資訊，請參閱[這裡](enroll-your-device-with-telecom-expense-management-android.md)。

如果在 Intune 中嘗試註冊裝置時出現錯誤，您可以[寄送電子郵件給您的公司支援人員](send-logs-to-your-it-admin-by-email-android.md)。  

是否仍需要協助？ 請連絡您公司的支援人員。 如需連絡資訊，請查看[公司入口網站](https://go.microsoft.com/fwlink/?linkid=2010980)。  