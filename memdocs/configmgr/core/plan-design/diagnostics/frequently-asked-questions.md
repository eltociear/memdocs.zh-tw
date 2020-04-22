---
title: 診斷及使用方式資料常見問題集
titleSuffix: Configuration Manager
description: 與 Configuration Manager 的診斷及使用方式資料有關的常見問題集
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688476"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>與診斷和使用方式資料有關的常見問題集

適用於：  Configuration Manager (最新分支)

本文提供 System Center Configuration Manager 的診斷和使用方式資料的常見問題集解答。

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> 我可以關閉診斷及使用方式資料嗎？

若要在站台傳送資料時協助管理，可以在離線模式下使用服務連接點。 然後使用服務連線工具來手動傳送資料。 如需詳細資訊，請參閱下列文章：

- [關於服務連接點](../../servers/deploy/configure/about-the-service-connection-point.md)
- [使用服務連線工具](../../servers/manage/use-the-service-connection-tool.md)

若要支援新版本的 Windows 10 和雲端服務 (例如 Microsoft Intune)，您需要定期更新 Configuration Manager 的最新分支。 Microsoft 需要診斷及使用方式資料至少為基本層級。 使用此資料可將產品保持在最新狀態，不但能改善更新體驗，還能提升產品的品質和安全性。

服務連接點處於離線模式時，不會將任何資料傳送至服務。 當您切換至線上模式或使用服務連線工具時，則會將資料傳送至服務以檢查是否有更新。

您也可以選擇 Configuration Manager 收集的資料層級。 如需詳細資訊，請參閱[診斷使用方式資料的層級](levels-overview.md)。

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> 什麼是資料保留期間？

Microsoft 會將 Configuration Manager 診斷及使用方式資料儲存一年。

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> 在安裝程式執行時，是否會傳送診斷及使用方式資料？

否。 只有在安裝完站台並正常運作之後，才會傳送診斷和使用方式資料。

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> 多久傳送一次資料？

從您安裝站台的日期開始，SQL 預存程式會每七天執行一次。

- 在線上模式中，服務連接點會在執行查詢之後上傳資料。

- 在離線模式中，您可以使用服務連線工具來上傳資料。 (資料一開始並不可供離線使用，必須等到您安裝完站台 7 天後，才可供離線使用。)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> 是否可以使用資料來形成網路地圖？

否。 此資料並不會包括任何網路詳細資料，例如 IP 位址或詳細的地理資訊。 如需詳細資訊，請參閱[診斷使用方式資料的層級](levels-overview.md#bkmk_versions)，並尋找您所使用版本的詳細資料。

資料會包含每個站台的時區資訊。 這資訊可讓您深入了解階層中站台的廣泛地理位置和全球散佈情況。

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> 您是否可以看到自訂 SQL 資料表中的資料？

否。 Configuration Manager 會透過 SQL 預存程序來收集診斷及使用方式資料。 這些預存程序針對資料庫中的預設產品資料表執行。 所有這些 SQL 資料表前面會加上 **TEL_** 。 在進行 SQL 結構描述偵測查詢的過程中，所有資料表名稱都會經過雜湊處理，以便與已知的預設值做比較。 這個行為會判斷自訂資料表是否存在於資料庫中。 若自訂資料表存在，就會通知 Microsoft 您已從預設值延伸資料庫結構描述。 它不包含任何這些資料表內儲存的資料。

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> 您是否可以看到其他資料庫？

否。 用來收集資料的預存程序會限制在 Configuration Manager 站台資料庫。 Microsoft 無法看到其他資料庫的名稱，或其他資料庫中的資料。

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> 是否會有任何資料傳送至其他整合式雲端服務？

是，當您將這些服務與 Configuration Manager 整合的時候。 在與任何雲端服務互動的過程中，Configuration Manager 會將某些資料傳送至該服務。 此資料特定於該雲端服務，且會與 Configuration Manager 診斷及使用方式資料分開。 如需與其他雲端服務互動時所使用的特定資料詳細資訊，請參閱該服務的文件。

例如，下列雲端服務是 Microsoft 端點管理員的一部分：

- [電腦分析資料隱私權](../../../desktop-analytics/privacy.md)
- [Intune 中的隱私權與個人資料](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Windows Autopilot 需求](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> Configuration Manager 是否會收集任何個人資料？

否。 Configuration 不會收集或傳輸任何個人資料或客戶資料。 Configuration 是內部部署產品，您可以直接部署、管理及操作。 Microsoft 收集的診斷及使用方式資料可改善未來版本的安裝體驗、品質與安全性。

如需 Configuration Manager 資料的詳細資訊，請參閱[診斷使用方式資料的層級](levels-overview.md)。
