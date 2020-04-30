---
title: 一般合規性管理工作
titleSuffix: Configuration Manager
description: 透過處理一些常見的案例，了解 Configuration Manager 合規性設定需要。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1ccb0f0a042a0dd82817e030f96bbbc729e752f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692216"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>管理具有 Configuration Manager 用戶端之裝置上合規性的一般工作

適用於：  Configuration Manager (最新分支)

本文透過引導您進行您可能遇到的一些常見案例，為您簡介使用 Configuration Manager 的相容性設定。  

 若您已熟悉合規性設定，您可以在[由 Configuration Manager 用戶端管理之裝置的設定項目](../../compliance/deploy-use/create-configuration-items.md)中找到所用全部功能的詳細資訊。  

 開始之前，請先閱讀[開始使用合規性設定](../../compliance/get-started/get-started-with-compliance-settings.md)以了解合規性設定的一些基本概念。 如需所需必要條件的詳細資訊，請參閱[規劃和設定合規性設定](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

## <a name="general-information-for-each-scenario"></a>每個案例的通用資訊  
 在每個案例中，您會建立執行特定工作的設定項目。 若要開啟 [建立設定項目精靈] 並且啟動，請採取下列步驟：  

1.  在 Configuration Manager 主控台中，選取 [資產與合規性]   > [合規性設定]   > [設定項目]  。  

1.  在 [首頁]  索引標籤的 [建立]  群組中，選取 [建立設定項目]  。  

1.  在 [建立設定項目精靈] 的 [一般]  頁面上 (如下列螢幕擷取畫面所示)，指定設定項目的名稱與描述。 然後為本文中的每個案例選擇適當的設定項目類型。  

     ![[建立設定項目精靈] 的 [一般] 頁面](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>案例：停用 Windows 10 裝置上的藍牙

 在此案例中，您的安全性部門發現裝置上的藍牙功能可作為將公司機密資訊傳送到公司外部的方式。 您最近將所有電腦都升級為 Windows 10。 您決定停用這些裝置上的藍牙。  

1. 在 [建立設定項目精靈] 的 [一般]  頁面上，選取 [Windows 10]  設定項目類型，然後選取 [下一步]  。  

2. 在精靈的 [支援的平台]  頁面上，選取所有 Windows 10 平台。  

3. 在 [裝置設定]  頁面上，選取 [裝置]  ，然後選取 [下一步]  。  

4. 在 [裝置]  頁面上，選取 [禁止]  作為 [藍牙]  的值。  

5. 選取 [補救不相容的設定]  確保變更套用至所有 Windows 10 裝置。  

6. 完成精靈以建立設定項目。  

 您現在可以使用[以 Configuration Manager 建立及部署設定基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)文章中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>案例：補救 Windows 桌上型電腦上的不正確登錄值

> [!NOTE] 
> 在執行 Configuration Manager 用戶端的 Mac 電腦上 ，有兩個評估相容性選項：  
> - 評估 Mac OS X 喜好設定 (plist) 檔案。
> - 使用自訂指令碼，並評估指令碼所傳回的結果。  
>
>如需詳細資訊，請參閱[如何為 Configuration Manager 用戶端所管理的 Mac OS X 裝置建立設定項目](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)。  

 在此案例中，您發現您所管理的某些 Windows 8.1 電腦上未正確地執行重要的企業營運應用程式。 您發現這是因為某些電腦上名為 **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** 的登錄機碼值設定為 [0]  。 若要讓企業營運應用程式成功執行，此值必須設定為 [1]  。  

 在此程序中，您將建立監視並自動補救所找到之任何不正確登錄機碼值的設定項目。  

1. 在 [建立設定項目精靈] 的 [一般]  頁面上，選取 [Windows 桌面或伺服器 (自訂)]  設定項目類型，然後選取 [下一步]  。  

2. 在精靈的 **支援的平台** 頁面上，選取 **「Windows 8.1」** (確保設定項目僅套用至受影響的電腦)。  

3. 在 [設定]  頁面上，選取 [新增]  以建立新設定。  

4. 在 [建立設定]  對話方塊的 [一般]  索引標籤上，設定下列設定：  

   -   **名稱** > **設定範例**  

   -   **設定類型** > **登錄值**  

   -   **資料類型** > **整數** (因為值只包含數字)  

   -   **Hive** > **HKEY_LOCAL_MACHINE**  

   -   **機碼** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **值** > **1** (必要值)  

5. 在 [建立設定]  對話方塊的 [合規性規則]  索引標籤上，選取 [新建]  。 在 [建立規則]  對話方塊中，設定下列設定：  

   -   **名稱** > **範例規則**  

   -   **選取的設定** > 確認選取的設定為 [範例設定]  。

   -   **規則類型** > **值**  

   -   **設定必須符合下列規則** > 確認設定名稱正確，並將選項設定為指定設定值必須等於 **1**。  

   -   **支援時補救不相容的規則** >選取此核取方塊，以確保 Configuration Manager 在值不正確時會重設正確的登錄機碼值。  

6. 完成精靈以建立設定項目。  

 您現在可以使用[建立及部署設定基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)文章中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="next-steps"></a>後續步驟

[建立和部署設定基準](common-tasks-for-creating-and-deploying-configuration-baselines.md)
