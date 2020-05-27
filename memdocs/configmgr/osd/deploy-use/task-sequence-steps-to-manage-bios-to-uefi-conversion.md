---
title: 將 BIOS 轉換為 UEFI
titleSuffix: Configuration Manager
description: 了解如何自訂作業系統部署工作順序，為轉換至 UEFI 準備 FAT32 磁碟分割。
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0118dd448520a6f0c21bfeea5f8509bd8e49fd46
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429434"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>用於管理 BIOS 轉換到 UEFI 的工作順序步驟

Windows 10 提供許多新安全性功能，都需要啟用 UEFI 的裝置。 您可能擁有支援 UEFI、但使用傳統 BIOS 的較新 Windows 裝置。 在過去，將裝置轉換為 UEFI 需要您實際操作每部裝置，重新分割硬碟，並重新設定韌體。

使用 Configuration Manager，即可將下列動作自動化：

- 準備硬碟以將 BIOS 轉換為 UEFI
- 在就地升級的流程期間，將 BIOS 轉換為 UEFI
- 執行硬體清查時收集 UEFI 資訊

## <a name="hardware-inventory-collects-uefi-information"></a>硬體清查會收集 UEFI 資訊

硬體清查類別 (**SMS_Firmware**) 與屬性 (**UEFI**) 都可有助判斷電腦是否以 UEFI 模式啟動。 以 UEFI 模式啟動電腦時，**UEFI** 屬性設為 [TRUE]。 硬體清查預設會啟用此類別。 如需硬體清查的詳細資訊，請參閱[如何設定硬體清查](../../core/clients/manage/inventory/configure-hardware-inventory.md)。

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>建立自訂工作順序來準備硬碟

您可使用 **TSUEFIDrive** 變數來自訂作業系統部署工作順序。 [重新啟動電腦] 步驟會在硬碟上準備 FAT32 磁碟分割，以便執行轉換為 UEFI。 下列程序可提供範例，說明如何建立工作順序步驟，以執行此動作。

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>準備用於轉換為 UEFI 的 FAT32 磁碟分割

在安裝作業系統的現有工作順序中，新增包含執行將 BIOS 轉換為 UEFI 其步驟的新群組。

1. 在擷取檔案和設定的步驟之後，並在安裝作業系統的步驟之前，建立新工作順序群組。 例如，在 [擷取檔案和設定] 之後，建立名為 **BIOS-to-UEFI** 的群組。

1. 在新群組的 [選項] 索引標籤中，新增工作順序變數作為條件。 設定 [_SMSTSBootUEFI 不等於 True]。 在此情況下，工作順序只會在 BIOS 裝置上執行這些步驟。

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="BIOS 轉換為 UEFI 群組的條件":::

1. 在新群組底下，新增 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [已選取指派給此工作順序的開機映像]。 此動作會在 Windows PE 中重新啟動電腦。

1. 在 [選項] 索引標籤上，新增工作順序變數作為條件。 設定 [_SMSTSInWinPE 等於 False]。 在此情況下，如果電腦已經在 Windows PE 中，工作順序就不會執行此步驟。

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="重新啟動電腦步驟的條件":::

1. 新增啟動 OEM 工具的步驟，以將韌體從 BIOS 轉換為 UEFI。 此步驟通常為 [執行命令列]，並具有執行 OEM 工具的命令。

1. 新增 [格式化和分割磁碟] 工作順序步驟。 在此步驟中設定下列選項：

    1. 在安裝作業系統之前，請先建立 FAT32 磁碟分割以轉換為 UEFI。 選擇 [GPT] 作為 [磁碟類型]。

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="格式化與分割磁碟設定步驟":::

    1. 移至 FAT32 的 [磁碟分割內容]。 在 [變數] 欄位中，輸入 `TSUEFIDrive`。 當工作順序偵測到此變數時，便會準備供 UEFI 轉換的磁碟分割，然後重新啟動電腦。

        :::image type="content" source="media/partition-properties.png" alt-text="FAT32 磁碟分割屬性設定":::

    1. 建立工作順序用來儲存其狀態及存放記錄檔的 NTFS 磁碟分割。

1. 新增另一個 [重新啟動電腦] 工作順序步驟。 在 [指定重新啟動後執行的項目] 中，選取 [指派給此工作順序的開機映像] 以在 Windows PE 中啟動電腦。

    > [!TIP]
    > 根據預設，EFI 磁碟分割大小為 500 MB。 在某些環境中，會因為開機映像太大而無法儲存在此磁碟分割上。 若要解決此問題，請增加 EFI 磁碟分割的大小。 例如，將其設定為 1 GB。<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a> 在就地升級期間將 BIOS 轉換為 UEFI

Windows 10 包含簡單的轉換工具，**MBR2GPT**。 此工具會針對已啟用 UEFI 的硬體來自動重新分割硬碟。 您可將此轉換工具整合至 Windows 10 的就地升級流程中。 將升級工作順序、以及可將韌體從 BIOS 轉換為 UEFI 的 OEM 工具與此工具結合在一起。

### <a name="requirements"></a>需求

- 支援的 Windows 10 版本
- 支援 UEFI 的電腦
- 可將電腦韌體從 BIOS 轉換至 UEFI 的 OEM 工具

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>在就地升級工作順序期間將 BIOS 轉換為 UEFI 的流程

1. [建立工作順序以升級 OS](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. 編輯工作順序。 在 [後續處理] 群組中，進行下列變更：

    1. 新增 [執行命令列] 步驟。 指定 MBR2GPT 工具的命令列。 在完整作業系統中執行時，請將其設定為將磁碟從 MBR 轉換為 GPT，而不修改或刪除資料。 在**命令列**中，輸入下列命令：`MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > 您也可以選擇在 Windows PE (而非完整作業系統) 中執行 MBR2GPT.EXE 工具。 在執行 MBR2GPT.EXE 工具的步驟之前，請新增將電腦重新啟動為 Windows PE 的步驟。 然後從命令列中移除 **/AllowFullOS** 選項。

    如需工具與可用選項的詳細資訊，請參閱 [MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt) (機器翻譯)。

    1. 新增執行 OEM 工具的步驟，以將韌體從 BIOS 轉換為 UEFI。 此步驟通常為 [執行命令列]，並具有執行 OEM 工具的命令列。

    1. 新增 [重新啟動電腦] 步驟，然後選取 [目前安裝的預設作業系統]。

1. 部署工作順序。
