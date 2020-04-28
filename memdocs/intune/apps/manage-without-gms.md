---
title: 如何在沒有 Google 行動服務的環境中使用 Intune
titleSuffix: Microsoft Intune
description: 了解如何在沒有 Google 行動服務的環境中使用 Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5aa91a84b2fe5d8870afc93022ab5a468b30e0db
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074787"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>如何在沒有 Google 行動服務的環境中使用 Intune

Microsoft Intune 在管理 Android 裝置時，會使用 Google 行動服務 (GMS) 與 Microsoft Intune 公司入口網站進行通訊。 在某些情況下，裝置可能會暫時或永久無法存取 GMS。 例如，裝置出貨時可能就沒有 GMS，或者裝置可能連線到無法使用 GMS 的封閉式網路。 此文件摘要說明在安裝並使用 Intune 來管理沒有 GMS 的 Android 裝置時，可能會看到的差異與限制。

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>在無法存取 Google Play 商店的情況下安裝 Intune 公司入口網站應用程式。 

### <a name="for-users-outside-of-mainland-china"></a>適用於中國大陸以外的使用者 

如果 Google Play 無法使用，Android 裝置可以下載 [適用於 Android 的 Microsoft Intune 公司入口網站](https://www.microsoft.com/en-us/download/details.aspx?id=49140)，並側載應用程式。 以這種方式安裝時，應用程式不會自動接收更新或或修正程式。 您必須確定定期更新，並手動修補應用程式。 

### <a name="for-users-in-mainland-china"></a>適用於中國大陸的使用者 

由於中國大陸目前無法使用 Google Play 商店，因此 Android 裝置必須從中文應用程式市集取得應用程式。 如需詳細資訊，請參閱[在中國大陸安裝公司入口網站應用程式](../user-help/install-company-portal-android-china.md)。

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>當 GMS 無法使用時，Intune 裝置管理員管理的限制 

### <a name="unavailable-intune-features"></a>無法使用的 Intune 功能

有些 Intune 功能依賴 GMS 的元件，例如 Google Play 商店或 Google Play 服務。 因為這些元件無法在沒有 GMS 的環境中使用，所以 Intune 管理員主控台中的下列功能可能無法使用。  

| 案例  | 功能  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 裝置合規性原則  | 建立或編輯 Android 裝置管理員的合規性政策時，**Google Play 安全防護**下列出的所有選項都無法使用。  |
| 應用程式保護原則 (條件式啟動)  | **SafetyNet 裝置證明**與**需要對應用程式進行威脅掃描**裝置條件無法用於條件式啟動。  |
| 用戶端應用程式  | **Android** 類型的應用程式無法使用。 請改為使用**企業營運應用程式**來部署及管理應用程式。  |
| Mobile Threat Defense  | 請與您的 MTD 廠商合作，以了解其解決方案是否與 Intune 整合、在重點區域是否可用，以及是否依賴 GMS。  |

### <a name="some-tasks-may-be-delayed"></a>某些工作可能會延遲 

在可以使用 GMS 的環境中，Intune 依賴推播通知來加快工作的完成速度。 例如，如果您嘗試從遠端抹除裝置，則通知通常會在幾秒鐘內到達裝置。 在無法使用 GMS 的情況下，可能也無法使用推播通知。 因此，Intune 必須等候下一個裝置簽入時間才能完成工作。  

已註冊的 Android 裝置每 8 小時會向 Intune 回報一次。 例如，如果裝置在下午 1 點向 Intune 回報，而遠端工作在下午 1:05 發出，Intune 將在下午 9 點與裝置聯繫以完成工作。 

下列工作最多可能需要 8 小時才能完成： 

**Intune 主控台**：
- 完整抹除
- 選擇性抹除
- 新的或更新的應用程式部署
- 遠端鎖定
- 密碼重設

**適用於 Android 的 Intune 公司入口網站應用程式**：
- 遠端裝置移除
- 裝置重設
- 安裝可用的企業營運應用程式

**Intune 公司入口網站**：
- 裝置移除 (本機與遠端)
- 裝置重設
- 裝置密碼重設

如果裝置是最近註冊的，則合規性、非合規性與設定簽入的執行頻率比較高。 如需裝置簽入的詳細資訊，請參閱 [Microsoft Intune 中裝置原則與設定檔常見的問題、疑問與解決方法](../configuration/device-profile-troubleshoot.md)。 

## <a name="next-steps"></a>後續步驟

- [使用 Microsoft Intune 將應用程式指派給群組](../apps/apps-deploy.md)
