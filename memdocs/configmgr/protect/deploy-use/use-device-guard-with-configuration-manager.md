---
title: 如何管理 Windows Defender 應用程式控制
titleSuffix: Configuration Manager
description: 了解如何使用 Configuration Manager 來管理 Windows Defender 應用程式控制。
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f9aff29d2773c4994272317d5fcd486b83cba8d7
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210174"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>使用 Configuration Manager 來管理 Windows Defender 應用程式控制

適用於：  Configuration Manager (最新分支)

## <a name="introduction"></a>簡介
Windows Defender 應用程式控制的設計是為了保護電腦免於惡意程式碼和其他未受信任軟體的攻擊。 它藉由確保只能執行您知道的已核准程式碼，來防止執行惡意程式碼。

Windows Defender 應用程式控制是軟體安全層，可強制允許在電腦上執行的明確軟體清單。 應用程式控制本身並沒有任何硬體或韌體必要條件。 如果電腦在符合本文所述最低 Windows 版本和 SKU 需求的目標集合中，則使用 Configuration Manager 部署的應用程式控制原則會為其啟用原則。 此外，也可以選擇在支援的硬體上透過群組原則來啟用 Configuration Manager 所部署應用程式控制原則的 Hypervisor 型保護。

若要深入了解 Windows Defender 應用程式控制，請閱讀 [Windows Defender 應用程式控制部署指南](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)。

   > [!NOTE]
   > - 從 Windows 10 1709 版 開始，可設定的程式碼完整性原則即稱為「Windows Defender 應用程式控制」。
   > - 從 Configuration Manager 1710 版開始，Device Guard 原則已重新命名為 Windows Defender 應用程式控制原則。

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>搭配 Configuration Manager 來使用 Windows Defender 應用程式控制

您可以使用 Configuration Manager 來部署 Windows Defender 應用程式控制原則。 此原則可讓您設定 Windows Defender 應用程式控制在集合中的電腦上執行時所要使用的模式。 

您可以設定下列其中一種模式：

1. **已啟用強制** - 僅允許執行信任的可執行檔。
2. **僅稽核** - 允許執行所有可執行檔，但將執行的未受信任可執行檔記錄到本機用戶端事件記錄檔。

> [!Tip]  
> 這項功能最初是以[發行前版本功能](../../core/servers/manage/pre-release-features.md)的形式引入 1702 版。 從 1906 版開始，它不再是發行前版本功能。  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>部署 Windows Defender 應用程式控制原則時，可以執行哪些功能？

Windows Defender 應用程式控制可讓您嚴格控制可在您管理的電腦上執行的項目。 對於高安全性部門中的電腦而言，絕對禁止執行不必要的軟體，因此這項功能相當實用。

當您部署原則時，通常可以執行下列可執行檔：

- Windows 作業系統元件
- 硬體開發人員中心驅動程式 (具有 Windows 硬體品質實驗室簽章)
- Windows 市集應用程式
- Configuration Manager 用戶端 
- 所有透過 Configuration Manager 部署的軟體 (電腦在處理 Windows Defender 應用程式控制原則之後所安裝的軟體)。 
- 來自下列項目的 Windows 元件更新：
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager
    - (選擇性) 由 Microsoft Intelligent Security Graph (ISG) 判斷為信譽良好的軟體。 ISG 包括 Windows Defender SmartScreen 和其他 Microsoft 服務。 裝置必須執行 Windows Defender SmartScreen 和 Windows 10 1709 版或更新版本，才能讓該軟體受到信任。

>[!IMPORTANT]
>這些項目不包括「未內建」  於 Windows 的任何軟體，這些軟體不論是透過先前所述之任何更新機制或從網際網路安裝，都會自動從網際網路或第三方軟體更新進行更新。 只有透過 Configuration Manager 用戶端部署的軟體變更才可以執行。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

設定或部署 Windows Defender 應用程式控制原則之前，請閱讀下列資訊：

- Windows Defender 應用程式控制管理是 Configuration Manager 的發行前版本功能，而且可能隨時變更。
- 若要藉由 Configuration Manager 來使用 Windows Defender 應用程式控制，您所管理的電腦必須執行 Windows 10 企業版 1703 或更新版本。
- 一旦用戶端電腦上成功處理原則，Configuration Manager 便會設定為該用戶端上的受控安裝程式。 透過受控安裝程式部署的軟體，在原則處理之後便會自動受到信任。 在 Windows Defender 應用程式控制原則處理之前由 Configuration Manager 安裝的軟體，則不會自動受到信任。
- 可在部署期間設定的應用程式控制原則預設合規性評估排程為每天進行。 如果在原則處理中發現問題，將相容性評估排程設定得更短 (例如每小時) 可能會有幫助。 此排程規定發生錯誤時，用戶端重新嘗試處理 Windows Defender 應用程式控制原則的頻率。
- 不論選取的強制模式為何，部署 Windows Defender 應用程式控制原則時，用戶端電腦無法執行副檔名為 .hta 的 HTML 應用程式。

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>如何建立 Windows Defender 應用程式控制原則
1. 在 Configuration Manager 主控台中，按一下 [資產與合規性]  。
2. 在 [資產與合規性]  工作區中，展開 [Endpoint Protection]  ，然後按一下 [Windows Defender 應用程式控制]  。
3. 在 [常用]  索引標籤的 [建立]  群組中，按一下 [建立應用程式控制原則]  。
4. 在 [建立應用程式控制原則精靈]  的 [一般]  頁面中，指定下列設定：
    - **名稱** - 輸入此 Windows Defender 應用程式控制原則的唯一名稱。 
    - **描述** - (選擇性) 輸入可協助您在 Configuration Manager 主控台中識別此原則的原則描述。
    - **強制重新啟動裝置，讓此原則能夠針對所有程序強制執行**：在用戶端電腦上處理原則之後，系統會根據 [電腦重新啟動]  的 [用戶端設定]  ，在該用戶端上排程重新啟動。
        - 執行 Windows 10 1703 版或更舊版本的裝置會一律自動重新啟動。
        - 從 Windows 10 1709 版開始，目前在裝置上執行的應用程式將不會套用新的應用程式控制原則，直到重新啟動才會套用。 不過，在原則套用之後啟動的應用程式將會採用新的應用程式控制原則。 
    - **強制模式** - 針對用戶端電腦上的 Windows Defender 應用程式控制選擇下列其中一個強制方法。
        - **已啟用強制** - 僅允許執行信任的可執行檔。
        - **僅稽核** - 允許執行所有可執行檔，但將執行的未受信任可執行檔記錄到本機用戶端事件記錄檔。
5. 在 [建立應用程式控制精靈]  的 [包含]  索引標籤上，選擇您是否要**授權受 Intelligent Security Graph 信任的軟體**。
6. 如果您要對電腦上的特定檔案或資料夾新增信任，請按一下 [新增]  。 在 [新增信任的檔案或資料夾]  對話方塊中，您可以指定要信任的本機檔案或資料夾路徑。 您也可以指定您具有連線權限的遠端裝置上檔案或資料夾路徑。 在 Windows Defender 應用程式控制原則中，新增對特定檔案或資料夾的信任時，您可以：
    - 克服與受管理安裝程式相關的問題
    - 信任無法以 Configuration Manager 部署的商務營運應用程式
    - 信任作業系統部署映像中所包含的應用程式。 
8. 按一下 [下一步]  以完成精靈。

>[!IMPORTANT]
>只有在執行 Configuration Manager 用戶端 1706 版或更新版本的電腦上才支援包含信任的檔案或資料夾。 如果 Windows Defender 應用程式控制原則中含有任何包含規則，但該原則被部署到執行舊版 Configuration Manager 用戶端的用戶端電腦上，則無法套用這個原則。 升級這些舊版用戶端將能解決此問題。 不包含任何包含原則的原則可能仍能在舊版 Configuration Manager c用戶端上套用。

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>如何部署 Windows Defender 應用程式控制原則
1. 在 Configuration Manager 主控台中，按一下 [資產與合規性]  。
2. 在 [資產與合規性]  工作區中，展開 [Endpoint Protection]  ，然後按一下 [Windows Defender 應用程式控制]  。
3. 從原則清單中選取您要部署的原則，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署應用程式控制原則]  。
4. 在 [部署應用程式控制原則]  對話方塊中，選取想要部署原則的目標集合。 然後，設定用戶端評估原則的排程。 最後，選取用戶端是否可以在任何已設定的維護期間以外評估原則。
5. 完成後，請按一下 [確定]  部署原則。 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>如何監視 Windows Defender 應用程式控制原則

您可以使用[監視相容性設定](../../compliance/deploy-use/monitor-compliance-settings.md)一文中的資訊，協助監視部署的原則是否已正確套用至所有電腦。

若要監視 Windows Defender 應用程式控制原則的處理狀況，請查看用戶端電腦的下列記錄檔：

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

若要確認特定軟體正被封鎖或稽核，請參閱下列本機用戶端事件記錄檔：

1. 如需封鎖及稽核可執行檔，請使用 [應用程式及服務記錄檔]   > [Microsoft]   > [Windows]   > [程式碼完整性]   > [操作]  。
2. 如需封鎖及稽核 Windows 安裝程式和指令碼檔案，請使用 [應用程式及服務記錄檔]   > [Microsoft]   > [Windows]   > [AppLocker]   > [MSI and Script]\(MSI 和指令碼)  。

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Windows Defender 應用程式控制的安全性和隱私權資訊

- 使用這個發行前版本時，請不要在生產環境中使用「僅限稽核」  強制模式，來部署 Windows Defender 應用程式控制原則。 此模式只是為了協助您測試實驗室設定中的功能。
- 以 [僅限稽核]  或 [強制啟用]  模式部署原則但尚未重新啟動以強制執行原則的裝置，容易被安裝不受信任的軟體。
在此情況下，可能會繼續允許執行軟體，即使裝置重新啟動或收到 [已啟用強制]  模式中的原則也一樣。
- 若要確保 Windows Defender 應用程式控制原則是有效的，請在實驗室環境中準備裝置。 接著，部署 [強制啟用]  原則。最後，在重新啟動裝置之後，再將裝置提供給使用者。
- 請勿部署 [已啟用強制]  原則，然後在稍後將 [僅稽核]  原則部署到相同的裝置。 此設定可能會導致允許執行不受信任的軟體。
- 當您在用戶端電腦上使用 Configuration Manager 來啟用 Windows Defender 應用程式控制時，原則並無法防止具有本機系統管理員權限的使用者規避應用程式控制原則或執行未受信任的軟體。 
- 針對具有本機系統管理員權限的使用者，若要防止其停用應用程式控制，唯一的方式就是部署已簽署的二進位原則。 此部署可以透過群組原則進行，但目前 Configuration Manager 中不支援。
- 將 Configuration Manager 設定為用戶端電腦上受管理的安裝程式會使用 AppLocker 原則。 AppLocker 只能用來識別受控安裝程式，以及 Windows Defender 應用程式控制的所有強制執行項目。 

## <a name="next-steps"></a>後續步驟

 [管理反惡意程式碼原則和防火牆設定](endpoint-antimalware-firewall.md)



