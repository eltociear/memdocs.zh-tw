---
title: 設定安全性
titleSuffix: Configuration Manager
description: 設定 Configuration Manager 的安全性相關選項。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701406"
---
# <a name="configure-security-in-configuration-manager"></a>設定 Configuration Manager 中的安全性

適用於：  Configuration Manager (最新分支)

使用本文的資訊，協助您設定 Configuration Manager 的安全性相關選項。 其中包含下列安全性選項：
- 適用於用戶端 PKI 憑證的[用戶端電腦通訊](#BKMK_ConfigureClientPKI)  
- [簽署和加密](#BKMK_ConfigureSigningEncryption)  
- [以角色為基礎的系統管理](#BKMK_ConfigureRBA)  
- [管理帳戶](#BKMK_ManageAccounts)  
- [設定 Azure Active Directory](#bkmk_azuread)  
- [設定 SMS 提供者驗證](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> 設定用戶端 PKI 憑證的設定  

如果您想要使用公開金鑰基礎結構 (PKI) 憑證，和使用 Internet Information Services (IIS) 的站台系統進行用戶端連線，請使用下列程序設定這些憑證的設定。  

#### <a name="to-configure-client-pki-certificate-settings"></a>設定用戶端 PKI 憑證設定  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取主要站台進行設定。  

2.  在功能區中，選擇 [內容]  。 然後切換至 [用戶端電腦通訊]  索引標籤。  

    > [!Note]
    > 從 1906 版開始，此索引標籤稱為**通訊安全性**。<!-- SCCMDocs#1645 -->  

3.  為使用 IIS 的站台系統選取設定。  

    - **僅 HTTPS**：指派給站台之用戶端在連線到使用 IIS 的站台系統時，一律會使用用戶端 PKI 憑證。  

    - **HTTPS 或 HTTP**：您不需要用戶端即可使用 PKI 憑證。  

    - **對 HTTP 站台系統使用 Configuration Manager 產生的憑證**：如需此設定的詳細資訊，請參閱[增強 HTTP](../hierarchy/enhanced-http.md)。  

4.  為用戶端電腦選取設定。  

    - **使用可用的用戶端 PKI 憑證 (用戶端驗證功能)** ：如果您已選擇 [HTTPS 或 HTTP]  站台伺服器設定，選擇此選項可使用用戶端 PKI 憑證進行 HTTP 連線。 用戶端會改用此憑證而非使用自我簽署憑證，以對站台系統做自我驗證。 如果您選擇 [僅 HTTPS]  ，則會自動選擇此選項。  

    當用戶端有多個有效的 PKI 用戶端憑證可用時，選擇 [修改]  可設定用戶端憑證選取方法。  

    如需用戶端憑證選擇方法的詳細資訊，請參閱[規劃 PKI 用戶端憑證選擇](plan-for-security.md#BKMK_PlanningForClientCertificateSelection)。  

    - **由用戶端檢查站台系統的憑證撤銷清單 (CRL)** ：啟用此設定可讓用戶端檢查您組織的 CRL 中是否有已撤銷憑證。  

    如需用戶端 CRL 檢查的詳細資訊，請參閱[規劃 PKI 憑證撤銷](plan-for-security.md#BKMK_PlanningForCRLs)。  

5.  若要匯入、檢視和刪除受信任根憑證授權單位中的憑證，請選擇 [設定]  。  

    如需詳細資訊，請參閱[規劃 PKI 受信任根憑證及憑證簽發者清單](plan-for-security.md#BKMK_PlanningForRootCAs)。  


為階層中的所有主要站台重複此程序。  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> 設定簽署及加密  

為站台系統設定站台之所有用戶端皆支援的最安全簽署及加密設定。 這些設定在您讓用戶端使用自我簽署憑證透過 HTTP 與站台系統通訊時，尤其重要。  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>設定站台的簽署及加密  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取主要站台進行設定。  

2.  在功能區中，選取 [內容]  ，然後切換至 [簽署和加密]  索引標籤。  

    這個索引標籤只能在主要站台使用。 如果沒有看到 [簽署和加密]  索引標籤，請確定您未連線到管理中心網站或次要站台。  

3.  設定 [簽署和加密] 選項讓用戶端可以與站台通訊。  

    - **需要簽署**：用戶端會先簽署資料，再傳送至管理點。  

    - **需要 SHA-256**：用戶端使用 SHA-256 演算法來簽署資料。  

    > [!WARNING]  
    >  請先確認所有用戶端皆支援此雜湊演算法，再啟用 [需要 SHA-256]  。 這些用戶端包含未來可能指派給站台的用戶端。  
    >   
    >  如果您選擇此選項，但具有自我簽署憑證的用戶端無法支援 SHA-256，則 Configuration Manager 會拒絕這些用戶端。 SMS_MP_CONTROL_MANAGER 元件會記錄訊息識別碼 5443。  

    - **使用加密**：用戶端會先加密用戶端清查資料和狀態訊息，再傳送至管理點。 其使用 3DES 演算法。  

為階層中的所有主要站台重複此程序。  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> 設定以角色為基礎的系統管理  

以角色為基礎的系統管理結合了安全性角色、安全性範圍和指派的集合，為每個系統管理使用者定義系統管理範圍。 此範圍包含使用者可以在主控台中檢視的物件，以及與這些使用者擁有執行權限之物件相關的工作。 以角色為基礎的系統管理設定會套用到階層中的每個站台。  

如需詳細資訊，請參閱[設定以角色為基礎的系統管理](../../servers/deploy/configure/configure-role-based-administration.md)。 本文詳細說明下列動作：  

- 建立自訂安全性角色  

- 設定安全性角色  

- 設定物件的安全性範圍  

- 設定集合以管理安全性  

- 建立新的系統管理使用者  

- 修改系統管理使用者的系統管理範圍  

> [!IMPORTANT]  
>  您自己的系統管理範圍，定義您在為其他系統管理使用者設定以角色為基礎的系統管理時，可指派的物件和設定。 如需以角色為基礎的系統管理資訊，請參閱[以角色為基礎的系統管理基本概念](../../understand/fundamentals-of-role-based-administration.md)。  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a> 管理 Configuration Manager 使用的帳戶  

Configuration Manager 支援用於多種不同工作及用途的 Windows 帳戶。 若要檢視針對不同工作設定的帳戶，以及管理 Configuration Manager 用於每個帳戶的密碼，請使用下列程序：  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>管理 Configuration Manager 使用的帳戶  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [安全性]  ，然後選擇 [帳戶]  節點。  

2.  若要變更帳戶的密碼，請從清單中選取帳戶。 然後在功能區中，選擇 [內容]  。  

3.  選擇 [設定]  開啟 [Windows 使用者帳戶]  對話方塊。 指定 Configuration Manager 用於此帳戶的新密碼。  

    > [!NOTE]  
    >  您指定的密碼必須符合此帳戶在 Active Directory 中的密碼。  

如需詳細資訊，請參閱 [Accounts used in Configuration Manager](../hierarchy/accounts.md) (Configuration Manager 中使用的帳戶)。



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a> 設定 Azure Active Directory

整合 Configuration Manager 與 Azure Active Directory (Azure AD) 可簡化您的環境並啟用其雲端功能。 讓站台和用戶端使用 Azure AD 進行驗證。 如需詳細資訊，請參閱[設定 Azure 服務](../../servers/deploy/configure/azure-services-wizard.md)中的**雲端管理**服務。



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a> 設定 SMS 提供者驗證

從 1810 版開始，您可以指定系統管理員存取 Configuration Manager 站台的最低驗證層級。 這項功能會強制系統管理員以必要層級登入 Windows。 如需詳細資訊，請參閱[規劃 SMS 提供者](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)。 <!--1357013-->  



## <a name="see-also"></a>請參閱

- [規劃安全性](plan-for-security.md)  

- [Configuration Manager 用戶端的安全性和隱私權](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [端點間的通訊](../hierarchy/communications-between-endpoints.md)  

- [密碼編譯控制技術參考](cryptographic-controls-technical-reference.md)  

- [PKI 憑證需求](../network/pki-certificate-requirements.md)  
