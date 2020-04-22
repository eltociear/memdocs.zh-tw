---
title: CMG 安全性和隱私權
titleSuffix: Configuration Manager
description: 深入了解使用雲端管理閘道的安全性和隱私權的指引和建議。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 93427cb34b2216bf16f713818481e69573a4b0de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693236"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>雲端管理閘道的安全性和隱私權

適用於：  Configuration Manager (最新分支)

本文包含 Configuration Manager 雲端管理閘道 (CMG) 的安全性和隱私權資訊。 如需詳細資訊，請參閱[規劃雲端管理閘道](plan-cloud-management-gateway.md)。

## <a name="cmg-security-details"></a>CMG 安全性詳細資料

- CMG 接受並管理從 CMG 連接點而來的連線。 它會使用利用憑證和連線識別碼的相互 SSL 驗證。
- CMG 使用下列方法接受並轉送用戶端要求：
    - 使用相互 SSL，搭配以 PKI 為基礎的用戶端驗證憑證或 Azure AD，預先驗證連線。
      - CMG VM 執行個體上的 IIS 根據上傳至 CMG 的受信任根憑證，驗證憑證路徑。
      - VM 執行個體上的 IIS 也會驗證用戶端憑證撤銷 (如果啟用)。 如需詳細資訊，請參閱[發佈憑證撤銷清單](#bkmk_crl)。
    - 憑證信任清單會檢查用戶端驗證憑證的根。 同時也會針對用戶端執行與管理點相同的驗證。 如需詳細資訊，請參閱[檢閱站台憑證信任清單中的項目](#bkmk_ctl)。
    - 驗證並篩選用戶端要求 (URL)，以檢查是否有任何 CMG 連接點可以服務此要求。  
    - 針對每個發佈端點檢查內容長度。
    - 使用循環配置資源行為，負載平衡相同站台中的 CMG 連接點。
- CMG 連接點使用下列方法：
    - 對 CMG 的所有 VM 執行個體，建置一致的 HTTPS/TCP 連線。 它會在每分鐘檢查並維護這些連線。
    - 使用相互 SSL 利用憑證向 CMG 進行驗證。
    - 根據 URL 對應轉送用戶端要求。
    - 報告連線狀態以在主控台中顯示服務健康情況狀態。
    - 每隔五分鐘報告每個端點的流量。

### <a name="configuration-manager-client-facing-roles"></a>設定管理員用戶端面向角色

管理點和軟體更新點在 IIS 中裝載端點來服務用戶端要求。 CMG 不會公開所有的內部端點。 每個發行至 CMG 的端點都具有 URL 對應。

- 用戶端使用外部 URL 來與 CMG 通訊。
- 內部 URL 為用來將要求轉送至內部伺服器的 CMG 連接點。

#### <a name="url-mapping-example"></a>URL 對應範例

當您在管理點上啟用 CMG 流量時，Configuration Manager 會針對每個管理點伺服器建立一組內部的 URL 對應。 例如：ccm_system、ccm_incoming 和 sms_mp。 管理點 ccm_system 端點的外部 URL 看起來應該會類似：  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
每個管理點的 URL 皆會是唯一的。 接著，設定管理員用戶端會將已啟用 CMG 的管理點名稱放在其網際網路管理點清單中。 此名稱看起來像：  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
站台會自動將所有已發佈的外部 URL 上傳至 CMG。 此行為可讓 CMG 執行 URL 篩選。 所有 URL 對應都會複寫至 CMG 連接點。 然後會根據用戶端要求中的外部 URL，將通訊轉送至內部伺服器。


## <a name="security-guidance-for-cmg"></a>CMG 的安全性指引

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>發佈憑證撤銷清單

發佈您的 PKI 憑證撤銷清單 (CRL)，供以網際網路為基礎的用戶端存取。 使用 PKI 部署 CMG 時，請在 [設定] 索引標籤上設定服務以**驗證用戶端憑證撤銷**。此設定會設定服務使用已發佈的憑證撤銷清單 (CRL)。 如需詳細資訊，請參閱[規劃 PKI 憑證撤銷](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。

此 CMG 選項會驗證用戶端驗證憑證。

- 如果用戶端使用 Azure AD 驗證，那麼，CRL 並不重要。
- 如果您使用 PKI 並在外部發佈 CRL，則要啟用此選項 (建議使用)。
- 如果您使用 PKI，請不要發佈 CRL，接著停用此選項。
- 如果您誤設此選項，可能導致將額外流量從用戶端傳送至 CMG。 此額外流量可能會增加 Azure 輸出資料，這可能會增加您的 Azure 成本。<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>檢閱站台憑證信任清單中的項目

<!--503739-->
每個 Configuration Manager 站台都包含一份受信任的根憑證授權單位清單，也就是憑證信任清單 (CTL)。 移至 [系統管理] 工作區，展開 [站台設定]，然後選取 [站台] 來檢視和修改清單。 選取站台，在功能區中按一下 [內容]。 切換至 [用戶端電腦通訊]  索引標籤，然後在 [信任的根憑證授權單位] 下方按一下 [設定]  。

> [!Note]
> 從 1906 版開始，此索引標籤稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

針對站台使用更嚴格的 CTL，搭配使用 PKI 用戶端驗證的 CMG。 否則，用戶端只要擁有由管理點上已經存在的任何受信任根所發出的用戶端驗證憑證，就會自動接受而進行用戶端註冊。

此子集提供系統管理員對安全性有更多的控制。 CTL 會限制伺服器只接受由 CTL 中憑證授權單位所發出的用戶端憑證。 例如，Windows 出貨時隨附數個著名的協力廠商憑證授權單位 (CA) 憑證，如 VeriSign 與 Thawte。 根據預設，執行 IIS 的電腦會信任鏈結至這些著名 CA 的憑證。 如果沒有使用 CTL 設定 IIS，擁有由這些 CA 所發出之用戶端憑證的任何電腦，都會被視為是有效的設定管理員用戶端。 如果您使用未包含這些 CA 的 CTL 來設定 IIS，若憑證鏈結至這些 CA，就會拒絕用戶端連線。

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a> 強制使用 TLS 1.2

<!-- SCCMDocs-pr#4021 -->

從 1906 版開始，請使用 CMG 設定來**強制使用 TLS 1.2**。 此設定僅適用於 Azure 雲端服務 VM。 它不適用於任何內部部署 Configuration Manager 站台伺服器或用戶端。 如需 TLS 1.2 的詳細資訊，請參閱[如何啟用 TLS 1.2](../../../plan-design/security/enable-tls-1-2.md)。


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>後續步驟

- [規劃雲端管理閘道](plan-cloud-management-gateway.md)
- [設定雲端管理閘道](setup-cloud-management-gateway.md)
- [雲端管理閘道的相關常見問題集](cloud-management-gateway-faq.md)
- [雲端管理閘道的憑證](certificates-for-cloud-management-gateway.md)
