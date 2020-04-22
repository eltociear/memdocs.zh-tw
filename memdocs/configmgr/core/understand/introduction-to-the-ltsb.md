---
title: 長期維護分支 (LTSB) 簡介
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 的長期維護分支。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eda58982094860ccf075bcd2d1d8ed9e3d3bb2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706916"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Configuration Manager 的長期維護分支簡介

適用於：System Center Configuration Manager (長期維護分支) 

Configuration Manager 的長期維護分支 (LTSB) 是較為特別的分支，它是設計成適用於所有客戶的安裝選項。 不過，針對其 Configuration Manager 的軟體保證 (SA) 或同等訂閱權限到期的客戶，這是唯一選項。

針對以 Configuration Manager 1606 版為基礎的分支而言，相較於 Configuration Manager 的最新分支，LTSB 的功能較少。

> [!TIP]   
> Configuration Manager LTSB 與 System Center 套件的長期維護通道 (LTSC) 沒有任何關聯。 如需詳細資訊，請參閱 [System Center 版本選項概觀](https://docs.microsoft.com/system-center/ltsc-and-sac-overview) \(英文\)。

## <a name="features-that-arent-available"></a>無法使用的功能

Configuration Manager 的最新分支支援下列使用 LTSB 時無法使用的功能：

- 新增功能和改進的主控台內更新。
- 支援使用新推出的作業系統做為站台伺服器和用戶端。
- 內部部署 MDM
- Windows 10 服務儀表板和服務計畫，包含對 Windows 10 最新版本的支援。  
- 支援未來的 Windows Server 和 Windows 10 LTSB 版本
- Asset Intelligence
- 雲端式發佈點
- 使用 Exchange Online 做為 Exchange Connector    

雖然使用 LTSB 無法取得這些功能的支援，但 Configuration Manager 主控台仍會顯示部分功能，只是無法選取或使用。

LTSB 不提供雲端整合，以及 Configuration Manager 最新分支 1610 版或更新版本隨附的任何功能。 這些功能包括 (但不限於) 以下幾項：<!--SCCMDocs#1823-->

- 共同管理
- 電腦分析
- 雲端管理閘道
- Azure Active Directory 整合
- 從商務用 Microsoft Store 購買的應用程式

## <a name="find-ltsb-documentation"></a>尋找 LTSB 的文件

LTSB 是以最新分支 1606 版為基礎。 請使用[最新分支文件](https://docs.microsoft.com/sccm/)，其中有 LTSB 特定的注意事項與限制。 那些注意事項與限制可在下列文章中找到：

- [安裝 LTSB](install-the-ltsb.md)
- [將 LTSB 升級至最新分支](convert-to-current-branch.md)
- [LTSB 支援的設定](supported-configurations-for-ltsb.md)
- [管理 Configuration Manager 的 LTSB](manage-the-ltsb.md)

當您針對 LTSB 參考最新分支文件時，適用於 1606 版或更早版本的詳細資料也會適用於 LTSB。 LTSB 不支援 1610 版或更新版本中推出的功能或詳細資料。

## <a name="licensing-overview-for-the-ltsb"></a>LTSB 授權概觀   

如果客戶具有 Configuration Manager 授權的作用中軟體保證 (SA) 或自 2016 年 10 月 1 日起的對等訂閱權限，即有權使用 2016 年 10 月發行的 Configuration Manager 1606 版。 如果客戶具有自 2016 年 10 月 1 日起的 Configuration Manager 權限，則在安裝時會發現最新分支和長期維護分支 (LTSB) 這兩個授權選項。

如果客戶擁有 System Center Configuration Manager 的永久權限 ，或可接受 SA 或訂閱於 10 月 1 日之後失效，則可在失效當下安裝 System Center Configuration Manager LTSB 版。

如需這些授權的詳細資訊，請參閱[透過 Microsoft 大量授權方案購買之產品的完整條款及條件](https://go.microsoft.com/fwlink/?LinkId=800052) \(英文\)。

如需 Configuration Manager 分支的授權詳細資訊，請參閱 [Configuration Manager 授權與分支](learn-more-editions.md)。

## <a name="next-steps"></a>後續步驟

如果您認為 Configuration Manager LTSB 是適合您環境的正確分支，請[安裝新的 LTSB](install-the-ltsb.md#install-a-new-site) 站台做為新階層的一部分，或[升級 System Center 2012 Configuration Manager 站台](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager)和階層。
