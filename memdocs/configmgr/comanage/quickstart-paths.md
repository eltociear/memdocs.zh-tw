---
title: 共同管理的路徑
titleSuffix: Configuration Manager
description: 了解您用來設定共同管理的兩個主要方法的先決條件。
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d481976a6c86da67670871690ba16985a67c80d8
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746454"
---
# <a name="paths-to-co-management"></a>共同管理的路徑

您用來設定共同管理的主要方法有兩個。 請務必了解每個路徑的先決條件。 每個路徑都需要 Azure Active Directory (Azure AD)、Configuration Manager、Microsoft Intune 與 Windows 10 的一些組合。 

1. [將現有受 Configuration Manager 管理的裝置自動註冊到 Intune 中](#bkmk_path1)  
2. [使用現代化佈建來啟動 Configuration Manager 用戶端](#bkmk_path2)  

![共同管理路徑的圖表](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a> 路徑 1：自動註冊現有用戶端

採用此路徑可快速將您現有受 Configuration Manager 管理的裝置自動註冊到 Intune 中。 從 Configuration Manager 管理這些裝置，就和啟用共同管理之前一樣。 現在，您已獲得所有雲端式的優點。 此路徑對於您的使用者是公開透明的。

以下是進行設定所需的項目：
- 混合式 Azure AD
    - 下列其中一個 [Azure AD 混合式身分識別選項](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin)：  
       - [密碼雜湊同步處理](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization)與[無縫單一登入 (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [傳遞驗證](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta)與[無縫單一登入 (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [同盟的 SSO (搭配 Active Directory Federation Services (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium 授權
    - 設定混合式 Azure AD Join (選擇一個選項)：
        - 適用於受控網域
        - 適用於同盟網域
- 混合式 Azure AD Join 的用戶端代理程式設定
- 設定針對 Intune 自動註冊裝置
- 在 Configuration Manager 中啟用共同管理

如需此路徑的教學課程，請參閱[教學課程：針對現有 Configuration Manager 用戶端啟用共同管理](tutorial-co-manage-clients.md)。



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> 路徑 2：使用現代化佈建來啟動

以下是進行設定所需的項目：

1. [設定增強 HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [在 Azure 中建立雲端服務](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [設定管理點和用戶端以使用雲端管理閘道](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [使用 Intune 來部署 Configuration Manager 用戶端](how-to-prepare-Win10.md)  

如需此路徑的教學課程，請參閱[教學課程：為新的網際網路型裝置啟用共同管理](tutorial-co-manage-new-devices.md)。

