---
title: 應用程式部署至使用者技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 中應用程式部署使用者進行疑難排解的技術參考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690266"
---
# <a name="application-deployment-policy-for-users"></a>適用於使用者的應用程式部署原則

適用於：  Configuration Manager (最新分支)

將應用程式部署至使用者集合時，只會針對「必要」部署建立部署的原則。 針對「可用」部署，當使用者嘗試從軟體中心安裝應用程式時，就會建立原則。 本文將說明「必要」部署以及「可用」部署的程序。

> [!TIP]
> 可以藉由執行[開始之前](app-deployment-technical-reference.md#before-you-begin)區段中參考的 SQL 查詢，取得檢閱用戶端記錄所需的所有資訊。

## <a name="required-deployments"></a>必要部署

在建立部署時，必要應用程式部署至使用者集合的原則是以集合中的所有使用者為目標。 這些部署的用戶端處理類似於裝置集合的必要部署。 部署啟用會在定義的「可用時間」發生，並在定義的「期限」時間進行強制執行。 如需詳細資訊，請參閱[裝置集合的應用程式部署](device-deployment-technical-reference.md)。

## <a name="available-deployments"></a>可用的部署

以「可用」形式部署到使用者集合的應用程式會以不同的方式運作。 這種行為變更可讓系統管理員將應用程式提供給使用者，而不會造成原則的資源爭用。 當使用者啟動軟體中心時，系統會即時從管理點查詢使用者可用的應用程式清單。 此要求是對管理點上的 `CMUserService_WindowsAuth` 虛擬目錄提出，而且可以在用戶端上的 **SCClient_[UserName].log** 中看到。

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

當管理點收到此要求時，會藉由執行 `usp_GetApplicationPropertyValuesFiltered` 預存程序來查詢可供使用者使用的應用程式清單。 您可以在管理點上的 **UserService.log** 中追蹤此活動。

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

軟體中心會接收清單，並顯示使用者可以安裝的應用程式。 當使用者按一下應用程式時，系統會從管理點查詢應用程式的相關額外資訊，其中牽涉到預存程序的執行，例如 usp_GetApplicationInfo、usp_GetAppModelApplicationSupersedence、usp_GetDeploymentTypeForAnApp 等等。

部署會在使用者選取應用程式並按一下 [安裝]  按鈕時啟用，並且會建立 DCM 代理程式作業來評估應用程式。 如果應用程式適用，則會建立另一個 DCM 代理程式作業來下載並強制執行應用程式。 您可以在用戶端上的 **DCMAgent.log** 中追蹤此活動。

## <a name="next-steps"></a>後續步驟

- [了解應用程式部署用戶端元件](client-components-technical-reference.md)
