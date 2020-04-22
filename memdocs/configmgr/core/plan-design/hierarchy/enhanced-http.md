---
title: 增強 HTTP
titleSuffix: Configuration Manager
description: 使用新式驗證來保護用戶端通訊安全，而不需使用 PKI 憑證。
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb14830e99600da1b71c516a44d51a0090cdc673
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703566"
---
# <a name="enhanced-http"></a>增強 HTTP

適用於：  Configuration Manager (最新分支)

<!--1356889,1358460-->

> [!Tip]  
> 這項功能最初是以[發行前版本功能](../../servers/manage/pre-release-features.md)的形式引進 1806 版。 從 1810 版開始，這項功能就不再是發行前版本功能。  

Microsoft 建議為所有 Configuration Manager 通訊路徑使用 HTTPS 通訊，不過管理 PKI 憑證需付出額外的人力物力，對於某些客戶而言難以辦到。

Configuration Manager 1806 版包含用戶端與站台系統通訊方式的改進。 這些增強的功能，目前有兩個主要的目標：  

- 您不需使用 PKI 伺服器驗證憑證，即可確保敏感性用戶端通訊的安全，。  

- 用戶端可以安全地從發佈點存取內容，而不需要網路存取帳戶、用戶端 PKI 憑證及 Windows 驗證。  

所有其他用戶端通訊皆透過 HTTPS 進行。 增強 HTTP 與針對用戶端通訊或站台系統啟用 HTTPS 不同。<!-- SCCMDocs issue #1212 -->

> [!Note]  
> 對於有下列需要的客戶而言，PKI 憑證仍是有效的選項：  
>
> - 所有用戶端通訊皆透過 HTTPS 進行  
> - 進階控制簽署基礎結構
>
> 此外，如果已在使用 PKI，即使增強的 HTTP 已開啟，仍會使用繫結在 IIS 中的 PKI 憑證。



## <a name="scenarios"></a><a name="bkmk_scenario"></a> 案例

以下案例會因為這些增強的功能而獲益：  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> 案例 1：用戶端對管理點

<!--1356889-->
[加入 Azure Active Directory (Azure AD) 的裝置](/azure/active-directory/devices/concept-azure-ad-join)可與針對 HTTP 設定的管理點通訊。 站台伺服器會為管理點產生一個憑證，讓它可以透過安全通道進行通訊。

> [!Note]  
> 此行為從 Configuration Manager 目前的分支版本 1802 變更而來，該版本需要啟用 HTTPS 的管理點，才能讓加入 Azure AD 的用戶端透過雲端管理閘道通訊。 如需詳細資訊，請參閱[啟用 HTTPS 的管理點](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps)。  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> 案例 2：複製到發佈點

<!--1358228-->
工作群組或加入 Azure AD 的用戶端，可以從針對 HTTP 設定的發佈點透過安全通道來驗證與下載內容。 這些類型的裝置也可以從針對 HTTPS 設定的發佈點驗證及下載內容，而不需要用戶端具有 PKI 憑證。 將用戶端驗證憑證新增至工作群組或加入 Azure AD 的用戶端而言較為困難。

此行為包括從開機媒體、PXE、或軟體中心執行工作順序的 OS 部署案例。 如需詳細資訊，請參閱[網路存取帳戶](accounts.md#network-access-account)。<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> 案例 3：Azure AD 裝置身分識別

<!--1358460-->
加入 Azure AD 或沒有任何 Azure AD 使用者登入的[混合式 Azure AD 裝置](/azure/active-directory/devices/concept-azure-ad-join-hybrid)，可以安全地與其指派站台通訊。 針對以裝置為主的案例，現在只要有雲端裝置身分識別，便能向 CMG 和管理點驗證。 (至於以使用者為主的案例，則仍需使用者權杖。)  


## <a name="features"></a>功能

下列 Configuration Manager 功能均支援或需要增強 HTTP：

- [雲端管理閘道](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [不使用網路存取帳戶進行 OS 部署](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [為新的網際網路型 Windows 10 裝置啟用共同管理](../../../comanage/tutorial-co-manage-new-devices.md)
- [透過電子郵件核准應用程式](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [系統管理服務](../../../develop/adminservice/overview.md)
- [檢視最近連線的主控台](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> 軟體更新點及相關案例一直以來都支援用戶端以及雲端管理閘道的安全 HTTP 流量。 它所使用的管理點機制與憑證型或權杖型驗證不同。<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>先決條件  

- 為 HTTP 用戶端連線設定的管理點。 請在管理點角色屬性的 [一般]  索引標籤上設定此選項。  

- 為 HTTP 用戶端連線設定的發佈點。 請在發佈點角色內容的 [通訊]  索引標籤上設定此選項。 請勿為此選項啟用 [允許用戶端匿名連線]  。  

- 將站台與 Azure AD 搭配以進行雲端管理。  

    - 如果您的站台已符合此項必要條件，則您需要更新 Azure AD 應用程式。 在 Configuration Manager 主控台中，移至 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [Azure Active Directory 租用戶]  。 選取 Azure AD 租用戶，接著選取 [應用程式]  窗格中的 Web 應用程式，再選取功能區中的 [更新應用程式設定]  。  

- *僅適用於[案例 3](#bkmk_scenario3)* ：執行 Windows 10 版本 1803 或更新版本且已加入 Azure AD 的用戶端。 用戶端需要此設定，才能進行 Azure AD 裝置驗證。<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>設定站台

1. 在 Configuration Manager 主控台中，前往 [系統管理]  工作區，展開 [站台設定]  ，然後選取 [站台]  節點。 選取站台，然後選擇功能區中的 [屬性]  。  

2. 切換至 [用戶端電腦通訊]  索引標籤。

    > [!Note]
    > 從 1906 版開始，此索引標籤稱為 [通訊安全性]  。<!-- SCCMDocs#1645 -->  

    選取適用於 **HTTPS 或 HTTP** 的選項。 然後啟用 [為 HTTP 站台系統使用 Configuration Manager 產生的憑證]  選項。

> [!Tip]
> 等候管理點從站台接收和設定新憑證，最長 30 分鐘。

<!--3798957-->
從 1902 版開始，您也可以為管理中心網站啟用增強 HTTP。 使用這個相同的程序，並開啟管理中心網站的屬性。 此動作只會為管理中心網站的 SMS 提供者角色啟用增強 HTTP。 它不是適用於階層中所有網站的全域設定。

您可以在 Configuration Manager 主控台中查看這些憑證。 移至 [系統管理]  工作空間，展開 [安全性]  ，然後選取 [憑證]  節點。 尋找 **SMS 發行**根憑證，以及 SMS 發行根簽發的站台伺服器角色憑證。

如需用戶端如何使用此設定與管理點和發佈點通訊的詳細資訊，請參閱[從用戶端到站台系統與服務的通訊](communications-between-endpoints.md#Planning_Client_to_Site_System)。


## <a name="see-also"></a>請參閱

- [規劃安全性](../security/plan-for-security.md)  

- [Configuration Manager 用戶端的安全性和隱私權](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [設定安全性](../security/configure-security.md)  

- [端點間的通訊](communications-between-endpoints.md)  
