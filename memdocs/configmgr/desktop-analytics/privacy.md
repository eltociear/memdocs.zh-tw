---
title: 電腦分析資料隱私權
titleSuffix: Configuration Manager
description: 電腦分析致力於保護客戶資料隱私權
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 34005a63b372198bbc2e3079f8ab560ef6b2b791
ms.sourcegitcommit: c333fc6627f5577cde9d2fa8f59e642202a7027b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2020
ms.locfileid: "84795630"
---
# <a name="desktop-analytics-data-privacy"></a>電腦分析資料隱私權

電腦分析完全致力於保護客戶資料隱私權，主要原則如下：

- **透明度：** 我們會完整記錄 Windows 診斷事件。 請與貴公司的安全性與合規性小組一同審查。 Windows 診斷資料檢視器可讓您查看從指定裝置送出的診斷資料。 如需詳細資訊，請參閱[診斷資料檢視器概觀](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview)。  

- **控制權：** 您可以掌控要與 Microsoft 分享診斷資料的層級。 Windows 10 1709 版新增一項原則，可將增強診斷資料限制為電腦分析所需的最小值。  

- **安全性：** Microsoft 利用強大的安全性和加密，保護您的資料。  

- **信任：** 電腦分析支援 Microsoft [隱私權聲明](https://privacy.microsoft.com/privacystatement)和[線上服務條款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)。  

如需詳細資訊，請參閱 [Microsoft 根據 GDPR 為處理器的 Windows 服務](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr)。<!-- 5353168 -->

## <a name="data-flow"></a>資料流程

下圖顯示診斷資料從個別裝置通過診斷資料服務、暫時性儲存體，以及到 Log Analytics 工作區的流動方式：

![說明裝置診斷資料流程的圖表](media/da-data-flow.png)

1. 您登入 Azure 入口網站，並連線到電腦分析。 您建立要與 Configuration Manager 連線的 Azure AD 應用程式。 當您設定電腦分析時，您會在所選擇的位置中建立 Azure Log Analytics 工作區。  

2. 您連線到 Configuration Manager 並註冊裝置  

    1. 您在 Configuration Manager 中使用 Azure AD 應用程式詳細資料設定電腦分析雲端服務。  

    2. 在 15 分鐘內，Configuration Manager 會使用您的租用戶識別碼，將下列資料與電腦分析進行同步處理。 此程序會每小時重複一次。

      - [建立部署計劃](create-deployment-plans.md)所需的裝置集合相關資訊。 此資訊包括集合識別碼、階層識別碼、集合名稱和裝置計數。 
      - [註冊裝置](enroll-devices.md)所需的資訊。 此資訊包括集合識別碼、SMS 唯一識別碼、OS 組建版本、裝置名稱和序號。
      - 來自[監視連線健全狀況](monitor-connection-health.md)儀表板的資訊。 此資訊包括每個健全狀況狀態的裝置計數，以及裝置屬性。
      - 部署計劃的相關資訊，其中包括集合識別碼、部署識別碼、試驗或生產部署類型，以及每個升級決策的裝置計數。

    3. Configuration Manager 為目標集合中的裝置設定商業識別碼、診斷資料層級和其他設定。 此設定會指定要出現在電腦分析工作區中的裝置。  

    4. 您將相容性更新部署到所有目標裝置。  

3. 裝置將診斷資料傳送至適用於 Windows 的 Microsoft 診斷資料管理服務。 所有診斷資料都會透過 HTTPS 加密，並在從裝置傳輸到此服務期間使用憑證釘選。 Microsoft 資料管理服務裝載於美國。

      - 應用程式錯誤、核心錯誤、沒有回應的應用程式，以及其他應用程式特定的問題，會使用 Windows 錯誤報告 API 將特定於應用程式的問題報告傳送給 Microsoft。 如需此資料流程的特定詳細資料，請參閱[使用 WER](https://docs.microsoft.com/windows/win32/wer/using-wer) \(英文\)。
      
4. Microsoft 每天都會產生以 IT 為主的見解快照集。 此快照集結合了來自 Windows 的診斷資料與已註冊裝置的輸入。 此程序會在只有電腦分析能使用的暫時性儲存體中進行。 該暫時性儲存體裝載於美國的 Microsoft 資料中心。 所有資料都是透過 SSL (HTTPS) 加密通道來傳送。 快照集會依商業識別碼來分隔。  

5. 快照集接著會複製到 Azure Log Analytics 工作區。 這項資料轉送會透過 HTTPS 使用 Webhook 擷取通訊協定進行，這是 Log Analytics 的功能。 電腦分析對 Log Analytics 儲存體沒有任何讀取或寫入權限。 電腦分析使用共用存取簽章 (SAS) URI 來呼叫 Webhook API。 然後，Log Analytics 會透過 HTTPS 從儲存體資料表取得資料。

6. 電腦分析會將輸入儲存在 Log Analytics 儲存體中。 這些設定包括部署計劃，以及升級和重要性的資產決策。  

## <a name="other-resources"></a>其他資源

如需電腦分析的隱私權相關常見問題集，請參閱[隱私權常見問題集](faq.md#privacy)。

如需相關隱私權層面的詳細資訊，請參閱下列文章：

- [適用於 IT 決策者的 Windows 10 和 GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [在組織中設定 Windows 診斷資料](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7, Windows 8, and Windows 8.1 appraiser diagnostic data events and fields](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields) (Windows 7、Windows 8 和 Windows 8.1 評鑑程式診斷資料事件與欄位)  

- [Windows 10 1809 版基本層級 Windows 診斷事件與欄位](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [電腦分析使用的 Windows 10 1709 版增強診斷資料事件與欄位](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Windows 安裝程式錯誤報告](https://docs.microsoft.com/windows/deployment/upgrade/windows-error-reporting) \(部分機器翻譯\)

- [診斷資料檢視器概觀](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Licensing terms and documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) (授權條款與文件)  

- [Log Analytics 資料金安全性](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Microsoft Azure 資料中心的安全性和隱私權](https://azure.microsoft.com/global-infrastructure/)  

- [對受信任雲端充滿信心](https://azure.microsoft.com/overview/trusted-cloud/)  

- [信任中心](https://www.microsoft.com/trustcenter)  

- [隱私盾](https://www.privacyshield.gov/)  

不同於電腦分析，Configuration Manager 會將診斷和使用方式資料傳送給 Microsoft。 Microsoft 可使用這項資料來改善 Configuration Manager 未來版本的安裝體驗、品質及安全性。 如需詳細資訊，請參閱 [Configuration Manager 的診斷和使用方式資料](../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。
