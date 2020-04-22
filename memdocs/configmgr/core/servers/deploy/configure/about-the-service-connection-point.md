---
title: 服務連接點
titleSuffix: Configuration Manager
description: 了解此 Configuration Manager 站台系統角色，並了解及規劃其使用範圍。
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704946"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>關於 Configuration Manager 中的服務連線點

適用於：  Configuration Manager (最新分支)

服務連接點是可提供階層中幾項重要功能的站台系統角色。 請先了解並規劃服務連接點的使用範圍，再設定服務連接點。 規劃使用方式可能會影響您設定此站台系統角色的方式：

- 下載適用於 Configuration Manager 基礎結構的更新。 系統會根據您上傳的使用方式資料，僅提供與基礎結構相關的更新。

- 從 Configuration Manager 基礎結構上傳使用方式資料。 您可以控制上傳詳細資料的層級或數量。 如需詳細資訊，請參閱[使用方式資料層級和設定](../install/setup-reference.md#bkmk_usage)。

- 在 Azure 中部署[雲端管理閘道](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

- 同步處理來自[商務用與教育用 Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) 的應用程式

- 探索 [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc) 中的使用者和群組

- 使用[電腦分析](../../../../desktop-analytics/overview.md)來取得有關 Windows 10 更新和應用程式整備程度的見解

每個階層都支援此角色的單一執行個體。 此角色只能安裝在階層的頂層站台 (管理中心網站 (CAS) 或獨立主要站台) 上。 如果您將獨立主要站台擴充至較大的階層，請從主要站台解除安裝此角色，然後在 CAS 上安裝此角色。

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a> 作業模式

服務連接點支援兩種作業模式：

- **連線**：服務連接點每隔 24 小時會自動檢查更新。 它會下載您目前基礎結構和產品版本可用的新更新，在 Configuration Manager 主控台中提供它們。

- **離線**：服務連接點不會連線到 Microsoft 雲端服務。 若要手動匯入可用的更新，請使用[服務連線工具](../../manage/use-the-service-connection-tool.md)。

### <a name="change-mode"></a>變更模式

若在安裝服務連接點之後要切換線上或離線模式，請先重新啟動 SMS_Executive 服務的 **SMS_DMP_DOWNLOADER** 執行緒。 您必須重新啟動此執行緒，這項變更才會生效。 若要重新啟動此執行緒，請使用 Configuration Manager Service Manager。

> [!TIP]
> 您也可以重新啟動 Configuration Manager 的 SMS_Executive 服務，這會重新啟動大部分的站台元件。 或者，請等候站台備份等排程工作，該工作會為您停止 SMS_Executive 服務，並於稍後重新啟動。

若要使用 Configuration Manager Service Manager 來重新啟動 SMS_DMP_DOWNLOADER 執行緒：

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區，展開 [系統狀態]  ，然後選取 [元件狀態]  節點。 在功能區中，選擇 [開始]  ，然後選取 [Configuration Manager Service Manager]  。

1. 在 Service Manager 瀏覽窗格中，依序展開站台和 [元件]  ，然後選擇要重新啟動的元件：**SMS_DMP_DOWNLOADER**。

1. 移至 [元件]  功能表，然後選擇 [查詢]  。

1. 確認元件的目前狀態。 然後移至 [元件]  功能表，並選擇 [停止]  。  

1. 再次 [查詢]  元件，確認該元件已停止。 然後選擇 [啟動]  元件動作將其重新啟動。

## <a name="remote-site-system-requirements"></a>遠端站台系統需求

當您在站台伺服器的遠端站台系統伺服器上安裝服務連接點時，請設定下列需求：

- 站台伺服器電腦帳戶在裝載遠端服務連接點的電腦上必須是本機系統管理員。

- 請使用[站台系統安裝帳戶](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)設定裝載此角色的站台系統伺服器。 站台伺服器上的發佈管理員會使用站台系統安裝帳戶，傳送來自服務連線點的更新。

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a> 網際網路存取需求

如果貴組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，則您需要允許服務連接點可存取網際網路端點。

如需詳細資訊，請參閱[網際網路存取需求](../../../plan-design/network/internet-endpoints.md#bkmk_scp)。

## <a name="install"></a>安裝

當執行 [安裝]  以安裝階層的頂層站台時，您可以安裝服務連接點。

執行安裝程式之後，或若要重新安裝此角色時，請使用 [新增站台系統角色精靈]  或 [建立站台系統伺服器精靈]  。 (只在您階層的頂層站台上安裝服務連接點。)如需詳細資訊，請參閱[安裝站台系統角色](install-site-system-roles.md)。

## <a name="move-the-role"></a><a name="bkmk_move"></a> 移動角色

<!-- SCCMDocs#922 -->
在幾種情況下，您可能需要將服務連接點移到另一部伺服器：

- [復原](../../manage/recover-sites.md)
- [站台伺服器的高可用性](site-server-high-availability.md)
- [站台擴充](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

在移動服務連接點之後，請檢查所有站台功能。 例如，您可能需要針對 Azure Active Directory (Azure AD) 租用戶的任何連線更新祕密金鑰。 如需詳細資訊，請參閱[更新秘密金鑰](azure-services-wizard.md#bkmk_renew)。

## <a name="log-files"></a>記錄檔

若要檢視關於上傳到 Microsoft 的資訊，請在執行服務連接點的伺服器上檢視 **Dmpuploader.log**。 針對更新的下載進度，請檢視 **Dmpdownloader.log**。 如需服務連接點相關的完整記錄清單，請參閱[記錄檔 - 服務連接點](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog)。

## <a name="next-steps"></a>後續步驟

使用下列流程圖來了解程序流程和重要記錄項目。 此程序包括更新下載，以及將更新複寫至其他站台。

- [流程圖 - 下載更新](../../manage/download-updates-flowchart.md)

- [流程圖 - 更新複寫](../../manage/update-replication-flowchart.md)
