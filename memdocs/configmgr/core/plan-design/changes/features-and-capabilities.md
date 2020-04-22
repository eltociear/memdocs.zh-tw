---
title: 特色與功能
titleSuffix: Configuration Manager
description: 深入了解 Configuration Manager 的主要管理功能。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706396"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Configuration Manager 的功能

適用於：  Configuration Manager (最新分支)

本文摘要說明 Configuration Manager 的主要管理功能。 每一項功能都有自己的必要條件，且您使用每一項功能的方式可能會影響 Configuration Manager 階層的設計和實作。 例如，如果想要將軟體更新部署到階層中的裝置，則需要軟體更新點站台系統角色。  

如需如何規劃和安裝 Configuration Manager 以便在環境中支援這些管理功能的詳細資訊，請參閱[準備開始使用 Configuration Manager](../get-ready.md)。  

## <a name="co-management"></a>共同管理

共同管理是將您現有的 Configuration Manager 部署附加至 Microsoft 365 雲端其中一種主要方式。 它可讓您使用 Configuration Manager 和 Microsoft Intune 同時管理多部 Windows 10 裝置。 共同管理可讓您透過新增功能 (例如條件式存取)，在雲端附加您在 Configuration Manager 方面現有的投資。 如需詳細資訊，請參閱[什麼是共同管理](../../../comanage/overview.md)。

## <a name="desktop-analytics"></a>電腦分析

電腦分析是與 Configuration Manager 整合的雲端式服務。 這項服務可提供您見解與智慧，有助您針對自己的 Windows 用戶端更新整備做出更旁徵博引的決定。 其結合了您組織的資料，以及從連線到 Microsoft 雲端服務之數百萬部裝置彙總而成的資料。 如需詳細資訊，請參閱[什麼是電腦分析](../../../desktop-analytics/overview.md)。

## <a name="cloud-attached-management"></a>雲端連結管理

使用雲端管理閘道、雲端式發佈點與 Azure Active Directory 等功能來管理以網際網路為基礎的用戶端。

如需詳細資訊，請參閱下列文章：

- [管理網際網路上的用戶端](../../clients/manage/manage-clients-internet.md)
- [規劃 Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>即時管理

使用 CMPivot 來立即查詢線上裝置，然後篩選並分組資料以取得更深入的見解。 此外，使用 Configuration Manager 主控台來管理 Windows PowerShell 指令碼並將其部署到用戶端。 如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md) 和[建立並執行 PowerShell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)。

## <a name="application-management"></a>應用程式管理

協助建立、管理、部署及監視您所管理一系列不同裝置中的應用程式。 從 Configuration Manager 主控台部署、更新及管理 Office 365。 此外，Configuration Manager 會與商務與教育用 Microsoft Store 整合，以提供雲端式應用程式。 如需詳細資訊，請參閱[應用程式管理簡介](../../../apps/understand/introduction-to-application-management.md)。

## <a name="os-deployment"></a>OS 部署

部署 Windows 10 的就地升級，或是擷取並部署 OS 映像。 映像部署可以使用 PXE、多點傳送或可開機媒體。 也可協助使用 Windows AutoPilot 重新部署現有的裝置。 如需詳細資訊，請參閱 [OS 部署簡介](../../../osd/understand/introduction-to-operating-system-deployment.md)。  

## <a name="software-updates"></a>軟體更新

管理、部署及監視組織中的軟體更新。 與 Windows 傳遞最佳化和其他對等快取技術整合，以協助控制網路使用量。 如需詳細資訊，請參閱[軟體更新簡介](../../../sum/understand/software-updates-introduction.md)。  

## <a name="company-resource-access"></a>公司資源存取

讓您授權組織中的使用者從遠端位置存取資料和應用程式。 這項功能包括 Wi-Fi、VPN、電子郵件和憑證設定檔。 如需詳細資訊，請參閱[保護資料和站台基礎結構](../../../protect/understand/protect-data-and-site-infrastructure.md)。

## <a name="compliance-settings"></a>相容性設定

協助您評定、追蹤及補救組織中用戶端裝置的設定合規性。 此外，您可以使用合規性設定來設定一系列您所管理裝置上的功能和安全性設定。 如需詳細資訊，請參閱[確保裝置合規性](../../../compliance/understand/ensure-device-compliance.md)。  

## <a name="endpoint-protection"></a>Endpoint Protection

為組織中的電腦提供安全性、反惡意程式碼及 Windows 防火牆管理。 此區域包括使用下列 Windows Defender 套件功能進行管理及整合：

- Windows Defender 防毒軟體
- Microsoft Defender 進階威脅防護
- Windows Defender 惡意探索防護
- Windows Defender 應用程式防護
- Windows Defender 應用程式控制
- Windows Defender 防火牆

如需詳細資訊，請參閱 [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

## <a name="inventory"></a>清查

協助識別及監視資產。

### <a name="hardware-inventory"></a>硬體清查

收集組織中裝置硬體的詳細資訊。 如需詳細資訊，請參閱[硬體清查簡介](../../clients/manage/inventory/introduction-to-hardware-inventory.md)。  

### <a name="software-inventory"></a>軟體清查

收集和報告組織中用戶端電腦上所儲存檔案的資訊。 如需詳細資訊，請參閱[軟體清查簡介](../../clients/manage/inventory/introduction-to-software-inventory.md)。  

### <a name="asset-intelligence"></a>Asset Intelligence

提供收集組織中清查資料及監視軟體授權使用情形的工具。 如需詳細資訊，請參閱 [Asset Intelligence 簡介](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

## <a name="on-premises-mobile-device-management"></a>內部部署行動裝置管理

使用內部部署 Configuration Manager 基礎結構和裝置平台內建的管理功能來註冊及管理裝置。 (一般管理會使用個別安裝的 Configuration Manager 用戶端)。這項功能目前支援管理 Windows 10 企業版和 Windows 10 行動裝置版裝置。 如需詳細資訊，請參閱[使用內部部署基礎結構來管理行動裝置](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

## <a name="power-management"></a>電源管理

管理及監視組織中用戶端電腦的耗電量。 設定電源計劃，並使用網路喚醒功能在上班時間以外進行維護。 如需詳細資訊，請參閱[電源管理簡介](../../clients/manage/power/introduction-to-power-management.md)。  

## <a name="remote-control"></a>遠端控制

提供從 Configuration Manager 主控台遠端管理用戶端電腦的工具。 如需詳細資訊，請參閱[遠端控制簡介](../../clients/manage/remote-control/introduction-to-remote-control.md)。  

## <a name="reporting"></a>報告

從 Configuration Manager 主控台使用 SQL Server Reporting Services 的進階報告功能。 這項功能提供數百種預設報告。 如需詳細資訊，請參閱[報告簡介](../../servers/manage/introduction-to-reporting.md)。  

## <a name="software-metering"></a>軟體計量

從 Configuration Manager 用戶端監視及收集軟體使用方式資料。 您可以使用此資料來判斷是否要在安裝軟體之後使用該軟體。 如需詳細資訊，請參閱[使用軟體計量監視應用程式使用量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  
