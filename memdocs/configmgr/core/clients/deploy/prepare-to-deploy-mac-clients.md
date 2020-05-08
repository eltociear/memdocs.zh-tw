---
title: 準備將用戶端部署至 Mac
titleSuffix: Configuration Manager
description: 先完成設定工作，再將 Configuration Manager 用戶端部署至 Mac。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b5bcbce659601e10f44f06af94eb939767a389a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906632"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>準備將用戶端軟體部署到 Mac

適用於：  Configuration Manager (最新分支)

請遵循這些步驟以確保您準備好[將 Configuration Manager 用戶端部署至 Mac 電腦](deploy-clients-to-macs.md)。



## <a name="mac-prerequisites"></a>Mac 必要條件

Configuration Manager 媒體未隨附 Mac 用戶端安裝套件。 從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=47719)下載**其他作業系統的用戶端**。  

如需支援版本的清單，請參閱[支援用戶端和裝置的作業系統](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)。



## <a name="certificate-requirements"></a>憑證需求

Mac 電腦的用戶端安裝和管理需要公開金鑰基礎結構 (PKI) 憑證。 PKI 憑證會使用相互驗證及加密的資料傳送，對 Mac 電腦和 Configuration Manager 站台之間的通訊進行加密。 Configuration Manager 可以要求並安裝使用者用戶端憑證。 會搭配企業憑證授權使用憑證服務，以及 Configuration Manager 註冊點和註冊 Proxy 點。 您也可以不透過 Configuration Manager 來要求並安裝電腦憑證。 此憑證必須符合 Configuration Manager 憑證需求。  

Configuration Manager Mac 用戶端一律會執行憑證撤銷檢查。 您無法停用此功能。  

如果 Mac 用戶端找不到憑證撤銷清單 (CRL)，將無法連線至 Configuration Manager 站台系統。 特別是針對在不同樹系中發行憑證授權的 Mac 用戶端，請檢查您的 CRL 設計。 請確定 Mac 用戶端可以找出並下載 CRL。  

您必須先決定要如何安裝用戶端憑證，才能在 Mac 電腦上安裝 Configuration Manager 用戶端：  

-   利用 [CMEnroll 工具](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll)使用 Configuration Manager 註冊。 註冊程序不支援自動憑證更新。 在憑證到期前，請重新註冊 Mac 電腦。  

-   [使用獨立於 Configuration Manager 的憑證要求和安裝方法](deploy-clients-to-macs.md#bkmk_external)。  

如需 Mac 用戶端憑證需求的詳細資訊，請參閱 [Configuration Manager 的 PKI 憑證需求](../../plan-design/network/pki-certificate-requirements.md)。  

Mac 用戶端會自動指派給管理它們的 Configuration Manager 站台。 即使通訊受限於內部網路，Mac 用戶端還是會安裝為僅限網際網路的用戶端。 此設定表示 Mac 用戶端會在其指派的站台中，與啟用網際網路的管理點和發佈點進行通訊。 Mac 電腦不會與其指派的站台以外的站台系統通訊。  

> [!IMPORTANT]  
>  適用於 macOS 的 Configuration Manager 用戶端，無法用於連線到設定為使用[資料庫複本](../../servers/deploy/configure/database-replicas-for-management-points.md)的管理點。  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>將 Web 伺服器憑證部署至站台系統伺服器  

如果這些站台系統沒有 Web 伺服器憑證，請將此種憑證部署至具有這些站台系統角色的電腦︰  

-   管理點  

-   發佈點  

-   註冊點  

-   註冊 Proxy 點  

Web 伺服器憑證必須包含站台系統內容中指定的網際網路 FQDN。 伺服器不必從網際網路存取也能支援 Mac 電腦。 如果您不需要以網際網路為基礎的用戶端管理，您可以將網際網路 FQDN 指定為內部網路 FQDN 值。  

請在管理點、發佈點和註冊 Proxy 點的 Web 伺服器憑證中，指定站台系統的網際網路 FQDN 值。

如需範例部署的詳細資訊，請參閱[為執行 IIS 的站台系統部署 Web 伺服器憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>將用戶端驗證憑證部署至站台系統伺服器  

如果這些站台系統沒有用戶端驗證憑證，請將此種憑證部署至裝載這些站台系統角色的電腦：  

-   管理點  

-   發佈點  

如需建立及安裝管理點用戶端憑證的部署範例，請參閱[部署 Windows 電腦的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)。  

如需建立及安裝管理點用戶端憑證的部署範例，請參閱[部署發佈點的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)。  

> [!IMPORTANT]  
>  若要將用戶端部署到執行 macOS Sierra 的裝置上，必須正確設定管理點憑證的主體名稱。 例如，使用管理點伺服器的 FQDN。  



## <a name="prepare-the-client-certificate-template-for-macs"></a>準備 Mac 的用戶端憑證範本  

憑證範本必須擁有將在 Mac 電腦上註冊憑證之使用者帳戶的**讀取**和**註冊**權限。  

如需詳細資訊，請參閱[部署 Mac 電腦的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)。  



## <a name="configure-the-management-point-and-distribution-point"></a>設定管理點和發佈點  

為管理點設定下列選項：  

-   HTTPS  

-   允許用戶端從網際網路連線。 此設定值是管理 Mac 電腦所必備。 然而，這並不代表站台系統伺服器必須能夠從網際網路存取。  

-   允許行動裝置和 Mac 電腦使用此管理點  

安裝 Mac 的用戶端時不需要發佈點。 如果您要在安裝用戶端後將軟體部署到這些電腦，請設定發佈點以允許用戶端從網際網路連線。  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>設定管理點及發佈點以支援 Mac  

請確定使用網際網路 FQDN 設定執行管理點和發佈點，再開始執行此程序。 如果這些伺服器不支援以網際網路為基礎的用戶端管理，請將內部網路 FQDN 指定為網際網路 FQDN 值。

這些站台系統角色必須位於主要站台中。  

1.  在 Configuration Manager 主控台中，移至 [系統管理]  工作區，並展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。 然後選取具有正確站台系統角色的伺服器。  

2.  在詳細資料窗格中，選取 [管理點]  角色，然後在功能區中選取 [屬性]  。 在 [管理點屬性]  視窗中，設定這些選項：  

    1.  選擇 [HTTPS]  。  

    2.  選擇 [僅允許網際網路用戶端連線]  或 [允許內部網路和網際網路用戶端連線]  。 這些選項需要網際網路或內部網路 FQDN。  

    3.  選擇 [允許行動裝置和 Mac 電腦使用此管理點]  。  

    4. 按一下 [確定]  儲存這項設定。  

3.  在 [伺服器和站台系統角色] 節點詳細資料窗格中，選取 [發佈點]  角色，然後在功能區中選取 [屬性]  。 在 [發佈點屬性]  視窗中，設定這些選項：  

    -   選擇 [HTTPS]  。  

    -   選擇 [僅允許網際網路用戶端連線]  或 [允許內部網路和網際網路用戶端連線]  。 這些選項需要網際網路或內部網路 FQDN。  

    -   選擇 [匯入憑證]  ，瀏覽至匯出的用戶端發佈點憑證檔案，然後指定密碼。  

4.  針對主要站台中管理 Mac 電腦的所有管理點和發佈點，重複執行此程序。  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>設定註冊 Proxy 點和註冊點  

在相同站台中安裝這兩個角色。 您不一定要將這兩個角色安裝到同一部站台系統伺服器上，或相同的 Active Directory 樹系中。  

如需站台系統角色放置和考量的詳細資訊，請參閱[站台系統角色](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)。  

若要新增站台系統角色以支援 Mac 電腦，請參閱[安裝站台系統角色](../../servers/deploy/configure/install-site-system-roles.md)。

在 [系統角色選取]  頁面上，從可用角色的清單中選取 [註冊 Proxy 點]  和 [註冊點]  。  



## <a name="install-the-reporting-services-point"></a>安裝 Reporting Services 點  

如需詳細資訊，請參閱[安裝報表服務點](../../servers/manage/configuring-reporting.md)。  



## <a name="next-steps"></a>後續步驟

[將 Configuration Manager 用戶端部署至 Mac 電腦](deploy-clients-to-macs.md)  
