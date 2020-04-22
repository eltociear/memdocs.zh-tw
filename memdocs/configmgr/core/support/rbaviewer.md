---
title: 以角色為基礎的管理工具
titleSuffix: Configuration Manager
description: 使用以角色為基礎的管理和稽核工具模型化和稽核安全性角色，並設定在 Configuration Manager 中的範圍。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707556"
---
# <a name="role-based-administration-and-auditing-tool"></a>以角色為基礎的管理與稽核工具

適用於：  Configuration Manager (最新分支)

以角色為基礎的管理和稽核工具是 [Configuration Manager 工具](tools.md)的其中之一。 使用此工具來執行下列工作：

- 建立具有特定權限的安全性角色模型  

- 稽核其他使用者擁有的安全性範圍和安全性角色



## <a name="requirements"></a>需求

- 在與 Configuration Manager 主控台所在的同一部電腦上執行它  

- 您擁有**系統高權限管理員**、**唯讀分析師**或**安全性系統管理員**角色  

- 將您的帳戶指派給**所有**安全性範圍和所有集合  

- (*選擇性*) 您必須具有 SQL 存取權才能分析報表資料夾安全性  

- (*選擇性*) 請對具有報告點角色的站台系統伺服器執行此工具以分析報表鑽研



## <a name="procedures"></a>程序


### <a name="model-permissions-for-a-new-role"></a>建立新角色的權限模型

使用下列程序為您想要建立的新角色建立權限模型： 

1. 執行 **RBAViewer.exe**。  

2. 選取您想要使用的安全性角色建置基礎，或從空的權限集開始。 選取必要的權限。  

3. 按一下 [分析]  查看這個自訂角色會看到的使用者介面。  

    > [!Note]  
    > 若要查看是否有符合您需求的現有安全性角色，請切換到 [相似性]  索引標籤。  

4. 按一下 [匯出]  將角色儲存為 XML 檔案。 然後將它滙入 Configuration Manager 主控台。 如需詳細資訊，請參閱 [建立自訂安全性角色](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)。


### <a name="audit-existing-security-scopes"></a>稽核現有的安全性範圍

使用下列程序稽核 Configuration Manager 中所有現有的系統管理使用者、集合和安全性範圍：

1. 執行 **RBAViewer.exe**。  

2. 選取工具列的 [Audit RBA] \(稽核 RBA\)  按鈕。  

    1. 若要檢視樹狀檢視中的集合限制關聯性，請切換至 [Collection Summary] \(集合摘要\)  索引標籤。  

    2. 若要檢視指派給安全性角色的物件，請切換到 [範圍摘要]  索引標籤。  


### <a name="audit-a-specific-user"></a>稽核特定使用者

使用下列程序稽核特定使用者以角色為基礎的管理設定：

1. 執行 **RBAViewer.exe**。  

2. 選取工具列的 [執行身分]  按鈕。  

3. 輸入特定使用者名稱以檢查該帳戶的權限。  

4. 此工具會顯示指派給使用者的安全性角色，或使用者所屬的安全性群組。 它也會顯示此使用者可以看到的物件，以及其可在主控台中採取的動作。  



## <a name="see-also"></a>請參閱

- [以角色為基礎的系統管理基本概念](../understand/fundamentals-of-role-based-administration.md)
- [設定以角色為基礎的系統管理](../servers/deploy/configure/configure-role-based-administration.md)
