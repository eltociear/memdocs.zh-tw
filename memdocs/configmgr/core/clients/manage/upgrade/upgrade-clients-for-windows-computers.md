---
title: 升級 Windows 用戶端
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中升級 Windows 電腦上的用戶端。
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b0a69b07a3be633434203f93b0724cec4ea88a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347131"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>如何在 Configuration Manager 中升級 Windows 電腦的用戶端

適用於：Configuration Manager (最新分支)

您可以使用用戶端安裝方法或自動用戶端升級功能，升級 Windows 電腦上的 Configuration Manager 用戶端。 下列用戶端安裝方法可有效地在 Windows 電腦上升級用戶端軟體：  

- 群組原則安裝  

- 登入指令碼安裝  

- 手動安裝  

- 升級安裝  

如需詳細資訊，請參閱[如何將用戶端部署至 Windows 電腦](../../deploy/deploy-clients-to-windows-computers.md)。

您可以指定排除集合來排除用戶端不進行升級。 如需詳細資訊，請參閱[如何排除用戶端不進行升級](exclude-clients-windows.md)。 排除的用戶端仍會下載並執行 CCMSETUP，但不會升級。

> [!TIP]  
> 如果您從舊版的 Configuration Manager 升級伺服器基礎結構，請先完成伺服器升級，再升級 Configuration Manager 用戶端。 此程序包括安裝所有最新分支更新。 最新的最新分支更新包含最新版本用戶端。 請先安裝所有 Configuration Manager 更新，再升級用戶端。

> [!NOTE]
> 如果您想要在升級期間重新指派用戶端的站台，請使用 `SMSSITECODE` client.msi 屬性來指定新站台。 如果您針對 `SMSSITECODE` 使用 `AUTO` 值，請同時指定 `SITEREASSIGN=TRUE`。 此屬性可讓系統在升級期間自動重新指派站台。 如需詳細資訊，請參閱[用戶端安裝屬性 - SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode)。

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a> 關於自動用戶端升級

將站台設定為自動將用戶端升級至最新的 Configuration Manager 版本。 當 Configuration Manager 識別出指派用戶端的版本比階層版本更早時，它會自動升級用戶端。 此案例包含當用戶端嘗試指派至 Configuration Manager 站台時，會將用戶端升級至最新版本。  

用戶端可以在下列情況自動升級：  

- 用戶端版本比階層中使用的版本更早。  

- 管理中心網站 (CAS) 上的用戶端已安裝語言套件，現有用戶端則沒有安裝。  

- 階層中的用戶端必要條件，與用戶端上安裝的版本不同。  

- 有一或多個用戶端安裝檔案的版本不同。  

> [!NOTE]  
> 若要識別您階層中不同版本的 Configuration Manager 用戶端，請使用 [站台 - 用戶端資訊] 報告資料夾中的 [依用戶端版本列出的 Configuration Manager 用戶端計數] 報告。  

Configuration Manager 預設會建立升級套件。 它會自動將套件傳送至階層中的所有發佈點。 如果您對 CAS 上的用戶端套件進行變更，Configuration Manager 會自動更新套件，並重新發佈它。 範例變更如：新增用戶端語言套件。 如果您已啟用自動用戶端升級，則每個用戶端都會自動安裝新的用戶端語言套件。

在您的整個階層啟用自動用戶端升級。 此設定可讓您的用戶端以較少的投入量來保持最新狀態。  

如果您也將 Configuration Manager 站台系統當作用戶端來管理，請決定是否要將它們包含在自動升級程序中。 您可以將所有伺服器或特定集合從用戶端升級中排除。 某些 Configuration Manager 站台角色會共用用戶端架構。 例如，管理點和提取發佈點。 當您更新站台時，這些角色會升級，因此這些伺服器上的用戶端版本會同時更新。

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a> 設定自動用戶端升級

使用下列程序，設定在 CAS 的自動用戶端升級。 此設定適用於您階層中的所有用戶端。  

1. 在 Configuration Manager 主控台中，移至 [系統管理] 工作區，展開 [站台設定]，然後選取 [站台] 節點。  

1. 在功能區 [常用] 索引標籤的 [站台] 群組中，選取 [階層設定]。  

1. 切換至 [用戶端升級] 索引標籤。檢閱生產用戶端的版本和日期。 請確定它是您要用來升級用戶端的版本。 如果它不是您預期的用戶端版本，您可能需要將生產前用戶端升階為生產用戶端。 如需詳細資訊，請參閱[如何測試進入生產階段前集合用戶端升級](test-client-upgrades.md)。  

1. 選取 [使用實際執行用戶端升級階層中的所有用戶端]。 選取 [確定] 來確認。  

1. 如果您不想要將用戶端升級套用至伺服器，選取 [不升級伺服器]。  

1. 指定裝置必須在幾天內升級用戶端。 裝置收到原則之後，它會在此天數內以隨機間隔升級用戶端。 此行為可防止大量用戶端同時升級。

    > [!NOTE]
    > 電腦必須處於執行中，才能升級用戶端。 如果電腦在排程要接收升級的時間未執行，則不會升級。 當電腦啟動並收到原則時，它會將升級排程在所允許天數內的隨機時間。 如果這在升級的天數到期之後發生，則會將升級排程在電腦啟動之後 24 小時內的任意時間。
    >
    > 基於這項行為，如果隨機排程的升級時間不在正常工作時間內，則會定時關機的電腦可能需要比預期時間更長的時間來升級。

1. 若要排除用戶端不進行升級，請選取 [排除指定的用戶端不進行升級]，並指定要排除的集合。 如需詳細資訊，請參閱[排除用戶端不進行升級](exclude-clients-windows.md)。

1. 如果您要站台將用戶端安裝套件複製到已經啟用[預先設置的內容](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)的發佈點，請選取 [將用戶端安裝套件自動發佈至針對預先設置內容啟用的發佈點]。  

1. 選取 [確定] 來儲存設定，然後關閉 [階層設定內容]。

用戶端接著下載原則時，就會收到這些設定。

> [!NOTE]
> 用戶端升級會遵循您所設定的任何 Configuration Manager 維護時段。 execmgr 執行緒只會在維護視窗期間執行用戶端安裝程式啟動程式 (ccmsetup.exe)。 如果裝置執行具有寫入篩選器的 Windows 版本，則 ccmsetup 會嘗試同時下載並安裝。 否則，ccmsetup 會隨機設定下載內容的時間。 在下載內容並編譯本機原則之後，execmgr 會在下一次維護視窗期間為用戶端升級進行排程。<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>後續步驟

如需升級用戶端的替代方法，請參閱[如何將用戶端部署至 Windows 電腦](../../deploy/deploy-clients-to-windows-computers.md)。

排除特定用戶端不進行自動升級。 如需詳細資訊，請參閱[如何排除用戶端不進行升級](exclude-clients-windows.md)。
