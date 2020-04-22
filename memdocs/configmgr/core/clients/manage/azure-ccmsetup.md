---
title: Azure AD 驗證工作流程
titleSuffix: Configuration Manager
description: 在 Windows 10 裝置上使用 Azure Active Directory 驗證進行設定管理員用戶端安裝程序的詳細資料
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694996"
---
# <a name="azure-ad-authentication-workflow"></a>Azure AD 驗證工作流程

適用於：  Configuration Manager (最新分支)

本文為一份技術參考，適用於在已加入至 Azure Active Directory (Azure AD) 的 Windows 10 裝置上進行設定管理員用戶端安裝程序。 其中將詳細說明適用於裝置驗證和用戶端安裝的工作流程程序。  
 

## <a name="azure-ad-token-request-workflow"></a>Azure AD 權杖要求工作流程

![Azure AD CCMSetup 工作流程圖](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1.Azure AD 權杖要求

已加入 Azure AD 網域的 Windows 10 用戶端會使用 Azure AD 參數來要求權杖。 下列項目均記錄於 **ccmsetup.log**：

- 要求 Azure AD 裝置權杖：

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- 如果無法取得裝置權杖，它就會要求 Azure AD 使用者權杖：

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> 當它加入 Azure AD 時，用戶端應該會取得加入工作場所網路 (WPJ) 憑證。 如果找不到加入工作場所網路憑證，用戶端就不會嘗試使用安全性權杖服務通訊通道 (CCM_STS) 來建立要求。 此行為是因為用戶端無法將 Azure AD 權杖加入至要求。 若未正確地將用戶端加入至 Azure AD，裝置通常不會擁有此憑證用戶端。
>
> 此外，如果權杖無效，雲端管理閘道 (CMG) 就不會將要求轉送到內部網站角色。 如果未在 Configuration Manager 中將租用戶註冊為雲端管理服務，則權杖可能無效。


### <a name="2-configuration-manager-client-token-request"></a>2.Configuration Manager 用戶端權杖要求

一旦用戶端擁有 Azure AD 權杖之後，就會要求 Configuration Manager 用戶端 (CCM) 權杖。

下列項目均記錄於 CMG 虛擬機器的 **ccmsetup.log**：

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 CMG 取得要求

下列項目均記錄於 **IIS.log**：

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 CMG 會將要求轉送到 CMG 連接點

下列項目均記錄於 **CMGService.log**：

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 CMG 連接點會將 CMG 用戶端要求轉送到管理點用戶端要求

下列項目均記錄於 **SMS_CLOUD_PROXYCONNECTOR.log**：

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 管理點會在站台資料庫中確認使用者權杖

下列項目均記錄於 **CCM_STS.log**：

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>內容位置要求

一旦用戶端使用 CCM 權杖取得回應之後，即會快取並使用它，以透過 CMG 來要求站台資訊和內容位置。 下列項目均記錄於 **ccmsetup.log**：

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>用戶端安裝

裝置會下載用戶端內容並開始安裝。

### <a name="communication-validation"></a>通訊驗證

- CMG 會透過 CMG、CMG 連接點和 HTTP(S)，以及管理點資料庫要求，來驗證用戶端權杖。
- 用戶端會確認 CMG 服務憑證或管理憑證
- 適用於 CMG 服務憑證的 PKI：用戶端會在本機存放區上要求 CMG 憑證的根憑證授權單位 (CA)
- 第三方 CMG 服務憑證：用戶端會使用其在網際網路上發佈的根 CA 自動驗證憑證


## <a name="common-issues"></a>常見問題

- 根 CA 不存在
- 已啟用 CRL 檢查：在網際網路上發佈 CRL，或在命令列中使用 **/NoCRLcheck** 選項
- 找不到 WPJ 憑證：用戶端已向 Azure AD 註冊，但未加入至 Azure AD

使用 /NoCRLCheck 僅適用於 ccmsetup 啟動程序。 對於完全正常運作的用戶端，您應該在網際網路上發佈 CRL。 因應措施為，您可以在站台的用戶端通訊設定上停用 CRL 檢查。 否則，當位置服務重新整理安全性設定之後，用戶端就會停止與伺服器通訊。


## <a name="client-registration"></a>用戶端註冊

![Azure AD 註冊工作流程圖](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1.Configuration Manager 用戶端要求註冊

下列項目均記錄於 **ClientIDManagerStartup.log** 中：

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2.Configuration Manager 要求需提供 Azure AD 驗證權杖才能註冊用戶端

下列項目均記錄於 **ADALOperationProvider.log** 中：

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 已註冊設定管理員用戶端  

下列項目均記錄於 **ClientIDManagerStartup.log** 中：

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> 在用戶端註冊期間，一律會執行憑證驗證。 即使您使用 Azure AD 驗證方法註冊用戶端，也一樣會執行此程序。


### <a name="3-configuration-manager-client-token-request"></a>3.Configuration Manager 用戶端權杖要求

一旦網站註冊用戶端，用戶端就會要求 CCM 權杖。 CCM 權杖會針對本機系統帳戶 (S-1-5-18) 加密，並快取保留 8 小時。 八小時後權杖就會過期，並在用戶端要求權杖時更新。

下列項目均記錄於 **ClientIDManagerStartup.log** 中：

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1 CMG 取得要求

下列項目均記錄於 **IIS.log**：

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 CMG 會將要求轉送到 CMG 連接點

下列項目均記錄於 **CMGService.log**：

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3 CMG 連接點會將 CMG 用戶端要求轉送到管理點用戶端要求

下列項目均記錄於 **SMS_CLOUD_PROXYCONNECTOR.log**：

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 管理點會在站台資料庫中確認使用者權杖

下列項目均記錄於 **CCM_STS.log**：

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
