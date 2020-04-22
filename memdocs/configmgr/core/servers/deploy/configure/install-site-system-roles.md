---
title: 安裝站台系統角色
titleSuffix: Configuration Manager
description: 將站台系統角色新增至站台中現有或新的站台系統伺服器。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 102d07f29b9addd1f2c37dd741db09e972cd5802
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701656"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>為 Configuration Manager 安裝站台系統角色

適用於：  Configuration Manager (最新分支)

在 Configuration Manager 主控台中，有兩種方法可以安裝站台系統角色：

- **新增站台系統角色**：將站台系統角色新增至站台中現有站台系統伺服器。

- **建立站台系統伺服器**：指定新伺服器作為站台系統伺服器，然後安裝一或多個角色。 除了第一頁之外，此方法與**新增站台系統角色**相同。 您必須先指定伺服器的名稱，以及要在其中安裝角色的目標站台。

> [!TIP]
> 當在遠端電腦上安裝角色時，Configuration Manager 會將遠端電腦的電腦帳戶新增至站台伺服器上的本機群組。
>
> 當在網域控制站上安裝站台時，站台伺服器上的群組為網域群組，而不是本機群組。 在此情況下，遠端站台系統角色並不會立即生效。 站台系統伺服器需要重新啟動，或您必須更新遠端伺服器電腦帳戶的 Kerberos 票證。 如需詳細資訊，請參閱[已使用的帳戶](../../../plan-design/hierarchy/accounts.md)。

在安裝站台系統角色之前，Configuration Manager 會檢查目的電腦，以確保其符合所選站台系統角色的先決條件。

根據預設，當 Configuration Manager 安裝站台系統角色時，會安裝檔案至擁有最多磁碟空間的第一部可用 NTFS 格式化磁碟機上。 若要避免 Configuration Manager 安裝到特定磁碟機上，在安裝站台系統伺服器前，請先在磁碟機根目錄中建立名為 **no_sms_on_drive.sms** 的空白檔案。

Configuration Manager 會使用**站台系統安裝帳戶**來安裝角色。 當安裝角色時請指定此帳戶。 根據預設，此帳戶為站台伺服器電腦的本機系統帳戶。 您可將網域使用者帳戶指定為站台系統安裝帳戶。 如需詳細資訊，請參閱[帳戶 - 站台系統安裝帳戶](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)。

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> 在現有的站台系統伺服器上安裝角色

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。 選取現有的站台系統伺服器，以安裝新的站台系統角色。

1. 在功能區的 [首頁]  索引標籤上，於 [伺服器]  群組中，選取 [新增站台系統角色]  。

1. 在 [一般]  頁面上檢閱設定。

    > [!TIP]
    >  若要從網際網路存取此站台系統角色，請確認您指定網際網路完整網域名稱 (FQDN)。

1. 在 [Proxy]  頁面上，如果這部伺服器上的角色需要網際網路 Proxy，請指定 Proxy 伺服器的設定。 如需詳細資訊，請參閱 [Proxy 伺服器支援](../../../plan-design/network/proxy-server-support.md)。

1. 在 [系統角色選取]  頁面上，選取要新增的站台系統角色。

1. 完成精靈。 特定角色可能會顯示其他頁面。 如需詳細資訊，請參閱[站台系統角色的設定選項](configuration-options-for-site-system-roles.md)。

> [!TIP]
> Windows PowerShell Cmdlet 的 **New-CMSiteSystemServer** 會執行與此程序相同的功能。 如需詳細資訊，請參閱 [New-CMSiteSystemServer](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps)。

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> 在新的站台系統伺服器上安裝角色

1. 在 Configuration Manager 主控台中，移至 [系統管理]  工作區。 展開 [站台設定]  ，然後選取 [伺服器和站台系統角色]  節點。

1. 在功能區的 [首頁]  索引標籤上，於 [建立]  群組中，選取 [建立站台系統伺服器]  。

1. 在 [一般]  頁面上，指定站台系統的一般設定。

    > [!TIP]
    > 若要從網際網路存取新的站台系統角色，請確認您指定網際網路 FQDN。

1. 在 [Proxy]  頁面上，如果這部伺服器上的角色需要網際網路 Proxy，請指定 Proxy 伺服器的設定。 如需詳細資訊，請參閱 [Proxy 伺服器支援](../../../plan-design/network/proxy-server-support.md)。

1. 在 [系統角色選取]  頁面上，選取要新增的站台系統角色。

1. 完成精靈。 特定角色可能會顯示其他頁面。 如需詳細資訊，請參閱[站台系統角色的設定選項](configuration-options-for-site-system-roles.md)。

> [!TIP]
> Windows PowerShell Cmdlet 的 **New-CMSiteSystemServer** 會執行與此程序相同的功能。 如需詳細資訊，請參閱 [New-CMSiteSystemServer](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps)。

## <a name="next-steps"></a>後續步驟

- [站台系統角色的設定選項](configuration-options-for-site-system-roles.md)

- [移除角色](../install/uninstall-sites-and-hierarchies.md#bkmk_role)
