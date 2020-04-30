---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: 了解套件轉換管理員如何在 Configuration Manager 中將套件轉換為應用程式。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689006"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

適用於：  Configuration Manager (最新分支)

<!--1357861-->

從 1806 版開始，套件轉換管理員可協助您將 Configuration Manager 的舊版套件轉換為應用程式。 應用程式具備相依性、需求規則、偵測方法及使用者裝置親和性等其他優點。

> [!Tip]  
> 這項功能最初是以[發行前版本功能](../../core/servers/manage/pre-release-features.md)的形式引進 1806 版。 從 1810 版開始，這項功能就不再是發行前版本功能。  


Configuration Manager 應用程式包含您部署到用戶端裝置的檔案和程式。 不過，不同於舊版套件和程式，應用程式會提供以使用者為中心的其他功能。 例如，應用程式可以包含在本機安裝軟體封裝、虛擬應用程式封裝或適用於行動裝置之應用程式版本的部署類型。

如需詳細資訊，請參閱下列文章： 
- [應用程式管理簡介](../understand/introduction-to-application-management.md)  
- [套件和程式](../deploy-use/packages-and-programs.md)  

> [!Important]  
> 如果您先前已安裝舊版的 Package Conversion Manager，請先解除安裝後再升級您的網站。 這個整合版本不需要安裝，但可能會與現有的版本發生衝突。  

套件轉換管理員的這個整合版本適用於 Configuration Manager 目前分支站台中的套件。 它不是獨立的工具。 如果您在較舊版本的 Configuration Manager 中具有套件和程式，請先將套件移轉至您目前的分支站台。 如需詳細資訊，請參閱[在階層間移轉資料](../../core/migration/migrate-data-between-hierarchies.md)。

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager 1902 版包含下列改善：
- 根據預設，已排程的套件分析會每 7 天執行一次
- 用來分析及轉換套件的 PowerShell Cmdlet
- 一般 Bug 修正和改善



## <a name="planning"></a>規劃

開始將套件轉換為應用程式之前，請先開發方案。 下列程序為一個範例方案：

- [定義詳細的套件轉換方案](#bkmk_define)  

- [選取並準備套件以進行轉換](#bkmk_prepare)  

- [選取測試套件](#bkmk_test)  

- [分析、調查及轉換套件](#bkmk_analyze)  

- [測試及部署應用程式](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a> 定義詳細的套件轉換方案

本節說明兩個範例套件轉換方案：  

- [具大量資源的測試環境](#bkmk_define-high)：您的測試環境具備完全複製您生產環境的資源、權限及架構。  

- [具有限資源的測試環境](#bkmk_define-limited)：您沒有完全複製您生產環境的測試環境。  

視需要針對您環境特有的其他問題來調整這些方案。

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a> 適用於具大量資源之測試環境的範例方案

您的測試環境具有類似您生產環境的資源、權限及架構。 使用測試環境，有效率地分析和轉換您的所有套件，然後測試您的所有 Configuration Manager 應用程式。 完成該工作之後，將它傳輸到生產環境。 

您的套件轉換方案可能類似下列步驟：  

1.  選取要轉換的套件。  

2.  將要轉換的套件移轉到測試環境。  

3.  準備封裝以便轉換。  

4.  選取測試封裝。  

5.  分析、調查及轉換測試封裝。  

6.  測試轉換後的應用程式。  

7.  分析並轉換其餘 (非測試) 封裝。  

8.  從測試環境匯出應用程式。 將它們匯入到生產環境。  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a> 適用於有限資源測試環境的範例方案

您的測試環境並未具備類似您生產環境的資源、權限及架構。 您無法分析、測試及轉換所有套件。 在此案例中，只能分析、調查、轉換及測試您的測試套件。 然後將剩餘的套件移轉至生產環境來進行分析和轉換。 

您的套件轉換方案可能類似下列步驟：

1.  選取要轉換的套件。  

2.  選取測試封裝。  

3.  移轉測試封裝到您的測試環境。  

4.  準備測試封裝以便轉換。  

5.  分析、調查及轉換測試封裝。  

6.  測試轉換後的應用程式。  

7.  從測試環境匯出測試應用程式。 接著將它們匯入到生產環境。  

8.  將其餘封裝移轉到生產環境，然後準備轉換。  

9.  在生產環境中分析、調查及轉換其餘封裝。  

10. 將其餘應用程式發行至生產環境。  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a> 選取並準備套件以進行轉換

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a> 選取要轉換的套件

並非所有封裝都適合用來轉換成應用程式。 開始轉換套件之前，先找出將不會轉換的套件。 

最適合轉換成應用程式的封裝類型為包含與使用者互動之軟體的封裝，例如︰  

- Windows Installer 檔案 (.msi 和 .msu)  

- Microsoft Application Virtualization (App-V) 程式  

- Windows 可執行檔 (.exe)  

最適合做為封裝保存，且並不會轉換成應用程式的封裝類型包括：

- 系統維護工具。 例如，指令碼或備份公用程式。  

- 不支援的軟體套件。

> [!Tip]  
> 找出不適合轉換為應用程式的套件之後，將它們移至 Configuration Manager 主控台中的不同資料夾。 在 Configuration Manager 主控台中建立套件資料夾：  
> - 以滑鼠右鍵按一下 [套件]  節點。  
> - 選取 [資料夾]  ，然後選取 [建立資料夾]  。  
> - 輸入資料夾名稱，例如 `Not Converted`。  
> - 按一下 [確定]  。  

#### <a name="prepare-the-packages-for-conversion"></a>準備封裝以便轉換

對於您想要轉換的每一個封裝，請確定它們符合下列條件：  

- 來源檔案位置是完整的 UNC 路徑，例如 `\\Server\Share\File`。  

- Windows Installer 檔案只會使用一個唯一的產品代碼。  


### <a name="select-test-packages"></a><a name="bkmk_test"></a> 選取測試套件

可能的話，您的測試套件群組應該包含符合下列準則的套件：  

- 至少一個整備狀態為 **自動**的測試封裝。  

- 至少一個整備狀態為 **手動**的測試封裝。  

在理想的情況下，您的測試套件應該是核心套件，例如：  

- 您熟悉的封裝。  

- 對您的組織最重要的套件。  

- 您最易於測試的封裝。  

識別適用於測試的套件。 接著在 Configuration Manager 主控台中，將它們移至不同的資料夾。


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a> 分析、調查及轉換套件

#### <a name="analyze-packages"></a>分析套件

若要分析個別套件或小型群組，請使用已在 Configuration Manager 主控台中整合的套件轉換管理員。 如需詳細資訊，請參閱[如何分析和轉換套件](how-to-analyze-and-convert.md)。  

> [!NOTE]  
> 查看 [監視]  工作區中的 [套件轉換狀態]  節點。 其會顯示有關分析與轉換程序的摘要資訊。  

#### <a name="investigate-analysis-results"></a>調查分析結果

在分析測試封裝之後，請調查整備狀態為 **手動** 或 **錯誤**的封裝。 判斷它們為何有該狀態的原因。 一些整備狀態為 **手動** 或 **錯誤** 的常見原因包括：

- 此套件不包含在應用程式部署類型中建立偵測方法所需的資訊。  

- 此套件不包含將集合轉換為全域條件和需求所需的資訊。  

- 此封裝包含多個程式。  

- 此套件相依於尚未轉換為應用程式的另一個套件。  

如需詳細資訊，請使用下列資源：  

- 檢閱[套件轉換管理員錯誤訊息的技術參考](error-messages.md)中的錯誤訊息和修正  

- 檢閱記錄檔 **PCMTrace.log**  

- [針對套件轉換管理員進行疑難排解](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>轉換套件

如需如何轉換套件的詳細資訊，請參閱[如何分析和轉換套件](how-to-analyze-and-convert.md)。

> [!NOTE]  
> 查看 [監視]  工作區中的 [套件轉換狀態]  節點。 其會顯示有關分析和轉換程序的摘要資訊。  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a> 測試及部署應用程式

請根據您的封裝轉換詳細計畫，在您的測試環境或生產環境測試此應用程式。



## <a name="recommendations"></a>建議

- 使用 [監視]  工作區中的 [套件轉換狀態]  節點。 其會顯示有關分析和轉換程序的摘要資訊。  

- 調查套件中的程式 (稱為包裝函式)。 使用套件轉換管理員外掛程式，將其函式轉換為對等的 Configuration Manager 功能。  

- 請務必徹底測試每個轉換後的應用程式，再部署到生產環境中。  



## <a name="next-steps"></a>後續步驟

[如何分析和轉換套件](how-to-analyze-and-convert.md)
