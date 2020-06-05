---
title: 使用 Microsoft Intune 的端點安全性管理裝置 | Microsoft Docs
description: 了解安全性系統管理員如何使用端點安全性節點檢視裝置，並採取行動以在 Microsoft 端點管理員中管理裝置。
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
ms.openlocfilehash: 8171eb3cf484c61e2b99046b36553a633d92044e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431458"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>使用 Microsoft Intune 的端點安全性管理裝置

身為安全性系統管理員，請使用 Microsoft Endpoint Manager 系統管理中心內的 [所有裝置] 檢視，檢閱管理您的裝置並採取相應行動。 此檢視會顯示您 Azure Active Directory (Azure AD) 中所有裝置的清單。 包括分別受 Intune 和 Configuration Manager 管理的裝置，以及透過 Intune 和 Configuration Manager [共同管理](https://docs.microsoft.com/configmgr/comanage/overview)的裝置。 與您的 Azure AD 整合後，裝置可以位在雲端，也可以來自您的內部部署基礎結構。

 若要尋找此檢視，請開啟 [Microsoft Endpoint Manager 系統管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然後選取 [端點安全性] > [所有裝置]。

初始的 [所有裝置] 檢視會顯示您的裝置，並包括各自的重要資訊：

- 裝置的管理方式
- 合規性狀態
- 作業系統詳細資料
- 裝置上次存回的時間
- 更多

![系統管理中心的 [所有裝置] 檢視](./media/endpoint-security-manage-devices/all-device-view.png)

檢視裝置詳細資料時，您可以選取要鑽研取得詳細資訊的裝置。

## <a name="available-details-by-management-type"></a>依管理類型排列的可用詳細資料

在 Microsoft Endpoint Manager 系統管理中心內檢視裝置時，請考慮裝置的管理方式。 管理來源會影響系統管理中心呈現的資訊，以及可用來管理裝置的動作。

請考慮下列欄位：

- [管理者] – 此欄會識別裝置的管理方式。 [管理者] 選項包括：

  - [MDM] - 由 Intune 管理的裝置。 Intune 會收集相容性資料，並向系統管理中心回報。

  - [ConfigMgr] – 當您使用 *[租用戶連結]* 新增使用 Configuration Manager 管理的裝置時，這些裝置就會出現在 Microsoft Endpoint Manager 系統管理中心。 為受此工具管理，裝置必須執行 Configuration Manager 用戶端，且：

    - 在工作群組中 (已加入 AAD 及其他)
    - 已加入網域
    - 已加入混合式 AAD (已加入 AD 和 AAD)

    Microsoft Endpoint Manager 系統管理中心不會顯示使用 Configuration Manager 管理的裝置相容性狀態。

    如需詳細資訊，請參閱 Configuration Manager 文件中的[啟用租用戶連結](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions)。

  - **[MDM/ConfigMgr 代理程式]** – 由 Intune 和 Configuration Manager 共同管理的裝置。

    透過共同管理，您可以[選擇不同的共同管理工作負載](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)，決定由 Configuration Manager 或 Intune 管理的層面。 這些選項會影響裝置套用的原則，以及如何向系統管理中心報告相容性資料。

    例如，您可以使用 Intune 設定防毒軟體、防火牆和加密原則。 這些原則類型會視為 *Endpoint Protection* 原則。 若要讓共同管理的裝置使用 Intune 原則，而不是 Configuration Manager 原則，請將 Endpoint Protection 的共同管理滑杆設定為 *[Intune]* 或 *[試驗 Intune]* 。 如果滑杆設定為 [Configuration Manager]，此裝置即會改用 Configuration Manager 的原則和設定。

- [合規性]：合規性評估是以指派給裝置的相容性原則為依據。 這些原則的來源和主控台中的資訊，會因裝置的管理方式而異：Intune、Configuration Manager 或共同管理。 若要讓共同管理的裝置報告合規性，請將 [裝置相容性] 的共同管理滑杆設定為 [Intune] 或 [Pilot Intune] \(試驗 Intune\)。  

  向系統管理中心回報裝置的相容性之後，您就可以鑽研詳細資料，以檢視其他詳細資料。 當裝置不相容時，請鑽研其詳細資料，以了解哪些原則不符合規範。 該資訊可協助您調查並協助您使裝置符合規範。

- [上次存回時間]：此欄位會識別裝置上次回報狀態的時間。

## <a name="review-a-devices-policy"></a>檢閱裝置原則

在檢視裝置清單時，您可以開啟裝置的 [概觀] 頁面，選取要鑽研詳細資訊的裝置。

然後，在裝置的概觀頁面中，選取 **[端點安全性設定]** ，以檢視套用至該裝置的端點安全性原則。 即可取得受 MDM 和 Intune 管理的裝置原則詳細資料。

![檢視端點安全性原則詳細資料](./media/endpoint-security-manage-devices/view-policy-details.png)

由 Configuration Manager 管理的裝置不顯示原則詳細資料。 若要檢視這些裝置的其他資訊，請使用 Configuration Manager 主控台。

## <a name="remote-actions-for-devices"></a>裝置的遠端動作

遠端動作是您可以從 Microsoft Endpoint Manager 系統管理中心啟動或套用至裝置的動作。 當您檢視裝置的詳細資料時，您可以存取套用至該裝置的遠端動作。

遠端動作會顯示在裝置 [概觀] 頁面的頂端。 您可以選取右側的省略號，取得因螢幕空間有限而無法顯示的動作：

![檢視其他動作](./media/endpoint-security-manage-devices/view-additional-actions.png)

可用的遠端動作視裝置管理方式而定：

- **Intune**：適用於裝置平台的所有 [Intune 遠端動作](../remote-actions/device-management.md)皆可用。  
- **Configuration Manager**：您可使用下列 Configuration Manager 動作：

  - 同步處理電腦原則
  - 同步處理使用者原則
  - 應用程式評估週期

- **共同管理**：Intune 遠端動作和 Configuration Manager 動作皆可存取。

有些 Intune 遠端動作可協助保護裝置或留置在裝置中的資料安全。 透過遠端動作，您可以：

- 鎖定裝置
- 重設裝置
- 移除公司資料
- 在排程執行以外掃描是否有惡意程式碼
- 輪換 BitLocker 金鑰

下列是安全性系統管理員感興趣的 Intune 遠端動作，是[完整清單](../remote-actions/device-inventory.md#view-the-device-details)的一部分。 並非所有裝置平台都能使用所有動作。 提供每個動作深入詳細資料內容的連結。

- [同步處理裝置](../remote-actions/device-sync.md) – 讓裝置立即存回 Intune。 裝置存回時，會收到所有擱置動作或已指派的原則。  

- [重新開機](../remote-actions/device-restart.md) – 在五分鐘內強制 Windows 10 裝置重新開機。 重新開機時不會自動通知裝置擁有者，所以工作可能會遺失。

- [快速掃描](../configuration/device-restrictions-windows-10.md) – 讓 Defender 對裝置執行快速掃描，查看是否有惡意程式碼，然後將結果提交至 Intune。 快速掃描會查看可能出現惡意程式碼的常見位置，例如登錄機碼和已知的 Windows 啟動資料夾。

- [完整掃描](../configuration/device-restrictions-windows-10.md) – 讓 Defender 對裝置執行掃描，查看是否有惡意程式碼，然後將結果提交至 Intune。 完整掃描會查看可能出現惡意程式碼的常見位置，同時掃描裝置中的每個檔案和資料夾。

- 更新 Windows Defender 安全性情報 – 讓裝置更新其 Microsoft Defender 防毒軟體的惡意程式碼定義。 此動作不會啟動掃描。

- [BitLocker 金鑰輪換](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – 從遠端為執行 Windows 10 1909 版或更新版本的裝置輪換 BitLocker 修復金鑰。

您也可以同時在多部裝置上使用 **大量裝置動作**來管理某些動作，例如淘汰和抹除。 [[大量動作]](../remote-actions/bulk-device-actions.md) 可從 [所有裝置] 檢視中取得。 您將選取平台、動作，然後指定最多 100 部裝置。

![選取 [大量動作]](./media/endpoint-security-manage-devices/select-bulk-actions.png)

在裝置存回 Intune 之前，您管理的裝置選項都不會生效。

## <a name="next-steps"></a>後續步驟

[在 Intune 中管理端點安全性](../protect/endpoint-security.md)