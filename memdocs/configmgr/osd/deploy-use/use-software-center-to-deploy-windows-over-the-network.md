---
title: 使用軟體中心透過網路部署 Windows
titleSuffix: Configuration Manager
description: 您可以將作業系統部署至 Software Center，以使用新版本的 Windows 重新整理現有電腦，或將 Windows 升級至最新版本。
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709026"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>使用 Configuration Manager 透過網路使用軟體中心部署 Windows

適用於：  Configuration Manager (最新分支)

您可以在軟體中心中提供會在 Configuration Manager 中安裝作業系統的工作順序。 您可以透過下列作業系統部署案例將作業系統部署到軟體中心：

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)

完成其中一個作業系統部署案例的步驟。 然後使用以下各節的內容來針對於軟體中心提供的部署進行準備。

## <a name="configure-deployment-settings"></a>設定部署設定  
請設定部署來使作業系統部署可在軟體中心取得。 您可以在 [部署軟體精靈] 的 [部署設定]  頁面上，或是在部署內容的 [部署設定]  索引標籤上設定部署。 如果是 [供下列項目使用]  設定，請設定 [只有 Configuration Manager 用戶端]  或是 [Configuration Manager 用戶端、媒體與 PXE]  。 當系統部署作業系統之後，目標集合的成員就可以在軟體中心中看到該作業系統。

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> 將工作順序部署到電腦  
將作業系統部署至目標集合。 如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md)。 當您針對軟體中心部署作業系統時，可以將該部署設定為必要或可用的部署。

-   **必要的部署**：必要的部署會在軟體中心內提供作業系統，而且會依設定的指派排程自動啟動。

-   **可用的部署**：軟體中心內會提供作業系統，使用者可於需要時安裝該作業系統。
