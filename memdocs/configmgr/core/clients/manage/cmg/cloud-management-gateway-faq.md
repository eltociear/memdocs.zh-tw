---
title: CMG 常見問題集
titleSuffix: Configuration Manager
description: 使用本文來回答關於雲端管理閘道的常見問題
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 2bd3824df18ecdf426720a99db8720ef4b678733
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694926"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>雲端管理閘道的相關常見問題集

適用於：  Configuration Manager (最新分支)

本文回答關於雲端管理閘道的常見問題。 如需詳細資訊，請參閱[規劃雲端管理閘道](plan-cloud-management-gateway.md)。


## <a name="frequently-asked-questions"></a>常見問題集

### <a name="what-certificates-do-i-need"></a>我需要哪些憑證？

如需更詳細的資訊，請參閱[雲端管理閘道的憑證](certificates-for-cloud-management-gateway.md)。


### <a name="do-i-need-azure-expressroute"></a>我需要 Azure ExpressRoute 嗎？

否。 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 可讓您將內部部署網路擴充到 Microsoft 的雲端。 設定管理員雲端管理閘道並不需要 ExpressRoute 或其他這類虛擬網路連線。 雲端管理閘道的設計可讓以網際網路為基礎的用戶端透過 Azure 服務與內部部署站台系統進行通訊，不需要額外的網路設定。 如需詳細資訊，請參閱[規劃雲端管理閘道](plan-cloud-management-gateway.md)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>我需要維護 Azure 虛擬機器嗎？

不需要任何維護。 雲端管理閘道的設計使用 Azure 平台即服務 (PaaS)。 使用您提供的訂用帳戶，Configuration Manager 會建立必要的虛擬機器 (VM)、存放裝置和網路功能。 Azure 會保護並更新虛擬機器。 這些 VM 不屬於您的內部部署環境，在此情況下是基礎結構即服務 (IaaS)。 雲端管理閘道是將您的 Configuration Manager 環境延伸到雲端的 PaaS。 如需詳細資訊，請參閱[保護 PaaS 部署](/azure/security/security-paas-deployments)。


### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>如何在服務更新期間確保服務不中斷？

藉由將 CMG 調整為包含兩個或多個執行個體，您可以自動從 Azure 中的「更新網域」受益。 請參閱[如何更新雲端服務](/azure/cloud-services/cloud-services-update-azure-service)。


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>我已經在使用 IBCM。 如果我新增 CMG，用戶端會如何運作？

如果您已部署[以網際網路為基礎的用戶端管理](../plan-internet-based-client-management.md) (IBCM)，則也可以部署雲端管理閘道。 用戶端會接收兩個服務的原則。 當它們漫遊至網際網路，它們會隨機選取並使用其中一個以網際網路為基礎的服務。


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a>使用者帳戶是否必須與裝載 CMG 雲端服務的訂用帳戶所相關聯的租用戶位於相同的 Azure AD 租用戶？
<!--SCCMDocs-pr issue #2873-->
如果您的環境具有多個訂用帳戶，您可以將 CMG 部署到任何可託管 Azure 雲端服務的訂用帳戶中。 

此問題常見於下列情況：  

- 您有不同的測試和生產 Active Directory 與 Azure AD 環境，但只有一個集中式 Azure 主控訂用帳戶時  

- 您的 Azure 使用量有系統地跨不同小組成長  

當您使用 Resource Manager 部署時，請登入與訂用帳戶相關聯的 Azure AD 租用戶。 此連線可讓設定管理員向 Azure 進行驗證，以建立、部署及管理 CMG。  

如果您針對透過 CMG 管理的使用者和裝置使用 Azure AD 驗證，請登入該 Azure AD 租用戶。 如需使用 Azure 服務進行雲端管理的詳細資訊，請參閱[設定 Azure 服務](../../../servers/deploy/configure/azure-services-wizard.md)。 當您登入每個 Azure AD 租用戶時，單一 CMG 可為多個租用戶提供 Azure AD 驗證，而不論裝載位置為何。

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>CMG 會如何影響我透過 VPN 連線的用戶端？

透過 VPN 連線至您環境的漫遊用戶端，通常會受偵測為內部網路對向。 這些用戶端會嘗試連線至您的內部部署基礎結構，例如管理點和發佈點。 即便是透過 VPN 連線，有部分客戶還是傾向讓雲端服務管理這些漫遊用戶端。 從 1902 版開始，將 CMG 關聯至界限群組。 這個動作會強制用戶端不使用內部部署站台系統。 如需詳細資訊，請參閱[設定界限群組](setup-cloud-management-gateway.md#configure-boundary-groups)。

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>如果我啟用 CMG，則我的客戶會在連線至內部網路時，只連線至啟用 CMG 的管理點嗎？

為了確保能安全地透過 CMG 傳送敏感性流量，請設定 HTTPS 管理點或使用增強式 HTTP。

如果您選擇部署 CMG 並使用 PKI 憑證在啟用 CMG 的管理點上進行 HTTPS 通訊，請於管理點屬性上選取選項以**允許僅限網際網路的用戶端**。 這項設定能確保內部用戶端在您的環境中繼續使用 HTTP 管理點。

如果您使用增強式 HTTP，則不需要進行此設定。 當直接對啟用 CMG 的管理點通訊時，用戶端會繼續使用 HTTP。 如需詳細資訊，請參閱[Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md) (增強 HTTP)。

## <a name="next-steps"></a>後續步驟

- [規劃雲端管理閘道](plan-cloud-management-gateway.md)
- [設定雲端管理閘道](setup-cloud-management-gateway.md)
- [雲端管理閘道的憑證](certificates-for-cloud-management-gateway.md)
- [雲端管理閘道器的安全性和隱私權](security-and-privacy-for-cloud-management-gateway.md)
- [雲端管理閘道的大小和規模數量](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
