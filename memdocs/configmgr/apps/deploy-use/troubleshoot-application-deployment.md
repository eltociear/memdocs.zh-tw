---
title: 疑難排解應用程式部署問題的提示
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 中的應用程式部署問題進行疑難排解的提示
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689966"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>疑難排解應用程式部署問題的提示

適用於：  Configuration Manager (最新分支)

應用程式部署的典型問題可分為下列其中一個類別：

- 應用程式下載失敗

- 應用程式部署相容性卡在 0%

如果您遇到上述任一問題，本文提供一些可用來進行疑難排解的步驟。 若要深入了解疑難排解，請參閱[疑難排解應用程式部署問題的技術參考](../understand/app-deployment-technical-reference.md)。


## <a name="download-failures"></a>下載失敗

應用程式下載失敗包括下列問題：

- 用戶端阻礙下載應用程式

- 用戶端無法下載應用程式內容

- 用戶端在下載應用程式時卡在 0%

發生應用程式下載失敗時，首先要檢查的是界限和界限群組是否有遺漏或其設定不正確。 比方說，如果用戶端位於內部網路，但未針對僅限網際網路用戶端管理進行設定，其網路位置必須位在設定的界限中。 還必須有指派給此界限的界限群組，以便用戶端下載內容。 如需詳細資訊，請參閱[定義站台界限與界限群組](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。

如果您無法設定用戶端的界限，或者特定界限群組不能是另一個界限群組的成員：

1. 在 Configuration Manager 主控台中，開啟 [部署類型]  的屬性。  

1. 切換至 [內容]  索引標籤。

1. 在使用鄰近界限群組或預設站台界限群組之發佈點的區段中，將 [部署選項]  變更為 [從發佈點下載內容並在本機執行]  。 (此設定預設是 [不要下載內容]  。)

如果用戶端無法下載應用程式內容，請確定該內容已發佈至發佈點。 若要確認這項設定，請使用主控台內功能來監視對發佈點的內容發佈。 如需詳細資訊，請參閱[管理已發佈的內容](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)。  


## <a name="compliance-stuck-at-0"></a>相容性卡在 0%

當應用程式的部署相容性為 0% 時，請在 [監視]  工作區中 [部署]  節點下方檢查應用程式的部署狀態。

- **進行中**：用戶端可能在[下載內容](#download-failures)時停滯

- **錯誤**：如需如何針對此問題進行疑難排解的詳細資訊，請參閱下列部落格文章：[提示和訣竅：如何對報告失敗部署的資產採取動作](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019) \(英文\)

- **未知**：這個狀態通常表示用戶端未收到原則。 請手動重新整理用戶端原則，以查看用戶端是否收到該原則。 如需詳細資訊，請參閱[起始 Configuration Manager 用戶端的原則抓取](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。
  
如果這些動作都不能解決此問題，請檢查用戶端狀態。 用戶端可能有更深層的潛在問題。 如需詳細資訊，請參閱[如何監視用戶端](../../core/clients/manage/monitor-clients.md)。


## <a name="next-steps"></a>後續步驟

- [監視應用程式](monitor-applications-from-the-console.md)
- [部署應用程式](deploy-applications.md)
- [應用程式的管理工作](management-tasks-applications.md)
- [針對應用程式部署進行疑難排解的技術參考](../understand/app-deployment-technical-reference.md)
