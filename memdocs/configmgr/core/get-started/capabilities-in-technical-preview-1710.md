---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1710 版中可用的功能。
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3dd4c3f22a0f2c24153e6d26be2e3098511c5dc4
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905314"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Configuration Manager Technical Preview 1710 中的功能

適用於：  Configuration Manager (Technical Preview 分支)

此文章介紹 Configuration Manager 技術預覽 1710 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 的已知問題：**
- **對 Windows 10 1709 版 (也稱為 Fall Creators Update) 的支援**。  從這個 Windows 版本開始，Windows 媒體會包含數個版本。 設定工作順序以使用作業系統升級套件或作業系統映像時，請務必選取[支援由 Configuration Manager 使用的版本](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)。
- **當您有以被動模式執行的站台伺服器時，更新到新的預覽版本會失敗**。 當您執行具有[以被動模式執行的主要站台伺服器](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)的預覽版本時，必須先將被動模式站台伺服器解除安裝，才能順利將預覽站台更新到這個新的預覽版本。 當您的站台完成更新之後，就可以重新安裝被動模式站台伺服器。

  將被動模式站台伺服器解除安裝：
  1. 在主控台中，移至 [系統管理]   > [概觀]   > [站台設定]   > [伺服器和站台系統角色]  ，然後選取被動模式站台伺服器。
  2. 在 [站台系統角色]  頁面上，以滑鼠右鍵按一下 [站台伺服器]  角色，然後選擇 [移除角色]  。
  3. 以滑鼠右鍵按一下被動模式站台伺服器，然後選擇 [刪除]  。
  4. 站台伺服器解除安裝之後，請在主動主要站台伺服器上重新啟動服務 **CONFIGURATION_MANAGER_UPDATE**。

**以下是您可以使用此版本試用的新功能。**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>從 Configuration Manager 部署 PowerShell 指令碼的改善
在此版本中，您部署的 PowerShell 指令碼現在支援使用下列改善： 
- **安全性範圍**：  現在，指令碼會使用安全性範圍來控制指令碼的撰寫和執行。 您可藉由指派代表使用者群組的標籤來完成上述作業。 如需使用安全性範圍的詳細資訊，請參閱[為 Configuration Manager 設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。
- **即時監視**： 現在，當您監視指令碼的執行狀態時，是在指令碼的即時執行狀態下進行監視。
- **參數驗證**： 指令碼中的每個參數都有 [Script Parameter Properties] (指令碼參數屬性)  對話方塊，可讓您新增該參數的驗證。 新增驗證之後，如果輸入的參數值與驗證不符，應該會收到錯誤。

PowerShell 指令碼部署最初是在 Technical Preview 的 [Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console) 中引入。 其他改善則陸續在 [Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) 和 [Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) 中提供。


### <a name="try-it-out"></a>試試看！

若要嘗試使用「執行指令碼」功能，請參閱[建立和執行指令碼](../../apps/deploy-use/create-deploy-scripts.md)。



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>限制 Windows 10 增強資料只傳送與 Windows Analytics 裝置健全狀況相關的資料
<!-- 1356148 -->

在此版本中，您可以將 Windows 10 診斷資料收集層級設定為 [增強 (受限)]  。 在 Windows 10 1709 版或更新版本中，此設定讓您能夠獲取可對環境中之裝置採取動作的深入解析，而不需讓裝置回報 [增強式]  層級中的所有資料。

[增強 (受限)] 層級包含基本層級的計量，以及 [增強]  層級所收集資料中與 Windows Analytics 相關的資料子集。


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>軟體中心已不會再使大於 250x250 的圖示出現失真  
<!-- 1356194 -->

在此版本中，軟體中心已不會再使大於 250x250 的圖示出現失真。 軟體中心先前會使這些圖示變得模糊不清。 您現在可以設定像素尺寸最多為 512x512 的圖示，該圖示於顯示時將不會出現失真。

### <a name="try-it-out"></a>試試看！
在軟體中心中為應用程式新增圖示。 若要嘗試，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>從軟體中心檢查共同管理之裝置的合規性
<!-- 1356374 -->
在此版本中，使用者可以使用軟體中心檢查其共同管理之 Windows 10 裝置的合規性，就算條件式存取是由 Intune 所管理也一樣。 如需詳細資訊，請參閱 [Windows 10 裝置的共同管理](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)。


## <a name="support-for-exploit-guard"></a>針對惡意探索防護的支援
此版本新增了針對 Windows Defender 惡意探索防護的支援。 您可以設定並部署能管理惡意探索防護所有四個元件的原則。 這些元件包括：
-   攻擊表面縮減
-   受控資料夾存取權
-   惡意探索保護
-   網路保護

適用於惡意探索防護原則部署的合規性資料，可從 Configuration Manager 主控台內取得。

如需惡意探索防護及特定元件和規則的詳細資訊，請參閱 Windows 文件庫中的 [Windows Defender 惡意探索防護](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard)。

### <a name="prerequisites"></a>先決條件
受管理的裝置必須執行 Windows 10 1709 Fall Creators Update 或更新版本，並滿足下列需求 (根據所設定的元件及規則而定)：

|惡意探索防護元件 |其他必要條件|
|------------------------|------------------------|
| 攻擊表面縮減  | 裝置必須啟用 [Windows Defender AV 即時保護]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)。  |
| 受控資料夾存取權  | 裝置必須啟用 [Windows Defender AV 即時保護]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)。   |
| 惡意探索保護  | 無  |
| 網路保護  |  裝置必須啟用 [Windows Defender AV 即時保護]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)。  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>建立惡意探索防護原則  <!--1355468 -->
1. 在 Configuration Manager 主控台中，移至 [資產與合規性]   > [Endpoint Protection]  ，然後按一下 [Windows Defender 惡意探索防護]  。
2. 在 [首頁]  索引標籤上的 [建立]  群組中，按一下 [建立惡意探索原則]  。
3. 在 [建立設定項目精靈]  的 [一般]  頁面上，指定設定項目的名稱和選擇性描述。
4. 接下來，選取您想要以此原則管理的惡意探索防護元件。 針對每個選取的元件，您可以進一步設定其他詳細資料。
   - **受攻擊面縮小：** 設定您想要封鎖或稽核的 Office 威脅、指令碼威脅，以及電子郵件威脅。 您也可以將特定的檔案或資料夾排除於此規則之外。
   - **受控資料夾存取權：** 設定封鎖或稽核，然後新增可以略過此原則的應用程式。  您也可以指定其他預設沒有受到保護的資料夾。
   - **惡意探索保護：** 指定 XML 檔案，此檔案包含用於減輕對系統處理序及應用程式之惡意探索的設定。 您可以從 Windows 10 裝置上的 Windows Defender 資訊安全中心應用程式中匯出這些設定。
   - **網路保護：** 設定網路保護以對可疑網域的存取進行封鎖或稽核。
5. 完成精靈以建立原則，您後續可以將該原則部署至裝置。

### <a name="deploy-an-exploit-guard-policy"></a>部署惡意探索防護原則     
在您建立惡意探索防護原則之後，請使用 [部署惡意探索防護原則] 精靈來部署那些原則。 若要這麼做，請開啟 Configuration Manager 主控台，並移至 [資產與合規性]   > [Endpoint Protection]  ，然後按一下 [部署惡意探索防護原則]  。

## <a name="limited-support-for-cng-certificates"></a>針對 CNG 憑證的有限支援
<!-- 1356191 -->
從此版本開始，您現在可以針對下列案例使用[加密 API：新一代 (CNG) API](https://docs.microsoft.com/windows/win32/seccng/cng-features) 憑證範本：

- 搭配 HTTPS 管理點進行用戶端註冊及通訊。   
- 搭配 HTTPS 發佈點進行軟體發佈及應用程式部署。   
- 作業系統部署。  
- 用戶端傳訊 SDK (據最新更新) 及 ISV Proxy。   
- 雲端管理閘道設定。  

若要使用 CNG 憑證，您的憑證授權單位 (CA) 必須為目標電腦提供 CNG 憑證範本。  範本詳細資料會因案例而有所不同，不過下列屬性皆為必要項目：

- [相容性]  索引標籤

    - [憑證授權單位]  必須為 Windows Server 2008 或更新版本。 (建議使用 Windows Server 2012)。

    - [憑證接收者]  必須為 Windows Vista/Server 2008 或更新版本。 (建議使用 Windows 8/Windows Server 2012)。

- [密碼編譯]  索引標籤

    - [提供者類別]  必須為 [金鑰儲存提供者]  。  (必要)

若要獲得最佳結果，建議根據 Active Directory 資訊建置 [主體名稱]。  使用 [DNS 名稱] 作為 [主體名稱格式]  ，並將 DNS 名稱包含在次要主體名稱中。  否則，您必須在裝置註冊至憑證設定檔時提供此資訊。


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>已改進對於擱置電腦重新啟動的描述   <!--1356283 -->
在 [Technical Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console) 中，我們已新增從 Configuration Manager 主控台內識別正在等候重新啟動之裝置的功能。

從此 Technical Preview 開始，主控台會顯示額外的詳細資料，以提供要求重新啟動之處理序或動作的相關資訊。

## <a name="device-guard-policy-changes----1355092---"></a>Device Guard 原則變更 <!-- 1355092 -->
從 1710 Technical Preview 組建開始，已做出下列與 Device Guard 原則相關的三個變更：

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Device Guard 原則已重新命名為 Windows Defender 應用程式控制原則
Device Guard 原則已重新命名為 Windows Defender 應用程式控制原則。 因此，像 [建立 Device Guard 原則]  精靈這樣的名稱，現在已名為 [建立 Windows Defender 應用程式控制原則]  精靈。

### <a name="restart-is-not-required-to-apply-policies"></a>無需重新啟動以套用原則
自 Windows 1709 版的 Fall Creators Update 起，使用新版 Windows 的裝置無須重新啟動，就會套用 Windows Defender 應用程式控制原則。

重新啟動是預設值。

#### <a name="try-it-out"></a>試試看！  

如果您想要關閉重新啟動，請遵循下列步驟：

1.  開啟 [建立 Windows Defender 應用程式控制原則]  精靈。
2.  在 [一般]  頁面上，清除 [強制重新啟動裝置，讓此原則能夠針對所有程序強制執行]  核取方塊。
3.  持續按一下 [下一步]  ，直到精靈完成為止。

針對舊版的 Windows，系統仍會強制執行自動重新啟動。

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>自動執行 Intelligent Security Graph 所信任的軟體

系統管理員現在可以允許鎖定的裝置執行由 Microsoft Intelligent Security Graph (ISG) 判斷為信譽良好的受信任軟體。 ISG 是由 Windows Defender SmartScreen 和其他 Microsoft 服務所組成。

裝置必須執行 Windows Defender SmartScreen，才能讓系統信任該軟體。

#### <a name="try-it-out"></a>試試看！  

若要讓執行 Windows Defender SmartScreen 的裝置執行受信任的軟體，請遵循下列步驟：

1.  開啟 [建立 Windows Defender 應用程式控制原則]  精靈。
2.  在 [包含]  頁面上，選取 [授權受 Intelligent Security Graph 信任的軟體]  的方塊。
3.  在 [受信任的檔案或資料夾]  方塊中，新增您想要信任的檔案和資料夾。
4.  持續按一下 [下一步]  ，直到精靈完成為止。

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>設定及部署 Windows Defender 應用程式防護原則 <!-- 1351960 -->

[Windows Defender 應用程式防護](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)是一個新的 Windows 功能，可藉由在作業系統其他部分所無法存取的安全隔離容器中開啟未受信任的網站，來協助保護您的使用者。 此技術預覽新增一項支援，可以讓您使用您所設定的 Configuration Manager 合規性設定來設定此功能，並將其部署到集合中。 此功能將隨 Windows 10 Creators Update 64 位元版的預覽版發行。 若要立即測試此功能，您必須使用此更新的預覽版本。

### <a name="before-you-start"></a>在您開始使用 Intune 之前
若要建立及部署「Windows Defender 應用程式防護」原則，必須為您要部署原則的 Windows 10 裝置設定網路隔離原則。 如需詳細資訊，請參閱稍後引用的部落格文章。 此功能只能與最新的「Windows 10 測試人員組建」搭配運作。 若要測試它，您的用戶端必須執行最新的「Windows 10 測試人員組建」。

### <a name="try-it-out"></a>試試看！

若要了解 Windows Defender 應用程式防護的相關基本知識，請參閱[部落格文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) \(英文\)。

建立原則並瀏覽至可用的設定：
1. 在 **Configuration Manager** 主控台中，選擇 [資產與合規性]  。
2. 在 [資產與合規性]  工作區中，選擇 [概觀]   > [Endpoint Protection]   > [Windows Defender 應用程式防護]  。
3. 在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立 Windows Defender 應用程式防護原則]  。
4. 藉由使用部落格文章作為參考，您可以瀏覽並設定可用的設定以試用此功能。
5. 我們在此版中，為精靈新增了 [網路定義] 頁面。 在這裡，請指定公司身分識別，並定義您的公司網路界限。

    > [!NOTE]
    > Windows 10 電腦只會在用戶端上儲存一份網路隔離清單。 在此版本中，您可以建立兩種不同的網路隔離清單 (一個來自 Windows 資訊保護，另一個來自 Windows Defender 應用程式防護)，並將其部署至用戶端。 如果您兩個原則都部署，則這些網路隔離清單必須相符。 若您部署的清單，與同一部用戶端不符，部署將會失敗。

    如需了解如何指定網路定義，請參閱 [Windows 資訊保護文件] - [使用 Windows 資訊保護 (WIP) 保護您的企業資料](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr) (機器翻譯)。

6. 完成操作時，請完成精靈步驟，然後將原則部署到一或多個 Windows 10 裝置。

### <a name="further-reading"></a>延伸閱讀

若要深入了解「Windows Defender 應用程式防護」請參閱[這篇部落格文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此外，若要深入了解「Windows Defender 應用程式防護」獨立模式，請參閱[這篇部落格文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。

## <a name="next-steps"></a>後續步驟
如需安裝或升級 Technical Preview 分支的資訊，請參閱 [Configuration Manager 的 Technical Preview](technical-preview.md)。    
