---
title: BitLocker 事件記錄檔
titleSuffix: Configuration Manager
description: 了解如何在 Windows 事件記錄檔中使用 BitLocker 資訊來針對問題進行疑難排解
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706026"
---
# <a name="bitlocker-event-logs"></a>BitLocker 事件記錄檔

適用於：  Configuration Manager (最新分支)

BitLocker 管理代理程式和 Web 服務會使用 Windows 事件記錄檔來記錄訊息。 在事件檢視器中，請移至 [應用程式及服務記錄檔]  、[Microsoft]  、[Windows]  。 記錄通道 (節點) 會根據電腦和元件而有所不同：

- **MBAM**：用戶端電腦上的 BitLocker 管理代理程式
- **MBAM-Web**：
  - 管理點上的復原服務
  - 自助入口網站
  - 管理和監視網站

如需這些記錄檔中特定訊息的詳細資訊，請參閱下列文章：

- [用戶端事件記錄檔](client-event-logs.md)
- [伺服器事件記錄檔](server-event-logs.md)

根據預設，您會在每個節點中看到兩個記錄通道：**系統管理員**和**作業**。 如需更詳細的疑難排解資訊，您也可以顯示[分析和偵錯記錄檔](#bkmk_debug)。

## <a name="log-properties"></a>記錄內容

在 Windows 事件檢視器中選取特定記錄檔。 例如，**系統管理員**。移至 [執行]  功能表，然後選取 [屬性]  。 進行以下設定：

- **記錄檔大小上限 (KB)** ：根據預設，所有記錄檔的此設定為 `1028` (1 MB)。
- **達到事件記錄檔大小上限時**：根據預設，**系統管理員**和**作業**記錄檔會設定為 [視需要覆寫事件 (最舊的事件優先)]  。

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a> 分析和偵錯記錄

您可以啟用更詳細的記錄檔以便進行疑難排解。 在事件檢視器中，移至 [檢視]  功能表，然後選取 [顯示分析和偵錯記錄檔]  。 現在瀏覽至記錄檔通道時，將會看到兩個額外的記錄檔：**分析**與**偵錯**。

> [!TIP]
> 根據預設，這些記錄檔具有下列屬性：
>
> - **記錄檔大小上限 (KB)** ：`1028` (1 MB)
> - **不覆寫事件 (手動清除記錄)**

## <a name="export-logs-to-text"></a>將記錄匯出到文字

特別是在[分析和偵錯記錄檔](#bkmk_debug)時，您可能會發現在單一文字檔中檢視項目會更容易。 請使用下列 PowerShell 命令，將事件記錄檔項目匯出至文字檔：

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
