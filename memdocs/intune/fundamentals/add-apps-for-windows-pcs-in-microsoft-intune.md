---
title: 為執行 Intune 軟體用戶端的 Windows 電腦新增應用程式
titleSuffix: Microsoft Intune
description: 使用本主題的資訊，了解如何在部署之前，將適用於 Windows 電腦的應用程式新增至 Intune。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 08/29/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: bc8c8be9-7f4f-4891-9224-55fc40703f0b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: a2c5590acd870e2623491052ba43bf29e4676568
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79344359"
---
# <a name="add-apps-for-windows-pcs-that-run-the-intune-software-client"></a>為執行 Intune 軟體用戶端的 Windows 電腦新增應用程式

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

使用本主題的資訊，了解如何在部署之前，將應用程式新增至 Intune。

> [!IMPORTANT]
> 本主題中的資訊可協助您為使用 Intune 軟體用戶端管理的 Windows 電腦新增應用程式。 如果您想要為已註冊的 Windows 電腦及其他行動裝置新增應用程式，請參閱[將應用程式新增至 Microsoft Intune](../apps/apps-add.md)。

若要將應用程式安裝到電腦，它們必須可以透過無訊息模式安裝，而不需要使用者互動。 如果不是這種情況，則安裝會失敗。

## <a name="additional-security-settings-for-windows-installer"></a>Windows Installer 的其他安全性設定
您可以允許使用者控制應用程式安裝。 如啟用，則可讓以安全性違規方式停止的安裝繼續執行。 您可以指示 Windows Installer 在系統上安裝任何程式時使用提升的權限。 此外，您可以將 Windows 資訊保護 (WIP) 項目編入索引，並將跟其有關的中繼資料儲存在未加密的位置。 停用此原則時，不會編製 WIP 保護項目的索引，且不會出現在 Cortana 或檔案總管的結果中。 預設會停用這些選項的功能。 

## <a name="add-the-app"></a>新增應用程式
您將使用 Intune 軟體發行者設定應用程式的內容，並使用下列程序，將應用程式上傳至您的雲端儲存空間：

1. 在 [Microsoft Intune 系統管理員主控台](https://manage.microsoft.com)中，選擇 [應用程式]  &gt; [新增應用程式]  ，以啟動 Intune 軟體發佈工具。

   > [!TIP]
   > 您可能需要輸入 Intune 使用者名稱和密碼，才能啟動發行者。

2. 在發行者的 [軟體安裝程式]  頁面上，於 [選取將此軟體開放給裝置使用的方式]  下，選擇 [軟體安裝程式]  ，然後指定：

   - [選取軟體安裝程式檔案類型]  。 這會指出您要部署的軟體類型。 針對 Windows 電腦，請選擇 **[Windows Installer]** 。
   - [指定軟體安裝檔的位置]  。 輸入安裝檔的位置，或選擇 [瀏覽]  以從清單中選取位置。
   - [包含同一個資料夾的其他檔案和子資料夾]  。 某些使用 Windows Installer 的軟體會需要支援檔案。 這些必須位於安裝檔所在的相同資料夾中。 如果您也想要部署這些支援檔案，請選取這個選項。

   例如，如果想要將應用程式命名的 Application.msi 發行到 intune，頁面將如下所示︰![發佈工具的 [軟體設定] 頁面](./media/add-apps-for-windows-pcs-in-microsoft-intune/publisher-for-pc.png)

   這個安裝類型會佔用部分雲端儲存空間。

3. 在 [軟體描述]  頁面上，設定下列項目。

   > [!NOTE]
   > 根據您使用的安裝程式檔案，其中有些值可能已自動輸入，或可能不會出現。

   - **發行者**。 輸入應用程式發行者的名稱。
   - **名稱**。 輸入要顯示在公司入口網站中的應用程式名稱。<br />確定您使用的所有應用程式名稱都是唯一的。 如果有重複的應用程式名稱，使用者只會在公司入口網站中看到其中一個應用程式。
   - **描述**。 輸入應用程式的描述。 使用者會在公司入口網站中看到這個描述。
   - **軟體資訊的 URL** (選用)。 輸入包含此應用程式相關資訊的網站 URL。 使用者會在公司入口網站中看到這個 URL。
   - **隱私權 URL** (選用)。 輸入包含此應用程式隱私權資訊的網站 URL。 使用者會在公司入口網站中看到這個 URL。
   - **類別** (選用)。 選取其中一個內建應用程式類別。 這可以讓使用者在瀏覽公司入口網站時，更輕鬆地找到應用程式。
   - **圖示** (選用)。 上傳要與應用程式相關聯的圖示。 這是使用者瀏覽公司入口網站時，會隨應用程式一起顯示的圖示。

4. 在 [需求]  頁面上，選取必須符合才能安裝應用程式的需求。 從下列選項進行選擇：

   - **架構**。 選取這個應用程式可以安裝在 32 位元或 64 位元作業系統上，還是兩個作業系統都可以。
   - **作業系統**。 選取可以安裝這個應用程式的最低作業系統。

5. 在 [偵測規則]  頁面上，您可以設定規則以偵測您正在設定的應用程式是否已安裝於電腦上。 或者，您可以使用預設的偵測規則以自動覆寫任何之前已經安裝的應用程式版本。 這個選項適用於 Windows Installer (僅限 .exe 檔)。

   您可以設定的規則包括：
   - **檔案已存在**。 指定所要偵測檔案的路徑。 您可以搜尋下列位置：電腦上的 **%ProgramFiles%** 下 (這將會搜尋 **Program Files**\&lt;path&gt; 和 **Program Files (x86)** \&lt;path&gt;)，或是 **%SystemDrive%** 下 (這將會從電腦的根磁碟機進行搜尋，通常是 C:)。
   - **MSI 產品代碼已存在**。 選擇 [瀏覽]  以選擇您要偵測的 Windows Installer (.msi) 檔案。
   - <strong>登錄機碼已存在</strong>。 指定以 <strong>HKEY_LOCAL_MACHINE\</strong> 開頭的登錄機碼。 系統會搜尋 32 位元和 64 位元登錄路徑。 如果任一位置已有您指定的機碼，便會符合偵測規則。

   如果應用程式符合任何已設定的規則，則不會進行安裝。

6. 僅限 **Windows Installer** 檔案類型 (.msi 和 .exe)：在 [命令列引數]  頁面上，選擇是否想為安裝程式提供選擇性的命令列引數。
   Intune 會自動新增下列參數︰
   - 針對 .exe 檔案，會新增 **/install**。
   - 針對 .msi 檔案，會新增 **/quiet**。
   請注意，只有在應用程式套件建立者啟用此項目的功能時，這些選項才會運作。

7. 僅限 **Windows Installer** 檔案類型 (僅限 .exe)：您可以在 [傳回碼]  頁面上，新增應用程式在受控 Windows 電腦上進行安裝時，供 Intune 解譯的新錯誤碼。

   根據預設，Intune 會使用業界標準的傳回碼來回報應用程式套件安裝失敗或成功：**0** (成功) 或 **3010** (成功但需要重新啟動)。 您也可以將自己的傳回碼新增至這份清單。 如果您指定了傳回碼清單，但應用程式安裝傳回不在清單中的代碼，則會解譯為失敗。

8. 在 [摘要]  頁面上，檢閱您指定的資訊。 當您準備好時，選擇 [上傳]  。

9. 選擇 [關閉]  來完成。

應用程式會顯示在 [應用程式]  工作區的 [應用程式]  節點上。

## <a name="next-steps"></a>後續步驟

完成建立應用程式後，下一個步驟是進行部署。 如需詳細資訊，請參閱[使用 Microsoft Intune 將應用程式指派給群組](../apps/apps-deploy.md)。

如果想要閱讀將軟體部署至 Windows 電腦的祕訣和技巧詳細資訊，請參閱部落格文章：[支援祕訣：將 Intune 軟體發佈到電腦的最佳做法](https://support.microsoft.com/en-US/help/2583929)。
