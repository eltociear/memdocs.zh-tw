---
title: BitLocker 設定參考
titleSuffix: Configuration Manager
description: Configuration Manager 中所有可用的 BitLocker 管理設定
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6a9c566fec22e69c0a4a7fde01b911330ec1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708616"
---
# <a name="bitlocker-settings-reference"></a>BitLocker 設定參考

適用於：  Configuration Manager (最新分支)

<!-- 5925683 -->

Configuration Manager 中的 BitLocker 管理原則包含下列原則群組：

- Setup
- 作業系統磁碟機
- 固定式磁碟機
- 抽取式磁碟機
- 用戶端管理

下列小節將描述並建議每個群組中之設定的組態。

> [!NOTE]
> 這些設定都是以 Configuration Manager 2002 版為基礎。 1910 版並未包含這些所有設定。

## <a name="setup"></a>Setup

此頁面上的設定會設定全域 BitLocker 加密選項。

### <a name="drive-encryption-method-and-cipher-strength"></a>磁碟機加密方法和加密強度

*建議的設定*：已使用預設或更好的加密方法來**啟用**。

> [!NOTE]
> [設定]  屬性頁面包含適用於不同 Windows 版本的兩個設定群組。 此節將描述這兩個群組。

#### <a name="windows-81-devices"></a>Windows 8.1 裝置

針對 Windows 8.1 裝置，啟用 [磁碟機加密方法和加密強度]  選項，然後選取下列其中一種加密方法：

- 具有 Diffuser 的 AES 128 位元
- 具有 Diffuser 的 AES 256 位元
- AES 128 位元 (預設值)
- AES 256 位元

#### <a name="windows-10-devices"></a>Windows 10 裝置

針對 Windows 10 裝置，啟用 [磁碟機加密方法和加密強度 (Windows 10)]  選項。 然後，分別針對 OS 磁碟機、固定式資料磁碟機及抽取式資料磁碟機，選取下列其中一種加密方法：

- AES-CBC 128 位元
- AES-CBC 256 位元
- XTS-AES 128 位元 (預設值)
- XTS-AES 256 位元

> [!TIP]
> BitLocker 使用進階加密標準 (AES) 作為其加密演算法，其可設定的金鑰長度為 128 或 256 位元。 在 Windows 10 裝置上，AES 加密支援加密區塊鏈結 (CBC) 或加密文字竊取 (XTS)。
>
> 如果您需要在未執行 Windows 10 的裝置上使用抽取式磁碟機，請使用 AES-CBC。

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>磁碟機加密和加密強度的一般使用注意事項

- 如果您停用或未進行這些設定，BitLocker 就會使用預設加密方法。

- 當您開啟 BitLocker 時，Configuration Manager 會套用這些設定。

- 如果磁碟機已經加密或正在進行中，則對這些原則設定所做的任何變更都不會變更裝置上的磁碟機加密。

- 如果您使用預設值，BitLocker 電腦合規性報告可能會將加密強度顯示為**未知**。 若要解決此問題，請啟用此設定，並為加密強度設定明確的值。

### <a name="prevent-memory-overwrite-on-restart"></a>防止在重新開機時覆寫記憶體

*建議的設定*：**未設定**

設定此原則可改善重新開機效能，但不會在重新啟動時覆寫記憶體中的 BitLocker 密碼。

當您未設定此原則時，BitLocker 會在電腦重新啟動時，從記憶體中移除其密碼。

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>驗證智慧卡憑證使用規則合規性

*建議的設定*：**未設定**

設定此原則，以使用智慧卡憑證式 BitLocker 保護。 接著，為憑證指定**物件識別碼**。

當您未設定此原則時，BitLocker 會使用預設物件識別碼 `1.3.6.1.4.1.311.67.1.1` 來指定憑證。

### <a name="organization-unique-identifiers"></a>組織唯一識別碼

*建議的設定*：**未設定**

設定此原則，以使用憑證式資料復原代理或 BitLocker To Go 讀取裝置。

當您未設定此原則時，BitLocker 就不會使用 [識別]  欄位。

如果您的組織需要更高的安全性測量，請設定 [識別]  欄位。 在所有目標 USB 裝置上設定此欄位，並使其符合此設定。

## <a name="os-drive"></a>OS 磁碟機

此頁面上的設定會針對 Windows 安裝所在的磁碟機進行加密設定。

### <a name="operating-system-drive-encryption-settings"></a>作業系統磁碟機加密設定

*建議的設定*：**Enabled**

如果您啟用此設定，使用者必須保護 OS 磁碟機和 BitLocker 加密磁碟機。 如果您停用此設定，則使用者無法保護磁碟機。 如果您未設定此原則，OS 磁碟機上就不需要 BitLocker 保護。

> [!NOTE]
> 如果磁碟機已加密，且您停用此設定，BitLocker 會解密該磁碟機。  

如果您的裝置不含[信賴平台模組 (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node) \(部分機器翻譯\)，請使用 [允許沒有相容 TPM 的 BitLocker (需要密碼)]  選項。 此設定可讓 BitLocker 加密 OS 磁碟機，即使裝置不含 TPM 也一樣。 如果您允許此選項，Windows 就會提示使用者指定 BitLocker 密碼。

在具有相容 TPM 的裝置上，可以在啟動時使用兩種類型的驗證方法，為加密資料提供額外的保護。 電腦啟動時，可以只使用 TPM 進行驗證，也可以要求輸入個人識別碼 (PIN)。 進行以下設定：

- **選取作業系統磁碟機的保護程式**：將其設定為使用 TPM 和 PIN，或僅 TPM。

- **設定啟動的 PIN 長度下限**：如果您要求 PIN，此值會是使用者可以指定的最短長度。 使用者在電腦開機時輸入這個 PIN 來解除鎖定磁碟機。 根據預設，PIN 長度下限為 `4`。

> [!TIP]
> 為提高安全性，當您以 TPM + PIN 保護裝置啟用裝置時，請考慮在 [系統]   > [電源管理]   > [睡眠設定]  中「停用」  下列群組原則設定：
>
> - 睡眠時允許待命狀態 (S1-S3) (一般電源)
>
> - 睡眠時允許待命狀態 (S1-S3) (使用電池)

### <a name="allow-enhanced-pins-for-startup"></a>允許增強 PIN 用於啟動

*建議的設定*：**未設定**

將 BitLocker 設定為使用增強式啟動 PIN。 這些 PIN 允許使用大小寫字母、符號、數字和空格等其他字元。 當您開啟 BitLocker 時，即會套用此設定。

> [!IMPORTANT]
> 並非所有電腦都可在開機前環境中支援增強式 PIN。 請先評估您的裝置是否與此功能相容，才能加以使用。

如果您啟用此設定，所有新的 BitLocker 啟動 PIN 都允許使用者建立增強式 PIN。

- **需要純 ASCII 的 PIN**：有助於讓增強式 PIN 與限制您可在開機前環境中輸入之字元類型或字元數的電腦更相容。

如果您停用或未設定此原則設定，BitLocker 就不會使用增強式 PIN。

### <a name="operating-system-drive-password-policy"></a>作業系統磁碟機密碼原則

*建議的設定*：**未設定**

使用這些設定來設定密碼的限制，以將受 BitLocker 保護的 OS 磁碟機解除鎖定。 如果您在 OS 磁碟機上允許非 TPM 保護裝置，請進行下列設定：

- **設定作業系統磁碟機的密碼複雜度**：若要強制執行密碼的複雜性需求，請選取 [需要密碼複雜性]  。

- **作業系統磁碟機的最小密碼長度**：根據預設，長度下限為 `8`。

- **需要抽取式 OS 磁碟機的純 ASCII 密碼**

如果您啟用此原則設定，使用者就能設定符合您所定義之需求的密碼。

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>OS 磁碟機密碼原則的一般使用注意事項

- 若要讓這些複雜性需求設定生效，還要在 [電腦設定]   > [Windows 設定]   > [安全性設定]   > [帳戶原則]   > [密碼原則]  中，啟用 [密碼必須符合複雜性需求]  群組原則設定。

- BitLocker 會在您將其開啟時強制執行這些設定，而不是在您將磁碟區解除鎖定時強制執行。 BitLocker 可讓您使用磁碟機上任何可用的保護裝置來將磁碟機解除鎖定。

- 如果您使用群組原則來啟用可用來進行加密、雜湊和簽署的 FIPS 相容演算法，則不能允許密碼作為 BitLocker 保護裝置。

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>在 BitLocker 復原後重設平台驗證資料

*建議的設定*：**未設定**

控制 Windows 在 BitLocker 復原之後啟動時，是否要重新整理平台驗證資料。

在此情況下，如果您啟用或未進行此設定，Windows 就會重新整理平台驗證資料。

在此情況下，如果您停用此原則設定，則 Windows 不會重新整理平台驗證資料。

### <a name="pre-boot-recovery-message-and-url"></a>開機前的修復訊息及 URL

*建議的設定*：**未設定**

當 BitLocker 鎖定 OS 磁碟機時，請使用此設定，在開機前 BitLocker 復原畫面上顯示自訂復原訊息或 URL。 此設定只適用於 Windows 10 裝置。

當您啟用此設定時，為開機前復原訊息選取下列其中一個選項：

- **使用預設復原訊息和 URL**：在開機前 BitLocker 復原畫面中，顯示預設的 BitLocker 復原訊息和 URL。 如果您先前已設定自訂復原訊息或 URL，請使用此選項來還原為預設訊息。

- **使用自訂復原訊息**：在開機前的 BitLocker 復原畫面中包含自訂訊息。

  - **自訂復原訊息選項**：輸入要顯示的自訂訊息。 如果您也想要指定復原 URL，請將其納入為此自訂復原訊息的一部分。 字串長度上限為 32,768 個字元。

- **使用自訂復原 URL**：取代開機前 BitLocker 復原畫面中顯示的預設 URL。

  - **自訂復原 URL 選項**：輸入要顯示的 URL。 字串長度上限為 32,768 個字元。

> [!NOTE]
> 開機前並未支援所有字元和語言。 先測試您的自訂訊息或 URL，以確定其會在開機前 BitLocker 復原畫面上正確顯示。

### <a name="encryption-policy-enforcement-settings-os-drive"></a>加密原則實施設定 (OS 磁碟機)

*建議的設定*：**Enabled**

設定使用者可以針對 OS 磁碟機延遲 BitLocker 合規性的天數。 **不符合規範的寬限期**會在 Configuration Manager 第一次偵測到其不符合規範時開始。 在此寬限期過後，使用者就無法延遲所要求的動作或要求豁免。

如果加密程序需要使用者輸入，則會在 Windows 中顯示對話方塊，使用者必須提供必要資訊，才能關閉此對話方塊。 未來對於錯誤或狀態的通知將不會有此限制。

如果 BitLocker 不需要使用者互動即可新增保護裝置，則在寬限期過後，BitLocker 就會在背景開始加密。

如果您停用或未進行此設定，Configuration Manager 就不會要求使用者遵守 BitLocker 原則。

若要立即強制執行此原則，請將寬限期設為 `0`。

## <a name="fixed-drive"></a>固定式磁碟機

此頁面上的設定會針對裝置中的其他資料磁碟機設定加密。

### <a name="fixed-data-drive-encryption"></a>固定式資料磁碟機加密

*建議的設定*：**Enabled**

管理您對固定式資料磁碟機加密的需求。 如果您啟用此設定，BitLocker 就會要求使用者將所有固定式資料磁碟機置於保護之下。 接著，其會加密資料磁碟機。

當您啟用此原則時，請啟用自動解除鎖定或 [固定資料磁碟機密碼原則]  的設定。

- **對固定資料磁碟機設定自動解除鎖定**：允許或要求 BitLocker 自動將任何加密的資料磁碟機解除鎖定。 若要使用自動解除鎖定，也需要 BitLocker 加密 [OS 磁碟機](#os-drive)。

如果您未進行此設定，BitLocker 就不會要求使用者將固定式資料磁碟機置於保護之下。

如果您停用此設定，使用者便無法將固定式資料磁碟機置於 BitLocker 保護之下。 如果您在 BitLocker 加密固定式資料磁碟機之後停用此原則，BitLocker 就會將固定式資料磁碟機解密。

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>拒絕對未受 BitLocker 保護的固定式磁碟機擁有寫入權限

*建議的設定*：**未設定**

需要適用於 Windows 的 BitLocker 保護，才能將資料寫入至裝置上的固定式磁碟機。 BitLocker 會在您開啟時套用此原則。

當您啟用此設定時：

- 如果 BitLocker 會保護固定式資料磁碟機，Windows 就會掛接該磁碟機，並提供讀取和寫入存取權。

- 對於 BitLocker 不會保護的任何固定式資料磁碟機，Windows 會將其掛接為唯讀。

當您未進行此設定時，Windows 會掛接具有讀取和寫入存取權的所有固定式資料磁碟機。

<!-- ### Allow access to BitLocker-protected fixed drives from earlier versions of Windows -->

### <a name="fixed-data-drive-password-policy"></a>固定資料磁碟機密碼原則

*建議的設定*：**未設定**

使用這些設定來設定密碼的限制，以將受 BitLocker 保護的固定式資料磁碟機解除鎖定。

如果您啟用此設定，使用者就能設定符合您所定義需求的密碼。

為提高安全性，請啟用此設定，然後進行下列設定：

- **固定式資料磁碟機需要密碼**：使用者必須指定密碼，才能將受 BitLocker 保護的固定式資料磁碟機解除鎖定。

- **設定固定式資料磁碟機的密碼複雜性**：若要強制執行密碼的複雜性需求，請選取 [需要密碼複雜性]  。

- **固定式資料磁碟機的最小密碼長度**：根據預設，長度下限為 `8`。

如果您停用此設定，使用者就無法設定密碼。

未設定原則時，BitLocker 支援具有預設設定的密碼。 預設設定不包含密碼複雜性需求，而且只需要八個字元。

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>固定式資料磁碟機密碼原則的一般使用注意事項

- 若要讓這些複雜性需求設定生效，還要在 [電腦設定]   > [Windows 設定]   > [安全性設定]   > [帳戶原則]   > [密碼原則]  中，啟用 [密碼必須符合複雜性需求]  群組原則設定。

- BitLocker 會在您將其開啟時強制執行這些設定，而不是在您將磁碟區解除鎖定時強制執行。 BitLocker 可讓您使用磁碟機上任何可用的保護裝置來將磁碟機解除鎖定。

- 如果您使用群組原則來啟用可用來進行加密、雜湊和簽署的 FIPS 相容演算法，則不能允許密碼作為 BitLocker 保護裝置。

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>加密原則實施設定 (固定式資料磁碟機)

*建議的設定*：**Enabled**

設定使用者可以針對固定式資料磁碟機延遲 BitLocker 合規性的天數。 **不符合規範的寬限期**會在 Configuration Manager 第一次偵測到固定式資料磁碟機不符合規範時開始。 在 OS 磁碟機符合規範之前，其不會強制執行固定式資料磁碟機原則。 在寬限期過後，使用者就無法延遲所要求的動作或要求豁免。

如果加密程序需要使用者輸入，則會在 Windows 中顯示對話方塊，使用者必須提供必要資訊，才能關閉此對話方塊。 未來對於錯誤或狀態的通知將不會有此限制。

如果 BitLocker 不需要使用者互動即可新增保護裝置，則在寬限期過後，BitLocker 就會在背景開始加密。

如果您停用或未進行此設定，Configuration Manager 就不會要求使用者遵守 BitLocker 原則。

若要立即強制執行此原則，請將寬限期設為 `0`。

## <a name="removable-drive"></a>抽取式磁碟機

此頁面上的設定會針對抽取式磁碟機 (例如 USB 金鑰) 設定加密。

### <a name="removable-data-drive-encryption"></a>抽取式資料磁碟機加密

*建議的設定*：**Enabled**

此設定會控制在抽取式磁碟機上使用 BitLocker 的方式。

- **允許使用者在抽取式資料磁碟機上套用 BitLocker 保護**：使用者可以對抽取式磁碟磁碟機開啟 BitLocker 保護。

- **允許使用者在抽取式資料磁碟機上暫停和解密 BitLocker**：使用者可以從抽取式磁碟機中移除或暫停 BitLocker 磁碟機加密。

當您啟用此設定並允許使用者套用 BitLocker 保護時，Configuration Manager 用戶端會將抽取式磁碟機的復原資訊儲存到管理點上的復原服務。 如果使用者忘記或遺失保護裝置 (密碼)，則此行為可讓使用者復原裝置。

當您啟用此設定時：

- 啟用 [抽取式資料磁碟機密碼原則]  的設定

- 在 [系統]   > [抽取式存放裝置存取權]  中，針對使用者和電腦設定「停用」  下列群組原則設定：

  - **所有抽取式儲存裝置類別:拒絕所有存取**
  - **抽取式磁碟機:拒絕寫入存取權**
  - **抽取式磁碟機:拒絕讀取存取權**

如果您停用此設定，使用者就無法在抽取式磁碟機上使用 BitLocker。

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>拒絕對未受 BitLocker 保護的抽取式資料磁碟機擁有寫入權限

*建議的設定*：**未設定**

需要適用於 Windows 的 BitLocker 保護，才能將資料寫入至裝置上的抽取式磁碟機。 BitLocker 會在您開啟時套用此原則。

當您啟用此設定時：

- 如果 BitLocker 會保護抽取式磁碟機，Windows 就會掛接該磁碟機，並提供讀取和寫入存取權。

- 對於 BitLocker 不會保護的任何抽取式磁碟機，Windows 會將其掛接為唯讀。

- 如果您啟用 [拒絕在其他組織中設定之裝置的寫入存取權]  選項，BitLocker 就只會為識別欄位符合允許識別欄位的抽取式磁碟機授與寫入存取權。 在[設定](#setup)頁面上，使用 [組織唯一識別碼]  全域設定來定義這些欄位。

當您停用或未進行此設定時，Windows 會掛接具有讀取和寫入存取權的所有抽取式磁碟機。

> [!NOTE]
> 您可以在 [系統]   > [抽取式存放裝置存取權]  中，使用群組原則設定來覆寫此設定。 如果您啟用群組原則設定 [抽取式磁碟:  拒絕寫入存取權]，則 BitLocker 會忽略此 Configuration Manager 設定。

<!-- ### Allow access to BitLocker-protected removable data drives from earlier versions of Windows -->

### <a name="removable-data-drive-password-policy"></a>抽取式資料磁碟機密碼原則

*建議的設定*：**Enabled**

使用這些設定來設定密碼的限制，以將受 BitLocker 保護的抽取式磁碟機解除鎖定。

如果您啟用此設定，使用者就能設定符合您所定義需求的密碼。

為提高安全性，請啟用此設定，然後進行下列設定：

- **抽取式資料磁碟機需要密碼**：使用者必須指定密碼，才能將受 BitLocker 保護的抽取式磁碟機解除鎖定。

- **設定抽取式資料磁碟機的密碼複雜性**：若要強制執行密碼的複雜性需求，請選取 [需要密碼複雜性]  。

- **抽取式資料磁碟機的最小密碼長度**：根據預設，長度下限為 `8`。

如果您停用此設定，使用者就無法設定密碼。

未設定原則時，BitLocker 支援具有預設設定的密碼。 預設設定不包含密碼複雜性需求，而且只需要八個字元。

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>抽取式資料磁碟機密碼原則的一般使用注意事項

- 若要讓這些複雜性需求設定生效，還要在 [電腦設定]   > [Windows 設定]   > [安全性設定]   > [帳戶原則]   > [密碼原則]  中，啟用 [密碼必須符合複雜性需求]  群組原則設定。

- BitLocker 會在您將其開啟時強制執行這些設定，而不是在您將磁碟區解除鎖定時強制執行。 BitLocker 可讓您使用磁碟機上任何可用的保護裝置來將磁碟機解除鎖定。

- 如果您使用群組原則來啟用可用來進行加密、雜湊和簽署的 FIPS 相容演算法，則不能允許密碼作為 BitLocker 保護裝置。

## <a name="client-management"></a>用戶端管理

此頁面上的設定會設定 BitLocker 管理服務和用戶端。

### <a name="bitlocker-management-services"></a>BitLocker 管理服務

*建議的設定*：**Enabled**

如果您啟用此設定，Configuration Manager 會以無訊息方式自動備份站台資料庫中的金鑰復原資訊。 如果您停用或未進行此設定，Configuration Manager 就不會儲存金鑰復原資訊。

- **選取要儲存的 BitLocker 復原資訊**：設定金鑰復原服務以備份 BitLocker 復原資訊。 其提供的系統管理方法可復原 BitLocker 加密的資料，有助於避免因缺少金鑰資訊而導致資料遺失。

- **允許以純文字格式儲存復原資訊**：如果沒有適用於 SQL Server 的 BitLocker 管理加密憑證，Configuration Manager 就會以純文字格式儲存金鑰復原資訊。 如需詳細資訊，請參閱[加密復原資料](../../deploy-use/bitlocker/encrypt-recovery-data.md)。

- **用戶端檢查狀態頻率 (分鐘)** ：用戶端會按照設定的頻率來檢查電腦上的 BitLocker 保護原則和狀態，也會備份用戶端復原金鑰。 根據預設，Configuration Manager 用戶端每 90 分鐘就會更新一次其 BitLocker 復原資訊。

### <a name="user-exemption-policy"></a>使用者豁免原則

*建議的設定*：**未設定**

設定連絡方式，讓使用者可用來要求豁免 BitLocker 加密。

如果您啟用此原則設定，請提供下列資訊：

- **延遲的天數上限**：使用者可以延遲強制執行原則的天數。 根據預設，此值為 `7` 天 (一週)。

- **連絡方式**：指定使用者如何要求豁免的方式：URL、電子郵件地址或電話號碼。

- **連絡人**：指定 URL、電子郵件地址或電話號碼。 當使用者要求豁免 BitLocker 保護時，會看到 Windows 對話方塊，其中提供如何申請的指示。 Configuration Manager 不會驗證您輸入的資訊。

  - **URL**：使用標準 URL 格式 `https://website.domain.tld`。 Windows 會將 URL 顯示為超連結。

  - **電子郵件地址**：使用標準電子郵件地址格式 `user@domain.tld`。 Windows 會將此地址顯示為下列超連結：`mailto:user@domain.tld?subject=Request exemption from BitLocker protection`。

  - **電話號碼**：指定您想要讓使用者撥打的電話號碼。 Windows 會以下列描述顯示電話號碼：`Please call <your number> for applying exemption`。

如果您停用或未進行此設定，Windows 就不會向使用者顯示豁免要求指示。

> [!NOTE]
> BitLocker 會管理每位使用者 (而不是每一部電腦) 的豁免。 如果有多位使用者登入同一部電腦，只要其中有任何使用者未豁免，BitLocker 就會加密電腦。

### <a name="url-for-the-security-policy-link"></a>安全性原則連結的 URL

*建議的設定*：**Enabled**

指定要向使用者顯示的 URL，以作為 Windows 中的**公司安全性原則**。 使用此連結，可為使用者提供加密需求的相關資訊。 當 BitLocker 提示使用者加密磁碟機時會加以顯示。

如果您啟用此設定，請設定**安全性原則連結 URL**。

如果您停用或未進行此設定，BitLocker 就不會顯示安全性原則連結。
