---
title: 在 Microsoft Intune - Azure 中建立裝置設定檔 | Microsoft Docs
description: 在 Microsoft Intune 中新增或設定裝置組態設定檔。 選取平台類型、進行設定、新增範圍標籤。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c2031ba23b49bda4890d2638272e3b808b4bf5a9
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327443"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>在 Microsoft Intune 中建立裝置設定檔

裝置設定檔可讓您新增設定項目並加以設定，然後再將這些設定推送至您組織中的裝置。 [使用裝置設定檔在裝置上套用功能和設定](device-profiles.md)則能提供更詳細的資料，包括您可以執行哪些作業。

這篇文章：

- 會列出建立設定檔的步驟。
- 會說明如何新增範圍標籤以「篩選」設定檔。
- 描述 Windows 10 裝置上的適用性規則，並示範如何建立規則。
- 會在裝置接收設定檔和任何設定檔更新時，列出簽入重新整理週期時間。

## <a name="create-the-profile"></a>建立設定檔

設定檔是在 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內建立。 在此系統管理中心內，選取 [裝置]  。 下列選項可供您選擇：

- **概觀**：列出您的設定檔狀態，並在您指派給使用者和裝置的設定檔中提供其他詳細資料。
- **監視**：檢查設定檔的狀態為成功或失敗，另檢視設定檔中的記錄。
- **依平台**：依平台建立及檢視原則和設定檔。 此檢視也會顯示平台特定的功能。 例如，選取 [Windows]  。 您會看到 Windows 特定的功能，例如 **Windows 10 更新通道**和 **PowerShell 指令碼**。
- **原則**：建立裝置設定檔，上傳要在設定檔中執行的自訂 [PowerShell 指令碼](../apps/intune-management-extension.md)，並使用 [eSIM](esim-device-configuration.md) 將行動數據方案新增至裝置。

當建立設定檔 ([組態設定檔]   > [建立設定檔]  ) 時，請選擇平台：

- **Android 裝置系統管理員**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 及以上版本**
- **Windows 8.1 及更新版本**
- **Windows Phone 8.1**

然後，選擇設定檔類型。 您可設定的設定會視您選擇的平台而不同。 下列文章會描述不同設定檔類型的設定︰

- [系統管理範本 (Windows)](administrative-templates-windows.md)
- [自訂](custom-settings-configure.md)
- [傳遞最佳化 (Windows)](delivery-optimization-windows.md)
- [衍生認證 (Android Enterprise、iOS、iPadOS)](../protect/derived-credentials.md)
- [裝置功能 (macOS、iOS、iPadOS)](device-features-configure.md)
- [裝置韌體 (Windows)](device-firmware-configuration-interface-windows.md)
- [裝置限制](device-restrictions-configure.md)
- [網域加入 (Windows)](domain-join-configure.md)
- [版本升級及模式切換 (Windows)](edition-upgrade-configure-windows-10.md)
- [教育 (iOS、iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [電子郵件](email-settings-configure.md)
- [端點保護 (macOS、Windows)](../protect/endpoint-protection-configure.md)
- [延伸模組 (macOS)](kernel-extensions-overview-macos.md)
- [Identity Protection (Windows)](../protect/identity-protection-configure.md)
- [Kiosk](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [行動延伸模組 (MX) 設定檔 (Android 裝置系統管理員)](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [PKCS 憑證](../protect/certficates-pfx-configure.md)
- [PKCS 匯入憑證](../protect/certificates-imported-pfx-configure.md)
- [喜好設定檔案 (macOS)](preference-file-settings-macos.md)
- [SCEP 憑證](../protect/certificates-scep-configure.md)
- [安全性評定 (教育) (Windows)](education-settings-configure.md)
- [共用的多重使用者裝置 (Windows)](shared-user-device-settings.md)
- [電信費用 (Android 裝置系統管理員、iOS、iPadOS)](telecom-expenses-monitor.md)
- [信任的憑證](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)

例如，如果針對平台選取 [iOS/iPadOS]  ，您的設定檔類型選項會看起來類似下列設定檔：

> [!div class="mx-imgBorder"]
> ![在 Intune 中建立 iOS/iPadOS 設定檔](./media/device-profile-create/create-device-profile.png)

## <a name="scope-tags"></a>範圍標籤

新增設定之後，您也可以新增範圍標籤至設定檔。 範圍標籤會將設定檔篩選到特定 IT 群組 (例如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`)。 以及用於分散式 IT。

如需範圍標籤和可執行哪些作業的相關詳細資訊，請參閱[針對分散式 IT 使用 RBAC 和範圍標籤](../fundamentals/scope-tags.md)。

## <a name="applicability-rules"></a>適用性規則

適用於：

- Windows 10 及更新版本

適用性規則可讓系統管理員以符合特定準則之群組中的裝置為目標。 例如，您可以建立要套用至 [所有 Windows 10 裝置]  群組的裝置限制設定檔。 而且，您只想將設定檔指派給執行 Windows 10 企業版的裝置。

若要執行此工作，請建立**適用性規則**。 這些規則非常適合下列案例：

- 您使用 Windows 10 教育版 (EDU)。 在 Bellows College，您想要以 RS3 與 RS4 之間的所有 Windows 10 EDU 裝置為目標。
- 您想要以 Contoso 人力資源部門中的所有使用者為目標，但只想要 Windows 10 專業版或企業版裝置。

若要解決這些案例，您可以：

- 建立裝置群組以包含 Bellows College 的所有裝置。 在設定檔中，新增適用性規則，以便在 OS 最低版本為 `16299` 且最高版本為 `17134` 時套用。 將此設定檔指派給 Bellows College 裝置群組。

  指派之後，設定檔即會套用至介於您所輸入之最低和最高版本間的裝置。 如果裝置不在您輸入的最低和最高版本之間，則其狀態會顯示為 [不適用]  。

- 建立使用者群組以包含 Contoso 人力資源部門 (HR) 中的所有使用者。 在設定檔中，新增適用性規則，以套用至執行 Windows 10 專業版或企業版的裝置。 將此設定檔指派給 HR 使用者群組。

  指派之後，設定檔即會套用至執行 Windows 10 專業版或企業版的裝置。 針對不是執行這些版本的裝置，其狀態會顯示為 [不適用]  。

- 如果有兩個設定檔具有完全相同的設定，則會套用不含適用性規則的設定檔。 

  例如，ProfileA 以 Windows 10 裝置群組為目標、啟用 BitLocker，且沒有適用性規則。 ProfileB 以相同的 Windows 10 裝置群組為目標、啟用 BitLocker，而且具有只將設定檔套用至 Windows 10 企業版的適用性規則。

  指派這兩個設定檔時會套用 ProfileA，因為它沒有適用性規則。 

當您將設定檔指派給群組時，會使用適用性規則作為篩選條件，而且只會以符合您準則的裝置為目標。

### <a name="add-a-rule"></a>新增規則

1. 選取 [適用性規則]  。 您可以選擇 [規則]  、[屬性]  和 [OS 版本]  ：

    > [!div class="mx-imgBorder"]
    > ![在 Microsoft Intune 中新增裝置組態設定檔的適用性規則](./media/device-profile-create/applicability-rules.png)

2. 在 [規則]  中，選擇您是否要包含或排除使用者或群組。 選項包括：

    - **指派設定檔的條件**：包含符合您所輸入準則的使用者或群組。
    - **不指派設定檔的條件**：排除符合您所輸入準則的使用者或群組。

3. 在 [屬性]  中，選擇您的篩選條件。 選項包括： 

    - **OS 版本**：在清單中，檢查您要在規則中包含 (或排除) 的 Windows 10 版本。
    - **OS 版本**：輸入您想要在規則中包含 (或排除) 的**最低**和**最高** Windows 10 版本號碼。 這兩者均為必要值。

      例如，您可以針對最低版本輸入 `10.0.16299.0` (RS3 或 1709)，並針對最高版本輸入 `10.0.17134.0` (RS4 或 1803)。 或者，您可以更精細地針對最低版本輸入 `10.0.16299.001`，並針對最高版本輸入 `10.0.17134.319`。

4. 選取 [新增]  以儲存您的變更。

## <a name="refresh-cycle-times"></a>重新整理週期時間

Intune 會使用各種重新整理循環來檢查組態設定檔是否有更新。 如果裝置是最近註冊的，則簽入的執行頻率會更加頻繁。 [原則和設定檔重新整理循環](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)列出預估的重新整理時間。

使用者可以在任何時間開啟公司入口網站應用程式並同步處理裝置，以立即檢查是否有設定檔更新。

## <a name="recommendations"></a>建議

建立設定檔時，請考量下列建議：

- 為您的原則命名，讓您知道它們是什麼，以及它們會做什麼。 所有[合規性政策](../protect/create-compliance-policy.md)和[組態設定檔](../configuration/device-profile-create.md)，都有一個選擇性的 [描述]  屬性。 在 [描述]  中，明確描述並包含資訊，使其他人可以知道原則的用途。

  一些組態設定檔範例包括：

  **設定檔名稱**：系統管理範本 - 適用於所有 Windows 10 使用者的 OneDrive 組態設定檔  
  **設定檔描述**：OneDrive 系統管理範本設定檔，包含適用於所有 Windows 10 使用者的最低與基礎設定。 由 user@contoso.com 建立，以防止使用者將組織資料共用至個人 OneDrive 帳戶。

  **設定檔名稱**：適用於所有 iOS/iPadOS 使用者的 VPN 設定檔  
  **設定檔描述**：VPN 設定檔，包含讓所有 iOS/iPadOS 使用者連線到 Contoso VPN 的最低與基礎設定。 由 user@contoso.com 建立，讓使用者自動向 VPN 驗證，而不是提示使用者輸入其使用者名稱和密碼。

- 藉由其工作來建立您的設定檔，例如，設定 Microsoft Edge 設定、啟用 Microsoft Defender 防毒程式設定、封鎖 iOS/iPadOS 越獄裝置等。

- 建立適用於特定群組的設定檔，例如，行銷、銷售、IT 系統管理員，或依地點或學校系統。

- 將使用者原則與裝置原則分開。

  例如，[Intune 中的系統管理範本](administrative-templates-windows.md)有數百個 ADMX 設定。 這些範本會顯示設定是否適用於使用者或裝置。 建立系統管理範本時，將您的使用者設定指派給使用者群組，並將您的裝置設定指派給裝置群組。

  下列影像顯示可套用至使用者及/或套用至裝置的設定範例：

  > [!div class="mx-imgBorder"]
  > ![適用於使用者與裝置的 Intune 系統管理範本](./media/device-profile-create/setting-applies-to-user-and-device.png)

- 當您每次建立受限的原則時，請將此變更傳達給使用者。 例如，如果要將密碼需求從 4 個字元變更為 6 個字元，請在指派原則之前，讓您的使用者知道。

## <a name="next-steps"></a>後續步驟

[指派設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。
