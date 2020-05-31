---
title: Windows 10 的支援
titleSuffix: Configuration Manager
description: 針對搭配 Configuration Manager 作為用戶端或用於 OSD 的狀況，了解支援的 Windows 10 版本
ms.date: 05/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a67a22f788af39dacb9f3a39e91e0f28444c6988
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879063"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Configuration Manager 對於 Windows 10 的支援  

適用於：Configuration Manager (最新分支)

了解 Configuration Manager 支援的 Windows 10 版本，包括：

- [作為 Configuration Manager 用戶端的 Windows 10](#windows-10-as-a-client)
- [Windows 10 的 Windows 評定及部署套件 (ADK)](#windows-10-adk)

> [!Tip]
> Windows Server 組建，因為支援與相關聯 Windows 10 版本相同的用戶端。 例如，Windows Server 2016 是與 Windows 10 LTSB 2016 相同的組建版本，而 Windows Server 1803 版是與 Windows 10 1803 版相同的組建版本。
>
> 如需 Windows Server 作為站台系統的詳細資訊，請參閱 [Configuration Manager 站台系統伺服器支援的作業系統](supported-operating-systems-for-site-system-servers.md#bkmk_core)。

## <a name="windows-10-as-a-client"></a>做為用戶端的 Windows 10

Configuration Manager 會在每個新的 Windows 10 版本推出之後，盡快支援以新版本作為用戶端。 因為產品具有個別的開發和發行排程，所以 Configuration Manager 提供的支援取決於每個產品的推出時間。

當某個 Configuration Manager 版本的[版本支援](../../servers/manage/current-branch-versions-supported.md)終止之後，就會從矩陣中卸除該版本。 同樣地，從支援中移除 Windows 10 版本 (例如企業版 2015 LTSB 或 1511) 的支援時，將會從矩陣中卸除這些版本。

- Configuration Manager 最新分支的最新版本同時接收安全性和重大更新，以包含 Windows 10 版本問題的修正程式。 Microsoft 發行新版 Configuration Manager 最新分支時，舊版本只會收到安全性更新。 如需詳細資訊，請參閱 [Configuration Manager 最新分支版本的支援](../../servers/manage/current-branch-versions-supported.md)。  

    > [!Note]  
    > 讓 Windows 10 維持最新狀態的最佳方式是維持 Configuration Manager 的最新狀態。 如需詳細資訊，請參閱 [Configuration Manager 與 Windows 即服務](../../understand/configuration-manager-and-windows-as-service.md)。  

- 這項資訊會補充說明[用戶端和裝置的支援作業系統](supported-operating-systems-for-clients-and-devices.md)。  

- 如果您使用 Configuration Manager 長期維護分支，請參閱[支援的長期維護分支設定](../../understand/supported-configurations-for-ltsb.md)。  

下表列出可搭配不同 Configuration Manager 版本作為用戶端使用的 Windows 10 版本。

| Windows 10 版本 | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--10/13/2020-->   | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![不支援](media/Red_X.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/10/2022-->   | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **2004**<br>(10.0.19041)   <!--??/??/2021-->   | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![支援](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

如需 Windows 生命週期的詳細資訊，請參閱 [Windows 生命週期事實表](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

| 機碼 |
|--|
| ![支援](media/green_check.png) = **支援**  |
| ![不支援](media/Red_X.png) = **不支援** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Windows 10 用戶端支援注意事項

- Windows 10 半年通道版本支援包含下列版本：企業版、專業版、教育版和專業教育版。  

- 從 1906 版開始，Configuration Manager 支援適用於工作站的 Windows 10 Pro。

- 針對 Windows 10 1909 版，OS 部署媒體會將版本顯示為10.0.18362.418。

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> ARM64 上的 Windows 10

Configuration Manager 支援 Windows 10 ARM64 裝置上的用戶端。 不支援 OS 部署。<!-- 1353704 -->

從 2002 版開始，<!--5954175--> 在具有需求規則或適用性清單的物件上支援 OS 版本的清單中，已提供**所有 Windows 10 (ARM64)** 平台。

> [!NOTE]
> 如果您先前已選取最上層的 **Windows 10** 平台，則此動作會自動選取 [所有 Windows 10 (64 位元)] 和 [所有 Windows 10 (32位元)]。 系統不會自動選取這個新平台。 如果想要新增 [所有 Windows 10 (ARM64)]，請在清單中手動選取該選項。

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> Windows 測試人員的支援

從 Configuration Manager 1906 版開始，您可以[更新及服務 Windows 測試人員](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB)組建。 這項功能是為了方便我們的客戶使用。 雖然此功能應該可運作，仍會提供它為好的支援。 如果此功能停止運作，Configuration Manager 可能不會為該功能發行 Hotfix。  

若要提供有關 Windows 測試人員的意見反應，請使用 [Feedback Hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback) (意見反應中樞)。

## <a name="windows-10-adk"></a>Windows 10 ADK

當您使用 Configuration Manager 部署作業系統時，Windows ADK 是必要的外部相依性。 如需詳細資訊，請參閱下列文章：

- [OS 部署的基礎結構需求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [下載適用於 Windows 10 的 Windows ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > 從 Windows 10 1809 版開始，Windows PE 是個別的安裝程式。 否則，沒有任何功能差異。
    >
    > 請務必下載 **Windows 10 版 Windows ADK** 和**適用於 ADK 的 Windows PE 附加元件**。

下表列出可搭配不同 Configuration Manager 版本使用的 Windows 10 ADK 版本。

| Windows 10 ADK 版本  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![不支援](media/Red_X.png)   | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![回溯相容](media/blue_compat.png) | ![回溯相容](media/blue_compat.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![回溯相容](media/blue_compat.png) | ![回溯相容](media/blue_compat.png) | ![不支援](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![不支援](media/Red_X.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) | ![支援](media/green_check.png) |
| **2004**<br>(10.1.19041) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![不支援](media/Red_X.png) | ![支援](media/green_check.png) |

|機碼|
|--|
| ![支援](media/green_check.png) = **支援** <br/> 此表格只顯示與 Configuration Manager 版本相關的 Windows ADK 可支援性。 Microsoft 建議使用符合您所要部署 Windows 版本的 Windows ADK。 部署最新的 Windows 10 版本時，請使用最新的 Windows ADK 版本。 最新的 Windows ADK 版本可能支援較舊 OS 版本的部署，例如 Windows 8.1。<!-- SCCMDocs issue 1229 --> 如需 Windows ADK 元件可支援性的詳細資訊，請參閱 [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) (DISM 支援的平台) 和 [USMT Requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1) (USMT 需求)。 |
| ![回溯相容](media/blue_compat.png)  = **回溯相容** <br/> 此組合未經測試，但應可運作。 我們將記載任何已知問題或警示。 |
| ![不支援](media/Red_X.png) = **不支援** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Windows 10 ADK 支援注意事項

- Configuration Manager 僅支援 Windows 10 ADK 的 x86 和 amd64 元件。 它目前不支援 ARM 或 ARM64 元件。

- Windows Server 組建的 Windows ADK 需求與相關聯的 Windows 10 版本相同。 例如，Windows Server 2016 的組建版本與 Windows 10 LTSB 2016 相同。
