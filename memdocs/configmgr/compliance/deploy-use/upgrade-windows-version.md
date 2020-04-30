---
title: 將 Windows 裝置升級至不同的版本
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 自動將 Windows 10 裝置升級至不同的 Windows 版本。
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77ef255a820104ef2042a370b5056677fddb9d12
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692296"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>使用 Configuration Manager 將 Windows 裝置升級至新版本

適用於：  Configuration Manager (最新分支)

您可利用**版本升級原則**，將 Windows 10 裝置自動升級至不同版本。

下列是支援的升級路徑：

- 從 Windows 10 專業版到 Windows 10 企業版
- 從 Windows 10 家用版到 Windows 10 教育版
- 從 Windows 10 Mobile 到 Windows 10 Mobile Enterprise

裝置必須執行 Configuration Manager 用戶端軟體。 不支援由[內部部署 MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) 管理的裝置。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

在開始將裝置升級至最新版本之前，請檢閱下列必要條件：  

- Windows 10 桌面版：以原則在所有裝置上設為目標的新版 Windows 有效產品金鑰。 此產品金鑰可為多次啟用金鑰 (MAK) 或泛型的大量授權金鑰 (GVLK)。 GVLK 也稱為金鑰管理服務 (KMS) 的用戶端安裝金鑰。 如需詳細資訊，請參閱[大量啟用計劃](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 用戶端安裝金鑰的清單，請參閱＜Windows Server 啟用指南 ＞的[附錄 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。 <!--496871-->  

- Windows 10 行動裝置版：Microsoft 大量授權服務中心 (VLSC) 的 XML 授權檔案。 這個檔案包含您以原則在所有裝置上設為目標之新版 Windows 的授權資訊。

- 若要管理此原則類型，您必須是 Configuration Manager 的**系統高權限管理員**安全性角色。

## <a name="configure-the-policy"></a>設定原則  

1. 在 Configuration Manager 主控台中，前往 [資產與合規性]  工作區並展開 [合規性設定]  ，然後選取 [Windows 10 版本升級]  節點。  

2. 在功能區 [首頁]  索引標籤的 [建立]  群組中，選取 [建立版本升級原則]  。  

3. 選取[建立原則]  。  

4. 在 [建立版本升級原則精靈]  的 [一般]  頁面上，指定下列資訊：  

    - **名稱** - 輸入版本升級原則的名稱  

    - **描述** (選用) - 也可輸入能協助您在 Configuration Manager 主控台中識別此原則的原則描述  

    - **升級裝置用的 SKU** - 從下拉式清單中選取 Windows 10 Desktop 或 Windows 10 行動裝置版的目標版本  

    - **授權資訊** - 選取下列其中一個選項：  

        - **產品金鑰** - 輸入目標 Windows 10 Desktop 的有效產品金鑰  

            > [!NOTE]  
            > 建立包含產品金鑰的原則之後，稍後無法再編輯產品金鑰。 Configuration Manager 基於安全性會遮蔽金鑰。 若要變更產品金鑰，請再次輸入完整的金鑰。  

        - **授權檔** - 選取 [瀏覽]  以選擇 XML 格式的有效授權檔。 Configuration Manager 會使用此授權檔升級 Windows 10 行動裝置。  

5. 完成精靈。  

## <a name="deploy-the-policy"></a>部署原則  

1. 在 Configuration Manager 主控台中，前往 [資產與合規性]  工作區並展開 [合規性設定]  ，然後選取 [Windows 10 版本升級]  節點。  

2. 選取您想要部署的 Windows 10 版本升級原則。 在功能區 [常用]  索引標籤上的 [部署]  群組中，選取 [部署]  。  

3. 選擇您想要將原則部署至其中的裝置集合。

4. 選取用戶端評估原則的排程。

5. 完成精靈。

## <a name="next-steps"></a>後續步驟

從 [監視]  工作區的 [部署]  節點監視此部署。 如果看到指出不成功部署的錯誤，例如：

- **不適用於此裝置**
- **資料類型轉換失敗**

這些錯誤並不表示部署失敗。 在目標裝置上確認執行升級成功。

用戶端評估設目標原則之後，就會在兩個小時內套用升級。 [某些版本的 Windows](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades) (部分機器翻譯) 屆時可能需要重新啟動。 請務必通知所有您要部署該原則的使用者，或將原則排程在非使用者上班時間執行。

如果用戶端上的 **DcmWmiProvider.log** 出現下列錯誤，請確認您的啟用案例是使用正確的金鑰。 如需詳細資訊，請參閱[開始之前](#before-you-start)一節。 若目前使用金鑰管理服務 (KMS) 啟用，請務必使用 [KMS 用戶端安裝金鑰](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>請參閱

- [大量啟用規劃](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client) (部分機器翻譯)

- [Windows 10 版本升級](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [使用 Microsoft Intune 在裝置上升級 Windows 10 版本或切換移出 S 模式](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)
