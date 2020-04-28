---
title: 支援的用戶端和裝置
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 針對用戶端和裝置支援的 OS 版本。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 57c60fcdadf3e58b59d33ecf2753789122a38ecc
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078680"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Configuration Manager 針對用戶端和裝置支援的 OS 版本

適用於：  Configuration Manager (最新分支)

Configuration Manager 支援在 Windows 和 macOS 電腦上安裝用戶端軟體。  

## <a name="general-requirements-and-limitations"></a>一般需求和限制

檢閱下列適用於所有用戶端的需求和限制：

- 不支援變更任何 Configuration Manager 服務的啟動類型或 [登入身分]  設定。 此變更可能導致重要服務無法正確執行。

## <a name="windows-computers"></a>Windows 電腦  

若要管理下列 Windows OS 版本，請使用 Configuration Manager 隨附的用戶端。 如需詳細資訊，請參閱[如何將用戶端部署至 Windows 電腦](../../clients/deploy/deploy-clients-to-windows-computers.md)。  

### <a name="supported-client-os-versions"></a>支援的用戶端 OS 版本

- **Windows 10**  

    如需詳細資訊，請參閱[對 Windows 10 的支援](support-for-windows-10.md)。  

- **Windows 8.1** (x86、x64)：專業版、企業版

#### <a name="windows-virtual-desktop"></a>Windows 虛擬桌面

<!--3556025-->
[Windows 虛擬桌面](https://docs.microsoft.com/azure/virtual-desktop/)是在 Microsoft Azure 上執行的桌面和應用程式虛擬化服務。 從 1906 版開始，請使用 Configuration Manager 來管理這些在 Azure 中執行 Windows 的虛擬裝置。

與終端伺服器類似，其中部分虛擬裝置允許多個並行的作用中使用者工作階段。 為了協助提升用戶端效能，Configuration Manager 現在可以在允許這些多個使用者工作階段的任何裝置上停用使用者原則。 即使啟用使用者原則，用戶端仍會根據預設在這些裝置 (包括 Windows 10 企業版多重工作階段與終端機伺服器) 上將其停用。

用戶端只會在新安裝期間偵測到這類裝置時停用使用者原則。 針對您更新到此版本後的此類型現有用戶端，仍會保存先前的行為。 在現有裝置上，即使偵測到裝置允許多個使用者工作階段，也會設定使用者原則設定。

如果在此案例中需要使用者原則，並接受任何潛在的效能影響，請使用下列其中一種方法，以啟用使用者原則：

- 在 1910 版和更新版本中，請使用[用戶端設定](../../clients/deploy/configure-client-settings.md)。 在 [用戶端原則]  群組中，進行下列設定：**啟用多個使用者工作階段的使用者原則**。<!-- 4737447 -->

- 在 1906 版中，請使用 Configuration Manager SDK 搭配 [SMS_PolicyAgentConfig 伺服器 WMI 類別](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md)。 將新的 `PolicyEnableUserPolicyOnTS` 屬性設為 `true`。

> [!Note]  
> 您無法搭配執行 Windows 10 企業版多工作階段的用戶端使用共同管理。 <!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>支援的伺服器 OS 版本

- **Windows Server 2019**：Standard、Datacenter <sup>[附註 1](#bkmk_note1)</sup>  
    (從 Configuration Manager 1806 版開始。)

- **Windows Server 2016**：Standard、Datacenter <sup>[附註 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**：Workgroup、Standard  

- **Windows Server 2012 R2** (x64)：Standard、Datacenter <sup>[附註 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64)：Standard、Datacenter <sup>[附註 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

下列版本專指 OS 的 Server Core 安裝。 <sup>[附註 3](#bkmk_note3)</sup>  

Windows Server 半年通道版本是 Server Core 安裝，例如，Windows Server 1809 版。 做為 Configuration Manager 用戶端，就像關聯的 Windows 10 半年通道版本一樣，它們也受支援。 如需詳細資訊，請參閱[對 Windows 10 的支援](support-for-windows-10.md)。

- **Windows Server 2019** (x64) <sup>[附註 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[附註 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[附註 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[附註 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a> 附註 1

Configuration Manager 已測試並支援 Windows Server Datacenter 版本，但並未正式通過 Windows Server 的認證。 針對 Windows Server Datacenter Edition 特定問題，未提供 Configuration Manager Hotfix 支援。 如需有關 Windows Server 用戶端程式的詳細資訊，請參閱 [Windows Server Catalog](https://www.windowsservercatalog.com/)。

#### <a name="note-2"></a><a name="bkmk_note2"></a> 附註 2

若要支援[用戶端推送安裝](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)，請新增「檔案和存放服務」伺服器角色的「檔案伺服器」服務。 如需有關在 Server Core 上安裝 Windows 功能的詳細資訊，請參閱[使用 Windows PowerShell Cmdlet 安裝角色、角色服務與功能](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets) \(英文\)。  

#### <a name="note-3"></a><a name="bkmk_note3"></a> 附註 3

在任何版本的 Windows Server Core 上都不支援新的「軟體中心」應用程式。<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded 電腦  

您可以藉由在裝置上安裝 Configuration Manager 用戶端，來管理 Windows Embedded 裝置。 如需詳細資訊，請參閱[規劃將用戶端部署至 Windows Embedded 裝置](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

### <a name="requirements-and-limitations"></a>需求及限制

- 在未啟用寫入篩選器的 Windows Embedded 系統上可支援所有用戶端功能。  

- 針對所有功能 (電源管理除外)，支援使用下列其中一項的用戶端：  

  - 增強式寫入篩選器 (EWF)

  - RAM 檔案型寫入篩選器 (FBWF)

  - 整合寫入篩選器 (UWF)  

- 所有 Windows Embedded 裝置都不支援應用程式目錄。  

### <a name="supported-os-versions"></a>支援的 OS 版本  

- **Windows 10 企業版** (x86、x64)  

- **Windows 10 IoT 企業版** (x86、x64)  
    此版本包含長期維護通道 (LTSC)。 如需詳細資訊，請參閱 [Windows 10 IoT 企業版概觀](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) \(部分機器翻譯\)。<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry** (x86、x64)

- **Windows Embedded 8 Standard** (x86、x64)

- **Windows Thin PC** (x86、x64)

- **Windows Embedded POSReady 7** (x86、x64)

- **Windows Embedded Standard 7 (含 SP1)** (x86、x64)

## <a name="windows-ce-computers"></a>Windows CE 電腦

您可以使用 Configuration Manager 隨附的舊版 Configuration Manager 行動裝置用戶端來管理 Windows CE 裝置。  

### <a name="requirements-and-limitations"></a>需求及限制

- 行動裝置用戶端需要 0.78 MB 的儲存空間來安裝。 登入可能需要最多 256 KB 的額外儲存空間。

- 這些行動裝置的功能因平台和用戶端類型而異。 如需有關所支援管理功能的資訊，請參閱[選擇裝置管理解決方案](../choose-a-device-management-solution.md)。  

### <a name="supported-os-versions"></a>支援的 OS 版本

- Windows CE 7.0 (ARM 和 x86 處理器)  

    > [!Note]
    > 對 Configuration Manager 中 Windows CE 7.0 的支援已淘汰。 如需詳細資訊，請參閱[已移除與已淘汰的 Configuration Manager 用戶端項目](../changes/deprecated/removed-and-deprecated-client.md)。

#### <a name="supported-languages-include"></a>支援的語言包括

- 中文 (簡體及繁體)

- 英文 (美國)

- 法文 (法國)

- 德文

- 義大利文

- 日文  

- 韓文  

- 葡萄牙文 (巴西)  

- 俄文  

- 西班牙文 (西班牙)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> 延長安全性更新與 Configuration Manager

[延長安全性更新 (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) 計畫是需要在特定舊版 Microsoft 產品超過終止支援日期之後繼續使用該產品的最後選項。 例如，Windows 7。 它包括產品延伸支援終止日期之後最長三年的重大和/或重要安全性更新 (如 [Microsoft 安全回應中心 (MSRC)](https://www.microsoft.com/msrc) 所定義)。

已超出其支援生命週期的產品不支援搭配 Configuration Manager 使用。 這包括 ESU 計畫涵蓋的任何產品。 依 ESU 計畫發行的安全性更新將會發佈到 Windows Server Update Services (WSUS)。 這些更新將會出現在 Configuration Manager 主控台中。 雖然 ESU 計畫涵蓋的產品已不再支援搭配 Configuration Manager 使用，但 [Configuration Manager 最新分支的最新發行版本](../../servers/manage/updates.md#version-details)可用來部署及安裝依該計畫發行的 Windows 安全性更新。 最新發行版本也可以用來將 Windows 10 部署到執行 Windows 7 的裝置。

與 Windows 軟體更新管理或 OS 部署無關的用戶端管理功能，將不再於 ESU 計畫涵蓋的作業系統上測試，而且我們不保證這些功能將可繼續運作。 強烈建議您儘快升級或移轉到最新的作業系統版本，以接收用戶端管理支援。

## <a name="mac-computers"></a>Mac 電腦  

使用適用於 macOS 的 Configuration Manager 用戶端來管理 Apple Mac 電腦。  

Configuration Manager 媒體未隨附 macOS 用戶端安裝套件。 從 Microsoft 下載中心下載：[Microsoft Endpoint Configuration Manager - macOS 用戶端 (64 位元)](https://www.microsoft.com/download/details.aspx?id=100850) \(英文\)。  

如需詳細資訊，請參閱[如何將用戶端部署至 Mac](../../clients/deploy/deploy-clients-to-macs.md)。  

### <a name="requirements-and-limitations"></a>需求及限制

- 不支援在使用非根帳戶的電腦上，安裝或執行適用於 macOS 的 Configuration Manager 用戶端。 這麼做可能會導致重要服務無法正確執行。  

### <a name="supported-versions"></a>支援的版本

- **macOS Catalina (10.15)** (需要 Configuration Manager 站台 1910 版或更新版本，以及適用於 macOS 5.0.8742.1000 版或更新版本的 Configuration Manager 用戶端)

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Linux 和 UNIX 伺服器  

> [!Important]  
> Configuration Manager 1902 版已捨棄針對 Linux 和 UNIX 作為用戶端的支援。 淘汰隨 [1802 版](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support)宣布。 請考慮以 Microsoft Azure 管理來管理 Linux 伺服器。 Azure 解決方案具有廣泛的 Linux 支援，在大部分情況下都超越 Configuration Manager 的功能性，包括 Linux 的完整修補程式管理。

Configuration Manager 媒體未隨附 Linux 和 UNIX 用戶端安裝套件。 從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?LinkID=525184)下載**其他作業系統的用戶端**。 除了用戶端安裝套件之外，用戶端下載還會包括管理每部電腦上用戶端安裝的指令碼。  

### <a name="requirements-and-limitations"></a>需求及限制

- 若要檢閱適用於 Linux 和 UNIX 之用戶端的 OS 檔案相依性，請參閱 [Linux 和 UNIX 伺服器的用戶端部署先決條件](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)。  

- 如需支援的 Linux 或 UNIX 管理功能概觀，請參閱[如何將用戶端部署至 UNIX 和 Linux 伺服器](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

- 如需支援的 Linux 和 UNIX 版本，列出的版本會包含所有後續的次要版本。 例如，CentOS 第 6 版包括 CentOS 6.3。 同樣地，對使用 Service Pack (例如 SUSE Linux Enterprise Server 11 SP1) 之 OS 的支援也會包含該 OS 版本的後續 Service Pack。  

- 如需有關用戶端安裝套件和 Universal Agent 的資訊，請參閱[如何將用戶端部署至 UNIX 和 Linux 伺服器](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

### <a name="supported-versions"></a>支援的版本

使用指定的 .tar 檔可支援下列版本。  

#### <a name="aix"></a>AIX  

|版本|TAR 檔案|  
|-|-|  
|6\.1 版 (Power)|ccm-Aix61ppc.&lt;組建\>.tar|  
|7\.1 版 (Power)|ccm-Aix71ppc.&lt;組建\>.tar|  

#### <a name="centos"></a>CentOS  

|版本|TAR 檔案|  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

#### <a name="debian"></a>Debian  

|版本|TAR 檔案|  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;版本\>.tar|  
|第 8 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 8 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|版本|TAR 檔案|  
|-|-|  
|11iv3 版 IA64|ccm-HpuxB.11.31i64.&lt;組建\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|版本|TAR 檔案|  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|版本|TAR 檔案|  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

#### <a name="solaris"></a>Solaris  

|版本|TAR 檔案|  
|-|-|  
|第 10 版 x86|ccm-Sol10x86.&lt;組建\>.tar|  
|第 10 版 SPARC|ccm-Sol10sparc.&lt;組建\>.tar|  
|第 11 版 x86|ccm-Sol11x86.&lt;組建\>.tar|  
|第 11 版 SPARC|ccm-Sol11sparc.&lt;組建\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|版本|TAR 檔案|  
|-|-|  
|第 10 版 SP1 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 10 版 SP1 x86|ccm-Universalx64.&lt;組建\>.tar|  
|第 11 版 SP1 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 11 版 SP1 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 12 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|版本|TAR 檔案|  
|-|-|  
|10.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|10.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|12.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|12.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|14.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|14.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|16.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|16.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> 內部部署 MDM

Configuration Manager 具有內建功能，可用以管理內部部署的行動裝置，而不需安裝用戶端軟體。 如需詳細資訊，請參閱[使用內部部署基礎結構來管理行動裝置](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

### <a name="supported-operating-systems"></a>支援的作業系統

- **Windows 10 專業版** (x86、x64)  

- **Windows 10 專業企業版** (x86、x64)  

- **Windows 10 IoT 企業版** (x86、x64)  
    此版本包含長期維護通道 (LTSC)。 如需詳細資訊，請參閱 [Windows 10 IoT 企業版概觀](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) \(部分機器翻譯\)。<!--SCCMDocs issue 560-->  

- **Windows 10 IoT 行動裝置企業版**  

- **適用於 Surface Hub 的 Windows 10 團隊版**  

- **Windows 10 Mobile**  

- **Windows 10 行動裝置企業版**  

    > [!Note]
    > 在 Configuration Manager 中，對 Windows 10 行動裝置版和 Windows 10 行動裝置企業版的支援已淘汰。 如需詳細資訊，請參閱[已移除與已淘汰的 Configuration Manager 用戶端項目](../changes/deprecated/removed-and-deprecated-client.md)。


## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Exchange Server 連接器  

Configuration Manager 支援有限制地管理連線至您 Exchange Server 的裝置，而不需要安裝 Configuration Manager 用戶端。 如需詳細資訊，請參閱[使用 Configuration Manager 和 Exchange 管理行動裝置](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="supported-versions-of-exchange-server"></a>支援的 Exchange Server 版本

- **Exchange Online (Office 365)** ：此版本包括 Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** 或 **Exchange Server 2010 SP2**
