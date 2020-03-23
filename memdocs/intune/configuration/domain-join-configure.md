---
title: Microsoft Intune 中 Windows 10 的網域加入設定檔設定 - Azure | Microsoft Docs
description: 建立混合式 Azure AD 加入裝置的網域加入裝置設定檔。 使用此設定檔，將內部部署 Active Directory 網域資訊部署至以 Windows Autopilot 和 Microsoft Intune 佈建的裝置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364392"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Microsoft Intune 中混合式 Azure AD 加入裝置的設定網域加入設定

許多環境都使用內部部署 Active Directory (AD)。 當 AD 網域加入裝置也加入了 Azure AD 時，即稱為混合式 Azure AD 加入裝置。 利用 Windows Autopilot，您可以在 Intune 中[註冊混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)。 您同時也需要**網域加入**組態設定檔才能註冊。

**網域加入**組態設定檔包含內部部署 Active Directory 網域資訊。 佈建裝置 (通常為離線) 時，此設定檔會部署 AD 網域詳細資料，讓裝置知道要加入哪個內部部署網域。 如果未建立網域加入設定檔，則可能會無法部署這些裝置。

本功能適用於：

- Windows 10 和更新版本
- 混合式 Azure AD 加入裝置
- 使用 Autopilot + Intune 進行混合式部署

本文說明如何為混合式 Autopilot 部署建立網域加入設定檔。 您也可以查看可用的設定。

## <a name="create-the-profile"></a>建立設定檔

1. 登入 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置]   > [組態設定檔]   > [建立設定檔]  。
3. 輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，一個良好的原則名稱是 **Windows 10：包含內部部署網域資訊的網域加入設定檔，以透過 Windows Autopilot 來註冊混合式 AD 加入裝置**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。
    - **平台**：選取 [Windows 10 及更新版本]  。
    - **設定檔類型**：選取 [網域加入 (預覽)]  。

4. 選取 [設定]  。 輸入下列內容：

    - **電腦名稱前置詞**：輸入裝置名稱的前置詞。 電腦名稱稱長度為 15 個字元。 前置詞後方的剩餘 15 個字元會隨機產生。
    - **網域名稱**：輸入裝置要加入的完整網域名稱 (FQDN)。 例如，輸入 `americas.corp.contoso.com.`
    - **組織單位** (選擇性)：輸入要在其中建立電腦帳戶的組織單位 (OU) 完整路徑 ([辨別名稱](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name))。 例如，輸入 `"CN=Users,DC=Contoso,DC=com"`。 如果未輸入值，則會使用已知的電腦物件容器。

      如需此設定的詳細資訊和建議，請參閱[部署混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)。

5. 當您完成時，請選取 [確定]   > [建立]  儲存變更。

設定檔隨即建立，並顯示在設定檔清單上。 您現在可以[使用 Intune 和 Windows Autopilot 部署混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)。

## <a name="next-steps"></a>後續步驟

建立設定檔之後即可加以指派。 接下來，[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

[使用 Intune 和 Windows Autopilot 部署混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)
