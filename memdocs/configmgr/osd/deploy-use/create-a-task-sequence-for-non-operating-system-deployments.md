---
title: 為非 OS 部署建立工作順序
titleSuffix: Configuration Manager
description: 建立不適用於部署 OS 的工作順序，例如散發軟體或將工作自動化
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 583a90452fe077057b93150e9cb635fe9269de5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709066"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>為非 OS 部署建立工作順序

適用於：  Configuration Manager (最新分支)

Center Configuration Manager 中的工作順序是用來將環境中各種不同的工作自動化。 這些工作主要針對部署作業系統來進行設計和測試。 Configuration Manager 具有許多應該作為下列案例主要技術使用的其他功能：

- [應用程式安裝](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > 從 2002 版開始，請透過應用程式模型，使用工作順序安裝複雜的應用程式。 將部署類型新增到本身為工作順序的應用程式 (安裝或解除安裝應用程式)。 如需詳細資訊，請參閱[建立 Windows 應用程式](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)。<!-- 3555953 -->

- [軟體更新安裝](../../sum/understand/software-updates-introduction.md)

- [設定組態](../../compliance/understand/ensure-device-compliance.md)

此外請考慮其他 Microsoft System Center 自動化技術，例如 [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) 和 [Service Management Automation](https://docs.microsoft.com/system-center/sma/)。  

工作順序的優勢在於其彈性，以及您使用它們的方式。 它們可以在獨立於 OS 部署的情況下設定用戶端設定、散發軟體、更新驅動程式、編輯使用者狀態，以及執行其他工作。 您可以建立自訂工作順序以新增任何數量的工作。 Configuration Manager 支援使用非 OS 部署的自訂工作順序。 不過，如果工作順序產生不想要或不一致的結果，請查看如何簡化作業：

- 使用較簡單的步驟
- 將動作分散到多個工作順序
- 針對建立及測試工作順序採取分段式的方式

支援在非 OS 部署自訂工作順序中使用下列步驟：  

- [檢查整備程度](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [連線到網路資料夾](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [下載套件內容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [安裝應用程式](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [安裝套件](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [安裝軟體更新](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [重新啟動電腦](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [執行 PowerShell 指令碼](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [執行工作順序](../understand/task-sequence-steps.md#child-task-sequence)  

- [設定動態變數](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [設定工作順序變數](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  
