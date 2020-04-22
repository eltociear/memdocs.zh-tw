---
title: 電腦分析中的資產
titleSuffix: Configuration Manager
description: 了解電腦分析中的裝置、驅動程式和應用程式。
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706646"
---
# <a name="assets-in-desktop-analytics"></a>電腦分析中的資產

當裝置向電腦分析回報資料之後，即會提供下列資產的清查：

- 裝置
- 已安裝的應用程式  

在服務入口網站中，選取 [電腦分析] 功能表中的 [資產]  。

## <a name="devices"></a>裝置

[裝置]  索引標籤會顯示組織中已向電腦分析註冊的所有裝置重要資訊。 您可以依任何資料行排序，或針對特定值篩選。

> [!NOTE]  
> 如果儀表板回報的環境裝置數目不如預期，請參閱[針對電腦分析進行疑難排解](troubleshooting.md)。  

在部署計劃中有更多關於裝置的詳細資料。 如需詳細資訊，請參閱[規劃資產](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>應用程式

[應用程式]  索引標籤會顯示服務在您 Windows 裝置中偵測到的所有已安裝應用程式。

**值得注意**的應用程式已安裝在 2% 已註冊裝置上。

藉由設定下列類別之一來設定應用程式的 [重要性]  ：

- 重大
- 重要
- 忽略
- 未檢閱
- 不重要<!-- 3587232 -->

從清單中選取應用程式，然後選取 [編輯]  。 此動作會顯示應用程式的詳細資料。 選取 [重要性]  下拉式功能表並設定值。 您也可以指派**擁有者**。 如要變更，請選取 [儲存]  。

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> 系統和 Store 應用程式的自動升級決策

<!-- 3587232 -->
識別**重要性**和**升級決策**對電腦分析工作流程中所有值得注意的應用程式而言至關重要。 為有助於簡省您批註這些應用程式的精力，某些類型的應用程式會自動標示為 [不重要]  。 這些應用程式的部署計劃升級決策也會標示為 [就緒]  。 下列應用程式皆相容，而且在您升級 Windows 之後應可繼續運作：

- Microsoft 發佈的系統應用程式和元件

- 在 Microsoft Store 中管理和更新的應用程式

> [!TIP]
> 在全域層級或依每個部署計劃管理任何應用程式的輸入。
>
> 1. 在電腦分析入口網站的 [管理]  功能表中，選取 [資產]  。 然後選取 [應用程式]  。
>
> 2. 使用 [類型]  和 [類別]  欄管理這些應用程式類別：
>
>    - 篩選出 [類型]  為 [現代化]  的 Store 應用程式
>    - 篩選 [類別]  為 [背景程序]  或 [Windows 元件]  的系統應用程式

在部署計劃中，您也可以設定**升級決策**。 如需詳細資訊，請參閱[規劃資產](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>使用方式

<!-- 5533890 -->

- **安裝數總計**：這個值是所選應用程式安裝在所有電腦分析註冊裝置上的數目。

- **安裝百分比**：這個值是所選應用程式安裝在所有電腦分析註冊裝置上的百分比。

- **過去 30 天曾啟動此應用程式的裝置**：這個值是使用者啟動所選應用程式的裝置計數。 此值只包含過去 30 天回報使用量的裝置。 此計數包含您所有向電腦分析註冊的裝置，但限於在任何 Windows 10 版本執行的電腦分析。 此計數可能會因部署計劃而有所不同。

## <a name="next-steps"></a>後續步驟

- [了解電腦分析部署計劃](about-deployment-plans.md)  

- [了解安全性和功能更新](about-updates.md)  

- [電腦分析中的相容性評定](compat-assessment.md)  
