---
title: OS 部署的使用者體驗
titleSuffix: Configuration Manager
description: 了解使用者體驗，例如 Configuration Manager 中適用於作業系統部署的工作順序進度和媒體精靈。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5f92e76047a70f6d86406b1a364603163d902e62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703216"
---
# <a name="user-experiences-for-os-deployment"></a>OS 部署的使用者體驗

適用於：  Configuration Manager (最新分支)

在[部署工作順序](../deploy-use/deploy-a-task-sequence.md)之後，視案例而定，使用者可以透過不同的方式與部署互動。 本文說明 OS 部署的主要使用者體驗，以及如何加以設定：

- 適用於高影響力部署的軟體中心使用者通知
- 範例 PXE 開機體驗
- 媒體中的工作順序精靈
- 工作順序執行時的進度視窗
- 工作順序失敗時的錯誤視窗

## <a name="software-center"></a>軟體中心

針對高影響力部署，可自訂軟體中心所顯示的訊息。 當使用者在軟體中心開啟 OS 部署時，會看到類似下列視窗的訊息：

![軟體中心發給終端使用者的自訂工作順序通知](../media/user-notification-enduser.png)

如需如何在此視窗中自訂訊息的詳細資訊，請參閱[建立高風險部署的自訂通知](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments)。

您也可以在視窗頂端自訂組織名稱。 (上述範例顯示預設值 `IT Organization`)。 變更 [電腦代理程式]  群組中的 [組織名稱]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#computer-agent)。

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

如需詳細資訊，請參閱[使用軟體中心透過網路部署 Windows](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md)。

## <a name="pxe"></a>PXE

不同的硬體型號有不同 PXE 體驗。 若要開機進入網路，UEFI 型裝置通常會使用 `Enter` 鍵，而 BIOS 型裝置則會使用 `F12` 鍵。

下列範例顯示 Hyper-V Gen1 (BIOS) PXE 體驗：

![Hyper-V 虛擬機器的範例 BIOS PXE 畫面](media/hyperv-pxe.png)

裝置透過 PXE 成功開機之後，其行為類似於可開機媒體。 如需詳細資訊，請參閱下一節的[工作順序精靈](#task-sequence-wizard)。

如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。

> [!WARNING]
> 如果您使用 PXE 部署，並以網路介面卡作為第一個開機裝置來設定裝置硬體，則這些裝置就可以自動啟動 OS 部署工作順序，而不需要使用者互動。 部署驗證不會管理此設定。 雖然此設定可以簡化處理程序並減少使用者互動，但會將裝置置於意外重新安裝映像的更高風險中。

## <a name="task-sequence-wizard"></a>工作順序精靈

當使用[工作順序媒體](../deploy-use/create-task-sequence-media.md)時，會執行工作順序精靈來引導處理程序。

### <a name="welcome-to-the-task-sequence-wizard"></a>歡迎使用工作順序精靈

![[工作順序精靈] 主頁面的螢幕擷取畫面](media/welcome-task-sequence-wizard.png)

- 如果以密碼來保護媒體，則使用者必須在此歡迎頁面上輸入密碼。

- 選取 [設定網路設定]  來指定靜態 IP 位址或其他自訂網路設定。 否則，裝置預設會使用 DHCP。

- 如果網路需要 Proxy，請選取 [設定 Proxy 設定]  。

### <a name="select-a-task-sequence-to-run"></a>選取要執行的工作順序

如果將一個以上的工作順序部署到裝置，即會看到可選取工作順序的這個頁面。 請務必針對工作順序採用使用者可以了解的名稱和描述。

![[工作順序精靈] 的工作順序選取頁面螢幕擷取畫面](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>編輯工作順序變數

如果任何工作順序變數具有空白值，則精靈會顯示一個頁面來編輯變數值。

![[工作順序精靈] 的 [編輯工作順序變數] 頁面螢幕擷取畫面](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>啟動前置命令

您可自訂工作順序媒體或開機映像，以執行啟動前置命令。 啟動前置命令會在工作順序開始之前執行。 以下是一些較常見的動作：

- 提示使用者輸入動態值，例如電腦名稱
- 指定網路設定
- 設定使用者裝置親和性

啟動前置命令是以指令碼或程式所指定的命令列。 使用者體驗對該指令碼或程式而言是唯一的。

如需詳細資訊，請參閱下列文章：

- [工作順序媒體的啟動前置命令](prestart-commands-for-task-sequence-media.md)
- [管理開機映像](../get-started/manage-boot-images.md#customization)
- [工作順序媒體](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>工作順序進度

當執行工作順序時，其會顯示 [安裝進度]  視窗：

![工作順序進度視窗的範例](media/task-sequence-progress.png)

- 此視窗一律位在最上方；可移動此視窗，但無法關閉或將其最小化。

- 可在視窗頂端自訂組織名稱。 (上述範例顯示預設值 `IT Organization`)。 變更 [電腦代理程式]  群組中的 [組織名稱]  用戶端設定。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md#computer-agent)。

    > [!TIP]
    > 工作順序會將此值儲存在唯讀變數 [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName) 中。

- 您可自訂次標題。 (上述範例顯示預設值 `Running: <task sequence name>`。)在工作順序的屬性上，選取 [使用自訂文字]  的選項作為進度通知文字。 最多允許使用 255 個字元。

- **執行動作**：第一行顯示目前工作順序步驟的名稱。 其底下的進度列會顯示工作順序整體完成情況。

- 第二行僅顯示提供更詳細進度的一些步驟。

- 使用工作順序變數 [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) 來控制工作順序顯示進度的時間。

    若要完全停用進度視窗，請在工作順序部署的 [使用者體驗]  頁面上，停用 [顯示工作順序進度]  的選項。

從 2002 版開始，工作順序進度視窗包含下列改善：<!--5932692-->

- 顯示目前的步驟編號、步驟總數和完成百分比

- 增加視窗的寬度來提供更多的空間，以在單一行中顯示完整的組織名稱

![範例工作順序進度視窗](media/2356386-task-sequence-progress.png)

根據預設，工作順序進度視窗會使用現有的文字。 如果未進行任何變更，則其工作方式會與 1910 版和更早版本相同。 若要顯示新的進度資訊，請指定工作順序變數 [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel)。

已完成的計數與百分比僅供一般指引之用。 這些值是以工作順序中的步驟總數為基礎。 若是所含步驟會根據工作順序邏輯按條件執行的更複雜工作順序，則進度可能不是線性的。

總步驟的計數不會在工作順序中包含下列項目：

- 群組。 此項目為其他步驟的容器，而不是步驟本身。

- [執行工作順序]  步驟的執行個體。 此步驟為其他步驟的容器。

- 您明確停用的步驟。 已停用的步驟不會在工作順序期間執行。

    > [!NOTE]
    > 仍然會將已停用群組中的已啟用步驟包含在總計數中。

## <a name="task-sequence-error"></a>工作順序錯誤

如果工作順序失敗，則會顯示 [工作順序錯誤]  視窗。

![範例工作順序錯誤視窗](media/task-sequence-error.png)

- 您可自訂標頭資訊，這與工作順序進度視窗相同。

- 此視窗會顯示工作順序的名稱、錯誤碼，以及使用者的一般訊息。 例如：`Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- 視窗會在逾時時間之後自動關閉。 此逾時預設為 15 分鐘。 您可使用工作順序變數 [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout) 來自訂此值。
