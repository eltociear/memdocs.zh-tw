---
title: 針對工作順序進行偵錯
titleSuffix: Configuration Manager
description: 使用工作順序偵錯工具來針對工作順序進行疑難排解。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66f460b7ba5c870a9ee81d10835ceb9f660cba89
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690606"
---
# <a name="debug-a-task-sequence"></a>針對工作順序進行偵錯

適用於：  Configuration Manager (最新分支)

<!--3612274-->

從 1906 版開始，工作順序偵錯工具是一種新的疑難排解工具。 您可以在偵錯模式中將工作順序部署至小型集合。 它可讓您以受控的形式逐步執行工作順序，協助進行疑難排解和調查。 偵錯工具目前是在與工作順序引擎相同的裝置上執行，其不是遠端偵錯工具。

> [!Note]  
> 在這個版本的 Configuration Manager 中，工作順序偵錯工具是發行前版本功能。 若要啟用此功能，請參閱[發行前版本功能](../../core/servers/manage/pre-release-features.md)。  


## <a name="prerequisites"></a>先決條件

- 更新目標裝置上的 Configuration Manager 用戶端

- 以本機**系統管理員**群組中的使用者身分登入目標裝置。 偵錯工具只能由系統管理員執行。

- 更新與工作順序建立關聯的開機映像，確保它具有最新的用戶端版本


## <a name="start-the-tool"></a>啟動工具

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫]  工作區，展開 [作業系統]  ，然後選取 [工作順序]  。

1. 選取工作順序。 在功能區的 [部署] 群組中，選取 [偵錯]  。

    > [!Tip]  
    > 除此之外也可將部署工作順序之目標集合或電腦物件的 **TSDebugMode** 變數設為 `TRUE`。 已設定此變數的任何裝置會將部署到其中的所有工作順序設為偵錯模式。

1. 建立偵錯部署。 部署設定與一般工作順序部署相同。 如需詳細資訊，請參閱 [Deploy a task sequence](deploy-a-task-sequence.md#process)。

    > [!Note]  
    > 您只能選取一個小型集合來進行偵錯部署。 只會顯示具有 10 個或更少成員的裝置集合。

從 1910 版開始，使用新的工作順序變數 **TSDebugOnError** 在工作順序傳回錯誤時自動啟動偵錯工具。<!-- 5012536 --> 如需詳細資訊，請參閱[工作順序變數 - TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError)。

## <a name="use-the-tool"></a>使用工具

當工作順序在裝置上運作時，[工作順序偵錯工具] 視窗隨即會開始，與下列螢幕擷取畫面相似：

![工作順序偵錯工具的螢幕擷取畫面](media/3612274-tsdebug.png)

偵錯工具包含下列控制項：

- **步驟**：從 [目前]  位置，僅執行工作順序中的下一個步驟。  

    > [!Note]  
    > 當工作順序處於偵錯模式時，如果步驟傳回嚴重錯誤，工作順序就不會正常失敗。 此行為可讓您選擇在進行外部變更之後重試步驟。

- **執行**：從 [目前]  位置，以一般方式執行工作順序直到結尾、下一個 [中斷]  點，或是當某個步驟失敗時。 使用此動作之前，請務必使用**設定中斷**動作來設定任何中斷點。

- **設為目前**：在偵錯工具中選取一個步驟，然後選取 [設為目前]  。 此動作會將 [目前]  指標移動到此步驟。 此動作可讓您跳過步驟，或是反向移動。  

    > [!Warning]  
    > 偵錯工具不會在您變更順序中目前位置時考慮步驟的類型。 某些步驟可能會設定稍後步驟條件評估所需的工作順序變數。 若未依順序執行，有些步驟可能會失敗，或對裝置造成重大的損害。 使用此選項時請自行承擔風風險。  

- **設定中斷**：在偵錯工具中選取一個步驟，然後選取 [設定中斷]  。 此動作會在偵錯工具中新增一個 [中斷]  點。 當您 [執行]  工作順序時，它會在 [中斷]  處停止。  

    - 使用**執行**動作之前，請先設定中斷點。

    - 從 1910 版開始，若您在偵錯工具中建立中斷點，然後工作順序重新啟動電腦，偵錯工具會在重新啟動之後維持您的中斷點。<!-- 5012509 -->

    - 在 1906 版中，電腦重新啟動之後就不會儲存中斷點，例如使用[重新啟動電腦](../understand/task-sequence-steps.md#BKMK_RestartComputer)步驟時。 例如，如果您從軟體中心針對映像工作順序啟動偵錯工具，請勿在 Windows PE 階段中設定中斷。 當電腦重新啟動至 Windows PE 時，偵錯工具會暫停工作順序，讓您可以設定中斷。

- **清除所有中斷**：移除所有中斷點。

- **記錄檔**：使用 [CMTrace](../../core/support/cmtrace.md)，開啟目前的工作順序記錄檔 **smsts.log**。 當工作順序引擎「正在等候偵錯工具」時，您可以看到記錄項目。

- **CMD 提示**：在 Windows PE 中，開啟命令提示字元。

- **取消**：關閉偵錯工具，讓工作順序失敗。

- **結束**：卸離和關閉偵錯工具，但是工作順序會繼續正常執行。

[工作順序變數]  視窗會顯示工作順序環境中所有變數目前的值。 如需詳細資訊，請參閱[工作順序變數](../understand/task-sequence-variables.md)。 如果您使用[設定工作順序變數](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)步驟，並且使用 [不要顯示此值]  選項，則偵錯工具不會顯示變數值。 您無法在偵錯工具中編輯變數值。

> [!Note]
> 某些工作順序變數僅供內部使用，不會列在參考文件中。

工作順序偵錯工具會在[重新啟動電腦](../understand/task-sequence-steps.md#BKMK_RestartComputer)步驟之後繼續執行，但是您必須重新建立任何中斷點。 雖然工作順序可能不需要中斷點，但是由於偵錯工具需要使用者互動，因此您必須登入 Windows 才能繼續。 如果您未在一小時內登入以繼續進行偵錯，工作順序就會失敗。

該作業也會逐步執行子工作順序，其中包含[執行工作順序](../understand/task-sequence-steps.md#child-task-sequence)步驟。 偵錯工具視窗會顯示子工作順序和主要工作順序的步驟。


## <a name="known-issues"></a>已知問題

如果您在多個部署中將一般部署和偵錯部署目標設為相同的裝置，則工作順序偵錯工具可能不會啟動。


## <a name="see-also"></a>請參閱

- [關於工作順序步驟](../understand/task-sequence-steps.md)
- [工作順序變數](../understand/task-sequence-variables.md)
- [如何使用工作順序變數](../understand/using-task-sequence-variables.md)
- [部署工作順序](deploy-a-task-sequence.md)
