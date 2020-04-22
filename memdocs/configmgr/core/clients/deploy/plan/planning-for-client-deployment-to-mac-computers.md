---
title: 規劃將用戶端部署至 Mac 電腦
titleSuffix: Configuration Manager
description: 規劃在 Configuration Manager 中將用戶端部署至 Mac 電腦。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693716"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>規劃在 Configuration Manager 中將用戶端部署至 Mac 電腦

適用於：  Configuration Manager (最新分支)

您可以在執行 Mac OS X 作業系統的 Mac 電腦上安裝 Configuration Manager 用戶端，並使用下列管理功能：  

- **硬體清查**  

   您可以使用 Configuration Manager 硬體清查，在 Mac 電腦上收集有關硬體和已安裝應用程式的資訊。 接著，您可以在 Configuration Manager 主控台的資源總管中檢視此資訊，並用於建立集合、查詢和報告。 如需詳細資訊，請參閱[如何使用 [資源總管] 檢視硬體清查](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)。  

   Configuration Manager 會從 Mac 電腦收集下列硬體資訊：  

  -   處理器  

  -   電腦系統  

  -   磁碟機  

  -   磁碟分割  

  -   網路介面卡  

  -   作業系統  

  -   Service  

  -   程序  

  -   已安裝的軟體  

  -   電腦系統產品  

  -   USB 控制器  

  -   USB 裝置  

  -   CDROM 光碟機  

  -   視訊控制卡  

  -   桌上型監視器  

  -   可攜式電池  

  -   實體記憶體  

  -   印表機  

  > [!IMPORTANT]  
  >  您無法擴充在硬體清查期間從 Mac 電腦收集的硬體資訊。  

- **相容性設定**  

   您可以使用 Configuration Manager 相容性設定來檢視與補救 Mac OS X 喜好設定 (.plist) 設定的相容性。 例如，您可以在 Safari 網頁瀏覽器中強制設定首頁，或確定已啟用 Apple 防火牆。 您也可以使用殼層指令碼來監視和補救 MAC OS X 中的設定。  

- **應用程式管理**  

   Configuration Manager 可以將軟體部署至 Mac 電腦。 您可以部署下列軟體格式至 Mac 電腦：  

  -   Apple 磁碟映像檔 (.DMG)  

  -   中繼套件檔案 (.MPKG)  

  -   Mac OS X 安裝程式套件 (.PKG)  

  -   Mac OS X 應用程式 (.APP)  

  當您在 Mac 電腦上安裝 Configuration Manager 用戶端時，不能在 Windows 電腦上使用下列 Configuration Manager 用戶端支援的管理功能：  

- 用戶端推入安裝  

- 作業系統部署  

- 軟體更新  

  > [!NOTE]  
  >  您可以使用 Configuration Manager 應用程式管理功能，將必要的 Mac OS X 軟體更新部署至 Mac 電腦。 此外，您可以使用相容性設定來確定電腦已安裝所有必要的軟體更新。  

- 維護期間  

- 遠端控制  

- 電源管理  

- 用戶端狀態的用戶端檢查和補救  

  如需如何安裝和設定 Configuration Manager Mac 用戶端的詳細資訊，請參閱[如何將用戶端部署至 Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md)。
