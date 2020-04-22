---
title: 搭配共同管理的雲端連線
titleSuffix: Configuration Manager
description: 共同管理能在您啟用它時立即提供價值。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ebadb47ca67f331ac88f8947b396438893e12386
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690866"
---
# <a name="cloud-connecting-with-co-management"></a>搭配共同管理的雲端連線

![Blastoff 系列橫幅](media/blastoff-banner.png)

共同管理能在不變更現有工作方式的情況下，將新功能新增至您現有的 Configuration Manager 部署。 啟用共同管理時，您將能立即獲得來自雲端的優點。 您可以將該價值套用到現有的管理基礎結構與程序。

在此共同管理快速入門系列中，您將能了解如何快速地驅動這些新的管理價值。 共同管理的目的是為了建立能供您立即使用的功能與工具。

在下列影片中，Microsoft 企業副總裁 Brad Anderson 將會介紹這個共同管理系列：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| 立即運算值 | 使用者入門 |
|-----------------|-----------------|
| - [條件式存取](#bkmk_ca)<br> - [來自 Intune 的遠端動作](#bkmk_remote)<br> - [用戶端健康情況](#bkmk_client-health)<br> - [混合式 Azure AD](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [共同管理的路徑](#bkmk_paths)<br> - [設定混合式 Azure AD](#bkmk_setup-hybrid-aad)<br> - [升級到 Windows 10](#bkmk_upgrade-win10)<br> - [從 FastTrack 取得協助](#bkmk_fasttrack) |

## <a name="immediate-value"></a>立即運算值

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**搭配裝置合規性的條件式存取** | 根據來自 Intune 的合規性規則控制使用者對企業資源的存取 | [![條件式存取影片的縮圖](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**來自 Intune 的遠端動作** | 從 Intune 針對共同管理裝置執行遠端動作。 例如，在維持註冊和帳戶的同時抹除並重設裝置 | [![遠端動作影片的縮圖](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Configuration Manager 用戶端健康情況** | 在 Azure 入口網站中從 Intune 維持對 Configuration Manager 用戶端健康情況的可見度 | [![用戶端健康情況影片的縮圖](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | 透過 Azure AD，您可以同時在雲端與內部部署環境中取得提升使用者生產力與資源安全性的好處 | [![混合式 Azure AD 影片的縮圖](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | 減少與部署、管理及淘汰或回收裝置相關的時間、資源與複雜度。 Autopilot 也能為使用者提供更好的體驗。 | [![Windows Autopilot 影片的縮圖](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>使用者入門

如果您想要啟用共同管理，請從這裡開始，以針對您任何可能的技術性疑慮取得解答。

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**共同管理的路徑** | 設定共同管理主要有兩種方法，而您應該了解這兩種方法個別的先決條件。  每個路徑都需要以某種程度搭配使用 Azure AD、ConfigMgr、Intune 與 Windows 用戶端。 | [![共同管理路徑投影片的縮圖](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**設定混合式 Azure AD** | 如果您的環境目前有已加入網域的 Windows 10 裝置，請在啟用共同管理前先設定混合式 Azure AD | [![混合式 Azure AD 設定影片的縮圖](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**升級到 Windows 10** | 共同管理需要 Windows 10 1709 版或更新版本 | [![升級 Windows 10 影片的縮圖](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**從 FastTrack 取得協助** | FastTrack 組織是由一大群 Microsoft 工程師所組成，其專精於協助所有類型的組織部署 Microsoft 365 應用程式，其包括設定共同管理。 | [![FastTrack 影片的縮圖](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
