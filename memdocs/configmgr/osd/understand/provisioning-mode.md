---
title: 佈建模式
titleSuffix: Configuration Manager
description: 深入了解用戶端在 Configuration Manager 工作順序期間的佈建模式。
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 815b32ecf7e9cd315c2365cb5ed73004b2a48718
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708646"
---
# <a name="provisioning-mode"></a>佈建模式

適用於：  Configuration Manager (最新分支)

在 OS 部署工作順序期間，Configuration Manager 會將用戶端置於佈建模式中。 (作業系統部署工作順序包含就地升級至 Windows 10。)在此狀態下，用戶端不會處理來自站台的原則。 此行為可讓工作順序執行，而不需擔負在用戶端上執行其他部署的風險。 當工作順序完成時，不論成功還是處理失敗，它都會結束用戶端佈建模式。

如果工作順序意外失敗，則用戶端會保持於佈建模式中。 例如，如果在工作順序處理中間重新啟動裝置，它便無法復原。 系統管理員必須手動找出並修正處於此狀態的用戶端。


## <a name="manually-remove-provisioning-mode"></a>手動移除佈建模式

如果用戶端留在佈建模式中，請使用此手動程序讓用戶端返回正常作業。

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> 此 WMI 方法所進行變更的其中之一是設定登錄值，但它也會進行其他變更。 只變更登錄值不能讓用戶端完全退出佈建模式。 如果您手動編輯登錄，用戶端可能會出現非預期的行為。  


## <a name="client-provisioning-mode-timeout"></a>用戶端佈建模式逾時

從 1902 版開始，工作順序會在將用戶端置於佈建模式時，設定時間戳記。 每隔 60 分鐘，處於佈建模式之用戶端會檢查自時間戳記以來的持續時間。 如果它處於佈建模式的時間已超過 48 小時，用戶端會自動結束佈建模式，並重新啟動其程序。

佈建模式的逾時值預設為 48 小時。 您可以調整裝置上的這個計時器，方法是在下列登錄機碼中設定 **ProvisioningMaxMinutes** 值：`HKLM\Software\Microsoft\CCM\CcmExec`。 如果此值不存在或為 `0`，則用戶端會使用預設的 48 小時。

時間戳記 **ProvisioningEnabledTime** 位於下列登錄機碼中：`HKLM\Software\Microsoft\CCM\CcmExec`。 時間戳記的值提供電腦上次進入佈建模式的時間。 該值的格式為 Epoch (Unix 時間戳記) 及 UTC。

當您使用下列命令，手動讓電腦進入佈建模式，此時間戳記也會重設成目前的時間：

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>程序流程圖

這些圖表會顯示工作順序和用戶端的程序流程。

### <a name="task-sequence"></a>工作順序

下圖顯示工作順序設定佈建模式的方式：

![工作順序設定佈建模式的流程圖](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>用戶端補救

下圖顯示用戶端結束佈建模式的方式：

![用戶端結束佈建模式的流程圖](media/3197824-client-flow.png)


## <a name="see-also"></a>請參閱

[varname](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[升級作業系統](task-sequence-steps.md#BKMK_UpgradeOS)
