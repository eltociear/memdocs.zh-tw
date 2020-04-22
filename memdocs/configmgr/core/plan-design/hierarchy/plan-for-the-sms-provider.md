---
title: 規劃 SMS 提供者
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的 SMS 提供者站台系統角色。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01ea9b089da3cfcfc3e8d23e7ad25d27ab2fec7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692756"
---
# <a name="plan-for-the-sms-provider"></a>規劃 SMS 提供者

適用於：  Configuration Manager (最新分支)

若要管理 Configuration Manager，可以使用連線到 **SMS 提供者**執行個體的 Configuration Manager 主控台。 根據預設，SMS 提供者會在安裝管理中心站台或主要站台時，一併安裝在站台伺服器上。

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> 關於 SMS 提供者  

SMS 提供者是 Windows Management Instrumentation (WMI) 提供者，會指派站台之 Configuration Manager 資料庫的**讀取**與**寫入**權限。  

- 每個管理中心網站和主要網站上至少需要一個 SMS 提供者。 您可以視需要安裝額外的提供者。  

- **SMS Admins** 安全性群組提供對 SMS 提供者的存取。 Configuration Manager 會自動在站台伺服器上和每部安裝了 SMS 提供者執行個體的電腦上，建立此群組。 如需詳細資訊，請參閱 [SMS Admins](accounts.md#sms-admins)。  

- 次要站台不支援 SMS 提供者角色。  

Configuration Manager 系統管理使用者使用 SMS 提供者來存取儲存於資料庫中的資訊。 若要執行此動作，系統管理員可以使用 Configuration Manager 主控台、資源總管、工具以及自訂指令碼。 SMS 提供者不會與 Configuration Manager 用戶端互動。 當 Configuration Manager 主控台連線到站台時，它會查詢站台伺服器上的 WMI，以找出要使用的 SMS 提供者執行個體。  

SMS 提供者會協助強制執行 Configuration Manager 安全性。 它僅會傳回主控台使用者獲授權可檢視的資訊。  

SMS 提供者也會透過 HTTPS 提供 API 互通性存取，稱為**管理服務**。 此 REST API 可用於取代自訂 Web 服務，以存取來自網站的資訊。 如需詳細資訊，請參閱[什麼是管理服務？](../../../develop/adminservice/overview.md)

> [!IMPORTANT]  
> 當站台的每個 SMS 提供者執行個體離線時，Configuration Manager 主控台將無法連線到該站台。  

如需如何管理 SMS 提供者的詳細資訊，請參閱[管理 SMS 提供者](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。  

## <a name="installation-prerequisites"></a>安裝必要條件  

若要支援 SMS 提供者，目標伺服器必須符合下列必要條件：  

- 與站台伺服器和站台資料庫站台系統位於相同的網域  

- 不可擁有來自不同站台的站台系統角色  

- 不可已有來自任何站台的 SMS 提供者  

- 執行支援的 OS 版本  

- 至少有 650 MB 的可用磁碟空間，才能支援 Windows ADK 元件。 如需 Windows ADK 與 SMS 提供者的詳細資訊，請參閱 [OS 部署需求](#BKMK_WAIKforSMSProv)。  

- 針對[管理服務](../../../develop/adminservice/overview.md) REST API：

  - .NET 4.5 或更新版本

  - 啟用 Windows 伺服器角色**網頁伺服器 (IIS)**

    > [!Note]  
    > 每個 SMS 提供者都會嘗試安裝管理服務，該服務需要憑證。 此服務對 IIS 具有相依性，以將該憑證繫結 HTTPS 連接埠 443。 如果您啟用[增強 HTTP](enhanced-http.md)，則站台會使用 IIS API 繫結該憑證。 如果您的站台使用 PKI，則您需要手動將 PKI 憑證繫結在 SMS 提供者的 IIS 中。 從 2002 版開始，站台會自動使用站台的自我簽署憑證。

## <a name="locations"></a><a name="bkmk_location"></a> 位置  

安裝站台時，會自動安裝該站台的第一個 SMS 提供者。 您可以為 SMS 提供者指定以下任何一個受支援的位置：  

- 站台伺服器  

- 站台資料庫伺服器  

- 另一部符合[安裝必要條件](#installation-prerequisites)的伺服器  

若要檢視站台的每個 SMS 提供者位置：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 從清單中選取所需的站台，然後在功能區中選擇 [內容]  。  

3. 在站台 [內容]  的 [一般]  索引標籤上，檢視 [SMS 提供者位置]  欄位。  

每個 SMS 提供者支援來自多個請求的同時連線。 這些連線的唯一限制是 Windows 可用的伺服器連線數目，以及伺服器上可用來服務連線要求的資源。  

安裝站台後，您可以再次在站台伺服器上執行 Configuration Manager 安裝程式。 使用安裝程式變更現有 SMS 提供者的位置，或在該站台上安裝其他 SMS 提供者。 只在電腦上安裝一個 SMS 提供者。 一部電腦無法裝載來自多個站台的 SMS 提供者。  

### <a name="choosing-a-location"></a>選擇位置

下列各節描述在每個受支援位置上安裝 SMS 提供者的優缺點：  

#### <a name="configuration-manager-site-server"></a>Configuration Manager 站台伺服器

- **優點：**  

  - SMS 提供者不使用站台資料庫電腦的系統資源。  

  - 除了網站伺服器或網站資料庫電腦外，此位置也可提供比位於電腦上的 SMS 提供者更好的效能。  

- **缺點：**  

  - SMS 提供者會使用網站伺服器操作專用的系統和網路資源。  

#### <a name="sql-server-that-hosts-the-site-database"></a>裝載站台資料庫的 SQL Server

- **優點：**  

  - SMS 提供者不使用站台伺服器上的系統資源。  

  - 若有足夠伺服器資源可以使用，此位置可提供三個位置中最佳的效能。  

- **缺點：**  

  - SMS 提供者會使用網站資料庫操作專用的系統和網路資源。  

  - 當站台資料庫裝載於 SQL Server 的叢集執行個體上時，即無法使用此位置。  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>站台伺服器或站台資料庫伺服器以外的電腦

- **優點：**  

  - SMS 提供者不使用站台伺服器或站台資料庫系統資源。  

  - 此類型的位置可讓您部署額外 SMS 提供者，以提供高使用性的連線。  

- **缺點：**  

  - SMS 提供者效能可能會降低。 此行為是由於協調站台伺服器與站台資料庫電腦需要額外網路活動所造成。  

  - 必須讓站台資料庫伺服器與所有安裝 Configuration Manager 主控台的電腦一律能存取此伺服器。  

  - 此位置可使用其他服務專用的系統資源。  

## <a name="authentication"></a><a name="bkmk_auth"></a> 驗證

<!--1357013-->
從 1810 版開始，您可以指定系統管理員存取 Configuration Manager 站台的最低驗證層級。 這項功能會強制系統管理員以必要層級登入 Windows。 它會套用至存取 SMS 提供者的所有元件。 例如，Configuration Manager 主控台、SDK 方法和 Windows PowerShell Cmdlet。

### <a name="configure-authentication"></a>設定驗證

若要進行此設定，請先以預期的驗證層級登入 Windows。

> [!Important]  
> 此設定是全階層設定。 在您變更此設定之前，請確定所有 Configuration Manager 系統管理員都能以必要的驗證層級登入 Windows。

若要進行此設定，請使用下列步驟：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 在功能區中選取 [階層設定]  。  

3. 切換至 [驗證]  索引標籤。選取所需的[驗證層級](#authentication-levels)，然後選取 [確定]  。  

    - 只有在必要時，才選取 [新增]  來排除特定使用者或群組。 如需詳細資訊，請參閱[排除](#exclusions)。  

### <a name="authentication-levels"></a>驗證層級

可用的層級如下：

- **Windows 驗證**：需要使用 Active Directory 網域認證驗證。 此設定為之前的行為以及目前的預設設定。 當您更新站台時，不會變更驗證層級。  

- **憑證驗證**：需要使用由信任的 PKI 憑證授權單位發出的有效憑證進行驗證。 您並不是在 Configuration Manager 中設定此憑證。 Configuration Manager 需要系統管理員使用 PKI 登入。  

- **Windows Hello 企業版驗證**：需要以繫結至裝置強式雙因素驗證進行驗證並使用生物識別技術或 PIN。 如需詳細資訊，請參閱 [Windows Hello 企業版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)。  

### <a name="exclusions"></a>排除

您也可以從 [階層設定] 的 [驗證]  索引標籤排除特定使用者或群組。 請謹慎使用此選項。 例如，當特定使用者需要存取 Configuration Manager 主控台時，但無法在所需層級通過 Windows 驗證。 它可能也需要在系統帳戶內容底下執行的自動化或服務。

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> 關於 SMS 提供者語言  

SMS 提供者操作時顯示的語言可與您安裝該 SMS 提供者之伺服器的語言不同。  

當系統管理使用者或 Configuration Manager 使用 SMS 提供者處理要求資料時，它會嘗試傳回格式符合要求電腦 OS 語言的資料。

其嘗試比對語言的方式是間接方式。 SMS 提供者不會將資訊從一種語言翻譯成另一種語言。 當傳回的資料在 Configuration Manager 主控台上顯示時，資料的顯示語言會視物件來源和儲存類型而定。  

當 Configuration Manager 將物件的資料儲存在資料庫時，可用的語言取決於下列因素：  

- Configuration Manager 使用多國語言支援，來儲存其所建立的物件。 它使用您執行安裝程式時為站台設定的語言，將物件儲存在站台資料庫中。 Configuration Manager 主控台會以要求電腦的顯示語言來顯示這些物件 (若物件可使用該語言)。 如果主控台無法以要求電腦的顯示語言來顯示物件，則會以預設語言顯示物件，亦即英文。  

- Configuration Manager 使用用來建立物件的語言，來儲存系統管理使用者所建立的物件。 這些物件會在 Configuration Manager 主控台中以相同語言顯示。 SMS 提供者無法翻譯這些物件，且沒有多個語言選項。  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> 使用多重 SMS 提供者  

網站完成安裝後，您可以為網站安裝額外的 SMS 提供者。 若要安裝其他的 SMS 提供者，請在站台伺服器上執行 Configuration Manager 安裝程式。

若下列任何一項為真，請考慮安裝額外的 SMS 提供者：  

- 多位系統管理使用者必須使用 Configuration Manager 主控台同時連線到一個站台。  

- 您使用可能引入經常呼叫 SMS 提供者的 Configuration Manager SDK 或其他產品。  

- 您有 SMS 提供者高可用性的商務需求。  

當您在站台上安裝多個 SMS 提供者，並提出連線要求時，站台會隨機指派每個新連線要求，以便使用安裝的 SMS 提供者。 您無法指定 SMS 提供者搭配使用特定的連線工作階段。  

> [!NOTE]  
> 請考慮每個 SMS 提供者位置的優缺點。 如需詳細資訊，請參閱[位置](#bkmk_location)。 請在您擁有之資訊無法讓您控制要為每個新連線使用哪個 SMS 提供者的情況下，在這些考量之間取得平衡。  

首次將 Configuration Manager 主控台連線到某個站台時，連線會查詢站台伺服器上的 WMI。 此查詢會找出主控台所使用的 SMS 提供者執行個體。 在工作階段結束前，主控台會持續使用這個特定的 SMS 提供者執行個體。 若因 SMS 提供者伺服器在網路上無法使用，導致工作階段結束，則當您將主控台重新連線到站台時，它會重複初始查詢。 可能是站台指派了無法使用的相同 SMS 提供者執行個體。 若發生此行為，請嘗試重新連線到主控台，直到站台傳回可用的 SMS 提供者為止。  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> 關於 SMS 提供者命名空間  

Configuration Manager WMI 架構會定義 SMS 提供者的結構。 架構命名空間會描述 SMS 提供者架構內 Configuration Manager 資料的位置。 下表包含 SMS 提供者所使用的一些常見命名空間：  

|命名空間|說明|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|SMS 提供者，廣泛為 Configuration Manager 主控台、資源總管、Configuration Manager 工具以及指令碼所用。|  
|`Root\SMS\SMS_ProviderLocation`|站台 SMS 提供者電腦的位置。|  
|`Root\CIMv2`|清查硬體與軟體時，清查 WMI 命名空間資訊的位置。|  
|`Root\CCM`|Configuration Manager 用戶端設定原則和用戶端資料。|  
|`Root\CIMv2\SMS`|清查用戶端代理程式所收集清查回報類別的位置。 用戶端會在電腦原則評估期間編譯這些設定。 這些設定是以電腦的用戶端設定組態為基礎。|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a> OS 部署需求

您安裝 SMS 提供者執行個體的電腦需要所支援 Windows ADK 版本。  

如需此需求的詳細資訊，請參閱 [OS 部署的基礎結構需求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)和 [Windows 10 的支援](../configs/support-for-windows-10.md)。  

管理 OS 部署時，Windows ADK 允許 SMS 提供者可完成各類工作，例如：  

- 檢視 WIM 檔案詳細資料  

- 新增驅動程式檔案至現有的開機映像  

- 建立開機 ISO 檔案  

Windows ADK 安裝可能在每台安裝 SMS 提供者的電腦上，最多會需要 650 MB 的可用磁碟空間。 這個大量的磁碟空間是 Configuration Manager 安裝 Windows PE 開機映像的必要條件。  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a> 系統管理服務

<!--3607711, fka 1321523-->

SMS 提供者會透過 HTTPS OData 連線提供 API 互通性存取，稱為**管理服務**。 此 REST API 可用於取代自訂 Web 服務，以存取來自網站的資訊。

如需詳細資訊，請參閱[什麼是管理服務？](../../../develop/adminservice/overview.md)
