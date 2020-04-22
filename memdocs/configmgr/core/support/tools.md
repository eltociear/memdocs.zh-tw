---
title: Configuration Manager 工具
titleSuffix: Configuration Manager
description: 深入了解工具，有助於您管理及針對您的 Configuration Manager 基礎結構進行疑難排解。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e308a54ee9636a7781667823e7b7f98ae6f25c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701266"
---
# <a name="configuration-manager-tools"></a>Configuration Manager 工具

適用於：  Configuration Manager (最新分支)

Configuration Manager 工具包括[以用戶端為基礎](#client-tools)和[以伺服器端為基礎的工具](#server-tools)。 使用這些工具，有助於支援及針對您的 Configuration Manager 基礎結構進行疑難排解。

從 Configuration Manager 1806 版開始，這些工具都會包含在站台伺服器的 `CD.Latest\SMSSETUP\Tools` 資料夾中。 不需要進一步安裝。<!--1357145--> 請搭配 Configuration Manager 1806 版和更新版本使用這些工具版本。

在[支援的用戶端和裝置作業系統](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中，列為支援之用戶端的所有 Windows 作業系統都支援使用這些工具。

> [!Note]  
> [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) 仍可從 Microsoft 下載中心取得。 若為 Configuration Manager 1806 版和更新版本，請使用站台伺服器上 CD.Latest 資料夾中的工具版本。 有些工具過去是在工具組中，但未納入 1806 版。 這些舊版工具不再受到支援。


## <a name="client-tools"></a>用戶端工具

這些工具位於 `ClientTools` 子資料夾中：

- [CMTrace](cmtrace.md)：檢視、監視及分析 Configuration Manager 記錄檔  

- [Client Spy](clispy.md)：針對軟體發佈、清查和計量等相關問題進行疑難排解

- [部署監視工具](deployment-monitoring-tool.md)：對應用程式、更新和基準部署進行疑難排解  

- [原則監視](policy-spy.md)：檢視原則指派  

- [電源檢視器工具](power-viewer-tool.md)：檢視電源管理功能的狀態  

- [傳送排程工具](send-schedule-tool.md)：觸發設定基準的排程和評估  

> [!Note]  
> `ClientTools` 資料夾也包含 Microsoft.Diagnostics.Tracing.EventSource.dll 檔案。 多個用戶端工具都需要此程式庫。 您無法直接使用它。  


## <a name="server-tools"></a>伺服器工具

這些工具位於 `ServerTools` 子資料夾中：

- [DP 作業佇列管理員](dp-job-manager.md)：對針對發佈點的內容發佈作業進行疑難排解  

- [集合評估檢視器](ceviewer.md)：檢視集合評估的詳細資料  

- [內容庫總管](content-library-explorer.md)：檢視內容庫單一執行個體存放區的內容  

- [內容庫傳輸](content-library-transfer.md)：在磁碟機之間傳送內容庫  

- [內容擁有權工具](content-ownership-tool.md)：變更孤立套件的擁有權。 這些套件存在於站台中，但沒有擁有套件的站台伺服器。

- [以角色為基礎的系統管理和稽核工具](rbaviewer.md)：協助系統管理員對角色設定進行稽核  

- [執行計量摘要工具](run-meter-summ.md)：執行計量摘要工作並分析計量資料

> [!Note]  
> [ServerTools] 資料夾也包含下列檔案：
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> 多個伺服器工具都需要這些程式庫。 您無法直接使用它們。  

## <a name="other-tools-and-toolkits"></a>其他工具和工具套件

- [支援中心](support-center.md)：進行疑難排解時從用戶端收集資訊以便輕鬆進行分析。

    從 1906 版開始，**OneTrace** 是支援中心的新記錄檢視器。 其運作方式與 CMTrace 類似，但包含改良功能。 如需詳細資訊，請參閱[支援中心 OneTrace](support-center-onetrace.md)。

- [將內部部署站台延伸及移轉到 Microsoft Azure](azure-migration-tool.md)：協助以程式設計方式為 Configuration Manager 建立 Azure 虛擬機器 (VM)。 <!--3556022--> 

- [內容庫清理工具](../plan-design/hierarchy/content-library-cleanup-tool.md)：使用 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中的 **ContentLibraryCleanup.exe** 移除發佈點的孤立內容。  

- [階層維護工具](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md)：使用站台伺服器上 `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` 共用資料夾中的 **Preinst.exe**，將命令傳遞給階層管理員元件。  

- [更新重設工具](../servers/manage/update-reset-tool.md)：使用 `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` 中的 **CMUpdateReset.exe** 來修正無法下載或複寫主控台內更新的問題。  

- [服務連線工具](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md)：使用 `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` 中的 **ServiceConnectionTool.exe**，讓您的站台在服務連接點離線時仍保持在最新狀態。   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md)：針對自動化電腦與伺服器 OS 部署提供供的一組統一的工具、程序與指導方針。

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md)：可用來管理及匯入自訂軟體更新的獨立式工具。

- [套件轉換管理員](../../apps/pcm/package-conversion-manager.md)：將傳統套件轉換為應用程式。
