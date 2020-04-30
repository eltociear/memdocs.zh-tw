---
title: 為裝置安裝應用程式
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 立即將應用程式安裝至不具有集合的裝置。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689446"
---
# <a name="install-applications-for-a-device"></a>為裝置安裝應用程式

<!--4402180-->

從 1906 版開始，您可以從 Configuration Manager 主控台將應用程式即時安裝到裝置。 這項功能可協助減少為每個應用程式區分集合的需求。

## <a name="prerequisites"></a>先決條件

- 啟用 [依據裝置為使用者核准應用程式要求]  [選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。  

- [部署應用程式](deploy-applications.md)為「可用於」  裝置集合。  

    - 在部署精靈的 [部署設定]  頁面上，選取下列選項：**系統管理員必須在裝置上核准此應用程式要求**。  

        > [!Note]  
        > 使用這些部署設定時，不會將任何原則傳送至用戶端。 應用程式不會在軟體中心顯示為可用，且使用者無法使用此部署來安裝應用程式。 在您使用此動作安裝應用程式後，使用者可執行它，並在軟體中心內看到它的安裝狀態。

- 您的使用者帳戶需要下列權限：

    - **應用程式**：讀取、核准

    - **集合**：讀取、讀取資源、修改資源、檢視收集的檔案

    例如，**應用程式系統管理員**內建角色具有這些權限。

> [!TIP]
> 在階層中，等候應用程式和部署資訊複寫至目標用戶端指派到的主要站台。<!-- SCCMDocs#2113 -->

## <a name="process"></a>程序

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [裝置]  節點。 選取目標裝置，然後在功能區中選取 [安裝應用程式]  動作。

1. 從清單選取一或多個應用程式。 此清單只會顯示您已使用必要設定來部署的應用程式。

此動作會在裝置上觸發所選取預先部署應用程式的安裝流程。

若要查看核准要求的狀態，請在 [軟體程式庫]  工作區中，展開 [應用程式管理]  ，然後選取 [應用程式要求]  節點。

使用與在 [監視]  工作區中 [部署]  節點內相同的方式，監視應用程式的安裝。


## <a name="see-also"></a>請參閱

[核准應用程式](app-approval.md)
