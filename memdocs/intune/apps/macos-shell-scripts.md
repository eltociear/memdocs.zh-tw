---
title: 在 Microsoft Intune 的 macOS 裝置上使用 Shell 指令碼 | Microsoft Docs
description: 在 Microsoft Intune 中，針對 macOS 裝置建立、指派、監視和疑難排解 Shell 指令碼。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba099e3614c11e10ce4cd9ae94668a1648bfc150
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808048"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>在 Intune 的 macOS 裝置上使用 Shell 指令碼 (公開預覽)

> [!NOTE]
> 適用於 macOS 裝置的 Shell 指令碼目前為預覽狀態。 使用這項功能之前，請先參閱[預覽中的已知問題](macos-shell-scripts.md#known-issues)清單。

在 Intune 中使用 Shell 指令碼來擴充裝置管理功能，超越 macOS 作業系統所支援的功能。 

## <a name="prerequisites"></a>先決條件
撰寫 Shell 指令碼並將其指派給 macOS 裝置時，請確定符合下列必要條件。 
 - 裝置執行 macOS 10.12 或更新版本。
 - 裝置是由 Intune 管理。 
 - Shell 指令碼以 `#!` 為開頭，且必須在有效的位置，例如 `#!/bin/sh` 或 `#!/usr/bin/env zsh`。
 - 已安裝適用 Shell 的命令列解譯器。

## <a name="important-considerations-before-using-shell-scripts"></a>使用 Shell 指令碼之前的重要考慮
 - Shell 指令碼需要在 macOS 裝置上成功安裝 Microsoft Intune MDM 代理程式。 如需詳細資訊，請參閱[適用於 macOS 的 Microsoft Intune MDM 代理程式](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos)。
 - Shell 指令碼會以平行方式在裝置上以個別的處理序執行。
 - 以登入使用者身分執行的 Shell 指令碼會在執行時，針對裝置上所有目前登入的使用者帳戶執行。
 - 終端使用者必須登入裝置，才能以登入使用者身分執行指令碼。
 - 如果指令碼需要進行標準使用者帳戶無法進行的變更，則需要根使用者權限。
 - 在某些情況下，Shell 指令碼會嘗試比所選的指令碼頻率更頻繁地執行，例如磁碟已滿、儲存位置遭到修改、本機快取遭到刪除，或 Mac 裝置重新開機。
 
## <a name="create-and-assign-a-shell-script-policy"></a>建立並指派 Shell 指令碼原則
1. 登入 [Microsoft 端點管理員系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 選取 [裝置]   > [macOS]   > [指令碼]   > [新增]  。
3. 在 [基本資訊]  中，輸入下列內容，然後選取 [下一步]  ：
   - **名稱**：輸入 Shell 指令碼的名稱。
   - **描述**：輸入 Shell 指令碼的描述。 這是選擇性設定，但建議執行。
4. 在 [指令碼設定]  中，輸入下列內容，然後選取 [下一步]  ：
   - **上傳指令碼**：瀏覽至 Shell 指令碼。 指令碼檔案的大小必須小於 200 KB。
   - **以登入使用者身分執行指令碼**：選取 [是]  以使用裝置上的使用者認證來執行指令碼。 選擇 [否]  (預設) 以根使用者身分執行指令碼。 
   - **在裝置上隱藏指令碼通知：** 根據預設，會針對每個執行的指令碼顯示指令碼通知。 終端使用者會在 MacOS 裝置上從 Intune 看到「IT 正在設定您的電腦」  通知。
   - **指令碼頻率：** 選取指令碼的執行頻率。 選擇 [未設定]  \(預設\)，只執行一次指令碼。
   - **指令碼失敗時可重試的最大次數：** 選取指令碼傳回非零結束代碼 (零表示成功) 時，應該執行的次數。 選擇 [未設定]  \(預設\) 以在指令碼失敗時不重試。
5. 在 [範圍標籤]  中，選擇性地為指令碼新增範圍標籤，然後選取 [下一步]  。 您可使用範圍標籤來決定可在 Intune 中看見指令碼的人員。 如需範圍標籤的完整詳細資料，請參閱[針對分散式 IT 使用角色型存取控制和範圍標籤](../fundamentals/scope-tags.md)。
6. 選取 [指派]   > [選取要包含的群組]  。 Azure AD 群組的現有清單會隨即顯示。 選取一或多個裝置群組，其包含 macOS 裝置要接收指令碼的使用者。 選擇 [選取]  。 選擇的群組會顯示在清單中，且會接收指令碼原則。
   > [!NOTE]
   > - Intune 中的 Shell 指令碼只能指派給 Azure AD 裝置安全性群組。 預覽中不支援使用者群組指派。 
   > - 更新 Shell 指令碼的指派，也會更新[適用於 macOS 的 Microsoft Intune MDM 代理程式](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos)指派。
7. 在 [檢閱 + 新增]  中，會顯示您設定的設定摘要。 選取 [新增]  以儲存此指令碼。 選取 [新增]  時，會將指令碼原則部署到選擇的群組。

所建立的應用程式現在會出現在指令碼清單中。 

## <a name="monitor-a-shell-script-policy"></a>監視 Shell 指令碼原則
您可選擇下列其中一種報告，以監視使用者和裝置所有指派指令碼的執行狀態：
- [指令碼]   > **選取要監視的指令碼** > [裝置狀態] 
- [指令碼]   > **選取要監視的指令碼** > [使用者狀態] 

>[!IMPORTANT]
> 不論選取的 [指令碼頻率]  為何，只有在第一次執行指令碼時，才會報告指令碼執行狀態。 在後續執行時，指令碼執行狀態不會更新。 不過，更新的指令碼會視為新指令碼，且會再次報告執行狀態。

指令碼執行之後，就會傳回下列其中一個狀態：
- 指令碼執行狀態 [失敗]  表示指令碼傳回非零的結束代碼，或指令碼的格式不正確。 
- 指令碼執行狀態 [成功]  表示指令碼傳回的結束代碼為零。 

## <a name="frequently-asked-questions"></a>常見問題集
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>為什麼指派的 Shell 指令碼未在裝置上執行？
可能原因如下：
* 代理程式可能需要簽入，才能接收新的或已更新指令碼。 此簽入程序會每 8 小時發生一次，且與 MDM 簽入不同。 請確定裝置處於喚醒狀態，且已連線到網路，以順利完成代理程式簽入，並等候代理程式簽入。
* 可能未安裝代理程式。 檢查代理程式是否安裝在 macOS 裝置上的 `/Library/Intune/Microsoft Intune Agent.app`。
* 代理程式可能不是處於健全狀態。 代理程式會嘗試復原 24 小時、將自己移除，並在仍指派 Shell 指令碼的情況下重新安裝。

### <a name="how-frequently-is-script-run-status-reported"></a>指令碼執行狀態的報告頻率為何？
當指令碼執行完成時，就會將指令碼執行狀態回報給 Microsoft Endpoint Manager 系統管理主控台。 如果指令碼排定以設定的頻率定期執行，則只會在第一次執行時報告狀態。

### <a name="when-are-shell-scripts-run-again"></a>何時會再次執行 Shell 指令碼？
只有在已設定 [指令碼失敗時可重試的最大次數]  設定，且指令碼在執行時失敗，才會再次執行指令碼。 如果未設定 [指令碼失敗時可重試的最大次數]  ，且指令碼在執行時失敗，則不會再次執行，且執行狀態會回報為 [失敗]  。 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Shell 指令碼需要什麼 Intune 角色權限？
指派的 Intune 角色需要 [裝置設定]  權限，才能刪除、指派、建立、更新或讀取 Shell 指令碼。

## <a name="microsoft-intune-mdm-agent-for-macos"></a>適用於 macOS 的 Microsoft Intune MDM 代理程式
 ### <a name="why-is-the-agent-required"></a>為什麼需要代理程式？
 Microsoft Intune MDM 代理程式必須安裝在受控 macOS 裝置上，才能啟用原生 macOS 作業系統不支援的進階裝置管理功能。
 
 ### <a name="how-is-the-agent-installed"></a>如何安裝代理程式？
 代理程式會自動以無訊息方式安裝在受 Intune 管理的 macOS 裝置上，您可在 Microsoft Endpoint Manager 系統管理中心為其指派至少一個 Shell 指令碼。 代理程式會在適用時安裝在 `/Library/Intune/Microsoft Intune Agent.app`，且不會出現在 macOS 裝置上的 [搜尋工具]   > [應用程式]  中。 在 macOS 裝置上執行時，代理程式會在 [活動監視器]  中顯示為 `IntuneMdmAgent`。

### <a name="what-does-the-agent-do"></a>代理程式有哪些功能？
 - 代理程式會在簽入以接收 macOS 裝置的已指派 Shell 指令碼之前，以無訊息方式向 Intune 服務進行驗證。
 - 代理程式會接收已指派 Shell 指令碼，並根據系統管理員所設定的設定排程、重試嘗試、通知設定和其他設定來執行指令碼。
 - 代理程式通常每 8 小時會使用 Intune 服務來檢查新的或已更新指令碼。 此簽入程序與 MDM 簽入無關。 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>如何從 Mac 手動起始代理程式簽入？
在已安裝代理程式的受控 Mac 上，開啟**終端機**，執行 `sudo killall IntuneMdmAgent` 命令以終止 `IntuneMdmAgent` 處理序。 `IntuneMdmAgent` 處理序會立即重新啟動，這將會起始 Intune 的簽入。

或者，您可以執行下列動作：
1. 開啟 [活動監視器]   > [檢視]   > 選取 [所有處理序]  。  
2. 搜尋名為 `IntuneMdmAgent` 的處理序。 
3. 結束為 **root** 使用者執行的處理序。 

> [!NOTE]
> 公司入口網站中的**檢查設定**動作，以及 Microsoft 端點管理員管理主控台中裝置的**同步處理**動作，會起始 MDM 簽入，而不會強制代理程式簽入。

 ### <a name="when-is-the-agent-removed"></a>何時會移除代理程式？
 有幾個情況可能會導致代理程式從裝置中移除，例如：
 - Shell 指令碼不再指派給裝置。 
 - macOS 裝置不再受控。
 - 代理程式處於無法復原的狀態超過 24 小時 (裝置喚醒時間)。

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>如何關閉傳送給 Microsoft 的 Shell 指令碼使用量資料？
 若要關閉從 Intune MDM 代理程式傳送給 Microsoft 的使用量資料，請開啟公司入口網站並選取 [功能表]   > [偏好設定]   > 取消核取 [允許 Microsoft 收集使用量資料]  。 這會關閉針對 Intune MDM 代理程式和公司入口網站傳送的使用量資料。

## <a name="known-issues"></a>已知問題
- **使用者群組指派：** 指派給使用者群組的 Shell 指令碼不適用於裝置。 預覽中目前不支援使用者群組指派。 使用裝置群組指派來指派指令碼。
- **收集記錄檔：** 可看見「收集記錄檔」動作。 但嘗試記錄檔收集時，它顯示「發生錯誤」且未擷取記錄檔。 預覽中目前不支援記錄檔收集。
- **沒有指令碼執行狀態：** 雖然不太可能發生，但如果在裝置上收到指令碼，且裝置在回報執行狀態之前就離線，則裝置將不會在系統管理主控台中報告指令碼的執行狀態。
- **使用者狀態報告：** 有空白的報告問題存在。 在 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)內，選取 [監視器]  。 [使用者狀態] 會顯示空白的報告。

## <a name="next-steps"></a>後續步驟

- [在 Microsoft Intune 中建立合規性政策](..\protect\create-compliance-policy.md)
