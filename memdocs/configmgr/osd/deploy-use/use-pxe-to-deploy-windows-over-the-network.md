---
title: 透過網路使用 PXE 進行 OSD
titleSuffix: Configuration Manager
description: 使用 PXE 起始的 OS 部署來重新整理電腦的作業系統，或在新電腦上安裝新的 Windows 版本。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11045ff31dc3832ac97d62f491561b3cf989813c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079343"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>利用 Configuration Manager 透過網路使用 PXE 來部署 Windows

適用於：  Configuration Manager (最新分支)

Configuration Manager 中開機前執行環境 (PXE) 起始的 OS 部署，可讓用戶端透過網路要求與部署作業系統。 在此部署案例中，您會將 OS 映像和開機映像傳送到支援 PXE 的發佈點。

> [!NOTE]  
> 當您建立僅以 x64 BIOS 電腦為目標的 OS 部署時，x64 開機映像和 x86 開機映像在發佈點上都必須為可用狀態。

您可以在下列案例中使用 PXE 起始的 OS 部署：

- [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

完成任一 OS 部署案例中的步驟，然後使用本文各節的內容來準備 PXE 起始的部署。

> [!WARNING]
> 如果您使用 PXE 部署，並以網路介面卡作為第一個開機裝置來設定裝置硬體，則這些裝置就可以自動啟動 OS 部署工作順序，而不需要使用者互動。 部署驗證不會管理此設定。 雖然此設定可以簡化處理程序並減少使用者互動，但會將裝置置於意外重新安裝映像的更高風險中。

## <a name="configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> 將至少一個發佈點設定為接受 PXE 要求

若要將作業系統部署至發出 PXE 開機要求的 Configuration Manager 用戶端，您必須設定一或多個發佈點來接受 PXE 要求。 在您設定發佈點之後，該發佈點會回應 PXE 開機要求，並判斷要採取的適當部署動作。 如需詳細資訊，請參閱[安裝或修改發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。  

> [!NOTE]  
> 設定支援 PXE 的單一發佈點來支援多個子網路時，不支援使用 DHCP 選項。 在路由器上設定 IP 協助程式，可將 PXE 要求轉送到支援 PXE 的發佈點。
>
> 在 1810 版中，如果也在執行 DHCP 伺服器的伺服器上沒有 WDS，就不支援使用 PXE 回應程式。
>
> 從 1902 版開始，當您在發佈點上啟用 PXE 回應程式而不需要 Windows 部署服務時，它現在可位於與 DHCP 服務相同的伺服器上。<!--3734270, SCCMDocs-pr #3416--> 新增下列設定，以支援此設定：  
>
> - 在下列登錄機碼中將 DWord 值 **DoNotListenOnDhcpPort** 設定為 `1`：`HKLM\Software\Microsoft\SMS\DP`。
> - 將 DHCP 選項 60 設定為 `PXEClient`。  
> - 在伺服器上重新啟動 SCCMPXE 和 DHCP 服務。  

## <a name="prepare-a-pxe-enabled-boot-image"></a>準備啟用 PXE 的開機映像

若要使用 PXE 來部署 OS，您必須擁有 x86 和 x64 的支援 PXE 開機映像，以發佈到一或多個支援 PXE 的發佈點。 使用資訊在開機映像上啟用 PXE，並將開機映像發佈到發佈點：

- 若要在開機映像上啟用 PXE，請從開機映像內容中的 [資料來源]  索引標籤，選取 [從支援 PXE 的發佈點部署此開機映像]  。

- 如果您變更開機映像的內容，請更新開機映像並將它重新發佈至發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

## <a name="manage-duplicate-hardware-identifiers"></a>管理重複的硬體識別碼

如果多部電腦具有重複的 SMBIOS 屬性，或您使用共用的網路介面卡，則 Configuration Manager 可能會將它們辨識為相同裝置。 藉由在階層設定中管理重複的硬體識別碼來緩解這些問題。 如需詳細資訊，請參閱[管理重複的硬體識別碼](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)。

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> 建立 PXE 部署的排除清單

> [!Note]  
> 在某些情況下，[管理重複硬體識別碼](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)的程序可能比較容易。<!-- SCCMDocs issue 802 -->
>
> 每個行為在某些情況可能會造成不同結果。 不論在任何情況下，排除清單永遠不會將具有所列 MAC 位址的用戶端開機。
>
> 重複識別碼清單不會使用 MAC 來尋找用戶端的工作順序原則。 如果它符合 SMBIOS 識別碼，或如果有未知機器的工作順序原則，則用戶端仍會開機。

當您使用 PXE 部署作業系統時，可以在每個發佈點上建立排除清單。 將要發佈點忽略之電腦的 MAC 位址新增到排除清單。 清單中的電腦不會接收 Configuration Manager 用來進行 PXE 部署的部署工作順序。

### <a name="process-to-create-the-exclusion-list"></a>建立排除清單的程序

1. 在啟用 PXE 的發佈點上建立文字檔。 例如，將此文字檔命名為 **pxeExceptions.txt**。  

2. 使用純文字編輯器 (像是記事本)，並新增要讓啟用 PXE 的發佈點忽略的電腦 MAC 位址。 以分號分隔 MAC 位址值，且一行輸入一個位址。 例如：`01:23:45:67:89:ab`  

3. 將文字檔儲存在啟用 PXE 的發佈點站台系統伺服器上。 文字檔可以儲存到伺服器上的任何位置。  

4. 編輯啟用 PXE 之發佈點的登錄，以建立 **MACIgnoreListFile** 登錄機碼。 將文字檔之完整路徑的字串值新增至啟用 PXE 的發佈點站台系統伺服器上。 使用下列登錄路徑：  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > 如果您不正確使用 [登錄編輯程式]，可能造成嚴重的問題，而需要重新安裝 Windows。 Microsoft 無法保證您可以解決因不正確使用登錄編輯程式所造成的問題。 您需自行承擔使用登錄編輯程式的風險。  

5. 進行這項登錄變更後，請重新啟動 WDS 服務或 PXE 回應者服務。 您不需要將伺服器重新開機。<!--512129-->  

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a> RamDisk TFTP 區塊大小和視窗大小

您可以針對支援 PXE 的發佈點自訂 RamDisk TFTP 區塊和視窗大小。 如果您已自訂網路，大型區塊或視窗大小可能會導致開機映像下載因發生逾時錯誤而失敗。 藉由自訂 RamDisk TFTP 區塊和視窗大小，可讓您在使用 PXE 來滿足特定網路需求時，將 TFTP 流量最佳化。 若要判斷哪一個設定最有效率，請在您的環境中測試自訂設定。 如需詳細資訊，請參閱[自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊大小和視窗大小](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)。

## <a name="configure-deployment-settings"></a>設定部署設定

若要使用 PXE 起始的 OS 部署，請設定部署，讓 OS 適用於 PXE 開機要求。 在部署內容的 [部署設定]  索引標籤上，設定可用的作業系統。 如果是 [Make available to the following]  \(供下列項目使用\) 設定，請選取下列其中一個選項：

- Configuration Manager 用戶端、媒體與 PXE

- 僅媒體與 PXE

- 僅媒體與 PXE (隱藏)

## <a name="option-82-during-pxe-dhcp-handshake"></a>PXE DHCP 交握期間的選項 82
從 1906 版開始，不含 WDS 的 PXE 回應程式支援 PXE DHCP 交握期間的選項 82。 如果需要選項 82，請務必使用不含 WDS 的 PXE 回應程式。 WDS 不支援選項 82。

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> 部署工作順序

將 OS 部署到目標集合。 如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md)。 當您使用 PXE 部署作業系統時，可設定部署是否為需要部署或是提供進行部署。

- **必要的部署**：必要的部署會使用 PXE，完全不需要任何使用者介入。 使用者無法略過 PXE 開機。 不過，如果使用者在發佈點回應之前取消 PXE 開機，就不會部署 OS。

- **可用的部署**：可用的部署會要求使用者必須親自到目的地電腦操作。 使用者必須按下 **F12** 鍵以繼續進行 PXE 開機程序。 如果使用者不在電腦端，無法按下 **F12** 鍵，電腦就會開機到目前的 OS，或從下一個可用開機裝置開機。

您可以藉由清除指派到 Configuration Manager 集合或電腦的最後一個 PXE 部署狀態，重新部署必要的 PXE 部署。 如需**清除必要的 PXE 部署**動作的詳細資訊，請參閱[管理用戶端](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode)或[管理集合](../../core/clients/manage/collections/manage-collections.md#bkmk_device)。 此動作會重設該部署的狀態，並重新安裝最新的必要部署。

> [!IMPORTANT]  
> PXE 通訊協定不安全。 請確認 PXE 伺服器及 PXE 用戶端皆位於實體上安全的網路，例如位於資料中心可防止對於您站台的未授權存取。

## <a name="how-the-boot-image-is-selected-for-pxe"></a>如何為 PXE 選取開機映像

用戶端使用 PXE 開機時，Configuration Manager 會將要使用的開機映像提供給用戶端。 Configuration Manager 會使用具有完全相符架構的開機映像。 如果找不到具有完全相符架構的開機映像，Configuration Manager 會使用具有相容架構的開機映像。

下列清單提供如何為使用 PXE 開機的用戶端選取開機映像的詳細資料：  

1. Configuration Manager 會查看站台資料庫中是否有系統記錄符合嘗試開機的用戶端的 MAC 位址或 SMBIOS。  

    > [!NOTE]  
    > 如果指派給站台的電腦會開機至不同站台的 PXE，就不會顯示適用於該電腦的原則。 例如，如果已經將用戶端指派給站台 A，站台 B 的管理點和發佈點就無法存取站台 A 的原則，而用戶端就不會成功進行 PXE 開機。  

2. Configuration Manager 會尋找部署至步驟 1 中所找到之系統記錄的工作順序。  

3. 在步驟 2 中找到的工作順序清單中，Configuration Manager 會尋找符合嘗試開機的用戶端架構的開機映像。 如果找到相同架構的開機映像，則會使用該開機映像。  

    如果找到一個以上的開機映像，則會使用「最高」  或最新的工作順序部署識別碼。 在多站台階層的情況下，「較高」  字母站台在字串比較中會有較高優先順序。 例如，如果它們都符合，則系統會選擇來自站台 ZZZ 的一年前部署，而不是來自站台 AAA 昨天的部署。<!-- SCCMDocs issue 877 -->  

4. 如果找不到具有相同架構的開機映像，Configuration Manager 會尋找與用戶端架構相容的開機映像。 系統會在步驟 2 中的工作順序清單中尋找。 例如，64 位元 BIOS/MBR 用戶端與 32 位元和 64 位元開機映像相容。 32 位元 BIOS/MBR 用戶端僅與 32 位元開機映像相容。 UEFI 用戶端僅與符合的架構相容。 64 位元 UEFI 用戶端僅相容於 64 位元開機映像，而 32 位元 UEFI 用戶端僅相容於 32 位元開機映像。
