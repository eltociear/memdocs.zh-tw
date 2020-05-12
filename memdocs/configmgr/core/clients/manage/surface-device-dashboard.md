---
title: Surface 裝置儀表板
titleSuffix: Configuration Manager
description: 使用儀表板檢閱 Surface 裝置的相關資訊。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: f9b9c49bde16754b7a60112905f14da2cd5e48eb
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906284"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Configuration Manager 中的 Surface 裝置儀表板

適用於：  Configuration Manager (最新分支)

從 1802 版開始，Surface 裝置儀表板能夠一覽無遺地提供在您的環境中所找到的 Surface 裝置的相關資訊。 <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>開啟 Surface 裝置儀表板

若要開啟 Surface 裝置儀表板，請使用下列步驟： 

1. 開啟 Configuration Manager 主控台。 
2. 按一下 [監視]  節點。 
3. 若要載入儀表板，請按一下 [Surface 裝置]  。

**Surface 裝置儀表板**
![Surface 裝置儀表板](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>檢閱 Surface 裝置儀表板中的資訊

Surface 裝置儀表板會針對您的環境顯示三個圖形。 

- **Surface 裝置的百分比** - 提供您 Surface 裝置在整個環境中的百分比。

    ![Surface 裝置百分比圖形](media/Percent-Surface-Devices.PNG)
- **Surface 型號** - 顯示 Surface 型號的裝置數目。 
  - 將滑鼠游標移到圖表區段上方可提供您 Surface 裝置屬於所選取型號的百分比。 

       ![Surface 型號圖形](media/Surface-Models-Hover.PNG)
  - 按一下圖形區段會帶您前往該型號的裝置清單。 
      ![Surface 型號裝置清單](media/Surface-Model-Device-List.PNG)

- **前五個韌體版本** - 顯示您的環境中前五個韌體型號的圖表。 
  - 將滑鼠游標移到圖表區段上方可提供您 Surface 裝置屬於所選取韌體版本的數目。 從 Configuration Manager 1806 版開始，按一下圖表區段會顯示相關裝置的清單。 <!--1358654-->
     ![Surface 型號裝置清單](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>更多資訊

如需 Surface 裝置的詳細資訊，請參閱 [Surface](https://www.microsoft.com/surface) 網站。

如需在 Configuration Manager 中部署 Surface 韌體更新的詳細資訊，請參閱[如何管理 Surface 驅動程式更新](https://support.microsoft.com/help/4098906) (機器翻譯)。




