---
title: Microsoft Intune 中 Windows 10 的裝置限制設定 | Microsoft Docs
description: 查看有關在 Windows 10 和更新版本的裝置上建立裝置限制的所有設定及其描述的清單。 使用組態設定檔中的這些設定，在 Microsoft Intune 中控制螢幕擷取畫面、密碼要求、Kiosk 設定、市集中的應用程式、Microsoft Edge 瀏覽器、Microsoft Defender、雲端存取及開始功能表等。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f469d9646fad3b247743b6017f0ecbc7917f2cdf
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311160"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>使用 Intune 來允許或限制功能的 Windows 10 (和更新版本) 裝置設定

本文列出並描述您可以在 Windows 10 和更新版本裝置上控制的所有不同設定。 作為行動裝置管理 (MDM) 解決方案的一部分，請使用這些設定來允許或停用功能、設定密碼規則、自訂鎖定畫面、使用 Microsoft Defender，以及執行其他作業。

這些設定會新增至 Intune 裝置組態設定檔，然後指派或部署到您的 Windows 10 裝置。

> [!Note]
> 並非所有版本的 Windows 都提供全部選項。 若要查看支援的版本，請參閱 [Policy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (原則 CSP) (開啟另一個 Microsoft 網站)。

## <a name="before-you-begin"></a>開始之前

[建立 Windows 10 裝置的限制設定檔](device-restrictions-configure.md#create-the-profile)。

## <a name="app-store"></a>App Store

這些設定使用 [ApplicationManagement 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement)，它也會列出支援的 Windows 版本。

- **App Store (僅限行動裝置版)** ：[封鎖] 會防止使用者在行動裝置上存取 App Store。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者存取 App Store。
- **自動更新來自市集的應用程式**：[封鎖] 會防止自動從 Microsoft Store 安裝更新。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許自動更新從 Microsoft Store 安裝的應用程式。

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate) \(部分機器翻譯\)

- **安裝信任的應用程式**：選擇是否可以安裝非 Microsoft Store 應用程式，也稱為側載。 側載是安裝、然後執行或測試未經 Microsoft Store 認證的應用程式。 例如，僅公司內部使用的應用程式。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **封鎖**：防止側載。 無法安裝非 Microsoft Store 應用程式。
  - **允許**：允許側載。 可以安裝非 Microsoft Store 應用程式。

- **開發人員解除鎖定**：允許 Windows 開發人員設定，例如允許使用者修改側載的應用程式。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **封鎖**：防止開發人員模式和側載應用程式。
  - **允許**：允許開發人員模式和側載應用程式。

  [啟用您的裝置用於開發](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)有這項功能的詳細資訊。
  
  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps) \(部分機器翻譯\)

- **共用的使用者應用程式資料**：選擇 [允許]，則應用程式資料可供相同裝置的不同使用者共用，也可與該應用程式的其他執行個體共用。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會防止與相同應用程式的其他使用者及其他執行個體共用資料。

  [ApplicationManagement/AllowSharedUserAppData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata) \(部分機器翻譯\)

- **僅使用私人市集**：[允許] 僅允許從私人市集下載應用程式，不會從包括零售目錄在內的公用儲存區下載應用程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許從私人市集和公用市集下載應用程式。

  [ApplicationManagement/RequirePrivateStoreOnly CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly) \(部分機器翻譯\)

- **啟動來自市集的應用程式**：[封鎖] 會停用預先安裝於裝置上，或是從 Microsoft Store 下載的所有應用程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許開啟這些應用程式。

  [ApplicationManagement/DisableStoreOriginatedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps) \(部分機器翻譯\)

- **將應用程式資料安裝在系統磁碟區**：[封鎖] 會阻止應用程式將資料儲存在裝置的系統磁碟區上。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許應用程式將資料儲存在系統磁碟區。

  [ApplicationManagement/RestrictAppDataToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume) \(部分機器翻譯\)

- **將應用程式安裝在系統磁碟機**：[封鎖] 會防止應用程式安裝在裝置的系統磁碟機上。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許應用程式安裝在系統磁碟機。

  [ApplicationManagement/RestrictAppToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume) \(部分機器翻譯\)

- **遊戲 DVR (僅限桌面版)** ：[封鎖] 會停用 Windows 遊戲錄影和廣播。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許遊戲錄影和廣播。

  [ApplicationManagement/AllowGameDVR CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr) \(部分機器翻譯\)

- **僅限來自 Store 的應用程式**：此設定會決定使用者從 Microsoft Store 以外位置安裝應用程式時的使用者體驗。 其不會防止從 USB 裝置、網路共用或其他非網際網路來源安裝內容。 使用值得信任的瀏覽器，協助確保這些保護如預期般運作。

  選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者從 Microsoft Store 以外的位置安裝應用程式，包括其他原則設定中定義的應用程式。  
  - **任何位置**：關閉應用程式建議，並允許使用者從任何位置安裝應用程式。  
  - **僅限 Store**：意圖是要防止您的使用者裝置在從網際網路下載可執行內容時，受到惡意內容影響。 當使用者嘗試從網際網路安裝應用程式時，系統會封鎖安裝。 使用者會看到一則訊息，建議他們從 Microsoft Store 下載應用程式。
  - **建議**：從 Microsoft Store 中提供的網頁安裝應用程式時，使用者會看到一則訊息，建議其從市集下載該應用程式。  
  - **優先使用 Store**：當使用者從 Microsoft Store 以外位置安裝應用程式時，會發出警告。

  [SmartScreen/EnableAppInstallControl CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **由使用者控制安裝**：[封鎖] 會防止使用者變更通常保留給系統管理員的安裝選項，例如輸入目錄以安裝檔案。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，Windows Installer 可能會防止使用者變更這些安裝選項，並略過一些 Windows Installer 安全性功能。

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall) \(英文\)

- **以較高的權限安裝應用程式**：[封鎖] 會指示 Windows Installer 在系統上安裝任何程式時使用較高的權限。 這些權限會延伸至所有程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，系統可能會在安裝系統管理員未部署或提供的程式時，套用目前使用者的權限。

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges) \(英文\)

- **啟動應用程式**：輸入當使用者登入裝置後要開啟的應用程式清單。 請務必使用 Windows 應用程式的套件系列名稱 (PFN) 清單 (以分號分隔)。 若要使此原則生效，Windows 應用程式中的資訊清單必須使用啟動工作。

  [ApplicationManagement/LaunchAppAfterLogOn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon) \(英文\)

## <a name="cellular-and-connectivity"></a>行動數據與連線

這些設定使用[連線原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity)和 [Wi-Fi 原則](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi) CSP，它也會列出支援的 Windows 版本。

- **行動數據頻道**：當使用者連線到行動電話通訊網路時，選擇是否讓使用者使用瀏覽網頁之類的資料。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 使用者可以將其關閉。
  - **封鎖**：不允許行動數據頻道。 終端使用者無法開啟該設定。
  - **允許 (無法編輯)** ：允許行動數據頻道。 終端使用者無法關閉它。

- **數據漫遊**：[封鎖] 防止裝置上的行動數據漫遊。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，存取資料時可允許網路之間的漫遊。
- **透過行動電話通訊網路的 VPN**：[封鎖] 防止裝置在連線到行動電話通訊網路時存取 VPN 連線。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 VPN 使用包括行動電話在內的任何連線。
- **透過行動電話通訊網路的 VPN 漫遊**：[封鎖] 會阻止裝置在行動電話通訊網路漫遊時存取 VPN 連線。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許在漫遊時的 VPN 連線。
- **連線的裝置服務**：[封鎖] 會停用連線的裝置平台 (CDP) 元件。 CDP 能夠探索並連線到其他裝置 (透過藍牙/區域網路或雲端) 來支援遠端應用程式啟動、遠端傳訊、遠端應用程式工作階段，以及其他跨裝置體驗。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許連線的裝置服務，這可探索並連線到其他藍牙裝置。
- **NFC**：[封鎖] 防止近距離無線通訊 (NFC) 功能。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者啟用並設定裝置上的 NFC 功能。
- **Wi-Fi**：[封鎖] 防止使用者在裝置上啟用、設定及使用 Wi-Fi 連線。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 Wi-Fi 連線。
- **自動連線至 Wi-Fi 熱點**：[封鎖] 防止裝置自動連線至 Wi-Fi 熱點。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓裝置自動連線到免費 Wi-Fi 熱點，並自動接受任何連線的條款和條件。
- **手動設定 Wi-Fi**：[封鎖] 防止裝置連線至 MDM 伺服器安裝網路外的 Wi-Fi。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者新增及設定自己的 Wi-Fi 連線網路 SSID。
- **Wi-Fi 掃描間隔**：輸入裝置掃描 Wi-Fi 網路的頻率。 輸入 1 (最頻繁) 到 500 (最不頻繁) 的值。 預設值為 `0` (零)。

### <a name="bluetooth"></a>Bluetooth

這些設定使用[藍牙原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth)，其也會列出支援的 Windows 版本。

- **藍牙**：[封鎖] 防止使用者啟用藍牙。 [未設定] (預設) 允許在裝置上使用藍牙。
- **藍牙探索**：[封鎖] 防止其他藍牙啟用的裝置探索此裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許其他具備藍牙功能的裝置 (例如耳機) 探索此裝置。

  [Bluetooth/AllowDiscoverableMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **藍牙預先配對**：[封鎖] 防止特定的藍牙裝置與主機裝置自動配對。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許與主機裝置自動配對。

  [Bluetooth/AllowPrepairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **藍牙通知**：[封鎖] 防止裝置傳送出藍牙通知。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許裝置送出藍牙公告。

  [Bluetooth/AllowAdvertising CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **藍牙允許的服務**：以十六進位字串，**新增**允許的藍牙服務和設定檔清單，例如 `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`。

  [ServicesAllowedList usage guide](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) (ServicesAllowedList 使用指南) 有服務清單的詳細資訊。

  [Bluetooth/ServicesAllowedList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>雲端與儲存體

這些設定使用[帳戶原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts)，其也會列出支援的 Windows 版本。

> [!IMPORTANT]
> 封鎖或停用這些 Microsoft 帳戶設定可能會影響需要使用者登入 Azure AD 的註冊案例。 例如，您使用的是 [AutoPilot 白手套](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove)。 一般而言，使用者會看見 Azure AD 登入視窗。 當這些設定設定為 [封鎖] 或 [停用] 時，可能不會顯示 Azure AD 登入選項。 相反地，系統會要求使用者接受 EULA，並建立本機帳戶 (這可能不是您想要的)。

- **Microsoft 帳戶**：[封鎖] 會防止使用者建立 Microsoft 帳戶與裝置的關聯。 [封鎖] 可能也會影響一些註冊案例，這些案例需依賴使用者才能完成註冊程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許新增及使用 Microsoft 帳戶。
- **非 Microsoft 帳戶**：[封鎖] 會防止使用者以使用者介面新增非 Microsoft 帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者新增未與 Microsoft 帳戶關聯的電子郵件帳戶。
- **Microsoft 帳戶的設定同步**：[封鎖]  會防止與 Microsoft 帳戶關聯的裝置和應用程式設定在裝置之間進行同步處理。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許此同步處理。
- **Microsoft 帳戶登入小幫手**：此 OS 服務可讓使用者登入其 Microsoft 帳戶。 根據預設，OS 可能允許使用者啟動和停止 **Microsoft 帳戶登入小幫手** (wlidsvc) 服務。
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者啟動和停止 **Microsoft 帳戶登入小幫手** (wlidsvc) 服務。
  - **Disabled**：將 Microsoft 登入小幫手服務 (wlidsvc) 設定為 [已停用]，並防止使用者手動將其啟動。

      [停用] 可能也會影響一些註冊案例，這些案例需依賴使用者才能完成註冊。 例如，您使用的是 [AutoPilot 白手套](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove)。 一般而言，使用者會看見 Azure AD 登入視窗。 當設定為 [停用] 時，可能不會顯示 [Azure AD 登入] 選項。 相反地，系統會要求使用者接受 EULA，並建立本機帳戶 (這可能不是您想要的)。

## <a name="cloud-printer"></a>雲端印表機

這些設定使用 [EnterpriseCloudPrint 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint)，其也會列出支援的 Windows 版本。

- **印表機探索 URL**：輸入用於尋找雲端印表機的 URL。 例如，輸入 `https://cloudprinterdiscovery.contoso.com`。
- **印表機存取授權 URL**：輸入用於取得 OAuth 權杖的驗證端點 URL。 例如，輸入 `https://azuretenant.contoso.com/adfs`。
- **Azure 原生用戶端應用程式 GUID**：輸入經允許可從 OAuthAuthority 取得 OAuth 權杖的用戶端應用程式 GUID。 例如，輸入 `E1CF1107-FF90-4228-93BF-26052DD2C714`。
- **列印服務資源 URI**：輸入 Azure 入口網站中所設定列印服務的 OAuth 資源 URI。 例如，輸入 `http://MicrosoftEnterpriseCloudPrint/CloudPrint`。
- **要查詢的印表機上限**：輸入您要接受查詢的印表機數目上限。 預設值為 `20`。
- **印表機探索服務資源 URI**：輸入 Azure 入口網站中所設定印表機探索服務的 OAuth 資源 URI。 例如，輸入 `http://MopriaDiscoveryService/CloudPrint`。

> [!TIP]
> 設定 [Windows Server 混合式雲端列印](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview)之後，您可以設定這些設定，然後將它們部署到 Windows 裝置。

## <a name="control-panel-and-settings"></a>控制台和設定

- **設定應用程式**：[封鎖] 會防止使用者存取 Windows 設定應用程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者在裝置上開啟此設定。
  - **系統**：[封鎖] 防止存取 [設定] 應用程式的 [系統] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
    - **修改電源與睡眠設定** (僅限桌面版)：[封鎖] 會防止使用者變更裝置上的電源及睡眠設定。 [未設定] (預設) 可讓使用者變更電源與睡眠設定。
  - **裝置**：[封鎖] 防止存取裝置 [設定] 應用程式的 [裝置] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **網路網際網路**：[封鎖] 防止存取裝置 [設定] 應用程式的 [網路與網際網路] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **個人化**：[封鎖] 防止存取裝置 [設定] 應用程式的 [個人化] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **應用程式**：[封鎖] 防止存取裝置 [設定] 應用程式的 [應用程式] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **帳戶**：[封鎖] 防止存取裝置 [設定] 應用程式的 [帳戶] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **時間與語言**：[封鎖] 防止存取裝置 [設定] 應用程式的 [時間與語言] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
    - **修改系統時間**：[封鎖] 會防止使用者變更裝置的日期和時間設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 使用者可以變更這些設定。
    - **修改地區設定** (僅限桌面版)：[封鎖] 會防止使用者變更裝置上的區域設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 使用者可以變更這些設定。
    - **修改語言設定 (僅限桌面版)** ：[封鎖] 會防止使用者變更裝置上的語言設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 使用者可以變更這些設定。

      [設定原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **遊戲**：[封鎖] 防止存取裝置 [設定] 應用程式的 [遊戲] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **輕鬆存取**：[封鎖] 防止存取裝置 [設定] 應用程式的 [輕鬆存取] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **隱私權**：[封鎖] 防止存取裝置 [設定] 應用程式的 [隱私權] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
  - **更新與安全性**：[封鎖] 防止存取裝置 [設定] 應用程式的 [更新與安全性] 區域。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

## <a name="display"></a>顯示

這些設定使用[顯示原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display)，其也會列出支援的 Windows 版本。

GDI DPI 縮放比例會讓非 DPI 感知的應用程式變成依監視器 DPI 感知。

- **開啟應用程式的 GDI 調整功能**：**新增**您要開啟 GDI DPI 縮放比例的舊版應用程式。 例如，輸入 `filename.exe` 或 `%ProgramFiles%\Path\Filename.exe`。

  您清單中的所有舊版應用程式都會開啟 GDI DPI 縮放比例。

- **關閉應用程式的 GDI 調整功能**：**新增**您要關閉 GDI DPI 縮放比例的舊版應用程式。 例如，輸入 `filename.exe` 或 `%ProgramFiles%\Path\Filename.exe`。

  您清單中的所有舊版應用程式都會關閉 GDI DPI 縮放比例。

您也可以 [匯入] 具有應用程式清單的 .csv 檔案。

## <a name="general"></a>一般

這些設定使用[體驗原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience)，它也會列出支援的 Windows 版本。 

- **螢幕擷取** (僅限行動裝置版)：[封鎖] 會防止使用者在裝置上取得螢幕擷取畫面。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **複製並貼上 (僅限行動裝置版)** ：[封鎖] 會防止使用者在裝置的應用程式之間使用複製並貼上。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **手動取消註冊**：[封鎖] 會禁止使用者使用裝置上的工作場所控制台刪除工作場所帳戶。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  如果電腦已加入 Azure AD，且啟用自動註冊，則不會套用此原則設定。

- **手動安裝根憑證** (僅限行動裝置版)：[封鎖] 會防止使用者手動安裝根憑證及中繼 CAP 憑證。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **相機**：[封鎖] 會防止使用者在裝置上使用相機。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許存取裝置相機。

  Intune 只管理裝置相機的存取權。 其無權存取圖片或影片。

  [相機 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **OneDrive 檔案同步**：[封鎖] 會防止使用者將裝置中的檔案同步至 OneDrive。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [System/DisableOneDriveFileSync CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **抽取式存放裝置**：[封鎖] 會防止使用者使用外部存放裝置，如裝置的 SD 卡。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **地理位置**：[封鎖] 會禁止使用者開啟裝置的定位服務。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [System/AllowLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **網際網路共用**：[封鎖] 防止裝置共用網際網路連線。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **重設手機**：[封鎖] 會防止使用者在裝置上抹除或執行原廠重設。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **USB 連線**：[封鎖] 防止透過裝置的 USB 連線存取外部存放裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 這項設定不會影響 USB 充電。

  [Connectivity/AllowUSBConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **防竊模式** (僅限行動裝置版)：[封鎖] 會防止使用者選取裝置的防竊模式喜好設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **Cortana**：[封鎖] 會停用裝置的 Cortana 語音助理。 Cortana 關閉時，使用者仍可搜尋，在裝置上尋找項目。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許 Cortana。

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **錄音** (僅限行動裝置版)：[封鎖] 會防止使用者在裝置上使用裝置語音錄音機。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許應用程式的錄音。
- **修改裝置名稱** (僅限行動裝置版)：[封鎖] 會防止使用者變更裝置名稱。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **新增佈建套件**：[封鎖] 防止執行階段設定代理程式在裝置上安裝佈建套件。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **移除佈建套件**：[封鎖] 防止執行階段設定代理程式移除裝置上的佈建套件。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **裝置探索**：[封鎖] 防止其他裝置找到此裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Experience/AllowDeviceDiscovery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **工作切換器** (僅限行動裝置版)：[封鎖] 防止在裝置上切換工作。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。
- **SIM 卡錯誤對話方塊** (僅限行動裝置版)：[封鎖] 在沒有偵測到 SIM 卡情況下會顯示於裝置上的錯誤訊息。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會顯示錯誤訊息。
- **Ink 工作區**：選擇使用者是否以及如何存取 Ink 工作區。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能會開啟 Ink 工作區，並允許使用者在鎖定畫面上方使用該工作區。
  - **在鎖定畫面上停用**：啟用 Ink 工作區，並開啟功能。 但是，使用者無法在鎖定畫面上方存取該工作區。
  - **Disabled**：停用 Ink 工作區的存取。 這會關閉功能。

  [WindowsInkWorkspace 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Autopilot 重設**：選擇 [允許]，讓具有系統管理權限的使用者能夠在裝置鎖定畫面使用 **CTRL + Win + R** 刪除所有使用者資料和設定。 裝置會自動重新設定並重新註冊以納入管理。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會禁用此功能。
- **要求使用者在裝置設定期間連線到網路**：選擇 [必要]，讓裝置在 Windows 設定期間先連線到網路，再通過 [網路] 頁面。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，即使 OS 不連線到網路，OS 仍可能允許使用者通過 [網路] 頁面。

  此設定會在下一次抹除或重設裝置時生效。 和任何其他 Intune 設定相似，裝置必須向 Intune 註冊並由 Intune 管理才能接收組態設定。 然而一旦註冊並接收原則，然後重設裝置後，便會在下一次 Windows 設定期間時實行設定。

  [TenantLockdown CSP](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **直接記憶體存取**：[封鎖] 會防止所有隨插即用 PCI 下游連接埠的直接記憶體存取 (DMA)，直到使用者登入 Windows 為止。 [啟用] (預設值) 會允許存取 DMA，就算使用者未登入也一樣。

  [DataProtection/AllowDirectMemoryAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **從 [工作管理員] 結束處理序**：此設定決定非系統管理員是否可以使用 [工作管理員] 來結束工作。 [封鎖] 可防止標準使用者 (非系統管理員) 使用 [工作管理員] 來結束裝置上的處理序或工作。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許標準使用者使用 [工作管理員] 結束處理序或工作。

  [TaskManager/AllowEndTask CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>鎖定畫面體驗

- **控制中心通知 (僅限行動裝置版)** ：[封鎖] 防止控制中心通知出現在裝置的鎖定畫面。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者選擇哪些應用程式可在鎖定畫面上顯示通知。

  [AboveLock/AllowActionCenterNotifications CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **鎖定畫面圖片 URL (僅限桌面版)** ：輸入 JPG、JPEG 或 PNG 格式圖片的 URL，這些圖片會作為 Windows 鎖定畫面桌布使用。 例如，輸入 `https://contoso.com/image.png`。 這項設定會鎖定映像，且以後不能變更。

  [個人化/LockScreenImageUrl CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **使用者可設定的畫面逾時 (僅限行動裝置版)** ：[允許] 可讓使用者設定畫面逾時。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能不會為使用者提供此選項。

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **鎖定畫面上的 Cortana** (僅限桌面版)：[封鎖] 會在裝置位於鎖定畫面上時防止使用者與 Cortana 互動。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許與 Cortana 的互動。

  [AboveLock/AllowCortanaAboveLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **鎖定畫面上的快顯通知**：[封鎖] 防止在裝置鎖定畫面上顯示快顯通知。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許這些通知。

  [AboveLock/AllowToasts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **畫面逾時 (僅限行動裝置版)** ：設定螢幕從鎖定到關閉的持續時間 (秒)。 支援的值為 11-1800。 例如，輸入 `300` 將此逾時設為 5 分鐘。

  [DeviceLock/ScreenTimeoutWhileLocked CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>訊息傳送

這些設定使用[傳訊原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging)，其中也會列出支援的 Windows 版本。

- **訊息同步 (僅限行動裝置版)** ：[封鎖] 會停用文字訊息的備份及還原，也會停用 Windows 裝置之間的訊息同步。 停用有利於防止資訊儲存在不受組織控制的伺服器上。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者變更這些設定，且可同步其訊息。
- **多媒體簡訊 (僅限行動裝置版)** ：[封鎖] 會停用裝置的多媒體訊息傳送和接收功能。 就企業而言，使用此原則停用裝置的多媒體訊息，作為稽核或管理需求的一部分。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 MMS 的傳送和接收。
- **RCS (僅限行動裝置版)** ：[封鎖] 會停用裝置上的 Rich Communication Services (RCS) 傳送和接收功能。 就企業而言，使用此原則停用裝置的 RCS，作為稽核或管理需求的一部分。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 RCS 的傳送和接收。

## <a name="microsoft-edge-browser"></a>Microsoft Edge 瀏覽器

這些設定使用[瀏覽器原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser)，它也會列出支援的 Windows 版本。

### <a name="use-microsoft-edge-kiosk-mode"></a>使用 Microsoft Edge kiosk 模式

可用設定會因您選擇的項目而變更。 選項包括：

- [否] (預設)：Microsoft Edge 並非正在 Kiosk 模式中執行。 您可以使用所有 Microsoft Edge 設定，且可進行變更和設定。
- **數位/互動式告示板 (單一應用程式 Kiosk)** ：篩選 Microsoft Edge 設定，只提供適用於數位/互動告示板 Microsoft Edge Kiosk 模式的設定，用於 Windows 10 單一應用程式 Kiosk。 選擇此設定，以全螢幕方式開啟 URL，並只顯示網站的內容。 [設定數位告示板](https://docs.microsoft.com/windows/configuration/setup-digital-signage)提供此功能的詳細資訊。
- **InPrivate 公開瀏覽 (單一應用程式 Kiosk)** ：篩選 Microsoft Edge 設定，只提供適用於 InPrivate 公開瀏覽 Microsoft Edge Kiosk 模式的設定，用於 Windows 10 單一應用程式 Kiosk。 執行 Microsoft Edge 的多分頁版本。
- **標準模式 (多應用程式 Kiosk)** ：篩選 Microsoft Edge 設定，只提供適用於標準 Microsoft Edge Kiosk 模式的設定。 執行具備所有瀏覽功能的 Microsoft Edge 完整版本。
- **公開瀏覽 (多應用程式 Kiosk)** :篩選 Microsoft Edge 設定，只提供適用於在 Windows 10 多應用程式 Kiosk 上公開瀏覽的設定。  執行 Microsoft Edge InPrivate 的多分頁版本。

> [!TIP]
> 如需這些選項作用的詳細資訊，請參閱 [Microsoft Edge Kiosk 模式設定類型](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types)。

此裝置限制設定檔直接與您使用 [Windows Kiosk 設定](kiosk-settings-windows.md)建立的 Kiosk 設定檔相關。 總括來說：

1. 建立 [Windows Kiosk 設定](kiosk-settings-windows.md)設定檔，來在 Kiosk 模式下執行裝置。 選取 Microsoft Edge 作為應用程式，並在 Kiosk 設定檔中設定 Microsoft Edge Kiosk 模式。
2. 建立本文中描述的裝置限制設定檔，並設定 Microsoft Edge 中允許的特定功能及設定。 請務必選擇和您在 Kiosk 設定檔 ([Windows Kiosk 設定](kiosk-settings-windows.md)) 中所選取項目相同的 Microsoft Edge Kiosk 模式類型。 

    [支援的 Kiosk 模式設定](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode)是良好資源。

> [!IMPORTANT] 
> 請務必將此 Microsoft Edge 設定檔指派給與您 Kiosk 設定檔 ([Windows Kiosk 設定](kiosk-settings-windows.md)) 相同的裝置。

[ConfigureKioskMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>[開始] 體驗

- **啟動 Microsoft Edge 並顯示**：選擇 Microsoft Edge 啟動時開啟的頁面。 選項包括：
  - **自訂起始畫面**：輸入起始畫面，例如 `http://www.contoso.com`。 Microsoft Edge 會載入您輸入的起始畫面。
  - **新索引標籤頁面**：Microsoft Edge 會載入您在 [新增索引標籤 URL] 設定中輸入的任何內容。
  - **上一個工作階段的頁面**：Microsoft Edge 會載入上一個工作階段的頁面。
  - **本機應用程式設定中的起始畫面**：Microsoft Edge 以 OS 所定義的預設起始畫面啟動。

- **允許使用者變更起始畫面**：[是] (預設) 可讓使用者變更起始畫面。 系統管理員可以使用 `EdgeHomepageUrls` 輸入使用者在開啟 Microsoft Edge 時預設看到的起始畫面。 [否] 會封鎖使用者變更起始畫面。
- **允許新索引標籤頁面上的 Web 內容**：設定為 [是] (預設) 時，Microsoft Edge 會開啟 [新索引標籤 URL] 設定中輸入的 URL。 如果 [新增索引標籤 URL]設定為空白，Microsoft Edge 會開啟 Microsoft Edge 設定中列出的新索引標籤頁面。 使用者可以變更它。 設定為 [否] 時，Microsoft Edge 會以空白頁開啟新的索引標籤。 使用者無法變更它。
- **新索引標籤 URL**：輸入要在新索引標籤頁面上開啟的 URL。 例如，輸入 `https://www.bing.com` 或 `https://www.contoso.com`。

- **首頁按鈕**：選擇選取 [首頁] 按鈕時所發生的情況。 選項包括：
  - **起始畫面**：開啟您在 [啟動 Microsoft Edge 並顯示] 設定中選擇的選項
  - **新索引標籤頁面**：開啟您在 [新索引標籤 URL] 設定中輸入的 URL。
  - **[首頁] 按鈕 URL**：輸入要開啟的 URL。 例如，輸入 `https://www.bing.com` 或 `https://www.contoso.com`。
  - **隱藏首頁按鈕**：隱藏 [首頁] 按鈕
- **允許使用者變更 [首頁] 按鈕**：[是] 可讓使用者變更 [首頁] 按鈕。 使用者變更會將任何的系統管理員設定覆寫為 [首頁] 按鈕。 [否] (預設) 會封鎖使用者變更系統管理員的 [首頁] 按鈕設定方式。
- **顯示首次執行體驗頁面 (僅限行動裝置版)** ：[是] (預設) 會顯示 Microsoft Edge 第一次使用的簡介頁面。 [否] 會在您第一次執行 Microsoft Edge 時阻止顯示簡介頁面。 這項功能可讓企業 (如註冊零輸出設定的組織) 封鎖這個頁面。
- **首次執行體驗 URL 清單位置** (僅限 Windows 10 行動裝置版)：輸入指向 XML 檔案的 URL，此檔案包含初次執行頁面 URL。 例如，輸入 `https://www.contoso.com/sites.xml`。

- **在閒置時間後重新整理瀏覽器**：輸入閒置時間數 (分鐘)，在經過此時時間後便會重新整理瀏覽器，範圍介於 0 到 1440 分鐘。 預設為 `5` 分鐘。 當設為 `0` (零) 時，瀏覽器便不會在閒置後重新整理。

  此設定只有在於 [InPrivate 公開瀏覽 (單一應用程式 Kiosk)](#use-microsoft-edge-kiosk-mode) 中執行時才可使用。

- **允許快顯視窗** (僅限桌面版)：[是] (預設) 允許網頁瀏覽器的快顯視窗。 [否] 防止瀏覽器顯示快顯視窗。
- **將內部網路流量傳送到 Internet Explorer** (僅限桌面版)：[是] 讓使用者可在 Internet Explorer 而不是 Microsoft Edge 中開啟內部網路網站。 這項設定是針對回溯相容性。 [否] (預設) 允許使用者使用 Microsoft Edge。
- **企業模式網站清單位置** (僅限桌面版)：輸入指向 XML 檔案的 URL，此檔案包含以企業模式開啟的網站清單。 使用者無法變更此清單。 例如，輸入 `https://www.contoso.com/sites.xml`。
- **在 Internet Explorer 中開啟網站時出現的訊息**：使用此設定將 Microsoft Edge 設定為在 Internet Explorer 11 中開啟網站之前顯示通知。 選項包括：
  - **不要顯示訊息**：使用 OS 預設行為，這可能不會顯示訊息。
  - **顯示網站在 Internet Explorer 11 中開啟的訊息**：在 IE 中開啟網站時顯示訊息。 在 IE 中開啟網站。 
  - **顯示訊息並提供在 Microsoft Edge 中開啟網站的選項**：在 Microsoft Edge 中開啟網站時顯示訊息。 此訊息包含**繼續使用 Microsoft Edge** 連結，因此使用者可以選擇 Microsoft Edge 而非 IE。

  > [!IMPORTANT]
  > 此設定要求您使用 [企業模式網站清單位置] 設定、[將內部網路流量傳送到 Internet Explorer] 設定，或兩者都使用。

- **允許 Microsoft 相容性清單**：[是] (預設) 允許使用 Microsoft 相容性清單。 [否] 防止 Microsoft Edge 中的 Microsoft 相容性清單。 Microsoft 的此清單可協助 Microsoft Edge 正確顯示具有已知的相容性問題的網站。
- **預先載入起始畫面與新索引標籤頁面**：[是] (預設) 會使用 OS 預設行為，這可能表示要預先載入這些頁面。 預先載入可將啟動 Microsoft Edge 的時間降至最低，並載入新的索引標籤。 [否] 會防止 Microsoft Edge 預先載入起始畫面與新索引標籤頁面。
- **預先啟動起始畫面與新索引標籤頁面**：[是] (預設) 會使用 OS 預設行為，這可能表示要預先啟動這些頁面。 預先啟動有助於 Microsoft Edge 的效能，並將啟動 Microsoft Edge 所需的時間降至最低。 [否]會防止 Microsoft Edge 預先啟動起始畫面與新索引標籤頁面。

### <a name="favorites-and-search"></a>我的最愛和搜尋

- **顯示我的最愛列**：選擇任何 Microsoft Edge 頁面上我的最愛列設定內容。 選項包括：
  - **在 [開始] 和新索引標籤頁面上**：當 Microsoft Edge 啟動時，在所有的索引標籤頁面中顯示 [我的最愛] 列。 使用者無法變更此設定。
  - **在所有頁面上**：在所有頁面上顯示我的最愛列。 使用者無法變更此設定。
  - **隱藏**：在所有頁面上隱藏我的最愛列。 使用者無法變更此設定。
- **允許變更我的最愛**：[是] (預設) 會使用作業系統預設，讓使用者變更清單。 [否] 會防止使用者新增、匯入、排序或編輯 [我的最愛] 清單。
  - **我的最愛清單**：將 URL 清單新增至我的最愛檔案。 例如：新增 `http://contoso.com/favorites.html`。
- **在 Microsoft 瀏覽器之間同步我的最愛** (僅限桌面版)：[是] 可強制 Windows 在 Internet Explorer 與 Microsoft Edge 之間同步我的最愛。 在瀏覽器之間共用對我的最愛的新增、刪除、修改及順序變更。  [否] (預設) 會使用作業系統預設值，這可讓使用者選擇在瀏覽器間同步我的最愛。
- **預設搜尋引擎**：選擇裝置上的預設搜尋引擎。 使用者隨時可以變更此值。 選項包括：
  - 用戶端 Microsoft Edge 設定中的搜尋引擎
  - Bing
  - Google
  - Yahoo
  - 自訂值：在 **OpenSearch Xml URL** 中，至少輸入 XML 檔案包含簡短名稱的 HTTPS URL 和搜尋引擎的 URL。 例如，輸入 `https://www.contoso.com/opensearch.xml`。
- **顯示搜尋建議**：[是] (預設) 可讓搜尋引擎在您輸入搜尋片語時建議網站。 [否] 會防止此功能。
- **允許變更搜尋引擎**：[是] (預設) 可讓使用者在 Microsoft Edge 中新增新的搜尋引擎，或是變更預設搜尋引擎。 選擇 [否] 以防止使用者自訂搜尋引擎。

  此設定只有在於[標準模式 (多應用程式 Kiosk)](#use-microsoft-edge-kiosk-mode) 中執行時才可使用。

### <a name="privacy-and-security"></a>隱私權和安全性

- **允許 InPrivate 瀏覽**：[是] (預設) 允許在 Microsoft Edge 中使用 InPrivate 瀏覽。 關閉所有 InPrivate 索引標籤之後，Microsoft Edge 會刪除裝置的瀏覽資料。 [否] 會防止使用者開啟 InPrivate 瀏覽工作階段。
- **儲存瀏覽歷程記錄**：[是] (預設) 允許儲存 Microsoft Edge 的瀏覽歷程記錄。 [否] 防止儲存瀏覽歷程記錄。
- **在結束時清除瀏覽資料** (僅限桌面版)：[是] 會在使用者結束 Microsoft Edge 時，清除歷程記錄和瀏覽資料。 [否] (預設) 會使用作業系統預設值，這可能會快取瀏覽資料。
- **在使用者裝置之間同步瀏覽器設定**：選擇在裝置之間同步瀏覽器設定的方式。 選項包括：
  - **允許**：允許在使用者的裝置之間同步 Microsoft Edge 瀏覽器設定
  - **封鎖並啟用使用者覆寫**：禁止在使用者的裝置之間同步 Microsoft Edge 瀏覽器設定。 使用者可以覆寫此設定。
  - **封鎖**：封鎖在使用者裝置之間同步處理 Microsoft Edge 瀏覽器設定。 使用者無法覆寫此設定。

選取 [禁止並允許使用者覆寫] 後，使用者可以覆寫管理員指定。

- **允許密碼管理員**：[是] (預設) 允許 Microsoft Edge 自動使用密碼管理員，讓使用者儲存及管理裝置上的密碼。 [否] 防止 Microsoft Edge 使用密碼管理員。
- **Cookie**：選擇在網頁瀏覽器中處理 Cookie 的方式。 選項包括：
  - **允許**：Cookie 會儲存在裝置上。
  - **封鎖所有 Cookie**：Cookie 不會儲存在裝置上。
  - **只封鎖第三方 Cookie**：協力廠商或合作對象 Cookie 不會儲存在裝置上。
- **允許表單自動填滿**：[是] (預設) 讓使用者變更瀏覽器的自動完成設定，自動填入表單欄位。 [否] 會停用 Microsoft Edge 的自動填寫功能。
- **傳送不追蹤標頭**：[是] 會向要求追蹤資訊的網站傳送不追蹤標頭 (建議選項)。 [否] (預設) 不會傳送讓網站追蹤使用者的標頭。 使用者可以進行此設定。
- **顯示 WebRTC localhost IP 位址**：[是] (預設) 允許使用者在使用此通訊協定通話時顯示 localhost IP 位址。 [否] 防止顯示使用者的 localhost IP 位址。 
- **允許收集動態磚資料**：[是] (預設) 允許 Microsoft Edge 收集釘選到 [開始] 功能表的動態磚資訊。 [否] 防止收集這項資訊，這可能會讓使用者體驗受限。
- **使用者可以覆寫憑證錯誤**：[是] (預設) 允許使用者存取有安全通訊端層/傳輸層安全性 (SSL/TLS) 錯誤的網站。 [否] (建議項目，可提高安全性) 防止使用者存取有 SSL 或 TLS 錯誤的網站。

### <a name="additional"></a>其他

- **允許 Microsoft Edge 瀏覽器** (僅限行動裝置版)：[是] (預設) 允許在裝置上使用 Microsoft Edge 網頁瀏覽器。 [否] 會防止在裝置上使用 Microsoft Edge。 如果您選擇 [否]，則其他的個別設定僅適用於 Desktop。
- **允許網址列下拉式清單**：[是] (預設) 允許 Microsoft Edge 顯示網址列下拉式清單，其中包含建議清單。 [否] 可阻止 Microsoft Edge 在您鍵入時，於下拉式清單中顯示建議清單。 設定為 [否] 時，您：
  - 協助將 Microsoft Edge 與 Microsoft 服務之間的網路頻寬降到最低。
  - 停用 Microsoft Edge > [設定] 中的 [在我輸入的同時顯示搜尋與網站建議]。
- **允許全螢幕模式**：[是] (預設) 允許 Microsoft Edge 使用全螢幕模式，這樣會只顯示 Web 內容並隱藏 Microsoft Edge UI。 [否] 防止 Microsoft Edge 的全螢幕模式。
- **允許關於旗標頁面**：[是] (預設) 會使用 OS 預設值，這可能會允許存取 `about:flags` 頁面。 `about:flags` 頁面可讓使用者變更開發人員設定並啟用實驗功能。 [否] 會防止使用者存取 Microsoft Edge 的 `about:flags` 頁面。
- **允許開發人員工具**：[是] (預設) 允許使用者以 F12 開發人員工具來建置和偵錯預設網頁。 [否] 會防止使用者使用 F12 開發人員工具。
- **允許 JavaScript**：[是] (預設) 允許在 Microsoft Edge 瀏覽器中執行 JavaScript 等指令碼。 [否] 防止在瀏覽器中執行 Java 指令碼。
- **使用者可以安裝延伸模組**：[是] (預設) 允許使用者在裝置上安裝 Microsoft Edge 延伸模組。 [否] 會防止安裝。
- **允許側載開發人員延伸模組**：[是] (預設) 會使用 OS 預設值，這可能會允許側載。 側載會安裝並執行未經驗證的延伸模組。 [否] 防止 Microsoft Edge使用 [載入延伸模組] 功能側載。 它不會防止使用 PowerShell 等其他方式側載延伸模組。
- **必要的延伸模組**：選擇 Microsoft Edge 中的使用者無法關閉哪些延伸模組。 輸入套件系列名稱，然後選取 [新增]。 [尋找每個應用程式 VPN 的套件系列名稱 (PFN)](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) 提供一些指引。

  您也可以**匯入** CSV 檔案，其中包含套件系列名稱。 或者，[匯出] 您輸入的套件系列名稱。

## <a name="network-proxy"></a>網路 Proxy

這些設定使用 [NetworkProxy 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp)，它也會列出支援的 Windows 版本。

- **自動偵測 Proxy 設定**：[封鎖] 會停用裝置，使其無法自動偵測 Proxy 自動設定 (PAC) 指令碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會啟用此功能，且裝置會嘗試尋找 PAC 指令碼的路徑。
- **使用 Proxy 指令碼**：選擇 [允許] 輸入 PAC 指令碼路徑以設定 Proxy 伺服器。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能不讓您輸入 PAC 指令碼的 URL。
  - **設定指令碼位址 URL**：輸入您想要用於設定 Proxy 伺服器的 PAC 指令碼 URL。
- **使用手動 Proxy 伺服器**：選擇 [允許] 手動輸入 Proxy 伺服器的名稱或 IP 位址及 TCP 通訊埠號碼。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能不讓您手動輸入 Proxy 伺服器的詳細資料。
  - **位址**：輸入 Proxy 伺服器的名稱或 IP 位址。
  - **連接埠號碼**：輸入 Proxy 伺服器的連接埠號碼。
  - **Proxy 例外狀況**：輸入任何不得使用 Proxy 伺服器的 URL。 請使用分號 (`;`) 來分隔每個項目。
  - **為本機位址略過 Proxy 伺服器**：[允許] 不會將 Proxy 伺服器用在本機內部網路位址。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能在內部網路使用本機位址的 Proxy 伺服器。

## <a name="password"></a>密碼

這些設定使用 [DeviceLock 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock)，它也會列出支援的 Windows 版本。

- **密碼**：[需要] 會強制使用者輸入密碼，才能存取裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會允許不用密碼即可存取裝置。 僅適用於本機帳戶。 網域帳戶密碼仍然由 Active Directory (AD) 和 Azure AD 設定。

  [DeviceLock/DevicePasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **必要的密碼類型**：選擇密碼的類型。 選項包括：
    - **未設定**：Intune 不會變更或更新此設定。 根據預設，OS 可能允許密碼包含數字和字母。
    - **英數字元**：密碼必須混合數字和字母。
    - **數字**：密碼只能是數字。

    [DeviceLock/AlphanumericDevicePasswordRequired CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **密碼長度下限**：輸入所需的字元數下限，從 4 到 16。 例如，輸入 `6` 表示密碼長度至少需要六個字元。 根據預設，OS 可能會將密碼設為 `4`。
  
    [DeviceLock/MinDevicePasswordLength CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > 在 Windows 桌面上變更密碼需求時，使用者會在下次登入時受到影響，因為此時裝置會從閒置變成作用中。 系統仍會提示密碼符合需求的使用者變更其密碼。

  - **登入失敗幾次後即抹除裝置**：輸入抹除裝置前允許的錯誤密碼次數，最多 11 次。 您輸入的有效號碼視版本而定。 [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) 會列出支援的值。 `0` (零) 可停用裝置抹除功能。

    此設定因版本不同也會有不同影響。 如需此設定的特定詳細資訊，請參閱 [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) \(英文\)。

  - **停止活動最多幾分鐘後鎖定螢幕**：輸入裝置必須閒置多久的時間，才會鎖定螢幕。 例如，輸入 `5` 會在閒置 5 分鐘後鎖定裝置。 當設定為 [未設定] 時，Intune 則不會變更或更新此設定。 根據預設，OS 可能會將此值設定為 `0` (零) (非逾時)。

    [DeviceLock/MaxInactivityTimeDeviceLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **密碼到期 (天數)** ：輸入裝置必須變更密碼的天數，從 1 到 365。 例如，輸入 `90`，密碼會在 90 天後到期。 當此值為空白時，Intune 則不會變更或更新此設定。 根據預設，OS 可能會將此值設定為 `0` (零) (非到期)。

    [DeviceLock/DevicePasswordExpiration CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **避免重複使用以前用過的密碼**：輸入不得重複使用的舊密碼，從 1 到 24。 列如，輸入 `5` 讓使用者無法將新密碼設定為其目前密碼或之前使用過的四個密碼之一。 當此值為空白時，Intune 則不會變更或更新此設定。

    [DeviceLock/DevicePasswordHistory CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **裝置從閒置狀態回復時需要密碼** (行動裝置和全像攝影)：[需要] 會強制使用者輸入密碼，才能在閒置後解除鎖定裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 在閒置後不需要 PIN 或密碼。

    [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **簡單密碼**：[封鎖] 會防止使用者建立簡單密碼，例如 `1234` 或 `1111`。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會讓使用者建立簡單密碼。 此設定也會封鎖圖片密碼的使用。

    [DeviceLock/AllowSimpleDevicePassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **在 AADJ 期間的自動加密**：[封鎖] 會防止當裝置加入 Azure AD，並準備將裝置供初次使用時啟動自動 BitLocker 裝置加密。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會啟用加密。

  請參閱 [BitLocker 裝置加密](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption)。

  [Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **聯邦資訊處理標準 (FIPS) 原則**：[允許] 會使用聯邦資訊處理標準 (FIPS) 原則，該標準是美國政府針對加密、雜湊和簽署提出的標準。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 FIPS。

  [Cryptography/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Windows Hello 裝置驗證**：[允許] 使用者使用 Windows Hello 隨附裝置，例如手機、健身手環或 IoT 裝置登入 Windows 10 電腦。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會防止 Windows Hello 隨附裝置進行驗證。

  [Authentication/AllowSecondaryAuthenticationDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **慣用的 Azure AD 租用戶網域**：輸入您 Azure AD 組織中現有的網域名稱。 當使用者在此網域登入時，他們便不需要鍵入網域名稱。 例如，輸入 `contoso.com`。 `contoso.com` 網域中的使用者可以使用其使用者名稱登入，例如 `abby`，而非 `abby@contoso.com`。

  [Authentication/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>個別應用程式的隱私權例外狀況

[新增] 應用程式的隱私權行為應與「預設隱私權」中定義的行為不同。

- **套件名稱**：應用程式套件系列名稱。
- **應用程式名稱**：應用程式的名稱。

### <a name="exceptions"></a>例外狀況

- **帳戶資訊**：定義此應用程式能否存取使用者名稱、圖片及其他連絡人資訊。
- **背景應用程式**：定義此應用程式能否在背景執行。
- **行事曆**：定義此應用程式能否存取行事曆。
- **通話記錄**：定義此應用程式能否存取我的通話記錄。
- **相機**：定義此應用程式能否存取相機。
- **連絡人**：定義此應用程式能否存取連絡人。
- **電子郵件**：定義此應用程式能否存取及傳送電子郵件。
- **位置**：定義此應用程式能否存取位置資訊。
- **訊息中心**：定義此應用程式能否讀取或傳送文字或多媒體簡訊。
- **麥克風**：定義此應用程式能否使用麥克風。
- **動作**：定義此應用程式能否存取裝置動作資訊。
- **通知**：定義此應用程式能否存取通知。
- **電話**：定義此應用程式能否存取手機。
- **無線通訊**：有些應用程式會在您的裝置上使用無線電通訊 (例如，藍牙) 來傳送及接收資料，因此必須開啟或關閉這些無線通訊。 定義此應用程式能否控制這些無線電波。
- **工作**：定義此應用程式能否存取您的工作。
- **信任的裝置**：選擇此應用程式能否使用信任的裝置。 受信任裝置是您已連線的硬體，或隨附於裝置的硬體。 例如，將電視、投影機等作為信任的裝置使用。
- **意見反應與診斷**：定義此應用程式能否存取診斷資訊。
- **與裝置同步**：選擇此應用程式能否與未和該裝置明確配對的無線裝置自動共用及同步資訊。

## <a name="personalization"></a>個人化

這些設定使用[個人化原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)，它也會列出支援的 Windows 版本。

- **桌面背景圖片 URL (僅限桌面版)** ：輸入 .jpg、.jpeg 或 .png 格式圖片的 URL，這些圖片要作為 Windows 桌面背景圖案使用。 使用者無法變更此圖片。 例如，輸入 `https://contoso.com/logo.png`。

  保留空白時，Intune 不會變更或更新此設定。

## <a name="printer"></a>印表機

- **印表機**：使用網路主機名稱 (DNS 名稱) 新增印表機。 OS 會搜尋裝置上每部印表機的印表機驅動程式並安裝相符的印表機驅動程式。 當您沒有輸入值，Intune 則不會變更或更新此設定。

  [Education/PrinterNames CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-printernames)

- **預設印表機**：針對要作為預設印表機的已安裝印表機，輸入其網路主機名稱 (DNS 名稱)。 當您沒有輸入值，Intune 則不會變更或更新此設定。

  [Education/DefaultPrinterName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **新增印表機**：[封鎖] 會防止使用者新增印表機。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許新增印表機。

  [Education/PreventAddingNewPrinters CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>隱私權

這些設定使用[隱私權原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy)，它也會列出支援的 Windows 版本。

- **隱私權體驗**：[封鎖] 會防止隱私權體驗在使用者登入時開啟，以及在新的和已升級的使用者使用時開啟。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Privacy/DisablePrivacyExperience](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **輸入個人化**：[封鎖] 防止使用語音聽寫以及和 Cortana 及其他使用 Microsoft 雲端式語音辨識的應用程式通話。 此功能已停用，且使用者不能啟用線上語音辨識使用設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會讓使用者進行選擇。 如果您允許使用這些服務，Microsoft 可能會收集語音資料來改進服務。

  [Privacy/AllowInputPersonalization CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **自動接受配對及隱私權使用者同意提示**：選擇 [允許]，讓 Windows 在執行應用程式時，自動接受配對及隱私權同意訊息。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會防止自動接受。

  [Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **發佈使用者活動**：[封鎖] 會防止應用程式和 OS 發佈使用者活動。 同時也會防止共用體驗，以及在活動摘要中探索最近使用的資源。 使用者活動會追蹤使用者在應用程式或 OS 中的工作狀態。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會啟用這項功能，讓應用程式可以發佈使用者活動。

  [Privacy/PublishUserActivities CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **僅限本機活動**：[封鎖] 可防止共用體驗，以及僅根據本機活動，在工作切換器中探索最近使用的資源。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

您可以設定可供裝置上所有應用程式存取的資訊。 您也可以使用**個別應用程式隱私權例外狀況**，以個別應用程式為基礎來定義例外狀況。

### <a name="exceptions"></a>例外狀況

- **帳戶資訊**：定義此應用程式能否存取使用者名稱、圖片及其他連絡人資訊。
- **背景應用程式**：定義此應用程式能否在背景執行。
- **行事曆**：定義此應用程式能否存取行事曆。
- **通話記錄**：定義此應用程式能否存取我的通話記錄。
- **相機**：定義此應用程式能否存取相機。
- **連絡人**：定義此應用程式能否存取連絡人。
- **電子郵件**：定義此應用程式能否存取及傳送電子郵件。
- **位置**：定義此應用程式能否存取位置資訊。
- **訊息中心**：定義此應用程式能否讀取或傳送文字或多媒體簡訊。
- **麥克風**：定義此應用程式能否使用麥克風。
- **動作**：定義此應用程式能否存取裝置動作資訊。
- **通知**：定義此應用程式能否存取通知。
- **電話**：定義此應用程式能否存取手機。
- **無線通訊**：有些應用程式會在您的裝置上使用無線電通訊 (例如，藍牙) 來傳送及接收資料，因此必須開啟或關閉這些無線通訊。 定義此應用程式能否控制這些無線電波。
- **工作**：定義此應用程式能否存取您的工作。
- **信任的裝置**：選擇此應用程式能否使用信任的裝置。 受信任裝置是您已連線的硬體，或隨附於裝置的硬體。 例如，將電視、投影機等作為信任的裝置使用。
- **意見反應與診斷**：選擇此應用程式能否存取診斷資訊。
- **與裝置同步** - 定義此應用程式能否自動與未和此電腦、平板電腦或手機直接配對的無線裝置共用及同步資訊。

## <a name="projection"></a>投影

這些設定使用 [WirelessDisplay 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay)，它也會列出支援的 Windows 版本。

- **來自無線顯示接收器的使用者輸入**：[封鎖] 防止來自無線顯示接收器的使用者輸入。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能讓無線顯示器將鍵盤、滑鼠、畫筆和觸控輸入傳送回來源裝置。

  [WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **投影到此電腦**：[封鎖] 會防止其他裝置尋找投影裝置，並防止投影到其他裝置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會讓裝置可供可探索，並可以投影到鎖定畫面上方的裝置。

  [WirelessDisplay/AllowProjectionFromPC CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **要求提供 PIN 以進行配對**：[需要] 於連線至投影裝置時一律提示要求 PIN。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能不需要 PIN，即可與裝置配對。

  [WirelessDisplay/RequirePinForPairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>報告與遙測

- **共用使用方式資料**：選擇提交診斷資料的層級。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者可以選擇要提交的層級。 根據預設，OS 不會共用任何資料。
  - **安全性**：協助提升 Windows 安全性的必要資訊，包括已連線使用者體驗與遙測元件設定、惡意軟體移除工具及 Microsoft Defender 的相關資料
  - **基本**：基本裝置資訊，包括品質相關資料、應用程式相容性、應用程式使用量資料和 [安全性] 層級的資料
  - **增強**：額外的見解，包括 Windows、Windows Server、System Center 和應用程式的使用方式、執行方式、進階的可靠性資料，以及 [基本] 和 [安全性] 層級的資料
  - **完整**：找出及協助修正問題的所有必要資料，加上 [安全性]、[基本] 和 [增強] 層級的資料。

  [System/AllowTelemetry CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **將 Microsoft Edge 瀏覽資料傳送到 Microsoft 365 Analytics** ：若要使用這項功能，請將 [共用使用方式資料] 設定為 [增強] 或 [完整]。 此功能控制 Microsoft Edge 針對具有設定商業識別碼的企業裝置傳送至 Microsoft 365 Analytics 的資料。 選項包括：
  - **未設定**：Intune 不會變更或更新此設定。 根據預設，OS 可能不會收集或傳送任何瀏覽歷程記錄資料。
  - **僅傳送內部網路資料**：允許系統管理員傳送內部網路資料歷程記錄。
  - **僅傳送網際網路資料**：允許系統管理員傳送網際網路資料歷程記錄。
  - **傳送內部網路與網際網路資料**：允許系統管理員傳送內部網路與網際網路資料歷程記錄。

  [Browser/ConfigureTelemetryForMicrosoft365Analytics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **遙測 Proxy 伺服器**：輸入 Proxy 伺服器的完整網域名稱 (FQDN) 或 IP 位址，用來轉送「已連線使用者體驗與遙測」要求 (使用安全通訊端層 (SSL) 連線)。 此設定的格式是*伺服器*:*連接埠*。 若具名 Proxy 失敗，或若未輸入 Proxy，則不傳送已連線使用者體驗與遙測資料。 此資料會保留在本機裝置上。

  當您沒有輸入值，Intune 則不會變更或更新此設定。 根據預設，OS 可能會使用預設 proxy 設定，將已連線的使用者體驗和遙測資料傳送至 Microsoft。

  範例格式：

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [System/TelemetryProxy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>搜尋

這些設定使用[搜尋原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search)，它也會列出支援的 Windows 版本。

- **安全搜尋 (僅限行動裝置版)** ：控制 Cortana 在搜尋結果中篩選成人內容的方式。 選項包括：
  - **使用者定義**：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇他們自己的設定。
  - **嚴格**：針對成人內容進行最高程度的篩選
  - **中**：針對成人內容進行中等程度的篩選。 不篩選有效的搜尋結果。
- **在 [搜尋] 中顯示網頁搜尋結果**：[封鎖] 會防止使用者使用 Windows Search 來搜尋網際網路，而搜尋中不會顯示 web 結果。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者搜尋 web，並在裝置上顯示結果。
- **讀音符號**：[封鎖] 會防止在 Windows Search 中顯示讀音符號。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會顯示讀音符號。

  [Search/AllowUsingDiacritics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **自動語言偵測**：[封鎖] 會防止 Windows Search 在編製內容或屬性的索引時自動偵測語言。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許此功能。

  [Search/AlwaysUseAutoLangDetection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **搜尋位置**：[封鎖] 會禁止 Windows Search 使用位置。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許此功能。

  [Search/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **索引子輪詢**：[封鎖] 會停用搜尋索引子輪詢功能。 即使系統活動很高，編製索引仍會全速繼續進行。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，當系統活動很高時，OS 可能會使用輪詢邏輯來節流編製索引活動。

  [Search/DisableBackoff CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **抽取式磁碟機編製索引**：[封鎖] 會讓使用者無法將抽取式磁碟機上的位置新增至程式庫，且無法編製索引。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會允許此功能。

  [Search/DisableRemovableDriveIndexing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **磁碟空間不足時的索引編製**：[啟用] 允許自動編製索引 (即使磁碟空間不足也一樣)。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，當硬碟空間為 600 MB 或更少時，OS 可能會關閉自動編製索引。 如果您組織中裝置的硬碟空間有限，請將其設定為 [未設定]。

  [Search/PreventIndexingLowDiskSpaceMB CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **遠端查詢**：[啟用] 允許裝置索引的遠端查詢。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會防止使用者遠端查詢裝置的索引。

  [Search/PreventRemoteQueries CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>開始

這些設定使用[啟動原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start)，它也會列出支援的 Windows 版本。  

- **[開始] 功能表配置**：上傳包含您自訂項目的 XML 檔案，包括應用程式的列出順序等等。 XML 檔案會覆寫預設的開始配置。 使用者無法變更您輸入的 [開始] 功能表配置。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/StartLayout CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **將網站釘選為 [開始] 功能表中的磚**：從 Microsoft Edge 匯入影像。 這些影像會作為桌面裝置 Windows [開始] 功能表中的連結顯示。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/ImportEdgeAssets CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **從工作列取消釘選應用程式**：[封鎖] 防止使用者從工作列取消釘選應用程式。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者從工作列中將應用程式取消釘選。

  [Start/NoPinningToTaskbar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **快速切換使用者**：[封鎖] 防止同時登入的使用者未經登出即切換使用者。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會在使用者磚上顯示 [切換使用者]。

  [Start/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **最常使用的應用程式**：[封鎖] 會隱藏最常使用的應用程式，使其不顯示在 [開始] 功能表中。 它也會停用「設定」應用程式中相對應的切換。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會顯示最常使用的應用程式。

  [Start/HideFrequentlyUsedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **最近新增的應用程式**：[封鎖] 會隱藏在 [開始] 功能表中最近新增的應用程式。 它也會停用「設定」應用程式中相對應的切換。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會在 [開始] 功能表中顯示最近新增的應用程式。

  [Start/HideRecentlyAddedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **開始畫面模式**：選擇開始畫面的大小。 選項包括：
  - **使用者定義**：Intune 不會變更或更新此設定。 不強制任何設定。 使用者可以設定大小。
  - **全螢幕**：強制開始畫面的全螢幕大小。
  - **非全螢幕**：強制開始畫面的非全螢幕大小。

  [Start/ForceStartSize CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **捷徑清單中最近開啟的項目**：[封鎖] 會隱藏最近的捷徑清單，使其無法顯示在 [開始] 功能表和工作列中。 它也會停用「設定」應用程式中相對應的切換。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會在捷徑清單中顯示最近開啟的項目。

  [Start/HideRecentJumplists CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **應用程式清單**：選擇如何顯示所有的應用程式清單。 選項包括：
  - **使用者定義**：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇如何顯示應用程式清單。
  - **摺疊**：隱藏所有應用程式清單。
  - **摺疊及停用 [設定] 應用程式**：隱藏所有應用程式清單，並停用 [設定] 應用程式中的 [在 [開始] 功能表中顯示應用程式清單]。
  - **移除並停用 [設定] 應用程式**：隱藏所有應用程式清單、移除所有應用程式按鈕，以及停用 [設定] 應用程式中的 [在 [開始] 功能表中顯示應用程式清單]。

  [Start/HideAppList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **電源按鈕**：[封鎖] 會隱藏 [開始] 功能表中的 [電源] 按鈕。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會顯示電源按鈕。

  [Start/HidePowerButton CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **使用者磚**：[封鎖] 會隱藏 [開始] 功能表中的使用者磚。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會顯示使用者磚。 進行以下設定：
  - **鎖定**：[封鎖] 會隱藏 [開始] 功能表的使用者磚中 [鎖定] 選項。  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會顯示 [鎖定] 按鈕。
  - **登出**：[封鎖] 會隱藏 [開始] 功能表的使用者磚中 [登出] 選項。 [未設定] (預設) 會顯示 [登出] 選項。

  [Start/HideUserTile CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **關機**：[封鎖] 會隱藏 [開始] 功能表的 [電源] 按鈕中 [更新並關機] 和 [關機] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/HideShutDown CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **睡眠**：[封鎖] 會隱藏 [開始] 功能表的 [電源] 按鈕中 [睡眠] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/HideSleep CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **休眠**：[封鎖] 會隱藏 [開始] 功能表的 [電源] 按鈕中 [休眠] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/HideHibernate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **切換帳戶**：[封鎖] 會隱藏 [開始] 功能表的使用者磚中 [切換帳戶] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **重新啟動選項**：[封鎖] 會隱藏 [開始] 功能表的 [電源] 按鈕中 [更新並重新啟動] 和 [重新啟動] 選項。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

  [Start/HideRestart CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **[開始] 上的 [文件]** ：隱藏或顯示 Windows [開始] 功能表中的 [文件] 資料夾。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderDocuments CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **[開始] 上的 [下載]** ：隱藏或顯示 Windows [開始] 功能表中的 [下載] 資料夾。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderDownloads CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **[開始] 上的檔案總管**：隱藏或顯示 Windows [開始] 功能表中的 [檔案總管] 應用程式。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderFileExplorer CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **[開始] 上的 [家用群組]** ：隱藏或顯示 Windows [開始] 功能表中的 [家用群組] 捷徑。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderHomeGroup CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **[開始] 上的 [音樂]** ：隱藏或顯示 Windows [開始] 功能表中的 [音樂] 資料夾。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderMusic CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **[開始] 上的 [網路]** ：隱藏或顯示 Windows [開始] 功能表中的 [網路]。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderNetwork CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **[開始] 上的 [個人] 資料夾**：隱藏或顯示 Windows [開始] 功能表中的 [個人] 資料夾。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderPersonalFolder CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **[開始] 上的 [圖片]** ：隱藏或顯示 Windows [開始] 功能表中的 [圖片] 資料夾。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderPictures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **[開始] 上的 [設定]** ：隱藏或顯示 Windows [開始] 功能表中的 [設定] 捷徑。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderSettings CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **[開始] 上的 [影片]** ：隱藏或顯示 Windows [開始] 功能表中的 [影片] 資料夾。 選項包括：
  - **未設定** (預設值)：Intune 不會變更或更新此設定。 不強制任何設定。 使用者選擇顯示或隱藏捷徑。
  - **隱藏**：隱藏捷徑，並停用 [設定] 應用程式的設定。
  - **顯示**：顯示捷徑，並停用 [設定] 應用程式的設定。

  [Start/AllowPinnedFolderVideos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **適用於 Microsoft Edge 的 SmartScreen**：[需要] 會開啟 Microsoft Defender SmartScreen，並防止使用者將其關閉。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會開啟 SmartScreen，並允許使用者將其開啟或關閉。

  Microsoft Edge 會使用 Microsoft Defender SmartScreen (已開啟)，以保護使用者免於遭受潛在的網路釣魚詐騙和惡意軟體攻擊。

  [Browser/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **惡意網站存取**：[封鎖] 防止使用者略過 Microsoft Defender SmartScreen 篩選工具警告，並阻止他們進入網站。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者略過警告，繼續前往網站。

  [Browser/PreventSmartScreenPromptOverride CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **未經驗證的檔案下載**：[封鎖] 會防止使用者略過 Microsoft Defender SmartScreen 篩選工具警告，並防止他們下載未經驗證的檔案。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓使用者略過警告，繼續下載未經驗證的檔案。

  [Browser/PreventSmartScreenPromptOverrideForFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows 焦點

這些設定使用[體驗原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience)，它也會列出支援的 Windows 版本。

- **Windows 焦點**：[封鎖] 會關閉鎖定畫面、Windows 提示、Microsoft 消費者功能，以及其他相關功能的 Windows 焦點。 如果您的目標是要將裝置網路流量降到最低，請選取 [是]。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 Windows 焦點功能，且使用者可以控制 OS。

  [Experience/AllowWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  設定為 [未設定] 時，您也可以允許或封鎖下列設定：

  - **鎖定畫面上的 Windows 焦點**：[封鎖] 會阻止 Windows 焦點在裝置鎖定畫面上顯示資訊。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會在鎖定畫面上顯示 Windows 焦點資訊。

    [Experience/ConfigureWindowsSpotlightOnLockScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Windows 焦點中的第三方建議**：[封鎖] 會阻止 Windows 焦點建議不是由 Microsoft 發佈的內容。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許來自合作夥伴的應用程式和內容建議，並在 [開始] 功能表中顯示建議的應用程式，以及 Windows 提示。

    [Experience/AllowThirdPartySuggestionsInWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **消費者功能**：[封鎖] 會關閉通常僅供消費者使用的體驗，例如開始建議、成員資格通知、應用程式安裝後的全新體驗及重新導向磚。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。

    [Experience/AllowWindowsConsumerFeatures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Windows 提示**：[封鎖] 會停用快顯的 Windows 提示。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許顯示 Windows 提示。

    [Experience/AllowWindowsTips CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **控制中心的 Windows 焦點**：[封鎖] 防止控制中心顯示 Windows 焦點通知。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會在控制中心顯示通知，建議可協助使用者在 Windows 提高生產力的應用程式或功能。

    [Experience/AllowWindowsSpotlightOnActionCenter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Windows 焦點個人化**：[封鎖] 會防止 Windows 使用診斷資料，為使用者提供自訂的體驗。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓 Microsoft 使用診斷資料提供個人化的建議、提示，並針對使用者需求提供量身打造的 Windows。

    [Experience/AllowTailoredExperiencesWithDiagnosticData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Windows 歡迎使用體驗**：[封鎖] 會關閉 Windows 焦點的 Windows 歡迎使用功能。 當 Windows 及其應用程式有更新和變更時，不會顯示 Windows 歡迎使用體驗。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許 Windows 歡迎使用體驗向使用者顯示新功能或更新功能的資訊。

    [Experience/AllowWindowsSpotlightWindowsWelcomeExperience CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender 防毒軟體

這些設定使用 [Defender 原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender)，它也會列出支援的 Windows 版本。

- **即時監視**：[啟用] 會開啟即時掃描來掃描是否有惡意程式碼、間諜軟體和其他垃圾軟體。 終端使用者無法關閉它。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，作業系統會開啟這項功能，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowRealtimeMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **行為監視**：[啟用] 會開啟行為監視，並檢查裝置上是否有某些已知模式的可疑活動。 使用者無法關閉行為監視。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會開啟行為監視，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowBehaviorMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **網路檢查系統 (NIS)** ：NIS 可協助保護裝置免於遭受網路型入侵。 它會使用 Microsoft Endpoint Protection 中心提供之已知弱點的病毒碼，協助偵測及阻擋惡意流量。

  - **啟用**：開啟網路保護和網路封鎖。 終端使用者無法關閉它。 啟用時，使用者會被封鎖而無法連線到已知的弱點。

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，作業系統會開啟 NIS，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/EnableNetworkProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **掃描所有下載**：[啟用] 會開啟此設定，而 Defender 會掃描從網際網路下載的所有檔案。 使用者無法關閉此設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會開啟此設定，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowIOAVProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **掃描 Microsoft 網頁瀏覽器中所載入的指令碼**：[啟用] 允許 Defender 掃描在 Internet Explorer 中使用的指令碼。 使用者無法關閉此設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 會開啟此設定，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowScriptScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Defender 的終端使用者存取**：[封鎖] 會向使用者隱藏 Microsoft Defender 使用者介面。 也會隱藏所有 Microsoft Defender 通知。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者存取 Microsoft Defender UI，並允許使用者進行變更。

  如果您封鎖設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  變更此設定之後，將會在下一次裝置重新啟動時生效。

  [Defender/AllowUserUIAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **安全情報更新間隔 (以小時為單位)** ：輸入 Defender 檢查新安全情報的間隔，從 0 到 24。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 作業系統預設可能每 8 小時檢查一次更新。
  - **不檢查**：Defender 不會檢查是否有新的安全情報更新。
  - [1-24]：`1` 為每小時檢查一次、`2` 為每兩小時檢查一次、`24` 為每天檢查一次等等。
  
  [Defender/SignatureUpdateInterval CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **監視檔案和程式活動**：允許 Defender 監視裝置上的檔案和程式活動。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 作業系統預設可能會監視所有檔案。
  - **已停用監視**
  - **監視所有檔案**
  - **僅監視傳入檔案**
  - **僅監視傳出檔案**

  [Defender/RealTimeScanDirection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **多少天之後刪除隔離的惡意程式碼**：在您輸入天數內繼續追蹤解析的惡意程式碼，讓您可以手動檢查先前受影響的裝置。 

  如果您未設定此設定，或將其設為 `0` 天，惡意程式碼會保留在隔離資料夾中，且系統不會將其自動移除。 設為 `90` 時，隔離項目會在系統上儲存 90 天，然後移除。

  [Defender/DaysToRetainCleanedMalware CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **掃描期間的 CPU 使用率限制**：限制掃描可以使用的 CPU 資源數量 (從 `0` 至 `100` %)。 根據預設，OS 可能會將此值設為 50%。
- **掃描封存檔**：[啟用] 會開啟 Defender，使其掃描封存檔案 (例如 Zip 或 Cab 檔案)。 使用者無法關閉此設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能開啟此掃描，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowArchiveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **掃描內送郵件訊息**：[啟用] 允許 Defender 在電子郵件訊息到達裝置的時候進行掃描。 啟用時，引擎會剖析信箱和郵件檔案，以分析郵件內文和附件。 您可以掃描 .pst (Outlook)、.dbx、.mbx、MIME (Outlook Express) 和 BinHex (Mac) 格式。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，作業系統會關閉此掃描，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowEmailScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **在完整掃描期間掃描抽取式磁碟機**：[啟用] 會在完整掃描期間開啟 Defender 抽取式磁碟機掃描。 使用者無法關閉此設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓 Defender 掃描抽取式磁碟機 (例如 USB 隨身碟)，並允許使用者變更此設定。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  在快速掃描期間，可能仍會掃描抽取式磁碟機。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowFullScanRemovableDriveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **在完整掃描期間掃描對應的網路磁碟機**：[啟用] 讓 Defender 掃描相對應網路磁碟機上的檔案。 如果磁碟機上的檔案是唯讀，則 Defender 無法移除在其中發現的任何惡意程式碼。 使用者無法關閉此設定。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，作業系統會開啟這項功能，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。 

  在快速掃描期間，可能仍會掃描對應的網路磁碟機機。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **掃描從網路資料夾中開啟的檔案**：[啟用] 會讓 Defender 掃描從網路資料夾或共用網路磁碟機開啟的檔案，例如從 UNC 路徑存取的檔案。 使用者無法關閉此設定。 如果磁碟機上的檔案是唯讀，則 Defender 無法移除在其中發現的任何惡意程式碼。

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，作業系統會掃描從網路資料夾中開啟的檔案，並允許使用者進行變更。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowScanningNetworkFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **雲端保護**：[啟用] 會開啟 Microsoft Active Protection Service 以從您管理的裝置接收惡意程式碼活動的相關資訊。 使用者無法變更此設定。 

  當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，作業系統允許 Microsoft Active Protection Service 接收資訊，並允許使用者變更此設定。

  如果您啟用此設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前設定的狀態。

  Intune 不會關閉這項功能。 若要停用，請使用自訂 URI。

  [Defender/AllowCloudProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **在提交範例之前提示使用者**：控制是否將可能需要進一步分析的潛在惡意檔案，自動傳送給 Microsoft。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 作業系統預設可能會自動傳送安全的範例。
  - **一律提示**
  - **在傳送個人資料之前提示**
  - **永不傳送資料**
  - **不提示而直接傳送所有資料**：資料會自動傳送。

  [Defender/SubmitSamplesConsent CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **執行每日快速掃描的時間**：選擇要執行每日快速掃描的小時。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能會在上午 2 點執行此掃描。

  若您需要自訂更多項目，請設定 [要執行的系統掃描類型] 設定。

  [Defender/ScheduleQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **要執行的系統掃描類型**：排程系統掃描，包含掃描層級，以及要執行掃描的日期和時間。 選項包括：
  - **未設定**：Intune 不會變更或更新此設定。 不強制任何設定。 使用者可以視需要在裝置上手動執行掃描。
  - **停用**：停用裝置上的任何系統掃描。 若您使用會掃描裝置的合作夥伴防毒軟體解決方案，請選擇此選項。
  - **快速掃描**：查看惡意程式碼可能註冊的常見位置，例如登錄機碼和已知的 Windows 啟動資料夾。
    - **排定的日期**：選擇要執行掃描的日期。
    - **排定的時間**：選擇要執行掃描的小時。
  - **完整掃描**：查看惡意程式碼可能註冊的常見位置，同時掃描裝置上的每個檔案和資料夾。
    - **排定的日期**：選擇要執行掃描的日期。
    - **排定的時間**：選擇要執行掃描的小時。

  > [!TIP]
  > 這項設定可能會和 [執行每日快速掃描的時間] 設定衝突。 一些建議：  
  >
  > - 如果您想要排程每日快速掃描和每週完整掃描，則：
  >   1. 設定 [執行每日快速掃描的時間] 設定。
  >   2. 設定 [要執行的系統掃描類型]，以進行完整掃描。
  > 
  > - 如果您每日只想要一次快速掃描 (不進行完整掃描)，請使用下列其中一項設定：**執行每日快速掃描的時間**或**要執行的系統掃描類型**。 例如，若要在每個星期二早上 6 點執行快速掃描，請設定 [要執行的系統掃描類型] 設定。
  > 
  > - 請不要同時設定 [執行每日快速掃描的時間] 並將 [要執行的系統掃描類型] 設為 [快速掃描]。 這些設定可能會衝突，導致掃描無法執行。

  [Defender/ScanParameter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **偵測潛在的不必要應用程式**：這項功能會識別並封鎖潛在的垃圾應用程式 (PUA)，使其無法在您的網路中下載和安裝。 這些應用程式不會被視為病毒、惡意程式碼或其他類型的威脅。 但是，這些應用程式可以在可能影響其效能或使用的端點上執行動作。 選擇 Windows 偵測 PUA 時的保護層級。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，Microsoft Defender 可能會停用這項功能。
  - **Off**：關閉 PUA 保護。
  - **啟用**：Microsoft Defender 會偵測到 PUA，並封鎖偵測到的項目。 這些項目會和其他威脅一起顯示在歷程記錄中。
  - **稽核**：Microsoft Defender 會偵測 PUA，但不採取任何動作。 您可以檢閱那些應用程式 (Microsoft Defender 會採取動作) 的相關資訊。 例如，在 [事件檢視器] 中搜尋由 Microsoft Defender 建立的事件。

  如需潛在垃圾應用程式的詳細資訊，請參閱[偵測及封鎖潛在的垃圾應用程式](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus)。

  [Defender/PUAProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **提交同意範例**：目前此設定不會有任何影響。 請勿使用此設定。 未來的版本可能會移除這個設定。

- **存取保護時**：[封鎖] 會防止掃描已存取或已下載的檔案。 終端使用者無法開啟該設定。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可能啟用這項功能，並允許使用者進行變更。

  如果您封鎖設定，然後將其變更回 [未設定]，則 Intune 會將設定保留在先前 OS 設定的狀態。

  Intune 不會開啟這項功能。 若要啟用，請使用自訂 URI。

  [Defender/AllowOnAccessProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **對偵測到的惡意程式碼威脅採取的動作**：選取 [啟用]，可選擇您希望 Defender 針對偵測到的每種威脅等級 (低、中、高及嚴重) 所採取的動作。 當設定為 [未設定] (預設) 時，Intune 不會變更或更新此設定。 根據預設，OS 可讓 Microsoft Defender 選擇最佳選項。

  當設定為 [啟用] 時，請選取動作：
  
  - **清除**
  - **隔離**
  - **移除**
  - **允許**
  - **使用者定義**
  - **封鎖**

  如果您的動作不可行，則 Microsoft Defender 會選擇最佳選項，以確保已修復威脅。

  [Defender/ThreatSeverityDefaultAction CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender 防毒軟體排除

您可以透過修改排除清單，從 Microsoft Defender 防毒軟體掃描中排除特定檔案。 **一般來說，您應該不需要套用排除項**。 Microsoft Defender 防毒軟體會包含一些以已知 OS 行為和一般管理檔案為基礎的自動排除項，例如，用於企業管理、資料庫管理，以及其他企業案例和情況的那些檔案。

> [!WARNING]
> **定義排除項會減弱 Microsoft Defender 防毒軟體所提供的保護**。 一律評估與實作排除項相關聯的風險。 僅排除您已知不是惡意的檔案。

- **不進行掃描和即時保護的檔案和資料夾**：將一或多個 **C:\Path** 或 **%ProgramFiles%\Path\filename.exe** 等檔案和資料夾新增至排除清單。 這些檔案和資料夾不會包含在即時或排程的掃描中。
- **不進行掃描和即時保護的副檔名**：將一個或多個 **jpg** 或 **txt** 等副檔名新增至排除清單。 任何即時掃描或排定的掃描，都不會包含有這些副檔名的任何檔案。
- **不進行掃描和即時保護的處理序**：將一或多個 **.exe**、 **.com** 或 **.scr** 等類型的處理程序新增至排除清單。 任何即時或已排程的掃描都不會包含這些處理序。

## <a name="power-settings"></a>電源設定

這些設定使用[電源原則 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power)，其也會列出支援的 Windows 版本。

### <a name="battery"></a>電池

- **開啟節能程式的電池電量**：當裝置使用電池電力時，請輸入電池電量等級，以從 0 到 100 開啟節能程式。 輸入表示電池電量等級的百分比值。 例如，設定為 `80` 時，當電池的電量為 80% 或更低時，會開啟節能程式。

  當您沒有輸入值，Intune 則不會變更或更新此設定。 根據預設，OS 可能會將此值設為 70%。

  [Power/EnergySaverBatteryThresholdOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **關閉上蓋 (僅限行動裝置版)** ：當裝置使用電池電力時，請選擇關閉上蓋時要執行的動作。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者控制此設定。
  - **不進行動作**：裝置會保持開啟狀態，並繼續使用電池電力。
  - **睡眠**：裝置進入睡眠模式，並使用少量的電池電量。 電腦仍然開啟，而開啟的應用程式和檔案則儲存在隨機存取記憶體 (RAM) 中。
  - **休眠**：裝置進入休眠模式。 開啟的應用程式和檔案會儲存在硬碟上，而裝置會關閉。
  - **關機**：裝置關機。 開啟的應用程式和檔案會關閉而不儲存。

  [Power/SelectLidCloseActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **電源按鈕**：當裝置使用電池電力時，選擇當選取 [電源] 按鈕時要執行的動作。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者控制此設定。
  - **不進行動作**：裝置會保持開啟狀態，並繼續使用電池電力。
  - **睡眠**：裝置進入睡眠模式，並使用少量的電池電量。 電腦仍然開啟，而開啟的應用程式和檔案則儲存在隨機存取記憶體 (RAM) 中。
  - **休眠**：裝置進入休眠模式。 開啟的應用程式和檔案會儲存在硬碟上，而裝置會關閉。
  - **關機**：裝置關機。 開啟的應用程式和檔案會關閉而不儲存。

  [Power/SelectPowerButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **[睡眠] 按鈕**：當裝置使用電池電力時，選擇當選取 [睡眠] 按鈕時要執行的動作。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者控制此設定。
  - **不進行動作**：裝置會保持開啟狀態，並繼續使用電池電力。
  - **睡眠**：裝置進入睡眠模式，並使用少量的電池電量。 電腦仍然開啟，而開啟的應用程式和檔案則儲存在隨機存取記憶體 (RAM) 中。
  - **休眠**：裝置進入休眠模式。 開啟的應用程式和檔案會儲存在硬碟上，而裝置會關閉。
  - **關機**：裝置關機。 開啟的應用程式和檔案會關閉而不儲存。

  [Power/SelectSleepButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **交互式睡眠**：當裝置使用電池電力時，選擇 [允許交互式睡眠模式] 或 [停用交互式睡眠模式]。

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者控制此設定。
  - **啟用**：裝置可以進入交互式睡眠模式。 開啟的應用程式和檔案會儲存在隨機存取記憶體 (RAM) 和硬碟上。 會使用少量的電池電量。
  - **停用**：防止裝置進入交互式睡眠模式。

  [Power/TurnOffHybridSleepOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **開啟節能程式的電池電量**：當裝置插入電源時，請輸入電池電量等級，以從 0 到 100 開啟節能程式。 輸入表示電池電量等級的百分比值。 例如，設定為 `80` 時，當電池的電量為 80% 或更低時，會開啟節能程式。

  當您沒有輸入值，Intune 則不會變更或更新此設定。 根據預設，OS 可能會將此值設為 70%。

  [Power/EnergySaverBatteryThresholdPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **關閉上蓋 (僅限行動裝置版)** ：當裝置插入電源時，請選擇關閉上蓋時要執行的動作。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **不進行動作**：裝置會保持開啟。
  - **睡眠**：裝置進入睡眠模式。 電腦仍然開啟，而開啟的應用程式和檔案則儲存在隨機存取記憶體 (RAM) 中。
  - **休眠**：裝置進入休眠模式。 開啟的應用程式和檔案會儲存在硬碟上，而裝置會關閉。
  - **關機**：裝置關機。 開啟的應用程式和檔案會關閉而不儲存。
  
    [Power/SelectLidCloseActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **電源按鈕**：當裝置插入電源時，選擇當選取 [電源] 按鈕時要執行的動作。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **不進行動作**：裝置會保持開啟。
  - **睡眠**：裝置進入睡眠模式。 電腦仍然開啟，而開啟的應用程式和檔案則儲存在隨機存取記憶體 (RAM) 中。
  - **休眠**：裝置進入休眠模式。 開啟的應用程式和檔案會儲存在硬碟上，而裝置會關閉。
  - **關機**：裝置關機。 開啟的應用程式和檔案會關閉而不儲存。

  [Power/SelectPowerButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **[睡眠] 按鈕**：當裝置插入電源時，選擇當選取 [睡眠] 按鈕時要執行的動作。 選項包括：

  - **未設定** (預設值)：Intune 不會變更或更新此設定。
  - **不進行動作**：裝置會保持開啟。
  - **睡眠**：裝置進入睡眠模式。 電腦仍然開啟，而開啟的應用程式和檔案則儲存在隨機存取記憶體 (RAM) 中。
  - **休眠**：裝置進入休眠模式。 開啟的應用程式和檔案會儲存在硬碟上，而裝置會關閉。
  - **關機**：裝置關機。 開啟的應用程式和檔案會關閉而不儲存。

  [Power/SelectSleepButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **交互式睡眠**：當裝置充電時，選擇 [允許交互式睡眠模式] 或 [停用交互式睡眠模式]。

  - **未設定** (預設值)：Intune 不會變更或更新此設定。 根據預設，OS 可能允許使用者控制此設定。
  - **啟用**：裝置可以進入交互式睡眠模式。 開啟的應用程式和檔案會儲存在隨機存取記憶體 (RAM) 和硬碟上。
  - **停用**：防止裝置進入交互式睡眠模式。

  [Power/TurnOffHybridSleepPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>後續步驟

如需每項設定的其他技術詳細資料，以及支援哪些 Windows 版本，請參閱 [Windows 10 Policy CSP Reference](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (Windows 10 原則 CSP 參考)

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
