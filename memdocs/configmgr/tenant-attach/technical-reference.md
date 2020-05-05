---
title: 裝置動作的疑難排解
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 的裝置動作技術參考進行疑難排解
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "82140273"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>針對 Configuration Manager 裝置的裝置動作進行疑難排解

適用於：  Configuration Manager (最新分支)

從 Configuration Manager 2002 開始，Configuration Manager 用戶端可以同步處理至 Microsoft Endpoint Manager 系統管理中心。 某些用戶端動作可以從已同步處理的用戶端上的 Microsoft Endpoint Manager 系統管理中心執行。

可用動作為：
- 同步處理電腦原則
- 同步使用者原則
- 應用程式評估週期


[![Microsoft Endpoint Manager 系統管理中心的裝置總覽](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
當系統管理員從 Microsoft Endpoint Manager 系統管理中心執行動作時，會將通知要求轉送到 Configuration Manager 網站，以及從網站轉送給用戶端。

## <a name="configuration-manager-components"></a>Configuration Manager 元件

- **SMS_SERVICE_CONNECTOR**：使用閘道通知背景工作角色來處理 Microsoft Endpoint Manager 系統管理中心的通知。
- **SMS_NOTIFICATION_SERVER**：取得通知並建立用戶端通知。
- **BgbAgent**：用戶端會取得工作並執行要求的動作。

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

從 Microsoft Endpoint Manager 系統管理中心起始動作時， **CMGatewayNotificationWorker**會處理要求。  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. 從 Microsoft Endpoint Manager 系統管理中心收到通知。

   ```text
   Received new notification. Validating basic notification details..
   ```

1. 系統會驗證使用者和裝置動作。

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. 遠端工作會轉送到 SMS_NOTIFICATION_SERVER。

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

一旦訊息傳送至 SMS_NOTIFICATION_SERVER，工作就會從管理點傳送到對應的用戶端。 您會在**bgbserver.log**的管理點上看到下列內容：

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

最後一個步驟會發生在用戶端上，而且可以在**CcmNotificationAgent**中看到。 一旦收到工作，它就會要求排程器執行此動作。 執行此動作時，您會看到確認訊息：

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>常見問題

如果系統管理員在 Configuration Manager 中沒有必要的許可權，您會在`Unauthorized` **CMGatewayNotificationWorker**中看到回應。

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

請確定從 Microsoft Endpoint Manager 系統管理中心執行此動作的使用者，具有 Configuration Manager 網站的必要許可權。 如需詳細資訊，請參閱[Microsoft Endpoint Manager 租使用者附加必要條件](device-sync-actions.md#prerequisites)。

## <a name="next-steps"></a>後續步驟

[啟用共同管理](../comanage/overview.md)以取得額外的雲端功能，例如條件式存取。
