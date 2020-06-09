---
title: 中國部署的網路端點 - Microsoft Intune
titleSuffix: ''
description: 檢閱 Intune 的中國端點。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5551e537716ed12a0a5b5de19b747ffc7c4dcac
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347333"
---
# <a name="china-endpoints-for-microsoft-intune"></a>Microsoft Intune 的中國端點

此頁面會列出您 Intune 部署中 Proxy 設定所需要的中國端點。

若要管理位於防火牆和 Proxy 伺服器後方的裝置，您必須啟用 Intune 的通訊功能。

- Proxy 伺服器必須同時支援 **HTTP (80)** 和 **HTTPS (443)** ，因為 Intune 用戶端會使用這兩種通訊協定
- 針對某些工作 (例如下載軟體更新)，Intune 會需要未驗證的 Proxy 伺服器存取 manage.microsoft.com

您可以修改個別用戶端電腦上的 Proxy 伺服器設定。 也可以使用群組原則設定，針對位於指定 Proxy 伺服器後方的所有用戶端電腦變更設定。

受管理裝置需要進行可讓 [所有使用者] 穿過防火牆存取服務的設定。

如需適用於中國客戶的 Windows 10 自動註冊和裝置註冊的詳細資訊，請參閱[設定 Windows 裝置的註冊](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration)。

下表列出 Intune 用戶端存取的連接埠和服務：

|**端點**|**IP 位址**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>中國 Intune 客戶指定端點
- Azure 入口網站：https:\//portal.azure.cn/
- Office 365：https:\//portal.partner.microsoftonline.cn/
- Intune 公司入口網站：https:\//portal.manage.microsoftonline.cn/
- Microsoft 端點管理員系統管理中心：https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>合作夥伴服務端點

由 21Vianet 營運的 Intune 相依於下列合作夥伴服務端點：
- Azure AD 同步服務：https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo STS：https:\//login.chinacloudapi.cn/
- Azure AD Graph：https:\//graph.chinacloudapi.us
- MS Graph：https:\//microsoftgraph.chinacloudapi.cn
- ADRS：https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>後續步驟
[深入了解在中國由 21Vianet 營運的 Intune](china.md)

