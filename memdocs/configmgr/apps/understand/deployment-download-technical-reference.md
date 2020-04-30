---
title: 應用程式下載技術參考
titleSuffix: Configuration Manager
description: 針對 Configuration Manager 應用程式下載進行疑難排解的技術參考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688856"
---
# <a name="application-download-in-configuration-manager"></a>Configuration Manager 中的應用程式下載

適用於：  Configuration Manager (最新分支)

在繼續之前，請先參閱[應用程式部署用戶端元件](client-components-technical-reference.md)以了解 DCM 和 CI 代理程式作業處理。

## <a name="download-initiation"></a>下載起始

應用程式內容下載是由用戶端上的 CI 代理程式元件在 **StateDownloadingContents** 階段期間起始。 無論應用程式是部署至裝置集合或使用者集合，此程序都相同。

- 針對**可用**部署，當使用者從軟體中心起始應用程式安裝時，就會下載應用程式內容。
- 針對**必要**部署，當啟用指派並且在評估之後發現應用程式「適用」時，就會下載應用程式內容。 若要了解何時啟用指派，請參閱[應用程式部署至裝置集合](device-deployment-technical-reference.md)或[應用程式部署至使用者集合](user-deployment-technical-reference.md)文章。

當 CI 代理程式起始內容下載時，會建立由 CI 工作管理員元件處理的工作。 CI 工作管理員接著會起始內容下載。 您可以使用部署類型唯一識別碼，在 **CITaskMgr.log** 中追蹤此活動。

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>發佈點位置

所有下載工作都是由內容存取元件處理，負責管理用戶端快取。 建立下載工作之後，內容存取元件會檢查用戶端快取中是否已有內容。 如果內容無法使用，其會建立一個位置要求，以取得可從其中取得內容的發佈點清單。 您可以使用內容唯一識別碼，在用戶端上的 **CAS.log** 和 **LocationServices.log** 中追蹤此活動。

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> 雖然位置服務元件會處理位置要求，但是不會直接從管理點要求位置。 對於管理點的所有要求通常會經過 CCM 傳訊元件，該元件會記錄至 **CcmMessaging.log**。

位置回覆 XML 包含根據用戶端界限群組的發佈點清單。 此清單會根據[內容來源優先順序](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority)在用戶端上進行剖析和保存。 您可以藉由使用內容唯一識別碼並尋找 `Persisted location`，在 **ContentTransferManager.log** 中看到此活動。 

如果位置回覆 XML 不包含任何發佈點，**ContentTransferManager.log** 會顯示 `Received empty location update`，用戶端在下載應用程式時可能會卡在 0%。 此回覆通常是因為界限群組設定問題所造成。 如需詳細資訊，請參閱[下載失敗](../deploy-use/troubleshoot-application-deployment.md#download-failures)。

## <a name="content-download"></a>內容下載

一旦取得發佈點位置，內容存取元件就會建立內容傳輸作業。 您可以使用內容唯一識別碼，在 **CAS.log** 中追蹤此活動。

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

內容傳輸管理員接著會建立資料傳輸服務作業來執行內容下載。 您可以使用內容唯一識別碼，在用戶端上的 **ContentTransferManager.log** 中追蹤此活動。

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> 此記錄項目可以用來識別 CTM 和 DTS 作業識別碼，該識別碼可用來分別在 **ContentTransferManager.log** 和 **DataTransferService.log** 中追蹤內容傳輸的進度。

資料傳輸服務會藉由建立背景智慧型傳送服務 (BITS) 作業並等候下載完成，來執行應用程式內容的下載。 您可以使用從 **ContentTransferService.log** 取得的 DTS 作業識別碼，在用戶端上的 **DataTransferService.log** 中追蹤此活動。

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

下載完成之後，就會通知內容存取元件。 內容存取元件接著會驗證下載的內容，以確保在下載期間不會更改內容。 您可以使用內容唯一識別碼，在 **CAS.log** 中追蹤此活動。

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

最後，在驗證內容之後，CI 代理程式會收到工作完成通知，而且 CI 代理程式作業會移至下一個階段。

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>後續步驟

- [應用程式安裝](deployment-install-technical-reference.md)
