---
title: Microsoft Defender 進階威脅防護
titleSuffix: Configuration Manager
description: 了解如何管理及監視 Microsoft Defender 進階威脅防護，此為協助企業回應先進攻擊的一項新服務。
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801aee9665e567ce1a983fba294f1e58f58eee04
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406669"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender 進階威脅防護

適用於：Configuration Manager (最新分支)

Endpoint Protection 可協助管理及監視 [Microsoft Defender 進階威脅防護 (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (先前稱為 Windows Defender ATP)。 Microsoft Defender ATP 可協助企業偵測、調查及因應其公司網路上先進的攻擊。 Configuration Manager 原則可協助您上線及監視 Windows 10 用戶端。

Microsoft Defender ATP 是 [Windows Defender 資訊安全中心](https://securitycenter.windows.com)的一項服務。 新增及部署用戶端上架設定檔後，Configuration Manager 即可監視部署狀態與 Microsoft Defender ATP 代理程式健全狀況。 在執行 Configuration Manager 用戶端或[由 Microsoft Intune 管理](https://docs.microsoft.com/intune/protect/advanced-threat-protection)的電腦上，都支援 Microsoft Defender ATP。

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
- Windows Server 2016 1803 版
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>建立上線設定檔

1. 移至 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)並登入。
1. 選取 [設定] 下方的 [電腦管理]，然後選取 [上線]。
1. 從清單中選取要上線的作業系統。
   - 如果要讓 Windows 10、Windows Server 1803 和 Windows Server 2019 上線：
      1. 請選取 [Configuration Manager (最新分支) 1606 版]，然後選取 [下載套件]。
      1. 下載壓縮的封存檔案 (.zip)，並將內容解壓縮。
   - 如果要上線另一個 Windows 作業系統：
      1. 從 Microsoft Defender ATP 線上服務所提供的清單中選取您想要使其上線的作業系統。
      1. 當處理序完成時，從 [設定連線] 區段中，複製 [工作區金鑰] 和 [工作區識別碼] 的值。

> [!IMPORTANT]
> - Microsoft Defender ATP 設定檔包含應受到保護的敏感性資訊。

## <a name="onboard-devices"></a>將裝置上線

1. 在 Configuration Manager 主控台中，巡覽至 [資產與相容性] > [Endpoint Protection] > [Windows Defender ATP 原則]，然後選取 [建立 Windows Defender ATP 原則]。 [Microsoft Defender ATP 原則精靈] 隨即開啟。  
1. 輸入Microsoft Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [上線]。
1. **瀏覽**至組織的 Microsoft Defender ATP 雲端服務租用戶所提供設定檔。
   - 針對 Windows 8.1 或 Windows Server 2012 R2 與 2016，請提供 [工作區金鑰] 與 [工作區識別碼]。
   - 針對 Configuration Manager 2002 版，即使只是將 Windows Server 2019 和 Windows Server 1803 或更新版本的裝置上線，也會需要**工作區金鑰**和**工作區識別碼**。 從 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)選取 [設定] > [上線] > [Windows 7 和 8.1] 來取得這些值。 <!--7054188-->
1. 指定為了分析而從受管理裝置收集和分享的範例檔案。  

   - **無**

   - **所有檔案類型**  
1. 檢閱摘要並完成精靈。  

選取 [部署]，將 Microsoft Defender ATP 原則的目標設定為用戶端。

## <a name="monitor"></a>監視

1. 在 Configuration Manager 主控台中，巡覽至 [監視] > [安全性]，然後選取 [Windows Defender ATP]。  

1. 檢閱 [Microsoft Defender 進階威脅防護] 儀表板。  

    - **Windows Defender 代理程式部署狀態**：已將使用中 Microsoft Defender ATP 原則上線，且符合受控用戶端電腦的數目與百分比  

    - **Windows Defender ATP 代理程式健全狀況**：回報其 Microsoft Defender ATP 代理程式狀態的電腦用戶端百分比  

        - **狀況良好** - 運作正常  

        - **非使用中** - 在這段期間不會將任何資料傳送至服務  

        - **代理程式狀態** - Windows 中未執行此代理程式的系統服務  

        - **未上線** - 已套用原則，但代理程式尚未回報原則上線  

## <a name="create-an-offboarding-configuration-file"></a>建立離線設定檔  

1. 登入 [Microsoft Defender ATP 線上服務](https://securitycenter.windows.com/)。

1. 選取 [設定] 下方的 [電腦管理]，然後選取 [上線]。  

1. 選取 [Configuration Manager (最新分支) 1606 版]，然後選取 [端點離線]。  

1. 下載壓縮的封存檔案 (.zip)，並將內容解壓縮。 將檔案下架的有效期限為 30 天。

1. 在 Configuration Manager 主控台中，巡覽至 [資產與相容性] > [Endpoint Protection] > [Windows Defender ATP 原則]，然後選取 [建立 Windows Defender ATP 原則]。 [Microsoft Defender ATP 原則精靈] 隨即開啟。  

1. 輸入 Microsoft Defender ATP 原則的 [名稱] 和 [描述]，然後選取 [下線]。

1. **瀏覽**至組織的 Microsoft Defender ATP 雲端服務租用戶所提供設定檔。

1. 檢閱摘要並完成精靈。  

選取 [部署]，將 Microsoft Defender ATP 原則的目標設定為用戶端。  

> [!IMPORTANT]
> Microsoft Defender ATP 設定檔包含應受到保護的敏感性資訊。

## <a name="next-steps"></a>後續步驟

- [Microsoft Defender 進階威脅防護](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [針對 Microsoft Defender 進階威脅防護上線問題進行疑難排解](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
