---
title: 1606 版的新功能
titleSuffix: Configuration Manager
description: 取得 Configuration Manager 1606 版中變更和所引進新功能的詳細資料。
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4298a6a66d60d79d05f8b5cdc9ff8caa0e7f4426
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074022"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Configuration Manager 1606 版中的新功能

適用於：  Configuration Manager (最新分支)

Configuration Manager 1606 更新會以執行 1511 或 1602 版之原安裝站台的主控台內更新形式提供。 1511 版是您用來安裝新 Configuration Manager 站台的初始基準版本。
> [!TIP]  
> 深入了解：  
>   
> - [安裝新的站台](../../servers/deploy/install/prepare-to-install-sites.md) (使用 1511 等基準版本)  
> - [在站台安裝更新](../../servers/manage/updates.md) (如更新 1602 或 1606)  

 下列各節提供 Configuration Manager 1606 版中的變更和推出的新功能詳細資料。  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>更新與服務

### <a name="changes-for-the-updates-and-servicing-node"></a>[更新與服務] 節點的變更
Configuration Manager 主控台的 [更新與服務] 節點變更如下︰
> [!NOTE]
> 要安裝 1606 版後才能使用這些變更。

- **節點名稱變更：**

    在 [監視]  工作區中，[Site Servicing status]\(站台服務狀態)  節點已重新命名為 [更新與服務狀態]  。
- **更多安裝狀態詳細資料：**

    當您檢視站台的更新安裝狀態時，主控台現在會分開顯示下列動作的詳細資料：
    - **下載** (僅適用於服務連接點站台系統角色安裝所在的頂層站台)
    - **複寫**
    - **必要條件檢查**
    - **安裝**

  此外，現在各步驟都有更詳細的資訊，包括您可以在哪一個記錄檔中檢視詳細資訊。  
-   **新增在先決條件失敗時重試的選項︰**

    在 [管理]  和 [監視]  工作區的 [更新與服務]  節點中，其功能區上皆包含名為 [忽略先決條件警告]  的新按鈕。

    當您從 [更新精靈] 安裝更新，但未使用忽略先決條件警告的選項，而導致該更新安裝由於警告突然停止時，您可以選取功能區上的 [忽略先決條件警告]  ， 即可觸發自動接續更新安裝。  



- **更整潔的更新檢視畫面：**

    現在，[更新與服務]  節點只會顯示最近安裝的更新，以及可供您安裝的任何新更新。 若要檢視先前安裝的更新，請按一下功能區顯示的 [歷程記錄]  新按鈕。  

-   **進入生產階段前已重新命名的選項︰**

    在 [更新與服務]  節點中，原本的 [用戶端選項]  按鈕現已稱為 [將生產階段前用戶端升階]  。


###  <a name="pre-release-features"></a>發行前版本功能
從 1606 開始，您必須同意使用 Configuration Manager 中的發行前版本功能，才可以選取並啟用這些功能。 如需詳細資訊，請參閱[使用發行前版本功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

### <a name="new-distribution-point-update-behavior"></a>新的發佈點更新行為
1606 版更新所導入的變更，可讓您在安裝未來更新時，提高發佈點的可用性。

如果站台需要自動重新安裝標準及提取發佈點站台系統角色，在您安裝 1606 版更新之後，並接著在該站台安裝更新時，就再也不會同時離線更新所有發佈點。 取而代之的是，站台伺服器會使用站台的內容發佈設定，在任何指定時間將更新發佈至一部分發佈點。 這樣一來，只有部分發佈點會離線安裝更新。 如此可讓還沒有開始更新或已完成更新的發佈點保持線上狀態，以提供內容給用戶端。



## <a name="accessibility"></a><a name="accessibility"></a> 協助工具
現在，若要在工作區的不同節點間瀏覽，您可以輸入節點名稱的第一個字母。 每個按鍵動作都會將游標移至以該字母開頭的下一個節點。 如果使用者有使用螢幕助讀程式，則助讀程式會讀出該節點的名稱。 如需協助工具選項的詳細資訊，請參閱[協助工具功能](../../../core/understand/accessibility-features.md)。

## <a name="administration"></a><a name="administration"></a>管理
Configuration Manager 主控台的管理變更如下︰
### <a name="oms-connector"></a>OMS 連接器

現在，您可以將 Configuration Manager 以 Configuration Manager 的集合形式連接到 [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/)。 這樣就可以在 OMS 中顯示 Configuration Manager 部署的資料，如集合。 如需詳細資訊，請參閱[將資料從 Configuration Manager 同步處理至 Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)。

OMS 連接器是發行前版本的功能。 若要啟用它，請參閱[使用更新的發行前版本功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)。

### <a name="support-for-cache-size-in-client-settings"></a>用戶端設定的快取大小支援

您現在可以在 Configuration Manager 主控台中，使用 [用戶端設定]  在用戶端電腦上設定快取資料夾的大小。 以往，您只能在安裝或重新安裝用戶端軟體時，設定用戶端的快取大小。 現在，您可以將快取大小指定為用戶端設定 (預設或自訂)，然後將這些設定與下一個原則更新套用到用戶端，而不必重新安裝用戶端。 如需詳細資訊，請參閱 [設定 Configuration Manager 用戶端的用戶端快取](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。

## <a name="on-premises-mobile-device-management"></a>內部部署行動裝置管理

### <a name="support-for-multiple-device-management-points"></a>對多個裝置管理點的支援

內部部署行動裝置管理 (MDM) 現在支援 Windows 10 年度更新版中的一項新功能，其會自動將已註冊的裝置設為具有多個裝置管理點以供使用。 這項功能可在裝置無法使用慣用的裝置管理點時，改用其他的裝置管理點。 這項功能只適用於安裝 Windows 10 年度更新版的電腦及裝置。


## <a name="application-management"></a>應用程式管理

### <a name="manage-apps-from-the-windows-store-for-business"></a>從商務用 Windows 市集管理應用程式

您可以在[商務用 Windows 市集](https://www.microsoft.com/business-store)中尋找適合組織的 Windows 應用程式，並視需要個別或大量購買。 藉由將市集連線到 Configuration Manager，您就可以同步處理使用 Configuration Manager 所購買的應用程式清單、在 Configuration Manager 主控台中進行檢視，以及像是任何其他應用程式一樣進行部署。

如需詳細資訊，請參閱[使用 Configuration Manager 管理從商務用 Windows 市集購買的應用程式](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)。

### <a name="manage-ios-volume-purchased-apps"></a>管理 iOS 大量採購的應用程式

已改善管理大量採購 iOS 應用程式及使用 Configuration Manager 部署這些應用程式的工作流程。


### <a name="software-center-user-interface"></a>軟體中心使用者介面

軟體中心使用者介面已經過簡化，更容易探索。
*  [安裝狀態]  和 [安裝的軟體]  索引標籤已合併為單一的 [安裝狀態]  索引標籤。
*  已分隔出 [更新]  、[作業系統]  和 [應用程式]  三個不同的索引標籤。
* 您現在可以選取一次安裝多個更新，或按一下 [全部安裝]  按鈕，一次安裝所有更新。

### <a name="content-status-links"></a>內容狀態連結
在應用程式或套件的內容中，現已提供可前往該物件狀態的連結。

## <a name="software-updates"></a>軟體更新

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>管理 Office 365 用戶端代理程式的用戶端設定
您現在可以使用 Configuration Manager 用戶端設定來管理 Office 365 用戶端代理程式。 在您做好上述設定並部署 Office 365 更新之後，Configuration Manager 用戶端代理程式會與 Office 365 用戶端代理程式合作，從發佈點下載 Office 365 更新並加以安裝。

如需詳細資訊，請參閱[使用 Configuration Manager 管理 Office 365 ProPlus 更新](../../../sum/deploy-use/manage-office-365-proplus-updates.md)。

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>手動將用戶端切換到新軟體更新點
您現在可以啟用相關選項，以便 Configuration Manager 用戶端在主動式軟體更新點發生問題時切換到新軟體更新點。 啟用之後，用戶端會在下次掃描時尋找另一個軟體更新點。

如需詳細資訊，請參閱[在 Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)。

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>提供在安裝軟體更新後重新啟動 Windows 10 用戶端的選項
如果軟體更新需要重新啟動，但該軟體更新是使用 Configuration Manager 來部署並安裝於電腦上，則會排定擱置重新啟動， 並顯示重新啟動對話方塊。 從 Configuration Manager 1606 版本開始，只要 Configuration Manager 軟體更新擱置重新啟動，就會提供 [更新並重新啟動]  和 [更新並關機]  選項。 在 Windows 10 電腦的 Windows 電源選項中，會顯示上述選項。 一旦您使用其中一個選項，重新開機之後就不會顯示重新啟動對話方塊。

如需詳細資訊，請參閱[規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions)。

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>在用戶端安裝軟體更新並重新啟動之後，立刻執行軟體更新合規性掃描
您現在可以在用戶端安裝軟體更新並重新啟動之後，立刻執行軟體更新合規性掃描。 若要為某個部署進行此設定，請在 [部署軟體更新精靈] 的 [使用者體驗]  頁面上，選取 [若此部署中的任何更新需要重新啟動系統，請在重新啟動後執行更新部署評估週期]  。 這可讓用戶端檢查在用戶端重新啟動後是否有其他軟體更新轉變為適用，然後在同一個維護時段內安裝這些更新 (以成為符合規範)。 如需詳細資訊，請參閱[自動部署軟體更新](../../../sum/deploy-use/automatically-deploy-software-updates.md)或[手動部署軟體更新](../../../sum/deploy-use/manually-deploy-software-updates.md)。

## <a name="operating-system-deployment"></a>作業系統部署

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>工作順序步驟的改善：安裝軟體更新
[從快取掃描結果評估軟體更新]  這項新設定可讓您選擇執行完整掃描軟體更新，而不是使用快取的掃描結果。 如需詳細資訊，請參閱[工作順序步驟](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)。

此外，您也可以使用新的 **SMSTSSoftwareUpdateScanTimeout** 工作順序變數。 此變數可讓您在「安裝軟體更新」工作順序步驟期間，控制軟體更新掃描的逾時。 預設值為 30 分鐘。 如需詳細資訊，請參閱[工作順序內建變數](../../../osd/understand/task-sequence-variables.md)。

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>OSDPreserveDriveLetter 工作順序變數已被取代
OSDPreserveDriveLetter 工作順序變數已被取代。 從 Configuration Manager 1606 版開始，Windows 安裝程式在作業系統部署期間，預設會決定使用最佳的磁碟機代號 (通常是 C:)。

如需詳細資訊，請參閱[工作順序內建變數](../../../osd/understand/task-sequence-variables.md)。

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>自訂 PXE 之發佈點的 RamDisk TFTP 視窗大小
您現在可以自訂 PXE 之發佈點的 RamDisk TFTP 視窗大小。 如果您已自訂網路，可能會因為視窗太大導致開機映像下載發生逾時錯誤而失敗。 自訂 RamDisk 簡單式檔案傳輸通訊協定 (TFTP) 視窗大小可讓您在使用 PXE 來滿足特定的網路需求時，將 TFTP 流量最佳化。

如需詳細資訊，請參閱[使用 Configuration Manager 為作業系統部署準備站台系統角色](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="compliance-settings"></a>相容性設定

### <a name="smart-lock-setting-for-android-devices"></a>Android 裝置的 SmartLock 設定
Android 和 Samsung KNOX Standard 設定項目中已加入 [允許 Smart Lock 和其他信任的代理程式]  這項新設定。

此設定可讓您控制相容 Android 裝置上的 Smart Lock 功能。 此電話功能 (有時也稱為信任代理程式) 可讓您在裝置位於受信任的位置時，停用或略過裝置鎖定畫面密碼。 例如，當裝置連線到特定的藍牙裝置或靠近 NFC 標記時，就可能位於受信任的位置。 您可以使用此設定來防止使用者設定 Smart Lock。


## <a name="device-configuration-and-protection"></a>裝置的設定與保護

### <a name="product-name-changes"></a>產品名稱變更

* Microsoft Passport for Work 現在稱為 **Windows Hello 企業版**。
* 企業資料保護現在稱為 **Windows 資訊保護**。

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Windows Hello 企業版的部署 (Passport for Work)

您現在可以將 Windows Hello 企業版原則部署至受 Configuration Manager 用戶端管理且已加入網域的 Windows 10 裝置。

已更新 Configuration Manager 主控台以反映這些變更。

### <a name="ios-activation-lock"></a>iOS 啟用鎖定
Configuration Manager 可以協助您管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 啟用「啟用鎖定」時，必須先輸入使用者的 Apple ID 和密碼，才能讓所有人：
* 關閉「尋找我的 iPhone」。
* 清除裝置。
* 重新啟動裝置。

Configuration Manager 可以透過兩種方式協助您管理啟用鎖定：

- 在受監督裝置上啟用「啟用鎖定」。
- 在受監督裝置上略過「啟用鎖定」。


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender 進階威脅防護

Endpoint Protection 可協助管理及監視 Microsoft Defender 進階威脅防護 (ATP)。 Microsoft Defender ATP 是新的服務，將可協助企業偵測、調查和回應其網路上的進階攻擊。 Configuration Manager 原則可協助您登入及監視執行 Windows 10 1607 版 (組建 14328) 或更新版本的受管理電腦。

如需詳細資訊，請參閱 [Microsoft Defender 進階威脅防護](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md)。

### <a name="device-categories"></a>裝置類別
您可以建立裝置類別，以在使用 Configuration Manager 與 Microsoft Intune 時自動將裝置放入裝置集合。 使用者向 Intune 註冊裝置時，必須選擇裝置類別。 您也可以從 Configuration Manager 主控台中變更裝置類別。

如需詳細資訊，請參閱[如何使用 Configuration Manager 自動將裝置分類為集合](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md)。

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>使用 IMEI 或 iOS 序號預先宣告裝置

您可以透過匯入國際站移動設備識別碼 (IMEI) 號碼或 iOS 序號，識別公司擁有的裝置。 您可以上傳包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。 針對在裝置清單中註冊為「公司」的裝置，系統會使用匯入的資訊來設定其擁有權。 每一位存取服務的使用者還是需要 Intune 授權。

### <a name="on-premises-health-attestation-service-communication"></a>內部部署健康情況證明服務通訊

您現在可以直接使用內部部署基礎結構，啟用 Windows 10 電腦的健全狀況證明服務監視，讓沒有網際網路存取的電腦可以回報裝置健全狀況證明 (DHA)。

如需詳細資料，請參閱 [Configuration Manager 的健康情況證明](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers)。  

## <a name="remote-control"></a>遠端控制
可讓您的使用者在遠端控制工作階段中，從共用剪貼簿傳輸內容之前，得以接受或拒絕檔案傳輸。 使用者只需要在每個工作階段中授與權限一次，且檢視人員不能自我授權進行檔案傳輸。 您可以在 [管理]  工作區中找到這個新設定。 前往 [用戶端設定]  ，然後開啟 [預設設定]  中的 [遠端工具]  面板。
