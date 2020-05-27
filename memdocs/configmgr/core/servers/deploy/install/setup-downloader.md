---
title: 安裝程式下載程式工具
titleSuffix: Configuration Manager
description: 使用獨立工具來下載安裝程式的最新版本金鑰安裝檔案。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428841"
---
# <a name="setup-downloader-for-configuration-manager"></a>Configuration Manager 的安裝程式下載程式

適用於：Configuration Manager (最新分支)

執行 Configuration Manager 安裝程式來安裝或升級站台之前，您可使用安裝程式下載程式獨立工具來下載更新的安裝程式檔案。 從您想要安裝的 Configuration Manager 版本執行工具。 使用更新的安裝程式檔案，以確保站台安裝會使用最新版本的金鑰安裝檔案。

當使用安裝程式下載程式時，您會指定要包含檔案的資料夾。 您用來執行工具的帳戶必須具有下載資料夾的 [完全控制] 權限。 在執行安裝程式來安裝或升級站台時，您可指定先前所下載檔案的本機複本。 此行為可在開始安裝或升級站台時，防止安裝程式連線至 Microsoft。 您可使用相同安裝程式檔案本機複本來用於其他相同版本的站台安裝或升級作業。

安裝程式下載程式工具會下載下列類型的檔案：

- 所需的必要條件可轉散發檔案
- 語言套件
- 安裝程式的最新產品更新

您有兩個選項可執行安裝程式下載程式：

- 使用使用者介面來執行應用程式
- 在命令提示字元中執行應用程式，以取得其他命令列選項

如果組織禁止使用防火牆或 Proxy 裝置來與網際網路進行網路通訊，則需要允許工具存取網際網路端點。 您要用來執行此工具的裝置需要具有與服務連線點同等網際網路存取權。 如需詳細資訊，請參閱[網際網路存取需求](../../../plan-design/network/internet-endpoints.md#bkmk_scp)。<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a> 以使用者介面來執行安裝程式下載程式

1. 在可存取網際網路的電腦上，瀏覽至您所要安裝 Configuration Manager 版本的安裝媒體。

1. 在 **SMSSETUP\BIN\X64** 子資料夾中，執行 **Setupdl.exe**。

1. 指定要儲存更新安裝檔案的資料夾路徑，然後選取 [下載]。 安裝程式下載程式會驗證目前在下載資料夾中的檔案。 它只會下載遺漏的檔案，或是比現有檔案還要新的檔案。 安裝程式下載程式會針對下載的語言建立子資料夾以及其他必要元件。

1. 若要查看下載結果，請參閱 **C:\ConfigMgrSetup.log**。

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a> 從命令提示字元中執行安裝程式下載程式

1. 開啟命令提示字元，並將目錄變更為所要安裝 Configuration Manager 版本的安裝媒體。

1. 將目錄變更為 **SMSSETUP\BIN\X64** 子資料夾，並使用必要的選項執行 **Setupdl.exe**。

1. 若要查看下載結果，請參閱 **C:\ConfigMgrSetup.log**。

### <a name="command-line-options"></a>命令列選項

您可以搭配使用下列命令列選項與 **Setupdl.exe**：

- **/VERIFY**：驗證下載資料夾中的檔案，包括語言檔案。 如需過期檔案的清單，請參閱 **C:\ConfigMgrSetup.log**。 當使用此選項時，系統便不會下載任何檔案。

- **/VERIFYLANG**：僅驗證下載資料夾中的語言檔案。 如需過期語言檔案的清單，請參閱 **C:\ConfigMgrSetup.log**。

- **/LANG**：僅下載語言檔案至下載資料夾。

- **/NOUI**：不使用使用者介面來啟動安裝程式下載程式。 當使用此選項時，需要**下載路徑**。

- **下載路徑**：若要自動啟動驗證或下載程序，請指定下載資料夾的路徑。 當使用 **/NOUI** 選項時，需要下載路徑。 如果未指定下載路徑，則安裝程式下載程式會提示要指定路徑。 如果資料夾不存在，則安裝程式下載程式會建立資料夾。

### <a name="example-commands"></a>範例命令

#### <a name="example-1"></a>範例 1

安裝程式下載程式會驗證指定下載資料夾中的檔案，然後下載檔案。

`setupdl.exe C:\Download`

#### <a name="example-2"></a>範例 2

安裝程式下載程式僅會驗證指定下載資料夾中的檔案。

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>範例 3

安裝程式下載程式會驗證指定下載資料夾中的檔案，然後下載檔案。 此工具不會顯示任何使用者介面。

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>範例 4

安裝程式下載程式會驗證指定下載資料夾中的語言檔案，然後僅下載語言檔案。

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a> 將安裝程式下載程式檔案複製到另一部電腦

1. 在 Windows 檔案總管中，前往下列其中一個位置：

    - **&lt;Configuration Manager 安裝媒體>\SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager 安裝路徑>\BIN\X64**

1. 將下列檔案複製到另一部電腦的相同目的地資料夾：

    - **setupdl.exe**

    - **.\\&lt;語言>\\setupdlres.dll**

        > [!NOTE]
        > 此檔案位於安裝語言的子資料夾中。 例如，英文是在 `00000409` 子資料夾中。

    裝置上的目的地資料夾應該會類似下列範例：

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. 從目的地電腦執行安裝程式下載程式。 請使用[使用者介面](#bkmk_ui)或[命令提示字元](#bkmk_cmd)。
