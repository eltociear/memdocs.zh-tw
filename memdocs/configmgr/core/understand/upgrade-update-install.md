---
title: 關於升級、更新及安裝
titleSuffix: Configuration Manager
description: 了解管理 Configuration Manager 基礎結構時，關於「安裝」、「更新」及「升級」等詞彙之間的差異。
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706716"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>關於站台及階層基礎結構的升級、更新及安裝

適用於：  Configuration Manager (最新分支)

管理 Configuration Manager 站台及階層基礎結構時，「升級」  、「更新」  及「安裝」  等詞彙是用來描述三種不同的概念。

## <a name="upgrade"></a>升級

「升級」  或「就地升級」  是將您的 Configuration Manager 2012 站台或階層轉換為執行 Configuration Manager 最新分支的站台或階層時使用。

當您將 System Center 2012 Configuration Manager 升級為 Configuration Manager 最新分支時，您會繼續使用相同的伺服器來裝載您的站台及站台伺服器，並且會保留 Configuration Manager 現有的資料及設定。  這與[移轉](../migration/migrate-data-between-hierarchies.md)不同，「移轉」是使用安裝於新硬體上新的 Configuration Manager 最新分支站台，同時保留有關受管理裝置之設定與資料的方式。

如需詳細資料，請參閱[升級至 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)。



## <a name="update"></a>更新
「更新」  是用於安裝 Configuration Manager 的主控台內更新，以及安裝無法從 Configuration Manager 主控台內傳遞的頻外更新。 主控台內更新會修改您的最新分支站台 (或 Technical Preview 站台) 的版本，使它執行更新版本。 例如，假設您的站台是執行 1806 版，您可以安裝 1810 版更新。 更新也能安裝已知問題的修正程式，而不必修改站台版本。      

通常，更新會將安全性修正程式、品質改良和新功能加入到您現有的部署。 若您使用 Technical Preview 分支，更新可能會安裝較新版本的 Technical Preview。
- 您可以選擇安裝主控台內更新的時機，從階層的頂層站台開始。
- 您可以安裝主控台內提供的任何更新。 例如，如果您的站台執行版本 1802，並同時提供 1806 和 1810，您應該考慮安裝版本 1810，因為每個版本都會包含前一個發行版本所提供的功能。
- 在新的更新於您的頂層站台完成更新後，子主要站台會自動開始更新程序。 不過，您可以設定[服務保留時間](../servers/manage/service-windows.md)來控制更新的時機。
- 次要站台不會自動安裝更新。 相反地，您必須從 Configuration Manager 主控台中手動開始更新。

如需詳細資訊，請參閱 [Configuration Manager 的更新](../servers/manage/updates.md)，和 [Configuration Manager 的 Technical Preview](../get-started/technical-preview.md)。



## <a name="install"></a>安裝
「安裝」  是用於從頭開始建立新的 Configuration Manager 階層，或是將額外站台加入到現有的階層。  

當您安裝新的主要站台或管理中心網站時，您所使用的 setup.exe 以及與其相關聯的來源檔案位置取決於您的安裝案例。

如需詳細資訊，請參閱[準備安裝站台](../servers/deploy/install/prepare-to-install-sites.md)。
