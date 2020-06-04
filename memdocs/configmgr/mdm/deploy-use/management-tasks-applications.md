---
title: 管理內部部署 MDM 的應用程式
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中管理內部部署行動裝置管理（MDM）的應用程式。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9fafcc4b5462afb1b8e528837ea6ba61203e73d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347132"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中管理內部部署 MDM 的應用程式

適用於：  Configuration Manager (最新分支)

當您使用 Configuration Manager 內部部署行動裝置管理（MDM）來管理裝置時，您可以管理下列應用程式類型：

- Windows Phone 應用程式套件 (*.xap 檔案)
- Windows Phone 應用程式套件 (在 Windows Phone 市集中)
- 透過 MDM 的 Windows Installer
- Web 應用程式

如需有關管理 Configuration Manager 應用程式和部署類型的一般資訊，請參閱[Configuration Manager 應用程式的管理](../../apps/deploy-use/management-tasks-applications.md)工作。

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>建立 Windows Phone 應用程式

Configuration Manager 應用程式有一或多種部署類型。 部署類型包含將軟體部署到裝置所需的安裝檔案和資訊。 部署類型也包含指定部署軟體之時間和方法的規則。

如需建立應用程式和部署類型的一般步驟，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md#bkmk_create)。

Configuration Manager 支援下列適用于 Windows mobile 裝置的應用程式檔案類型：

|裝置類型|支援的檔案類型|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap、appx、appxbundle|
|Windows 10 Mobile|xap、appx、appxbundle|

將 Windows Phone 應用程式部署為 [可用]**** 或 [必要]****。 解除安裝應用程式時也請使用部署。

## <a name="deploy-and-monitor-apps"></a>部署和監視應用程式

在 Configuration Manager 中部署和監視行動裝置的應用程式，就像您針對其他裝置（例如桌上型電腦和伺服器）所做的一樣。 如需詳細資訊，請參閱下列文章：

- [部署應用程式](../../apps/deploy-use/deploy-applications.md)
- [監視應用程式](../../apps/deploy-use/monitor-applications-from-the-console.md)

請參閱下列行動裝置特有的限制：

- 已註冊 MDM 的裝置不支援模擬部署、使用者體驗或排程設定。

- 請不要在單一應用程式中新增超過100的地區設定。 此動作可防止在裝置上安裝應用程式。

## <a name="next-step"></a>後續步驟

若要進行變更、卸載，或將已部署的應用程式取代為新的應用程式，請使用 Configuration Manager 中的任何應用程式來進行管理。 如需詳細資訊，請參閱[修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)。
