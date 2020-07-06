---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590522"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a> Azure AD 驗證無法運作
<!--7569264-->
Configuration Manager 無法使用 Azure Active Directory (Azure AD) Security Token Service。 管理點上的 **CCM_STS.log** 包含類似下列錯誤項目：`ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` 其也包含 HRESULT 0x80131040。

另一個徵兆是雲端管理閘道 (CMG) 出現問題。 如果執行 CMG 連接分析器，其會發生下列錯誤而無法測試管理點的 CMG 通道：`Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

此問題是因為支援程式庫的版本不一致。

若要解決此問題，請從站台伺服器上安裝目錄的 \bin\X64 資料夾，將 **System.IdentityModel.Tokens.JWT.dll** 複製到管理點上的 SMS_CCM\CCM_STS\bin 資料夾。
