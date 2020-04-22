---
title: 站台必要條件
titleSuffix: Configuration Manager
description: 了解如何將 Windows 電腦設定為 Configuration Manager 站台系統伺服器。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d4fb94d0ab64cb7c3dc3128c982b0c2b162b22b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702156"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Configuration Manager 的站台和站台系統必要條件

適用於：  Configuration Manager (最新分支)

Windows 電腦需要特定的設定，以支援當成 Configuration Manager 站台系統伺服器來使用。

對於軟體更新點的 Windows Server Update Services (WSUS) 等產品，您需要參閱產品文件來識別該產品使用的其他必要條件和限制。 這裡只包含直接套用以與 Configuration Manager 搭配使用的設定。

如需 .NET Framework 的詳細資訊，請參閱[生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)。


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> 一般需求和限制

下列需求適用於所有站台系統伺服器：

- 每個站台系統伺服器必須使用 64 位元 OS。 唯一的例外是發佈點站台系統角色，您可以將它安裝在部分的 32 位元作業系統上。  

- 任何作業系統的 Server Core 安裝上不支援站台系統。 例外狀況是發佈點站台系統角色支援 Server Core 安裝。 如需詳細資訊，請參閱 [Configuration Manager 站台系統伺服器支援的作業系統](supported-operating-systems-for-site-system-servers.md)。  

- 安裝站台系統伺服器之後，不支援變更：  

    - 站台系統電腦所在網域的網域名稱 (也稱為**網域重新命名**)。  

    - 電腦的網域成員資格。  

    - 電腦的名稱。  

    如果您必須變更任何項目，請先從電腦移除站台系統角色。 然後在變更完成之後重新安裝角色。 若變更會影響站台伺服器，請先將站台解除安裝。 然後在變更完成之後重新安裝站台。  

- Windows Server 叢集執行個體上不支援站台系統角色。 唯一的例外是站台資料庫伺服器。 如需詳細資訊，請參閱[針對 Configuration Manager 站台資料庫使用 SQL Server 叢集](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)。  

    從 1810 版開始，Configuration Manager 安裝程序不會再封鎖在具有容錯移轉叢集 Windows 角色的電腦上安裝站台伺服器角色。 SQL Always On 需要此角色，因此先前您無法將站台資料庫共置在站台伺服器上。 透過這項變更，您可以使用較少的伺服器建立高可用性的站台，方法是被動模式中使用 SQL AlwaysOn 和站台伺服器。 如需詳細資訊，請參閱[高可用性選項](../../servers/deploy/configure/high-availability-options.md)。 <!--3607761, fka 1359132-->  

- 不支援變更任何 Configuration Manager 服務的啟動類型或 [登入身分] 設定。 如果這麼做，可能會導致重要服務無法正確執行。  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Windows Server 2012 和更新版本作業系統的必要條件  

請參閱本文的主要章節，以了解 Windows Server 2012 和更新版本上站台系統伺服器和角色的特定必要條件：

- [管理中心網站和主要站台伺服器](#bkmk_2012sspreq)
- [次要站台伺服器](#bkmk_2012secpreq)
- [資料庫伺服器](#bkmk_2012dbpreq)
- [SMS 提供者伺服器](#bkmk_2012smsprovpreq)
- [應用程式類別目錄網站點](#bkmk_2012acwspreq)
- [應用程式類別目錄 Web 服務點](#bkmk_2012ACwsitepreq)
- [Asset Intelligence 同步處理點](#bkmk_2012AIpreq)
- [憑證登錄點](#bkmk_2012crppreq)
- [發佈點](#bkmk_2012dppreq)
- [Endpoint Protection 點](#bkmk_2012EPPpreq)
- [註冊點](#bkmk_2012Enrollpreq)
- [註冊 Proxy 點](#bkmk_2012EnrollProxpreq)
- [後援狀態點](#bkmk_2012FSPpreq)
- [管理點](#bkmk_2012MPpreq)
- [ Reporting Services 點](#bkmk_2012RSpoint)
- [服務連接點](#bkmk_SCPpreq)
- [軟體更新點](#bkmk_2012SUPpreq)
- [狀態移轉點](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> 管理中心網站和主要站台伺服器

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- 遠端差異壓縮  

- 當您在站台伺服器以外的伺服器上使用軟體更新點時，請在站台伺服器上安裝 WSUS 管理主控台。

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- 在您安裝或升級管理中心網站或主要站台之前，請安裝您正在安裝或升級之 Configuration Manager 目標版本所需的 Windows 評定及部署套件 (ADK) 版本。 如需詳細資訊，請參閱 [Windows 10 ADK](support-for-windows-10.md#windows-10-adk)。  

- 如需此需求的詳細資訊，請參閱 [OS 部署的基礎結構需求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

### <a name="visual-c-redistributable"></a>Visual C++ 可轉散發套件  

- Configuration Manager 會將 Microsoft Visual C++ 2013 可轉散發套件安裝在要安裝站台伺服器的每部電腦上。  

- 管理中心網站和主要站台需要適用之可轉散發檔案的 x86 和 x64 版本。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> 次要站台伺服器

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- 遠端差異壓縮  

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ 可轉散發套件

- Configuration Manager 會將 Microsoft Visual C++ 2013 可轉散發套件安裝在要安裝站台伺服器的每部電腦上。  

- 次要站台只需要 x64 版本。  

### <a name="default-site-system-roles"></a>預設站台系統角色  

- 根據預設，次要站台會安裝**管理點**和**發佈點**。  

- 請確定次要站台伺服器符合這些站台系統角色的必要條件。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> 資料庫伺服器  

### <a name="remote-registry-service"></a>遠端登錄服務  

- 在安裝 Configuration Manager 站台期間，請在裝載站台資料庫的電腦上啟用**遠端登錄**服務。  

### <a name="sql-server"></a>SQL Server  

- 在您安裝管理中心網站或主要站台之前，請安裝支援的 SQL Server 版本來裝載站台資料庫。 如需詳細資訊，請參閱[支援的 SQL Server 版本](support-for-sql-server-versions.md)。  

- 安裝次要站台之前，您可以安裝支援的 SQL Server 版本。  

- 如果您選擇讓 Configuration Manager 安裝 SQL Server Express 作為次要站台安裝的一部分，請確定電腦是否符合執行 SQL Server Express 的需求。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS 提供者伺服器  

### <a name="windows-adk"></a>Windows ADK

- 安裝 SMS 提供者執行個體的電腦必須具有您正在安裝或升級之 Configuration Manager 目標版本所需要的 Windows ADK 版本。 如需詳細資訊，請參閱 [Windows 10 ADK](support-for-windows-10.md#windows-10-adk)。  

- 如需此需求的詳細資訊，請參閱[作業系統部署的基礎結構需求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- 若使用[系統管理服務](../../../develop/adminservice/overview.md)，則裝載 SMS 提供者角色的伺服器需要 .NET 4.5 或更新版本  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager 1810 版需要 .NET 4.5.2 或更新版本。

- 網頁伺服器 (IIS)：每個提供者都會嘗試安裝[系統管理服務](../../../develop/adminservice/overview.md)。 此服務對 IIS 具有相依性，可將憑證繫結至 HTTPS 連接埠 443。 Configuration Manager 會使用 IIS API 來檢查此憑證設定。 如果將站台設定為[增強型 HTTP](../hierarchy/enhanced-http.md)，則 Configuration Manager 會使用 IIS API 來繫結站台產生的憑證。 從 2002 版開始，站台會自動使用站台的自我簽署憑證。

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> 應用程式目錄網站點  

> [!Important]  
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定  

- 一般 HTTP 功能：  

    - 預設文件  

    - 靜態內容  

- 應用程式開發：  

    - ASP.NET 3.5 (及自動選取的選項)  

    - ASP.NET 4.5 (及自動選取的選項)  

    - .NET 擴充性 3.5  

    - .NET 擴充性 4.5  

- 安全性：  

    - Windows 驗證  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> 應用程式目錄 Web 服務點  

> [!Important]  
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- ASP.NET 4.5：  

    - HTTP 啟動 (及自動選取的選項)  

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定

- 一般 HTTP 功能：  

    - 預設文件  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

- 應用程式開發：  

    - ASP.NET 3.5 (及自動選取的選項)  

    - .NET 擴充性 3.5  

    - ASP.NET 4.5 (及自動選取的選項)  

    - .NET 擴充性 4.5  

### <a name="computer-memory"></a>電腦記憶體  

- 裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

- 此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Asset Intelligence 同步處理點  

### <a name="net-framework"></a>.NET Framework

請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> 憑證登錄點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework

    - HTTP 啟動  

### <a name="net-framework"></a>.NET Framework

請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定

- 應用程式開發：  

    - ASP.NET 3.5 (及自動選取的選項)  

    - ASP.NET 4.5 (及自動選取的選項)  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

    - IIS 6 WMI 相容性  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> 發佈點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- 遠端差異壓縮  

#### <a name="iis-configuration"></a>IIS 設定

- 應用程式開發：  

    - ISAPI 擴充程式  

- 安全性：  

    - Windows 驗證  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

    - IIS 6 WMI 相容性  

### <a name="powershell"></a>PowerShell  

- 於 Windows Server 2012 或更新版本上，在您安裝發佈點之前需要 PowerShell 3.0 或 4.0。  

### <a name="visual-c-redistributable"></a>Visual C++ 可轉散發套件

- Configuration Manager 會在裝載發佈點的每部電腦上安裝 Microsoft Visual C++ 2013 可轉散發套件。  

- 安裝的版本取決於電腦平台 (x86 或 x64)。  

### <a name="microsoft-azure"></a>Microsoft Azure  

- 您可以使用 Microsoft Azure 中的雲端服務來裝載發佈點。  

### <a name="to-support-pxe-or-multicast"></a>支援 PXE 或多點傳送  

- 在不使用 Windows 部署服務的情況下，於發佈點上啟用 PXE 回應程式。  

- 安裝和設定 Windows 部署服務 (WDS) Windows Server 角色。  

    > [!NOTE]  
    > 當您設定發佈點以在執行 Windows Server 2012 或更新版本的伺服器上支援 PXE 或多點傳送時，WDS 會自動安裝與設定。  

- 針對已啟用多點傳送的發佈點，確定已安裝 SQL Server Native Client 且其為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

如需詳細資訊，請參閱[安裝及設定發佈點](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> 發佈點傳輸內容時，會使用內建於 Windows 的**背景智慧型傳送服務** (BITS) 進行傳輸。 發佈點角色不需要安裝選擇性的「BITS IIS 伺服器延伸模組功能」，因為用戶端不會將資訊上傳到它上面。  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection 點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能  

- .NET Framework 3.5

- Windows Defender 功能 (Windows Server 2016 或更新版本)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> 註冊點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

    - HTTP 啟動 (及自動選取的選項)  

    - ASP.NET 4.5  

    - Windows Communication Foundation (WCF) 服務<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

> [!Note]
> 此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 如果 .NET Framework 在重新開機時擱置，則伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定

- 一般 HTTP 功能：  

    - 預設文件  

- 應用程式開發：  

    - ASP.NET 3.5 (及自動選取的選項)  

    - .NET 擴充性 3.5  

    - ASP.NET 4.5 (及自動選取的選項)  

    - .NET 擴充性 4.5  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

### <a name="computer-memory"></a>電腦記憶體

- 裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

- 此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> 註冊 Proxy 點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

> [!Note]
> 此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 如果 .NET Framework 在重新開機時擱置，則伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定

- 一般 HTTP 功能：  

    - 預設文件  

    - 靜態內容  

- 應用程式開發：  

    - ASP.NET 3.5 (及自動選取的選項)  

    - ASP.NET 4.5 (及自動選取的選項)  

    - .NET 擴充性 3.5  

    - .NET 擴充性 4.5  

- 安全性：  

    - Windows 驗證  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

### <a name="computer-memory"></a>電腦記憶體

- 裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

- 此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> 後援狀態點

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- BITS 伺服器擴充功能 (和自動選取的選項) 或背景智慧型傳送服務 (BITS) (及自動選取的選項)

#### <a name="iis-configuration"></a>IIS 設定

需要預設 IIS 設定，再加上下列各項：  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> 管理點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- BITS 伺服器擴充功能 (和自動選取的選項) 或背景智慧型傳送服務 (BITS) (及自動選取的選項)  

### <a name="net-framework"></a>.NET Framework

請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定

- 應用程式開發：  

    - ISAPI 擴充程式  

- 安全性：  

    - Windows 驗證  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

    - IIS 6 WMI 相容性  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Reporting Services 點  

### <a name="net-framework"></a>.NET Framework

請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- 安裝並設定至少一個 SQL Server 執行個體以支援 SQL Server Reporting Services，之後才能安裝報告點。  

- 您用於 SQL Server Reporting Services 的執行個體可以是用於站台資料庫的相同執行個體。  

- 此外，只要其他 System Center 產品不限制共用 SQL Server 執行個體，您使用的執行個體就可以與其他 System Center 產品共用。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> 服務連接點  

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

> [!Note]
> 此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 如果 .NET Framework 在重新開機時擱置，則伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ 可轉散發套件

- Configuration Manager 會在裝載發佈點的每部電腦上安裝 Microsoft Visual C++ 2013 可轉散發套件。  

- 站台系統角色需要使用 x64 版本。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> 軟體更新點  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

需要預設 IIS 設定。

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- 在電腦上安裝 Windows Server 角色 Windows Server Update Services，之後才能安裝軟體更新點。  

- 如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。  

> [!NOTE]  
> 當您在站台伺服器以外的伺服器上使用軟體更新點時，必須在站台伺服器上安裝 WSUS 管理主控台。

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> 狀態移轉點

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

    - HTTP 啟動 (及自動選取的選項)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

啟用 .NET Framework 3.5 的 Windows 功能。

也請安裝支援 .NET Framework 4.5 版或更新版本的版本。 從 1906 版開始，Configuration Manager 支援 .NET Framework 4.8。

> [!Note]
> 此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 如果 .NET Framework 在重新開機時擱置，則伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

如需 .NET Framework 版本的詳細資訊，請參閱下列文章：

- [.NET Framework 版本和相依性](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命週期常見問題 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 設定

- 一般 HTTP 功能：  

    - 預設文件  

- 應用程式開發：  

    - ASP.NET 3.5 (及自動選取的選項)  

    - .NET 擴充性 3.5  

    - ASP.NET 4.5 (及自動選取的選項)  

    - .NET 擴充性 4.5  

- IIS 6 管理相容性：  

    - IIS 6 Metabase 相容性  

### <a name="sql-server-native-client"></a>SQL Server Native Client

當您安裝新站台時，Configuration Manager 會自動安裝 SQL Server Native Client 作為可轉散發元件。 安裝站台之後，Configuration Manager 不會升級 SQL Server Native Client。 請確定此元件為最新狀態。 如需詳細資訊，請參閱[先決條件檢查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

