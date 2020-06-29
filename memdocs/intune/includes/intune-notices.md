---
title: 包含檔案
description: 包含檔案
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 22dc48a60d03a0cc6bc10e04bc3facbf36983ff9
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84637571"
---
這些注意事項提供可協助您針對未來的 Intune 變更與功能進行準備的重要資訊。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>適用於 Windows 10 行動裝置版的 Microsoft Intune 支援結束<!--3544938-->
Microsoft 針對 Windows 10 行動裝置版的主要支援已於 2019 年 12 月結束。 如此支援聲明中所述，Windows 10 行動裝置版使用者將不再具備接收來自 Microsoft 的新安全性更新、非安全性 Hotfix、免費協助支援選項，或線上技術內容更新的資格。 基於已結束的行動裝置版 OS 支援，Microsoft Intune 從 2020 年 8 月 10 日起將終止支援適用於 Windows 10 行動裝置版的公司入口網站應用程式，以及 Windows 10 行動裝置版作業系統。

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？
如果已在組織中部署 Windows 10 行動裝置版裝置，從現在到 2020 年 8 月 10 日為止，您可註冊新裝置、新增或移除原則與應用程式，或更新任何管理設定。 在 8 月 10 日之後，我們將會停止新的註冊，而且最終會從 Intune UI 移除 Windows 10 行動裝置版管理。 裝置將無法再簽入 Intune 服務，而且我們將會刪除裝置與原則資料。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？
您可以檢查您的 Intune 報告，查看哪些裝置或使用者可能會受到影響。 移至 [裝置] > [所有裝置]，然後依作業系統篩選。 您可以新增其他欄，協助識別您組織中誰擁有執行 Windows 10 行動裝置版的裝置。 請要求您的終端使用者升級其裝置，或停止將該裝置用於公司存取。


### <a name="end-of-support-for-legacy-pc-management"></a>結束對舊版電腦管理的支援

自 2020 年 10 月 15 日起結束對舊版電腦管理的支援。 請將裝置升級至 Windows 10，並重新註冊為行動裝置管理 (MDM) 裝置，以繼續交由 Intune 管理。

[深入了解](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>請移至 Microsoft Endpoint Manager 系統管理中心處理所有的 Intune 管理
三月張貼的 MC208118 中，我們為您的 Microsoft Endpoint Manager – Intune 管理引入了一個新的簡易 URL：[https://endpoint.microsoft.com](https://endpoint.microsoft.com)。 Microsoft Endpoint Manager 是包含 Microsoft Intune 與 Configuration Manager 的整合平台。 **自 2020 年 8 月 1 日起**，我們將移除位在 [https://portal.azure.com](https://portal.azure.com) 的 Intune 管理，建議您改用 [https://endpoint.microsoft.com](https://endpoint.microsoft.com) 處理所有端點管理。 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>減少 Android 裝置系統管理員的支援<!--7371518-->
在 Android 2.2 中發行的 Android 裝置系統管理員管理是管理 Android 裝置的一種方式。 從 Android 5 開始，已發行更現代化的 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理架構 (適用於可確實連線到 Google 行動服務的裝置)。 Google 透過減少對新 Android 版本的管理支援，鼓勵移出裝置系統管理員管理。

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？
因為 Google 的這些變更，在 2020 年的第四季，您在受影響的受裝置系統管理員管理的裝置上，將不再具有廣泛的管理功能。 

> [!NOTE]
> 此日期原訂為 2020 年第三季，但已依據 [Google 最新資訊](https://www.blog.google/products/android-enterprise/da-migration/)異動。

##### <a name="device-types-that-will-be-impacted"></a>受影響的裝置類型
適用於下列三項條件的裝置，就是會受減少裝置系統管理員支援所影響的裝置：
- 在裝置系統管理員管理中註冊。
- 執行 Android 10 或更新版本。
- 非 Samsung 裝置。

下列任一項裝置則不會受到影響：
- 未使用裝置系統管理員管理註冊。
- 執行 Android 10 以下的 Android 版本。
- Samsung 裝置。 在此期間內，Samsung Knox 裝置不會受到影響，因為其透過 Intune 與 Knox 平台的整合來獲得延伸支援。 這讓您有更多時間，為 Samsung 裝置規劃轉移出裝置系統管理員管理。

##### <a name="settings-that-will-be-impacted"></a>受影響的設定
[Google 減少的裝置系統管理員支援](https://developers.google.com/android/work/device-admin-deprecation)會阻止在受影響的裝置上套用這些組態設定。

###### <a name="configuration-profile-device-restriction-settings"></a>組態設定檔裝置限制設定

- 封鎖 [相機]
- 設定 [密碼長度下限]
- 設定 [登入失敗幾次後即抹除裝置] (不會套用在未設定密碼的裝置上，但會套用在具有密碼的裝置上)
- 設定 [密碼到期 (天數)]
- 設定 [所需的密碼類型]
- 設定 [Prevent use of previous passwords] \(防止使用舊密碼\)
- 封鎖 [Smart Lock 與其他信任代理程式]

###### <a name="compliance-policy-settings"></a>相容性原則設定

- 設定 [所需的密碼類型]
- 設定 [密碼長度下限]
- 設定 [密碼過期前的天數]
- 設定 [防止重複使用的舊密碼數目]

###### <a name="additional-impacts-based-on-android-os-version"></a>Android OS 版本的其他影響

**Android 10**：凡是執行 Android 10 與更新版本之受裝置系統管理員管理的裝置 (包括 Samsung)，Google 均已限制公司入口網站等裝置系統管理員管理代理程式，存取裝置識別碼資訊的能力。 當裝置更新為 Android 10 或更新版本之後，此限制會影響下列 Intune 功能：
- VPN 的網路存取控制將不再有效
- 透過 IMEI 或序號識別為公司擁有的裝置，將不會自動將裝置標示為公司擁有
- 在 Intune 中，IT 系統管理員再也看不到 IMEI 與序號

**Android 11**：我們目前正在測試 Android 11 對最新開發人員搶鮮版 (Beta) 的支援，以評估其會否對受裝置系統管理員管理的裝置造成影響。

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>受影響裝置之受影響設定的使用者體驗

受影響的組態設定：
- 針對已套用設定的已註冊裝置，將繼續施行受影響的組態設定。
- 針對新註冊的裝置、新指派的設定與更新的設定，將不會施行受影響的組態設定 (但仍會施行所有的其他組態設定)。

受影響的合規性設定：
- 對於已套用設定的已註冊裝置，受影響的合規性設定將仍會因不符合規範而顯示在 [更新裝置設定] 頁面上，裝置列為不符合規範，然後仍然會在設定應用程式中施行密碼需求。
- 對於新註冊的裝置、新指派的設定與更新的設定，受影響的合規性設定將仍因不符合規範而顯示在 [更新裝置設定] 頁面上，且裝置列為不符合規範，但不會在設定應用程式中施行較嚴格的密碼需求。

#### <a name="cause-of-impact"></a>影響的原因 
裝置會在 2020 年的第四季開始受到影響。 屆時，將會有公司入口網站應用程式更新，將公司入口網站 API 目標從層級 28 增加到層級 29 ([依 Google 要求](https://www.blog.google/products/android-enterprise/da-migration/))。 

屆時，一旦使用者完成下列這兩個動作，非 Samsung 製造的受裝置系統管理員管理的裝置將受到影響：
- 更新至 Android 10 或更新版本。
- 將公司入口網站應用程式更新為以 API 層級 29 為目標的版本。

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？
為避免 2020 年第四季出現的功能減少，建議您執行下列動作：
- **新的註冊**：將新裝置上線到 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理 (如果有的話)，以及 (或) [應用程式防護原則](../apps/app-protection-policies.md)。 避免將新裝置上線到裝置系統管理員管理。 
- **先前已註冊的裝置**：若受裝置系統管理員管理的裝置執行 Android 10 或更新版本，或可能更新為 Android 10 或更新版本 (特別是當此裝置不是 Samsung 裝置)，請將其從裝置系統管理員管理，移至 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) 管理及/或 [應用程式防護原則](../apps/app-protection-policies.md)。 您可以運用簡化的流程，[將 Android 裝置從裝置系統管理員移至工作設定檔管理](../enrollment/android-move-device-admin-work-profile.md)。

#### <a name="additional-information"></a>其他資訊
- [將 Android 裝置從裝置系統管理員移至工作設定檔管理](../enrollment/android-move-device-admin-work-profile.md)
- [設定 Android Enterprise 工作設定檔裝置的註冊](../enrollment/android-work-profile-enroll.md)
- [設定 Android Enterprise 專用裝置的註冊](../enrollment/android-kiosk-enroll.md)
- [設定 Android Enterprise 完全受控裝置的註冊](../enrollment/android-fully-managed-enroll.md)
- [如何建立及指派應用程式防護原則](../apps/app-protection-policies.md)
- [如何在沒有 Google 行動服務的環境中使用 Intune](../apps/manage-without-gms.md)
- [了解 Android Enterprise 裝置上的應用程式防護原則與工作設定檔](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Google’s blog about what you need to know about Device Admin deprecation](https://www.blog.google/products/android-enterprise/da-migration/) (Google 部落格：取代裝置系統管理員須知)
- [Google's guidance for migration from device administrator to Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf) (Google 指南：從裝置系統管理員移轉到 Android Enterprise)
- [Google 文件：裝置系統管理員 API 的取代計劃](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>規劃變更：適用於 iOS/iPadOS 之 Apple 自動裝置註冊的 Intune 註冊流程更新
在公司入口網站 7 月的版本中，我們將變更 Apple 自動裝置註冊 (前稱為 DEP)的 iOS/iPadOS 註冊流程。 只有在「使用使用者親和性註冊」流程期間，才能變更註冊流程。 過去，如在在設定中將 [安裝公司入口網站] 設為 [否]，使用者仍然可以從商店安裝公司入口網站應用程式，然後觸發註冊，讓使用者新增適當的序號。 即將推出的公司入口網站版本將移除此序號確認畫面。 但建議您建立對應的應用程式設定原則，以與公司入口網站並存向下傳送，以確保使用者可以成功註冊，或在設定中將 [安裝公司入口網站] 設為 [是]。 
 - 如需詳細資訊，請參閱[這裡](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629)的文章。
