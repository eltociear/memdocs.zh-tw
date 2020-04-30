---
title: BitLocker 管理和監視網站
titleSuffix: Configuration Manager
description: 如何使用 Configuration Manager 中的 BitLocker 管理和監視網站 (服務台入口網站)
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84725ac494e1d9497524303b841207bd05cd3859
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699836"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>BitLocker 管理和監視網站

適用於：  Configuration Manager (最新分支)

<!--3601034-->

BitLocker 管理和監視網站是 BitLocker 磁碟機加密的系統管理介面。 其也稱為服務台入口網站。 使用此網站可檢閱報告、復原使用者的磁碟機，以及管理裝置 TPM。

[![預設 BitLocker 管理和監視網站的螢幕擷取畫面](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

若要能夠使用，請先在 Web 伺服器上安裝此元件。 如需詳細資訊，請參閱[設定 BitLocker 報告和入口網站](setup-websites.md)。

透過下列 URL 來存取管理和監視網站：`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> 您可以在 Administration and Monitoring 網站中檢視**復原稽核報告**。 您可以將其他 BitLocker 管理報告新增至 Reporting Services 點。 如需詳細資訊，請參閱[檢視 BitLocker 報告](view-reports.md)。

## <a name="groups"></a>中

若要存取管理和監視網站的特定區域，使用者帳戶必須位於下列其中一個群組。 使用您想要的名稱在 Active Directory 中建立這些群組。 當您安裝此網站時，請指定這些群組名稱。 如需詳細資訊，請參閱[設定 BitLocker 報告和入口網站](setup-websites.md)。

|群組|說明|
|--- |--- |
|BitLocker 服務台系統管理員|可存取管理和監視網站的所有區域。 當您協助使用者復原其磁碟機時，您只需輸入修復金鑰，而不是網域和使用者名稱。 如果使用者同時是此群組和 BitLocker 服務台使用者群組的成員，則系統管理員群組的權限會覆寫使用者群組的權限。|
|BitLocker 服務台使用者|可存取管理和監視網站的 [管理 TPM]  和 [磁碟機修復]  區域。 使用任一區域都必須填寫所有欄位，包括使用者的網域和帳戶名稱。 如果使用者同時是此群組和 BitLocker 服務台系統管理員群組的成員，則系統管理員群組的權限會覆寫使用者群組的權限。|
|BitLocker 報告使用者|可存取管理和監視網站的 [報告]  區域。|

## <a name="manage-tpm"></a>管理 TPM

使用者輸入錯誤 PIN 的次數太多時便會鎖定 TPM。 使用者在 TPM 鎖定前可以輸入錯誤 PIN 的次數，視不同的製造商而異。 從管理和監視網站的 [管理 TPM]  區域可存取集中式金鑰修復資料系統。

如需 TPM 所有權的詳細資訊，請參閱[設定 MBAM 以委付 TPM 和儲存 OwnerAuth 密碼](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm)。

> [!NOTE]
> 從 Windows 10 1607 版開始，Windows 就已不會在佈建 TPM 時保留 TPM 擁有者密碼。

1. 請在網頁瀏覽器中移至管理和監視網站，例如 `https://webserver.contoso.com/HelpDesk`。

1. 在左窗格中，選取 [管理 TPM]  區域。

    ![BitLocker 管理和監視網站 [管理 TPM] 頁面](media/bitlocker-admin-manage-tpm.png)

1. 輸入電腦的完整網域名稱和電腦名稱。

1. 如有需要，請輸入使用者的網域和使用者名稱，以擷取 TPM 擁有者密碼檔案。

1. 針對 [要求 TPM 擁有者密碼檔案的原因]  選擇下列其中一個選項：

    - 重設 PIN 鎖定
    - 開啟 TPM
    - 關閉 TPM
    - 變更 TPM 密碼
    - 清除 TPM
    - 其他

    在 [提交]  表單後，網站會傳回下列其中一種回應：

    - 如果網站找不到相符的 TPM 擁有者密碼檔案，便會傳回錯誤訊息。

    - 所提交電腦的 TPM 擁有者密碼檔案

    在擷取到 TPM 擁有者密碼檔案之後，網站會顯示擁有者密碼。

1. 若要將密碼儲存到檔案，請選取 [儲存]  。

1. 在 [管理 TPM]  區域中，選取 [重設 TPM 鎖定]  選項，然後提供 TPM 擁有者密碼檔案。

    TPM 鎖定便會重設。 BitLocker 會還原使用者對裝置的存取權。

    > [!IMPORTANT]
    > 請勿共用 TPM 雜湊值或 TPM 擁有者密碼檔案。

## <a name="drive-recovery"></a>磁碟機修復

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a> 修復處於修復模式的磁碟機

在下列案例中，磁碟機會進入修復模式：

- 使用者遺失或忘記其 PIN 或密碼
- 信賴模組平台 (TPM) 偵測到電腦的 BIOS 或啟動檔案有所變更

若要取得修復密碼，請使用管理和監視網站的 [磁碟機修復]  區域。

> [!IMPORTANT]
> 修復密碼在使用一次後即過期。 OS 磁碟機和固定資料磁碟機會自動套用單次使用規則。 在卸除式磁碟機上，則會在您移除並重新插入磁碟機時套用。

1. 請在網頁瀏覽器中移至管理和監視網站，例如 `https://webserver.contoso.com/HelpDesk`。

1. 在左窗格中，選取 [磁碟機修復]  區域。

    ![BitLocker 管理和監視網站的 [驅動程式修復] 頁面](media/bitlocker-admin-drive-recovery.png)

1. 如有需要，請輸入使用者的網域和使用者名稱，以檢視修復資訊。

1. 若要查看可能符合的修復金鑰清單，請輸入修復金鑰識別碼的前八個數字。 若要取得確切的修復金鑰，請輸入完整的修復金鑰識別碼。

1. 選擇下列其中一個選項作為 [解除鎖定磁碟機的原因]  ：

    - 作業系統開機順序已變更
    - BIOS 已變更
    - 作業系統檔案已修改
    - 遺失啟動金鑰
    - 遺失 PIN
    - TPM 重設
    - 遺失複雜密碼
    - 遺失智慧卡
    - 其他

    在 [提交]  表單後，網站會傳回下列其中一種回應：

    - 如果使用者有多個相符的修復密碼，則會傳回多個可能的相符項。

    - 所提交使用者的修復密碼和修復套件。

        > [!NOTE]
        > 如果您要修復損壞的磁碟機，修復套件選項會將修復磁碟機所需的重要資訊提供給 BitLocker。

    - 如果找不到相符的修復密碼，就會傳回錯誤訊息。

    在擷取到修復密碼和修復套件之後，網站便會顯示修復密碼。

1. 若要複製密碼，請選取 [複製金鑰]  。 若要將復原密碼儲存到檔案，請選取 [儲存]  。

若要解除鎖定磁碟機，請輸入修復密碼或使用修復套件。

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a> 修復已移動的磁碟機

當您將磁碟機移到新電腦時，因為 TPM 不同，所以 BitLocker 不會接受先前的 PIN。 若要修復已移動的磁碟機，請取得修復金鑰識別碼以擷取修復密碼。

若要修復已移動的磁碟機，請使用管理和監視網站的 [磁碟機修復]  區域。

1. 在擁有所移動磁碟機的電腦上，以 Windows 修復環境 (WinRE) 模式啟動電腦。

1. 在 WinRE 中，BitLocker 會將所移動的 OS 磁碟機視為固定式資料磁碟機。 BitLocker 會顯示磁碟機的修復密碼識別碼，並提示您輸入修復密碼。

    > [!NOTE]
    > 在某些情況下，請於啟動程序進行期間選取 [忘記 PIN]  (如果此選項可用的話)。 然後進入修復模式以顯示修復金鑰識別碼。

1. 使用修復金鑰識別碼，從管理和監視網站取得修復密碼。 如需詳細資訊，請參閱[修復處於修復模式的磁碟機](#bkmk_recovery)。

如果您將已移動的磁碟機設定為使用原始電腦上的 TPM 晶片，請完成下列步驟。 否則，就會完成修復程序。

1. 解除鎖定磁碟機之後，請以 WinRE 模式啟動電腦。 在 WinRE 中開啟命令提示字元，然後使用 `manage-bde` 命令來解密磁碟機。 如果不想透過原始 TPM 晶片來移除 **TPM + PIN** 保護裝置，此工具會是唯一的方法。 如需此命令的詳細資訊，請參閱 [Manage-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde)。

1. 完成時，請正常啟動電腦。 Configuration Manager 會強制執行 BitLocker 原則，以新電腦的 TPM 加上 PIN 來加密磁碟機。

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a> 修復損毀的磁碟機

使用修復金鑰識別碼，從管理和監視網站取得修復金鑰套件。 如需詳細資訊，請參閱[修復處於修復模式的磁碟機](#bkmk_recovery)。

1. 將 [修復金鑰套件]  儲存到電腦上，然後將其複製到擁有損毀磁碟機的電腦上。

1. 以系統管理員身分開啟命令提示字元，然後鍵入下列命令：

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    取代下列值：

    - `<corrupted drive>`：損毀磁碟機的磁碟機代號，例如 `D:`
    - `<fixed drive>`：與損毀磁碟機的大小相近或更大的可用硬碟機代號。 BitLocker 會修復損毀磁碟機上的資料，並將資料移到指定的磁碟機。 這個磁碟機上的所有資料都會遭到覆寫。
    - `<key package>`：修復金鑰套件的位置
    - `<recovery password>`：相關聯的修復密碼

    例如：

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

如需此命令的詳細資訊，請參閱 [Repair-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde)。

## <a name="reports"></a>報告

管理和監視網站中包含**修復稽核報告**。 其他報告則可從 Configuration Manager Reporting Services 點來取得。 如需詳細資訊，請參閱[檢視 BitLocker 報告](view-reports.md)。

1. 請在網頁瀏覽器中移至管理和監視網站，例如 `https://webserver.contoso.com/HelpDesk`。

1. 在左窗格中，選取 [報告]  區域。

1. 從頂端功能表列中，選取 [修復稽核報告]  。

如需這份報告的詳細資訊，請參閱[修復稽核報告](view-reports.md#bkmk-audit)

> [!TIP]
> 若要儲存報告結果，請選取 [報告]  功能表列上的 [匯出]  。
