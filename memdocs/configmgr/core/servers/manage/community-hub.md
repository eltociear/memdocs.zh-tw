---
title: 社群中樞和 GitHub
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中啟用並使用社群中樞
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0ef065cce691ce6f0b251d70ea8c4bd08904071
ms.sourcegitcommit: 9a8a9cc7dcb6ca333b87e89e6b325f40864e4ad8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2020
ms.locfileid: "84740787"
---
# <a name="community-hub-and-github"></a>社群中樞和 GitHub
<!--3555935, 3555936-->

多年來，IT 系統管理員社群已經開發了豐富的知識。 我們不是從頭開始重新編寫指令碼和報告之類的項目，而是已建置一個 **Configuration Manager 社群中樞**，IT 系統管理員可以彼此共用。 藉由其他人的工作，您可以節省數小時的工作。 社群中樞透過以他人的工作為基礎進行建置，或讓其他人以您的工作為基礎進行建置來培養創意。 GitHub 已經擁有專為共用而建置的產業程序和工具。 現在，社群中樞將直接在 Configuration Manager 主控台中，利用這些工具作為推動此新社群的基本部分。 在初始版本中，社群中樞提供的內容只會由 Microsoft 上傳。 在未來，IT 系統管理員將能夠使用自己的 GitHub 帳戶來自行上傳內容。

> [!Note]  
> 「社群中樞」是選擇性的雲端式功能。 其在 2020 年 6 月首度引進。 如需如何加入「社群中樞」的詳細資訊，請參閱[選擇性功能](install-in-console-updates.md#bkmk_options)。

## <a name="about-community-hub"></a>關於社群中樞

社區中樞支援下列物件：
- PowerShell 指令碼
- 報告
- 工作順序
- 應用程式
- 設定項目  

## <a name="prerequisites"></a>先決條件

- 執行 Configuration Manager 主控台 (用於存取社群中樞) 的裝置需要下列項目：
   - .NET Framework 4.6 版或更高版本
   - Windows 10 組建 17110 或更高版本
      - 不支援 Windows Server，因此 Configuration Manager 主控台必須安裝在與站台伺服器不同的 Windows 10 裝置上。
   - 登入的使用者帳戶不可以是內建的系統管理員帳戶

- 若要下載報表，您需要在要匯入的站台上開啟選項 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]。 如需詳細資訊，請參閱[增強式 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。
   1. 移至 [系統管理] > [站台設定] > [站台]。
   1. 選取站台，然後選擇功能區中的 [屬性]。
   1. 在 [通訊安全性] 索引標籤上，選取 [對 HTTP 站台系統使用 Configuration Manager 產生的憑證] 選項。

- 如果組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，則需要允許 Configuration Manager 主控台存取網際網路端點。 如需詳細資訊，請參閱[網際網路存取需求](../../plan-design/network/internet-endpoints.md#community-hub)。

## <a name="permissions"></a>權限

- 若要匯入指令碼：適用於 **SMS_Scripts** 類別的 **Create** 權限。
- 若要匯入報表：完整的系統管理員安全性角色。


## <a name="use-the-community-hub"></a>使用社群中樞

1. 移至 [社群] 工作區中的 [社群中樞] 節點。
1. 選取要下載的項目。
1. 您需要 Configuration Manager 站台中的適當權限，才能從中樞下載物件並將它們匯入至站台。
    - 若要匯入指令碼：適用於 SMS_Scripts 類別的 **Create** 權限。
    - 若要匯入報表：完整的系統管理員安全性角色。
1. 已下載的報表將部署到報表服務點上名為 **hub** 的報表資料夾中。 可以在 [指令碼節點] 節點中看到已下載的指令碼。
1. 按一下 [社群中樞] 節點中的 [您的下載]，以檢視貴組織從中樞下載的所有項目。

[![從社群中樞下載的所有項目](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="next-steps"></a>後續步驟

深入了解如何建立及使用下列物件：

- [建立並執行 Powershell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)
- [報告簡介](introduction-to-reporting.md)
- [建立及管理工作順序](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [建立和部署應用程式](../../../apps/get-started/create-and-deploy-an-application.md)
- [建立設定項目](../../../compliance/deploy-use/create-configuration-items.md)