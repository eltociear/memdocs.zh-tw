---
title: 針對 MSfB 整合進行疑難排解
titleSuffix: Configuration Manager
description: 提供建議和解決方法，以針對商務用和教育用 Microsoft Store 整合的一些常見問題進行疑難排解。
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149098"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>對商務用和教育用 Microsoft Store 與 Configuration Manager 的整合進行疑難排解

本文針對您在整合商務用和教育用 Microsoft Store (MSfB) 與 Configuration Manager 時可能遇到的一些常見問題，提供重要的疑難排解秘訣和修正。

如需關於搭配使用商務用和教育用 Microsoft Store 與 Configuration Manager 的詳細資訊，請參閱[使用 Configuration Manager 管理從商務與教育用 Microsoft Store 取得的應用程式](manage-apps-from-the-windows-store-for-business.md)。

## <a name="monitor"></a>監視

### <a name="component-status"></a>元件狀態

在 Configuration Manager 主控台中，移至 [監視]  工作區，展開 [系統狀態]  ，然後選取 [元件狀態]  節點。 監視下列元件的狀態：

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>同步狀態

在 Configuration Manager 主控台中，前往 [系統管理]  工作區，展開 [雲端服務]  ，然後選取 [商務用 Microsoft Store]  節點。 查看 [上次同步狀態]  資料行。

### <a name="view-synchronized-apps"></a>檢視已同步處理的應用程式

在 Configuration Manager 主控台上，前往 [軟體程式庫]  工作區，展開 [應用程式管理]  ，然後選取 [市集應用程式的授權資訊]  。


## <a name="log-files"></a>記錄檔

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

此記錄檔位於服務連接點上，存放在 Configuration Manager 安裝目錄中的 `\Logs` 下。 此檔案會記錄與雲端服務通訊的相關資訊。 這些資訊包括中繼資料、圖示、套件和授權檔案擷取。

若要變更記錄層級，請將 `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` 登錄機碼中的 `LoggingLevel` 值變更為 `0`。 如需詳細資訊，請參閱[設定記錄選項](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site)。

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

此記錄檔位於服務連接點上，存放在 Configuration Manager 安裝目錄中的 `\Logs` 下。 如果 WSfBSyncWorker 服務未啟動，或是反覆啟動並停止，請檢閱此記錄檔中的項目。

> [!NOTE]
> 此記錄檔會與其他功能共用。

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

此記錄檔位於階層中頂層站台的站台伺服器上。 其位置在 Configuration Manager 安裝目錄的 `\Logs` 下。 檔案中會記錄下列程序的相關資訊：

- 將 BusinessAppProcessWorker 元件同步處理的中繼資料資訊插入資料庫中
- 處理 `\InstallDir\inboxes\businessappprocess.box` 中的檔案

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

此記錄檔位於階層中頂層站台的站台伺服器上。 其位置在 Configuration Manager 安裝目錄的 `\Logs` 下。 如果 BusinessAppProcessWorker 服務未啟動，或是反覆啟動並停止，請檢閱此記錄檔中的項目。



## <a name="last-sync-failed"></a>上次同步失敗

如果上次同步狀態為*失敗*，請先檢閱下列[記錄檔](#log-files)以找出徵兆：

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

然後，查看下列其中一個小節說明的常見問題：

- [授權錯誤](#bkmk_fail-symptom1)
- [秘密金鑰無效](#bkmk_fail-symptom2)
- [取得應用程式權杖時發生錯誤](#bkmk_fail-symptom3)
- [內容位置不存在或權限不正確](#bkmk_fail-symptom4)
- [發出呼叫 'GET' 方法的 HTTP 要求時發生錯誤](#bkmk_fail-symptom5)
- [無法將更多位元組寫入緩衝區](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a> 授權錯誤

#### <a name="cause"></a>原因

如果設定的 Azure Active Directory (Azure AD) 應用程式無權管理此租用戶的商務用和教育用 Microsoft Store，就會發生此問題。

#### <a name="workaround"></a>因應措施

1. 以管理員身分登入商務用和教育用 Microsoft Store 入口網站。
1. 移至 [設定]  ，然後選取 [管理工具]  。
1. 如果未列出應用程式，請選取 [新增管理工具]  。 然後，依名稱搜尋，並選取與 Configuration Manager 的相同 ClientID 相關聯的 Azure AD 應用程式。
1. 如果狀態未顯示為 [作用中]  ，請選取 [動作]  區段中的 [啟用]  。
1. 在 Configuration Manager 主控台中，前往 [系統管理]  工作區並展開 [雲端服務]  ，然後選取 [商務用 Microsoft Store]  節點。 與商店同步處理，或等待下一個同步間隔發生。

> [!Tip]
> 若要在 Configuration Manager 中尋找 ClientID：
>
> 1. 在 Configuration Manager 主控台中，前往 [系統管理]  工作區並展開 [雲端服務]  ，然後選取 [Azure Active Directory 租用戶]  節點。
> 1. 選取您用於商務用和教育用 Microsoft Store 整合的租用戶。
> 1. 在結果窗格中尋找相符的應用程式，並查看 [用戶端識別碼]  資料行。

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a> 秘密金鑰無效

#### <a name="cause"></a>原因

如果 Azure AD 應用程式上用於商務用和教育用 Microsoft Store 設定的秘密金鑰已過期，就會發生此問題。

#### <a name="resolution"></a>解決方案

更新 Azure AD 應用程式的秘密金鑰。 如需詳細資訊，請參閱[更新秘密金鑰](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew)。

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a> 取得應用程式權杖時發生錯誤

#### <a name="cause"></a>原因

如果連線的應用程式已不存在於 Azure AD 中，就會發生此問題。

#### <a name="resolution"></a>解決方案

刪除並重新建立商務用和教育用 Microsoft Store 的連線。

1. 在 Configuration Manager 主控台中，前往 [系統管理]  工作區並展開 [雲端服務]  ，然後選取 [商務用 Microsoft Store]  節點。
1. 選取現有的連線。
1. 在功能區中選取 [刪除]  。

然後重新建立連線。 如需詳細資訊，請參閱下列文章：

- [設定 Azure 服務](../../core/servers/deploy/configure/azure-services-wizard.md)
- [設定商務用和教育用 Microsoft Store 同步處理](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a> 內容位置不存在或權限不正確

#### <a name="cause"></a>原因

在設定商務用和教育用 Microsoft Store 的連線時，您可以指定用來儲存同步處理內容的網路共用。 如果此共用不存在或權限不正確，就會發生此問題。 服務連接點其電腦帳戶應該是此目錄和任何子目錄的擁有者。<!-- memdocs#146 --> 如果不是，則會看到類似下列的錯誤：

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

若要查看您設定的位置：

1. 在 Configuration Manager 主控台中，前往 [系統管理]  工作區並展開 [雲端服務]  ，然後選取 [商務用 Microsoft Store]  節點。

1. 選取帳戶並開啟其 [屬性]  。

1. 切換至 [設定]  索引標籤。[位置]  設定會顯示用來儲存從商務用和教育用 Microsoft Store 下載之應用程式內容的網路路徑。

#### <a name="workaround"></a>因應措施

1. 如果共用尚不存在，請加以建立。

1. 檢查資料夾的 NTFS 權限，以及網路共用的權限。 為服務連接點的電腦帳戶授與**讀取**和**寫入**權限。

如果您想要重新設定位置，請刪除與新內容位置的連線，然後重新加以建立。

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a> 發出呼叫 'GET' 方法的 HTTP 要求時發生錯誤

#### <a name="cause"></a>原因

如果來自商店的應用程式在同步時耗時過久，而致使內容 URL 過期，就會發生此問題。

#### <a name="workaround"></a>因應措施

重試同步程序

1. 在 Configuration Manager 主控台中，前往 [系統管理]  工作區並展開 [雲端服務]  ，然後選取 [商務用 Microsoft Store]  節點。
1. 選取連線。 在功能區中，選取 [從商務用 Microsoft Store 同步]  。

每次嘗試時，作業應該會漸趨完成。 視下列因素之不同，有可能需要重試數次：

- 離線應用程式的數目
- 套件的大小
- 網路速度

隨著每次的嘗試，您看到錯誤的次數應該會愈來愈少。 如果錯誤數目未減少，表示還有其他問題。

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a> 無法將更多位元組寫入緩衝區

#### <a name="cause"></a>原因

如果應用程式的套件大於 500 MB，就會發生此問題。 Configuration Manager 僅支援以小於 500 MB 的套件自動同步處理離線應用程式。

#### <a name="workaround"></a>因應措施

您無法自動同步這些應用程式，但您可以下載內容，並手動建立應用程式：

1. 從 **WSfbSynWorker.log** 中的以下這一行取得失敗應用程式的識別碼：

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. 以管理員身分登入商務用和教育用 Microsoft Store 入口網站。 尋找此應用程式的頁面。

    > [!Tip]
    > 頁面的 URL 類似於：`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. 選取 [離線]  (如果尚未選取)。 然後，選取 [管理]  。

    1. 在您的應用程式內容共用上為所有支援的平台分別建立個別的資料夾。

    1. 將套件下載至套件資料夾。

    1. 將編碼的授權檔案以 `.bin` 檔案的形式下載至套件資料夾。

    1. 將所有必要的架構下載至套件資料夾。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [應用程式管理]  ，然後選取 [應用程式]  節點。

1. [建立應用程式](create-applications.md)，並手動指定應用程式資訊。

    1. 為您先前下載的每個支援平台建立部署類型。

    1. 類型：**Windows 應用程式套件 (\*.appx、\*.appxbundle)**

    1. 為實際的應用程式套件指定 appx/appxbundle，而不是為必要的相依性套件指定。

在最終的 [匯入資訊]  頁面上確認下列詳細資料：

- **授權檔案：** 指定 `.bin` 檔案。 離線應用程式需要此授權檔案。
- **Windows 應用程式相依性：** 確認已為此套件下載所有必要的相依性。


## <a name="sync-doesnt-run"></a>同步未執行

本節將說明下列同步問題：

- 您以手動方式啟動了同步程序，但該程序未執行
- 站台不會自動每日同步

請先檢閱下列[記錄檔](#log-files)以找出徵兆：

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

然後，查看下列其中一個小節說明的常見問題：

- [手動同步未啟動](#bkmk_sync-symptom1)
- [自動每日同步未執行，且 SMS_BUSINESS_APP_PROCESS_MANAGER.記錄中出現「正在關閉 # 個背景工作」錯誤](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a> 手動同步未啟動

#### <a name="cause"></a>原因

如果您在上一次同步後的 10 分鐘內再次啟動同步，就會發生此問題。同步的頻率不可超過每 10 分鐘一次。

#### <a name="resolution"></a>解決方案

等待至少 10 分鐘，再啟動另一個同步。

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a> 自動每日同步未執行，且 SMS_BUSINESS_APP_PROCESS_MANAGER.記錄中出現「正在關閉 # 個背景工作」錯誤

#### <a name="cause"></a>原因

如果 SMS_BUSINESS_APP_PROCESS_MANAGER 元件停止 WsfbSyncWorker 執行緒，就會發生此問題。 此錯誤可能會指出 `2` 或 `4` 個背景工作。

#### <a name="workaround"></a>因應措施

重新啟動 **SMS_EXECUTIVE** 服務。

如果您無法重新開機該主要服務，請停止具有 MSfB 背景工作的兩個元件，然後再啟動這兩個元件：

1. 在執行服務連接點的伺服器上開啟 Windows 登錄

1. 移至 `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. 將 [要求的作業] 設定為 [停止]  。

    1. 重新整理以確認目前的狀態為 [已停止]  。

1. 移至 `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. 將 [要求的作業] 設定為 [停止]  。

    1. 重新整理以確認 [目前的狀態] 為 [已停止]  。

1. 在 **SMS_CLOUDCONNECTION** 中，將 [要求的作業] 設定為 [啟動]  。

1. 在 **SMS_BUSINESS_APP_PROCESS_MANAGER** 中，將 [要求的作業] 設定為 [啟動]  。


## <a name="language-related-issues"></a>語言相關問題

本節包含下列常見的問題：

- [未套用語言選擇變更](#bkmk_lang-symptom1)
- [並非所有授權資訊都會以所有選取的語言顯示](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a> 未套用語言選擇變更

#### <a name="cause"></a>原因

如果快取語言選取項目，且在屬性值變更後未加以清除，就會發生此問題。

#### <a name="workaround"></a>因應措施

若要解決此問題，請重新啟動 **SMS_Executive** 服務。

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a> 並非所有授權資訊都會以所有選取的語言顯示

#### <a name="cause"></a>原因

如果商務用和教育用 Microsoft Store 應用程式的授權資訊未包含指定語言的當地語系化資料，就會發生此問題。

#### <a name="workaround"></a>因應措施

為已建立的應用程式手動新增任何遺漏的語言。


## <a name="offline-applications"></a>離線應用程式

本節包含下列常見的問題：

- [因無法驗證內容而無法建立離線應用程式](#bkmk_off-symptom1)
- [無法安裝從離線授權資訊建立的應用程式](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a> 因無法驗證內容而無法建立離線應用程式

#### <a name="cause"></a>原因

如果離線應用程式的同步處理內容已損毀或修改，就會發生此問題。

#### <a name="workaround"></a>因應措施

啟動新的同步。同步完成後，應該驗證並下載任何不正確的內容檔案。

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a> 無法安裝從離線授權資訊建立的應用程式

#### <a name="cause"></a>原因

如果您將應用程式部署到執行的 Windows 10 版本早於 1511 版的用戶端，就會發生此問題。 只有在 Windows 10 1511 版和更新版本上，才支援對來自商務用和教育用 Microsoft Store 的應用程式進行離線授權。

#### <a name="resolution"></a>解決方案

安裝 Windows 10 的最新版本。


## <a name="next-steps"></a>後續步驟

若要尋找其他說明，請參閱[尋找使用 Configuration Manager 的說明](../../core/understand/find-help.md)。
