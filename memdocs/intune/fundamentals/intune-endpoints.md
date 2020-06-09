---
title: Microsoft intune 的網路端點
titleSuffix: ''
description: 檢閱 Intune 的端點。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49ec674f8aa0ec0fd00aaf4be25f307158d79781
ms.sourcegitcommit: b0ae4a9972bac3518d0d4f33e033ac492eefe3c1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84126493"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Microsoft intune 的網路端點  

此頁面會列出 Intune 部署中 Proxy 設定所需要的 IP 位址和連接埠設定。

Intune 屬於僅限雲端的服務，因此不需要內部部署基礎結構，例如伺服器或閘道。

## <a name="access-for-managed-devices"></a>受控裝置的存取權  

若要管理位於防火牆和 Proxy 伺服器後方的裝置，您必須啟用 Intune 的通訊功能。

> [!NOTE]
> 區段中的資訊也會套用於 Microsoft Intune 憑證連接器。 此連接器具有與受控裝置相同的網路需求

- Proxy 伺服器必須同時支援 **HTTP (80)** 和 **HTTPS (443)** ，因為 Intune 用戶端使用這兩種通訊協定。 Windows 資訊保護使用連接埠 444。
- 針對某些工作 (例如下載傳統電腦代理程式的軟體更新)，Intune 會需要未驗證的 Proxy 伺服器存取 manage.microsoft.com

您可以修改個別用戶端電腦上的 Proxy 伺服器設定。 也可以使用群組原則設定，針對位於指定 Proxy 伺服器後方的所有用戶端電腦變更設定。


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

受管理裝置需要進行可讓 [所有使用者] 穿過防火牆存取服務的設定。


下表列出 Intune 用戶端存取的連接埠和服務：

|網域    |IP 位址      |
|-----------|----------------|
|login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net| 更多資訊請參閱 [Office 365 URL 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua05.manage.microsoft.com|138.91.244.151|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msub01.manage.microsoft.com|137.135.128.214|
|fef.msub02.manage.microsoft.com|137.135.130.29|
|fef.msub03.manage.microsoft.com|52.169.82.238|
|fef.msub05.manage.microsoft.com|23.97.166.52|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|enterpriseregistration.windows.net|52.175.211.189|
|fef.amsua0102.manage.microsoft.com|52.242.211.0|
|fef.amsua0702.manage.microsoft.com|52.232.225.75|
|fef.amsub0502.manage.microsoft.com|40.67.219.144|
|fef.msud01.manage.microsoft.com|20.40.178.139|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>PowerShell 指令碼和 Win32 應用程式的網路需求  

如果您使用 Intune 部署 PowerShell 指令碼或 Win32 應用程式，您也需要將存取權授與您租用戶目前所在的端點。

|ASU | 儲存體名稱 | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows 推播通知服務 (WNS)  

針對使用行動裝置管理 (MDM) 的受 Intune 管理 Windows 裝置，裝置動作和其他立即的活動都需要使用 Windows 推播通知服務 (WNS)。 如需詳細資訊，請參閱[透過企業防火牆允許 Windows 通知流量](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config)。  

## <a name="delivery-optimization-port-requirements"></a>傳遞最佳化的連接埠需求  

### <a name="port-requirements"></a>連接埠需求  

針對對等流量，傳遞最佳化會對 TCP/IP 使用 7680，或對 NAT 周遊 (或 Teredo) 使用 3544。 針對用戶端服務通訊，它會在連接埠 80/443 上使用 HTTP 或 HTTPS。

### <a name="proxy-requirements"></a>Proxy 需求  

若要使用傳遞最佳化，您必須允許位元組範圍要求。 如需詳細資訊，請參閱 [Windows Update 的 Proxy 需求](https://docs.microsoft.com/windows/deployment/update/windows-update-troubleshooting)。

### <a name="firewall-requirements"></a>防火牆需求  

允許下列主機名稱通過您的防火牆，以支援傳遞最佳化。
用戶端與傳遞最佳化雲端服務間的通訊：
- \*.do.dsp.mp.microsoft.com

傳遞最佳化中繼資料：
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Apple 裝置網路資訊  

|用途|主機名稱 (IP 位址/子網路)|通訊協定|Port|
|-----|--------|------|-------|
|擷取並顯示來自 Apple 伺服器的內容|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|與 APNS 伺服器通訊|#-courier.push.apple.com<br>'#' 是從 0 至 50 的隨機數字。|    TCP     |  5223 和 443  |
|各種功能，包括存取全球資訊網、iTunes store、macOS app store、iCloud、Messaging 等。 |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 或 443   |

如需詳細資訊，請參閱 Apple 提供的 [Apple 軟體產品使用的 TCP 和 UDP 連接埠](https://support.apple.com/HT202944)、[關於 macOS、iOS/iPadOS 和 iTunes 伺服器主機連線與 iTunes 背景處理序](https://support.apple.com/HT201999)，以及[如果 macOS 和 iOS/iPadOS 用戶端未取得 Apple 推播通知](https://support.apple.com/HT203609)。  