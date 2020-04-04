---
title: 包含檔案
description: 包含檔案
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438728"
---
這些注意事項提供可協助您針對未來的 Intune 變更與功能進行準備的重要資訊。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>適用於 Windows 10 行動裝置版的 Microsoft Intune 支援結束<!--3544938-->
Microsoft 針對 Windows 10 行動裝置版的主要支援已於 2019 年 12 月結束。 如此支援聲明中所述，Windows 10 行動裝置版使用者將不再具備接收來自 Microsoft 的新安全性更新、非安全性 Hotfix、免費協助支援選項，或線上技術內容更新的資格。 基於已結束的行動裝置版 OS 支援，Microsoft Intune 從 2020 年 5 月 11 日起將終止支援適用於 Windows 10 行動裝置版的公司入口網站應用程式，以及 Windows 10 行動裝置版作業系統。

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？
如果已在組織中部署 Windows 10 行動裝置版裝置，從現在到 2020 年 5 月 11 日為止，您可註冊新裝置、新增或移除原則與應用程式，或更新任何管理設定。 在 5 月 11 日之後，我們將會停止新的註冊，而且最終會從 Intune UI 移除 Windows 10 行動裝置版管理。 裝置將無法再簽入 Intune 服務，而且我們將會刪除裝置與原則資料。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？
您可以檢查您的 Intune 報告，查看哪些裝置或使用者可能會受到影響。 移至 [裝置]   > [所有裝置]  ，然後依作業系統篩選。 您可以新增其他欄，協助識別您組織中誰擁有執行 Windows 10 行動裝置版的裝置。 請要求您的終端使用者升級其裝置，或停止將該裝置用於公司存取。


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>「Adobe Acrobat Reader for Intune」行動應用程式的已更新支援聲明<!--5746776-->
我們在 8 月底於 MC188653 中分享了 Adobe Acrobat Reader for Intune 行動應用程式會在 2019 年 12 月 1 日終止生命週期，且 Adobe 已規劃在其主要 Acrobat Reader 應用程式中支援 Intune 的應用程式保護原則。 從那時起，我們收到客戶意見反應，我們需要提供更多時間來繼續讓 IT 系統管理員以 Adobe Acrobat Reader for Intune 為目標，以及讓終端使用者繼續使用它。 有鑑於 Adobe Acrobat Reader for Intune 在終端使用者裝置上有高使用量，以及其在企業案例中的重要性，我們想要確保任何體驗都符合組織的應用程式防護需求。 

雖然 Adobe Acrobat Reader for Intune 應用程式會繼續受支援，直到 2020 年 3 月 31 日為止，我們仍然建議您在原則中將一般的 Acrobat Reader 行動應用程式設為目標，因為 Acrobat Reader 行動應用程式支援應用程式保護原則，且已整合 Intune SDK。 

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？
因為我們的報告指出您組織中的一或多個原則是以 Adobe Acrobat Reader for Intune 應用程式為目標，且/或您已收到我們先前的 EOL 通訊，所以傳送此訊息通知您。 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？
讓您的終端使用者和技術服務人員知道此變更。 您可以使用[公司入口網站的支援資訊功能](../apps/company-portal-app.md#support-information)，來建立 Intune 相關問題的通道。

#### <a name="additional-information"></a>其他資訊
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>採取動作：將 Microsoft Edge 用於受保護的 Intune 瀏覽器體驗<!--5728447-->
隨著過去一年的分享，Microsoft Edge 行動裝置版支援與 Managed Browser 相同的一組管理功能，同時提供大幅改善的終端使用者體驗。 為了讓 Microsoft Edge 中提供的強大體驗得以實現，我們將會淘汰 Intune Managed Browser。 從 2020 年 1 月 27 日開始，Intune 將不再支援 Intune Managed Browser。  

#### <a name="how-does-this-affect-me"></a>此變更會對我造成什麼影響？ 
從 2020 年 2 月 1 日開始，Google Play 商店或 iOS App Store 中將不再提供 Intune Managed Browser。 此時，您仍然可以將新應用程式保護原則的目標設為 Intune Managed Browser，但新的使用者將無法下載 Intune Managed Browser 應用程式。 此外，在 iOS 上，向下推送至 MDM 註冊裝置的新 Web 剪輯，將會在 Microsoft Edge 中開啟，而不是在 Intune Managed Browser 中開啟。  

從 2020 年 3 月 31 日起，將從 Azure 主控台移除 Intune Managed Browser。 這表示您將無法再為 Intune Managed Browser 建立新原則。 現有的 Intune Managed Browser 原則不會受到影響。 Intune Managed Browser 將會顯示在主控台中，作為沒有圖示的 LOB 應用程式，而現有的原則仍會顯示為以應用程式為目標。 此時，我們也會在應用程式保護原則的 [資料保護] 區段中，移除將 Web 內容重新導向至 Intune Managed Browser 的選項。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要為這項變更做什麼準備？ 
若要確保從 Intune Managed Browser 順利轉換到 Microsoft Edge，建議您主動執行下列步驟： 

1. 使用應用程式保護原則 (亦稱為 MAM) 與應用程式組態設定，以適用於 iOS 與 Android 的 Microsoft Edge 為目標。 您也可以將現有原則的目標設定為 Microsoft Edge，以針對 Microsoft Edge 重複使用 Intune Managed Browser 原則。  
2. 確定您環境中所有受 MAM 保護的應用程式的應用程式保護原則設定 [限制使用其他應用程式的 Web 內容傳輸] 設定為 [受原則管理的瀏覽器]。 
3. 在受管理的應用程式組態設定 "com.microsoft.intune.useEdge" 設定為 True 的情況下以所有受 MAM 保護的項目為目標。 從下個月將推出的 1911 版開始，您只需要設定 [限制使用其他應用程式的 Web 內容傳輸] 設定以在您應用程式保護原則的 [資料保護] 區段中選取 [Microsoft Edge]，就可以完成步驟 2 與 3。 

即將推出對 iOS 與 Android 上 Web 剪輯的支援。 當此支援發行後，您必須為預先存在的 Web 剪輯重定目標，以確保其在 Microsoft Edge 中開啟，而不是在 Managed Browser 中開啟。 

#### <a name="additional-information"></a>其他資訊
如需詳細資訊，請參閱我們的[搭配應用程式保護原則使用 Microsoft Edge](../apps/manage-microsoft-edge.md) 相關文件，或我們的[支援部落格文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269)。

### <a name="end-of-support-for-legacy-pc-management"></a>結束對舊版電腦管理的支援

自 2020 年 10 月 15 日起結束對舊版電腦管理的支援。 請將裝置升級至 Windows 10，並重新註冊為行動裝置管理 (MDM) 裝置，以繼續交由 Intune 管理。

[深入了解](https://go.microsoft.com/fwlink/?linkid=2107122)


