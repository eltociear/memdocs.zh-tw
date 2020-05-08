---
title: Microsoft Defender 進階威脅防護的 Intune 安全性基準設定
titleSuffix: Microsoft Intune
description: 由 Intune 支援、用於管理 Microsoft Defender 進階威脅防護的安全性基準設定Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: e1081395c733807c38dc940ebd1b7c2765da7a9a
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693403"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Intune 的 Microsoft Defender 進階威脅防護基準設定

檢視 Microsoft Intune 支援的 Microsoft Defender 進階威脅防護基準設定。 進階威脅防護 (ATP) 基準預設值代表 ATP 建議的設定，可能不符合其他安全性基準的基準預設值。

::: zone pivot="atp-april-2020"

本文中詳細資料適用於 2020 年 4 月 21 日發行的第 4 版 Microsoft Defender ATP 基準。 若要了解此基準版本與先前版本相較之下的變更內容，請使用檢視此基準 [版本]  窗格時可取得的[比較基準](../protect/security-baselines.md#compare-baseline-versions)動作。

::: zone-end
::: zone pivot="atp-march-2020"

本文中詳細資料適用於 2020 年 3 月 1 日發行的第 3 版 Microsoft Defender ATP 基準。 若要了解此基準版本與先前版本相較之下的變更內容，請使用檢視此基準 [版本]  窗格時可取得的[比較基準](../protect/security-baselines.md#compare-baseline-versions)動作。

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


當您的環境符合使用 [Microsoft Defender 進階威脅防護](advanced-threat-protection.md#prerequisites)的必要條件時，即可使用 Microsoft Defender 進階威脅防護基準。

此基準會針對實體裝置最佳化，目前不建議用於虛擬機器 (VM) 或 VDI 端點。 特定基準設定可能會影響虛擬化環境上的遠端互動式工作階段。 如需詳細資訊，請參閱 Windows 文件中的[提高 Microsoft Defender ATP 安全性基準的合規性](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) \(英文\)。


## <a name="application-guard"></a>應用程式防護

如需詳細資訊，請參閱 Windows 文件中的 [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) \(英文\)。  

使用 Microsoft Edge 時，Microsoft Defender 應用程式防護可保護您的環境免受組織不信任之網站的影響。 當使用者瀏覽未列在隔離之網路界限中的網站時，這些網站將在 Hyper-V 虛擬瀏覽工作階段中開啟。 信任的網站是由網路界限定義的。  

- **為 Edge 開啟應用程式防護 (選項)**  
  CSP：[Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **為 Edge 啟用** (預設  ) - 應用程式防護會在 Hyper-V 虛擬化瀏覽容器中開啟未核准的網站。
  - **未設定** - 所有網站 (受信任與未受信任) 都會在裝置上開啟，而非在虛擬化容器中開啟。  
  
  設定為 [為 Edge 啟用]  時，即可設定 [禁止未經企業所核准網站的外部內容]  和 [剪貼簿行為]  。

  - **禁止未經企業所核准網站的外部內容**  
    CSP：[Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **是** (預設  ) - 禁止來自未核准網站的內容載入。
    - **未設定** - 非企業網站可在裝置上開啟

  - **剪貼簿行為**  
    CSP：[Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    選擇要在本機電腦和應用程式防護虛擬瀏覽器之間允許的複製與貼上動作。 這些選項包括：
    - **尚未設定**  
    - **禁止電腦和瀏覽器之間的複製並貼上** (預設  ) - 封鎖這兩者。 資料無法在電腦與虛擬瀏覽器之間傳輸。
    - **僅允許從瀏覽器到電腦的複製並貼上** - 資料無法從電腦傳輸到虛擬瀏覽器。
    - **僅允許從電腦到瀏覽器的複製並貼上** - 資料無法從虛擬瀏覽器傳輸到電腦。
    - **允許電腦和瀏覽器之間的複製並貼上** - 不封鎖內容。

- **Windows 網路隔離原則**  
  CSP：[原則 CSP - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation) (機器翻譯)

  指定 [網路網域]  清單，這是裝載於雲端的企業資源，應用程式防護會將其視為企業網站
  - **設定** (預設  )
  - **未設定**

  設定為 [設定]  時，即可接著定義 [網路網域]  。

  - **網路網域**  
    選取 [新增]  ，然後指定網域、IP 位址範圍和網路界限。 預設會設定 *securitycenter.windows.com*。

## <a name="bitlocker"></a>BitLocker

如需詳細資訊，請參閱 Windows 文件中的 [BitLocke 群組原則設定](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) \(部分機器翻譯\)。

- **需要加密儲存卡 (僅限行動裝置)**  
  CSP：[RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  此設定僅適用於 Windows 行動裝置版和行動裝置企業版 SKU 裝置。
  - **是** (預設  ) - 行動裝置需要加密儲存卡。
  - **未設定** - 此設定會還原為 OS 預設值，也就是不需要加密儲存卡。

- **為 OS 及固定資料磁碟機啟用完整的磁碟加密**  
  CSP：[RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  如果磁碟機在套用此原則之前已加密，則不會採取任何額外的動作。 如果加密方法和選項符合此原則，則設定應該會傳回成功。 如果現有的 BitLocker 設定選項不符合此原則，則設定可能會傳回錯誤。
  
  若要將此原則套用至已加密的磁碟，請將磁碟機解密，再重新套用 MDM 原則。 Windows 預設值為不需要 BitLocker 磁碟機加密，但在 Azure AD Join 和 Microsoft 帳戶 (MSA) 註冊/登入時，自動加密可能會在 XTS-AES 128 位元加密啟用 BitLocker。

  - **是** (預設  ) - 強制使用 BitLocker。
  - **未設定** - 不強制使用 BitLocker。

- **BitLocker 系統磁碟機原則**  
  [BitLocker 群組原則設定](https://go.microsoft.com/fwlink/?linkid=2067025) (機器翻譯)

  - **設定** (預設  )
  - **未設定**

  設定為 [設定]  時，即可接著設定 [設定作業系統磁碟機的加密方法]  。

  - **設定作業系統磁碟機的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    當 [BitLocker 系統磁碟機原則]  設定為 [設定]  時，即可使用此設定。  

    設定系統磁碟機的加密方法和加密強度。  「XTS-AES 128 位元」  是 Windows 預設加密方法和建議值。

    - [未設定]  (預設  )
    - **AES 128 位元 CBC**
    - **AES 256 位元 CBC**
    - **AES 128 位元 XTS**
    - **AES 256 位元 XTS**

- **BitLocker 固定磁碟機原則**  
  [BitLocker 群組原則設定](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **設定** (預設  )
  - **未設定**

  設定為 [設定]  時，即可接著設定 [禁止寫入未受 BitLocker 保護的固定資料磁碟機]  和 [設定固定資料磁碟機的加密方法]  。

  - **禁止寫入未受 BitLocker 保護的固定資料磁碟機**  
    CSP：[FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    當 [BitLocker 固定磁碟機原則]  設定為 [設定]  時，即可使用此設定。

    - **未設定** (預設  ) - 可將資料寫入未加密的固定磁碟機。
    - **是** - Windows 不允許將任何資料寫入未受 BitLocker 保護的固定磁碟機。 若固定磁碟機未加密，則使用者必須先為磁碟機完成 BitLocker 安裝精靈，才能授與寫入權限。

  - **設定固定資料磁碟機的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    當 [BitLocker 固定磁碟機原則]  設定為 [設定]  時，即可使用此設定。

    設定固定資料磁碟機磁碟的加密方法和加密強度。 「XTS-AES 128 位元」  是 Windows 預設加密方法和建議值。

    - [未設定]  (預設  )
    - **AES 128 位元 CBC**
    - **AES 256 位元 CBC**
    - **AES 128 位元 XTS**
    - **AES 256 位元 XTS**

- **BitLocker 抽取式磁碟機原則**  
  [BitLocker 群組原則設定](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **設定** (預設  )
  - **未設定**

  設定為 [設定]  時，即可接著設定 [設定抽取式資料磁碟機的加密方法]  和 [禁止寫入未受 BitLocker 保護的抽取式資料磁碟機]  。

  - **設定抽取式資料磁碟機的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    當 [BitLocker 抽取式磁碟機原則]  設定為 [設定]  時，即可使用此設定。

    設定抽取式資料磁碟機磁碟的加密方法和加密強度。 「XTS-AES 128 位元」  是 Windows 預設加密方法和建議值。

    - **未設定**
    - **AES 128 位元 CBC**
    - **AES 256 位元 CBC** (預設  )
    - **AES 128 位元 XTS**
    - **AES 256 位元 XTS**

  - **禁止寫入未受 BitLocker 保護的抽取式資料磁碟機**  
    CSP：[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    當 [BitLocker 抽取式磁碟機原則]  設定為 [設定]  時，即可使用此設定。

    - **未設定** (預設  ) - 可將資料寫入未加密的抽取式磁碟機。  
    - **是** - Windows 不允許將任何資料寫入未受 BitLocker 保護的抽取式磁碟機。 若抽取式磁碟機未加密，則使用者必須先為磁碟機完成 BitLocker 安裝精靈，才能授與寫入權限。

## <a name="browser"></a>瀏覽器

- **Microsoft Edge 需要 SmartScreen**  
  CSP：[Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **是** (預設  ) - 使用 SmartScreen 保護使用者免於潛在的網路釣魚詐騙和惡意軟體攻擊。
  - **未設定**

- **封鎖惡意網站存取**  
  CSP：[Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **是** (預設  ) - 禁止使用者略過 Microsoft Defender SmartScreen 篩選工具警告，並防止其進入網站。
  - **未設定**

- **封鎖未經驗證的檔案下載**  
  CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **是** (預設  ) - 禁止使用者略過 Microsoft Defender SmartScreen 篩選工具警告，並防止其下載未經驗證的檔案。
  - **未設定**

## <a name="data-protection"></a>資料保護

- **封鎖直接記憶體存取**  
  CSP：[DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031) \(英文\)  

  只有在啟用 BitLocker 或裝置加密時，才會強制執行此原則設定。

  - **是** (預設  ) - 禁止所有隨插即用 PCI 下游連接埠的直接記憶體存取 (DMA)，直到使用者登入 Windows 為止。 使用者登入後，Windows 就會列舉連接至隨插即用 PCI 連接埠的 PCI 裝置。 只要使用者鎖定電腦，在使用者再次登入之前，將會在沒有子裝置的隨插即用 PCI 連接埠上封鎖 DMA。 電腦解除鎖定時已列舉的裝置將繼續運作，直到遭拔除為止。
  - **未設定**

## <a name="device-guard"></a>Device Guard  

- **開啟 Credential Guard**  
  CSP：[DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard 使用 Windows Hypervisor 來提供保護，這需要安全開機和 DMA 保護運作正常，因此必須符合硬體需求。

  - **未設定** - 停用 Credential Guard (Windows 預設值為啟用)。
  - **啟用且具備 UEFI 鎖定** (預設  ) - 啟用 Credential Guard，且不允許從遠端將其停用，因為必須手動清除 UEFI 保存的設定。
  - **啟用但不具備 UEFI 鎖定** - 啟用 Credential Guard，且允許在不實際存取電腦的情況下將其關閉。

## <a name="device-installation"></a>裝置安裝

- **依裝置識別碼的硬體裝置安裝**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  此原則設定可讓您針對 Windows 防止安裝的裝置，指定隨插即用硬體識別碼與相容識別碼的清單。 此原則設定優先於任何其他允許 Windows 安裝裝置的原則設定。  如果您在遠端桌面伺服器上啟用此原則設定，此原則設定會影響指定裝置從遠端桌面用戶端到遠端桌面伺服器的重新導向。

  - **未設定**
  - **允許硬體裝置安裝** - 其他原則設定可允許或防止安裝及更新裝置。
  - **禁止硬體裝置安裝** (預設  ) - 防止 Windows 安裝其硬體識別碼或相容識別碼出現在所定義清單中的裝置。

  設定為 [禁止硬體裝置安裝]  時，即可設定 [移除相符的硬體裝置]  和 [封鎖的硬體裝置識別碼]  。

  - **移除相符的硬體裝置**

    只有在 [依裝置識別碼的硬體裝置安裝]  設定為 [封鎖硬體裝置安裝]  時，才能使用此設定。
    - **是**
    - **未設定**

  - **已封鎖的硬體裝置識別碼**  
    
    只有在 [依裝置識別碼的硬體裝置安裝]  設定為 [封鎖硬體裝置安裝]  時，才能使用此設定。

    選取 [新增]  ，然後指定所要封鎖的硬體裝置識別碼。

- **依安裝類別的硬體裝置安裝**  
  CSP：[DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  此原則設定可讓您針對 Windows 防止安裝的裝置驅動程式，指定裝置安裝類別全域唯一識別碼 (GUID) 的清單。 此原則設定優先於任何其他允許 Windows 安裝裝置的原則設定。 如果您在遠端桌面伺服器上啟用此原則設定，此原則設定會影響指定裝置從遠端桌面用戶端到遠端桌面伺服器的重新導向。

  - **未設定**
  - **允許硬體裝置安裝** - 其他原則設定可允許或防止 Windows 安裝及更新裝置。
  - **禁止硬體裝置安裝** (預設  ) - 防止 Windows 安裝其安裝類別 GUID 出現在所定義清單中的裝置。

  設定為 [禁止硬體裝置安裝]  時，即可設定 [移除相符的硬體裝置]  和 [封鎖的硬體裝置識別碼]  。

  - **移除相符的硬體裝置**

    只有在 [依裝置識別碼的硬體裝置安裝]  設定為 [封鎖硬體裝置安裝]  時，才能使用此設定。
    - **是**
    - **未設定**

  - **已封鎖的硬體裝置識別碼**

    只有在 [依裝置識別碼的硬體裝置安裝]  設定為 [封鎖硬體裝置安裝]  時，才能使用此設定。

    選取 [新增]  ，然後指定所要封鎖的硬體裝置識別碼。

## <a name="dma-guard"></a>DMA 保護

- **列舉與 Kernel DMA Protection 不相容的外部裝置**  
  CSP：[DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  此原則可以提供外部 DMA 裝置的額外安全性。 它可讓您更有效地控制與 DMA 重新對應/裝置記憶體隔離和沙箱處理不相容之外部 DMA 裝置的列舉。
  
  只有當支援 Kernel DMA Protection 並由系統韌體啟用它時，此原則才會生效。 Kernel DMA Protection 是系統製造時必須支援的平台功能。 若要檢查系統是否支援 Kernel DMA Protection，請檢查 MSINFO32.exe [摘要] 頁面中的 [Kernel DMA Protection] 欄位。

  - **未設定** - (*預設*)
  - **全部封鎖**
  - **全部允許**

## <a name="endpoint-detection-and-response"></a>端點偵測與回應

如需下列設定的詳細資訊，請參閱 Windows 文件中的 [WindowsAdvancedThreatProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) (機器翻譯)。

- **所有檔案的範例共用**  
  CSP：[Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  傳回或設定 Microsoft Defender 進階威脅防護範例共用設定參數。  
  
  - **是** (預設  )
  - **未設定**

- **加快遙測回報頻率**  
  CSP：[Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  加快 Microsoft Defender 進階威脅防護遙測回報頻率。  

  - **是** (預設  )
  - **未設定**

## <a name="firewall"></a>防火牆

如需詳細資訊，請參閱 Windows 文件中的[防火牆 CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) \(英文\)。

- **停用具狀態檔案傳輸通訊協定 (FTP)**  
  CSP：[MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **是** (預設  )
  - **未設定** - 防火牆將會使用 FTP 來檢查及篩選次要網路連線，但可能會因此而略過防火牆規則。

- **刪除安全性關聯前的閒置秒數**  
CSP：[MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  指定保留安全性關聯的時間長度，之後將不會再看到網路流量。 若未設定，則系統會在閒置 *300* 秒 (預設值) 後刪除安全性關聯。
  
  此數值必須介於 **300** 到 **3600** 秒之間。

- **預先共用金鑰編碼**  
  CSP：[MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   若不需要 UTF-8，則預先共用金鑰一開始將會使用 UTF-8 編碼。 在此之後，裝置使用者可以選擇其他編碼方法。

  - **未設定**
  - **無**
  - **UTF8** (預設  )

- **憑證撤銷清單 (CRL) 驗證**  
  CSP：[MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  指定憑證撤銷清單 (CRL) 驗證的強制執行方式。  

  - **未設定** (預設  ) - 停用 CRL 驗證。
  - **無**
  - **嘗試**
  - **需要**

- **封包佇列**  
  CSP：[MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  指定如何啟用接收端軟體的規模調整，處理 IPsec 通道閘道案例中加密的接收和純文字轉送。 此設定可確保保留封包順序。

  - **未設定** (預設  ) - 封包佇列會還原為用戶端預設值，也就是停用。
  - **停用**
  - **輸入佇列**
  - **輸出佇列**
  - **將兩者放入佇列**

- **私人的防火牆設定檔**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **設定** (預設  )
  - **未設定**

  設定為 [設定]  時，即可進行下列其他設定。

  - **已封鎖輸入連線**  
    CSP：[/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **是** (預設  )
    - **未設定**

  - **需要多點傳送廣播的單點傳播回應**  
    CSP：[/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **是** (預設  )
    - **未設定**

  - **需要隱形模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是** (預設  )
    - **未設定**

  - **需要輸出連線**  
    CSP：[/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **是** (預設  )
    - **未設定**

  - **已封鎖輸入通知**  
    CSP：[/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **是** (預設  )
    - **未設定**

  - <bpt id="p1">**</bpt>Global port rules from group policy merged<ept id="p1">**</ept>  
    CSP：[/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **是** (預設  )
    - **未設定**

  - **已封鎖隱形模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是** (預設  )
    - **未設定**

  - **已啟用防火牆**  
    CSP：[/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **未設定**
    - **封鎖**
    - **允許** (預設  )

  - **來自群組原則的授權應用程式規則未合併**  
    CSP：[/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **是** (預設  )
    - **未設定**

  - **來自群組原則的連線安全性規則已合併**  
    CSP：[/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **是** (預設  )
    - **未設定**

  - **需要連入流量**  
    CSP：[/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **是** (預設  )
    - **未設定**

  - **來自群組原則的原則規則已合併**  
    CSP：[/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **是** (預設  )
    - **未設定**

- **公用的防火牆設定檔**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **設定** (預設  )
  - **未設定**

  設定為 [設定]  時，即可進行下列其他設定。

  - **已封鎖輸入連線**  
    CSP：[/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **是** (預設  )
    - **未設定**

  - **需要多點傳送廣播的單點傳播回應**  
    CSP：[/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **是** (預設  )
    - **未設定**

  - **需要隱形模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是** (預設  )
    - **未設定**

  - **需要輸出連線**  
    CSP：[/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **是** (預設  )
    - **未設定**

  - **來自群組原則的授權應用程式規則未合併**  
    CSP：[/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **是** (預設  )
    - **未設定**

  - **已封鎖輸入通知**  
    CSP：[/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **是** (預設  )
    - **未設定**

  - <bpt id="p1">**</bpt>Global port rules from group policy merged<ept id="p1">**</ept>  
    CSP：[/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **是** (預設  )
    - **未設定**

  - **已封鎖隱形模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是** (預設  )
    - **未設定**

  - **已啟用防火牆**  
    CSP：[/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **未設定**
    - **封鎖**
    - **允許** (預設  )

  - **來自群組原則的連線安全性規則已合併**  
    CSP：[/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **是** (預設  )
    - **未設定**

  - **需要連入流量**  
    CSP：[/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **是** (預設  )
    - **未設定**

  - **來自群組原則的原則規則已合併**  
    CSP：[/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **是** (預設  )
    - **未設定**

- **防火牆設定檔網域**  
  CSP：[2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **需要多點傳送廣播的單點傳播回應**  
    CSP：[/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **來自群組原則的授權應用程式規則未合併**  
    CSP：[/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **是** (預設  )
    - **未設定**  

  - **已封鎖輸入通知**  
    CSP：[/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **是** (預設  )
    - **未設定**

  - <bpt id="p1">**</bpt>Global port rules from group policy merged<ept id="p1">**</ept>  
    CSP：[/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **是** (預設  )
    - **未設定**

  - **已封鎖隱形模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是** (預設  )
    - **未設定**

  - **已啟用防火牆**  
    CSP：[/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **未設定**
    - **封鎖**
    - **允許** (預設  )

  - **來自群組原則的連線安全性規則已合併**  
    CSP：[/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **是** (預設  )
    - **未設定**

  - **來自群組原則的原則規則已合併**  
    CSP：[/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **是** (預設  )
    - **未設定**

## <a name="microsoft-defender"></a>Microsoft Defender

- **每日快速掃描的執行時間**  
  CSP：[Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   設定每日快速掃描的執行時間。 根據預設，掃描執行設定為 [上午 2 點]  。

- **排定的掃描開始時間**  
  
  根據預設，這會設定為 [上午 2 點]  。

- **設定已排定之掃描的低 CPU 優先順序**  
  CSP：[Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**是** (預設  )
  - **未設定**

- **禁止 Office 通訊應用程式建立子處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874499) (機器翻譯)  

  這項 ASR 規則是透過下列 GUID 來控制：26190899-1602-49e8-8b27-eb1d0a1ce869。
  - **未設定** - 已還原 Windows 預設值，也就是不禁止建立子處理序。
  - **使用者定義**
  - **啟用** (預設  ) - 禁止 Office 通訊應用程式建立子處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖子處理序。

- **禁止 Adobe Reader 建立子處理序**  
  [使用受攻擊面縮小規則來縮小受攻擊面](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **未設定** - 已還原 Windows 預設值，也就是不禁止建立子處理序。
  - **使用者定義**
  - **啟用** (預設  ) - 禁止 Adobe Reader 建立子處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖子處理序。

- **掃描內送電子郵件訊息**  
  CSP：[Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **是** (預設  ) - 掃描電子郵件信箱與郵件檔案，例如 PST、DBX、MNX、MIME 及 BINHEX。
  - **未設定** - 此設定會還原為用戶端預設值，也就是不掃描電子郵件檔案。

- **開啟即時保護**  
  CSP：[Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **是** (預設  ) - 強制執行即時監視，且使用者無法將其停用。
  - **未設定** - 此設定會還原為用戶端預設值，也就是開啟，但使用者可予以變更。 若要停用即時監視，請使用自訂 URI。

- **隔離惡意程式碼後的保留天數 (0-90)**  
  CSP：[Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  設定項目從隔離資料夾中移除前應保留的天數。 預設值為零 (**0**)，這會導致絕不移除隔離的檔案。

- **Defender 系統掃描排程**  
  CSP：[Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  排定 Defender 將在哪天掃描裝置。 根據預設，掃描為 [使用者定義]  ，但可設定為 [每天]  、一週中的任何一天或 [未排程任何掃描]  。

- **加上額外的時間 (0-50 秒)，以延長雲端保護逾時**  
  CSP：[Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender 防毒軟體會自動封鎖可疑的檔案 10 秒，使其可以掃描雲端的檔案，以確保其安全無虞。 使用此設定時，您最多可以對此逾時額外加上 50 秒。  根據預設，逾時設定為零 (**0**)。

- **在完整掃描期間掃描對應的網路磁碟機**  
  CSP：[Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **是** (預設  ) - 在完整掃描期間，包含對應的網路磁碟機。
  - **未設定** - 用戶端會還原為其預設值，也就是停用對應網路磁碟機的掃描。

- **開啟網路保護**  
  CSP：[Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **是** (預設  ) - 封鎖網路檢查系統 (NIS) 中簽章所偵測到的惡意流量。
  - **未設定**

- **掃描所有已下載的檔案和附件**  
  CSP：[Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **是** (預設  ) - 掃描所有已下載的檔案和附件。 此設定會還原為用戶端預設值，也就是開啟，但使用者可予以變更。 若要停用此設定，請使用自訂 URI。
  - **未設定** - 此設定會還原為用戶端預設值，也就是開啟，但使用者可予以變更。 若要停用此設定，請使用自訂 URI。

::: zone-end
::: zone pivot="atp-april-2020"

- **封鎖即時監視保護**  
  CSP：[Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **是**
  - [未設定]  (預設  )

::: zone-end
::: zone pivot="atp-march-2020"

- **封鎖即時監視保護**  
  CSP：[Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **是** (預設  )
  - **未設定**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **掃描瀏覽器指令碼**  
  CSP：[Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **是** (預設  ) - 強制執行 Microsoft Defender 指令碼掃描功能，且使用者無法將其關閉。
  - **未設定** - 此設定會還原為用戶端預設值，也就是啟用指令碼掃描，但使用者可予以關閉。

- **禁止使用者存取 Microsoft Defender 應用程式**  
  CSP：[Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **是** (預設  ) - 無法存取 Microsoft Defender 使用者介面 (UI)，且會隱藏通知
  - **未設定** - 設定為 [是] 時，無法存取 Microsoft Defender 使用者介面 (UI)，且會隱藏通知。 設定為 [未設定] 時，此設定會還原為用戶端預設值，其中允許 UI 與通知

- **每次掃描允許的最大 CPU 使用量 (0-100%)**  
  CSP：[Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  以百分比指定要用於掃描的最大 CPU 數量。 預設值為 **50**。

- **掃描類型**  
  CSP：[Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **使用者定義**
  - **停用**
  - **快速掃描** (預設  )
  - **完整掃描**

- **輸入檢查安全性情報更新的頻率 (0-24 小時)**  
  CSP：[Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  指定檢查是否有已更新簽章的頻率 (以小時為單位)。 例如，值為 1 將會每小時檢查一次。 值為 2 時，將會每隔兩小時檢查一次，依此類推。

  若未定義任何值，則裝置會使用 **8** 小時。

- [Defender 範例提交同意]   
  CSP：[Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  檢查 Microsoft Defender 中針對傳送資料的使用者同意層級。 如果已獲得必要的同意，Microsoft Defender 將會提交同意。 如果沒有 (而且指定了一律不再詢問使用者)，您可以啟動 UI，要求使用者同意 (當 [雲端提供的保護]  設定為 [是]*Yes* 時) 再傳送資料。

  - **自動傳送安全範例** (預設  )
  - **一律提示**
  - **一律不傳送**
  - **自動傳送所有樣本**

- **雲端提供的保護層級**  
  CSP：[CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  設定 Defender 防毒軟體在封鎖及掃描可疑檔案方面的主動性。
  - **未設定** (*預設*) - 預設的 Defender 封鎖層級。
  - **高** - 主動地封鎖未知的檔案，同時最佳化用戶端效能 (極可能發生誤判)。
  - **極高** - 主動地封鎖未知的檔案，並套用可能會影響用戶端效能的額外保護措施。
  - **零容錯** - 封鎖所有未知的可執行檔。

- **掃描封存檔**  
  CSP：[Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **是** (預設  ) - 強制掃描封存檔案 (例如 ZIP 或 CAB 檔案)。
  - **未設定** - 此設定會還原為用戶端預設值，也就是掃描封存檔案，但使用者可以停用掃描。

- **開啟行為監視**  
  CSP：[Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **是** (預設  ) - 強制執行行為監視，且使用者無法予以停用。
  - **未設定** - 此設定會還原為用戶端預設值，也就是開啟，但使用者可予以變更。 若要停用即時監視，請使用自訂 URI。
  
- **在完整掃描期間掃描抽取式磁碟機**  
  CSP：[Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **是** (預設  ) - 在完整掃描期間，掃描抽取式磁碟機 (例如 USB 快閃磁碟機)。
  - **未設定** - 此設定會還原為用戶端預設值，也就是掃描抽取式磁碟機，但使用者可以停用此掃描。
  
- **掃描網路檔案**  
  CSP：[Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **是** (預設  ) - Microsoft Defender 會掃描網路檔案。
  - **未設定** - 用戶端會還原為其預設值，也就是停用網路檔案的掃描。
  
- **Defender 潛在的垃圾應用程式動作**  
  CSP：[Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  指定潛在垃圾應用程式 (PUA) 的偵測層級。 Defender 會在下載潛在垃圾軟體或嘗試安裝在裝置上時，對使用者發出警示。
  - **裝置預設**
  - **封鎖** (預設  ) - 封鎖偵測到的項目，並與其他威脅一起顯示在歷程記錄中。
  - **稽核** - Defender 偵測到潛在垃圾應用程式，但不採取任何動作。 您可以搜尋 [事件檢視器] 中由 Defender 建立的事件，以檢閱 Defender 會對其採取動作之應用程式的相關資訊。

- **開啟雲端提供的保護**  
  CSP：[AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  根據預設，Windows 10 Desktop 裝置上的 Defender 會將所發現的任何問題的相關資訊傳送給 Microsoft。 Microsoft 會分析該資訊，以深入了解影響您與其他客戶的問題，並提供改善的解決方案。

  - **是** (預設  ) - 開啟雲端提供的保護。  裝置使用者無法變更此設定。
  - **未設定** - 此設定會還原為系統預設值。

- **禁止 Office 應用程式將程式碼插入其他處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872974) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - 禁止 Office 應用程式將程式碼插入其他處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止 Office 應用程式建立可執行的內容**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872975) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：3B576869-A4EC-4529-8536-B80A7769E899
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - 禁止 Office 應用程式建立可執行的內容。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。
  
- **禁止 JavaScript 與 VBScript 啟動下載的可執行內容**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872979) (機器翻譯)

   這項 ASR 規則是透過下列 GUID 來控制：D3E037E1-3EB8-44C8-A917-57927947596D
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - Defender 禁止執行從網際網路下載的 JavaScript 或 VBScript 檔案。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。
  
- **啟用網路保護**  
  CSP：[Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **未設定** - 此設定會還原為 Windows 預設值，也就是停用。
  - **使用者定義**
  - **啟用** - 為系統上的所有使用者啟用網路保護。
  - **稽核模式** (預設  ) - 不會禁止使用者存取危險網域，而是引發 Windows 事件。

- **封鎖從 USB 執行的不受信任和未簽署處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874502) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - 封鎖從 USB 磁碟機執行的未受信任與未簽署處理序。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **從 Windows 規則：封鎖竊取自 Windows 本機安全性授權子系統 (lsass.exe) 的認證**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=874499) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **使用者定義**
  - **啟用** (預設  ) - 禁止嘗試透過 lsass.exe 竊取認證。
  - **稽核模式** - 不會禁止使用者存取危險網域，而是引發 Windows 事件。

- **封鎖從電子郵件及網路郵件用戶端下載的可執行內容**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872980) (機器翻譯)

  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - 封鎖從電子郵件及網路郵件用戶端下載的可執行內容。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止所有 Office 應用程式建立子處理序**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872976) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  )
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **禁止執行可能經過混淆處理的指令碼 (js/vbs/ps)**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872978) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - Defender 將會禁止執行經過混淆處理的指令碼。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

- **封鎖來自 Office 巨集的 Win32 API 呼叫**  
  [防止裝置遭到入侵](https://go.microsoft.com/fwlink/?linkid=872977) (機器翻譯)

  這項 ASR 規則是透過下列 GUID 來控制：92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **未設定** - 此設定會還原為 Windows 預設值，也就是關閉。
  - **封鎖** (預設  ) - 禁止 Office 巨集使用 Win32 API 呼叫。
  - **稽核模式** - 引發 Windows 事件，而不是封鎖。

## <a name="microsoft-defender-security-center"></a>Microsoft Defender 資訊安全中心

- **禁止使用者編輯惡意探索防護保護介面**  
  CSP：[WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **是** (預設  ) - 防止使用者對 Microsoft Defender 資訊安全中心的惡意探索保護設定區域進行變更。
  - **未設定** - 本機使用者可以在惡意探索保護設定區域中進行變更。

## <a name="smart-screen"></a>Smart Screen

- **禁止使用者略過 SmartScreen 警告**  
  CSP：[SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   此設定需要啟用 [Enforce SmartScreen for apps and files' setting] \(施行應用程式及檔案適用的 SmartScreen\) 設定。
  - **是** (預設  ) - SmartScreen 不會顯示讓使用者略過警告並執行應用程式的選項。 警告會顯示，但使用者無法將其略過。
  - **未設定** - 此設定會還原為 Windows 預設值，也就是允許使用者覆寫。

- **要求僅限市集中的應用程式**  

  - **是** (預設  )
  - **未設定**

- **開啟 Windows SmartScreen**  
  CSP：[SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **是** (預設  ) - 強制所有使用者使用 SmartScreen。
  - **未設定** - 此設定會還原為 Windows 預設值，也就是啟用 SmartScreen，但使用者可以變更此設定。 若要停用 SmartScreen，請使用自訂 URI。

## <a name="windows-hello-for-business"></a>Windows Hello 企業版

如需詳細資訊，請參閱 Windows 文件中的 [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) \(英文\)。

- **封鎖 Windows Hello 企業版**  

   Windows Hello 企業版是一種能取代密碼、智慧卡及虛擬智慧卡來登入 Windows 的方法。

  - **未設定** - 裝置會佈建 Windows Hello 企業版，這是 Windows 預設值。
  - **停用** (預設  ) - 裝置會佈建 Windows Hello 企業版。
  - **啟用** - 裝置不會為任何使用者佈建 Windows Hello 企業版。

  設定為 [停用]  時，即可進行下列設定：

  - **PIN 中的小寫字母**  
    - **不允許**
    - **必要**
    - **允許** (預設  )

  - **PIN 中的特殊字元**
    - **不允許**
    - **必要**
    - **允許** (預設  )

  - **PIN 中的大寫字母**
    - **不允許**
    - **必要**
    - **允許** (預設  )

::: zone-end

## <a name="next-steps"></a>後續步驟

- [深入了解安全性基準](security-baselines.md)
- [避免衝突](security-baselines.md#avoid-conflicts)
- [針對 Intune 中的原則和設定檔進行疑難排解](../configuration/troubleshoot-policies-in-microsoft-intune.md)