---
title: CD.Latest 資料夾
titleSuffix: Configuration Manager
description: 了解從 Configuration Manager 主控台內將更新傳遞到產品的程序。
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704046"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Configuration Manager 的 [CD.Latest] 資料夾

適用於：  Configuration Manager (最新分支)

Configuration Manager 有程序可從 Configuration Manager 主控台內將更新傳遞到產品。 若要支援更新 Configuration Manager 的這個新方法，需要建立名為 **CD.Latest** 的資料夾。 此資料夾包含您站台之更新版本的 Configuration Manager 安裝檔案複本。  

[CD.Latest] 資料夾包含名為 **Redist** 的資料夾，其中包含安裝程式所下載及使用的可轉散發檔案。 這些檔案會與該 CD.Latest 資料夾中找到的 Configuration Manager 檔案版本相符。 當您從 CD.Latest 資料夾執行安裝程式時，必須使用與該版本安裝程式相符的檔案。 若要執行此操作，您可以指示安裝程式從 Microsoft 下載最新的檔案，或指示安裝程式使用來自 [CD.Latest] 資料夾隨附之 [Redist] 資料夾中的檔案。

基準媒體不包含 [Redist]  資料夾。 在您安裝主控台內更新之前，站台不會建立 [Redist] 資料夾。 同時，使用您從基準媒體安裝站台時所使用的 Redist 資料夾。  

> [!TIP]  
> 請確定您使用的可轉散發檔案是最新的。 如果您最近沒有下載可轉散發檔案，請進行規劃讓安裝程式從 Microsoft 下載。   

下列案例會在管理中心網站或主要站台伺服器上建立或更新 [CD.Latest] 資料夾：  

- 當您從 Configuration Manager 主控台內安裝更新或 Hotfix 時，站台會在 Configuration Manager 安裝資料夾中建立或更新該資料夾。  

- 當您執行內建的 Configuration Manager 備份工作時，站台會在指定的備份資料夾位置底下建立或更新該資料夾。  

- 當您使用基準媒體安裝新的站台時，站台會建立 [CD.Latest] 資料夾。


## <a name="supported-scenarios"></a>支援的案例

下列案例支援使用來自 [CD.Latest] 資料夾的來源檔案：  

### <a name="backup-and-recovery"></a>備份與復原
若要復原站台，請使用符合您站台之 [CD.Latest] 資料夾中的來源檔案。 當您使用內建站台備份工作執行站台備份時，CD.Latest 資料夾會包含為備份的一部分。

- 當您在站台復原過程中重新安裝站台時，您是透過備份中包含的 [CD.Latest] 資料夾來安裝站台。 此動作會使用與您站台備份和站台資料庫相符的檔案版本來安裝站台。  

    - 如果您無法存取正確版本的 [CD.Latest] 資料夾，請藉由在實驗室環境中安裝站台來取得包含正確檔案版本的 [CD.Latest] 資料夾。 然後將站台更新為符合您要復原的版本。  

    - 如果您無法取得正確的 [CD.Latest] 資料夾和其內容，您就無法復原站台。 在此情況下，您需要重新安裝站台。  

- 當您沒有 [CD.Latest] 資料夾但有正常運作的子主要站台或管理中心網站時，您可以使用該站台作為進行站台復原的參照站台。  

### <a name="install-a-child-primary-site"></a>安裝子主要站台
當您要在已安裝一或多個主控台內更新的管理中心網站底下安裝新的子主要站台，請使用安裝程式及來自管理中心網站 [CD.Latest] 資料夾的來源檔案。 此程序會使用與管理中心網站版本相符的安裝來源檔案。 如需詳細資訊，請參閱[使用安裝精靈安裝站台](../deploy/install/use-the-setup-wizard-to-install-sites.md)。  

### <a name="expand-a-stand-alone-primary-site"></a>擴充獨立主要站台
當您藉由安裝新的管理中心網站來擴充獨立主要站台時，請使用來自主要站台 [CD.Latest] 資料夾的安裝程式和來源檔案。 此程序會使用符合主要站台版本的安裝來源檔案。 如需詳細資訊，請參閱[擴充獨立主要站台](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)。

### <a name="install-a-secondary-site"></a>安裝次要站台
<!-- SCCMDocs-pr issue #3164 -->
當您要在已安裝一或多個主控台內更新的主要站台下安裝新的次要站台時，請使用來自主要站台 [CD.Latest] 資料夾的來源檔案。 

如需詳細資訊，請參閱[安裝次要站台](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)。 


## <a name="unsupported-scenarios"></a>不支援的案例

不支援使用已更新的 CD.Latest 來源檔案進行下列作業：  

- 為新階層安裝新站台  
- 將 Microsoft System Center 2012 Configuration Manager 站台升級至 Configuration Manager 最新分支
- 安裝 Configuration Manager 用戶端
- 安裝 Configuration Manager 主控台
