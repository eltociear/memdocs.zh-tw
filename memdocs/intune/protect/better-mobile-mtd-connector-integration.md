---
title: 設定 Better Mobile 與 Intune 的整合
titleSuffix: Intune on Azure
description: 與 Intune 的 Better Mobile 連接器整合
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6208c8f225cc3e54a61181960223f3f8cad8423d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989740"
---
# <a name="integrate-better-mobile-with-intune"></a>整合 Better Mobile 與 Intune

完成下列步驟以將 Better Mobile Threat Defense 解決方案與 Intune 整合。

## <a name="before-you-begin"></a>開始之前

在 [Better Mobile 管理員主控台](https://aad.bmobi.net)中完成下列步驟，會讓 Better Mobile 的服務連線到已註冊 Intune 的裝置 (使用裝置合規性)，以及尚未註冊的裝置 (使用應用程式防護原則)。

開始將 Better Mobile 與 Intune 整合之前，請確定您有下列項目：

- Microsoft Intune 訂閱

- 可授與下列權限的 Azure Active Directory 管理員認證：

  - 登入及讀取使用者設定檔

  - 以登入的使用者身分存取目錄

  - 讀取目錄資料

  - 將裝置資訊傳送至 Intune

- 可存取 Better Mobile 管理主控台的系統管理員認證。

### <a name="better-mobile-app-authorization"></a>Better Mobile 應用程式授權

Better Mobile 應用程式授權程序如下：

- 允許 Better Mobile 服務將裝置健康情況狀態的相關資訊傳送回 Intune。

- 將 Better Mobile 與 Azure AD 註冊群組成員資格同步，以填入其裝置的資料庫。

- 允許 Better Mobile 管理主控台使用 Azure AD 單一登入 (SSO)。

- 允許 Better Mobile 應用程式使用 Azure AD SSO 登入。

## <a name="to-set-up-better-mobile-integration"></a>設定 Better Mobile 整合

1. 移至 [Better Mobile 管理主控台](https://aad.bmobi.net)，並使用您的認證登入。
2. 選擇 [整合]   > [EMM/MDM]   > [新增帳戶]  。

     ![Better Mobile 管理主控台影像](./media/better-mobile-mtd-connector-integration/better_mobile_console.png)

3. 選擇 [Intune]  。
4. 在 [帳戶名稱]  旁，輸入描述。
5. 在 [Microsoft 登入]  視窗中，輸入您的 Intune 認證。
6. 在 [要求的權限]  視窗中，選擇 [接受]  。
7. 搜尋您想要讓 Better Mobile 從中同步裝置的 Azure AD 安全性群組，並在清單中選取它們。 接著，選取 [繼續]  。
8. 選取 [完成]  。
9. [新增帳戶]  頁面隨即出現。 關閉頁面。

## <a name="next-steps"></a>後續步驟

- [針對已註冊的裝置設定 Better Mobile 行動應用程式](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [針對尚未註冊的裝置設定 Better Mobile 行動應用程式](mtd-add-apps-unenrolled-devices.md)
