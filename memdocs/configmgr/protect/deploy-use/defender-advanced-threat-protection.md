---
title: Microsoft Defender 進階威脅防護
titleSuffix: Configuration Manager
description: 了解如何管理及監視 Microsoft Defender 進階威脅防護，此為協助企業回應先進攻擊的一項新服務。
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613453"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender 進階威脅防護

適用於：Configuration Manager (最新分支)

Endpoint Protection 可協助管理及監視 [Microsoft Defender 進階威脅防護 (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (先前稱為 Windows Defender ATP)。 Microsoft Defender ATP 可協助企業偵測、調查及因應其公司網路上先進的攻擊。 Configuration Manager 原則可協助您上線及監視 Windows 10 用戶端。

Microsoft Defender ATP 是 [Microsoft Defender 資訊安全中心](https://securitycenter.windows.com)的一項服務。 新增及部署用戶端上架設定檔後，Configuration Manager 即可監視部署狀態與 Microsoft Defender ATP 代理程式健全狀況。 在執行 Configuration Manager 用戶端或[由 Microsoft Intune 管理](https://docs.microsoft.com/intune/protect/advanced-threat-protection)的電腦上，都支援 Microsoft Defender ATP。

## <a name="prerequisites"></a>先決條件

- 訂閱 Microsoft Defender 進階威脅防護線上服務  
- 執行 Configuration Manager 用戶端的用戶端電腦
- 使用[支援的用戶端作業系統](#bkmk_os)一節中所列 OS 的用戶端。

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> 支援的用戶端作業系統

根據正在執行的 Configuration Manager 版本，下列用戶端作業系統可以上線：

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager 1910 版和較舊版本

- 執行 Windows 10 (1607 版及更新版本) 的用戶端電腦

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager 2002 版和更新版本
<!--5229962-->
從 Configuration Manager 2002 版開始，您可以將下列作業系統上線：

- Windows 8.1
- Windows 10 1607 版或更新版本
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016 1803 版或更新版本
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>如何使用 Configuration Manager 上線至 ATP

使用不同作業系統上線到 ATP 時，其需求也不同。 若是 Windows 8.1 和其他下層作業系統裝置，則需要使用**工作區金鑰**和**工作區識別碼**才能上線。 上層裝置 (例如 Windows Server 1803 版) 則需要上線設定檔。 當上線裝置需要 Microsoft Monitoring Agent (MMA) 時，Configuration Manager 也會加以安裝，但不會自動更新代理程式。

上層作業系統包含：
- Windows 10 1607 版和更新版本
- Windows Server 2016 1803 版或更新版本
- Windows Server 2019

下層作業系統包含：
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016 1709 版和更早版本

使用 Configuration Manager 將裝置上線到 ATP 時，您會將 ATP 原則部署至目標集合或多個集合。 有時目標集合所含裝置會執行任意數量的支援作業系統。 這些裝置的上線指示是根據目標集合所含裝置為上層及/或下層作業系統而定。

- 如果目標集合同時包含上層和下層裝置，請依照指示[將執行任何支援作業系統的裝置上線](#bkmk_any_os) (建議使用)。
- 如果集合只包含上層裝置，請使用[上層上線指示](#bkmk_uplevel)。
- 如果集合只包含下層裝置，請使用[下層上線指示](#bkmk_downlevel)。

> [!Warning]
> - 如果目標集合包含上層裝置，且您使用下層裝置的指示，則無法成功將上層裝置上線。
> - 如果目標集合包含下層裝置，且您使用上層裝置的指示，則無法成功將下層裝置上線。

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a> 將執行任何支援作業系統的裝置上線到 ATP (建議使用)
 您可提供 Configuration Manager 所需的設定檔、**工作區金鑰**和**工作區識別碼**，以將執行任何[支援作業系統](#bkmk_os)的裝置上線至 ATP。

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>取得設定檔、工作區識別碼和工作區金鑰

1. 移至 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)並登入。
1. 選取 [設定]，然後選取 [裝置管理] 標題下的 [上線]。
1. 針對作業系統，選取 [Windows 10]。
1. 針對部署方法，選擇 [Microsoft Endpoint Configuration Manager 最新分支和更新版本]。
1. 按一下 [下載套件]。
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="下載上線設定檔" lightbox="media/5229962-onboarding-configuration.png":::
1. 下載壓縮的封存檔案 (.zip)，並將內容解壓縮。
1. 選取 [設定]，然後選取 [裝置管理] 標題下的 [上線]。
1. 針對作業系統，請從清單中選取 [Windows 7 SP1 和 8.1] 或 [Windows Server 2008 R2 Sp1、2012 R2 和 2016]。
   - 無論選擇哪一個選項，**工作區金鑰**和**工作區識別碼**都相同。
1. 從 [設定連線] 區段中，複製 [工作區金鑰] 和 [工作區識別碼] 的值。

   > [!IMPORTANT]
   > Microsoft Defender ATP 設定檔包含應受到保護的敏感性資訊。


### <a name="onboard-the-devices"></a>將裝置上線

1. 在 Configuration Manager 主控台中，巡覽至 [資產與相容性] > [Endpoint Protection] > [Windows Defender ATP 原則]。
1. 選取 [建立 Windows Defender ATP 原則]，開啟 [Microsoft Defender ATP 原則精靈]。 
1. 輸入Microsoft Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [上線]。
1. 選取 [瀏覽]，找到從已下載 .zip 檔案解壓縮的設定檔案。
1. 提供**工作區金鑰**及**工作區識別碼**，然後按一下 [下一步]。

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="建立 Microsoft Defender ATP 原則精靈" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. 指定為了分析而從受管理裝置收集和分享的範例檔案。  
   - **無**
   - **所有檔案類型**  
1. 檢閱摘要並完成精靈。  
1. 以滑鼠右鍵按一下所建立的原則，然後選取 [部署]，將 Microsoft Defender ATP 原則的目標設定為用戶端。

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a> 將執行上層作業系統的裝置上線至 ATP

上層用戶端需要需要上線設定檔才能上線至 ATP。 上層作業系統包含：
- Windows 10 1607 版和更新版本 
- Windows Server 2016 1803 版和更新版本
- Windows Server 2019

如果目標集合同時包含上層和下層裝置，或不確定包含哪種裝置，請依照指示[將執行任何支援作業系統的裝置上線 (建議使用)](#bkmk_any_os)。

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>取得上層裝置的上線設定檔

1. 移至 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)並登入。
1. 選取 [設定]，然後選取 [裝置管理] 標題下的 [上線]。
1. 針對作業系統，選取 [Windows 10]。
1. 針對部署方法，選擇 [Microsoft Endpoint Configuration Manager 最新分支和更新版本]。
1. 按一下 [下載套件]。
1. 下載壓縮的封存檔案 (.zip)，並將內容解壓縮。

> [!IMPORTANT]
> Microsoft Defender ATP 設定檔包含應受到保護的敏感性資訊。


### <a name="onboard-the-up-level-devices"></a>將上層裝置上線

1. 在 Configuration Manager 主控台中，巡覽至 [資產與相容性] > [Endpoint Protection] > [Microsoft Defender ATP 原則]，然後選取 [建立 Microsoft Defender ATP 原則]。 [Microsoft Defender ATP 原則精靈] 隨即開啟。  
1. 輸入Microsoft Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [上線]。
1. 選取 [瀏覽]，找到從已下載 .zip 檔案解壓縮的設定檔案。
   > [!Note]
   > 針對 Configuration Manager 2002 版，即使只是將上層裝置上線，也需要使用**工作區金鑰**和**工作區識別碼**。 從 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)選取 [設定] > [上線] > [Windows 7 和 8.1] 來取得這些值。 <!--7054188-->
1. 指定為了分析而從受管理裝置收集和分享的範例檔案。  
   - **無**
   - **所有檔案類型**  
1. 檢閱摘要並完成精靈。  
1. 以滑鼠右鍵按一下所建立的原則，然後選取 [部署]，將 Microsoft Defender ATP 原則的目標設定為用戶端。

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a> 將執行下層作業系統的裝置上線至 ATP

下層用戶端需要使用**工作區金鑰**以及**工作區識別碼**，才能進行 ATP 上線。 下層作業系統包含：
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016 1709 版和更早版本

如果目標集合同時包含上層和下層裝置，或不確定包含哪種裝置，請依照指示[將執行任何支援作業系統的裝置上線 (建議使用)](#bkmk_any_os)。

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>取得下層裝置的工作區識別碼和工作區金鑰

1. 移至 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)並登入。
1. 選取 [設定]，然後選取 [裝置管理] 標題下的 [上線]。
1. 針對作業系統，請從清單中選取 [Windows 7 SP1 和 8.1] 或 [Windows Server 2008 R2 Sp1、2012 R2 和 2016]。
   - 無論選擇哪一個選項，**工作區金鑰**和**工作區識別碼**都相同。
1. 從 [設定連線] 區段中，複製 [工作區金鑰] 和 [工作區識別碼] 的值。

### <a name="onboard-the-down-level-devices"></a>將下層裝置上線

1. 在 Configuration Manager 主控台中，巡覽至 [資產與相容性] > [Endpoint Protection] > [Microsoft Defender ATP 原則]，然後選取 [建立 Microsoft Defender ATP 原則]。 [Microsoft Defender ATP 原則精靈] 隨即開啟。  
1. 輸入Microsoft Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [上線]。
1. 提供**工作區金鑰**和**工作區識別碼**。
   > [!Note]
   > - 針對 Configuration Manager 2002 版，即使只需將下層裝置上線，也需要使用設定檔。 從 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)選取 [設定] > [上線] > [Windows 10] 來取得這些值。 <!--7054188--> 
   > - Microsoft Defender ATP 設定檔包含應受到保護的敏感性資訊。
1. 指定為了分析而從受管理裝置收集和分享的範例檔案。  
   - **無**
   - **所有檔案類型**  
1. 檢閱摘要並完成精靈。  
1. 以滑鼠右鍵按一下所建立的原則，然後選取 [部署]，將 Microsoft Defender ATP 原則的目標設定為用戶端。


## <a name="monitor"></a>監視

1. 在 Configuration Manager 主控台中，巡覽至 [監視] > [安全性]，然後選取 [Microsoft Defender ATP]。  

1. 檢閱 [Microsoft Defender 進階威脅防護] 儀表板。  

    - **Microsoft Defender ATP 代理程式上線狀態**：已將使用中 Microsoft Defender ATP 原則上線，且符合受控用戶端電腦的數目與百分比  

    - **Microsoft Defender ATP 代理程式健全狀況**：回報其 Microsoft Defender ATP 代理程式狀態的電腦用戶端百分比  

        - **狀況良好** - 運作正常  

        - **非使用中** - 在這段期間不會將任何資料傳送至服務  

        - **代理程式狀態** - Windows 中未執行此代理程式的系統服務  

        - **未上線** - 已套用原則，但代理程式尚未回報原則上線  

## <a name="create-an-offboarding-configuration-file"></a>建立離線設定檔  

1. 登入 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)。
1. 選取 [設定]，然後選取 [裝置管理] 標題下的 [離線]。
1. 針對作業系統，選取 [Windows 10]並針對部署方法，選取 [Microsoft Endpoint Configuration Manager 最新分支和更新版本]。
   - 使用 [Windows 10] 選項可確保集合中的所有裝置都離線，並在需要時解除安裝 MMA。
1. 下載壓縮的封存檔案 (.zip)，並將內容解壓縮。 將檔案下架的有效期限為 30 天。

1. 在 Configuration Manager 主控台中，巡覽至 [資產與相容性] > [Endpoint Protection] > [Microsoft Defender ATP 原則]，然後選取 [建立 Microsoft Defender ATP 原則]。 [Microsoft Defender ATP 原則精靈] 隨即開啟。  

1. 輸入 Microsoft Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [下線]。

1. 選取 [瀏覽]，找到從已下載 .zip 檔案解壓縮的設定檔案。

1. 檢閱摘要並完成精靈。  

選取 [部署]，將 Microsoft Defender ATP 原則的目標設定為用戶端。  

> [!IMPORTANT]
> Microsoft Defender ATP 設定檔包含應受到保護的敏感性資訊。

## <a name="next-steps"></a>後續步驟

- [Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [針對 Microsoft Defender 進階威脅防護上線問題進行疑難排解](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
