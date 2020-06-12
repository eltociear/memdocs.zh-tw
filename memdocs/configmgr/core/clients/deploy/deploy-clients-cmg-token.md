---
title: CMG 的權杖型驗證
titleSuffix: Configuration Manager
description: 在內部網路上註冊用戶端以取得唯一權杖，或為網際網路型裝置建立大量註冊權杖。
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5054d44371fd3114a9644f90d37dabf1e81d1997
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455016"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>雲端管理閘道的權杖型驗證

適用於：Configuration Manager (最新分支)

<!--5686290-->

雲端管理閘道 (CMG) 支援許多類型的用戶端，但即便使用[增強 HTTP](../../plan-design/hierarchy/enhanced-http.md)，這些用戶端還是需要[用戶端驗證憑證](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway)。 對於以網際網路為基礎的用戶端而言，若不常連線至內部網路、則無法加入 Azure Active Directory (Azure AD)，且沒有方法可安裝 PKI 發行憑證，則可能難以佈建此憑證需求。

為了克服這些困難，從 2002 版開始，Configuration Manager 使用下列方法擴充其裝置支援：

- 在內部網路註冊以取得唯一權杖

- 為以網際網路為基礎的裝置建立大量註冊權杖

若要充分利用此功能，請在更新站台之後，也將用戶端更新為最新版本。 除非用戶端版本也是最新版本，否則此完整案例無法運作。 如有必要，請確定[將新的用戶端版本升級為生產環境](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)。

Configuration Manager 用戶端會與管理點一起管理此權杖，因此不會有 OS 版本相依性。 這項功能適用於任何[支援的用戶端 OS 版本](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。

> [!NOTE]
> 這些方法僅支援以裝置為主的管理案例。
>
> Microsoft 建議將裝置加入至 Azure AD。 以網際網路為基礎的裝置可以使用 Azure AD 向 Configuration Manager 進行驗證。 無論該裝置是在網際網路上，或與內部網路連線，Azure AD 都會同時啟用裝置與使用者案例。 如需詳細資訊，請參閱[使用 Azure AD 身分識別安裝和註冊用戶端](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。

## <a name="register-on-the-internal-network"></a>在內部網路上註冊

此方法需要用戶端先於內部網路的管理點進行註冊。 您通常可以在安裝後立即進行用戶端註冊。 管理點會為用戶端提供唯一權杖，其會顯示正在使用自我簽署憑證。 當用戶端於網際網路漫遊時，若要與 CMG 通訊，則會將其自我簽署憑證與管理點發行的權杖配對。 用戶端每個月會更新一次權杖，且有效期為 90 天。

根據預設，網站會啟用此行為。

## <a name="create-a-bulk-registration-token"></a>建立大量註冊權杖

如果無法在內部網路安裝並註冊用戶端，請建立大量註冊權杖。 當用戶端安裝在以網際網路為基礎的裝置上，並透過 CMG 註冊時，請使用此權杖。 大量註冊權杖的有效期很短，且不會儲存在用戶端或網站上。 其可讓用戶端產生與自我簽署憑證配對的唯一權杖，讓該權杖能夠使用 CMG 進行驗證。

1. 以本機系統管理員權限登入階層中的頂層站台伺服器。

1. 以系統管理員身分開啟命令提示字元。

1. 在站台伺服器上 Configuration Manager 安裝目錄的 `\bin\X64` 資料夾中執行此工具：`BulkRegistrationTokenTool.exe`。 使用 `/new` 參數建立新的權杖。 例如 `BulkRegistrationTokenTool.exe /new`。 如需詳細資訊，請參閱[大量註冊權杖工具使用方式](#bulk-registration-token-tool-usage)。

1. 複製權杖，並將其儲存在安全的位置。

1. 在以網際網路為基礎的裝置上安裝 Configuration Manager 用戶端。 包含用戶端安裝參數：[ **/regtoken**](about-client-installation-properties.md#regtoken)。 下列範例命令列包含其他必要的安裝程式參數和屬性：

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > 如需此命令列的詳細資訊，請參閱[使用 Azure AD 身分識別](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)安裝和註冊用戶端。 此流程與上述流程很類似，只是不會使用 Azure AD 的屬性。

若要驗證，請檢查下列記錄檔中是否有類似的項目：<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

### <a name="known-issues"></a>已知問題

無法在所含站台伺服器處於被動模式的站台上建立大量註冊權杖。<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>大量註冊權杖工具使用方式

`BulkRegistrationTokenTool.exe` 工具位於站台伺服器上 Configuration Manager 安裝目錄的 `\bin\X64` 資料夾中。 登入站台伺服器，然後以系統管理員身分執行。 其支援下列命令列參數：

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

顯示此使用方式資訊。

範例：`BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

建立新的大量註冊權杖。

範例：`BulkRegistrationTokenTool.exe /new`

此工具會顯示下列資訊：
  
- 網站用來追蹤已發行權杖的 GUID
- 權杖有效期間，預設為三天。
- 大量註冊權杖。

權杖不會儲存在用戶端或站台上。 請務必從命令提示字元複製權杖，並將其儲存在安全的位置。

#### <a name="lifetime"></a>/lifetime

搭配使用 `/new` 參數來指定權杖的權杖有效期間。 指定整數值 (以分鐘為單位)。 預設值為 4,320 (3 天)。 最大值為 10,080 (7 天)。

範例：`BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>大量註冊權杖管理

如有需要，您可以在 Configuration Manager 主控台中查看先前建立的大量註冊權杖與其存留期，並封鎖其使用方式。 不過，站台資料庫不會儲存大量註冊權杖。

### <a name="review-a-bulk-registration-token"></a>檢閱大量註冊權杖

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區。

2. 展開 [安全性]，然後選取 [憑證] 節點。 主控台會在詳細資料窗格中列出所有與站台相關的憑證與大量註冊權杖。

3. 選取要檢閱的大量註冊權杖。

您也可以篩選或排序 [類型] 資料行。 根據其 GUID 識別特定的大量註冊權杖。 當您建立大量註冊權杖時，此工具會顯示 GUID。

### <a name="block-a-bulk-registration-token"></a>封鎖大量註冊權杖

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區。

2. 展開 [安全性]，選取 [憑證] 節點，然後選取要封鎖的大量註冊權杖。

3. 在功能區列的 [常用] 索引標籤上或滑鼠右鍵內容功能表中，選取 [封鎖]。 若要解除封鎖之前已封鎖的大量註冊權杖，請選取 [解除封鎖] 動作。

## <a name="see-also"></a>請參閱

- [規劃雲端管理閘道](../manage/cmg/plan-cloud-management-gateway.md)

- [安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證](deploy-clients-cmg-azure.md)
