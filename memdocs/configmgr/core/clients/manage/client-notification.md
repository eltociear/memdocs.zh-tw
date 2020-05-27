---
title: 用戶端通知
titleSuffix: Configuration Manager
description: 立即從中央 Configuration Manager 主控台中採取行動以管理用戶端。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7680c8f955773f169d56f36eb9bbe6507d2d7ce6
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427814"
---
# <a name="client-notification-in-configuration-manager"></a>Configuration Manager 中的用戶端通知

適用於：Configuration Manager (最新分支)

若要對遠端用戶端立即採取行動，請從 Configuration Manager 主控台傳送用戶端通知動作。 在個別裝置或裝置集合上啟動這些動作。

## <a name="actions"></a>動作

下列動作位在 [常用] 索引標籤的裝置或集合群組功能區。

### <a name="install-client"></a>安裝用戶端

開啟 [安裝用戶端精靈]。 此精靈會使用用戶端推入安裝來安裝 Configuration Manager 用戶端。 如需詳細資訊，請參閱[用戶端推入安裝](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。

#### <a name="permissions---install-client"></a>權限 - 安裝用戶端

這個動作需要 **Collection** 物件的**修改資源**和**讀取**權限。

下列內建角色預設具有這些權限：

- 應用程式系統管理員  
- 系統高權限管理員  
- 基礎結構系統管理員  
- 操作系統管理員  
- OS Deployment Manager  

將這些權限新增至需要推入用戶端的任何自訂角色。

### <a name="run-script"></a>執行指令碼

開啟 [執行指令碼] 精靈，以在集合內的所有用戶端上執行 PowerShell 指令碼。 如需詳細資訊，請參閱[建立及執行 PowerShell 指令碼](../../../apps/deploy-use/create-deploy-scripts.md)。

#### <a name="permissions---run-script"></a>權限 - 執行指令碼

這個動作需要 **Collection** 物件的**執行指令碼**權限。

下列內建角色預設具有此權限：

- 系統高權限管理員  
- 基礎結構系統管理員  
- 操作系統管理員  

將此權限新增至需要執行指令碼的任何自訂角色。

### <a name="start-cmpivot"></a>啟動 CMPivot

啟動 **CMPivot**，針對目標裝置執行即時查詢。 如需詳細資訊，請參閱 [CMPivot](../../servers/manage/cmpivot.md)。

#### <a name="permissions---start-cmpivot"></a>權限 - 啟動 CMPivot

這個動作需要和[執行指令碼](#run-script)動作相同的權限。

從 1906 版本開始，您可以在 [集合] 物件上使用 [執行 CMPivot] 權限。

## <a name="client-notification"></a>用戶端通知

這些動作位在 [用戶端通知] 功能表下，[常用] 索引標籤的裝置或集合群組功能區中。

在 1806 版和較舊版本中，[用戶端通知] 選項僅從 [裝置集合] 節點，或是檢視 [裝置集合] 的成員資格時提供。 從 1810 版開始，您可以直接從 [裝置] 節點啟動 [用戶端通知]。 不需要再從集合成員資格檢視中執行。 <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>權限 - 用戶端通知

<!--SCCMDocs-pr issue #2972-->
從 1810 版開始，用戶端通知動作現在需要 Collection 物件的**通知資源**權限。 此權限適用於 [用戶端通知] 功能表下的所有動作。

下列內建角色預設具有此權限：

- 系統高權限管理員  
- 操作系統管理員  

將此權限新增至需要使用用戶端通知動作的任何自訂角色。

### <a name="download-computer-policy"></a>下載電腦原則

重新整理裝置原則。 如需詳細資訊，請參閱[起始 Configuration Manager 用戶端的原則抓取](manage-clients.md#BKMK_PolicyRetrieval)。  

### <a name="download-user-policy"></a>下載使用者原則

重新整理使用者原則。  

### <a name="collect-discovery-data"></a>收集探索資料

觸發用戶端以傳送探索資料記錄 (DDR)。 如需詳細資訊，請參閱[活動訊號探索](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。  

### <a name="collect-software-inventory"></a>收集軟體清查

觸發用戶端以執行軟體清查週期。 如需詳細資訊，請參閱[軟體清查簡介](inventory/introduction-to-software-inventory.md)。  

### <a name="collect-hardware-inventory"></a>收集硬體清查

觸發用戶端以執行硬體清查週期。 如需詳細資訊，請參閱[硬體清查簡介](inventory/introduction-to-hardware-inventory.md)。  

### <a name="evaluate-application-deployments"></a>評估應用程式部署

觸發用戶端以執行應用程式部署評估週期。 如需詳細資訊，請參閱[排程部署的重新評估](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments)。  

### <a name="evaluate-software-update-deployments"></a>評估軟體更新部署

觸發用戶端以執行軟體更新部署評估週期。 如需詳細資訊，請參閱[軟體更新簡介](../../../sum/understand/software-updates-introduction.md)。  

### <a name="switch-to-the-next-software-update-point"></a>切換至下一個軟體更新點

觸發用戶端以切換至下一個可用的軟體更新點。 如需詳細資訊，請參閱[軟體更新點切換](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)。  

### <a name="evaluate-device-health-attestation"></a>評估裝置健全狀況證明

觸發 Windows 10 用戶端以檢查並傳送其最新的裝置健全狀況狀態。 如需詳細資訊，請參閱[健全狀況證明](../../servers/manage/health-attestation.md)。  

### <a name="wake-up"></a>喚醒

從 1810 版開始，觸發程序裝置設定為支援使用相同子網路上的其他裝置來傳送網路喚醒套件進行喚醒。 如需詳細資訊，請參閱[如何設定網路喚醒](../deploy/configure-wake-on-lan.md)。

### <a name="restart"></a>重新啟動

觸發以重新啟動選取的裝置。 如需詳細資訊，請參閱[重新啟動用戶端](manage-clients.md#restart-clients)。

## <a name="client-diagnostics"></a>用戶端診斷
<!--4433455-->

從 1910 版開始，Configuration Manager 主控台中有 [用戶端診斷] 的新裝置動作。 已新增下列動作：

- **啟用詳細資訊記錄**：將 CCM 元件的全域記錄層級變更為 [詳細資訊]，並啟用 [偵錯記錄]。
- **停用詳細資訊記錄**：將全域記錄層級變更為預設值，並停用偵錯記錄。
- **收集用戶端記錄** (自 2002 版開始)：用戶端通知訊息會傳送至選取的用戶端，以收集 CCM 記錄。 系統會使用軟體清查檔案收集來傳回記錄。 <!--4226618-->
   - 壓縮的用戶端記錄檔大小限制為 100 MB。 <!--6366098-->
   - 使用[資源總管](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag)管理及檢視這些檔案。

   [![從主控台收集用戶端記錄](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - 這些動作只會變更記錄詳細程度，而不是大小或歷程記錄。 更詳細的記錄會產生更多記錄內容。
> - 管理點角色也會使用 CCM 元件。 如果目標裝置也是管理點，此動作也適用於該角色。

如需這些用戶端設定的詳細資訊，請參閱[關於記錄檔](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)。

在用戶端的 **diagnostics.log** 中追蹤工作狀態。 收集用戶端記錄檔後，系統會將其他資訊記錄在管理點的 **MP_SinvCollFile.log** 及站台伺服器的 **sinvproc.log** 中。

> [!Tip]
> 收集的用戶端記錄檔會根據軟體清查檔案收集設定來儲存。 這些檔案會儲存在 **Inboxes\sinv.box\FileCol** 目錄中的站台伺服器上。 版本數目沒有已定義的限制。 [刪除過時收集檔案](../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-collected-files)的站台維護工作會依排程刪除檔案，其預設為每 90 天。

### <a name="prerequisites---client-diagnostics"></a>必要條件 - 用戶端診斷

- 將目標用戶端更新為最新版本。

- 您的 Configuration Manager 系統管理使用者需要**通知資源**權限。

  下列內建角色預設具有此權限：

  - 系統高權限管理員  
  - 基礎結構系統管理員  

  將此權限新增至需要使用用戶端通知動作的任何自訂角色。


## <a name="endpoint-protection"></a>Endpoint Protection

下列動作位在 [Endpoint Protection] 功能表下。 此功能表位於 [常用] 索引標籤的集合群組功能區中。當您選取一或多部裝置時，這些動作是位在功能區 [選取的物件] 索引標籤。

如需詳細資訊，請參閱 [Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。

### <a name="permissions---endpoint-protection"></a>權限 - Endpoint Protection

這個動作需要 **Collection** 物件的**強制執行安全性**權限。

下列內建角色預設具有此權限：

- 系統高權限管理員  
- Endpoint Protection Manager  
- 操作系統管理員  

將此權限新增至需要觸發 Endpoint Protection 動作的任何自訂角色。

### <a name="full-scan"></a>完整掃描

觸發 Endpoint Protection 或 Windows Defender 以執行「完整」反惡意程式碼軟體掃描。  

### <a name="quick-scan"></a>快速掃描

觸發 Endpoint Protection 或 Windows Defender 以執行「快速」反惡意程式碼軟體掃描。  

### <a name="download-definition"></a>下載定義

觸發 Endpoint Protection 或 Windows Defender 以下載最新的反惡意程式碼軟體定義。  

## <a name="see-also"></a>請參閱

- [如何管理用戶端](manage-clients.md)
- [如何管理集合](collections/manage-collections.md)
