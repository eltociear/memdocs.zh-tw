---
title: 規劃雲端管理閘道
titleSuffix: Configuration Manager
description: 規劃和設計雲端管理閘道 (CMG)，以簡化網際網路用戶端的管理。
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d6165678331811f4b04e8b1f540f3dcbb7f015d
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502250"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中進行雲端管理閘道規劃

適用於：Configuration Manager (最新分支)

<!--1101764-->
雲端管理閘道 (CMG) 可讓您輕鬆管理網際網路上的 Configuration Manager 用戶端。 您可以部署 CMG 作為 Microsoft Azure 中的雲端服務，來管理在網際網路上漫遊的傳統用戶端，而不需要額外的內部部署基礎結構。 您也不需要將內部部署基礎結構公開至網際網路。

> [!NOTE]
> 根據預設，Configuration Manager 不會啟用此選擇性功能。 您必須先先啟用這項功能才能使用它。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../../servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

建立必要條件之後，建立 CMG 包含 Configuration Manager 主控台中的下列三個步驟：

1. 將 CMG 雲端服務部署至 Azure。
2. 新增 CMG 連接點角色。
3. 設定服務的站台和站台角色。
部署並設定之後，用戶端不論是在內部網路或網際網路，都能順利地存取內部部署站台角色。

本文所提供的基本知識可讓您了解 CMG、如何設計以符合環境與規劃實作。

## <a name="scenarios"></a>案例

CMG 有助於以下數種案例。 以下是一些常見的案例：  

- 管理具有加入 Active Directory 網域身分識別的傳統 Windows 用戶端。 這些用戶端包括 Windows 8.1 與 Windows 10。 它會使用 PKI 憑證來保護通訊通道。 管理活動包括：  

  - 軟體更新和 Endpoint Protection
  - 清查和用戶端狀態
  - 相容性設定
  - 對裝置發佈軟體
  - Windows 10 就地升級工作順序

- 管理具有 Azure Active Directory (Azure AD) 混合式或純加入雲端網域新式身分識別的傳統 Windows 10 用戶端。 用戶端會使用 Azure AD 進行驗證，而不是使用 PKI 憑證。 相較於複雜的 PKI 系統，使用 Azure AD 會更容易設定和維護。 管理活動與第一個案例相同，再加上：  

  - 對使用者發佈軟體  

- 透過網際網路在 Windows 10 裝置上安裝 Configuration Manager 用戶端。 使用 Azure AD 可讓裝置向 CMG 驗證，以進行用戶端註冊和指派。 您可以手動安裝用戶端，或是使用 Microsoft Intune 等其他軟體發佈方法。  

- 使用共同管理的新裝置佈建。 當自動註冊現有的用戶端時，不需要 CMG 來進行共同管理。 對於涉及 Windows AutoPilot、Azure AD、Microsoft Intune 與 Configuration Manager 的新裝置，則需要它。 如需詳細資訊，請參閱[共同管理的路徑](../../../../comanage/quickstart-paths.md)。

### <a name="specific-use-cases"></a>特定使用案例

下列特定裝置使用案例可能適用於上述案例：

- 膝上型電腦之類的漫遊裝置  

- 可透過網際網路來管理的遠端或分公司裝置，相較於透過 WAN 或 VPN 來管理，會較為便宜且更有效率。  

- 在合併和收購的情況下，將裝置加入 Azure AD 並透過 CMG 來管理可能是最簡易的方式。  

- 工作群組用戶端。 這些裝置可能需要額外的設定，例如憑證。<!-- SCCMDocs#1925 -->

    從 2002 版開始，Configuration Manager 支援權杖型驗證，這可能有助於管理遠端工作群組用戶端。 如需詳細資訊，請參閱 [CMG 的權杖型驗證](../../deploy/deploy-clients-cmg-token.md)。

> [!Important]
> 所有用戶端變成以網際網路為基礎時，預設都會接收並開始使用 CMG 的原則。 依您組織適用的案例與使用案例而定，您可能需要限制 CMG 的使用範圍。 如需詳細資訊，請參閱[讓用戶端使用雲端管理閘道](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway)用戶端設定。

## <a name="topology-design"></a>拓撲設計

### <a name="cmg-components"></a>CMG 元件

CMG 的部署和作業包括下列元件：  

- Azure 中的 **CMG 雲端服務**會向 CMG 連接點驗證並轉送 Configuration Manager 用戶端要求。  

- **CMG 連接點**站台系統角色可啟用 Azure 中從內部部署網路至 CMG 服務的一致且高效能連線。 它也會將設定發佈至 CMG，包括連線資訊和安全性設定。 CMG 連接點會根據 URL 對應，將用戶端要求從 CMG 轉送至內部部署角色。

- [**服務連接點**](../../../servers/deploy/configure/about-the-service-connection-point.md)站台系統角色會執行雲端服務管理員元件，以處理所有 CMG 部署工作。 此外，它也會從 Azure AD 監視並報告服務健康情況和記錄資訊。 請確認您的服務連接點處於[線上模式](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)。  

- **管理點**站台系統角色可以回應一般用戶端要求。

- **軟體更新點**站台系統角色可以回應一般用戶端要求。

    > [!NOTE]
    > 管理點和軟體更新點的大小調整指導方針並不會改變，無論其服務對象是內部部署或網際網路型用戶端。 如需詳細資訊，請參閱[大小和縮放比例](../../../plan-design/configs/size-and-scale-numbers.md#management-point)。

- **以網際網路為基礎的用戶端**會連線到 CMG，以存取內部部署的 Configuration Manager 元件。

- CMG 會使用**以憑證為基礎的 HTTPS** Web 服務，以協助保護與用戶端之間的網路通訊。  

- 以網際網路為基礎的用戶端會使用 **PKI 憑證或 Azure AD** 於身分識別和驗證。  

- [**雲端發佈點**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)會視需要提供內容給以網際網路為基礎的用戶端。  

  - CMG 也可將內容提供給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。 如需詳細資訊，請參閱[修改 CMG](setup-cloud-management-gateway.md#modify-a-cmg)。<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
使用 **Azure Resource Manager 部署**來建立 CMG。 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) 是可將所有解決方案資源當作單一實體 (稱為[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)) 來管理的新式平台。 使用 Azure Resource Manager 部署 CMG 時，站台會使用 Azure Active Directory (Azure AD) 來驗證並建立必要的雲端資源。 這個現代化的部署不需要傳統的 Azure 管理憑證。  

> [!NOTE]
> 此功能不會啟用對 Azure 雲端服務提供者 (CSP) 的支援。 含 Azure Resource Manager 的 CMG 部署會繼續使用 CSP 不支援的傳統雲端服務。 如需詳細資訊，請參閱 [Azure CSP 中可用的 Azure 服務](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services)。

從 Configuration Manager 1902 版開始，對於雲端管理閘道的新執行個體，Azure Resource Manager 是唯一的部署機制。 現有的部署可繼續運作。<!-- 3605704 -->

在 Configuration Manager 1810 版和更早版本中，CMG 精靈仍會使用 Azure 管理憑證來提供**傳統服務部署**的選項。 若要簡化資源的部署與管理，建議針對所有新的 CMG 執行個體使用 Azure Resource Manager 部署模型。 如果可能，請透過 Resource Manager 重新部署現有的 CMG 執行個體。 如需詳細資訊，請參閱[修改 CMG](setup-cloud-management-gateway.md#modify-a-cmg)。

> [!IMPORTANT]
> Azure 已淘汰傳統服務部署，不再供 Configuration Manager 使用。 1810 版是支援建立這些 Azure 部署的最後版本。 此功能將會在未來的 Configuration Manager 版本中移除。<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>階層設計

在階層的頂層站台建立 CMG。 如果是管理中心網站，請在子主要站台建立 CMG 連接點。 雲端服務管理員元件位於服務連接點上，而服務連接點也位於管理中心網站上。 此設計可視需要在不同的主要站台之間共用該服務。

您可以在 Azure 中建立多個 CMG 服務，且可以建立多個 CMG 連接點。 多個 CMG 連接點能在 CMG 和內部部署角色之間提供用戶端流量上的負載平衡。

從 1902 版開始，您可以將 CMG 關聯至界限群組。 此設定可讓用戶端根據[界限群組關聯性](../../../servers/deploy/configure/boundary-groups.md)來預設或回復為 CMG 以進行用戶端通訊。 此行為在分公司和 VPN 案例中特別有用。 您可以將用戶端流量從昂貴且緩慢的 WAN 連結導向成改用 Microsoft Azure 中較快的服務。<!--3640932-->

> [!NOTE]
> 以網際網路為基礎的用戶端不屬於任何界限群組。
>
> 在 Configuration Manager 1810 版和更早版本中，CMG 不屬於任何界限群組。

其他因素 (例如要管理的用戶端數目) 也會影響您的 CMG 設計。 如需詳細資訊，請參閱[效能和擴充](#performance-and-scale)。

#### <a name="example-1-standalone-primary-site"></a>範例 1：獨立主要站台

Contoso 在其紐約市總部的內部部署資料中心具有獨立主要站台。

- 他們在美國東部 Azure 區域建立 CMG 以減少網路延遲。
- 他們建立兩個 CMG 連接點，這兩個連接點皆連結至單一的 CMG 服務。  

當用戶端漫遊至網際網路時，它們會與位於美國東部 Azure 區域的 CMG 通訊。 CMG 會透過上述兩個 CMG 連接點轉送此通訊。

#### <a name="example-2-hierarchy"></a>範例 2：階層

Fourth Coffee 在其西雅圖總部的內部部署資料中心具有管理中心網站。 其中一個主要站台位於相同的資料中心，另一個主要站台則在該公司位於巴黎的主要歐洲辦公室。

- 在管理中心網站上，他們在美國西部 Azure 區域中建立 CMG 服務。 他們根據整個階層中預期的漫遊用戶端負載來調整 VM 數目。
- 在位於西雅圖的主要站台上，他們建立連結至單一 CMG 的 CMG 連接點。
- 在位於巴黎的主要站台上，他們建立連結至單一 CMG 的 CMG 連接點。

當用戶端漫遊至網際網路時，他們會與位於美國西部 Azure 區域的 CMG 通訊。 CMG 會將此通訊轉送至用戶端受指派之主要網站中的 CMG 連接點。

> [!TIP]
> 您不需要為了地理位置而部署多個雲端管理閘道。 雲端服務可能發生輕微延遲，但設定管理員用戶端幾乎不會受其影響，即使在地理位置較遠的情況下也是如此。

### <a name="test-environments"></a>測試環境
<!-- SCCMDocs#1225 -->
許多組織都有用於生產、測試、開發或品質保證的個別環境。 當您規劃 CMG 部署時，請考慮下列問題：

- 您的組織具有多少個 Azure AD 租用戶？
  - 是否有用於測試的個別租用戶？
  - 使用者和裝置身分識別是否位於相同的租用戶？

- 每個租用戶中有多少個訂用帳戶？
  - 是否有特別用於測試的訂用帳戶？

Configuration Manager 適用於**雲端管理**的 Azure 服務支援多個租用戶。 多個 Configuration Manager 站台可以連線到相同的租用戶。 單一站台可以將多個 CMG 服務部署到不同的訂用帳戶。 多個站台可以將 CMG 服務部署到相同的訂用帳戶。 Configuration Manager 能根據您的環境和商務需求提供彈性。

如需詳細資訊，請參閱下列常見問題集：[使用者帳戶是否必須與裝載 CMG 雲端服務的訂用帳戶所相關聯的租用戶位於相同的 Azure AD 租用戶？](cloud-management-gateway-faq.md#bkmk_tenant)

## <a name="requirements"></a>需求

- 裝載 CMG 的 **Azure 訂用帳戶**。

    > [!IMPORTANT]
    > CMG 不支援具有 Azure 雲端服務提供者 (CSP) 的訂用帳戶。<!-- MEMDocs#320 -->

- 您的使用者帳戶在 Configuration Manager 中必須為**系統高權限管理員**或**基礎結構系統管理員**。<!-- SCCMDocs#2146 -->

- 需要 **Azure 系統管理員**參與部分元件的初始建立 (視您的設計而定)。 此角色與 Configuration Manager 系統管理員可以為相同 (或個別) 角色。 若為個別角色，則不需要 Configuration Manager 中的權限。

  - 若要部署 CMG，您需要**訂用帳戶擁有者**
  - 若要將網站與 Azure AD 整合以使用 Azure Resource Manager 來部署 CMG，您需要**全域管理員**

- 至少一個內部部署 Windows 伺服器以裝載 **CMG 連接點**。 您可以搭配另一個 Configuration Manager 站台系統角色共置此角色。  

- **服務連接點**必須處於[線上模式](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)。  

- 與 **Azure AD** 整合以使用 Azure Resource Manager 來部署服務。 如需詳細資訊，請參閱[設定 Azure 服務](../../../servers/deploy/configure/azure-services-wizard.md)。  

- 供 CMG 使用的[**伺服器驗證憑證**](certificates-for-cloud-management-gateway.md#bkmk_serverauth)。  

- 視您用戶端 OS 版本及驗證模型的不同，它可能會需要**其他憑證**。 如需詳細資訊，請參閱 [CMG 憑證](certificates-for-cloud-management-gateway.md)。  

    當使用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證] 站台選項時，HTTP 可作為管理點。 如需詳細資訊，請參閱[Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md) (增強 HTTP)。

- 在 Configuration Manager 1810 版和更早版本中，如果使用 Azure 傳統部署方法，您必須使用 [**Azure 管理憑證**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt)。  

    > [!TIP]  
    > 使用 **Azure Resource Manager** 部署模型。 它並不需要此管理憑證。
    >
    > 自 1810 版開始淘汰傳統部署方法。  

- 用戶端必須使用 **IPv4**。  

## <a name="specifications"></a>規格

- 列於[用戶端和裝置支援的作業系統](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)中的所有 Windows 版本皆支援 CMG。  

- CMG 僅支援管理點和軟體更新點角色。  

- CMG 不支援僅透過 IPv6 位址進行通訊的用戶端。<!--495606-->  

- 使用網路負載平衡器的軟體更新點無法與 CMG 搭配使用。 <!--505311-->  

- 使用 Azure 資源模型的 CMG 部署將不會提供對 Azure 雲端服務提供者 (CSP) 的支援。 含 Azure Resource Manager 的 CMG 部署會繼續使用 CSP 不支援的傳統雲端服務。 如需詳細資訊，請參閱 [Azure CSP 計畫中可用的 Azure 服務](https://docs.microsoft.com/partner-center/azure-plan-available)。

### <a name="support-for-configuration-manager-features"></a>針對 Configuration Manager 功能的支援

下表列出針對 Configuration Manager 功能的 CMG 支援：

|功能  |支援  |
|---------|---------|
| 軟體更新     | ![支援](media/green_check.png) |
| Endpoint Protection     | ![支援](media/green_check.png) <sup>[附註 1](#bkmk_note1)</sup> |
| 硬體與軟體清查     | ![支援](media/green_check.png) |
| 用戶端狀態和通知     | ![支援](media/green_check.png) |
| 執行指令碼     | ![支援](media/green_check.png) |
| CMPivot     | ![支援](media/green_check.png) |
| 相容性設定     | ![支援](media/green_check.png) |
| 用戶端安裝<br>(使用 [Azure AD 整合](../../deploy/deploy-clients-cmg-azure.md)) | ![支援](media/green_check.png) |
| 用戶端安裝<br>(使用[權杖驗證 ](../../deploy/deploy-clients-cmg-token.md)) | ![支援](media/green_check.png) (2002) |
| 軟體發佈 (以裝置為目標)     | ![支援](media/green_check.png) |
| 軟體發佈 (以使用者為目標，必要)<br>(搭配 Azure AD 整合)     | ![支援](media/green_check.png) |
| 軟體發佈 (以使用者為目標，可用)<br>([所有需求](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![支援](media/green_check.png) |
| Windows 10 [就地升級工作順序](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) | ![支援](media/green_check.png) |
| 不使用開機映像且使用以下選項部署的工作順序：**啟動工作順序之前下載所有內容到本機** | ![支援](media/green_check.png) |
| 不使用開機映像與[任何一種下載選項](../../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)的工作順序： | ![支援](media/green_check.png) (1910)|
| 所有其他工作順序案例     | ![不支援](media/Red_X.png) |
| 用戶端推入     | ![不支援](media/Red_X.png) |
| 自動站台指派     | ![不支援](media/Red_X.png) |
| 軟體核准要求     | ![不支援](media/Red_X.png) |
| Configuration Manager 主控台     | ![不支援](media/Red_X.png) |
| 遠端工具     | ![不支援](media/Red_X.png) |
| 報告網站     | ![不支援](media/Red_X.png) |
| 網路喚醒     | ![不支援](media/Red_X.png) |
| Mac、Linux 及 UNIX 用戶端     | ![不支援](media/Red_X.png) |
| 對等快取     | ![不支援](media/Red_X.png) |
| 內部部署 MDM     | ![不支援](media/Red_X.png) |
| BitLocker 管理     | ![不支援](media/Red_X.png) |

|機碼|
|--|
|![支援](media/green_check.png) = 此功能由所有支援的 Configuration Manager 支援搭配 CMG 使用  |
|![支援](media/green_check.png) (*YYMM*) = 此功能從 Configuration Manager 的 *YYMM* 版開始支援搭配 CMG 使用  |
|![不支援](media/Red_X.png) = 此功能不支援與 CMG 搭配使用 |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a> 附註 1：端點保護支援
<!-- 4350561 -->
已加入網域的裝置若要套用端點保護原則，就需要網域存取權。 不常存取內部網路的裝置可能會在套用端點保護原則時遇到延遲。 如果您要求裝置在收到端點保護原則之後立即加以套用，請考慮下列其中一個選項：

- 使用共同管理，並將 [Endpoint Protection 工作負載](../../../../comanage/workloads.md#endpoint-protection)切換至 Intune，然後從雲端管理 [Microsoft Defender 防毒軟體](https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus)。

- 使用[設定項目](../../../../compliance/deploy-use/create-configuration-items.md)而非原生[反惡意程式碼原則](../../../../protect/deploy-use/endpoint-antimalware-policies.md)功能，來套用端點保護原則。

## <a name="cost"></a>成本

> [!IMPORTANT]  
> 下面的成本資訊僅供評估之用。 您的環境可能有其他變數會影響使用 CMG 的總成本。

CMG 會使用下列 Azure 元件，並會針對 Azure 訂用帳戶產生費用：

### <a name="virtual-machine"></a>虛擬機器

- CMG 使用 Azure 雲端服務作為平台即服務 (PaaS)。 此服務使用會產生計算成本的虛擬機器 (VM)。  

- CMG 會使用標準 A2 V2 VM。  

- 您可以選取支援 CMG 的 VM 執行個體數目。 預設值為 1，最大值為 16。 此數字是在建立 CMG 時設定，並可以視需要於未來針對服務規模進行變更。

- 如需支援用戶端所需之 VM 數目的詳細資訊，請參閱[效能和擴充](#performance-and-scale)。

- 請參閱 [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/)以利判斷潛在成本。

    > [!NOTE]  
    > 虛擬機器的成本隨地區而異。

### <a name="outbound-data-transfer"></a>輸出資料傳輸

- 費用是根據自 Azure 流出 (輸出或下載) 的資料而定。 流至 Azure (輸入或上傳) 的所有資料皆為免費。 自 Azure 流出的 CMG 資料包括由 CMG 轉送至站台的用戶端原則、用戶端通知及用戶端回應。 這些回應包括清查報表、狀態訊息及合規性狀態。  

- 就算沒有用戶端正在與 CMG 通訊，某些背景通訊仍會在 CMG 和內部部署站台之間產生網路流量。  

- 在 Configuration Manager 主控台中檢視**輸出資料傳輸 (GB)** 。 如需詳細資訊，請參閱[監視 CMG 上的用戶端](monitor-clients-cloud-management-gateway.md)。  

- 請參閱 [Azure 頻寬定價詳細資料](https://azure.microsoft.com/pricing/details/bandwidth/)以利判斷潛在成本。 資料傳輸的訂價為階層式。 使用的量越多，每 GB 的價格便越低。  

- *僅供評估之用*，針對以網際網路為基礎的用戶端，預期每個用戶端每月大約為 100-300 MB。 較低的估計是適用於預設的用戶端設定。 較高的估計是適用於較為積極的用戶端設定。 您實際的使用量可能會因您設定用戶端設定的方式而有所不同。  

    > [!NOTE]  
    > 執行其他動作 (例如部署軟體更新或應用程式) 會增加從 Azure 輸出的資料傳輸量。

- 以網際網路為基礎的用戶端能免費從 Windows Update 取得 Microsoft 軟體更新內容。 請不要將具有 Microsoft 更新內容的更新套件發佈至雲端發佈點，否則可能會產生儲存和資料輸出成本。  

- **驗證用戶端憑證撤銷**的 CMG 選項設定錯誤，可能導致額外流量從用戶端傳送至 CMG。 此額外流量可能會增加 Azure 輸出資料，這可能會增加您的 Azure 成本。<!-- SCCMDocs#1434 --> 如需詳細資訊，請參閱[發佈憑證撤銷清單](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl)。  

### <a name="content-storage"></a>內容儲存體

- 以網際網路為基礎的用戶端能免費從 Windows Update 取得 Microsoft 軟體更新內容。 請不要將具有 Microsoft 更新內容的更新套件發佈至雲端發佈點，否則可能會產生儲存和資料輸出成本。  

- 針對所有其他必要內容 (例如應用程式或協力廠商軟體更新)，您必須將它發佈至雲端發佈點。 目前，CMG 僅支援使用雲端發佈點將內容傳送至用戶端。
   - 使用 CMG 來儲存內容時，如果已啟用 [Download delta content when available] \(在提供差異內容時下載\) 的[用戶端設定](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)，協力廠商更新的內容就不會下載至用戶端。 <!--6598587--> 

- 如需詳細資訊，請參閱使用[雲端發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost)的成本。  

- CMG 也可以作為雲端發佈點，以提供內容給用戶端。 這項功能可減少 Azure VM 所需的憑證和成本。 如需詳細資訊，請參閱[修改 CMG](setup-cloud-management-gateway.md#modify-a-cmg)。<!--1358651-->  

- CMG 使用 Azure 本地備援儲存體 (LRS)。 如需詳細資訊，請參閱[本地備援儲存體](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs) \(部分機器翻譯\)。  

### <a name="other-costs"></a>其他成本

- 每個雲端服務都具有動態 IP 位址。 每個相異 CMG 都會使用新的動態 IP 位址。 針對每個 CMG 新增額外的 VM 將不會增加這些位址。  

## <a name="performance-and-scale"></a>效能和擴充

如需 CMG 擴充的詳細資訊，請參閱[大小和縮放比例](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)。

下列建議可協助您改善 CMG 效能：

- Configuration Manager 用戶端和 CMG 之間的連線並無法感知區域。 用戶端通訊不太會受到延遲/地理分隔的影響。 不需要針對地理位置的接近而部署多個 CMG。 將 CMG 部署在您階層中的頂層網站，並新增執行個體以增加規模。

- 若要取得服務的高可用性，請針對每個站台建立具有至少兩個 CMG 執行個體與兩個 CMG 連接點的 CMG。  

- 透過新增更多 VM 執行個體來調整 CMG，以支援更多用戶端。 Azure 負載平衡器會控制針對服務的用戶端連線。  

- 建立更多 CMG 連接點以將負載分散於它們之間。 CMG 會透過循環配置資源的方式，將流量發佈至其正在連線的 CMG 連接點。  

- 當 CMG 處於用戶端數目超過支援數目的高負載狀態時，它仍會處理要求，但可能出現延遲。  

> [!NOTE]
> 雖然 Configuration Manager 針對 CMG 連接點沒有嚴格的用戶端數目限制，Windows Server 預設的 TCP 動態連接埠範圍上限為 16,384。 若 Configuration Manager 站台搭配單一 CMG 連接點管理超過 16,384 個用戶端，您必須提升該 Windows Server 限制。 所有的用戶端都會針對用戶端通知維持一個通道，這會在 CMG 連接點上持續開啟一個連接埠。 如需如何使用 netsh 命令來提升此限制的詳細資訊，請參閱 [Microsoft 支援服務文章 929851](https://support.microsoft.com/help/929851) \(機器翻譯\)。

## <a name="ports-and-data-flow"></a>連接埠和資料流程

您不需要針對內部部署網路開啟任何輸入連接埠。 服務連接點和 CMG 連接點會起始與 Azure 和 CMG 的所有通訊。 這兩個站台系統角色必須能夠建立與 Microsoft 雲端的輸出連線。 服務連接點會在 Azure 中部署及監視該服務，因此它必須處於線上模式。 CMG 連接點會連線至 CMG 以管理 CMG 和內部部署站台系統角色之間的通訊。

下表為 CMG 的基礎概念資料流程：

[![CMG 資料流程](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. 服務連接點會透過 HTTPS 連接埠 443 連線至 Azure。 它會使用 Azure AD 或 Azure 管理憑證進行驗證。 服務連接點會在 Azure 中部署 CMG。 CMG 會使用伺服器驗證憑證建立 HTTPS 雲端服務。  

2. CMG 連接點會透過 TCP-TLS 或 HTTPS 連線至 Azure 中的 CMG。 它會將連線保持開啟，並建置通道以供未來的雙向通訊使用。  

3. 用戶端會透過 HTTPS 連接埠 443 連線至 CMG。 它會使用 Azure AD 或用戶端驗證憑證進行驗證。  

    > [!NOTE]
    > 如果您啟用 CMG 以提供內容或使用雲端發佈點，用戶端會透過 HTTPS 連接埠 443 直接連線到 Azure Blob 儲存體。 如需詳細資訊，請參閱[使用雲端式發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow)。<!-- SCCMDocs#2332 -->

4. CMG 會透過針對內部部署 CMG 連接點的現有連線轉送用戶端通訊。 您不需要開啟任何輸入防火牆連接埠。  

5. CMG 連接點會將用戶端通訊轉送至內部部署管理點和軟體更新點。  

如需您在 Azure 中裝載內容時的詳細資訊，請參閱[使用雲端式發佈點](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow)。

### <a name="required-ports"></a>必要的連接埠

此表列出必要的網路連接埠和通訊協定。 [用戶端] 是起始連線的裝置，需要輸出連接埠。 [伺服器] 是接受連線的裝置，需要輸入連接埠。

| 用戶端 | 通訊協定 | Port | 伺服器 | 說明 |
|--------|----------|------|--------|-------------|
| 服務連接點 | HTTPS | 443 | Azure | CMG 部署 |
| CMG 連接點 | TCP-TLS | 10140-10155 | CMG 服務 | 建置 CMG 通道的偏好通訊協定 <sup>[附註 1](#bkmk_port-note1)</sup> |
| CMG 連接點 | HTTPS | 443 | CMG 服務 | 僅針對單一 VM 執行個體建置 CMG 通道的後援通訊協定<sup>[附註 2](#bkmk_port-note2)</sup> |
| CMG 連接點 | HTTPS | 10124-10139 | CMG 服務 | 針對兩個或多個 VM 執行個體建置 CMG 通道的後援通訊協定<sup>[附註 3](#bkmk_port-note3)</sup> |
| 用戶端 | HTTPS | 443 | CMG | 一般用戶端通訊 |
| 用戶端 | HTTPS | 443 | Blob 儲存體 | 下載雲端式內容 |
| CMG 連接點 | HTTPS 或 HTTP | 443 或 80 | 管理點 | 內部部署流量，連接埠會因管理點設定而有所不同 |
| CMG 連接點 | HTTPS 或 HTTP | 443 或 80 | 軟體更新點 | 內部部署流量，連接埠會因軟體更新點設定而有所不同 |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a> 附註 1：CMG 連接點 TCP-TLS 連接埠

CMG 連接點會先針對每個 CMG VM 執行個體嘗試建立長時間執行的 TCP-TLS 連線。 它會透過連接埠 10140 連線至第一個 VM 執行個體。 第二個 VM 執行個體會使用連接埠 10141，依此類推，直到使用連接埠 10155 連線至第 16 個 VM 執行個體為止。 TCP-TLS 連線的執行效能最佳，但不支援網際網路 Proxy。 若 CMG 連接點無法透過 TCP-TLS 連線，則會退為使用 HTTPS<sup>[附註 2](#bkmk_port-note2)</sup>。

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a> 附註 2：單一 VM 的 CMG 連接點 HTTPS 連接埠

若 CMG 連接點無法透過 TCP-TLS 連線至 CMG<sup>[附註 1](#bkmk_port-note1)</sup>，則在只有單一 VM 執行個體的情況下，其會透過 HTTPS 443 連線至 Azure 網路負載平衡器。  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a> 附註 3：兩部 (或以上) VM 的 CMG 連接點 HTTPS 連接埠

若存在兩個 (或以上) VM 執行個體，則 CMG 連接點會針對第一個 VM 執行個體使用 HTTPS 10124，而非 HTTPS 443。 它會透過 HTTPS 10125 連線至第二個 VM 執行個體，依此類推，直到使用 HTTPS 連接埠 10139 連線至第 16 個 VM 執行個體為止。

### <a name="internet-access-requirements"></a>網際網路存取需求

如果貴組織禁止使用防火牆或 Proxy 裝置來與網際網路網路通訊，則您需要允許 CMG 連接點和服務連接點存取網際網路端點。

如需詳細資訊，請參閱[網際網路存取需求](../../../plan-design/network/internet-endpoints.md#bkmk_cloud)。

## <a name="next-steps"></a>後續步驟

- [雲端管理閘道的憑證](certificates-for-cloud-management-gateway.md)
- [雲端管理閘道器的安全性和隱私權](security-and-privacy-for-cloud-management-gateway.md)
- [雲端管理閘道的大小和規模數量](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [雲端管理閘道的相關常見問題集](cloud-management-gateway-faq.md)
- [設定雲端管理閘道](setup-cloud-management-gateway.md)
