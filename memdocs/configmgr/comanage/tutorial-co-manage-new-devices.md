---
title: 教學課程：啟用網際網路裝置的共同管理
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 和 Microsoft Intune 設定新網際網路型 Windows 10 裝置的共同管理。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/12/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 75016e8028dde29c83ae7e7f5a23a1f6dbb4417f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692986"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>教學課程：為新的網際網路型裝置啟用共同管理

藉由共同管理，您將可保有已妥善建立的程序，以使用 Configuration Manager 來管理您組織中的電腦。 同時，您也將透過使用 Intune 投資雲端來進行安全性和現代化佈建。

在此教學課程中，您會在同時使用 Azure Active Directory (AD) 和內部部署 AD 但沒有[混合式 Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD) 的環境中，設定 Windows 10 裝置的共同管理。 Configuration Manager 環境包括一個所有站台系統角色都位於相同伺服器 (站台伺服器) 上的主要站台。 此教學課程一開始的前題是您的 Windows 10 裝置已經向 Intune 註冊。 

如果您具有將內部部署 AD 與 Azure AD 聯結的混合式 Azure AD，建議您依照我們的隨附教學課程[為 Configuration Manager 用戶端啟用共同管理](tutorial-co-manage-clients.md)進行操作。

在下列情況下，請使用此教學課程：
  
- 您有要進行共同管理的 Windows 10 裝置。 這些裝置可能是已透過 Windows Autopilot 佈建的，或直接來自您的硬體 OEM。
- 您在網際網路上有目前以 Intune 管理的 Windows 10 裝置，而您想要將 Configuration Manager 用戶端新增至這些裝置。

**在此教學課程中，您將：**  
> [!div class="checklist"]  
> * 檢閱 Azure 和您內部部署環境的先決條件
> * 為雲端管理閘道 (CMG) 要求公用 SSL 憑證
> * 在 Configuration Manager 中啟用 Azure 服務
> * 部署及設定雲端管理閘道  
> * 設定管理點和用戶端以使用 CMG
> * 在 Configuration Manager 中啟用共同管理
> * 設定 Intune 以安裝 Configuration Manager 用戶端

## <a name="prerequisites"></a>先決條件  

### <a name="azure-services-and-environment"></a>Azure 服務和環境

- Azure 訂用帳戶 ([免費試用](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune 訂閱
  > [!TIP]  
  > Enterprise Mobility + Security (EMS) 訂用帳戶同時包括 Azure Active Directory Premium 和 Microsoft Intune。 EMS 訂用帳戶 ([免費試用](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))。  

- Intune 已設定為會[自動註冊裝置](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  

> [!TIP]
> 您不再需要購買並指派個別的 Intune 或 EMS 授權給使用者。 如需詳細資訊，請參閱[產品與授權常見問題集](../core/understand/product-and-licensing-faq.md#bkmk_mem)。

### <a name="on-premises-infrastructure"></a>內部部署基礎結構

- Configuration Manager 最新分支 1810 版或更新版本。
  
  1810 版導入了[增強型 HTTP](../core/plan-design/hierarchy/enhanced-http.md)，這在此課程中用來簡化 PKI 需求。 透過使用「增強型 HTTP」，您用來管理用戶端的主要站台必須設定為對 HTTP 站台系統使用 Configuration Manager 產生的憑證。  

  1810 版也針對 Configuration Manager 用戶端的網際網路型安裝導入了更簡單的命令列。

- MDM 授權單位必須設定為 Intune  

### <a name="external-certificates"></a>外部憑證

- CMG 伺服器驗證憑證。 此憑證是來自公用且全球受信任之憑證提供者的 SSL 憑證。 例如 (但不限於)，DigiCert、Thawte 或 VeriSign。 您將把此憑證與私密金鑰一起匯出成 .PFX 檔案。  

- 稍後在此教學課程中，我們會提供有關如何設定此憑證之要求的指引。

### <a name="permissions"></a>權限

在此教學課程的整個過程中，請使用下列權限來完成工作：

- 屬於 Azure Active Directory (Azure AD)「全域管理員」  的帳戶
- 在您內部部署基礎結構上為「網域管理員」  的帳戶  
- 在 Configuration Manager 中為「所有」  範圍之「系統高權限管理員」  的帳戶

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>為雲端管理閘道要求公用憑證

當裝置位於網際網路上時，必須要有 Configuration Manager 雲端管理閘道 (CMG)，才能進行共同管理。 CMG 可讓您的網際網路型 Windows 10 裝置與內部部署的 Configuration Manager 部署進行通訊。 為了在裝置與您的 Configuration Manager 環境之間建立信任，CMG 必須要有 SSL 憑證。

此教學課程會使用一個稱為 **CMG 伺服器驗證憑證**的公用憑證，此憑證會從全球信任的憑證提供者取得授權。 雖然您可以使用從內部部署 Microsoft 憑證授權單位取得授權的憑證來設定共同管理，但使用自我簽署憑證已超出此教學課程的範圍。

**CMG 伺服器驗證憑證**可用來加密 Configuration Manager 用戶端與 CMG 之間的通訊流量。 此憑證會往回追蹤至「可信任的根」以向用戶端確認伺服器的身分識別。 公用憑證包含 Windows 用戶端已經信任的「可信任的根」。

關於此憑證： 

- 您需在 Azure 中識別您 CMG 服務的唯一名稱，然後在憑證要求中指定該名稱。  
- 您需在特定伺服器上產生憑證要求，然後將該要求提交給公用憑證提供者以取得必要的 SSL 憑證。  
- 您需將您從提供者收到傳回的憑證匯入至產生該要求的系統。 稍後將 CMG 部署至 Azure 時，您需使用相同的電腦來匯出憑證以供使用。  
- 當 CMG 進行安裝時，它會使用您在憑證中指定的名稱，在 Azure 中建立 CMG 服務。  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>在 Azure 中識別您雲端管理閘道的唯一名稱

當您要求 CMG 伺服器驗證憑證時，需指定必須要有什麼唯一名稱，才能在 Azure 中識別您的「雲端服務 (傳統)」  。 Azure 公用雲端預設會使用 *cloudapp.net*，而 CMG 則以 *\<YourUniqueDnsName>.cloudapp.net* 的形式裝載於 cloudapp.net 網域內。  

> [!TIP]  
> 在此教學課程中，**CMG 伺服器驗證憑證**會使用結尾為 *contoso.com* 的 FQDN。  在建立 CMG 之後，我們將會在組織的公用 DNS 中設定正式名稱記錄 (CNAME)。 此記錄會為 CMG 建立一個與我們在公用憑證中所用名稱對應的別名。  

在您要求公用憑證之前，請確認您想要使用的名稱在 Azure 中可供使用。 您並不會直接在 Azure 中建立服務。 取而代之的是，當您安裝 CMG 時，Configuration Manager 會使用您所要求之公用憑證中指定的名稱來建立雲端服務。  

1. 登入 [Microsoft Azure 入口網站](https://portal.azure.com/)。  

2. 選取 [建立資源]  ，選擇 [計算]  類別，然後選取 [雲端服務]  。 [雲端服務 (傳統)] 頁面隨即開啟。

3. 針對 [DNS 名稱]  ，指定您將使用之雲端服務的首碼名稱。 此首碼必須與您稍後為 CMG 伺服器驗證憑證要求發佈憑證時所用的首碼相同。 我們會使用 *MyCSG*，這會建立 *MyCSG.cloudapp.net* 命名空間。 介面會確認該名稱可供使用，還是已經被另一個服務使用。  
 在您確認想要使用的名稱可供使用之後，即可提交「憑證簽署要求」(CSR)。

### <a name="request-the-certificate"></a>要求憑證

請使用下列資訊，向公用憑證提供者提交 CMG 的憑證簽署要求。 將下列值變更成與您環境相關的值。  

- 變更 *MyCMG* 以識別雲端管理閘道的服務名稱
- 將 *Contoso* 變更成公司名稱
- 將 *Contoso.com* 變更成公用網域

建議您使用主要站台伺服器來產生憑證簽署要求 (CSR)。 當您取得憑證時，必須在產生 CSR 的相同伺服器上註冊該憑證，否則便無法匯出必要的憑證私密金鑰。  

產生 CSR 時，請要求第 2 版金鑰提供者類型。 僅支援第 2 版憑證。  

> [!TIP]  
> 部署 CMG 時，將同時也安裝雲端發佈點 (CDP)。 部署 CMG 時，預設會選取 [允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容]  選項。 如果將 CDP 與 CMG 共置於伺服器上，則無需另外的憑證和設定，即可支援 CDP。 雖然不需要 CDP 即可使用共同管理，但其在大多數環境中都相當有用。  
>
> 如果您將針對共同管理使用額外的雲端發佈點，則必須為每部額外的伺服器要求個別的憑證。 若要為 CDP 要求公開憑證，請使用與雲端管理閘道 CSR 相同的詳細資料。 您只需要變更一般名稱，使每個 CDP 的一般名稱都是唯一名稱即可。  

#### <a name="details-for-the-cloud-management-gateway-csr"></a>雲端管理閘道 CSR 的詳細資料

- **一般名稱**：CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
範例：MyCSG.contoso.com  
- **主體別名**：與一般名稱 (CN) 相同  
- **組織**：您組織的名稱  
- **部門**：依據您的組織  
- **縣市**：依據您的組織  
- **狀態**：依據您的組織  
- **國家/地區**：依據您的組織  
- **金鑰大小：2048**  
- **提供者：Microsoft RSA SChannel 密碼編譯提供者**  

### <a name="import-the-certificate"></a>匯入憑證

在您收到公用憑證之後，請將其匯入至建立 CSR 之電腦的本機憑證存放區。 然後將憑證匯出成 .PFX 檔案，以便在 Azure 中用於您的 CMG。  

公用憑證提供者通常會提供匯入憑證的指示。 匯入憑證的程序應該與以下指引類似：  

1. 在要匯入憑證的電腦上，找出 .pfx 憑證檔案。  

2. 在該檔案上按一下滑鼠右鍵，然後選取 [安裝 PFX]   

3. 當 [憑證匯入精靈] 啟動時，選取 [下一步]  。  

4. 在 [要匯入的檔案]  頁面上，選取 [下一步]  。

5. 在 [密碼]  頁面上，於 [密碼] 方塊中輸入私密金鑰的密碼，然後選取 [下一步]  。  
  
   選取將金鑰設定為可匯出的選項。

6. 在 [憑證存放區]  頁面上，選擇 [自動根據憑證類型來選取憑證存放區]  ，然後選取 [下一步]  。  

7. 選取 [完成]  。

### <a name="export-the-certificate"></a>匯出憑證

從您的伺服器匯出「CMG 伺服器驗證憑證」  。 重新匯出憑證會讓該憑證在 Azure 中可供您的雲端管理閘道使用。  

1. 在您匯入公用 SSL 憑證的伺服器上，執行 **certlm.msc** 以開啟 [憑證管理員] 主控台。  

2. 在 [憑證管理員] 主控台中，選取 [個人] > [憑證]  。 接著，在您於先前程序中註冊的「CMG 伺服器驗證憑證」  上按一下滑鼠右鍵，然後選取 [所有工作] > [匯出]  。  

3. 在 [憑證匯出精靈] 中，依序選取 [下一步]  、[是，匯出私密金鑰]  及 [下一步]  。  

4. 在 [匯出檔案格式] 頁面上，依序選取 [個人資訊交換 – PKCS #12 (.PFX)]  和 [下一步]  ，然後提供密碼。 針對檔案名稱，指定一個類似 **C:\ConfigMgrCloudMGServer** 的名稱。 當您在 Azure 中建立 CMG 時，將會參考此檔案。  

5. 選取 [下一步]  ，然後先確認下列設定，再選取 [完成]  來完成匯出：  

   - 匯出金鑰 = 是  
   - 包含憑證路徑中的所有憑證 = 是  
   - 檔案格式 = 個人資訊交換 (*.pfx)  

6. 完成匯出之後，找出 .pfx 檔案，並將其複本放在將管理網際網路型用戶端之 Configuration Manager 主要站台伺服器上的 **C:\Certs** 中。 [Certs] 資料夾是在伺服器之間移動憑證時要使用的暫時資料夾。 將雲端管理閘道部署至 Azure 時，您會從主要站台伺服器存取憑證檔案。  

將憑證複製到主要站台伺服器之後，您便可以從成員伺服器的「個人憑證」存放區中刪除該憑證。

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>在 Configuration Manager 中啟用 Azure 雲端服務

若要從 Configuration Manager 主控台內設定 Azure 服務，您需使用 [設定 Azure 服務] 精靈，然後建立兩個 Azure Active Directory (Azure AD) 應用程式。  

- **伺服器應用程式** – Azure AD 中的「Web 應用程式」   
- **用戶端應用程式** – Azure AD 中的「原生用戶端」  應用程式  

請從主要站台伺服器執行下列程序。  

1. 從主要站台伺服器中，開啟 Configuration Manager 主控台並移至 [系統管理] > [雲端服務] > [Azure 服務]  ，然後選取 [設定 Azure 服務]  。  

   在 [設定 Azure 服務] 頁面上，為您要設定的雲端管理服務指定易記名稱。 例如：我的雲端管理服務  。

   然後依序選取 [雲端管理]  和 [下一步]  。  

   > [!TIP]  
   > 如需有關您在精靈中所做設定的詳細資訊，請參閱[啟動 Azure 服務精靈](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard)

2. 在 [應用程式屬性]  頁面上，針對 [Web 應用程式]  ，選取 [瀏覽]  以開啟 [伺服器應用程式]  對話方塊，然後選取 [建立]  。 設定下列欄位：

   - **應用程式名稱**：為應用程式指定一個易記名稱，例如「雲端管理 Web 應用程式」  。  

   - **首頁 URL**：Configuration Manager 並不使用此值，但卻是 Azure AD 的必要值。 根據預設，此值為 `https://ConfigMgrService`。  

   - **App 識別碼 URI**：這在 Azure AD 租用戶中必須是唯一的值。 它是在存取權杖中，由 Configuration Manager 用戶端用來要求存取該服務。 根據預設，此值為 `https://ConfigMgrService`。  

   接著，選取 [登入]  ，然後指定「Azure AD 全域管理員」帳戶。 Configuration Manager 不會儲存這些認證。 此角色不需要在 Configuration Manager 中具有權限，也不需要是執行「Azure 服務精靈」的相同帳戶。

   在您登入之後，就會顯示結果。 選取 [確定]  以關閉 [建立伺服器應用程式] 對話方塊，並返回 [應用程式屬性] 頁面。

3. 針對 [原生用戶端應用程式]  ，選取 [瀏覽]  以開啟 [用戶端應用程式]  對話方塊。

4. 選取 [建立]  以開啟 [建立用戶端應用程式] 對話方塊  ，然後設定下列欄位：  

   - **應用程式名稱**：為應用程式指定一個易記名稱，例如「雲端管理原生用戶端應用程式」  。

   - **回覆 URL**：Configuration Manager 不使用此值，但卻是 Azure AD 的必要值。 根據預設，此值為 `https://ConfigMgrClient`。
   接著，選取 [登入]  ，然後指定「Azure AD 全域管理員」帳戶。 就像 Web 應用程式一樣，這些認證並不會儲存，也不需要在 Configuration Manager 中具有權限。

   在您登入之後，就會顯示結果。 選取 [確定]  以關閉 [建立用戶端應用程式] 對話方塊，並返回 [應用程式屬性] 頁面。 接著，選取 [下一步]  以繼續進行操作。

5. 在 [設定探索設定]  頁面上，選取 [啟用 Azure Active Directory 使用者探索]  的方塊、選取 [下一步]  ，然後完成您環境的「探索」對話方塊設定。  

6. 繼續完成 [摘要]、[進度] 及 [完成] 頁面，然後關閉精靈。  

   現在已在 Configuration Manager 中啟用「Azure AD 使用者」探索的「Azure 服務」。  目前讓主控台保持開啟。  

7. 開啟瀏覽器並登入 [Azure 入口網站](https://portal.azure.com/)。  

8. 選取 [所有服務] > [Azure Active Directory] > [應用程式註冊]  ，然後：

   1. 選取您建立的 Web 應用程式。

   2. 移至 [設定] > [必要權限]  ，選取 [授與權限]  ，然後選取 [是]  。  

   3. 選取您建立的「原生用戶端」應用程式。

   4. 移至 [設定] > [必要權限]  ，選取 [授與權限]  ，然後選取 [是]  。  

9. 在 Configuration Manager 主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [Azure 服務]  ，然後選取您的「Azure 服務」。 接著，在 [Azure Active Directory 使用者探索]  上按一下滑鼠右鍵，然後選取 [立即執行完整探索]  。 選取 [是]  以確認該動作。  

10. 在主要站台伺服器上，開啟 Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT.log**，然後尋找下列項目以確認該探索能夠運作：「已成功發佈 Azure Active Directory 使用者的 UDX」   

    此記錄檔預設位於 *%Program_Files%\Microsoft Configuration Manager\Logs* 中。  

## <a name="create-the-cloud-services-in-azure"></a>在 Azure 中建立雲端服務

**在此教學課程的這一節中，您將**：

- 建立 CMG 雲端服務  
- 為兩個服務建立 DNS CNAME 記錄  

### <a name="create-the-cmg"></a>建立 CMG

請使用此程序將雲端管理閘道安裝成 Azure 中的服務。 CMG 會在階層的頂層站台進行安裝。 在此教學課程中，我們會繼續使用已註冊並匯出憑證的主要站台。

1. 在主要站台伺服器上，開啟 Configuration Manager 主控台，接著移至 [系統管理] > [概觀] > [雲端服務] > [雲端管理閘道]  ，然後選取 [建立雲端管理閘道]  。  

2. 在 [一般]  頁面上：  

   1. 針對 [Azure 環境]  ，選取您的雲端環境。 此教學課程使用 **AzurePublicCloud**。  

   2. 選取 [Azure Resource Manager 部署]  。  
  
   3. **登入**您的 Azure 訂用帳戶。 Configuration Manager 會根據您為 Configuration Manager 啟用 Azure 雲端服務時所設定的資訊，填入額外的資訊。  

   選取 [下一步]  以繼續進行操作。  

3. 在 [設定]  頁面上，瀏覽並選取名為 **ConfigMgrCloudMGServer.pfx** 的檔案，這是您在匯入 CMG 伺服器驗證憑證之後所匯出的檔案。 在您指定密碼之後，[服務名稱]  和 [部署名稱]  即會根據 .pfx 憑證檔案中的詳細資料自動填入。

4. 設定您的 [區域]  。

5. 針對 [資源群組]  ，使用現有的資源群組，或以不包含任何空格的易記名稱 (例如 **CofigMgrCloudServices**) 建立一個群組。 如果您選擇建立群組，該群組會在 Azure 中新增為資源群組。  

6. 除非您已準備好進行大規模設定，否則請使用一 (1) 作為 [VM 執行個體]  的數目。 VM 執行個體的數目可讓單一「雲端管理閘道」(CMG) 雲端服務向外延展，以支援多個用戶端連線。 稍後，您可以使用 Configuration Manager 主控台來傳回和編輯您使用的 VM 執行個體數目。  

7. 啟用 [驗證用戶端憑證撤銷]  的核取方塊。

8. 如果您想要使用 CMG 來部署雲端發佈點，請啟用 [允許使用 CMG 當作雲端發佈點及處理來自 Azure 儲存體的內容]  的核取方塊。

9. 選取 [下一步]  以繼續進行操作。

10. 檢閱 [警示]  頁面上的值，然後選取 [下一步]  。

11. 檢閱 [摘要]  頁面，然後按 [下一步]  以建立雲端管理閘道雲端服務。 選取 [關閉]  以完成精靈。  

12. 在 Configuration Manager 主控台的 [雲端管理閘道] 節點中，您現在已可檢視該項新服務。  

### <a name="create-dns-cname-records"></a>建立 DNS CNAME 記錄

當您為 CMG 建立 DNS 項目時，會讓您在公司網路內部和外部的 Windows 10 裝置都能夠使用名稱解析在 Azure 中尋找 CMG 雲端服務。

我們 CNAME 記錄範例使用下列詳細資料：  

- 公司名稱為 **Contoso**，其公用 DNS 命名空間為 ***Contoso.com***。  

- CMG 服務名稱為 **MyCMG**，這在 Azure 中會變成 ***MyCMG.CloudApp.Net***。  

CNAME 記錄範例：*MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>設定管理點和用戶端以使用 CMG

設定可讓內部部署管理點和用戶端使用雲端管理閘道的設定。

由於我們使用「增強型 HTTP」來進行用戶端通訊，因此不需要使用 HTTPS 管理點。  

### <a name="create-the-cmg-connection-point"></a>建立 CMG 連接點

設定網站以支援「增強型 HTTP」。  

1. 在 Configuration Manager 主控台中，移至 [系統管理] > [概觀] > [站台設定] > [站台]  ，然後開啟主要站台的屬性。  

2. 在 [用戶端電腦通訊]  索引標籤上，針對 [對 HTTP 站台系統使用 Configuration Manager 產生的憑證]  ，選取 [HTTPS 或 HTTP]  選項，然後選取 [確定]  以儲存設定。

    > [!Note]
    > 從 1906 版開始，此索引標籤稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

3. 現在，移至 [系統管理] > [概觀] > [站台設定] > [伺服器和站台系統角色]  ，然後選取具有您想要安裝雲端管理閘道連接點之管理點的伺服器。  

4. 選取 [新增站台系統角色]  ，然後選取 [下一步]  > [下一步]  。  

5. 選取 [雲端管理閘道連接點]  ，然後選取 [下一步]  以繼續進行操作。  

6. 檢閱 [雲端管理閘道連接點]  頁面上的預設選取項目，並確定已選取正確的 CMG。 如果您有多個雲端管理閘道，則可以使用下拉式清單來指定不同的 CMG。 您也可以在安裝後變更所使用的 CMG。 選取 [下一步]  以繼續進行操作。

7. 選取 [下一步]  以開始安裝，然後在 [完成] 頁面上檢視結果。  選取 [關閉]  以完成連接點的安裝。

8. 現在，移至 [系統管理] > [概觀] > [站台設定] > [伺服器和站台系統角色]  ，然後開啟您安裝連接點之管理點的 [屬性]  。 在 [一般]  索引標籤上，選取 [允許 Configuration Manager 雲端管理閘道流量]  的方塊，然後選取 [確定]  以儲存設定。
   > [!TIP]  
   > 雖然對於啟用共同管理來說並非必要，但建議您對所有軟體更新點都進行這個相同的編輯。

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>設定用戶端設定以指示用戶端使用 CMG

使用 [用戶端設定] 來設定讓 Configuration Manager 用戶端與 CMG 進行通訊。  

1. 開啟 Configuration Manager 主控台 > [系統管理] > [概觀] > [用戶端設定]  ，然後編輯 [預設用戶端設定]  。  

2. 選取 [雲端服務]  。

3. 在 [預設設定]  頁面上，設定下列設定 = [是]  。  

   - **自動向 Azure Active Directory 註冊新加入 Windows 10 網域的裝置**  

   - **讓用戶端使用雲端管理閘道**

   - **允許存取雲端發佈點**

4. 在 [用戶端原則]  頁面上，設定 [從網際網路用戶端啟用使用者原則要求]   = [是]  。

5. 按一下 [確定]  儲存這項設定。

## <a name="enable-co-management-in-configuration-manager"></a>在 Configuration Manager 中啟用共同管理

在備妥 Azure 設定、站台系統角色及用戶端設定之後，您便可以設定 Configuration Manager 來啟用共同管理。 不過，在啟用共同管理之後，於完成此教學課程之前，您仍然需要在 Intune 中進行一些設定。 這些工作其中之一，就是設定 Intune 以部署 Configuration Manager 用戶端。 藉由儲存可從 [Co-management Configuration Wizard] \(共同管理設定精靈\) 內使用的用戶端部署命令列，可讓該工作變得較輕鬆。 這就是為何我們要在此時於完成 Intune 設定之前啟用共同管理的原因。

> [!TIP]
> - 當您啟用共同管理時，將會指派一個集合作為「試驗群組」  。 這是一個包含少量用戶端的群組，以用來測試共同管理設定。 建議您先建立一個適當的集合，再開始進行此程序。 如此一來，您無需結束此程序，即可選取該集合。
> - 從 Configuration Manager 1906 版開始，您可能需要多個集合，因為您可以為每個工作負載指派不同的「試驗群組」  。

### <a name="enable-co-management-starting-in-version-1906"></a>從 1906 版開始啟用共同管理

若要從 Configuration Manager 1906 版開始啟用共同管理，請遵循下列指示：

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>在 1902 版和更早版本中啟用共同管理

若要針對 Configuration Manager 1902 版和更早版本啟用共同管理，請遵循下列指示：

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>使用 Intune 來部署 Configuration Manager 用戶端

您可以使用 Intune 將 Configuration Manager 用戶端安裝在目前僅以 Intune 管理的 Windows 10 裝置上。  

然後，當先前非受控的 Windows 10 裝置向 Intune 註冊時，它就會自動安裝 Configuration Manager 用戶端。

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>建立 Intune 應用程式以安裝 Configuration Manager 用戶端

1. 從主要站台伺服器中，登入 [Azure 入口網站](https://portal.azure.com/)，然後移至 [Intune] > [用戶端應用程式] > [應用程式] > [新增]  。

2. 針對 [應用程式類型]  ：選取 [企業營運應用程式]  。

3. 選取 [應用程式套件檔案]  ，接著瀏覽至 Configuration Manager 檔案 **ccmsetup.msi** 的位置，然後選取 [開啟] > [確定]  。
例如 *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*

4. 選取 [應用程式資訊]  ，然後指定下列詳細資料：
   - **描述**：Configuration Manager 用戶端  

   - **發行者**：Microsoft  

   - **命令列引數**： *\<指定 **CCMSETUPCMD** 命令列。您可以從 [Co-management Configuration Wizard] \(共同管理設定精靈\) 的 [Enablement] \(啟用\)* *頁面使用已儲存的命令列。此命令列包含您的雲端服務名稱，以及可讓裝置安裝 Configuration Manager 用戶端軟體的額外值。*  

     命令列結構應該與這個僅使用 CCMSETUPCMD 和 SMSSiteCode 參數的範例類似：  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > 如果您沒有可用的命令列，您可以在 Configuration Manager 主控台中檢視 *CoMgmtSettingsProd* 的屬性來取得此命令列的複本。

5. 選取 [確定] > [新增]  。  應用程式便會隨即建立，並在 Intune 主控台中變成可供使用。 在應用程式可供使用之後，您即可使用下一節來設定 Intune 以將其指派給 Windows 10 裝置。

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>指派 Intune 應用程式以安裝 Configuration Manager 用戶端

下列程序會部署應用程式來安裝您在先前程序中建立的 Configuration Manager 用戶端。

1. 登入 [Azure 入口網站](https://portal.azure.com/)。  選取 [所有服務] > [Intune] > [用戶端應用程式] > [應用程式]  ，然後選取 [ConfigMgr Client Setup Bootstrap] \(ConfigMgr 用戶端安裝程式啟動程序\)  ，這是您所建立用來部署 Configuration Manager 用戶端的應用程式。  

2. 選取 [指派] > [加入群組]  。  將 [指派類型]  設定為 [必要]  ，然後使用 [包含的群組]  和 [排除的群組]  來設定含有要參與共同管理之使用者和裝置的 Azure Active Directory (AD) 群組。  

3. 依序選取 [確定]  和 [儲存]  來儲存設定。
該應用程式現在已成為作為您指派對象之使用者和裝置的必要應用程式。 在應用程式將 Configuration Manager 用戶端安裝在裝置上之後，便可對該裝置進行共同管理。

## <a name="summary"></a>[摘要]

完成本教學課程的設定步驟之後，您就可以開始進行裝置的共同管理。

## <a name="next-steps"></a>後續步驟

- 使用[共同管理儀表板](how-to-monitor.md)來檢閱共同管理裝置的狀態
- 使用 [Windows Autopilot](quickstart-autopilot.md) 來佈建新裝置
- 使用[條件式存取](quickstart-conditional-access.md)和 Intune 合規性規則來管理使用者對公司資源的存取
