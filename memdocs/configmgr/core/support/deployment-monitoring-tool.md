---
title: 部署監視工具
titleSuffix: Configuration Manager
description: 使用部署監視工具，針對 Configuration Manager 用戶端上的軟體部署進行疑難排解。
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707826"
---
# <a name="deployment-monitoring-tool"></a>部署監視工具

適用於：  Configuration Manager (最新分支)

部署監視工具是其中一種 [Configuration Manager 工具](tools.md)。 它是一種圖形化使用者介面，設計來協助針對 Configuration Manager 用戶端上的應用程式、軟體更新和設定基準部署進行疑難排解。 此工具為唯讀，因為它不會變更用戶端上的任何狀態。 您可以安全地使用它來診斷常見的部署案例。


## <a name="features"></a>功能

- 以系統管理員身分執行，來針對本機用戶端上的部署進行疑難排解。  

- 針對遠端用戶端上的部署進行疑難排解。 以系統管理員身分啟動工具並連線到遠端電腦。  

- 將工具中收集的所有資料都匯出成 XML。 與其他人共用 XML 檔案，並使用它作為針對部署進行疑難排解的通用平台。  

- 將先前匯出的資料匯入到不同的電腦，並使用它以離線模式執行此工具。   


## <a name="usage"></a>使用方式

部署監視工具僅支援圖形化使用者介面。 若要啟動工具，請以系統管理員身分執行 **DeploymentMonitoringTool.exe**。 有三種檢視：  

- **用戶端內容**：裝置與 Configuration Manager 用戶端的相關實用屬性清單。 此檢視為預設。   

- **部署**：檢視所有目前設為目標的部署。 若要檢視 [詳細資料] 窗格中的其他資訊，請選取 [結果] 窗格中某個部署。  

- **所有更新**：檢視所有軟體更新和其狀態。  

若要複製任何檢視中的資料，請選取資料格，然後按下 **CTRL** + **C**。


### <a name="actions-menu"></a>[動作] 功能表

[動作]  功能表提供下列動作：  

- **連線到遠端電腦**：選取要連線的電腦。 當您未指定使用者名稱和密碼時，它會使用目前的認證。 按一下 [儲存]  連線至遠端電腦。  

- **匯出資料**：選取要寫入資料的檔案，然後按一下 [儲存]  。 使用匯出的 XML 檔案，在不同的電腦上進行遠端疑難排解。  

- **匯入資料**：選取要匯入工具的檔案。  

- **檢視記錄**：根據檢視而定，開啟相關聯的記錄檔：  
    - 用戶端內容：`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - 部署：`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - 所有更新：`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>請參閱

- [部署應用程式](../../apps/deploy-use/deploy-applications.md)
- [部署軟體更新](../../sum/deploy-use/deploy-software-updates.md)
- [部署設定基準](../../compliance/deploy-use/deploy-configuration-baselines.md)
