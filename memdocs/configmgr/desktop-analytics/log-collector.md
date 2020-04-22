---
title: 記錄收集器
titleSuffix: Configuration Manager
description: 使用記錄收集器工具協助針對電腦分析進行疑難排解
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701716"
---
# <a name="desktop-analytics-log-collector"></a>電腦分析記錄收集器

自 Configuration Manager 1906 版開始，使用 Configuration Manager 安裝目錄中的 **DesktopAnalyticsLogsCollector.ps1** 工具，以協助針對電腦分析裝置註冊的問題進行疑難排解。 它會執行一些基本的疑難排解步驟，並將相關記錄收集到單一工作目錄中。 您可以與 Microsoft 支援服務共用此內容。


## <a name="prerequisites"></a>先決條件

- 執行 Windows 10、Windows 8.1 或 Windows 7 (含 Service Pack 1) 的電腦分析用戶端

- 以系統管理使用者身分在裝置上執行指令碼，並 [以系統管理員身分執行]  。

    > [!Tip]
    > 您可以使用 Configuration Manager 的**指令碼**功能搭配此工具。 如需詳細資訊，請參閱[範例 5：透過 Configuration Manager **指令碼**部署指令碼](#bkmk_ex5)。

- Windows 7 (含 Service Pack 1)、PowerShell 4.0 版或更新版本
    - [.NET Framework 4.6 版或更新版本](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [4.0 版](https://support.microsoft.com/help/2819745) (aka.ms/wmf4download) 或 [5.1 版](https://www.microsoft.com/download/details.aspx?id=54616) (aka.ms/wmf5download)

## <a name="usage"></a>使用方式

從 Configuration Manager 安裝內容取得指令碼：`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>參數

### `-LogPath`

指定放置記錄檔和其他輸出檔案的本機或 UNC 路徑。

**值**：

- 本機路徑 (長度上限 = 130)，例如：`c:\myfolder`

- UNC 路徑 (長度上限 = 130)，例如：`\\myserver\myfolder`

**類型**：字串

**位置**：1

**預設值**：`$Env:SystemDrive\M365AnalyticsLogs` (當此參數為 null、空值或空白字元時，指令碼會在系統磁碟機下建立 M365AnalyticsLogs 資料夾。)

### `-LogMode`

指定記錄檔的詳細資訊層級。

**值**：

- `0`：僅將指令碼訊息記錄到 PowerShell 命令視窗。

- `1`：將指令碼訊息同時記錄到輸出資料夾下的記錄檔和 PowerShell 命令視窗。

- `2`：僅將指令碼訊息記錄到輸出資料夾下的記錄檔。

**類型**：Int16

**位置**：2

**預設值**：`1` (將指令碼訊息同時記錄到記錄檔和 PowerShell 命令視窗。)

### `-CollectNetTrace`

指定指令碼是否收集網路追蹤。

**值**：

- `0`：不啟用網路追蹤。

- `1` (任何非零的整數值)：啟用網路追蹤並收集結果。

**類型**：Int16

**位置**：3

**預設值**：`0` (不啟用網路追蹤)

### `-CollectUTCTrace`

指定指令碼是否收集 Windows UTC 追蹤並執行連線能力診斷。

**值**：

- `0`：不啟用 UTC 追蹤，或不執行連線能力診斷。

- `1` (任何非零的整數值)：啟用 UTC 追蹤、執行連線能力診斷，以及收集結果。

**類型**：Int16

**位置**：4

**預設值**：`0` (不啟用 UTC 追蹤，或不執行連線能力診斷)


## <a name="output"></a>輸出

指令碼會在指定的路徑下建立「工作資料夾」  。 例如，**M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**。 它會將所有輸出檔案放入此工作資料夾。

如果啟用指令碼寫入「記錄檔」  ，即會在工作資料夾中產生一個記錄檔。 例如，**M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss.txt**。

指令碼也會在工作資料夾內產生其他的「診斷檔案」  。 例如：

- `installedKBs.txt`：安裝在裝置上的 Windows 更新清單
- `appcompat`：應用程式相容性資料
- `Reg*.txt`：具有自 Windows 登錄所匯出資料的系列檔案


## <a name="examples"></a>範例

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a> 範例 1：使用預設值透過 PowerShell 命令視窗執行指令碼

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a> 範例 2：使用指定的參數透過 PowerShell 命令視窗執行指令碼

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a> 範例 3：使用正確位置的指定參數透過 PowerShell 命令視窗執行指令碼

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a> 範例 4：使用指定的參數和詳細資訊訊息透過 PowerShell 命令視窗執行指令碼

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a> 範例 5：透過 Configuration Manager **指令碼**部署指令碼

如需詳細資訊，請參閱[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](../apps/deploy-use/create-deploy-scripts.md)。

DesktopAnalyticsLogsCollector.ps1 是由 Microsoft 以數位方式簽署。 您可能需要將其 Microsoft 程式碼簽署憑證新增為目標裝置上的受信任發行者。

1. 在 Windows 檔案總管中開啟指令碼的屬性。 切換至 [數位簽章]  索引標籤並選取 [詳細資料]  。

2. 在 [一般]  索引標籤上，選取 [檢視憑證]  。

    > [!Note]
    > 若要透過其他機制散發憑證，請先將憑證匯出至檔案。 移至 [詳細資料]  索引標籤並選取 [複製到檔案]  。

3. 選取 [安裝憑證]  。 匯入憑證，將它放置在**受信任的發行者**存放區。


## <a name="see-also"></a>請參閱

- [針對電腦分析進行疑難排解](troubleshooting.md) \(部分機器翻譯\)

- [從 Configuration Manager 主控台建立和執行 PowerShell 指令碼](../apps/deploy-use/create-deploy-scripts.md)
