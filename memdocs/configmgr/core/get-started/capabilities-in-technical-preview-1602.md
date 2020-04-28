---
title: Technical Preview 1602 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1602 版中可用的功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 64d01598f3d5feb162898761645ac84b1c73b175
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074464"
---
# <a name="capabilities-in-technical-preview-1602-for-configuration-manager"></a>Configuration Manager Technical Preview 1602 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

本文介紹 Configuration Manager Technical Preview 1602 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

 以下是您可以使用此版本試用的新功能。  

##  <a name="improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a> 行動裝置管理的增強功能  

### <a name="ios-activation-lock"></a>iOS 啟用鎖定  
 Configuration Manager 可以協助您管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 當裝置上使用「尋找我的 iPhone」應用程式時，啟用鎖定會自動啟用。 啟用之後，就必須輸入使用者的 Apple ID 和密碼，才能夠讓所有人：  

- 關閉「尋找我的 iPhone」  

- 清除裝置  

- 重新啟動裝置  

  Configuration Manager 可以要求執行 iOS 7.1 和更新版本之受監督和不受監督裝置的啟用鎖定狀態。 針對受監督的裝置，Intune 可以擷取啟用鎖定略過碼並直接發給裝置。  

##  <a name="improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a> 1602 版本中對軟體中心的改進  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>從軟體中心重新整理 PC 電腦和使用者原則  
 新的 [同步原則]  選項已新增至軟體中心的 [選項]   > [電腦維護]  頁面，可讓電腦重新整理其 Configuration Manager 電腦和使用者原則。  

##  <a name="improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a> Windows 10 服務的增強功能  
 在 1602 Technical Preview 中，我們新增了下列 Windows 10 服務增強功能：  

-   新的服務方案篩選選項。  您現在可以篩選 [語言]  、[必要]  和 [標題]  。 只有符合指定準則的升級會新增至相關聯的部署。  

-   當您選取 [升級]  分類進行軟體更新同步處理時，將出現警告對話方塊，讓您知道需要 WSUS [Hotfix 3095113](https://support.microsoft.com/kb/3095113) 才能順利同步處理軟體更新，且 Windows 10 服務才能正常運作。  在對話方塊中，您可以移至 Hotfix 的知識庫文章。  

-   可用的 Windows 10 升級現在只顯示於 Configuration Manager 主控台的 [Windows 10 服務]   \ [所有 Windows 10 更新]  節點。 這些更新不會再顯示於 [軟體更新]   \ [所有軟體更新]  節點。  

-   系統將以對話方塊提示啟動 Windows 10 升級套件的使用者，讓他們知道其將升級作業系統。  
