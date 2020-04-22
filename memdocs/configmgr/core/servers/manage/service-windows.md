---
title: 服務保留時間
titleSuffix: Configuration Manager
description: 您可以使用服務時間來控制 Configuration Manager 站台安裝更新的時間。
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702046"
---
#  <a name="service-windows-for-site-servers"></a>站台伺服器的服務保留時間

適用於：  Configuration Manager (最新分支)

您可以在管理中心網站和主要站台設定服務保留時間，來控制可安裝主控台內更新的時機。  您可以設定多個保留時間，包含由該站台伺服器所有保留時間的組合決定可安裝更新的保留時間。

當未設定服務保留時間時：
- **在頂層站台上** (系統管理中心網站或獨立主要站台) 您可以選擇要開始更新安裝的時間。
- **在子主要站台上**，更新會在管理中心網站完成安裝更新後自動安裝。
- **在次要站台上**，永遠不會自動開始更新。 相反地，您必須在父主要站台安裝更新之後，從主控台內開始手動更新安裝。

當已設定服務保留時間時：
- **在頂層站台上**，您將無法從 Configuration Manager 主控台內開始任何新的更新安裝。 只要先設定服務保留時間，站台就會自動下載更新以備安裝。  
- **在子主要站台上**，已安裝於管理中心網站的更新會下載至主要站台，但不會自動開始。 您無法在使用服務保留時間封鎖的時間期間手動開始安裝更新。 當服務保留時間不再封鎖安裝更新時，就會自動開始安裝更新。
- **次要站台**不支援服務保留時間，也不會自動安裝更新。 在次要站台的主要父站台安裝更新後，您可以從主控台內開始次要站台的更新。

## <a name="to-configure-a-service-window"></a>設定服務保留時間

1.  在 Configuration Manager 主控台中，依序開啟 [系統管理]   > [站台設定]   > [站台]  ，然後選取要設定維護時段的站台伺服器。  

2.  接著，編輯站台伺服器的 **[內容]** ，然後選取 **[維護時段]** 索引標籤，您可在此為該站台伺服器設定一或多個維護時段。  
