---
title: Proxy 伺服器支援
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站台系統伺服器如何使用 Proxy 伺服器。
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 89a2f76f394d3bdf8fd6785429ae0ae60302537a
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802084"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Configuration Manager 中的 Proxy 伺服器支援

適用於：  Configuration Manager (最新分支)

部分 Configuration Manager 站台系統伺服器需要連線至網際網路。 如果您的環境需要網際網路流量才能使用 Proxy 伺服器，請設定這些站台系統角色以使用 Proxy。  

- 裝載站台系統伺服器的電腦支援單一 Proxy 伺服器設定。 在該電腦上的所有站台系統角色會共用這項相同的 Proxy 設定。 如果不同的角色或角色執行個體需要個別的 Proxy 伺服器，請將這些角色放在不同的站台系統伺服器上。  

- 當您為已有 Proxy 伺服器設定的站台系統伺服器設定新的 Proxy 伺服器設定時，將會覆寫原始設定。  

- 根據預設，若要與 Proxy 連線，需使用裝載站台系統角色之電腦的**系統**帳戶。  

- 如果無法驗證電腦帳戶，站台系統伺服器可以儲存使用者認證以連線到 Proxy 伺服器。 這些認證是**站台系統 Proxy 伺服器帳戶**。  

## <a name="site-system-roles-that-use-a-proxy"></a>使用 Proxy 的站台系統角色

下列站台系統角色會連線到網際網路，而且如有必要，可以使用 Proxy 伺服器：  

### <a name="asset-intelligence-synchronization-point"></a>Asset Intelligence 同步處理點

此站台系統角色會連線到 Microsoft，並且會在裝載 Asset Intelligence 同步處理點的電腦上使用 Proxy 伺服器設定。  

### <a name="cloud-distribution-point"></a>雲端發佈點

雲端發佈點角色在 Microsoft Azure 中執行。 您未將此站台系統角色設定為使用 Proxy。 請在管理雲端發佈點的主要站台伺服器上進行 Proxy 設定。  

針對這個組態，主要站台伺服器：  

- 必須能夠連線到 Microsoft Azure，才可設定、監視及發佈內容到雲端發佈點。  

- 根據預設，使用該電腦的**系統**帳戶來進行連線。 如有必要，它也可以使用站台系統 Proxy 伺服器帳戶。  

- 使用 Windows 網頁瀏覽器 API。  

### <a name="cloud-management-gateway-connection-point"></a>雲端管理閘道連接點

雲端管理閘道 (CMG) 連接點是與 Azure 中的 CMG 服務進行通訊的內部部署角色。 如需詳細資訊，請參閱[針對 CMG 進行規劃](../../clients/manage/cmg/plan-cloud-management-gateway.md)。

### <a name="distribution-point"></a>發佈點

<!-- 5856396 -->

從 2002 版開始，如果針對 Microsoft 網內快取啟用 Configuration Manager 發佈點，則該發佈點可以透過未經驗證的 Proxy 伺服器通訊以進行網際網路存取。 如需詳細資訊，請參閱 [Microsoft 連線快取](../hierarchy/microsoft-connected-cache.md)。

### <a name="exchange-server-connector"></a>Exchange Server 連接器

此站台系統角色會連線到 Exchange Server。 它會在裝載 Exchange Server 連接器的電腦上使用 Proxy 伺服器設定。  

### <a name="service-connection-point"></a>服務連接點

此站台系統角色會連線到 Configuration Manager 雲端服務來下載 Configuration Manager 的版本更新。 它會使用裝載服務連線點之電腦上所設定的 Proxy 伺服器。  

### <a name="software-update-point"></a>軟體更新點

此站台系統角色可在連線到 Microsoft Update 以下載修補程式，並同步處理更新的相關資訊時，使用 Proxy。 與每個其他站台系統角色一樣，請先設定站台系統 Proxy 設定。 然後，設定軟體更新點特有的下列選項：  

- **同步處理軟體更新時使用 Proxy 伺服器**  

- **使用自動部署規則在下載內容時使用 Proxy 伺服器**  

    > [!NOTE]
    > 雖然可供使用，但次要站台上的軟體更新點不會使用此設定。  

這些設定位於軟體更新點內容的 [Proxy 和帳戶設定]  索引標籤上。  

> [!NOTE]
> 根據預設，當自動部署規則執行時，會使用已建立自動部署規則之站台中站台伺服器的**系統**帳戶來連線到網際網路，並下載軟體更新。 或者，設定和使用站台系統 Proxy 伺服器帳戶。 
>
> 當此帳戶無法存取網際網路時，軟體更新便無法下載。 下列項目會記錄到 **ruleengine.log** 中：  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a> 針對站台系統伺服器使用 Proxy 的其他功能

(在 2002 版中引進) 

從 Configuration Manager 2002 版開始，下列功能會使用裝載[服務連接點](#service-connection-point)角色的站台系統 Proxy： <!--5913817-->

- [Azure Active Directory (Azure AD) 使用者探索](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Azure AD 使用者群組探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [將集合成員資格結果同步至 Azure Active Directory 群組](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>設定站台系統伺服器的 Proxy  

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。  

2. 選取您要編輯的站台系統伺服器。 在 [詳細資料] 窗格中，以滑鼠右鍵按一下 [站台系統]  角色，然後選取 [內容]  。  

3. 在 [站台系統內容] 中，切換至 [Proxy]  索引標籤。指定下列 Proxy 設定：  

    - **同步處理來自網際網路的資訊時使用 Proxy 伺服器**：選取此選項，讓站台系統伺服器使用 Proxy 伺服器。  

    - **Proxy 伺服器名稱**：指定您環境中 Proxy 伺服器的主機名稱或 FQDN。  

    - **連接埠**：指定要與 Proxy 伺服器通訊的網路連接埠。 根據預設，它會使用連接埠 **80**。  

    - **使用認證連線至 Proxy 伺服器**：許多 Proxy 伺服器需要使用者進行驗證。 根據預設，站台系統伺服器會使用其電腦帳戶連線到 Proxy 伺服器。 如有必要，請啟用此選項，按一下 [設定]  ，然後選擇 [現有的帳戶]  或指定 [新增帳戶]  。 這些認證是**站台系統 Proxy 伺服器帳戶**。  如需詳細資訊，請參閱 [Accounts used in Configuration Manager](../hierarchy/accounts.md) (Configuration Manager 中使用的帳戶)。  

4. 選擇 [確定]  即可儲存新的 Proxy 伺服器設定。  

## <a name="next-steps"></a>後續步驟

如果貴組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，則您需要允許存取網際網路端點。 如需詳細資訊，請參閱[網際網路存取需求](internet-endpoints.md)。
