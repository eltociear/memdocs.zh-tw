---
title: 診斷資料的使用
titleSuffix: Configuration Manager
description: 了解 Microsoft 如何使用 Configuration Manager 收集的診斷及使用方式資料。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697126"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Microsoft 如何使用 Configuration Manager 診斷及使用方式資料

適用於：  Configuration Manager (最新分支)

Configuration Manager 所收集的診斷和使用方式資料會以近乎即時的方式將產品的運作狀況提供給 Microsoft，並用來調整後續的更新。 Microsoft 也可以查看設定資料，用於設計及測試您在生產環境中使用的設定。 例如：

- 在站台伺服器使用的 Windows Server 版本

- 安裝的語言套件

- SQL 結構描述與產品預設值的差異

這份資料可協助工程小組規劃未來測試，以確保您透過最常見的設定獲得最佳體驗。 這份資料對於快速調整並配合頻繁的發行週期而言十分重要。

診斷及使用方式資料不受到運用的情形也同樣重要。 Microsoft 不會將這份資料用來︰

- 授權稽核，例如針對授權合約比對用戶端使用方式

- 稽核不支援的產品

- 根據可用資料 (例如功能使用習慣或地理位置 (時區)) 推銷廣告

Microsoft 會利用可用的資料來改善產品。 例如：

- Configuration Manager 最新分支所提供的初始支援，會限制 Windows Server 2008 R2 的支援時間表。 Microsoft 檢查了已升級至 Configuration Manager 最新分支的客戶使用方式資料。 然後，Microsoft 發現需要修改並延長此時間表，以支援仍在使用此 OS 的客戶。

- Microsoft 已改善安裝更新的必要條件檢查。 Microsoft 移除了過時的規則、說明了其他案例，並自動補救了某些問題。  

> [!div class="nextstepaction"]
> [Configuration Manager 如何收集資料](how-diagnostics-and-usage-data-is-collected.md)
