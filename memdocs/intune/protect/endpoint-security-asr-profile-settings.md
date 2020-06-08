---
title: Intune 端點安全性的受攻擊面縮小設定 |Microsoft Docs
description: Microsoft Intune 端點安全性的受攻擊面縮小原則設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 7f200e5cb5bb4aa0f29cbd3adc0f177bb14e5476
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431692"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Intune 端點安全性的受攻擊面縮小原則設定

在 Intune 的端點安全性節點中，檢視您可以在設定檔中隨[端點安全性原則](../protect/endpoint-security-policy.md)一併進行的「受攻擊面縮小」原則設定。

支援的平台和設定檔：

- **Windows 10 及更新版本**：
  - 設定檔：**應用程式與瀏覽器隔離**
  - 設定檔：**Web 防護**
  - 設定檔：**應用程式控制**
  - 設定檔：**受攻擊面縮小規則**
  - 設定檔：**裝置控制**
  - 設定檔：**惡意探索保護**

## <a name="app-and-browser-isolation-profile"></a>應用程式與瀏覽器隔離設定檔

### <a name="app-and-browser-isolation"></a>應用程式與瀏覽器隔離

- **為 Edge 開啟應用程式防護 (選項)**  
  CSP：[AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - [未設定] (預設)
  - **為 Edge 啟用** - 應用程式防護會在 Hyper-V 虛擬化瀏覽容器中開啟未核准的網站。

  設為 [為 Edge 啟用] 時，可用的設定如下：
  
  - **剪貼簿行為**  
    CSP：[ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    選擇從本機電腦及應用程式防護虛擬瀏覽器，允許執行哪些複製並貼上的動作。
    - [未設定] (預設)
    - **禁止電腦和瀏覽器之間的複製並貼上**
    - **僅允許從瀏覽器到電腦的複製並貼上**
    - **僅允許從電腦到瀏覽器的複製並貼上**
    - **允許電腦和瀏覽器之間的複製並貼上**

  - **禁止未經企業所核准網站的外部內容**  
    CSP：[BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - [未設定] (預設)
    - **是** - 封鎖從未經核准的網站載入內容。

  - **收集在應用程式防護瀏覽工作階段中發生的事件記錄**  
    CSP：[AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - [未設定] (預設)
    - **是** - 收集應用程式防護虛擬瀏覽工作階段內發生的事件記錄檔。

  - **允許儲存使用者產生的瀏覽器資料**  
    CSP：[AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - [未設定] (預設)
    - **是** - 允許儲存在應用程式防護虛擬瀏覽工作階段期間所建立的使用者資料。 使用者資料的範例包括密碼、我的最愛和 cookie。

  - **啟用硬體圖形加速**  
    CSP：[AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - [未設定] (預設)
    - **是** - 在應用程式防護虛擬瀏覽工作階段內，使用虛擬圖形處理器來加快載入含有大量圖形的網站。

  - **允許使用者將檔案下載到主機**  
    CSP：[SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - [未設定] (預設)
    - **是** - 允許使用者從虛擬瀏覽器將檔案下載到主機作業系統上。

- **應用程式防護允許列印至本機印表機**  

  - [未設定] (預設)
  - **是** - 允許列印至本機印表機。

- **應用程式防護允許列印至網路印表機**  

  - [未設定] (預設)
  - **是** - 允許列印至網路印表機。

- **應用程式防護允許列印至 PDF**  

  - [未設定] (預設)
  - **是** - 允許列印至 PDF。

- **應用程式防護允許列印至 XPS**  

  - [未設定] (預設)
  - **是** - 允許列印至 XPS。

- **Windows 網路隔離原則**  
  
  - [未設定] (預設)
  - **是** - 設定 Windows 網路隔離原則。  
  
  設為 [設定] 時，您可以進行下列設定。

  - **IP 範圍**  
    展開下拉式清單，選取 [新增]，然後指定「較低位址」，再指定「較高位址」。

  - **雲端資源**  
    展開下拉式清單，選取 [新增]，然後指定「IP 位址或 FQDN」和 *Proxy*。

  - **網路網域**  
   展開下拉式清單，選取 [新增]，然後指定「網路網域」。

  - **Proxy 伺服器**  
    展開下拉式清單，選取 [新增]，然後指定「Proxy 伺服器」。

  - **內部 Proxy 伺服器**  
    展開下拉式清單，選取 [新增]，然後指定「內部 Proxy 伺服器」。

  - **中性資源**  
    展開下拉式清單，選取 [新增]，然後指定「中性資源」。

  - **停用自動偵測其他企業 Proxy 伺服器**  
    - [未設定] (預設)
    - **是** - 停用自動偵測其他企業 Proxy 伺服器。

  - **停用自動偵測其他企業 IP 範圍**  
    - [未設定] (預設)
    - **是** - 停用自動偵測其他企業 IP 範圍。

## <a name="web-protection-profile"></a>Web 防護設定檔

### <a name="web-protection"></a>Web 防護

- **啟用網路保護**  
  CSP：[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是停用。
  - **使用者定義**
  - **啟用** - 為系統上的所有使用者啟用網路保護。
  - **稽核模式** - 不會禁止使用者存取危險網域，而是引發 Windows 事件。

- **Microsoft Edge 需要 SmartScreen**  
  CSP：[Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **是** - 使用 SmartScreen 保護使用者免於潛在的網路釣魚詐騙和惡意軟體攻擊。
  - [未設定] (預設)

- **封鎖惡意網站存取**  
  CSP：[Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **是** - 禁止使用者略過 Microsoft Defender SmartScreen 篩選工具警告，並防止其進入網站。
  - [未設定] (預設)

- **封鎖未經驗證的檔案下載**  
  CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **是** - 禁止使用者略過 Microsoft Defender SmartScreen 篩選工具警告，並防止其下載未經驗證的檔案。
  - [未設定] (預設)

## <a name="application-control-profile"></a>應用程式控制設定檔

### <a name="microsoft-defender-application-control"></a>Microsoft Defender 應用程式控制

- **AppLocker 應用程式控制**  
  - [未設定] (預設)
  - **施行元件及商店應用程式**
  - **稽核元件與商店應用程式**
  - **施行元件、商店應用程式及 Smartlocker**
  - **稽核元件、商店應用程式及 Smartlocker**

- **禁止使用者略過 SmartScreen 警告**  
  [PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  此設定需要啟用 [Enforce SmartScreen for apps and files' setting] \(施行應用程式及檔案適用的 SmartScreen\) 設定。
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是允許使用者覆寫。
  - **是** - SmartScreen 不會顯示讓使用者略過警告並執行應用程式的選項。 警告會顯示，但使用者無法將其略過。

- **開啟 Windows SmartScreen**  
  CSP：[SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是啟用 SmartScreen，但使用者可以變更此設定。 若要停用 SmartScreen，請使用自訂 URI。
  - **是** - 強制所有使用者使用 SmartScreen。

## <a name="attack-surface-reduction-rules-profile"></a>受攻擊面縮小規則設定檔

### <a name="attack-surface-reduction-rules"></a>受攻擊面縮小規則

- **從 Windows 規則：封鎖竊取自 Windows 本機安全性授權子系統 (lsass.exe) 的認證**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874499) (機器翻譯)

  這項受攻擊面縮小 (ASR) 規則是透過下列 GUID 來控制：9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **使用者定義**
  - **啟用** - 禁止嘗試透過 lsass.exe 竊取認證。
  - **稽核模式** - 不會禁止使用者存取危險網域，而是引發 Windows 事件。

- **禁止 Adobe Reader 建立子處理序**  
  [使用受攻擊面縮小規則來縮小受攻擊面](https://go.microsoft.com/fwlink/?linkid=853979)
  
  這項 ASR 規則是透過下列 GUID 來控制：7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **未設定** (預設) - 已還原 Windows 預設值，也就是不禁止建立子處理序。
  - **使用者定義**
  - **啟用** - 禁止 Adobe Reader 建立子處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖子處理序。

- **禁止 Office 應用程式將程式碼插入其他處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872974) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - 禁止 Office 應用程式將程式碼插入其他處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止 Office 應用程式建立可執行的內容**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872975) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：3B576869-A4EC-4529-8536-B80A7769E899
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - 禁止 Office 應用程式建立可執行的內容。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止所有 Office 應用程式建立子處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872976) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **禁止** - 禁止 Office 應用程式建立子處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **封鎖來自 Office 巨集的 Win32 API 呼叫**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872977) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - 禁止 Office 巨集使用 Win32 API 呼叫。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止 Office 通訊應用程式建立子處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874499) (機器翻譯)  

  這項 ASR 規則是透過下列 GUID 來控制：26190899-1602-49e8-8b27-eb1d0a1ce869。
  - **未設定** (預設) - 已還原 Windows 預設值，也就是不禁止建立子處理序。
  - **使用者定義**
  - **啟用** - 禁止 Office 通訊應用程式建立子處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖子處理序。

- **禁止執行可能經過混淆處理的指令碼 (js/vbs/ps)**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872978) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - Defender 會禁止執行經過混淆處理的指令碼。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止 JavaScript 與 VBScript 啟動下載的可執行內容**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872979) (機器翻譯)

   這項 ASR 規則是透過下列 GUID 來控制：D3E037E1-3EB8-44C8-A917-57927947596D
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - Defender 禁止執行從網際網路下載的 JavaScript 或 VBScript 檔案。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **封鎖源自 PSExec 和 WMI 命令的處理序建立**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874500) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - 禁止 PSExec 或 WMI 命令建立處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **封鎖從 USB 執行的不受信任和未簽署處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874502) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - 禁止從 USB 磁碟機執行的未受信任與未簽署處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止可執行檔執行，除非其符合普遍性、存留期或信任的清單準則**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874503) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖**
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **封鎖從電子郵件及網路郵件用戶端下載的可執行內容**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872980) (機器翻譯)

  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** - 禁止從電子郵件及網路郵件用戶端下載的可執行內容。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **使用進階防護來防範勒索軟體**  
   [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874504) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：c1db55ab-c21a-4637-bb3f-a12568109d35
  - **未設定** (預設) - 此設定會還原為 Windows 預設值，也就是關閉。
  - **使用者定義**
  - **啟用**
  - **稽核模式** - - 引發 Windows 事件，而不是禁止。

- **啟用資料夾保護**  
  CSP：[EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **未設定** (預設) - 此設定會還原為預設值，而不會禁止讀取或寫入。
  - **啟用** - 針對不受信任的應用程式，Defender 會禁止嘗試修改或刪除受保護資料夾中的檔案，或寫入磁碟磁區。 Defender 會自動判斷哪些應用程式可以信任。 或者，您也可以定義自己的信任應用程式清單。
  - **稽核模式** - 當不受信任的應用程式存取受控制資料夾，但未施行任何禁止時，就會引發 Windows 事件。
  - **禁止磁碟修改** - 只會禁止嘗試寫入磁碟磁區。
  - **稽核磁碟修改** - 會引發 Windows 事件，而不會禁止嘗試寫入磁碟磁區。
  
- **排除攻擊面縮減規則中的檔案與路徑**  
  CSP：[AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  展開下拉式清單，然後選取 [新增]，定義要從受攻擊面縮小規則中排除的檔案或資料夾**路徑**。

## <a name="device-control-profile"></a>裝置控制設定檔

### <a name="device-control"></a>裝置控制

- **依裝置識別碼的硬體裝置安裝**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  此設定可讓您針對 Windows 防止安裝的裝置，指定隨插即用硬體識別碼與相容識別碼的清單。 此原則設定優先於任何其他允許 Windows 安裝裝置的原則設定。  如果您在遠端桌面伺服器上啟用此原則設定，此原則設定會影響指定裝置從遠端桌面用戶端到遠端桌面伺服器的重新導向。

  - **未設定**
  - **允許硬體裝置安裝** - 其他原則設定可允許或防止安裝及更新裝置。
  - **禁止硬體裝置安裝** (預設) - 防止 Windows 安裝其硬體識別碼或相容識別碼出現在所定義清單中的裝置。

  設為 [封鎖硬體裝置安裝] 時，您可以進行下列設定：

  - **移除相符的硬體裝置**

    只有在 [依裝置識別碼的硬體裝置安裝] 設定為 [封鎖硬體裝置安裝] 時，才能使用此設定。
    - **是**
    - **未設定**

  - **已封鎖的硬體裝置識別碼**  

    只有在 [依裝置識別碼的硬體裝置安裝] 設定為 [封鎖硬體裝置安裝] 時，才能使用此設定。

    選取 [新增]，然後指定所要封鎖的硬體裝置識別碼。

- **依安裝類別的硬體裝置安裝**  
  CSP：[DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  此原則設定可讓您針對 Windows 防止安裝的裝置驅動程式，指定裝置安裝類別全域唯一識別碼 (GUID) 的清單。 此原則設定優先於任何其他允許 Windows 安裝裝置的原則設定。 如果您在遠端桌面伺服器上啟用此原則設定，此原則設定會影響指定裝置從遠端桌面用戶端到遠端桌面伺服器的重新導向。

  - **未設定**
  - **允許硬體裝置安裝** - 其他原則設定可允許或防止 Windows 安裝及更新裝置。
  - **禁止硬體裝置安裝** (預設) - 防止 Windows 安裝其安裝類別 GUID 出現在所定義清單中的裝置。

  設定為 [禁止硬體裝置安裝] 時，即可設定 [移除相符的硬體裝置] 和 [封鎖的硬體裝置識別碼]。

  - **移除相符的硬體裝置**

    只有在 [依裝置識別碼的硬體裝置安裝] 設定為 [封鎖硬體裝置安裝] 時，才能使用此設定。
    - **是**
    - **未設定**

  - **已封鎖的硬體裝置識別碼**

    只有在 [依裝置識別碼的硬體裝置安裝] 設定為 [封鎖硬體裝置安裝] 時，才能使用此設定。

    選取 [新增]，然後指定所要封鎖的硬體裝置識別碼。

- **在完整掃描期間掃描抽取式磁碟機**  
  CSP：[Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **未設定** (預設) - 此設定會還原為用戶端預設值，也就是掃描抽取式磁碟機，但使用者可以停用此掃描。
  - **是** - 在完整掃描期間，掃描抽取式磁碟機 (例如 USB 快閃磁碟機)。
  
## <a name="exploit-protection-profile"></a>惡意探索保護設定檔

### <a name="exploit-protection"></a>惡意探索保護

- **上傳 XML**  
  CSP：[ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  讓 IT 系統管理員得以將代表想要的系統及應用程式風險降低選項設定，推送至組織中的所有裝置。 此設定以 XML 檔案表示。 惡意探索保護可協助保護裝置，以防惡意程式碼利用惡意探索散播和感染。 您可以使用 Windows 安全性應用程式或 PowerShell 建立風險降低集合 (稱為設定)。 然後，您可以將此設定匯出為 XML 檔案，並在您網路上的多部電腦之間共用，以便所有檔案都有相同的風險降低設定集合。 您也可以將現有的 EMET 設定 XML 檔案轉換並匯入到惡意探索保護設定 XML。

  選擇 [選取 XML 檔案]，指定 XML 檔案上傳，然後按一下 [選取]。
  - [未設定] (預設)
  - **是**

- **禁止使用者編輯惡意探索防護保護介面**  
  CSP：[DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **未設定** (預設) - 本機使用者可以在惡意探索保護設定區域中進行變更。
  - **是** - 防止使用者對 Microsoft Defender 資訊安全中心的惡意探索保護設定區域進行變更。

## <a name="next-steps"></a>後續步驟

[ASR 端點安全性原則](../protect/endpoint-security-asr-policy.md)
