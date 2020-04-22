---
title: 安全性基本概念
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的安全性階層。
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707056"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Configuration Manager 的安全性基本概念

適用於：  Configuration Manager (最新分支)

本文摘要說明下列任一 Configuration Manager 環境的基本安全性元件：
- [安全性階層](#bkmk_layers)
- [以角色為基礎的系統管理](#bkmk_rba)
- [確保用戶端端點安全](#bkmk_endpoints)
- [Configuration Manager 帳戶和群組](#bkmk_accounts)
- [隱私權](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> 安全性階層

Configuration Manager 的安全性階層分為下列幾項： 
- [Windows OS 和網路安全性](#bkmk_layer-windows)
- [網路基礎結構：防火牆、入侵偵測、公開金鑰基礎結構 (PKI)](#bkmk_layer-network)
- [Configuration Manager 安全性控制](#bkmk_layer-cm)
- [SMS 提供者](#bkmk_layer-provider)
- [網站資料庫權限](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Windows OS 和網路安全性
第一層由 Windows 安全性功能針對 OS 及網路所提供。 這一層包含下列元件：  

-   在 Configuration Manager 元件之間傳輸檔案的檔案共用  

-   存取控制清單 (ACL) 可確保檔案和登錄機碼的安全  

-   網際網路通訊協定安全性 (IPsec) 可確保通訊安全  

-   群組原則可設定安全性原則  

-   分散式元件物件模型 (DCOM) 權限可用於分散式應用程式，例如 Configuration Manager 主控台  

-   Active Directory 網域服務可儲存安全性原則  

-   Windows 帳戶安全性，包括 Configuration Manager 在安裝期間建立的部分群組  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> 網路基礎結構

額外的安全性元件，例如防火牆和入侵偵測，可協助提供整個環境的防護。 由符合業界標準的公開金鑰基礎結構 (PKI) 實作所發行之憑證可協助提供驗證、簽署和加密。  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Configuration Manager 安全性控制

除了 Windows 伺服器和網路基礎結構所提供的安全性之外，Configuration Manager 也會以數種方式控制對其主控台與資源的存取。 依預設，只有本機系統管理員有權存取檔案和登錄機碼，以在您安裝 Configuration Manager 的電腦上執行主控台。  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> SMS 提供者

下一層安全性以透過 Windows Management Instrumentation (WMI) 的存取為基礎，特別是 SMS 提供者。 「SMS 提供者」是一個 Configuration Manager 元件，授與使用者查詢站台資料庫以取得資訊的存取權。 依照預設，對提供者的存取權已限制為僅授與本機 SMS Admins 群組的成員。 此群組一開始僅包含已安裝 Configuration Manager 的使用者。 若要將其他帳戶權限授與給通用訊息模型 (CIM) 存放庫和 SMS 提供者，請新增其他帳戶到 SMS Admins 群組。  

從 1810 版開始，您可以指定系統管理員存取 Configuration Manager 站台的最低驗證層級。 這項功能會強制系統管理員以必要層級登入 Windows。 <!--1357013-->  

如需詳細資訊，請參閱[規劃 SMS 提供者](../plan-design/hierarchy/plan-for-the-sms-provider.md)。

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> 站台資料庫權限

最後一層安全性是基於網站資料庫中物件的權限。 依預設，您安裝 Configuration Manager 時使用的本機系統帳戶和使用者帳戶，都有權限管理站台資料庫中的所有物件。 使用以角色為基礎的系統管理，對 Configuration Manager 主控台中的額外系統管理使用者授與或限制權限。  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a> 以角色為基礎的系統管理  

 Configuration Manager 使用以角色為基礎的系統管理，協助保護集合、部署及站台這類物件。 此管理模式主要針對所有網站和網站設定，定義與管理整個階層的安全性存取權設定。 

 系統管理員會指派「安全性角色」  給系統管理使用者和群組權限。 這些權限會連線到不同的 Configuration Manager 物件類型，例如建立或變更用戶端設定。 

 *安全性範圍*會將系統管理使用者負責管理的特定物件執行個體 (例如安裝 Microsoft Office 的應用程式) 分組。 

 結合安全性角色、安全性範圍和集合來定義系統管理使用者可檢視與管理的物件。 Configuration Manager 安裝部分預設安全性角色以進行一般管理工作。 建立自己的安全性角色來支援特定的業務需求。  

 如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../servers/deploy/configure/configure-role-based-administration.md)。  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> 確保用戶端端點安全  

 Configuration Manager 使用自我簽署/PKI 憑證或 Azure Active Directory (Azure AD) 權杖來保護用戶端與站台系統角色間的通訊。 某些情況下需要使用 PKI 憑證。 例如，[以網際網路為基礎的用戶端管理](../clients/manage/plan-internet-based-client-management.md)，以及面對[行動裝置用戶端](../../mdm/plan-design/plan-on-premises-mdm.md)時。  

 您可為用戶端連線的站台系統角色設定 HTTPS 或 HTTP 用戶端通訊。 用戶端電腦一律會使用最安全的可用方法來通訊。 只有在您的站台系統角色允許 HTTP 通訊時，用戶端電腦才會退而使用較不安全的通訊方法。  

 如需詳細資訊，請參閱[規劃安全性](../plan-design/security/plan-for-security.md)。



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Configuration Manager 帳戶和群組  

 Configuration Manager 在進行大部分站台作業時會使用本機系統帳戶。 部分管理工作可能需要建立與維護額外帳戶。 Configuration Manager 會在安裝期間建立數個預設群組和 SQL Server 角色。 您可能需要將電腦或使用者帳戶手動新增到預設群組和 SQL Server 角色。  

 如需詳細資訊，請參閱 [Accounts used in Configuration Manager](../plan-design/hierarchy/accounts.md) (Configuration Manager 中使用的帳戶)。  



## <a name="privacy"></a><a name="bkmk_privacy"></a> 隱私權  

 在實作 Configuration Manager 之前，請先考慮您的隱私權需求。 雖然企業管理產品能夠有效管理大量的用戶端而具備許多優點，但此軟體可能會影響組織中的使用者隱私權。 Configuration Manager 內含許多可用來收集資料和監視裝置的工具。 部分工具可能會引發組織中的隱私權疑慮。  

 例如，當您安裝 Configuration Manager 用戶端時，許多管理設定都會預設為啟用。 此設定會導致用戶端軟體將資訊傳送到 Configuration Manager 站台。 此站台會將用戶端資訊儲存在站台資料庫中， 而不會將用戶端資訊直接傳送至 Microsoft。 如需詳細資訊，請參閱[診斷和使用方式資料](../plan-design/diagnostics/diagnostics-and-usage-data.md)。



## <a name="see-also"></a>請參閱

- [規劃安全性](../plan-design/security/plan-for-security.md)  

- [Configuration Manager 用戶端的安全性和隱私權](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [設定安全性](../plan-design/security/configure-security.md)   

- [端點間的通訊](../plan-design/hierarchy/communications-between-endpoints.md)  

- [密碼編譯控制技術參考](../plan-design/security/cryptographic-controls-technical-reference.md)  
