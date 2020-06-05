---
title: Technical Preview 版本
titleSuffix: Configuration Manager
description: 了解可試用 Configuration Manager 新功能的 Technical Preview 分支。
ms.date: 05/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4c0842a3e23eb8503c945073a4be35db5173086
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226248"
---
# <a name="technical-preview-for-configuration-manager"></a>設定管理員的 Technical Preview

適用於：Configuration Manager (Technical Preview 分支)

本文提供有關 Configuration Manager 每月 Technical Preview 分支的詳細資料。 Technical Preview 會導入 Microsoft 正致力於開發的新功能。 它會導入 Configuration Manager 最新分支中尚未包含的新功能。 這些功能最後可能會包含於最新分支的更新中。 在我們完成功能之前，希望您能親身體驗它們並提供意見反應給我們。

由於這一版是 Technical Preview，因此詳細資料和功能可能會有所變更。

此資訊適用於所有版本的 Configuration Manager Technical Preview 分支。 本文列出每個新功能以及該功能第一次出現的 Technical Preview 版本。 例如，**2001** 版代表 2020 (`20`) 年一月 (`01`)。 專屬於每個預覽版的個別文章都會詳細說明各個功能。

如需 Configuration Manager「最新分支」的新功能相關資訊，請參閱 [Configuration Manager 累加版本的新功能](../plan-design/changes/whats-new-incremental-versions.md)。

> [!Tip]
> 若要在此頁面更新時收到通知，請複製下列 URL 並貼到您的 RSS 摘要讀取程式：`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> 需求和限制

> [!IMPORTANT]
> Technical Preview 僅授權在實驗室環境中使用。 Microsoft 可能無法提供支援服務，而技術預覽版可能未提供某些功能。 此外，相較於市面上提供的軟體，技術預覽軟體的安全性、隱私權、可存取性、可用性和可靠性標準可能較低或有所差異。

如需大部分的產品先決條件，請使用[支援的設定](../plan-design/configs/supported-configurations.md)中的資訊。 以下是 Technical Preview 分支適用的例外狀況：

- 每個安裝的有效期為 90 天，之後即變成無效。

- 英文是唯一支援的語言。

- 它只支援下列安裝程式命令列參數：

  - `/silent`
  - `/testdbupgrade`

- 服務連接點會安裝為線上模式。 它不支援離線模式。

- 每個特定 Technical Preview 版本的個別文章都會包含其他限制或需求 (適用時)。

- Technical Preview 分支不支援下列功能：

  - [移轉](../migration/migrate-data-between-hierarchies.md)到這個預覽分支或從中移出。

  - [升級](../servers/deploy/install/upgrade-to-configuration-manager.md)到這個預覽分支。

  - 從 cd.latest 資料夾進行[站台復原](../servers/manage/recover-sites.md)。<!--507106-->

- 不支援從這個預覽分支更新到最新分支。

    > [!Note]
    > 為預覽版提供可用更新時，您仍然可以從 Configuration Manager 主控台的 [更新與服務] 節點尋找並安裝更新。 如需在主控台中進行升級程序的影片，請參閱 youtube.com 上的[安裝 Configuration Mananger 更新套件](https://www.youtube.com/embed/KBd_EGFbUT8) \(英文\)。

- 它只支援獨立的主要站台。 不支援管理中心網站、多個主要站台或次要站台。

Configuration Manager 的 Technical Preview 分支可支援下列產品和技術：

- 除非另有說明，否則技術預覽分支與最新分支支援相同版本的 SQL Server。 如需詳細資訊，請參閱[支援的 SQL Server 版本](../plan-design/configs/support-for-sql-server-versions.md)。

- 站台支援最多 10 個用戶端，用戶端可以執行任何[支援的用戶端 OS 版本](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。<!-- SCCMDocs#1656 -->

> [!Note]
> 在此內容中包含這些產品，並不代表可對已超過其支援週期的版本延長支援。 Configuration Manager 不支援已超過其支援週期的產品。 如需詳細資訊，請參閱 [Microsoft 週期原則](https://support.microsoft.com/lifecycle)。

## <a name="install-and-update"></a><a name="bkmk_install"></a> 安裝及更新

供實驗室使用的 Configuration Manager Technical Preview 分支，與在生產環境中使用的 Configuration Manager 最新分支不同。

首先，安裝 Technical Preview 分支的基準版本。 安裝基準版本之後，接著使用主控台內的更新，使安裝與最新的預覽版本保持同步。 一般而言，每個月都會提供新版本的 Technical Preview。

Microsoft 支援每個 Technical Preview 版本，直到有三個連續版本可供使用為止。 例如，發行 1908 版時，就不再支援 1904 版， 但仍支援 1905 版、1906 版和 1907 版。 當基準不受支援時，假設您會立即更新到支援的版本，則它仍支援安裝新的 Technical Preview 網站。 在新的基準版本可供使用之前，仍會支援舊版的基準。 除非您安裝最新的 Technical Preview 版本，否則，請從基準更新為最新的可用版本，然後重複執行更新程序。

> [!TIP]
> 當您將更新安裝為 Technical Preview 時，可以將 Preview 安裝更新為新的 Technical Preview 版本。 Technical Preview 安裝永遠無法選擇升級為最新分支安裝。 它也永遠不會接收到來自最新分支版本的更新。
>
> 一年內有數次，Technical Preview 分支和最新分支版本會使用相同的版本號碼。 例如，會有 Technical Preview 1910 版和最新分支 1910 版。

### <a name="active-baseline-versions"></a>作用中的基準版本

在基準版本發行後的一年內安裝該版本。 當安裝新的 Technical Preview 站台時，請使用最新的基準版本。

- **Technical Preview 2002 版**：Configuration Manager Technical Preview 分支 2002 版同時會以兩種形式提供：主控台內更新和新的基準版本。

從 [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) 下載基準版本。

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> 提供意見反應

歡迎您提供有關 Technical Preview 新功能的意見反應。 如需詳細資訊，請參閱[產品意見反應](../understand/find-help.md#product-feedback)。

如果您有想要看到之新功能的構想，也請告訴我們！ 提交新的想法，且也對其他人的想法表達支持：[Configuration Manager UserVoice](https://configurationmanager.uservoice.com)。

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> 最新版本的功能

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2005.md) <!--ID-->

以下是最新 Configuration Manager Technical Preview 版本所提供的功能：

### <a name="technical-preview-version-2005"></a>2005 技術預覽版

- [租用戶連結：系統管理中心的裝置時間軸](2020/technical-preview-2005.md#bkmk_timeline) <!--7141381-->
- [租用戶連結：從系統管理中心安裝應用程式](2020/technical-preview-2005.md#bkmk_apps) <!--6024389-->
- [租用戶連結：系統管理中心的 CMPivot](2020/technical-preview-2005.md#bkmk_cmpivot) <!--6024392-->
- [租用戶連結：從系統管理中心執行指令碼](2020/technical-preview-2005.md#bkmk_scripts) <!--6234688-->
- [VPN 界限類型](2020/technical-preview-2005.md#bkmk_vpn) <!--7020519-->
- [軟體中心的 Azure AD 驗證](2020/technical-preview-2005.md#bkmk_availapp) <!--6935376-->
- [在計量付費連線上安裝及升級用戶端](2020/technical-preview-2005.md#bkmk_meter) <!--6976145-->
- [雲端式內容的工作順序媒體支援](2020/technical-preview-2005.md#bkmk_tsmedia) <!--6209223-->
- [雲端管理閘道 Cmdlet 的改善](2020/technical-preview-2005.md#bkmk_pwshcmg) <!--6978300-->
- [社群中樞和 GitHub](2020/technical-preview-2005.md#community-hub-and-github) <!--3555935-->
- [Microsoft 365 Apps 企業版](2020/technical-preview-2005.md#bkmk_365_apps) <!--6298093-->
- [向 Microsoft 回報設定及升級失敗](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) <!--5622909-->
- [Azure AD 應用程式秘密金鑰到期通知](2020/technical-preview-2005.md#bkmk_alertkey) <!--6386392-->
- [BitLocker 工作順序步驟的改善](2020/technical-preview-2005.md#bkmk_tsbitlocker) <!--6995601-->
- [內容庫清理工具的改善](2020/technical-preview-2005.md#bkmk_content) <!--6887878-->
- [在 Windows 10 就地升級期間移除命令提示字元](2020/technical-preview-2005.md#bkmk_ipucmd) <!--2837795-->

> [!NOTE]
> 舊版 Technical Preview 中的可用功能仍會保留在較新版本中。 同樣地，已新增至 Configuration Manager 最新分支的功能仍會保留在 Technical Preview 分支中。

## <a name="features-in-recent-technical-previews"></a>最新 Technical Preview 中的功能

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

下列是自最新分支 2002 版以來，Configuration Manager Technical Preview 分支所發行過的功能：

> [!TIP]
> 當新的最新分支版本推出時，於該版本中推出的功能會列在最新的新功能文章。 如需詳細資訊，請參閱[累加版本的新功能](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)。

### <a name="technical-preview-version-2004"></a>Technical Preview 2004 版

- [Microsoft 端點管理員租用戶附加：ConfigMgr 用戶端詳細資料](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [來自 Microsoft 的通知](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [從主控台複製探索資料](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [CMPivot 的改善](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [PowerShell 第 7 版的支援](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [格式化和分割磁碟工作順序步驟的改善](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [OS 部署的管理見解規則](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [適用於工作順序部署類型的 PowerShell Cmdlet](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

### <a name="technical-preview-version-2003"></a>Technical Preview 2003 版

- [透過 Microsoft 端點管理員主控台將 Configuration Manager 用戶端上線至 Microsoft Defender ATP](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [追蹤設定項目補救](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [顯示裝置的界限群組](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [新增意見反應精靈](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Microsoft Edge 管理儀表板的改善](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [CMPivot 的改善](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [查詢傳送給 Microsoft 的意見反應](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [新增適用於工作順序進度的 SDK 方法](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [OS 部署的改善](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>舊版 Technical Preview 的功能

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

以下是透過舊版 Configuration Manager Technical Preview 分支所發行的功能。 這些功能仍會保留在更新版本中，但在最新分支中尚未提供。

| 功能        | Technical Preview 版本 |
|----------------|---------------------------|
| 將檔案附加至意見反應 <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| 啟用多點傳送網路發佈點的改善 <!--3785535--> | [Tech Preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| 階段式部署範本 <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| 使用雲端管理閘道在任何位置進行遠端控制 <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| 社群中樞改善 <!--3555935--> | [Tech Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| 社群中樞改善 <!--4224401--> | [Tech Preview 1905](2019/technical-preview-1905.md#bkmk_hub) |
| 社群中樞和 GitHub <!--3555935--> | [Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| 雲端服務費用估算 <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| 從社群中樞下載報表 <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| 社群中樞 <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| 用戶端的 PXE 回應程式服務 <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| 適用於 IPv6 的 PXE 網路開機支援 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| 使用 Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Asset Intelligence 的改進 <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>請參閱

如需詳細資訊，請參閱下列文章：

- [在實驗室中評估 Configuration Manager](evaluate-with-lab-environment.md)
- [Configuration Manager 累加版本的新功能](../plan-design/changes/whats-new-incremental-versions.md)
- [Configuration Manager 簡介](../understand/introduction.md)

> [!Tip]
> 如需目前的分支功能詳細資訊，請參閱[發行前版本功能](../servers/manage/pre-release-features.md)。
>
> 如需您必須先啟用的目前分支功能詳細資訊，請參閱[從更新啟用選擇性功能](../servers/manage/install-in-console-updates.md#bkmk_options)。
