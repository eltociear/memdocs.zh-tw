---
title: 將內部部署站台延伸及移轉到 Microsoft Azure
titleSuffix: Configuration Manager
description: 了解如何使用移轉工具，以程式設計方式為 Configuration Manager 建立 Azure 虛擬機器。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707936"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>將內部部署站台延伸及移轉到 Microsoft Azure

適用於：*Configuration Manager (最新分支)*


1910 版中所推出的這項工具，可協助以程式設計方式為 Configuration Manager 建立 Azure 虛擬機器 (VM)。 <!--3556022--> 您可以使用預設設定站台角色 (如被動站台伺服器、管理點與發佈點) 安裝它。 一旦驗證新角色，您就可以使用他們作為額外站台系統以獲得高可用性。 您也可以移除內部部署站台系統角色，並指保留 Azure VM 角色。

## <a name="prerequisites"></a>先決條件

- Azure 訂用帳戶

- Azure 虛擬網路 (含 ExpressRoute 閘道)

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- 您的使用者帳戶必須是 Configuration Manager **系統高權限管理員**並擁有主要站台伺服器上的系統管理員權限。

- 若要新增被動伺服器，主要站台必須符合[站台伺服器的高可用性需求](../servers/deploy/configure/site-server-high-availability.md#prerequisites)。 例如，它需要[遠端內容庫](../plan-design/hierarchy/the-content-library.md#bkmk_remote)。

### <a name="required-azure-permissions"></a>必要的 Azure 權限

執行工具時，需要 Azure 的下列權限：
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


如需權限和指派角色的詳細資訊，請參閱 [Manage access to Azure resources using RBAC](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) (使用 RBAC 來管理 Azure 資源的存取權)。

## <a name="run-the-tool"></a>執行工具

1. 登入主要站台伺服器並執行 Configuration Manager 安裝目錄中的下列工具：`Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. 檢閱 [一般]  索引標籤上的指示，然後切換到 [Azure 資訊]  索引標籤。

1. 在 [Azure 資訊]  索引標籤上，選擇您的 [Azure 環境]  ，然後選取 [登入]  。

    > [!TIP]
    > 您可能必須新增 `https://*.microsoft.com` 到您信任的網站清單以正確地登入。

    [ ![延伸及移轉工具中的 [Azure 資訊] 索引標籤](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. 登入之後，選取您的 [訂用帳戶識別碼]  與 [虛擬網路]  。 工具只會列出具有 ExpressRoute 閘道的網路。

## <a name="site-server-high-availability"></a>站台伺服器的高可用性

1. 在 [站台伺服器的高可用性]  索引標籤上，選取 [檢查]  以評估您站台的整備程度。

    若任一檢查失敗，請選取 [更多詳細資料]  以判斷如何針對問題進行補救。 如需有關這些先決條件的詳細資訊，請參閱[站台伺服器的高可用性](../servers/deploy/configure/site-server-high-availability.md#prerequisites)。

2. 若要延伸或移轉您的站台伺服器到 Azure，請選取 [在 Azure 中建立站台伺服器]  。 接著填寫下列欄位：

    |Name|說明|
    |---|---|
    |**訂用帳戶**|唯讀。 顯示訂用帳戶名稱與識別碼。|
    |**資源群組**| 列出可用的資源群組。 若您需要建立新的資源群組，請使用 [Azure 入口網站](https://portal.azure.com)，然後重新執行此工具。|
    |**位置**| 唯讀。 由您虛擬網路的位置所決定|
    |**VM 大小**|選擇適合您工作負載的大小。 Microsoft 建議使用 **Standard_DS3_v2**。|
    |**作業系統**|唯讀。 該工具使用 Windows Server 2019。|
    |**磁碟類型**|唯讀。 該工具使用 Premium SSD 以獲得最佳效能。|
    |**虛擬網路**|唯讀。|
    |**子網路**|選取要使用的子網路。 若您需要建立新的子網路，請使用 [Azure 入口網站](https://portal.azure.com)。|
    |**電腦名稱**|輸入 Azure 中的被動站台伺服器 VM 名稱。 它與 [Azure 入口網站](https://portal.azure.com)中顯示的名稱相同。|
    |**本機系統管理員使用者名稱**|輸入 Azure VM 在加入網域之前所建立之本機系統管理員使用者的名稱。|
    |**本機系統管理員密碼**|本機系統管理員使用者的密碼。 若要在 Azure 部署期間保護密碼，請將密碼儲存為 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview) 中的祕密。 接著，在裡使用該參考。 如果有需要，請從 [Azure 入口網站](https://portal.azure.com)建立新項目。|
    |**網域 FQDN**|要加入之 Active Directory 網域的完整網域名稱。 根據預設，工具會從您目前的電腦取得此值。|
    |**網域使用者名稱**|允許加入網域的網域使用者名稱。 根據預設，工具會使用目前已登入使用者的名稱。|
    |**網域密碼**|要加入網域之網域使用者的密碼。 當您選取 [開始]  之後，工具會驗證密碼。 若要在 Azure 部署期間保護密碼，請將密碼儲存為 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview) 中的祕密。 接著，在裡使用該參考。 如果有需要，請從 [Azure 入口網站](https://portal.azure.com)建立新項目。|
    |**網域 DNS IP**|用於加入網域。 根據預設，工具會使用來自您目前電腦的目前 DNS。|
    |**類型**|唯讀。 它會顯示 [被動站台伺服器]  作為類型。|

    > [!IMPORTANT]
    > 根據預設，虛擬機器的 [使用現有的 Windows Server 授權]  是設定為 [否]  。 若要利用具有軟體保證的內部部署 Windows Server 授權，請在佈建虛擬機器之後，於 [Azure 入口網站](https://portal.azure.com)中設定此設定。 如需詳細資訊，請參閱[適用於 Windows Server 的 Azure Hybrid Benefit](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit)。

1. 若要開始佈建 Azure VMM，請選取 [開始]  。 若要監視部署狀態，請切換到工具中的 [Azure 中的部署]  索引標籤。 若要取得最新狀態，請選取 [重新整理部署狀態]  。

    > [!TIP]
    > 您也可以使用 [Azure 入口網站](https://portal.azure.com)來檢查狀態、尋找錯誤，以及決定潛在修正方式。

1. 當部署完成時，請移至您的 SQL 伺服器，然後為新 Azure VM 授與權限。 如需詳細資訊，請參閱[站台伺服器的高可用性 - 先決條件](../servers/deploy/configure/site-server-high-availability.md#prerequisites)。

1. 若要新 Azure VM 作為被動模式中的站台伺服器，請選取 [在被動模式中新增站台伺服器]  。

1. 一旦站台以被動模式新增站台伺服器，[伺服器的高可用性]  索引標籤就會顯示狀態。

   [![被動站台伺服器已新增至 [站台伺服器的高可用性] 索引標籤](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. 接著，移至 [Azure 中的部署](#bkmk_deploy-azure)索引標籤以完成部署。

## <a name="site-database"></a>網站資料庫

工具目前沒有任何工作要將資料庫從內部部署移轉到 Azure。 您可以選擇將資料庫從內部部署 SQL 伺服器移至 Azure SQL Server VM。 工具會在 [站台資料庫]  索引標籤列出下列文章以提供說明：

- [備份及還原資料庫](../servers/manage/backup-and-recovery.md)
- [設定 SQL Always On 並允許資料複寫](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [將 SQL 資料庫移轉到 Azure SQL Server VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>網站系統角色

1. 切換到 [站台系統角色]  索引標籤。若要使用預設設定佈建新站台系統角色，請選取 [建立新項目]  。 您可以佈建角色，例如管理點、發佈點與軟體更新點。 目前並非所有角色在工具中都可用。

    [![延伸及移轉工具中的 [站台系統角色] 索引標籤](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. 在佈建視窗中，填寫下列欄位以在 Azure 中佈建站台角色的 VM。 這些詳細資料與上面站台伺服器清單類似。

1. 若要開始佈建 Azure VMM，請選取 [開始]  。 若要監視部署狀態，請切換到工具中的 [Azure 中的部署]  索引標籤。 若要取得最新狀態，請選取 [重新整理部署狀態]  。

    > [!TIP]
    > 您也可以使用 [Azure 入口網站](https://portal.azure.com)來檢查狀態、尋找錯誤，以及決定潛在修正方式。

1. 重複此程序以新增更多站台系統角色。

1. 接著，移至 [Azure 中的部署](#bkmk_deploy-azure)索引標籤以完成部署。

1. 當部署完成時，請移至 Configuration Manager 主控台以對站台角色進行額外的變更。

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Azure 中的部署

1. 一旦 Azure 建立 VM，請切換到, 工具中的 [Azure 中的部署]  索引標籤。 選取 [部署]  以使用預設設定來設定角色。

1. 選取 [執行]  以開始執行 PowerShell 指令碼。

    [![透過執行產生的 PowerShell 指令碼來部署站台角色](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. 請重複此程序以設定更多角色。

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> 新增站台角色至現有的虛擬機器部署
<!--5665775, 6307931-->
從 Configuration Manager 2002 版開始，將內部部署站台延伸及移轉到 Microsoft Azure 工具可支援在單一 Azure 虛擬機器上佈建多個站台系統角色。 您可以在初始 Azure 虛擬機器部署完成之後，新增站台系統角色。 若要將新角色新增至現有的虛擬機器，請執行下列步驟：
1. 在 [ Azure 中的部署]  索引標籤上，按一下狀態為 [已完成]  的虛擬機器部署。
1. 按一下 [新建]  按鈕，將額外的角色新增至虛擬機器。


## <a name="next-steps"></a>後續步驟

在 [Azure 入口網站](https://portal.azure.com)中檢閱您的變更
