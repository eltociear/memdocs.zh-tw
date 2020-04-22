---
title: 支援中心 OneTrace (預覽)
titleSuffix: Configuration Manager
description: OneTrace 是支援中心的新記錄檢視器，其對 CMTrace 進行了改進。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707446"
---
# <a name="support-center-onetrace-preview"></a>支援中心 OneTrace (預覽)

<!--3555962-->

從 1906 版開始，OneTrace 是支援中心的新記錄檢視器。 其運作方式與 CMTrace 相似，但改善了下列項目：

- 索引標籤式檢視
- 可停駐視窗
- 改善的搜尋功能
- 在不離開記錄檢視的情況下啟用篩選的功能
- 捲軸提示，可快速識別錯誤叢集
- 快速開啟大型檔案的記錄

[![OneTrace 記錄檢視器的螢幕擷取畫面](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace 可搭配許多記錄檔類型使用，例如：

- Configuration Manager 用戶端記錄
- Configuration Manager 伺服器記錄
- 狀態訊息
- Windows 10 上的 Windows Update ETW 記錄檔
- Windows 7 和 Windows 8.1 上的 Windows Update 記錄檔

## <a name="prerequisites"></a>先決條件

- .NET Framework 4.6 版或更新版本

## <a name="install"></a>安裝

OneTrace 會與支援中心一起安裝。 在下列路徑的站台伺服器上找到支援中心安裝程式：`cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

根據預設，OneTrace 應用程式安裝在 `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`。

> [!Note]  
> 支援中心和 OneTrace 使用 Windows Presentation Foundation (WPF)。 此元件不適用於 Windows PE。 繼續在開機映像中，搭配工作順序部署使用 CMTrace。  

## <a name="log-groups"></a>記錄檔群組

<!--5559993-->

自 2002 版開始，OneTrace 支援可自訂的記錄檔群組，類似支援中心的功能。 記錄檔群組可讓您開啟單一案例的所有記錄檔。 OneTrace 目前包含下列案例的群組：

- 應用程式管理
- 相容性設定 (也稱為 Desired Configuration Management)
- 軟體更新

若要顯示記錄檔群組，請移至 [檢視]  功能表，然後選取 [記錄檔群組]  。

![應用程式管理的 OneTrace 記錄檔群組螢幕擷取畫面](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>自訂記錄檔群組

您可以藉由修改設定 XML 來自訂這些群組，其預設位於下列路徑中：`C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`。

下列範例是預設設定檔的一部分：

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

`GroupType` 屬性接受下列值：

- `0`：未知或其他
- `1`：Configuration Manager 用戶端記錄
- `2`：Configuration Manager 伺服器記錄

`GroupFilePath` 屬性可以包含記錄檔的明確路徑。 如為空白，則 OneTrace 會依賴群組類型的登錄設定。 例如，如果您設定 `GroupType=1`，則根據預設，OneTrace 會自動在 `C:\Windows\CCM\Logs` 中尋找群組的記錄。 在此範例中，您不需要指定 `GroupFilePath`。

## <a name="see-also"></a>請參閱

- [支援中心記錄檢視器](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
