---
title: 升級用戶端
titleSuffix: Configuration Manager
description: 取得如何在 Configuration Manager 中升級用戶端的相關資訊。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 40fc094d6c1a1acbd31f1d26e6fe6617972f8da5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696236"
---
# <a name="upgrade-clients-in-configuration-manager"></a>在 Configuration Manager 中升級用戶端

適用於：  Configuration Manager (最新分支)

您可以使用不同的方法，升級 Windows 電腦、UNIX 和 Linux 伺服器以及 Mac 電腦上的 Configuration Manager 用戶端軟體。 以下是各種方法的優缺點。  

> [!TIP]  
>  如果您從舊版的 Configuration Manager \(例如 Configuration Manager 2007 或 System Center 2012 Configuration Manager\) 升級伺服器基礎結構，建議您先完成伺服器升級 (包含安裝所有的最新分支更新)，然後再升級 Configuration Manager 用戶端。 如此一來，您也會有用戶端軟體的最新版本。  

## <a name="group-policy-installation"></a>群組原則安裝  
 **支援的用戶端平台：** Windows  

#### <a name="advantages"></a>優點  

- 升級用戶端前不需要先探索電腦。  

- 可用於全新安裝或升級用戶端。  

- 電腦可以讀取已發佈至 Active Directory 網域服務的用戶端安裝內容。  

- 不需在目標用戶端電腦設定及維護安裝帳戶。  

#### <a name="disadvantages"></a>缺點  

- 如果升級大量用戶端，可能會使網路流量增高。  

- 如果未延伸 Configuration Manager 的 Active Directory 架構，您必須使用 [[群組原則] 設定](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP)，將用戶端安裝內容新增至站台中的電腦。  


## <a name="logon-script-installation"></a>登入指令碼安裝  
 **支援的用戶端平台：** Windows  

#### <a name="advantages"></a>優點  

- 安裝用戶端前不需要先探索電腦。  

- 可用於全新安裝或升級用戶端。  

- 支援使用 CCMSetup 命令列屬性。  

#### <a name="disadvantages"></a>缺點  

- 如果在短時間內升級大量用戶端，可能會使網路流量增高。  

- 如果使用者不常登入網路，可能需要花很長的時間才能升級所有用戶端電腦。  

  如需詳細資訊，請參閱 [How to Install Configuration Manager Clients by Using Logon Scripts](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript) (如何使用登入指令碼安裝 Configuration Manager 用戶端)。  

## <a name="manual-installation"></a>手動安裝  
 **支援的用戶端平台：** Windows、UNIX/Linux、Mac OS X  

#### <a name="advantages"></a>優點  

- 升級用戶端前不需要先探索電腦。  

- 可供測試之用。  

- 支援使用 CCMSetup 命令列屬性。  

#### <a name="disadvantages"></a>缺點  

- 不提供自動化功能，因此相當耗時。  

  如需詳細資訊，請參閱下列主題：  

- [如何手動安裝 Configuration Manager 用戶端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [如何升級 Linux 和 UNIX 伺服器的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [如何升級 Mac 電腦上的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>升級安裝 (應用程式管理)  
 **支援的用戶端平台：** Windows  

> [!NOTE]  
>  您無法使用這種方法升級 Configuration Manager 2007 用戶端。 在此案例中，您可以從 Configuration Manager 2007 站台將 Configuration Manager 用戶端部署為套件，或者您可以使用自動用戶端升級以自動建立和部署含有最新用戶端版本的套件。  

#### <a name="advantages"></a>優點  

- 支援使用 CCMSetup 命令列屬性。  

#### <a name="disadvantages"></a>缺點  

- 如果您將用戶端發佈至大量集合，可能會使網路流量增高。  

- 必須先探索電腦並將電腦指派至站台，才能升級這些電腦上的用戶端軟體。  

  如需詳細資訊，請參閱 [How to Install Configuration Manager Clients by Using a Package and Program](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp) (如何使用封裝和程式安裝 Configuration Manager 用戶端)。  

## <a name="automatic-client-upgrade"></a>自動用戶端升級  

> [!NOTE]  
> 可以用來將 Configuration Manager 2007 用戶端升級至 Configuration Manager 最新分支用戶端。 Configuration Manager 2007 用戶端可以指派至 Configuration Manager 站台，但是無法執行自動用戶端升級以外的任何動作。  

 **支援的用戶端平台：** Windows  

#### <a name="advantages"></a>優點  

- 因為指定期間具有隨機性質，所以只有自動升級最適合大規模用戶端更新。 其他方法在碰到大規模升級時不是太慢，就是沒有隨機性質。 

    > [!Note]
    > 用戶端試驗完全不具隨機性質，因此不適合大規模升級。  
- 可用於自動將站台中的用戶端保持在最新版本。  

- 需要進行最基本的管理。  

#### <a name="disadvantages"></a>缺點  

- 只能用於升級用戶端軟體，不可用於安裝新用戶端。  

- 適用於階層中指派至某個站台的所有用戶端。 不能依集合設定範圍。  

- 排程選項有限。  

  如需詳細資訊，請參閱[如何升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

## <a name="client-testing"></a>用戶端測試  
 **支援的用戶端平台：** Windows  

#### <a name="advantages"></a>優點  

- 可用來在較小的進入生產階段前集合中測試新的用戶端版本。  

- 測試完成時，進入生產階段前的用戶端會升級至生產，並跨 Configuration Manager 站台自動進行升級。  

#### <a name="disadvantages"></a>缺點  

- 只能用於升級用戶端軟體，不可用於安裝新用戶端。  

  [如何在生產階段前集合中測試用戶端升級](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
