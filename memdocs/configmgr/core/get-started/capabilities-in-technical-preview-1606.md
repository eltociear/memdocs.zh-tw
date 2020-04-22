---
title: Technical Preview 1606 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1606 版中可用的功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05e7bbe6373ed91de5a2bb8e99a8425e733274f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705566"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Configuration Manager Technical Preview 1606 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1606 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    

**此 Technical Preview 的已知問題：**  
*  當您從 Technical Preview 1604 更新至 1605，再更新至 1606 版時，更新可能會失敗，並出現類似 **cmupdate.log** 中所記錄的下列錯誤：

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    如果發生這種情況，請在 [更新與服務]  節點中，按一下 [檢查更新]  ，然後**重試**更新安裝。
    ***

**以下是您可以使用此版本試用的新功能。**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a> 自動將裝置分類為集合
您可以建立裝置類別，如此可在您使用 Configuration Manager 與 Microsoft Intune 時自動將裝置放在裝置集合中。 使用者向 Intune 註冊裝置時，必須選擇裝置類別。 您也可以從 Configuration Manager 主控台中變更裝置類別。

**重要：** 這項功能適用於 Microsoft Intune 的 **2016 年 6 月**版。 請先確定已更新為此版，再嘗試這些程序。

### <a name="try-it-out"></a>試試看！

### <a name="create-a-set-of-device-categories"></a>建立一組裝置類別
1.  在 Configuration Manager 主控台的 [資產與相容性]  工作區中，展開 [概觀]  ，然後按一下 [裝置集合]  。
2.  在 [常用]  索引標籤的 [類別]  群組中，按一下 [管理裝置類別]  。
3.  在 [管理裝置類別]  對話方塊中，您可以建立、編輯或移除類別。 嘗試建立新的類別。

### <a name="associate-a-collection-with-a-device-category"></a>建立集合與裝置類別的關聯
當您建立集合與裝置類別的關聯時，您在類別中指定的所有裝置都會新增至該集合。
1.  在裝置集合的 [內容]  對話方塊中，按一下 [新增規則]   > [裝置類別規則]  。
2.  在 [Create Device Category Membership Rule]\(建立裝置類別成員資格規則)  對話方塊中，選取將套用至集合中所有裝置的類別。
3.  關閉 [Create Device Category Membership Rule]\(建立裝置類別成員資格規則)  對話方塊和集合的 [內容] 對話方塊。

### <a name="change-the-category-of-a-device"></a>變更裝置類別
1.  在 Configuration Manager 主控台的 [資產與相容性]  工作區中，展開 [概觀]  ，然後按一下 [裝置]  。
2.  從 [裝置]  清單中選取裝置，然後在 [常用]  索引標籤的 [裝置]  群組中，按一下 [變更類別]  。
3.  在 [編輯裝置類別]  對話方塊中，選擇要套用至此裝置的類別，然後按一下 [確定]  。

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a> 針對必要應用程式和軟體更新部署的強制執行寬限期

在某些情況下，您可能想要提供更多時間給使用者，以在超過您設定的任何期限之後，還能安裝必要應用程式部署或軟體更新。 當電腦已關閉一段時間，而且需要安裝大量應用程式或更新部署時，通常可能會需要此設定。
例如，如果使用者剛結束休假，他們可能必須等候很長的時間，讓逾期的應用程式部署完成安裝。
為了協助解決這個問題，您現在可以藉由將 Configuration Manager 用戶端設定部署至集合，來定義施行寬限期。

### <a name="try-it-out"></a>試試看！

若要設定寬限期，請採取下列動作：

1.  在用戶端設定的 [電腦代理程式]  頁面上，將新內容 [延後到部署期限後施行的寬限期 (小時)]  設定為 **1** 到 **120** 小時之間的值。
2.  在新的必要應用程式部署中，或在現有部署的內容中，選取 [排程]  頁面上的 [根據使用者喜好設定，延遲強制施行此部署，最多可延後用戶端設定中所定義的寬限期]  核取方塊。
已選取此核取方塊並以您同時部署用戶端設定之裝置為目標的所有部署，都會使用此施行寬限期。

如果您設定施行寬限期並選取此核取方塊，一旦應用程式安裝到期，就會在使用者所設定寬限期內的第一個非營業時間進行安裝。 不過如果需要，使用者仍可隨時開啟 [軟體中心] 並安裝應用程式。 過了寬限期後，就會強制還原為逾時部署的標準行為。
[軟體更新部署精靈]、[自動部署規則精靈] 和 [內容] 頁面都已新增類似的選項。

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>將 Configuration Manager 作為含 Device Guard 的受管理安裝程式

Device Guard 是 Windows 10 功能，它使用硬體和軟體功能來嚴格控制可在裝置上執行的功能。

您可以在[此 Technet 文章](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview)中，閱讀有關 Device Guard 功能及其運作方式的詳細概觀。

在此版本中，Configuration Manager 可以與 Device Guard 和 [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) 交互操作，讓使用 Configuration Manager 部署的可執行檔和 DLL 檔案自動受到信任並視為來自受管理的安裝程式，這表示它們可以在目標裝置上執行；至於其他軟體，除非其他 AppLocker 規則明確允許執行，否則將無法執行。  

目前，您無法從 Configuration Manager 主控台設定這項功能。 若要設定此原則，您必須在每個用戶端上設定登錄機碼，並在用戶端上設定 Windows 服務。
完成後，即可設定 AppLocker 原則檔案。 設定原則檔案之後，您就可以將它部署至任何相容的用戶端裝置。


如同所有 AppLocker 原則，具有受管理安裝程式規則的原則可以在兩個模式下執行：

- 稽核模式 - 應用程式已標記防止執行，但任何已封鎖的應用程式都會在記錄檔中報告 (更新版的 Configuration Manager 將提供支援)。
- 強制啟用 - 應用程式會遭到封鎖，無法執行。

如需如何搭配使用 Device Guard 和 Configuration Manager 的進一步資訊，請參閱 [Enterprise Mobility and Security 部落格](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10)。

延伸閱讀：

- [Device Guard 簡介](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Device Guard 憑證和相容性](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Device Guard 部署指南](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a> 針對內部部署行動裝置管理提供多個裝置管理點  
  在 Technical Preview 1606 中，內部部署行動裝置管理 (MDM) 支援 Windows 10 年度更新版中的一項新功能，該功能會自動設定已註冊的裝置，以提供多個可供使用的裝置管理點。 這項功能允許在通常使用的裝置無法使用時，以其他裝置管理點代替。 這項功能只適用於安裝 Windows 10 年度更新版的電腦。  

### <a name="try-it-out"></a>試試看！  

1.  在您的階層中安裝多個裝置管理點。  

2.  註冊 Windows 10 年度更新版裝置，以進行內部部署行動裝置管理。  

如需如何準備站台及註冊裝置以進行內部部署行動裝置管理的資訊，請參閱[使用內部部署基礎結構管理行動裝置](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>用於管理網際網路上之用戶端的雲端 Proxy 服務

雲端 Proxy 服務提供簡單的方法，管理網際網路上的 Configuration Manager 用戶端。 部署至 Microsoft Azure 且需要 Azure 訂用帳戶的服務，使用稱為雲端 Proxy 連接器端點的新角色，連線到內部部署的 Configuration Manager 基礎結構。 在它完全部署及設定好後，用戶端將能夠存取內部部署的 Configuration Manager 站台系統角色，不論它們是連線到內部的私人網路還是網際網路。

您可以使用 Configuration Manager 主控台將服務部署至 Azure、新增雲端 Proxy 連接器端點角色，並設定站台系統角色以允許雲端 Proxy 流量。 雲端 Proxy 服務目前只支援管理點、發佈點和軟體更新點角色。

需要用戶端憑證和安全通訊端層 (SSL) 憑證，才能進行電腦驗證，以及加密不同服務層級之間的通訊。 用戶端電腦通常會透過強制執行群組原則來接收用戶端憑證。 若要加密用戶端與裝載角色的站台系統伺服器之間的流量，您必須從 CA 建立自訂 SSL 憑證。 除了這兩種憑證類型之外，您也必須在 Azure 上設定管理憑證，以允許 Configuration Manager 部署雲端 Proxy 服務。  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>TP 1606 中雲端 Proxy 服務的需求
- 用戶端電腦和執行雲端 Proxy 連接器端點的站台系統伺服器。
- 來自內部 CA 的自訂 SSL 憑證 - 用來加密與用戶端電腦的通訊，並驗證雲端 Proxy 服務的身分識別。
- 雲端服務的 Azure 訂用帳戶。
- Azure 管理憑證 - 用來向 Azure 驗證 Configuration Manager。

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>TP 1606 中雲端 Proxy 服務的限制

- 只支援管理點、發佈點和軟體更新點角色。
- 不支援使用者原則。
- 無法搭配 Configuration Manager 中的[內部部署行動裝置管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)使用。
- 只有 Azure 的公用雲端平台才提供支援。


### <a name="try-it-out"></a>試試看！

部署雲端 Proxy 服務的程序包含下列步驟：

1. 建立及發行雲端 Proxy 服務的自訂 SSL 憑證。
1. 匯出用戶端憑證的根目錄。
2. 將管理憑證上傳至 Azure。
3. 在 Configuration Manager 主控台中設定雲端 Proxy 服務。
4. 設定主要站台以使用用戶端憑證驗證。
5. 將雲端 Proxy 連接器端點新增至您的站台。
6. 將站台系統角色設定為接受雲端 Proxy 流量。

下列各節提供完成這些步驟的詳細資訊。

#### <a name="create-a-custom-ssl-certificate"></a>建立自訂 SSL 憑證

您可以透過針對雲端架構發佈點所執行的相同方式，為雲端 Proxy 服務建立自訂 SSL 憑證。 請遵循[為雲端架構的發佈點部署服務憑證](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)中的指示，但針對下列作業採用不同的做法：

* 設定新的憑證範本時，將 [讀取]  和 [註冊]  權限授與您針對 Configuration Manager 伺服器所設定的安全性群組。

#### <a name="export-the-client-certificates-root"></a>匯出用戶端憑證的根目錄

匯出網路上所使用之用戶端憑證根目錄的最簡單方式，是在具有用戶端憑證的其中一部加入網域的電腦上開啟並複製此用戶端憑證。

>[!NOTE]
>您想要透過雲端 Proxy 服務管理的任何電腦上，以及裝載雲端 Proxy 連接器端點的站台系統伺服器上，都需要用戶端憑證。 如果您必須將用戶端憑證新增至任何電腦，請參閱[部署 Windows 電腦的用戶端憑證](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)。

1. 在 [執行] 視窗中，輸入 **mmc** 並按下 Return 鍵。
2. 在管理主控台的 [檔案] 功能表中，按一下 [新增/移除嵌入式管理單元...]  。
3. 在 [新增或移除嵌入式管理單元] 對話方塊中，依序按一下 [憑證]  、[新增 >]  、[電腦帳戶]  、[下一步]  、[本機電腦]  和 [完成]  。 按一下 [確定]  關閉對話方塊。
4. 移至 [憑證] > [個人] > [憑證]  。
5. 在電腦上按兩下憑證以進行用戶端驗證，按一下 [憑證路徑] 索引標籤，然後按兩下根授權單位 (位於最上層路徑)。
6.  按一下 [詳細資料] 索引標籤，然後按一下 [複製到檔案...]  。
7. 使用預設憑證格式完成 [憑證匯出精靈]。 記下您所建立之根憑證的名稱和位置。 您將需要此資訊，以在稍後步驟中設定雲端 Proxy 服務。

#### <a name="upload-the-management-certificate-to-azure"></a>將管理憑證上傳至 Azure

Configuration Manager 需要 Azure 管理憑證才能存取 Azure API 及設定雲端 Proxy 服務。 如需如何上傳管理憑證的詳細資訊和指示，請參閱 Azure 文件中的下列文章：
- [Azure 雲端服務的憑證概觀](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [上傳 Azure 管理 API 管理憑證](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)。

請務必複製與管理憑證相關聯的訂用帳戶 ID。 您將需要此資訊，以在 Configuration Manager 主控台中設定雲端 Proxy 服務。

#### <a name="set-up-cloud-proxy-service"></a>設定雲端 Proxy 服務

1. 在 Configuration Manager 主控台中，移至 [管理] > [雲端服務] > [雲端 Proxy 服務]  。
2. 按一下 [建立雲端 Proxy 服務]  。
3. 在 [建立雲端 Proxy 服務精靈] 中，輸入您的 Azure 訂用帳戶 ID (複製自 Azure 管理入口網站)，按一下 [瀏覽]，然後選取您用來上傳作為 Azure 管理憑證的憑證檔案。 按一下 [下一步]  。 請稍候片刻，主控台將會連線到 Azure。
4. 在精靈中填寫其他詳細資料：
    - 指定您要從自訂 SSL 憑證匯出的私密金鑰 (.pfx 檔案)。
    - 指定從用戶端憑證匯出的根憑證。
    - 指定建立新的憑證範本時所使用的相同服務名稱 FQDN。
    - 清除 [驗證用戶端憑證撤銷]  旁邊的方塊 (除非您要公開發行 CRL 資訊)。
    - 完成時按一下 [下一步]  。
5. 檢閱設定，然後按一下 [下一步]  。 Configuration Manager 隨即開始設定服務。 當精靈完成時，您可以按一下 [關閉]  ，不過需要 5 到 15 分鐘才能完成 Azure 中的服務佈建。 檢查新安裝之雲端 Proxy 服務的 [狀態]  欄，以判斷服務何時就緒。

#### <a name="configure-primary-site-for-client-certification-authentication"></a>設定主要站台以進行用戶端憑證驗證

1. 在 Configuration Manager 主控台中，移至 [管理] > [站台設定] > [站台]  。
2. 選取您想要透過雲端 Proxy 服務管理之用戶端的主要站台，然後按一下 [內容]  。
3. 在主要站台內容表的 [用戶端電腦通訊] 索引標籤上，核取 [使用可用的 PKI 用戶端憑證 (用戶端驗證)]  旁邊的方塊。
4. 確定清除 [由用戶端檢查站台系統的憑證撤銷清單 (CRL)]  旁邊的方塊。 只有您要公開發行 CRL 時才需要此選項。
5. 按一下 [確定]  。

#### <a name="add-the-cloud-proxy-connector-point"></a>新增雲端 Proxy 連接器端點

雲端 Proxy 連接器端點是用來與雲端 Proxy 服務進行通訊的新站台系統角色。 若要新增雲端 Proxy 連接器端點，請遵循[為 Configuration Manager 新增站台系統角色](../../core/servers/deploy/configure/add-site-system-roles.md)中的指示。

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>為雲端 Proxy 流量設定角色

設定雲端 Proxy 服務的最後一個步驟，就是設定接受雲端 Proxy 流量的站台系統角色。 在 Tech Preview 1606 中，雲端 Proxy 服務只支援管理點、發佈點和軟體更新點角色。 您必須個別設定每個角色。

1. 在 Configuration Manager 主控台中，移至 [管理] > [站台設定] > [伺服器和站台系統角色]  。
2. 按一下代表您想要為雲端 Proxy 流量設定之角色的站台系統伺服器。
3. 按一下此角色，然後按一下 [內容]  。
4. 在角色內容表的 [用戶端連線] 底下，選擇 [允許 Configuration Manager 雲端 Proxy 流量]  旁邊的 [HTTPS]  核取方塊，然後按一下 [確定]  。 針對其餘角色重複上述步驟。

#### <a name="check-status-on-a-client-on-the-internet"></a>檢查網際網路上之用戶端的狀態

服務和角色設定完成之後，內部用戶端會在出現下一個位置要求時，取得雲端 Proxy 服務的位置。 已更新位置資訊的用戶端可接著與網際網路上的 Configuration Manager 進行通訊。 位置要求的輪詢週期為每 24 小時。 如果您不想等候標準排程的位置要求，您可以在電腦上重新啟動 SMS Agent Host 服務 (ccmexec.exe) 來強制執行要求。

用戶端取得雲端 Proxy 服務的新位置資訊之後，請嘗試檢查內部私人網路上不再存在但可存取網際網路之用戶端的狀態。 您也可以監視雲端 Proxy 服務上的流量，請移至 [管理] > [雲端服務] > [雲端 Proxy 服務]  ，選取清單窗格中的服務，然後檢視詳細資料窗格中的流量資訊。   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>在 Configuration Manager 中管理 Office 365 用戶端代理程式  

從 Technical Preview 1606 開始，您可以使用 Configuration Manager 用戶端代理程式設定 (而不是群組原則)，讓 Office 365 用戶端從 Configuration Manager 接收更新。 在設定這項設定並部署 Office 365 更新之後，Configuration Manager 用戶端代理程式會與 Office 365 用戶端代理程式進行通訊，從發佈點下載 Office 365 更新並安裝它們。 Configuration Manager 也採用用戶端代理程式設定的清查。

如需詳細資訊，請參閱 [Manage Office 365 ProPlus updates](https://technet.microsoft.com/library/mt741983.aspx)(管理 Office 365 ProPlus 更新)。

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>設定 Configuration Manager 用戶端設定來管理 Office 365 用戶端代理程式
1.  在 Configuration Manager 主控台中，按一下 [管理]   > [概觀]   > [用戶端設定]  。
2. 開啟適當的裝置設定，以啟用用戶端代理程式。 如需預設和自訂的用戶端設定詳細資訊，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。
3. 按一下 [軟體更新]  ，然後針對 [啟用管理 Office 365 用戶端代理程式]  設定選取 [是]  。  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter 工作順序變數已被取代
OSDPreserveDriveLetter 工作順序變數決定工作順序將作業系統映像套用至目的地電腦時，是否要使用該映像 WIM 檔中所擷取的磁碟機代號。
- 此工作順序變數在 Technical Preview 1606 中已被取代。

在作業系統部署期間，Windows 安裝程式現在預設會決定要使用的最佳磁碟機代號 (通常是 C:)。 如果您想要指定使用不同的磁碟機，您可以在「套用作業系統」工作順序步驟中變更位置。 移至 [請選取要套用此作業系統的位置]  設定，選取 [特定邏輯磁碟機代號]  ，然後選擇您想要使用的磁碟機。 目的地電腦上必須有指派您所選擇之代號的磁碟機。 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>更新和服務節點有所變更
在 Technical Preview 1606 中，引進了適用於 Configuration Manager 主控台之 [更新與服務] 的數項變更：
- **節點名稱變更：**

    在 [監視]  工作區中，[Site Servicing status]\(站台服務狀態)  節點已重新命名為 [更新與服務狀態]  。
- **更多安裝狀態：**

    當您檢視站台的更新安裝狀態時，主控台現在會分開顯示下列動作的詳細資料：
    - **下載** (僅適用於服務連接點站台系統角色安裝所在的頂層站台)
    - **複寫**
    - **必要條件檢查**
    - **安裝**

  此外，現在各步驟都有更詳細的資訊，包括在哪一個記錄檔中可以檢視詳細資訊。  
-   **新增在先決條件失敗時重試的選項︰**

    在 [管理]  和 [監視]  工作區的 [更新與服務]  節點，其功能區上皆包含名為 [忽略先決條件警告]  的新按鈕。

    當您從 [更新精靈] 安裝更新時未使用 [忽略先決條件警告] 的選項，但該更新安裝突然停止並處於**先決條件警告**的狀態中，您可以選取功能區上的 [忽略先決條件警告]  ，觸發自動接續安裝要忽略先決條件警告的這項更新。  



- **更整潔的更新檢視畫面：**

    當您檢視 [更新與服務]  節點時，您現在只會看到最近安裝的更新，以及可供安裝之任何新的更新。 若要檢視先前安裝的更新，請按一下功能區顯示的新 [歷程記錄]  按鈕。  

-   **進入生產階段前已重新命名的選項︰**

    在 [更新與服務] 節點中，原稱為 [用戶端選項]  的按鈕現在已重新命名為 [將生產階段前用戶端升階]  。
