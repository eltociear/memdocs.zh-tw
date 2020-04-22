---
title: 針對 CMPivot 進行疑難排解
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中針對 CMPivot 進行疑難排解。
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 69178f9ac1c1acb1ee2a2931c88a55a0784435b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708016"
---
# <a name="troubleshoot-cmpivot"></a>針對 CMPivot 進行疑難排解

CMPivot 這個工具可讓您存取環境中裝置的即時狀態。 CMPivot 立即在目標集合中，所有目前已連線的裝置上執行查詢，然後傳回結果。

有時候，您可能需要針對 CMPivot 進行疑難排解。 例如，如果用戶端到 CMPivot 的狀況訊息損毀，站台伺服器無法處理該訊息。 本文協助您了解 CMPivot 的資訊流程。

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a> 在 1902 與更新版本中針對 CMPivot 進行疑難排解

在 Configuration Manager 1902 版與新版本中，您可以從管理中心網站 (CAS) 的階層中執行 CMPivot。 主要站台仍會處理與用戶端的通訊。

當您從 CAS 執行 CMPivot 時，它會使用高速訊息訂閱通道來與主要站台溝通。 CMPivot 不會在站台之間使用標準 SQL 複寫。 若您使用遠端 SQL Server 執行個體或 SQL 提供者，或使用 SQL Always On，則會有 CMPivot 的「雙躍點案例」。 如需如何為「雙躍點案例」定義限制委派的相關資訊， 請參閱 [從版本 1902 開始的 CMPivot](cmpivot.md#bkmk_cmpivot1902)。

>[!IMPORTANT]
> 針對 CMPivot 進行疑難排解時，請在您的管理點 (MP) 與站台伺服器的 SMS_MESSAGE_PROCESSING_ENGINE 上啟用詳細資訊記錄，以取得詳細資訊。 此外，若用戶端的輸出大於 80 KB，請在 MP 與站台伺服器的 SMS_STATE_SYSTEM 元件上啟用詳細資訊記錄。 如需有關如何啟用詳細資訊記錄的資訊，請參閱[站台伺服器記錄選項 ](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site)。

### <a name="get-information-from-the-site-server"></a>從站台伺服器取得資訊

根據預設，站台伺服器記錄檔位於 `C:\Program Files\Microsoft Configuration Manager\logs`。 若您指定非預設安裝目錄，或若您將 SMS 提供者等項目卸載至另一部伺服器，此位置可能會不同。 若您從 CAS 執行 CMPivot，記錄將位於主要站台伺服器。

查看 `smsprov.log` 以尋找這些行：

- Configuration Manager 1906 版：
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager 1902 版：
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14` 是適用於 CMPivot 的 Script-Guid。 您也可以在 [CMPivot 稽核狀態訊息](cmpivot.md#cmpivot-audit-status-messages)中查看此 GUID。

下一步，在 CMPivot 視窗中尋找識別碼。 此識別碼是 `ClientOperationID`。

![醒目提示 ClientOperationID 的 CMPivot 視窗](media/cmpivot-client-operationid-1902.png)

從 ClientAction 資料表尋找 `TaskID`。 `TaskID` 對應到 ClientAction 資料表中的 `UniqueID`。

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

在 `BgbServer.log` 中，尋找您從 SQL 收集的 `TaskID`，並記下 `PushID`。 `TaskID` 標示為 `TaskGUID`。 例如：

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>用戶端記錄

從站台伺服器取得資訊之後，請檢查用戶端記錄。 根據預設，用戶端記錄位於 `C:\Windows\CCM\Logs`。

在 `CcmNotificationAgent.log` 中，尋找看起來向下列各行的記錄項目：  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

檢查 `Scripts.log` 以尋找 `TaskID`。 在下列範例中，您會看到 `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`：

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> 如果您在 `Scripts.log` 中看1不到 "(fast)"，則該資料可能超過 80 KB。 在此情況下，資訊會以狀況訊息的形式傳送至站台伺服器。 使用用戶端的 `StateMessage.log` 與站台伺服器的 `Statesys.log`。

### <a name="review-messages-on-the-site-server"></a>檢閱站台伺服器上的訊息

在管理點上啟用[詳細資訊記錄](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)時，您可以看到傳入用戶端訊息的處理方式。 在 `MP_RelayMsgMgr.log` 中，尋找 `TaskID`。

在 `MP_RelayMsgMgr.log` 範例中，您可以看到用戶端的識別碼 `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` 與 `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`。 在傳送訊息識別碼至訊息處理引擎之前，會將其指派給用戶端的回應：

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

在 [ 上啟用](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions)詳細資訊記錄`SMS_MESSAGE_PROCESSING_ENGINE.log`時，會處理用戶端結果。 使用您在 `MP_RelayMsgMgr.log` 中找到的訊息識別碼。 處理記錄項目類似下列範例：

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> 如果在處理期間發生例外狀況，您可以執行下列 SQL 查詢並查看例外狀況資料行來加以檢閱。 處理訊息之後，它就不會再出現在 `MPE_RequestMessages_Instant` 資料表中。
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

在 `BgbServer.log` 中，尋找 `PushID` 以查看已回報或失敗的用戶端數目。

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

使用 `TaskID` 從 SQL 檢查 CMPivot 的監視檢視。

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[ ![針對在 1902 版中進行疑難排解的 CMPivot SQL 查詢](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a> 在 1810 與更舊版本中針對 CMPivot 進行疑難排解

在 Configuration Manager 1810 版與更舊版本中，您的站台伺服器會處理與用戶端的通訊。

### <a name="get-information-from-the-site-server"></a>從站台伺服器取得資訊

根據預設，站台伺服器記錄檔位於 `C:\Program Files\Microsoft Configuration Manager\logs`。 若您指定非預設安裝目錄，或若您將 SMS 提供者等項目卸載至另一部伺服器，此位置可能會不同。

查看 `smsprov.log` 以尋找這行：

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

在 CMPivot 視窗中尋找識別碼。 此識別碼是 `ClientOperationID`。

![醒目提示 ClientOperationID 的 CMPivot 視窗](media/cmpivot-clientoperationid.png)

從 ClientAction 資料表尋找 `TaskID`。 `TaskID` 對應到 ClientAction 資料表中的 `UniqueID`。

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

在 `BgbServer.log` 中，尋找您從 SQL 收集的 `TaskID`。 它標示為 `TaskGUID`。 例如：

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>用戶端記錄

從站台伺服器取得資訊之後，請檢查用戶端記錄。 根據預設，用戶端記錄位於 `C:\Windows\CCM\Logs`。

在 `CcmNotificationAgent.log` 中，查看與下列項目類似的記錄檔：  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

查看 `Scripts.log` 以尋找 `TaskID`。 在下列範例中，我們會看到 `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}`：

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

查看 `StateMessage.log`。 在下列範例中，您會看到 `TaskID` 位於接近訊息底部的 `<Param>` 旁：

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>檢閱站台伺服器上的訊息

開啟 `statesys.log` 以查看訊息是否收到並經過處理。 在下列範例中，您會看到 `TaskID` 位於接近訊息底部的 `<Param>` 旁。 在 SMS_STATE_SYSTEM 元件上啟用[詳細資訊記錄](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions)，以查看這些記錄項目。

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

如果訊息未經處理，請檢查狀況訊息收件匣。 預設收件匣位置是 `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`。 在那些位置中尋找檔案：

- 正在傳入
- 已損毀
- 程序

使用 `TaskID` 從 SQL 檢查 CMPivot 的監視檢視。

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>對於使用 1810 或更高版本的用戶端，除非輸出大於 80 KB，否則不會使用狀況訊息。 在這些情況下針對 CMPivot 進行疑難排解時，在您的 MP 與站台伺服器的 SMS_MESSAGE_PROCESSING_ENGINE 上啟用詳細資訊記錄即可取得詳細資訊。 如需有關如何啟用詳細資訊記錄的資訊，請參閱[站台伺服器記錄選項 ](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site)。
>
> 若要進行疑難排解，請參閱下列記錄：
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>後續步驟

- [使用 CMPivot](cmpivot.md)
- [建立並執行 Powershell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)
