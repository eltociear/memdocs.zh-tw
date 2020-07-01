---
title: Ready for Windows
titleSuffix: Configuration Manager
description: 關於 Ready for Windows 網站的淘汰
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 18e703691696a2cfc02a5b9715fb6062360229e2
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353457"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Ready for modern desktop 淘汰的常見問題集

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Ready for Windows 採用狀態

採用狀態會以與 Microsoft 共用資料之商業裝置的資訊為基礎。 此狀態會與軟體廠商的支援聲明整合。

電腦分析則為在商業裝置中找到的每個資產版本提供採用狀態。 此狀態不包含取用者裝置的資料或不共用資料的裝置資料。 而且此狀態並不代表所有 Windows 10 裝置的採用率。

可能的類別包括：

- **已高度採用**：至少有 100,000 部商業 Windows 10 裝置安裝此應用程式。

- **已採用**：至少有 10,000 部商業 Windows 10 裝置安裝此應用程式。

- **資料不足**：共用此應用程式資訊的商業 Windows 10 裝置太少，因此 Microsoft 無法分類其採用狀況。

- **連絡開發人員**：此應用程式版本可能有相容性問題。 Microsoft 建議連絡軟體提供者以深入了解。

- **未知**：此應用程式的此版本沒有可用的資訊。 應用程式的其他版本可能會提供資訊。

## <a name="general"></a>一般

### <a name="what-happened-to-the-ready-for-windows-website"></a>Ready for Windows 網站發生了什麼事？

許多客戶在使用 Windows 10 與 Office 365 ProPlus 時，都會面臨困難。 其中最主要的問題就是測試應用程式，因為這項流程通常為手動。 這導致 IT 系統管理員及應用程式擁有者需要花費大量時間來持續分析現有的應用程式，然後針對產生的問題進行補救。

*Ready for modern desktop* 目錄已列出軟體解決方案，這些解決方案可支援並使用於執行 Windows 10 與 Office 365 ProPlus 的商業裝置上。 此目錄可協助正為其部署而考慮最新版本 Windows 10 與 Office 365 的 IT 主管。

根據 IT 主管們的意見反應，其希望將這些見解與已經用於部署計劃的工具整合在一起。 使用[電腦分析](https://aka.ms/dadocs)與 [Office 365 ProPlus 整備功能](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch)在 Configuration Manager 中規劃及管理 Windows 10 與 Office 365 ProPlus 升級專案。 

> [!Note]
> 從 2020 年 4 月 21 日開始，「Office 365 專業增強版」會重新命名為「Microsoft 365 Apps 企業版」。 如需詳細資訊，請參閱 [Office 365 專業增強版的名稱變更](https://docs.microsoft.com/deployoffice/name-change) \(部分機器翻譯\)。 在主控台正在進行更新時，您在 Configuration Manager 主控台與輔助文件中可能仍會看到提及舊名稱。

### <a name="what-is-desktop-analytics"></a>什麼是電腦分析？

[電腦分析](https://aka.ms/dadocs)是以雲端為基礎的服務，其整合了 Configuration Manager。 這項服務可提供您見解與智慧，有助針對自己的 Windows 端點更新整備做出旁徵博引的決定。 其結合組織的特定資料，且彙總了來自數百萬部 Windows 裝置 (連線至 Microsoft 雲端服務) 的見解。

-    全面了解組織中管理的端點、應用程式及驅動程式。

-    使用最新 Windows 功能更新來評定應用程式與驅動程式的相容性。 取得已知問題的風險降低建議，以及企業營運應用程式的深入見解。

-    使用 Microsoft 雲端的人工智慧 (AI)，以最佳化可充分代表整體環境的試驗裝置。

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>為什麼應該針對 Windows 部署計劃使用電腦分析？

電腦分析提供下列幾項優點：

-    **裝置與軟體清查**：對應用程式與 Windows 版本等關鍵因素進行清查。

-    **試驗識別**：識別涵蓋提供最廣泛因素的最小設備集合。 其著重於對於 Windows 升級與更新試驗最重要的因素。 確定試驗更加成功，讓您可以更快速且更安心地在生產環境中進行廣泛的部署。

-    **問題識別**：透過使用彙總的市場資料與您環境中資料，本服務能夠預測潛在問題，以隨時讓 Windows 保持在最新狀態。 然後會建議可行的風險降低措施。

-    **Configuration Manager 整合**：本服務能讓現有的內部部署基礎結構進入雲端。 透過使用此資料與分析，在裝置上部署與管理 Windows。

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>*Ready for Windows* 狀態在電腦分析中的意義為何？

**採用狀態**是以與 Microsoft 共用資料的商業裝置資訊為基礎。 此狀態會與軟體廠商的支援聲明整合。

電腦分析則為在商業裝置中找到的每個資產版本提供採用狀態。 此狀態不包含取用者裝置的資料或不共用資料的裝置資料。 而且此狀態並不代表所有 Windows 10 裝置的採用率。

如需詳細資訊，請參閱[相容性評定](compat-assessment.md)。

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>哪些資產可以在電腦分析中取得 *Ready for Windows* 狀態？ 

資產可以在電腦分析中擁有 *Ready for Windows* 狀態，如果：

-    軟體提供者宣告支援解決方案。
-    客戶已將其部署在與 Microsoft 共用資訊的大量商業 Windows 10 裝置上。
-    該資產與商業使用者相關。

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>我還可以在電腦分析中取得哪些見解？

電腦分析可供清查[裝置與其安裝的應用程式](about-assets.md)，以及針對企業營運應用程式的[深入見解](compat-assessment.md#advanced-insights)。 

## <a name="software-providers"></a>軟體提供者

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>我仍然可以在電腦分析中列出軟體解決方案嗎？

請為您的產品發佈支援聲明，其可於 32 位元或 64 位元的 Windows 10 或 Office 365 ProPlus 中作業。 若要在電腦分析中展示解決方案，請連絡 Microsoft 連絡人。

### <a name="how-can-listing-my-solutions-benefit-me"></a>列出解決方案有什麼好處？

數以千計的 IT 系統管理員使用 Configuration Manager 與電腦分析來管理數百萬部裝置。 他們使用這些工具，以安心地規劃並將組織升級至最新版本的 Windows 10 與 Office 365 ProPlus。 他們也會透過這些工具來做出購買軟體解決方案的決策。

Microsoft 整合軟體廠商的支援聲明與從商業裝置接收到的採用資訊。 世界各地的組織都在電腦分析與 Office 整備工具中使用這些資料。 

如果支援聲明未正確地與資產建立關聯，請連絡 Microsoft 連絡人。

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>可以在我的資產上看到詳細的效能標準嗎？

透過開發人員中心的健全狀況與計量報表，以評定解決方案的效能： 

- [Windows Store](https://docs.microsoft.com/windows/uwp/publish/health-report) (Windows 市集)
- [Desktop](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program) (電腦)
- [Office Add-ins](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) (Office 增益集) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>我要如何開發適用於 Windows 10 和 Office 365 ProPlus 的相容資產？

請確保傳統型應用程式目前與 Windows 10 相容，並在未來繼續與其保持相容。 如需詳細資訊，請參閱[適用於開發人員的應用程式相容性](https://developer.microsoft.com/windows/desktop/app-compatibility)。

如果您要開發 Office 365 ProPlus 的解決方案，請參閱[適用於 Office 中 COM、VSTO 及 VBA 增益集的開發最佳作法](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office)。
