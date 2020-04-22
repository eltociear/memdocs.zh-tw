---
title: 更新整備小幫手
titleSuffix: Configuration Manager
description: 將更新整備小幫手與 Configuration Manager 整合，以存取 Windows 10 升級相容性資料，以及設定目標裝置來進行升級或修復。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 18d8b66a7b9f5ad889645cbc8e48ebcbfe6550a9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696316"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>將更新整備小幫手與 Configuration Manager 整合

適用於：  Configuration Manager (最新分支)

> [!Important]  
> Windows Analytics 服務已在 2020 年 1 月 31 日淘汰。 如需詳細資訊，請參閱 [KB 4521815：Windows Analytics 於 2020 年 1 月 31 日淘汰](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。
>
> 電腦分析是 Windows Analytics 的演進。 如需詳細資訊，請參閱[什麼是電腦分析](../../../desktop-analytics/overview.md)。

如果您的 Configuration Manager 站台與更新整備小幫手相連，則必須將其移除並重新設定用戶端。

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a> 移除更新整備小幫手連線

1. 以具有**系統高權限管理員**角色的使用者身分開啟 Configuration Manager 主控台。

1. 移至 [管理]  工作區、展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。

1. 刪除 Windows Analytics 服務。

## <a name="reconfigure-clients"></a>重新設定用戶端

### <a name="unenroll-devices"></a>取消註冊裝置

首先檢閱站台的預設值，或 **Windows Analytics** 群組中的任何自訂用戶端裝置設定。 例如，停用下列設定：**使用 Configuration Manager 管理 Windows 遙測設定**。

> [!IMPORTANT]
> 如果您打算使用電腦分析，其會在用戶端上設定 Windows 診斷資料設定。 使用 Azure 服務連線精靈進行這些設定，以搭配電腦分析使用。 如需詳細資訊，請參閱[如何將 Configuration Manager 連線至電腦分析](../../../desktop-analytics/connect-configmgr.md)。

在已註冊的裝置上，移除下列 Windows 登錄機碼中的 CommercialID 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows 診斷資料設定

如不希望裝置繼續傳送診斷資料：

- Windows 10：將診斷資料層級設定為 [安全性] 
- Windows 7 SP1 或 8.1：停用**商業資料加入金鑰**

使用下列方法之一設定這些值：

- 群組原則，位在 [電腦設定]   > [系統管理範本]   > [Windows 元件]   > [資料收集與預覽組建] 
- 行動裝置管理 (MDM)，例如 [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

如需詳細資訊，請參閱[在組織中設定 Windows 診斷資料](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)。

> [!NOTE]  
> 當您套用這些變更時，裝置會立即停止傳送診斷資料。 Microsoft 約需 24-48 小時才會停止處理您工作區的見解。 Microsoft 會在 30 天內 (或更短) 自其雲端服務刪除此資料。

<!--
Upgrade Readiness is a part of [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)  
