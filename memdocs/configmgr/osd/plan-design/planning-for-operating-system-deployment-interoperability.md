---
title: OS 部署互通性
titleSuffix: Configuration Manager
description: 了解單一階層中不同 Configuration Manager 站台使用不同版本時的互通性問題。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708076"
---
# <a name="plan-for-os-deployment-interoperability"></a>規劃 OS 部署互通性

適用於：  Configuration Manager (最新分支)

單一階層中不同 Configuration Manager 站台使用不同版本時，部分 Configuration Manager 功能會無法使用。 通常，執行舊版之站台或用戶端無法存取新版 Configuration Manager 的功能。 如需詳細資訊，請參閱 [Configuration Manager 不同版本之間的互通性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)。  


## <a name="objects"></a>物件

當您升級階層中頂層站台以及階層中執行舊版 Configuration Manager 的其他站台時，請考慮下列物件：  

### <a name="client-installation-package"></a>用戶端安裝套件  

- 預設用戶端安裝套件的來源會自動升級。 階層中所有發佈點都會使用新的用戶端安裝套件進行更新。 即使在階層中舊版的站台發佈點上，還是會發生此行為。  

- 您無法將新版本用戶端指派給您尚未升級至新版本的站台。 指派會在管理點遭到封鎖。  

### <a name="boot-images"></a>開機映像  

- 當頂層站台升級至最新版的 Configuration Manager 時，它會自動更新預設的開機映像 (x86 和 x64)。 更新會使用 Windows ADK for Windows 10，其中包含 Windows PE 10。 與預設開機映像相關聯的檔案會隨最新版的 Configuration Manager 檔案更新。 站台不會自動更新自訂開機映像。 您必須手動更新包含舊版 Windows PE 的自訂開機映像。  

- 當您的站台階層包含採用不同 Configuration Manager 版本站台時，請避免使用動態媒體。 請改用以站台為基礎的媒體來連絡特定管理點。 將所有站台更新為相同版本的 Configuration Manager 之後，您可以再次使用動態媒體。

- 確認最新 Configuration Manager 開機映像包含您的自訂內容。 然後，使用最新版新開機映像來更新新版本站台的所有發佈點。  

### <a name="user-state-migration-tool-usmt"></a>使用者狀態移轉工具 (USMT)  

當頂層站台升級至最新版的 Configuration Manager 時，它會自動將預設的 USMT 套件更新為最新版本。 它不會自動更新任何自訂 USMT 套件。 您必須手動更新這些套件。  

### <a name="new-task-sequence-steps"></a>新的工作順序步驟  

新版的 Configuration Manager 會定期引入新的工作順序步驟。 當您依新步驟將工作順序部署到舊版的用戶端時，工作順序步驟會失敗。 請先確定目標集合中的用戶端已更新為新版本，再依新步驟部署工作順序。  

### <a name="os-deployment-media"></a>OS 部署方法  

當站台更新為新版本時，請使用新的 Configuration Manager 用戶端套件來更新所有媒體。 這些媒體類型包含可開機、擷取、預先設置及獨立。

### <a name="third-party-extensions-to-os-deployment"></a>OS 部署的協力廠商延伸模組  

當 OS 部署具有協力廠商延伸模組，且您有不同版本的 Configuration Manager 站台或 Configuration Manager 用戶端時，延伸模組可能會發生問題。  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>混合階層中的最新版 Configuration Manager 站台  

當您將站台升級為最新版 Configuration Manager 時，參照預設用戶端安裝套件的工作順序會自動開始部署最新 Configuration Manager 用戶端版本。

參照自訂用戶端安裝套件的工作順序會繼續部署該自訂套件中所包含用戶端版本。 自訂套件可能會包含舊版的 Configuration Manager 用戶端。 若要避免工作順序部署失敗，請將任何自訂的用戶端安裝套件更新為最新版本。

當您設定工作順序以使用自訂用戶端安裝套件時，請執行下列其中一個動作：

- 更新工作順序步驟，以使用最新 Configuration Manager 版本的用戶端安裝套件
- 更新自訂套件，以使用最新的 Configuration Manager 用戶端安裝來源

> [!IMPORTANT]  
> 請勿將參照最新 Configuration Manager 用戶端安裝套件的工作順序，部署到舊版 Configuration Manager 站台的用戶端。 當指派給舊版 Configuration Manager 站台的用戶端升級為最新的 Configuration Manager 用戶端版本時，Configuration Manager 會封鎖舊版 Configuration Manager 站台的用戶端。 這些用戶端不再指派給任何站台。 直到您手動將用戶端指派給最新的 Configuration Manager 站台，或在電腦上重新安裝舊版的 Configuration Manager 用戶端為止，這些用戶端會維持非受控狀態。


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>混合階層中的舊版 Configuration Manager  

當您將管理中心網站升級至最新版本的 Configuration Manager 時，請確定您所部署的 OS 部署工作順序不會讓這些用戶端處於非受控狀態。 例如，如果您部署到指派給舊版 Configuration Manager 站台 (您尚未升級至最新版本的 Configuration Manager) 的用戶端。

請複製您用來部署到最新版本 Configuration Manager 站台之用戶端的工作順序。 然後，修改工作順序，讓您能夠將它部署到舊版 Configuration Manager 站台的用戶端。 設定工作順序以參照使用舊版 Configuration Manager 用戶端安裝來源的自訂用戶端安裝套件。 如果沒有參照舊版 Configuration Manager 用戶端安裝來源的自訂用戶端安裝套件，則請手動建立一份。  

> [!Important]  
> 從 1902 版開始，您無法將套件或工作順序部署至用戶端版本 5.7730 或更早版本。 若要解決此限制，請將用戶端升級至較新版本。<!-- SCCMDocs-pr issue #3493 -->
