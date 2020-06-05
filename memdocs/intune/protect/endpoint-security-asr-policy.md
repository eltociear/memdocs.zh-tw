---
title: 使用 Microsoft Intune 中的端點安全性原則管理受攻擊面縮小設定 | Microsoft Docs
description: 使用 Microsoft Intune 中之端點安全性受攻擊面縮小原則來設定及佈署您所管理的裝置原則
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
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431445"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Intune 中端點安全性的受攻擊面縮小原則

當您的 Windows 10 裝置使用 Defender 防毒軟體時，您可使用 Intune 中的端點安全性原則來縮小受攻擊面，以管理這些設定。

受攻擊面縮小原則可將您組織容易遭受網路威脅及攻擊的地方最小化，以協助縮小受攻擊面。 如需詳細資訊，請參閱 Windows 威脅防護文件中的[受攻擊面縮小概觀]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) (機器翻譯)。

在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)的 [端點安全性] 節點中，在 [管理] 下尋找縮小受攻擊面的端點安全性原則。 每個受攻擊面縮小「設定檔」會管理 Windows 10 裝置中特定區域的設定。

檢視[受攻擊面縮小設定檔的設定](../protect/endpoint-security-asr-profile-settings.md)。

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>受攻擊面縮小設定檔的必要條件

- Windows 10 或以上版本
- Defender 防毒軟體必須為裝置上的主要防毒軟體

## <a name="attack-surface-reduction-profiles"></a>受攻擊面縮小設定檔

**Windows 10 設定檔**：

- **應用程式和瀏覽器隔離** – 管理屬於 Defender ATP 的 Windows Defender 應用程式防護 (應用程式防護) 設定。 應用程式防護有助於防止舊有及新興的攻擊，並可在定義哪些網站、雲端資源和內部網路為可信任的同時，隔離企業定義為不信任的網站。

  若要深入了解，請參閱 Microsoft Defender ATP 文件中的[應用程式防護](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。

- **Web 防護** – 您在 Microsoft Defender ATP 中管理的 Web 防護設定，可以設定網路防護以保護您的電腦不受 Web 威脅。 透過與 Microsoft Edge 及熱門的協力廠商瀏覽器（例如 Chrome 和 Firefox 等）進行整合，Web 防護可在沒有 Web Proxy 的情況下阻擋網路威脅，並保護處於離開或內部部署狀態的機器。 Web 保護禁止以下來源進行存取：
  - 網路釣魚網站
  - 惡意程式碼媒介
  - 惡意探索網站
  - 不受信任或低信譽的網站
  - 您在自訂指示器清單中封鎖的網站。

  若要深入了解，請參閱 Microsoft Defender ATP 文件中的 [Web 防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) (機器翻譯)。

- **應用程式控制** - 應用程式控制設定透過限制使用者執行之應用程式及在系統核心 (核心) 中執行的程式碼，協助降低安全性威脅。 管理可封鎖未簽署指令碼和 MSI 的設定，並限制在限制語言模式中執行 Windows PowerShell。

  若要深入了解，請參閱 Microsoft Defender ATP 文件中的[應用程式控制](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)。

- **受攻擊面縮小規則** – 設定受攻擊面縮小規則的設定，此規則針對惡意程式碼和惡意應用程式常用來感染電腦的方式，包括：
  - 用於 Office 應用程式或網路郵件中，嘗試下載或執行檔案的可執行檔及指令碼
  - 模糊或可疑的指令碼
  - 應用程式在日常工作中不會出現的行為。縮少受攻擊面表示可以降低攻擊者執行攻擊的機會。

  若要深入了解，請參閱 Microsoft Defender ATP 文件中的[受攻擊面縮小規則](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) (機器翻譯)。

- **裝置控制** – 利用裝置控制的設定，您就可設定裝置使用多層次方法以保護抽取式媒體。 Microsoft Defender ATP 提供多項監視與控制功能，協助防止未經授權之周邊設備入侵您的裝置。

  若要深入了解，請參閱 Microsoft Defender ATP 文件中的 [如何使用 Microsoft Defender ATP 控制 USB 裝置和其他抽取式媒體](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) (機器翻譯)。

- **惡意探索保護** - 惡意探索保護設定有助於防範使用入侵程式感染裝置並散佈的惡意程式碼。 惡意探索保護包含一些可套用至作業系統或個別應用程式的緩和措施。

  若要深入了解，請參閱 Microsoft Defender ATP 文件中的[啟用惡意探索保護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) (機器翻譯)。

## <a name="next-steps"></a>後續步驟

[設定端點安全性原則](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
