---
title: 商務用 OneDrive 設定檔
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的商務用 OneDrive 設定檔，將 Windows 已知資料夾重新導向到商務用 OneDrive。
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 47d44c96e0ae63504278c58a5838c54648665505
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692306"
---
# <a name="onedrive-for-business-profiles"></a>商務用 OneDrive 設定檔

從 Configuration Manager 版本 1902 開始，您可以建立商務用 OneDrive 設定檔，將 Windows 已知資料夾移動到商務用 OneDrive。 這些資料夾包括 [桌面]、[文件] 及 [圖片]。 在每個設定檔中，您可以指定用於移動 Windows 已知資料夾的設定。 如需商務用 OneDrive 的詳細資訊，請參閱[將 Windows 已知資料夾重新導向及移至 OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders) \(機器翻譯\)。 <!--3556021-->

## <a name="prerequisites"></a>必要條件

- [尋找您的 Office 365 租用戶識別碼](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id) \(機器翻譯\)  

- 部署 OneDrive 同步用戶端 18.111.0603.0004 版或更新版本。 如需詳細資訊，請參閱[使用 Configuration Manager 部署 OneDrive 應用程式](https://docs.microsoft.com/onedrive/deploy-on-windows) \(部分機器翻譯\)。  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a> 將 Windows 已知資料夾移至 OneDrive
<!--3556021-->
使用 Configuration Manager 將 Windows 已知資料夾移至「商務用 OneDrive」。 這些資料夾包括 [桌面]、[文件] 及 [圖片]。 若要簡化您的 Windows 10 升級，請在部署工作順序之前，先將這些設定部署至 Windows 7 用戶端。 

1. 在 Configuration Manager 主控台中，前往 [資產與合規性]  工作區，展開 [合規性設定]  ，然後選取 [商務用 OneDrive 設定檔]  節點。  

   ![商務用 OneDrive 設定檔](media/onedrive-for-business-profiles-node.png)
2. 在功能區中，選取 [建立商務用 OneDrive 設定檔]  。  

3. 指定用於識別此原則的名稱，然後選取 [下一步]  。  

4. 選取會與此商務用 OneDrive 設定檔一併佈建的平台。 當您完成選取平台後，按一下 [下一步]  。

    ![選取商務用 OneDrive 設定檔的平台](media/onedrive-for-business-profile-select-platforms.png) 

5. 在 [設定]  頁面上：

    1. 指定您的 Office 365 租用戶識別碼。  

    2. 選取下列其中一個選項以將已知資料夾移至 OneDrive：  

        - **提示使用者將 Windows 已知資料夾移動到 OneDrive** ：使用此選項時，使用者可以看到精靈移動其檔案。 如果他們選擇延後或拒絕移動其資料夾，OneDrive 會定期提醒他們。  

        - **以無訊息方式將 Windows 已知資料夾移至 OneDrive**：當此原則適用於裝置時，OneDrive 用戶端會自動將已知資料夾重新導向到「商務用 OneDrive」。  

            - **將資料夾重新導向後，對使用者顯示通知**：如果您啟用此選項，OneDrive 用戶端就會在移動使用者的資料夾後通知使用者。  

    3. **防止使用者將其 Windows 已知資料夾重新導向回他們的電腦**：若要讓使用者將這些資料夾移回到裝置上，請在用戶端的商務用 OneDrive上停用此選項。  

       ![商務用 OneDrive 已知資料夾移動設定](media/onedrive-for-business-profile-move-folder-settings.png)

6. 完成精靈步驟，然後部署原則。  


## <a name="deploy-the-onedrive-for-business-profile"></a>部署商務用 OneDrive 設定檔

1. 在 Configuration Manager 主控台中，前往 [資產與合規性]  工作區，展開 [合規性設定]  ，然後選取 [商務用 OneDrive 設定檔]  節點。  


2. 選取設定檔，然後選取功能區中的 [部署]  。

3. 針對您的部署指定下列設定：

   1. **集合**：按一下 [瀏覽]  ，然後選取您要部署設定檔的集合。  
   1. **產生警示**：

      - **當合規性低於以下標準**：保持用戶端合規性的最小百分比，低於該百分比將產生警示。
      -  **日期和時間**：開始根據設定檔合規性產生警示的日期。
      - **產生 System Center Operations Manager 警示**：向 System Center Operations Manager 傳送合規性警示。
   1. **排程**：

      - **簡易排程**：根據預設，此設定使用簡易排程，每七天起始一次合規性評估。
      - **自訂排程**：定義何時執行合規性評估。 在建立排程或者您可以使用 UTC 時，開始時間是以執行 Configuration Manager 主控台之電腦的本機時間為基礎。
 
      ![部署商務用 OneDrive 設定檔](media/onedrive-for-business-deploy-profile.png)

4. 按一下 [確定]  以部署商務用 OneDrive 設定檔。


## <a name="next-steps"></a>後續步驟

[建立遠端連線設定檔](create-remote-connection-profiles.md)
