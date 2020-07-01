---
title: 管理 Surface 驅動程式更新
titleSuffix: Configuration Manager
description: Configuration Manager 會同步處理 Surface 驅動程式更新，以部署至 Surface 裝置。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: 04793a053e85be051ce9ffafd2f15d274cf166f0
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973072"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>使用 Configuration Manager 管理 Surface 驅動程式

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 可讓您同步處理 Surface 裝置的驅動程式並加以部署，就像部署軟體更新一樣。 此功能可讓您確保 Surface 裝置正在執行最新的可用驅動程式。 此同步處理最初是以發行前版本功能的形式在 1706 版中引進，並成為 1710 中的功能。 <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>同步處理 Surface 驅動程式的先決條件

- 已連線到網際網路的頂層軟體更新點。
- 所有軟體更新點都必須執行已安裝累積更新 KB4025339 或更新版本的 Windows Server 2016。
- 根據預設，Configuration Manager 不會啟用此選擇性功能。 請先啟用這項功能再使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>啟用 Surface 驅動程式的同步處理

若要啟用 Surface 驅動程式的同步處理，請執行下列步驟：

1. 將 Configuration manager 主控台連線至頂層站台伺服器。
1. 移至 [系統管理] > [站台設定] > [站台]，然後在您的頂層站台上按一下。
1. 在功能區中，選取 [設定] > [設定站台元件] > [軟體更新點]。
1. 按一下 [分類] 索引標籤，然後按一下 [包含 Microsoft Surface 驅動程式與韌體更新] 的核取方塊，然後按一下 [套用]。

     ![從軟體更新點屬性啟用 Surface 驅動程式](media/enable-surface-driver-sync.png)

1. 在 [軟體更新點元件內容] 中，按一下 [產品] 索引標籤。如需詳細資訊，請參閱 [Surface 驅動程式的產品](#bkmk_prod)與 [Surface 型號](#bkmk_models)小節。
1. 針對您要支援 Surface 驅動程式的每個 Windows 10 版本選取產品。 您會發現，驅動程式的每個產品各都有兩個不同版本：

   - Windows 10 *版本* **更新及其後的維護驅動程式**
   - Windows 10 *版本* **更新及其後的升級與維護驅動程式**。

     ![Windows 10 版本驅動程式產品清單](media/surface-driver-products-sup.png)

1. 當您完成選取產品後，請按一下 [確定]。
1. [同步處理您的軟體更新點](../get-started/synchronize-software-updates.md)，將 Surface 驅動程式帶入 Configuration Manager。
1. 同步處理 Surface 驅動程式之後，請以部署其他更新的相同方式來加以部署。

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Surface 驅動程式的產品

大部分驅動程式都屬於下列產品群組：

- Windows 10 與更新版本的驅動程式
- Windows 10 與更新版本的升級與維護驅動程式
- Windows 10 年度更新版與更新版本的維護驅動程式
- Windows 10 年度更新版與更新版本的升級與維護驅動程式
- Windows 10 Creators Update 與更新版本的維護驅動程式
- Windows 10 Creators Update 與更新版本的升級與維護驅動程式
- Windows 10 Fall Creators Update 與更新版本的維護驅動程式
- Windows 10 Fall Creators Update 與更新版本的升級與維護驅動程式
- Windows 10 S 與更新版本的維護驅動程式
- 用於測試的 Windows 10 S 1709 版與更新版本的維護驅動程式
- 用於測試的 Windows 10 S 1709 版與更新版本的升級與維護驅動程式
- Windows 10 S 1803 版與更新版本的維護驅動程式
- Windows 10 S 1803 版與更新版本的升級與維護驅動程式
- Windows 10 S 1809 版與更新版本 (維護驅動程式)
- Windows 10 S 1809 版與更新版本 (升級與維護驅動程式)
- Windows 10 S 1903 版與更新版本 (維護驅動程式)
- Windows 10 S 1903 版與更新版本 (升級與維護驅動程式)
- Windows 10 1803 版與更新版本的維護驅動程式
- Windows 10 1803 版與更新版本的升級與維護驅動程式
- Windows 10 1809 版與更新版本 (維護驅動程式)
- Windows 10 1809 版與更新版本 (升級與維護驅動程式)
- Windows 10 1903 版與更新版本 (維護驅動程式)
- Windows 10 1903 版與更新版本 (升級與維護驅動程式)

> [!NOTE]
> 大部分 Surface 驅動程式都屬於多個 Windows 10 產品群組。 您可能不需要選取此處所列的所有產品。 為了協助減少填入您更新類別目錄的產品數目，建議您只選取環境進行同步處理所需的產品。

## <a name="surface-models"></a><a name="bkmk_models"></a> Surface 型號

下表包含 Configuration Manager 可以在上面安裝驅動程式的 Surface 型號與 Windows 10 版本。 Surface 驅動程式更新在發行至 Microsoft Update 目錄的當天是無法在 Configuration Manager 中取得的。 Configuration Manager 會維護其自己要匯入的 Surface 驅動程式清單。 需要 Windows 10 S 產品的裝置已加以註明。 Microsoft 的目標是在每個月的第二個星期二將 Surface 驅動程式新增至允許清單，讓其可供同步處理到 Configuration Manager。 如需詳細資訊，請參閱[常見問題集](#bkmk_faq)。

</br>

|Surface 型號|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|是| 是| 是 |是|是|
|Surface Pro 4|是| 是| 是 |是|是|
|Surface Pro 6|N/A| 是| 是 |是|是|
|Surface Pro 7|N/A| N/A| N/A |是|是|
|Surface Pro X|N/A| N/A| N/A |是|是|
|Surface Book|是| 是| 是 |是|是|
|Surface Book 2|是| 是| 是 |是|是|
|Surface Book 3|N/A| N/A| N/A |是|是|
|Surface Laptop|是，必須選取產品 [Windows 10 S 1709 版與更新版本的維護驅動程式]| 是，必須選取產品 [Windows 10 S 1803 版與更新版本的維護驅動程式]|是，必須選取產品 [Windows 10 S 1809 版與更新版本的升級與維護驅動程式]|是，必須選取產品 [Windows 10 S 1903 版與更新版本的升級與維護驅動程式]|是，必須選取產品 [Windows 10 S 1903 版與更新版本的升級與維護驅動程式]|
|Surface Laptop 2|N/A| 是 |是|是|是|
|Surface Laptop 3|N/A| N/A|N/A|是 |是|
|Surface Go|N/A| 是，必須選取產品 [Windows 10 S 1803 版與更新版本的維護驅動程式]|是，必須選取產品 [Windows 10 S 1809 版與更新版本的升級與維護驅動程式]|是，必須選取產品 [Windows 10 S 1903 版與更新版本的升級與維護驅動程式]|是，必須選取產品 [Windows 10 S 1903 版與更新版本的升級與維護驅動程式]|
|Surface Go 2|N/A| N/A| 是 |是|是，必須選取產品 [Windows 10 S 1903 版與更新版本的升級與維護驅動程式]|
|Surface Studio|是| 是| 是 |是|是|
|Surface Studio 2|N/A| 是| 是 |是|是|

## <a name="verify-the-configuration"></a>驗證設定

若要驗證已正確設定軟體更新點，請使用 **WsyncMgr.log** 與 **WCM.log**。

1. 開啟 WsyncMgr.log，並檢查下列記錄項目：

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. 如果下列其中一個項目已記錄在 **WsyncMgr.log** 中，請再次確認您已在軟體更新點的內容中選取 [包含 Microsoft Surface 驅動程式與韌體更新] 選項：
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. 開啟 **WCM.log** 並尋找類似下列項目的項目：
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   此項目是 XML 元素，其會列出軟體更新點伺服器目前已同步處理的每個產品群組與分類。 如果您找不到已選取的產品，請再次檢查軟體更新點的產品是否已儲存。
1. 您也可以等到下一次同步處理完成。 然後，檢查 Surface 驅動程式與韌體更新是否已列在 Configuration Manager 主控台的 [軟體更新] 中。 例如，主控台可能會顯示下列資訊：![Configuration Manager 主控台中已同步處理的 Surface 驅動程式](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> 常見問題集 (FAQ)

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>遵循此文章中的步驟之後，我的 Surface 驅動程式仍然未同步。 為什麼？

如果您從上游 Windows Server Update Services (WSUS) 伺服器進行同步處理，而不是從 Microsoft Update，請確定上游 WSUS 伺服器已設定為支援且會同步處理 Surface 驅動程式更新。 所有下游伺服器僅限存在於上游 WSUS 伺服器資料庫中的更新。

在 WSUS 中，有超過 68,000 個更新分類為驅動程式。 為了防止非 Surface 相關驅動程式同步處理到 Configuration Manager，Microsoft 會依允許清單來篩選驅動程式同步處理。 新的允許清單已發佈且併入 Configuration Manager 之後，新的驅動程式會在下一次同步處理時新增至主控台。 Microsoft 的目標是在每個月的第二個星期二將 Surface 驅動程式新增至允許清單，讓其可供同步處理到 Configuration Manager。

如果您的 Configuration Manager 環境處於離線狀態，則每次您將[維護更新](../../core/servers/manage/use-the-service-connection-tool.md)匯入 Configuration Manager 時，就會匯入新的允許清單。 在 Configuration Manager 主控台中顯示更新之前，您也必須匯入包含驅動程式的[新 WSUS 目錄](../get-started/synchronize-software-updates-disconnected.md)。 因為獨立 WSUS 環境包含的驅動程式比 Configuration Manager SUP 多，所以建議您建立具有線上功能的 Configuration Manager 環境，並將其設定為會同步處理 Surface 驅動程式。 這會提供類似離線環境且較小的 WSUS 匯出。

如果您的 Configuration Manager 環境已上線，且能夠偵測新的更新，您將會自動收到清單的更新。 如果您看不到預期的驅動程式，請檢閱 WCM.log 與 WsyncMgr.log 中是否有任何同步處理失敗。

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>我的 Configuration Manager 環境處於離線狀態，我是否可以手動將 Surface 驅動程式匯入到 WSUS？

否。 如果更新沒有在允許清單中列出，即使已匯入 WSUS，其也不會匯入至 Configuration Manager 主控台進行部署。 您必須使用[服務連線工具](../../core/servers/manage/use-the-service-connection-tool.md)，將服務更新匯入到 Configuration Manager 以更新允許清單。

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>部署 Surface 驅動程式與韌體更新有哪些替代方法？

如需有關如何透過替代通道部署 Surface 驅動程式與韌體更新的詳細資訊，請參閱[管理 Surface 驅動程式與韌體更新](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates) \(部分機器翻譯\)。 如果您想要下載 .msi 或 .exe 檔案，然後透過傳統軟體部署通道進行部署，請參閱[使用 Configuration Manager 讓 Surface 韌體保持為最新版](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager) \(英文\)。

## <a name="next-steps"></a>後續步驟

如需 Surface 驅動程式的詳細資訊，請參閱下列文章：

- [Surface 與 System Center Configuration Manager 的考量](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager) \(部分機器翻譯\)
- [Surface 更新記錄](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [下載 Surface 裝置的最新韌體和驅動程式](https://docs.microsoft.com/surface/deploy-the-latest-firmware-and-drivers-for-surface-devices) \(部分機器翻譯\)
