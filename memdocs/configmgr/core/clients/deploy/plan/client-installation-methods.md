---
title: 用戶端安裝方法
titleSuffix: Configuration Manager
description: 深入了解安裝 Configuration Manager 用戶端的方法。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693836"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Configuration Manager 中的用戶端安裝方法

適用於：  Configuration Manager (最新分支)

您可以使用不同的方法來安裝 Configuration Manager 用戶端軟體。 請使用其中一種方法或多種方法的組合。 本文會說明每個方法，因此您可以了解哪一種方法最適合您的組織。  

## <a name="client-push-installation"></a>用戶端推入安裝  

**支援的用戶端平台**：Windows  

#### <a name="advantages"></a>優點  

-   可將用戶端安裝在單一電腦或一組電腦上，或是安裝至查詢結果。  

-   可用於在所有探索的電腦上自動安裝用戶端。  

-   會自動使用在 [用戶端推入安裝內容]  對話方塊中，[用戶端]  索引標籤上定義的用戶端安裝內容。  

#### <a name="disadvantages"></a>缺點  

-   推入至大量集合時，可能會使網路流量增高。  

-   只能用於 Configuration Manager 已探索的電腦。  

-   不可用於將用戶端安裝於工作群組中。  

-   必須指定用戶端推入安裝帳戶，且此帳戶在目標用戶端電腦上必須具有系統管理權限。  

-   在用戶端電腦上必須針對例外狀況設定 Windows 防火牆。   

-   您無法取消用戶端推入安裝。 Configuration Manager 會嘗試在探索到的所有資源上安裝用戶端。 它會重試任何失敗最多達七天。  

如需詳細資訊，請參閱[如何使用用戶端推入來安裝用戶端](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)。  



## <a name="software-update-point-based-installation"></a>以軟體更新點為基礎的安裝  

**支援的用戶端平台**：Windows  

#### <a name="advantages"></a>優點  

-   可以使用現有的軟體更新基礎結構管理用戶端軟體。  

-   如果 Active Directory 網域服務中的 Windows Server Update Services (WSUS) 和群組原則設定均正確無誤，它就可以在新電腦上自動安裝用戶端軟體。  

-   安裝用戶端前不需要先探索電腦。  

-   電腦可以讀取已發佈至 Active Directory 網域服務的用戶端安裝內容。  

-   如果已移除用戶端，此方法會重新安裝。  

-   不需在目標用戶端電腦設定及維護安裝帳戶。  

#### <a name="disadvantages"></a>缺點  

-   需要運作正常的軟體更新基礎結構作為必要條件。  

-   用戶端安裝和軟體更新必須使用同一個伺服器。 此伺服器必須位於主要站台中。  

-   若要安裝新的用戶端，您必須在 Active Directory 網域服務中使用用戶端的主動式軟體更新點和連接埠來設定群組原則物件。  

-   如果未延伸 Configuration Manager 的 Active Directory 架構，您必須使用群組原則設定來佈建含用戶端安裝內容的電腦。  

如需詳細資訊，請參閱[如何使用以軟體更新為基礎的安裝安裝用戶端](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)。  



## <a name="group-policy-installation"></a>群組原則安裝  

**支援的用戶端平台**：Windows  

#### <a name="advantages"></a>優點  

-   安裝用戶端前不需要先探索電腦。  

-   可用於全新安裝或升級用戶端。  

-   電腦可以讀取已發佈至 Active Directory 網域服務的用戶端安裝內容。  

-   不需在目標用戶端電腦設定及維護安裝帳戶。  

#### <a name="disadvantages"></a>缺點  

-   如果安裝大量用戶端，可能會使網路流量增高。  

-   如果未延伸 Configuration Manager 的 Active Directory 架構，您必須使用群組原則設定，將用戶端安裝內容新增至站台中的電腦。  

如需詳細資訊，請參閱[如何使用群組原則安裝用戶端](../deploy-clients-to-windows-computers.md#BKMK_ClientGP)。  



## <a name="logon-script-installation"></a>登入指令碼安裝  

**支援的用戶端平台**：Windows  

#### <a name="advantages"></a>優點  

-   安裝用戶端前不需要先探索電腦。  

-   支援使用 CCMSetup 命令列屬性。  

#### <a name="disadvantages"></a>缺點  

-   如果在短時間內安裝大量用戶端，可能會使網路流量增高。  

-   如果使用者不常登入網路，可能需花很長的時間才能安裝在所有用戶端電腦上。  

如需詳細資訊，請參閱[如何使用登入指令碼安裝用戶端](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)。  



## <a name="manual-installation"></a>手動安裝  

**支援的用戶端平台**：Windows、UNIX/Linux、Mac OS X  

#### <a name="advantages"></a>優點  

-   安裝用戶端前不需要先探索電腦。  

-   可供測試之用。  

-   支援使用 CCMSetup 命令列屬性。  

#### <a name="disadvantages"></a>缺點  

-   不提供自動化功能，因此相當耗時。  

如需有關如何在每個平台手動安裝用戶端的詳細資訊，請參閱下列文章：  

-   [如何將用戶端部署至 Windows 電腦](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [如何將用戶端部署至 UNIX 和 Linux 伺服器](../deploy-clients-to-unix-and-linux-servers.md)  

-   [如何將用戶端部署至 Mac](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM 安裝

**支援的用戶端平台**：Windows 10

#### <a name="advantages"></a>優點  

-   安裝用戶端前不需要先探索電腦。  

-   不需在目標用戶端電腦設定及維護安裝帳戶。  

-   可以使用 Azure Active Directory 進行新式驗證。  

-   可以安裝並指派網際網路上的電腦。  

-   可以使用 Windows AutoPilot 和 Microsoft Intune 自動化共同管理。  

#### <a name="disadvantages"></a>缺點  

-   需要 Configuration Manager 外部的其他技術。  

-   需要裝置存取網際網路，即使它不是以網際網路為基礎。  

如需詳細資訊，請參閱下列文章：  

-   [如何將用戶端安裝至 Intune MDM 管理的 Windows 裝置](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [安裝並指派 Configuration Manager Windows 10 用戶端，並使用 Azure AD 進行驗證](../deploy-clients-cmg-azure.md)  

