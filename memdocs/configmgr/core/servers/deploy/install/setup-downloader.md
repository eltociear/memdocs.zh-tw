---
title: 安裝程式下載程式
titleSuffix: Configuration Manager
description: 請閱讀這個獨立應用程式，設計成確保您的站台安裝使用最新版本的金鑰安裝檔案。
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700566"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager 的安裝程式下載程式

適用於：  Configuration Manager (最新分支)

執行安裝程式來安裝或升級 Configuration Manager 站台之前，您可以使用您想要安裝之 Configuration Manager 版本中的安裝程式下載程式獨立應用程式來下載已更新的安裝程式檔案。  

使用更新的安裝程式檔案，便能確保您的站台安裝會使用最新版本的金鑰安裝檔案。 概觀而言︰   
-   如果您在啟動安裝程式前使用安裝程式下載程式來下載檔案，請指定要包含檔案的資料夾。  
-   您用來執行安裝程式下載程式的帳戶必須具有下載資料夾的**完全控制**權限。  
-   在您執行安裝程式來安裝或升級站台時，可以加以指引，讓其使用您先前所下載檔案的這份本機複本。 如此一來，在您開始安裝或升級站台時，安裝程式便不需連線至 Microsoft。  
-   您可以使用相同的安裝程式檔案本機複本，用於後續的站台安裝或升級作業。  

下列類型的檔案是透過安裝程式下載程式所下載：  
-   所需的必要條件可轉散發檔案  
-   語言套件  
-   安裝程式的最新產品更新  

您有兩個選項可以執行安裝程式下載程式：
- 使用使用者介面來執行應用程式
- 針對命令列選項，在命令提示字元執行應用程式


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> 利用使用者介面來執行安裝程式下載程式  

1.  在可存取網際網路的電腦上，開啟 Windows 檔案總管，並移至 &lt;Configuration Manager 安裝媒體\>\SMSSETUP\BIN\X64。   

2.  若要開啟安裝程式下載程式，請按兩下 **Setupdl.exe**。   

3. 指定要裝載更新的安裝檔案的資料夾路徑，然後按一下 [下載]  。 安裝程式下載程式會驗證目前在下載資料夾中的檔案。 它只會下載遺漏的檔案，或是比現有檔案還要新的檔案。 安裝程式下載程式會針對下載的語言建立子資料夾以及其他必要子資料夾。  

4.  若要檢閱下載結果，請在磁碟機 C 的根目錄中開啟 **ConfigMgrSetup.log** 檔案。  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> 從命令提示字元中執行安裝程式下載程式  

1.  在命令提示字元視窗中，移至 **&lt;*Configuration Manager 安裝媒體*\>\SMSSETUP\BIN\X64**。   

2.  若要開啟安裝程式下載程式，請執行 **Setupdl.exe**。

    您可以搭配使用下列命令列選項與 **Setupdl.exe**：   

    -   **/VERIFY**：使用此選項可驗證下載資料夾中的檔案，包括語言檔案。 在磁碟機 C 的根目錄中，檢閱 ConfigMgrSetup.log 檔案中列出的過期檔案。 如果您使用此選項，則不會下載任何檔案。  

    -   **/VERIFYLANG**：使用此選項可驗證下載資料夾中的語言檔案。 在磁碟機 C 的根目錄中，檢閱 ConfigMgrSetup.log 檔案中列出的過期語言檔案。

    -   **/LANG**：使用此選項只會將語言檔案下載至下載資料夾。  

    -   **/NOUI**：使用此選項可啟動「安裝程式下載程式」，但不顯示使用者介面。 使用此選項時，您必須在命令提示字元將**下載路徑**指定為命令的一部分。  

    -   **&lt;DownloadPath\>** ：您可以指定下載資料夾的路徑，以自動啟動驗證或下載程序。 使用 **/NOUI** 選項時，必須指定下載路徑。 如果您未指定下載路徑，則必須在安裝程式下載程式開啟時指定路徑。 如果資料夾不存在，則安裝程式下載程式會建立資料夾。  

    範例命令：

    -   **setupdl &lt;下載路徑\>**  

        -   安裝程式下載程式會啟動，並驗證指定下載資料夾中的檔案，然後只下載遺漏的檔案或是比現有檔案版本還要新的檔案。     

    -   **setupdl /VERIFY &lt;下載路徑\>**  

        -   安裝程式下載程式會啟動並驗證指定下載資料夾中的檔案。  

    -   **setupdl /NOUI &lt;下載路徑\>**  

        -   安裝程式下載程式會啟動，並驗證指定下載資料夾中的檔案，然後只下載遺漏的檔案或是比現有檔案還要新的檔案。  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   安裝程式下載程式會啟動，並驗證指定下載資料夾中的語言檔案，然後只下載遺漏的語言檔案或是比現有檔案還要新的語言檔案。  

    -   **setupdl /VERIFY**  

        -   啟動安裝程式下載程式，然後您必須指定下載資料夾的路徑。 接下來，在您按一下 [驗證]  之後，安裝程式下載程式會驗證下載資料夾中的檔案。  

3.  若要檢閱下載結果，請在磁碟機 C 的根目錄中開啟 **ConfigMgrSetup.log** 檔案。

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> 將安裝程式下載程式檔案複製到另一部電腦

1. 在 Windows 檔案總管中，前往下列其中一個位置：

    - **&lt;Configuration Manager 安裝媒體>\SMSSETUP\BIN\X64**
    - **&lt;Configuration Manager 安裝路徑>\BIN\X64**
    
1. 將下列檔案複製到另一部電腦的相同目的地資料夾：
    
    - **setupdl.exe**
    - **.\\&lt;語言>\\setupdlres.dll**
      - 此檔案位於安裝語言的子資料夾中。 例如，英文是在 `00000409` 子資料夾中。

    例如，裝置上的目的地資料夾看起來應該像這樣：
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. 利用[使用者介面](#bkmk_ui)或[命令提示字元](#bkmk_cmd)，從電腦啟動安裝程式下載程式 (如以上各節所述)。
