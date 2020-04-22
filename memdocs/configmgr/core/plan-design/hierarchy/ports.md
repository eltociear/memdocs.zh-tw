---
title: 用於連線的連接埠
titleSuffix: Configuration Manager
description: 了解設定管理員用於連線的必要和可自訂網路連接埠。
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0bb4f3f3dfcddaa12a8c6f3fffbe59954b10964a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704486"
---
# <a name="ports-used-in-configuration-manager"></a>設定管理員中使用的連接埠

適用於：  Configuration Manager (最新分支)

本文列出設定管理員使用的網路連接埠。 有些連線使用不可設定的連接埠，有些則支援您指定的自訂連接埠。 如果您使用任何連接埠篩選技術，請驗證所需連接埠是否可用。 這些連接埠篩選技術包括防火牆、路由器、Proxy 伺服器或 IPsec。   

> [!NOTE]  
> 如果使用 SSL 橋接功能支援以網際網路為基礎的用戶端，除了連接埠需求外，可能還必須允許某些 HTTP 動詞和標頭來周遊防火牆。   



##  <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> 您可以設定的連接埠  
Configuration Manager 可讓您設定用於下列通訊類型的連接埠：  

- 應用程式類別目錄網站點對應用程式類別目錄 Web 服務點  

- 註冊 Proxy 點對註冊點  

- 執行 IIS 的用戶端對站台系統  

- 用戶端對網際網路 (如 Proxy 伺服器設定)  

- 軟體更新點對網際網路 (如 Proxy 伺服器設定)  

- 軟體更新點對 WSUS 伺服器  

- 網站伺服器對網站資料庫伺服器  

- 站台伺服器對 WSUS 資料庫伺服器

- Reporting Services 點  

  > [!NOTE]  
  > 您必須在 SQL Server Reporting Services 中設定 Reporting Services 點站台系統角色所用的連接埠。 然後，Configuration Manager 會在與 Reporting Services 點通訊期間使用這些連接埠。 請務必檢閱這些連接埠，以定義用於 IPsec 原則或設定防火牆的 IP 篩選資訊。  

根據預設，用戶端對站台系統通訊所使用的 HTTP 連接埠是連接埠 80，且預設的 HTTPS 連接埠是 443。 您可以在安裝期間變更用戶端對站台系統的 HTTP 或 HTTPS 通訊連接埠，也可以在 Configuration Manager 站台的站台內容中進行變更。  

您必須在 SQL Server Reporting Services 中設定 Reporting Services 點站台系統角色所用的連接埠。 然後，Configuration Manager 會在與 Reporting Services 點通訊期間使用這些連接埠。 在您定義 IP 篩選資訊以用於 IPsec 原則或設定防火牆時，請務必檢閱這些連接埠。  



##  <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> 不可設定的連接埠  

設定管理員不允許設定用於下列通訊類型的連接埠：  

- 網站對網站  

- 網站伺服器對網站伺服器  

- Configuration Manager 主控台對 SMS 提供者  

- 設定管理員主控台對網際網路  

- 與 Microsoft Intune 和雲端發佈點等雲端服務的連線  



##  <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Configuration Manager 用戶端和站台系統使用的連接埠  

下列各節詳細說明 Configuration Manager 中用於通訊的連接埠。 章節標題中的箭頭顯示通訊方向：  

- -- > 表示其中一部電腦起始通訊，而另一部電腦一律會回應  

- &lt; -- > 表示兩部電腦皆可起始通訊  


###  <a name="asset-intelligence-synchronization-point-----microsoft"></a><a name="BKMK_PortsAI"></a> Asset Intelligence 同步處理點 -- > Microsoft  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="asset-intelligence-synchronization-point-----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Asset Intelligence 同步處理點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="application-catalog-web-service-point-----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> 應用程式類別目錄 Web 服務點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="application-catalog-website-point-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> 應用程式類別目錄網站點 -- > 應用程式類別目錄 Web 服務點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="client-----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> 用戶端 -- > 應用程式類別目錄網站點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="client-----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> 用戶端 -- &gt; 用戶端  

除了下表所列的連接埠之外，喚醒 Proxy 也會在用戶端之間使用 ICMP 回應要求訊息。 用戶端使用此通訊來確認網路上的另一個用戶端是否處於喚醒狀態。 ICMP 有時稱為 Ping 命令。 ICMP 沒有 UDP 或 TCP 通訊協定號碼，因此未列在下表中。 不過，這些用戶端電腦或子網路內中介網路裝置上的所有主機型防火牆都必須允許 ICMP 流量，否則喚醒 Proxy 通訊不會成功。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|網路喚醒|9 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|--|  
|喚醒 proxy|25536 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|--|  
|Windows PE 對等快取廣播|8004|--|  
|Windows PE 對等快取下載|--|8003|  

如需詳細資訊，請參閱 [Windows PE 對等快取](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements)。


###  <a name="client-----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a> 用戶端 -- > 設定管理員網路裝置註冊服務 (NDES) 原則模組   

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  


###  <a name="client-----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> 用戶端 -- > 雲端發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

如需詳細資訊，請參閱[連接埠和資料流程](use-a-cloud-based-distribution-point.md#bkmk_dataflow)。


###  <a name="client-----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a> 用戶端 -- > 雲端管理閘道 (CMG)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

如需詳細資訊，請參閱 [CMG 連接埠和資料流程](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。


###  <a name="client-----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a> 用戶端 -- > 發佈點，標準與提取兩者  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="client-----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a> 用戶端 -- > 設定用於多點傳送的發佈點，標準與提取  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|多點傳送通訊協定|63000-64000|--|  

###  <a name="client-----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a> 用戶端 -- > 設定用於 PXE 的發佈點，標準與提取  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 和 68|--|  
|TFTP|69 <sup>[附註 4](#bkmk_note4)</sup> |--|  
|開機資訊交涉階層 (BINL)|4011|--|  

> [!Important]  
> 如果您啟用主機型防火牆，請確定規則允許伺服器在這些連接埠上傳送和接收。 當您啟用 PXE 的發佈點時，設定管理員可以在 Windows 防火牆上啟用輸入 (接收) 規則。 它不會設定輸出 (傳送) 規則。<!--SCCMDocs issue #744-->  


###  <a name="client-----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> 用戶端 -- > 後援狀態點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="client-----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> 用戶端 -- > 通用類別目錄的網域控制站  
設定管理員用戶端屬於工作群組電腦或設定僅用於網際網路通訊時，不會連絡通用類別目錄伺服器。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|通用類別目錄 LDAP|--|3268|  


###  <a name="client-----management-point"></a><a name="BKMK_PortsClient-MP"></a> 用戶端 -- > 管理點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|用戶端通知 (後援至 HTTP 或 HTTPS 之前的預設通訊)|--|10123 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="client-----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> 用戶端 -- > 軟體更新點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 或 8530 <sup>[附註 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 或 8531 <sup>[附註 3](#bkmk_note3)</sup>|  


###  <a name="client-----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> 用戶端 -- > 狀態移轉點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|伺服器訊息區 (SMB)|--|445|  


###  <a name="cmg-connection-point-----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a> CMG 連接點 -- > CMG 雲端服務  

設定管理員會使用這些連線來建置 CMG 通道。 如需詳細資訊，請參閱 [CMG 連接埠和資料流程](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (偏好選項)|--|10140-10155|  
|HTTPS (以一部 VM 後援)|--|443|  
|HTTPS (以兩部或多部 VM 後援)|--|10124-10139|  


###  <a name="cmg-connection-point-----management-point"></a><a name="bkmk_cmgcp-mp"></a> CMG 連接點 -- > 管理點  

#### <a name="version-1706-or-1710"></a>1706 或 1710 版
具體連接埠會因管理點設定而有所不同。 

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

#### <a name="version-1802"></a>1802 版

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

如需詳細資訊，請參閱 [CMG 連接埠和資料流程](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。


###  <a name="cmg-connection-point-----software-update-point"></a><a name="bkmk_cmgcp-sup"></a> CMG 連接點 -- > 軟體更新點  

具體連接埠會因軟體更新點設定而有所不同。 

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

如需詳細資訊，請參閱 [CMG 連接埠和資料流程](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。


###  <a name="configuration-manager-console-----client"></a><a name="BKMK_PortsConsole-Client"></a> Configuration Manager 主控台 -- > 用戶端  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|遠端控制 (控制)|--|2701|  
|遠端協助 (RDP 和 RTC)|--|3389|  


###  <a name="configuration-manager-console-----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Configuration Manager 主控台 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

設定管理員主控台使用網際網路存取下列動作： 
- 從 Microsoft Update 下載部署套件的軟體更新。
- 功能區中的意見反應項目。
- 主控台中的文件連結。
<!--506823-->


###  <a name="configuration-manager-console-----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> 設定管理員主控台 -- > Reporting Services 點  


|說明|UDP|TCP|
|-----------------|---------|---------|   
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="configuration-manager-console-----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Configuration Manager 主控台 -- > 站台伺服器  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (與 WMI 的初始連線，用於尋找提供者系統)|--|135|  


###  <a name="configuration-manager-console-----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Configuration Manager 主控台 -- > SMS 提供者  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> 設定管理員網路裝置註冊服務 (NDES) 原則模組 -- > 憑證登錄點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="data-warehouse-service-point-----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a> 資料倉儲服務點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="distribution-point-both-standard-and-pull-----management-point"></a><a name="BKMK_PortsDist_MP"></a> 發佈點，標準與提取 -- > 管理點  
在下列情況中，發佈點會與管理點通訊：  

- 報告預先設置內容的狀態  

- 報告摘要資料的使用方式  

- 報告內容驗證  

- 報告套件下載 (僅限提取發佈點) 的狀態

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="endpoint-protection-point-----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection 點 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  


###  <a name="endpoint-protection-point-----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection 點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="enrollment-proxy-point-----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> 註冊 Proxy 點 -- > 註冊點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="enrollment-point-----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> 註冊點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="exchange-server-connector-----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server 連接器 -- &gt; Exchange Online  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|Windows 透過 HTTPS 的遠端管理|--|5986|  


###  <a name="exchange-server-connector-----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server 連接器 -- > 內部部署 Exchange Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 HTTP 的 Windows 遠端管理|--|5985|  


###  <a name="mac-computer-----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac 電腦 -- > 註冊 Proxy 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="management-point-----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> 管理點 -- > 網域控制站  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|輕量型目錄存取通訊協定 (LDAP)|389|389|  
|通用類別目錄 LDAP|--|3268|  
|RPC 端點對應程式|--|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="management-point-lt-----site-server"></a><a name="BKMK_PortsMP-Site"></a> 管理點 &lt; -- > 站台伺服器  
<sup>[附註 5](#bkmk_note5)</sup>   

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 端點對應程式|--|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  
|伺服器訊息區 (SMB)|--|445|  


###  <a name="management-point-----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> 管理點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="mobile-device-----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> 行動裝置 -- > 註冊 Proxy 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="mobile-device-----microsoft-intune"></a><a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> 行動裝置 -- > Microsoft Intune  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="reporting-services-point-----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Reporting Services 點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="service-connection-point-----microsoft-intune"></a><a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> 服務連接點 -- > Microsoft Intune  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

如需詳細資訊，請參閱服務連接點的[網際網路存取需求](../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls)。


###  <a name="service-connection-point-----azure-cmg"></a><a name="bkmk_scp-cmg"></a> 服務連接點 -- > Azure (CMG)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|適用於 CMG 服務部署的 HTTPS|--|443|

如需詳細資訊，請參閱 [CMG 連接埠和資料流程](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)。


###  <a name="site-server-lt-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> 站台伺服器 &lt; -- > 應用程式類別目錄 Web 服務點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> 站台伺服器 &lt; -- > 應用程式類別目錄網站點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> 站台伺服器 &lt; -- > Asset Intelligence 同步處理點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----client"></a><a name="BKMK_PortsSite-Client"></a> 站台伺服器 -- > 用戶端  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|網路喚醒|9 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|--|  


###  <a name="site-server-----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> 站台伺服器 -- > 雲端發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

如需詳細資訊，請參閱[連接埠和資料流程](use-a-cloud-based-distribution-point.md#bkmk_dataflow)。


###  <a name="site-server-----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a> 站台伺服器 -- > 發佈點，標準與提取兩者  
 <sup>[附註 5](#bkmk_note5)</sup>  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> 站台伺服器 -- > 網域控制站  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|輕量型目錄存取通訊協定 (LDAP)|389|389|  
|通用類別目錄 LDAP|--|3268|  
|RPC 端點對應程式|--|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> 站台伺服器 &lt; -- > 憑證登錄點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> 站台伺服器 &lt; -- > Endpoint Protection 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> 站台伺服器 &lt; -- > 註冊點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> 站台伺服器 &lt; -- > 註冊 Proxy 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> 站台伺服器 &lt; -- > 後援狀態點  
 <sup>[附註 5](#bkmk_note5)</sup>  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----internet"></a><a name="BKMK_PortSite-Internet"></a> 站台伺服器 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 1](#bkmk_note1)</sup>|  


###  <a name="site-server-lt-----issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> 站台伺服器 &lt; -- > 發行憑證授權單位 (CA)  
 當您想要藉由使用憑證登錄點來部署憑證設定檔時，可使用此項通訊。 並非階層中的每部站台伺服器都會使用這種通訊。 反之，只有階層的頂層站台伺服器會加以使用。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 端點對應程式|135|135|  
|RPC (DCOM)|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a> 站台伺服器 - > 裝載遠端內容程式庫共用的伺服器  
從版本 1806 開始，您可以將內容庫重新定位到另一個儲存位置，以釋出管理中心或主要站台伺服器上的硬碟空間。 如需詳細資訊，請參閱[針對站台伺服器設定遠端內容庫](the-content-library.md#bkmk_remote)。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  


###  <a name="site-server-lt-----reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> 站台伺服器 &lt; -- > Reporting Services 點  
 <sup>[附註 5](#bkmk_note5)</sup>  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----site-server"></a><a name="BKMK_PortsSite-Site"></a> 站台伺服器 &lt; -- > 站台伺服器  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  


###  <a name="site-server-----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> 站台伺服器 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  

 如果站台會使用遠端 SQL Server 來裝載站台資料庫，則在安裝該站台時，請在站台伺服器和 SQL Server 之間開啟下列連接埠：  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  

###  <a name="site-server-----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a> 站台伺服器 -- > WSUS 的 SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 3](#bkmk_note3) 可用的替代連接埠</sup>|  

###  <a name="site-server-----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> 站台伺服器 -- > SMS 提供者  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC <sup>[附註 6](#bkmk_note6)</sup>|  


###  <a name="site-server-lt-----software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> 站台伺服器 &lt; -- > 軟體更新點  
 <sup>[附註 5](#bkmk_note5)</sup>  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|HTTP|--|80 或 8530 <sup>[附註 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 或 8531 <sup>[附註 3](#bkmk_note3)</sup>|  


###  <a name="site-server-lt-----state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> 站台伺服器 &lt; -- > 狀態移轉點  
 <sup>[附註 5](#bkmk_note5)</sup>  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  


###  <a name="sms-provider-----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> SMS 提供者 -- &gt; SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="software-update-point-----internet"></a><a name="BKMK_PortsSUP-Internet"></a> 軟體更新點 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[附註 1](#bkmk_note1)</sup>|  


###  <a name="software-update-point-----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> 軟體更新點 -- > 上游 WSUS 伺服器  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 或 8530 <sup>[附註 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 或 8531 <sup>[附註 3](#bkmk_note3)</sup>|  


###  <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 進行站台間的資料庫複寫時，其中一個站台上的 SQL Server 必須直接與其父站台或子站台的 SQL Server 通訊。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server 服務|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  
|SQL Server Service Broker|--|4022 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  

> [!TIP]  
>  設定管理員不需要使用連接埠 UDP 1434 的 SQL Server Browser。  


###  <a name="state-migration-point-----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> 狀態移轉點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 <sup>[附註 2](#bkmk_note2)：可用的替代連接埠</sup>|  


###  <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Configuration Manager 用戶端和站台系統使用的連接埠附註  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a> 附註 1：Proxy 伺服器連接埠
無法設定此連接埠，但可以經設定的 Proxy 伺服器路由。  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a> 附註 2：可用的替代連接埠
您可以在設定管理員中定義此值的替代連接埠。 如果定義自訂連接埠，請在定義 IPsec 原則或設定防火牆的 IP 篩選器資訊時替代該自訂連接埠。  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a> 附註 3：Windows Server Update Services (WSUS)
針對用戶端通訊，可以安裝 WSUS 以使用連接埠 80/443 或連接埠 8530/8531。 當您在 Windows Server 2012 或 Windows Server 2016 中執行 WSUS 時，預設會將 WSUS 設定為針對 HTTP 使用連接埠 8530，並針對 HTTPS 使用連接埠 8531。  

安裝後，即可變更連接埠。 您不需要在整個站台階層都使用相同的連接埠號碼。  

- 如果 HTTP 連接埠是80，HTTPS 連接埠必須是 443。  

- 如果 HTTP 連接埠使用其他任何號碼，則 HTTPS 連接埠必須比該連接埠號碼多 1 (或以上)，例如 8530 和 8531。   

    > [!NOTE]  
    >  當您設定軟體更新點使用 HTTPS 時，也必須開啟 HTTP 連接埠。 未加密的資料，例如特定更新的 EULA，會使用 HTTP 連接埠。 

- 當您針對 WSUS 清理啟用下列選項時，站台伺服器會連線到裝載 SUSDB 的 SQL 伺服器：
  - 將非叢集索引新增至 WSUS 資料庫以改進 WSUS 清理效能
  - 從 WSUS 資料庫移除已淘汰的更新
  
  若預設 SQL Server 連接埠已變更為具有 SQL Server 組態管理員的替代連接埠，請確定站台伺服器可以使用已定義的連接進行連線。 Configuration Manager 不支援動態連接埠。 根據預設，SQL Server 具名執行個體會使用動態連接埠連線到資料庫引擎。 當您使用具名執行個體時，請手動設定靜態連接埠。

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a> 附註 4：Trivial FTP (TFTP) 精靈
Trivial FTP (TFTP) 精靈系統服務不需要使用者名稱或密碼，而且是 Windows 部署服務 (WDS) 的一部分。 Trivial FTP 精靈服務支援下列 RFC 定義的 TFTP 通訊協定：  

- RFC 1350：TFTP  

- RFC 2347：選項延伸模組  

- RFC 2348：區塊大小選項  

- RFC 2349：逾時間隔，以及傳輸大小選項  

TFTP 的設計可支援無磁碟開機環境。 TFTP 精靈會接聽 UDP 連接埠 69，但會從動態配置的高連接埠回應。 因此，啟用此連接埠可讓 TFTP 服務接收傳入的 TFTP 要求，但不會讓所選伺服器回應這些要求。 除非您將 TFTP 伺服器設為從連接埠 69 回應，否則無法讓所選伺服器回應輸入的 TFTP 要求。  

Windows PE 中已啟用 PXE 發佈點及用戶端會為 TFTP 傳輸選取動態配置高連接埠。 Microsoft 會定義 49152 到 65535 之間的連接埠。 如需詳細資訊，請參閱 [Windows 的服務概觀及網路連接埠需求](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows) (機器翻譯)

不過，在實際的 PXE 開機期間，裝置上的網路卡會選取其在 TFTP 傳輸期間所使用的動態配置高連接埠。 裝置上的網路卡並非繫結至由 Microsoft 定義的動態配置高連接埠。 它只繫結至在 RFC 1350 中定義的連接埠。 此連接埠可以是從 0 到 65535 的任一項。 如需關於網路卡所使用動態配置高連接埠的詳細資訊，請連絡裝置硬體製造商。


#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a> 附註 5：站台伺服器與站台系統之間的通訊
根據預設，網站伺服器和網站系統之間的通訊是雙向的。 網站伺服器會起始通訊以設定網站系統，然後多數網站系統會連回網站伺服器以傳送狀態資訊。 Reporting Services 點及發佈點不會傳送狀態資訊。 安裝好站台系統後，如果您在站台系統內容中選取 [要求站台伺服器起始與此站台系統的連線]  ，站台系統將不會起始與站台伺服器的通訊。 反之，站台伺服器會起始通訊，並使用站台系統安裝帳戶來驗證站台系統伺服器。  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a> 附註 6：動態連接埠
動態連接埠會使用由作業系統版本定義的連接埠號碼範圍。 這些連接埠也稱為暫時連接埠。 如需有關預設連接埠範圍的詳細資訊，請參閱 [Windows Server 系統的服務概觀和網路連接埠需求](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)。  



##  <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> 其他連接埠清單  

 下列各節提供有關 Configuration Manager 使用之連接埠的其他資訊。  

###  <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> 用戶端對伺服器共用  

 用戶端一律使用伺服器訊息區塊 (SMB) 連線至 UNC 共用。 例如：  

- 指定 CCMSetup.exe **/source:** 命令列內容的手動用戶端安裝  

- 從 UNC 路徑下載定義檔案的 Endpoint Protection 用戶端

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  


###  <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Microsoft SQL Server 的連線  

 如為 SQL Server 資料庫引擎和網站間複寫通訊，可以使用預設 SQL Server 連接埠或指定自訂連接埠：  

- 網站間通訊使用：  

  - SQL Server Service Broker，預設為連接埠 TCP 4022。  

  - SQL Server 服務，預設為連接埠 TCP 1433。  

- SQL Server 資料庫引擎與不同 Configuration Manager 站台系統角色之間的站台內通訊預設為連接埠 TCP 1433。  

- Configuration Manager 使用相同的連接埠及通訊協定，與裝載站台資料庫的各個 SQL 可用性群組複本通訊，如同複本是獨立的 SQL Server 執行個體。

當您使用 Azure，而站台資料庫位於內部或外部負載平衡器後方時，請設定下列元件：
- 每個複本上的防火牆例外
- 負載平衡規則 

設定下列連接埠：
- 透過 TCP 的 SQL：TCP 1433
- SQL Server Service Broker：TCP 4022
- 伺服器訊息區 (SMB)：TCP 445
- RPC 端點對應程式：TCP 135

> [!WARNING]  
> Configuration Manager 不支援動態連接埠。 根據預設，SQL Server 具名執行個體會使用動態連接埠連線到資料庫引擎。 當您使用具名執行個體時，請手動設定要用於站台間通訊的靜態連接埠。  

下列網站系統角色會直接與 SQL Server 資料庫通訊：  

- 應用程式類別目錄 Web 服務點  

- 憑證登錄點角色  

- 註冊點角色  

- 管理點  

- 網站伺服器  

- Reporting Services 點  

- SMS 提供者  

- SQL Server --> SQL Server  

當 SQL Server 裝載來自多個站台的資料庫時，每個資料庫都必須使用不同的 SQL Server 執行個體。 請將每個執行個體設定為一組唯一的連接埠。  

如果您在 SQL Server 上啟用主機型防火牆，請將它設定為允許正確的連接埠。 此外，請在與 SQL Server 通訊的電腦之間設定網路防火牆。  

如需如何設定 SQL Server 以使用特定連接埠的詳細資訊，請參閱[將伺服器設定為在特定 TCP 連接埠上接聽](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。  


### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> 探索和發行

設定管理員使用下列連接埠來探索和發佈站台資訊：
- 輕量型目錄存取通訊協定 (LDAP)：389
- 通用類別目錄 LDAP：3268
- RPC 端點對應程式：135
- RPC：動態配置的高 TCP 通訊埠
- TCP：1024：5000
- TCP：49152：65535


###  <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Configuration Manager 進行的外部連線  

內部部署設定管理員用戶端或站台系統可以進行下列外部連線：  

- [Asset Intelligence 同步處理點 -- &gt; Microsoft](#BKMK_PortsAI)  

- [Endpoint Protection 點 -- &gt; 網際網路](#BKMK_PortsEndpointProtection_Internet)  

- [用戶端 -- &gt; 通用類別目錄網域控制站](#BKMK_PortsClient-GCDC)  

- [Configuration Manager 主控台 -- &gt; 網際網路](#BKMK_PortsConsole-Internet)  

- [管理點 -- &gt; 網域控制站](#BKMK_PortsMP-DC)  

- [站台伺服器 -- &gt; 網域控制站](#BKMK_PortsSite-DC)  

- [站台伺服器 &lt; -- &gt; 發行憑證授權單位 (CA)](#BKMK_PortsIssuingCA_SiteServer)  

- [軟體更新點 -- &gt; 網際網路](#BKMK_PortsSUP-Internet)  

- [軟體更新點 -- &gt; 上游 WSUS 伺服器](#BKMK_PortsSUP-WSUS)  

- [服務連接點 -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

- [服務連接點 -- > Azure](#bkmk_scp-cmg)  

- [CMG 連接點 -- > CMG 雲端服務](#bkmk_cmgcp-cmg)  


###  <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> 支援以網際網路為基礎用戶端的站台系統安裝需求  

> [!Note]  
> 本節僅適用於以網際網路為基礎的用戶端管理 (IBCM)。 不適用於雲端管理閘道。 如需詳細資訊，請參閱[管理網際網路上的用戶端](../../clients/manage/manage-clients-internet.md)。  

以網際網路為基礎的管理點和發佈點 (支援以網際網路為基礎的用戶端)、軟體更新點，以及後援狀態點均使用下列連接埠進行安裝及修復：  

- 站台伺服器 --> 站台系統：使用 UDP 和 TCP 連接埠 135 的 RPC 端點對應程式。  

- 站台伺服器 --> 站台系統：RPC 動態 TCP 連接埠  

- 站台伺服器 &lt; --> 站台系統：使用 TCP 通訊埠 445 的伺服器訊息區 (SMB)

發佈點上的應用程式和套件安裝需要下列 RPC 連接埠：  

- 站台伺服器 --> 發佈點：使用 UDP 和 TCP 通訊埠 135 的 RPC 端點對應程式

- 站台伺服器 --> 發佈點：RPC 動態 TCP 連接埠  

使用 IPsec 協助保護網站伺服器和網站系統之間的流量。 如果必須限制與 RPC 搭配使用的動態連接埠，可以使用 Mircrosoft RPC 設定工具 (rpccfg.exe) 為這些 RPC 封包設定有限的連接埠範圍。 如需 RPC 設定工具的詳細資訊，請參閱 [如何設定 RPC 使用特定連接埠，以及如何使用 IPsec 以協助保護這些連接埠](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those)。  

> [!IMPORTANT]  
>  安裝這些站台系統之前，請確認站台系統伺服器上正在執行遠端登錄服務；如果站台系統在另一個沒有信任關係的 Active Directory 樹系中，則需確認您已指定站台系統安裝帳戶。 例如，執行站台系統 (例如發佈點 (提取與標準))、遠端 SQL 伺服器與應用程式類別目錄的伺服器上會使用遠端登錄服務。


###  <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Configuration Manager 用戶端安裝使用的連接埠  

Configuration Manager 在用戶端安裝期間使用的連接埠會因部署方法而有所不同。 

- 如需各用戶端部署方法的連接埠清單，請參閱[用戶端部署期間使用的連接埠](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment)  

- 如需如何在用戶端上設定 Windows 防火牆以進行用戶端安裝及安裝後通訊的詳細資訊，請參閱[用戶端適用的 Windows 防火牆和連接埠設定](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md)  


###  <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> 移轉使用的連接埠  

執行移轉的站台伺服器會使用使用數個連接埠連線到來源階層中的適用站台。 如需詳細資訊，請參閱[移轉的必要設定](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations)。  


###  <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Windows Server 使用的連接埠  

下表列出 Windows Server 所使用的一些主要連接埠。 

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 和 68|--|  
|NetBIOS 名稱解析|137|--|  
|NetBIOS Datagram Service|138|--|  
|NetBIOS Session Service|--|139|  
|Kerbero 驗證|--|88|

如需詳細資訊，請參閱下列文章：
- [Service overview and network port requirements for the Windows Server system](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows) (Windows Server System 的服務概觀和網路連接埠需求)。  

- [How to configure a firewall for domains and trusts](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts) (如何設定防火牆以供網域和信任使用)
