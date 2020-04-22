---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1709 版中可用的功能。
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3cefbbb9824266fd5fa057a7625332e85ec0ab32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705116"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Configuration Manager Technical Preview 1709 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1709 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 的已知問題：**
- **當您有以被動模式執行的站台伺服器時，更新到預覽版 1709 失敗**。 當您執行預覽版 1706、1707 或 1708 且有[以被動模式執行的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)時，必須先將被動模式站台伺服器解除安裝，才能順利將預覽站台更新到 1709 版。 當您的站台執行 1709 版之後，就可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。


**以下是您可以使用此版本試用的新功能。**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>改善的 Configuration Manager 主控台 VPN 設定檔體驗
<!-- 1313282 -->
我們在此版本中更新了 VPN 設定檔精靈和屬性頁面，以顯示所選平台的合適設定。 明確說來：

- 每個平台都有自己的工作流程，這表示新的 VPN 設定檔只包含平台支援的設定。
- [支援的平台]  頁面現在會出現在 [一般]  頁面之後。  您現在要先選擇平台再設定屬性值。
- 當平台設定為 [Android]  、[Android for Work]  或 [Windows Phone 8.1]  時，就不需要也不會顯示 [支援的平台]  頁面。
- Configuration Manager 用戶端型工作流程已結合混合式行動裝置 (MDM) 用戶端型 Windows 10 工作流程，它們支援相同的設定。
- 每個平台工作流程只包含適用於該工作流程的設定。  例如，Android 的工作流程包含適用於 Android 的設定，適用於 iOS 或 Windows 10 行動裝置版的設定不會再出現在 Android 的工作流程中。
- Windows 8.1 裝置會明確標示由 Configuration Manager 管理的設定。
- [自動 VPN] 頁面已淘汰並予移除。

這些變更適用於新的 VPN 設定檔。  

為將相容性風險降至最低，不變更現有的 VPN 設定檔。  當您編輯現有的設定檔時，顯示的設定一如當初建立設定檔時一樣。  

### <a name="try-it-out"></a>試試看！

使用一般的程序建立新的 VPN 設定檔。 請注意，在 [VPN 設定檔精靈] 選項中的第一頁已變更。

1. 請移至 [資產與相容性]   > [概觀]   > [合規性設定]   > [公司資源存取]   > [VPN 設定檔]  ，然後選擇 [建立 VPN 設定檔]  。
2. 在 [一般]  頁面上輸入名稱，並在 [指定您要建立的 VPN 設定檔類型]  下選擇下列選項之一：

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS 和 macOS  
    - Android  
    - Android for Work  

3. 如果您選擇 **Windows 8.1**，就可以選擇 [建立新的設定檔]  或 [從檔案匯入]  。
4. 完成精靈以建立設定檔。

當您選取不同的平台時，請注意，只會顯示與所選平台相關的設定。

## <a name="co-management-for-windows-10-devices"></a>Windows 10 裝置的共同管理    
<!-- 1350871 -->
許多客戶想要以他們管理使用簡化、低成本、雲端型解決方案之行動裝置的相同方式來管理 Windows 10 裝置。 不過，從傳統的管理轉換成現代化的管理可說困難重重。 從 Windows 10 1607 版 (也稱為年度更新版) 開始，您可以讓 Windows 10 裝置同時加入內部部署 Active Directory (AD) 和雲端型 Azure AD (混合式 Azure AD)。 共同管理能夠利用這項功能改進，讓您同時使用 Configuration Manager 和 Intune 來管理 Windows 10 裝置。 這個解決方案能讓您從傳統管理過渡到現代化管理，並提供您使用分段式方法來完成轉換。 

### <a name="prerequisites"></a>先決條件
您必須先備妥下列必要條件，才能啟用共同管理。 有一般的必要條件，以及針對現有 Configuration Manager 用戶端和非用戶端裝置的不同必要條件。

### <a name="known-issues"></a>已知問題
建立共同管理原則之後，即無法編輯原則。 若要變更原則，請刪除原則，然後使用您需要的設定重新建立原則。 

#### <a name="general-prerequisites"></a>一般先決條件
啟用共同管理的一般必要條件如下：  

- Technical Preview for Configuration Manager 版本 1709
- Azure AD 
- 所有使用者的 EMS 或 Intune 授權
- Intune 訂閱 &#40;在 Intune 中設定為 [Intune]  的 MDM 授權單位&#41;

   > [!Note]  
   > 如有混合式的 MDM 環境 (整合了 Configuration Manager 的 Intune)，即無法啟用共同管理。

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>現有 Configuration Manager 用戶端的其他必要條件
- Windows 10 版本 1709 (Fall Creators Update) 及更新版本
- 混合式 Azure AD 聯結 (加入 AD 與 Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>新 Windows 10 裝置的其他必要條件
- Windows 10 版本 1709 (Fall Creators Update) 及更新版本
- Configuration Manager 中的[雲端管理閘道](../clients/manage/manage-clients-internet.md#cloud-management-gateway)

### <a name="workloads-you-can-switch-to-intune"></a>可以切換到 Intune 的工作負載
啟用共同管理之後，Configuration Manager 會繼續管理所有工作負載。 當您認為準備好時，您可以指揮 Intune 開始管理可用的工作負載。 在此版本中，您可以使用 Intune 管理下列工作負載。   

#### <a name="compliance-policies"></a>相容性原則
相容性原則會定義裝置必須符合，才能被條件式存取原則視為相容的規則與設定。 您也可以使用合規性政策，來監視和修復與條件式存取無關的裝置合規性問題。

#### <a name="windows-update-for-business-policies"></a>商務用 Windows Update 原則
商務用 Windows Update 原則可讓您設定 Windows 10 功能更新或品質更新的延遲原則，讓商務用 Windows Update 直接管理 Windows 10 裝置。 如需詳細資料，請參閱[設定商務用 Windows Update 延遲原則](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)。  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Azure 上的 Intune 針對共同受管理裝置提供的遠端動作
當 Windows 10 裝置啟用共同管理時，您可從 Azure 上的 Intune 取得下列遠端動作：  
- [重設為原廠設定](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [選擇性抹除](https://docs.microsoft.com/intune/apps-selective-wipe)
- [刪除裝置](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [重新啟動裝置](https://docs.microsoft.com/intune/device-restart)
- [重新開始](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>準備 Intune 進行共同管理
請先建立您在 Intune 中需要的設定檔和原則，確保裝置繼續受到保護，再從 Configuration Manager 切換至 Intune 工作負載。
您可以根據 Configuration Manager 中的物件，在 Intune 中建立物件。 或者，如果您目前的策略是以舊版或傳統管理為基礎，您可能要回到前面的步驟，重新思考現代化管理需要哪些原則與設定檔。 使用下列資源建立原則與設定檔。    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [商務用 Windows Update 原則](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [裝置組態設定檔](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>共同管理的架構概觀
下圖提供共同管理的架構概觀，以及如何將它放入現有的設定與 Intune 基礎結構。

![共同管理架構圖](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>啟用共同管理的案例  
您可以啟用在 Microsoft Intune 與現有的 Windows 10 Configuration Manager 用戶端都註冊的 Windows 10 裝置共同管理。 這兩種情況都會導致 Windows 10 裝置由 Configuration Manager 和 Intune 同時管理，以及加入 AD 和 Azure AD。  

#### <a name="devices-enrolled-in-intune"></a>在 Intune 中註冊的裝置  
在 Intune 中註冊 Windows 10 裝置時，您可以在裝置上安裝 Configuration Manager 用戶端 (使用特定的命令列引數)，準備用戶端以進行共同管理。 然後，從 Configuration Manager 主控台啟用共同管理，開始將特定的工作負載移至特定 Windows 10 裝置的 Intune。  

至於尚未在 Intune 中註冊的 Windows 10 裝置，您可以使用 Azure 中的自動註冊來註冊裝置。 新的 Windows 10 裝置則可以使用 Windows AutoPilot 來設定全新體驗 (OOBE)，包括在 Intune 中註冊裝置的自動註冊。  

#### <a name="configuration-manager-clients"></a>Configuration Manager 用戶端
當您擁有的是 Configuration Manager 用戶端的 Windows 10 裝置時，您可以註冊這些裝置並從 Configuration Manager 主控台啟用共同管理。 Configuration Manager 會根據 Azure AD 租用戶資訊，觸發向 Intune 自動註冊。  

### <a name="prepare-windows-10-devices-for-co-management"></a>準備 Windows 10 裝置進行共同管理
您可以在已加入 AD 和 Azure AD，且已在 Intune 與 Configuration Manager 用戶端註冊的 Windows 10 裝置上啟用共同管理。 若為新的 Windows 10 裝置，以及已在 Intune 註冊的裝置，要先安裝 Configuration Manager 用戶端才能共同管理。 若為已是 Configuration Manager 用戶端的 Windows 10 裝置，您可以向 Intune 註冊這些裝置，並在 Configuration Manager 主控台啟用共同管理。

#### <a name="command-line-to-install-configuration-manager-client"></a>安裝 Configuration Manager 用戶端的命令列
為還不是 Configuration Manager 用戶端的 Windows 10 裝置，使用 Intune 建立應用程式。 當您在後列各節中建立應用程式時，請使用下列命令列：

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*雲端管理閘道相互驗證端點的 URL*&#62;/ CCMHOSTNAME=&#60;*雲端管理閘道相互驗證端點的 URL*&#62; SMSSiteCode=&#60;*站台碼*&#62; SMSMP=https:&#47;/&#60;*MP 的 FQDN*&#62; AADTENANTID=&#60;*AAD 租用戶識別碼*&#62; AADTENANTNAME=&#60;*租用戶名稱*&#62; AADCLIENTAPPID=&#60;*AAD 整合的伺服器應用程式識別碼*&#62; AADRESOURCEURI=https:&#47;/&#60;*資源識別碼*&#62;”

例如，如果您有下列值：

- **雲端管理閘道相互驗證端點的 URL**：https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >**雲端管理閘道相互驗證端點的 URL** 值的 **vProxy_Roles** SQL 檢視請使用 **MutualAuthPath** 值。

- **管理點 (MP) 的 FQDN**：sccmmp.corp.contoso.com    
- **站台碼**：PS1    
- **Azure AD 租用戶識別碼**：72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Azure AD 租用戶名稱**：contoso    
- **Azure AD 用戶端應用程式識別碼**：bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **AAD 資源識別碼 URI**：ConfigMgrServer    

  > [!Note]    
  > 使用在 **AAD 資源識別碼 URI**值的 **vSMS_AAD_Application_Ex** SQL 檢視中找到的 **IdentifierUri** 值。

您可能會使用下列命令列：

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
>您可以使用下列步驟，找到您網站的命令列參數：     
> 1. 在 Configuration Manager 主控台中，移至 [管理]   > [概觀]   > [雲端服務]   > [共同管理]  。  
> 2. 在 [首頁] 索引標籤的管理群組中，選擇 [設定共同管理]  以開啟 [共同管理登入精靈]。    
> 3. 在 [訂閱] 頁面上，按一下 [登入]  登入您的 Intune 租用戶，然後按一下 [下一步]  。    
> 4. 在 [啟用] 頁面上，按一下 [在 Intune 中註冊的裝置]  區段中的 [複製]  ，將命令列複製到剪貼簿，然後儲存命令列以在建立應用程式的程序中使用。  
> 5. 按一下 [取消]  結束精靈。

#### <a name="new-windows-10-devices"></a>新的 Windows 10 裝置
若為新的 Windows 10 裝置，您可以使用 Autopilot 服務設定全新體驗，包括將裝置加入 AD 和 Azure AD，以及在 Intune 中註冊裝置。 然後使用 Intune 建立應用程式來部署 Configuration Manager 用戶端。  
1. 啟用新 Windows 10 裝置的 AutoPilot。 如需詳細資料，請參閱 [Windows AutoPilot 概觀](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)。  
2. 在 Azure AD 中設定自動註冊，以在 Intune 中自動註冊裝置。 如需詳細資料，請參閱 [註冊 Microsoft Intune 的 Windows 裝置](https://docs.microsoft.com/intune/windows-enroll)。
3. 在 Intune 中使用 Configuration Manager 用戶端套件建立應用程式，並將應用程式部署到您要共同管理的 Windows 10 裝置。 當您執行步驟來[使用 Azure AD 從網際網路安裝用戶端](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure)時，請使用[安裝 Configuration Manager 用戶端的命令列](#command-line-to-install-configuration-manager-client)。   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>未在 Intune 或 Configuration Manager 用戶端註冊的 Windows 10 裝置
若是未在 Intune 中註冊或有 Configuration Manager 用戶端的 Windows 10 裝置，您可以使用自動註冊在 Intune 中註冊裝置。 然後使用 Intune 建立應用程式來部署 Configuration Manager 用戶端。
1. 在 Azure AD 中設定自動註冊，以在 Intune 中自動註冊裝置。 如需詳細資料，請參閱 [註冊 Microsoft Intune 的 Windows 裝置](https://docs.microsoft.com/intune/windows-enroll)。  
2. 在 Intune 中使用 Configuration Manager 用戶端套件建立應用程式，並將應用程式部署到您要共同管理的 Windows 10 裝置。 當您執行步驟來[使用 Azure AD 從網際網路安裝用戶端](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure)時，請使用[安裝 Configuration Manager 用戶端的命令列](#command-line-to-install-configuration-manager-client)。

#### <a name="windows-10-devices-enrolled-in-intune"></a>在 Intune 中註冊的 Windows 10 裝置
若是已在 Intune 註冊的 Windows 10 裝置，請使用 Intune 建立應用程式以部署 Configuration Manager 用戶端。 當您執行步驟來[使用 Azure AD 從網際網路安裝用戶端](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure)時，請使用[安裝 Configuration Manager 用戶端的命令列](#command-line-to-install-configuration-manager-client)。  

### <a name="switch-configuration-manager-workloads-to-intune"></a>將 Configuration Manager 工作負載切換至 Intune
在上一節中，您已備妥 Windows 10 裝置進行共同管理。 這些裝置現在已加入 AD 和 Azure AD，而且它們已在 Intune 中註冊，並具有 Configuration Manager 用戶端。 您可能仍擁有已加入 AD 並具有 Configuration Manager 用戶端的 Windows 10 裝置，但它們尚未加入 Azure AD 或在 Intune 中註冊。 下列程序提供啟用共同管理的步驟，備妥其餘 Windows 10 裝置 (未向 Intune 註冊的 Configuration Manager 用戶端) 進行共同管理，並可讓您開始將特定的 Configuration Manager 工作負載切換至 Intune。

1. 在 Configuration Manager 主控台中，移至 [管理]   > [概觀]   > [雲端服務]   > [共同管理]  。    
2. 在 [首頁] 索引標籤的管理群組中，選擇 [設定共同管理]  以開啟 [共同管理登入精靈]。    
3. 在 [訂閱] 頁面上，按一下 [登入]  登入您的 Intune 租用戶，然後按一下 [下一步]  。   
4. 在 [預備] 頁面上設定下列設定，然後按一下 [下一步]  ：
    - **試驗群組**：試驗群組包含一或多個您選取的集合。 使用此群組作為共同管理分段推出的一部分。 您可以從小型的測試集合開始，當向更多使用者與裝置推出共同管理時，再新增更多的集合到試驗群組。 您可以隨時從共同管理屬性變更試驗群組中的集合。
    - **Production**：當您選取此設定時，會啟用所有支援的 Windows 10 裝置進行共同管理。 設定有一或多個集合的**排除群組**。 凡是此群組中任何集合成員的裝置，都會從使用共同管理中排除。 
5. 在 [啟用] 頁面上，選擇 [試驗]  或 [所有]  (取決於您在 [預備] 頁面上設定的設定) 以啟用 Intune 的自動註冊，然後按一下 [下一步]  。 當您選擇 [試驗]  時，只有為試驗群組成員的 Configuration Manager 用戶端會在 Intune 中自動註冊。 這可讓您在用戶端子集上啟用共同管理，初步測試共同管理，並推出使用分段方法的共同管理。 
6. 在 [工作負載] 頁面上，選擇是否要將 Configuration Manager 工作負載切換為受 Intune 管理，然後按一下 [下一步]  。 使用滑桿選取是要切換到試驗群組工作負載，還是所有 Windows 10 用戶端 (取決於您在 [預備] 頁面上設定的設定)。 
7. 若要啟用共同管理，請完成精靈。  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>請參閱
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。 
