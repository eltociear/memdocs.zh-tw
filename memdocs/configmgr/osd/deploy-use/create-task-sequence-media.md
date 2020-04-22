---
title: 建立工作順序媒體
titleSuffix: Configuration Manager
description: 建立工作順序媒體將 OS 部署至 Configuration Manager 環境中的目的地電腦。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690596"
---
# <a name="create-task-sequence-media"></a>建立工作順序媒體

適用於：  Configuration Manager (最新分支)

您可以使用媒體從參照電腦擷取 OS 映像，也可以將 OS 部署至 Configuration Manager 環境中的目的地電腦。 您所建立的媒體可以是 CD、DVD 組或 USB 快閃磁碟機。  

如果目的地電腦沒有網路連線或與 Configuration Manager 站台的連線頻寬不足，則大部分會使用媒體在其上部署作業系統。 不過，您也可以使用媒體在現有的 Windows OS 以外啟動 OS 部署。 當沒有任何現有的 OS、OS 無法運作，或者您想要重新分割硬碟時，這個方法會很有用。  

部署媒體包括可開機媒體、獨立媒體，以及預先設置的媒體。 媒體的內容會依所使用的媒體類型而有所不同。 例如，獨立媒體包含部署 OS 的工作順序。 其他類型的媒體從管理點擷取工作順序。  

> [!IMPORTANT]  
> 若要建立工作順序媒體，您必須為執行 Configuration Manager 主控台之電腦上的系統管理員。 如果您不是系統管理員，當您啟動「建立工作順序媒體」精靈時，系統將會提示您輸入系統管理員認證。  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> 擷取媒體

擷取媒體可用於從參照電腦擷取 OS 映像。 擷取媒體包含啟動參照電腦的開機映像，以及擷取 OS 映像的工作順序。

如需有關如何建立擷取媒體的詳細資訊，請參閱[建立擷取媒體](create-capture-media.md)。  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> 可開機媒體

可開機媒體包含下列元件：

- 開機映像
- 選用的[啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)及其必要檔案
- Configuration Manager 二進位檔

目的地電腦啟動時會連線至網路，並從網路擷取工作順序、OS 映像，以及任何其他必要的內容。 由於工作順序不在媒體上，因此不需要重新建立媒體即可變更工作順序或內容。  

> [!IMPORTANT]  
> 可開機媒體上的套件並未加密。 採取適當的安全防護措施 (例如新增媒體密碼)，以確保未經授權的使用者無法存取套件內容。  

如需如何建立可開機媒體的相關詳細資訊，請參閱[建立可開機媒體](create-bootable-media.md)。  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> 預先設置的媒體

預先設置的媒體允許您在佈建程序之前，將可開機媒體和 OS 映像套用至硬碟上。 預先設置的媒體是 Windows 映像檔 (WIM)。 其可由廠商安裝於裸機電腦上，或是安裝在未連線至 Configuration Manager 生產環境的設置中心。  

預先設置的媒體包含用於啟動目的電腦的開機映像，以及套用至目的電腦的 OS 映像。 您也可以指定在預先設置的媒體中加入應用程式、套件及驅動程式套件。 媒體中不包含部署 OS 的工作順序。 當您部署使用預先設置媒體的工作順序時，用戶端會先檢查本機工作順序快取中是否存在有效內容。 如果找不到內容或內容已被修改，用戶端便會從發佈點或同儕節點下載該內容。  

將電腦交給使用者之前，即需將預先設置的媒體套用至新電腦的硬碟中。 當電腦在您套用預先設置媒體後首次啟動時，它將會在 Windows PE 中啟動。 它會連線至管理點以尋找能完成 OS 部署程序的工作順序。  

> [!IMPORTANT]  
> 預先設置媒體上的套件並未加密。 採取適當的安全防護措施 (例如新增媒體密碼)，以確保未經授權的使用者無法存取套件內容。  

如需如何建立預先設置媒體的相關詳細資訊，請參閱[建立預先設置媒體](create-prestaged-media.md)。  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> 獨立媒體

獨立媒體包含部署 OS 所需的完整內容。 此內容包括工作順序和任何其他必要內容。 由於部署 OS 所需的所有內容都儲存在獨立媒體上，因此獨立媒體比其他類型的媒體需要更大的磁碟空間。  

如需如何建立獨立媒體的相關詳細資訊，請參閱[建立獨立媒體](create-stand-alone-media.md)。  


## <a name="considerations-when-using-https"></a>使用 HTTPS 時的考量

將管理點和發佈點設定為使用 HTTPS 通訊時，必須在主要站台而非管理中心網站建立開機媒體和預先設置的媒體。 此外，判斷要設定動態媒體或以網站為基礎的媒體時，請考量下列幾點：  

- 要將媒體設定為動態媒體，所有主要站台都必須要有用於建立媒體之網站的根憑證授權單位 (CA)。 您可以將根 CA 匯入至階層中的所有主要網站。  

- 若 Configuration Manager 階層中的主要站台使用不同的根 CA，您必須在每個站台上使用以站台為基礎的媒體。  
