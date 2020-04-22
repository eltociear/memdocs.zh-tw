---
title: 管理用戶端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理用戶端。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d7697f8b5a2017aa732c52512bf31598c070fbc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696076"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>如何在 Configuration Manager 中管理用戶端

適用於：  Configuration Manager (最新分支)

已在裝置上安裝 Configuration Manager 用戶端並順利指派給站台之後，就會在 [裝置]  節點的 [資產與相容性]  工作區，以及在 [裝置集合]  節點的一或多個集合中查看裝置。 選取裝置或集合，然後執行管理作業。 不過，有其他方法可以管理用戶端，這些方法可能與主控台的其他工作區有關，或與主控台以外的工作有關。  

> [!NOTE]  
> 如果您安裝 Configuration Manager 用戶端，但尚未成功指派用戶端給站台，則該用戶端可能不會顯示在主控台中。 指派用戶端給站台之後，請更新集合成員資格，然後重新整理主控台檢視。  
>
> 若尚未安裝 Configuration Manager 用戶端，主控台中可能也會顯示裝置。 如果站台發現裝置，但尚未安裝和指派用戶端，就會發生此行為。
>
> 利用 [Exchange Server 連接器](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)或[內部部署 MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) 管理的行動裝置不會安裝 Configuration Manager 用戶端。  
>
> 若要從主控台管理裝置，請使用 [裝置]  節點中的 [用戶端]  資料行來判斷是否已安裝用戶端。  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> 從 [裝置]  節點管理用戶端  

根據不同的裝置類型，某些選項可能無法使用。  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [裝置]  節點。  

2. 選取一或多部裝置，然後從功能區中選取其中一個用戶端管理工作。 您也可以在裝置上按一下滑鼠右鍵。  

### <a name="import-user-device-affinity"></a>匯入使用者裝置親和性

設定使用者和裝置間的關聯，讓您有效地部署軟體給使用者。  

如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

### <a name="import-computer-information"></a>匯入電腦資訊

啟動 [匯入電腦資訊精靈]  ，將新的電腦資訊匯入 Configuration Manager 資料庫。 您可以使用檔案匯入多部電腦，或指定單一電腦的資訊。

### <a name="add-selected-items"></a>新增選取的項目

提供下列選項：

- **將選取的項目新增至現有裝置集合**：開啟 [選取集合]  對話方塊。 選取您要新增此裝置的集合。 使用 [直接]  成員資格規則，將裝置包含在此集合中。  

- **將選取的項目新增至新裝置集合**：開啟 [建立裝置集合精靈]  ，您可以在其中建立新的集合。 使用 [直接]  成員資格規則，將選取的集合包含在此集合中。  

如需詳細資訊，請參閱[如何建立集合](collections/create-collections.md)。

### <a name="install-client"></a>安裝用戶端

開啟 [安裝用戶端精靈]  。 此精靈會使用用戶端推入安裝，在選取的裝置上安裝或重新安裝 Configuration Manager 用戶端。

> [!TIP]  
> 安裝 Configuration Manager 用戶端的方式有很多種。 雖然 [用戶端推入精靈] 提供從主控台方便執行的用戶端安裝方法，但此方法有許多相依性，不適用於所有環境。 如需這些相依性的詳細資訊，請參閱[將用戶端部署到 Windows 電腦的必要條件](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation)。 如需其他用戶端安裝方法的詳細資訊，請參閱[用戶端安裝方法](../deploy/plan/client-installation-methods.md)。

如需詳細資訊，請參閱[如何使用用戶端推入來安裝 Configuration Manager 用戶端](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。

### <a name="run-script"></a>執行指令碼

開啟 [執行指令碼精靈]  ，在選取的裝置上執行 PowerShell 指令碼。

如需詳細資訊，請參閱[建立及執行 PowerShell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)。

### <a name="install-application"></a>安裝應用程式

即時將應用程式安裝到裝置。 這項功能可協助減少為每個應用程式區分集合的需求。

如需詳細資訊，請參閱[為裝置安裝應用程式](../../../apps/deploy-use/install-app-for-device.md)。

### <a name="reassign-site"></a>重新指派站台

重新指派一個或多個用戶端 (包括受管理的行動裝置) 到階層中的另一個主要網站。 您可以個別重新指派用戶端，或選取多個以進行大量重新指派。  

### <a name="client-settings---resultant-client-settings"></a>用戶端設定 - 結果用戶端設定

您將多個用戶端設定部署到相同裝置時，設定的優先順序和組合會很複雜。 使用此選項可查看部署到此裝置的用戶端設定結果集。

如需詳細資訊，請參閱[如何設定用戶端設定](../deploy/configure-client-settings.md)。

### <a name="start"></a>開始

- 執行 [資源總管]  以查看來自 Windows 用戶端的軟硬體清查資訊。 如需詳細資訊，請參閱下列文章：

  - [如何使用資源總管檢視硬體清查](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [如何使用資源總管檢視軟體清查](inventory/use-resource-explorer-to-view-software-inventory.md)

- 使用 [遠端控制]  、[遠端協助]  或 [遠端桌面用戶端]  來遠端管理裝置。 如需詳細資訊，請參閱[如何從遠端管理 Windows 用戶端電腦](remote-control/remotely-administer-a-windows-client-computer.md)。

### <a name="approve"></a>核准

當用戶端使用 HTTP 和自我簽署憑證與站台系統通訊時，您必須核准這些用戶端，以便將它們識別為受信任的電腦。 根據預設，站台設定會自動核准相同 Active Directory 樹系和受信任樹系的用戶端。 此預設行為表示您不需要手動核准每個用戶端。 請手動核准您信任的工作群組電腦，以及您信任但未核准的任何其他電腦。

> [!IMPORTANT]  
> 雖然某些管理功能可用於未核准的用戶端，但 Configuration Manager 不支援此狀況。  

您不需要核准一律使用 HTTPS 與站台系統通訊的用戶端，或在使用 HTTP 與站台系統通訊時使用 PKI 憑證的用戶端。 這些用戶端會使用 PKI 憑證建立信任關係。

### <a name="block-or-unblock"></a>封鎖或解除封鎖

封鎖您不再信任的用戶端。 封鎖會防止用戶端接收原則，以及防止站台系統與用戶端通訊。  

> [!IMPORTANT]  
> 封鎖用戶端只會防止用戶端與 Configuration Manager 站台系統通訊。 它不會防止用戶端與其他裝置通訊。 當用戶端使用 HTTP 而非 HTTPS 與站台系統通訊時，有一些安全性限制。  

您也可以解除封鎖已封鎖的用戶端。

如需詳細資訊，請參閱[判斷是否要封鎖用戶端](../deploy/plan/determine-whether-to-block-clients.md)。

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>清除必要的 PXE 部署

您可以藉由清除指派到 Configuration Manager 集合或電腦的最後一個 PXE 部署狀態，重新部署必要的 PXE 部署。 此動作會重設該部署的狀態，並重新安裝最新的必要部署。

如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。

### <a name="client-notification"></a>用戶端通知

如需詳細資訊，請參閱[用戶端通知](client-notification.md#client-notification)。

### <a name="endpoint-protection"></a>Endpoint Protection

如需詳細資訊，請參閱[用戶端通知](client-notification.md#endpoint-protection)。

### <a name="edit-primary-users"></a>編輯主要使用者

檢視此裝置過去 90 天的使用者，或指定此裝置的主要使用者。

如需詳細資訊，請參閱[透過使用者裝置親和性連結使用者和裝置](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

### <a name="wipe-a-mobile-device"></a>抹除行動裝置

您可以抹除支援抹除命令的行動裝置。 此動作會永久移除行動裝置上的所有資料，這些資料包括個人設定和個人資料。 此動作通常會將行動裝置重設回原廠預設值。 行動裝置不再受信任時，請抹除行動裝置。 例如，裝置遺失或遭竊。  

> [!TIP]  
> 如需行動裝置如何處理遠端抹除命令的詳細資訊，請參閱製造商的文件。  

在行動裝置收到抹除命令前，通常會有一段延遲時間：  

- 如果行動裝置是由 Configuration Manager 所註冊，則用戶端會在下載其用戶端原則時收到此命令。

- 如果行動裝置是由 Exchange Server 連接器所管理，則會在與 Exchange 進行同步處理時收到此命令。  

若要監視裝置收到抹除命令的時間，請使用 [抹除狀態]  資料行。 在裝置將抹除認可傳送給 Configuration Manager 之後，您才可以取消抹除命令。  

### <a name="retire-a-mobile-device"></a>淘汰行動裝置

只有由內部部署 MDM註冊的行動裝置才支援 [淘汰]  選項。  

如需詳細資訊，請參閱[透過遠端抹除、遠端鎖定或密碼重設來協助保護您的資料](../../../mdm/deploy-use/wipe-lock-reset-devices.md)。

### <a name="change-ownership"></a>變更擁有權

如果裝置未加入網域且未安裝 Configuration Manager 用戶端，請使用此選項將擁有權變更為 [公司]  或 [個人]  。  

您可以在應用程式需求中使用這個值來控制部署，以及控制要從使用者裝置收集多少清查。  

您可能需要以滑鼠右鍵按一下任意欄標題，然後選擇 [裝置擁有者]  欄以將該欄新增至檢視。

### <a name="delete"></a>刪除

> [!WARNING]  
> 如果您想要解除安裝 Configuration Manager 用戶端，或將該用戶端從集合中移除，請勿刪除該用戶端。  

[刪除]  動作會手動移除 Configuration Manager 資料庫中的用戶端記錄。 僅使用此動作來針對問題進行疑難排解。 如果您刪除此物件，但仍然安裝用戶端且其與站台進行通訊，則活動訊號探索會重新建立用戶端記錄。 雖然用戶端歷程記錄和任何先前的關聯都會遺失，但是用戶端記錄會重新出現在 Configuration Manager 主控台中。  
> [!NOTE]  
> 當您刪除 Configuration Manager 所註冊的行動裝置用戶端時，此動作也會撤銷已發出的 PKI 憑證。 管理點接著會拒絕此憑證，即使 IIS 並未檢查憑證撤銷清單 (CRL) 也一樣。
>
> 當您刪除這些用戶端時，不會撤銷行動裝置舊版用戶端上的憑證。

若要解除安裝用戶端，請參閱[解除安裝 Configuration Manager 用戶端](#BKMK_UninstalClient)。  

若要將用戶端指派給新的主要站台，請參閱[如何將用戶端指派給站台](../deploy/assign-clients-to-a-site.md)。

若要將用戶端從集合中移除，請重新設定集合內容。 如需詳細資訊，請參閱[如何管理集合](collections/manage-collections.md)。

### <a name="refresh"></a>重新整理

以資料庫中的最新資料重新整理主控台檢視。 例如，如果裝置出現在探索的清單中，但未顯示為已安裝。 在您安裝用戶端並確定它已指派給站台之後，請選取 [重新整理]  。

### <a name="properties"></a>屬性

檢視以用戶端為目標的探索資料和部署。

您也可以設定讓工作順序用來將作業系統部署到裝置的變數。 如需詳細資訊，請參閱[針對裝置與集合建立工作順序變數](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var)。


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> 從 [裝置集合]  節點管理用戶端

可供 [裝置]  節點中裝置使用的許多工作，也可在集合上使用。 主控台會自動將作業套用至集合中的所有合格裝置。 整個集合上的此動作會產生額外的網路封包，並增加站台伺服器上的 CPU 使用量。  

請先考慮下列問題，再執行集合層級工作。 一旦啟動，就無法從主控台停止工作。

- 集合中有多少裝置？
- 裝置是透過低頻寬網路連線進行連線嗎？
- 這項工作完成所有裝置需要多少時間？

如需詳細資訊，請參閱[如何管理集合](collections/manage-collections.md)。


## <a name="restart-clients"></a>重新啟動用戶端

使用 Configuration Manager 主控台來識別需要重新啟動的用戶端。 然後使用用戶端通知動作來重新啟動它們。

> [!Tip]
> 啟用自動用戶端升級，能以更少的投入量，讓用戶端保持最新狀態。 如需詳細資訊，請參閱[關於自動用戶端升級](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)。

若要識別擱置重新啟動的裝置，請移至 Configuration Manager 主控台中的 [資產與相容性]  工作區，然後選取 [裝置]  節點。 然後在名為 [擱置重新啟動]  之新資料行的詳細資料窗格中，檢視每個裝置的狀態。 每個裝置都會有下列其中一或多個值：

- **否**：沒有擱置重新啟動
- **Configuration Manager**：這個值來自用戶端重新開機協調器元件 (RebootCoordinator.log)
- **檔案重新命名**：這個值來自 Windows，以回報擱置檔案重新命名作業 (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**：這個值來自 Windows Update Agent，以回報一或多個更新需要擱置重新啟動 (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **新增或移除功能**：這個值來自以 Windows 元件為基礎的服務，以回報新增或移除 Windows 功能需要重新啟動 (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

### <a name="create-the-client-notification-to-restart-a-device"></a>建立重新啟動裝置的用戶端通知

1. 在主控台的 [裝置集合]  節點中，選取您想要在集合內重新啟動的裝置。
2. 在功能區中，選取 [用戶端通知]  ，然後選取 [重新啟動]  。 即會開啟有關重新啟動的資訊視窗。 選取 [確定]  以確認重新啟動要求。

當通知抵達用戶端時，會開啟 [軟體中心]  通知視窗，以通知使用者有關重新啟動一事。 根據預設，將會在 90 分鐘後重新啟動。 您可以設定[用戶端設定](../deploy/configure-client-settings.md)，以修改重新啟動時間。 重新啟動行為的設定位於預設設定的[電腦重新啟動](../deploy/about-client-settings.md#computer-restart)索引標籤上。


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a> 設定用戶端快取

用戶端快取會儲存用戶端安裝應用程式和程式時所使用的暫存檔案。 軟體更新也會使用用戶端快取，但一律會嘗試下載至快取，而不論大小設定為何。 手動安裝用戶端時、使用用戶端推入安裝時，或安裝之後，設定快取設定 (例如大小和位置)。

您可以使用 Configuration Manager 主控台中用戶端設定來指定快取資料夾的大小。 如需詳細資訊，請參閱[用戶端快取設定](../deploy/about-client-settings.md#client-cache-settings)。

Configuration Manager 用戶端快取的預設位置為 `%windir%\ccmcache` 且預設磁碟空間為 5120 MB。  

> [!IMPORTANT]  
> 請不要加密用戶端快取所使用的資料夾。 Configuration Manager 無法下載內容至加密的資料夾。  

### <a name="about-the-client-cache"></a>關於用戶端快取  

Configuration Manager 用戶端會在收到部署後隨即下載所需軟體的內容，但是會等到部署排程的時間才執行。 Configuration Manager 用戶端會在排程的時間查看快取中是否有內容。 如果內容是在快取中且是正確的版本，則用戶端會使用此快取內容。 如果所需的內容版本變更，或用戶端刪除內容以將空間讓給另一個套件，則用戶端會再次將內容下載至快取。  

如果用戶端嘗試下載的程式或應用程式內容超過快取大小，部署就會因快取大小不足而失敗。 用戶端會產生狀態訊息 10050，指出快取大小不足。 如果您之後增加快取大小，則結果為：  

- 對於必要程式：用戶端不會自動重試下載內容。 將套件和程式重新部署至用戶端。  
- 對於必要應用程式：用戶端會在下載其用戶端原則時自動重試下載內容。  

如果用戶端嘗試下載的套件小於快取大小，但快取已滿，則所有「必要」  部署會繼續重試，直到：

- 有快取空間可用
- 下載逾時
- 重試計數達到其限制

如果您稍後增加快取大小，則用戶端會在下一個重試間隔期間再次嘗試下載套件。 用戶端每隔四個小時就會嘗試下載內容，直到嘗試達 18 次為止。  

快取的內容不會自動刪除。 在用戶端使用該內容之後，它至少會保留在快取中一天。 如果您設定套件內容時選擇將內容保存在用戶端快取中，用戶端就不會自動刪除該內容。 如果過去 24 小時內下載的套件使用快取空間，且用戶端必須下載新套件，則請增加快取大小或選擇刪除所保存快取內容的選項。  

利用下列程序在手動安裝用戶端期間或用戶端安裝後，設定用戶端快取。  

### <a name="configure-the-cache-during-manual-client-installation"></a>在手動用戶端安裝期間設定快取  

從安裝來源位置執行 CCMSetup.exe 命令，然後指定下列需要的內容，並以空格分隔：  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > 使用 Configuration Manager 主控台中 [用戶端設定]  提供的快取大小設定，而不是 SMSCACHESIZE。 如需詳細資訊，請參閱[用戶端快取設定](../deploy/about-client-settings.md#client-cache-settings)。

如需如何將這些命令列屬性用於 CCMSetup.exe 的詳細資訊，請參閱[關於用戶端安裝內容](../deploy/about-client-installation-properties.md)。

### <a name="configure-the-cache-during-client-push-installation"></a>在手動用戶端推入安裝期間設定快取  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。  

2. 選取適當的站台。 在功能區 [常用]  索引標籤的 [設定]  群組中，選取 [用戶端安裝設定]  ，然後選擇 [用戶端推入安裝]  。 切換至 [安裝內容]  索引標籤。  

3. 指定下列內容並以空格分隔：  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > 使用 Configuration Manager 主控台中 [用戶端設定]  提供的快取大小設定，而不是 SMSCACHESIZE。 如需詳細資訊，請參閱[用戶端快取設定](../deploy/about-client-settings.md#client-cache-settings)。

     如需如何將這些命令列屬性用於 CCMSetup.exe 的詳細資訊，請參閱[關於用戶端安裝內容](../deploy/about-client-installation-properties.md)。  

### <a name="configure-the-cache-on-the-client-computer"></a>設定用戶端電腦上的快取  

1. 在用戶端電腦上，開啟 **Configuration Manager** 控制台。  

2. 切換至 [快取]  索引標籤。設定空間和位置內容。 預設位置為 `%windir%\ccmcache`。  

3. 若要刪除快取資料夾中的檔案，請選擇 [刪除檔案]  。  

### <a name="configure-client-cache-size-in-client-settings"></a>在用戶端設定中設定用戶端快取大小

調整用戶端快取的大小，而不需要重新安裝用戶端。 使用 Configuration Manager 主控台中 [用戶端設定]  提供的快取大小設定。 如需詳細資訊，請參閱[用戶端快取設定](../deploy/about-client-settings.md#client-cache-settings)。


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a> 解除安裝用戶端

您可以使用 **CCMSetup.exe** 搭配 **/Uninstall** 屬性，從電腦中解除安裝 Configuration Manager 用戶端軟體。 在個別電腦上的命令提示字元中執行 CCMSetup.exe，或部署套件來解除安裝一組電腦集合的用戶端。  

> [!NOTE]  
> 您無法從行動裝置解除安裝 Configuration Manager 用戶端。 如果您必須從行動裝置移除 Configuration Manager 用戶端，則必須抹除裝置，這樣會刪除行動裝置上的所有資料。  

1. 以系統管理員的身分開啟 Windows 命令提示字元。 將資料夾變更為 CCMSetup.exe 所在的位置，例如：`cd %windir%\ccmsetup`

2. 執行下列命令：`CCMSetup.exe /uninstall`

> [!TIP]  
> 解除安裝程序不會在畫面上顯示任何結果。 若要驗證用戶端已成功解除安裝，請參閱下列記錄檔：`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> 如果您需要先等候解除安裝程序完成，再執行其他作業，請在 PowerShell 中執行 `Wait-Process CCMSetup`。 此命令可以暫停指令碼，直到 CCMSetup 程序完成為止。


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a> 管理衝突的記錄

Configuration Manager 使用硬體識別碼嘗試識別可能重複的用戶端，並發出衝突記錄的警示。 例如，如果您重新安裝電腦，硬體識別碼會相同，但 Configuration Manager 所使用的 GUID 可能會變更。  

Configuration Manager 會使用電腦帳戶的 Windows 驗證或來自受信任來源的 PKI 憑證，來自動解決衝突。 當 Configuration Manager 無法解決重複硬體識別碼的衝突時，階層設定可決定此行為。

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>變更管理衝突記錄的階層設定  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。

1. 在功能區中選取 [階層設定]  。

1. 切換至 [用戶端核准和衝突的記錄]  索引標籤，然後選取下列其中一個選項：

    - **自動解決衝突的記錄**
    - **手動解決衝突的記錄**

### <a name="manually-resolve-conflicting-records"></a>手動解決衝突的記錄  

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區，展開 [系統狀態]  ，然後選取 [衝突的記錄]  節點。  

1. 選取一或多個衝突的記錄，然後選擇 [衝突的記錄]  。  

1. 選取下列其中一個選項：  

    - **合併**：將新偵測到的記錄與現有用戶端記錄結合。  

    - **新增**：為衝突的用戶端記錄建立新記錄。  

    - **封鎖**：為衝突的用戶端記錄建立新記錄，但會將它標示為已封鎖。  


## <a name="manage-duplicate-hardware-identifiers"></a>管理重複的硬體識別碼

您可以提供一份硬體識別碼清單，讓 Configuration Manager 在 PXE 開機及用戶端註冊時略過這些識別碼。 這份清單有助於解決兩個常見問題：

1. 許多新裝置未包含上架的乙太網路埠。 技術人員會使用 USB 到乙太網路介面卡來建立進行作業系統部署的有線連線。 基於成本和一般使用性的考量，這些介面卡通常是共用的。 站台會使用此介面卡的 MAC 位址來識別裝置。 因此，在每個部署之間沒有其他系統管理員動作的情況下，重複使用介面卡會造成問題。 若要在此案例中重複使用介面卡，請排除其 MAC 位址。

2. 雖然 SMBIOS 屬性應該是唯一的，但有些專門硬體裝置有重複的識別碼。 排除這個重複的識別碼，並依賴每部裝置的唯一 MAC 位址。

使用下列處理序來新增 Configuration Manager 要略過的硬體識別碼：

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。

2. 在功能區 [常用]  索引標籤的 [站台]  群組中，選取 [階層設定]  。

3. 切換至 [用戶端核准和衝突的記錄]  索引標籤。若要新增硬體識別碼，請在 [重複硬體識別碼]  區段中選擇 [新增]  。

> [!TIP]
> 從 1910 版開始，使用下列 PowerShell Cmdlet 來自動化重複硬體識別碼的管理：<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a> 啟動原則抓取

Configuration Manager 用戶端會依照您設定的排程 (用戶端設定) 下載其用戶端原則。 您也可以從用戶端啟動隨選原則抓取。 例如，用於疑難排解或測試的情況。  

- [用戶端通知](#bkmk_policy-notify)
- [用戶端控制台](#bkmk_policy-manual)
- [支援中心](#bkmk_policy-support)
- [指令碼](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a> 使用用戶端通知來啟動用戶端原則抓取  

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，然後選取 [裝置]  。  

1. 選取要下載原則的裝置。 在功能區 [常用]  索引標籤的 [裝置]  群組中，選取 [用戶端通知]  ，然後選擇 [下載電腦原則]  。  

    > [!NOTE]  
    > 您也可以使用用戶端通知，以針對集合中的所有裝置啟動原則抓取。  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a> 從 Configuration Manager 用戶端控制台啟動用戶端原則抓取

1. 在電腦上開啟 **Configuration Manager** 控制台。  

2. 切換至 [動作]  索引標籤。選取 [電腦原則抓取和評估週期]  來啟動電腦原則，然後選取 [立即執行]  。  

3. 選取 [確定]  確認提示。  

4. 針對任何其他動作重複上述步驟。 例如，針對使用者用戶端設定的 [電腦原則抓取和評估週期]  。  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a> 使用支援中心來啟動用戶端原則抓取

使用支援中心來要求和檢視用戶端原則。 如需詳細資訊，請參閱[支援中心參考](../../support/support-center-ui-reference.md#bkmk_support-policy)。

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a> 透過指令碼啟動用戶端原則抓取  

1. 開啟指令碼編輯器，例如 [記事本] 或 Windows PowerShell ISE。  

2. 複製下列 PowerShell 程式碼範例並插入<!-- SCCMDocs#1591 --> 至檔案：  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > 如需排程識別碼的詳細資訊，請參閱[訊息識別碼](../../support/send-schedule-tool.md#bkmk_sendschedule-guids)。

3. 以副檔名 .ps1 儲存檔案。  

4. 在用戶端上執行指令碼。
