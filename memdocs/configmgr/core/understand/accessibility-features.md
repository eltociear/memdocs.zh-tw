---
title: Accessibility
titleSuffix: Configuration Manager
description: 深入了解可供所有人使用的 Configuration Manager 功能。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2ff86df999ab744d590b1ca120a8b566d18f446b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701256"
---
# <a name="accessibility-features-in-configuration-manager"></a>Configuration Manager 的協助工具功能

適用於：  Configuration Manager (最新分支)


Configuration Manager 包含協助所有人使用的功能。

> [!Note]  
> 從 1902 版開始，若要改善 Configuration Manager 主控台的協助工具功能，請在執行主控台的電腦上，將 .NET 更新至 4.7 版或更新版本。 <!-- SCCMDocs-pr issue #3228 -->  
> 
> 更多有關 .NET 4.7.1 和 4.7.2 中的協助工具變更的詳細資訊，請參閱 [.NET Framework 中的協助工具有哪些新功能](https://docs.microsoft.com/dotnet/framework/whats-new/whats-new-in-accessibility)。  



## <a name="keyboard-shortcuts"></a>鍵盤快速鍵

### <a name="console-workspaces"></a>主控台工作區

使用下列鍵盤快速鍵存取工作區：  

|鍵盤快速鍵| 工作區|
|--------|--------|  
|Ctrl + 1| 資產與相容性|
|Ctrl + 2|  軟體程式庫|
|Ctrl + 3|  監視|
|Ctrl + 4|  系統管理|


### <a name="other-keyboard-shortcuts"></a>其他鍵盤快速鍵

|鍵盤快速鍵|  目的|
|--------|--------|  
|Ctrl + M|將焦點設定在主要 (中央) 窗格上。|
|Ctrl + T|將焦點設定至瀏覽窗格中的最上層節點。 如果焦點已經在該窗格中，則會將焦點設定至您瀏覽的最後一個節點。|
|Ctrl + I|將焦點設定至功能區下的階層連結列。|
|Ctrl + L|將焦點設定至 [搜尋]  欄位 (如果可用)。|
|Ctrl + D|將焦點設定至 [詳細資料] 窗格 (如果可用)。|
|Alt     |在功能區內外切換焦點。|



## <a name="other-accessibility-features"></a>其他協助工具功能

- 若要巡覽 [瀏覽] 窗格，請輸入節點名稱的字母。

- 在主要檢視和功能區的鍵盤瀏覽是採用循環方式。

- 在詳細資料窗格中的鍵盤瀏覽是採用循環方式。 若要返回上一個物件或窗格，請使用 Ctrl + D，然後使用 Shift + TAB。

- 重新整理 [工作區] 檢視之後，焦點會設定至該工作區的主要窗格。

- 若要存取工作區功能表，請選取 Tab 鍵，直到 [展開/收合] 圖示進入焦點。 接著選取向下鍵以存取工作區功能表。  

- 若要瀏覽工作區功能表，請使用方向鍵。  

- 若要存取工作區中的不同區域，請使用 Tab 鍵和 Shift+Tab 鍵。 若要在工作區的某個區域中瀏覽 (例如功能區)，請使用方向鍵。  

- 若要在焦點位於樹狀節點時存取位址列，請按 Shift+Tab 鍵 3 次。  

- 在精靈或內容頁面中，使用鍵盤快速鍵可在方塊之間移動。 同時選取 Alt 鍵和加底線的字元 (Alt+_) 可選取特定方塊。     

- 若要瀏覽到工作區的不同節點，請輸入節點名稱的第一個字母。 每個按鍵動作都會將游標移至以該字母開頭的下一個節點。 當您使用螢幕助讀程式時，助讀程式會讀出該節點的名稱。



## <a name="see-also"></a>請參閱

如需巡覽 Configuration Manager 使用者介面之基本概念的相關詳細資訊，請參閱下列文章：
- [使用 Configuration Manager 主控台](../servers/manage/admin-console.md)  
- [軟體中心使用者指南](software-center.md)

> [!NOTE]  
> 本文提供的資訊僅適用於擁有 Microsoft 產品美國地區授權的使用者。 如果您在美國以外地區取得本產品，可以使用軟體套件隨附的子公司資訊卡，或者瀏覽 [Microsoft 協助工具網站](https://go.microsoft.com/fwlink/?LinkId=8431)，取得 Microsoft 支援服務的連絡資訊。 您可以與您所在地區的子公司連絡，了解本節所述的產品及服務類型是否已於當地銷售。 關於協助工具的資訊，還有其他語言版本，包括日文和法文。  

