---
title: 在 Azure 中建立實驗室
titleSuffix: Configuration Manager
description: 使用 Azure 範本自動建立 Configuration Manager 技術預覽版實驗室或最新分支的評估實驗室
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd2a8b3bfb7c4b8af277616c7eaed329bc143bb7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691396"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>在 Azure 中建立 Configuration Manager 實驗室

適用於：  Configuration Manager (Technical Preview 分支)

<!--3556017-->

本指南描述如何在 Microsoft Azure 中建置 Configuration Manager 實驗室環境。 它會使用 Azure 範本來簡化及自動化使用 Azure 資源建立實驗室的作業。 其提供兩個 Azure 範本： 

- Configuration Manager 技術預覽版 Azure 範本會安裝最新版的 Configuration Manager 技術預覽版分支。
- Configuration Manager 最新分支 Azure 範本會安裝最新版的 Configuration Manager 最新分支評估。 

如需詳細資訊，請參閱 [Azure 上的 Configuration Manager](../understand/configuration-manager-on-azure.md)。



## <a name="prerequisites"></a>先決條件

此程序需要 Azure 訂用帳戶，您可以在其中建立下列物件： 
- 用於網域控制站和 MP 與 DP角色的兩個 Standard_B2s 虛擬機器。
- 一部 Standard_B2ms 虛擬機器用於主要站台伺服器和 SQL Database 伺服器。
- Standard_LRS 儲存體帳戶

> [!Tip]  
> 請參閱 [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/)以利判斷潛在成本。  



## <a name="process"></a>程序

1. 前往 [Configuration Manager 技術預覽版範本](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/)或 [Configuration Manager 最新分支範本](https://azure.microsoft.com/resources/templates/sccm-currentbranch/)。  

2. 選取 [部署至 Azure]  ，這會開啟 Azure 入口網站。  

3. 以下列資訊完成 Azure 快速入門範本：

    - 基本  

        - **訂用帳戶**：要在其中建立 VM 的訂用帳戶名稱  

        - **資源群組**：選取要用於這些 VM 的資源群組  

        - **位置**：選取 Azure 資料中心來裝載此實驗室環境  

    - 設定  

        - **前置詞**：機器的前置詞名稱。 如需詳細資訊，請參閱 [Azure VM 資訊](#azure-vm-info)。  

        - **系統管理員使用者名稱**：VM 上具有系統管理權限的使用者名稱。 您可以使用此使用者登入 VM。  

        - **系統管理員密碼**：密碼必須符合 Azure 的複雜性需求。 如需詳細資訊，請參閱 [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile)。  

    > [!Important]  
    > Azure 需要下列設定。 請使用預設值。 請勿變更這些值。  
    > 
    > - **\_成品位置**：此範本的指令碼位置 <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_成品位置 SAS 權杖**：需要有 sasToken 才能存取成品位置  
    > 
    > - **位置**：所有資源的位置

4. 閱讀條款及條件。 如果您同意，請選取 [我同意上方所述的條款及條件]  。 然後選取 [購買]  以繼續。 

Azure 會驗證設定，接著開始部署。 請在 Azure 入口網站中檢查部署的狀態。 

> [!NOTE]
> 此程序可能需要 2 到 4 小時的時間。 即使 Azure 入口網站顯示部署成功，設定指令碼還是會繼續執行。 請勿在此程序期間重新啟動 VM。

若要查看設定指令碼的狀態，請連線至 `<prefix>PS1` 伺服器，並檢視下列檔案：`%windir%\TEMP\ProvisionScript\PS1.json`。 如果它顯示所有步驟均已完成，即表示此程序已完成。

若要連線至 VM，首先要從 Azure 入口網站取得每部 VM 的公用 IP 位址。 當您連線至 VM 時，網域名稱為 `contoso.com`。 請使用您在部署範本中指定的認證。 如需詳細資訊，請參閱[如何連線及登入執行 Windows 的 Azure 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon)。



## <a name="azure-vm-info"></a>Azure VM 資訊

所有三部 VM 都具有下列規格：
- 150 GB 的磁碟空間
- 公用和私人 IP 位址兩者。 公用 IP 位於網路安全性群組中，而該群組只允許在 TCP 連接埠 3389 上進行遠端桌面連線。 

您在部署範本中指定的前置詞是 VM 名稱前置詞。 例如，如果您設定 "contoso" 作為前置詞，則網域控制站機器名稱為 `contosoDC`。


### `<prefix>DC01`

- Active Directory 網域控制站
- Standard_B2s，有兩個 CPU 和 4 GB 的記憶體
- Windows Server 2019 Datacenter 版

#### <a name="windows-features-and-roles"></a>Windows 功能和角色
- Active Directory Domain Services (ADDS)
- .NET
- 遠端差異壓縮 (RDC)


### `<prefix>PS01`

- Standard_B2ms，有兩個 CPU 和 8 GB 的記憶體
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows 10 ADK (含 Windows PE) 
- Configuration Manager 主要站台

#### <a name="windows-features-and-roles"></a>Windows 功能和角色
- .NET
- 遠端差異壓縮 (RDC) 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- Standard_B2s，有兩個 CPU 和 4 GB 的記憶體
- Windows Server 2019 Datacenter 版
- 發佈點
- 管理點

#### <a name="windows-features-and-roles"></a>Windows 功能和角色
- .NET
- 遠端差異壓縮 (RDC) 
- Internet Information Service (IIS)
- 背景智慧型傳送服務 (BITS)

### `<prefix>CL01`

- 僅適用於 Configuration Manager 最新分支評估範本
- Windows 10
- Configuration Manager 用戶端
