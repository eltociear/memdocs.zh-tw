---
title: 建立應用程式群組
titleSuffix: Configuration Manager
description: 建立您可以在 Configuration Manager 中作為單一部署傳送給使用者或裝置集合的應用程式群組。
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643121"
---
# <a name="create-application-groups"></a>建立應用程式群組

適用於：  Configuration Manager (最新分支)

<!--3555907-->

從 1906 版開始，建立您可以作為單一部署傳送給使用者或裝置集合的應用程式群組。 您所指定應用程式群組相關中繼資料會顯示為軟體中心內的單一實體。 您可以排序群組中的應用程式，讓用戶端依特定順序來安裝這些應用程式。

> [!Note]  
> 在這個版本的 Configuration Manager 中，應用程式群組是發行前版本功能。 若要啟用此功能，請參閱[發行前版本功能](../../core/servers/manage/pre-release-features.md)。  

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區。 展開 [應用程式管理]  ，然後選取 [應用程式群組]  節點。  

1. 在功能區的 [建立] 群組上，選取 [建立應用程式群組]  。

1. 在 [一般資訊]  頁面上，指定應用程式群組的相關資訊。  

1. 在 [軟體中心]  頁面上，包含顯示在軟體中心內的資訊。  

1. 在 [應用程式群組]  頁面上，選取 [新增]  。 選取此群組的一或多個應用程式。 使用 [上移]  和 [下移]  動作來重新排列其順序。  

1. 完成精靈。  

使用與應用程式相同的程序來部署應用程式群組。 如需詳細資訊，請參閱[部署應用程式](deploy-applications.md)。 從 1910 版開始，您可以將應用程式群組部署至裝置或使用者集合。

部署群組之後：

- 如果您將新的應用程式新增至群組，您必須將新的應用程式內容分別發佈至發佈點。

- 如果您修改應用程式群組中的應用程式，請重新發佈內容。

若要針對應用程式群組部署進行疑難排解，請使用用戶端上的下列記錄檔：

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!Important]  
> 在您將整個階層和目標用戶端更新為最新版本 1906 之前，請不要建立或部署應用程式群組。

### <a name="known-issues"></a>已知問題

- *1906 版*：群組中的應用程式只能包含 **Windows Installer** 或**指令碼**部署類型。
  - *1906 版*：將部署類型安裝行為設定為 [針對系統安裝]  。
- 下列部署選項可能無法使用：警示、核准、階段式部署、修復。
- 您無法匯出或匯入應用程式群組。
- 請不要在群組中包含任何需要重新啟動的應用程式，否則群組部署可能會失敗。
- *1906 版*：您無法將應用程式群組部署到使用者集合。
- *1906 版*：使用者無法在 [軟體中心] 將應用程式群組**解除安裝**。
- 如果您刪除屬於應用程式群組一部分的應用程式，當您下一次檢視應用程式群組的屬性時，您會看到下列警告：「無法載入群組中所有應用程式的相關資訊。」 對應用程式群組進行簡單變更並加以儲存。 例如，在 [系統管理員註解]  中新增一個空格。 當您儲存變更時，其會從群組移除已刪除的應用程式。<!-- 7099542 -->
