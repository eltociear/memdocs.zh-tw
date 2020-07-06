---
title: Android Enterprise 完全受控安全性設定
titleSuffix: Microsoft Intune
description: 了解適用於 Android Enterprise 完全受控基本、增強及高安全性的建議設定。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4c2a9aa48d17b9cb2b386a4e4cb4df8fb36caac
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502940"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Android Enterprise 完全受控安全性設定

作為 [Android Enterprise 安全性設定架構](android-configuration-framework.md)的一部分，請針對 Android Enterprise 完全受控行動裝置使用者套用下列設定。 如需每個原則設定的詳細資訊，請參閱[使用 Intune 來將裝置標記為符合規範或不符合規範的 Android Enterprise 裝置擁有者設定](../protect/compliance-policy-create-android-for-work.md#device-owner)和[使用 Intune 來允許或限制功能的 Android Enterprise 裝置設定](../configuration/device-restrictions-android-for-work.md#device-owner-only)。

選擇您的設定時，請務必檢閱並分類使用方式案例。 接著，請遵循所選安全性層級的指導方針來設定使用者。 您可以根據組織的需求調整建議的設定。 請務必讓您的安全性小組評估威脅環境、風險偏好，以及對可用性的影響。

針對公司擁有的完全受控裝置，有三個建議的安全性設定架構：

- [完全受控基本安全性 (層級 1)](#fully-managed-basic-security) 
- [完全受控增強式安全性 (層級 2)](#fully-managed-enhanced-security)
- [完全受控高安全性 (層級 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>完全受控基本安全性

層級 1 是針對由組織擁有的行動裝置所建議的最低安全性設定。

層級 1 中的原則會在將對使用者的影響降至最低的情況下，強制執行合理的資料存取層級。 這是透過強制執行密碼原則、最低作業系統版本、SafetyNet 裝置證明，以及停用部分裝置功能 (例如 USB 檔案傳輸) 來達成。 

### <a name="device-compliance"></a>裝置相容性

| 區段 | 設定 | 值 | 備忘錄 |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | 裝置須等於或低於電腦風險分數 | 尚未設定 ||
| 裝置健全狀況 | 裝置須等於或低於裝置威脅等級 | 尚未設定||
| 裝置健全狀況 | SafetyNet 裝置證明 | 檢查基本完整性和經認證的裝置 | 此設定會在使用者裝置上設定 Google 的 SafetyNet 證明。 [基本完整性] 會驗證裝置的完整性。 Root 破解的裝置、模擬器、虛擬裝置，以及具有竄改跡象的裝置都無法通過基本完整性檢查。<br>[基本完整性和經認證的裝置] 會驗證裝置與 Google 服務的相容性。 只有經過 Google 認證且未修改的裝置可以通過這項檢查。 |
| 裝置內容 | 最低 OS 版本 | 格式：Major.Minor<br>範例：8.0| Microsoft 建議將最低 Android 主要版本設定為符合 Microsoft 應用程式所支援的 Android 版本。 遵守 Android Enterprise 建議需求的 OEM 和裝置必須支援目前發行版本 + 一個字母升級。 目前，Android 建議知識工作者使用 Android 8.0 和更新版本。 如需 Android 的最新建議，請參閱 [Android Enterprise Recommended 規格需求](https://www.android.com/enterprise/recommended/requirements/)。 |
| 裝置內容 | 最高 OS 版本 | 尚未設定 ||
| 裝置內容 | 安全性修補程式等級下限 | 尚未設定 | Android 裝置可能會收到每月安全性修補程式，但版本會取決於 OEM 和/或電訊廠商。 組織應該確保所部署的 Android 裝置確實收到安全性更新，再實作此設定。 如需最新的修補程式版本，請參閱 [Android 安全性公告](https://source.android.com/security/bulletin/)。 |
| 系統安全性 | 需要密碼來解除鎖定行動裝置 | 要求 ||
| 系統安全性 | 所需的密碼類型 | 複雜數字 | 組織可能需要更新此設定以符合其密碼原則。 |
| 系統安全性 | 密碼長度下限 | 6 | 組織可能需要更新此設定以符合其密碼原則。 |
| 系統安全性 | 在停止活動最少幾分鐘後必須輸入密碼| 5 | 組織可能需要更新此設定以符合其密碼原則。|
| 系統安全性 | 密碼過期前的天數| 尚未設定 ||
| 系統安全性 |    使用者在重複使用某組密碼前，必須使用的密碼組數 | 尚未設定 ||
| 系統安全性 | 加密裝置上儲存的資料 | 要求 ||
| 處理不相容狀況的動作 | 將裝置標示為不符合規範 | 立即 | 根據預設，原則會設定為將裝置標示為不符合規範。 有其他動作可供使用。 如需詳細資訊，請參閱[在 Intune 中為不符合規範的裝置設定動作](../protect/actions-for-noncompliance.md)。|

### <a name="device-restrictions"></a>裝置限制

| 區段 | 設定 | 值 | 備忘錄 |
| ----- | ----- | ----- | ----- |
| 一般 | 螢幕擷取 | 尚未設定 ||
| 一般 | 相機 | 尚未設定 ||
| 一般 | 預設權限原則 | 裝置預設 ||
| 一般 | 日期與時間變更 | 尚未設定 ||
| 一般 | 音量變更 | 尚未設定 ||
| 一般 | 原廠重設 | 封鎖 ||
| 一般 | 安全開機 | 封鎖 ||
| 一般 | 狀態列 | 尚未設定 ||
| 一般 | 漫遊資料服務 | 尚未設定 ||
| 一般 | Wi-Fi 設定變更 | 尚未設定 ||
| 一般 | 藍牙設定 | 尚未設定 ||
| 一般 | 網際網路共用和存取熱點 | 尚未設定 ||
| 一般 | USB 儲存裝置 | 尚未設定 ||
| 一般 | USB 檔案傳輸 | 封鎖 ||
| 一般 | 外部媒體 | 封鎖 ||
| 一般 | 使用 NFC 發送資料 | 尚未設定 ||
| 一般 | 偵錯功能 | 尚未設定 ||
| 一般 | 麥克風調整 | 尚未設定 ||
| 一般 | 恢復出廠預設值保護電子郵件 | 尚未設定 ||
| 一般 | 網路備案 | 尚未設定 ||
| 一般 | 系統更新 | 自動 ||
| 一般 | 通知視窗 | 尚未設定 ||
| 一般 | 略過初次使用提示 | 尚未設定 ||
| 系統安全性 | 對應用程式進行威脅掃描 |要求 ||
| 裝置體驗 | 註冊設定檔類型 | 完全受控 ||
| 裝置體驗 | 將 Microsoft Launcher 設定為預設啟動程式 | 尚未設定 | 組織可以選擇實作 Microsoft Launcher 以在完全受控裝置上確保一致的主畫面體驗。 如需詳細資訊，請參閱[如何使用 Intune 在 Android Enterprise 完全受控裝置上設定 Microsoft Launcher](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134) \(英文\) |
| 密碼 | 停用鎖定畫面 | 尚未設定 ||
| 密碼 | 已停用鎖定畫面功能 | 0 (已選取) ||
| 密碼 | 所需的密碼類型 | 複雜數字 ||
| 密碼 | 密碼長度下限 | 6 ||
| 密碼 | 密碼過期前的天數 | 尚未設定 ||
| 密碼 | 使用者在重複使用某組密碼前，必須使用的密碼組數 | 尚未設定 ||
| 密碼 | 登入失敗幾次後即抹除裝置 | 10 ||
| 電源設定 | 畫面鎖定時間 | 5 ||
| 電源設定 | 畫面在裝置充電時開啟 | 尚未設定 ||
| 使用者及帳戶 | 新增使用者 | 尚未設定 ||
| 使用者及帳戶 | 使用者移除 | 尚未設定 ||
| 使用者及帳戶 | 帳戶變更 (僅限專用裝置) | 尚未設定 ||
| 使用者及帳戶 | 個人 Google 帳戶 | 尚未設定 ||
| 使用者及帳戶 | 使用者可以設定認證 | 封鎖 ||
| 應用程式 | 允許從不明來源安裝 | 尚未設定 ||
| 應用程式 | 允許存取 Google Play 商店中的所有應用程式 | 尚未設定 | 根據預設，使用者無法在完全受控裝置上從 Google Play 商店安裝個人應用程式。 如果組織想要允許將完全受控裝置用於個人用途，請考慮變更此設定。 |
| 應用程式 | 應用程式自動更新 | 僅限 Wi-Fi | 組織應視需要調整此設定，因為如果應用程式更新是透過行動電話通訊網路發生，則可能會產生行動數據方案費用。 |

## <a name="fully-managed-enhanced-security"></a>完全受控增強式安全性

層級 2 是針對使用者會存取更敏感資訊的公司擁有裝置所建議的設定。 這些裝置理所當然會成為現今企業中的攻擊目標。 這些設定會假設公司並沒有大量具備高度技術的安全性人員。 因此，其應該最適合大部分的企業組織使用。 此設定會擴充層級 1 的設定，並制定更強的密碼原則並停用使用者/帳戶功能。

層級 2 設定包含針對層級 1 所建議的所有原則設定。 不過，下列設定僅包含新增或變更的設定。 這些設定對使用者或應用程式可能會有稍微更多的影響。 其會強制執行更適合能在行動裝置上存取敏感性資訊，且須面對風險之使用者的安全性層級。

### <a name="device-compliance"></a>裝置相容性

| 區段 | 設定 | 值 | 備忘錄 |
| ----- | ----- | ----- | ----- |
| 系統安全性 | 密碼過期前的天數 | 365 | 組織可能需要更新此設定以符合其密碼原則。 |
| 系統安全性 |    使用者在重複使用某組密碼前，必須使用的密碼組數 | 5 | 組織可能需要更新此設定以符合其密碼原則。 |

### <a name="device-restrictions"></a>裝置限制

| 區段 | 設定 | 值 | 備忘錄 |
| ----- | ----- | ----- | ----- |
| 一般 | 恢復出廠預設值保護電子郵件 | Google 帳戶電子郵件地址 ||
| 一般 | 電子郵件地址清單 (僅限 Google 帳戶電子郵件地址選項) | example@gmail.com | 手動更新此原則來指定可在抹除裝置後將裝置解除鎖定之裝置系統管理員的 Google 電子郵件地址。 |
| 裝置密碼 | 密碼過期前的天數 | 365 | 組織可能需要更新此設定以符合其密碼原則。 |
| 裝置密碼 | 使用者在重複使用某組密碼前，必須使用的密碼組數 | 5 | 組織可能需要更新此設定以符合其密碼原則。 |
| 裝置密碼 | 登入失敗幾次後即抹除裝置 | 5 ||
| 使用者及帳戶 | 新增使用者 | 封鎖 ||
| 使用者及帳戶 | 使用者移除 | 封鎖 ||
| 使用者及帳戶 | 個人 Google 帳戶 | 封鎖 ||

## <a name="fully-managed-high-security"></a>完全受控高安全性

層級 3 是針對下列兩者所建議的設定：
- 具有大型且複雜安全性組織的組織。
- 攻擊者會特別鎖定的特定使用者和群組。
此類組織通常會成為資金充裕且經驗老道之攻擊者的目標。 因此，便應該採取下列額外的條件約束和控制。

此設定會以下列方式擴充層級 2：
- 提高最低作業系統版本。
- 透過強制執行最安全的 Microsoft Defender ATP 或行動裝置威脅防護層級，來確保裝置是符合規範的。
- 提高最低作業系統版本。
- 強制執行額外的裝置限制 (例如在鎖定畫面上停用未編校的通知)。
- 要求應用程式一律處於最新狀態。 

在層級 3 中強制執行的原則設定，會包含針對層級 2 所建議的所有原則設定。 下列設定僅包含新增或變更的設定。 這些設定可能會對使用者或應用程式造成顯著的影響。 其會強制執行更適合會成為攻擊者的目標，且須面對風險之組織的安全性層級。


### <a name="device-compliance"></a>裝置相容性

| 區段 | 設定 | 值 | 備忘錄 |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | 裝置須等於或低於電腦風險分數 | 清除 | 此設定需要 Microsoft Defender ATP。 如需詳細資訊，請參閱[在 Intune 中使用條件式存取強制執行 Microsoft Defender ATP 的合規性](../protect/advanced-threat-protection.md)。<p> 客戶應該考慮實作 Microsoft Defender ATP 或行動裝置威脅防護解決方案。 並不需要同時部署兩者。 |
| 裝置健全狀況 | 裝置須等於或低於裝置威脅等級 | 受保護 | 此設定需要行動裝置威脅防護產品。 如需詳細資訊，請參閱[已註冊裝置的行動裝置威脅防護](../protect/mtd-device-compliance-policy-create.md)。<p>客戶應該考慮實作 Microsoft Defender ATP 或行動裝置威脅防護解決方案。 並不需要同時部署兩者。|
| 裝置內容 | 最低 OS 版本 | 格式：Major.Minor<br>範例：10.0| Microsoft 建議將最低 Android 主要版本設定為符合 Microsoft 應用程式所支援的 Android 版本。 遵守 Android Enterprise 建議需求的 OEM 和裝置必須支援目前發行版本 + 一個字母升級。 目前，Android 建議知識工作者使用 Android 8.0 和更新版本。 如需 Android 的最新建議，請參閱《Android Enterprise Recommended 規格需求》 |

### <a name="device-restrictions"></a>裝置限制

| 區段 | 設定 | 值 | 備忘錄 |
| ----- | ----- | ----- | ----- |
| 一般 | 日期與時間變更 | 封鎖 ||
| 一般 | 網際網路共用和存取熱點 | 封鎖 ||
| 一般 | 使用 NFC 發送資料 | 封鎖 ||
| 裝置密碼 | 已停用鎖定畫面功能 | 信任代理程式、未編校的通知 ||
| 應用程式 | 應用程式自動更新 | 永遠 | 組織應視需要調整此設定，因為如果應用程式更新是透過行動電話通訊網路發生，則可能會產生行動數據方案費用。 |


## <a name="next-steps"></a>後續步驟

系統管理員可以藉由匯入範例 [Android Enterprise 安全性設定架構 JSON 範本](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) \(英文\) 和 [Intune 的 PowerShell 指令碼](https://github.com/microsoftgraph/powershell-intune-samples) \(英文\)，在其部署更新步調方法中納入上述設定層級，以供測試和生產使用。
