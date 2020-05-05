---
title: 包含檔案
description: 包含檔案
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183038"
---
這些注意事項提供可協助您針對未來的 Intune 變更與功能進行準備的重要資訊。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>適用於 Windows 10 行動裝置版的 Microsoft Intune 支援結束<!--3544938-->
Microsoft 針對 Windows 10 行動裝置版的主要支援已於 2019 年 12 月結束。 如此支援聲明中所述，Windows 10 行動裝置版使用者將不再具備接收來自 Microsoft 的新安全性更新、非安全性 Hotfix、免費協助支援選項，或線上技術內容更新的資格。 基於已結束的行動裝置版 OS 支援，Microsoft Intune 從 2020 年 8 月 10 日起將終止支援適用於 Windows 10 行動裝置版的公司入口網站應用程式，以及 Windows 10 行動裝置版作業系統。

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？
如果已在組織中部署 Windows 10 行動裝置版裝置，從現在到 2020 年 8 月 10 日為止，您可註冊新裝置、新增或移除原則與應用程式，或更新任何管理設定。 在 8 月 10 日之後，我們將會停止新的註冊，而且最終會從 Intune UI 移除 Windows 10 行動裝置版管理。 裝置將無法再簽入 Intune 服務，而且我們將會刪除裝置與原則資料。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？
您可以檢查您的 Intune 報告，查看哪些裝置或使用者可能會受到影響。 移至 [裝置]   > [所有裝置]  ，然後依作業系統篩選。 您可以新增其他欄，協助識別您組織中誰擁有執行 Windows 10 行動裝置版的裝置。 請要求您的終端使用者升級其裝置，或停止將該裝置用於公司存取。


### <a name="end-of-support-for-legacy-pc-management"></a>結束對舊版電腦管理的支援

自 2020 年 10 月 15 日起結束對舊版電腦管理的支援。 請將裝置升級至 Windows 10，並重新註冊為行動裝置管理 (MDM) 裝置，以繼續交由 Intune 管理。

[深入了解](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>減少 Android 裝置系統管理員的支援<!--5857738-->
Android 裝置系統管理員 (有時稱為「舊版」Android 管理，隨 Android 2.2 發行)，是一種管理 Android 裝置的方式。 不過，您現在可以在 [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) \(隨 Android 5.0 發行\) 中找到已改善的管理功能。 為了要移到現代化、更豐富且更安全的裝置管理，Google 在新的 Android 版本中減少了裝置系統管理員的支援。

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？
由於 Google 的這些變更，Intune 使用者會受到下列方面的影響：  
- Intune 只能為執行 Android 10 和更新版本之裝置系統管理員受控的 Android 裝置提供完整支援，且支援僅提供至 2020 年度第 2 季。 在此期間過後，執行 Android 10 或更新版本之裝置系統管理員受控的裝置將無法再完全受控。 尤其受影響的裝置不會再收到新密碼要求。
    - 在此期間內，Samsung Knox 裝置不會受到影響，因為其透過 Intune 與 Knox 平台的整合來獲得延伸支援。 讓您有更多時間規劃裝置系統管理員管理的轉換。    
- 在 Android 10 以下的 Android 版本上，仍由裝置系統管理員管理的 Android 裝置不會受到影響，並可繼續由裝置系統管理員全權管理。    
- 針對所有執行 Android 10 與更新版本的裝置，Google 已限制裝置系統管理員管理代理程式 (例如公司入口網站) 存取裝置識別碼資訊的能力。 當裝置更新為 Android 10 或更新版本之後，此限制會影響下列 Intune 功能：  
    - VPN 的網路存取控制將不再有效。   
    - 透過 IMEI 或序號識別為公司擁有的裝置將不會自動將裝置標示為公司擁有。  
    - 在 Intune 中，IT 系統管理員再也看不到 IMEI 與序號。 
        > [!NOTE]
        > 這只會影響 Android 10 與更新版本的裝置系統管理員受控裝置，且不會影響受 Android Enterprise 管理的裝置。 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？
若要避免功能在 2020 年度第 3 季減少，建議您執行下列動作:
- 不要在裝置系統管理員管理中上架新裝置。
- 若裝置預期會收到 Android 10 的更新，請將它從裝置系統管理員管理移轉到 Android Enterprise 管理和/或應用程式保護原則。

#### <a name="additional-information"></a>其他資訊
- [Google's guidance for migration from device administrator to Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf) (Google 指南：從裝置系統管理員移轉到 Android Enterprise)
- [Google's documentation on the plan to deprecate the device administrator API](https://developers.google.com/android/work/device-admin-deprecation) (Google 文件：裝置系統管理員 API 淘汰因應措施)