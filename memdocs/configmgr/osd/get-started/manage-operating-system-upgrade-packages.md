---
title: 管理 OS 升級套件
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 管理 OS 升級套件。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc50fc60601b63bca7b4a4b01ba3fb4a39fd8b91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708866"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>使用 Configuration Manager 管理 OS 升級套件

適用於：  Configuration Manager (最新分支)

Configuration Manager 中的 OS 升級套件包含用來升級電腦上現有 OS 的 Windows 安裝程式來源檔案。 本文描述如何新增、發佈及檢修 OS 升級套件。

> [!NOTE]
> OS 升級套件也能用於新的 Windows 安裝。 不過，驅動程式必須與此方法相容。 從 OS 升級套件安裝新的 Windows 時，會安裝驅動程式，但驅動程式仍在 Windows PE 中，而不是像在 Windows PE 中只是插入。 某些驅動程式不相容，因此無法安裝在 Windows PE 中。 在 Windows PE 中，若驅動程式不相容而無法安裝，請改為使用 [OS 映像](manage-operating-system-images.md)，例如 **install.wim**。

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a> 新增 OS 升級套件  

在您可以使用 OS 升級套件之前，先將其新增至您的 Configuration Manager 站台。

1. 在 Configuration Manager 主控台中，前往 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [作業系統升級套件]  節點。  

2. 在功能區索引標籤 [首頁]  上的 [建立]  群組中，選取 [新增作業系統升級套件]  。 此動作會啟動 [新增作業系統升級精靈]。  

3. 在 [資料來源]  頁面上，指定下列設定：

    - OS 升級套件安裝來源檔案的網路 [路徑]  。 例如 `\\server\share\path`。  

        > [!NOTE]  
        >  安裝來源檔案包含 setup.exe 和其他檔案及資料夾，以便安裝 OS。  

        > [!IMPORTANT]  
        >  限制這些安裝來源檔案的存取權，以避免不必要的竄改。  

    - **從所選升級套件的 install.wim 檔案中解壓縮特定的映像索引**，然後從清單中選取映像索引。<!--4931110--> 從 1910 版開始，此選項會自動匯入單一索引，而非檔案中的所有映像索引。 使用此選項會產生較小的映像檔案，以及更快的離線服務。 這也支援在套用軟體更新之後，針對較小的映像檔案[最佳化映像服務](#bkmk_resetbase)的程序。  

        > [!IMPORTANT]  
        > Configuration Manager 會覆寫 OS 升級套件中的現有 install.wim。 它會將映像索引解壓縮至暫存位置，然後將它移至原始來源目錄。 在匯入作業系統升級套件並啟用此選項之前，請務必先備份原始來源檔案。

    - 如果您希望在用戶端上預先快取內容，請指定映像的 [架構]  和 [語言]  。 如需詳細資訊，請參閱[設定預先快取內容](../deploy-use/configure-precache-content.md)。  

4. 在 [一般]  頁面上，指定下列資訊。 這項資訊可在您有多個 OS 升級套件時用於識別用途。  

    - **名稱**：OS 升級套件的唯一名稱。  

    - **版本**：版本識別碼 (選用)。 此屬性不需為升級套件的 OS 版本。 通常是貴組織的套件版本。  

    - **註解**：簡短描述 (選用)。  

5. 完成精靈。  

接下來，將 OS 升級套件發佈至發佈點。  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a> 將內容發佈至發佈點  

將 OS 升級套件發佈至與其他內容相同的發佈點。 在您部署工作順序之前，請將 OS 升級套件發佈到至少一個發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>後續步驟

[建立工作順序以升級 OS](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
