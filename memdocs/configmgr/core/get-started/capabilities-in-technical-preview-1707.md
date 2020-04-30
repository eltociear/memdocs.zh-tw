---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1707 版中可用的功能。
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705136"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Configuration Manager Technical Preview 1707 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

此文章介紹 Configuration Manager 技術預覽 1707 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**此 Technical Preview 的已知問題：**
- **當您有以被動模式執行的站台伺服器時，更新到預覽版 1707 失敗**。 當您執行預覽版 1706 且有[以被動模式執行的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)時，您必須先將被動模式站台伺服器解除安裝，才能順利將預覽站台更新到 1707 版。 當您的站台執行 1707 版之後，您可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。



**以下是您可以使用此版本試用的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Windows 10 和 Office 365 快速安裝檔案的用戶端對等快取支援
<!-- 1352486 -->
從這個版本開始，對等快取支援適用於 Windows 10 的內容發佈快速安裝檔案和適用於 Office 365 的更新檔案。 無須進行其他設定。

## <a name="surface-device-dashboard"></a>Surface 裝置儀表板
<!--1355788-->
Surface 裝置儀表板提供在您的環境中找到的 Surface 裝置相關資訊。 在主控台中，移至 [監視]   > [Surface Devices] (Surface 裝置)  。 您可以檢視下列資訊：
- Surface 百分比
- Surface 模型的百分比
- 前五大作業系統版本

按一下 [Surface Models] (表面模型)  圖表的一個區段可看到完整裝置清單。  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>設定及部署 Windows Defender 應用程式防護原則
<!-- 1351960 -->

[Windows Defender 應用程式防護](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)是一個新的 Windows 功能，可藉由在作業系統其他部分所無法存取的安全隔離容器中開啟未受信任的網站，來協助保護您的使用者。 在此 Technical Preview 中，我們已新增支援，可使用您所設定並接著部署到集合的 Configuration Manager 合規性設定來設定此功能。 此功能將在 64 位元版 Windows 10 Fall Creator’s Update (代號：RS3) 的預覽版中推出。 若要立即測試此功能，您必須使用此更新的預覽版本。

### <a name="before-you-start"></a>在您開始使用 Intune 之前

若要建立及部署「Windows Defender 應用程式防護」原則，必須為您要部署原則的 Windows 10 裝置設定網路隔離原則。 如需詳細資訊，請參閱[此部落格文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此功能只能與最新的「Windows 10 測試人員組建」搭配運作。 若要測試它，您的用戶端必須執行最新的「Windows 10 測試人員組建」。

### <a name="try-it-out"></a>試試看！

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>建立原則並瀏覽至可用的設定：

1. 在 Configuration Manager 主控台中，選擇 [資產與相容性]  。
2. 在 [資產與合規性]  工作區中，選擇 [概觀]   > [Endpoint Protection]   > [Windows Defender 應用程式防護]  。
3. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立 Windows Defender 應用程式防護原則]  。
4. 藉由使用部落格文章作為參考，您可以瀏覽並設定可用的設定以試用此功能。
5. 在此版本中，我們在精靈中增加了新的 [網路定義]  頁面。 在這個頁面上指定公司身分識別，以及定義您的公司網路界限。<br>Windows 10 電腦只會在用戶端上儲存一份網路隔離清單。 在此版本中，您可以建立兩種不同的網路隔離清單 (一個來自 Windows 資訊保護，另一個來自 Windows Defender 應用程式防護)，並將其部署至用戶端。 如果您兩個原則都部署，則這些網路隔離清單必須相符。 如果您部署至相同用戶端的清單不相符，部署將會失敗。
您可以在 [Windows 資訊保護文件](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)中找到有關如何指定網路定義的詳細資訊。

6. 完成操作時，請完成精靈步驟，然後將原則部署到一或多個 Windows 10 裝置。

### <a name="further-reading"></a>延伸閱讀
若要深入了解「Windows Defender 應用程式防護」請參閱[這篇部落格文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此外，若要深入了解「Windows Defender 應用程式防護」獨立模式，請參閱[這篇部落格文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>在從 Configuration Manager 部署 PowerShell 指令碼時新增參數

<!-- 1236459 --->

在上一個 Technical Preview 中，我們引進了新的功能，可讓您[從 Configuration Manager 主控台建立和執行 PowerShell 指令碼](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)。
在此 Technical Preview 中，我們擴展了這項功能。 Configuration Manager 現在可讀取 PowerShell 指令碼，並會在 [建立指令碼精靈] 中顯示任何參數。 您可以在指令碼執行時會使用的精靈中，為參數提供值。 您也可以將參數保留為空白。 如果這樣做，就必須在執行指令碼時提供參數值。
在此 Technical Preview 中，您必須提供指令碼所需的所有參數。 在未來的版本中，我們計畫讓提供指令碼參數變成選擇性。

### <a name="try-it-out"></a>試試看！

1. 遵循[從 Configuration Manager 主控台建立及執行 PowerShell 指令碼](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)的指示。
2. 在 [建立指令碼精靈]  的新 [指令碼參數]  頁面上選擇參數，然後按一下 [編輯]  。
3. 為選取的參數提供參數值，然後按一下 [確定]  。
4. 完成精靈。

指令碼執行時，會使用您所設定的任何參數值。
