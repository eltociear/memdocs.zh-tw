---
title: Intune 端點安全性磁碟加密原則設定 | Microsoft Docs
description: Microsoft Intune 中 BitLocker 和 FileVault 的端點安全性磁碟加密原則設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: db23ee1742934e8545c03c529d6a05c13cc59f1a
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633276"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Intune 中端點安全性的磁碟加密原則設定

檢視在 Intune [端點安全性] 節點中，您可在設定檔中為[端點安全性原則](../protect/endpoint-security-policy.md)「磁碟加密」原則進行的設定。

支援的平台和設定檔：

- **macOS**：
  - 設定檔：**FileVault**
- **Windows 10 及更新版本**：
  - 設定檔：**BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>加密

**啟用 FileVault**  
- [未設定] (預設)
- **是** - 您可以在執行 macOS 10.13 和更新版本的裝置上，在 FileVault 使用 XTS-AES 128 以啟用完整磁碟加密。 FileVault 會在使用者登出裝置時啟用。

  設為 [是] 時，您可以為 FileVault 進行其他設定。

  - **修復金鑰類型**
    系統會為裝置建立「個人金鑰」修復金鑰。 請為個人金鑰設定下列設定：

    - **個人修復金鑰輪替**  
      指定裝置的個人修復金鑰輪替頻率。 您可以選取預設的 [未設定]，或 **1** 到 **12** 個月的值。
    - **個人修復金鑰的委付位置描述**  
      指定簡短的訊息給使用者，說明如何擷取其個人修復金鑰。 當使用者忘記密碼，而系統提示其輸入個人修復金鑰時，就會在登入畫面上看到此訊息。

  - **允許略過的次數**  
    設定使用者可以忽略幾次啟用 FileVault 的提示，使用者即會需要 FileVault 才能登入。
    - **未設定** (預設) - 在允許下一次登入之前，需要在裝置上進行加密。
    - **1** 到 **10** - 需要在裝置上進行加密之前，允許使用者忽略提示 1 到 10 次。
    - **無限制，一律提示** - 系統會提示使用者啟用 FileVault，但一律不需要加密。

  - **允許延遲到登出為止**  
    - [未設定] (預設)
    - **是** - 延遲啟用 FileVault 的提示，直到使用者登出為止。  

  - **停用登出時的提示**  
    當使用者登出時，避免提示使用者要求其啟用 FileVault。當設定為 [停用] 時，會停用登出時的提示，並改為在使用者登入時向其提示。
    - [未設定] (預設)
    - **是** - 停用在登出時顯示啟用 FileVault 的提示。

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker - 基本設定

- **為 OS 及固定資料磁碟機啟用完整的磁碟加密**  
  CSP：[RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  如果磁碟機在套用此原則之前已加密，則不會採取任何額外的動作。 如果加密方法和選項符合此原則，則設定應該會傳回成功。 如果現有的 BitLocker 設定選項不符合此原則，則設定可能會傳回錯誤。
  
  若要將此原則套用至已加密的磁碟，請將磁碟機解密，再重新套用 MDM 原則。 Windows 預設為不需要 BitLocker 磁碟機加密。 不過，在 Azure AD Join 和 Microsoft 帳戶 (MSA) 註冊/登入時可套用自動加密，以啟用 XTS-AES 128 位元的 BitLocker 加密。

  - **未設定** (預設) - 不強制使用 BitLocker。
  - **是** - 強制使用 BitLocker。

- **需要加密儲存卡 (僅限行動裝置)**  
  CSP：[RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  此設定僅適用於 Windows 行動裝置版和行動裝置企業版 SKU 裝置。
  - **未設定** (預設) - 此設定會還原為 OS 預設，也就是不需要加密儲存卡。
  - **是** - 行動裝置需要加密儲存卡。

- **隱藏有關於第三方加密的提示**  
  CSP：[AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  如果在已由第三方加密產品加密的系統上啟用 BitLocker，可能會導致裝置無法使用。 資料可能會遺失，而您可能會需要重新安裝 Windows。 強烈建議您勿在已安裝或啟用第三方加密的裝置上啟用 BitLocker。

  根據預設，BitLocker 安裝精靈會提示使用者確認沒有任何第三方加密。

  - **未設定** (預設) - BitLocker 安裝精靈會顯示警告，並提示使用者確認第三方加密不存在。
  - **是** - 對使用者隱藏 BitLocker 安裝精靈的提示。

  如果需要 BitLocker 無訊息啟用功能，請務必隱藏第三方加密警告，因為所要求的任何提示都會中斷無訊息啟用工作流程。

  設為 [是] 時，您即可進行下列設定：

  - **允許標準使用者在 Autopilot 期間啟用加密**  
    CSP：[AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **未設定** (預設) - 在 Azure Active Directory Join (AADJ) 無訊息啟用案例期間，使用者即使不是本機系統管理員也能啟用 BitLocker。
    - **是** - 設定會保留為用戶端預設，也就是需要本機系統管理員存取權才能啟用 BitLocker。

    若是無訊息啟用和 Autopilot 以外的案例，使用者必須是本機系統管理員才能完成 BitLocker 安裝精靈。

- **啟用用戶端驅動的復原密碼以用於**  
  CSP：[ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  不支援新增公司帳戶 (AWA，先前稱為 Workplace Joined) 裝置進行金鑰輪替。
  - **未設定** (預設) - 用戶端不會輪替 BitLocker 修復金鑰。
  - **停用**
  - **已加入 Azure AD 的裝置**
  - **已加入 Azure AD 與混合式的裝置**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker - 固定磁碟機設定

- **BitLocker 固定磁碟機原則**  
  [BitLocker 群組原則設定](https://go.microsoft.com/fwlink/?linkid=2067018) (機器翻譯)

  - **固定式磁碟機修復**  
    CSP：[FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    控制在缺少必要的啟動金鑰資訊時，如何復原受 BitLocker 保護的固定資料磁碟機。

    - **未設定** (預設) - 支援預設的復原選項，包括資料修復代理程式 (DRA)。 終端使用者可以指定復原選項，且復原資訊不會備份到 Azure Active Directory。
    - **設定** - 允許存取以設定各種磁碟機復原技術。

    設為 [設定] 時，可用的設定如下：

    - **使用者的修復金鑰建立**  
      - **封鎖** (預設)
      - **必要**
      - **允許**

    - **設定 BitLocker 復原套件**
      - **密碼和金鑰** (預設) - 包含系統管理員和使用者用於為受保護磁碟機解除鎖定的 BitLocker 復原密碼，以及系統管理員在 Active Directory 中用於資料復原的修復金鑰套件。
      - **僅密碼** - 在需要時可能會無法存取修復金鑰套件。

    - **要求裝置將修復資訊備份到 Azure AD**
      - **未設定** (預設) - 即使將修復金鑰備份至 Azure AD 失敗，仍會完成 BitLocker 啟用。 這可能會導致沒有任何復原資訊儲存在外部。
      - **是** - 除非已成功將修復金鑰儲存至 Azure Active Directory，否則 BitLocker 將無法完成啟用。

    - **使用者的修復密碼建立**  
      - **封鎖** (預設)
      - **必要**
      - **允許**

    - **在 BitLocker 安裝期間隱藏復原選項**
      - **未設定** (預設) - 允許使用者存取額外的復原選項。
      - **是** - 禁止終端使用者在 BitLocker 安裝精靈期間選擇額外的復原選項 (例如列印修復金鑰)。

    - **在儲存復原資訊後啟用 BitLocker**
      - [未設定] (預設)  
      - **是**

    - **禁止使用憑證型資料修復代理程式 (DRA)**
      - **未設定** (預設) - 允許設定 DRA 使用方式。 設定 DRA 需要企業 PKI 和群組原則物件，才能部署 DRA 代理程式和憑證。
      - **是** - 禁止使用資料修復代理程式 (DRA) 來復原已啟用 BitLocker 的磁碟機。

  - **禁止寫入未受 BitLocker 保護的固定資料磁碟機**  
    CSP：[FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    當 [BitLocker 固定磁碟機原則] 設定為 [設定] 時，即可使用此設定。

    - **未設定** (預設) - 可將資料寫入未加密的固定磁碟機。
    - **是** - Windows 不允許將任何資料寫入未受 BitLocker 保護的固定磁碟機。 若固定磁碟機未加密，則使用者必須先為磁碟機完成 BitLocker 安裝精靈，才能授與寫入權限。

  - **設定固定資料磁碟機的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    設定固定資料磁碟機磁碟的加密方法和加密強度。 「XTS-AES 128 位元」是 Windows 預設加密方法和建議值。

    - [未設定] (預設)
    - **AES 128 位元 CBC**
    - **AES 256 位元 CBC**
    - **AES 128 位元 XTS**
    - **AES 256 位元 XTS**

### <a name="bitlocker---os-drive-settings"></a>BitLocker - OS 磁碟機設定

- **BitLocker 系統磁碟機原則**  
  CSP：[BitLocker 群組原則設定](https://go.microsoft.com/fwlink/?linkid=2067025) (機器翻譯)

  - **設定** (預設)  
  - **未設定**

  設為 [設定] 時，您可以進行下列設定：

  - **需要啟動驗證**  
    CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - [未設定] (預設)
    - **是** - 設定系統啟動時的額外驗證要求，包括使用信賴平台模組 (TPM) 或啟動 PIN 要求。

    設為 [是] 時，您可以進行下列設定：

    - **相容 TPM 啟動**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      建議您為 BitLocker 要求 TPM。 只有在第一次啟用 BitLocker 時才會套用此設定，如果 BitLocker 已啟用，則不會有任何作用。

      - **封鎖** (預設) - BitLocker 不會使用 TPM。
      - **必要** - 只有當 TPM 存在且可使用時，BitLocker 才會啟用。
      - **允許** - BitLocker 會使用 TPM (如果有的話)。

    - **相容 TPM 啟動 PIN**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **封鎖** (預設) 禁止使用 PIN。
      - **必要** - 需要有 PIN 和 TPM 才能啟用 BitLocker。
      - **允許** - BitLocker 會使用 TPM (如果有的話) 並允許使用者設定啟動 PIN。

      若是無訊息啟用案例，您必須將此項設為 [封鎖]。 需要使用者互動時，無訊息啟用案例 (包括 Autopilot) 不會成功。

    - **相容 TPM 啟動金鑰**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **封鎖** (預設) 禁止使用啟動金鑰。
      - **必要** - 需要有啟動金鑰和 TPM 才能啟用 BitLocker。
      - **允許** - BitLocker 會使用 TPM (如果有的話)，並允許使用啟動金鑰 (例如 USB 磁碟機) 來解除磁碟機的鎖定。

      若是無訊息啟用案例，您必須將此項設為 [封鎖]。 需要使用者互動時，無訊息啟用案例 (包括 Autopilot) 不會成功。

    - **相容 TPM 啟動金鑰及 PIN**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **封鎖** (預設) - 禁止使用啟動金鑰和 PIN 組合。
      - **必要** - 要求 BitLocker 必須有啟動金鑰和 PIN 才能啟用。
      - **允許** - BitLocker 會使用 TPM (如果有的話) 並允許啟動金鑰和 PIN 組合。

      若是無訊息啟用案例，您必須將此項設為 [封鎖]。 需要使用者互動時，無訊息啟用案例 (包括 Autopilot) 不會成功。

    - **在 TPM 不相容的裝置上停用 BitLocker**  
    CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      如果 TPM 不存在，則 BitLocker 需要使用密碼或 USB 磁碟機來啟動。

      只有在第一次啟用 BitLocker 時才會套用此設定，如果 BitLocker 已啟用，則不會有任何作用。

      - [未設定] (預設)
      - **是** - 禁止在沒有相容 TPM 晶片的情況下設定 BitLocker。

    - **啟用開機前復原訊息及 URL**  
      CSP：[SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configure

      - **未設定** (預設) - 使用預設的 BitLocker 開機前復原資訊。
      - **是** - 啟用自訂開機前復原訊息和 URL 的設定，以協助您的使用者了解如何尋找其修復密碼。 當使用者在修復模式中遇到電腦鎖住的情形時，會看到開機前訊息和 URL。

      設為 [是] 時，您可以進行下列設定：

      - **開機前復原訊息**  
        指定自訂開機前復原訊息。

      - **開機前復原 URL**  
        指定自訂開機前復原 URL。

    - **系統磁碟機復原**  
      CSP：[SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - [未設定] (預設)  
      - **設定** - 允許進行額外設定。

      設為 [設定] 時，可用的設定如下：

      - **使用者的修復金鑰建立**  
        - **封鎖** (預設)
        - **必要**
        - **允許**

      - **設定 BitLocker 復原套件**
        - **密碼和金鑰** (預設) - 包含系統管理員和使用者用於為受保護磁碟機解除鎖定的 BitLocker 復原密碼，以及系統管理員在 Active Directory 中用於資料復原的修復金鑰套件。
        - **僅密碼** - 在需要時可能會無法存取修復金鑰套件。

      - **要求裝置將修復資訊備份到 Azure AD**
        - **未設定** (預設) - 即使將修復金鑰備份至 Azure AD 失敗，仍會完成 BitLocker 啟用。 這可能會導致沒有任何復原資訊儲存在外部。
        - **是** - 除非已成功將修復金鑰儲存至 Azure Active Directory，否則 BitLocker 將無法完成啟用。

      - **使用者的修復密碼建立**  
        - **封鎖** (預設)
        - **必要**
        - **允許**

      - **在 BitLocker 安裝期間隱藏復原選項**
        - **未設定** (預設) - 允許使用者存取額外的復原選項。
        - **是** - 禁止終端使用者在 BitLocker 安裝精靈期間選擇額外的復原選項 (例如列印修復金鑰)。

      - **在儲存復原資訊後啟用 BitLocker**
        - [未設定] (預設)  
        - **是**

      - **禁止使用憑證型資料修復代理程式 (DRA)**
        - **未設定** (預設) - 允許設定 DRA 使用方式。 設定 DRA 需要企業 PKI 和群組原則物件，才能部署 DRA 代理程式和憑證。
        - **是** - 禁止使用資料修復代理程式 (DRA) 來復原已啟用 BitLocker 的磁碟機。

    - **PIN 長度下限**  
      CSP：[SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      指定 BitLocker 啟用期間需要 TPM + PIN 時的啟動 PIN 長度下限。 PIN 的長度必須介於 4 到 20 個數字之間。

      如果您未進行此設定，則使用者可以設定任意長度 (介於 4 到 20 個數字之間) 的啟動 PIN

      只有在第一次啟用 BitLocker 時才會套用此設定，如果 BitLocker 已啟用，則不會有任何作用。

  - **設定作業系統磁碟機的加密方法**  
   CSP：[EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    設定 OS 磁碟機的加密方法和加密強度。 「XTS-AES 128 位元」是 Windows 預設加密方法和建議值。

    - [未設定] (預設)
    - **AES 128 位元 CBC**
    - **AES 256 位元 CBC**
    - **AES 128 位元 XTS**
    - **AES 256 位元 XTS**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker - 抽取式磁碟設定

- **設定作業系統磁碟機的加密方法**  
  CSP：[BitLocker 群組原則設定](https://go.microsoft.com/fwlink/?linkid=2067140) (機器翻譯)

  - [未設定] (預設)  
  - **設定 [報告]**

  設為 [設定] 時，您可以進行下列設定。

  - **設定抽取式資料磁碟機的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    選取要用於抽取式資料磁碟機磁碟的加密方法。

    - [未設定] (預設)
    - **AES 128 位元 CBC**
    - **AES 256 位元 CBC**
    - **AES 128 位元 XTS**
    - **AES 256 位元 XTS**

  - **禁止寫入未受 BitLocker 保護的抽取式資料磁碟機**  
    CSP：[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **未設定** (預設) - 可將資料寫入未加密的抽取式磁碟機。
    - **是** - Windows 不允許將資料寫入未受 BitLocker 保護的抽取式磁碟機。 若插入的抽取式磁碟機未加密，則使用者必須先完成 BitLocker 安裝精靈，才能授與磁碟機寫入權限。

    - **禁止寫入未受 BitLocker 保護的抽取式資料磁碟機**  
      CSP：[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **未設定** (預設) - 可以使用任何 BitLocker 加密磁碟機。
      - **是** - 禁止存取抽取式磁碟機，除非其已在貴組織擁有的電腦上加密。

## <a name="next-steps"></a>後續步驟

[磁碟加密的端點安全性原則](../protect/endpoint-security-disk-encryption-policy.md)
