---
title: 電腦分析
titleSuffix: Configuration Manager
description: 與 Configuration Manager 整合的電腦分析服務概觀。
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b280661c4de9282d3907b7d480477fc67f6a8dc5
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824059"
---
# <a name="what-is-desktop-analytics"></a>什麼是電腦分析？

電腦分析是與 Configuration Manager 整合的雲端式服務。 這項服務可提供您見解與智慧，有助您針對自己的 Windows 用戶端更新整備做出更旁徵博引的決定。 其結合了您組織的資料，以及從連線到 Microsoft 雲端服務之數百萬部裝置彙總而成的資料。

您可以搭配 Configuration Manager 使用電腦分析來執行下列作業：  

- 為您組織中正在執行的應用程式建立清查  

- 使用最新的 Windows 10 功能更新，評估應用程式相容性  

- 找出相容性問題，並根據具備雲端功能的資料見解獲得風險降低建議  

- 建立試驗群組，來代表一組最少裝置上的整個應用程式和驅動程式資產  

- 將 Windows 10 部署到試驗和生產環境受控裝置  

![Azure 入口網站中電腦分析首頁的螢幕擷取畫面](media/portal-home.png)

下列影片是來自 Ignite 2019 的研討會，其中包含有關電腦分析的詳細資訊：

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[透過資料導向的見解，使用電腦分析和 Configuration Manager 降低 Windows TCO，以利管理、服務及支援](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions) (英文)

跳至 10:00 以取得深入示範。

> [!Note]  
> 電腦分析是 Windows Analytics 的後續任務，Windows Analytics 已在 2020 年 1 月 31 日淘汰。
>
> Windows Analytics 的功能結合在電腦分析服務中。 電腦分析也與 Configuration Manager 更緊密整合。 如需詳細資訊，請參閱 [Windows Analytics 客戶的常見問題集](faq.md#existing-windows-analytics-customers)。

## <a name="benefits"></a>優點

許多客戶在讓 Windows 10 保持最新狀態時面臨挑戰。 主要挑戰是測試應用程式。 這通常是手動程序。 這導致 IT 系統管理員及應用程式擁有者需要花費大量時間來持續分析現有的應用程式。 然後針對所產生的任何問題進行補救。

電腦分析提供了下列幾項優點：

- **裝置與軟體清查**：對應用程式與 Windows 版本等關鍵因素進行清查。  

- **試驗識別**：識別涵蓋提供最廣泛因素的最小設備集合。 其關注的重點在於對 Windows 升級及更新試驗最重要的因素。 確定試驗更加成功，讓您可以繼續更快速且更安心地在生產環境中進行廣泛的部署。  

- **問題識別**：透過使用彙總的市場資料與您環境中資料，本服務能夠預測潛在問題，以隨時讓 Windows 保持在最新狀態。 然後會建議可行的風險降低措施。  

- **Configuration Manager 整合**：本服務能讓您現有的內部部署基礎結構進入雲端。 透過使用此資料與分析，在您的裝置上部署與管理 Windows。  

## <a name="prerequisites"></a>先決條件

若要使用電腦分析，請確定您的環境符合下列必要條件。

### <a name="technical"></a>技術

- 具有[全域管理員](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)權限的使用中全球 Azure 訂用帳戶。 不支援 [Microsoft 帳戶](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts)。  

    > [!Important]  
    > 電腦分析目前需要您在 Azure AD 租用戶中部署 Office 365 服務。 未來將不會有此需求。

    - [工作區擁有者] 權限以完成 [設定您的工作區] 步驟，以及下列角色：  

      - [**電腦分析系統管理員**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions)角色。

      - 資源群組的 [**Log Analytics 參與者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor)和[**使用者存取系統管理員**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)，以便使用現有的工作區，或在現有的資源群組中建立新的工作區。

      - 訂用帳戶的[**擁有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)或[**參與者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)以及[**使用者存取系統管理員**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)權限，以便在新的資源群組中建立工作區。  

    - 若要在上線之後存取入口網站，您必須：

      - 在工作區建立所在的資源群組上具有[**電腦分析系統管理員**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) \(部分機器翻譯\) 角色與[**擁有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) \(部分機器翻譯\) 或[**參與者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) \(部分機器翻譯\) 權限。

- Configuration Manager 1902 版含更新彙總套件 (4500571) 或更新版本。 如需詳細資訊，請參閱[更新 Configuration Manager](connect-configmgr.md#bkmk_hotfix)。  

    - Configuration Manager 的[**系統高權限管理員**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles)角色  

    > [!NOTE]
    > 電腦分析支援多個向單一 Azure AD 租用戶報告的 Configuration Manager 階層。<!-- 4814075 --> 如果您的環境中有多個階層，則有下列選項：
    >
    > - 使用不同的商業識別碼與 Azure AD 租用戶。
    > - 將兩個階層設定為使用相同的商業識別碼，以共用 Azure AD 租用戶與電腦分析執行個體。 使用[不同的應用程式](connect-configmgr.md#bkmk_connect)來將每個階層連線。 中斷與階層的連線後，入口網站最多可能需要 30 天的時間來反映變更。 

- 執行 Windows 7、Windows 8.1 或 Windows 10 的裝置  

    - 安裝最新的更新。 如需詳細資訊，請參閱[更新裝置](enroll-devices.md#update-devices)。  

    - 裝置也必須具有 Configuration Manager 用戶端 1902 版含更新彙總套件 (4500571) 或更新版本。 如需詳細資訊，請參閱[更新 Configuration Manager](connect-configmgr.md#bkmk_hotfix)。  

    > [!Note]  
    > 電腦分析不支援升級至 Windows 10 長期維護通道 (LTSC)。 如需詳細資訊，請參閱 [Windows 即服務概觀](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。
    >
    > 電腦分析的設計，是為了能更好地支援就地升級案例。 如果您需要進行重大變更 (例如從 32 位元變更為 64 位元架構)，請使用映像處理案例。 在這些傳統 OS 部署案例中，電腦分析見解仍然具有參考價值，但您可以忽略就地升級特定的指導方針。 如需詳細資訊，請參閱[使用 Configuration Manager 部署企業作業系統的案例](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)。

- Windows 診斷資料。 如需詳細資訊，請參閱下列文章：  

    - [診斷資料層級](enable-data-sharing.md#diagnostic-data-levels)  

    - [電腦分析隱私權](privacy.md)  

- 從裝置到 Microsoft 公用雲端的網路連線。 如需詳細資訊，請參閱[如何啟用資料共用](enable-data-sharing.md)  

> [!Important]
> Microsoft 堅決致力於提供可讓您掌控隱私權的工具和資源。 因此，Microsoft 不會從位於歐洲國家/地區 (EEA 和瑞士) 的裝置收集下列資料：
>
> - Windows 8.1 裝置的 Windows 診斷資料
> - Windows 7 的應用程式使用方式資料

### <a name="licensing-and-costs"></a>授權與費用

- 有效的全球 Azure 訂閱。

    > [!NOTE]
    > Configuration Manager 的大部分對等訂閱也包括 Azure AD。 例如，請參閱 [Microsoft 365 方案](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans)和 [Enterprise Mobility + Security 授權](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security)。

- 註冊於電腦分析中的裝置需要 Configuration Manager 有效授權。 如需詳細資訊，請參閱 [Configuration Manager 授權](../core/understand/product-and-licensing-faq.md)。

- 裝置的使用者需要下列其中一種授權：

  - Windows 10 企業版 E3 或 E5 (隨附於 Microsoft 365 F3、E3 或 E5 中)

  - Windows 10 教育版 A3 或 A5 (隨附於 Microsoft 365 A3 或 A5)

  - Windows 虛擬桌面存取 E3 或 E5  

> [!NOTE]
> 除了這些授權訂閱的費用之外，在 Azure Log Analytics 中使用電腦分析不需支付額外費用。 電腦分析所擷取的資料類型不收取任何 Log Analytics 資料擷取和保留費用。 此資料作為非計費資料類型，也不會受限於任何 Log Analytics 每日資料擷取上限。 如需詳細資訊，請參閱 [Log Analytics 使用方式和費用](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)。

## <a name="next-steps"></a>後續步驟

下列教學課程提供逐步指南，協助您開始使用電腦分析與 Configuration Manager：
  
> [!div class="nextstepaction"]
> [將 Windows 10 部署到試驗](tutorial-windows10.md)
