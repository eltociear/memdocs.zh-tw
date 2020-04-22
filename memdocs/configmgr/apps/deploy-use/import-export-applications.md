---
title: 匯入和匯出應用程式
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中匯入和匯出應用程式，以便在不同的階層之間共用。
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4ed1c10e23b75dc4478a0409d197015c98aff8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689436"
---
# <a name="import-and-export-applications"></a>匯入和匯出應用程式

適用於：  Configuration Manager (最新分支)

使用 Configuration Manager 在兩個階層之間匯入和匯出應用程式。 例如，將應用程式從測試環境複製到生產環境。

## <a name="export"></a>匯出

1. 在 Configuration Manager 主控台中，選取 [應用程式]  節點。 在功能區的 [建立] 群組中，選擇 [匯出應用程式]  。
1. 在 [一般]  畫面上，輸入匯出目標之新 ZIP 檔案的路徑。 選擇性地指定是否要匯出「相依性、取代關聯性、條件和虛擬環境」  ，以及「所選取應用程式和相依性的內容」  。  如有需要，請輸入任何系統管理員註解，並選取 [下一步]  。
1. 確認應用程式和任何相依性列在 [相關物件]  頁面上，然後選取 [下一步]  。
1. 在 [摘要] 頁面上，選取 [下一步]  。
1. 程序完成之後，它會建立 ZIP 檔案，然後您就可以關閉此精靈。

> [!IMPORTANT]
> 如果您要將這個應用程式複製到另一個環境，會同時需要 ZIP 檔案和其隨附的資料夾。 ZIP 檔案必須存在於與所建立資料夾相同的目錄中。

## <a name="import"></a>匯入

> [!NOTE]
> 您只能從 UNC 路徑匯入應用程式，而無法從您的本機磁碟直接匯入。

1. 在 Configuration Manager 主控台中，選取 [應用程式]  節點。 在功能區的 [建立] 群組中，選擇 [匯入應用程式]  。
1. 選擇您想要匯入的 ZIP 檔案，並選取 [下一步]  。
1. [檔案內容] 視窗隨即顯示當您匯入應用程式時會發生的情況。 選取 [下一步]  。
1. 檢閱摘要畫面，並選取 [下一步]  。
1. 關閉精靈。 應用程式現在即可在站台中使用。

## <a name="see-also"></a>請參閱
 
使用 PowerShell 來自動化應用程式的匯入和匯出。

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
