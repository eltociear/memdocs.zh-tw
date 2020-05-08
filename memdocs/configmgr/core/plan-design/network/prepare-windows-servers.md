---
title: 準備 Windows 伺服器
titleSuffix: Configuration Manager
description: 請確定電腦符合作為 Configuration Manager 站台伺服器或站台系統伺服器的必要條件。
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e4e84b55c929dd878cb0720b3f61dfceedcf449
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904101"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>準備 Windows Servers 以支援 Configuration Manager

適用於：  Configuration Manager (最新分支)

Windows 電腦必須符合其作為站台伺服器或站台系統伺服器的預期用途必要條件，您才能使用它作為 Configuration Manager 的站台系統伺服器。  

- 這些必要條件通常包含一個或多個 Windows 功能或角色，使用電腦伺服器管理員可加以啟用。  

- 由於啟用 Windows 功能和角色的方法會因 OS 版本而異，因此請參考 OS 版本的文件，以取得有關如何設定您所使用 OS 的詳細資訊。  

這篇文章中的資訊提供支援 Configuration Manager 站台系統所需的 Windows 設定類型概觀。 如需特定站台系統角色的設定詳細資料，請參閱[站台和站台系統必要條件](../configs/site-and-site-system-prerequisites.md)。

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Windows 功能和角色  
當您在電腦上設定 Windows 功能和角色時，可能需要將電腦重新開機，才能完成設定。 因此，在安裝 Configuration Manager 站台或站台系統伺服器之前，找出即將裝載特定站台系統角色是個不錯的主意。

### <a name="features"></a>功能  
下列 Windows 功能為特定站台系統伺服器所需，並且應該先加以設定，再將站台系統角色安裝於該電腦。  

- **.NET Framework**：包括  

    - ASP.NET  
    - HTTP 啟動  
    - 非 HTTP 啟動  
    - Windows Communication Foundation (WCF) 服務  

    不同站台系統角色需要不同版本的 .NET Framework。  

    由於 .NET Framework 4.0 和更新版本無法與舊版相容以取代 3.5 和更舊版本，因此當不同版本列為必要版本時，請規劃在同一部電腦上啟用每個版本。  

- **背景智慧型傳送服務 (BITS)** ：管理點需要 BITS (和自動選取的選項) 才可支援與受管理裝置間的通訊。  

- **BranchCache**：可為發佈點設定 BranchCache，以支援使用 BranchCache 的用戶端。  

- **重複資料刪除**：可為發佈點設定重複資料刪除並從中獲得好處。  

- **遠端差異壓縮 (RDC)** ：每部裝載站台伺服器或發佈點的電腦都需要 RDC。 RDC 可用於產生封裝簽章及執行簽章比較。  

### <a name="roles"></a>角色  
以下是支援特定功能 (例如軟體更新和 OS 部署) 所需的 Windows 角色，而最常見的站台系統角色則需要 IIS。  

- **網路裝置註冊服務** (在「Active Directory 憑證服務」底下)：此 Windows 角色是在 Configuration Manager 中使用憑證設定檔的必要條件。  

- **網頁伺服器 (IIS)** ：包括：  
    - 一般 HTTP 功能  
          - HTTP 重新導向  
    - 應用程式開發  
          - .NET 擴充性  
          - ASP.NET  
          - ISAPI 擴充程式  
          - ISAPI 篩選器  
    - 管理工具  
          - IIS 6 管理相容性  
          - IIS 6 Metabase 相容性  
          - IIS 6 Windows Management Instrumentation (WMI) 相容性  
    - 安全性  
          - 要求篩選  
          - Windows 驗證  

  下列站台系統角色使用其中一或多項所列 IIS 設定：  
  - 應用程式類別目錄 Web 服務點  
  - 應用程式類別目錄網站點  
  - 發佈點  
  - 註冊點  
  - 註冊 Proxy 點  
  - 後援狀態點  
  - 管理點  
  - 軟體更新點  
  - 狀態移轉點     

  所需的 IIS 最低版本是站台伺服器 OS 隨附的版本。  

  除了這些 IIS 設定外，您可能還需要設定[用於發佈點的 IIS 要求篩選](#BKMK_IISFiltering)。  

- **Windows 部署服務**：此角色會與 OS 部署搭配使用。  

- **Windows Server Update Services**：此角色是軟體更新的必要角色。  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> 用於發佈點的 IIS 要求篩選  
IIS 預設會使用要求篩選來封鎖 HTTP 或 HTTPS 通訊存取伺服器數個副檔名和資料夾位置。 在發佈點上，如此可預防用戶端下載包含遭封鎖副檔名或資料夾位置的套件。  

如果您的套件來源檔案包含在 IIS 中遭要求篩選設定封鎖的副檔名，您就必須將要求篩選設定為允許這些副檔名。 在您發佈點電腦上的「IIS 管理員」中[編輯要求篩選功能](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11))，即可完成此操作。  

此外，Configuration Manager 的套件和應用程式使用下列副檔名。 請確認您的要求篩選設定未封鎖下列副檔名：  

- .PCK  
- .PKG  
- .STA  
- .TAR  

例如，軟體部署的來源檔案中可能包含名為 **bin**的資料夾，或是副檔名為 **.mdb** 的檔案。  

- IIS 要求篩選預設會封鎖對這些項目的存取 (**bin** 會以「隱藏區段」的形式遭到封鎖， **.mdb** 則以副檔名的形式遭到封鎖)。  

- 當您在發佈點上使用預設的 IIS 設定時，使用 BITS 的用戶端會無法從發佈點下載此軟體部署，並且會表示他們正在等候內容。  

- 若要讓用戶端下載此內容，請在每個適用的發佈點上編輯 IIS Manager 中的 [要求篩選]  ，以允許存取您所部署套件及應用程式中的副檔名和資料夾。  

> [!IMPORTANT]  
> 編輯要求篩選可能會增加電腦的受攻擊面。  
> 
> - 您在伺服器層級進行的編輯適用於伺服器上所有網站。   
>     - 您對個別網站所做的編輯僅使用於該網站。  
> 
> 最佳安全作法是在專用 Web 伺服器上執行 Configuration Manager。 如果必須在該 Web 伺服器上執行其他應用程式，請使用 Configuration Manager 的自訂網站。 如需相關資訊，請參閱[站台系統伺服器的網站](websites-for-site-system-servers.md)。  

## <a name="http-verbs"></a>HTTP 動詞
**管理點：** 為了確保用戶端可以成功地與管理點進行通訊，請在管理點伺服器上確認允許下列 HTTP 動詞︰  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**發佈點：** 發佈點需要允許下列 HTTP 動詞：
- GET
- HEAD
- PROPFIND

如需詳細資訊，請參閱[設定 IIS 中的要求篩選](https://docs.microsoft.com/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)#http-verbs) \(英文\)。 
