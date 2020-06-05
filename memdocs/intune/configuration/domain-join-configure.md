---
title: Microsoft Intune 中 Windows 10 的網域加入設定檔設定 - Azure | Microsoft Docs
description: 建立混合式 Azure AD 加入裝置的網域加入裝置設定檔。 使用此設定檔，將內部部署 Active Directory 網域資訊部署至以 Windows Autopilot 和 Microsoft Intune 佈建的裝置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 211722a02183d3b86525468f907d4093331d9de6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988423"
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
2. 選取 [裝置] > [組態設定檔] > [建立設定檔]。
3. 輸入下列內容：

    - **平台**：選取 [Windows 10 及更新版本]。
    - **設定檔**：選取 [網域加入 (預覽)]。

4. 選取 [建立]。
5. 在 [基本資訊] 中，輸入下列內容：

    - **名稱**：輸入政策的描述性名稱。 為您的設定檔命名，以方便之後能夠輕鬆識別。 例如，一個良好的原則名稱是 **Windows 10：包含內部部署網域資訊的網域加入設定檔，以透過 Windows Autopilot 來註冊混合式 AD 加入裝置**。
    - **描述**：輸入政策的描述。 這是選擇性設定，但建議執行。

6. 選取 [下一步]。
7. 在 [組態設定] 中，輸入下列內容：

    - **電腦名稱前置詞**：輸入裝置名稱的前置詞。 電腦名稱稱長度為 15 個字元。 前置詞後方的剩餘 15 個字元會隨機產生。
    - **網域名稱**：輸入裝置要加入的完整網域名稱 (FQDN)。 例如，輸入 `americas.corp.contoso.com.`
    - **組織單位** (選擇性)：輸入要在其中建立電腦帳戶的組織單位 (OU) 完整路徑 ([辨別名稱](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name))。 例如，輸入 `"CN=Users,DC=Contoso,DC=com"`。 如果未輸入值，則會使用已知的電腦物件容器。

      如需此設定的詳細資訊和建議，請參閱[部署混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)。

8. 選取 [下一步]。

9. 在 [範圍標籤] (選擇性) 中，指派標籤來針對特定 IT 群組篩選設定檔，例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`。 如需範圍標籤的詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

    選取 [下一步]。

10. 在 [指派] 中，選取將接收您設定檔的使用者或使用者群組。 如需指派設定檔的詳細資訊，請參閱[指派使用者和裝置設定檔](device-profile-assign.md)。

    選取 [下一步]。

11. 在 [檢閱 + 建立] 中，檢閱您的設定。 當您選取 [建立] 時，系統會儲存您的變更，然後指派設定檔。 原則也會顯示在設定檔清單中。

您現在可以[使用 Intune 和 Windows Autopilot 部署混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)。

## <a name="next-steps"></a>後續步驟

[指派](device-profile-assign.md)設定檔之後，請[監視其狀態](device-profile-monitor.md)。

[使用 Intune 和 Windows Autopilot 部署混合式 Azure AD 加入裝置](../enrollment/windows-autopilot-hybrid.md)
