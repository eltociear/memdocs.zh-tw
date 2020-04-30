---
title: Updates Publisher
titleSuffix: Configuration Manager
description: 使用 System Center Updates Publisher 以管理自訂更新
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700026"
---
# <a name="system-center-updates-publisher"></a>System Center 更新發行者

適用於：  System Center Updates Publisher

System Center Updates Publisher (Updates Publisher) 是一個獨立的工具，可讓獨立軟體廠商或企業營運應用程式開發人員管理自訂更新。 這項自訂更新管理包含具有相依性的更新，例如驅動程式和更新套件組合。

Updates Publisher 可用於：

-   從外部目錄 (非 Microsoft 的更新目錄) 匯入更新。
-   修改更新定義，包括適用性及部署中繼資料。
-   將更新匯出至外部目錄。
-   將更新發行至更新伺服器。

將更新發行到更新伺服器之後，您便可以使用 Configuration Manager 來偵測那些更新，並將它們部署至受控裝置。

## <a name="workspaces"></a>工作區
當您開啟 Updates Publisher 時，預設會顯示 [更新工作區]  的 [概觀] 節點。

![Updates Publisher 主控台](media/console1.png)


Updates Publisher 具有四個工作區來協助整理其功能。


**更新工作區**：使用此工作區來[建立](create-updates-with-updates-publisher.md)及[管理](manage-updates-with-updates-publisher.md)軟體更新和更新套件組合。 此工作區包括指派更新與套件組合到發行集、發行並匯出到另一個 Updates Publisher 存放庫。

**發行集工作區**：此工作區是您[管理發行集](updates-publisher-publications.md)的位置。 發行集是您所建立之更新的群組，以簡化更新的匯出及發行。

管理發行集包括將更新發行到伺服器，來讓用戶端可以尋找並安裝更新、匯出更新和配套以供另一個 Updates Publisher 安裝使用，或是修改發行集的內容或詳細資料。

**規則工作區**：您可以在此處[管理適用性規則](updates-publisher-applicability-rules.md)並儲存它們，然後搭配您部署的更新使用。 規則有兩種：

-   可安裝的規則 - 這些規則可協助判斷用戶端是否應安裝更新。
-   已安裝的規則 - 這些規則會驗證更新是否已安裝。

**目錄工作區**：使用此工作區來新增及[管理軟體更新目錄](updates-publisher-catalogs.md)。 此工作區包含將軟體更新從那些目錄匯入到 Updates Publisher 存放庫。

## <a name="whats-new-in-system-center-updates-publisher"></a>System Center Updates Publisher 的新功能

>[!NOTE] 
> 最新版本的 System Center Updates Publisher 於 2019 年 11 月 6 日發行。 如需詳細資訊，請參閱[發行歷程記錄](#release-history)一節。

有新的撰寫模式 System Center Updates Publisher 可協助您撰寫更新。 啟用撰寫模式時，會將 [類別工作區]  新增至開始畫面。 撰寫模式啟用時，也會將新的 [Detectoid]  按鈕新增至 [更新工作區]  。

### <a name="to-enable-authoring-mode"></a>啟用撰寫模式

1. 在主控台左上角按一下 [Updates Publisher 屬性]   索引標籤，然後選擇 [選項]  。
1. 移至 [撰寫]  選項。
1. 核取 [啟用撰寫模式]  的方塊。

![啟用 Updates Publisher 的撰寫模式](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>關於類別工作區

類別工作區可讓更新作者組織隸屬於同類的更新。 例如，如果您是 OEM，您可能會想要根據模型或產品線來組織您的更新。 您可以定義多個類別和子類別，但無法定義第三層類別，因為您限用兩個層級。

![類別工作區的螢幕擷取畫面](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>將更新指派給類別

撰寫更新之後，您可以選取該更新，然後按一下 [分類]  按鈕，將其指派給類別。 您也可以用滑鼠右鍵按一下更新，然後選取 [分類]  。

![分類更新的螢幕擷取畫面](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>關於 Detectoid

啟用撰寫模式後，您可以建立更新的 Detectoid。 如果您有多個更新使用相同的規則 (或同一組規則) 來判斷適用性，Detectoid 將有其效用。 在這類情況下，您可以建立 Detectoid，並將其指派為更新的必要條件。 您可以將多個 Detectoid 指派給一個撰寫的更新。


### <a name="create-a-detectoid"></a>建立 Detectoid

1. 開啟 [更新工作區]  。
1. 在功能區中，按一下 [Detectoid]  按鈕。
1. 依照精靈中的提示建立您的 Detectoid。



![使用 Detectoid 的更新必要條件](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>版本歷程記錄

- [2019 RTW 6.0.394.0 版](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111)。 2019 年 11 月 6 日發佈
- [KB4462765 中的更新彙總套件 6.0.283.0 版](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher)。 發行日期：2018 年 9 月 7 日。
- [2017 RTW 6.0.276.0 版](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986)。 發行日期：2018 年 3 月 26 日。


## <a name="next-steps"></a>後續步驟
若要開始使用，請先[安裝](install-updates-publisher.md) Updates Publisher，然後[設定 Updates Publisher 的選項](updates-publisher-options.md)。
