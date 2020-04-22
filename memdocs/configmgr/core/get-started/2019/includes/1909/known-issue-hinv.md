---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697926"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a> 硬體清查報表

<!--5468413-->
若您嘗試執行仰賴於硬體清查的報表，它會傳回錯誤。 例如，BitLocker 報表會傳回類似下列訊息的錯誤：

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

您可能會在 **dataldr.log** 檔案中看到下列錯誤：

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

仰賴硬體清查的主控台儀表板可能也會受影響。

發生此問題的原因是特定硬體清查資料表上的資料庫結構描述發生變更。

#### <a name="workaround"></a>因應措施

因應措施是從資料庫卸除既有的屬性。 資料載入器站台元件接著可已建立新屬性。 菜站台資料庫伺服器上執行下列 SQL 指令碼以修正資料表結構描述：

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
