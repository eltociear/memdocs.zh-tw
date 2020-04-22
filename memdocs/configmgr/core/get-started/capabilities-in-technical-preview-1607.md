---
title: Technical Preview 1607 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1607 版中可用的功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 7ec5802a8931bc4397eaf302920f09d8597802fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705556"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Configuration Manager Technical Preview 1607 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1607 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>改進 Windows 10 版本升級原則

在此版本中，已對此原則做了下列改進：

* 除了向 Microsoft Intune 註冊的 Windows 10 電腦之外，您現在還可以對執行 Configuration Manager 用戶端的 Windows 10 電腦使用版本升級原則。
* 您可以在精靈中，從 Windows 10 專業版升級到與您的硬體相容的任何平台。

[深入了解 Windows 10 版本升級原則](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>試試看！

1. 使用[現有版本升級原則主題](../../compliance/deploy-use/upgrade-windows-version.md)中的資訊來建立版本升級原則。
2. 將此原則部署到執行 Configuration Manager 用戶端的 Windows 10 電腦。
一旦原則達到目標的 Windows 電腦，電腦便會在兩個小時內重新啟動，套用升級。 您目前無法抑制此重新啟動。 確定通知任何您要部署原則的使用者，或排程在非使用者工作時間執行原則。

### <a name="known-issue-with-this-release"></a>此版本的已知問題
在 Configuration Manager 用戶端設定中，您可能會看到 [版本升級]  的設定。 在此版本中，這些設定沒有作用。 請使用上面提供的指示，將 Windows 10 升級到更新的版本。

## <a name="customizable-branding-for-software-center-dialogs"></a>可自訂軟體中心對話方塊的商標

Configuration Manager 1602 版中引進了軟體中心的自訂商標。 在 Technical Preview 1607 版中，該商標現在已擴充到所有相關的對話方塊和工作列通知，以提供軟體中心使用者更一致的體驗。

### <a name="try-it-out"></a>試試看！

軟體中心的自訂商標會根據下列規則套用：

1. 如果未安裝「應用程式類別目錄網站點」站台伺服器角色，則軟體中心將會顯示 [電腦代理程式]  用戶端設定之 [顯示在軟體中心的組織名稱]  中指定的組織名稱。 如需相關指示，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。

2. 如果未安裝「應用程式類別目錄網站點」站台伺服器角色，則「軟體中心」將會顯示「應用程式類別目錄網站點」站台伺服器角色內容中指定的組織名稱和色彩。 如需詳細資訊，請參閱[應用程式類別目錄網站點的設定選項](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)。

3. 如果已設定 Microsoft Intune 訂閱並連線到 Configuration Manager 環境，則軟體中心將會顯示 Intune 訂閱內容中指定的組織名稱、色彩及公司標誌。

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>針對多個 PXE 起始的部署使用相同的網路介面卡
在 Technical Preview 1607 版中，當您使用乙太網路介面卡製作多部裝置的映像時 (例如您在多部裝置上使用的 USB 乙太網路介面卡)，您可以啟用新的設定，以便輸入乙太網路介面卡的硬體識別碼。 執行 PXE 安裝和註冊用戶端時，Configuration Manager 會略過清單中的硬體識別碼。

如需此問題的詳細資訊，請參閱 [Configuration Manager OSD 支援小組部落格](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/)。  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>啟用此功能以管理重複的硬體識別碼  
1. 在 Configuration Manager 主控台中，移至 [管理]   > [概觀]   > [雲端服務]   > [更新與服務]   > [功能]  。
2. 在顯示窗格中，選取 [管理重複硬體識別碼]  。
3. 在 [常用]  索引標籤的 [功能]  群組中，按一下 [開啟]  。

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>新增 Configuration Manager 要略過的硬體識別碼  
1. 在 Configuration Manager 主控台中，移至 [管理]   > [概觀]   > [站台設定]   > [站台]  。
2. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [階層設定]  。
3. 移至 [用戶端核准和衝突的記錄]  索引標籤。
4. 在 [重複硬體識別碼]  區段中，按一下 [新增]  以新增硬體識別碼。
