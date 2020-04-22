---
title: 支援中心
titleSuffix: Configuration Manager
description: 使用支援中心針對 Configuration Manager 用戶端進行疑難排解。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21279eb2f7d7962d1286d60a599411912d38313a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701316"
---
# <a name="support-center-for-configuration-manager"></a>適用於 Configuration Manager 的支援中心

適用於：  Configuration Manager (最新分支)

<!--1357489-->
從 1810 版開始，使用支援中心來進行用戶端疑難排解、即時檢視記錄檔，或擷取 Configuration Manager 用戶端電腦的狀態，以於稍後進行分析。 支援中心為合併眾多系統管理員疑難排解工具的單一工具。


## <a name="about"></a>關於

支援中心旨在減少對 Configuration Manager 用戶端電腦進行疑難排解時的挑戰和挫折。 過去，在配合技術支援人員解決 Configuration Manager 用戶端問題時，您需要手動收集記錄檔和其他資訊，以利針對問題進行疑難排解。 一不小心就容易漏掉重要的記錄檔，造成您及合作支援人員的額外困擾。

使用支援中心簡化支援體驗。 這可讓您：

- 建立包含 Configuration Manager 用戶端記錄檔的疑難排解配套 (.zip 檔案)。 然後，您只要向支援人員傳送一個檔案。  

- 檢視 Configuration Manager 用戶端記錄檔、憑證、登錄設定、偵錯傾印、用戶端原則。  

- 即時診斷清查 (取代 ClientSpy)、原則 (取代 PolicySpy) 及用戶端快取。  

### <a name="support-center-viewer"></a>支援中心檢視器

支援中心包含支援中心檢視器，這是支援人員用來開啟您使用支援中心所建立之配套檔案的工具。 支援中心之資料收集器會收集並封裝本機或遠端 Configuration Manager 用戶端的診斷記錄檔。 請使用檢視器應用程式檢視資料收集器配套檔案。

### <a name="support-center-log-file-viewer"></a>支援中心記錄檔檢視器

支援中心包含最新的記錄檔檢視器。 此工具取代 OneTrace 並提供可自訂的介面及索引標籤和可停駐視窗支援。 它有快速的簡報層，並可在數秒內載入大型的記錄檔。

### <a name="support-center-onetrace-preview"></a>支援中心 OneTrace (預覽)

<!--3555962-->
從 1906 版開始，**OneTrace** 是支援中心的新記錄檢視器。 其運作方式與 CMTrace 類似，但包含改良功能。 如需詳細資訊，請參閱[支援中心 OneTrace](support-center-onetrace.md)。

### <a name="powershell-cmdlets"></a>PowerShell Cmdlet

支援中心也包含 [Windows PowerShell Cmdlet](https://go.microsoft.com/fwlink/?linkid=397830)。 您可以使用這些 Cmdlet 建立其他 Configuration Manager 用戶端的遠端連線、設定資料收集選項，以及啟動資料收集。


## <a name="prerequisites"></a>先決條件

請在要安裝支援中心的伺服器或用戶端電腦上安裝下列元件：

- Configuration Manager 支援的作業系統版本。 如需詳細資訊，請參閱[用戶端支援的作業系統版本](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。 支援中心不支援行動裝置。  

- 在您執行支援中心及其元件的電腦上需要有 .NET Framework 4.5.2。  


## <a name="install"></a>安裝

在下列路徑的站台伺服器上找到支援中心安裝程式：`cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

安裝它之後，請在 [開始] 功能表的 **Microsoft System Center** 群組中尋找下列項目：  

- 支援中心 (ConfigMgrSupportCenter.exe)  
- 支援中心記錄檔檢視器 (CMLogViewer.exe)  
- 支援中心檢視器 (ConfigMgrSupportCenterViewer.exe)  


## <a name="known-issues"></a>已知問題

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>如果已安裝較舊的版本，就無法安裝最新版本

<!--SCCMDocs-pr issue #3090-->
*適用於 1810 版和 1902 版*

如果您已安裝舊版的支援中心，新版安裝程式將會失敗。 此問題的原因是檔案的原始版本與最新版本之間的版本控制方式。 若要解決此問題，請先將舊版本支援中心解除安裝。 接著，安裝最新的版本。

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>遠端連線的使用者名稱必須包含電腦名稱或網域

如果您從支援中心連線至遠端用戶端，則必須提供建立連線時的使用者帳戶電腦名稱或網域名稱。 如果您使用簡易的電腦名稱或網域名稱 (例如 `.\administrator`)，連線會成功，但支援中心卻無法收集用戶端資料。

為避免這個問題，請使用下列使用者名稱格式連線到遠端用戶端：

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>您可能需要移除遠端用戶端已編寫指令碼的伺服器訊息區連線

使用 [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) PowerShell Cmdlet 連線到遠端用戶端時，支援中心會建立每個遠端用戶端的伺服器訊息區 (SMB) 連線。 在您完成資料收集之後，它會保留這些連線。 為避免超出 Windows 遠端連線數的上限，請使用 `net use` 命令查看目前使用中的遠端連線集合。 然後使用下列命令停用任何不需要的連線：`net use <connection_name> /d`
其中 `<connection_name>` 是遠端連線的名稱。

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>應用程式部署評估週期要求未正確地傳送至遠端電腦

<!--2849356-->
*適用於 1810 版*

在支援中心，如果您從 [內容]  索引標籤上的 [叫用觸發程序]  動作選取 [應用程式部署評估]  ，此動作會啟動評估已部署應用程式的工作。 如果您連線到本機用戶端，它會評估電腦和使用者的應用程式部署。 不過，如果您連線到遠端用戶端，它只會評估電腦的應用程式部署。


## <a name="next-steps"></a>後續步驟

[支援中心快速入門](support-center-quickstart.md)
