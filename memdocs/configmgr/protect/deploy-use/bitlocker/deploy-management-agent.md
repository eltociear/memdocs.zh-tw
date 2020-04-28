---
title: 部署 BitLocker 管理
titleSuffix: Configuration Manager
description: 將 BitLocker 管理代理程式部署到 Configuration Manager 用戶端，並將復原服務部署到管理點
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 96594731ef64577d30267376d3bcb93268e59a9e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075008"
---
# <a name="deploy-bitlocker-management"></a>部署 BitLocker 管理

適用於：  Configuration Manager (最新分支)

<!--3601034-->

Configuration Manager 中的 BitLocker 管理包含下列元件：

- **BitLocker 管理代理程式**：當您[建立原則](#create-a-policy)並[將其部署到集合](#deploy-a-policy)時，Configuration Manager 會在裝置上啟用此代理程式。

- **復原服務**：此伺服器元件可接收來自用戶端的 BitLocker 復原資料。 如需詳細資訊，請參閱[復原服務](#recovery-service)。

在您建立並部署 BitLocker 管理原則之前：

- 檢閱[必要條件](../../plan-design/bitlocker-management.md#prerequisites)

- 視需要在站台資料庫中[加密復原金鑰](encrypt-recovery-data.md)

## <a name="create-a-policy"></a>建立原則

當您建立並部署此原則時，Configuration Manager 用戶端會在裝置上啟用 BitLocker 管理代理程式。

> [!NOTE]
> 若要建立 BitLocker 管理原則，您需要在 Configuration Manager 中具備 [系統高權限管理員]  角色。

1. 在 Configuration Manager 主控台中，移至 [資產與合規性]  工作區，展開 [Endpoint Protection]  ，然後選取 [BitLocker 管理]  節點。

1. 在功能區中，選取 [建立 BitLocker 管理控制原則]  。

1. 在 [一般]  頁面中指定名稱和選擇性描述。 選取要使用此原則在用戶端上啟用的元件：  

    - **作業系統磁碟機**：管理是否要加密 OS 磁碟機

    - **固定磁碟機**：管理裝置中其他資料磁碟機的加密

    - **抽取式磁碟機**：管理可從裝置中移除之磁碟機的加密，例如 USB 金鑰

    - **用戶端管理**：管理 BitLocker 磁碟機加密復原資訊的金鑰復原服務備份  

1. 在 [設定]  頁面上，為 [BitLocker 磁碟機加密] 設定下列全域設定：

    > [!NOTE]
    > 當您啟用 BitLocker 時，Configuration Manager 會套用這些設定。 如果磁碟機已經加密或正在進行中，則對這些原則設定所做的任何變更都不會變更裝置上的磁碟機加密。
    >
    > 如果您停用或未進行這些設定，BitLocker 就會使用預設加密方法 (AES 128 位元)。

    - 針對 Windows 8.1 裝置，請啟用 [磁碟機加密方法和加密強度]  選項。 然後選取加密方法。

    - 針對 Windows 10 裝置，請啟用 [磁碟機加密方法和加密強度 (Windows 10)]  選項。 然後，分別針對 OS 磁碟機、固定資料磁碟機及抽取式資料磁碟機選取加密方法。

    如需這些設定及此頁面上其他設定的詳細資訊，請參閱[設定參考 - 設定](../../tech-ref/bitlocker/settings.md#setup)。

1. 在 [作業系統磁碟機]  頁面上，指定下列設定：  

    - **作業系統磁碟機加密設定**：如果您啟用此設定，使用者必須保護 OS 磁碟機和 BitLocker 加密磁碟機。 如果您停用此設定，則使用者無法保護磁碟機。  

    在具有相容 TPM 的裝置上，可以在啟動時使用兩種類型的驗證方法，為加密資料提供額外的保護。 電腦啟動時，可以只使用 TPM 進行驗證，也可以要求輸入個人識別碼 (PIN)。 進行以下設定：

    - **選取作業系統磁碟機的保護程式**：將其設定為使用 TPM 和 PIN，或僅 TPM。

    - **設定啟動的 PIN 長度下限**：如果您要求 PIN，此值會是使用者可以指定的最短長度。 使用者在電腦開機時輸入這個 PIN 來解除鎖定磁碟機。 根據預設，PIN 長度下限為 `4`。

    如需這些設定及此頁面上其他設定的詳細資訊，請參閱[設定參考 - OS 磁碟機](../../tech-ref/bitlocker/settings.md#os-drive)。

1. 在 [固定磁碟機]  頁面上，指定下列設定：

    - **固定資料磁碟機加密**：如果您啟用此設定，BitLocker 就會要求使用者將所有固定資料磁碟機置於保護之下。 接著，其會加密資料磁碟機。 當您啟用此原則時，請啟用自動解除鎖定或 [固定資料磁碟機密碼原則]  的設定。

    - **對固定資料磁碟機設定自動解除鎖定**：允許或要求 BitLocker 自動解除鎖定任何加密的資料磁碟機。 若要使用自動解除鎖定，也需要 BitLocker 加密 OS 磁碟機。

    如需這些設定及此頁面上其他設定的詳細資訊，請參閱[設定參考 - 固定磁碟機](../../tech-ref/bitlocker/settings.md#fixed-drive)。

1. 在 [抽取式磁碟機]  頁面上，指定下列設定：

    - **抽取式資料磁碟機加密**：當您啟用此設定並允許使用者套用 BitLocker 保護時，Configuration Manager 用戶端會將抽取式磁碟機的復原資訊儲存到管理點上的復原服務。 如果使用者忘記或遺失保護裝置 (密碼)，此行為可讓使用者復原磁碟機。

    - **允許使用者在抽取式資料磁碟機上套用 BitLocker 保護**：使用者可以對抽取式磁碟機開啟 BitLocker 保護。

    - **抽取式資料磁碟機密碼原則**：使用這些設定來設定解除鎖定受 BitLocker 保護之抽取式磁碟機的密碼限制。

    如需這些設定及此頁面上其他設定的詳細資訊，請參閱[設定參考 - 抽取式磁碟機](../../tech-ref/bitlocker/settings.md#removable-drive)。

1. 在 [用戶端管理]  頁面上，指定下列設定：

    > [!IMPORTANT]
    > 如果您沒有具備 HTTPS 功能之網站的管理點，請不要設定此設定。 如需詳細資訊，請參閱[復原服務](#recovery-service)。

    - **設定 BitLocker 管理服務**：如果您啟用此設定，Configuration Manager 會以無訊息方式將金鑰復原資訊自動備份到站台資料庫中。 如果您停用或未進行此設定，Configuration Manager 就不會儲存金鑰復原資訊。

        - **選取要儲存的 BitLocker 復原資訊**：您可以將其設定為使用復原密碼和金鑰套件，或僅復原密碼。

        - **允許以純文字格式儲存復原資訊**：如果沒有 BitLocker 管理加密憑證，Configuration Manager 就會以純文字格式儲存金鑰復原資訊。 如需詳細資訊，請參閱[加密復原資料](encrypt-recovery-data.md)。

    如需這些設定及此頁面上其他設定的詳細資訊，請參閱[設定參考 - 用戶端管理](../../tech-ref/bitlocker/settings.md#client-management)。

1. 完成精靈。

若要變更現有原則的設定，請在清單中選擇該原則，然後選取 [屬性]  。

當您建立一個以上的原則時，您可以設定其相對優先順序。 如果您將多個原則部署到用戶端，則其會使用優先順序值來判斷設定。

## <a name="deploy-a-policy"></a>部署原則

1. 在 [BitLocker 管理]  節點中，選擇現有的原則。 在功能區中，選取 [部署]  。

1. 選取裝置集合作為部署的目標。

1. 如果您想要讓裝置隨時都能加密或解密其磁碟機，請選取 [允許在維護期間以外補救]  選項。 如果集合有任何維護視窗，則其仍會補救此 BitLocker 原則。

1. 設定 [簡單]  或 [自訂]  排程。 根據預設，用戶端每隔 12 小時就會評估其與此原則的合規性。

1. 選取 [確定]  以部署原則。

您可以建立相同原則的多個部署。 若要檢視關於每個部署的其他資訊，請在 [BitLocker 管理]  節點中選取原則，然後在詳細資料窗格中切換至 [部署]  索引標籤。

## <a name="monitor"></a>監視

在 [BitLocker 管理]  節點的詳細資料窗格中，檢視關於原則部署的基本合規性統計資料：

- 符合規範計數
- 失敗計數
- 不符合規範計數

切換至 [部署]  索引標籤，以查看合規性百分比和建議的動作。 選取部署，然後在功能區中選取 [檢視狀態]  。 此動作會將檢視切換至 [監視]  工作區的 [部署]  節點。 與部署其他設定原則部署類似，您可以在此檢視中查看更詳細的合規性狀態。

若要了解為什麼用戶端會報告不符合 BitLocker 管理原則的規範，請參閱[不符合規範代碼](../../tech-ref/bitlocker/non-compliance-codes.md)。

如需詳細的疑難排解資訊，請參閱[針對 BitLocker 進行疑難排解](../../tech-ref/bitlocker/troubleshoot.md)。

使用下列記錄來進行監視與進行疑難排解：

### <a name="client-logs"></a>用戶端記錄

- MBAM 事件記錄檔：在 Windows 事件檢視器中，瀏覽至 [應用程式和服務] > [Microsoft] > [Windows] > [MBAM]。  如需詳細資訊，請參閱[關於 BitLocker 事件記錄檔](../../tech-ref/bitlocker/about-event-logs.md)與[用戶端事件記錄檔](../../tech-ref/bitlocker/client-event-logs.md)。

- 用戶端記錄路徑中的 **BitlockerMangementHandler.log**，根據預設為 `%WINDIR%\CCM\Logs`

### <a name="management-point-logs-recovery-service"></a>管理點記錄檔 (復原服務)

- 復原服務事件記錄檔：在 Windows 事件檢視器中，瀏覽至 [應用程式和服務] > [Microsoft] > [Windows] > [MBAM-Web]。 如需詳細資訊，請參閱[關於 BitLocker 事件記錄檔](../../tech-ref/bitlocker/about-event-logs.md)與[伺服器事件記錄檔](../../tech-ref/bitlocker/server-event-logs.md)。

- 復原服務追蹤記錄檔：`<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>復原服務

BitLocker 復原服務是一個伺服器元件，會接收來自 Configuration Manager 用戶端的 BitLocker 復原資料。 當您建立 BitLocker 管理原則時，此網站會部署復原服務。 Configuration Manager 會在有具備 HTTPS 功能之網站的每個管理點上自動安裝復原服務。

Configuration Manager 會將這些復原資訊儲存於站台資料庫中。 如果沒有 BitLocker 管理加密憑證，Configuration Manager 就會以純文字格式儲存金鑰復原資訊。

如需詳細資訊，請參閱[加密復原資料](encrypt-recovery-data.md)。

## <a name="migration-considerations"></a>移轉考量

如果您目前使用 Microsoft BitLocker Administration and Monitoring (MBAM)，就能順暢地將管理移轉至 Configuration Manager。 當您在 Configuration Manager 中部署 BitLocker 管理原則時，用戶端會自動將復原金鑰和套件上傳到 Configuration Manager 復原服務。

> [!IMPORTANT]
> 當您從獨立 MBAM 移轉至 Configuration Manager BitLocker 管理時，如果您需要獨立 MBAM 的現有功能，請勿搭配 Configuration Manager BitLocker 管理重複使用獨立 MBAM 伺服器或元件。 如果您重複使用這些伺服器，當 Configuration Manager BitLocker 管理在那些伺服器上安裝其元件時，獨立 MBAM 將會停止運作。 不要在獨立 MBAM 伺服器上執行 MBAMWebSiteInstaller.ps1 指令碼來設定 BitLocker 入口網站。 當您設定 Configuration Manager BitLocker 管理時，請使用不同的伺服器。

### <a name="group-policy"></a>群組原則

- BitLocker 管理設定與 MBAM 群組原則設定完全相容。 如果裝置同時收到群組原則設定和 Configuration Manager 原則，請設定來使其相符。

- Configuration Manager 不會實作所有 MBAM 群組原則設定。 如果您在群組原則中設定其他設定，Configuration Manager 用戶端上的 BitLocker 管理代理程式會接受這些設定。

### <a name="tpm-password-hash"></a>TPM 密碼雜湊

- 先前的 MBAM 用戶端不會將 TPM 密碼雜湊上傳至 Configuration Manager。 用戶端只會上傳 TPM 密碼雜湊一次。

- 如果您需要將此資訊移轉至 Configuration Manager 復原服務，請清除裝置上的 TPM。 重新啟動之後，其會將新的 TPM 密碼雜湊上傳至復原服務。

### <a name="re-encryption"></a>重新加密

Configuration Manager 不會重新加密已經使用 BitLocker 磁碟機加密來保護的磁碟機。 如果您部署不符合磁碟機目前保護的 BitLocker 管理原則，系統會將其報告為不符合規範。 磁碟機仍會受到保護。

例如，您使用 MBAM 來加密不具 PIN 保護的磁碟機，但 Configuration Manager 原則需要 PIN。 該磁碟機會因此不符合原則的規範，即使該磁碟機已加密也一樣。

若要解決此行為，請先停用裝置上的 BitLocker。 然後部署具有新設定的新原則。

## <a name="co-management-and-intune"></a>共同管理與 Intune

<!-- SCCMDocs#2321 -->

適用於 BitLocker 的 Configuration Manager 用戶端處理常式是共同管理感知的。 如果裝置是共同管理的，而您將 [Endpoint Protection 工作負載](../../../comanage/workloads.md#endpoint-protection)切換至 Intune，則 Configuration Manager 用戶端會忽略其 BitLocker 原則。 裝置會從 Intune 取得 Windows 加密原則。

當您切換加密管理授權單位時，請為[重新加密](#re-encryption)做規劃。

如需有關使用 Intune 來管理 BitLocker 的詳細資訊，請參閱下列文章：

- [搭配 Intune 使用裝置加密](../../../../intune/protect/encrypt-devices.md#bitlocker-encryption-for-windows-10)
- [針對 Microsoft Intune 中的 BitLocker 原則進行疑難排解](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>後續步驟

[設定 BitLocker 報告和入口網站](setup-websites.md)
