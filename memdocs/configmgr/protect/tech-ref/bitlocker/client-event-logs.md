---
title: 用戶端事件記錄檔
titleSuffix: Configuration Manager
description: Windows 事件記錄檔中可能之 BitLocker (MBAM) 用戶端項目的技術參考
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c38b6963-cb1f-40ed-a888-e19d401ec3fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4043af4aa30942a5e8e1f7d2a3d1017c1e72d89f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705966"
---
# <a name="client-event-logs"></a>用戶端事件記錄檔

適用於：  Configuration Manager (最新分支)

<!--3601034-->

在您要部署 BitLocker 管理原則的 Configuration Manager 用戶端上，請使用 Windows 事件檢視器來檢視 BitLocker 用戶端事件記錄檔。 針對[系統管理員](#admin)和[作業](#operational)事件記錄檔，請移至 [應用程式及服務記錄檔]  、[Microsoft]  、[Windows]  、[MBAM]  。

## <a name="admin"></a>系統管理員

### <a name="2-volumeenactmentfailed"></a>2：VolumeEnactmentFailed

套用 MBAM 原則時發生錯誤。

#### <a name="error-code--2144272219"></a>錯誤碼：-2144272219

詳細資料：BitLocker 磁碟機加密只支援精簡佈建儲存體上的僅加密已使用空間。

如果您嘗試使用 BitLocker 來加密執行 Windows 10 1803 版或更早版本的虛擬機器，就會發生此錯誤。 更早版本的 Windows 10 不支援完整磁碟加密。 BitLocker 管理原則會強制執行完整磁碟加密。

#### <a name="error-code--2147024774"></a>錯誤碼：-2147024774

詳細資料：傳遞給系統呼叫的資料區域太小。

若要解決此問題，請重新啟動電腦。

### <a name="4-transferstatusdatafailed"></a>4：TransferStatusDataFailed

傳送加密狀態資料時發生錯誤。

### <a name="8-systemvolumenotfound"></a>8：SystemVolumeNotFound

系統磁碟區已遺失。 需要系統磁碟區才能加密作業系統磁碟機。

### <a name="9-tpmnotfound"></a>9：TPMNotFound

TPM 硬體已遺失。 需要 TPM 才能使用任何 TPM 保護裝置加密作業系統磁碟機。

### <a name="10-machinehwexempted"></a>10：MachineHWExempted

電腦已豁免加密。 機器的硬體狀態：已豁免

### <a name="11-machinehwunknown"></a>11：MachineHWUnknown

電腦已豁免加密。 機器的硬體狀態：Unknown

### <a name="12-hwcheckfailed"></a>12：HWCheckFailed

硬體豁免檢查失敗。

### <a name="13-userisexempted"></a>13：UserIsExempted

使用者已豁免加密。

### <a name="14-useriswaiting"></a>14：UserIsWaiting

使用者已要求豁免。

### <a name="15-userexemptioncheckfailed"></a>15：UserExemptionCheckFailed

使用者豁免檢查失敗。

### <a name="16-userpostponed"></a>16：UserPostponed

使用者已延遲加密程序。

### <a name="17-tpminitializationfailed"></a>17：TPMInitializationFailed

TPM 初始化失敗。 使用者已拒絕 BIOS 變更。

### <a name="18-coreservicedown"></a>18：CoreServiceDown

無法連線至 MBAM Recovery and Hardware 服務。

#### <a name="error-code--2147024809"></a>錯誤碼：-2147024809

詳細資料：參數不正確。

如果網站不是 HTTPS，或用戶端沒有 PKI 憑證，就會發生此錯誤。

### <a name="20-policymismatch"></a>20：PolicyMismatch

BitLocker 管理原則發生衝突或已損毀。

### <a name="21-conflictingosvolumepolicies"></a>21：ConflictingOSVolumePolicies

偵測到 OS 磁碟區加密原則衝突。 檢查與 OS 磁碟機保護裝置相關的 BitLocker 原則。

### <a name="22-conflictingfddvolumepolicies"></a>22：ConflictingFDDVolumePolicies

偵測到固定資料磁碟機磁碟區加密原則衝突。 請檢查與固定資料磁碟機保護裝置相關的 BitLocker 原則。

### <a name="27-encryptionfailednodra"></a>27：EncryptionFailedNoDra

加密時發生錯誤。 Windows 8.1 版以前的電腦需要啟用 FIPS 模式的資料修復代理 (DRA) 保護裝置。

### <a name="34-tpmlockoutresetfailed"></a>34：TpmLockOutResetFailed

無法重設 TPM 鎖定。

### <a name="36-tpmownerauthretrievalfailed"></a>36：TpmOwnerAuthRetrievalFailed

無法從 MBAM 服務擷取 TPM OwnerAuth。

### <a name="37-wmiproviderdllsearchpathupdatefailed"></a>37：WmiProviderDllSearchPathUpdateFailed

無法更新 WMI 提供者的 DLL 搜尋路徑。

### <a name="38-timedoutwaitingforwmiprovider"></a>38：TimedOutWaitingForWmiProvider

代理程式正在停止。 等候 MBAM WMI 提供者執行個體時發生逾時。

## <a name="operational"></a>作業

### <a name="1-volumeenactmentsuccessful"></a>1：VolumeEnactmentSuccessful

已成功套用 BitLocker 管理原則。

### <a name="3-transferstatusdatasuccessful"></a>3：TransferStatusDataSuccessful

已成功傳送加密狀態資料。

### <a name="19-coreserviceup"></a>19：CoreServiceUp

已成功連線至 MBAM Recovery and Hardware 服務。

### <a name="28-tpmownerauthescrowed"></a>28：TpmOwnerAuthEscrowed

已委付 TPM OwnerAuth。

### <a name="29-recoverykeyescrowed"></a>29：RecoveryKeyEscrowed

已委付磁碟區的 BitLocker 修復金鑰。

### <a name="30-recoverykeyreset"></a>30：RecoveryKeyReset

已更新磁碟區的 BitLocker 修復金鑰。

### <a name="31-enforcepolicydateset"></a>31：EnforcePolicyDateSet

已設定磁碟區的強制執行原則日期

### <a name="32-enforcepolicydatecleared"></a>32：EnforcePolicyDateCleared

已清除磁碟區的強制執行原則日期。

### <a name="33-tpmlockoutresetsucceeded"></a>33：TpmLockOutResetSucceeded

已成功重設 TPM 鎖定。

### <a name="35-tpmownerauthretrievalsucceeded"></a>35：TpmOwnerAuthRetrievalSucceeded

已成功從 MBAM 服務擷取 TPM OwnerAuth。

### <a name="39-removabledrivemounted"></a>39：RemovableDriveMounted

已掛接抽取式磁碟機。

### <a name="40-removabledrivedismounted"></a>40：RemovableDriveDismounted

已取消掛接抽取式磁碟機。

### <a name="41-failedtoenactendpointunreachable"></a>41：FailedToEnactEndpointUnreachable

無法連線到 MBAM Recovery and Hardware 服務，導致了 BitLocker 管理原則無法成功套用至磁碟區。

### <a name="42-failedtoenactlockedvolume"></a>42：FailedToEnactLockedVolume

鎖定的磁碟區狀態導致 BitLocker 管理原則無法成功套用至磁碟區。

### <a name="43-transferstatusdatafailedendpointunreachable"></a>43：TransferStatusDataFailedEndpointUnreachable

無法連線到 MBAM Compliance and Status 服務，導致了加密狀態資料無法傳送。

## <a name="see-also"></a>請參閱

如需有關使用這些記錄檔的詳細資訊，請參閱 [BitLocker 事件記錄檔](about-event-logs.md)。

如需詳細的疑難排解資訊，請參閱[針對 BitLocker 進行疑難排解](troubleshoot.md)。
