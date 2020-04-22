---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 分支 1807 版中可用的新功能。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 398f16b8f75d894030d76406807f74bdaa4be9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695946"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Configuration Manager Technical Preview 1807 版的功能 

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager technical Preview 1807 版中可用的功能。 安裝此版本進行更新，並將新功能新增到您的 Technical Preview 網站。 

請先檢閱 [Technical Preview](technical-preview.md) 文章，再安裝此更新。 該篇文章會讓您熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何提供意見反應。     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>已知問題 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a> 關於 Office 365 軟體更新的問題
<!--521365-->
如果您使用 Technical Preview 分支版本 1806 和 1806.2 來管理 Office 365 更新，它們可能會無法安裝在用戶端上。 

#### <a name="workaround"></a>因應措施
- 刪除適用於 Office 365 的現有部署套件和軟體更新群組。  

- 從 2018 年 7 月 31 日開始，同步處理 Office 365 軟體更新，並且只部署最新的更新。  



</br>

**下列各節說明要在此版本中試用的新功能：**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> Community Hub
<!--1357766-->

Community Hub 是與他人共用實用 Configuration Manager 物件的集中式位置。 請查看 Configuration Manager 主控台中新的 [社群]  工作區，然後選取 [中樞]  節點。 使用 Community Hub 來下載下列類型的 Configuration Manager 物件： 
- 指令碼
- 設定項目

![Configuration Manager 主控台、社群工作區、中樞節點](media/1357766-hub.png)

若要查看有關可用項目的更多詳細資料，在中樞內按一下該項目。 從詳細資料頁面上，按一下 [下載]  以取得該項目。 當您從中樞下載項目時，即會自動將它新增到您的網站。 

![Configuration Manager 主控台、社群工作區、中樞節點、詳細資料頁面](media/1357766-hub-details.png)

**社群**工作區也會包含下列節點：

- **文件**：顯示 Configuration Manager [文件庫](https://docs.microsoft.com/sccm/)  

- **意見反應**：顯示 Configuration Manager [UserVoice 網站](https://configurationmanager.uservoice.com/)  


### <a name="prerequisites"></a>先決條件

- 在用戶端 OS 上使用 Configuration Manager 主控台。  

    - 或者：在伺服器 OS 上，停用 [Internet Explorer:Enhanced Security Configuration](https://go.microsoft.com/fwlink/?LinkId=253461) (Internet Explorer：增強型安全性設定) (不建議)。  

- 使用主控台的電腦需要存取網際網路，並連線到下列網站：  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>已知問題

目前無法在此版本中將項目提供給中樞。 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> 針對離線 OS 映像服務指定磁碟機  
<!--1358924-->

現在，根據您的 [UserVoice 意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive) \(英文\)，指定 Configuration Manager 要在 OS 映像離線服務期間使用的磁碟機。 此程序會使用暫存檔來耗用大量磁碟空間，因此，此選項可讓您彈性地選取要使用的磁碟機。 


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 接著，傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)以及您對於此功能的想法。

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 在功能區中，按一下 [設定站台元件]  ，然後選取 [軟體更新點]  。  

2. 切換到 [離線服務]  索引標籤，然後指定**供映像離線服務使用的本機磁碟機**的選項。  

此設定預設為 [自動]  。 使用此值，Configuration Manager 會選取其安裝所在的磁碟機。 

在離線服務期間，Configuration Manager 會將暫存檔儲存在資料夾 `<drive>:\ConfigMgr_OfflineImageServicing` 中。 它也會在此資料夾中掛接 OS 映像。 

檢閱 **OfflineServicingMgr.log** 記錄檔。 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> 從 Intune 共同管理的裝置同步活動
<!--1358565-->

在 Configuration Manager 主控台中顯示與 Microsoft Intune 共同管理的裝置是否為作用中。 此狀態會以 [Intune 資料倉儲](https://docs.microsoft.com/intune/reports-nav-create-intune-reports)的資料為基礎。 Configuration Manager 主控台中的 [用戶端狀態]  儀表板會顯示**非作用中用戶端正在使用 Intune**。 這個新類別適用於與 Configuration Manager 共同管理且處於非作用中狀態的裝置，但該裝置已於上週與 Intune 服務進行同步處理。


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 接著，傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)以及您對於此功能的想法。

如果您已經將網站設定來進行共同管理： 

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [共同管理]  節點。 在功能區中，按一下 [屬性]  。  

2. 切換到 [報表]  索引標籤。按一下 [登入]  並進行驗證。 然後按一下 [更新]  以啟用 Intune 資料倉儲的讀取權限。  

3. 當網站與 Intune 進行同步處理之後，移至 [監視]  工作區，然後選取 [用戶端狀態]  節點。 在 [整體用戶端狀態]  區段中，查看**非作用中用戶端正在使用 Intune** 的列。  

如需啟用共同管理的詳細資訊，請參閱 [Windows 10 裝置的共同管理](../../comanage/overview.md)。



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> 修復應用程式
<!--1357866-->

現在根據您的 [UserVoice 意見反應](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application) \(英文\)，指定 Windows Installer 和指令碼安裝程式部署類型的修復命令列。 


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 接著，傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)以及您對於此功能的想法。

1. 在 Configuration Manager 主控台中，開啟 Windows 安裝程式或指令碼安裝程式部署類型的屬性。  

2. 切換到 [程式]  索引標籤。指定**修復程式**命令。  

3. 部署應用程式。 在部署的 [部署設定]  索引標籤上，啟用選項以**讓使用者可嘗試修復此應用程式**。  


### <a name="known-issue"></a>已知問題

在此版本中看不到使用者可在軟體中心用來**修復**應用程式的新按鈕。  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> 透過電子郵件核准應用程式要求
<!--1321550-->

設定應用程式核准要求的電子郵件通知。 當使用者要求應用程式時，您會收到一封電子郵件。 按一下電子郵件中的連結來核准或拒絕要求，而不需使用 Configuration Manager 主控台。


### <a name="prerequisites"></a>先決條件

#### <a name="to-send-email-notifications"></a>傳送電子郵件通知
- 啟用 [依據裝置為使用者核准應用程式要求]  [選用功能](../servers/manage/install-in-console-updates.md#bkmk_options)。  

- 設定[警示的電子郵件通知](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)。  

#### <a name="to-approve-or-deny-requests-from-email"></a>從電子郵件核准或拒絕要求
如果您未設定這些必要條件，網站就會針對應用程式要求傳送電子郵件通知，但不含核准或拒絕要求的連結。  

- 在網站屬性中，**啟用此網站上所有提供者角色的 REST 端點，並允許 Configuration Manager 雲端管理閘道流量**。 如需詳細資訊，請參閱 [OData 端點資料存取](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)。  

    - 啟用 REST 端點之後重新啟動 SMS_EXEC 服務

- [雲端管理閘道](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- 將該網站與 [Azure 服務](../servers/deploy/configure/azure-services-wizard.md)配合以進行**雲端管理**  

    - 啟用 [Azure AD 使用者探索](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

    - 在 Azure AD 中，以手動方式設定此原生應用程式的下列設定：  

        - **重新導向 URI**：`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`。 使用雲端管理閘道 (CMG) 服務的完整網域名稱 (FQDN)，例如 GraniteFalls.Contoso.com。   

        - **資訊清單**：將 **oauth2AllowImplicitFlow** 設為 True：`"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 接著，傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)以及您對於此功能的想法。

1. 在 Configuration Manager 主控台中，將應用程式部署為可供使用者集合使用。 在 [部署設定]  頁面上，啟用它以進行核准。 接著，輸入「單一」  電子郵件地址來接收通知。  

     > [!Note]  
     > 您 Azure AD 組織中任何收到此電子郵件的人員都可核准要求。 不要將電子郵件轉寄給其他人，除非您想要他們採取動作。  

2. 以使用者身分，在軟體中心要求應用程式。  

3. 您會收到類似下列範例的電子郵件通知：  

![用於核准應用程式的範例電子郵件通知](media/1321550-email.png)

> [!Note]  
> 核准或拒絕的連結僅供單次使用。 例如，您可以設定群組別名來接收通知。 Meg 會核准要求。 現在 Bruce 無法拒絕要求。  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> 指令碼輸出的改善
<!--1236459-->

您現在可以檢視原始或結構化 JSON 格式的詳細指令碼輸出。 此格式可讓輸出變得更容易讀取與分析。 如果指令碼傳回有效的 JSON 格式文字，則可將詳細的輸出當成 **JSON 輸出**或**原始輸出**來檢視。 否則，唯一的選項是**指令碼輸出**。 

#### <a name="example-script-output-is-valid-json"></a>範例：指令碼輸出是有效的 JSON
命令：`$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>範例：指令碼輸出不是有效的 JSON
命令：`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>試試看！

請嘗試完成工作。 接著，傳送[意見反應](capabilities-in-technical-preview-1804.md#bkmk_feedback)以及您對於此功能的想法。

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選擇 [裝置集合]  節點。 以滑鼠右鍵按一下集合，然後選取 [執行指令碼]  。 如需建立和執行指令碼的詳細資訊，請參閱[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](../../apps/deploy-use/create-deploy-scripts.md)。  

2. 在目標集合上執行指令碼。  

3. 在 [執行指令碼] 精靈的 [指令碼狀態監視]  頁面上，選取底部的 [摘要]  索引標籤。 將位於上方的兩個下拉式清單變更為 [指令碼輸出]  和 [運算列表]  。 然後按兩下結果列，以開啟 [詳細的輸出]  對話方塊。  

4. 在 [執行指令碼] 精靈的 [指令碼狀態監視]  頁面上，選取底部的 [執行詳細資料]  索引標籤。 按兩下結果列，以開啟該裝置的 [詳細的輸出] 對話方塊。  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> 協力廠商軟體更新的改善
<!--1358714-->

您現在可以修改自訂類別目錄的屬性。

如需詳細資訊，請參閱[協力廠商軟體更新支援自訂類別目錄](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)。



## <a name="next-steps"></a>後續步驟

如需安裝或升級 Technical Preview 分支的詳細資訊，請參閱 [Technical Preview](technical-preview.md)。    

如需 Configuration Manager 不同分支的詳細資訊，請參閱[我應該使用哪個 Configuration Manager 分支？](../understand/which-branch-should-i-use.md)
