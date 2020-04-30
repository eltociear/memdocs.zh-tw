---
title: 針對 Endpoint Protection 進行疑難排解
titleSuffix: Configuration Manager
description: 了解如何為 Windows Defender 和 Endpoint Protection 問題進行疑難排解。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709416"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>針對 Windows Defender 或 Endpoint Protection 用戶端進行疑難排解

適用於：  Configuration Manager (最新分支)

如果發生 Windows Defender 或 Endpoint Protection 方面的問題，請使用本文的指示對下列問題進行疑難排解：  

- [更新 Windows Defender 或 Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [啟動 Windows Defender 或 Endpoint Protection 服務](#starting-windows-defender-or-endpoint-protection-service)  
- [網際網路連線問題](#internet-connection-issues)  
- [偵測到無法修復的威脅](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>更新 Windows Defender 或 Endpoint Protection

### <a name="symptoms"></a>徵兆

Windows Defender 或 Endpoint Protection 會自動與 Microsoft Update 一起運作，確定病毒和間諜軟體定義處於最新狀態。  

此節解決自動更新的常見問題，包括下列情況：  

- 您看到錯誤訊息，指出更新已失敗。  

- 當您檢查更新時，會收到錯誤訊息，指出無法檢查、下載或安裝病毒和間諜軟體定義更新。  

- 即使您的裝置已連線到網際網路，更新還是失敗。  

- 未依排程自動安裝更新。  

### <a name="causes"></a>原因

更新問題的最常見原因是網際網路連線問題。 如果您的裝置因可瀏覽至其他網站而知道已連線到網際網路，則問題可能是與 Windows 中的網際網路設定衝突所造成。  

### <a name="options-to-resolve"></a>解決問題的選項

#### <a name="step-1-reset-your-internet-settings"></a>步驟 1：重設您的網際網路設定  

1. 結束所有開啟的程式，包括網頁瀏覽器。  

    > [!NOTE]  
    > 重設這些網際網路設定時，可能會刪除您的瀏覽器暫存檔、Cookie、瀏覽歷程記錄和線上密碼。 「我的最愛」並不會刪除。  

2. 移至 [開始]  功能表，然後開啟 `inetcpl.cpl`。  

3. 切換至 [進階]  索引標籤。  

4. 在 [重設 Internet Explorer 設定]  的區段中選取 [重設]  ，然後再次選取 [重設]  加以確認。  

5. 在設定重設後，選取 [確定]  。

6. 再次嘗試更新 Windows Defender。

如果問題持續發生，請繼續進行下一個步驟。  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>步驟 2：確定電腦上的日期和時間設定正確  

如果錯誤訊息包含 0x80072f8f 代碼，此問題最可能是電腦上的日期或時間設定不正確所造成。 移至 [開始]  功能表，然後依序選取 [設定]  、[時間與語言]  以及 [日期和時間]  。

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>步驟 3：重新命名電腦上的軟體發佈資料夾  

1. 停止 **Windows Update** 服務。  

    1. 移至 [開始]  ，然後開啟 **services.msc**。  

    2. 選取 **Windows Update** 服務。 移至 [動作]  功能表，然後選取 [停止]  。

2. 重新命名 **SoftwareDistribution** 目錄。  

    1. 以系統管理員身分開啟命令提示字元。  

    2. 輸入下列命令：

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. 重新啟動 **Windows Update** 服務。

    1. 切換回 [服務]  視窗。  

    2. 選取 **Windows Update** 服務。 移至 [動作]  功能表，然後選取 [開始]  。

    3. 關閉 [服務] 視窗。  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>步驟 4：重設電腦上的 Microsoft 防毒更新引擎  

1. 以系統管理員身分開啟命令提示字元。

2. 輸入下列命令：

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. 重新啟動電腦。  

4. 再次嘗試更新 Windows Defender。

如果問題持續發生，請繼續進行下一個步驟。  

#### <a name="step-5-manually-install-the-definition-updates"></a>步驟 5：手動安裝定義更新  

[手動下載最新的更新](https://www.microsoft.com/en-us/wdsi/defenderupdates)。  

#### <a name="step-6-contact-microsoft-support"></a>步驟 6：連絡 Microsoft 支援服務  

如果這些步驟無法解決問題，請連絡 Microsoft 支援服務。 如需詳細資訊，請參閱[支援選項與社群資源](../../core/understand/find-help.md#BKMK_SupportOptions)。  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>啟動 Windows Defender 或 Endpoint Protection 服務

### <a name="symptom"></a>徵兆

您收到訊息通知，表示「Windows Defender 或 Endpoint Protection 並未監控電腦，因為程式的服務已停止。**您應該立即重新啟動該服務。」**

### <a name="solution"></a>解決方案

#### <a name="step-1-restart-your-computer"></a>步驟 1：重新啟動電腦

關閉所有應用程式，然後重新啟動電腦。  

#### <a name="step-2-check-the-windows-service"></a>步驟 2：檢查 Windows 服務

1. 移至 [開始]  ，然後開啟 **services.msc**。  

2. 選取 [Windows Defender 防毒軟體服務]  。  

3. 確定 [啟動類型]  已設定為 [自動]  。

4. 移至 [動作]  功能表，然後選取 [開始]  。

    1. 如果無法使用此動作，請選取 [停止]  。 等待服務停止，然後選取 [開始]  動作以重新啟動服務。  

請留意在此程序執行期間可能出現的任何錯誤。 [連絡 Microsoft 支援服務](../../core/understand/find-help.md#BKMK_SupportOptions)，並提供錯誤資訊。  

#### <a name="step-3-remove-any-third-party-security-programs"></a>步驟 3：移除任何第三方安全性程式  

> [!NOTE]  
> 有些安全性應用程式不會完全解除安裝。 您可能需要下載並執行先前安全性應用程式的清理公用程式，才能完全移除該應用程式。  

1. 移至 [開始]  ，然後開啟 **appwiz.cpl**。  

2. 在已安裝程式的清單中，解除安裝所有協力廠商的安全性程式。

3. 重新啟動電腦。  

> [!CAUTION]  
> 當您移除安全性程式時，您的電腦可能無法受到保護。 若無法在移除現有安全性程式之後安裝 Windows Defender，請連絡 [Microsoft 支援服務](https://support.microsoft.com/supportforbusiness/productselection)。 選取 [安全性]  產品系列，然後選取 **Windows Defender** 產品。

## <a name="internet-connection-issues"></a>網際網路連線問題

若要讓您的電腦接收來自 Windows Update 的最新更新，請將其連線至網際網路。  

1. 移至 [開始]  ，然後開啟 **ncpa.cpl**。  

2. 開啟連接名稱以檢視連線**狀態**。  

3. 如果您的電腦已連線，則 **IPv4 連線**和/或 **IPv6 連線**狀態會是 [網際網路]  。  

4. 如果您的電腦似乎未連線，請選取連線名稱，然後選取 [診斷此連線]  。

關閉所有開啟的程式，然後重新啟動電腦。  

## <a name="detected-threat-cant-be-remediated"></a>偵測到無法修復的威脅

Windows Defender 或 Endpoint Protection 在偵測到潛在威脅時，會嘗試隔離或移除威脅以降低威脅。 這些威脅可能會隱藏在壓縮的封存 (`.zip`) 或網路共用中。

### <a name="remove-or-scan-the-file"></a>移除或掃描檔案  

- 如果偵測到的威脅是在壓縮的封存檔案中，請瀏覽至該檔案。 將檔案刪除，或手動掃描該檔案。 以滑鼠右鍵按一下該檔案，然後選取 [以 Endpoint Protection 掃描]  。 Windows Defender 在偵測到檔案中有其他威脅時，將會通知您。 您可據以選擇適當的動作。  

- 如果偵測到的威脅位於網路共用中，請開啟該共用，並手動加以掃描。 以滑鼠右鍵按一下該檔案，然後選取 [以 Endpoint Protection 掃描]  。 Windows Defender 在偵測到網路共用中有其他威脅時，將會通知您。 您可據以選擇適當的動作。  

- 如果您不確定檔案的來源，請在電腦上執行完整掃描。 完整掃描可能需要一些時間才能完成。  

## <a name="see-also"></a>請參閱

[Endpoint Protection 用戶端常見問題集](endpoint-protection-client-faq.md)

[Endpoint Protection 用戶端說明](endpoint-protection-client-help.md)
