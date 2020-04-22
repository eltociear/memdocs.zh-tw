---
title: 設定 Azure 服務
titleSuffix: Configuration Manager
description: 將 Configuration Manager 環境與 Azure 服務連線，以提供雲端管理、商務用 Microsoft Store 及 Log Analytics。
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3a4dee8af68fec8c08cc58b02520f53e13adfbb3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704886"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>設定要與 Configuration Manager 搭配使用的 Azure 服務

適用於：  Configuration Manager (最新分支)

使用 **Azure 服務精靈**以簡化與 Configuration Manager 一起使用的 Azure 雲端服務設定程序。 此精靈透過使用 Azure Active Directory (Azure AD) Web 應用程式註冊來提供通用的設定體驗。 這些應用程式提供訂用帳戶和設定詳細資料，並驗證與 Azure AD 的通訊。 每次您使用 Azure 設定新的 Configuration Manager 元件或服務時，應用程式會替換輸入這筆相同資訊。


## <a name="available-services"></a>可用的服務

使用此精靈設定下列 Azure 服務：  

- **雲端管理**：此服務可讓站台與用戶端使用 Azure AD 進行驗證。 此驗證可啟用其他案例，例如：  

    - [安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證](../../../clients/deploy/deploy-clients-cmg-azure.md)  

    - [設定 Azure AD 使用者探索](configure-discovery-methods.md#azureaadisc)  

    - [設定 Azure AD 使用者群組探索](configure-discovery-methods.md#bkmk_azuregroupdisco)

    - 支援某些[雲端管理閘道案例](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

    - [應用程式核准電子郵件通知](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics 連接器**：[連線到 Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)。 將集合資料同步處理到 Log Analytics。  

    > [!Note]  
    > 本文指的是先前稱為「OMS 連接器」  的「Log Analytics 連接器」  。 功能上沒有任何差異。 如需詳細資訊，請參閱 [Azure 管理 - 監視](https://docs.microsoft.com/azure/azure-monitor/terminology#log-analytics)。  

- **商務用 Microsoft Store**：連線到[商務用 Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。 為您的組織取得可以使用 Configuration Manager 部署的市集應用程式。  

### <a name="service-details"></a>服務詳細資料

下表列出每個服務的相關詳細資料。  

- **租用戶**：您可以設定的服務執行個體數目。 每個執行個體都必須是不同的 Azure 租用戶。  

- **雲端**：所有服務都支援全域 Azure 雲端，但並非所有服務都支援私人雲端，例如 Azure 美國政府雲端。  

- **Web 應用程式**：服務是否使用「Web 應用程式 / API」  類型的 Azure AD 應用程式，也稱為 Configuration Manager 中的伺服器應用程式。  

- **原生應用程式**：服務是否使用「原生」  類型的 Azure AD 應用程式，也稱為 Configuration Manager 中的用戶端應用程式。  

- **動作**：您是否可以在 Configuration Manager 的 Azure 服務精靈中匯入或建立這些應用程式。  

|Service  |租用戶  |雲端  |Web 應用程式  |原生應用程式  |動作  |
|---------|---------|---------|---------|---------|---------|
|雲端管理搭配使用<br>Azure AD 探索 | 多個 | 公用、私人 | ![支援](media/green_check.png) | ![支援](media/green_check.png) | 匯入、建立 |
|Log Analytics 連接器 | 一個 | 公用、私人 | ![支援](media/green_check.png) | ![不支援](media/Red_X.png) | 匯入 |
|商務用<br>Microsoft Store | 一個 | 公用 | ![支援](media/green_check.png) | ![不支援](media/Red_X.png) | 匯入、建立 |

### <a name="about-azure-ad-apps"></a>關於 Azure AD 應用程式

不同的 Azure 服務需要不同的設定，而您可在 Azure 入口網站中設定。 此外，每個服務應用程式都可以要求不同的 Azure 資源權限。  

您可以使用單一應用程式進行多個服務。 Configuration Manager 和 Azure AD 中只有一個物件要管理。 當應用程式上的安全性金鑰到期時，您只要重新整理一個金鑰。

當您在精靈中建立其他 Azure 服務時，Configuration Manager 設計成可重複使用服務之間共通的資訊。 此行為可協助您不必多次輸入相同的資訊。

如需每個服務所需應用程式權限與設定的詳細資訊，請參閱[可用的服務](#available-services)中相關的 Configuration Manager 文章。

如需 Azure 應用程式的詳細資訊，請參閱下列文章：

- [Azure App Service 的驗證和授權](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)
- [Web 應用程式概觀](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)
- [在 Azure AD 中註冊應用程式的基本概念](/azure/active-directory/develop/authentication-scenarios)  
- [向 Azure Active Directory 租用戶註冊應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)


## <a name="before-you-begin"></a>開始之前

決定您要連線的服務之後，請參閱[服務詳細資料](#service-details)的表格。 下表提供完成 Azure 服務精靈所需的資訊。 請與 Azure AD 系統管理員事先討論。 決定要採取下列哪個動作：

- 預先在 Azure 入口網站中手動建立應用程式。 然後將應用程式詳細資料匯入 Configuration Manager。  

- 使用 Configuration Manager 直接在 Azure AD 中建立應用程式。 若要從 Azure AD 收集必要的資料，請檢閱本文其他章節的資訊。  

部分服務需要 Azure AD 應用程式擁有特定權限。 檢閱每個服務的資訊，以判斷任何必要的權限。 例如，Azure 系統管理員必須先在 [Azure 入口網站](https://portal.azure.com)中建立 Web 應用程式後，您才能予以匯入。

設定 Log Analytics 連接器時，在包含相關工作區的資源群組上，將「參與者」  權限提供給新註冊的 Web 應用程式。 此權限可讓 Configuration Manager 存取該工作區。 在指派權限時，於 Azure 入口網站的 [新增使用者]  區域中搜尋該應用程式註冊的名稱。 此程序與[為 Configuration Manager 提供 Log Analytics 權限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics)時的程序相同。 Azure 系統管理員必須先指派這些權限後，您才能將應用程式匯入 Configuration Manager。


## <a name="start-the-azure-services-wizard"></a>啟動 Azure 服務精靈

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。  

2. 在功能區的 [首頁]  索引標籤上，於 [Azure 服務]  群組中，選取 [設定 Azure 服務]  。  

3. 在 Azure 服務精靈的 [Azure 服務]  頁面上：  

    1. 為 Configuration Manager 中的物件指定 [名稱]  。  

    2. 指定選用 [描述]  以協助您識別服務。  

    3. 選取您想要與 Configuration Manager 連線的 Azure 服務。  

4. 選取 [下一步]  ，繼續前往 [Azure 服務精靈] 的 [Azure 應用程式內容](#azure-app-properties)頁面。  


## <a name="azure-app-properties"></a>Azure 應用程式屬性

在 Azure 服務精靈的 [應用程式]  頁面上，先從清單中選取 [Azure 環境]  。 該服務目前可用的環境，請參閱[服務詳細資料](#service-details)中的表格。

[應用程式] 頁面的其餘部分，會依特定服務而有所不同。 服務可使用的應用程式類型和您可使用的動作，請參閱[服務詳細資料](#service-details)中的表格。

- 如果應用程式支援匯入與建立這兩個動作，請選取 [瀏覽]  。 此動作會開啟 [[伺服器應用程式] 對話方塊](#server-app-dialog)或 [[用戶端應用程式] 對話方塊](#client-app-dialog)。  

- 如果應用程式只支援匯入動作，請選取 [匯入]  。 此動作會開啟 [[匯入應用程式] 對話方塊 (伺服器)](#import-apps-dialog-server) 或 [[匯入應用程式] 對話方塊 (用戶端)](#import-apps-dialog-client)。

在此頁面指定應用程式之後，選取 [下一步]  ，繼續前往 [Azure 服務精靈] 的 [[設定] 或 [探索]](#configuration-or-discovery) 頁面。

### <a name="web-app"></a>Web 應用程式

此應用程式的 Azure AD 類型為「Web 應用程式 / API」  ，也稱為 Configuration Manager 中的伺服器應用程式。

#### <a name="server-app-dialog"></a>伺服器應用程式對話方塊

當您在 [Azure 服務精靈] 的 [應用程式] 頁面上，選取 [Web 應用程式]  的 [瀏覽]  時，隨即會開啟 [伺服器應用程式] 對話方塊。 上面顯示的清單會顯示任何現有 Web 應用程式的下列屬性：

- 租用戶易記名稱
- 應用程式易記名稱
- 服務類型

您可以從 [伺服器應用程式] 對話方塊採取的動作有三個：

- 若要重複使用現有的 Web 應用程式，請從清單中選取。
- 選取 [匯入]  ，來開啟 [[匯入應用程式] 對話方塊](#import-apps-dialog-server)。
- 選取 [建立]  ，來開啟 [[建立伺服器應用程式] 對話方塊](#create-server-application-dialog)。

在您選取、匯入或建立 Web 應用程式之後，選取 [確定]  以關閉 [伺服器應用程式] 對話方塊。 此動作可以返回 Azure 服務精靈的 [[應用程式] 頁面](#azure-app-properties)。

#### <a name="import-apps-dialog-server"></a>匯入應用程式對話方塊 (伺服器)

當您從 [伺服器應用程式] 對話方塊或 [Azure 服務精靈] 的 [應用程式] 頁面選取 [匯入]  時，隨即會開啟 [匯入應用程式] 對話方塊。 您可以在此頁面輸入有關已在 Azure 入口網站建立的 Azure AD Web 應用程式資訊。 它會將該 Web 應用程式的相關中繼資料匯入至 Configuration Manager。 指定下列資訊：

- **Azure AD 租用戶名稱**
- **Azure AD 租用戶識別碼**
- **應用程式名稱**：應用程式的易記名稱。
- **用戶端識別碼**
- **祕密金鑰**
- **祕密金鑰的到期日**：從日曆選取未來的日期。
- **App 識別碼 URI**：這在 Azure AD 租用戶中必須是唯一的值。 它是在存取權杖中，由 Configuration Manager 用戶端用來要求存取該服務。 根據預設，此值為 `https://ConfigMgrService`。  

輸入資訊後，選取 [驗證]  。 然後選取 [確定]  ，以關閉 [匯入應用程式] 對話方塊。 此動作可以返回 Azure 服務精靈的 [[應用程式] 頁面](#azure-app-properties) 或 [[伺服器應用程式] 對話方塊](#server-app-dialog)。

#### <a name="create-server-application-dialog"></a>建立伺服器應用程式對話方塊

當您從 [伺服器應用程式] 對話方塊選取 [建立]  時，隨即會開啟 [建立伺服器應用程式] 對話方塊。 此頁面會在 Azure AD 中自動建立 Web 應用程式。 指定下列資訊：

- **應用程式名稱**：應用程式的易記名稱。
- **首頁 URL**：Configuration Manager 不使用此值，但卻是 Azure AD 的必要值。 根據預設，此值為 `https://ConfigMgrService`。  
- **App 識別碼 URI**：這在 Azure AD 租用戶中必須是唯一的值。 它是在存取權杖中，由 Configuration Manager 用戶端用來要求存取該服務。 根據預設，此值為 `https://ConfigMgrService`。  
- **祕密金鑰有效期間**：從下拉式清單中選擇 [1 年]  或 [2 年]  。 預設值為一年。

選取 [登入]  ，向 Azure 驗證為系統管理使用者。 Configuration Manager 不會儲存這些認證。 此角色在 Configuration Manager 中不需要權限，而且不需要為執行 Azure 服務精靈的相同帳戶。 向 Azure 成功驗證身分後，頁面會顯示 [Azure AD 租用戶名稱]  以供參考。

選取 [確定]  以在 Azure AD 中建立 Web 應用程式，然後關閉 [建立伺服器應用程式] 對話方塊。 此動作可以返回 [[伺服器應用程式] 對話方塊](#server-app-dialog)。

> [!NOTE]
> 如已定義 Azure AD 條件式存取原則，並適用於**所有雲端應用程式** - 必須從此原則排除已建立的伺服器應用程式。 如需如何排除特定應用程式的詳細資訊，請參閱 [Azure AD 條件式存取文件](https://docs.microsoft.com/azure/active-directory/conditional-access/)。

### <a name="native-client-app"></a>原生用戶端應用程式

此應用程式的 Azure AD 類型為「原生」  ，也稱為 Configuration Manager 中的用戶端應用程式。

#### <a name="client-app-dialog"></a>用戶端應用程式對話方塊

當您在 [Azure 服務精靈] 的 [應用程式] 頁面上，選取 [原生用戶端應用程式]  的 [瀏覽]  時，隨即會開啟 [用戶端應用程式] 對話方塊。 上面顯示的清單會顯示任何現有原生應用程式的下列屬性：

- 租用戶易記名稱
- 應用程式易記名稱
- 服務類型

您可以從 [用戶端應用程式] 對話方塊採取的動作有三個：

- 若要重複使用現有的原生應用程式，請從清單中選取。 
- 選取 [匯入]  ，來開啟 [[匯入應用程式] 對話方塊](#import-apps-dialog-client)。
- 選取 [建立]  ，來開啟 [[建立用戶端應用程式] 對話方塊](#create-client-application-dialog)。

在您選取、匯入或建立原生應用程式之後，選擇 [確定]  以關閉 [用戶端應用程式] 對話方塊。 此動作可以返回 Azure 服務精靈的 [[應用程式] 頁面](#azure-app-properties)。

#### <a name="import-apps-dialog-client"></a>匯入應用程式對話方塊 (用戶端)

當您從 [用戶端應用程式] 對話方塊選取 [匯入]  時，隨即會開啟 [匯入應用程式] 對話方塊。 您可以在此頁面輸入有關已在 Azure 入口網站建立的 Azure AD 原生應用程式資訊。 它會將該原生應用程式的相關中繼資料匯入至 Configuration Manager。 指定下列資訊：

- **應用程式名稱**：應用程式的易記名稱。
- **用戶端識別碼**

輸入資訊後，選取 [驗證]  。 然後選取 [確定]  ，以關閉 [匯入應用程式] 對話方塊。 此動作可以返回 [[用戶端應用程式] 對話方塊](#client-app-dialog)。

#### <a name="create-client-application-dialog"></a>建立用戶端應用程式對話方塊

當您從 [用戶端應用程式] 對話方塊選取 [建立]  時，隨即會開啟 [建立用戶端應用程式] 對話方塊。 此頁面會在 Azure AD 中自動建立原生應用程式。 指定下列資訊：

- **應用程式名稱**：應用程式的易記名稱。
- **回覆 URL**：Configuration Manager 不使用此值，但卻是 Azure AD 的必要值。 根據預設，此值為 `https://ConfigMgrService`。

選取 [登入]  ，向 Azure 驗證為系統管理使用者。 Configuration Manager 不會儲存這些認證。 此角色在 Configuration Manager 中不需要權限，而且不需要為執行 Azure 服務精靈的相同帳戶。 向 Azure 成功驗證身分後，頁面會顯示 [Azure AD 租用戶名稱]  以供參考。

選取 [確定]  以在 Azure AD 中建立原生應用程式，然後關閉 [建立用戶端應用程式] 對話方塊。 此動作可以返回 [[用戶端應用程式] 對話方塊](#client-app-dialog)。

## <a name="configuration-or-discovery"></a>設定或探索

在 [應用程式] 頁面上指定 Web 與原生應用程式後，Azure 服務精靈會繼續前往 [設定]  或 [探索]  頁面，取決於您連線的服務。 此頁面的詳細資料會因不同的服務而異。 如需詳細資訊，請參閱下列文章之一：  

- **雲端管理** 服務的 [探索]  頁面：[設定 Azure AD 使用者探索](configure-discovery-methods.md#azureaadisc)  

- **Log Analytics 連接器** 服務的 [設定]  頁面：[設定與 Log Analytics 的連線](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- **商務用 Microsoft Store**服務的 [設定]  頁面：[設定商務用 Microsoft Store 同步處理](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

最後，透過 [摘要]、[進度] 與 [完成] 頁面來完成 Azure 服務精靈。 您已經完成在 Configuration Manager 中設定 Azure 服務。 請重複此程序來設定其他 Azure 服務。


## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> 更新祕密金鑰

> [!Note]
> 若要在 1802 版和更舊版本中更新 Azure 應用程式的祕密金鑰，您必須重新建立應用程式。

### <a name="renew-key-for-created-app"></a>為已建立的應用程式更新金鑰

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區、展開 [雲端服務]  ，然後選取 [Azure Active Directory 租用戶]  節點。

1. 在 [詳細資料] 窗格上，選取應用程式的 Azure AD 租用戶。

1. 在功能區中，選取 [更新秘密金鑰]  。 輸入應用程式擁有者或 Azure AD 系統管理員的認證。

### <a name="renew-key-for-imported-app"></a>為已匯入的應用程式更新金鑰

如果您已在 Configuration Manager 中匯入 Azure 應用程式，請使用 Azure 入口網站來更新。 請注意新的秘密金鑰和到期日。 在 [更新祕密金鑰]  精靈上新增此資訊。  

> [!Note]  
> 關閉 Azure 應用程式屬性 [金鑰]  頁面之前請先儲存祕密金鑰。 當您關閉頁面時，會移除此資訊。


## <a name="view-the-configuration-of-an-azure-service"></a>檢視 Azure 服務的設定

檢視設定要使用之 Azure 服務的屬性。 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  。 選取您想要檢視或編輯的服務，然後選取 [內容]  。

如果您選取一項服務，然後選擇功能區中的 [刪除]  ，此動作會刪除 Configuration Manager 中的連線。 它不會移除 Azure AD 中的應用程式。 不再需要該應用程式時，請要求 Azure 系統管理員予以刪除。 或執行 Azure 服務精靈來匯入應用程式。<!--483440-->


## <a name="cloud-management-data-flow"></a>雲端管理資料流程

下圖是 Configuration Manager、Azure AD 及所連線雲端服務之間互動的概念性資料流程。 這個特定範例使用**雲端管理**服務，其包括 Windows 10 用戶端及伺服器與用戶端應用程式。 其他服務的流程都很類似。

![Configuration Manager 搭配使用 Azure AD 與雲端管理的資料流程圖](media/aad-auth.png)

1. Configuration Manager 系統管理員在 Azure AD 中匯入或建立的用戶端和伺服器應用程式。  

2. Configuration Manager Azure AD 使用者探索方法執行。 站台針對使用者物件使用 Azure AD 伺服器應用程式權杖來查詢 Microsoft Graph。  

3. 站台儲存有關使用者物件的資料。 如需詳細資訊，請參閱 [Azure AD 使用者探索](about-discovery-methods.md#azureaddisc)。  

4. Configuration Manager 用戶端要求 Azure AD 使用者權杖。 用戶端使用 Azure AD 用戶端應用程式的應用程式識別碼進行宣告，並將伺服器應用程式作為對象。 如需詳細資訊，請參閱[Azure AD 安全性權杖中的宣告](/azure/active-directory/develop/authentication-scenarios#security-tokens)。  

5. 用戶端會透過向雲端管理閘道和內部部署啟用 HTTPS 的管理點呈現 Azure AD 權杖，來向站台驗證身分。  
