---
title: 管理 OS 映像
titleSuffix: Configuration Manager
description: 了解如何管理儲存在 Windows 映像 (WIM) 檔案中的 OS 映像。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 190a203494cecfd28c198197f3a582adff745265
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708886"
---
# <a name="manage-os-images-with-configuration-manager"></a>使用 Configuration Manager 管理 OS 映像

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的 OS 映像會以 Windows Image (WIM) 檔案格式儲存。 這些映像是參考檔案和資料夾的壓縮集合，用於安裝和設定電腦上的新 OS。 許多 OS 部署案例都需要 OS 映像。


## <a name="os-image-types"></a>OS 映像類型

您可以使用[預設的 OS映像](#default-image)，或從您設定的[參照電腦](#bkmk_capture)建置 OS 映像。 當您建置參照電腦時，您可以將 OS 檔案、驅動程式、支援檔案、軟體更新、工具和應用程式新增至 OS。 然後擷取它以建立映像檔。

### <a name="default-image"></a>預設映像

Windows 安裝檔案包含預設 OS 映像。 此映像是包含一組標準驅動程式的基本 OS 映像。 當您使用預設 OS 映像並在裝置上安裝 OS 之後，請使用工作順序步驟來安裝應用程式並進行其他設定。 在 Windows 來源檔案中找出預設 OS 映像： `\Sources\install.wim`。  

#### <a name="default-image-advantages"></a>預設映像的優點

- 映像的大小會小於擷取的映像大小。  

- 使用工作順序步驟安裝應用程式與設定更具彈性。 例如，您可以變更安裝於工作順序中的設定和應用程式，而不需要為裝置重新安裝映像。  

#### <a name="default-image-disadvantages"></a>預設映像的缺點

- OS 安裝可能花費較多時間。 OS 安裝完成後，需要進行應用程式安裝和其他設定。  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> 從參照電腦擷取的映像

若要建立自訂 OS 映像，請使用所需的 OS 來建置參照電腦。 然後安裝應用程式並進行設定。 從參照電腦擷取 OS 映像以建立 WIM 檔案。 手動建置參照電腦，或使用工作順序將部分或所有建置步驟自動化。 如需詳細資訊，請參閱[自訂 OS 映像](customize-operating-system-images.md)。  

#### <a name="captured-image-advantages"></a>擷取映像的優點

- 此種安裝可以比使用預設映像更快。 例如，應用程式可以使用擷取的 OS 映像來預先安裝。 您即不需要使用工作順序步驟再次安裝這些相同的應用程式。  

#### <a name="captured-image-disadvantages"></a>所擷取映像的缺點

- 映像大小可能會大於預設映像。  

- 當您需要更新應用程式和工具時，需要建立新的映像。  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> 新增 OS 映像  

在您可以使用 OS 映像前，先將其新增至您的 Configuration Manager 站台。

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [作業系統映像]  節點。  

2. 在功能區索引標籤 [首頁]  上的 [建立]  群組中，選取 [新增作業系統映像]  。 此動作會啟動 [新增作業系統映像精靈]。  

3. 在 [資料來源]  頁面上，指定下列資訊：

    - OS 映像檔的網路**路徑**。 例如 `\\server\share\path\image.wim`。

    - **從指定的 WIM 檔案解壓縮特定映像索引**，然後從清單中選取映像索引。<!--3719699--> 從 1902 版開始，此選項會自動匯入單一索引，而非檔案中的所有映像索引。 使用此選項會產生較小的映像檔案，以及更快的離線服務。 這也支援在套用軟體更新之後，針對較小的映像檔案[最佳化映像服務](#bkmk_resetbase)的程序。  

        > [!Note]  
        > Configuration Manager 不會修改來源映像檔。 它會在相同來源目錄中建立新的映像檔。
        >
        > 非常大型的映像檔 (例如超過 60 GB) 可能會導致此解壓縮程序失敗。 DISM 錯誤為 `Not enough storage is available to process this command.` Configuration Manager 使用的命令列位於 smsprov.log 和 dism.log 中。 手動執行相同的命令，然後匯入映像。<!-- SCCMDocs-pr issue 3502 -->  

    - 從 1906 版開始，如果您希望在用戶端上預先快取內容，請指定映像的 [架構]  和 [語言]  。 如需詳細資訊，請參閱[設定預先快取內容](../deploy-use/configure-precache-content.md)。<!--4224642-->  

4. 在 [一般]  頁面上，指定下列資訊。 這項資訊可在您有多個 OS 映像時用於識別用途。  

    - **名稱**：映像的唯一名稱。 根據預設，名稱來自 WIM 檔案名稱。  

    - **版本**：版本識別碼 (選用)。 此屬性不需要是映像的 OS 版本。 通常是貴組織的套件版本。  

    - **註解**：簡短描述 (選用)。  

5. 完成精靈。  

如需此主控台精靈的 PowerShell Cmdlet 對應項目，請參閱 [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps) (英文)。

接下來，將 OS 映像發佈至發佈點。  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> 將內容發佈至發佈點  

將 OS 映像發佈至與其他內容相同的發佈點。 在您部署工作順序之前，請將 OS 映像發佈到至少一個發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> 準備多點傳送部署的 OS 映像  

使用多點傳送部署，以允許多部電腦同時下載 OS 映像。 此映像檔由發佈點多點傳送至用戶端，而不是讓用戶端透過個別連線從發佈點下載映像的複本。 當您選擇 OS 部署方法來[透過網路使用多點傳送部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)，請設定支援多點傳送的 OS 映像。 然後，將映像發佈至啟用多點傳送的發佈點。

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [作業系統映像]  節點。  

2. 選取您要發佈至啟用多點傳送之發佈點的 OS 映像。  

3. 在功能區 [常用]  索引標籤的 [內容]  群組中，選取 [內容]  。  

4. 切換至 [發佈設定]  索引標籤，並設定下列選項：  

    - **允許透過多點傳送傳送此套件 (僅適用於 WinPE)** ：為 Configuration Manager 選取此選項，才能使用多點傳送來同時部署 OS 映像。  

    - **加密多點傳送套件**：指定是否要在將映像傳送至發佈點前，先讓站台對映像進行加密。 如果映像包含敏感性資訊，請使用此選項。 如果映像未加密，其內容會在網路上以純文字顯示。 未經授權的使用者可以攔截並檢視映像內容。  

    - **僅透過多點傳送傳送此套件**：指定是否只要在多點傳送工作階段期間讓發佈點部署映像。  

         如果您選取 [僅透過多點傳送傳送此套件]  ，則必須同時將工作順序部署選項指定為 [執行工作順序以視需要將內容下載到本機]  。 如需詳細資訊，請參閱 [Deploy a task sequence](../deploy-use/deploy-a-task-sequence.md)。  

5. 選取 [確定]  儲存設定並關閉映像屬性。  
