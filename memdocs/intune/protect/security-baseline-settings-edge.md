---
title: 適用於 Microsoft Edge 的 Intune 安全性基準設定
titleSuffix: Microsoft Intune
description: 由 Intune 支援、用於管理 Microsoft Edge 瀏覽器的安全性基準設定
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 623752d0eaf2742e21a78c688d58cd062f87ed52
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351210"
---
# <a name="microsoft-edge-baseline-settings-for-intune"></a>Intune 的 Microsoft Edge 基準設定

檢視 Microsoft Intune 支援的 Microsoft Edge 網頁瀏覽器基準設定。 Microsoft Edge 基準預設代表 Microsoft Edge 瀏覽器建議的設定，可能不符合其他安全性基準的基準預設。

> [!NOTE]
> Microsoft Edge 基準處於公開預覽狀態。 

## <a name="microsoft-edge"></a>Microsoft Edge

- **防止略過站台的 Microsoft Defender SmartScreen 提示**  
  **預設**：已啟用  
  Microsoft Edge CSP：[Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  此原則設定可供決定使用者是否可以覆寫 Microsoft Defender SmartScreen 有關潛在惡意網站的警告。 
  - 如果啟用此設定，使用者就無法忽略 Microsoft Defender SmartScreen 警告，且使用者會遭到封鎖而無法繼續前往網站。 
  - 如果停用或未設定此設定，使用者可以忽略 Microsoft Defender SmartScreen 警告並繼續前往網站。

- **已啟用最低 SSL 版本**  
  **預設**：已啟用  

  設定 SSL 的最低支援版本。 如果將此原則設定為 [未設定]  ，Microsoft Edge 會使用 *TLS 1.0* 的預設最低版本。 當設定為 [已啟用]  時，即可從下列值選取最低版本：

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **已啟用最低 SSL 版本**  
    **預設**：TLS 1.2

- **防止略過關於下載的 Microsoft Defender SmartScreen 警告**  
  **預設**：已啟用  
  Microsoft Edge CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  此原則可供判斷使用者是否可以覆寫 Microsoft Defender SmartScreen 有關未經驗證下載的警告。
  - 如果啟用此原則，則組織中的使用者就無法忽略 Microsoft Defender SmartScreen 警告，且會阻止使用者完成未經驗證的下載。
  - 如果停用或未設定此原則，使用者可以忽略 Microsoft Defender SmartScreen 警告並完成未經驗證的下載。

- **允許使用者從 SSL 警告頁面繼續**  
  **預設**：停用  
  Microsoft Edge CSP：[Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  當使用者瀏覽具有 SSL 錯誤的網站時，Microsoft Edge 會顯示警告頁面。 如果將此原則設定為 [已啟用]  或 [未設定]  ，則使用者可以點選這些警告頁面。 當此原則為 [已停用]  時，使用者會遭到封鎖而無法點選任何警告頁面。 

- **預設 Adobe Flash 設定**  
  **預設**：已啟用  
  Microsoft Edge CSP：[Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash)，以及 [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  判斷 'PluginsAllowedForUrls' 或 'PluginsBlockedForUrls' 未涵蓋的網站是否可以自動執行 Adobe Flash 外掛程式。 

  - 選取 [BlockPlugins] 以封鎖所有網站上的 Adobe Flash
  - 選取 [ClickToPlay] 以讓 Adobe Flash 執行，但要求使用者按一下預留位置加以啟動。
  
   在任何情況下，'PluginsAllowedForUrls' 和 'PluginsBlockedForUrls' 原則的優先順序會高於 'DefaultPluginsSetting'。 只有在 'PluginsAllowedForUrls' 原則中明確列出的網域才允許自動播放。 
   如果想要啟用所有網站的自動播放，請考慮將 http://* 和 https://* 新增至此清單。 
   
   - 如果將此原則設定為 [未設定]  ，則使用者可以手動變更此設定。 * 2 = 封鎖 Adobe Flash 外掛程式 * 3 = 按一下播放原本的 '1' 選項設定為全部允許，但這項功能現在只能由 'PluginsAllowedForUrls' 原則處理。 使用 '1' 的現有原則將會以「按一下播放」模式運作。  
 
  - **預設 Adobe Flash 設定**  
    **預設**：封鎖 Adobe Flash 外掛程式

- **針對所有站台啟用站台隔離**  
  **預設**：已啟用  

  'SitePerProcess' 原則可用來防止使用者退出隔離所有站台的預設行為。 您也可以使用 IsolateOrigins 原則來隔離其他的更精細來源。

  - 當此原則設定為 [已啟用]  時，使用者無法退出每個站台在其處理程序中執行的預設行為。 
  - 如果使用 [已停用]  或 [未設定]  ，使用者就可以退出站台隔離。 (例如，在 edge://flags 中使用「停用站台隔離」項目。)停用原則或未設定該原則，並不會關閉站台隔離。

- **支援的驗證配置**  
  **預設**：已啟用  

  指定支援的 HTTP 驗證配置。 您可以使用下列值來設定原則：'basic'、'digest'、'ntlm' 和 'negotiate'。 請使用逗號分隔多個值。 如果未設定此原則，則會使用所有四種配置。
 
  - **支援的驗證配置**  
    從下列選項選取： 
    - 基本
    - Digest
    - NTLM *(預設已選取)*
    - Negotiate (預設已選取) 

- **啟用將密碼儲存到密碼管理員**  
  **預設**：停用  
  Microsoft Edge CSP：[Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  啟用 Microsoft Edge 以儲存使用者密碼。 
  - 如果啟用此原則，使用者可以將其密碼儲存在 Microsoft Edge 中。 下一次前往站台時，Microsoft Edge 會自動輸入密碼。 
  - 如果停用此原則，使用者就無法儲存新密碼，但仍然可以使用先前儲存的密碼。 
  
  當將此原則設定為 [已啟用]  或 [已停用]  時，使用者無法在 Microsoft Edge 中變更或覆寫此原則。 
  
  如果將此原則設定為 [未設定]  ，使用者就可以儲存密碼，以及關閉這項功能。

- **控制無法安裝的延伸模組**  
  **預設**：已啟用  

  列出使用者無法在 Microsoft Edge 中安裝的特定延伸模組。 當部署此原則時，會停用此清單上先前安裝的任何延伸模組，且使用者將無法啟用這些延伸模組。 如果從封鎖的延伸模組清單中移除某個項目，該延伸模組會在其先前安裝的任何位置上自動重新啟用。
  
  使用 **\*** 來封鎖未明確列在允許清單中的所有延伸模組。 如果此原則設定為 [未設定]  ，使用者就可以在 Microsoft Edge 中安裝任何延伸模組。 
  
  範例值：extension_id1 extension_id2。  
  <br>
  - **應禁止使用者安裝的延伸模組識別碼 (輸入 * 代表全部)**  
    選取 [新增]  並指定其他延伸模組。 **\*** 預設已選取。

- **設定 Microsoft Defender SmartScreen**  
  **預設**：已啟用  
  Microsoft Edge CSP：[Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  此原則設定可供設定是否要開啟 Microsoft Defender SmartScreen。 Microsoft Defender SmartScreen 提供一些警告訊息，以協助保護使用者免於遭受潛在的網路釣魚詐騙和惡意軟體攻擊。 
  
  - 根據預設，Microsoft Defender SmartScreen 已開啟。 如果啟用此設定，則會開啟 Microsoft Defender SmartScreen，且使用者無法將其關閉。
  - 如果停用此設定，則會關閉 Microsoft Defender SmartScreen，且使用者無法將其開啟。 
  - 當設定為 [未設定]  時，使用者可以選擇是否要使用 Microsoft Defender SmartScreen。 
  
  此原則僅適用於已加入 Microsoft Active Director 網域的 Windows 執行個體，或已註冊進行裝置管理的 Windows 10 專業版或企業版執行個體。

- **允許使用者層級原生傳訊主機 (在沒有系統管理員權限的情況下安裝)**  
  **預設**：停用  

  啟用原生傳訊主機的使用者層級安裝。 
  - 如果停用此原則，Microsoft Edge 只會使用安裝在系統層級上的原生傳訊主機。 根據預設，如果未設定此原則，Microsoft Edge 會允許使用使用者層級的原生傳訊主機。

## <a name="next-steps"></a>後續步驟

[在 Intune 中使用安全性基準](security-baselines.md)
