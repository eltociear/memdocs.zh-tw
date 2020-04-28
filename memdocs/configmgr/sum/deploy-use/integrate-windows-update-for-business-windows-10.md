---
title: 整合商務用 Windows Update
titleSuffix: Configuration Manager
description: 使用商務用 Windows Update (WUfB)，讓連線到 Windows Update 服務裝置的 Windows 10 保持在最新狀態。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8bfd535c93cb9f1dcfc42705f3cce61874dfe226
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709316"
---
# <a name="integrate-with-windows-update-for-business"></a>與商務用 Windows Update 整合

適用於：  Configuration Manager (最新分支)

「商務用 Windows Update」(WUfB) 可讓您組織中的 Windows 10 裝置在直接連線到 Windows Update (WU) 服務時，永遠掌握最新的安全性防禦措施及 Windows 功能。 Configuration Manager 能夠區分使用 WUfB 與 WSUS 來取得軟體更新的 Windows 10 電腦。  

> [!WARNING]
> 如果您為您的裝置使用共同管理，且將 [Windows Update 原則](../../comanage/workloads.md#windows-update-policies)移動到 Intune，則您的裝置會[從 Intune 取得其商務用 Windows Update 原則](https://docs.microsoft.com/intune/windows-update-for-business-configure)。
> - 如果 Configuration Manager 用戶端仍安裝在共同管理裝置上，則「累積更新」和「功能更新」的設定是由 Intune 管理。 不過，如果協力廠商修補在[**用戶端設定**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)中是啟用的，它仍會由 Configuration Manager 管理。  

 將 Configuration Manager 用戶端設定為從 WU (包括 WUfB 或 Windows 測試人員) 接收更新時，某些 Configuration Manager 功能便無法再使用：  

- Windows Update 相容性報告：  
  - Configuration Manager 不會察覺發佈到 WU 的更新。 設定為從 WU 接收更新的 Configuration Manager 用戶端會將 Configuration Manager 主控台中的更新顯示為 [不明]  。  

  - 針對整體合規性狀態進行疑難排解相當困難，因為**不明**狀態以往僅適用於尚未從 WSUS 回報掃描狀態的用戶端。 現在則也包含從 WU 接收更新的 Configuration Manager 用戶端。  

  - 定義更新合規性是整體更新合規性報告的一部分，而且也無法如預期般運作。

- 由於遺失的掃描資料，以更新合規性狀態為基礎的 Defender 整體 Endpoint Protection 報告將不會傳回準確的結果。  

- 針對連線到 WUfB 以接收更新的用戶端，Configuration Manager 將無法向其部署 Microsoft 更新 (例如 Office、IE 與 Visual Studio)。  

- 針對連線到 WUfB 以接收更新的用戶端，Configuration Manager 仍然可以向其部署發行至 WSUS 且透過 Configuration Manager 管理的協力廠商更新。 如果您不想要在連線到 WUfB 的用戶端上安裝任何協力廠商更新，請停用名為[在用戶端上啟用軟體更新](../../core/clients/deploy/about-client-settings.md#software-updates)的用戶端設定。

- 使用軟體更新基礎結構的 Configuration Manager 完整用戶端部署，不適用於連線到 WUfB 以接收更新的用戶端。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>識別使用 WUfB 進行 Windows 10 更新的用戶端

請使用下列程序來識別使用 WUfB 取得 Windows 10 更新和升級的用戶端。 接著，將這些用戶端設定為停止使用 WSUS 取得更新，並部署用戶端代理程式設定，停用這些用戶端的軟體更新工作流程。  

### <a name="prerequisites-for-wufb"></a>WUfB 的必要條件

- 執行 Windows 10 Desktop Pro 或 Windows 10 Enterprise Edition 1511 版或更新版本的用戶端

- [商務用 Windows Update](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) 已部署，且用戶端使用 WUfB 取得 Windows 10 更新及升級。  

### <a name="to-identify-clients-that-use-wufb"></a>識別使用 WUfB 的用戶端  

1. 請確定 Windows Update 代理程式未掃描 WSUS (如果先前已啟用)。 您可以使用下列登錄機碼，指出電腦是否會對 WSUS 或 Windows Update 進行掃描。 如果登錄機碼不存在，就不會掃描 WSUS。
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. 在 Configuration Manager [資源總管] 的 [Windows Update]  節點下，有一個新屬性 **UseWUServer**。
1. 根據透過 WUfB 連線之所有電腦的 **UseWUServer** 屬性，建立要更新和升級的集合。 您可以根據類似以下的查詢來建立集合：  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. 建立用戶端代理程式設定以停用軟體更新工作流程。 將設定部署至直接連線到 WUfB 的電腦集合。
1. 透過 WUfB 管理的電腦會在相容性狀態中顯示 [不明]  ，而且不會計入整體相容性百分比的一部分。  

## <a name="configure-windows-update-for-business-deferral-policies"></a>設定 Windows Update for Business 延遲原則
<!-- 1290890 -->
從 Configuration Manager 1706 版開始，您可以為由 Windows Update for Business 直接管理的 Windows 10 裝置，設定 Windows 10「功能更新」或「品質更新」的延遲原則。 您可以在 [軟體程式庫]   > [Windows 10 服務]  底下的新 [Windows Update for Business 原則]  節點中管理延遲原則。

> [!NOTE]
> 從 Configuration Manager 1802 版開始，您可以為「Windows 測試人員」設定延遲原則。 <!--507201-->  
如需有關 Windows 測試人員計畫的詳細資訊，請參閱[開始使用商務用 Windows 測試人員計畫](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business) \(部分機器翻譯\)。

### <a name="prerequisites-for-deferral-policies"></a>延遲原則的必要條件

- Windows 10 1703 版或更新版本
- Windows Update for Business 所管理的 Windows 10 裝置必須能夠連線到網際網路

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>建立 Windows Update for Business 延遲原則

1. 在 [軟體程式庫]   > [Windows 10 服務]   > [Windows Update for Business 原則]  中
1. 在 [首頁]  索引標籤的 [建立]  群組中，選取 [建立 Windows Update for Business 原則]  以開啟「建立 Windows Update for Business 原則精靈」。
1. 在 [一般]  頁面上，提供原則的名稱和描述。
1. 在 [延遲原則]  頁面上，設定是要延遲還是暫停「功能更新」。 「功能更新」通常是 Windows 的新功能。 在設定 [分支整備層級]  設定之後，您可以接著定義在 Microsoft 提供「功能更新」之後，是否要延遲接收「功能更新」，以及要延遲多久。
    - **分支整備層級**：設定裝置將接收 Windows 更新的分支。 選擇 [半年通道 (已設定目標)]、[半年通道] 或 [Windows 測試人員組建]。

        > [!NOTE]
        > 將**半年通道 (已設定目標)** 的原則部署到 Windows 10 *1903 版或更新版本*。 將**半年通道**的原則部署到 Windows 10 *1809 版或更早版本*。
        >
        > 如果您將**半年通道**的原則部署到 Windows 10 1903 版或更新版本，部署將會失敗，並出現錯誤 **0x8004100c**。<!-- 5593139 -->

    - **延遲期 (天)** ：指定功能更新要延期的天數。 您可以將接收這些功能更新的時間自其發行日起最多延遲 365 天。
    - **暫停功能更新開始**：選取是否要讓裝置在自暫停更新日算起最長可達 35 天內，暫停接收「功能更新」。 在過了天數上限之後，暫停功能將自動失效，裝置將會掃描 Windows Update 是否有適用的更新。 進行此掃描之後，您可以再次暫停更新。 您可以取消選取此核取方塊來取消暫停「功能更新」。
1. 選擇是要延遲還是暫停「功能更新」。 「品質更新」通常是對現有 Windows 功能的修正和改進，並且通常是在每個月的第一個星期二發佈，但是可由 Microsoft 隨時發行。 您可以定義在「品質更新」可供使用之後，是否要延遲接收「品質更新」，以及要延遲多久。
    - **延遲期 (天)** ：指定品質更新要延期的天數。 您可以將接收這些品質更新的時間自其發行日起最多延遲 30 天。
    - **暫停品質更新開始**：選取是否要讓裝置在自暫停更新日算起最長可達 35 天內，暫停接收「品質更新」。 在過了天數上限之後，暫停功能將自動失效，裝置將會掃描 Windows Update 是否有適用的更新。 進行此掃描之後，您可以再次暫停更新。 您可以取消選取此核取方塊來取消暫停「品質更新」。
1. 選取 [安裝來自其他 Microsoft 產品的更新]  ，以啟用讓延遲設定適用於 Microsoft Update 及 Windows Update 的群組原則設定。
1. 選取 [包含 Windows Update 的驅動程式]  以自動從 Windows Update 更新驅動程式。 如果您取消選取此設定，系統就不會從 Windows Update 下載驅動程式更新。
1. 完成精靈步驟以建立新的延遲原則。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>部署 Windows Update for Business 延遲原則

1. 在 [軟體程式庫]   > [Windows 10 服務]   > [Windows Update for Business 原則]  中
1. 在 [首頁]  索引標籤的 [部署]  群組中，選取 [部署 Windows Update for Business 原則]  。
1. 進行以下設定：
    - **要部署的組態原則**：選取您要部署的商務用 Windows Updat 原則。
    - **集合**：按一下 [瀏覽]  以選取您要部署原則的集合。
    - **允許在維護期間以外補救**：如果已針對您部署原則的集合設定維護期間，啟用此選項即可讓原則設定在維護期間之外補救值。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。
    - **排程**：指定在用戶端電腦上評估已部署之原則時所依據的合規性評估排程。 此排程可以是簡易或自訂排程。
1. 完成精靈步驟以部署原則。
