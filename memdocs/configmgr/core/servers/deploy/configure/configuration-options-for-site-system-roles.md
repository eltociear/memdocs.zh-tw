---
title: 站台系統角色選項
titleSuffix: Configuration Manager
description: 如需不一定一目了然的 Configuration Manager 站台系統角色的詳細資訊，請參閱這篇文章。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704806"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Configuration Manager 中站台系統角色的設定選項

適用於：  Configuration Manager (最新分支)

Configuration Manager 站台系統角色的大部分設定選項都是一目了然，或是您在設定它們時就已在精靈或對話方塊中加以說明。 下列各節說明其設定可能需要其他資訊的站台系統角色。  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> 應用程式類別目錄網站點  

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

如需有關如何設定應用程式類別目錄網站點的詳細資訊，請參閱[規劃和設定應用程式管理](../../../../apps/plan-design/plan-for-and-configure-application-management.md)。  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> 應用程式類別目錄 Web 服務點  

> [!Important]
> 從 1806 最新分支版本開始即不支援應用程式類別目錄的 Silverlight 使用者體驗。 從 1906 版開始，已更新的用戶端會自動使用適用於使用者可用應用程式部署的管理點。 此外，您也無法安裝新的應用程式目錄角色。 1910 版會終止對應用程式類別目錄角色的支援。  
>
> 如需詳細資訊，請參閱下列文章：
>
> - [設定軟體中心](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已移除和已淘汰的功能](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

如需如何設定應用程式類別目錄 Web 服務點的詳細資訊，請參閱[規劃和設定應用程式管理](../../../../apps/plan-design/plan-for-and-configure-application-management.md)。  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> 憑證登錄點  

如需如何設定憑證登錄點的詳細資訊，請參閱[憑證設定檔簡介](../../../../protect/deploy-use/introduction-to-certificate-profiles.md)。  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a> 發佈點  

如需如何設定內容部署發佈點的詳細資訊，請參閱[管理內容與內容基礎結構](manage-content-and-content-infrastructure.md)。  

如需如何設定 PXE 部署發佈點的詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

如需如何設定多點傳送部署發佈點的詳細資訊，請參閱[使用多點傳送透過網路部署 Windows](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>在 Configuration Manager 需要時安裝並設定 IIS

選取此選項，讓 Configuration Manager 在站台系統上安裝及設定 IIS (如果尚未安裝)。 IIS 必須安裝在所有發佈點上，而且您必須選取此設定以在精靈中繼續操作。  

### <a name="site-system-installation-account"></a>站台系統安裝帳戶

對於安裝在站台伺服器的發佈點，只有站台伺服器的電腦帳戶可以當成站台系統安裝帳戶來使用。 如需詳細資訊，請參閱[帳戶](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)。  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> 註冊點  

註冊點可用來安裝 macOS 電腦，以及註冊您利用內部部署行動裝置管理所管理的裝置。 如需詳細資訊，請參閱下列文章：  

- [如何將用戶端部署至 Mac](../../../clients/deploy/deploy-clients-to-macs.md)  

- [使用者如何使用內部部署 MDM 註冊裝置](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>允許的連線

HTTPS 設定會自動選取，且需要在伺服器上提供 PKI 憑證，才能用於對註冊 Proxy 點進行伺服器驗證，並透過 SSL 進行資料加密。 如需詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。  

如需伺服器憑證的範例部署，以及如何在 IIS 中進行設定的相關資訊，請參閱[為執行 IIS 的站台系統部署 Web 伺服器憑證](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> 註冊 Proxy 點  

如需如何為行動裝置設定註冊 Proxy 點的詳細資訊，請參閱[使用者如何使用內部部署 MDM 註冊裝置](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)。  

### <a name="client-connections"></a>用戶端連線

系統會自動選取 HTTPS 設定。 它在伺服器上需要有下列 PKI 憑證：

- 對您使用 Configuration Manager 註冊的行動裝置和 Mac 電腦進行的伺服器驗證
- 透過安全通訊端層 (SSL) 的資料加密

如需憑證需求的詳細資訊，請參閱 [PKI 憑證需求](../../../plan-design/network/pki-certificate-requirements.md)。  

如需伺服器憑證的範例部署，以及如何在 IIS 中進行設定的相關資訊，請參閱[為執行 IIS 的站台系統部署 Web 伺服器憑證](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> 後援狀態點  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>狀況訊息數目和節流間隔 (秒)

這些選項的預設設定是 10,000 則狀況訊息和 3,600 秒的節流間隔。 雖然這些設定足以應付大部分的情況，但您可能必須在下列兩個條件都成立時變更它們：  

- 後援狀態點僅接受來自內部網路的連線。  

- 在為多部電腦進行用戶端部署首展期間，您會使用後援狀態點。  

在此案例中，持續的狀況訊息資料流可能會造成狀況訊息的積存，該積存會使得站台伺服器上處理器使用量過高的情況持續一段時間。 此外，您可能會看不到 Configuration Manager 主控台以及在用戶端部署報告中用戶端部署的最新資訊。  

這些後援狀態點的設計，主要是針對用戶端部署期間所產生狀態訊息進行設定。 這些設定並不是針對用戶端通訊問題而設計的，例如，當網際網路上的用戶端無法連線到以網際網路為基礎的管理點時。 由於後援狀態點無法只將這些設定套用到在用戶端部署期間所產生的狀況訊息，因此，請勿在後援狀態點接受來自網際網路的連線時設定這些設定。  

成功安裝 Configuration Manager 用戶端的每一部電腦，都會將下列四種狀況訊息傳送到後援狀態點：  

- 已啟動用戶端部署  

- 成功完成用戶端部署  

- 已啟動用戶端指派  

- 成功完成用戶端指派  

無法安裝的電腦或指派 Configuration Manager 用戶端的電腦，都會傳送其他的狀況訊息。  

例如，假設您將 Configuration Manager 用戶端部署到 20,000 部電腦，部署可能會傳送 80,000 個狀態訊息到後援狀態點。 因為預設的節流設定可每 3600 秒 (1 小時) 傳送 10,000 個狀態訊息到後援狀態點，所以狀態訊息可能會積存在後援狀態點上。 此外，也必須考慮到後援狀態點和站台伺服器之間的可用網路頻寬，以及可處理許多狀況訊息之站台伺服器的處理能力。  

為避免發生這些問題，請考慮增加狀態訊息數目，並縮短節流間隔時間。  

如果下列其中一項條件為 True，請重設後援狀態點的節流值：  

- 您估計目前的節流值，比處理來自後援狀態點之狀況訊息所需的節流值還要高。  

- 您發現目前的節流設定會在站台伺服器上導致高處理器使用量。  

除非您了解會產生何種結果，否則請勿變更後援狀態點節流設定的設定值。 例如，當您提高節流設定時，站台伺服器上的處理器使用量就會增高，進而造成所有的站台作業變得緩慢。  
