---
title: CMG 常見問題集
titleSuffix: Configuration Manager
description: 使用本文來回答關於雲端管理閘道的常見問題
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: bd846b0155a0baddad76d6027ffbd239d7dbf26f
ms.sourcegitcommit: 5f15a3abf33ce7bfd6855ffeef2ec3cd4cd48a7f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721885"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>雲端管理閘道的相關常見問題集

適用於：Configuration Manager (最新分支)

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

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a> 使用者帳戶是否必須與裝載 CMG 雲端服務的訂用帳戶所相關聯的租用戶位於相同的 Azure AD 租用戶？
<!--SCCMDocs-pr issue #2873-->
否。您可以將 CMG 部署到任何可裝載 Azure 雲端服務的訂用帳戶中。

為了釐清詞彙：

- 「租用戶」是使用者帳戶和應用程式註冊的目錄。 一個租用戶可以有多個訂用帳戶。
- 「訂用帳戶」會區隔計費、資源及服務。 其會與單一租用戶相關聯。

此問題常見於下列情況：  

- 當您有不同的測試和生產 Active Directory 與 Azure AD 環境，但只有一個集中式的 Azure 主控訂用帳戶。

- 您的 Azure 使用量有系統地跨不同小組成長

當您使用 Resource Manager 部署時，請登入與訂用帳戶相關聯的 Azure AD 租用戶。 此連線可讓設定管理員向 Azure 進行驗證，以建立、部署及管理 CMG。  

如果您針對透過 CMG 管理的使用者和裝置使用 Azure AD 驗證，請登入該 Azure AD 租用戶。 如需使用 Azure 服務進行雲端管理的詳細資訊，請參閱[設定 Azure 服務](../../../servers/deploy/configure/azure-services-wizard.md)。 當您登入每個 Azure AD 租用戶時，單一 CMG 可為多個租用戶提供 Azure AD 驗證，而不論裝載位置為何。

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>範例 1：具有多個訂用帳戶的單一租用戶

使用者身分識別、裝置註冊，以及應用程式註冊都位於相同的租用戶。 您可以選擇 CMG 使用的訂用帳戶。 您可以將多個 CMG 服務從單一站台部署到個別的訂用帳戶。 站台與租用戶具有一對一關聯性。 您決定要針對各種不同的原因 (例如計費或邏輯分隔) 使用哪些訂用帳戶。

#### <a name="example-2-multiple-tenants"></a>範例 2：多個租用戶

換句話說，您的環境具有一個以上的 Azure AD。 如果您需要支援兩個租用戶中的使用者和裝置身分識別，便必須將站台附加到每個租用戶。 此程序需要來自每個租用戶的系統管理帳戶，以在該租用戶中建立應用程式註冊。 單一站台接著可以在多個租用戶中裝載 CMG 服務。 您可以在任一租用戶中任何可用的訂用帳戶中建立 CMG。 已加入或混合式加入任一 Azure AD 的裝置都可以使用 CMG。

如果使用者和裝置身分識別位於某個租用戶，但 CMG 的訂用帳戶位於另一個租用戶，您便需要將站台附加到這兩個租用戶。 技術上而言，只有 CMG 服務的第二個租用戶並不需要用戶端應用程式。 用戶端應用程式只會針對使用 CMG 服務的用戶端提供使用者和裝置驗證。<!-- SCCMDocs#1902 -->

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
