---
title: Intune 之 Windows 安全性體驗的 Windows 10 防毒軟體原則設定 | Microsoft Docs
description: Microsoft Intune 之 Windows 安全性應用程式的端點安全性防毒軟體原則設定
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
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431731"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Microsoft Intune 中 Windows 安全性體驗設定檔的設定

為完善[端點安全性原則](../protect/endpoint-security-policy.md)，檢視您在 Microsoft Intune 中，可針對 Windows 10 的 **Windows 安全性體驗** 設定檔設定的防毒軟體原則設定。

**Windows 安全性**

- **啟用竄改防護以免無法使用 Microsoft Defender**  
  [使用竄改防護以免安全性設定遭變更](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **未設定** (預設) - 當用戶端存在*啟用*或*停用*狀態時，部署「未設定」不會影響設定。 
  - **啟用** - 啟用竄改防護限制。 若要變更啟用或停用狀態，請部署相反的設定使其生效。
  - **停用** - 停用竄改防護限制。 若要變更啟用或停用狀態，請部署相反的設定使其生效。

- **隱藏 Windows 安全性應用程式的病毒與威脅防護區域**  
  CSP：[DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的病毒與威脅防護區域。 隱藏病毒與威脅防護相關的通知。

  - **隱藏 Windows 安全性應用程式中的勒索軟體資料復原選項**  
    CSP：[](https://go.microsoft.com/fwlink/?linkid=873664)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的勒索軟體資料復原區域。 隱藏勒索軟體的相關通知。

- **隱藏 Windows 安全性應用程式中的帳戶保護區域**  
  CSP：[DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的帳戶保護區域。 隱藏帳戶保護的相關通知。

- **隱藏 Windows 安全性應用程式中的防火牆與網路保護區域**  
  CSP：[DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的防火牆與網路保護區域。 隱藏防火牆與網路保護的相關通知。

- **隱藏 Windows 安全性應用程式中的應用程式與瀏覽器控制區域**  
  CSP：[DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性中的應用程式與瀏覽器控制區域。 隱藏應用程式和瀏覽器控制項的相關通知。

- **隱藏 Windows 安全性應用程式中的裝置安全性區域**  
  CSP：[DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的便體保護區域。 這會隱藏硬體保護的相關通知。
  
- **隱藏 Windows 安全性應用程式中的裝置效能與健全狀況區域**  
  CSP：[DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的裝置效能與健全狀況區域。 隱藏裝置效能與健全狀況的相關通知

- **隱藏 Windows 安全性應用程式中的家長監護選項區域**  
  CSP：[DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許使用者存取及通知。
  - [是] - 向使用者隱藏 Windows 安全性應用程式的家長監護選項區域。 這也會隱藏家長監護選項區域的相關通知。

- **Windows 安全性應用程式通知**  
  CSP：[](https://go.microsoft.com/fwlink/?linkid=873675)

  使用此設定可封鎖上述所有功能設定的 Windows 安全性通知，向使用者隱藏所有設定通知。 或者，您也可以使用上述設定，依功能管理 Windows 安全性代理程式通知。

  - **未設定** (預設) - 允許不受其他設定控制的所有 Windows 安全性應用程式通知。
  - **封鎖非嚴重通知** - 封鎖掃描完成之類的通知。
  - **封鎖所有通知** - 封鎖所有 Windows 安全性功能的嚴重和非嚴重通知。

- **隱藏通知區域中的 Windows 安全性圖示**  
  CSP：[HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  使用者必須登出後登入，或重新啟動電腦，此設定才會生效。
  - **未設定** (預設) - 此設定會將用戶端還原為預設，顯示圖示。
  - [是] - 隱藏使用者系統匣中的 Windows 安全性圖示。
  
- **停用 Windows 安全性應用程式中的 [清除 TPM] 選項**  
  CSP：[DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **未設定** (預設) - 此設定會還原為用戶端預設，允許存取此按鈕。
  - [是] - 停用存取 Windows 安全性應用程式的 [清除 TPM] 按鈕。

- **如果發現弱點，則提示使用者更新 TPM 韌體**  
  CSP：[DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **未設定** (預設) - 此設定會還原為用戶端預設，不向使用者發出提示。
  - [是] - 允許 Windows 提示使用者在 TPM 韌體中發現可能的弱點。 然後建議使用者執行韌體更新以解決此弱點。

- **組織的支援連絡人資訊**  
  CSP：[EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  宣告您要在 Windows 安全性應用程式和通知中顯示 IT 組織資訊的位置。
  - [未設定] (預設)
  - **顯示在應用程式與通知中**
  - **只顯示在應用程式中**
  - **只顯示在通知中**