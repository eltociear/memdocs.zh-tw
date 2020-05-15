---
title: 設定電腦分析
titleSuffix: Configuration Manager
description: 設定和連線到電腦分析的操作指南。
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: a90f3260782f08fdf8f7424a95e09b34e38e97d3
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268142"
---
# <a name="how-to-set-up-desktop-analytics"></a>如何設定電腦分析

使用此程序登入電腦分析，並在您的訂用帳戶中加以設定。 此程序是為您組織設定電腦分析的一次性程序。  

> [!Important]  
> 如需電腦分析與 Configuration Manager 的一般必要條件資訊，請參閱[必要條件](overview.md#prerequisites)。  

## <a name="initial-onboarding"></a>初始上線

1. 以具有**全域管理員**角色的使用者身分，在 Microsoft 365 裝置管理中開啟[電腦分析入口網站](https://aka.ms/desktopanalytics)。 選取 [開始]  。 或者，在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，選取 [電腦分析服務]  節點，然後選取 [規劃部署]  。

2. 在 [接受服務合約]  頁面上檢閱服務合約，然後選取 [接受]  。  

3. 在 [確認您的訂閱]  頁面上，檢閱所需的合格授權清單。 將設定切換為 [是否擁有其中一個支援版本或更高版本的訂閱]  旁的 [是]  ，然後選取 [下一步]  。  

4. 在 [Give users access] \(授與使用者存取權\)  頁面上：

    - **讓電腦分析代表您管理目錄角色**：電腦分析會自動為**工作區擁有者**指派**電腦分析系統管理員**角色。 如果這些群組已經是**全域管理員**，就不會有任何變更。

        如果您未選取此選項，電腦分析仍會將使用者新增為安全性群組的成員。 **全域管理員**需要手動為使用者指派**電腦分析系統管理員**角色。

        如需在 Azure Active Directory 中指派系統管理員角色權限的詳細資訊，以及指派給**電腦分析系統管理員**的權限，請參閱 [Administrator role permissions in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) (Azure Active Directory 中的系統管理員角色權限)。  

    - 電腦分析在 Azure Active Directory 中預先設定了**工作區擁有者**安全性群組，以建立及管理工作區和部署計劃。

        若要將使用者新增至群組，請在 [輸入名稱或電子郵件地址]  區段中，鍵入其名稱或電子郵件地址。 完成後，選取 [下一步]  。

5. 在 [設定您的工作區]  頁面上：  

    > [!NOTE]  
    > 若要完成此步驟，使用者需要**工作區擁有者**權限，以及 Azure 訂用帳戶和資源群組的其他存取權。 如需詳細資訊，請參閱[必要條件](overview.md#prerequisites)。  

    - 若要使用電腦分析的現有工作區，請加以選取，然後繼續下一個步驟。  

        > [!TIP]  
        > 每個 Azure AD 租用戶只擁能有一個電腦分析工作區。 裝置只能將診斷資料傳送至一個工作區。  

    - 若要為電腦分析建立工作區，請選取 [新增工作區]  。  

        1. 輸入全域唯一的 [工作區名稱]  。

        2. 選取 [Select the Azure subscription name for this workspace] \(選取此工作區的 Azure 訂用帳戶名稱\)  的下拉式清單，然後選擇此工作區的 Azure 訂用帳戶。  

        3. [新建]  資源群組或 [使用現有的]  資源群組。

        4. 從清單中選取 [區域]  ，然後選取 [新增]  。  

6. 選取新的或現有的工作區，然後選取 [設為電腦分析工作區]  。  然後在 [確認並授與存取]  對話方塊中選取 [繼續]  。  

7. 在新的瀏覽器索引標籤中，選擇要登入的帳戶。 選取 [代表您的組織同意]  選項，然後選取 [接受]  。  

    > [!Note]  
    > 此同意允許將工作區的 Log Analytics 讀取者角色指派給 MALogAnalyticsReader 應用程式。 電腦分析需要此應用程式角色。 如需詳細資訊，請參閱 [MALogAnalyticsReader 應用程式角色](troubleshooting.md#bkmk_MALogAnalyticsReader)。  

8. 回到 [設定您的工作區]  頁面，並選取 [下一步]  。  

9. 在 [最後步驟]  頁面上，選取 [移至電腦分析]  。

Azure 入口網站會顯示電腦分析 [首頁]  頁面。

## <a name="next-steps"></a>後續步驟

前往下一篇文章，以連線 Configuration Manager 與電腦分析。
> [!div class="nextstepaction"]  
> [連線 Configuration Manager](connect-configmgr.md)  
