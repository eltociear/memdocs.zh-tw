---
title: 共同管理網際網路型裝置
titleSuffix: Configuration Manager
description: 了解如何準備 Windows 10 網際網路型裝置以進行共同管理。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 32c148b695a47241c6646a2a7309f0a27f3b3070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691046"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>如何準備網際網路型裝置以進行共同管理

此文章著重於新網際網路型裝置共同管理的第二個路徑。 此案例是當您有新的 Windows 10 裝置加入 Azure AD，並自動註冊到 Intune。 請安裝 Configuration Manager 用戶端以達到共同管理狀態。  

## <a name="windows-autopilot"></a>Windows Autopilot

針對新的 Windows 10 裝置，您可以使用 Autopilot 服務設定全新體驗 (OOBE)。 此程序包括將裝置加入 Azure AD，並在 Intune 中註冊裝置。  

如需詳細資訊，請參閱 [Windows Autopilot 概觀](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) \(部份機器翻譯\)。

若要將裝置設定為在加入 Azure AD 時自動註冊到 Intune，請參閱 [為 Microsoft Intune 註冊 Windows 裝置](https://docs.microsoft.com/intune/windows-enroll)。  

### <a name="gather-information-from-configuration-manager"></a>從 Configuration Manager 收集資訊

使用 Configuration Manager 來收集和報告 Intune 所需的裝置資訊。 此資訊包括裝置序號、Windows 產品識別碼及硬體識別碼。 它用於在 Intune 中註冊裝置以支援 Windows Autopilot。

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區，依序展開 [報表]  節點和 [報表]  ，然後選取 [硬體 - 一般]  節點。  

2. 執行報表 **Windows AutoPilot 裝置資訊**，然後檢視結果。  

3. 在報表檢視器中選取 [匯出]  圖示，然後選擇 [CSV (逗號分隔)]  選項。  

4. 儲存檔案之後，將資料上傳至 Intune。  

如需詳細資訊，請參閱[在 Intune 中新增裝置](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices)。

### <a name="autopilot-for-existing-devices"></a>適用於現有裝置的 Autopilot
<!--1358333-->

您可以在 Windows 10 1809 版或更新版本中找到[適用於現有裝置的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) \(英文\)。 此功能可讓您使用單一、原生的 Configuration Manager 工作順序，針對 [Windows Autopilot 使用者驅動模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) \(部分機器翻譯\) 對 Windows 7 裝置重新安裝映像並進行佈建。

如需詳細資訊，請參閱[適用於現有裝置的 Windows Autopilot 工作順序](../osd/deploy-use/windows-autopilot-for-existing-devices.md)。

## <a name="install-the-configuration-manager-client"></a>安裝 Configuration Manager 用戶端

針對第二個路徑中的網際網路型裝置，您需要在 Intune 中建立應用程式。 將此應用程式部署至還不是 Configuration Manager 用戶端的 Windows 10 裝置。

> [!NOTE]
> 在 Intune 中將此應用程式指派給裝置之前，請確定裝置信任 CMG 伺服器驗證憑證。 如需詳細資訊，請參閱[用戶端的 CMG 受信任的根憑證](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot)。 若裝置不信任 CMG 伺服器驗證憑證，則會在用戶端上的 ccmsetup.log on 中看到 WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA 錯誤。

### <a name="get-the-command-line-from-configuration-manager"></a>從 Configuration Manager 取得命令列

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [共同管理]  節點。  

2. 選取共同管理物件，然後在功能區中選擇 [屬性]  。  

3. 在 [啟用]  索引標籤上，複製命令列。 將它貼到 [記事本] 並儲存，以準備供下一個程序使用。  

下列命令列是一個範例：`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215-->
決定環境所需的命令列屬性：  

- 所有案例都需要有下列命令列屬性：  
  - CCMHOSTNAME  
  - SMSSITECODE  

- 使用 Azure AD 進行用戶端驗證，而不是以 PKI 為基礎的用戶端驗證憑證時，需要下列屬性：  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- 如果用戶端將漫遊回到內部網路，則需要下列屬性：  
  - SMSMP  

- 如果使用自己的 PKI 憑證，且 CRL 未發佈到網際網路，則需要下列參數：  
  - /noCRLCheck  

    如需詳細資訊，請參閱[規劃 CRL](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。

- 從 2002 版開始，使用下列屬性以在用戶端註冊後立即啟動工作順序：
  - PROVISIONTS

    如需詳細資訊，請參閱[關於用戶端安裝屬性 - PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts)。

此站台會將額外的 Azure AD 資訊發佈至雲端管理閘道 (CMG)。 已加入 Azure AD 的用戶端會在 ccmsetup 過程中從 CMG 取得此資訊 (使用它所加入的同一租用戶)。 在具有多個 Azure AD 租用戶的環境中，此行為可進一步簡化共同管理的裝置註冊作業。 唯二必要的 ccmsetup 屬性分別為 **CCMHOSTNAME** 和 **SMSSiteCode**。<!--3607731-->

> [!NOTE]
> 如果您已從 Intune 部署 Configuration Manager 用戶端，請使用新的命令列與新的 MSI 更新 Intune 應用程式。 <!-- SCCMDocs-pr issue 3084 -->

下列範例包含所有這些屬性：

`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001`

如需詳細資訊，請參閱[用戶端安裝屬性](../core/clients/deploy/about-client-installation-properties.md)。

### <a name="create-the-app-in-intune"></a>在 Intune 中建立應用程式

1. 移至 [Azure 入口網站](https://portal.azure.com)，然後開啟 [Intune] 頁面。  

2. 選取 [用戶端應用程式]   > [應用程式]   > [新增]  。  

3. 在 [其他]  下，選取 [企業營運應用程式]  。  

4. 上傳 **ccmsetup.msi** 應用程式套件檔案。 在 Configuration Manager 站台伺服器上的下列資料夾中尋找此檔案：`<ConfigMgr installation directory>\bin\i386`。  

    > [!Tip]  
    > 當您更新站台時，請務必也在 Intune 中更新此應用程式。  

5. 更新應用程式之後，使用從 Configuration Manager 複製的命令列設定應用程式資訊。  

> [!IMPORTANT]
> 如果您自訂此命令列，請確定其長度不超過 1024 個字元。 當命令列長度超過 1024 個字元時，用戶端安裝會失敗。
