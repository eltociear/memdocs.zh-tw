---
title: 電腦分析常見問題集
titleSuffix: Configuration Manager
description: 電腦分析常見問題集。
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c6b8df10a9a20c96cd2f8c1a0b6583c9c5f6e4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708156"
---
# <a name="desktop-analytics-faq"></a>電腦分析常見問題集

## <a name="prerequisites"></a>先決條件

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> 我可以將具備雲端功能的分析搭配 Intune 管理的裝置使用嗎？

目前不行，但請參閱 Microsoft Ignite 2019 的公告 [insights-driven device management](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions) (見解導向的裝置管理)。 這個經規劃解決方案是裝置健全狀況和更新整備小幫手的後續任務。

從電腦分析工作流程中受益的絕大多數客戶都是使用 Configuration Manager 來部署 Windows。 我們了解 Intune 客戶喜歡分析資料中的其他見解，而我們也正致力於研究與其共同見解的方法。

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>已經超過 72 小時，且入口網站仍然在處理資料，該怎麼辦？

當第一次設定電腦分析時，Configuration Manager 和電腦分析入口網站中的報告可能不會立即顯示完整資料。 這項服務可能需要 2 - 3 天的時間來處理資料。 如果已經超過 72 小時，且入口網站仍然在處理資料，請執行下列步驟：

- 若要確認是否已正確設定作用中裝置，請使用[連線健全狀況儀表板](monitor-connection-health.md)， 但此儀表板並不會即時更新。
- 請確定裝置正在將診斷資料傳送至電腦分析服務。 如需詳細資訊，請參閱[啟用資料共用](enable-data-sharing.md)。
- 在 Azure AD 上佈建 [Azure AD 應用程式](troubleshooting.md#bkmk_AzureADApps)。
- 檢查過去七天內與組織建立關聯的裝置。 在[電腦分析入口網站](https://aka.ms/desktopanalytics)中，移至 [已連線的服務]  窗格。 選取 [註冊裝置]  和 [查看最近的資料] 

如果裝置已正確設定，且您仍然看不到工作區中的資料，請[連絡 Microsoft 支援服務](https://support.microsoft.com/hub/4343728/support-for-business)。

## <a name="connect-configuration-manager"></a>連線 Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>我可以變更目標或其他集合嗎？

是，請執行下列流程：

- 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。 開啟與電腦分析服務建立關聯的項目屬性。

- 在 [電腦分析連線]  索引標籤上，變更**目標集合**或管理其他集合。

> [!IMPORTANT]  
> Configuration Manager 使用設定原則來設定目標集合中的裝置。 此原則包括可讓裝置將資料傳送至 Microsoft 的診斷資料設定。 變更目標集合並不會復原裝置上的設定原則 (即使該裝置已不再位於該目標集合中)。 如果不想要讓裝置繼續傳送診斷資料，請[重新設定裝置](account-close.md#reconfigure-clients)。

## <a name="windows-upgrade"></a>Windows 升級

### <a name="can-i-upgrade-windows-and-change-architecture"></a>我可以升級 Windows 和變更架構嗎？

電腦分析的設計是為了能更好地支援就地升級， 而就地升級並不支援從 32 位元到 64 位元的架構移轉。 如果您需要在此案例中移轉電腦，請使用重新整理案例。 在此案例中，電腦分析見解仍然具有參考價值，但您可以忽略升級特定指導。

如需詳細資訊，請參閱[使用新的 Windows 版本重新整理現有的電腦](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)。

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>升級 Windows 時，可以將 BIOS 變更為 UEFI 嗎？

是。 如需詳細資訊，請參閱[在就地升級期間將 BIOS 轉換至 UEFI](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>可以搭配 Windows 10 LTSC 使用電腦分析嗎？

電腦分析不支援 Windows 10 長期維護通道 (LTSC) 裝置。 如需詳細資訊，請參閱 [Windows 即服務概觀](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>可以減少電腦分析入口網站中重新整理資料所需的時間嗎？

電腦分析入口網站中有兩種類型的資料：系統管理員資料與診斷資料。 若要依需求重新整理系統管理員資料，請開啟 [資料流通] 飛出視窗，然後選取 [套用變更]  。 此動作會立即觸發工作區的任何擱置中系統管理員變更的一次性重新整理。 這些變更會在 15 - 60 分鐘內散佈並全面套用， 其花費時間取決於工作區大小與擱置變更的範圍。 在 24 小時的期間內，可以視需要要求重新整理最多六次資料。

所有資料每天會自動更新一次，即使不要求重新整理資料也一樣。 然而，您無法視需要觸發診斷資料的重新整理。 如需電腦分析中不同資料類型的詳細資訊，請參閱[資料延遲](troubleshooting.md#data-latency)。

## <a name="privacy"></a>隱私權

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>可以不需要將直接用戶端連線到 Microsoft 資料管理服務，就能使用電腦分析嗎？

否，整個服務都是由 Windows 診斷資料提供技術支援，而這需要裝置具有此直接連線能力。

### <a name="can-i-choose-the-data-center-location"></a>可以選擇資料中心位置嗎？

針對 Azure Log Analytics：是，在設定電腦分析並建立 Log Analytics 工作區的情況下。

針對 Microsoft 資料管理服務與分析 Azure 儲存體：否，這兩項服務是在美國託管。

### <a name="where-is-my-organizations-data-stored"></a>我的組織資料會儲存在哪裡？

來自電腦的 Windows 診斷資料會在位於美國、由 Microsoft 管理的安全資料中心進行加密、傳送及處理。 Microsoft 會透過 Azure 入口網站中電腦分析解決方案來提供電腦分析相關資料的分析。 絕大部分[可使用 Log Analytics](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all) 的區域亦支援電腦分析。 即使選取國際 Azure 區域，診斷資料仍會傳送至位於美國的 Microsoft 安全資料中心並加以處理。

## <a name="existing-windows-analytics-customers"></a>現有的 Windows Analytics 客戶

> [!Important]  
> Windows Analytics 服務已在 2020 年 1 月 31 日淘汰。
>
> 如需詳細資訊，請參閱 [KB 4521815：Windows Analytics 於 2020 年 1 月 31 日淘汰](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>可以搭配電腦分析使用更新合規性嗎？

是。 如果您目前已經在 Azure 入口網站中使用[更新合規性](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)，則無論是現在或 2020 年 1 月之後您都可以繼續使用。

如需詳細資訊，請參閱 [KB 4521815：Windows Analytics 於 2020 年 1 月 31 日淘汰](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>電腦分析中是否有任何無法使用的 Windows Analytics 功能？

<!-- 3616924 -->
是，下列 Windows Analytics 功能已從電腦分析中淘汰或尚未提供使用：

#### <a name="general"></a>一般

- 支援不需要 Configuration Manager 的案例。 例如，[Intune 支援](#bkmk_intune)。
- 任何有效 Windows 授權與 E3、E5 的授權先決條件
- 支援每個 Azure AD 租用者擁有多個工作區
- 執行自訂查詢並匯出原始解決方案資料的能力
- 自訂報表的資料模型文件

#### <a name="upgrade-readiness"></a>更新整備小幫手

- Internet Explorer 網站探索資料
- Office 增益集見解 (現已可於 [Configuration Manager 中使用](#bkmk_office))
- 意見反應中樞見解

#### <a name="update-compliance"></a>更新合規性

- 支援商務用 Windows Update
- 傳遞最佳化見解
- 支援 Windows 10 長期維護通道 (TSC)
- Windows 測試人員報告
- Windows Defender 狀態

> [!Note]
> 所有現有更新合規性功能 (包含電腦分析中無法使用的功能)，仍可於 Azure 入口網站的[更新合規性](/windows/deployment/update/update-compliance-get-started)解決方案中取得。

#### <a name="device-health"></a>裝置健全狀況

- 驅動程式健全狀況
- 應用程式健全狀況 (部署計劃外部)
- 經常損毀的裝置或驅動程式所導致損毀
- Windows 登入健全狀況
- Windows 資訊保護
- 支援 Windows Server

## <a name="other"></a>其他

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a> 可以使用電腦分析進行 Office 365 ProPlus 升級嗎？

否，電腦分析主要著重於 Windows。 Microsoft 開發了與許多客戶密切共同作業的電腦分析， 而客戶的意見反應是關於電腦分析如何改善其能力，以讓其自信地管理 Windows 部署。 我們也得知，客戶希望 [Office 365 ProPlus 整備](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)能夠與 Configuration Manager 及 Intune 中的 Office 管理工具更加緊密地整合。 Microsoft 會持續投資這些區域，並專注於電腦分析的 Windows 案例。

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>可以如何提供有關電腦分析的意見反應？

若要分享對電腦分析的意見反應，請選取入口網站上方的**傳送笑臉**圖示。 請一併將螢幕擷取畫面包含在其中，以協助 Microsoft 進一步了解您的意見反應。 您也可以在 [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805) 提交產品建議，並附議其他想法。

> [!Note]
> 請永遠不要透過「傳送笑臉」或 UserVoice 分享私人資訊， 這類私人資訊也包含您的租用者識別碼或商業識別碼。Microsoft 並不會透過「傳送笑臉」或 UserVoice 通道來提供支援。 若要取得電腦分析工作區的說明，請選取導覽功能表中的 [說明及支援]  連結，以開啟支援票證。
