---
title: 報告的簡介
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中可讓您用來管理報告的工具組和資源。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1aae76845d18d8191b6f773df5491d3a144940c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694546"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Configuration Manager 的報告簡介

適用於：  Configuration Manager (最新分支)

Configuration Manager 的報告會提供一組工具與資源，其有助使用 SQL Server Reporting Services (SSRS) 以及 Power BI 報表伺服器的進階報告功能。 這兩種報告平台都能提供豐富的自訂報表撰寫體驗。 報告功能有助收集、整理及呈現組織中豐富的 Configuration Manager 資料資訊。 Configuration Manager 可在 Reporting Services 中提供許多預先定義的報表，以供在不需要進行任何變更的情況下加以利用。 您可複製並修改這些預設報表以符合需求，也可以建立自訂報表。

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services 提供齊全的現成工具與服務，其有助您建立、部署以及管理組織的報表。 此服務同時具有程式設計功能，其可供延伸和自訂報表功能。 Reporting Services 是一個以伺服器為基礎的報告平台，可針對不同類型的資料來源提供完整報告功能。

Configuration Manager 使用 SQL Server Reporting Services 作為主要報告解決方案。 與 Reporting Services 整合可提供以下優勢：  

- 使用業界標準報告系統，查詢 Configuration Manager 資料庫。  

- 使用 Configuration Manager 報表檢視器或使用報表管理員 (透過 Web 連線至報告) 顯示報告。  

- 提供高效能、 可用性和延展性。  

- 提供可供使用者訂閱的報表訂閱。 例如，主管可訂閱每天以電子郵件傳送的報表，其詳述軟體更新發行的狀態。

- 使用不同種類的熱門格式來匯出報表。  

如需詳細資訊，請參閱[什麼是 SQL Server Reporting Services (SSRS)？](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports?view=sql-server-ver15)

## <a name="power-bi-report-server"></a>Power BI 報表伺服器

<!-- 3721603 -->

從 2002 版開始，Power BI 報表伺服器已與 Configuration Manager 報告整合。 這項整合為您提供現代化視覺效果和更好的效能。 其新增的 Power BI 報表主控台支援類似 SQL Server Reporting Services 已有的功能。 如需詳細資訊，請參閱[整合 Power BI 報表伺服器](powerbi-report-server.md)。

Power BI 報表伺服器是具有入口網站的內部部署報表伺服器，您可在此伺服器中陳列和管理報表。 伺服器中包含用來建立 Power BI 報表、編頁報表、行動報表及 KPI 的工具。 如需詳細資訊，請參閱[什麼是 Power BI 報表伺服器？](https://docs.microsoft.com/power-bi/report-server/get-started)。

## <a name="reporting-services-point"></a>Reporting Services 點

Reporting Services 點是您在執行 Microsoft SQL Server Reporting Services 的伺服器上所新增站台系統角色。 Reporting Services 點具有下列功能：

- 將 Configuration Manager 的報表定義複製到 Reporting Services
- 根據報表類別建立報表資料夾
- 在報表資料夾和報表上設定安全性原則。 這些原則是根據 Configuration Manager 系統管理使用者的角色型權限所設定。 如果變更安全性原則，則 Reporting Services 點會在 10 分鐘內連線至 Reporting Services 以重新套用該安全性原則。

如需如何規劃及安裝 Reporting Services 點的詳細資訊，請參閱下列文章：

- [規劃報告](planning-for-reporting.md)

- [設定報告](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager 報告

Configuration Manager 在超過 50 個報告資料夾中提供超過 400 份報表的報表定義。 在 Reporting Services 點安裝程序期間，Configuration Manager 會將這些報表定義複製到 SQL Server Reporting Services 的根報告資料夾中。 Configuration Manager 主控台會顯示這些報告，並根據報告類別將其歸類到子資料夾中。

報表不會在 Configuration Manager 階層中向上或向下散佈， 只會針對建立該報表的站台資料庫執行。 由於 Configuration Manager 會複製整個階層的全域資料，因此可在報表中存取整個階層的資訊。 當有報告從站台資料庫擷取資料時，報告會具有目前站台和子站台的站台資料存取權，以及階層中每個站台的全域資料存取權。

就像其他 Configuration Manager 物件一樣，系統管理使用者必須具有執行或修改報告所需的適當權限。 若要執行報告，系統管理使用者必須具有物件的 [執行報告]  權限。 若要建立或修改報告，系統管理使用者必須具有物件的 [修改報告]  權限。

### <a name="create-and-modify-reports"></a>建立和修改報表

對於以 Reporting Services 為基礎的報表，Configuration Manager 會將 Microsoft SQL Server 報表產生器作為專用的撰寫與編輯工具，以用於處理模型式與 SQL 式報表。 當您在 Configuration Manager 主控台建立或編輯報告時，會開啟報表產生器。 如需詳細資訊，請參閱[報告作業和維護](operations-and-maintenance-for-reporting.md)。

從 2002 版開始，主控台已與 Power BI Desktop 整合，以供建立或編輯 Power BI 報表。 如需詳細資訊，請參閱[建立 Power BI 報表](powerbi-report-server.md#create-power-bi-reports)。

### <a name="run-reports"></a>執行報表

當在 Configuration Manager 主控台執行以 Reporting Services 為基礎的報表時，報表檢視器會隨即開啟並連線至 Reporting Services。 在您指定任何必要的報告參數後，Reporting Services 便會擷取資料，並在檢視器中顯示結果。 您也可以連線到 SQL Services Reporting Services，連線到站台的資料來源，然後執行報告。

從 2002 版開始，當執行以 Power BI 為基礎的報表時，該報表會在網頁瀏覽器中開啟。

### <a name="report-prompts"></a>報告提示

當建立或修改報表時，可以設定報表提示或參數。 建立報表提示來限制報表可擷取的資料，或將報表擷取資料設為目標。 報表可以包含多個提示。 請確定該提示名稱是唯一的，且只包含符合 SQL Server 識別碼規則的英數字元。

當執行報表時，提示會要求一個必要參數的值。 報表會根據該參數值擷取報表資料。 例如，**特定電腦的電腦資訊**報表會提示輸入電腦名稱。 Reporting Services 會將指定值傳遞至在該報表 SQL 陳述式中所定義的變數。

### <a name="report-links"></a>報告連結

Configuration Manager 中的報表連結可連結到來源報表，以供輕鬆存取其他資料。 例如，其可連結至來源報表中每個項目的詳細資訊。 如果目的地報告需要執行一個或多個提示，則來源報告必須包含具有各提示適用之值的資料欄。

連結必須指定具有提示值的資料行編號。 例如：

- 某份報表列出站台最近探索到的電腦。
- 從該報表連結到另一份報表，該報表列出站台針對特定電腦所收到的最新訊息。
- 建立連結，並指定來源報表中 `2` 資料行必須包含電腦名稱。 此值為目的地報表的必要提示。
- 執行來源報表，接著各個資料列左方會顯示連結圖示。
- 選取某一列的圖示，報表檢視器會將該列指定資料行中值作為目的地報告的提示值來傳遞。

只能為報表設定一個連結，且該連結只能連接到單一目的地報表。

> [!WARNING]  
> 如果您將目的地報告移動至不同的報告資料夾，則目的地報告的位置會因而變更。 Configuration Manager 不會自動更新來源報表中的報表連結位置，且來源報表中的連結將會失去作用。

## <a name="report-folders"></a>報告資料夾

報表資料夾可協助排序與篩選 Configuration Manager 儲存在 Reporting Services 中的報表。 當有許多報表需要管理時，報表資料夾特別管用。 當安裝 Reporting Services 點時，報表資料夾會將報表複製到 Reporting Services，並將報表整理為 50 個以上的報表資料夾。 報告資料夾是唯讀的。 無法在 Configuration Manager 主控台中修改報表資料夾。

## <a name="report-subscriptions"></a>報告訂閱

Reporting Services 的報表訂閱是一種週期性要求，會在特定時間或特定事件發生後傳遞報表。 可在訂閱中指定應用程式檔案格式。 訂閱可提供您隨選執行報告的替代方式。 使用隨選報告需要主動在每次想要撿視報告時選取報告。 相較之下，訂閱則可以用於排程，並自動傳遞報告。

您可以在 Configuration Manager 主控台中管理報告訂閱。 報表伺服器會處理訂閱， 透過部署在伺服器上的傳遞延伸模組來發佈。 根據預設，您可以建立的訂閱可將報告傳送至共用資料夾或電子郵件地址。

如需詳細資訊，請參閱[管理報表訂閱](operations-and-maintenance-for-reporting.md#bkmk_subscription)。

## <a name="report-builder"></a>報表產生器

對於以 Reporting Services 為基礎的報表，Configuration Manager 會將 Microsoft SQL Server 報表產生器作為專用的撰寫與編輯工具來同時處理模型式與 SQL 式報表。 當在 Configuration Manager 主控台建立或編輯報表時，會開啟報表產生器。 當初次建立或修改報表時，會自動安裝報表產生器。 當您執行或編輯報告時，會開啟與已安裝之 SQL Server 版本關聯的報表產生器版本。  

 報表產生器安裝可新增超過 20 種語言的支援。 當執行報表產生器時，資料會以本機電腦 OS 所使用的語言顯示。 如果報表產生器不支援該語言，則資料會以英文顯示。 報表產生器支援 SQL Server Reporting Services 的完整功能，其包括下列功能：

- 提供外觀類似 Microsoft Office 的直覺化報告撰寫環境。  

- 提供 SQL Server 報表定義語言 (RDL) 的彈性化報表版面配置。  

- 提供包括圖表和量表在內的各種資料虛擬化格式。  

- 提供格式豐富的文字方塊。  

- 匯出為 Microsoft Word 格式。  

您也可以直接從 SQL Server Reporting Services 開啟報表產生器。

## <a name="report-models-in-sql-server-reporting-services"></a>SQL Server Reporting Services 中的報告模型

SQL Reporting Services 會使用報表模型以協助從 Configuration Manager 資料庫中選取要包含在模型式報表中的項目。 當建置報表時，報表模型只會顯示可供選擇的指定檢視和項目。 若要建立模型式報告，至少必須有一個可用的報告模型。

報告模型具有下列功能：

- 為資料庫欄位與檢視提供邏輯商務名稱。 您不需要了解 Configuration Manager 資料庫結構就能產生報表。

- 有邏輯地為項目分組。  

- 定義項目之間的關聯性。  

- 保護模型元素，使系統管理使用者只能查看權限內的資料。

即使 Configuration Manager 提供範例報告模型，您也可以自行定義報告模型，以符合商務需求。 如需如何建立報表模型的詳細資訊，請參閱[建立自訂報表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。

## <a name="next-steps"></a>後續步驟

[規劃報告](planning-for-reporting.md)
