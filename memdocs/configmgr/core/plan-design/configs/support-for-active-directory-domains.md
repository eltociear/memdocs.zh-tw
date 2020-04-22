---
title: Active Directory 網域的支援
titleSuffix: Configuration Manager
description: 了解 Active Directory 網域中 Configuration Manager 站台系統的需求。
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688576"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>對 Configuration Manager 中 Active Directory 網域的支援

適用於：  Configuration Manager (最新分支)

所有 Configuration Manager 站台系統皆必須是支援的 Active Directory 網域成員。 Configuration Manager 用戶端電腦可以是網域成員或工作群組成員。  

## <a name="requirements-and-limitations"></a>需求及限制

- 網域成員資格也適用於支援周邊網路以網際網路為基礎之用戶端管理的站台系統。 (這些網路也稱為 DMZ (非軍事區域)，以及過濾的子網路)。  

- 您無法為裝載站台系統角色的電腦變更下列設定：  

  - 網域成員資格，包括將站台系統從網域移除，然後重新加入相同的網域。

  - 網域名稱  

  - 電腦名稱  

  在進行這些變更之前，請先解除安裝網站系統角色。 若要對站台伺服器進行這些變更，請先解除安裝站台。 您也可以考慮建立[被動模式的站台伺服器](../../servers/deploy/configure/site-server-high-availability.md)以協助管理站台伺服器上的此變更。

- Configuration Manager 支援 Windows Server 2008 R2 或更新版本的網域與樹系功能等級。<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> 脫離的命名空間

您可以在具有*脫離之命名空間*的網域中安裝 Configuration Manager 站台系統與用戶端。  

在脫離的命名空間中，電腦的主要 DNS 尾碼不符合該電腦的 Active Directory DNS 網域名稱。 另一個脫離的命名空間案例則發生於網域控制站的 NetBIOS 網域名稱不符合 Active Directory DNS 網域名稱時。  

### <a name="disjoint-scenarios"></a>脫離的案例

下列各節識別脫離的命名空間的支援案例。  

#### <a name="scenario-1"></a>案例 1

網域控制站的主要 DNS 尾碼與 Active Directory DNS 網域名稱不同。 身為網域成員的電腦不一定會脫離。

網域控制站在此案例中是脫離的。 屬於網域成員的電腦 (例如站台伺服器與電腦) 可以有符合下列項目的主要 DNS 尾碼：

- 網域控制站的主要 DNS 尾碼
- Active Directory DNS 網域名稱

#### <a name="scenario-2"></a>案例 2

Active Directory 網域成員電腦是脫離的，但網域控制站不脫離。

在此案例中，站台系統的主要 DNS 尾碼與 Active Directory DNS 網域名稱不同。 網域控制站的主要 DNS 尾碼與 Active Directory DNS 網域相同。 Configuration Manager 用戶端的成員電腦可以有符合下列項目的主要 DNS 尾碼：

- 脫離的站台系統伺服器的主要 DNS 尾碼
- Active Directory DNS 網域名稱

### <a name="configure-disjoint-namespace"></a>設定脫離的命名空間

若要允許電腦存取脫離的網域控制站，您必須變更網域物件容器上的 **msDS-AllowedDNSSuffixes** Active Directory 屬性。 將兩個 DNS 尾碼都新增到屬性。  

為了確定 *DNS 尾碼搜尋清單*包含組織中的所有 DNS 命名空間，您必須針對脫離網域中的每部電腦設定搜尋清單。 在命名空間清單中包括下列尾碼：

- 網域控制站的主要 DNS 尾碼
- DNS 網域名稱
- Configuration Manager 可能與其通訊之任何其他伺服器的其他命名空間

您可以使用群組原則來設定 [網域名稱系統 (DNS) 尾碼搜尋]  清單。  

> [!IMPORTANT]  
> 當您在 Configuration Manager 中參考電腦時，請使用主要 DNS 尾碼來輸入電腦。 這個尾碼應該符合註冊為 Active Directory 網域中 **dnsHostName** 屬性的完整網域名稱，和與系統相關聯的服務主體名稱。  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> 單一標籤網域

當符合下列準則時，Configuration Manager 支援單一標籤網域中的站台系統及用戶端：  

- 使用具有有效的頂層網域的脫離 DNS 命名空間來設定 Active Directory 網域服務中的單一標籤網域。  

  **例如：** Contoso 的單一標籤網域已設定為在 contoso.com 的 DNS 中具有脫離的命名空間。 當您為 Contoso 網域中的電腦指定 Configuration Manager 中的 DNS 尾碼時，您會指定 "Contoso.com"，而不是 "Contoso"。  

- 系統內容中的站台伺服器之間的分散式元件物件模型 (DCOM) 連線必須成功使用 Kerberos 驗證。  
