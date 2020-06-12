---
title: 整合 Check Point SandBlast Mobile 與 Intune
titleSuffix: Microsoft Intune
description: 如何使用 Intune 設定 Check Point SandBlast Mobile Threat Defense (MTD) 解決方案，來控制行動裝置對公司資源的存取。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 313e4b71d25d19437750f2321513076580091442
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330877"
---
# <a name="integrate-check-point-sandblast-mobile-with-intune"></a>整合 Check Point SandBlast Mobile 與 Intune

完成下列步驟以將 Check Point SandBlast Mobile Threat Defense 解決方案與 Intune 整合。

> [!NOTE]
> 此 Mobile Threat Defense 廠商不支援尚未註冊的裝置。

## <a name="before-you-begin"></a>開始之前

此文章中的指示會在 [Check Point SandBlast Mobile 主控台](https://intune-4.eu1.locsec.net/) \(英文\) 中完成。 

開始整合 Check Point SandBlast Mobile 與 Intune 之前，請確定您有下列項目：

- Microsoft Intune 訂閱

- 可授與下列權限的 Azure Active Directory 管理員認證：

  - 登入及讀取使用者設定檔

  - 以登入的使用者身分存取目錄

  - 讀取目錄資料

  - 將裝置資訊傳送至 Intune

- 可存取 Check Point SandBlast Mobile MTD 主控台的管理員認證。

### <a name="check-point-sandblast-app-authorization"></a>Check Point SandBlast 應用程式授權

Check Point SandBlast 應用程式授權程序是由下列項目所組成：

- 允許 Check Point SandBlast Mobile 將裝置健全狀況狀態的相關資訊傳送回 Intune。

- CheckPoint SandBlast Mobile 與「Azure AD 註冊群組」成員資格進行同步，以填入其裝置的資料庫。

- 允許 Check Point SandBlast 管理員主控台使用 Azure AD 單一登入 (SSO)。

- 允許 Check Point SandBlast 行動應用程式使用 Azure AD SSO 登入。

## <a name="to-set-up-check-point-sandblast-mobile-integration"></a>設定 Check Point SandBlast Mobile 整合

1. 移至 [Check Point SandBlast Mobile MTD 主控台](https://intune-4.eu1.locsec.net/)，以您的認證登入。

2. 按一下 [設定] 索引標籤。

3. 依序選擇 [裝置管理] 和 [設定]。

4. 從 [MDM Service] \(MDM 服務) 下拉式清單中選擇 [Microsoft Intune]。

5. 一旦將 Microsoft Intune 設為 MDM 服務，[Microsoft Intune 設定] 視窗就會出現。請針對下列每個裝置平台選擇 [新增至我的組織]：iOS/iPadOS、 Android 和 Windows，以授權 Check Point SandBlast Mobile 可與 Intune 和 Azure AD 進行通訊。

    ![顯示 Check Point MTD Intune 設定的影像](./media/checkpoint-sandblast-mobile-mtd-connector-integration/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > 您必須新增所有裝置平台，才能繼續下一個步驟。

6. 選擇 [接受] 授權 Check Point SandBlast Mobile 應用程式與 Intune 和 Azure Active Directory 進行通訊。

7. 一旦啟用了所有裝置平台，就需要進入 Azure AD 安全性群組。

8. 選擇 [驗證]，一旦成功驗證 Azure AD 安全性群組，即選擇 [儲存]。

## <a name="next-steps"></a>後續步驟

- [設定 Check Point SandBlast Mobile 應用程式](mtd-apps-ios-app-configuration-policy-add-assign.md)
