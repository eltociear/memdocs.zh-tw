---
title: Cmdlet 隱私權聲明
titleSuffix: Configuration Manager
description: 了解 Microsoft 如何收集和使用 Configuration Manager Cmdlet 的相關資料
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695746"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Configuration Manager Cmdlet 庫隱私權聲明

適用於：  Configuration Manager (最新分支)

本隱私權聲明涵蓋 Configuration Manager Cmdlet 程式庫的功能。  

## <a name="usage-data"></a>使用方式資料  

#### <a name="what-this-feature-does"></a>這項功能的作用

您可利用 Configuration Manager Cmdlet 程式庫，透過 Windows PowerShell Cmdlet 與指令碼，來管理 Configuration Manager 階層。 Cmdlet 程式庫會收集有關您如何使用程式庫中 Cmdlet 的資訊，以找出趨勢及使用習慣。 Cmdlet 程式庫也會收集您使用 Cmdlet 時收到的錯誤類型與數目。  

#### <a name="information-collected-processed-or-transmitted"></a>收集、處理或傳輸的資訊
   
收集的使用方式資料包括啟動、停止及終止 Cmdlet、執行已取代的 Cmdlet，以及與 Cmdlet 相關 SMS 提供者作業的活動指標。 這項資訊不具個人識別性質。 收集的錯誤資訊包括 Cmdlet 所傳回的錯誤，以及例外狀況錯誤的錯誤詳細資料。 某些錯誤詳細資料報告可能會不小心包含個人識別資料，例如連線至您電腦之裝置的序號。 Cmdlet 程式庫會篩選錯誤報告中的資訊，並以匿名方式處理資訊，以在將資訊傳輸給 Microsoft 之前移除個人識別資料。  

#### <a name="use-of-information"></a>資訊之使用
   
Microsoft 使用這項資訊的目的，是為了改善所提供產品與服務的品質、安全性與完整性。  

#### <a name="choicecontrol"></a>選擇/控制   

預設會啟用此使用方式資料功能。 Configuration Manager Cmdlet 程式庫有兩個登錄機碼可控制這項功能。  

 若要選擇完全退出，請設定下列這兩個登錄機碼值。 它們分別適用於兩個 Windows 事件追蹤 (ETW) 提供者：  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (選擇退出收集磁碟機提供者的使用方式資料)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (選擇退出收集 Cmdlet 的使用方式資料)  

  使用方式資料設定的變更，只對進行變更的電腦有效。  


## <a name="next-steps"></a>後續步驟

[Configuration Manager Cmdlet 程式庫文件](https://docs.microsoft.com/powershell/sccm/configurationmanager/) \(英文\)。   
