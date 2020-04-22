---
title: 什麼是 Configuration Manager？
titleSuffix: Configuration Manager
description: 了解 Microsoft Endpoint Configuration Manager 的基本概念。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78b9175c10d4389623bfa08ac7895df200944a13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706906"
---
# <a name="what-is-configuration-manager"></a>什麼是 Configuration Manager？

適用於：  Configuration Manager (最新分支)

從 1910 版開始，Configuration Manager 現在是 Microsoft 端點管理員的一部分。

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager 是一個整合的解決方案，可用於管理您的所有裝置。 Microsoft 將 Configuration Manager 和 Intune 整合在一起，其不需要複雜的移轉，並擁有簡化的授權。 繼續運用現有的 Configuration Manager 投資，同時以自有步調來利用 Microsoft 雲端的強大功能。

下列 Microsoft 管理解決方案全都是 **Microsoft Endpoint Manager** 品牌的一部分：

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [電腦分析](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- [裝置管理系統管理員主控台](https://go.microsoft.com/fwlink/?linkid=2109094)中的其他功能

如需詳細資訊，請參閱 [Microsoft Endpoint Configuration Manager 常見問題集](microsoft-endpoint-manager-faq.md)。

## <a name="introduction"></a>簡介

使用 Configuration Manager 來協助進行下列系統管理活動：

- 透過減少手動工作，並讓您專注於高價值專案，來提高 IT 生產力與效率。  
- 最大化硬體和軟體投資。  
- 適時提供正確的軟體，來加強使用者產能。  

Configuration Manager 可協助您提供更具效益的 IT 服務，方法是啟用：

- 安全且可調整規模的應用程式、軟體更新和作業系統部署。
- 受控裝置上的即時動作。
- 內部部署和網際網路裝置的雲端支援分析和管理。
- 合規性設定管理。  
- 伺服器、桌上型電腦和膝上型電腦的全方位管理。

Configuration Manager 可擴充並與許多 Microsoft 技術和解決方案搭配使用。 例如，Configuration Manager 可整合：  

- Microsoft Intune，以共同管理各種行動裝置平台
- Microsoft Azure，以裝載雲端服務來擴充管理服務
- Windows Server Update Services (WSUS) 來管理軟體更新
- 憑證服務
- Exchange Server 和 Exchange Online
- 群組原則
- DNS
- Windows Automated Deployment Kit (Windows ADK) 和使用者狀態移轉工具 (USMT)
- Windows 部署服務 (WDS)
- 遠端桌面和遠端協助

Configuration Manager 也會使用：  

- Active Directory 網域服務和 Azure Active Directory，以取得安全性、服務位置和設定，並探索您要管理的使用者和裝置。  
- Microsoft SQL Server 作為分散式變更管理資料庫，並與 SQL Server Reporting Services (SSRS) 整合以產生報告，用來管理及追蹤管理活動。  
- 擴充管理功能並使用 Internet Information Services (IIS) 的 Web 服務的站台系統角色。
- 傳遞最佳化、Windows 低額外延遲背景傳輸 (LEDBAT)、背景智慧型傳送服務 (BITS)、BranchCache 和其他對等快取技術，以協助管理網路上和裝置之間的內容。

若要在生產環境中成功使用 Configuration Manager，請徹底規劃並測試管理功能。 Configuration Manager 是功能強大的管理應用程式，因此可能會影響組織中的每一部電腦。 若您部署及管理 Configuration Manager 時仔細規劃並考量業務需求，Configuration Manager 就能減少您的系統管理負荷與整體擁有成本。  

## <a name="user-interfaces"></a>使用者介面

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a> Configuration Manager 主控台

在您安裝 Configuration Manager 之後，可使用 Configuration Manager 主控台設定站台和用戶端，並執行和監視管理工作。 此主控台是主要系統管理點，可讓您管理多個站台。  

您可以在其他電腦上安裝 Configuration Manager 主控台，並使用以 Configuration Manager 角色為基礎的系統管理來限制存取權，以及系統管理使用者可以在主控台中查看哪些項目。  

如需詳細資訊，請參閱[使用 Configuration Manager 主控台](../servers/manage/admin-console.md)。

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a> 軟體中心

**軟體中心**是您在 Windows 裝置上安裝 Configuration Manager 用戶端時所安裝的應用程式。 使用者可以使用軟體中心來要求並安裝您所部署的軟體。 軟體中心可讓使用者執行下列動作：  

- 瀏覽並安裝應用程式、軟體更新和新的 OS 版本
- 檢視其軟體要求歷程記錄
- 根據組織的原則來檢視裝置合規性

您也可以在軟體中心顯示自訂索引標籤來符合其他商務需求。

如需詳細資訊，請參閱[軟體中心使用者指南](software-center.md)。

## <a name="next-steps"></a>後續步驟

安裝 Configuration Manager 之前，請先熟悉下列基本概念和詞彙：

- 若您已熟悉 System Center 2012 Configuration Manager，請參閱 [System Center 2012 Configuration Manager 的變更內容](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md)。

- 如需 Configuration Manager 的高階技術概觀，請參閱 [Configuration Manager 的基礎](fundamentals.md)。

若您已熟悉這些基本概念，請使用此文件庫來協助您成功地部署與使用 Configuration Manager。 請從下列文章開始：

- [Configuration Manager 的功能](../plan-design/changes/features-and-capabilities.md)  
- [選擇裝置管理解決方案](../plan-design/choose-a-device-management-solution.md)  
- [建置專屬實驗室環境來評估 Configuration Manager](../get-started/set-up-your-lab.md)
- [尋找使用 Configuration Manager 的說明](find-help.md)  
