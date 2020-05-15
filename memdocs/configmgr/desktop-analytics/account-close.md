---
title: 如何關閉您的帳戶
titleSuffix: Configuration Manager
description: 如何從 Azure 帳戶移除電腦分析
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e24c2ee19093dd12af6e87280a31851a1f593782
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268465"
---
# <a name="how-to-close-your-account"></a>如何關閉帳戶

如果您在環境中設定電腦分析，然後決定需要移除它，請使用此程序來關閉帳戶。

## <a name="prerequisites"></a>先決條件

只有**全域管理員**可在 Azure 入口網站中關閉或動新啟用帳戶。

## <a name="process-to-offboard"></a>離線程序

1. 以具有**全域管理員**角色的使用者身分，在 Microsoft 365 裝置管理中開啟[電腦分析入口網站](https://aka.ms/desktopanalytics)。

1. 在 [全域設定]  功能表中，選取 [已連線的服務]  。 在 [註冊裝置] 區段中，選取 [離線]  選項。

1. 如決定繼續，即會關閉您的帳戶。

> [!Important]
> 90 天後或如果不重新啟用帳戶，才繼續本文的其餘部分。
>
> 如果不想等 90 天即完全關閉帳戶，請先[重設](account-reset.md)帳戶。

## <a name="reactivate"></a>重新啟用

在接下來的 90 天中，組織中所有存取電腦分析入口網站的系統管理員都會看到您選擇離線的通知。

全域管理員可以在 90 天內重新啟用帳戶。 若要還原組織的電腦分析，請選取 [帶我返回]  選項。

## <a name="delete-the-solution"></a>刪除解決方案

> [!Warning]
> 90 天後或如果不重新啟用帳戶，才繼續本文的其餘部分。 如果您刪除這些其他元件並中斷其連線，則請勿嘗試重新啟用。

1. 以具有**全域管理員**角色的使用者身分登入 [Azure 入口網站](https://portal.azure.com)。

1. 在 [所有資源]  中搜尋您的電腦分析工作區名稱。 這是您註冊服務時所建立的名稱。

1. 刪除 **Solution** 類型的 `Microsoft365Analytics(YourWorkspaceName)`。

電腦分析的資料時限由您工作區的資料保留原則決定。 您可在相同的工作區中繼續使用任何其他解決方案。

> [!Important]  
> 如要使用 Log Analytics 工作區與其他解決方案，請不要刪除工作區。

## <a name="remove-user-and-app-access"></a>移除使用者和應用程式存取權

1. 以具有**全域管理員**角色的使用者身分登入 [Azure 入口網站](https://portal.azure.com)。 移至 **Azure Active Directory**。

1. 在 [角色和系統管理員]  中搜尋**電腦分析管理員**角色。 移除其成員。

1. 在 [群組]  中，移除下列群組的成員：

    - **M365 Analytics 用戶端系統管理員 (Log Analytics 擁有者)**
    - **M365 Analytics 用戶端系統管理員 (Log Analytics 參與者)**

1. 在 [企業應用程式]  中，刪除或撤銷下列應用程式的存取權限：

    - `MaLogAnalyticsReader`

    - ConfigMgr 應用程式。 若要尋找此應用程式的名稱，請移至 Configuration Manager 主控台。 在 [管理]  工作區中展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。 開啟**電腦分析**服務的 [屬性]，然後切換至 [應用程式]  索引標籤。**Web 應用程式**即此 Azure 應用程式。

        > [!Important]  
        > 在 Azure AD 中變更此應用程式之前，請確定您不會在 Configuration Manager 的其他服務中重複使用它。

## <a name="disconnect-configuration-manager"></a>中斷 Configuration Manager 連線

1. 以具有**系統高權限管理員**角色的使用者身分開啟 Configuration Manager 主控台。

1. 移至 [管理]  工作區、展開 [雲端服務]  ，然後選取 [Azure 服務]  節點。

1. 刪除電腦分析服務。

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>刪除試驗和生產環境部署的集合

1. 在 Configuration Manager 主控台中，選取 [資產與合規性]  工作區中的 [裝置集合]  。

1. 刪除所有不再使用的集合。 根據預設，集合位於**部署計劃**資料夾下。  

## <a name="reconfigure-clients"></a>重新設定用戶端

### <a name="unenroll-devices"></a>取消註冊裝置

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
