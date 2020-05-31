---
title: 用戶端設計
titleSuffix: Configuration Manager
description: 了解控制用戶端行為的預設和自訂設定
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 127ed43fded6c66bc4395ae4d69a28ae8c9eddd5
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877514"
---
# <a name="about-client-settings-in-configuration-manager"></a>關於 Configuration Manager 中的用戶端設定

適用於：Configuration Manager (最新分支)

從 [系統管理] 工作區的 [用戶端設定] 節點中，管理 Configuration Manager 主控台中的所有用戶端設定。 Configuration Manager 會提供一組預設設定。 當您變更預設用戶端設定時，這些設定會套用至階層中的所有用戶端。 您也可以設定自訂用戶端設定，當您將它們指派給集合時，便會覆寫預設用戶端設定。 如需詳細資訊，請參閱[如何設定用戶端設定](configure-client-settings.md)。

下列各節將進一步詳細說明設定和選項。  


## <a name="background-intelligent-transfer-service-bits"></a>背景智慧型傳送服務 (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>限制 BITS 背景傳送的最大網路頻寬

此選項為 [是] 時，用戶端會使用 BITS 頻寬節流設定。 若要設定此群組中的其他設定，您必須啟用此設定。

### <a name="throttling-window-start-time"></a>節流時段開始時間

指定本機 BITS 節流時段的開始時間。  

### <a name="throttling-window-end-time"></a>節流時段結束時間

指定本機 BITS 節流時段的結束時間。 如果結束時間與**節流時段開始時間**相同，則一律會啟用 BITS 節流。  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>節流時段的最大傳輸速率 (Kbps)

指定用戶端於節流時段內可以使用的最大傳輸速率。  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>允許在節流時段以外進行 BITS 下載

允許用戶端在指定的時段之外使用獨立的 BITS 設定。  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>節流時段以外的最大傳輸速率 (Kbps)

指定用戶端可在 BITS 節流時段之外使用的最大傳輸速率。  



## <a name="client-cache-settings"></a>用戶端快取設定

### <a name="configure-branchcache"></a>設定 BranchCache

針對 [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
) 設定用戶端電腦。 若要允許 BranchCache 在用戶端上進行快取，請將 [啟用 BranchCache] 設定為 [是]。

- **啟用 BranchCache**：在用戶端電腦上啟用 BranchCache。

- **BranchCache 快取大小上限 (磁碟百分比)** ：您允許 BranchCache 使用之磁碟的百分比。

> [!TIP]
> 如果您將 [設定 BranchCache] 設定為 [否]，Configuration Manager 便無法設定任何 BranchCache 設定。
>
> 若要停用 BranchCache，請將 [設定 BranchCache] 設定為 [是]，然後將 [啟用 BranchCache] 設定為 [否]。<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>設定用戶端快取大小

Windows 電腦上的 Configuration Manager 用戶端快取會儲存用於安裝應用程式和程式的暫存檔案。 如果將此選項設為 [否]，則預設大小為 5,120 MB。

如果您選擇 [是]，接著指定：

- **最大快取大小 (MB)**
- **快取大小上限 (磁碟百分比)** ：用戶端快取大小會以 MB 或磁碟百分比為單位 (以較低者為準) 擴充至最大大小。

### <a name="enable-as-peer-cache-source"></a>啟用為對等快取來源

> [!Note]  
> 在 1902 版和較早版本中，此設定的名稱為**在完整作業系統中啟用 Configuration Manager 用戶端以共用內容**。 此設定的行為不會變更。

針對 Configuration Manager 用戶端啟用[對等快取](../../plan-design/hierarchy/client-peer-cache.md)。 選擇 [是]，然後指定用戶端要透過它來與對等電腦通訊的連接埠。

- **用於初始網路廣播的連接埠** (預設值為 UDP 8004)：Configuration Manager 會在 Windows PE 或完整 Windows OS 中使用此連接埠。 Windows PE 中的工作順序引擎會在啟動工作順序之前傳送廣播以取得內容位置。<!--SCCMDocs issue 910-->

- **用於從對等下載內容的連接埠** (預設值為 TCP 8003)：Configuration Manager 會自動設定 Windows 防火牆規則以允許此流量。 如果您使用不同的防火牆，則必須手動設定規則以允許此流量。  

    如需詳細資訊，請參閱[用於連線的連接埠](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp)。  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>可移除快取內容之前的持續時間下限 (分鐘)

<!--4485509-->
從 1906 版開始，請指定 Configuration Manager 用戶端保留快取內容的時間下限。 此用戶端設定定義 Configuration Manager 代理程式在將內容從快取中移除之前應等候的最小時間量。

此值預設為 1,440 分鐘 (24 小時)。
此設定的最大值是 10,080 分鐘 (1 周)。

此設定可讓您進一步控制不同類型裝置上的用戶端快取。 您可以在具有小型硬碟且不需要在執行其他部署之前保留現有內容的用戶端上，降低該值。


## <a name="client-policy"></a>用戶端原則  

### <a name="client-policy-polling-interval-minutes"></a>用戶端原則輪詢間隔 (分鐘)

指定下列 Configuration Manager 用戶端下載用戶端原則的頻率：

- Windows 電腦 (例如，桌上型電腦、伺服器、膝上型電腦)  
- Configuration Manager 註冊的行動裝置  
- Mac 電腦  
- 執行 Linux 或 UNIX 的電腦  

此值預設為 60 分鐘。 減少此值可能會導致用戶端更頻繁地對站台進行輪詢。 對於許多用戶端而言，此行為可能會對網站效能產生負面影響。 [大小和縮放比例指引](../../plan-design/configs/size-and-scale-numbers.md)是以預設值為基礎。 增加此值可能會導致用戶端較不頻繁地對站台進行輪詢。 任何針對用戶端原則的變更 (包括新部署)，都會使用戶端需要花費更長的時間來下載和處理。<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>在用戶端上啟用使用者原則

當您將此選項設為 [是] 並使用[使用者探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)時，則用戶端會接收以登入使用者為目標的應用程式和程式。  

如果此設定為 [否]，使用者就不會收到您部署至使用者的必要應用程式。 使用者也不會收到使用者原則中的任何其他管理工作。  

當使用者的電腦位於內部網路或網際網路時，即適用此設定。 如果您也想要啟用網際網路上的使用者原則，它必須為 [是]。  

> [!Note]  
> 從 1906 版開始，已更新的用戶端會自動使用使用者可用應用程式部署的管理點。 您無法安裝新的應用程式目錄角色。
>
> 如果您仍會使用應用程式目錄，則它會從站台伺服器接收使用者可用的軟體清單。 因此，此設定不需為 [是]，使用者就可以從應用程式目錄查看和要求應用程式。 如果此設定為 [否]，使用者就無法安裝他們在應用程式目錄中看到的應用程式。  

### <a name="enable-user-policy-requests-from-internet-clients"></a>從網際網路用戶端啟用使用者原則要求

將此選項設為 [是]，讓使用者接收以網際網路為基礎之電腦上的使用者原則。 也會套用下列需求：  

- 用戶端和站台會設定來進行[以網際網路為基礎的用戶端管理](../manage/plan-internet-based-client-management.md)或[雲端管理閘道](../manage/cmg/plan-cloud-management-gateway.md)。  

- [在用戶端上啟用使用者原則] 設定為 [是]。  

- 以網際網路為基礎的管理點會使用 Windows 驗證 (Kerberos 或 NTLM) 成功驗證使用者。 如需詳細資訊，請參閱[來自網際網路的用戶端通訊考量](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

- 雲端管理閘道可藉由使用 Azure Active Directory 成功驗證使用者。 如需詳細資訊，請參閱[在已加入 Azure AD 的裝置上部署使用者可用的應用程式](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)。  

如果您將此選項設為 [否]，或不符合任何先前的需求，則網際網路上的電腦只會接收電腦原則。 在此案例中，使用者仍可從網際網路型應用程式目錄中查看、要求及安裝應用程式。 如果此設定為 [否]，但 [在用戶端上啟用使用者原則] 為 [是]，則除非電腦連線至內部網路，否則使用者無法接收使用者原則。  

> [!NOTE]  
> 針對以網際網路為基礎的用戶端管理，使用者的應用程式核准要求並不需要使用者原則或使用者驗證。 雲端管理閘道不支援應用程式核准要求。  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>啟用多個使用者工作階段的使用者原則

<!--4737447-->

*適用於 1910 版*

根據預設，此設定為停用。 從 1906 版開始，即使啟用使用者原則，用戶端仍會根據預設在允許多個並行作用中使用者工作階段的任何裝置上將其停用。 例如 [Windows 虛擬桌面](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)中的終端機伺服器或 Windows 10 企業版多工作階段。

用戶端只會在新安裝期間偵測到這類裝置時停用使用者原則。 針對更新到 1906 版後的此類型現有用戶端，仍會保存先前的行為。 在現有裝置上，即使偵測到裝置允許多個使用者工作階段，也會設定使用者原則設定。

如果您在此案例中需要使用者原則，並接受任何潛在的效能影響，請啟用此用戶端設定。


## <a name="cloud-services"></a>雲端服務

### <a name="allow-access-to-cloud-distribution-point"></a>允許存取雲端發佈點

將此選項設為 [是]，讓用戶端從雲端發佈點取得內容。 此設定不需要裝置是以網際網路為基礎的。

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>自動向 Azure Active Directory 註冊新加入 Windows 10 網域的裝置

當您設定 Azure Active Directory 以支援混合式加入時，Configuration Manager 會針對這項功能設定 Windows 10 裝置。 如需詳細資訊，請參閱[如何設定加入混合式 Azure Active Directory 的裝置](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)。

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>允許用戶端使用雲端管理閘道

根據預設，所有網際網路漫遊用戶端都會使用任何可用的[雲端管理閘道](../manage/cmg/plan-cloud-management-gateway.md)。 何時將此設定設為 [否] 的範例是限定服務的使用量，例如在試驗專案期間或節省成本。



## <a name="compliance-settings"></a>相容性設定  

### <a name="enable-compliance-evaluation-on-clients"></a>啟用用戶端上的合規性評估

將此選項設為 [是]，以設定此群組中的其他設定。

### <a name="schedule-compliance-evaluation"></a>排程合規性評估

選取 [排程]，以建立設定基準部署的預設排程。 此值可以在 [部署設定基準] 對話方塊中，針對每個基準進行設定。  

### <a name="enable-user-data-and-profiles"></a>啟用使用者資料和設定檔

如果您想要部署[使用者資料和設定檔](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md)設定項目，請選擇 [是]。



## <a name="computer-agent"></a>電腦代理程式  

### <a name="user-notifications-for-required-deployments"></a>必要部署的使用者通知

如需下列三個設定的詳細資訊，請參閱[必要部署的使用者通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)：

- **部署期限超過 24 小時，每隔下列時間通知使用者 (小時)**
- **部署期限不到 24 小時，每隔下列時間提醒使用者 (小時)**
- **部署期限不到 1 小時，每隔下列時間提醒使用者 (分鐘)**

### <a name="default-application-catalog-website-point"></a>預設應用程式類別目錄網站點

> [!Important]  
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager 會使用此設定，從軟體中心將使用者連線至應用程式目錄。 選取 [設定網站]，以指定裝載應用程式目錄網站點的伺服器。 輸入其 NetBIOS 名稱或 FQDN、指定自動偵測，或指定自訂部署的 URL。 在大部分情況下，自動偵測是最佳選擇。

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>將預設應用程式類別目錄網站新增至 Internet Explorer 的信任的網站區域

> [!Important]  
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

如果此選項為 [是]，則用戶端會自動將目前的預設應用程式目錄網站 URL 新增至 Internet Explorer 信任的網站區域。  

此設定可確保不啟用受保護模式的 Internet Explorer 設定。 如果已啟用受保護模式，Configuration Manager 用戶端可能無法從應用程式目錄安裝應用程式。 根據預設，信任的網站區域也支援使用者登入應用程式目錄，此動作需要進行 Windows 驗證。  

如果您將此選項保留為 [否]，Configuration Manager 用戶端可能無法從應用程式目錄安裝應用程式。 替代方法是針對用戶端使用的應用程式目錄 URL，在另一個區域設定這些 Internet Explorer 設定。  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>允許 Silverlight 應用程式在更高的信任模式下執行

> [!Important]  
> 用戶端不會自動安裝 Silverlight。
>
> 從 1806 版開始，不再支援應用程式類別目錄網站點的 **Silverlight 使用者體驗**。 使用者應該使用新的軟體中心。 如需詳細資訊，請參閱[設定軟體中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)。  

此設定必須為 [是]，使用者才能使用應用程式目錄。  

如果您變更此設定，此設定會在使用者下一次載入瀏覽器或重新整理目前開啟的瀏覽器視窗時生效。  

如需此設定的詳細資訊，請參閱[應用程式類別目錄需要 Microsoft Silverlight 5 憑證和更高的信任模式](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5)。  

### <a name="organization-name-displayed-in-software-center"></a>顯示於軟體中心的組織名稱

輸入使用者會在軟體中心看到的名稱。 此商標資訊可協助使用者將此應用程式識別為信任的來源。 如需此設定之優先順序的詳細資訊，請參閱[設定軟體中心商標](../../../apps/plan-design/plan-for-software-center.md#branding-software-center)。  

### <a name="use-new-software-center"></a>使用新的軟體中心

預設值為 [是]。

當您將此選項設為 [是] 時，所有用戶端電腦都會使用軟體中心。 軟體中心會顯示您部署至使用者或裝置的軟體、軟體更新和工作順序。

### <a name="enable-communication-with-health-attestation-service"></a>啟用與健康情況證明服務之間的通訊

將此選項設為 [是]，讓 Windows 10 裝置使用[健康情況證明](../../servers/manage/health-attestation.md)。 當您啟用此設定時，也可以進行下列設定。

### <a name="use-on-premises-health-attestation-service"></a>使用內部部署健康情況證明服務

將此選項設為 [是]，讓裝置使用內部部署服務。 設為 [否]，讓裝置使用 Microsoft 雲端式服務。  

### <a name="install-permissions"></a>安裝權限

設定使用者如何安裝軟體、軟體更新和工作順序：  

- **所有使用者**：具有「來賓」以外之任何權限的使用者。  

- **僅系統管理員**：使用者必須是本機系統管理員群組中的成員。  

- **僅系統管理員和主要使用者**：使用者必須是本機系統管理員群組的成員或電腦的主要使用者。  

- **無使用者**：登入用戶端電腦的使用者皆無法安裝軟體、軟體更新和工作順序。 電腦的必要部署一律會在期限安裝。 使用者無法從軟體中心安裝軟體。  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>重新啟動時暫停輸入 BitLocker PIN

如果電腦需要 BitLocker PIN 項目，則此選項會在軟體安裝後重新啟動電腦時，略過輸入 PIN 的需求。  

- **永遠**：Configuration Manager 在安裝需要重新啟動的軟體並起始電腦的重新啟動後，會短暫地暫止 BitLocker。 此設定只適用於 Configuration Manager 所起始的電腦重新啟動。 使用者重新啟動電腦時，此設定不會暫停輸入 BitLocker PIN 的需求。 BitLocker PIN 輸入需求會在 Windows 啟動後繼續作用。

- **永不**：Configuration Manager 在安裝需要重新啟動的軟體後，不會暫止 BitLocker。 在此案例中，除非使用者輸入 PIN 完成標準啟動程序及載入 Windows，否則無法完成軟體安裝。

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>其他軟體會管理應用程式和軟體更新的部署

只有在下列其中一個條件成立時，才能啟用此選項：  

- 您可以使用需要啟用此設定的廠商解決方案。  

- 您可以使用 Configuration Manager 軟體部署套件 (SDK) 來管理用戶端代理程式通知，以及應用程式和軟體更新的安裝。  

> [!WARNING]  
> - 如果您在任一條件都不成立時選擇此選項，則用戶端不會安裝軟體更新和必要的應用程式。 此設定不會防止使用者從軟體中心安裝可用的軟體，包括應用程式、套件和工作順序。  
> -  當您啟用此設定時，用戶端上不會顯示新軟體或必要軟體的快顯通知。 <!--6347668-->

### <a name="powershell-execution-policy"></a>PowerShell 執行原則

設定 Configuration Manager 用戶端執行 Windows PowerShell 指令碼的方式。 您可能會使用這些指令碼來偵測設定項目的合規性設定。 您可能也會在部署中傳送指令碼作為標準指令碼。  

- **略過**：Configuration Manager 用戶端會略過用戶端電腦上的 Windows PowerShell 設定，使得未經簽署的指令碼得以執行。  

- **受限制**：Configuration Manager 用戶端會使用用戶端電腦上目前的 PowerShell 設定。 此設定會判斷是否可以執行未經簽署的指令碼。  

- **所有已簽署項目**：Configuration Manager 用戶端只會執行經由受信任發行者簽署的指令碼。 此限制與用戶端電腦上目前的 PowerShell 設定無關。  

此選項至少需要 Windows PowerShell 2.0 版。 預設值為 [所有已簽署項目]。  

> [!TIP]  
> 如果未經簽署的指令碼因為此項用戶端設定而無法執行，Configuration Manager 會透過下列方式回報此錯誤：  
>
> - 主控台中的 [監視] 工作區會顯示部署狀態錯誤識別碼 **0x87D00327**。 它也會顯示**未簽署指令碼**的描述。  
> - 報表會顯示**探索錯誤**的錯誤類型。 接著，報表會顯示錯誤碼 **0x87D00327** 和**未簽署指令碼**的描述，或錯誤碼 **0x87D00320** 和**尚未安裝指令碼裝載**的描述。 報告的範例為：**資產的設定基準中設定項目的錯誤詳細資料**。  
> - **DcmWmiProvider.log** 檔案會顯示**未簽署指令碼 (錯誤:87D00327; 來源:CCM)** 訊息。  

### <a name="show-notifications-for-new-deployments"></a>針對新部署顯示通知

選擇 [是]，針對提供尚未滿一週的部署顯示通知。 此訊息會在每次用戶端代理程式啟動時出現。

### <a name="disable-deadline-randomization"></a>停用期限隨機設定

在達到部署期限之後，此設定會判斷用戶端是否使用最多兩個小時的啟用延遲來安裝必要的軟體更新。 預設會停用啟用延遲功能。  

對於虛擬桌面基礎結構 (VDI) 案例，此延遲有助於分散 CPU 處理，以及具有多個虛擬機器之主機電腦的資料傳送。 即使您未使用 VDI，擁有許多同時安裝相同更新的用戶端，可能會大幅增加站台伺服器上的 CPU 使用量。 此行為也會讓發佈點速度變慢，以及大幅降低可用的網路頻寬。  

如果用戶端必須在部署期限安裝必要軟體更新，而且沒有延遲，則請將此設定設為 [是]。

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>延後到部署期限後施行的寬限期 (小時)

如果您想要為使用者提供更多時間，以在超過期限後還能安裝必要的應用程式或軟體更新部署，請設定此選項的值。 此寬限期適用於已關閉一段時間的電腦，而且使用者需要安裝許多應用程式或更新部署。 例如，如果使用者從假期歸來，而且必須等候很長的時間，讓用戶端安裝逾期的應用程式部署時，此設定就很實用。

設定 0 到 120 小時的寬限期。 此設定是與 [根據使用者偏好設定，延遲強制施行此部署] 部署內容搭配使用。 如需詳細資訊，請參閱[部署應用程式](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period)。


## <a name="computer-restart"></a>電腦重新啟動

下列設定的持續時間必須比套用至電腦的最短維護視窗還要短：

- **向使用者顯示短暫的通知，指出使用者登出或電腦重新啟動之前的間隔 (分鐘)**
- **顯示使用者無法關閉的對話方塊，其中顯示使用者登出或電腦重新啟動之前的倒數計時間隔 (分鐘)**


如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../manage/collections/use-maintenance-windows.md)。

- **指定電腦重新啟動倒數通知的延遲持續時間 (小時)** (從 1906 版開始)<!--3976435-->
  - 預設值為 240 分鐘。
  - 延遲持續時間值應小於暫時通知值減去使用者無法關閉的通知值。
  - 如需詳細資訊，請參閱[裝置重新啟動通知](device-restart-notifications.md)。

**部署必須重新啟動時，將對使用者顯示快顯通知改為顯示對話視窗**<!--3555947-->:從 1902 版開始，將此設定設為 [是] 會將使用者體驗變更為更具提示效果。 此設定適用於所有應用程式、工作順序及軟體更新的部署。 如需詳細資訊，請參閱[針對軟體中心進行規劃](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)。

> [!IMPORTANT]
> 在 Configuration Manager 1902 中，在某些情況下，對話方塊將不會取代快顯通知。 若要解決此問題，請安裝 [Configuration Manager 1902 的更新彙總套件](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->


## <a name="delivery-optimization"></a>傳遞最佳化 

<!-- 1324696 -->
您可以使用 Configuration Manager 界限群組，來定義和規範在您的公司網路上以及到遠端辦公室的內容發佈。 [Windows 傳遞最佳化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)是一種雲端式點對點技術，可在 Windows 10 裝置之間共用內容。 請設定讓「傳遞最佳化」在於同儕節點之間共用內容時，使用您的界限群組。

> [!Note]
> - 傳遞最佳化僅適用於 Windows 10 用戶端。
> - 若要使用「傳遞最佳化」的點對點功能，必須要能透過網際網路連線至「傳遞最佳化」雲端服務。 如需所必要網際網路端點的資訊，請參閱[傳遞最佳化的常見問題集](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。
> - 針對內容儲存體使用 CMG 時，如果已啟用 [下載可用的差異內容] [用戶端設定](#allow-clients-to-download-delta-content-when-available)，第三方更新的內容將不會下載至用戶端。 <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>針對傳遞最佳化群組識別碼使用 Configuration Manager 界限群組

選擇 [是] 以套用界限群組識別碼作為用戶端上的傳遞最佳化群組識別碼。 當用戶端與傳遞最佳化雲端服務進行通訊時，它會使用此識別碼來尋找含有所需內容的同儕節點。 啟用此設定也會在目標用戶端上，將傳遞最佳化下載模式設定為 [群組 (2)] 選項。

> [!Note]
> Microsoft 建議允許用戶端透過本機原則 (而非群組原則) 進行此設定。 此設定可允許將界限群組識別碼設為用戶端上的傳遞最佳化群組識別碼。 如需詳細資訊，請參閱[傳遞最佳化](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)。

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>允許 Configuration Manager 管理的裝置使用 Microsoft 已連線快取伺服器來下載內容

<!--3555764-->
選擇 [是] 以允許用戶端從內部部署發佈點下載內容，而您可以將其啟用為 Microsoft 已連線快取伺服器。 如需詳細資訊，請參閱 [Configuration Manager 中的 Microsoft 連線快取](../../plan-design/hierarchy/microsoft-connected-cache.md)。


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> 除了下列資訊之外，您還可以在[範例案例：使用 Endpoint Protection 保護電腦免受惡意程式碼的威脅](../../../protect/deploy-use/scenarios-endpoint-protection.md)中找到有關使用 Endpoint Protection 用戶端設定的詳細資料。

### <a name="manage-endpoint-protection-client-on-client-computers"></a>在用戶端電腦上管理 Endpoint Protection 用戶端

如果您想在階層的電腦上管理現有 Endpoint Protection 和 Windows Defender 用戶端，請選擇 [是]。  

如果您已安裝 Endpoint Protection 用戶端，且想要使用 Configuration Manager 進行管理，請選擇此選項。 這個個別安裝包含使用 Configuration Manager 應用程式或套件和程式的已編寫指令碼程序。 Windows 10 裝置不需要安裝 Endpoint Protection 代理程式。 不過，那些裝置將仍需要啟用 [在用戶端電腦上管理 Endpoint Protection 用戶端]。 <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>在用戶端電腦上安裝 Endpoint Protection 用戶端

選擇 [是]，在尚未執行用戶端的用戶端電腦上安裝並啟用 Endpoint Protection 用戶端。 Windows 10 用戶端不需要安裝 Endpoint Protection 代理程式。  

> [!NOTE]  
> 如果已安裝 Endpoint Protection 用戶端，則選擇 [否] 不會解除安裝 Endpoint Protection 用戶端。 若要解除安裝 Endpoint Protection 用戶端，請將 [在用戶端電腦上管理 Endpoint Protection 用戶端] 用戶端設定設定為 [否]。 然後部署套件和程式以解除安裝 Endpoint Protection 用戶端。  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>允許在維護期間以外安裝 Endpoint Protection 用戶端並重新啟動。 用戶端安裝的維護期間至少必須為 30 分鐘

將此選項設為 [是]，使用維護期間來覆寫一般安裝行為。 基於安全，此設定符合系統維護優先順序的商務需求。

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>針對具有寫入篩選器的 Windows Embedded 裝置，認可 Endpoint Protection 用戶端安裝 (需要重新啟動)

選擇 [是]，在 Windows Embedded 裝置上停用寫入篩選器，並重新啟動裝置。 這項動作會認可裝置上的安裝。  

如果您選擇 [否]，則會在裝置重新啟動時所清除的暫時重疊上安裝用戶端。 在此案例中，Endpoint Protection 用戶端會等到其他安裝認可裝置的變更後才會完全安裝。 此設定是預設值。  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>安裝 Endpoint Protection 用戶端後抑制任何必要的電腦重新啟動

選擇 [是]，以抑制安裝 Endpoint Protection 用戶端之後的電腦重新啟動。  

> [!IMPORTANT]  
> 如果 Endpoint Protection 用戶端需要重新啟動電腦，而且此設定為 [否]，則會重新啟動電腦，而不管是否已設定任何維護視窗。  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>使用者可以延遲必要重新啟動以完成 Endpoint Protection 安裝的允許期限 (小時)

如果安裝 Endpoint Protection 用戶端之後需要重新啟動，則此設定指定使用者可延遲必要重新啟動的時數。 此設定需要 [安裝 Endpoint Protection 用戶端後抑制任何必要的電腦重新啟動] 的設定為 [否]。  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>針對用戶端電腦上的初始定義更新停用替代來源 (例如 Microsoft Windows Update、Microsoft Windows Server Update Services 或 UNC 路徑)

如果您想要 Configuration Manager 只在用戶端電腦上安裝初始定義更新，請選擇 [是]。 此設定有助於在定義更新的初始安裝期間避免不必要的網路連線，並可降低網路頻寬。  



## <a name="enrollment"></a>註冊

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>行動裝置舊版用戶端的輪詢間隔

選取 [設定間隔]，以指定舊版行動裝置輪詢原則的時間長度 (分鐘或小時)。 這些裝置包含 Windows CE、Mac OS X 和 Unix 或 Linux 這類平台。

### <a name="polling-interval-for-modern-devices-minutes"></a>新式裝置的輪詢間隔 (分鐘)

輸入新式裝置輪詢原則的分鐘數。 此設定適用於透過內部部署行動裝置管理所管理的 Windows 10 裝置。

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>允許使用者註冊行動裝置和 Mac 電腦

若要啟用以使用者為基礎的傳統裝置註冊，請將此選項設為 [是]，然後進行下列設定：

- **註冊設定檔**：選取 [設定設定檔]，以建立或選取註冊設定檔。 如需詳細資訊，請參閱[設定註冊的用戶端設定](deploy-clients-to-macs.md#configure-client-settings)。

### <a name="allow-users-to-enroll-modern-devices"></a>允許使用者註冊新式裝置

若要啟用以使用者為基礎的新式裝置註冊，請將此選項設為 [是]，然後進行下列設定：

- **新式裝置註冊設定檔**：選取 [設定設定檔]，以建立或選取註冊設定檔。 如需詳細資訊，請參閱[建立允許使用者註冊新式裝置的註冊設定檔](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf)。



## <a name="hardware-inventory"></a>硬體清查  

### <a name="enable-hardware-inventory-on-clients"></a>在用戶端上啟用硬體清查

此設定預設為 [是]。 如需詳細資訊，請參閱[硬體清查簡介](../manage/inventory/introduction-to-hardware-inventory.md)。

### <a name="hardware-inventory-schedule"></a>硬體清查排程

選取 [排程]，以調整用戶端執行硬體清查週期的頻率。 根據預設，此週期會每七天執行一次。

### <a name="maximum-random-delay-minutes"></a>最大隨機延遲 (分鐘)

指定 Configuration Manager 用戶端從定義的排程隨機化硬體清查循環的分鐘數上限。 這項跨所有用戶端的隨機化有助於站台伺服器上的負載平衡清查處理。 您可以指定介於 0 到 480 分鐘之間的任何值。 預設會將此值設為 240 分鐘 (4 小時)。

### <a name="maximum-custom-mif-file-size-kb"></a>自訂 MIF 檔案大小上限 (KB)

指定大小上限 (以 KB 為單位)，允許用戶端在硬體清查週期期間所收集的每個自訂管理資訊格式 (MIF) 檔案。 Configuration Manager 硬體清查代理程式不會處理任何超過此大小的自訂 MIF 檔案。 您可以指定 1 KB 到 5,120 KB 的大小。 根據預設，此值設為 250 KB。 此設定不會影響一般硬體清查資料檔案的大小。  

> [!NOTE]  
> 僅預設用戶端設定提供此設定。  

### <a name="hardware-inventory-classes"></a>硬體清查類別

選取 [設定類別]，以延伸從用戶端收集的硬體資訊，而不需手動編輯 sms_def.mof 檔案。 如需詳細資訊，請參閱[如何設定硬體清查](../manage/inventory/configure-hardware-inventory.md)。  

### <a name="collect-mif-files"></a>收集 MIF 檔案

使用此設定，指定是否要在硬體清查期間從 Configuration Manager 用戶端收集 MIF 檔案。  

要由硬體清查收集的 MIF 檔案，必須位於用戶端電腦的正確位置。 根據預設，此檔案位於下列路徑：  

- **IDMIF 檔案**應該位於 Windows\System32\CCM\Inventory\Idmif 資料夾中。

- **NOIDMIF 檔案**應該位於 Windows\System32\CCM\Inventory\Noidmif 資料夾中。

> [!NOTE]  
> 僅預設用戶端設定提供此設定。



## <a name="metered-internet-connections"></a>計量付費網際網路連線  

管理 Windows 8 和最新版本的電腦如何使用計量付費網際網路連線，以與 Configuration Manager 進行通訊。 在您處於計量付費網際網路連線時，網際網路提供者有時會根據您傳送和接收的資料量來收取費用。  

> [!NOTE]  
> 在下列案例中，不會套用已設定的用戶端設定：  
>
> - 如果電腦位於漫遊資料連線，Configuration Manager 用戶端不會執行任何需要將資料傳輸至 Configuration Manager 站台的工作。  
> - 如果將 Windows 網路連線內容設為非計量付費，Configuration Manager 用戶端會以非計量付費連線運作，並將資料傳輸至站台。  

### <a name="client-communication-on-metered-internet-connections"></a>計量付費網際網路連線上的用戶端通訊

針對此設定，選擇下列其中一個選項：  

- **允許**：除非用戶端裝置使用的是漫遊資料連線，否則，允許所有用戶端透過計量付費網際網路進行通訊。  

- **限制**：只允許下列用戶端通訊透過計量付費網際網路連線進行：  

    - 擷取用戶端原則  

    - 傳送至網站的用戶端狀態訊息  

    - 軟體中心的軟體安裝要求  

    - 必要的部署 (到達安裝期限時)  

    如果用戶端達到計量付費網際網路連線的資料傳輸限制，用戶端便不再嘗試與 Configuration Manager 站台通訊。  

- **封鎖**：Configuration Manager 用戶端不會在位於計量付費網際網路連線時，嘗試與 Configuration Manager 站台通訊。 此選項是預設值。  

> [!IMPORTANT]  
> 用戶端一律允許來自軟體中心的軟體安裝，而不論計量付費網際網路連線設定為何。 如果使用者在裝置使用計量付費網路時要求軟體安裝，軟體中心會尊重使用者的意圖。<!-- MEMDocs#285 -->


## <a name="power-management"></a>電源管理  

### <a name="allow-power-management-of-devices"></a>允許管理裝置電源

將此選項設為 [是]，在用戶端上啟用電源管理。 如需詳細資訊，請參閱[電源管理簡介](../manage/power/introduction-to-power-management.md)。

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>允許使用者從電源管理排除其裝置

選擇 [是]，讓軟體中心使用者將他們的電腦從所有設定的電源管理設定中排除。  

### <a name="allow-network-wake-up"></a>允許網路喚醒

1810 的新功能。 當設定為 [啟用] 時，系統會設定網路介面卡上的電源設定，以允許網路介面卡喚醒裝置。 當設定為 [停用] 時，網路介面卡上的電源設定會設定為不允許網路介面卡喚醒裝置。

### <a name="enable-wake-up-proxy"></a>啟用喚醒 Proxy

指定 [是]，在針對單點傳播封包進行設定時，補充站台的網路喚醒設定。  

如需喚醒 Proxy 的詳細資訊，請參閱[規劃如何喚醒用戶端](plan/plan-wake-up-clients.md)。  

> [!WARNING]  
> 請勿在不了解運作方式並在測試環境中進行評估的情況下，於生產網路中啟用喚醒 Proxy。  

然後，視需要設定下列其他設定：

- **喚醒 Proxy 連接埠號碼 (UDP)** ：用戶端用來將喚醒封包傳送給睡眠中電腦的連接埠號碼。 保留預設連接埠 25536，或將數字變更為您所選擇的值。  

- **網路喚醒連接埠號碼 (UDP)** ：除非您已在網站 [內容] 的 [連接埠] 索引標籤中變更網路喚醒 (UDP) 連接埠號碼，否則請保留預設值 9。  

    > [!IMPORTANT]  
    > 此號碼必須符合 [內容] 中的號碼。 如果您在一個位置變更這個號碼，則不會在另一個位置進行自動更新。  

- **喚醒 Proxy 的 Windows Defender 防火牆例外**：Configuration Manager 用戶端會在執行 Windows Defender 防火牆的裝置上自動設定喚醒 Proxy 連接埠號碼。 選取 [設定]，以指定所需的防火牆設定檔。  

    如果用戶端執行不同的防火牆，請手動將其設定為允許 [喚醒 Proxy 連接埠號碼 (UDP)]。  

- **IPv6 首碼 (如果 DirectAccess 或其他中介網路裝置需要)。請使用逗號來指定多個項目**：輸入必要 IPv6 首碼，讓喚醒 Proxy 在網路上運作。



## <a name="remote-tools"></a>遠端工具  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>在用戶端上啟用遠端控制，以及防火牆例外設定檔

選取 [設定]，以啟用 Configuration Manager 遠端控制功能。 或者設定防火牆設定，以允許在用戶端電腦上使用遠端控制。  

遠端控制預設為停用。  

> [!IMPORTANT]  
> 如果您未設定防火牆設定，遠端控制可能無法正常運作。  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>使用者可以在軟體中心變更原則或通知設定

選擇使用者是否可以從軟體中心內變更遠端控制選項。  

### <a name="allow-remote-control-of-an-unattended-computer"></a>允許遠端控制無人看管的電腦

選擇系統管理員是否可以使用遠端控制來存取登出或鎖定的用戶端電腦。 當此設定停用時，只能對登入和解除鎖定的電腦進行遠端控制。  

### <a name="prompt-user-for-remote-control-permission"></a>提示使用者提供遠端控制權限

選擇用戶端電腦是否會先顯示詢問使用者權限的訊息，再允許遠端控制工作階段。  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>提示使用者提出權限，以傳輸共用剪貼簿的內容

在遠端控制工作階段中傳輸共用剪貼簿的內容之前，讓您的使用者有機會接受或拒絕檔案傳輸。 使用者針對每個工作階段只需要授與權限一次。 檢視者無法提供傳輸檔案的權限給自己。

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>將遠端控制權限授與本機系統管理員群組

選擇起始遠端控制連線之伺服器上的本機系統管理員，是否可以建立用戶端電腦的遠端控制工作階段。  

### <a name="access-level-allowed"></a>允許的存取層級

指定允許的遠端控制存取層級。 從下列設定進行選擇：  

- **不允許存取**
- **僅限檢視**
- **完全控制**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>遠端控制和遠端協助的獲准檢視器

選取 [設定檢視器]，以指定可對用戶端電腦建立遠端控制工作階段的 Windows 使用者名稱。  

### <a name="show-session-notification-icon-on-taskbar"></a>在工作列上顯示工作階段通知圖示

將此設定設為 [是]，以在用戶端的 Windows 工作列上顯示圖示，指出遠端控制工作階段作用中。  

### <a name="show-session-connection-bar"></a>顯示工作階段連線列

將此選項設為 [是]，在用戶端上顯示高可見度的工作階段連線列，以指出作用中的遠端控制工作階段。  

### <a name="play-a-sound-on-client"></a>在用戶端上播放音效

設定此選項，使用音效來表示用戶端電腦上的遠端控制工作階段為作用中。 選取下列其中一個選項：

- **沒有音效**
- **工作階段的開始和結束** (預設值)
- **在工作階段期間重複提示**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>管理未請求遠端協助設定

將此設定設為 [是]，讓 Configuration Manager 管理未請求的遠端協助工作階段。  

在未請求遠端協助工作階段中，用戶端電腦的使用者不會要求協助以起始工作階段。  

### <a name="manage-solicited-remote-assistance-settings"></a>管理請求遠端協助設定

將此選項設為 [是]，讓 Configuration Manager 管理請求的遠端協助工作階段。  

在請求遠端協助工作階段中，用戶端電腦的使用者會向系統管理員傳送遠端協助要求。  

### <a name="level-of-access-for-remote-assistance"></a>遠端協助的存取層級

選擇要指派給 Configuration Manager 主控台中所起始之遠端協助工作階段的存取層級。 選取下列其中一個選項：

- **無** (預設值)
- **遠端檢視**
- **完全控制**

> [!NOTE]  
> 用戶端電腦上的使用者必須授與權限，才能進行遠端協助工作階段。  

### <a name="manage-remote-desktop-settings"></a>管理遠端桌面設定

將此選項設為 [是]，讓 Configuration Manager 管理電腦的遠端桌面工作階段。  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>允許獲准的檢視器使用遠端桌面連線進行連線

將此選項設為 [是]，以將獲准檢視器清單中所指定的使用者新增至用戶端上的遠端桌面本機使用者群組。  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>在執行 Windows Vista 作業系統和更新版本的電腦上需要網路層級驗證

將此選項設為 [是]，以使用網路層級驗證 (NLA) 來建立遠端桌面與用戶端電腦的連線。 NLA 一開始所需的遠端電腦資源較少，因為它會在建立遠端桌面連線之前完成使用者驗證。 使用 NLA 是更安全的設定。 NLA 可協助保護電腦不受惡意使用者或軟體的影響，同時降低遭到拒絕服務攻擊的風險。  



## <a name="software-center"></a>軟體中心

### <a name="select-these-new-settings-to-specify-company-information"></a>選取這些新的設定以指定公司資訊

將此選項設為 [是]，然後指定下列設定，以設定您組織的軟體中心品牌：

- **公司名稱**：輸入使用者在軟體中心看到的組織名稱。  

- **軟體中心的色彩配置**：按一下 [選取色彩] 以定義軟體中心所使用的主要色彩。  

- **選取軟體中心的標誌**：按一下 [瀏覽] 以選取要出現在軟體中心的影像。 標誌必須是 400 x 100 像素的 JPEG、PNG 或 BMP，且大小上限為 750 KB。 標誌檔案名稱不應該包含空格。  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a> 在軟體中心中隱藏未核准的應用程式

當您啟用此選項時，需要核准的使用者可用應用程式會隱藏在軟體中心內。<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a> 在軟體中心中隱藏已安裝的應用程式

當您啟用此選項時，[應用程式] 索引標籤中不再顯示已經安裝的應用程式。當您安裝或升級至 Configuration Manager 1802 時，此選項會設定為預設值。 在 [安裝狀態] 索引標籤下，仍然得以檢閱已安裝的應用程式。 <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a> 隱藏軟體中心中的應用程式類別目錄連結

在軟體中心中指定應用程式類別目錄網站連結的可見度。 設定此選項時，使用者將不會在軟體中心的 [安裝狀態] 節點中看到應用程式目錄網站連結。 <!--1358214-->

> [!Important]  
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  

### <a name="software-center-tab-visibility"></a>軟體中心索引標籤可見性

#### <a name="starting-in-version-1906"></a>從 1906 版開始
<!--4063773-->

選擇應該在軟體中心顯示的索引標籤。 使用 [新增] 按鈕，將索引標籤移至 [可見的索引標籤]。 使用 [移除] 按鈕，將它移至 [隱藏的索引標籤] 清單。 使用 [上移] 或 [下移] 按鈕來排列索引標籤的順序。 

可用的索引標籤：
- **應用程式**
- **更新**
- **作業系統**
- **安裝狀態**
- **裝置相容性**
- **選項**
- 按一下 [新增索引標籤] 按鈕，最多新增 5 個自訂索引標籤。
  - 指定自訂索引標籤的**索引標籤名稱**和**內容 URL**。
  - 按一下 [刪除索引標籤] 以移除自訂索引標籤。  

  >[!Important]  
  > - 某些網站功能作為軟體中心的自訂索引標籤使用時，可能無法正常運作。 請務必測試結果，再將此項目部署至用戶端。 <!--519659-->
  > - 當您新增自訂索引標籤時，僅指定信任的或內部網路網站位址。<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>1902 版和更早版本

將此群組中的其他設定設定為 [是]，在軟體中心內顯示下列索引標籤：

- **應用程式**
- **更新**
- **作業系統**
- **安裝狀態**
- **裝置相容性**
- **選項**
- **為軟體中心指定自訂索引標籤** <!--1358132-->
    - **索引標籤名稱**
    - **內容 URL**

    >[!Important]  
    > 某些網站功能作為軟體中心的自訂索引標籤使用時，可能無法正常運作。 請務必測試結果，再將此項目部署至用戶端。 <!--519659-->
    >
    > 當您新增自訂索引標籤時，僅指定信任的或內部網路網站位址。<!--SCCMDocs issue 1575-->

例如，如果您的組織未使用合規性原則，而且您想要隱藏軟體中心的 [裝置合規性] 索引標籤，請將 [啟用裝置合規性] 索引標籤設為 [否]。

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a> 在軟體中心設定預設檢視
<!--3612112-->
(於 1902 版引進)

- 將 [預設應用程式篩選] 設為 [全部] 或只有 [必要] 應用程式。  

  - 「軟體中心」一律會使用您的預設設定。 使用者可以變更此篩選，但「軟體中心」不會保存其喜好設定。  

- 將 [預設應用程式檢視] 設為 [圖格檢視] 或 [清單檢視]。 

  - 如果使用者變更此設定，軟體中心之後會保存使用者的喜好設定。 


## <a name="software-deployment"></a>軟體部署  

### <a name="schedule-re-evaluation-for-deployments"></a>排程部署的重新評估

設定排程，讓 Configuration Manager 重新評估所有部署的需求規則。 預設值為每七天執行一次。  

> [!IMPORTANT]  
> 此設定對本機用戶端的侵入性大於對網路或站台伺服器的侵入性。 更頻繁的重新評估排程會對網路和用戶端電腦效能造成負面影響。 Microsoft 不建議將值設定成比預設值低。 如果您變更此值，請嚴密監視效能。  

從用戶端將此動作初始化，如下所示：在 [Configuration Manager] 控制台的 [動作] 索引標籤中，選取 [應用程式部署評估週期]。  



## <a name="software-inventory"></a>軟體清查  

### <a name="enable-software-inventory-on-clients"></a>在用戶端上啟用軟體清查

預設會將此選項設為 [是]。 如需詳細資訊，請參閱[軟體清查簡介](../manage/inventory/introduction-to-software-inventory.md)。

### <a name="schedule-software-inventory-and-file-collection"></a>排程軟體清查和檔案收集

選取 [排程]，以調整用戶端執行軟體清查和檔案收集週期的頻率。 根據預設，此週期會每七天執行一次。

### <a name="inventory-reporting-detail"></a>清查報告詳細資料

指定要清查的下列其中一個層級的檔案資訊：

- **僅檔案**
- **僅產品**
- **完整詳細資料** (預設值)

### <a name="inventory-these-file-types"></a>清查這些檔案類型

如果您想要指定要清查的檔案類型，選取 [設定類型]，然後設定下列選項：  

> [!NOTE]  
> 如果將多個自訂用戶端設定套用至電腦，就會合併每個設定所傳回的清查。  

- 選取 [新增]，以新增要清查的新檔案類型。 然後，在 [已清查的檔案內容] 對話方塊中，指定下列資訊：  

    - **名稱**：提供您要清查的檔案名稱。 使用星號 (`*`) 萬用字元來表示任何文字字串，以及使用問號 (`?`) 來表示任何單一字元。 例如，若您想要清查所有副檔名為 .doc 的檔案，請指定檔案名稱 `*.doc`。  

    - **位置**：選取 [設定] 以開啟 [路徑內容] 對話方塊。 將軟體清查設定為在所有用戶端硬碟中搜尋指定的檔案、搜尋指定的路徑 (例如 `C:\Folder`)，或搜尋指定的變數 (例如 `%windir%`)。 您也可以搜尋指定路徑下的所有子資料夾。  

    - **排除加密和壓縮檔案**：當您選擇此選項時，系統將不會清查任何壓縮或加密檔案。  

    - **排除 Windows 資料夾中的檔案**：當您選擇此選項時，系統將不會清查 Windows 資料夾和其子資料夾中的任何檔案。  

    選取 [確定] 以關閉 [已清查的檔案內容] 對話方塊。 新增您要清查的所有檔案，然後選取 [確定] 以關閉 [設定用戶端設定] 對話方塊。  

### <a name="collect-files"></a>收集檔案

如果您想要從用戶端電腦收集檔案，選取 [設定檔案]，然後進行下列設定：  

> [!NOTE]  
> 如果將多個自訂用戶端設定套用至電腦，就會合併每個設定所傳回的清查。  

- 在 [設定用戶端設定] 對話方塊中，選取 [新增] 以新增要收集的檔案。  

- 在 [收集到的檔案內容]  對話方塊中，提供下列資訊：  

    - **名稱**：提供您要收集的檔案名稱。 使用星號 (`*`) 萬用字元來表示任何文字字串，以及使用問號 (`?`) 來表示任何單一字元。  

    - **位置**：選取 [設定] 以開啟 [路徑內容] 對話方塊。 將軟體清查設定為在所有用戶端硬碟中搜尋您要收集的檔案、搜尋指定的路徑 (例如 `C:\Folder`)，或搜尋指定的變數 (例如 `%windir%`)。 您也可以搜尋指定路徑下的所有子資料夾。  

    - **排除加密和壓縮檔案**：當您選擇此選項時，系統將不會收集任何壓縮或加密檔案。  

    - **當檔案大小總計超過下列大小時停止檔案收集 (KB)** ：指定檔案大小 (以千位元組 (KB) 為單位)，用戶端會在超過該大小時停止收集指定檔案。  

    > [!NOTE]  
    > 站台伺服器會收集所收集檔案中最近五個變更的版本，並將它們儲存在 `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` 目錄中。 如果自從上次軟體清查週期以來未變更過檔案，則不會再次收集該檔案。  
    >
    > 軟體清查不收集超過 20 MB 的檔案。  
    >
    > [設定用戶端設定] 對話方塊中的 [所有收集到的檔案的大小上限 (KB)] 值會顯示所有已收集檔案的大小上限。 達到此大小時，會停止檔案收集。 已收集的檔案會保留並傳送到網站伺服器。  

    > [!IMPORTANT]
    > 如果您將軟體清查設定為收集許多大型檔案，則此設定可能會對網路和站台伺服器的效能造成負面影響。  

    如需如何檢視收集到之檔案的資訊，請參閱[如何使用資源總管檢視軟體清查](../manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

    選取 [確定] 以關閉 [收集到的檔案內容] 對話方塊。 新增您要收集的所有檔案，然後選取 [確定] 以關閉 [設定用戶端設定] 對話方塊。  

### <a name="set-names"></a>設定名稱

軟體清查代理程式會從檔案標頭資訊中擷取製造商和產品名稱。 在檔案標頭資訊中，不一定會標準化這些名稱。 當您在資源總管中檢視軟體清查時，可能會顯示相同製造商或產品名稱的不同版本。 若要將這些顯示名稱標準化，選取 [設定名稱]，然後進行下列設定：  

- **名稱類型**：軟體清查會收集有關製造商與產品的資訊。 選擇您想要設定 [製造商] 或 [產品] 的顯示名稱。  

- **顯示名稱**：指定您想要用來取代 [已清查的名稱] 清單中名稱的顯示名稱。 若要指定新的顯示名稱，選取 [新增]。  

- **已清查的名稱**：若要新增已清查的名稱，請選取 [新增]。 在軟體清查中，會將這個名稱取代為 [顯示名稱] 清單中所選擇的名稱。 您可以新增要取代的多個名稱。  



## <a name="software-metering"></a>軟體計量

### <a name="enable-software-metering-on-clients"></a>在用戶端上啟用軟體計量

根據預設，會將此設定設為 [是]。 如需詳細資訊，請參閱[軟體計量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering)。

### <a name="schedule-data-collection"></a>排程資料收集

選取 [排程]，以調整用戶端執行軟體計量週期的頻率。 根據預設，此週期會每七天執行一次。



## <a name="software-updates"></a>軟體更新  

### <a name="enable-software-updates-on-clients"></a>啟用用戶端上的軟體更新

使用這項設定以啟用 Configuration Manager 用戶端上的軟體更新。 當您停用此設定時，Configuration Manager 會從用戶端移除現有的部署原則。 重新啟用這項設定時，用戶端會下載目前的部署原則。  

> [!IMPORTANT]  
> 停用這項設定時，依賴軟體更新的合規性原則將不再有作用。  

### <a name="software-update-scan-schedule"></a>軟體更新掃描排程

選取 [排程]，以指定用戶端起始合規性評量掃描的頻率。 這項掃描會判斷用戶端上軟體更新的狀態 (例如，必要或已安裝)。 如需合規性評估的詳細資訊，請參閱 [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (軟體更新合規性評估)。  

根據預設，這項掃描會使用簡單排程，每隔七天進行起始。 您可以建立自訂排程。 您可以指定確切的開始日期和時間、使用全球定位時間 (UTC) 或本機時間，並且設定一週內的特定日期為週期性間隔。  

> [!NOTE]  
> 如果您指定的間隔少於一天，Configuration Manager 會自動預設為一天。  

> [!WARNING]  
> 用戶端電腦上的實際開始時間是開始時間加上最多兩小時的隨機時數。 這項隨機化會防止用戶端電腦啟動掃描並同時連線至主動式軟體更新點。  

### <a name="schedule-deployment-re-evaluation"></a>排程部署重新評估

選取 [排程]，以設定軟體更新用戶端代理程式重新評估軟體更新的頻率，來取得 Configuration Manager 用戶端電腦上的安裝狀態。 在用戶端上無法再找到先前安裝的軟體更新但仍然需要它們時，用戶端會重新安裝軟體更新。

根據軟體更新合規性的公司原則，以及使用者是否可以將軟體更新解除安裝，來調整此排程。 每個部署重新評估週期都會導致網路和用戶端電腦處理器活動。 根據預設，此設定會使用簡易排程，每隔七天起始部署重新評估掃描。  

> [!NOTE]  
> 如果您指定的間隔少於一天，Configuration Manager 會自動預設為一天。  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>當任何軟體更新部署期限達到時，安裝期限在指定期間內的所有其他軟體更新部署

將此選項設為 [是]，以安裝必要部署中期限在指定期間內的所有軟體更新。 當達到必要軟體更新部署期限時，用戶端會在部署中起始軟體更新的安裝。 此設定決定是否從其他必要部署中安裝軟體更新，而這些部署的期限落在指定的時間內。  

使用此設定，可加速必要軟體更新的安裝。 此設定有可能也會提高用戶端安全性、減少給予使用者的通知，並減少用戶端重新啟動的次數。 根據預設，此設定值是設為 [否] 。  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>期限在這段時間內的所有擱置中部署也會安裝的一段時間

使用此設定以指定先前設定的時間範圍。 您可以輸入的值為 1 到 23 小時以及 1 到 365 天。 根據預設，此設定會設定為七天。  

### <a name="allow-clients-to-download-delta-content-when-available"></a>讓用戶端得以在提供差異內容時，進行下載

(於 1902 版引進)

將此選項設定為 [是]，以允許用戶端使用差異內容檔案。 此設定可讓裝置上的 Windows Update 代理程式決定所需的內容，並選擇性地下載。 

- 啟用此用戶端設定之前，請確認已針對環境適當地設定傳遞最佳化。 如需詳細資訊，請參閱 [Windows 傳遞最佳化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization)和[傳遞最佳化用戶端設定](#delivery-optimization)。
 - 此用戶端設定取代了 [允許在用戶端上安裝 Express 安裝檔案]。 將此選項設為 [是]，以允許用戶端使用快速安裝檔案。 如需詳細資訊，請參閱[管理適用於 Windows 10 更新的快速安裝檔案](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md)。
 - 從 Configuration Manager 1910 版開始，當設定此選項時，差異下載會用於所有 Windows Update 安裝檔案，而不只是用於快速安裝檔案。
    - 針對內容儲存體使用 CMG 時，如果已啟用 [下載可用的差異內容] 用戶端設定，第三方更新的內容將不會下載至用戶端。 <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>用戶端用於接收差異內容要求的連接埠

(於 1902 版引進)

此設定會設定 HTTP 接聽程式的本機連接埠，以下載差異內容。 預設會設定為 8005。 您不需要在用戶端防火牆中開啟此連接埠。 

> [!NOTE]
>此用戶端設定取代了 [用以下載 Express 安裝檔案內容的連接埠]。


### <a name="enable-management-of-the-office-365-client-agent"></a>啟用管理 Office 365 用戶端代理程式

當您將此選項設為 [是] 時，就會啟用 Office 365 安裝設定的設定。 它也能從 Office 內容傳遞網路 (CDN) 下載檔案，並在 Configuration Manager 中將檔案部署為應用程式。 如需詳細資訊，請參閱[管理 Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md)。

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a> 當 [軟體更新] 維護視窗可以使用時，允許安裝 [所有部署] 維護視窗中的軟體更新

從 1810 版開始，當您將此選項設定為 [是] 且用戶端至少定義一個 [軟體更新] 維護時段時，將在 [所有部署] 維護時段安裝軟體更新。

根據預設，此設定值是設為 [否] 。 此值會使用和先前相同的行為：如果兩個類型都存在，其便會忽略該視窗。 <!--2839307-->

> [!NOTE]
> 此設定也適用於您設定以套用至**工作順序**的維護時段。<!-- SCCMDocs-pr #4596 -->
>
> 如果用戶端只有 [所有部署] 時段可用，其仍會在該時段安裝軟體更新或工作順序。

#### <a name="maintenance-window-example"></a>維護時段範例

例如，您可以設定下列維護時段：

- **所有部署**：02:00 - 04:00
- **軟體更新**：04:00 - 06:00

根據預設，用戶端只會在第二個維護時段期間安裝軟體更新。 在此案例中，它會忽略所有部署的維護視窗。 當將此設定變更為 [是] 時，用戶端會在 02:00 - 06:00 之間安裝軟體更新。


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a> 指定功能更新的執行緒優先順序

<!--3734525-->
從 Configuration Manager 版本 1902 開始，您可以調整 Windows 10 版本 1709 或更新版本用戶端透過 [Windows 10 維護](../../../osd/deploy-use/manage-windows-as-a-service.md)安裝功能更新的優先順序。 此設定對於 Windows 10 就地升級工作順序沒有任何影響。

此用戶端設定提供下列選項：

- **未設定**：Configuration Manager 不會變更此設定。 系統管理員可以預先設定自己的 setupconfig.ini 檔案。 此值為預設。

- **標準**：Windows 安裝程式會使用更多的系統資源，並更快速地更新。 它會使用更多的處理器時間，因此總安裝時間較短，但使用者的中斷時間較長。  

    - 使用 `/Priority Normal` [Windows 安裝程式命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)設定裝置上的 setupconfig.ini 檔案。

- **低**：當它在背景下載並更新時，您可以繼續在裝置上工作。 總安裝時間較長，但使用者的中斷時間較短。 您可能需要增加更新最大執行時間，以避免在使用此選項時逾時。  

    - 從 setupconfig.ini 檔案中移除 `/Priority` [Windows 安裝程式命令列選項](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。


### <a name="enable-third-party-software-updates"></a>啟用協力廠商軟體更新

當您將此選項設為 [是] 時，就會設定 [允許內部網路 Microsoft 更新服務位置的簽署更新] 的原則，並將簽署憑證安裝至用戶端的受信任發行者存放區。

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>針對功能更新啟用動態更新
<!--4062619-->
從 Configuration Manager 1906 版開始，您可以設定 [Windows 10 的動態更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) \(英文\)。 動態更新會引導用戶端從網際網路下載這些更新，以在 Windows 安裝期間安裝語言套件、隨選功能、驅動程式和累積更新。 當此設定設為 [是] 或[否] 時，Configuration Manager 會修改功能更新安裝期間所使用的 [setupconfig](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) \(部分機器翻譯\) 檔案。

- [未設定] - 預設值。 沒有對 setupconfig 檔案進行任何變更。
  - 在所有支援的 Windows 10 版本上，預設會啟用動態更新。
    - 針對 Windows 10 1803 版和較早版本，動態更新會檢查裝置的 WSUS 伺服器是否有核准的動態更新。 在 Configuration Manager 環境中，永遠都不會在 WSUS 伺服器中直接核准動態更新，因此，這些裝置不會安裝它們。
    - 從 Windows 10 1809 版開始，動態更新會使用裝置的網際網路連線，從 Microsoft Update 取得動態更新。 這些動態更新不會發佈來供 WSUS 使用。
- **是**：啟用動態更新。
- **否**：停用動態更新。


## <a name="state-messaging"></a>狀態訊息

### <a name="state-message-reporting-cycle-minutes"></a>狀況訊息回報週期 (分鐘)

指定用戶端回報狀態訊息的頻率。 根據預設，此設定為 15 分鐘。



## <a name="user-and-device-affinity"></a>使用者和裝置親和性  

### <a name="user-device-affinity-usage-threshold-minutes"></a>使用者裝置親和性使用閾值 (分鐘)

指定 Configuration Manager 建立使用者裝置親合型對應之前的分鐘數。 此值預設為 2880 分鐘 (兩天)。

### <a name="user-device-affinity-usage-threshold-days"></a>使用者裝置親和性使用閾值 (天)

指定天數，超過此天數之後，用戶端會測量使用量裝置親和性的閾值。 根據預設，此值為 30 天。

> [!NOTE]  
> 例如，您將 [使用者裝置親和性使用閾值 (分鐘)] 指定為 **60** 分鐘，並將 [使用者裝置親和性使用閾值 (天)] 指定為 **5** 天。 然後，使用者必須在 5 天期間內每 60 分鐘使用裝置一次，以建立與裝置的自動親和性。  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>從使用資料自動設定使用者裝置親和性

選擇 [是]，以根據 Configuration Manager 所收集的使用量資訊來建立自動使用者裝置親和性。  

### <a name="allow-user-to-define-their-primary-devices"></a>允許使用者定義其主要裝置
<!--3485366-->
當此設定為 [是] 時，使用者就能在軟體中心識別其專屬主要裝置。 如需詳細資訊，請參閱[軟體中心使用者指南](../../understand/software-center.md#work-information)。

## <a name="windows-analytics"></a>Windows Analytics

> [!Important]  
> Windows Analytics 服務已在 2020 年 1 月 31 日淘汰。 如需詳細資訊，請參閱 [KB 4521815：Windows Analytics 於 2020 年 1 月 31 日淘汰](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。
>
> 電腦分析是 Windows Analytics 的演進。 如需詳細資訊，請參閱[什麼是電腦分析](../../../desktop-analytics/overview.md)。
