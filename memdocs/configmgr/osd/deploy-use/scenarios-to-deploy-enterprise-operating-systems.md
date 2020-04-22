---
title: 部署企業作業系統的案例
titleSuffix: Configuration Manager
description: 了解使用 Configuration Manager 部署企業作業系統的多種案例。
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708386"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>使用 Configuration Manager 部署企業作業系統的案例

適用於：  Configuration Manager (最新分支)

Configuration Manager 提供下列 OS 部署案例：  

#### <a name="upgrade-windows-to-the-latest-version"></a>升級至最新版本的 Windows
此案例會升級目前執行 Windows 7、Windows 8.1 或 Windows 10 之電腦上的 OS。 升級程序會保留電腦上的應用程式、設定和使用者資料。 其沒有任何外部相依性，例如 Windows ADK。 此程序可能比傳統 OS 部署更快且更有彈性。  

如需詳細資訊，請參閱[將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)。


#### <a name="windows-autopilot-for-existing-devices"></a>適用於現有裝置的 Windows Autopilot
<!--3607717, fka 1358333-->
從 1810 版開始，將可針對搭配 Windows 10 1809 版或更新版本的現有裝置使用 Windows Autopilot。 此功能可讓您使用單一 Configuration Manager 工作順序，針對 Windows Autopilot 使用者驅動模式對 Windows 7 裝置重新安裝映像並進行佈建。

如需詳細資訊，請參閱[適用於現有裝置的 Windows Autopilot](windows-autopilot-for-existing-devices.md)。


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>使用新的 Windows 版本重新整理現有的電腦
此案例會分割並格式化 (抹除) 現有的電腦，並在該電腦上安裝新的 OS。 您可以在安裝 OS 後移轉設定和使用者資料。  

如需詳細資訊，請參閱[使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)。


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>在新電腦 (裸機) 上安裝新的 Windows 版本
此案例會在新電腦上安裝 OS。 這是全新的 OS 安裝，且不包含任何設定或使用者資料移轉。  

如需詳細資訊，請參閱[在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)。


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>取代現有的電腦和傳輸設定
此案例會在新電腦上安裝 OS。 您也可以將舊電腦的設定和使用者資料移轉至新電腦。  

如需詳細資訊，請參閱[取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)。


