---
title: 報告作業和維護
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中管理報告及報告訂閱的詳細資料。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694416"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Configuration Manager 中的報表作業和維護

適用於：  Configuration Manager (最新分支)

Configuration Manager 中用於報告的基礎結構就緒後，您通常會執行一些作業來管理報告及報告訂用帳戶。

> [!NOTE]
> 此文章著重於 SQL Server Reporting Services 中的報告。 從 2002 版開始，您可以將報告與 Power BI 報表伺服器整合。 如需詳細資訊，請參閱[與 Power BI 報表伺服器整合](powerbi-report-server.md)。

## <a name="run-a-report-from-reporting-services"></a>從 Reporting Services 執行報告

Configuration Manager 會將其報告儲存在 SQL Server Reporting Services 中。 報告會從 Configuration Manager 站台資料庫中擷取資料。 您可以在 Configuration Manager 主控台中存取報告，也可以使用報表管理員透過網頁瀏覽器來存取報告。 在任何可存取 Reporting Services 點而且使用者有足夠的權限可檢視報告的電腦上，從網頁瀏覽器開啟報告。 若要執行報告，您必須具有 [站台]  權限的 [讀取]  權限，以及特定物件的 [執行報告]  權限。

當您執行報告時，報告標題、描述與類別會以本機 OS 的語言顯示。 如需詳細資訊，請參閱[報告的語言](configuring-reporting.md#-languages-for-reports)。

> [!NOTE]  
> 報表管理員是一種 Web 型報表存取及管理工具。 您可以使用其透過 HTTPS 連線管理單一報表伺服器執行個體。 使用報表管理員進行操作工作：檢視報告、修改報告內容，以及管理相關聯的報告訂用帳戶。 此文章提供在報表管理員中檢視報告及修改報告屬性的步驟。 如需報表管理員中其他選項的詳細資訊，請參閱[什麼是報表管理員？](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode) \(部分機器翻譯\)

您可以使用下列程序來執行 Configuration Manager 報表。

### <a name="run-a-report-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中執行報告

1. 在 Configuration Manager 主控台中，按一下 [監視]  工作區。 展開 [報告]  ，然後選取 [報告]  。 此節點會列出可用的報告。

    > [!TIP]
    > 如果此節點未列出任何報告，請確認是否已安裝並設定 Reporting Services 點。 如需詳細資訊，請參閱[設定報告](configuring-reporting.md)。

1. 選取您想要執行的報告。 在功能區的 [常用]  索引標籤上，於 [報告群組]  區段中，選取 [執行]  以開啟報告。

1. 如果有必要的參數，請加以指定，然後選取 [檢視報告]  。

### <a name="run-a-report-in-a-web-browser"></a>在網頁瀏覽器中執行報告

1. 在網頁瀏覽器中，移至報表管理員 URL，例如 `https://Server1/Reports`。 在 Reporting Services Configuration Manager 中的 [報表管理員 URL]  頁面上尋找此位址。

1. 在報表管理員中，選取 Configuration Manager 的報表資料夾，例如 **ConfigMgr_CAS**。

    > [!TIP]
    > 如果報表管理員未列出任何報告，請確認是否已安裝並設定 Reporting Services 點。 如需詳細資訊，請參閱[設定報告](configuring-reporting.md)。

1. 選取您要執行之報告的報告類別，然後選取特定的報告。 報告會在報表管理員中開啟。

1. 如果有必要的參數，請加以指定，然後選取 [檢視報告]  。

## <a name="modify-the-properties-of-a-report"></a>修改報告的屬性

報告屬性包括報告名稱與描述。 您可以在 Configuration Manager 主控台中檢視報告的屬性。

若要變更屬性，請使用報表管理員：

1. 在網頁瀏覽器中，移至報表管理員 URL，例如 `https://Server1/Reports`。

1. 在報表管理員中，選取 Configuration Manager 的報表資料夾，例如 **ConfigMgr_CAS**。

1. 選取報告類別，然後選取特定的報告。 報告會在報表管理員中開啟。

1. 選取 [屬性]  索引標籤。修改報告名稱與描述，然後選取 [套用]  。

報表管理員會將報告屬性儲存在報表伺服器上。 Configuration Manager 主控台會顯示報告的已更新報告屬性。

## <a name="edit-a-report"></a><a name="bkmk_edit"></a> 編輯報告

當現有的 Configuration Manager 報告未擷取您想要的資訊時，請在報表產生器中進行編輯。 您也可以使用報表產生器來變更報告的版面配置或設計。 雖然您可以直接編輯預設報告，但最好是加以複製。 開啟要編輯的報告，然後選取 [另存新檔]  。

若要編輯報告，您需要對報告中的特定物件擁有**網站修改**權限與**修改報告**權限。

> [!IMPORTANT]
> 網站更新將保留內建報告。 若修改標準報告，則站台更新時會使用底線 (`_`) 作為前置詞來重新命名報告。 此行為可確保站台更新不會覆寫標準報告修改的報告。
>
> 如果您修改預先定義的報告，在安裝網站更新之前，請先備份您的自訂報告。 更新之後，請在 Reporting Services 中還原報告。 如果對預先定義的報告進行大幅變更，請改為建立新的報告。 您在升級站台之前建立的新報告不會被覆寫。

利用下列程序編輯 Configuration Manager 報告的內容。

1. 在 Configuration Manager 主控台中，按一下 [監視]  工作區。 展開 [報告]  ，然後選取 [報告]  節點。

1. 選取您要修改的報告。 在功能區的 [常用]  索引標籤上，於 [報表群組]  區段中，選取 [編輯]  。 系統可能會提示您輸入認證。 如果報表產生器未安裝在電腦上，Configuration Manager 會提示您加以安裝。 報表產生器為修改及建立報告時所需。

1. 在報表產生器中，修改適當的報告設定。 選取 [儲存]  將報告儲存至報表伺服器。

## <a name="create-reports"></a>建立報表

您可以建立兩種類型的報告：

- **模型式報告**可讓您以互動方式選取要包含在報告中的項目。 如需建立自訂報表模型的詳細資訊，請參閱[在 SQL Server Reporting Services 中建立 Configuration Manager 的自訂報表模型](creating-custom-report-models-in-sql-server-reporting-services.md)。

- **SQL 式報告**可讓您擷取以報告 SQL 陳述式為基礎的資料。

> [!IMPORTANT]
> 若要建立新報告，您的帳戶必須具有 [網站修改]  權限。 您只能在您具有 [修改報告]  權限的資料夾中建立報告。

### <a name="create-a-model-based-report"></a>建立模型式報告

您可以使用下列程序建立模型式的 Configuration Manager 報告。

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [報告]  ，然後選取 [報告]  節點。

1. 在功能區的 [常用]  索引標籤上，在 [建立]  區段中選取 [建立報表]  。 此動作會開啟 [建立報表精靈]  。

1. 在 [資訊]  頁面上，進行下列設定：

    - **類型**：選取 [模型式報告]  。

    - **名稱**：指定報告的名稱。

    - **描述**：指定報告的描述。

    - **伺服器**：顯示您在其中建立此報表之報表伺服器的名稱。

    - **路徑**：選取 [瀏覽]  以指定您要儲存報表的資料夾。

1. 在 [模式選擇]  頁面上，於清單中選取要用來建立此報告的可用模型。 [預覽]  區段會顯示此報表模型中可用的 SQL Server 檢視與實體。

1. 完成建立報表精靈。

1. 開啟報表產生器以設定報表設定。 如需詳細資訊，請參閱[編輯 Configuration Manager 報表](#bkmk_edit)。

1. 在報表產生器建立報表配置、 選取可用的 SQL Server 檢視中的資料、 將參數加入至報表等等。

1. 選取 [執行]  以執行您的報表。 確認報告提供您預期的資訊。 如有需要，請選取 [設計]  進一步修改報表。

1. 選取 [儲存]  將報告儲存至報表伺服器。

### <a name="create-a-sql-based-report"></a>建立 SQL 式報告

當您為自訂報告建立 SQL 陳述式時，請不要直接參照 SQL Server 資料表。 請一律參考來自網站資料庫的支援報告 SQL Server 檢視。 這些檢視的名稱開頭為 `v_`。 如需詳細資訊，請參閱[在 Configuration Manager 中使用 SQL Server 檢視建立自訂報告](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md)。

您也可以參考來自網站資料庫的公用預存程序。 這些預存程序的名稱開頭為 `sp_`。

您可以使用下列程序建立 SQL 式的 Configuration Manager 報告。

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [報告]  ，然後選取 [報告]  節點。

1. 在功能區的 [常用]  索引標籤上，在 [建立]  區段中選取 [建立報表]  。 此動作會開啟 [建立報表精靈]  。

1. 在 [資訊]  頁面上，進行下列設定：

    - **類型**：選取 [SQL 式報告]  。

    - **名稱**：指定報告的名稱。

    - **描述**：指定報告的描述。

    - **伺服器**：顯示您在其中建立此報表之報表伺服器的名稱。

    - **路徑**：選取 [瀏覽]  以指定您要儲存報表的資料夾。

1. 完成建立報表精靈。

1. 開啟報表產生器以設定報表設定。 如需詳細資訊，請參閱[編輯 Configuration Manager 報表](#bkmk_edit)。

1. 在報表產生器中，提供報告的 SQL 陳述式。 您還可以透過在可用檢視中使用資料行來建置 SQL 陳述式。 如有需要，請將參數加入報告。

1. 選取 [執行]  以執行您的報表。 確認報告提供您預期的資訊。 如有需要，請選取 [設計]  進一步修改報表。

1. 選取 [儲存]  將報告儲存至報表伺服器。

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a> 管理報告訂閱

SQL Server Reporting Services 中的報告訂閱可讓您設定以電子郵件自動傳遞指定的報告，或依排程的間隔傳遞至檔案共用。 若要設定報告訂用帳戶，請使用 Configuration Manager 中的 [建立訂閱精靈]  。

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>建立報告訂閱以將報告傳遞到檔案共用

當您建立報告訂用帳戶將報告傳遞至檔案共用時，Reporting Services 會以指定的格式將報告複製到您指定的檔案共用。 您一次只能訂閱和要求傳遞一份報告。

當您建立使用檔案共用的訂用帳戶時，請指定現有資料夾作為目的地資料夾。 報表伺服器不會建立資料夾或網路共用。 您在訂用帳戶中指定目的地資料夾時，請使用 UNC 路徑，而且不要包含資料夾路徑中的結尾反斜線 (`\`)。 下列範例是目的地資料夾的有效 UNC 路徑：`\\server\reportfiles\operations\2001`。

> [!NOTE]
> 當您建立訂用帳戶時，您可以指定使用者名稱與密碼。 此帳戶需要此共用的存取權，而且必須有目的地資料夾的**寫入**權限。

Reporting Services 可以採用不同的檔案格式轉譯報告。 例如，MHTML 或 Excel。 當您建立訂用帳戶時，請選取格式。 雖然您可以選取任何支援的轉譯格式，但是有些格式在轉譯為檔案時，會比其他格式效果更好。

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>對檔案共用報告訂用帳戶的限制

下列清單包含對檔案共用報告訂用帳戶的限制：

- 不同於您在報表伺服器上裝載和管理的報告，Reporting Services 會將報告作為靜態檔案傳遞至共用資料夾。

- 報告的互動式功能不適用於儲存為檔案的報告。 此報告會將任何互動式功能表示為靜態元素。

- 如果報告包含圖表，則其會使用預設呈現方式。

- 如果報告連結至另一個報告，則其會將該連結轉譯為靜態文字。

如果您要在傳遞的報告中保留互動功能，請使用電子郵件傳遞。 如需詳細資訊，請參閱[建立報告訂用帳戶以使用電子郵件傳遞報告](#bkmk_subscription-email)。

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>建立檔案共用之報告訂用帳戶的程序

利用下列程序建立報告訂閱將報告傳遞至檔案共用。  

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [報告]  ，然後選取 [報告]  節點。

1. 選取報表資料夾，然後選取您要訂閱的報表。 在功能區的 [常用]  索引標籤上，於 [報表群組]  區段中，選取 [建立訂閱]  。 此動作會開啟**建立訂閱精靈**。

1. 在 [訂閱傳遞]  頁面上，進行下列設定：  

    - **報告傳遞者**：選取 [Windows 檔案共用]  。

    - **檔案名稱**：指定報告的檔案名稱。 根據預設，報告檔案不會包含副檔名。 選取 [建立時新增副檔名]  ，根據格式自動新增副檔名。

    - **路徑**：指定您要傳遞此報告的目標現有資料夾的 UNC 路徑。 例如 `\\server\reportfiles\operations`。

    - **轉譯格式**：為報告檔案選取下列其中一種格式：

      - **包含報表資料的 XML 檔案**
      - **CSV (逗號分隔)**
      - **TIFF 檔案**
      - **Acrobat (PDF) 檔案**
      - **HTML 4.0**
        > [!NOTE]
        > 如果您的報告有影像，則 HTML 4.0 格式將不會包含那些影像。
      - **MHTML (網頁封存)**
      - **RPL 轉譯器** (報告頁面配置)
      - **Excel**
      - **Word**

    - **使用者名稱**：將具有*寫入*權限的 Windows 使用者帳戶，指定給指定的**路徑**。

    - **密碼**：指定上述 Windows 使用者帳戶的密碼。

    - **覆寫選項**：選取下列其中一個選項，設定目的地資料夾中存在相同名稱的檔案時的行為：

      - **使用較新版本覆寫現有的檔案**
      - **不覆寫現有的檔案**
      - **新增較新版本時，遞增檔案名稱**：此選項會在新報告的檔案名稱後面附加一個數字，以便與舊版進行區別。

    - **描述**：(選擇性) 指定此報告訂用帳戶的其他相關資訊。

1. 在 [訂閱排程]  頁面上，為報告訂閱選取下列其中一個傳遞排程選項：

    - **使用共用排程**：共用排程是之前定義的排程，可供其他報告訂閱使用。 當您選取此選項時，也請選取共用排程。 如果沒有共用排程，請選取選項來建立新的排程。

    - **建立新排程**：設定此報表執行的排程。 排程包括此訂用帳戶的間隔、開始時間與日期，以及結束日期。 根據預設，新的訂用帳戶會建立新的排程，從目前的日期和時間開始，每小時執行一次。

1. 在 [訂閱參數]  頁面上，指定自動執行此報告時所需的任何參數。 如果報表沒有參數，則精靈不會顯示此頁面。

1. 完成精靈。

1. 確認 Configuration Manager 已成功建立報告訂用帳戶。 選取 [訂用帳戶]  節點以檢視及修改報告訂用帳戶。

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a> 建立報告訂閱以使用電子郵件傳遞報告

當您建立報告訂用帳戶以透過電子郵件傳遞報告時，Reporting Services 將向您設定的收件者傳送電子郵件。 此電子郵件包含以附件形式提供的報告。 報表伺服器不會驗證電子郵件地址，或是從電子郵件伺服器取得電子郵件地址。 您可以用電子郵件將報告寄給組織內外任何有效的電子郵件帳戶。

> [!NOTE]
> 若要啟用 [電子郵件訂閱]  選項，您需要在 Reporting Services 中設定電子郵件設定。 如需詳細資訊，請參閱 [Reporting Services 中的電子郵件傳遞](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services)。

您可以選取下列其中一個電子郵件傳遞選項，或兩個都選取：

- 傳送通知，其中包含所產生報告的連結。

- 傳送內嵌或附加的報告。 轉譯格式與瀏覽器會決定是內嵌或附加報告。

  - 如果您的瀏覽器支援 HTML 4.0 與 MHTML，而且您選取 [MHTML (網頁封存)]  格式，則電子郵件會將報告內嵌為郵件的一部分。
  - 所有其他格式都會以附件形式傳遞報告。
  - Reporting Services 不會在傳送報告之前檢查附件或郵件的大小。 如果附件或訊息超過電子郵件伺服器允許的上限，就不會傳遞報告。

利用下列程序建立報告訂閱使用電子郵件傳遞報告。  

1. 在 Configuration Manager 主控台中，移至 [監視]  工作區、展開 [報告]  ，然後選取 [報告]  節點。

1. 選取報表資料夾，然後選取您要訂閱的報表。 在功能區的 [常用]  索引標籤上，於 [報表群組]  區段中，選取 [建立訂閱]  。 此動作會開啟**建立訂閱精靈**。

1. 在 [訂閱傳遞]  頁面上，進行下列設定：  

    - **報告傳遞者**：選取 [電子郵件]  。

    - **收件者**：請指定有效的電子郵件地址作為收件者。

        > [!NOTE]
        > 若要輸入多個收件者，請以分號 (`;`) 分隔每個電子郵件地址。

    - **副本**：選擇性地指定要接收此報告副本的電子郵件地址。

    - **密件副本**：選擇性地指定要接收此報告之密件副本的電子郵件地址。

    - **回覆**：指定回覆地址。 如果收件者回覆電子郵件訊息，則回覆會寄送至此地址。

    - **主旨**：指定訂閱電子郵件地址的主旨列。

    - **優先順序**：選取此電子郵件訊息的優先順序旗標：**低**、**正常**或**高**。 Microsoft Exchange 會使用此旗標來指出電子郵件訊息的重要性。

    - **註解**：指定訂閱電子郵件訊息本文的文字。

    - **描述**：(選擇性) 指定此報告訂用帳戶的其他相關資訊。

    - **包含連結**：在電子郵件訊息的本文中包含此報告的 URL。

    - **包含報告**：將報告附加至電子郵件訊息。 使用 [轉譯格式]  選項來指定要附加的報告格式。

    - **轉譯格式**：為附加的報告檔案選取下列其中一種格式：

      - **包含報表資料的 XML 檔案**
      - **CSV (逗號分隔)**
      - **TIFF 檔案**
      - **Acrobat (PDF) 檔案**
      - **MHTML (網頁封存)**
      - **Excel**
      - **Word**

1. 在 [訂閱排程]  頁面上，為報告訂閱選取下列其中一個傳遞排程選項：

    - **使用共用排程**：共用排程是之前定義的排程，可供其他報告訂閱使用。 當您選取此選項時，也請選取共用排程。 如果沒有共用排程，請選取選項來建立新的排程。

    - **建立新排程**：設定此報表執行的排程。 排程包括此訂用帳戶的間隔、開始時間與日期，以及結束日期。 根據預設，新的訂用帳戶會建立新的排程，從目前的日期和時間開始，每小時執行一次。

1. 在 [訂閱參數]  頁面上，指定自動執行此報告時所需的任何參數。 如果報表沒有參數，則精靈不會顯示此頁面。

1. 完成精靈。

1. 確認 Configuration Manager 已成功建立報告訂用帳戶。 選取 [訂用帳戶]  節點以檢視及修改報告訂用帳戶。
