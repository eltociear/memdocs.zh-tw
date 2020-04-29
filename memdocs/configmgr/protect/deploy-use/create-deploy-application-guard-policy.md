---
title: 管理應用程式防護原則
titleSuffix: Configuration Manager
description: 了解如何建立及部署 Windows Defender 應用程式防護原則
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 241e7ed9a2195e178cc1aac2ee2a146eea60b093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705746"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>建立及部署 Windows Defender 應用程式防護原則

適用於：  Configuration Manager (最新分支)
<!-- 1351960 -->  
您可以使用 Configuration Manager Endpoint Protection，建立及部署 [Windows Defender 應用程式防護原則 (Application Guard)](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。 這些原則可在作業系統其他部分所無法存取的安全隔離容器中開啟未受信任的網站，來協助保護您的使用者。

## <a name="prerequisites"></a>先決條件

若要建立及部署 Windows Defender 應用程式防護原則，必須使用 Windows 10 Fall Creators Update (1709)。 您必須使用網路隔離原則設定要部署原則的 Windows 10 裝置。 如需詳細資訊，請參閱 [Windows Defender Application Guard overview](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) (Windows Defender 應用程式防護概觀)。

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>建立原則並瀏覽可用的設定

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]  。
2. 在 [資產與合規性]  工作區中，選擇 [概觀]   > [Endpoint Protection]   > [Windows Defender 應用程式防護]  。
3. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立 Windows Defender 應用程式防護原則]  。
4. 您可以參考[文章](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) \(英文\)，瀏覽並設定可用的設定。 Configuration Manager 可讓您設定特定的原則設定：
   - [主機互動設定](#bkmk_HIS)
   - [應用程式行為](#bkmk_ABS)
   - [檔案管理](#bkmk_FM)
5. 在 [網路定義]  頁面上指定公司身分識別，以及定義您的公司網路界限。

    > [!NOTE]
    > Windows 10 電腦只會在用戶端上儲存一份網路隔離清單。 您可以建立兩種不同的網路隔離清單，並將它們部署至用戶端：
    >
    >  - 一個來自 Windows 資訊保護
    >  - 一個來自 Windows Defender 應用程式防護
    >
    > 如果您兩個原則都部署，則這些網路隔離清單必須相符。 若您部署的清單，與同一部用戶端不符，部署將會失敗。 如需詳細資訊，請參閱 [Windows 資訊保護文件](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)。

6. 完成操作時，請完成精靈步驟，然後將原則部署到一或多個 Windows 10 1709 裝置。

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> 主機互動設定

設定主機裝置和應用程式防護容器之間的互動。 在 Configuration Manager 1802 版之前，應用程式行為和主機互動都位在 [設定]  索引標籤底下。

- **剪貼簿**：在 Configuration Manager 1802 之前位在設定底下
  - 允許的內容類型
    - 文字
    - 映像
- **列印：**
  - 啟用列印至 XPS
  - 啟用列印至 PDF
  - 啟用列印至本機印表機
  - 啟用列印至網路印表機
- **圖形：** (從 Configuration Manager 1802 版開始)
  - 虛擬圖形處理器存取
- **檔案：** (從 Configuration Manager 1802 版開始)
  - 將下載的檔案儲存到主機

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> 應用程式行為設定

設定應用程式防護工作階段內的應用程式行為。 在 Configuration Manager 1802 版之前，應用程式行為和主機互動都位在 [設定]  索引標籤底下。

- **內容：**
  - 企業網站可載入非企業內容，例如協力廠商外掛程式。
- **其他：**
  - 保留使用者產生的瀏覽器資料
  - 獨立應用程式防護工作階段中的稽核安全性事件

### <a name="file-management"></a><a name="bkmk_FM"></a> 檔案管理
<!--3555858-->
自 Configuration Manager 1906 版起加入了一項原則設定，可以讓使用者信任在應用程式防護中正常開啟的檔案。 成功完成時，檔案會在主機裝置上 (而非在應用程式防護中) 開啟。 如需應用程式防護原則的詳細資訊，請參閱[設定 Windows Defender 應用程式防護設定](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard)\(部分內容為機器翻譯\)。

- **允許使用者信任在 Windows Defender 應用程式防護中開啟的檔案** - 允許使用者將檔案標示為信任。 檔案一經信任，就會在主機上開啟，而不是在應用程式防護中開啟。 適用於執行 Windows 10 1809 版或更新版本的用戶端。
  - **禁止：** 不允許使用者將檔案標示為受信任 (預設)。
  - **由防毒軟體檢查的檔案：** 允許使用者在防毒軟體檢查之後將檔案標示為受信任。
  - **所有檔案：** 允許使用者將任何檔案標示為受信任。

當您啟用檔案管理時，可能會在用戶端的 DCMReporting.log 中記載錯誤。 下列幾項錯誤通常不會影響功能： <!--4619457-->

- 在相容的裝置上：
  - 找不到 FileTrustCriteria_condition
- 在不相容的裝置上：
  - 找不到 FileTrustCriteria_condition
  - 在對應中找不到 FileTrustCriteria_condition
  - 在摘要中找不到 FileTrustCriteria_condition

若要編輯應用程式防護的設定，請在 [資產與相容性]  工作區中，展開 [Endpoint Protection]  ，然後按一下 [Windows Defender 應用程式防護]  節點。 以滑鼠右鍵按一下您要編輯的原則，然後選取 [屬性]  。

## <a name="next-steps"></a>後續步驟

若要深入了解 Windows Defender 應用程式防護：[Windows Defender 應用程式防護概觀](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) \(部分機器翻譯\)。
[Windows Defender 應用程式防護常見問題集](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard) \(英文\)。
