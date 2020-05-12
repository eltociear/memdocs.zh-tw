---
title: 核准應用程式
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的應用程式核准設定和行為。
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f725c1b7dc380a84cd94e666b98dbd309df3744c
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802050"
---
# <a name="approve-applications-in-configuration-manager"></a>Configuration Manager 的應用程式核准

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 中[部署應用程式](deploy-applications.md)時，您可以要求先核准再安裝。 使用者在軟體中心要求應用程式，然後您在 Configuration Manager 主控台中檢閱要求。 您可以核准或拒絕要求。

## <a name="approval-settings"></a><a name="bkmk_approval"></a> 核准設定

應用程式核准行為取決於您是否啟用建議的[選擇性應用程式核准體驗](#bkmk_opt)。 下列核准設定之一會出現在應用程式部署的 [部署設定]  頁面：  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a>系統管理員必須在裝置上核准此應用程式要求

> [!Note]  
> 根據預設，Configuration Manager 不會啟用此功能。 使用該功能之前，請先啟用 [依據裝置為使用者核准應用程式要求]  選用功能。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。
>
> 如果您未啟用此功能，就會看到[先前的體驗](#bkmk_prior)。  

系統管理員須先核准使用者的應用程式要求，使用者才可以在所要求的裝置上安裝應用程式。 如果系統管理員核准要求，使用者就只能在該裝置上安裝應用程式。 使用者必須提交其他要求，才能在其他裝置上安裝應用程式。 當部署目的為 [必要]  ，或是將應用程式部署至裝置集合時，無法使用此選項。 <!--1357015-->  

> [!Note]  
> 若要利用 Configuration Manager 的新功能，請先將用戶端更新為最新版本。 雖然當您更新主控台和站台時，Configuration Manager 主控台中會出現新功能，但要等到用戶端版本也是最新版，才能完整運作。<!--SCCMDocs issue 646-->  

在 Configuration Manager 主控台的 [軟體程式庫]  工作區中，檢視 [應用程式管理]  下的 [應用程式邀求]  。 (在 1902 版和更早版本中，此節點稱為**核准要求**。)目前在適用於每個要求的清單中都會有一個 [裝置]  資料行。 當您針對要求採取動作時，[應用程式要求] 對話方塊也會包含使用者從中提交要求的裝置名稱。

30 天內若未核准要求，即予以移除。 重新安裝用戶端可能會取消所有擱置中的核准要求。  

當您需要對於部署至裝置集合的核准時，應用程式不會顯示在軟體中心中。 如果您需要對於部署至使用者集合的核准，應用程式會顯示在軟體中心中。 您仍然可以使用用戶端設定，**在軟體中心中隱藏未核准的應用程式**，對使用者隱藏。 如需詳細資訊，請參閱[軟體中心用戶端設定](../../core/clients/deploy/about-client-settings.md#software-center)。

在您核准應用程式以供安裝之後，仍然可以在 Configuration Manager 主控台中 [拒絕]  該要求。 如果使用者尚未安裝應用程式，此動作會阻止其從軟體中心安裝新的應用程式複本。 如果先前已核准並安裝應用程式，則當您**拒絕**應用程式的要求時，用戶端會從使用者的裝置解除安裝該應用程式。<!--1357891-->

從 1906 版開始，如果您在主控台中核准應用程式要求，隨即拒絕該要求，您現在可以再次核准。 在您核准之後，應用程式會重新安裝於用戶端。  <!-- 4224910 -->

使用 [Approve-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) PowerShell Cmdlet 將核准程序自動化。 從 1902 版開始，此 Cmdlet 會包含 **InstallActionBehavior** 參數。 使用此參數可指定是要立即安裝還是在非上班時間安裝應用程式。<!-- SCCMDocs-pr issue #3418 -->

從 1906 開始，您可以查看哪些部署需要核准。 在 [應用程式]  節點中選取應用程式。 在詳細資料窗格中，切換至 [部署]  索引標籤。預設會顯示新的資料行，**需要核准**。

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a> 重試安裝預先核准的應用程式

<!--4336307-->
從 1906 版開始，您可以重試安裝您先前為使用者或裝置核准的應用程式。 核准選項僅適用於可用的部署。 若使用者解除安裝應用程式，或是初始安裝流程失敗，Configuration Manager 不會重新評估其狀態，也不會重新安裝它。 這項功能可讓支援技術人員為請求協助的使用者快速重試應用程式安裝。

1. 以具有應用程式物件**核准**權限的使用者身分，開啟 Configuration Manager 主控台。 例如，**應用程式系統管理員**或**應用程式作者**便具備此權限。

1. 部署需要核准的應用程式，並核准它。

    > [!Tip]  
    > 或者，[為裝置安裝應用程式](install-app-for-device.md)。 它會在裝置上為應用程式建立核准要求。  

如果應用程式未成功安裝，或使用者解除安裝應用程式，請使用下列程序來重試：

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [應用程式管理]  ，然後選取 [應用程式要求]  節點。 (在 1902 版和更早版本中，此節點稱為**核准要求**。)

1. 選取先前已核准的應用程式。 在功能區的 [核准要求] 群組中，選取 [重試安裝]  。

#### <a name="other-app-approval-resources"></a>其他應用程式核准資源

- [Application approval improvements in ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534) (ConfigMgr 1810 的應用程式核准增強功能)
- [Updates to the application approval process in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048) (Configuration Manager 中的應用程式核准程序更新)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a>如果使用者要求此應用程式，則需要經系統管理員核准

> [!Note]  
> 如果您未啟用建議的[選擇性應用程式核准體驗](#bkmk_opt)，則適用此體驗。

系統管理員須先核准使用者的應用程式要求，使用者才可以安裝應用程式。 當部署目的為 [必要]  ，或是將應用程式部署至裝置集合時，無法使用此選項。  

應用程式核准要求會顯示在 [軟體程式庫]  工作區中 [應用程式管理]  下方的 [應用程式要求]  節點中。 (在 1902 版和更早版本中，此節點稱為**核准要求**。)30 天內若未核准要求，即予以移除。 重新安裝用戶端可能會取消所有擱置中的核准要求。  

在您核准應用程式以供安裝之後，仍然可以在 Configuration Manager 主控台中 [拒絕]  該要求。 這個動作並不會造成用戶端解除安裝任何裝置上的應用程式。 它會防止使用者從軟體中心安裝新的應用程式複本。  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a> 電子郵件通知

<!--1321550-->

您可以設定應用程式核准要求的電子郵件通知。 當使用者要求應用程式時，您會收到一封電子郵件。 按一下電子郵件中的連結來核准或拒絕要求，而不需使用 Configuration Manager 主控台。

您可以在建立應用程式的新部署時，針對可核准或拒絕要求的使用者定義其電子郵件地址。 如果您之後需要變更電子郵件地址的清單，請移至 [監視]  工作區，展開 [警示]  ，然後選取 [訂用帳戶]  節點。 請從其中一個與應用程式部署相關的 [透過電子郵件核准應用程式]  訂用帳戶選取 [內容]  。

如果有多個警示，您可以判斷哪個警示要搭配哪個部署。 請開啟警示內容，並檢視 [一般] 索引標籤上的 [選取的警示]  清單。即會針對此訂用帳戶以該警示啟用部署。

使用者可以從軟體中心將註解新增至要求。 此註解會在 Configuration Manager 主控台的應用程式要求中顯示。 從 1902 版開始，該註解也會顯示於電子郵件中。 將此註解包含在電子郵件中，有助於核准者針對核准或拒絕要求，做出更佳的決策。<!--3594063-->

### <a name="prerequisites"></a>先決條件

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>傳送電子郵件通知，並在內部網路上採取動作

在這些先決條件下，收件者會收到一封附有要求通知的電子郵件。 如果他們位於內部網路，也可以在電子郵件中核准或拒絕要求。

- 啟用 [依據裝置為使用者核准應用程式要求]  [選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。  

- 設定[警示的電子郵件通知](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)。  

    > [!NOTE]
    > 部署應用程式的系統管理使用者需要建立警示與訂用帳戶的權限。 如果此使用者沒有這些權限，其會在 [部署軟體精靈]  的結尾看到錯誤：「您沒有執行此操作所需的安全性權限。」<!-- 2810283 -->

- 在主要站台上啟用 SMS 提供者以使用憑證。<!--SCCMDocs-pr issue 3135--> 使用下列其中一個選項：  

  - (建議) 為主要站台啟用[增強式 HTTP](../../core/plan-design/hierarchy/enhanced-http.md)。

    > [!Note]  
    > 當主要站台建立 SMS 提供者的憑證時，用戶端上的網頁瀏覽器不會信任該憑證。 回應應用程式要求時，根據您的安全性設定，您可能會看到安全性警告。  

  - 在 IIS 中手動將 PKI 型憑證繫結至裝載主要站台上 SMS 提供者角色的伺服器連接埠 443。

> [!NOTE]
> 如果您在階層中有多個子主要站台，請針對要啟用此功能的每個主要站台設定這些先決條件。 電子郵件通知中的連結適用於主要站台上的系統管理服務。<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>從網際網路採取動作

在這些額外的選擇性先決條件下，收件者可以從能連線到網際網路的任何位置，核准或拒絕要求。

- 透過雲端管理閘道啟用 SMS 提供者管理服務。 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，並展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。 選取有 SMS 提供者角色的伺服器。 在 [詳細資料] 窗格中，選取 [SMS 提供者]  角色，然後在 [站台角色] 索引標籤的功能區中選取 [內容]  。選取 [允許系統管理服務的 Configuration Manager 雲端管理閘道流量]  選項。  

- SMS 提供者需要 **.NET 4.5.2** 或更新版本。  

- 設定[雲端管理閘道](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)。

- 將該站台上線至 [Azure 服務](../../core/servers/deploy/configure/azure-services-wizard.md)以進行**雲端管理**。

- 啟用 [Azure AD 使用者探索](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)。

- 以手動方式設定 Azure AD 中的設定：  

    1. 以具有*全域管理員*權限的使用者身分移至 [Azure 入口網站](https://portal.azure.com)。 移至 [Azure Active Directory]  ，然後選取 [應用程式註冊]  。  

    1. 選取您為 Configuration Manager **雲端管理**整合所建立的類型應用程式。  

    1. 在 [管理]  功能表中，選取 [驗證]  。  

        1. 在 [重新導向 URI]  區塊中，貼上以下路徑：`https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. 使用您雲端管理閘道 (CMG) 服務的完整網域名稱 (FQDN)，取代 `<CMG FQDN>`。 例如 GraniteFalls.Contoso.com。  

        1. 然後選取 [儲存]  。  

    1. 在 [管理]  功能表中，選取 [資訊清單]  。  

        1. 在 [編輯資訊清單] 窗格中，尋找 **oauth2AllowImplicitFlow** 屬性。  

        1. 將值變更為 **true**。 例如，整行看起來應該像下面這一行：`"oauth2AllowImplicitFlow": true,`  

        1. 選取 [儲存]  。  

### <a name="configure-email-approval"></a>設定電子郵件核准

1. 在 Configuration Manager 主控台中，[部署應用程式](deploy-applications.md)供使用者集合使用。 在 [部署設定]  頁面上，啟用它以進行核准。 然後，輸入一或多個電子郵件地址來接收通知。 使用分號分隔電子郵件地址 (`;`)。  

     > [!Note]  
     > 您 Azure AD 組織中任何收到此電子郵件的人員都可核准要求。 不要將電子郵件轉寄給其他人，除非您想要他們採取動作。  

2. 以使用者身分，在軟體中心要求應用程式。  

3. 您會在五分鐘內收到電子郵件通知。 電子郵件的內容類似下列範例：  

![用於核准應用程式的範例電子郵件通知](media/1321550-email.png)

> [!Note]  
> 核准或拒絕的連結僅供單次使用。 例如，您可以設定群組別名來接收通知。 Meg 會核准要求。 現在 Bruce 無法拒絕要求。  

檢閱站台伺服器上的 **NotiCtrl.log** 檔案進行疑難排解。

## <a name="maintenance"></a>維護

Configuration Manager 會將應用程式核准要求的相關資訊儲存在站台資料庫中。 若為取消或拒絕的要求，站台會在 30 天後刪除此類要求歷程記錄。 您可以使用 [刪除過時應用程式要求資料]  的[站台維護工作](../../core/servers/manage/maintenance-tasks.md)來設定此刪除行為。 站台永遠不會刪除任何已核准或暫止的應用程式要求。
